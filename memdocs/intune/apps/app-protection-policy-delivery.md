---
title: Principy doručování a časování zásad ochrany aplikací
titleSuffix: Microsoft Intune
description: Přečtěte si o různých oknech nasazení pro zásady ochrany aplikací, které vám pomohou pochopit, kdy se mají změny zobrazovat na zařízeních koncových uživatelů.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ec111319-7e02-434f-946b-88647726bf1a
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 40d8e62e73e67d7db1978500d77118dfb1257748
ms.sourcegitcommit: 1aeb4a11e89f68e8081d76ab013aef6b291c73c1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/14/2020
ms.locfileid: "88217576"
---
# <a name="understand-app-protection-policy-delivery-timing"></a>Principy časování doručování zásad ochrany aplikací

Přečtěte si o různých oknech nasazení pro zásady ochrany aplikací, které vám pomohou pochopit, kdy se mají změny zobrazovat na zařízeních koncových uživatelů.

## <a name="delivery-timing-summary"></a>Souhrn časování doručení

Doručování zásad ochrany aplikací závisí na stavu licence a registraci služby Intune pro vaše uživatele.  

|    Stav uživatele    |    Chování ochrany aplikace     |    Interval opakování (viz poznámku)    |    Proč k tomu dochází?    |
|-----------------------------------------------------|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
|    Tenant není zaregistrované.    |    Počkejte na další interval opakování.  Ochrana aplikací není pro tohoto uživatele aktivní.    |    24 hodin    |    Vyvolá se v případě, že jste nestavili vašeho tenanta pro Intune.    |
|    Uživatel nemá licenci.     |    Počkejte na další interval opakování.  Ochrana aplikací není pro tohoto uživatele aktivní.     |    12 hodin – na zařízeních s Androidem ale tento interval vyžaduje Intune APP SDK verze 5.6.0 nebo novější. V opačném případě pro zařízení s Androidem je tento interval 24 hodin.   |    Vyvolá se v případě, že jste nelicencovaný uživatel pro Intune.    |
|    Uživatel nepřiřadil zásady ochrany aplikací.    |    Počkejte na další interval opakování.  Ochrana aplikací není pro tohoto uživatele aktivní.    |    12 hodin        |    Nastane, pokud jste uživateli nepřiřadili nastavení aplikace.    |
|    Uživatelem přiřazené zásady ochrany aplikací, ale aplikace není definovaná v zásadách ochrany aplikací   |    Počkejte na další interval opakování.  Ochrana aplikací není pro tohoto uživatele aktivní.    |    12 hodin        |    Vyvolá se v případě, že jste aplikaci nepřidali do aplikace.    |
|    Uživatel se úspěšně zaregistroval pro Intune MAM.    |    Ochrana aplikací se aplikuje na nastavení zásad.    K aktualizacím dochází na základě intervalu opakování.    |    Služba Intune definovaná na základě uživatelského zatížení.    Obvykle 30 minut.     |    Vyvolá se v případě, že se uživatel úspěšně zaregistroval ve službě Intune pro konfiguraci MAM.    |

> [!NOTE]
> Intervaly opakování můžou vyžadovat, aby se mohlo použít aktivní aplikace, což znamená, že se aplikace spouští a používá.  Pokud je interval opakování 24 hodin a uživatel počká 48 hodiny na spuštění aplikace, bude se klient ochrany aplikací opakovat za 48 hodin.

## <a name="handling-network-connectivity-issues"></a>Zpracování potíží s připojením k síti

Pokud se registrace uživatele z důvodu problémů s připojením k síti nezdařila, je použit akcelerovaný interval opakování.  Klient ochrany aplikací se znovu pokusí o více než delší dobu, dokud interval nedosáhne 60 minut nebo je vytvořeno úspěšné připojení.  Klient se pak bude pokračovat v intervalu 60 minut, dokud nebude provedeno úspěšné připojení. Pak se klient vrátí ke standardnímu intervalu opakování na základě stavu uživatele.

## <a name="next-steps"></a>Další kroky

[Přiřazení licencí uživatelům, aby mohli zaregistrovat zařízení v Intune](../fundamentals/licenses-assign.md)

