---
title: Vlastní nastavení – zařízení s Windows holografickým pro firmy – Microsoft Intune | Microsoft Docs
description: Přidejte nebo vytvořte si vlastní profil, abyste mohli v Microsoft Intune použít nastavení OMA-URI pro zařízení s Windows Holographic for Business, včetně zařízení Microsoft Hololens. Můžete nakonfigurovat nastavení poskytovatele služeb konfigurace zásad (CSP) AllowFastReconnect, AllowVPN, AllowUpdateService, UpdateServiceURL, RequireUpdatesApproval, ApprovedUpdates a ApplicationLaunchRestrictions.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.article: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.topic: reference
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3928cd13b5368c8ab196a67669cb3a9f7d3fc2e9
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910022"
---
# <a name="use-custom-settings-for-windows-holographic-for-business-devices-in-intune"></a>Použití vlastního nastavení u zařízení s Windows Holographic for Business v Intune

V Microsoft Intune můžete použít vlastní profily k přidání nebo vytvoření vlastního nastavení pro zařízení s Windows Holographic for Business. Vlastní profily jsou funkcí Intune. Jsou navržené tak, aby bylo možné přidat nastavení a funkce zařízení, které nejsou integrované do Intune.

Vlastní profily pro Windows Holographic for Business používají nastavení OMA-URI (Open Mobile Alliance Uniform Resource Identifier) ke konfiguraci různých funkcí. Tato nastavení obvykle používají výrobci mobilních zařízení k řízení funkcí na zařízení.

Windows Holographic for Business zpřístupňuje řadu nastavení poskytovatelů konfiguračních služeb (CSP). Základní informace o CSP najdete v [úvodu o poskytovatelích konfiguračních služeb (CSP) pro IT specialisty](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers). Konkrétní poskytovatele CSP, které podporuje Windows Holographic, najdete v části [Poskytovatelé CSP podporovaní ve Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens).

Pokud hledáte konkrétní nastavení, nezapomeňte, že řada integrovaných nastavení je v [restriktivním profilu zařízení s Windows Holographic for Business](device-restrictions-windows-holographic.md). Takže možná nebude potřeba zadávat vlastní hodnoty.

V tomto článku si ukážeme, jak vytvořit vlastní profil pro zařízení s Windows Holographic for Business. Článek také obsahuje seznam doporučených nastavení OMA-URI.

## <a name="before-you-begin"></a>Než začnete

[Vytvořte vlastní profil Windows 10](custom-settings-configure.md#create-the-profile).

## <a name="custom-oma-uri-settings"></a>Vlastní nastavení OMA-URI

**Přidat**: zadejte následující nastavení:

- **Název:** Zadejte jedinečný název nastavení OMA-URI, abyste ho v seznamu poznali.
- **Popis:** Zadejte popis, který nastavení stručně charakterizuje, a další důležité podrobnosti.
- **OMA-URI** (rozlišuje velká a malá písmena): Zadejte nastavení OMA-URI, které chcete použít.
- **Datový typ**: vyberte datový typ, který budete používat pro toto nastavení OMA-URI. Možnosti:

  - Řetězec
  - Řetězec (soubor XML)
  - Datum a čas
  - Integer
  - Plovoucí desetinná čárka
  - Logická hodnota
  - Base64 (soubor)

- **Hodnota:** Zadejte datovou hodnotu, kterou chcete přidružit k zadanému nastavení OMA-URI. Hodnota závisí na vybraném datovém typu. Pokud například vyberete položku **Datum a čas**, vyberte hodnotu z ovládacího prvku pro výběr data.

Po přidání nastavení můžete vybrat **Exportovat**. **Export** vytvoří seznam všech hodnot, které jste přidali do souboru hodnot oddělených čárkou (.csv).

## <a name="recommended-custom-settings"></a>Doporučená vlastní nastavení

Následující nastavení jsou užitečná pro zařízení s Windows Holographic for Business.

### <a name="allowfastreconnect"></a>[AllowFastReconnect](/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect|Integer<br/>0 – Nepovoluje se.<br/>1 – Povoluje se (výchozí).|

### <a name="allowupdateservice"></a>[AllowUpdateService](/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/AllowUpdateService|Integer<br/>0 – Služba aktualizací se nepovoluje. <br/>1 – Služba aktualizací se povoluje (výchozí).|

### <a name="allowvpn"></a>[AllowVPN](/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Settings/AllowVPN|Integer<br/>0 – Nepovoluje se.<br/>1 – Povoluje se (výchozí).|

### <a name="requireupdateapproval"></a>[RequireUpdateApproval](/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval|Toto nastavení je k dispozici v RS5 (Build 17763) a starší. Počínaje 19H1 (Build 18362) použijte [web Windows Update pro firmy](../protect/windows-update-for-business-configure.md).<br/><br/>Integer<br/>0 – Není nakonfigurováno. Zařízení nainstaluje všechny použitelné aktualizace.<br/>1 – Zařízení nainstaluje jenom aktualizace, které jsou použitelné a jsou také v seznamu schválených aktualizací. Pokud chce oddělení IT řídit nasazení aktualizací na zařízení, třeba když je před nasazením nutné testování, nastavte tuto zásadu na 1.|

### <a name="scheduledinstalltime"></a>[ScheduledInstallTime](/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime|Celé číslo 0–23, kde 0 = 12 dop. a 23 = 11 odp.<br/>Výchozí hodnota je 3.|

### <a name="updateserviceurl"></a>[UpdateServiceURL](/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl|Toto nastavení je k dispozici v RS5 (Build 17763) a starší. Počínaje 19H1 (Build 18362) použijte [web Windows Update pro firmy](../protect/windows-update-for-business-configure.md).<br/><br/>Řetězec<br/>URL – Zařízení vyhledá aktualizace na serveru WSUS na zadané adrese URL.<br/>Nenakonfigurováno – Zařízení vyhledá aktualizace ve službě Microsoft Update.|

### <a name="approvedupdates"></a>[ApprovedUpdates](/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |---|---|
> |./Vendor/MSFT/Update/ApprovedUpdates/*GUID*<br/><br/>**Důležité upozornění**<br/>Musíte si přečíst smlouvy EULA k aktualizacím a přijmout je jménem vašich koncových uživatelů. Pokud tak neučiníte, dojde k porušení právních nebo smluvních závazků.|Uzel pro schválení aktualizací a přijetí smlouvy EULA jménem koncového uživatele<br/><br/>Další informace naleznete v tématu [Update CSP](/windows/client-management/mdm/update-csp).|

### <a name="applicationlaunchrestrictions"></a>[ApplicationLaunchRestrictions](/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |/Vendor/MSFT/AppLocker/ApplicationLaunchRestrictions/*seskupení* / *typu ApplicationType*/Policy<br/><br/>**Důležité upozornění**<br/>V článku o AppLocker CSP se používají příklady XML, které obsahují pomocné řídicí znaky. Pokud chcete nakonfigurovat nastavení s vlastními profily Intune, je nutné použít prostý XML.|Řetězec<br/>Další informace najdete v článku o [AppLocker CSP](/windows/client-management/mdm/applocker-csp).|

### <a name="deletionpolicy"></a>[DeletionPolicy](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy|Integer<br/>0 – dojde k okamžitému odstranění, když se zařízení vrátí do stavu, ve kterém nemá žádné aktuálně aktivní uživatele.<br/>1 – dojde k odstranění při dosažení prahové hodnoty kapacity úložiště (výchozí nastavení).<br/>2 – dojde k odstranění při dosažení prahové hodnoty kapacity úložiště a prahové hodnoty neaktivity profilu.|

### <a name="enableprofilemanager"></a>[EnableProfileManager](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager|Logická hodnota<br/>True – povoleno<br/>False – zakázáno (výchozí)|

### <a name="profileinactivitythreshold"></a>[ProfileInactivityThreshold](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold|Integer<br/>Výchozí hodnota je 30.|

### <a name="storagecapacitystartdeletion"></a>[StorageCapacityStartDeletion](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion|Integer<br/>Výchozí hodnota je 25.|

### <a name="storagecapacitystopdeletion"></a>[StorageCapacityStopDeletion](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datový typ|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion|Integer<br/>Výchozí hodnota je 50.|

## <a name="find-the-policies-you-can-configure"></a>Vyhledání zásad, které můžete nakonfigurovat

Úplný seznam všech poskytovatelů konfiguračních služeb (CSP), které Windows Holographic podporuje, najdete v části [Poskytovatelé CSP podporovaní ve Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens). Ne všechna nastavení jsou kompatibilní se všemi verzemi Windows Holographic. V tabulce [poskytovatelů konfiguračních služeb podporovaných systémem Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens) je u každého poskytovatele konfiguračních služeb seznam podporovaných verzí.

Intune navíc nepodporuje všechna nastavení, která jsou v tabulce [poskytovatelů konfiguračních služeb podporovaných systémem Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens). Pokud chcete zjistit, jestli Intune podporuje vámi požadované nastavení, otevřete si článek týkající se daného nastavení. Na každé stránce nastavení se zobrazuje podporovaná operace. Aby dané nastavení fungovalo s Intune, musí podporovat operace **Přidat** nebo **Nahradit**.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

Vytvořte si [vlastní profil na zařízeních s Windows 10](custom-settings-windows-10.md).

Přečtěte si další informace o [vlastních profilech](custom-settings-configure.md) v Intune.