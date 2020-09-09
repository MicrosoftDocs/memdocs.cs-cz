---
title: Řešení potíží s Průzkumníkem prostředků
titleSuffix: Configuration Manager
description: Řešení potíží s Průzkumníkem prostředků pro Configuration Manager připojení klienta
ms.date: 09/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 05829d36-2cbf-4921-bf4b-cfcdef4cfcc1
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: a93127e28d451c74828c4362fa00418e35c6e56f
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564293"
---
# <a name="troubleshoot-resource-explorer-for-devices-uploaded-to-the-admin-center-preview"></a>Řešení potíží s Průzkumníkem prostředků pro zařízení odeslaná do centra pro správu (Preview)
<!--6479284-->
*Platí pro: Configuration Manager (Current Branch)*

K řešení potíží s Průzkumníkem prostředků pro zařízení nástroje ConfigMgr v centru pro správu Microsoft Endpoint Manager použijte následující postup:

> [!Important]
> Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a>Běžné chyby v centru pro správu Microsoft Endpoint Manageru

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a> V Azure Active Directory chybí potřebná konfigurace.

**Chybová zpráva:** V Azure Active Directory chybí potřebná konfigurace. Nezapomeňte připojit Configuration Manager lokality k vašemu tenantovi Azure a přiřadit správnou roli uživatele v Azure AD.

**Možná příčina:** V uživatelském účtu nejspíš chybí role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD. Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny. Změny tohoto oprávnění mohou trvat až hodinu.

### <a name="unable-to-get-resource-information"></a><a name="bkmk_noinfo"></a> Nepovedlo se získat informace o prostředku.

**Chybová zpráva 1:** Nelze získat informace o prostředku. Ujistěte se, že je nakonfigurované zjišťování uživatelů Azure AD a AD a že je uživatel zjištěn v obou. Ověřte, zda má uživatel správná oprávnění v Configuration Manager.

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

### <a name="the-site-information-hasnt-yet-synchronized"></a><a name="bkmk_sync"></a> Informace o lokalitě zatím nebyly synchronizovány.

**Chybová zpráva:** Informace o lokalitě ještě nejsou synchronizované z Configuration Manager do centra pro správu Microsoft Endpoint Manageru. 

**Možné příčiny:**
- K této chybě obvykle dochází při připojování nového připojení ke klientovi. Počkejte hodinu, než se informace synchronizují.
- Tato chyba se může zobrazit také v případě, že lokalita centrální správy byla upgradována na novou verzi Configuration Manager, ale některé podřízené primární lokality ještě nebyly upgradovány.

### <a name="unable-to-load-inventory-classes"></a><a name="bkmk_load"></a> Nejde načíst třídy inventáře.

**Chybová zpráva:** Nejde načíst třídy inventáře pro vaše prostředí.

**Možné příčiny:**

- Seznam entit nemusí být nahraný z místního prostředí. Počkejte hodinu a pak se podívejte, jestli chyba přetrvává.
- Bylo pravděpodobně zadáno neplatné **ID tenanta** nebo **ID hierarchie** . Zkontrolujte spojovací bod služby a ujistěte se, že funguje.
- Nelze úspěšně spustit dotaz pro získání tříd. Počkejte 15 minut, než se zobrazí, jestli chyba přetrvává.

### <a name="failed-to-get-inventory-classes-with-data"></a><a name="bkmk_get"></a> Nepovedlo se získat třídy inventáře s daty.

**Chybová zpráva:** Nepovedlo se získat třídy inventáře s daty. Místní Chyba 500.

**Možné příčiny:** Neočekávané chyby jsou obvykle způsobeny buď [spojovacím bodem služby](../core/servers/deploy/configure/about-the-service-connection-point.md), [službou správy](../develop/adminservice/overview.md)nebo problémy s připojením.

1. Ověřte, zda je spojovací bod služby připojen ke cloudu pomocí **protokolu CMGatewayNotificationWorker. log**.
1. Ověřte, zda je služba pro správu v pořádku, kontrolou součásti SMS_REST_PROVIDER z monitorování součástí lokality v centrální lokalitě.
1. Služba IIS musí být nainstalována na počítači poskytovatele. Další informace najdete v tématu [předpoklady pro službu správy](../develop/adminservice/overview.md#prerequisites).

### <a name="the-user-does-not-have-permissions"></a><a name="bkmk_user"></a> Uživatel nemá oprávnění.

**Chybová zpráva:** Nepovedlo se získat třídy inventáře s daty. Uživatel nemá oprávnění.

**Možné příčiny:** Uživatel nemusí mít přístup ke kolekci, do které je zařízení součástí. Ověřte následující položky:

1. Použijte stejný účet pro přihlášení k centru pro správu. Místní identita musí být synchronizovaná s cloudovou identitou a musí se shodovat.
1. Ověřte, že účet má oprávnění **ke čtení** pro **kolekci** zařízení v Configuration Manager.
1. Ujistěte se, že Configuration Manager zjistil účet administrativního uživatele, který používáte. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Vyberte uzel **Uživatelé** a vyhledejte svůj uživatelský účet.

    Pokud váš účet není uvedený v uzlu **Uživatelé** , Projděte si část konfigurace [zjišťování uživatelů služby Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)v lokalitě.

## <a name="known-issues"></a>Známé problémy

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## <a name="next-steps"></a>Další kroky

[Odstraňování potíží s připojením tenanta](troubleshoot.md)