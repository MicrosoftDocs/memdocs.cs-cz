---
title: Povolení datových připojení eSIM v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte nebo používejte technologii eSIM, abyste prostřednictvím různých datových tarifů získali přístup k internetu a datům. Přidejte nebo importujte aktivační kódy do Intune a potom tyto aktivační kódy přiřaďte pomocí konfiguračního profilu. Profily eSIM můžete také monitorovat a můžete kontrolovat stav zařízení s podporou eSIM.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 79e6f8c7b4501f0f15d00b094d7d90ad66225dd9
ms.sourcegitcommit: b94415467831517f2aeab9c7c8a13fe8db8bc8ed
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401770"
---
# <a name="configure-esim-cellular-profiles-in-intune-public-preview"></a>Konfigurace mobilních profilů eSIM v Intune (Public Preview)

Technologie eSIM je zabudovaný čip SIM, který vám na zařízení s podporou eSIM, jako je [Surface LTE Pro](https://www.microsoft.com/surface/business/surface-pro), umožňuje připojit se prostřednictvím mobilního datového připojení k internetu. Když využijete technologii eSIM, není nutné pořizovat SIM kartu od mobilního operátora. Při cestování po světě navíc můžete jednoduše přecházet mezi mobilními operátory a datovými tarify a zůstat v kontaktu se svými blízkými.

Můžete mít například mobilní datový tarif pro práci a jiný datový tarif od jiného mobilního operátora pro osobní použití. Když cestujete, můžete přístup k internetu získat vyhledáním mobilních operátorů s datovými tarify v dané oblasti.

Tato funkce platí pro:

- Windows 10 a novější

Do Intune můžete importovat jednorázové aktivační kódy poskytnuté vaším mobilním operátorem. Pokud chcete mobilní datové tarify konfigurovat na modulu eSIM, nasaďte tyto aktivační kódy do zařízení s podporou eSIM. Když Intune nainstaluje aktivační kód, hardwarový modul eSIM použije data v aktivačním kódu ke kontaktování mobilního operátora. Po dokončení se profil eSIM stáhne do zařízení a nakonfiguruje se pro připojení k mobilní síti.

Pokud chcete eSIM nasadit do zařízení pomocí Intune, budete potřebovat následující:

- **Zařízení s podporou eSIM** jako například Surface LTE: viz téma [Získání mobilního datového připojení na počítači s Windows 10 pomocí eSIM karty](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data). Nebo si zobrazte seznam [známých zařízení s podporou eSIM](#esim-capable-devices) (v tomto článku).
- **Počítač s Windows 10 Fall Creators Update** (1709 nebo novější), který je zaregistrovaný a spravovaný prostřednictvím MDM přes Intune.
- **Aktivační kódy** poskytnuté mobilním operátorem. Tyto jednorázové aktivační kódy se přidají do Intune a nasadí se do zařízení s podporou eSIM. Pokud chcete získat aktivační kódy eSIM, obraťte se na svého mobilního operátora.

## <a name="deploy-esim-to-devices---overview"></a>Nasazení eSIM do zařízení – přehled

Pokud chcete nasadit eSIM do zařízení, musí správce provést následující úlohy:

1. importovat aktivační kódy poskytnuté mobilním operátorem,
2. vytvořit skupinu zařízení služby Azure Active Directory (Azure AD), která obsahuje zařízení s podporou eSIM,
3. přiřadit skupinu Azure AD do importovaného fondu předplatných,
4. Monitorování nasazení

Tento článek vás uvedenými kroky provede.

## <a name="esim-capable-devices"></a>Zařízení s podporou eSIM

U následujících zařízení byla oznámena podpora eSIM a mohou už být v prodeji. Taky si můžete přečíst článek [Získání mobilního datového připojení na počítači s Windows 10 pomocí eSIM karty](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data).

- Acer Swift 7
- Asus NovoGo TP370QL
- Asus TP401
- Asus Transformer Mini T103
- HP Elitebook G5
- HP Envy x2
- HP Probook G5
- Lenovo Miix 630
- Lenovo T480
- Samsung Galaxy Book
- Surface Pro LTE
- HP Spectre Folio 13
- Lenovo Yoga C630

## <a name="step-1-add-cellular-activation-codes"></a>Krok 1: Přidání mobilních aktivačních kódů

Mobilní aktivační kódy poskytuje mobilní operátor v souboru CSV (textový soubor s oddělovači). Jakmile tento soubor budete mít, přidejte ho do Intune následujícím postupem:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení**  >  **mobilní profily eSIM karty**  >  **Přidat**.
3. Vyberte soubor CSV s aktivačními kódy.
4. Výběrem **OK** uložte změny.

### <a name="csv-file-requirements"></a>Požadavky na soubor CSV

Při práci se souborem CSV, který obsahuje aktivační kódy, se ujistěte, že se vy či váš mobilní operátor řídíte následujícími požadavky:

- Soubor musí být ve formátu CSV (názevsouboru.csv).
- Struktura souboru musí odpovídat striktnímu formátu, jinak nebude import úspěšný. Intune soubor při importu zkontroluje, a pokud se zjistí chyby, import selže.
- Aktivační kódy jsou jednorázové. Import aktivačních kódů, které jste už jednou importovali, se nedoporučuje, protože při nasazení na stejné či jiné zařízení může dojít k potížím.
- Každý soubor by měl být specifický pro jednoho mobilního operátora a všechny aktivační kódy v souboru by měli patřit pod stejný fakturační plán. Intune aktivační kódy distribuuje na cílová zařízení náhodně. Neexistuje žádná záruka, že konkrétní zařízení získá konkrétní aktivační kód.
- Do jednoho souboru CSV se může importovat maximálně 1000 aktivačních kódů.

### <a name="csv-file-example"></a>Příklad souboru CSV

1. První řádek a první buňka souboru CSV je adresa URL aktivační služby eSIM mobilního operátora, která se nazývá SM-DP+ (server přípravy dat správce předplatného). Adresa URL by měla být plně kvalifikovaným názvem domény (FQDN) bez čárek.
2. Druhý řádek a všechny následující řádky jsou jedinečnými jednorázovými aktivačními kódy, které obsahují dvě hodnoty:

    1. První sloupec je jedinečný ICCID (identifikátor čipu SIM).
    2. Druhý sloupec je ID pro porovnávání, které je oddělené čárkou (na konci už čárka není). Prohlédněte si následující příklad:

        :::image type="content" source="./media/esim-device-configuration/url-activation-code-examples.png" alt-text="Ukázkový soubor. CSV pro aktivační kód mobilní operátor.":::

3. Název souboru CSV se v centru pro správu Správce koncových bodů zobrazí jako název fondu mobilních předplatných. Na předchozím obrázku se soubor nazývá `UnlimitedDataSkynet.csv`. Takže Intune fond předplatných pojmenuje `UnlimitedDataSkynet.csv`:

    :::image type="content" source="./media/esim-device-configuration/subscription-pool-name-csv-file.png" alt-text="Fond odběrů mobilních předplatných se nazývá název souboru ukázka aktivačního kódu CSV.":::

## <a name="step-2-create-an-azure-ad-device-group"></a>Krok 2: Vytvoření skupiny zařízení služby Azure AD

Vytvořte skupinu zařízení, která obsahuje zařízení s podporou eSIM. Celý postup je uvedený v tématu [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md).

> [!NOTE]
> - Skupina se zaměřuje pouze na zařízení, ne uživatele.
> - Doporučujeme vytvořit statickou skupinu zařízení Azure AD, která obsahuje zařízení s podporou eSIM. Když použijete skupinu, budete mít jistotu, že cílíte pouze na zařízení s podporou eSIM.

## <a name="step-3-assign-esim-activation-codes-to-devices"></a>Krok 3: Přiřazení aktivačních kódů eSIM zařízením

Přiřaďte skupině Azure AD profil, který obsahuje zařízení s podporou eSIM.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení**  >  **mobilní profily na kartě**zařízení.
3. V seznamu profilů vyberte fond mobilních předplatných eSIM, který chcete přiřadit, a pak vyberte **Přiřazení**.
4. Zvolte **Zahrnout** skupiny nebo **Vyloučit** skupiny a pak tyto skupiny vyberte.

    :::image type="content" source="./media/esim-device-configuration/include-exclude-groups.png" alt-text="Zahrňte skupinu zařízení pro přiřazení profilu v Microsoft Intune.":::

5. Když skupiny vybíráte, zvolíte skupinu Azure AD. Pokud chcete vybrat více skupin, použijte klávesu **Ctrl** a požadované skupiny vyberte.
6. Až budete hotovi, zvolte **Uložit**, aby se změny uložily.

Aktivační kódy eSIM jsou jednorázové. Jakmile Intune nainstaluje aktivační kód na zařízení, modul eSIM kontaktuje mobilního operátora a stáhne mobilní profil. Tento kontakt dokončí registraci zařízení u sítě mobilního operátora.

## <a name="step-4-monitor-deployment"></a>Krok 4: Monitorování nasazení

### <a name="review-the-deployment-status"></a>Kontrola stavu nasazení

Po přiřazení profilu můžete monitorovat stav nasazení fondu předplatných.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení**  >  **mobilní profily na kartě**zařízení. Uvidíte uvedené všechny existující fondy mobilních předplatných eSIM.
3. Vyberte předplatné a zkontrolujte jeho **Stav nasazení**.

### <a name="check-the-profile-status"></a>Kontrola stavu profilu

Po vytvoření profilu zařízení Intune nabízí grafy. Tyto grafy zobrazují stav profilu, třeba že je úspěšně přiřazený k zařízením nebo jestli profil vykazuje konflikt.

1. Vyberte **zařízení**  >  **mobilní profily eSIM** > vybrat stávající předplatné.
2. Na kartě **Přehled** zobrazuje horní graf počet zařízení přiřazených ke konkrétnímu nasazení fondu mobilních předplatných eSIM.

    Ukazuje také počet zařízení pro jiné platformy, která jsou přiřazená ke stejnému profilu zařízení.

    Intune zobrazuje stav doručování a instalace aktivačního kódu cíleného na zařízení.

    - **Zařízení není synchronizované:** vybrané zařízení nekontaktovalo Intune od vytvoření zásady nasazení eSIM.
    - **Čekající aktivace:** přechodný stav, během kterého Intune aktivně instaluje aktivační kód do zařízení.
    - **Aktivní:** instalace aktivačního kódu proběhla úspěšně.
    - **Aktivace selhala:** instalace aktivačního kódu se nezdařila – přejděte na průvodce odstraňováním problémů.

#### <a name="view-the-detailed-device-status"></a>Zobrazení podrobného stavu zařízení

Podrobný seznam zařízení můžete monitorovat nebo si ho můžete zobrazit na stránce Stav zařízení.**

1. Vyberte **zařízení**  >  **mobilní profily eSIM** > vybrat stávající předplatné.
2. Vyberte **Stav zařízení**. Intune zobrazí další podrobnosti o zařízení:

    - **Název zařízení:** název vybraného zařízení
    - **Uživatel**: uživatel zaregistrovaného zařízení
    - **ICCID**: jedinečný kód poskytnutý mobilním operátorem v rámci aktivačního kódu nainstalovaného na zařízení
    - **Stav aktivace:** stav doručování a instalace aktivačního kódu na zařízení v Intune
    - **Stav mobilní sítě:** stav poskytovaný mobilním operátorem (Potíže řešte přímo s mobilním operátorem.)
    - **Poslední vrácení se změnami:** datum poslední komunikace zařízení s Intune

### <a name="monitor-esim-profile-details-on-the-actual-device"></a>Monitorování podrobností profilu eSIM na příslušném zařízení

1. Na svém zařízení otevřete **Nastavení** > přejděte na **Síť a internet**.
2. Vybrat **mobilní síť**  >  **Správa profilů eSIM**
3. Uvidíte profily eSIM:

    :::image type="content" source="./media/esim-device-configuration/device-settings-cellular-profiles.png" alt-text="Podívejte se na profily eSIM v nastavení zařízení.":::

## <a name="remove-the-esim-profile-from-device"></a>Odebrání profilu eSIM ze zařízení

Když odeberete zařízení ze skupiny Azure AD, odebere se i profil eSIM. Ujistěte se, že:

1. Zkontrolovat, že danou skupinu zařízení eSIM Azure AD používáte.
2. Přejít do skupiny Azure AD a požadované zařízení z ní odebrat.
3. Když odebrané zařízení kontaktuje Intune, vyhodnotí se aktualizovaná zásada a profil eSIM se odebere.

Profil eSIM se také odebere, když se zařízení [vyřadí](../remote-actions/devices-wipe.md#retire), uživatel zruší jeho registraci nebo když na zařízení proběhne [vzdálené obnovení továrního nastavení zařízení](../remote-actions/devices-wipe.md#wipe).

> [!NOTE]
> Odebrání profilu nemusí ukončit účtování. Ohledně stavu fakturace za své zařízení se obraťte na mobilního operátora.

## <a name="best-practices--troubleshooting"></a>Osvědčené postupy a řešení potíží

- Zkontrolujte, že je soubor CSV správně naformátovaný. Přesvědčte se, že soubor neobsahuje duplicitní kódy, více mobilních operátorů nebo různé datové tarify. Každý soubor musí být jedinečný pro daného mobilního operátora a mobilní datový tarif.
- Vytvořte statickou skupinu zařízení Azure AD, která obsahuje pouze vybraná zařízení eSIM.
- Pokud se vyskytl problém se stavem nasazení, zkontrolujte následující:
  - **Nesprávný formát souboru:** Viz **Krok 1: Přidání mobilních aktivačních kódů** (v tomto článku) popisující správné formátování souboru.
  - **Chyba mobilní aktivace, kontaktujte mobilního operátora:** Aktivační kód pravděpodobně nebude v jeho síti aktivovaný. Mohlo také selhat stažení profilu a mobilní aktivace.

## <a name="next-steps"></a>Další kroky

[Konfigurace profilů zařízení](device-profiles.md)
