---
title: Konfigurace nastavení Microsoft Edge
titleSuffix: Configuration Manager
description: Konfigurovat nastavení pro webový prohlížeč Microsoft Edge na klientech s Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 4ed49ed3623b34bfb51fd66fafa858ae3951a5af
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906359"
---
# <a name="configure-microsoft-edge-settings-in-configuration-manager"></a>Konfigurace nastavení Microsoft Edge v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<!-- 1357310 -->
Od verze 1802 pro zákazníky, kteří používají webový prohlížeč [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) na klientech Windows 10, vytvořte zásady nastavení dodržování předpisů Configuration Manager ke konfiguraci několika nastavení Microsoft Edge. 

Tato zásada platí jenom pro klienty ve Windows 10 verze 1703 nebo novější. <!--511552-->


## <a name="policy-settings"></a>Nastavení zásad
Tato zásada aktuálně obsahuje následující nastavení:
- **Nastavit prohlížeč Microsoft Edge jako výchozí**: konfiguruje nastavení výchozí aplikace Windows 10 pro webový prohlížeč na Microsoft Edge.
- Možnost **Povolení rozevíracího seznamu na panelu Adresa**: vyžaduje Windows 10 verze 1703 nebo novější. Další informace najdete v tématu [zásady prohlížeče AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Povolí synchronizaci oblíbených položek mezi prohlížeči Microsoftu**: vyžaduje Windows 10 verze 1703 nebo novější. Další informace najdete v tématu [zásady prohlížeče SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Povolení vymazání dat procházení při ukončení**: vyžaduje Windows 10 verze 1703 nebo novější. Další informace najdete v tématu [zásady prohlížeče ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Povolit hlavičky do Not Track**: Další informace najdete v tématu [zásady prohlížeče AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Povolení automatického vyplňování**: Další informace najdete v tématu [zásady prohlížeče AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Povolení souborů cookie**: Další informace najdete v tématu [zásady prohlížeče AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Povolení blokování automaticky otevíraných oken**: Další informace najdete v tématu [zásady prohlížeče AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Povolení návrhů hledání na adresním řádku**: Další informace najdete v tématu [zásady prohlížeče AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Povolení odesílání intranetového provozu do Internet Exploreru**: Další informace najdete v tématu [zásady prohlížeče SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Povolení správce hesel**: Další informace najdete v tématu [zásady prohlížeče AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Povolení vývojářské nástroje**: Další informace najdete v tématu [zásady prohlížeče AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Povolení rozšíření**: Další informace najdete v tématu [zásady prohlížeče AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Konfigurace nastavení filtru SmartScreen v programu Windows Defender pro Microsoft Edge
<!--1353701-->
Počínaje verzí 1806 tato zásada přidá tři nastavení [filtru SmartScreen v programu Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview). Zásady teď na stránce **nastavení filtru SmartScreen** obsahují následující dodatečná nastavení:

- **Povolit SmartScreen**: Určuje, zda je povolen filtr SmartScreen v programu Windows Defender. Další informace najdete v tématu [zásady prohlížeče AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Uživatelé můžou přepsat výzvu filtru SmartScreen pro weby**: Určuje, jestli můžou uživatelé potlačit upozornění filtru SmartScreen v programu Windows Defender týkající se potenciálně škodlivých webů. Další informace najdete v tématu [zásady prohlížeče PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Uživatelé můžou přepsat výzvu filtru SmartScreen pro soubory**: Určuje, jestli můžou uživatelé potlačit upozornění filtru SmartScreen v programu Windows Defender týkající se stahování neověřených souborů. Další informace najdete v tématu [zásady prohlížeče PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="create-the-microsoft-edge-browser-profile"></a>Vytvořit profil prohlížeče Microsoft Edge

1. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Rozbalte **Nastavení dodržování předpisů** a vyberte uzel **profily prohlížeče Microsoft Edge** . Pokud chcete **vytvořit profil Microsoft Edge**, klikněte na pásu karet možnost.
2. Zadejte **název** zásady, volitelně zadejte **Popis**a klikněte na **Další**.
3. Na stránce **Obecné nastavení** změňte hodnotu na **nakonfigurovanou** pro nastavení, která chcete zahrnout do této zásady, a klikněte na **Další**. Aby bylo možné pokračovat, musí být nastavení **nastavit prohlížeč Edge jako výchozí** .
4. V části verze 1806 a novější nakonfigurujte nastavení na stránce **nastavení filtru SmartScreen** a potom klikněte na tlačítko **Další**. 
5. Na stránce **podporované platformy** vyberte verze operačních systémů a architektury, pro které platí tato zásada, a klikněte na **Další**. 
6. Dokončete průvodce.



## <a name="deploy-the-policy"></a>Nasazení zásady

1. Vyberte zásadu a klikněte na možnost pásu karet k **nasazení**.
2. Klikněte na **Procházet** a vyberte kolekci uživatelů nebo zařízení, do které chcete zásady nasadit. 
3. Podle potřeby vyberte další možnosti.  
     a. Vygenerovat výstrahy, pokud zásady nedodržují předpisy.  
     b. Nastavte plán, podle kterého klient vyhodnotí kompatibilitu zařízení s touto zásadou. 
4. Kliknutím na tlačítko **OK** vytvořte nasazení.



## <a name="next-steps"></a>Další kroky

Stejně jako u zásad nastavení dodržování předpisů klient opraví nastavení podle zadaného plánu. [Monitorujte a ohlaste dodržování předpisů zařízením](monitor-compliance-settings.md) v konzole Configuration Manager.
