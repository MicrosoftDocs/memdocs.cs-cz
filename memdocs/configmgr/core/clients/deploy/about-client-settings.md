---
title: Nastavení klienta
titleSuffix: Configuration Manager
description: Přečtěte si o výchozím a vlastním nastavení pro řízení chování klienta.
ms.date: 08/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: reference
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8045df681560972a353e08ee43c10b6ae86dc50f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693416"
---
# <a name="about-client-settings-in-configuration-manager"></a>Informace o nastavení klienta v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Spravujte všechna nastavení klienta v konzole Configuration Manager v uzlu **nastavení klienta** v pracovním prostoru **Správa** . Configuration Manager obsahuje sadu výchozích nastavení. Když změníte výchozí nastavení klienta, budou tato nastavení platit pro všechny klienty v hierarchii. Můžete také nakonfigurovat vlastní nastavení klienta, která při přiřazování ke kolekcím přepíší výchozí nastavení klienta. Další informace najdete v tématu [Konfigurace nastavení klienta](configure-client-settings.md).

Následující části popisují nastavení a možnosti podrobněji.  


## <a name="background-intelligent-transfer-service-bits"></a>Služba inteligentního přenosu na pozadí (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>Omezit maximální šířku pásma sítě pro přenosy na pozadí BITS

Pokud je tato možnost **Ano**, klienti budou používat omezení šířky pásma BITS. Pokud chcete nakonfigurovat další nastavení v této skupině, musíte povolit toto nastavení.

### <a name="throttling-window-start-time"></a>Čas zahájení omezovacího okna

Zadejte místní čas spuštění pro okno omezování bitů.  

### <a name="throttling-window-end-time"></a>Čas ukončení omezovacího okna

Zadejte místní koncový čas pro okno omezování bitů. Pokud je koncový čas roven **času spuštění okna omezování**, omezování služby BITS je vždy povoleno.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Maximální přenosová rychlost během omezovacího okna (kB/s)

Zadejte maximální rychlost přenosu, kterou klienti můžou používat během tohoto okna.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>Povolit stažení ze serveru BITS mimo omezovací okno

Umožňuje klientům používat samostatná nastavení BITS mimo určené okno.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Maximální přenosová rychlost mimo omezovací okno (Kbps)

Zadejte maximální rychlost přenosu, kterou klienti můžou používat mimo okno omezování bitů.  



## <a name="client-cache-settings"></a>Nastavení mezipaměti klienta

### <a name="configure-branchcache"></a>Konfigurace služby BranchCache

Nastavte klientský počítač pro službu [Windows BranchCache](../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache
). Chcete-li povolit ukládání do mezipaměti služby BranchCache v klientovi, nastavte **možnost povolit službu BranchCache** na **hodnotu Ano**.

- **Povolit službu BranchCache**: povoluje BranchCache na klientských počítačích.

- **Maximální velikost mezipaměti BranchCache (procento disku)**: procento disku, který povolíte pro službu BranchCache.

> [!TIP]
> Pokud nastavíte možnost **Konfigurovat službu BranchCache** na **ne**, pak Configuration Manager nekonfiguruje žádná nastavení služby BranchCache.
>
> Pokud chcete službu BranchCache zakázat, nastavte možnost **Konfigurovat BranchCache** na **Ano**a potom nastavte **Povolit BranchCache** na **ne**.<!-- 6244852 -->

### <a name="configure-client-cache-size"></a>Konfigurace velikosti mezipaměti klienta

Mezipaměť klienta Configuration Manager v počítačích s Windows ukládá dočasné soubory používané k instalaci aplikací a programů. Pokud je tato možnost nastavená na **ne**, výchozí velikost je 5 120 MB.

Pokud zvolíte **Ano**, pak zadejte:

- **Maximální velikost mezipaměti (MB)**
- **Maximální velikost mezipaměti (procento disku)**: velikost mezipaměti klienta se zvětšuje na maximální velikost v megabajtech (MB) nebo v procentech disku, podle toho, co je míň.

### <a name="enable-as-peer-cache-source"></a>Povolit jako zdroj sdílené mezipaměti

> [!Note]  
> Ve verzi 1902 a novější bylo toto nastavení pojmenováno **povolit Configuration Manager klienta v plném operačním systému pro sdílení obsahu**. Chování nastavení se nezmění.

Povolí sdílenou [mezipaměť](../../plan-design/hierarchy/client-peer-cache.md) pro klienty Configuration Manager. Zvolte **Ano**a pak zadejte port, přes který klient komunikuje s partnerským počítačem.

- **Port pro počáteční síťové všesměrové vysílání** (výchozí UDP 8004): Configuration Manager používá tento port v systému Windows PE nebo v plném operačním systému Windows. Modul pořadí úkolů v systému Windows PE odesílá všesměrové vysílání, aby získal umístění obsahu před spuštěním pořadí úloh.<!--SCCMDocs issue 910-->

- **Port pro stažení obsahu z partnerského** zařízení (výchozí TCP 8003): Configuration Manager automaticky nakonfiguruje pravidla brány Windows Firewall pro povolení tohoto provozu. Pokud používáte jinou bránu firewall, musíte ručně nakonfigurovat pravidla, která povolují tento provoz.  

    Další informace najdete v tématu [porty používané pro připojení](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

### <a name="minimum-duration-before-cached-content-can-be-removed-minutes"></a>Minimální doba trvání, než bude možné odebrat obsah uložený v mezipaměti (minuty)

<!--4485509-->
Od verze 1906 Určete minimální dobu, po kterou má klient Configuration Manager uchovávat obsah v mezipaměti. Toto nastavení klienta definuje minimální dobu Configuration Manager agenta čekat, než bude moci odebrat obsah z mezipaměti v případě, že je potřeba více místa.

Ve výchozím nastavení je tato hodnota 1 440 minut (24 hodin).
Maximální hodnota tohoto nastavení je 10 080 minut (jeden týden).

Toto nastavení poskytuje větší kontrolu nad mezipamětí klienta na různých typech zařízení. Můžete snížit hodnotu v klientech s malými pevnými disky a nemusíte uchovávat stávající obsah před spuštěním jiného nasazení.


## <a name="client-policy"></a>Zásady klienta  

### <a name="client-policy-polling-interval-minutes"></a>Interval dotazování na zásady klienta (minuty)

Určuje, jak často následující klienti Configuration Manager stahují zásady klienta:

- Počítače s Windows (například stolní počítače, servery, přenosné počítače)  
- Mobilní zařízení, která Configuration Manager registrovat  
- Počítače Mac  
- Počítače, na kterých běží Linux nebo UNIX  

Ve výchozím nastavení je tato hodnota 60 minut. Snížení této hodnoty způsobí, že klienti dotazují web častěji. U mnoha klientů může mít toto chování negativní dopad na výkon webu. [Pokyny pro velikost a škálování](../../plan-design/configs/size-and-scale-numbers.md) jsou založené na výchozí hodnotě. Zvýšení této hodnoty způsobí, že se klienti dotazují na webu méně často. Všechny změny zásad klienta, včetně nových nasazení, trvat déle, než se klienti stáhnou a zpracují.<!-- SCCMDocs issue 823 -->

### <a name="enable-user-policy-on-clients"></a>Povolit zásady uživatele u klientů

Pokud nastavíte tuto možnost na **Ano**a použijete [zjišťování uživatelů](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), pak klienti dostanou aplikace a programy zaměřené na přihlášeného uživatele.  

Pokud toto nastavení není **, uživatelé**neobdrží požadované aplikace, které nasadíte pro uživatele. Uživatelé také neobdrží žádné další úlohy správy v zásadách uživatele.  

Toto nastavení platí pro uživatele, pokud je jejich počítač v intranetu nebo na internetu. Pokud chcete povolit také zásady uživatele na internetu, musí být **Ano** .  

> [!Note]  
> Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete instalovat nové role katalogu aplikací.
>
> Pokud stále používáte katalog aplikací, obdrží seznam dostupného softwaru pro uživatele ze serveru lokality. Proto toto nastavení nemusí být **Ano** , aby mohli uživatelé zobrazovat a žádat o aplikace z katalogu aplikací. Pokud toto nastavení není **, uživatelé**nebudou moci instalovat aplikace, které vidí v katalogu aplikací.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>Povolit žádosti o zásady uživatele od internetových klientů

Tuto možnost nastavte na **Ano** , pokud uživatelé obdrží zásady uživatele na internetových počítačích. Platí taky následující požadavky:  

- Klient a lokalita jsou konfigurovány pro [internetovou správu klientů](../manage/plan-internet-based-client-management.md) nebo [bránu pro správu cloudu](../manage/cmg/plan-cloud-management-gateway.md).  

- Nastavení **Povolit zásady uživatele u klientů** je **Ano**.  

- Internetový bod správy úspěšně ověří uživatele pomocí ověřování systému Windows (Kerberos nebo NTLM). Další informace najdete v tématu [požadavky na komunikaci klienta z Internetu](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

- Brána pro správu cloudu úspěšně ověřuje uživatele pomocí Azure Active Directory. Další informace najdete v tématu [nasazení aplikací dostupných pro uživatele](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications).

Pokud tuto možnost nastavíte na **ne**, nebo některý z předchozích požadavků není splněn, počítač v Internetu přijme pouze zásady počítače. V tomto scénáři uživatelé stále můžou zobrazit, žádat a instalovat aplikace z internetového katalogu aplikací. Pokud toto **nastavení není k dispozici, ale** **možnost povolit zásady uživatele u klientů** je **Ano**, uživatelé neobdrží zásady uživatele, dokud se počítač nepřipojí k intranetu.  

> [!NOTE]  
> Pro internetovou správu klientů žádosti o schválení aplikací od uživatelů nevyžadují zásady uživatele ani ověření uživatele. Brána pro správu cloudu nepodporuje žádosti o schválení aplikace.  

### <a name="enable-user-policy-for-multiple-user-sessions"></a>Povolit zásady uživatele pro více uživatelských relací

<!--4737447-->

*Platí pro verzi 1910*

Standardně je toto nastavení zakázáno. I když povolíte zásady uživatele, počínaje verzí 1906, klient je ve výchozím nastavení zakáže na jakémkoli zařízení, které umožňuje více souběžných aktivních uživatelských relací. Například Terminálové servery nebo Windows 10 Enterprise s více relacemi na [virtuálním počítači s Windows](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

Klient zakáže zásady uživatele pouze v případě, že během nové instalace detekuje tento typ zařízení. Pro existujícího klienta tohoto typu, který aktualizujete na verzi 1906 nebo novější, předchozí chování přetrvává. V existujícím zařízení nakonfiguruje nastavení zásad uživatele i v případě, že zjistí, že zařízení umožňuje více uživatelských relací.

Pokud v tomto scénáři požadujete zásady uživatele a přijměte případný případný dopad na výkon, povolte toto nastavení klienta.


## <a name="cloud-services"></a>Cloud Services

### <a name="allow-access-to-cloud-distribution-point"></a>Povolení přístupu k distribučnímu bodu cloudu

Tuto možnost nastavte na **Ano** , pokud chcete, aby klienti získali obsah z distribučního bodu cloudu. Toto nastavení nevyžaduje, aby bylo zařízení na internetu.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Automaticky registrovat nová zařízení s Windows 10 připojená k doméně pomocí Azure Active Directory

Když nakonfigurujete Azure Active Directory pro podporu hybridního připojení, Configuration Manager pro tuto funkci nakonfiguruje zařízení s Windows 10. Další informace najdete v tématu [jak nakonfigurovat zařízení připojená k hybridním Azure Active Directory](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>Povolit klientům používat bránu pro správu cloudu

Ve výchozím nastavení používají všichni internetoví klienti přístup k dostupné [bráně pro správu cloudu](../manage/cmg/plan-cloud-management-gateway.md). Příkladem toho, kdy nakonfigurovat toto nastavení na **ne** , je použití oboru služby, například během pilotního projektu nebo úspory nákladů.



## <a name="compliance-settings"></a>Nastavení dodržování předpisů  

### <a name="enable-compliance-evaluation-on-clients"></a>Povolit vyhodnocování dodržování předpisů u klientských počítačů

Nastavením této možnosti na **Ano** nakonfigurujete další nastavení v této skupině.

### <a name="schedule-compliance-evaluation"></a>Naplánovat vyhodnocování dodržování předpisů

Vyberte **plán** pro vytvoření výchozího plánu pro nasazení standardních hodnot konfigurace. Tato hodnota se dá konfigurovat pro každou standardní hodnotu v dialogovém okně **nasadit standardní hodnoty konfigurace** .  

### <a name="enable-user-data-and-profiles"></a>Povolit profily a data uživatelů

Vyberte možnost **Ano** , pokud chcete nasadit položky konfigurace [profilů a dat uživatele](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) .



## <a name="computer-agent"></a>Počítačový agent  

### <a name="user-notifications-for-required-deployments"></a>Oznámení uživatelů pro požadovaná nasazení

Další informace o následujících třech nastaveních najdete v tématu [oznámení uživatelů pro požadovaná nasazení](../../../apps/deploy-use/deploy-applications.md#bkmk_notify):

- **Konečný termín nasazení je delší než 24 hodin, připomenout uživateli každých (hodiny)**
- **Konečný termín nasazení kratší než 24 hodin, připomenout uživateli každých (hodiny)**
- **Konečný termín nasazení kratší než 1 hodina, připomenout uživateli každých (minuty)**

### <a name="default-application-catalog-website-point"></a>Výchozí bod webu Katalog aplikací

> [!Important]  
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v následujících článcích:
>
> - [Konfigurace centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Configuration Manager používá toto nastavení pro připojení uživatelů ke katalogu aplikací z centra softwaru. Vyberte **nastavit web** a zadejte server, který je hostitelem bodu webu Katalog aplikací. Zadejte název NetBIOS nebo plně kvalifikovaný název domény, zadejte automatické zjišťování nebo zadejte adresu URL pro přizpůsobená nasazení. Ve většině případů je nejlepší volbou automatické zjišťování.

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Přidat výchozí web Katalog aplikací do zóny důvěryhodných serverů Internet Exploreru

> [!Important]  
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v následujících článcích:
>
> - [Konfigurace centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Pokud je tato možnost **Ano**, klient automaticky přidá aktuální výchozí adresu URL webu Katalog aplikací do zóny důvěryhodných serverů aplikace Internet Explorer.  

Toto nastavení zajišťuje, že nastavení Internet Exploreru pro chráněný režim není povolené. Pokud je povolený chráněný režim, klient Configuration Manager nemusí být schopný instalovat aplikace z katalogu aplikací. Ve výchozím nastavení zóna důvěryhodných serverů také podporuje přihlášení uživatele ke katalogu aplikací, které vyžaduje ověřování systému Windows.  

Pokud tuto možnost necháte nastavenou na **ne**, Configuration Manager klienti nemusí být schopni instalovat aplikace z katalogu aplikací. Alternativním způsobem je nakonfigurovat tato nastavení aplikace Internet Explorer v jiné zóně pro adresu URL katalogu aplikací, kterou používají klienti nástroje.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Povolit aplikacím Silverlight spouštění v režimu zvýšené důvěryhodnosti

> [!Important]  
> Klient nebude automaticky instalovat program Silverlight.
>
> Počínaje verzí 1806 se **uživatelské prostředí Silverlight** pro bod webu Katalog aplikací už nepodporuje. Uživatelé by měli používat nové centrum softwaru. Další informace najdete v tématu [Konfigurace centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).  

Toto nastavení musí být **Ano** , aby mohli uživatelé používat Katalog aplikací.  

Pokud toto nastavení změníte, projeví se při příštím načtení prohlížeče nebo při obnovení aktuálně otevřeného okna prohlížeče.  

Další informace o tomto nastavení najdete v tématu [certifikáty pro Microsoft Silverlight 5 a režim zvýšené důvěryhodnosti vyžadované pro katalog aplikací](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

### <a name="organization-name-displayed-in-software-center"></a>Název organizace zobrazený v centru softwaru

Zadejte název, který uživatelé uvidí v centru softwaru. Tyto informace o značce pomáhají uživatelům identifikovat tuto aplikaci jako důvěryhodný zdroj. Další informace o prioritě tohoto nastavení najdete v tématu [brandinging Software Center](../../../apps/plan-design/plan-for-software-center.md#brand-software-center).  

### <a name="use-new-software-center"></a>Použít nové Centrum softwaru

Výchozí nastavení je **Ano**.

Pokud nastavíte tuto možnost na **Ano**, všechny klientské počítače použijí Centrum softwaru. Centrum softwaru zobrazuje software, aktualizace softwaru a sekvence úloh, které nasazujete pro uživatele nebo zařízení.

### <a name="enable-communication-with-health-attestation-service"></a>Povolit komunikaci se službou ověření stavu

Nastavte tuto možnost na **Ano** , pokud chcete, aby zařízení s Windows 10 používala [ověření stavu](../../servers/manage/health-attestation.md). Pokud povolíte toto nastavení, je pro konfiguraci k dispozici také následující nastavení.

### <a name="use-on-premises-health-attestation-service"></a>Použít místní službu ověření stavu

Tuto možnost nastavte na **Ano** , pokud chcete, aby zařízení používala místní službu. Nastavte na **ne** , pokud chcete, aby zařízení používala cloudovou službu Microsoftu.  

### <a name="install-permissions"></a>Oprávnění k instalaci

Konfigurace způsobu, jakým uživatelé můžou instalovat software, aktualizace softwaru a sekvence úloh:  

- **Všichni uživatelé**: uživatelé s libovolným oprávněním s výjimkou hostů.  

- **Pouze správci**: uživatelé musí být členy místní skupiny Administrators.  

- **Pouze správci a primární uživatelé**: uživatelé musí být členy místní skupiny Administrators nebo primární uživatel počítače.  

- **Žádní uživatelé**: žádní uživatelé přihlášení ke klientskému počítači nemohou instalovat software, aktualizace softwaru a sekvence úloh. Požadovaná nasazení pro počítač se vždy instalují v konečném termínu. Uživatelé nemůžou instalovat software z centra softwaru.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Pozastavení zadávání kódu PIN BitLockeru při restartu

Pokud počítače vyžadují zadání kódu PIN nástroje BitLocker, tato možnost obejít požadavek na zadání kódu PIN, když se počítač restartuje po instalaci softwaru.  

- **Always**: Configuration Manager dočasně pozastaví nástroj BitLocker po instalaci softwaru, který vyžaduje restart, a restartuje počítač. Toto nastavení platí pouze v případě, že Configuration Manager restartuje počítač. Toto nastavení neruší požadavek na zadání kódu PIN BitLockeru, když uživatel restartuje počítač. Požadavek na zadání kódu PIN BitLockeru se obnoví po spuštění systému Windows.

- **Nikdy**: Configuration Manager po instalaci softwaru vyžadujícího restart Nepozastavte nástroj BitLocker. V tomto scénáři nelze instalaci softwaru dokončit, dokud uživatel nezadá kód PIN, aby bylo možné dokončit standardní proces spuštění a načíst systém Windows.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>Další software spravuje nasazování aplikací a aktualizace softwaru

Tuto možnost povolte pouze v případě, že platí jedna z následujících podmínek:  

- Využíváte řešení dodavatele, které vyžaduje povolení tohoto nastavení.  

- Ke správě oznámení agenta klienta a instalaci aplikací a aktualizací softwaru slouží sada SDK (Configuration Manager Software Development Kit).  

> [!WARNING]  
> - Pokud zvolíte tuto možnost, když neplatí žádná z těchto podmínek, klient nenainstaluje aktualizace softwaru a požadované aplikace. Toto nastavení nebrání uživatelům instalovat dostupný software z centra softwaru, včetně aplikací, balíčků a sekvencí úloh.  
> -  Když toto nastavení povolíte, informační zprávy pro nový software nebo požadovaný software se na klientech neobjeví. <!--6347668-->

### <a name="powershell-execution-policy"></a>Zásady spouštění skriptu PowerShell

Nakonfigurujte, jak Configuration Manager klienti můžou spouštět skripty Windows PowerShellu. Tyto skripty můžete použít k detekci v položkách konfigurace pro nastavení dodržování předpisů. Můžete také poslat skripty v nasazení jako standardní skript.  

- **Bypass**: klient Configuration Manager obejít konfiguraci prostředí Windows PowerShell v klientském počítači, aby bylo možné spustit nepodepsané skripty.  

- **Omezeno**: klient Configuration Manager používá aktuální konfiguraci prostředí PowerShell v klientském počítači. Tato konfigurace určuje, zda lze spustit nepodepsané skripty.  

- **Všechny podepsané**: klient Configuration Manager spouští skripty pouze v případě, že je důvěryhodný vydavatel podepsal. Toto omezení platí nezávisle na aktuální konfiguraci prostředí PowerShell v klientském počítači.  

Tato možnost vyžaduje aspoň Windows PowerShell verze 2,0. Výchozí hodnota je **všechna podepsaná**.  

> [!TIP]  
> Pokud se nepodepsané skripty nepodaří spustit z důvodu tohoto nastavení klienta, Configuration Manager oznamuje tuto chybu následujícími způsoby:  
>
> - Pracovní prostor **monitorování** v konzole nástroje zobrazuje ID chyby stavu nasazení **0x87D00327**. Také se zobrazí popis **skriptu není podepsán**.  
> - V sestavách se zobrazuje **Chyba zjišťování**typu chyby. Pak se v sestavách zobrazí buď kód chyby **0x87D00327** a skript Description není **podepsaný**, nebo kód chyby **0x87D00320** a popis, **který Hostitel skriptu ještě není nainstalovaný**. Příklad sestavy: podrobnosti o **chybách položek konfigurace v směrném plánu konfigurace pro určitý prostředek**.  
> - V souboru **DcmWmiProvider. log** se zobrazí zpráva, že skript zprávy není **podepsaný (Chyba: 87D00327; Zdroj: CCM)**.  

### <a name="show-notifications-for-new-deployments"></a>Zobrazit oznámení pro nová nasazení

Vyberte **Ano** , pokud chcete zobrazit oznámení o nasazeních, která jsou k dispozici méně než týden. Tato zpráva se zobrazí při každém spuštění agenta klienta.

### <a name="disable-deadline-randomization"></a>Zakázat náhodné přeskupování termínu

Po uplynutí konečného termínu nasazení toto nastavení určuje, jestli klient k instalaci požadovaných aktualizací softwaru používá prodlevu aktivace o délce až dvou hodin. Ve výchozím nastavení je prodleva aktivace zakázána.  

V případě scénářů infrastruktury virtuálních klientských počítačů (VDI) Tato prodleva pomáhá distribuovat výpočetní výkon procesoru a přenos dat pro hostitelský počítač s více virtuálními počítači. I v případě, že infrastrukturu VDI nepoužíváte, může mít mnoho klientů, kteří instalují stejné aktualizace současně, negativní zvýšení využití procesoru na serveru lokality. Toto chování může také zpomalit distribuční body a významně omezit dostupnou šířku pásma sítě.  

Pokud klienti musí instalovat požadované aktualizace softwaru v konečném termínu nasazení bez prodlevy, nakonfigurujte toto nastavení na **Ano**.

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Poskytnutá lhůta pro vynucení po termínu nasazení (hodiny)

Pokud chcete uživatelům poskytnout více času na instalaci požadované aplikace nebo nasazení aktualizace softwaru po uplynutí konečného termínu, nastavte hodnotu pro tuto možnost. Tato lhůta odkladu je pro počítač vypnutý po delší dobu a uživatel musí instalovat mnoho nasazení aplikace nebo aktualizace. Toto nastavení je užitečné například v případě, že se uživatel vrátí z dovolené a musí počkat delší dobu, než klient nainstaluje zpožděná nasazení aplikace.

Nastavte období odkladu na 0 až 120 hodin. Toto nastavení použijte spolu s vlastností nasazení **zpoždění vynucení tohoto nasazení podle uživatelských předvoleb**. Další informace najdete v tématu [nasazení aplikací](../../../apps/deploy-use/deploy-applications.md#delay-enforcement-with-a-grace-period).


### <a name="enable-endpoint-analytics-data-collection"></a>Povolit shromažďování dat služby Endpoint Analytics

Povolí místní shromažďování dat na klientovi pro nahrání do služby Endpoint Analytics. Nastavte na **Ano** , pokud chcete nakonfigurovat zařízení pro místní shromažďování dat. Nastavte na **ne** , pokud chcete zakázat místní shromažďování dat. Další informace najdete v tématu [registrace zařízení Configuration Manager do služby Endpoint Analytics](../../../../analytics/enroll-configmgr.md).

## <a name="computer-restart"></a>Restartování počítače

Další informace o těchto nastaveních najdete v tématu [oznámení o restartování zařízení](device-restart-notifications.md).<!-- 7182335 -->

## <a name="delivery-optimization"></a>Optimalizace doručení

<!-- 1324696 -->
Skupiny hranic Configuration Manager slouží k definování a regulaci distribuce obsahu napříč podnikovou sítí a vzdálenými pobočkami. [Optimalizace doručení Windows](/windows/deployment/update/waas-delivery-optimization) je cloudová technologie peer-to-peer pro sdílení obsahu mezi zařízeními s Windows 10. Nakonfigurujte optimalizaci doručení pro použití skupin hranic při sdílení obsahu mezi partnerskými uzly.

> [!Note]
> - Optimalizace doručení je dostupná jenom na klientech s Windows 10.
> - Přístup k Internetu do cloudové služby optimalizace doručování je nutný k využití svých funkcí peer-to-peer. Informace o potřebných koncových bodech internetu najdete v tématu [Nejčastější dotazy k optimalizaci doručení](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).
> - Při použití CMG pro úložiště obsahu se nebude obsah pro aktualizace třetích stran stahovat do klientů, pokud je povolený **rozdílový obsah ke stažení, pokud** je povolené [nastavení klienta](#allow-clients-to-download-delta-content-when-available) dostupné. <!--6598587--> 

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>Pro ID skupiny pro optimalizaci doručení použijte Configuration Manager skupiny hranic.

Vyberte **Ano** , pokud chcete použít identifikátor skupiny hranic jako identifikátor skupiny Optimalizace doručení na klientovi. Když klient komunikuje s cloudovou službou Optimalizace doručení, používá tento identifikátor k vyhledání partnerských uzlů s obsahem. Když toto nastavení povolíte, nastaví se režim stažení Optimalizace doručení na skupinu (2) u cílových klientů.

> [!Note]
> Microsoft doporučuje, aby klient mohl nakonfigurovat toto nastavení prostřednictvím místních zásad místo zásad skupiny. To umožňuje, aby byl identifikátor skupiny hranic nastaven jako identifikátor skupiny Optimalizace doručení na klientovi. Další informace najdete v tématu [Optimalizace doručení](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### <a name="enable-devices-managed-by-configuration-manager-to-use-microsoft-connected-cache-servers-for-content-download"></a>Povolit zařízením spravovaným pomocí Configuration Manager používat servery připojené mezipaměti od Microsoftu k stažení obsahu

<!--3555764-->
Vyberte možnost **Ano** , pokud chcete klientům povolit stahování obsahu z místního distribučního bodu, který povolíte jako server s připojenou mezipamětí společnosti Microsoft. Další informace najdete v tématu věnovaném [mezipaměti připojené k Microsoftu v Configuration Manager](../../plan-design/hierarchy/microsoft-connected-cache.md).


## <a name="endpoint-protection"></a>Funkce Endpoint Protection

> [!Tip]
> Kromě následujících informací můžete najít podrobnosti o použití Endpoint Protection nastavení klienta v [ukázkovém scénáři: použití Endpoint Protection k ochraně počítačů před malwarem](../../../protect/deploy-use/scenarios-endpoint-protection.md).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>Správa klienta Endpoint Protection v klientských počítačích

Pokud chcete spravovat existující Endpoint Protection a klienty Windows Defenderu na počítačích ve vaší hierarchii, vyberte **Ano** .  

Tuto možnost vyberte, pokud jste již nainstalovali klienta Endpoint Protection a chcete ho spravovat pomocí Configuration Manager. Tato samostatná instalace zahrnuje skriptový proces, který používá Configuration Manager aplikace nebo balíček a program. Zařízení s Windows 10 nemusí mít nainstalovaného agenta Endpoint Protection. Tato zařízení ale budou dál potřebovat **spravovat Endpoint Protection klienta na klientských počítačích** povolených. <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>Instalovat klienta Endpoint Protection na klientských počítačích

Chcete-li nainstalovat a povolit klienta Endpoint Protection v klientských počítačích, které již klienta nepoužívají, klikněte na tlačítko **Ano** . Klienti s Windows 10 nemusí mít nainstalovaného agenta Endpoint Protection.  

> [!NOTE]  
> Pokud je klient Endpoint Protection již nainstalován, pak výběrem možnosti **ne** nedojde k odinstalaci klienta Endpoint Protection. Chcete-li odinstalovat klienta Endpoint Protection, nastavte klientské nastavení **spravovat Endpoint Protection klienta v klientských počítačích** na hodnotu **ne**. Pak nasaďte balíček a program pro odinstalaci klienta Endpoint Protection.  

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Povolí instalaci klienta Endpoint Protection a restarty mimo časová období údržby. Časové intervaly pro správu a údržbu musí být pro instalaci klienta nejméně 30 minut dlouhé.

Nastavte tuto možnost na **Ano** , pokud chcete potlačit typické chování při instalaci s časovými obdobími údržby. Toto nastavení splňuje obchodní požadavky na prioritu údržby systému z hlediska zabezpečení.

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>Pro zařízení se systémem Windows Embedded s filtry zápisu potvrďte Endpoint Protection instalaci klienta (vyžaduje restart).

Zvolením možnosti **Ano** zakážete filtr zápisu na zařízení se systémem Windows Embedded a restartujete zařízení. Tato akce potvrdí instalaci na zařízení.  

Pokud zvolíte **ne**, klient se nainstaluje do dočasného překrytí, které se po restartu zařízení vymaže. V tomto scénáři se klient Endpoint Protection neinstaluje úplně, dokud jiná instalace nepotvrdí změny v zařízení. Tato konfigurace je výchozí.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Potlačit všechny požadavky na restart počítače po instalaci klienta Endpoint Protection

Kliknutím na **tlačítko Ano** potlačíte restart počítače po instalaci klienta Endpoint Protection.  

> [!IMPORTANT]  
> Pokud klient Endpoint Protection vyžaduje restart počítače a toto nastavení je **ne**, počítač se restartuje bez ohledu na nakonfigurované časové intervaly pro správu a údržbu.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>Povolené období, po které mohou uživatelé odložit požadovaný restart k dokončení instalace Endpoint Protection (hodiny)

Pokud je po instalaci klienta Endpoint Protection nutné restartovat, určuje toto nastavení počet hodin, po které mohou uživatelé odložit požadovaný restart. Toto nastavení vyžaduje, abyste zakázali následující nastavení: **potlačit po instalaci klienta Endpoint Protection nepotřebné restartování počítače**.

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>Zakázat alternativní zdroje (například Microsoft web Windows Update, Microsoft Windows Server Update Services nebo sdílené složky UNC) pro počáteční aktualizaci definice v klientských počítačích

Pokud chcete Configuration Manager instalovat pouze počáteční aktualizaci definice v klientských počítačích, vyberte možnost **Ano** . Toto nastavení může být užitečné při Vyhněte se zbytečným síťovým připojením a omezením šířky pásma sítě během počáteční instalace aktualizace definice.  



## <a name="enrollment"></a>Registrace

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Interval dotazování pro starší verze klientů mobilních zařízení

Vyberte **nastavit interval** , pokud chcete zadat dobu v minutách nebo v hodinách, po kterou se starší mobilní zařízení dotazují na zásadu. Mezi tato zařízení patří platformy, jako jsou systém Windows CE, macOS a UNIX nebo Linux.

### <a name="polling-interval-for-modern-devices-minutes"></a>Interval dotazování pro moderní zařízení (minuty)

Zadejte počet minut, po které se moderní zařízení dotazují na zásadu. Toto nastavení se používá pro zařízení s Windows 10 spravovaná prostřednictvím místní správy mobilních zařízení.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Umožnění uživatelům zapsat mobilní zařízení a počítače se systémem Mac

Pokud chcete povolit registraci starších zařízení na základě uživatele, nastavte tuto možnost na **Ano**a pak nakonfigurujte následující nastavení:

- **Registrační profil**: vyberte **nastavit profil** a vytvořte nebo vyberte registrační profil. Další informace najdete v tématu [Konfigurace nastavení klienta pro registraci](deploy-clients-to-macs.md#configure-client-settings).

### <a name="allow-users-to-enroll-modern-devices"></a>Umožňuje uživatelům registrovat moderní zařízení.

Pokud chcete povolit registraci moderních zařízení na základě uživatele, nastavte tuto možnost na **Ano**a pak nakonfigurujte následující nastavení:

- **Profil registrace moderního zařízení**: vyberte **nastavit profil** a vytvořte nebo vyberte registrační profil. Další informace najdete v tématu [Vytvoření profilu registrace, který umožňuje uživatelům registrovat moderní zařízení](../../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md#bkmk_createProf).



## <a name="hardware-inventory"></a>Inventář hardwaru  

### <a name="enable-hardware-inventory-on-clients"></a>Povolit inventář hardwaru na klientech

Ve výchozím nastavení je toto nastavení **Ano**. Další informace najdete v tématu [Úvod do inventáře hardwaru](../manage/inventory/introduction-to-hardware-inventory.md).

### <a name="hardware-inventory-schedule"></a>Plán inventáře hardwaru

Vyberte **plán** pro úpravu frekvence, kterou klienti spouštějí cyklus inventarizace hardwaru. Ve výchozím nastavení se tento cyklus objevuje každých 7 dní.

### <a name="maximum-random-delay-minutes"></a>Maximální náhodné zpoždění (minuty)

Zadejte maximální dobu v minutách, po kterou má klient Configuration Manager náhodně vymezit cyklus inventáře hardwaru od definovaného plánu. Tato náhodnost u všech klientů umožňuje zpracování inventáře vyrovnávání zatížení na serveru lokality. Můžete zadat libovolnou hodnotu mezi 0 a 480 minutami. Ve výchozím nastavení je tato hodnota nastavená na 240 minut (4 hodiny).

### <a name="maximum-custom-mif-file-size-kb"></a>Maximální velikost vlastního souboru MIF (kB)

Zadejte maximální velikost v kilobajtech (KB) povolenou pro každý vlastní soubor MIF (Management Information Format), který klient shromažďuje během cyklu inventáře hardwaru. Agent pro inventář hardwaru Configuration Manager nezpracovává žádné vlastní soubory MIF, které překračují tuto velikost. Můžete zadat velikost 1 KB až 5 120 KB. Ve výchozím nastavení je tato hodnota nastavena na 250 kB. Toto nastavení neovlivňuje velikost běžného datového souboru inventáře hardwaru.  

> [!NOTE]  
> Toto nastavení je dostupné pouze ve výchozím nastavení klienta.  

### <a name="hardware-inventory-classes"></a>Třídy inventáře hardwaru

Vyberte možnost **nastavit třídy** pro rozšiřování informací o hardwaru, které shromažďujete od klientů bez ruční úpravou souboru Sms_def. mof. Další informace najdete v tématu [Konfigurace inventáře hardwaru](../manage/inventory/configure-hardware-inventory.md).  

### <a name="collect-mif-files"></a>Shromáždit soubory MIF

Pomocí tohoto nastavení můžete určit, jestli se mají shromažďovat soubory MIF od Configuration Manager klientů během inventáře hardwaru.  

Aby soubor MIF mohl shromažďovat inventář hardwaru, musí být ve správném umístění v klientském počítači. Ve výchozím nastavení se soubory nacházejí v následujících cestách:  

- **Soubory IDMIF** by měly být ve složce Windows\System32\CCM\Inventory\Idmif..

- **Soubory NOIDMIF** by měly být ve složce Windows\System32\CCM\Inventory\Noidmif..

> [!NOTE]  
> Toto nastavení je dostupné pouze ve výchozím nastavení klienta.

## <a name="metered-internet-connections"></a>Měřené připojení k Internetu

Spravujte, jak počítače se systémem Windows 8 a novějším používají ke komunikaci s Configuration Manager měřené internetové připojení. Poskytovatelé připojení k internetu někdy účtují podle množství dat, která odesíláte a přijímáte, když máte měřené připojení k Internetu.

> [!NOTE]
> Nakonfigurované nastavení klienta se nepoužívá v následujících scénářích:
>
> - Pokud je počítač v roamingovém datovém připojení, klient Configuration Manager neprovádí žádné úlohy, které vyžadují přenos dat do Configuration Managerch lokalit.  
> - Pokud jsou vlastnosti síťového připojení systému Windows nakonfigurovány jako neměřené, klient Configuration Manager se chová, jako by připojení neměřené, a tak přenáší data do lokality.  

### <a name="client-communication-on-metered-internet-connections"></a>Komunikace klienta u měřených připojení k Internetu

Pro toto nastavení vyberte jednu z následujících možností:

- **Povolit**: veškerá komunikace s klienty se povoluje přes měřené připojení k Internetu, pokud klientské zařízení nepoužívá Roamingové datové připojení.

- **Omezení**: klient komunikuje pouze s měřeným připojením k Internetu pro následující chování:

  - Stáhnout zásady klienta

  - Odeslat zprávy o stavu klienta

  - Žádost o instalaci softwaru z centra softwaru

  - Stažení dalších zásad a obsahu pro požadovaná nasazení v konečném termínu instalace

  Pokud klient dosáhne limitu přenosu dat u měřeného připojení k Internetu, klient již nebude komunikovat s lokalitou nástroje.

- **Blok**: když je zařízení na měřeném připojení k Internetu, klient Configuration Manager se nebude pokoušet o komunikaci s lokalitou. Tato možnost je výchozí.

> [!IMPORTANT]
> Klient vždy povoluje softwarové instalace z centra softwaru bez ohledu na nastavení měřeného připojení k Internetu. Pokud uživatel požádá o instalaci softwaru, když je zařízení v měřené síti, Centrum softwaru respektuje záměr uživatele.<!-- MEMDocs#285 -->

Od verze 2006 klient nainstaluje a aktualizuje při konfiguraci nastavení tohoto klienta na hodnotu **Povolení** nebo **omezení**obě tyto činnosti: Díky tomuto chování může klient zůstat aktuální, ale stále spravovat komunikaci klienta v měřené síti. Toto chování můžete řídit při instalaci klienta s parametrem CCMSetup **/AllowMetered**. Další informace najdete v tématu [informace o parametrech instalace a vlastnostech klienta](../../clients/deploy/about-client-installation-properties.md#allowmetered).<!--6976145-->

## <a name="power-management"></a>Řízení spotřeby  

### <a name="allow-power-management-of-devices"></a>Povolení řízení spotřeby zařízení

Tuto možnost nastavte na **Ano** , pokud chcete na klientech Povolit řízení spotřeby. Další informace najdete v tématu [Úvod do řízení spotřeby](../manage/power/introduction-to-power-management.md).

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Povolit uživatelům vyloučit své zařízení z řízení spotřeby

Vyberte **Ano** , pokud chcete, aby uživatelé centra softwaru vyloučili svůj počítač ze všech nakonfigurovaných nastavení řízení spotřeby.  

### <a name="allow-network-wake-up"></a>Povolení probuzení ze sítě

Když toto nastavení povolíte, klient nakonfiguruje nastavení napájení v počítači, aby síťový adaptér mohl zařízení probudit. Pokud toto nastavení zakážete, síťový adaptér počítače nemůže probudit zařízení.

### <a name="enable-wake-up-proxy"></a>Povolit proxy probuzení

Zadejte **Ano** pro doplnění nastavení Wake on LAN lokality, když je nakonfigurována pro pakety jednosměrového vysílání.  

Další informace o proxy probuzení najdete v tématu [plánování probuzení klientů](plan/plan-wake-up-clients.md).  

> [!WARNING]  
> Nepovolujte proxy probuzení v produkční síti, aniž byste nejdřív pochopili, jak funguje a vyhodnotili v testovacím prostředí.  

Pak podle potřeby nakonfigurujte následující další nastavení:

- **Číslo portu proxy probuzení (UDP)**: číslo portu, které klienti používají k odesílání paketů buzení ze spánku do spících počítačů. Ponechte výchozí port 25536 nebo změňte číslo na hodnotu podle vlastního výběru.  

- **Wake on LAN číslo portu (UDP)**: ponechte výchozí hodnotu 9, pokud jste nezměnili číslo portu Wake on LAN (UDP) na kartě **porty** ve **vlastnostech**lokality.  

    > [!IMPORTANT]  
    > Toto číslo se musí shodovat s číslem ve **vlastnostech**lokality. Pokud změníte toto číslo na jednom místě, nebude automaticky aktualizováno na druhém místě.  

- **Výjimka firewallu v programu Windows Defender pro proxy probuzení**: klient Configuration Manager automaticky nakonfiguruje číslo portu proxy probuzení na zařízeních, která používají firewall v programu Windows Defender. Vyberte **Konfigurovat** a zadejte profily brány firewall.  

    Pokud klienti používají jinou bránu firewall, nakonfigurujte ji ručně, aby povolovala **číslo portu proxy probuzení (UDP)**.  

- **Předpony IPv6 v případě potřeby pro DirectAccess nebo jiná síťová zařízení. Pro zadání několika položek použijte čárku**: zadejte potřebné předpony IPv6 pro proxy probuzení pro fungování ve vaší síti.



## <a name="remote-tools"></a>Vzdálené nástroje  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>Povolit vzdálené řízení na klientech a profily výjimek brány firewall

Pokud chcete povolit funkci vzdáleného řízení Configuration Manager, vyberte **Konfigurovat** . Volitelně můžete nakonfigurovat nastavení brány firewall, aby bylo možné vzdálené řízení pracovat na klientských počítačích.  

Vzdálené řízení je ve výchozím nastavení zakázáno.  

> [!IMPORTANT]  
> Pokud nastavení brány firewall nenakonfigurujete, vzdálené řízení nemusí správně fungovat.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Uživatelé mohou změnit nastavení zásad nebo oznámení v programu Software Center

Vyberte, zda uživatelé mohou změnit možnosti vzdáleného řízení v centru softwaru.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Povolit Vzdálené řízení na bezobslužném počítači

Vyberte, zda může správce použít vzdálené řízení pro přístup ke klientskému počítači, který je odhlášený nebo uzamčený. Když je toto nastavení zakázané, dá se vzdáleně ovládat jenom přihlášený a odemčený počítač.  

### <a name="prompt-user-for-remote-control-permission"></a>Zobrazit výzvu uživateli pro oprávnění ke Vzdálenému řízení

Vyberte, zda klientský počítač před povolením relace vzdáleného řízení zobrazí zprávu s výzvou k zadání oprávnění uživatele.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Dotázat se uživatele na oprávnění k přenosu obsahu ze sdílené schránky

Před převodem obsahu ze sdílené schránky v relaci vzdáleného řízení Umožněte uživatelům možnost přijmout nebo odmítnout přenosy souborů. Uživatelé musí udělit oprávnění pouze jednou pro každou relaci. Prohlížeč nemůže udělit oprávnění k přenosu souboru.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Udělit oprávnění Vzdáleného řízení skupině místních správců

Vyberte, zda mohou místní správci na serveru, který spouští připojení vzdáleného řízení, vytvořit relace vzdáleného řízení v klientských počítačích.  

### <a name="access-level-allowed"></a>Úroveň přístupu povolena

Zadejte úroveň přístupu vzdáleného řízení k povolení. Vyberte z následujících nastavení:  

- **Zakázaný přístup**
- **Jenom zobrazení**
- **Úplné řízení**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Povolené prohlížeče vzdáleného řízení a vzdálené pomoci

Vyberte možnost **nastavit prohlížeče** a zadejte jména uživatelů systému Windows, kteří mohou vytvořit relace vzdáleného řízení v klientských počítačích.  

### <a name="show-session-notification-icon-on-taskbar"></a>Zobrazit ikonu oznámení relace na hlavním panelu

Konfigurací tohoto nastavení na **Ano** zobrazíte ikonu na hlavním panelu systému Windows, která označuje aktivní relaci vzdáleného řízení.  

### <a name="show-session-connection-bar"></a>Zobrazit panel připojení relace

Tuto možnost nastavte na **Ano** , pokud chcete zobrazit panel připojení relace s vysokou viditelností na klientech, abyste označili aktivní relaci vzdáleného řízení.  

### <a name="play-a-sound-on-client"></a>Zvukový signál na klientském počítači

Tuto možnost nastavte, pokud chcete použít zvuk, který indikuje, že relace vzdáleného řízení je aktivní v klientském počítači. Vyberte jednu z následujících možností:

- **Žádný zvuk**
- **Začátek a konec relace** (výchozí)
- **Opakovaně během relace**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>Spravovat nastavení nevyžádané Vzdálené pomoci

Konfigurací tohoto nastavení na **Ano** umožníte Configuration Manager spravovat relace nevyžádané vzdálené pomoci.  

V relaci nevyžádaná Vzdálená pomoc nepožádal uživatel na klientském počítači o pomoc při spuštění relace.  

### <a name="manage-solicited-remote-assistance-settings"></a>Spravovat nastavení vyžádané Vzdálené pomoci

Tuto možnost nastavte na **Ano** , pokud chcete Configuration Manager spravovat relace vyžádané vzdálené pomoci.  

V relaci vyžádané vzdálené pomoci odeslal uživatel v klientském počítači požadavek správci o vzdálenou pomoc.  

### <a name="level-of-access-for-remote-assistance"></a>Úroveň přístupu pro Vzdálenou pomoc

Vyberte úroveň přístupu, kterou chcete přiřadit k relacím vzdálené pomoci, které jsou spuštěny v konzole Configuration Manager. Vyberte jednu z následujících možností:

- **Žádný** (výchozí)
- **Vzdálené zobrazení**
- **Úplné řízení**

> [!NOTE]  
> Uživatel v klientském počítači musí vždy udělit oprávnění relaci vzdálené pomoci, aby mohla být zahájena.  

### <a name="manage-remote-desktop-settings"></a>Spravovat nastavení Vzdálené plochy

Tuto možnost nastavte na **Ano** , pokud chcete Configuration Manager spravovat relace vzdálené plochy pro počítače.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>Povolit povoleným prohlížečům připojit se pomocí připojení Vzdálené plochy

Tuto možnost nastavte na **Ano** , pokud chcete přidat uživatele zadané v seznamu povolených prohlížečů do místní skupiny uživatelů vzdálené plochy na klientech.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Vyžádat ověření na úrovni sítě na počítačích, na kterých běží operační systém Windows Vista a pozdější verze

Tuto možnost nastavte na **Ano** , pokud chcete k navázání připojení vzdálené plochy ke klientským počítačům použít ověřování na úrovni sítě (NLA). NLA zpočátku vyžaduje méně prostředků vzdálených počítačů, protože dokončí ověření uživatele předtím, než vytvoří připojení ke vzdálené ploše. Použití NLA je bezpečnější konfigurace. NLA pomáhá chránit počítač před uživateli se zlými úmysly nebo softwarem a snižuje riziko útoků DOS (Denial-of-Service).  



## <a name="software-center"></a>Centrum softwaru

### <a name="select-the-user-portal"></a>Výběr uživatelského portálu

<!--CMADO-3601237,INADO-4297660-->
Pokud nasadíte Portál společnosti do spoluspravovaných zařízení verze 2006, nakonfigurujte toto nastavení na **portál společnosti**. Toto nastavení zajistí, že uživatelé budou dostávat jenom oznámení od Portál společnosti.

Pokud Portál společnosti nainstalujete na spoluspravované zařízení, ale nakonfigurujete toto nastavení na **Centrum softwaru**, budou se uživatelům zobrazovat oznámení z obou portálů. Toto prostředí může být matoucí pro uživatele.

Pokud změníte nastavení klienta pro Portál společnosti, když uživatel vybere Configuration Manager oznámení, spustí Portál společnosti. Pokud je oznámení pro scénář, který Portál společnosti nepodporuje, pak se při výběru oznámení spustí Centrum softwaru.

Chování Portál společnosti závisí na konfiguraci úloh spolusprávy. Další informace najdete v tématu [použití portál společnosti aplikace na spoluspravovaných zařízeních](../../../comanage/company-portal.md).

### <a name="select-these-new-settings-to-specify-company-information"></a>Tato nová nastavení vyberte, pokud chcete zadat informace o společnosti.

Nastavte tuto možnost na **Ano**a potom zadejte následující nastavení pro branding Software Center ve vaší organizaci:

- **Název společnosti**: zadejte název organizace, který se uživatelům zobrazí v centru softwaru.  

- **Barevné schéma pro Centrum softwaru**: kliknutím na **Vybrat barvu** definujte primární barvu použitou centrem softwaru.  

- **Vyberte logo pro Centrum softwaru**: klikněte na **Procházet** a vyberte obrázek, který se zobrazí v centru softwaru. Logo musí mít formát JPEG, PNG nebo BMP 400 × 100 pixelů a maximální velikost 750 KB. Název souboru loga by neměl obsahovat mezery.  

### <a name="hide-unapproved-applications-in-software-center"></a><a name="bkmk_HideUnapproved"></a> Skrýt neschválené aplikace v centru softwaru

Pokud povolíte tuto možnost, aplikace dostupné pro uživatele, které vyžadují schválení, budou v centru softwaru skryté.<!--1355146-->

### <a name="hide-installed-applications-in-software-center"></a><a name="bkmk_HideInstalled"></a> Skrýt nainstalované aplikace v centru softwaru

Pokud povolíte tuto možnost, aplikace, které jsou již nainstalovány, již nebudou zobrazeny na kartě aplikace. Tato možnost je nastavená jako výchozí při instalaci nebo upgradu na Configuration Manager. Nainstalované aplikace jsou stále k dispozici pro kontrolu na kartě stav instalace. <!--1357592-->

### <a name="hide-application-catalog-link-in-software-center"></a><a name="bkmk_HideAppCat"></a> Skrýt odkaz na katalog aplikací v centru softwaru

Zadejte viditelnost odkazu webu Katalog aplikací v centru softwaru. Pokud je tato možnost nastavena, uživatelé neuvidí odkaz Web Application Catalog v uzlu stav instalace v centru softwaru. <!--1358214-->

> [!Important]  
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  

### <a name="software-center-tab-visibility"></a>Viditelnost karty centra softwaru

#### <a name="starting-in-version-1906"></a>Počínaje verzí 1906
<!--4063773-->

Vyberte, které karty by se měly zobrazovat v centru softwaru. K přesunutí karty na **viditelné karty**použijte tlačítko **Přidat** . Použijte tlačítko **Odebrat**  a přesuňte ho do seznamu **skrytých karet** . Seřazení karet pomocí tlačítek **Přesunout nahoru** nebo **Přesunout dolů** 

Karty k dispozici:
- **Aplikace**
- **Aktualizace**
- **Operační systémy**
- **Stav instalace**
- **Dodržování předpisů zařízení**
- **Možnosti**
- Kliknutím na tlačítko **Přidat kartu** přidejte až pět vlastních karet.
  - Zadejte **název karty** a **adresu URL obsahu** pro vlastní kartu.
  - Vyberte **Odstranit kartu** a odeberte tak vlastní kartu.  

  >[!Important]  
  > - Některé funkce webu nemusí fungovat při použití jako vlastní karty v centru softwaru. Před nasazením tohoto klienta na klienty Nezapomeňte otestovat výsledky. <!--519659-->
  > - Při přidání vlastní karty zadejte jenom důvěryhodné nebo intranetové adresy webu.<!--SCCMDocs issue 1575-->

#### <a name="version-1902-and-earlier"></a>Verze 1902 a starší

Nakonfigurujte další nastavení v této skupině na **Ano** , pokud chcete, aby byly v centru softwaru viditelné následující karty:

- **Aplikace**
- **Aktualizace**
- **Operační systémy**
- **Stav instalace**
- **Dodržování předpisů zařízení**
- **Možnosti**
- **Zadejte vlastní kartu pro Centrum softwaru** <!--1358132-->
    - **Název karty**
    - **Adresa URL obsahu**

    >[!Important]  
    > Některé funkce webu nemusí fungovat při použití jako vlastní karty v centru softwaru. Před nasazením tohoto klienta na klienty Nezapomeňte otestovat výsledky. <!--519659-->
    >
    > Při přidání vlastní karty zadejte jenom důvěryhodné nebo intranetové adresy webu.<!--SCCMDocs issue 1575-->

Pokud například vaše organizace nepoužívá zásady dodržování předpisů a chcete skrýt kartu dodržování předpisů zařízením v centru softwaru, nastavte **možnost povolit kartu dodržování předpisů zařízením** na **ne**.

### <a name="configure-default-views-in-software-center"></a><a name="bkmk_swctr_defaults"></a> Konfigurace výchozích zobrazení v centru softwaru
<!--3612112-->
*(Představené ve verzi 1902)*

- Nakonfigurujte **výchozí filtr aplikace** buď na **všechny** , nebo jenom na **požadované** aplikace.  

  - Centrum softwaru vždy používá vaše výchozí nastavení. Uživatelé můžou tento filtr změnit, ale Centrum softwaru neuchovává své preference.  

- Nastavte **výchozí zobrazení aplikace** jako buď **zobrazení dlaždic** nebo **zobrazení seznamu**.

  - Pokud uživatel tuto konfiguraci změní, Centrum softwaru bude v budoucnu nadále mít přednost před uživatelem.


## <a name="software-deployment"></a>Nasazení softwaru  

### <a name="schedule-re-evaluation-for-deployments"></a>Naplánovat opakované vyhodnocení nasazení

Nakonfigurujte plán, kdy Configuration Manager znovu vyhodnocuje pravidla požadavků pro všechna nasazení. Výchozí hodnota je každých 7 dní.  

> [!IMPORTANT]  
> Toto nastavení je více invazivní pro místního klienta, než je síť nebo server lokality. Efektivnější plán nového vyhodnocení má negativní vliv na výkon sítě a klientských počítačů. Microsoft nedoporučuje nastavit nižší hodnotu než výchozí. Pokud tuto hodnotu změníte, důkladně monitorujte výkon.  

Spusťte tuto akci z klienta následujícím způsobem: v ovládacím panelu **Configuration Manager** na kartě **Akce** vyberte **cyklus vyhodnocení nasazení aplikace**.  



## <a name="software-inventory"></a>Inventář softwaru  

### <a name="enable-software-inventory-on-clients"></a>Povolit inventář softwaru na klientech

Tato možnost je ve výchozím nastavení nastavená na **hodnotu Ano** . Další informace najdete v tématu [Úvod do inventáře softwaru](../manage/inventory/introduction-to-software-inventory.md).

### <a name="schedule-software-inventory-and-file-collection"></a>Plánování inventáře softwaru a sběru souborů

Vyberte **plán** pro úpravu frekvence, kterou klienti spouštějí cykly sběru inventáře softwaru a kolekcí souborů. Ve výchozím nastavení se tento cyklus objevuje každých 7 dní.

### <a name="inventory-reporting-detail"></a>Údaj pro vytvoření zprávy inventáře

Zadejte jednu z následujících úrovní informací o souboru do inventáře:

- **Pouze soubor**
- **Pouze produkt**
- **Úplné podrobnosti** (výchozí)

### <a name="inventory-these-file-types"></a>Inventarizovat tyto typy souborů

Chcete-li zadat typy souborů k inventarizaci, vyberte možnost **nastavit typy**a poté nakonfigurujte následující možnosti:  

> [!NOTE]  
> Pokud je v počítači použito více vlastních nastavení klienta, dojde ke sloučení inventáře, který jednotlivá nastavení vrátí.  

- Pokud chcete přidat nový typ souboru do inventáře, vyberte **Nový** . Pak v dialogovém okně **vlastnosti souboru inventáře** zadejte následující informace:  

    - **Název**: zadejte název souboru, který chcete uvést do inventáře. Použijte zástupný znak hvězdička ( `*` ), který představuje libovolný textový řetězec, a otazník ( `?` ), který představuje libovolný jednotlivý znak. Pokud například chcete inventarizaci všech souborů s příponou. doc, zadejte název souboru `*.doc` .  

    - **Umístění**: výběrem možnosti **nastavit** otevřete dialogové okno **Vlastnosti cesty** . Nakonfigurujte inventář softwaru, aby hledal zadaný soubor na všech pevných discích klientů, aby hledal zadanou cestu (například `C:\Folder` ), nebo vyhledá zadanou proměnnou (například `%windir%` ). Můžete také prohledat všechny podsložky v zadané cestě.  

    - **Vyloučení šifrovaných a komprimovaných souborů**: když zvolíte tuto možnost, všechny komprimované nebo zašifrované soubory se neinventáří.  

    - **Vyloučit soubory ve složce Windows**: když zvolíte tuto možnost, všechny soubory ve složce Windows a jejích podsložkách nejsou v inventáři.  

    Kliknutím na **tlačítko OK** zavřete dialogové okno **vlastnosti souboru v inventáři** . Přidejte všechny soubory, které chcete inventář, a pak výběrem **OK** zavřete dialogové okno **Konfigurovat nastavení klienta** .  

### <a name="collect-files"></a>Shromáždit soubory

Pokud chcete shromáždit soubory z klientských počítačů, vyberte možnost **nastavit soubory**a pak nakonfigurujte následující nastavení:  

> [!NOTE]  
> Pokud je v počítači použito více vlastních nastavení klienta, dojde ke sloučení inventáře, který jednotlivá nastavení vrátí.  

- V dialogovém okně **Konfigurovat nastavení klienta** vyberte možnost **nové** a přidejte soubor, který se má shromažďovat.  

- V dialogovém okně **Sebrané vlastnosti souboru** zadejte následující údaje:  

    - **Název**: zadejte název souboru, který chcete shromáždit. Použijte zástupný znak hvězdička ( `*` ), který představuje libovolný textový řetězec, a otazník ( `?` ), který představuje libovolný jednotlivý znak.  

    - **Umístění**: výběrem možnosti **nastavit** otevřete dialogové okno **Vlastnosti cesty** . Nakonfigurujte inventář softwaru, který bude hledat soubor, který chcete shromáždit, na všech pevných discích klienta, vyhledat zadanou cestu (například `C:\Folder` ) nebo vyhledat zadanou proměnnou (například `%windir%` ). Můžete také prohledat všechny podsložky v zadané cestě.  

    - **Vyloučit šifrované a komprimované soubory**: Pokud zvolíte tuto možnost, všechny komprimované nebo zašifrované soubory se neshromažďují.  

    - **Zastavit sběr souborů, když celková velikost souborů překročí (KB)**: zadejte velikost souboru v kilobajtech (KB), po jejímž uplynutí klient přestane shromažďovat zadané soubory.  

    > [!NOTE]  
    > Server lokality shromažďuje pět naposledy změněných verzí shromážděných souborů a ukládá je do `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol` adresáře. Pokud se soubor od posledního cyklu inventáře softwaru nezměnil, soubor se znovu shromáždí.  
    >
    > Inventář softwaru neshromažďuje soubory větší než 20 MB.  
    >
    > Hodnota **maximální velikost pro všechny shromážděné soubory (KB)** v dialogovém okně **Konfigurovat nastavení klienta** zobrazí maximální velikost všech shromážděných souborů. Po dosažení této velikosti se zastaví shromažďování souborů. Již shromážděné soubory jsou uchovány a odeslány na server lokality.  

    > [!IMPORTANT]
    > Pokud nakonfigurujete inventář softwaru, aby mohl shromažďovat mnoho velkých souborů, může tato konfigurace negativně ovlivnit výkon sítě a serveru lokality.  

    Informace o tom, jak zobrazit shromážděné soubory, najdete v tématu [použití Průzkumník prostředků k zobrazení inventáře softwaru](../manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    Kliknutím na **tlačítko OK** zavřete dialogové okno **sebrané vlastnosti souboru** . Přidejte všechny soubory, které chcete shromáždit, a pak kliknutím na **tlačítko OK** zavřete dialogové okno **Konfigurovat nastavení klienta** .  

### <a name="set-names"></a>Nastavit názvy

Agent pro inventarizaci softwaru načte názvy výrobců a produktů z hlavičky souboru. Tyto názvy nejsou vždycky standardizované v informacích o hlavičkách souborů. Při zobrazení inventáře softwaru v Průzkumník prostředků se může zobrazit různé verze stejného výrobce nebo názvu produktu. Chcete-li tyto zobrazované názvy standardizovat, vyberte možnost **nastavit názvy**a pak nakonfigurujte následující nastavení:  

- **Typ názvu**: inventář softwaru shromažďuje informace o výrobcích a produktech. Vyberte, zda chcete nakonfigurovat zobrazované názvy pro **výrobce** nebo **produkt**.  

- **Zobrazovaný název**: Zadejte zobrazovaný název, který chcete použít místo názvů v seznamu **názvy v inventáři** . Chcete-li zadat nový zobrazovaný název, vyberte možnost **Nový**.  

- **Názvy inventáře**: Pokud chcete přidat název v inventáři, vyberte **Nový**. Tento název se v inventáři softwaru nahradí názvem vybraným v seznamu **Zobrazovaný název** . Můžete přidat více názvů, které mají být nahrazeny.  



## <a name="software-metering"></a>Měření softwaru

### <a name="enable-software-metering-on-clients"></a>Povolit monitorování míry využívání softwaru na klientech

Toto nastavení je ve výchozím nastavení nastaveno na **Ano** . Další informace najdete v tématu [monitorování míry využívání softwaru](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md#configure-software-metering).

### <a name="schedule-data-collection"></a>Shromažďování dat plánu

Vyberte **plán** pro úpravu frekvence, kterou klienti spouštějí cyklus měření softwaru. Ve výchozím nastavení se tento cyklus objevuje každých 7 dní.



## <a name="software-updates"></a>Aktualizace softwaru  

### <a name="enable-software-updates-on-clients"></a>Povolit aktualizace softwaru na klientských počítačích

Pomocí tohoto nastavení můžete povolit aktualizace softwaru na Configuration Manager klientech. Když toto nastavení zakážete, Configuration Manager odebere existující zásady nasazení z klientů. Pokud toto nastavení znovu povolíte, klient stáhne aktuální zásadu nasazení.  

> [!IMPORTANT]  
> Když toto nastavení zakážete, zásady dodržování předpisů, které spoléhají na aktualizace softwaru, už nebudou fungovat.  

### <a name="software-update-scan-schedule"></a>Naplánování prohledání aktualizací softwaru

Vyberte **plán** , který určí, jak často bude klient spouštět kontrolu vyhodnocení dodržování předpisů. Tato kontrola určuje stav aktualizací softwaru na klientovi (například požadováno nebo nainstalováno). Další informace o vyhodnocení dodržování předpisů najdete v tématu [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

Ve výchozím nastavení tato kontrola používá jednoduchý plán, který se spustí každých 7 dní. Můžete vytvořit vlastní plán. Můžete zadat přesný den a čas spuštění, použít světový koordinovaný čas (UTC) nebo místní čas a nakonfigurovat periodický interval pro určitý den v týdnu.  

> [!NOTE]  
> Pokud zadáte interval méně než jeden den, Configuration Manager automatické výchozí nastavení na jeden den.  

> [!WARNING]  
> Skutečný čas spuštění v klientských počítačích je čas spuštění plus náhodné množství času, a to až do dvou hodin. Tato náhodnost znemožňuje klientským počítačům iniciovat kontrolu a současně se připojit k aktivnímu bodu aktualizace softwaru.  

### <a name="schedule-deployment-re-evaluation"></a>Naplánovat opakované vyhodnocení nasazení

Pokud chcete nakonfigurovat, jak často klientský Agent aktualizace softwaru znovu vyhodnocuje aktualizace softwaru pro stav instalace na Configuration Manager klientských počítačích, vyberte **plán** . Pokud se už dříve nainstalované aktualizace softwaru na klientech nenašly, ale pořád se vyžadují, klient znovu nainstaluje aktualizace softwaru.

Upravte tento plán na základě zásad společnosti pro dodržování předpisů aktualizací softwaru a zda uživatelé mohou odinstalovat aktualizace softwaru. Každý cyklus opakovaného vyhodnocení nasazení vede k aktivitě sítě a procesoru klientského počítače. Ve výchozím nastavení toto nastavení používá jednoduchý plán ke spuštění kontroly opakovaného vyhodnocení nasazení každých 7 dní.  

> [!NOTE]  
> Pokud zadáte interval méně než jeden den, Configuration Manager automatické výchozí nastavení na jeden den.  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Po dosažení konečného termínu nasazení aktualizace softwaru Nainstalujte všechna ostatní nasazení aktualizace softwaru s konečným termínem v zadaném časovém období.

Tuto možnost nastavte na **Ano** , pokud chcete nainstalovat všechny aktualizace softwaru z požadovaných nasazení se stejnými termíny v zadaném časovém období. Když požadované nasazení aktualizace softwaru dosáhne konečného termínu, klient spustí instalaci pro aktualizace softwaru v nasazení. Toto nastavení určuje, zda se mají instalovat aktualizace softwaru z jiných požadovaných nasazení, jejichž konečný termín spadá do určeného času.  

Pomocí tohoto nastavení lze zrychlit instalaci požadovaných aktualizací softwaru. Toto nastavení také může zvýšit zabezpečení klienta, snížit oznámení uživateli a snížit restart klienta. Výchozí hodnota tohoto nastavení je **Ne**.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>Časové období, po které budou také instalována všechna nevyřízená nasazení s konečným termínem v tomto čase

Toto nastavení slouží k zadání časového období pro předchozí nastavení. Můžete zadat hodnotu od 1 do 23 hodin a od 1 do 365 dnů. Ve výchozím nastavení je toto nastavení nakonfigurováno na sedm dní.  

### <a name="allow-clients-to-download-delta-content-when-available"></a>Umožňuje klientům stahovat rozdílový obsah, pokud je dostupný.

*(Představené ve verzi 1902)*

Tuto možnost nastavte na **Ano** , pokud chcete, aby klienti mohli používat soubory rozdílového obsahu. Toto nastavení umožňuje agentovi web Windows Update na zařízení určit, jaký obsah je potřeba, a selektivně ho stáhnout. 

- Než povolíte toto nastavení klienta, ujistěte se, že je pro vaše prostředí správně nakonfigurovaná Optimalizace doručení. Další informace najdete v tématu [optimalizace doručování systému Windows](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#windows-delivery-optimization) a [nastavení klienta Optimalizace doručení](#delivery-optimization).
 - Toto nastavení klienta nahrazuje **možnost Povolit instalaci expresních instalačních souborů na klientech**. Tuto možnost nastavte na **Ano** , pokud chcete klientům dovolit používat soubory rychlé instalace. Další informace najdete v tématu [Správa souborů Expresní instalace pro aktualizace Windows 10](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).
 - Od verze Configuration Manager 1910 platí, že při nastavení této možnosti se rozdílové stahování používá pro všechny instalační soubory služby Windows Update, nikoli jenom pro expresní instalační soubory.
    - Při použití CMG pro úložiště obsahu se nebude obsah pro aktualizace třetích stran stahovat do klientů, pokud je povolený **rozdílový obsah ke stažení, pokud** je povolené nastavení klienta dostupné. <!--6598587--> 


### <a name="port-that-clients-use-to-receive-requests-for-delta-content"></a>Port, který klienti používají pro příjem požadavků na rozdílový obsah

*(Představené ve verzi 1902)*

Toto nastavení nakonfiguruje místní port pro naslouchací proces HTTP, aby stahoval rozdílový obsah. Ve výchozím nastavení je nastavená na 8005. Tento port nemusíte otevírat v bráně firewall klienta. 

> [!NOTE]
>Toto nastavení klienta nahrazuje **port používaný ke stahování obsahu pro soubory rychlé instalace**.


### <a name="enable-management-of-the-office-365-client-agent"></a>Povolit správu klientského agenta Office 365

Pokud tuto možnost nastavíte na **Ano**, povolí se nastavení instalace Microsoft 365 aplikací. Umožňuje taky stahovat soubory ze sítí pro doručování obsahu (sítě CDN) pro Office a nasazovat soubory jako aplikaci v Configuration Manager. Další informace najdete v tématu [Správa aplikací Microsoft 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="enable-installation-of-software-updates-in-all-deployments-maintenance-window-when-software-update-maintenance-window-is-available"></a><a name="bkmk_SUMMaint"></a> Povolit instalaci aktualizací softwaru v časovém intervalu pro správu všech nasazení, když je k dispozici okno Údržba aktualizace softwaru

Pokud nastavíte tuto možnost na **Ano**a u klienta je nadefinovaná aspoň jedna aktualizace softwaru pro správu údržby, aktualizace softwaru se budou instalovat během časového období údržby všechna nasazení.

Výchozí hodnota tohoto nastavení je **Ne**. Tato hodnota používá stejné chování jako předtím: Pokud oba typy existují, ignoruje okno. <!--2839307-->

> [!NOTE]
> Toto nastavení platí i pro časové intervaly pro správu a údržbu, které nakonfigurujete pro **pořadí úkolů**.<!-- SCCMDocs-pr #4596 -->
>
> Pokud má klient k dispozici pouze okno **všechna nasazení** , bude nadále instalovat aktualizace softwaru nebo sekvence úloh v tomto okně.

#### <a name="maintenance-window-example"></a>Příklad okna údržby

Například nakonfigurujete následující časové intervaly pro správu a údržbu:

- **Všechna nasazení**: 02:00-04:00
- **Aktualizace softwaru**: 04:00-06:00

Ve výchozím nastavení klient nainstaluje jenom aktualizace softwaru v průběhu druhého okna údržby. Ignoruje časový interval pro správu a údržbu pro všechna nasazení v tomto scénáři. Když změníte toto nastavení na **Ano**, klient nainstaluje aktualizace softwaru mezi 02:00-06:00.


### <a name="specify-thread-priority-for-feature-updates"></a><a name="bkmk_thread-priority"></a> Zadat prioritu vlákna pro aktualizace funkcí

<!--3734525-->
Od verze Configuration Manager 1902 můžete upravit prioritu, s jakou klienti Windows 10 verze 1709 nebo novější nainstalují aktualizaci funkcí prostřednictvím [údržby Windows 10](../../../osd/deploy-use/manage-windows-as-a-service.md). Toto nastavení nemá žádný vliv na místní upgrady pořadí úkolů Windows 10.

Toto nastavení klienta nabízí následující možnosti:

- **Nenakonfigurováno**: Configuration Manager nemění nastavení. Správci mohou předem připravit vlastní soubor setupconfig.ini. Tato hodnota je výchozí.

- **Normální**: Instalační program systému Windows využívá více systémových prostředků a aktualizace rychleji. Využívá více času procesoru, takže celkový čas instalace je kratší, ale výpadek uživatele trvá.  

    - Nakonfiguruje setupconfig.ini soubor na zařízení pomocí `/Priority Normal` [Možnosti příkazového řádku instalačního programu systému Windows](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

- **Nízká**: během stahování a aktualizace na pozadí můžete pokračovat v práci na zařízení. Celková doba instalace je delší, ale výpadek uživatele je kratší. Možná bude nutné zvýšit maximální dobu běhu aktualizace, aby nedocházelo k vypršení časového limitu při použití této možnosti.  

    - Odebere `/Priority` z setupconfig.ini souboru [možnost příkazového řádku instalačního programu systému Windows](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) .


### <a name="enable-third-party-software-updates"></a>Povolit aktualizace softwaru třetích stran

Pokud nastavíte tuto možnost na **Ano**, nastaví zásady pro **Povolení podepsaných aktualizací pro intranetovou službu Microsoft Update** a nainstaluje podpisový certifikát do úložiště důvěryhodných vydavatelů na klientovi.

### <a name="enable-dynamic-update-for-feature-updates"></a><a name="bkmk_du"></a>Povolit dynamickou aktualizaci pro aktualizace funkcí
<!--4062619-->
Od verze Configuration Manager 1906 můžete nakonfigurovat [dynamickou aktualizaci pro Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847). Dynamická aktualizace instaluje jazykové sady, funkce na vyžádání, ovladače a kumulativní aktualizace během instalace systému Windows nasměrováním klienta na stažení těchto aktualizací z Internetu. Pokud je toto nastavení nastaveno na **hodnotu Ano** nebo **ne**, Configuration Manager upraví soubor [setupconfig](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) , který se používá při instalaci aktualizace funkcí.

- **Nenakonfigurováno** – výchozí hodnota. V souboru setupconfig se neprovádí žádné změny.
  - Dynamická aktualizace je ve výchozím nastavení povolená ve všech podporovaných verzích Windows 10.
    - Pro Windows 10 verze 1803 a předchozí dynamická aktualizace ověří server WSUS pro schválené dynamické aktualizace. V prostředí Configuration Manager se dynamické aktualizace nikdy neschvalují přímo na serveru WSUS, takže je tato zařízení nenainstalovala.
    - Počínaje systémem Windows 10 verze 1809 používá dynamická aktualizace připojení k Internetu zařízení k získání dynamické aktualizace z Microsoft Update. Tyto dynamické aktualizace nejsou publikované pro použití WSUS.
- **Ano** – povolí dynamickou aktualizaci.
- **Ne** – zakáže dynamickou aktualizaci.


## <a name="state-messaging"></a>Stavová zpráva

### <a name="state-message-reporting-cycle-minutes"></a>Cyklus hlášení stavových zpráv (minuty)

Určuje, jak často klienti hlásí stavové zprávy. Toto nastavení je ve výchozím nastavení 15 minut.



## <a name="user-and-device-affinity"></a>Spřažení uživatelů a zařízení  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Práh využití spřažení zařízení a uživatele (minuty)

Zadejte počet minut, po kterém Configuration Manager vytvoří mapování spřažení uživatelského zařízení. Ve výchozím nastavení je tato hodnota 2880 minut (dva dny).

### <a name="user-device-affinity-usage-threshold-days"></a>Práh využití spřažení zařízení a uživatele (dny)

Zadejte počet dní, po který klient měří prahovou hodnotu pro spřažení zařízení na základě využití. Ve výchozím nastavení je tato hodnota 30 dnů.

> [!NOTE]  
> Například zadáte **prahovou hodnotu využití spřažení zařízení a uživatele (minuty)** jako **60** minut a **prahovou hodnotu využití spřažení zařízení a uživatele (dny)** jako **5** dní. Uživatel musí zařízení používat po dobu 60 minut během období 5 dní, aby bylo možné vytvořit automatické spřažení se zařízením.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Automaticky konfigurovat spřažení zařízení a uživatele z dat o návštěvnosti webu

Pokud chcete vytvořit automatické spřažení uživatelských zařízení na základě informací o využití, které Configuration Manager shromažďuje, vyberte **Ano** .  

### <a name="allow-user-to-define-their-primary-devices"></a>Povolit uživateli definovat primární zařízení
<!--3485366-->
Pokud je toto nastavení **Ano**, uživatelé můžou identifikovat svá vlastní primární zařízení v centru softwaru. Další informace najdete v [uživatelské příručce k centru softwaru](../../understand/software-center.md#work-information).

## <a name="windows-diagnostic-data"></a>Diagnostická data Windows

> [!IMPORTANT]
> Tato skupina se dřív nazývala **Windows Analytics**. Microsoft vyřazení služby Windows Analytics od 31. ledna 2020. Další informace najdete v [článku KB 4521815: vyřazení služby Windows Analytics na 31. ledna 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Desktop Analytics je vývoj Windows Analytics. Pomocí desktopové analýzy můžete spravovat nastavení diagnostických dat Windows. Další informace najdete v tématu [co je Desktop Analytics](../../../desktop-analytics/overview.md).