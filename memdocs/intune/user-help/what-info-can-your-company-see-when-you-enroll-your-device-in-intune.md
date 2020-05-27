---
title: Jaké informace vaše společnost uvidí při registraci zařízení?
description: Vysvětluje, co správce IT uvidí a neuvidí na vašem spravovaném zařízení.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: 028a568b9a588697139f97f292c70c50347217f3
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83882082"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>Jaké informace moje organizace uvidí, když zaregistruji své zařízení?

Při registraci zařízení do Microsoft Intune nevidí organizace vaše osobní údaje. Při registraci zařízení dáváte organizaci svolení k zobrazení určitých informací o vašem zařízení, jako je model zařízení a sériové číslo. Tyto informace pomáhají vaší organizaci chránit firemní data v zařízení.

**Údaje, které vaše organizace nikdy neuvidí:**

- Historie volání a procházení webu
- Textové a e-mailové zprávy
- Kontakty
- Kalendář
- Hesla
- Obrázky, včetně těch, které jsou ve fotografických aplikacích nebo mezi obrázky z fotoaparátu
- Soubory

**Údaje, které vaše organizace uvidí vždy:**

- Model zařízení, jako je Google Pixel
- Výrobce zařízení, například Microsoft
- Operační systém a jeho verzi, například iOS 12.0.1
- Inventář aplikací a názvy aplikací, jako je Microsoft Word Na osobních zařízeních může vaše organizace zobrazit jenom inventář spravovaných aplikací. Na zařízeních ve firemním vlastnictví uvidí vaše organizace inventář všech aplikací.
- Vlastník zařízení
- Název zařízení
- Sériové číslo zařízení
- IMEI

 > [!NOTE]
 > U plně spravovaných a vyhrazených zařízení pro Android Enterprise se nebudete moct podívat na všechny inventáře aplikací.
 
 > [!NOTE]
 > Aplikace se považuje za **spravovanou aplikaci** , když je nainstalovaná jedním z následujících způsobů:
 > 1. Uživatel si ho nainstaluje z aplikace Portál společnosti po jeho publikování jako **k dispozici** správcem Intune.
 > 2. Aplikace je publikovaná podle **požadavku** správce Intune a je na zařízení nainstalovaná. 
 >
 > Pokud jste správcem IT nebo pracovníkem podpory ve vaší organizaci a chcete získat další informace o správě aplikací v Intune, přečtěte si téma [porozumění možnostem nespravovaných aplikací, spravovaných aplikací a aplikací mam](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/understanding-the-capabilities-of-unmanaged-apps-managed-apps/ba-p/249164).
    
**Údaje, které vaše organizace může vidět:**

- Telefonní číslo: U zařízení ve firemním vlastnictví může být viditelné celé telefonní číslo. U zařízení v osobním vlastnictví vidí organizace jen poslední čtyři číslice vašeho telefonního čísla. Na stránce **Podrobnosti o zařízení** můžete zobrazit typ vlastnictví každého jednotlivého zařízení.
- Úložné místo v zařízení: Pokud nemůžete nainstalovat požadovanou aplikaci, může organizace zjistit, jestli ve vašem zařízení není nedostatek úložného místa.  
- Umístění: vaše organizace si nikdy nevidí umístění vašeho zařízení, pokud nepotřebujete obnovit ztracené, pod dohledem zařízení s iOS. Další informace o zařízeních pod dohledem najdete v [dokumentaci k Apple iOS](https://go.microsoft.com/fwlink/?linkid=853816) .  
- Podrobnosti inventáře aplikací: Pokud vaše organizace používá ochranu před mobilními hrozbami, bude moct zobrazit podrobnosti o aplikacích, které jsou na vašem zařízení s iOS. Přečtěte si další informace o [ochraně před mobilním hrozbami](set-up-mobile-threat-defense.md). Pokud máte osobní zařízení, může vaše organizace zobrazit jenom inventář spravovaných aplikací. Pokud máte zařízení vlastněné společností, může vaše organizace Zobrazit všechny inventáře aplikací.
- Informace o síti: Některé informace o připojení k síti na zařízeních s Androidem mohou být dostupné podpoře vaší organizace. Pokud vaše organizace například vyžaduje, aby zařízení zůstala v určité budově, identifikuje vaše zařízení síť, ke které je připojené. 
