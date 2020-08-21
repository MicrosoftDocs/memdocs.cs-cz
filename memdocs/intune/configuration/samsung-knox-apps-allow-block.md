---
title: Zásady Microsoft Intune k povolení/blokování aplikací pro Samsung Knox
titleSuffix: ''
description: Vytvořte vlastní profil, který zařízením se zabezpečením Samsung Knox Standard povolí nebo zablokuje aplikace.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3ee2e89dcfd7ab963dae3b14b5e7d53daaa07ff4
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695983"
---
# <a name="use-custom-policies-in-microsoft-intune-to-allow-and-block-apps-for-samsung-knox-standard-devices"></a>Použití vlastních zásad v Microsoft Intune, které v povolí nebo blokují aplikace pro zařízení se zabezpečením Samsung Knox Standard 

Postupy v tomto článku použijte k vytvoření vlastní zásady Microsoft Intune, která obsahuje jeden z těchto seznamů:

- Seznam aplikací, u kterých je v příslušném zařízení blokované spuštění. Aplikace v tomto seznamu nebude možné spouštět ani v případě, že již byly nainstalované v okamžiku nasazení zásady.
- Seznam aplikací, které si uživatelé příslušného zařízení mohou nainstalovat z obchodu Google Play. Je možné instalovat jen aplikace uvedené na seznamu. Z tohoto obchodu nejde nainstalovat žádné další aplikace.

Tato nastavení mohou používat jenom zařízení se spuštěnou aplikací Samsung Knox Standard.

## <a name="create-an-allowed-or-blocked-app-list"></a>Vytvoření seznamu povolených nebo blokovaných aplikací

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte následující nastavení:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **vlastní profil Android**.
    - **Popis:** Zadejte popis, který nastavení stručně charakterizuje, a další důležité podrobnosti.
    - **Platforma**: vyberte **Android**.
    - **Typ profilu**: vyberte **vlastní**.

4. V nabídce **Vlastní nastavení OMA-URI** vyberte **Přidat**. Zadejte následující nastavení:

    Seznam aplikací, u kterých je v příslušném zařízení blokované spuštění:

    - **Název**: zadejte **PreventStartPackages**.
    - **Popis:** Zadejte popis, který přehledně vystihuje nastavení, a další důležité informace kvůli jeho snadnějšímu vyhledání. Zadejte například **seznam aplikací, které jsou zablokovány pro spuštění**.
    - **OMA-URI** (rozlišuje velká a malá písmena): zadejte **./Vendor/MSFT/PolicyManager/my/ApplicationManagement/PreventStartPackages**.
    - **Datový typ**: vyberte **řetězec**.
    - **Hodnota**: Zadejte seznam názvů balíčků aplikací, které chcete zakázat. Můžete použít `;` , `:` nebo `|` jako oddělovač. Zadejte například `package1;package2;`.

   Pro seznam aplikací, které si uživatelé můžou nainstalovat z obchodu Google Play, s vyloučením všech ostatních:

    - **Název**: zadejte **AllowInstallPackages**.
    - **Popis**: zadejte popis, který poskytuje přehled nastavení, a další důležité informace, které vám pomůžou najít profil. Například zadejte **seznam aplikací, které uživatelé mohou instalovat z Google Play**.
    - **OMA-URI** (rozlišuje velká a malá písmena): zadejte **./Vendor/MSFT/PolicyManager/my/ApplicationManagement/AllowInstallPackages**.
    - **Datový typ**: vyberte **řetězec**.
    - **Hodnota**: Zadejte seznam názvů balíčků aplikací, které chcete zakázat. Můžete použít `;` , `:` nebo `|` jako oddělovač. Zadejte například `package1;package2;`.

5. Výběrem **OK** uložte změny.
6. Po dokončení vyberte **OK**  >  **vytvořit** a vytvořte profil Intune. Po dokončení se Váš profil zobrazí v seznamu **zařízení – konfigurační profily** .

>[!TIP]
> ID balíčku aplikace najdete tak, že na tuto aplikaci přejdete v obchodě Google Play. ID balíčku je součástí adresy URL stránky aplikace. Třeba aplikace Microsoft Word má ID balíčku **com.microsoft.office.word**.

Při příštím ověření každého cílového zařízení se použije nastavení aplikace.

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).
