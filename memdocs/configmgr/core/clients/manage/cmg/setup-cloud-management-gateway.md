---
title: Instalace brány pro správu cloudu
titleSuffix: Configuration Manager
description: Tento podrobný postup slouží k nastavení brány pro správu cloudu (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: a5800b40b581f2a65c4adcea0d229977ae61f774
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693331"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Nastavení brány pro správu cloudu pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento proces zahrnuje kroky potřebné k nastavení brány pro správu cloudu (CMG).

> [!Note]  
> Configuration Manager ve výchozím nastavení nepovolí tuto volitelnou funkci. Tuto funkci musíte před použitím povolit. Další informace naleznete v části [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options).

## <a name="before-you-begin"></a>Než začnete

Začněte tím, že si přečtete [plán článků pro bránu pro správu cloudu](plan-cloud-management-gateway.md). Pomocí tohoto článku můžete určit návrh CMG.

Pomocí následujícího kontrolního seznamu se ujistěte, že máte potřebné informace a předpoklady pro vytvoření CMG:  

- Prostředí Azure, které se má použít. Například veřejný cloud Azure nebo Cloud pro státní správu Azure USA.  

- V závislosti na návrhu budete potřebovat jeden nebo více certifikátů pro CMG. Další informace najdete v tématu [certifikáty pro bránu pro správu cloudu](certificates-for-cloud-management-gateway.md).  

- Pro [Azure Resource Manager](plan-cloud-management-gateway.md#azure-resource-manager) nasazení CMG potřebujete následující požadavky:  

  - Integrace se službou [Azure AD](../../../servers/deploy/configure/azure-services-wizard.md) pro **správu cloudu**. Zjišťování uživatelů služby Azure AD není vyžadováno. Pokud chcete web integrovat se službou Azure AD pro nasazení CMG pomocí Azure Resource Manager, budete potřebovat **globální správce**.

  - Poskytovatelé prostředků Microsoft. **ClassicCompute**  &  **Microsoft. Storage** musí být zaregistrovaní v rámci předplatného Azure. Další informace najdete v tématu [Azure Resource Manager](/azure/azure-resource-manager/resource-manager-supported-services).

  - K nasazení CMG se musí přihlásit **vlastník předplatného** .

- Globálně jedinečný název služby. Tento název pochází z [ověřovacího certifikátu serveru CMG](certificates-for-cloud-management-gateway.md#bkmk_serverauth).  

- Při povolování CMG jako distribučního bodu cloudu musí být stejný globálně jedinečný název služby CMG taky dostupný jako globálně jedinečný název účtu úložiště. Tento název pochází z [ověřovacího certifikátu serveru CMG](certificates-for-cloud-management-gateway.md#bkmk_serverauth).

- Oblast Azure pro toto nasazení CMG.  

- Kolik instancí virtuálních počítačů potřebujete pro škálování a redundanci.  

- Pokud stále potřebujete použít nasazení služby Azure Classic v Configuration Manager verze 1810 nebo starší, budete potřebovat následující požadavky:  

    > [!Important]  
    > Od verze 1810 jsou nasazení klasických služeb v Azure v Configuration Manager zastaralá. Pro bránu pro správu cloudu použijte Azure Resource Manager nasazení. Další informace najdete v tématu [plánování pro CMG](plan-cloud-management-gateway.md#azure-resource-manager).  
    >
    > Počínaje verzí 1902 Configuration Manager Azure Resource Manager je jediným mechanismem nasazení pro nové instance brány pro správu cloudu.<!-- 3605704 -->

  - ID předplatného Azure  

  - Certifikát pro správu Azure  

## <a name="set-up-a-cmg"></a>Nastavení CMG

Tento postup proveďte v lokalitě nejvyšší úrovně. Tato lokalita je buď samostatnou primární lokalitou, nebo lokalita centrální správy.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte možnost **Brána pro správu cloudu**.  

2. Na pásu karet vyberte **vytvořit brána pro správu cloudu** .  

3. Na stránce Obecné v průvodci vyberte **Přihlásit**se. Proveďte ověření pomocí účtu **vlastníka předplatného** Azure. Průvodce automaticky vyplní zbývající pole z informací uložených během předpokladu integrace služby Azure AD. Pokud vlastníte více předplatných, vyberte **ID předplatného** , které chcete použít.

    > [!Note]  
    > Od verze 1810 se nasazení klasických služeb v Azure už nepoužívá v Configuration Manager. Ve verzi 1902 a starší vyberte jako metodu nasazení CMG **Azure Resource Manager nasazení** .
    >
    > Pokud potřebujete použít klasické nasazení služby, vyberte tuto možnost na této stránce. Nejdřív zadejte své **ID předplatného**Azure. Pak vyberte **Procházet**a zvolte. Soubor PFX pro certifikát správy Azure.

4. Zadejte **prostředí Azure** pro tento CMG. Možnosti v rozevíracím seznamu se mohou lišit v závislosti na metodě nasazení.  

5. Vyberte **Další**. Počkejte, než lokalita otestuje připojení k Azure.  

6. Na stránce nastavení v průvodci vyberte možnost **Procházet** a zvolte. Soubor PFX pro ověřovací certifikát serveru CMG Název z tohoto certifikátu naplní požadovaná pole **plně kvalifikovaného názvu domény služby** a **názvu služby** .  

   > [!NOTE]  
   > Ověřovací certifikát serveru CMG podporuje zástupné znaky. Pokud používáte certifikát se zástupným znakem, nahraďte hvězdičku ( `*` ) v poli **plně kvalifikovaný název domény služby** požadovaným názvem hostitele pro CMG.<!--491233-->  

7. Vyberte rozevírací seznam **oblast** a zvolte oblast Azure pro tento CMG.  

8. Vyberte možnost **skupiny prostředků** .
   1. Pokud zvolíte možnost **použít existující**, pak v rozevíracím seznamu vyberte existující skupinu prostředků. Vybraná skupina prostředků už musí existovat v oblasti, kterou jste vybrali v kroku 7. Pokud vyberete existující skupinu prostředků, která je v jiné oblasti než dříve vybraná oblast, CMG se nepodaří zřídit.
   2. Pokud se rozhodnete **vytvořit nový**, zadejte nový název skupiny prostředků.

9. Do pole **instance virtuálního počítače** zadejte počet virtuálních počítačů pro tuto službu. Výchozí hodnota je jedna, ale můžete škálovat až 16 virtuálních počítačů na CMG.  

10. Vyberte **certifikáty** pro přidání důvěryhodných kořenových certifikátů klienta. Přidejte všechny certifikáty do řetězce důvěryhodnosti.  

    > [!Note]  
    > Důvěryhodný kořenový certifikát se nevyžaduje při použití Azure Active Directory (Azure AD) pro ověřování klientů. Pokud používáte certifikáty pro ověřování klientů PKI, musíte do CMG Přidat důvěryhodný kořenový certifikát.<!--SCCMDocs-pr issue #2872-->
    >
    > Ve verzi 1902 a starší můžete přidat pouze dva důvěryhodné kořenové certifikační autority a čtyři zprostředkující (podřízené) certifikační autority.<!-- SCCMDocs-pr#4022 -->

11. Ve výchozím nastavení Průvodce povolí možnost **ověřit odvolání klientského certifikátu**. Seznam odvolaných certifikátů (CRL) musí být veřejně publikovaný, aby tato kontrola fungovala. Další informace najdete v tématu [publikování seznamu odvolaných certifikátů](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

12. Počínaje verzí 1906 můžete **Vynutilit TLS 1,2**. Toto nastavení platí jenom pro virtuální počítač Azure Cloud Service. Nevztahuje se na žádné místní Configuration Manager servery lokality nebo klienty. Další informace o TLS 1,2 najdete v článku [Jak povolit tls 1,2](../../../plan-design/security/enable-tls-1-2.md).<!-- SCCMDocs-pr#4021 -->

13. Ve výchozím nastavení umožňuje průvodce následující možnost: povolit, **aby služba CMG fungovala jako distribuční bod cloudu a poskytovala obsah z Azure Storage**. CMG může také poskytovat obsah klientům. Tato funkce snižuje nároky na požadované certifikáty a náklady na virtuální počítače Azure.

14. Vyberte **Další**.  

15. Pokud chcete monitorovat provoz CMG s prahovou hodnotou 14 dní, zaškrtněte políčko, aby se výstraha prahové hodnoty zapnula. Pak zadejte prahovou hodnotu a procento, ve kterém chcete zvýšit počet různých úrovní výstrahy. Až budete hotovi, klikněte na tlačítko **Další** .  

16. Zkontrolujte nastavení a klikněte na tlačítko **Další**. Configuration Manager spustí nastavování služby. Po ukončení průvodce bude trvat pět až 15 minut, než se služba zřídí v Azure. Zkontrolujte sloupec **stav** nového CMG a určete, kdy bude služba připravena.  

    > [!NOTE]
    > K řešení potíží s nasazeními CMG použijte **CloudMgr. log** a **CMGSetup. log**. Další informace najdete v tématu [soubory protokolu](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).

## <a name="configure-primary-site-for-client-certificate-authentication"></a>Konfigurace primárního webového serveru pro ověřování klientských certifikátů

Pokud používáte certifikáty pro [ověřování](certificates-for-cloud-management-gateway.md#bkmk_clientauth) klientů k ověřování pomocí nástroje CMG, postupujte podle tohoto postupu, abyste nakonfigurovali každou primární lokalitu.  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte možnost **lokality**.  

2. Vyberte primární lokalitu, ke které jsou přiřazeni vaši internetoví klienti, a zvolte **vlastnosti**.  

3. Přepněte na seznam vlastností primární lokality na kartu **zabezpečení komunikace** , v případě, **že je k dispozici, zaškrtnout použít klientský certifikát PKI (ověřování klientů)**.  

    > [!NOTE]
    > Ve verzi 1902 a starší se tato karta nazývá **komunikace s klientským počítačem**.<!-- SCCMDocs#1645 -->

4. Pokud seznam CRL nepublikujete, zrušte výběr možnosti pro **klienty, kteří kontrolují seznam odvolaných certifikátů (CRL) pro systémy lokality**.  

## <a name="add-the-cmg-connection-point"></a>Přidání spojovacího bodu CMG

Bod připojení CMG je role systému lokality pro komunikaci s CMG. Chcete-li přidat bod připojení CMG, postupujte podle obecných pokynů pro [instalaci rolí systému lokality](../../../servers/deploy/configure/install-site-system-roles.md). Na stránce Výběr role systému v průvodci Přidat roli systému lokality vyberte **bod připojení brány pro správu cloudu**. Pak vyberte **název brány pro správu cloudu** , ke které se tento server připojuje. Průvodce zobrazí oblast pro vybrané CMG.

> [!IMPORTANT]
> Bod připojení CMG musí mít v některých scénářích [certifikát pro ověřování klientů](certificates-for-cloud-management-gateway.md#bkmk_clientauth) .

Pokud chcete řešit potíže se stavem služby CMG, použijte **CMGService. log** a **SMS_Cloud_ProxyConnector. log**. Další informace najdete v tématu [soubory protokolu](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).

## <a name="configure-client-facing-roles-for-cmg-traffic"></a><a name="bkmk_role"></a> Konfigurace klientských rolí pro provoz CMG

Konfigurujte body správy a systémy lokality bodu aktualizace softwaru pro příjem provozu CMG. Tento postup proveďte v primární lokalitě pro všechny body správy a body aktualizace softwaru, které používají internetové klienty.  

1. V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **servery a role systému lokality** . Na kartě Domů na pásu karet ve skupině zobrazení vyberte **servery s rolí**. Pak z tohoto seznamu vyberte **bod správy** .  

2. Vyberte server systému lokality, který chcete nakonfigurovat pro provoz CMG. V podokně podrobností vyberte roli **bod správy** a pak na pásu karet vyberte **vlastnosti** .  

3. V seznamu Vlastnosti bodu správy v části připojení klienta zaškrtněte políčko vedle možnosti **Configuration Manager provoz brány pro správu cloudu**.

    V závislosti na návrhu CMG a verzi Configuration Manager možná budete muset povolit možnost **https** . Další informace najdete v tématu [Povolení bodu správy pro protokol HTTPS](certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

4. Kliknutím na **tlačítko OK** zavřete okno Vlastnosti bodu správy.  

Opakujte tyto kroky pro další body správy podle potřeby a pro všechny body aktualizace softwaru.

## <a name="configure-boundary-groups"></a>Konfigurace skupin hranic
 
<!--3640932-->
Počínaje verzí 1902 můžete přidružit CMG k hraniční skupině. Tato konfigurace umožňuje klientům výchozí nebo záložní CMG pro komunikaci klientů podle vztahů skupin hranic.

Další informace o skupinách hranic najdete v tématu [Konfigurace skupin hranic](../../../servers/deploy/configure/boundary-groups.md).

Když [vytváříte nebo konfigurujete skupinu hranic](../../../servers/deploy/configure/boundary-group-procedures.md), na kartě **odkazy** přidejte bránu pro správu cloudu. Tato akce přidruží CMG k této skupině hranic.

## <a name="configure-clients-for-cmg"></a>Konfigurace klientů pro CMG

Jakmile CMG a role systému lokality běží, klienti získají automaticky umístění služby CMG při žádosti o další umístění. Klienti musí být na intranetu, aby mohli přijímat umístění služby CMG, pokud při [ověřování nenainstalujete a přiřadíte klienty s Windows 10 pomocí Azure AD](../../deploy/deploy-clients-cmg-azure.md). Cyklus cyklického dotazování na požadavky na umístění je každých 24 hodin. Pokud nechcete čekat na běžně naplánovaný požadavek na umístění, můžete žádost vynutit. Požadavek vynutíte restartováním služby Hostitel agenta serveru SMS (ccmexec.exe) v počítači.

> [!NOTE]
> Ve výchozím nastavení obdrží všichni klienti zásady CMG. Řízení tohoto chování pomocí nastavení klienta [umožní klientům používat bránu pro správu cloudu](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway).

Klient Configuration Manager automaticky určí, zda je na intranetu nebo Internetu. Pokud klient může kontaktovat řadič domény nebo místní bod správy, nastaví jeho typ připojení na **aktuálně intranet**. V opačném případě se přepne na **aktuálně Internet**a používá umístění služby CMG ke komunikaci s lokalitou.

> [!NOTE]
> Můžete vynutit, aby klient vždy používal CMG bez ohledu na to, jestli je na intranetu nebo Internetu. Tato konfigurace je užitečná pro účely testování nebo pro klienty, u kterých chcete vynutit, aby vždy používali CMG. V klientovi nastavte následující klíč registru:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> Toto nastavení můžete zadat i při instalaci klienta pomocí vlastnosti [CCMALWAYSINF](../../deploy/about-client-installation-properties.md#ccmalwaysinf) .
>
> Toto nastavení se bude používat vždycky, i když se klient bude přesouvat do umístění, kde by konfigurace skupiny hranic jinak využily místní prostředky.

Pokud chcete ověřit, že klienti mají zásady určující CMG, otevřete příkazový řádek prostředí Windows PowerShell jako správce na klientském počítači a spusťte následující příkaz:

```powershell
Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`
```

Tento příkaz zobrazí všechny internetové body správy, o kterých ví klient. I když CMG není technicky součástí internetového bodu správy, klienti ho budou zobrazovat jako jeden.

> [!NOTE]  
> K řešení potíží s klientskými přenosy CMG použijte **CMGHttpHandler. log**, **CMGService. log**a **SMS_Cloud_ProxyConnector. log**. Další informace najdete v tématu [soubory protokolu](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).

### <a name="install-off-premises-clients-using-a-cmg"></a>Instalace místních klientů pomocí CMG

Pro instalaci klienta Configuration Manager do systémů, které nejsou aktuálně připojené k intranetu, musí být jedna z následujících podmínek pravdivá. Ve všech případech se vyžaduje účet místního správce v cílových systémech.

1. Lokalita Configuration Manager je správně nakonfigurována tak, aby používala certifikáty PKI pro ověřování klientů. Kromě toho klientské systémy mají každý z nich již platný, jedinečný a důvěryhodný certifikát pro ověřování klientů.

2. Systémy jsou připojené k doméně Azure AD nebo k doméně Azure AD připojené k doméně.

3. Web používá Configuration Manager verze 2002 nebo novější.

Pokud pro možnosti 1 a 2 spustíte **ccmsetup.exe**, zadejte adresu URL CMG pomocí parametru **/MP** . Další informace najdete v tématu [informace o parametrech instalace a vlastnostech klienta](../../deploy/about-client-installation-properties.md#mp).

V případě možnosti 3 Configuration Manager počínaje verzí 2002 můžete nainstalovat klienta nástroje na systémy nepřipojené k intranetu pomocí hromadné registračního tokenu. Další informace o této metodě najdete v tématu [vytvoření registračního tokenu pro hromadnou registraci](../../deploy/deploy-clients-cmg-token.md#bulk-registration-token).

### <a name="configure-off-premises-clients-for-cmg"></a>Konfigurace místních klientů pro CMG

Systémy můžete propojit s nedávno nakonfigurovaným CMG, kde jsou splněné následující podmínky:  

- Systémy již mají nainstalovaného klienta Configuration Manager.

- Systémy nejsou připojené a nejde je připojit k intranetu.

- Systémy splňují jednu z následujících podmínek:

  - Každý z nich má certifikát s platným, jedinečným a důvěryhodným certifikátem pro ověření klienta.

  - Připojeno k doméně Azure AD

  - Připojení k doméně Hybrid Azure AD

- Nechcete nebo nemůžete úplně přeinstalovat stávajícího klienta.

- Máte způsob, jak změnit hodnotu registru počítače a restartovat službu **Hostitel agenta serveru SMS** pomocí účtu místního správce.

Pokud chcete vynutit připojení k těmto systémům, **REG_SZ** vytvořte `CMGFQDNs` v klíči položku registru REG_SZ `HKLM\Software\Microsoft\CCM` . Nastavte jeho hodnotu na adresu URL CMG, například `https://contoso-cmg.contoso.com` . Pak na zařízení restartujte službu systému Windows **hostitele agenta serveru SMS** .

Pokud klient Configuration Manager v registru nemá nastavenou aktuální CMG nebo internetový bod správy, automaticky zkontroluje `CMGFQDNs` hodnotu registru. Tato kontrolu probíhá každých 25 hodin, při spuštění služby **Hostitel agenta serveru SMS** nebo při zjištění změny sítě. Když se klient připojí k lokalitě a zjistí se CMG, tato hodnota se automaticky aktualizuje.

## <a name="modify-a-cmg"></a>Úprava CMG

### <a name="cmg-properties"></a>Vlastnosti CMG

Po vytvoření CMG můžete změnit některá z jeho nastavení. V konzole Configuration Manager vyberte CMG a vyberte **vlastnosti**. Nakonfigurujte nastavení na následujících kartách:  

#### <a name="general"></a>Obecné

- **Certifikát pro správu Azure**: změňte certifikát pro správu Azure pro CMG. Tato možnost je užitečná, když aktualizujete certifikát před jeho vypršením jeho platnosti.  

#### <a name="settings"></a>Nastavení

- **Soubor certifikátu**: Změňte ověřovací certifikát serveru pro CMG. Tato možnost je užitečná, když aktualizujete certifikát před jeho vypršením jeho platnosti.  

  > [!NOTE]
  > Po obnovení ověřovacího certifikátu serveru pro CMG se v plně kvalifikovaném názvu domény (CN) pro běžný název certifikátu rozlišují malá a velká písmena.  Pokud má aktuálně používaný certifikát například CN `https://contoso-cmg.contoso.com` , vytvoří nový certifikát se stejnou malým počtem CN. Průvodce nepřijme certifikát s CN `https://CONTOSO-CMG.CONTOSO.COM` .

- **Instance virtuálního počítače**: změňte počet virtuálních počítačů, které služba používá v Azure. Toto nastavení vám umožní dynamicky škálovat službu nahoru nebo dolů na základě informací o využití a nákladech.  

- **Certifikáty**: přidejte nebo odeberte certifikáty důvěryhodných kořenových certifikátů nebo zprostředkující certifikační autority. Tato možnost je užitečná při přidávání nových certifikačních autorit nebo vyřazování certifikátů s vypršenou platností.  

- **Ověřit odvolání klientského certifikátu**: Pokud jste při vytváření CMG nepovolili toto nastavení, můžete ho po publikování seznamu odvolaných certifikátů povolit později. Další informace najdete v tématu [publikování seznamu odvolaných certifikátů](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

- **Povolit, aby CMG fungoval jako distribuční bod cloudu a poskytoval obsah z Azure Storage**: Tato možnost je ve výchozím nastavení povolená. CMG může také poskytovat obsah klientům. Tato funkce snižuje nároky na požadované certifikáty a náklady na virtuální počítače Azure.<!--1358651-->

#### <a name="alerts"></a>Výstrahy

Překonfigurujte výstrahy kdykoli po vytvoření CMG.

### <a name="redeploy-the-service"></a>Opětovné nasazení služby

Důležitější změny, například následující konfigurace, vyžadují opětovné nasazení služby:

- Klasický způsob nasazení Azure Resource Manager
- Předplatné
- Název služby
- Privátní infrastruktura veřejných klíčů
- Region

Vždy udržujte aspoň jeden aktivní CMG pro internetové klienty pro příjem aktualizovaných zásad. internetoví klienti nemůžou komunikovat s odebraným CMG. Klienti neznají o novém, dokud nebudou moct přejít zpátky do intranetu. Při vytváření druhé instance CMG, která první odstraní, vytvoří také další spojovací bod CMG.

Klienti aktualizují zásady ve výchozím nastavení každých 24 hodin, takže před odstraněním staré CMG je třeba počkat aspoň jeden den po vytvoření nové. Pokud jsou klienti vypnuti nebo bez připojení k Internetu, možná budete muset počkat déle.

Pokud máte v klasické metodě nasazení existující CMG, musíte nasadit novou CMG pro použití metody nasazení Azure Resource Manager.<!--509753--> Existují dvě možnosti:  

- Pokud chcete znovu použít stejný název služby:  

    1. Nejdřív odstraňte klasický CMG s ohledem na pokyny, abyste měli vždy aspoň jeden aktivní CMG pro internetové klienty.  

    2. Vytvořte nový CMG pomocí nasazení Správce prostředků. Znovu použijte stejný ověřovací certifikát serveru.  

    3. Překonfigurujte bod připojení CMG, aby používal novou instanci CMG.  

- Pokud chcete použít nový název služby:  

    1. Vytvořte nový CMG pomocí nasazení Správce prostředků. Použijte nový ověřovací certifikát serveru.  

    2. Vytvořte nový spojovací bod CMG a připojte se k novému CMG.  

    3. Počkejte aspoň jeden den, aby internetoví klienti obdrželi zásady týkající se nového CMG.  

    4. Odstraňte klasický CMG.  

> [!TIP]
> Chcete-li zjistit aktuální model nasazení CMG:<!--SCCMDocs issue #611-->  
>
> 1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **Brána pro správu cloudu** .  
> 2. Vyberte instanci CMG.  
> 3. V podokně podrobností v dolní části okna vyhledejte atribut **model nasazení** . Pro nasazení Správce prostředků je tento atribut **Azure Resource Manager**. Starší verze modelu nasazení s certifikátem pro správu Azure se zobrazí jako **Azure Service Manager**.
>
> Můžete také přidat atribut **modelu nasazení** jako sloupec do zobrazení seznamu.  

### <a name="modifications-in-the-azure-portal"></a>Úpravy v Azure Portal

CMG se dá změnit jenom z konzoly Configuration Manager. Úpravy služby nebo podkladových virtuálních počítačů přímo v Azure se nepodporují. Jakékoli změny se můžou ztratit bez předchozího upozornění. Stejně jako u všech PaaS může služba kdykoli znovu sestavit virtuální počítače. Tato opětovné sestavení se mohou vyskytnout pro údržbu hardwaru back-endu nebo pro instalaci aktualizací operačního systému virtuálního počítače.

### <a name="delete-the-service"></a>Odstranit službu

Pokud potřebujete odstranit CMG, provedete to také z konzoly Configuration Manager. Ruční odebráním všech komponent v Azure dojde k nekonzistenci systému. Tento stav opouští osamocené informace a může dojít k neočekávanému chování.

## <a name="next-steps"></a>Další kroky

- [Monitorování klientů pro bránu pro správu cloudu](monitor-clients-cloud-management-gateway.md)
- [Nejčastější dotazy týkající se brány pro správu cloudu](cloud-management-gateway-faq.md)