---
title: Detaily o požadavcích na síť a šířce pásma pro Microsoft Intune
titleSuffix: ''
description: Podívejte se na detaily o požadavcích na konfiguraci sítě a šířce pásma pro Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/17/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0f737d48-24bc-44cd-aadd-f0a1d59f6893
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 569a80d21efd82b6008c7aa7a613c089a10c6ff3
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79331111"
---
# <a name="intune-network-configuration-requirements-and-bandwidth"></a>Šířka pásma a požadavky na konfiguraci sítě Intune

Tyto informace můžete použít k pochopení požadavků na šířku pásma pro nasazení Intune.

## <a name="average-network-traffic"></a>Průměrné zatížení sítě

Tabulka uvádí přibližnou velikost a četnost u nejčastějšího obsahu přenášeného po síti u každého klienta.

> [!NOTE]
> Aby bylo zajištěno, že zařízení obdrží aktualizace a obsah z Intune, musí se pravidelně připojovat k internetu. Čas potřebný k přijetí aktualizací nebo obsahu se může lišit. Zařízení by ale měla být připojená k internetu každý den nepřetržitě alespoň po dobu jedné hodiny.

|Typ obsahu|Přibližná velikost|Četnost a podrobnosti|
|----------------|--------------------|-------------------------|
|Instalace klienta Intune<br /><br />**K instalaci klienta Intune se přidávají ještě tyto požadavky**|125 MB|**Jednorázový**<br /><br />Velikost souborů klienta ke stažení se liší podle operačního systému klientského počítače.|
|Registrační balíček klienta|15 MB|**Jednorázový**<br /><br />Další stahování je možné, pokud jsou pro tento typ obsahu dostupné aktualizace.|
|Agent Endpoint Protection|65 MB|**Jednorázový**<br /><br />Další stahování je možné, pokud jsou pro tento typ obsahu dostupné aktualizace.|
|Agent Operations Manageru|11 MB|**Jednorázový**<br /><br />Další stahování je možné, pokud jsou pro tento typ obsahu dostupné aktualizace.|
|Agent zásad|3 MB|**Jednorázový**<br /><br />Další stahování je možné, pokud jsou pro tento typ obsahu dostupné aktualizace.|
|Agent Vzdálené pomoci prostřednictvím nástroje Microsoft Easy Assist|6 MB|**Jednorázový**<br /><br />Další stahování je možné, pokud jsou pro tento typ obsahu dostupné aktualizace.|
|Denní operace klienta|6 MB|**denně**<br /><br />Klient Intune pravidelně komunikuje se službou Intune a kontroluje aktualizace a zásady a oznamuje službě stav klienta.|
|Aktualizace definicí malwaru Endpoint Protection|Různé<br /><br />Obvykle 40 KB až 2 MB|**denně**<br /><br />Až třikrát denně|
|Aktualizace modulu Endpoint Protection|5 MB|**Nadpis**|
|Aktualizace softwaru|Různé<br /><br />Velikost závisí na nasazených aktualizacích.|**Nadpis**<br /><br />Aktualizace softwaru se obvykle vydávají k druhému úterý v měsíci.<br /><br />Nově zaregistrovaný nebo nasazený počítač může používat větší šířku pásma sítě při stahování celé sady dříve vydaných aktualizací.|
|Aktualizace Service Pack|Různé<br /><br />Velikost se liší u každé nasazené aktualizace Service Pack.|**Různé**<br /><br />Závisí na tom, kdy aktualizace Service Pack nasadíte.|
|Distribuce softwaru|Různé<br /><br />Velikost závisí na nasazeném softwaru.|**Různé**<br /><br />Závisí na tom, kdy software nasadíte.|

## <a name="ways-to-reduce-network-bandwidth-use"></a>Způsob snížení využití šířky pásma sítě

Ke snížení využití šířky pásma sítě pro klienty Intune můžete použít jeden nebo více těchto způsobů.

### <a name="use-a-proxy-server-to-cache-content-requests"></a>Používání proxy serveru pro ukládání požadavků obsahu do mezipaměti

Proxy server může ukládat do mezipaměti obsah a snížit tak počet duplicitních položek ke stažení a redukovat u obsahu z internetu využití šířky pásma sítě.

Proxy server ukládající do mezipaměti, který dostává z klientů žádosti o obsah, může takový obsah načíst a může uložit do mezipaměti odpovědi z webu i stahované položky. Server používá data uložená v mezipaměti pro odpovědi na následné žádosti z klientských počítačů.

Tady jsou obvyklá nastavení proxy serveru, který do mezipaměti ukládá obsah pro klienty Intune.


|          Nastavení           |           Doporučená hodnota           |                                                                                                  Podrobnosti                                                                                                  |
|----------------------------|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         Velikost mezipaměti         |             5 GB až 30 GB             | Hodnota se liší podle počtu klientských počítačích v síti a používaných konfigurací. Aby se soubory neodstranily příliš brzy, upravte velikost mezipaměti pro vaše prostředí. |
| Velikost jednotlivých souborů mezipaměti |                950 MB                 |                                                                     Toto nastavení nemusí být dostupné na všech proxy serverech s ukládáním do mezipaměti.                                                                     |
|   Typy objektů do mezipaměti    | HTTP<br /><br />HTTPS<br /><br />BITS |                                               Balíčky Intune jsou soubory CAB stažené Službou inteligentního přenosu na pozadí (BITS) přes HTTP.                                               |
> [!NOTE]
> Pokud použijete proxy server k ukládání požadavků obsahu do mezipaměti, komunikace je zašifrovaná jenom mezi klientem a proxy serverem a z proxy serveru do Intune. Připojení z klienta k Intune nebude zašifrované na konci.

Informace o používání proxy serveru k ukládání obsahu do mezipaměti najdete v dokumentaci k vašemu řešení proxy serveru.

### <a name="use-background-intelligent-transfer-service-bits-on-computers"></a>Použití Background Intelligent Transfer Service (BITS) na počítačích

Během hodin, které nakonfigurujete, můžete k omezení šířky pásma sítě použít službu BITS na počítači s Windows. Zásady BITS můžete nakonfigurovat na stránce **Šířka pásma sítě** v zásadách agenta Intune.

> [!NOTE]
> Pro správu MDM v systému Windows používá ke stažení bitů jenom rozhraní pro správu operačního systému pro typ aplikace MobileMSI. AppX/MsiX používají vlastní zásobník pro stahování bez služby BITS a aplikace Win32 přes agenta Intune místo bitů používá optimalizaci doručování.

Další informace o službě BITS a počítačích s Windows najdete v části [Služba inteligentního přenosu na pozadí](https://technet.microsoft.com/library/bb968799.aspx) v knihovně TechNet.

### <a name="delivery-optimization"></a>Optimalizace doručení

Optimalizace doručení vám umožní používat Intune k omezení spotřeby šířky pásma, když zařízení s Windows 10 stahují aplikace a aktualizace. Pomocí samoobslužné distribuce distribuované mezipaměti lze soubory ke stažení načíst z tradičních serverů a alternativních zdrojů (jako jsou síťové partnery).

Úplný seznam verzí a typů obsahu, které podporuje Optimalizace doručení, najdete v článku věnovaném [optimalizaci doručování pro Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#requirements).

[Optimalizace doručování můžete nastavit](../configuration/delivery-optimization-settings.md) jako součást profilů konfigurace zařízení.

### <a name="use-branchcache-on-computers"></a>Používání BranchCache na počítačích

Klienti Intune můžou díky BranchCache omezit přenos v síti WAN. BranchCache podporují následující operační systémy:

- Windows 7
- Windows 8.0
- Windows 8.1
- Windows 10

Abyste mohli BranchCache používat, musíte na klientském počítači povolit BranchCache a pak ho nakonfigurovat pro **režim distribuované mezipaměti**.

Když je klient Intune nainstalovaný na počítačích, služba BranchCache a režim distribuované mezipaměti jsou ve výchozím nastavení povolené. Pokud ale Zásady skupiny zakázal službu BranchCache, Intune tyto zásady nepřepíše a služba BranchCache zůstane zakázaná.

Pokud používáte BranchCache, měli byste při správě zásad skupiny a zásad brány firewall pro Intune spolupracovat s ostatními správci ve vaší organizaci. Zajistěte, aby nasadily zásady zakazující BranchCache nebo výjimky brány firewall. Další informace o BranchCache najdete v tématu [BranchCache – přehled](https://technet.microsoft.com/library/hh831696.aspx).

> [!NOTE]
> Pomocí Microsoft Intune můžete spravovat počítače s Windows buď [jako mobilní zařízení se správou mobilních zařízení (MDM)](../enrollment/windows-enroll.md) , nebo jako počítače s klientským softwarem Intune. Microsoft doporučuje, aby zákazníci [používali řešení správy](../enrollment/windows-enroll.md) mobilních zařízení, kdykoli to bude možné. Pokud tento způsob spravujete, služba BranchCache není podporována. Další informace najdete v tématu [porovnání správy počítačů s Windows jako počítačů nebo mobilních zařízení](pc-management-comparison.md).

## <a name="next-steps"></a>Další kroky

[Kontrola koncových bodů pro Intune](intune-endpoints.md)
