---
title: Řešení potíží s instalací aplikace
titleSuffix: Configuration Manager
description: Řešení potíží s instalací aplikace pro připojení klienta Configuration Manager
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 75f47456-cd8d-4c83-8dc5-98b336a7c6c8
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 7e02c642c95952c8751f03a8e1cb8838feff1155
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564039"
---
# <a name="troubleshoot-application-installation-for-devices-uploaded-to-the-admin-center-preview"></a>Řešení potíží s instalací aplikace pro zařízení odeslaná do centra pro správu (Preview)
<!--6374854, 6521921-->
*Platí pro: Configuration Manager (Current Branch)*

K řešení potíží s Configuration Manager aplikacemi v centru pro správu Microsoft Endpoint Manageru použijte následující postup:

> [!Important]
> Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a>Běžné chyby v centru pro správu Microsoft Endpoint Manageru

Při zobrazení nebo instalaci aplikací z centra pro správu Microsoft Endpoint Manageru můžete spustit jednu z těchto chyb.  

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> V Azure Active Directory chybí potřebná konfigurace.

**Chybová zpráva:** V Azure Active Directory chybí potřebná konfigurace. Nezapomeňte připojit Configuration Manager lokality k vašemu tenantovi Azure a přiřadit správnou roli uživatele v Azure AD.

**Možná příčina:** V uživatelském účtu nejspíš chybí role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD. Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny. Změny tohoto oprávnění mohou trvat až hodinu.

### <a name="unable-to-get-application-information"></a><a name="bkmk_noinfo"></a> Nepovedlo se získat informace o aplikaci.

**Chybová zpráva 1:** Nelze získat informace o aplikaci. Ujistěte se, že je nakonfigurované zjišťování uživatelů Azure AD a AD a že je uživatel zjištěn v obou. Ověřte, zda má uživatel správná oprávnění v Configuration Manager.

**Možné příčiny:** Tato chyba je obvykle způsobena problémem s účtem správce. Níže jsou uvedené nejběžnější problémy s účtem administrativního uživatele:

1. Použijte stejný účet pro přihlášení k centru pro správu. Místní identita musí být synchronizovaná s cloudovou identitou a musí se shodovat.
1. Ověřte, že účet má oprávnění **ke čtení** pro **kolekci** zařízení v Configuration Manager.
1. Ujistěte se, že Configuration Manager zjistil účet administrativního uživatele, který používáte. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Vyberte uzel **Uživatelé** a vyhledejte svůj uživatelský účet.

    Pokud váš účet není uvedený v uzlu **Uživatelé** , Projděte si část konfigurace [zjišťování uživatelů služby Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)v lokalitě.

1. Ověřte data zjišťování. Vyberte svůj uživatelský účet. Na pásu karet na kartě **Domů** vyberte **vlastnosti**. V okně Vlastnosti potvrďte následující data zjišťování:

    - **ID tenanta Azure Active Directory**: Tato hodnota by měla být identifikátorem GUID pro TENANTA Azure AD.
    - **ID uživatele Azure Active Directory**: Tato hodnota by měla být identifikátorem GUID pro tento účet ve službě Azure AD.
    - **Hlavní název uživatele**: formát této hodnoty je user@domain . Například, `jqpublic@contoso.com`.

    Pokud jsou vlastnosti služby Azure AD prázdné, ověřte konfiguraci [zjišťování uživatelů služby Azure AD](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).

### <a name="unexpected-error-occurred"></a><a name="bkmk_1603"></a> Stala se neočekávaná chyba.

**Chybová zpráva:** Stala se neočekávaná chyba.

#### <a name="error-code-500-with-an-unexpected-error-occurred-message"></a>Kód chyby 500 s neočekávanou chybou při výskytu zprávy

1. Pokud se zobrazí `System.Security.SecurityException` v **protokolu AdminService. log**, ověřte, že vaše hlavní uživatelské jméno (UPN) zjištěné [zjišťováním uživatelů služby Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) není nastavené na hlavní název uživatele (UPN), nikoli na místní hlavní název uživatele (UPN). Je také přijatelná prázdná hodnota hlavního názvu uživatele (UPN), která znamená, že se používá název domény zjištěné službou Active Directory. Pokud se zobrazí název UPN jenom pro Cloud (například onmicrosoft.com), který není platným hlavním názvem uživatele (contoso.com), máte problém a možná budete muset [nastavit příponu hlavního názvu uživatele (UPN) ve službě Active Directory](/office365/enterprise/prepare-a-non-routable-domain-for-directory-synchronization#add-upn-suffixes-and-update-your-users-to-them).
1. Pokud se v **protokolu AdminService. log**zobrazí tato chyba, v [centru pro správu Microsoft Endpoint Manageru se vyprší doba instalace KB4576782 – okno aplikace](https://support.microsoft.com/help/4576782) .
   ```log 
   System.Data.Entity.Core.EntityCommandExecutionException: An error occurred while executing the command definition. See the inner exception for details.
   System.Data.SqlClient.SqlException: Execution Timeout Expired.  The timeout period elapsed prior to completion of the operation or the server is not responding.
   System.ComponentModel.Win32Exception: The wait operation timed out
   ```

#### <a name="error-code-3-with-an-unexpected-error-occurred-message"></a>Kód chyby 3 s neočekávanou chybou při výskytu zprávy

Služba správy není spuštěná nebo není nainstalovaná služba IIS. Služba IIS musí být nainstalována na počítači poskytovatele. Další informace najdete v tématu [předpoklady pro službu správy](../develop/adminservice/overview.md#prerequisites).

#### <a name="other-possible-causes-of-unexpected-errors"></a>Další možné příčiny neočekávaných chyb

Neočekávané chyby jsou obvykle způsobeny buď [spojovacím bodem služby](../core/servers/deploy/configure/about-the-service-connection-point.md), [službou správy](../develop/adminservice/overview.md)nebo problémy s připojením.

1. Ověřte, zda je spojovací bod služby připojen ke cloudu pomocí **protokolu CMGatewayNotificationWorker. log**.
1. Ověřte, zda je služba pro správu v pořádku, kontrolou součásti SMS_REST_PROVIDER z monitorování součástí lokality v centrální lokalitě.
1. Služba IIS musí být nainstalována na počítači poskytovatele. Další informace najdete v tématu [předpoklady pro službu správy](../develop/adminservice/overview.md#prerequisites).


### <a name="the-site-information-hasnt-yet-synchronized"></a><a name="bkmk_sync"></a> Informace o lokalitě zatím nebyly synchronizovány.

**Chybová zpráva:** Informace o lokalitě ještě nejsou synchronizované z Configuration Manager do centra pro správu Microsoft Endpoint Manageru. Po připojení lokality k vašemu tenantovi Azure počkejte až 15 minut.

**Možné příčiny:**
- K této chybě obvykle dochází při připojování nového připojení ke klientovi. Počkat až hodinu, než se informace synchronizují.
- Tato chyba se může zobrazit také v případě, že lokalita centrální správy byla upgradována na novou verzi Configuration Manager, ale některé podřízené primární lokality ještě nebyly upgradovány.

### <a name="application-shows-as-installed-after-creating-a-new-deployment"></a><a name="bkmk_installed"></a> Aplikace se zobrazí jako nainstalovaná po vytvoření nového nasazení.

**Příznak:** Aplikace se v centru pro správu Microsoft Endpoint Manageru zobrazí jako nainstalovaná, protože po vytvoření nového dostupného zařízení se vyžaduje nasazení schválení nebo nasazení, které je k dispozici uživatelem.

**Možná příčina:** Stav aplikace zobrazený pro toto zařízení je z jiného aktivního nebo dřívějšího nasazení.

### <a name="errors-when-searching-or-retrying-an-installation"></a><a name="bkmk_hfru"></a> Chyby při hledání nebo opakování instalace

**Příznak:** Při provádění následujících akcí dojde k chybám:
- Použití vyhledávání
- Vybrat **opakovanou instalaci**

**Možná příčina:**  Ujistěte se, že je nainstalovaná [kumulativní aktualizace pro Microsoft Endpoint Configuration Manager verze 2002](https://support.microsoft.com/help/4560496/) a odpovídající verze konzoly. Další informace najdete v tématu [předpoklady pro instalaci aplikace z centra pro správu](applications.md#prerequisites).

## <a name="known-issues"></a>Známé problémy

### <a name="application-installation-times-out-if-application-requires-restart"></a>Časový limit instalace aplikace vypršel, pokud aplikace vyžaduje restart.

**Scénář:** Pokud používáte Configuration Manager verze 2002 a aplikace vyžaduje restart k dokončení procesu instalace, může dojít k vypršení časového limitu instalace.

**Příznaky:** Uživateli se zobrazí `restart pending` oznámení a v centru softwaru. V centru pro správu Microsoft Endpoint Manageru zůstává aplikace ve `Installing` stavu.  

**Alternativní řešení:** Jakmile uživatel zařízení restartuje, zobrazí se v centru pro správu správný stav.

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]


## <a name="next-steps"></a>Další kroky

[Odstraňování potíží s připojením tenanta](troubleshoot.md)