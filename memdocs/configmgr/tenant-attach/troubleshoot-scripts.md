---
title: Řešení potíží se skripty pro zařízení odeslaná do centra pro správu
titleSuffix: Configuration Manager
description: Řešení potíží se skripty pro připojení klienta Configuration Manager
ms.date: 09/18/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: a0eb1e8f-2c85-4f48-a0b5-945b3e5f63f3
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: b42663e649f50d1a785bf929d0b03fb4d2eb0632
ms.sourcegitcommit: af4fc4f928203c1bfdb27499a56c91fe0ebae854
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2020
ms.locfileid: "90803273"
---
# <a name="troubleshoot-scripts-preview-for-devices-uploaded-to-the-admin-center"></a>Řešení potíží se skripty (Preview) pro zařízení odeslaná do centra pro správu
<!--6024392-->
*Platí pro: Configuration Manager (Current Branch)*

K odstraňování potíží se skripty v centru pro správu Microsoft Endpoint Manageru použijte následující postup:

> [!Important]
> Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

## <a name="common-issues"></a>Běžné problémy

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> V Azure Active Directory chybí potřebná konfigurace.

**Chybová zpráva:** V Azure Active Directory chybí potřebná konfigurace. Nezapomeňte připojit Configuration Manager lokality k vašemu tenantovi Azure a přiřadit správnou roli uživatele v Azure AD.

**Možná příčina:** V uživatelském účtu nejspíš chybí role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD. Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny. Změny tohoto oprávnění mohou trvat až hodinu.

### <a name="configuration-manager-doesnt-meet-the-minimum-version-prerequisite"></a><a name="bkmk_version"></a> Configuration Manager nesplňuje požadavek na minimální verzi.

**Chybová zpráva:** Configuration Manager nesplňuje požadavky na minimální verzi.

**Možné příčiny:** Na vašich Configuration Managerch lokalitách není spuštěná minimální verze Configuration Manager 2006 s [KB4580678-tenant připojení pro Configuration Manager aktuální větev, verze 2006](https://support.microsoft.com/help/4580678) nainstalovaná. Zkontrolujte:
 - Je nainstalovaná verze Configuration Manager 2006 nebo vyšší.
 - Tato [KB4580678](https://support.microsoft.com/help/4580678) na webech, na kterých běží Configuration Manager verze 2006.
 - Aby všechny lokality v hierarchii splňovaly výše uvedené minimální požadavky.

### <a name="unable-to-get-scripts-information"></a><a name="bkmk_403"></a> Nepovedlo se získat informace o skriptech.

**Chybová zpráva:** Nepovedlo se získat informace o skriptech. Ujistěte se, že jsou nakonfigurovaná zjišťování uživatelů Azure AD a AD a že uživatelský účet, který přistupuje k funkcím připojení tenanta z centra pro správu Microsoft Endpoint Manageru, se zjistí v obou. Ověřte, zda má uživatel správná oprávnění v Configuration Manager.

**Možné příčiny:** Tato chyba je obvykle způsobena problémem s účtem správce. Níže jsou uvedené nejběžnější problémy s účtem administrativního uživatele:

1. Použijte stejný účet pro přihlášení k centru pro správu. Místní identita musí být synchronizovaná s cloudovou identitou a musí se shodovat.
1. Ověřte, že účet má oprávnění **ke čtení** pro **kolekci** zařízení v Configuration Manager.
1. Ověřte, že má účet oprávnění **číst prostředek** pro **kolekci** zařízení v Configuration Manager.
1. Ujistěte se, že Configuration Manager zjistil účet administrativního uživatele, který používáte pro přístup k funkcím připojení klienta v rámci centra pro správu služby Microsoft Endpoint Manager. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Vyberte uzel **Uživatelé** a vyhledejte svůj uživatelský účet.

    Pokud váš účet není uvedený v uzlu **Uživatelé** , Projděte si část konfigurace [zjišťování uživatelů služby Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)v lokalitě.

1. Ověřte data zjišťování. Vyberte svůj uživatelský účet. Na pásu karet na kartě **Domů** vyberte **vlastnosti**. V okně Vlastnosti potvrďte následující data zjišťování:

    - **ID tenanta Azure Active Directory**: Tato hodnota by měla být identifikátorem GUID pro TENANTA Azure AD.
    - **ID uživatele Azure Active Directory**: Tato hodnota by měla být identifikátorem GUID pro tento účet ve službě Azure AD.
    - **Hlavní název uživatele**: formát této hodnoty je user@domain . Například, `jqpublic@contoso.com`.

    Pokud jsou vlastnosti služby Azure AD prázdné, ověřte konfiguraci [zjišťování uživatelů služby Azure AD](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).


### <a name="unable-to-get-device-information"></a><a name="bkmk_noinfo"></a> Nepovedlo se získat informace o zařízení.

**Chybová zpráva:** Nepovedlo se získat informace o zařízení. Ujistěte se, že je nakonfigurované zjišťování uživatelů Azure AD a AD a že je uživatel zjištěn v obou. Ověřte, zda má uživatel správná oprávnění v Configuration Manager.

**Možná příčina:** Ujistěte se, že Configuration Manager zjistil účet administrativního uživatele, který používáte pro přístup k funkcím připojení klienta v rámci centra pro správu služby Microsoft Endpoint Manager. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Vyberte uzel **Uživatelé** a vyhledejte svůj uživatelský účet.

   Pokud váš účet není uvedený v uzlu **Uživatelé** , Projděte si část konfigurace [zjišťování uživatelů služby Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)v lokalitě.

1. Ověřte data zjišťování. Vyberte svůj uživatelský účet. Na pásu karet na kartě **Domů** vyberte **vlastnosti**. V okně Vlastnosti potvrďte následující data zjišťování:

    - **ID tenanta Azure Active Directory**: Tato hodnota by měla být identifikátorem GUID pro TENANTA Azure AD.
    - **ID uživatele Azure Active Directory**: Tato hodnota by měla být identifikátorem GUID pro tento účet ve službě Azure AD.
    - **Hlavní název uživatele**: formát této hodnoty je user@domain . Například, `jqpublic@contoso.com`.

    Pokud jsou vlastnosti služby Azure AD prázdné, ověřte konfiguraci [zjišťování uživatelů služby Azure AD](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).


### <a name="unexpected-error-occurred"></a><a name="bkmk_1603"></a> Stala se neočekávaná chyba.

**Chybová zpráva:** Stala se neočekávaná chyba.

#### <a name="possible-cause"></a>Možná příčina

Ověřte, že má účet oprávnění **číst prostředek** pro **kolekci** zařízení v Configuration Manager.

#### <a name="error-code-500-with-an-unexpected-error-occurred-message"></a>Kód chyby 500 s neočekávanou chybou při výskytu zprávy

Pokud se zobrazí `System.Security.SecurityException` v **protokolu AdminService. log**, ověřte, že vaše hlavní uživatelské jméno (UPN) zjištěné [zjišťováním uživatelů služby Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) není nastavené na hlavní název uživatele (UPN), nikoli na místní hlavní název uživatele (UPN). Je také přijatelná prázdná hodnota hlavního názvu uživatele (UPN), která znamená, že se používá název domény zjištěné službou Active Directory. Pokud se zobrazí název UPN jenom pro Cloud (například onmicrosoft.com), který není platným hlavním názvem uživatele (contoso.com), máte problém a možná budete muset [nastavit příponu hlavního názvu uživatele (UPN) ve službě Active Directory](/office365/enterprise/prepare-a-non-routable-domain-for-directory-synchronization#add-upn-suffixes-and-update-your-users-to-them).


#### <a name="other-possible-causes-of-unexpected-errors"></a>Další možné příčiny neočekávaných chyb

Neočekávané chyby jsou obvykle způsobeny buď [spojovacím bodem služby](../core/servers/deploy/configure/about-the-service-connection-point.md), [službou správy](../develop/adminservice/overview.md)nebo problémy s připojením.

1. Ověřte, zda je spojovací bod služby připojen ke cloudu pomocí **protokolu CMGatewayNotificationWorker. log**.
1. Ověřte, zda je služba pro správu v pořádku, kontrolou součásti SMS_REST_PROVIDER z monitorování součástí lokality v centrální lokalitě.
1. Služba IIS musí být nainstalována na počítači poskytovatele. Další informace najdete v tématu [předpoklady pro službu správy](../develop/adminservice/overview.md#prerequisites).

## <a name="known-issues"></a>Známé problémy

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]
