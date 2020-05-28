---
title: Příklad nasazení certifikátu PKI
titleSuffix: Configuration Manager
description: Pomocí podrobného příkladu se naučíte, jak vytvořit a nasadit certifikáty PKI, které Configuration Manager používá.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 45ef103645630b8e203710ec0ff36a71b3cef4cf
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904251"
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-configuration-manager-windows-server-2008-certification-authority"></a>Podrobný ukázkový postup nasazení certifikátů PKI pro Configuration Manager: certifikační autorita systému Windows Server 2008

*Platí pro: Configuration Manager (Current Branch)*

Tento podrobný příklad nasazení využívajícího certifikační autoritu (CA) Windows serveru 2008 obsahuje postupy, které ukazují, jak vytvořit a nasadit certifikáty infrastruktury veřejných klíčů (PKI), které Configuration Manager používá. Tyto postupy používají certifikační autoritu organizace (CA) rozlehlé sítě a šablony certifikátů. Tyto kroky jsou vhodné pouze pro testovací síť, jako testování konceptu.  

Vzhledem k tomu, že pro požadované certifikáty není k dispozici žádná jediná metoda nasazení, požádejte o požadované postupy a osvědčené postupy pro nasazení požadovaných certifikátů pro produkční prostředí dokumentaci k příslušnému nasazení PKI. Další informace o požadavcích na certifikát najdete v tématu [požadavky na certifikát PKI pro Configuration Manager](pki-certificate-requirements.md).  

> [!TIP]
> Pokyny v tomto tématu můžete přizpůsobit pro operační systémy, které nejsou popsané v části požadavky na testovací síť. Pokud však spustíte vydávající CA v systému Windows Server 2012, nebudete vyzváni k zadání verze šablony certifikátu. Místo toho ho zadejte na kartě **Kompatibilita** ve vlastnostech šablony:  
>
> - **Certifikační autorita**: **Windows Server 2003**  
>   - **Příjemce certifikátu**: **Windows XP / Server 2003**  

## <a name="test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a>Požadavky na testovací síť

Z podrobných pokynů vyplývají následující požadavky:  

- V testovací síti je spuštěna služba Active Directory Domain Services a systém Windows Server 2008 a celá síť je nainstalována jako jediná doména, jediná doménová struktura.  

- Máte členský server, na kterém běží Windows Server 2008 Enterprise Edition, na kterém je nainstalovaná role služby AD CS (Active Directory Certificate Services) a je nastavená jako kořenová certifikační autorita organizace.  

- Máte jeden počítač s nainstalovaným operačním systémem Windows Server 2008 (Standard Edition nebo Enterprise Edition R2 nebo novější), tento počítač je označený jako členský server a v něm je nainstalovaná Internetová informační služba (IIS). Tento počítač bude Configuration Manager Server systému lokality, který budete konfigurovat pomocí intranetového plně kvalifikovaného názvu domény (FQDN) pro podporu připojení klientů v intranetu a internetového plně kvalifikovaného názvu domény (Pokud musíte podporovat mobilní zařízení, která jsou zaregistrovaná pomocí Configuration Manager a klientů na internetu).  

- Máte jednoho klienta systému Windows Vista s nainstalovanou nejnovější aktualizací Service Pack a tento počítač je nastaven s názvem počítače, který obsahuje znaky ASCII a je připojen k doméně. Tento počítač bude Configuration Manager klientský počítač.  

- Můžete se přihlásit pomocí účtu správce kořenové domény nebo účtu správce podnikové domény a používat tento účet pro všechny postupy v tomto ukázkovém nasazení.  

## <a name="overview-of-the-certificates"></a><a name="BKMK_overview2008"></a>Přehled certifikátů

V následující tabulce jsou uvedeny typy certifikátů PKI, které mohou být požadovány pro Configuration Manager a popisuje, jak se používají.  

|Požadavek na certifikát|Popis certifikátu|  
|-----------------------------|-----------------------------|  
|Certifikát webového serveru pro systémy lokality, které spouštějí IIS|Tento certifikát se používá pro šifrování dat a pro ověření serveru vůči klientům. Musí být nainstalovaná externě z Configuration Manager na serverech systémů lokality, na kterých běží Internetová informační služba (IIS) a které jsou nastavené v Configuration Manager na používání protokolu HTTPS.<br /><br /> Postup nastavení a instalace tohoto certifikátu najdete v části [Nasazení certifikátu webového serveru pro systémy lokality, které spouští službu IIS](#BKMK_webserver2008_cm2012) v tomto tématu.|  
|Certifikát služby pro klienty pro připojení ke cloudovým distribučním bodům|Postup pro konfiguraci a instalaci tohoto certifikátu naleznete v části [Nasazení certifikátu služby pro cloudové distribuční body](#BKMK_clouddp2008_cm2012) v tomto tématu.<br /><br /> **Důležité:** Tento certifikát se používá současně s certifikátem správy služby Windows Azure. Další informace o certifikátu správy najdete v tématu [Postup vytvoření certifikátu správy](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#create-a-new-self-signed-certificate) a [Přidání certifikátu pro správu do předplatného služby Windows Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate-portal#step-3-upload-a-certificate).|  
|Certifikát klienta pro počítače se systémem Windows|Tento certifikát se používá k ověření Configuration Manager klientských počítačů na systémy lokality, které jsou nastavené na používání protokolu HTTPS. Dá se taky použít pro body správy a body migrace stavu, abyste mohli monitorovat provozní stav, když jsou nastavené na používání protokolu HTTPS. Musí být nainstalováno externě z Configuration Manager na počítačích.<br /><br /> Postup nastavení a instalace tohoto certifikátu najdete v části [Nasazení certifikátu klienta pro počítače se systémem Windows](#BKMK_client2008_cm2012) v tomto tématu.|  
|Certifikát klienta pro distribuční body|Tento certifikát má dva účely:<br /><br /> Tento certifikát se používá k ověření distribučního bodu vůči bodu správy s povoleným protokolem HTTPS předtím, než distribuční bod odešle stavové zprávy.<br /><br /> Jestliže se pro distribuční bod vybere možnost **Povolení podpory PXE pro klienty** , certifikát se odešle do počítačů, které se spouštějí pomocí technologie PXE, tak aby se v průběhu nasazování operačního systému mohly připojit k bodu správy s povoleným protokolem HTTPS.<br /><br /> Postup nastavení a instalace tohoto certifikátu najdete v části [Nasazení certifikátu klienta pro distribuční body](#BKMK_clientdistributionpoint2008_cm2012) v tomto tématu.|  
|Certifikát zápisu pro mobilní zařízení|Tento certifikát se používá k ověření Configuration Manager klientů mobilních zařízení na systémy lokality, které jsou nastavené na používání protokolu HTTPS. Musí být nainstalovaný jako součást registrace mobilního zařízení v Configuration Manager a jako nastavení klienta mobilního zařízení zvolíte konfigurovanou šablonu certifikátu.<br /><br /> Postup nastavení tohoto certifikátu najdete v části [Nasazení certifikátu zápisu pro mobilní zařízení](#BKMK_mobiledevices2008_cm2012) v tomto tématu.|  
|Certifikát klienta pro počítače Mac|Tento certifikát si můžete vyžádat a nainstalovat z počítače Mac, když použijete Configuration Manager registrace a zvolíte nakonfigurovanou šablonu certifikátu jako nastavení klienta mobilního zařízení.<br /><br /> Postup nastavení tohoto certifikátu najdete v části [Nasazení certifikátu klienta pro počítače Mac](#BKMK_MacClient_SP1) v tomto tématu.|  

## <a name="deploy-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a>Nasazení certifikátu webového serveru pro systémy lokality, na nichž je spuštěna služba IIS

Nasazení tohoto certifikátu zahrnuje následující postupy:  

- Vytvoření a vydání šablony certifikátu webového serveru v certifikační autoritě  

- Vyžádání certifikátu webového serveru  

- Konfigurace služby IIS pro používání certifikátu webového serveru  

### <a name="create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a>Vytvoření a vydání šablony certifikátu webového serveru v certifikační autoritě

Tento postup vytvoří šablonu certifikátu pro Configuration Manager systémy lokality a přidá je do certifikační autority.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Pro vytvoření a vydání šablony certifikátu webového serveru pro certifikační autoritu

1.  Vytvořte skupinu zabezpečení s názvem **servery CONFIGMGR IIS** , která obsahuje členské servery pro instalaci Configuration Manager systémů lokality, které budou spouštět službu IIS.  

2.  Na členském serveru, na němž je nainstalována Certifikační služba, klikněte v konzole Certifikační úřad pravým tlačítkem na položku **šablony certifikátů** a výběrem **možnosti spravovat** načtěte konzolu **šablony certifikátů** .  

3.  V podokně výsledků klikněte pravým tlačítkem myši na položku, která má **webový server** ve sloupci **Zobrazovaný název šablony** a pak zvolte možnost **Duplikovat šablonu**.  

4.  V dialogovém okně **Duplikovat šablonu** zkontrolujte, zda je vybrána možnost **Windows 2003 Server, Enterprise Edition** , a pak zvolte možnost **OK**.  

    > [!IMPORTANT]  
    >  Nevybírejte možnost **Windows 2008 Server, Enterprise Edition**.  

5.  V dialogovém okně **Vlastnosti nové šablony** na kartě **Obecné** zadejte název šablony, jako je třeba **certifikát webového serveru ConfigMgr**, a vygenerujte webové certifikáty, které budou použity v Configuration Manager systémech lokality.  

6.  Vyberte kartu **název subjektu** a ujistěte se, že je vybrána možnost **dodat v žádosti** .  

7.  Zvolte kartu **zabezpečení** a pak odeberte oprávnění **zapsat** ze skupin zabezpečení **Domain Admins** a **Enterprise Admins** .  

8.  Zvolte **Přidat**, do textového pole zadejte **Servery ConfigMgr IIS** a pak zvolte **OK**.  

9. Vyberte oprávnění **zapsat** pro tuto skupinu a nemažte oprávnění **číst** .  

10. Zvolte **OK**a pak zavřete **konzolu šablony certifikátů**.  

11. V konzole Certifikační autorita klikněte pravým tlačítkem na **šablony certifikátů**, zvolte **Nový**a pak vyberte **Vystavovaná šablona certifikátu**.  

12. V dialogovém okně **Povolit šablony certifikátů** , vyberte novou šablonu, kterou jste právě vytvořili, **certifikát webového serveru ConfigMgr**, a pak zvolte **OK**.  

13. Pokud nepotřebujete vytvářet a vydávat další certifikáty, zavřete **certifikační autoritu**.  

###  <a name="request-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a>Vyžádání certifikátu webového serveru  
 Tento postup umožňuje zadat intranetové a internetové plně kvalifikované názvy domén, které budou nastaveny ve vlastnostech serveru systému lokality, a poté nainstaluje certifikát webového serveru na členský server, na kterém je spuštěna služba IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Pro vyžádání certifikátu webového serveru  

1.  Restartujte členský server, který spouští službu IIS, aby se zajistilo, že počítač bude mít přístup k šabloně certifikátu, kterou jste vytvořili pomocí oprávnění **číst** a **zapsat** , která jste nakonfigurovali.  

2.  Zvolte **Start**, zvolte **Spustit**a pak zadejte **MMC. exe.** V prázdné konzole klikněte na položku **soubor**a vyberte možnost **Přidat nebo odebrat modul snap-in**.  

3.  V dialogovém okně **Přidat nebo odebrat moduly snap-in** vyberte ze seznamu moduly **snap-in k dispozici**položku **certifikáty** a pak zvolte možnost **Přidat**.  

4.  V dialogovém okně **modul snap-in Certifikáty** zvolte položku **účet počítače**a klikněte na tlačítko **Další**.  

5.  V dialogovém okně **Vybrat počítač** zkontrolujte, zda je vybrána možnost **místní počítač: (počítač, na kterém je spuštěna tato konzola)** a poté klikněte na tlačítko **Dokončit**.  

6.  V dialogovém okně **Přidat nebo odebrat moduly snap-in** klikněte na **tlačítko OK**.  

7.  V konzole rozbalte položku **certifikáty (místní počítač)** a pak zvolte možnost **osobní**.  

8.  Klikněte pravým tlačítkem na **certifikáty**, vyberte **všechny úlohy**a pak zvolte **požádat o nový certifikát**.  

9. Na stránce **než začnete** klikněte na tlačítko **Další**.  

10. Pokud se zobrazí stránka **Vybrat zásady zápisu certifikátů** , klikněte na tlačítko **Další**.  

11. Na stránce **Vyžádat certifikáty** Identifikujte **certifikát webového serveru ConfigMgr** ze seznamu dostupných certifikátů a pak zvolte možnost **pro zápis tohoto certifikátu jsou požadovány další informace. Kliknutím sem můžete nakonfigurovat nastavení**.  

12. V dialogovém okně **Vlastnosti certifikátu** na kartě **subjekt** neprovádějte žádné změny v poli **název předmětu**. To znamená, že pole **Hodnota** pro oddíl **Název subjektu** zůstává prázdné. Místo toho v části **alternativní název** zvolte rozevírací seznam **typ** a pak zvolte možnost **DNS**.  

13. V poli **hodnota** zadejte plně kvalifikované názvy domén, které chcete zadat ve vlastnostech systému lokality Configuration Manager, a pak kliknutím na **tlačítko OK** zavřete dialogové okno **Vlastnosti certifikátu** .  

     Příklady:  

    - Pokud bude systém lokality akceptovat jenom připojení klientů z intranetu a intranetový plně kvalifikovaný název domény systémového serveru lokality je **Server1.Internal.contoso.com**, zadejte **Server1.Internal.contoso.com**a pak zvolte **Přidat**.  

    - Pokud systém lokality bude akceptovat připojení klientů z intranetu a z Internetu a intranetový plně kvalifikovaný název domény systémového serveru lokality je **Server1.Internal.contoso.com** a internetový plně kvalifikovaný název domény systémového serveru lokality je **Server.contoso.com**:  

        1.  Zadejte **Server1.Internal.contoso.com**a pak zvolte **Přidat**.  

        2.  Zadejte **Server.contoso.com**a pak zvolte **Přidat**.  

        > [!NOTE]  
        >  Plně kvalifikované názvy domény pro Configuration Manager můžete zadat v libovolném pořadí. Ověřte ale, že všechna zařízení, která budou používat certifikát, například mobilní zařízení a proxy webové servery, můžou používat alternativní název subjektu certifikátu (SAN) a více hodnot v síti SAN. Jestliže zařízení mají pro hodnoty SAN v certifikátech omezenou podporu, možná budete muset změnit pořadí hodnot plně kvalifikovaného názvu domény nebo místo toho používat Hodnotu subjektu.  

14. Na stránce **Vyžádat certifikáty** v seznamu dostupných certifikátů vyberte **certifikát webového serveru ConfigMgr** a pak zvolte **zapsat**.  

15. Na stránce **Výsledky instalace certifikátů** počkejte, než se nainstaluje certifikát, a pak zvolte **Dokončit**.  

16. Zavřete stránku **Certifikáty (místní)**.  

###  <a name="configure-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a>Konfigurace služby IIS pro používání certifikátu webového serveru  
 Tato procedura váže instalovaný certifikát na IIS **Výchozí web**.  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>Nastavení služby IIS pro používání certifikátu webového serveru  

1. Na členském serveru, který má nainstalovanou službu IIS, zvolte **Start**, zvolte **programy**, zvolte **Nástroje pro správu**a potom zvolte **Správce služby Internetová informační služba (IIS)**.  

2. Rozbalte **weby**, klikněte pravým tlačítkem na **výchozí web**a pak zvolte **Upravit vazby**.  

3. Zvolte položku **https** a pak zvolte **Upravit**.  

4. V dialogovém okně **Upravit vazbu webu** vyberte certifikát, který jste požadovali, a to pomocí šablony certifikáty webového serveru ConfigMgr a pak klikněte na **tlačítko OK**.  

   > [!NOTE]  
   >  Pokud si nejste jisti, který certifikát je správný, vyberte jeden a klikněte na tlačítko **Zobrazit**. To vám umožní porovnat podrobnosti vybraného certifikátu s certifikáty v modulu snap-in Certifikáty. Například modul snap-in Certifikáty zobrazí šablonu certifikátu, která byla použita k vyžádání certifikátu. Pak můžete porovnat kryptografický otisk certifikátu, který byl vyžádán, pomocí šablony certifikáty webového serveru ConfigMgr s kryptografickým otiskem certifikátu aktuálně vybraného certifikátu v dialogovém okně **Upravit vazbu webu** .  

5. V dialogovém okně **Upravit vazbu webu** zvolte **OK** a pak zvolte **Zavřít**.  

6. Zavřít **Správce služby Internetová informační služba (IIS)**.  

   Členský server je nyní nastaven s certifikátem Configuration Manager webového serveru.  

> [!IMPORTANT]  
>  Když na tento počítač nainstalujete Configuration Manager systémový server lokality, ujistěte se, že jste zadali stejné plně kvalifikované názvy domény ve vlastnostech systému lokality, jak jste určili, když jste si vyžádali certifikát.  

##  <a name="deploy-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a>Nasazení certifikátu služby pro cloudové distribuční body  

Nasazení tohoto certifikátu zahrnuje následující postupy:  

- [Vytvoření a vydání vlastní šablony certifikátu webového serveru v certifikační autoritě](#BKMK_clouddpcreating2008)  

- [Vyžádání vlastního certifikátu webového serveru](#BKMK_clouddprequesting2008)  

- [Export vlastního certifikátu webového serveru pro cloudové distribuční body](#BKMK_clouddpexporting2008)  

###  <a name="create-and-issue-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a>Vytvoření a vydání vlastní šablony certifikátu webového serveru v certifikační autoritě  
 Tento postup vytvoří vlastní šablonu certifikátu založenou na šabloně certifikátu webového serveru. Certifikát je pro Configuration Manager cloudových distribučních bodů a je nutné exportovat privátní klíč. Po vytvoření je šablona certifikátu přidána do konzoly Certifikační úřad.  

> [!NOTE]
>  Tento postup používá šablonu certifikátu odlišnou od šablony certifikátu webového serveru, kterou jste vytvořili pro systémy lokalit, které spouští službu IIS. I když oba certifikáty vyžadují schopnost ověřování serveru, certifikát pro cloudové distribuční body vyžaduje, abyste zadali vlastní definovanou hodnotu pro název subjektu a pak se musí exportovat privátní klíč. Z hlediska zabezpečení je nejvhodnější vytvořit šablony certifikátů, aby bylo možné exportovat privátní klíč, pokud není tato konfigurace požadována. Cloudový distribuční bod vyžaduje tuto konfiguraci, protože musíte importovat certifikát jako soubor a nemusíte ho zvolit z úložiště certifikátů.  
> 
>  Při vytváření nové šablony certifikátu pro tento certifikát můžete omezit počítače, které mohou požadovat certifikát, jehož privátní klíč lze exportovat. V produkční síti můžete také zvážit přidání následujících změn pro tento certifikát:  
> 
> - Vyžadovat schválení pro instalaci certifikátu pro další zabezpečení  
>   - Prodloužení doby platnosti certifikátu. Vzhledem k tomu, že je nutné exportovat a importovat certifikát pokaždé, když jeho platnost vyprší, prodloužení doby platnosti sníží, jak často je nutné tento postup opakovat. Zvýšení doby platnosti však také zkracuje zabezpečení certifikátu, protože poskytuje více času, než by útočník mohl dešifrovat privátní klíč a ukrást certifikát.  
>   - Vlastní hodnota alternativního názvu předmětu Subject Alternative Name (SAN) pomáhá rozpoznat tento certifikát od standardních certifikátů webových serverů, které používáte se službou IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Vytvoření a vystavení vlastní šablony certifikátu webového serveru v certifikační autoritě  

1.  Vytvořte skupinu zabezpečení nazvanou **ConfigMgr Site Servers** , která má členské servery k instalaci Configuration Manager servery primární lokality, které budou spravovat cloudové distribuční body.  

2.  Na členském serveru, na němž je spuštěna konzola certifikační úřad, klikněte pravým tlačítkem na **šablony certifikátů**a pak zvolte **Spravovat** a načtěte konzolu pro správu šablon certifikátů.  

3.  V podokně výsledků klikněte pravým tlačítkem myši na položku, která má **webový server** ve sloupci **Zobrazovaný název šablony** a pak zvolte možnost **Duplikovat šablonu**.  

4.  V dialogovém okně **Duplikovat šablonu** zkontrolujte, zda je vybrána možnost **Windows 2003 Server, Enterprise Edition** , a pak zvolte možnost **OK**.  

    > [!IMPORTANT]  
    >  Nevybírejte možnost **Windows 2008 Server, Enterprise Edition**.  

5.  V dialogovém okně **Vlastnosti nové šablony** na kartě **Obecné** zadejte název šablony, jako je například **certifikát cloudového distribučního bodu nástroje ConfigMgr**, pro vygenerování certifikátu webového serveru pro cloudové distribuční body.  

6.  Zvolte kartu **vyřízení žádosti** a pak zvolte možnost **umožní export privátního klíče**.  

7.  Zvolte kartu **zabezpečení** a pak odeberte oprávnění **zapsat** ze skupiny zabezpečení **Enterprise Admins** .  

8.  Zvolte **Přidat**, do textového pole zadejte **Servery ConfigMgr Site Server** a pak zvolte **OK**.  

9. Vyberte oprávnění **zapsat** pro tuto skupinu a nemažte oprávnění **číst** .  

10. Vyberte kartu **kryptografie** a ujistěte se, že je **minimální velikost klíče** nastavená na **2048**.

11. Zvolte **OK**a pak zavřete **konzolu šablony certifikátů**.  

12. V konzole Certifikační autorita klikněte pravým tlačítkem na **šablony certifikátů**, zvolte **Nový**a pak vyberte **Vystavovaná šablona certifikátu**.  

13. V dialogovém okně **Povolit šablony certifikátů** zvolte novou šablonu, kterou jste právě vytvořili, **certifikát cloudového distribučního bodu nástroje ConfigMgr**, a pak zvolte **OK**.  

14. Pokud nepotřebujete vytvářet a vydávat další certifikáty, zavřete **certifikační autoritu**.  

###  <a name="request-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a>Vyžádání vlastního certifikátu webového serveru  
 Tato procedura vyžádá a pak nainstaluje vlastní certifikát webového serveru na členský server, na kterém bude server lokality běžet.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Vyžádání vlastního certifikátu webového serveru  

1.  Restartujte členský server, když vytvoříte a nakonfigurujete skupinu zabezpečení **webové servery nástroje ConfigMgr** , abyste zajistili, že počítač bude mít přístup k šabloně certifikátu, kterou jste vytvořili pomocí oprávnění **číst** a **zapsat** , která jste nakonfigurovali.  

2.  Zvolte **Start**, zvolte **Spustit**a pak zadejte **MMC. exe.** V prázdné konzole klikněte na položku **soubor**a vyberte možnost **Přidat nebo odebrat modul snap-in**.  

3.  V dialogovém okně **Přidat nebo odebrat moduly snap-in** vyberte ze seznamu moduly **snap-in k dispozici**položku **certifikáty** a pak zvolte možnost **Přidat**.  

4.  V dialogovém okně **modul snap-in Certifikáty** zvolte položku **účet počítače**a klikněte na tlačítko **Další**.  

5.  V dialogovém okně **Vybrat počítač** zkontrolujte, zda je vybrána možnost **místní počítač: (počítač, na kterém je spuštěna tato konzola)** a poté klikněte na tlačítko **Dokončit**.  

6.  V dialogovém okně **Přidat nebo odebrat moduly snap-in** klikněte na **tlačítko OK**.  

7.  V konzole rozbalte položku **certifikáty (místní počítač)** a pak zvolte možnost **osobní**.  

8.  Klikněte pravým tlačítkem na **certifikáty**, vyberte **všechny úlohy**a pak zvolte **požádat o nový certifikát**.  

9. Na stránce **než začnete** klikněte na tlačítko **Další**.  

10. Pokud se zobrazí stránka **Vybrat zásady zápisu certifikátů** , klikněte na tlačítko **Další**.  

11. Na stránce **Vyžádat certifikáty** Identifikujte **certifikát cloudového distribučního bodu nástroje ConfigMgr** ze seznamu dostupných certifikátů a pak zvolte možnost **k zápisu tohoto certifikátu jsou požadovány další informace. Chcete-li konfigurovat nastavení, zvolte zde**.  

12. V dialogovém okně **Vlastnosti certifikátu** na kartě **subjekt** v poli **název subjektu**jako **typ**vyberte **běžný název** .  

13. V poli **Hodnota** zadejte vaši volbu názvu služby a název vaší domény ve formátu FQDN. Příklad: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  V oboru názvů nastavte jedinečný název služby. Použijte službu DNS k vytvoření zástupce (záznam CNAME) pro mapování názvu této služby pro automaticky vytvářený identifikátor (GUID) a IP adresu z platformy Windows Azure.  

14. Zvolte možnost **Přidat**a potom kliknutím na **tlačítko OK** zavřete dialogové okno **Vlastnosti certifikátu** .  

15. Na stránce **Vyžádat certifikáty** zvolte **certifikát cloudového distribučního bodu nástroje ConfigMgr** ze seznamu dostupných certifikátů a pak zvolte možnost **zapsat**.  

16. Na stránce **Výsledky instalace certifikátů** počkejte, než se nainstaluje certifikát, a pak zvolte **Dokončit**.  

17. Zavřete stránku **Certifikáty (místní)**.  

###  <a name="export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a>Export vlastního certifikátu webového serveru pro cloudové distribuční body  
 Tento postup exportuje vlastní certifikát webového serveru do souboru, takže může být importován, když vytvoříte cloudový distribuční bod.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Export vlastního certifikátu webového serveru pro cloudové distribuční body  

1. V konzole **certifikáty (místní počítač)** klikněte pravým tlačítkem na certifikát, který jste právě nainstalovali, zvolte možnost **všechny úlohy**a pak zvolte **exportovat**.  

2. V Průvodci exportem certifikátů klikněte na tlačítko **Další**.  

3. Na stránce **exportovat soukromý klíč** vyberte možnost **Ano, exportovat privátní klíč**a klikněte na tlačítko **Další**.  

   > [!NOTE]  
   >  Pokud tato možnost není k dispozici, certifikát byl vytvořen bez možnosti exportu soukromého klíče. V tomto případě nemůžete exportovat certifikát v požadovaném formátu. Je nutné nastavit šablonu certifikátu tak, aby bylo možné exportovat soukromý klíč, a pak znovu požádat o certifikát.  

4. Na stránce **Formát souboru pro export** zajistěte, aby soubor **Personal Information Exchange-PKCS #12 (. **Je vybraná možnost PFX.  

5. Na stránce **heslo** zadejte silné heslo pro ochranu exportovaného certifikátu s jeho privátním klíčem a pak zvolte **Další**.  

6. Na stránce **soubor k exportu** zadejte název souboru, který chcete exportovat, a klikněte na tlačítko **Další**.  

7. Chcete-li ukončit průvodce, klikněte na tlačítko **Dokončit** na stránce **Průvodce exportem certifikátu** a pak zvolte možnost **OK** v potvrzovacím dialogovém okně.  

8. Zavřete stránku **Certifikáty (místní)**.  

9. Uložte soubor bezpečně a ujistěte se, že k němu máte přístup z konzoly Configuration Manager.  

   Certifikát je nyní připraven k importu, když vytvoříte cloudový distribuční bod.  

##  <a name="deploy-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a>Nasazení certifikátu klienta pro počítače se systémem Windows  
 Nasazení tohoto certifikátu zahrnuje následující postupy:  

- Vytvoření a vystavení šablony ověřovacího certifikátu pracovní stanice v certifikační autoritě  

- Konfigurace automatického zápisu šablony ověření pracovní stanice pomocí Zásady skupiny  

- Automatický zápis ověřovacího certifikátu pracovní stanice a ověření jeho instalace na počítačích  

###  <a name="create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a>Vytvoření a vystavení šablony ověřovacího certifikátu pracovní stanice v certifikační autoritě  
 Tento postup vytvoří šablonu certifikátu pro Configuration Manager klientských počítačů a přidá ji do certifikační autority.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Vytvoření a vystavení šablony ověřovacího certifikátu pracovní stanice v konzole Certifikační úřad  

1.  Na členském serveru, na němž je spuštěna konzola certifikační úřad, klikněte pravým tlačítkem na **šablony certifikátů**a pak zvolte **Spravovat** a načtěte konzolu pro správu šablon certifikátů.  

2.  V podokně výsledků klikněte pravým tlačítkem na položku, která má **ověřování pracovní stanice** ve sloupci **Zobrazovaný název šablony** a pak zvolte možnost **Duplikovat šablonu**.  

3.  V dialogovém okně **Duplikovat šablonu** zkontrolujte, zda je vybrána možnost **Windows 2003 Server, Enterprise Edition** , a pak zvolte možnost **OK**.  

    > [!IMPORTANT]  
    >  Nevybírejte možnost **Windows 2008 Server, Enterprise Edition**.  

4.  V dialogovém okně **Vlastnosti nové šablony** na kartě **Obecné** zadejte název šablony, jako je například **klientský certifikát nástroje ConfigMgr**, k vygenerování klientských certifikátů, které budou použity v Configuration Manager klientských počítačích.  

5.  Zvolte kartu **zabezpečení** , vyberte skupinu **Domain Computers** a potom vyberte další oprávnění **číst** a **automaticky zapsat**. Nerušte oprávnění **Zapsat**.  

6.  Zvolte **OK**a pak zavřete **konzolu šablony certifikátů**.  

7.  V konzole Certifikační autorita klikněte pravým tlačítkem na **šablony certifikátů**, zvolte **Nový**a pak vyberte **Vystavovaná šablona certifikátu**.  

8.  V dialogovém okně **Povolit šablony certifikátů** , vyberte novou šablonu, kterou jste právě vytvořili, **klientský certifikát nástroje ConfigMgr**, a pak zvolte **OK**.  

9. Pokud nepotřebujete vytvářet a vydávat další certifikáty, zavřete **certifikační autoritu**.  

###  <a name="configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a>Konfigurace automatického zápisu šablony ověření pracovní stanice pomocí Zásady skupiny  
 Tento postup nastaví Zásady skupiny pro automatický zápis klientského certifikátu na počítače.  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Nastavení automatického zápisu šablony ověření pracovní stanice pomocí Zásady skupiny  

1.  Na řadiči domény klikněte na tlačítko **Start**, zvolte **Nástroje pro správu**a potom zvolte možnost **Správa Zásady skupiny**.  

2.  Přejděte do domény, klikněte pravým tlačítkem na doménu a pak zvolte **vytvořit objekt zásad skupiny v této doméně a propojit ho sem**.  

    > [!NOTE]  
    >  Tento krok používá nejlepší postup vytvoření nových zásad skupiny pro vlastní nastavení místo úpravy výchozích zásad domény, které jsou nainstalovány se službou Active Directory Domain Services. Když tuto Zásady skupiny přiřadíte na úrovni domény, použijete ji pro všechny počítače v doméně. V produkčním prostředí můžete automatický zápis omezit tak, aby se zaregistroval jenom na vybraných počítačích. Zásady skupiny můžete přiřadit na úrovni organizační jednotky, nebo můžete Zásady skupiny domény filtrovat se skupinou zabezpečení tak, aby platila pouze pro počítače ve skupině. Pokud automatický zápis omezíte, nezapomeňte zahrnout server, který je nastaven jako bod správy.  

3.  V dialogovém okně **Nový objekt zásad skupiny** zadejte název, třeba certifikáty pro automatické **zápis**, pro nové zásady skupiny a pak zvolte **OK**.  

4.  V podokně výsledků na kartě **propojené zásady skupiny objekty** klikněte pravým tlačítkem na nový zásady skupiny a pak zvolte **Upravit**.  

5.  V **Editor pro správu zásad skupiny**rozbalte v části **Konfigurace počítače** **zásady** a pak klikněte na **nastavení Windows**nastavení  /  **zabezpečení**  /  **Zásady veřejných klíčů**.  

6.  Klikněte pravým tlačítkem myši na typ objektu s názvem **klient služby Certificate Services – automatický zápis**a pak zvolte možnost **vlastnosti**.  

7.  V rozevíracím seznamu **model konfigurace** zvolte možnost **povoleno**, zvolte možnost **obnovit certifikáty s vypršenou platností, aktualizovat nevyřízené certifikáty, odebrat odvolané certifikáty**, zvolte možnost **aktualizovat certifikáty, které používají šablony certifikátů**, a pak zvolte možnost **OK**.  

8.  Ukončete **správu Zásady skupiny**.  

###  <a name="automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-computers"></a><a name="BKMK_client22008"></a>Automatický zápis ověřovacího certifikátu pracovní stanice a ověření jeho instalace na počítačích  
 Tento postup nainstaluje klientský certifikát na počítače a ověří instalaci  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Automatický zápis ověřovacího certifikátu pracovní stanice a ověření jeho instalace na klientském počítači  

1. Restartujte počítač pracovní stanice a počkejte několik minut, než se přihlásíte.  

   > [!NOTE]  
   >  Restartování počítače je nejspolehlivější způsob zajištění úspěšného automatického zápisu certifikátu.  

2. Přihlaste se pomocí účtu, který má oprávnění správce.  

3. Do vyhledávacího pole zadejte **MMC. exe.** a pak stiskněte klávesu **ENTER**.  

4. V prázdné konzole pro správu klikněte na položku **soubor**a vyberte možnost **Přidat nebo odebrat modul snap-in**.  

5. V dialogovém okně **Přidat nebo odebrat moduly snap-in** vyberte ze seznamu moduly **snap-in k dispozici**položku **certifikáty** a pak zvolte možnost **Přidat**.  

6. V dialogovém okně **modul snap-in Certifikáty** zvolte položku **účet počítače**a klikněte na tlačítko **Další**.  

7. V dialogovém okně **Vybrat počítač** zkontrolujte, zda je vybrána možnost **místní počítač: (počítač, na kterém je spuštěna tato konzola)** a poté klikněte na tlačítko **Dokončit**.  

8. V dialogovém okně **Přidat nebo odebrat moduly snap-in** klikněte na **tlačítko OK**.  

9. V konzole rozbalte položku **certifikáty (místní počítač)**, rozbalte položku **osobní**a pak zvolte možnost **certifikáty**.  

10. V podokně výsledků ověřte, že certifikát má **ověřování klienta** ve sloupci **zamýšlený účel** a že **klientský certifikát nástroje ConfigMgr** je ve sloupci **Šablona certifikátu** .  

11. Zavřete stránku **Certifikáty (místní)**.  

12. Opakujte kroky 1 až 11 pro členský server, abyste ověřili, že server, který se má nastavit jako bod správy, má také klientský certifikát.  

    Počítač je nyní nastaven s Configuration Manager klientským certifikátem.  

##  <a name="deploy-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a>Nasazení klientského certifikátu pro distribuční body  

> [!NOTE]  
>  Tento certifikát může být použit také pro obrazy médií, které nepoužívají PXE bootování, protože požadavky na certifikát jsou stejné.  

 Nasazení tohoto certifikátu zahrnuje následující postupy:  

- Vytvoření a vydání vlastní šablony ověřovacího certifikátu pracovní stanice v certifikační autoritě  

- Vyžádání vlastního ověřovacího certifikátu pracovní stanice  

- Exportovat klientský certifikát pro distribuční body  

###  <a name="create-and-issue-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a>Vytvoření a vydání vlastní šablony ověřovacího certifikátu pracovní stanice v certifikační autoritě  
 Tento postup vytvoří vlastní šablonu certifikátu pro Configuration Manager distribuční body, aby bylo možné exportovat soukromý klíč a přidat šablonu certifikátu do certifikační autority.  

> [!NOTE]
>  Tento postup používá šablonu certifikátu odlišnou od šablony certifikátu, kterou jste vytvořili pro klientské počítače. I když oba certifikáty vyžadují možnost ověření klienta, certifikát pro distribuční body vyžaduje export soukromého klíče. Z hlediska zabezpečení je nejvhodnější vytvořit šablony certifikátů, aby se privátní klíč mohl exportovat, pokud není tato konfigurace požadována. Distribuční bod vyžaduje tuto konfiguraci, protože musíte importovat certifikát jako soubor a nemusíte ho zvolit z úložiště certifikátů.  
> 
>  Při vytváření nové šablony certifikátu pro tento certifikát můžete omezit počítače, které mohou požadovat certifikát, jehož privátní klíč lze exportovat. V našem příkladu nasazení to bude skupina zabezpečení, kterou jste dříve vytvořili pro Configuration Manager servery systému lokality, na kterých běží služba IIS. Ve výrobní síti, která distribuuje role systému lokality se službou IIS, zvažte vytvoření nové skupiny zabezpečení pro servery, které spouští distribuční body, abyste mohli omezit certifikát pouze na tyto servery systému lokality. Pro tento certifikát také zvažte přidání následujících úprav:  
> 
> - Vyžadovat schválení pro instalaci certifikátu pro další zabezpečení  
>   - Prodloužení doby platnosti certifikátu. Vzhledem k tomu, že je nutné exportovat a importovat certifikát pokaždé, když jeho platnost vyprší, prodloužení doby platnosti sníží, jak často je nutné tento postup opakovat. Zvýšení doby platnosti však také zkracuje zabezpečení certifikátu, protože poskytuje více času, než by útočník mohl dešifrovat privátní klíč a ukrást certifikát.  
>   - Vlastní hodnota v poli certifikátu Předmět nebo vlastní hodnota alternativního názvu předmětu Subject Alternative Name (SAN) pomáhá rozpoznat tento certifikát od standardních klientských certifikátů. To může být zvláště užitečné, když budete používat stejný certifikát pro více distribučních bodů.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Vytvoření a vystavení vlastní šablony ověřovacího certifikátu pracovní stanice v konzole Certifikační úřad  

1.  Na členském serveru, na němž je spuštěna konzola certifikační úřad, klikněte pravým tlačítkem na **šablony certifikátů**a pak zvolte **Spravovat** a načtěte konzolu pro správu šablon certifikátů.  

2.  V podokně výsledků klikněte pravým tlačítkem na položku, která má **ověřování pracovní stanice** ve sloupci **Zobrazovaný název šablony** a pak zvolte možnost **Duplikovat šablonu**.  

3.  V dialogovém okně **Duplikovat šablonu** zkontrolujte, zda je vybrána možnost **Windows 2003 Server, Enterprise Edition** , a pak zvolte možnost **OK**.  

    > [!IMPORTANT]  
    >  Nevybírejte možnost **Windows 2008 Server, Enterprise Edition**.  

4.  V dialogovém okně **Vlastnosti nové šablony** na kartě **Obecné** zadejte název šablony, jako je například **certifikát klientského distribučního bodu nástroje ConfigMgr**, pro vygenerování certifikátu pro ověřování klientů pro distribuční body.  

5.  Zvolte kartu **vyřízení žádosti** a pak zvolte možnost **umožní export privátního klíče**.  

6.  Zvolte kartu **zabezpečení** a pak odeberte oprávnění **zapsat** ze skupiny zabezpečení **Enterprise Admins** .  

7.  Zvolte **Přidat**, do textového pole zadejte **Servery ConfigMgr IIS** a pak zvolte **OK**.  

8.  Vyberte oprávnění **zapsat** pro tuto skupinu a nemažte oprávnění **číst** .  

9. Zvolte **OK**a pak zavřete **konzolu šablony certifikátů**.  

10. V konzole Certifikační autorita klikněte pravým tlačítkem na **šablony certifikátů**, zvolte **Nový**a pak vyberte **Vystavovaná šablona certifikátu**.  

11. V dialogovém okně **Povolit šablony certifikátů** zvolte novou šablonu, kterou jste právě vytvořili, **certifikát klienta nástroje ConfigMgr pro distribuční body**, a pak zvolte **OK**.  

12. Pokud nepotřebujete vytvářet a vydávat další certifikáty, zavřete **certifikační autoritu**.  

###  <a name="request-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a>Vyžádání vlastního ověřovacího certifikátu pracovní stanice  
 Tato procedura vyžádá a pak nainstaluje vlastní certifikát klienta na členský server, na kterém je spuštěna služba IIS, a který bude nastaven jako distribuční bod.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Pro vyžádání vlastního certifikátu pro ověřování pracovních stanic  

1.  Zvolte **Start**, zvolte **Spustit**a pak zadejte **MMC. exe.** V prázdné konzole klikněte na položku **soubor**a vyberte možnost **Přidat nebo odebrat modul snap-in**.  

2.  V dialogovém okně **Přidat nebo odebrat moduly snap-in** vyberte ze seznamu moduly **snap-in k dispozici**položku **certifikáty** a pak zvolte možnost **Přidat**.  

3.  V dialogovém okně **modul snap-in Certifikáty** zvolte položku **účet počítače**a klikněte na tlačítko **Další**.  

4.  V dialogovém okně **Vybrat počítač** zkontrolujte, zda je vybrána možnost **místní počítač: (počítač, na kterém je spuštěna tato konzola)** a poté klikněte na tlačítko **Dokončit**.  

5.  V dialogovém okně **Přidat nebo odebrat moduly snap-in** klikněte na **tlačítko OK**.  

6.  V konzole rozbalte položku **certifikáty (místní počítač)** a pak zvolte možnost **osobní**.  

7.  Klikněte pravým tlačítkem na **certifikáty**, vyberte **všechny úlohy**a pak zvolte **požádat o nový certifikát**.  

8.  Na stránce **než začnete** klikněte na tlačítko **Další**.  

9. Pokud se zobrazí stránka **Vybrat zásady zápisu certifikátů** , klikněte na tlačítko **Další**.  

10. Na stránce **Vyžádat certifikáty** zvolte **certifikát klienta nástroje ConfigMgr pro distribuční body** ze seznamu dostupných certifikátů a pak zvolte možnost **zapsat**.  

11. Na stránce **Výsledky instalace certifikátů** počkejte, než se nainstaluje certifikát, a pak zvolte **Dokončit**.  

12. V podokně výsledků ověřte, že certifikát má **ověřování klienta** ve sloupci **zamýšlený účel** a že **certifikát klienta nástroje ConfigMgr pro distribuční body** je ve sloupci **Šablona certifikátu** .  

13. Nezavírejte stránku **Certifikáty (místní)**.  

###  <a name="export-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a>Exportovat klientský certifikát pro distribuční body  
 Tento postup exportuje vlastní certifikát ověřování pracovní stanice do souboru, aby jej bylo možné importovat do vlastností distribučního bodu.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Pro exportování certifikátu klienta pro distribuční body  

1. V konzole **certifikáty (místní počítač)** klikněte pravým tlačítkem na certifikát, který jste právě nainstalovali, zvolte možnost **všechny úlohy**a pak zvolte **exportovat**.  

2. V Průvodci exportem certifikátů klikněte na tlačítko **Další**.  

3. Na stránce **exportovat soukromý klíč** vyberte možnost **Ano, exportovat privátní klíč**a klikněte na tlačítko **Další**.  

   > [!NOTE]  
   >  Pokud tato možnost není k dispozici, certifikát byl vytvořen bez možnosti exportu soukromého klíče. V tomto případě nemůžete exportovat certifikát v požadovaném formátu. Je nutné nastavit šablonu certifikátu tak, aby bylo možné exportovat soukromý klíč, a pak znovu požádat o certifikát.  

4. Na stránce **Formát souboru pro export** zajistěte, aby soubor **Personal Information Exchange-PKCS #12 (. **Je vybraná možnost PFX.  

5. Na stránce **heslo** zadejte silné heslo pro ochranu exportovaného certifikátu s jeho privátním klíčem a pak zvolte **Další**.  

6. Na stránce **soubor k exportu** zadejte název souboru, který chcete exportovat, a klikněte na tlačítko **Další**.  

7. Chcete-li ukončit průvodce, klikněte na tlačítko **Dokončit** na stránce **Průvodce exportem certifikátu** a v potvrzovacím dialogovém okně klikněte na **tlačítko OK** .  

8. Zavřete stránku **Certifikáty (místní)**.  

9. Uložte soubor bezpečně a ujistěte se, že k němu máte přístup z konzoly Configuration Manager.  

   Certifikát je nyní připraven k importu při nastavení distribučního bodu.  

> [!TIP]  
>  Při nastavování imagí médií pro nasazení operačního systému, který nepoužívá spouštění pomocí technologie PXE, můžete použít stejný soubor certifikátu a pořadí úkolů pro instalaci bitové kopie se musí spojit s bodem správy, který vyžaduje připojení klientů pomocí protokolu HTTPS.  

##  <a name="deploy-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a>Nasazení certifikátu zápisu pro mobilní zařízení  
 Nasazení tohoto certifikátu vyžaduje jedinou proceduru pro vytvoření a vydání šablony certifikátu zápisu pro certifikační autoritu.  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Vytvoření a vydání šablony certifikátu zápisu pro certifikační autoritu  
 Tato procedura vytváří šablonu certifikátu zápisu pro Configuration Manager mobilní zařízení a přidává ji k certifikační autoritě.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Pro vytvoření a vydání šablony certifikátu zápisu pro certifikační autoritu  

1. Vytvořte skupinu zabezpečení s uživateli, kteří budou registrovat mobilní zařízení v Configuration Manager.  

2. Na členském serveru, na němž je nainstalována Certifikační služba, klikněte v konzole Certifikační úřad pravým tlačítkem na položku **šablony certifikátů**a pak zvolte možnost **Spravovat** a načtěte konzolu pro správu šablon certifikátů.  

3. V podokně výsledků klikněte pravým tlačítkem myši na položku, která má ve sloupci **Zobrazovaný název šablony** **ověřenou relaci** , a pak zvolte možnost **Duplikovat šablonu**.  

4. V dialogovém okně **Duplikovat šablonu** zkontrolujte, zda je vybrána možnost **Windows 2003 Server, Enterprise Edition** , a pak zvolte možnost **OK**.  

   > [!IMPORTANT]  
   >  Nevybírejte možnost **Windows 2008 Server, Enterprise Edition**.  

5. V dialogovém okně **Vlastnosti nové šablony** na kartě **Obecné** zadejte název šablony, jako je například **certifikát zápisu mobilních zařízení nástroje ConfigMgr**, k vygenerování certifikátů zápisu pro mobilní zařízení, která budou spravována Configuration Manager.  

6. Zvolte kartu **název subjektu** , ujistěte se, že je vybrána možnost **Sestavit z těchto informací v adresáři Active Directory** , vyberte **běžný název** pro **Formát názvu subjektu:** a pak zrušte zaškrtnutí políčka **hlavní název uživatele (UPN)** z části **Zahrnout tyto informace v alternativním názvu subjektu**.  

7. Zvolte kartu **zabezpečení** , zvolte skupinu zabezpečení s uživateli, kteří mají mobilní zařízení, která chcete zaregistrovat, a pak zvolte Další oprávnění k **zápisu**. Ponechejte **Číst**.  

8. Zvolte **OK**a pak zavřete **konzolu šablony certifikátů**.  

9. V konzole Certifikační autorita klikněte pravým tlačítkem na **šablony certifikátů**, zvolte **Nový**a pak vyberte **Vystavovaná šablona certifikátu**.  

10. V dialogovém okně **Povolit šablony certifikátů** zvolte novou šablonu, kterou jste právě vytvořili, **certifikát zápisu mobilních zařízení nástroje ConfigMgr**, a pak zvolte **OK**.  

11. Pokud nepotřebujete vytvářet a vydávat další certifikáty, zavřete konzolu certifikační autorita.  

    Šablona certifikátu zápisu mobilních zařízení je nyní připravena k výběru při nastavení profilu zápisu mobilního zařízení v nastavení klienta.  

##  <a name="deploy-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a>Nasazení certifikátu klienta pro počítače Mac  

Nasazení tohoto certifikátu vyžaduje jedinou proceduru pro vytvoření a vydání šablony certifikátu zápisu pro certifikační autoritu.  

###  <a name="create-and-issue-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a>Vytvoření a vydání šablony certifikátu klienta pro systém Mac v certifikační autoritě  
 Tento postup vytvoří vlastní šablonu certifikátu pro počítače se systémem Configuration Manager Mac a přidá šablonu certifikátu do certifikační autority.  

> [!NOTE]  
>  Tento postup používá odlišnou šablonu certifikátu od šablony certifikátu, kterou jste mohli vytvořit pro klientské počítače se systémem Windows nebo pro distribuční body.  
>   
>  Při vytváření nové šablony certifikátu pro tento certifikát můžete omezit žádost o certifikát oprávněným uživatelům.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Vytvoření a vystavení šablony klientského certifikátu systému Mac v konzole Certifikační úřad  

1. Vytvořte skupinu zabezpečení, která obsahuje uživatelské účty pro administrativní uživatele, kteří budou registrovat certifikát na počítači Mac pomocí Configuration Manager.  

2. Na členském serveru, na němž je spuštěna konzola certifikační úřad, klikněte pravým tlačítkem na **šablony certifikátů**a pak zvolte **Spravovat** a načtěte konzolu pro správu šablon certifikátů.  

3. V podokně výsledků klikněte pravým tlačítkem myši na položku, která zobrazuje **ověřenou relaci** , ve sloupci **Zobrazovaný název šablony** a pak zvolte možnost **Duplikovat šablonu**.  

4. V dialogovém okně **Duplikovat šablonu** zkontrolujte, zda je vybrána možnost **Windows 2003 Server, Enterprise Edition** , a pak zvolte možnost **OK**.  

   > [!IMPORTANT]  
   >  Nevybírejte možnost **Windows 2008 Server, Enterprise Edition**.  

5. V dialogovém okně **Vlastnosti nové šablony** na kartě **Obecné** zadejte název šablony, jako je například **klientský certifikát systému Mac nástroje ConfigMgr**, pro vygenerování certifikátu klienta pro počítač Mac.  

6. Zvolte kartu **název subjektu** , ujistěte se, že je vybraná možnost **Sestavit z těchto informací v adresáři Active Directory** , zvolte možnost **běžný název** pro **Formát názvu subjektu:** a pak z části **Zahrnout tyto informace v ALTERNATIVNÍM názvu subjektu**zrušte **hlavní uživatelské jméno (UPN)** .  

7. Zvolte kartu **zabezpečení** a pak odeberte oprávnění **zapsat** ze skupin zabezpečení **Domain Admins** a **Enterprise Admins** .  

8. Zvolte **Přidat**, určete skupinu zabezpečení, kterou jste vytvořili v kroku 1, a pak zvolte **OK**.  

9. Vyberte oprávnění **zapsat** pro tuto skupinu a nemažte oprávnění **číst** .  

10. Zvolte **OK**a pak zavřete **konzolu šablony certifikátů**.  

11. V konzole Certifikační autorita klikněte pravým tlačítkem na **šablony certifikátů**, zvolte **Nový**a pak vyberte **Vystavovaná šablona certifikátu**.  

12. V dialogovém okně **Povolit šablony certifikátů** zvolte novou šablonu, kterou jste právě vytvořili, **klientský certifikát nástroje ConfigMgr pro Mac**, a pak zvolte **OK**.  

13. Pokud nepotřebujete vytvářet a vydávat další certifikáty, zavřete **certifikační autoritu**.  

    Šablona certifikátu klienta pro systém Mac je nyní připravena k výběru při nastavení nastavení klienta pro zápis.
