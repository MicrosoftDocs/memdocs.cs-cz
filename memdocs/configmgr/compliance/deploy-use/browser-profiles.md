---
title: Konfigurace nastavení Microsoft Edge
titleSuffix: Configuration Manager
description: Konfigurovat nastavení pro webový prohlížeč Microsoft Edge starší verze v klientech s Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 898d5240046655ca3d13037f74c92e730ab1993e
ms.sourcegitcommit: 7f542c97ac55bbd329f5befda97d671213c24e9a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/08/2020
ms.locfileid: "84506133"
---
# <a name="configure-microsoft-edge-legacy-settings-in-configuration-manager"></a>Konfigurace nastavení Microsoft Edge starší verze v Configuration Manager

> [!IMPORTANT]
> Pokud používáte Microsoft Edge verze 77 nebo novější a pokoušíte se otevřít podokno nastavení, zadejte `edge://settings/profiles` místo hledání do panelu Adresa prohlížeče. Další informace najdete v tématu o [tom, jak se seznámit s Microsoft Edgem](https://support.microsoft.com/help/17171/microsoft-edge-get-to-know).
>
> Tento článek je určený pro odborníky v oblasti IT, kde můžete spravovat nastavení starší verze Microsoft Edge pomocí Configuration Manager koncového bodu Microsoft.

*Platí pro: Configuration Manager (Current Branch)*

<!-- 1357310 -->
Pro zákazníky, kteří používají [starší verzi webového prohlížeče Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/) v klientech Windows 10, vytvořte Configuration Manager zásady dodržování předpisů pro konfiguraci nastavení prohlížeče.

Tato zásada platí jenom pro klienty ve Windows 10, verze 1703 nebo novější a Microsoft Edge starší verze 45 a starší. <!--511552-->

Další informace o správě Microsoft Edge verze 77 nebo novější s Configuration Manager najdete v tématu [nasazení Microsoft Edge, verze 77 a novější](../../apps/deploy-use/deploy-edge.md). Další informace o konfiguraci zásad pro Microsoft Edge verze 77 nebo novější najdete v tématu [Microsoft Edge-policies](https://docs.microsoft.com/DeployEdge/microsoft-edge-policies).

## <a name="policy-settings"></a>Nastavení zásad

Tato zásada aktuálně obsahuje následující nastavení:

- **Nastavit prohlížeč Microsoft Edge jako výchozí**: konfiguruje nastavení výchozí aplikace Windows 10 pro webový prohlížeč na Microsoft Edge.

- Možnost **Povolení rozevíracího seznamu na panelu Adresa**: vyžaduje Windows 10 verze 1703 nebo novější. Další informace najdete v tématu [zásady prohlížeče AllowAddressBarDropdown](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).

- **Povolí synchronizaci oblíbených položek mezi prohlížeči Microsoftu**: vyžaduje Windows 10 verze 1703 nebo novější. Další informace najdete v tématu [zásady prohlížeče SyncFavoritesBetweenIEAndMicrosoftEdge](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).

- **Povolení vymazání dat procházení při ukončení**: vyžaduje Windows 10 verze 1703 nebo novější. Další informace najdete v tématu [zásady prohlížeče ClearBrowsingDataOnExit](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).

- **Povolit hlavičky do Not Track**: Další informace najdete v tématu [zásady prohlížeče AllowDoNotTrack](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).

- **Povolení automatického vyplňování**: Další informace najdete v tématu [zásady prohlížeče AllowAutofill](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).

- **Povolení souborů cookie**: Další informace najdete v tématu [zásady prohlížeče AllowCookies](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).

- **Povolení blokování automaticky otevíraných oken**: Další informace najdete v tématu [zásady prohlížeče AllowPopups](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).

- **Povolení návrhů hledání na adresním řádku**: Další informace najdete v tématu [zásady prohlížeče AllowSearchSuggestionsinAddressBar](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).

- **Povolení odesílání intranetového provozu do Internet Exploreru**: Další informace najdete v tématu [zásady prohlížeče SendIntranetTraffictoInternetExplorer](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).

- **Povolení správce hesel**: Další informace najdete v tématu [zásady prohlížeče AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).

- **Povolení vývojářské nástroje**: Další informace najdete v tématu [zásady prohlížeče AllowDeveloperTools](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).

- **Povolení rozšíření**: Další informace najdete v tématu [zásady prohlížeče AllowExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

> [!TIP]
> Další informace o tom, jak nakonfigurovat tato a další nastavení pomocí zásad skupiny, najdete v článku [Zásady skupiny starší verze Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/group-policies/).

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge-legacy"></a>Konfigurace nastavení filtru SmartScreen v programu Windows Defender pro Microsoft Edge starší verze
<!--1353701-->
Tato zásada přidává tři nastavení [filtru SmartScreen v programu Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview). Zásady teď na stránce **nastavení filtru SmartScreen** obsahují následující dodatečná nastavení:

- **Povolit SmartScreen**: Určuje, zda je povolen filtr SmartScreen v programu Windows Defender. Další informace najdete v tématu [zásady prohlížeče AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).

- **Uživatelé můžou přepsat výzvu filtru SmartScreen pro weby**: Určuje, jestli můžou uživatelé potlačit upozornění filtru SmartScreen v programu Windows Defender týkající se potenciálně škodlivých webů. Další informace najdete v tématu [zásady prohlížeče PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).

- **Uživatelé můžou přepsat výzvu filtru SmartScreen pro soubory**: Určuje, jestli můžou uživatelé potlačit upozornění filtru SmartScreen v programu Windows Defender týkající se stahování neověřených souborů. Další informace najdete v tématu [zásady prohlížeče PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).

## <a name="create-the-browser-profile"></a>Vytvořit profil prohlížeče

1. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Rozbalte **Nastavení dodržování předpisů** a vyberte uzel **profily prohlížeče Microsoft Edge** . Na pásu karet vyberte **vytvořit profil Microsoft Edge**.

2. Zadejte **název** zásady, volitelně zadejte **Popis**a vyberte **Další**.

3. Na stránce **Obecné nastavení** změňte hodnotu na **nakonfigurovanou** pro nastavení, která chcete zahrnout do této zásady. Pokud chcete pokračovat v průvodci, ujistěte se, že jste nakonfigurovali nastavení pro **nastavení prohlížeče Edge jako výchozí**.

4. Nakonfigurujte nastavení na stránce **nastavení filtru SmartScreen** .

5. Na stránce **podporované platformy** vyberte verze operačních systémů a architektury, pro které platí tato zásada.

6. Dokončete průvodce.

## <a name="deploy-the-policy"></a>Nasazení zásady

1. Vyberte zásadu a na pásu karet vyberte **nasadit**.

2. **Procházením** vyberte kolekci uživatelů nebo zařízení, do které chcete zásady nasadit.

3. V případě potřeby vyberte další možnosti:

    1. Vygenerovat výstrahy, pokud zásady nedodržují předpisy.

    2. Nastavte plán, podle kterého klient vyhodnotí kompatibilitu zařízení s touto zásadou.

4. Vyberte **OK** a vytvořte nasazení.

## <a name="next-steps"></a>Další kroky

Stejně jako u zásad nastavení dodržování předpisů klient opraví nastavení podle zadaného plánu. [Monitorujte a ohlaste dodržování předpisů zařízením](monitor-compliance-settings.md) v konzole Configuration Manager.
