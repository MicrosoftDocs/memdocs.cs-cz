---
title: Ověření nastavení zásad ochrany aplikací
titleSuffix: Microsoft Intune
description: Naučte se, jak otestovat, jestli jsou vaše zásady ochrany aplikací správně nastavené a fungují v Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2020
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 15f8a838-0b69-412b-a42e-c6edb61f0cae
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d41dec48ff1f357733882ebe99bcad670e676675
ms.sourcegitcommit: d601f4e08268d139028f720c0a96dadecc7496d5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/01/2020
ms.locfileid: "80488008"
---
# <a name="how-to-validate-your-app-protection-policy-setup-in-microsoft-intune"></a>Ověření nastavení zásad ochrany aplikací v Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Prověřte, jestli jsou vaše zásady ochrany aplikací správně nastavené a jestli fungují. Tento návod se vztahuje k zásadám ochrany aplikací na portálu Azure Portal.

## <a name="checking-for-symptoms"></a>Zjišťování příznaků
Není pravděpodobné, že by problém nahlásili uživatelé, protože ochrana aplikací je nástroj na ochranu dat. Pokud dojde k potížím s konfigurací ochrany aplikací, bude mít uživatel neomezený přístup, protože by byl bez ochrany aplikací a nevěděl, že došlo k problému. Z tohoto důvodu doporučujeme ověřit konfiguraci ochrany aplikací tím, že provedete pilotní zásady ochrany aplikací s malou skupinou uživatelů, kteří můžou omezení ochrany aplikací záměrně otestovat.

## <a name="what-to-check"></a>Co zkontrolovat

Pokud se při testování ukáže, že chování zásad ochrany aplikací nefunguje podle očekávání, ověřte tyto položky:

- Mají uživatelé licenci k ochraně aplikací?
- Mají uživatelé licenci k O365?
- Je stav každé aplikace ochrany aplikací uživatelů podle očekávání. Aplikace můžou být ve stavu **Zaregistrováno** a **Není zaregistrováno**.

### <a name="user-app-protection-status"></a>Stav uživatele ochrany aplikací
1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Vyberte **aplikace** > **monitor** >  **stav ochrany aplikací**a pak vyberte dlaždici **přiřazení uživatelé** . 
4. Na stránce **vytváření sestav aplikací** vyberte **Vybrat uživatele** a zobrazte seznam uživatelů a skupin. 
5. Vyhledejte a vyberte uživatele ze seznamu a pak zvolte **Vybrat uživatele**. V horní části podokna **vytváření sestav aplikace** uvidíte, jestli má uživatel licenci k ochraně aplikací. Můžete také zjistit, jestli má uživatel licenci pro O365 a stav aplikace pro všechna zařízení uživatele.

## <a name="what-to-do"></a>Co dělat
Postupujte podle stavu uživatele:

- Pokud uživatel nemá licenci na ochranu aplikací, přiřaďte mu [licenci Intune](../fundamentals/licenses.md) .
- Pokud uživatel nemá licenci pro O365, Získejte [licenci](../fundamentals/licenses.md) pro uživatele.
- Pokud je aplikace uživatele uvedená **v seznamu nevráceno se změnami**, ověřte, jestli jste pro tuto aplikaci správně nakonfigurovali [Zásady ochrany aplikací](app-protection-policies-validate.md) .
- Ujistěte se, že tyto podmínky platí pro všechny uživatele, na které chcete [Zásady ochrany aplikací](app-protection-policies-monitor.md) použít.

## <a name="see-also"></a>Viz také

- [Co jsou zásady ochrany aplikací Intune?](app-protection-policies.md)
- [Licence, které zahrnují Intune](../fundamentals/licenses.md)
- [Přiřazení licencí uživatelům, aby mohli zaregistrovat zařízení v Intune](../fundamentals/licenses-assign.md)
- [Ověření nastavení zásad ochrany aplikací](app-protection-policies-validate.md)
- [Jak monitorovat zásady ochrany aplikací](app-protection-policies-monitor.md)

