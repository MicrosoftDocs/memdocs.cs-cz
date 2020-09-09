---
title: Řešení potíží s CMPivot pro zařízení odeslaná do centra pro správu
titleSuffix: Configuration Manager
description: Řešení potíží s CMPivot pro připojení klienta Configuration Manager
ms.date: 09/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 86f97154-c9fc-4efd-9d49-4a253cef5953
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d1ca270bc1095e1596f5e725c16a97f4e42e4411
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564289"
---
# <a name="troubleshoot-cmpivot-preview-for-devices-uploaded-to-the-admin-center"></a>Řešení potíží s CMPivot (Preview) pro zařízení odeslaná do centra pro správu
<!--6024392-->
*Platí pro: Configuration Manager (Current Branch)*

K řešení potíží s CMPivot v centru pro správu Microsoft Endpoint Manageru použijte následující postup:

> [!Important]
> Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

## <a name="common-issues"></a>Běžné problémy

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> V Azure Active Directory chybí potřebná konfigurace.

**Chybová zpráva:** V Azure Active Directory chybí potřebná konfigurace. Nezapomeňte připojit Configuration Manager lokality k vašemu tenantovi Azure a přiřadit správnou roli uživatele v Azure AD.

**Možná příčina:** V uživatelském účtu nejspíš chybí role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD. Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny. Změny tohoto oprávnění mohou trvat až hodinu.

### <a name="unable-to-get-device-information"></a><a name="bkmk_noinfo"></a> Nepovedlo se získat informace o zařízení.

**Chybová zpráva 1:** Nepovedlo se získat informace o zařízení. Ujistěte se, že je nakonfigurované zjišťování uživatelů Azure AD a AD a že je uživatel zjištěn v obou. Ověřte, zda má uživatel správná oprávnění v Configuration Manager.

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


### <a name="not-authorized-to-view-query-results"></a><a name="bkmk_rbac"></a> Neautorizováno pro zobrazení výsledků dotazu

**Chybová zpráva:** Nemáte oprávnění k zobrazení výsledků dotazu. Ověřte, že vám byla udělena oprávnění pro CMPivot v Configuration Manager

**Možné příčiny:** Ověřte, jestli má uživatelský účet oprávnění pro CMPivot. Další informace najdete v tématu [oprávnění pro CMPivot](cmpivot-start.md#permissions).

#### <a name="other-possible-causes-of-unexpected-errors"></a><a name="bkmk_other"></a> Další možné příčiny neočekávaných chyb

Neočekávané chyby jsou obvykle způsobeny buď [spojovacím bodem služby](../core/servers/deploy/configure/about-the-service-connection-point.md), [službou správy](../develop/adminservice/overview.md)nebo problémy s připojením.

1. Ověřte, zda je spojovací bod služby připojen ke cloudu pomocí **protokolu CMGatewayNotificationWorker. log**.
1. Ověřte, zda je služba pro správu v pořádku, kontrolou součásti SMS_REST_PROVIDER z monitorování součástí lokality v centrální lokalitě.
1. Služba IIS musí být nainstalována na počítači poskytovatele. Další informace najdete v tématu [předpoklady pro službu správy](../develop/adminservice/overview.md#prerequisites).

## <a name="known-issues"></a>Známé problémy

### <a name="inconsistent-results-for-some-operators-with-configuration-manager-version-2002"></a>Nekonzistentní výsledky pro některé operátory s Configuration Manager verze 2002
<!--7784718, 7884272-->
Pokud používáte CMPivot z centra pro správu Microsoft Endpoint Manageru s Configuration Manager verze 2002, můžete získat nekonzistentní výsledky pro následující operátory:

- Vytvořit souhrn podle
- Take
- Řadit podle
- Nahoře
- Počet
- Distinct

**Řešení**: instalace [dotazů KB4578123-CMPivot vrátí neočekávané výsledky v Configuration Manager aktuální větvi, verze 2002](https://support.microsoft.com/help/4578123).

### <a name="when-the-sms-provider-is-remote-from-the-cas-you-may-encounter-an-internal-server-error-from-the-admin-console"></a><a name="bkmk_dblhop"></a> Když je poskytovatel serveru SMS vzdálený od certifikačních autorit, může dojít k vnitřní chybě serveru z konzoly pro správu.

**Chybová zpráva:** Kód chyby on-Prem: 500 interní chyba serveru

**Scénář 1:** Pokud používáte Configuration Manager verze 2002 a pro certifikační autority existuje vzdálený poskytovatel, může dojít k vnitřní chybě serveru z konzoly pro správu.

**Scénář 2:** Při spuštění Configuration Manager verze 2006 se tato chyba může zobrazit i v případě, že spojovacímu bodu služby se nepovede připojit k poskytovateli v primární lokalitě a vrátit se k poskytovateli pro certifikační autority. 

**Scénář 3:** Pokud byly certifikační autority upgradovány na verzi 2006, ale ještě nebyla upgradována primární lokalita, požadavky budou směrovány prostřednictvím poskytovatele CAS. Pokud je zprostředkovatel vzdálený, může dojít k vnitřní chybě serveru z konzoly pro správu. 

**Alternativní řešení:** Postupujte podle pokynů pro [certifikační autority](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) s scénářem vzdáleného poskytovatele v článku CMPivot, abyste mohli vyřešit tento scénář dvojího směrování.


[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## <a name="next-steps"></a>Další kroky

[Odstraňování potíží s připojením tenanta](troubleshoot.md)
