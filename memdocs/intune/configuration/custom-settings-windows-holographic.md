---
title: Vlastní nastavení – zařízení s Windows holografickým pro firmy – Microsoft Intune | Microsoft Docs
description: Přidejte nebo vytvořte si vlastní profil, abyste mohli v Microsoft Intune použít nastavení OMA-URI pro zařízení s Windows Holographic for Business, včetně zařízení Microsoft Hololens. Můžete nakonfigurovat nastavení poskytovatele služeb konfigurace zásad (CSP) AllowFastReconnect, AllowVPN, AllowUpdateService, UpdateServiceURL, RequireUpdatesApproval, ApprovedUpdates a ApplicationLaunchRestrictions.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.article: article
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.topic: reference
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 43199009740f259c6a6484e455b0205da76492ba
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084047"
---
# <a name="use-custom-settings-for-windows-holographic-for-business-devices-in-intune"></a>Použití vlastního nastavení u zařízení s Windows Holographic for Business v Intune

V Microsoft Intune můžete použít vlastní profily k přidání nebo vytvoření vlastního nastavení pro zařízení s Windows Holographic for Business. Vlastní profily jsou funkcí Intune. Jsou navržené tak, aby bylo možné přidat nastavení a funkce zařízení, které nejsou integrované do Intune.

Vlastní profily pro Windows Holographic for Business používají nastavení OMA-URI (Open Mobile Alliance Uniform Resource Identifier) ke konfiguraci různých funkcí. Tato nastavení obvykle používají výrobci mobilních zařízení k řízení funkcí na zařízení.

Windows Holographic for Business zpřístupňuje řadu nastavení poskytovatelů konfiguračních služeb (CSP). Základní informace o CSP najdete v [úvodu o poskytovatelích konfiguračních služeb (CSP) pro IT specialisty](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers). Konkrétní poskytovatele CSP, které podporuje Windows Holographic, najdete v části [Poskytovatelé CSP podporovaní ve Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens).

Pokud hledáte konkrétní nastavení, nezapomeňte, že řada integrovaných nastavení je v [restriktivním profilu zařízení s Windows Holographic for Business](device-restrictions-windows-holographic.md). Takže možná nebude potřeba zadávat vlastní hodnoty.

V tomto článku si ukážeme, jak vytvořit vlastní profil pro zařízení s Windows Holographic for Business. Článek také obsahuje seznam doporučených nastavení OMA-URI.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující nastavení:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **vlastní profil HoloLens**.
    - **Popis:** Zadejte popis, který nastavení stručně charakterizuje, a další důležité podrobnosti.
    - **Platforma**: vyberte **Windows 10 a novější**.
    - **Typ profilu**: vyberte **vlastní**.

4. V nabídce **Vlastní nastavení OMA-URI** vyberte **Přidat**. Zadejte následující nastavení:

    - **Název:** Zadejte jedinečný název nastavení OMA-URI, abyste ho v seznamu poznali.
    - **Popis:** Zadejte popis, který nastavení stručně charakterizuje, a další důležité podrobnosti.
    - **OMA-URI** (rozlišuje velká a malá písmena): Zadejte nastavení OMA-URI, které chcete použít.
    - **Datový typ**: vyberte datový typ, který budete používat pro toto nastavení OMA-URI. Možnosti:

        - String
        - Řetězec (soubor XML)
        - Datum a čas
        - Celé číslo
        - Číslo s plovoucí desetinnou čárkou
        - Logická hodnota
        - Base64 (soubor)

    - **Hodnota:** Zadejte datovou hodnotu, kterou chcete přidružit k zadanému nastavení OMA-URI. Hodnota závisí na vybraném datovém typu. Pokud například vyberete položku **Datum a čas**, vyberte hodnotu z ovládacího prvku pro výběr data.

    Po přidání nastavení můžete vybrat **Exportovat**. **Export** vytvoří seznam všech hodnot, které jste přidali do souboru hodnot oddělených čárkou (.csv).

5. Výběrem **OK** uložte změny. Podle potřeby přidejte další nastavení.
6. Po dokončení vyberte **OK** > **vytvořit** a vytvořte profil Intune. Po dokončení se Váš profil zobrazí v seznamu **zařízení – konfigurační profily** .

## <a name="recommended-custom-settings"></a>Doporučená vlastní nastavení

Následující nastavení jsou užitečná pro zařízení s Windows Holographic for Business.

### <a name="allowfastreconnect"></a>[AllowFastReconnect](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect|Celé číslo<br/>0 – Nepovoluje se.<br/>1 – Povoluje se (výchozí).|

### <a name="allowupdateservice"></a>[AllowUpdateService](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/AllowUpdateService|Celé číslo<br/>0 – Služba aktualizací se nepovoluje. <br/>1 – Služba aktualizací se povoluje (výchozí).|

### <a name="allowvpn"></a>[AllowVPN](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Settings/AllowVPN|Celé číslo<br/>0 – Nepovoluje se.<br/>1 – Povoluje se (výchozí).|

### <a name="requireupdateapproval"></a>[RequireUpdateApproval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval|Toto nastavení je k dispozici v RS5 (Build 17763) a starší. Počínaje 19H1 (Build 18362) použijte [web Windows Update pro firmy](../protect/windows-update-for-business-configure.md).<br/><br/>Celé číslo<br/>0 – Není nakonfigurováno. Zařízení nainstaluje všechny použitelné aktualizace.<br/>1 – Zařízení nainstaluje jenom aktualizace, které jsou použitelné a jsou také v seznamu schválených aktualizací. Pokud chce oddělení IT řídit nasazení aktualizací na zařízení, třeba když je před nasazením nutné testování, nastavte tuto zásadu na 1.|

### <a name="scheduledinstalltime"></a>[ScheduledInstallTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime|Celé číslo 0–23, kde 0 = 12 dop. a 23 = 11 odp.<br/>Výchozí hodnota je 3.|

### <a name="updateserviceurl"></a>[UpdateServiceURL](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl|Toto nastavení je k dispozici v RS5 (Build 17763) a starší. Počínaje 19H1 (Build 18362) použijte [web Windows Update pro firmy](../protect/windows-update-for-business-configure.md).<br/><br/>String<br/>URL – Zařízení vyhledá aktualizace na serveru WSUS na zadané adrese URL.<br/>Nenakonfigurováno – Zařízení vyhledá aktualizace ve službě Microsoft Update.|

### <a name="approvedupdates"></a>[ApprovedUpdates](https://docs.microsoft.com/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Update/ApprovedUpdates/*GUID*<br/><br/>**Důležité**<br/>Musíte si přečíst smlouvy EULA k aktualizacím a přijmout je jménem vašich koncových uživatelů. Pokud tak neučiníte, dojde k porušení právních nebo smluvních závazků.|Uzel pro schválení aktualizací a přijetí smlouvy EULA jménem koncového uživatele<br/><br/>Další informace naleznete v tématu [Update CSP](https://docs.microsoft.com/windows/client-management/mdm/update-csp).|

### <a name="applicationlaunchrestrictions"></a>[ApplicationLaunchRestrictions](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |./Vendor/MSFT/AppLocker/ApplicationLaunchRestrictions/*Grouping*/*ApplicationType*/Policy<br/><br/>**Důležité**<br/>V článku o AppLocker CSP se používají příklady XML, které obsahují pomocné řídicí znaky. Pokud chcete nakonfigurovat nastavení s vlastními profily Intune, je nutné použít prostý XML.|String<br/>Další informace najdete v článku o [AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp).|

### <a name="deletionpolicy"></a>[DeletionPolicy](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy|Celé číslo<br/>0 – dojde k okamžitému odstranění, když se zařízení vrátí do stavu, ve kterém nemá žádné aktuálně aktivní uživatele.<br/>1 – dojde k odstranění při dosažení prahové hodnoty kapacity úložiště (výchozí nastavení).<br/>2 – dojde k odstranění při dosažení prahové hodnoty kapacity úložiště a prahové hodnoty neaktivity profilu.|

### <a name="enableprofilemanager"></a>[EnableProfileManager](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager|Logická hodnota<br/>True – povoleno<br/>False – zakázáno (výchozí)|

### <a name="profileinactivitythreshold"></a>[ProfileInactivityThreshold](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold|Celé číslo<br/>Výchozí hodnota je 30.|


### <a name="storagecapacitystartdeletion"></a>[StorageCapacityStartDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion|Celé číslo<br/>Výchozí hodnota je 25.|

### <a name="storagecapacitystopdeletion"></a>[StorageCapacityStopDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion|Celé číslo<br/>Výchozí hodnota je 50.|

## <a name="find-the-policies-you-can-configure"></a>Vyhledání zásad, které můžete nakonfigurovat

Úplný seznam všech poskytovatelů konfiguračních služeb (CSP), které Windows Holographic podporuje, najdete v části [Poskytovatelé CSP podporovaní ve Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens). Ne všechna nastavení jsou kompatibilní se všemi verzemi Windows Holographic. V tabulce [poskytovatelů konfiguračních služeb podporovaných systémem Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens) je u každého poskytovatele konfiguračních služeb seznam podporovaných verzí.

Intune navíc nepodporuje všechna nastavení, která jsou v tabulce [poskytovatelů konfiguračních služeb podporovaných systémem Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens). Pokud chcete zjistit, jestli Intune podporuje vámi požadované nastavení, otevřete si článek týkající se daného nastavení. Na každé stránce nastavení se zobrazuje podporovaná operace. Aby dané nastavení fungovalo s Intune, musí podporovat operace **Přidat** nebo **Nahradit**.

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Vytvořte si [vlastní profil na zařízeních s Windows 10](custom-settings-windows-10.md).
