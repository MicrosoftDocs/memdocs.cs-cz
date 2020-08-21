---
title: Schválení aplikací
titleSuffix: Configuration Manager
description: Přečtěte si o nastavení a chování při schvalování aplikací v Configuration Manager.
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15aba2a32e680ab9499f5295307c82daafbbed71
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695337"
---
# <a name="approve-applications-in-configuration-manager"></a>Schvalování aplikací v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Při [nasazování aplikace](deploy-applications.md) v Configuration Manager můžete pro instalaci vyžadovat schválení. Uživatelé požadují aplikaci v centru softwaru a pak si prohlédněte žádost v konzole Configuration Manager. Žádost můžete schválit nebo zamítnout.

## <a name="approval-settings"></a><a name="bkmk_approval"></a> Nastavení schválení

Chování při schvalování aplikací závisí na tom, jestli povolíte doporučené [volitelné prostředí pro schvalování aplikací](#bkmk_opt). Jedno z následujících nastavení schválení se zobrazí na stránce **nastavení nasazení** v nasazení aplikace:  

### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a><a name="bkmk_opt"></a> Správce musí na zařízení schválit žádost o tuto aplikaci.

> [!Note]  
> Configuration Manager ve výchozím nastavení tuto funkci nepovolí. Než ho použijete, povolte volitelnou funkci **schvalovat žádosti o aplikace pro uživatele na zařízení**. Další informace naleznete v části [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
>
> Pokud tuto funkci nepovolíte, zobrazí se [předchozí prostředí](#bkmk_prior).  

Správce schválí všechny požadavky uživatelů na aplikaci, aby ji uživatel mohl nainstalovat na požadované zařízení. Pokud správce žádost schválí, uživatel může aplikaci nainstalovat jenom na toto zařízení. Uživatel musí odeslat další žádost o instalaci aplikace na jiné zařízení. Tato možnost je zobrazena šedě, pokud je **požadován**účel nasazení nebo když nasadíte aplikaci do kolekce zařízení. <!--1357015-->  

> [!Note]  
> Pokud chcete využívat nové funkce Configuration Manager, nejdřív aktualizujte klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.<!--SCCMDocs issue 646-->  

V části **Správa aplikací** v pracovním prostoru **softwarová knihovna** konzoly Configuration Manager zobrazte **žádosti o aplikace** . (Ve verzi 1902 a starší se tento uzel nazývá **žádosti o schválení**.) Nyní je v seznamu sloupec **zařízení** pro každý požadavek. Pokud v žádosti provedete akci, dialogové okno žádosti o aplikaci také obsahuje název zařízení, ze kterého uživatel žádost odeslal.

Pokud žádost není během 30 dnů schválena, bude odebrána. Přeinstalování klienta může zrušit všechny žádosti o schválení, které čekají na schválení.  

Když budete vyžadovat schválení nasazení do kolekce zařízení, aplikace se nezobrazí v centru softwaru. Pokud budete vyžadovat schválení nasazení pro kolekci uživatelů, zobrazí se aplikace v centru softwaru. Můžete ho i nadále skrýt od uživatelů s nastavením klienta, **Skrýt neschválené aplikace v centru softwaru**. Další informace najdete v tématu [nastavení klienta centra softwaru](../../core/clients/deploy/about-client-settings.md#software-center).

Po schválení aplikace k instalaci můžete žádost **odmítnout** v konzole Configuration Manager. Pokud uživatelé už aplikaci ještě nenainstalovali, tato akce je zabrání v instalaci nových kopií aplikace z centra softwaru. Pokud **je aplikace** dřív schválená a nainstalovaná, pak klient odinstaluje aplikaci ze zařízení uživatele.<!--1357891-->

Pokud ve verzi 1906 schválíte žádost o aplikaci v konzole a pak ji odepřete, můžete ji teď schválit znovu. Aplikace se po schválení znovu nainstaluje na klienta.  <!-- 4224910 -->

Automatizujte proces schvalování pomocí rutiny CMApprovalRequest prostředí PowerShell pro [schválení](/powershell/module/configurationmanager/approve-cmapprovalrequest?view=sccm-ps) . Počínaje verzí 1902 Tato rutina zahrnuje parametr **InstallActionBehavior** . Pomocí tohoto parametru můžete určit, jestli se má aplikace nainstalovat hned, nebo během nepracovních hodin.<!-- SCCMDocs-pr issue #3418 -->

Od 1906 se můžete podívat, která nasazení vyžadují schválení. Vyberte aplikaci v uzlu **aplikace** . V podokně podrobností přepněte na kartu **nasazení** . Ve výchozím nastavení se zobrazuje nový sloupec, **vyžaduje schválení**.

#### <a name="retry-the-install-of-pre-approved-applications"></a><a name="bkmk_retry"></a> Opakovat instalaci předběžně schválených aplikací

<!--4336307-->
Počínaje verzí 1906 můžete opakovat instalaci aplikace, kterou jste předtím schválili pro uživatele nebo zařízení. Možnost schválení je dostupná jenom pro dostupná nasazení. Pokud uživatel aplikaci odinstaluje nebo dojde k chybě počáteční instalace, Configuration Manager nevyhodnocují svůj stav a znovu ho přeinstalujte. Tato funkce umožňuje technikovi podpory rychle opakovat instalaci aplikace pro uživatele, který volá nápovědu.

1. Otevřete konzolu Configuration Manager jako uživatel, který má oprávnění **schválit** u objektu aplikace. Toto oprávnění mají například předdefinované role **správce aplikace** nebo **Autor aplikace** .

1. Nasaďte aplikaci, která vyžaduje schválení, a schvalte ji.

    > [!Tip]  
    > Případně [nainstalujte aplikaci pro zařízení](install-app-for-device.md). Vytvoří na zařízení schválený požadavek na aplikaci.  

Pokud se aplikace nenainstalovala úspěšně, nebo uživatel odinstaluje aplikaci, zkuste to znovu pomocí následujícího postupu:

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **požadavky aplikace** . (Ve verzi 1902 a starší se tento uzel nazývá **žádosti o schválení**.)

1. Vyberte dřív schválenou aplikaci. Ve skupině žádost o schválení na pásu karet vyberte **opakovat instalaci**.

#### <a name="other-app-approval-resources"></a>Další prostředky pro schválení aplikací

- [Vylepšení schvalování aplikací v nástroji ConfigMgr 1810](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Application-approval-improvements-in-ConfigMgr-1810/ba-p/303534)
- [Aktualizace procesu schválení aplikace v Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Updates-to-the-application-approval-process-in-Configuration/ba-p/275048)

### <a name="require-administrator-approval-if-users-request-this-application"></a><a name="bkmk_prior"></a> Vyžadovat schválení správce, pokud uživatelé požadují tuto aplikaci

> [!Note]  
> Tento postup se používá, pokud nepovolíte doporučené [volitelné prostředí pro schvalování aplikací](#bkmk_opt).

Správce schválí všechny požadavky uživatelů na aplikaci, aby ji mohl uživatel nainstalovat. Tato možnost je zobrazena šedě, pokud je **požadován**účel nasazení nebo když nasadíte aplikaci do kolekce zařízení.  

Žádosti o schválení aplikace se zobrazují v uzlu **žádosti o aplikace** v části **Správa aplikací** v pracovním prostoru **softwarová knihovna** . (Ve verzi 1902 a starší se tento uzel nazývá **žádosti o schválení**.) Pokud žádost není během 30 dnů schválena, bude odebrána. Přeinstalování klienta může zrušit všechny žádosti o schválení, které čekají na schválení.  

Po schválení aplikace k instalaci můžete žádost **odmítnout** v konzole Configuration Manager. Tato akce nezpůsobí, že klient odinstalovat aplikaci z libovolného zařízení. Zabrání uživatelům instalovat nové kopie aplikace z centra softwaru.  

## <a name="email-notifications"></a><a name="bkmk_email-approve"></a> E-mailová oznámení

<!--1321550-->

Můžete nakonfigurovat e-mailová oznámení pro žádosti o schválení aplikace. Když uživatel požádá o aplikaci, obdržíte e-mail. Kliknutím na odkazy v e-mailu schválíte nebo odepřete žádost, aniž byste museli konzolu Configuration Manager.

Můžete definovat e-mailové adresy uživatelů, kteří mohou schválit nebo zamítnout požadavek při vytváření nového nasazení aplikace. Pokud potřebujete změnit seznam e-mailových adres, přejděte do pracovního prostoru **monitorování** , rozbalte položku **výstrahy**a vyberte uzel **odběry** . Vyberte **vlastnosti** z jedné ze **schválené aplikace prostřednictvím e-mailových** předplatných, která se vztahují k nasazení vaší aplikace.

Pokud je k dispozici více než jedna výstraha, můžete určit, která výstraha se nachází v rámci kterého nasazení. Otevřete vlastnosti výstrahy a zobrazte seznam **vybraných výstrah** na kartě Obecné. U tohoto předplatného je povolené nasazení jako výstraha.

Uživatelé můžou do žádosti přidat komentář z centra softwaru. Tento komentář se zobrazuje na žádost aplikace v konzole Configuration Manager. Počínaje verzí 1902 se tento komentář zobrazuje i v e-mailu. Zahrnutím tohoto komentáře do e-mailu můžou schvalovatelé učinit lepší rozhodnutí o schválení nebo zamítnutí žádosti.<!--3594063-->

### <a name="prerequisites"></a>Předpoklady

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>Odeslání e-mailových oznámení a provedení akce v interní síti

S těmito požadavky obdrží příjemci e-mail s oznámením o žádosti. Pokud jsou v interní síti, můžou žádost schválit nebo odmítnout i z e-mailu.

- Povolit [volitelnou funkci](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **schválit žádosti o aplikace pro uživatele na zařízení**.  

- Konfigurace [e-mailových oznámení pro výstrahy](../../core/servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts).  

    > [!NOTE]
    > Administrativní uživatel, který nasazuje aplikaci, potřebuje oprávnění k vytvoření výstrahy a předplatného. Pokud tento uživatel nemá tato oprávnění, zobrazí se na konci **Průvodce nasazením softwaru**Chyba: nemáte oprávnění zabezpečení k provedení této operace.<!-- 2810283 -->

- Povolte poskytovateli serveru SMS v primární lokalitě, aby používal certifikát.<!--SCCMDocs-pr issue 3135--> Použijte jednu z následujících možností:  

  - Doporučil Povolit [Rozšířený protokol HTTP](../../core/plan-design/hierarchy/enhanced-http.md) pro primární lokalitu.

    > [!Note]  
    > Když primární lokalita vytvoří certifikát pro poskytovatele služby SMS, webový prohlížeč v klientovi nebude důvěryhodný. Na základě nastavení zabezpečení při reakci na žádost o aplikaci se může zobrazit upozornění zabezpečení.  

  - Ručně navažte certifikát založený na infrastruktuře veřejných klíčů na port 443 ve službě IIS na serveru, který je hostitelem role poskytovatele služby SMS v primární lokalitě.

> [!NOTE]
> Pokud máte v hierarchii více podřízených primárních lokalit, nakonfigurujte tyto požadavky pro každou primární lokalitu, ve které chcete tuto funkci povolit. Odkazy v e-mailovém oznámení jsou pro službu správy v primární lokalitě.<!-- 7108472 -->

#### <a name="to-take-action-from-internet"></a>Provedení akce z Internetu

U těchto dalších volitelných požadavků můžou příjemci žádost schválit nebo odepřít odkudkoli, kde mají přístup k Internetu.

- Povolte službu pro správu poskytovatele služby SMS přes bránu pro správu cloudu. V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **servery a role systému lokality** . Vyberte server s rolí poskytovatele služby SMS. V podokně podrobností vyberte roli **poskytovatele služby SMS** a v pásu karet na kartě role webového serveru vyberte možnost **vlastnosti** . Vyberte možnost, která **povolí Configuration Manager provoz brány pro správu cloudu pro službu správy**.  

- Poskytovatel serveru SMS vyžaduje **rozhraní .NET 4.5.2** nebo novější.  

- Nastavte [bránu pro správu cloudu](../../core/clients/manage/cmg/plan-cloud-management-gateway.md).

- Připojte lokalitu ke [službám Azure](../../core/servers/deploy/configure/azure-services-wizard.md) pro **správu cloudu**.

- Povolte [zjišťování uživatelů Azure AD](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc).

- Ruční konfigurace nastavení v Azure AD:  

    1. Pro uživatele s oprávněními *globálního správce* použijte [Azure Portal](https://portal.azure.com) . Přejít na **Azure Active Directory**a vyberte **Registrace aplikací**.  

    1. Vyberte aplikaci, kterou jste vytvořili pro Configuration Manager integraci **správy cloudu** .  

    1. V nabídce **Správa** vyberte **ověřování**.  

        1. V části **identifikátory URI pro přesměrování** vložte následující cestu: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

        1. Nahraďte `<CMG FQDN>` plně kvalifikovaným názvem domény (FQDN) vaší služby brány pro správu cloudu (CMG). Například GraniteFalls.Contoso.com.  

        1. Pak vyberte **Uložit**.  

    1. V nabídce **Správa** vyberte možnost **manifest**.  

        1. V podokně upravit manifest Najděte vlastnost **oauth2AllowImplicitFlow** .  

        1. Změňte její hodnotu na **true**. Například celá čára by měla vypadat jako na následujícím řádku: `"oauth2AllowImplicitFlow": true,`  

        1. Vyberte **Uložit**.  

### <a name="configure-email-approval"></a>Konfigurace schválení e-mailu

1. V konzole Configuration Manager [Nasaďte aplikaci](deploy-applications.md) jako dostupnou pro kolekci uživatelů. Na stránce **nastavení nasazení** Povolte schválení. Pak zadejte jednu nebo více e-mailových adres pro příjem oznámení. Jednotlivé e-mailové adresy oddělujte středníkem ( `;` ).  

     > [!Note]  
     > Kdokoli ve vaší organizaci Azure AD, který obdrží e-mail, může žádost schválit. Nepředávejte e-mail ostatním uživatelům, pokud nechcete, aby provedli akci.  

2. Jako uživatel si vyžádejte aplikaci v centru softwaru.  

3. Během pěti minut obdržíte e-mailové oznámení. Obsah e-mailu je podobný následujícímu příkladu:  

![Příklad e-mailového oznámení pro schválení aplikace](media/1321550-email.png)

> [!Note]  
> Odkaz na schválení nebo odepření je pro jednorázové použití. Například můžete nakonfigurovat alias skupiny pro příjem oznámení. MB schválí požadavek. Nyní Bruce nemůže žádost zamítnout.  

Pokud chcete řešit potíže, zkontrolujte soubor **NotiCtrl. log** na serveru lokality.

## <a name="maintenance"></a>Údržba

Configuration Manager ukládá informace o žádosti o schválení aplikace v databázi lokality. U požadavků, které jsou zrušené nebo zamítnuté, lokalita odstraní historii žádostí po uplynutí 30 dnů. Toto chování při odstraňování můžete nakonfigurovat pomocí [úlohy údržby lokality](../../core/servers/manage/maintenance-tasks.md) **Odstranit zastaralá data žádosti o aplikaci** . Lokalita nikdy neodstraní žádné schválené nebo nedokončené žádosti o aplikace.