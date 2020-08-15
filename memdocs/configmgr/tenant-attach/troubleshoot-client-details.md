---
title: Řešení potíží s podrobnostmi klienta
titleSuffix: Configuration Manager
description: Řešení potíží s podrobnostmi klienta pro připojení klienta Configuration Manager
ms.date: 07/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 9ca99afa60ed5f8b9a1491381767ec4f6359826f
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252499"
---
# <a name="troubleshoot-configmgr-client-details-in-the-admin-center-preview"></a>Řešení potíží s podrobnostmi klienta nástroje ConfigMgr v centru pro správu (Preview)
<!--6374854, 6521921-->
*Platí pro: Configuration Manager (Current Branch)*

K řešení potíží s podrobnostmi klienta nástroje ConfigMgr v centru pro správu Microsoft Endpoint Manager použijte následující informace:

> [!Important]
> Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a>Běžné chyby v centru pro správu Microsoft Endpoint Manageru

Při prohlížení podrobností klienta nástroje ConfigMgr můžete spustit jednu z těchto chyb.  

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> V Azure Active Directory chybí potřebná konfigurace.

**Chybová zpráva:** V Azure Active Directory chybí potřebná konfigurace. Nezapomeňte připojit Configuration Manager lokality k vašemu tenantovi Azure a přiřadit správnou roli uživatele v Azure AD.

**Možná příčina:** V uživatelském účtu nejspíš chybí role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD. Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny. Změny tohoto oprávnění mohou trvat až hodinu.

### <a name="unable-to-get-device-or-collection-information"></a><a name="bkmk_noinfo"></a> Nepovedlo se získat informace o zařízení nebo kolekci.

**Chybová zpráva 1:** Nepovedlo se získat informace o podrobnostech klienta (nebo shromažďování). Ujistěte se, že je nakonfigurované zjišťování uživatelů Azure AD a AD a že je uživatel zjištěn v obou. Ověřte, zda má uživatel správná oprávnění v Configuration Manager.

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

**Možné příčiny:** Neočekávané chyby jsou obvykle způsobeny buď [spojovacím bodem služby](../core/servers/deploy/configure/about-the-service-connection-point.md), [službou správy](../develop/adminservice/overview.md)nebo problémy s připojením.

1. Ověřte, zda je spojovací bod služby připojen ke cloudu pomocí **protokolu CMGatewayNotificationWorker. log**.
1. Ověřte, zda je služba pro správu v pořádku, kontrolou součásti SMS_REST_PROVIDER z monitorování součástí lokality v centrální lokalitě.
1. Služba IIS musí být nainstalována na počítači poskytovatele. Další informace najdete v tématu [předpoklady pro službu správy](../develop/adminservice/overview.md#prerequisites).
1. Ověřte, zda jsou hodiny spojovacího bodu služby synchronizovány. Pokud je hodiny spojovacího bodu služby mírně na konci, použijte [kumulativní aktualizaci KB4563473-Update pro Configuration Manager problémy s připojením klienta ve verzi 2002](https://support.microsoft.com/help/4563473). Ověřte všechny chyby v počítači poskytovatele na **AdminService. log** .

## <a name="known-issues"></a>Známé problémy

### <a name="gettingresultstimedout"></a>Při získávání výsledků vypršel časový limit.

**Scénář:** Pokud máte bod připojení ke vzdálené službě a nainstalovali jste 2002 brzké aktualizace do 30. března 2020, v centru pro správu se zobrazí chyba s časovým limitem.

**Chybová zpráva:** Při získávání výsledků vypršel časový limit. Ujistěte se, že spojovací bod služby Configuration Manager je funkční a má připojení ke cloudu.

**Alternativní řešení:** Zkopírujte `Microsoft.ConfigurationManagement.ManagementProvider.dll` složku ze serveru lokality `bin\x64` do složky bodu připojení vzdálené služby `bin\x64` .  Restartujte `SMS_EXECUTIVE` službu na serveru bodu připojení služby.

### <a name="boundary-groups-list-is-empty"></a>Seznam skupin hranic je prázdný.

**Chybová zpráva**: nenašly se žádné skupiny hranic nebo uživatel nemusí mít oprávnění k zobrazení informací o skupině hranic.

Prázdný seznam je známý problém pro Configuration Manager verze 2002, když máte hierarchii Configuration Managerch lokalit.

:::image type="content" source="media/6024387-known-issue-device-details.png" alt-text="Seznam skupin hranic je prázdný." lightbox="media/6024387-known-issue-device-details.png":::

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## <a name="next-steps"></a>Další kroky

[Odstraňování potíží s připojením tenanta](troubleshoot.md)
