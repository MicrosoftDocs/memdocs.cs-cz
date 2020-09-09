---
title: Připojení klienta – aplikace (Preview) v centru pro správu
titleSuffix: Configuration Manager
description: Nainstalujte aplikace pro nahrané Configuration Manager zařízení z centra pro správu.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 963dda08-87b8-4e80-90a7-25625efe8861
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 2cd158a920d1a088b2bc1380ae8618be461b647b
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564077"
---
# <a name="tenant-attach-install-an-application-from-the-admin-center-preview"></a><a name="bkmk_apps"></a> Připojení tenanta: instalace aplikace z centra pro správu (Preview)
<!--cm 6024389, in 7220536 pubpreview Aug 10, 2020-->
*Platí pro: Configuration Manager (Current Branch)*

> [!Important]
> - Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

Microsoft Endpoint Manager je integrované řešení pro správu všech vašich zařízení. Společnost Microsoft spojuje Configuration Manager a Intune s jednou konzolou s názvem **Centrum pro správu Microsoft Endpoint Manager**. V centru pro správu Microsoft Endpoint Management můžete iniciovat instalaci aplikace v reálném čase pro zařízení připojené k tenantovi.

   :::image type="content" source="media/6024389-tenant-attach-application-list.png" alt-text="Aplikace v centru pro správu Microsoft Endpoint Manager" lightbox="media/6024389-tenant-attach-application-list.png":::

## <a name="prerequisites"></a>Požadavky

- Všechny předpoklady pro [připojení tenanta: podrobnosti o klientovi nástroje ConfigMgr](client-details.md#prerequisites).
- [Kumulativní aktualizace pro Microsoft Endpoint Configuration Manager verze 2002](https://support.microsoft.com/help/4560496/) a odpovídající verze nainstalované konzoly
- Povolit volitelnou funkci **schválit žádosti o aplikace pro uživatele na zařízení**. Další informace naleznete v části [Enable optional features from updates](../core/servers/manage/install-in-console-updates.md#bkmk_options).
- Alespoň jedna aplikace nasazená na kolekci zařízení se **správcem musí schválit žádost o tuto aplikaci na** nastavení možnosti zařízení v nasazení. Další informace najdete v tématu [schvalování aplikací](../apps/deploy-use/app-approval.md#bkmk_opt).
   - Aplikace cílené na uživatele nebo aplikace bez nastavené možnosti schválení se nezobrazí v seznamu aplikací, pokud používáte Configuration Manager verze 2002.

Kromě toho budete potřebovat následující pro instalaci [cílových aplikací pro uživatele](#bkmk_user):<!--7518897-->

- Minimálně verze Configuration Manager 2006 a odpovídající verze nainstalované konzoly.


## <a name="permissions"></a>Oprávnění

Uživatelský účet potřebuje následující oprávnění:

- Oprávnění **číst** pro **kolekci** zařízení v Configuration Manager.
- Oprávnění **číst** pro **aplikaci** v Configuration Manager.
- Oprávnění **schvalovat** pro **aplikaci** v Configuration Manager.
- Role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD. 
  - Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny.
   > [!TIP]
   > [Role Správce aplikací v Azure AD](/azure/active-directory/users-groups-roles/directory-assign-admin-roles) má dostatečná oprávnění pro přidání uživatele do role **uživatele správce** aplikace.

## <a name="deploy-an-application-to-a-device"></a><a name="bkmk_deploy"></a> Nasazení aplikace do zařízení

1. V prohlížeči přejděte na [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Vyberte **zařízení** a potom **všechna zařízení**.
1. Vyberte zařízení, které se synchronizuje z Configuration Manager prostřednictvím [připojení klienta](device-sync-actions.md).
1. Vyberte **aplikace**.
1. Vyberte aplikaci a klikněte na **nainstalovat**.

   :::image type="content" source="media/6024389-tenant-attach-application-install.png" alt-text="Instalace aplikace z centra pro správu služby Microsoft Endpoint Manager" lightbox="media/6024389-tenant-attach-application-install.png":::

Všechna data, která jsou aktuálně v zobrazení, můžete exportovat do souboru. csv. V horní části stránky vyberte možnost **exportu** a vytvořte soubor. Pokud zobrazení překročí 500 řádků, exportováno bude pouze prvních 500.

## <a name="application-status"></a>Stav aplikace

Seznam aplikací můžete filtrovat podle stavu. Stav aplikace může být jedna z následujících:

- **K dispozici**: aplikace nebyla nikdy na zařízení nainstalována.
- **Nainstalováno**: aplikace je nainstalována na zařízení.
- **Probíhá instalace**: aplikace je právě instalována.
- **Požadovaná instalace**: požádala o instalaci, ale klient ještě tuto žádost nepřijal.
   - Pokud je zařízení v režimu offline, žádost o instalaci se potvrdí, až se vrátí zpátky do režimu online a přijme zásady.  
- **Chyba**: instalace aplikace se nezdařila.
- **Požadavky nejsou splněny**: požadavky na aplikaci nebyly splněny.
- **Nenainstalováno**: aplikace není momentálně nainstalovaná. Tento stav se obvykle zobrazuje, pokud jiné nasazení nebo uživatel aplikaci odebrali.
- **Čeká**se na restartování: aplikace je nainstalovaná, ale vyžaduje restart, aby bylo možné dokončit (počínaje verzí 2006).

## <a name="deploy-an-application-to-a-user"></a><a name="bkmk_user"></a> Nasazení aplikace pro uživatele
<!--7518897-->
Od verze Configuration Manager 2006 se aplikace dostupné pro uživatele zobrazí v uzlu **aplikace** pro zařízení nástroje ConfigMgr. Seznam aplikací, které jsou k dispozici pro zařízení, zahrnuje také aplikace nasazené do aktuálně přihlášeného uživatele zařízení.

Nasazení aplikací pro uživatele má následující omezení:
- Scénáře relací s více uživateli nejsou podporovány.
- Zařízení připojená k Azure AD nejsou momentálně podporovaná.
   - Podporují se zařízení, která jsou připojená k doméně i připojená k Azure AD.

## <a name="next-steps"></a>Další kroky

[Řešení potíží s aplikacemi](troubleshoot-applications.md)