---
title: Technické informace o nasazení aplikací pro uživatele
titleSuffix: Configuration Manager
description: Řešení potíží s nasazením aplikací pro uživatele technické Reference k Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b44aad1db96b4191b9c9537acea4e64b1d30fde6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710794"
---
# <a name="application-deployment-policy-for-users"></a>Zásady nasazení aplikací pro uživatele

*Platí pro: Configuration Manager (Current Branch)*

Když se aplikace nasadí do uživatelské kolekce, zásada pro nasazení se vytvoří jenom pro požadovaná nasazení. V případě dostupných nasazení se zásada vytvoří, když se uživatel pokusí o instalaci aplikace z centra softwaru. Tento článek vysvětluje, jak postup nasazení vyžaduje i dostupná nasazení.

> [!TIP]
> Všechny informace, které jsou nezbytné pro kontrolu protokolů klienta, lze získat spuštěním dotazu SQL, na který se odkazuje v části [než začnete](app-deployment-technical-reference.md#before-you-begin) .

## <a name="required-deployments"></a>Požadovaná nasazení

Zásady pro požadované nasazení aplikace do kolekce uživatelů jsou zaměřené na všechny uživatele v kolekci, když je vytvořeno nasazení. Zpracovávání na straně klienta pro tato nasazení se podobá požadovanému nasazení kolekce zařízení. Aktivace nasazení probíhá ve stanoveném čase a k vynucení dojde v definovaném konečném termínu. Další informace najdete v tématu [nasazení aplikace do kolekcí zařízení](device-deployment-technical-reference.md).

## <a name="available-deployments"></a>Dostupná nasazení

Aplikace, které jsou nasazeny do uživatelské kolekce jako dostupné, se chovají jinak. Tato změna chování umožňuje správci zpřístupnit aplikace uživatelům, aniž by to způsobilo spory prostředků pro zásady. Když uživatel spustí Centrum softwaru, seznam aplikací, které jsou k dispozici pro uživatele, je dotazován z bodu správy v reálném čase. Tato žádost se provede ve `CMUserService_WindowsAuth` virtuálním adresáři v bodu správy a může se zobrazit v **SCClient_ [UserName]. log** v klientovi.

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

Když bod správy obdrží tuto žádost, dotazuje se seznam aplikací, které uživatel k dispozici, spuštěním `usp_GetApplicationPropertyValuesFiltered` uložené procedury. Tuto aktivitu lze sledovat v **userservice předefinovala smazání. log** v bodu správy.

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

Centrum softwaru obdrží seznam a zobrazí aplikace, které může uživatel nainstalovat. Když uživatel klikne na aplikaci, další informace o aplikaci se dotazují z bodu správy, který zahrnuje provádění uložených procedur, jako je usp_GetApplicationInfo, usp_GetAppModelApplicationSupersedence, usp_GetDeploymentTypeForAnApp atd.

Nasazení se aktivuje, když uživatel vybere aplikaci a klikne na tlačítko **nainstalovat** a vytvoří se úloha agenta DCM pro vyhodnocení aplikace. Pokud se aplikace použije, vytvoří se další úloha agenta DCM, která aplikaci stáhne a vynutila. Tuto aktivitu lze sledovat v **DCMAgent. log** v klientovi.

## <a name="next-steps"></a>Další kroky

- [Principy klientských komponent nasazení aplikace](client-components-technical-reference.md)
