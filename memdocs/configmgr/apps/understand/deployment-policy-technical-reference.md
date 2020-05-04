---
title: Technické informace o zásadách nasazení aplikací
titleSuffix: Configuration Manager
description: Řešení potíží s technickou referencí k zásadám nasazení aplikací pro Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709786"
---
# <a name="application-deployment-policy"></a>Zásada nasazení aplikace

*Platí pro: Configuration Manager (Current Branch)*

## <a name="policy-creation"></a>Vytvoření zásady

Při nasazení aplikace je vytvořena instance třídy [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md) , která představuje přiřazení aplikace do kolekce. Tuto aktivitu je možné sledovat v **Smsprov. log**.

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

V databázi Configuration Manager jsou tyto informace uloženy v `CI_CIAssignments` tabulce, kde `AssignmentType` 2 představuje nasazení aplikace. Když je přiřazení vytvořeno, komponenta monitorování databáze SMS zjistí změnu v tabulce a upozorní správce replikace objektů na zpracování zásad přiřazení CI (CIA). Součást Správce replikace objektů poté vytvoří zásadu pro přiřazení aplikace v databázi, která je uložena v `Policy` tabulce v databázi, a ID zásad je založena na jedinečném ID aplikace. Tuto aktivitu lze sledovat v **protokolu Objreplmgr. log** odkazem na jedinečné ID přiřazení, které lze získat z dotazu SQL, na který odkazuje oddíl [před zahájením](app-deployment-technical-reference.md#before-you-begin) .

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

Zásadu pro přiřazení aplikace lze zobrazit v databázi pomocí dotazu SQL, který je podobný jako v následujícím příkladu.

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>Cílení zásad

Po vygenerování zásady Tato zásada přiřadí tuto zásadu k prostředkům v kolekci, které cílí na nasazení aplikace. Informace o cílení zásady jsou uložené v `ResPolicyMap` tabulce v databázi. K sledování této aktivity v **protokolu Policypv. log**můžete použít PADBID vrácenou výše uvedeným dotazem. PADBID zaznamenané v protokolu ale nemusí vždycky odpovídat PADBID vrácenému výše uvedeným dotazem, pokud se více zásad zpracovává současně.

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> `ResPolicyMap`tabulka neobsahuje žádné informace o cíle pro aplikace, které jsou nasazeny jako **dostupné** pro kolekce uživatelů. Centrum softwaru dotazuje seznam těchto aplikací z bodu správy a informace o cílení zásad pro tyto aplikace se generují dynamicky, když si uživatel vyžádá aplikaci z centra softwaru.

## <a name="next-steps"></a>Další kroky

- [Nasazení aplikace do kolekcí zařízení](device-deployment-technical-reference.md)
- [Nasazení aplikace do kolekcí uživatelů](user-deployment-technical-reference.md)
