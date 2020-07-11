---
title: Povolit aktualizace třetích stran
titleSuffix: Configuration Manager
description: Povolit aktualizace třetích stran v Configuration Manager
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f5aa622ca5d98f2cb5eb0b0c3154625df11a42e
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240758"
---
# <a name="enable-third-party-updates"></a>Povolení aktualizací třetích stran 

*Platí pro: Configuration Manager (Current Branch)*

Od verze 1806 se uzel **katalogů aktualizací softwaru třetích stran** v konzole Configuration Manager může přihlásit k odběru katalogů třetích stran, publikovat aktualizace do bodu aktualizace softwaru (SUP) a pak je nasadit do klientů.  <!--1357605, 1352101, 1358714-->

> [!Note]  
> Configuration Manager ve výchozím nastavení tuto funkci nepovolí. Než ho použijete, povolte volitelnou funkci **Povolení podpory aktualizací třetích stran na klientech**. Další informace naleznete v části [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="prerequisites"></a>Požadavky 
- Dostatek místa na disku ve složce WSUSContent bodu aktualizace softwaru na nejvyšší úrovni pro ukládání zdrojového binárního obsahu pro aktualizace softwaru třetích stran.
    - Velikost požadovaného úložiště se liší v závislosti na dodavateli, typech aktualizací a konkrétních aktualizacích, které publikujete pro nasazení.
    - Pokud potřebujete přesunout složku WSUSContent na jinou jednotku s větším množstvím volného místa, přečtěte si téma [Postup změny umístění, kde služba WSUS ukládá aktualizace místně](https://docs.microsoft.com/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally) .
- Synchronizační služba aktualizace softwaru třetí strany vyžaduje přístup k Internetu.
    - Pro seznam katalogů partnerů je potřeba download.microsoft.com přes port HTTPS 443. 
    -  Přístup k Internetu pro všechny katalogy třetích stran a aktualizace souborů obsahu. Můžou být potřeba další porty, které jsou jiné než 443.
    - Aktualizace třetích stran používají stejné nastavení proxy serveru jako SUP.
- U Configuration Manager verzí starších než 1910 nemůže role zabezpečení **správce aktualizací softwaru** synchronizovat katalogy třetích stran. K synchronizaci katalogů budete potřebovat roli zabezpečení **správce s úplnými oprávněními** .


## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>Další požadavky, pokud je server SUP vzdálený od serveru lokality nejvyšší úrovně 

1. Při vzdáleném SUP musí být protokol SSL povolený. To vyžaduje certifikát ověřování serveru vygenerovaný z interní certifikační autority nebo prostřednictvím veřejného poskytovatele.
    - [Konfigurace protokolu SSL na serveru WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol)
        - Při konfiguraci protokolu SSL na serveru WSUS Pamatujte na to, že některé webové služby a virtuální adresáře jsou vždy HTTP a nikoli HTTPS. 
        - Configuration Manager stáhne obsah třetích stran pro balíčky aktualizací softwaru z adresáře obsahu WSUS přes HTTP.   
    - [Konfigurace SSL v SUP](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. Při nastavování konfigurace podpisového certifikátu WSUS pro **Configuration Manager spravuje certifikát** ve vlastnostech komponenty bodu aktualizace softwaru, vyžadují se následující konfigurace, aby bylo možné vytvořit podpisový certifikát služby WSUS podepsaný svým držitelem: 
   - Na serveru SUP by mělo být povoleno vzdálené Registry.
   -  **Účet pro připojení k serveru WSUS** by měl mít oprávnění ke vzdálenému registru na serveru SUP/WSUS. 


3. Na serveru Configuration Manager lokality vytvořte následující klíč registru: 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`, vytvořte novou hodnotu DWORD s názvem **EnableSelfSignedCertificates** s hodnotou `1` . 

4. Chcete-li povolit instalaci podpisového certifikátu služby WSUS podepsaného svým držitelem do důvěryhodných vydavatelů a důvěryhodných kořenových úložišť na vzdáleném serveru SUP:
   - **Účet pro připojení k serveru WSUS** by měl mít oprávnění ke vzdálené správě na serveru sup.

     Pokud tato položka není možná, exportujte certifikát z úložiště WSUS místního počítače do důvěryhodných vydavatelů a důvěryhodných kořenových úložišť. 

> [!NOTE] 
>**Účet pro připojení k serveru WSUS** můžete identifikovat zobrazením karty **nastavení serveru proxy a účtu** na stránce vlastnosti role systému lokality. Pokud není zadán účet, bude použit účet počítače serveru lokality.

## <a name="enable-third-party-updates-on-the-sup"></a>Povolit aktualizace aktualizací třetích stran v SUP
Pokud tuto možnost povolíte, můžete se přihlásit k odběru katalogů aktualizací třetích stran v konzole Configuration Manager. Tyto aktualizace pak můžete publikovat do služby WSUS a nasazovat je do klientů. Následující postup je třeba spustit jednou pro každou hierarchii a povolit a nastavit funkci pro použití. Pokud někdy nahradíte server WSUS nejvyšší úrovně, možná budete muset tento postup znovu spustit. 

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality**a vyberte uzel **weby** .
2. Vyberte lokalitu nejvyšší úrovně v hierarchii. Na pásu karet klikněte na položku **Konfigurovat součásti webu**a vyberte možnost **bod aktualizace softwaru**.
3. Přepněte na kartu **aktualizace třetích stran** . Vyberte možnost **Povolit aktualizace softwaru třetích stran**.

    ![Aktualizace třetích stran – obrazovka vlastností SUP](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>Konfigurace podpisového certifikátu služby WSUS
Budete se muset rozhodnout, jestli chcete, aby Configuration Manager automaticky spravovat podpisový certifikát služby WSUS třetí strany pomocí certifikátu podepsaného svým držitelem, nebo pokud potřebujete ručně nakonfigurovat certifikát. 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>Automatické spravování podpisového certifikátu služby WSUS
Pokud nemáte požadavek na používání certifikátů PKI, můžete se rozhodnout pro automatické spravování podpisových certifikátů pro aktualizace třetích stran. Správa certifikátů služby WSUS se provádí jako součást cyklu synchronizace a je přihlášena `wsyncmgr.log` . 

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality**a vyberte uzel **weby** .
2. Vyberte lokalitu nejvyšší úrovně v hierarchii. Na pásu karet klikněte na položku **Konfigurovat součásti webu**a vyberte možnost **bod aktualizace softwaru**.
3. Přepněte na kartu **aktualizace třetích stran** . vyberte možnost **Configuration Manager spravuje certifikát**. 
4. V uzlu **certifikáty** v části **zabezpečení** v pracovním prostoru **Správa** se vytvoří nový certifikát typu **podepisování služby WSUS třetí strany** .  

### <a name="manually-manage-the-wsus-signing-certificate"></a>Ruční správa podpisového certifikátu služby WSUS
Pokud potřebujete ručně nakonfigurovat certifikát, například potřebujete použít certifikát PKI, budete k tomu muset použít buď [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) , nebo jiný nástroj.  

1. Nakonfigurujte podpisový certifikát pomocí [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server).
2. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality**a vyberte uzel **weby** .
3. Vyberte lokalitu nejvyšší úrovně v hierarchii. Na pásu karet klikněte na položku **Konfigurovat součásti webu**a vyberte možnost **bod aktualizace softwaru**.
4. Přepněte na kartu **aktualizace třetích stran** . Vyberte možnost pro **Ruční správu certifikátu**.


## <a name="enable-third-party-updates-on-the-clients"></a>Povolit aktualizace třetích stran na klientech
Povolte aktualizace třetích stran na klientech v nastavení klienta. Toto nastavení nastaví zásady agenta web Windows Update pro možnost [Povolení podepsaných aktualizací pro intranetové umístění služby Microsoft Update](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#allow-signed-updates-from-an-intranet-microsoft-update-service-location). Toto nastavení klienta také nainstaluje podpisový certifikát služby WSUS do úložiště důvěryhodných vydavatelů v klientovi. Protokolování správy certifikátů se zobrazuje v `updatesdeployment.log` klientech nástroje.  Spusťte tyto kroky pro každé vlastní nastavení klienta, které chcete použít pro aktualizace třetích stran. Další informace najdete v článku [o nastavení klienta](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) .

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **nastavení klienta** .
2. Vyberte existující vlastní nastavení klienta nebo vytvořte nové. 
3. Na levé straně vyberte kartu **aktualizace softwaru** . Pokud tuto kartu nemáte, ujistěte se, že je zaškrtnuté políčko **aktualizace softwaru** .
4. Nastavte **možnost povolit aktualizace softwaru třetích stran** na **Ano**. 


## <a name="add-a-custom-catalog"></a>Přidat vlastní katalog
*Katalogy partnerů* jsou katalogy výrobců softwaru, které mají své informace už registrované u Microsoftu. U partnerských katalogů se můžete přihlásit k odběru bez nutnosti zadávat žádné další informace. Katalogy, které přidáte, se nazývají *vlastní katalogy*. K Configuration Manager můžete přidat vlastní katalog od dodavatele aktualizace jiného výrobce. Vlastní katalogy musí používat protokol HTTPS a aktualizace musí být digitálně podepsané. 

1. V pracovním prostoru **Knihovna aktualizací softwaru** rozbalte možnost **aktualizace softwaru**a vyberte uzel **katalogy aktualizací softwaru třetích stran** . 
   
     ![Snímek obrazovky uzlu aktualizací třetích stran](media/third-party-updates-node.PNG)
2. Na pásu karet klikněte na **Přidat vlastní katalog** . 

     ![Aktualizace třetích stran přidat vlastní katalog](media/third-party-updates-custom-catalog.png)
1. Na stránce **Obecné** zadejte následující položky: 
    - **Adresa URL pro stahování**: platná adresa https vlastního katalogu.
    - **Vydavatel**: název organizace, která publikuje katalog. 
    - **Name (název**): název katalogu, který se má zobrazit v konzole Configuration Manager. 
    - **Popis**: Popis katalogu. 
    - **Adresa URL podpory** (volitelné): platná adresa HTTPS webu, která má získat nápovědu ke katalogu. 
    - **Kontakt podpory** (volitelné): kontaktní informace, které vám pomůžou s katalogem. 
2. Kliknutím na **Další** zkontrolujte souhrn katalogu a pokračujte v dokončování **Průvodce vlastním katalogem aktualizací softwaru třetích stran**.


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>Přihlášení k odběru aktualizací katalogu a synchronizace třetích stran
Když se přihlásíte k odběru katalogu třetích stran v konzole Configuration Manager, metadata pro každou aktualizaci v katalogu se synchronizují do serverů WSUS pro vaši sup. Synchronizace metadat umožňuje klientům určit, jestli se některé aktualizace mají použít. U každého katalogu třetích stran, ke kterému se chcete přihlásit, proveďte následující kroky:  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **aktualizace softwaru** a vyberte uzel **katalogy aktualizací softwaru třetích stran** .  
2. Vyberte katalog, který se má přihlásit k odběru, a klikněte na pásu karet na **přihlásit k odběru katalogu** . 
    ![Aktualizace třetích stran přidat vlastní katalog](media/third-party-updates-subscribe.png)
3. Zkontrolujte a schvalte certifikát katalogu.  
   > [!NOTE]
   > 
   > Když se přihlásíte k odběru katalogu aktualizací softwaru třetí strany, certifikát, který zkontrolujete a schválíte v průvodci, se přidá do lokality. Tento certifikát je typu **katalog aktualizací softwaru třetích stran**. Můžete ji spravovat v uzlu **certifikáty** v části **zabezpečení** v pracovním prostoru **Správa** .  
4. Dokončete průvodce. Po počátečním předplatném by se měl katalog začít stahovat za několik minut. 
    - Katalog se automaticky synchronizuje každých 7 dní.
    - Kliknutím na tlačítko **synchronizovat nyní** na pásu karet vynuťte synchronizaci.
5. Po stažení katalogu musí být metadata produktu synchronizovaná z databáze WSUS do databáze Configuration Manager. [Ručním spuštěním synchronizace aktualizací softwaru](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) synchronizujte informace o produktu.
6. Jakmile se informace o produktu synchronizují, [NAKONFIGURUJTE sup, aby synchronizoval požadovaný produkt](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) na Configuration Manager.  
7. [Ručním spuštěním synchronizace aktualizací softwaru](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) synchronizujte aktualizace nového produktu do Configuration Manager.  
8. Po dokončení synchronizace uvidíte aktualizace třetích stran v uzlu **všechny aktualizace** . Tyto aktualizace jsou publikovány jako aktualizace **pouze s metadaty** , dokud se nerozhodnete je publikovat. 
     - Ikona s modrou šipkou představuje aktualizace softwaru obsahující jenom metadata. ![Ikona aktualizace softwaru pouze s metadaty](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>Publikování a nasazení aktualizací softwaru třetích stran 
Až budou aktualizace třetích stran v uzlu **všechny aktualizace** , můžete zvolit, které aktualizace se mají publikovat pro nasazení. Když publikujete aktualizaci, binární soubory se stáhnou od dodavatele a umístí se do adresáře WSUSContent v souboru SUP nejvyšší úrovně. 

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **aktualizace softwaru** a vyberte uzel **všechny aktualizace softwaru** .
2. Pokud chcete filtrovat seznam aktualizací, klikněte na **Přidat kritéria** . Přidejte například **dodavatele** pro **HP**. pro zobrazení všech aktualizací ze společnosti HP.  
3. Vyberte aktualizace, které vaše organizace vyžaduje. Klikněte na **publikovat obsah aktualizace softwaru třetí strany**.
    - Tato akce stáhne binární soubory aktualizace od dodavatele a pak je uloží do složky WSUSContent v bodu aktualizace softwaru nejvyšší úrovně. 
4. [Ručně spusťte synchronizaci aktualizací softwaru](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) , abyste změnili stav publikovaných aktualizací z metadat – jenom k nasazení aktualizací s obsahem. 
    >[!NOTE]
    >Při publikování obsahu aktualizace softwaru třetí strany se do lokality přidají všechny certifikáty, které se používají k podepsání obsahu. Tyto certifikáty jsou typu **obsahu aktualizací softwaru třetích stran**. Můžete je spravovat v uzlu **certifikáty** v části **zabezpečení** v pracovním prostoru **Správa** .  

5. Přečtěte si průběh v SMS_ISVUPDATES_SYNCAGENT. log. Protokol se nachází v bodu aktualizace softwaru nejvyšší úrovně ve složce protokoly systému lokality.
6. Nasaďte aktualizace pomocí procesu [nasadit aktualizace softwaru](../deploy-use/deploy-software-updates.md) . 
7. Na stránce **umístění pro stahování** v **Průvodci nasazením aktualizace softwaru**vyberte výchozí možnost pro **Stažení aktualizací softwaru z Internetu**. V tomto scénáři je obsah již publikován do bodu aktualizace softwaru, který slouží ke stažení obsahu pro balíček pro nasazení.
8. Než bude možné zobrazit výsledky dodržování předpisů, budou muset klienti spustit kontrolu a vyhodnotit aktualizace.  Tento cyklus lze aktivovat ručně z ovládacích panelů Configuration Manager v klientovi spuštěním akce **cyklus prověřování aktualizací softwaru** .


## <a name="improvements-for-third-party-updates-starting-in-1910"></a><a name="bkmk_1910"></a>Vylepšení aktualizací třetích stran od 1910.
<!--4469002-->
Nyní máte podrobnější ovládací prvky pro synchronizaci katalogů aktualizací třetích stran. Od verze Configuration Manager 1910 můžete naplánovat synchronizaci pro každý katalog nezávisle na sobě. Pokud používáte katalogy, které zahrnují aktualizace kategorií, můžete synchronizaci nakonfigurovat tak, aby zahrnovala jenom určité kategorie aktualizací, aby se předešlo synchronizaci celého katalogu. V případě, že máte jistotu, že nasazujete kategorii, můžete ji nakonfigurovat tak, aby se automaticky stáhla a publikovala na server WSUS.

### <a name="set-the-schedule-for-a-catalog-in-a-new-catalog-subscription"></a>Nastavení plánu katalogu v novém předplatném katalogu

1. V pracovním prostoru **softwarová knihovna** rozbalte možnost **aktualizace softwaru**a potom vyberte uzel **katalogy aktualizací softwaru třetích stran** .
1. Vyberte katalog, který se má přihlásit k odběru, a klikněte na pásu karet na **přihlásit k odběru katalogu** .
1. Vyberte své možnosti na stránce **plán** , pokud chcete přepsat výchozí plán synchronizace:
   - **Jednoduchý plán**: Vyberte interval hodin, dnů nebo měsíců.
   - **Vlastní plán**: nastavte složitý plán.

### <a name="update-the-schedule-per-catalog"></a>Aktualizace plánu na katalog

1. V pracovním prostoru **softwarová knihovna** rozbalte možnost **aktualizace softwaru**a potom vyberte uzel **katalogy aktualizací softwaru třetích stran** .
1. Klikněte pravým tlačítkem na katalog a vyberte **vlastnosti**.
1. Na kartě plán vyberte své možnosti: 
   - **Jednoduchý plán**: Vyberte interval hodin, dnů nebo měsíců.
   - **Vlastní plán**: nastavte složitý plán.

### <a name="new-subscription-to-a-third-party-v3-catalog"></a>Nové předplatné ke katalogu V3 třetí strany

> [!IMPORTANT]
> Tato možnost je dostupná jenom pro katalogy aktualizací verze 3, které podporují kategorie aktualizací. Tyto možnosti jsou zakázané pro katalogy, které nejsou publikované v novém formátu v3.


1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **aktualizace softwaru** a vyberte uzel **katalogy aktualizací softwaru třetích stran** .
1. Vyberte katalog, který se má přihlásit k odběru, a klikněte na pásu karet na **přihlásit k odběru katalogu** .
1. Zvolte své možnosti na stránce **vybrat kategorie** :

   - **Synchronizovat všechny kategorie aktualizací** (výchozí)
       - Synchronizuje všechny aktualizace v katalogu aktualizací třetích stran do Configuration Manager.
   -  **Vybrat kategorie pro synchronizaci**
       - Vyberte kategorie a podřízené kategorie, které chcete synchronizovat do Configuration Manager.

      ![Vyberte aktualizovat kategorie pro synchronizaci do Configuration Manager](./media/4469002-select-categories-for-sync.png)
1. Vyberte, jestli chcete pro katalog **připravit obsah aktualizace** . Po přípravě obsahu se všechny aktualizace ve vybraných kategoriích automaticky stáhnou do nejvyšší úrovně bodu aktualizace softwaru, což znamená, že nemusíte je před nasazením stahovat. Měli byste automaticky připravit obsah jenom na aktualizace, abyste se vyhnuli nadměrnému nároky na šířku pásma a úložiště.

   - **Neprovádějte přípravu obsahu, synchronizovat pouze pro skenování (doporučeno)**
     - Nestahovat žádný obsah pro aktualizace v katalogu třetích stran
   - **Automaticky připravit obsah pro vybrané kategorie**
     - Vyberte kategorie aktualizací, které budou automaticky stahovat obsah.
     - Obsah pro aktualizace ve vybraných kategoriích bude stažen do adresáře obsahu WSUS v bodu aktualizace softwaru nejvyšší úrovně.
      ![Výběr aktualizace kategorií pro přípravu obsahu](./media/4469002-stage-content.png)
1. Nastavte **plán** pro synchronizaci katalogu a pak dokončete průvodce.

 

### <a name="edit-an-existing-subscription"></a>Úprava existujícího předplatného

> [!IMPORTANT]
> Tato možnost je dostupná jenom pro katalogy aktualizací verze 3, které podporují kategorie aktualizací. Tyto možnosti jsou zakázané pro katalogy, které nejsou publikované v novém formátu v3.

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **aktualizace softwaru** a vyberte uzel **katalogy aktualizací softwaru třetích stran** .
1. Klikněte pravým tlačítkem na katalog a vyberte **vlastnosti**.
1. Zvolte možnosti na kartě **vybrat kategorie** .
   - **Synchronizovat všechny kategorie aktualizací** (výchozí)
       - Synchronizuje všechny aktualizace v katalogu aktualizací třetích stran do Configuration Manager.
   -  **Vybrat kategorie pro synchronizaci**
       - Vyberte kategorie a podřízené kategorie, které chcete synchronizovat do Configuration Manager.
1. Vyberte možnosti pro kartu **obsah aktualizace fáze** .
   - **Neprovádějte přípravu obsahu, synchronizovat pouze pro skenování (doporučeno)**
     - Nestahovat žádný obsah pro aktualizace v katalogu třetích stran
   - **Automaticky připravit obsah pro vybrané kategorie**
     - Vyberte kategorie aktualizací, které budou automaticky stahovat obsah.
     - Obsah pro aktualizace ve vybraných kategoriích bude stažen do adresáře obsahu WSUS v bodu aktualizace softwaru nejvyšší úrovně. 

## <a name="monitoring-progress-of-third-party-software-updates"></a>Monitorování průběhu aktualizací softwaru třetích stran 

Synchronizace aktualizací softwaru třetích stran je zpracována komponentou SMS_ISVUPDATES_SYNCAGENT ve výchozím bodu aktualizace softwaru nejvyšší úrovně. Můžete zobrazit stavové zprávy z této součásti nebo zobrazit podrobnější stav v SMS_ISVUPDATES_SYNCAGENT. log. Tento protokol se nachází v bodu aktualizace softwaru nejvyšší úrovně ve složce systémových protokolů lokality. Ve výchozím nastavení je tato cesta C:\Program Files\Microsoft Configuration Manager\Logs. Další informace o monitorování obecného procesu správy aktualizací softwaru najdete v tématu [monitorování aktualizací softwaru](../deploy-use/monitor-software-updates.md) . 

## <a name="known-issues"></a>Známé problémy

- Počítač, ve kterém je spuštěna konzola nástroje, slouží ke stažení aktualizací ze služby WSUS a k jejímu přidání do balíčku aktualizací. Podpisový certifikát služby WSUS musí být důvěryhodný na počítači konzoly. Pokud ne, může se při stahování aktualizací třetích stran zobrazovat problémy s kontrolou podpisu. 
- Služba synchronizace aktualizací softwaru třetí strany nemůže publikovat obsah do aktualizací, které byly přidány do služby WSUS, pomocí jiné aplikace, nástroje nebo skriptu, například SCUP. Akce **publikovat obsah aktualizace softwaru třetí strany** se u těchto aktualizací nezdařila. Pokud potřebujete nasadit aktualizace třetích stran, které tato funkce zatím nepodporuje, použijte k nasazení těchto aktualizací svůj stávající proces v plném rozsahu.  
-  Configuration Manager má novou verzi formátu souboru CAB katalogu. Nová verze zahrnuje certifikáty pro binární soubory dodavatele. Po schválení a důvěřování katalogu budou tyto certifikáty přidány do uzlu **certifikáty** v části **zabezpečení** v pracovním prostoru **Správa** .  
     - Starší verzi souboru CAB katalogu můžete dál používat, pokud je adresa URL pro stahování https a aktualizace se podepisují. Publikování obsahu se nezdaří, protože certifikáty pro binární soubory nejsou v souboru CAB a jsou již schváleny. Tento problém můžete obejít tak, že vyhledáte certifikát v uzlu **certifikáty** , odblokujete ho a pak znovu publikujete aktualizaci. Pokud publikujete více aktualizací podepsaných pomocí různých certifikátů, budete muset odblokovat každý použitý certifikát.
     - Další informace najdete v části stavové zprávy 11523 a 11524 v níže uvedené tabulce stavových zpráv.
-  Pokud služba synchronizace aktualizací softwaru třetí strany v bodu aktualizace softwaru nejvyšší úrovně vyžaduje proxy server k přístupu k Internetu, může dojít k selhání kontrol digitálních podpisů. Chcete-li tento problém zmírnit, nakonfigurujte nastavení proxy serveru WinHTTP v systému lokality. Další informace najdete v tématu [Příkazy Netsh pro WinHTTP](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731131(v=ws.10)).
- Při použití CMG pro úložiště obsahu se nebude obsah pro aktualizace třetích stran stahovat do klientů, pokud je povolený **rozdílový obsah ke stažení, pokud** je povolené [nastavení klienta](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) dostupné. <!--6598587-->

## <a name="status-messages"></a>Stavové zprávy

| Parametr       | Závažnost           | Popis | Možná příčina| Možné řešení
| ------------- |-------------| -----|----|----|
| 11516     | Chyba |Publikování obsahu pro aktualizaci ID aktualizace se nezdařilo, protože obsah je nepodepsaný.  Publikovat lze pouze obsah s platnými podpisy.  |Configuration Manager nepovoluje publikování nepodepsaných aktualizací.| Publikujte aktualizaci alternativním způsobem. </br></br>Podívejte se, jestli je od dodavatele k dispozici podepsaná aktualizace.|
| 11523  | Upozornění |  Katalog "X" neobsahuje certifikáty podepisování obsahu, pokusy o publikování obsahu aktualizace pro aktualizace z tohoto katalogu můžou být neúspěšné, dokud nebudou přidané a schválené certifikáty pro podepisování obsahu. | Tato zpráva se může vyskytnout při importu katalogu, který používá starší verzi formátu souboru CAB.|Kontaktujte poskytovatele katalogu a získejte aktualizovaný katalog, který obsahuje certifikáty podepisování obsahu. </br> </br> Certifikáty pro binární soubory nejsou zahrnuté do souboru CAB, takže se obsah nepodaří publikovat. Tento problém můžete obejít tak, že vyhledáte certifikát v uzlu **certifikáty** , odblokujete ho a pak znovu publikujete aktualizaci. Pokud publikujete více aktualizací podepsaných pomocí různých certifikátů, budete muset odblokovat každý použitý certifikát.|
| 11524| Chyba  | Nepovedlo se publikovat aktualizaci ID kvůli chybějícím metadatům aktualizace. | Aktualizace mohla být synchronizovaná se službou WSUS mimo Configuration Manager.| Před pokusem o publikování obsahu aktualizace synchronizujte s Configuration Manager.  </br> </br>Pokud se k publikování aktualizace **jenom jako metadata**použil externí nástroj, použijte stejný nástroj k publikování obsahu aktualizace.|



## <a name="working-with-third-party-updates-video"></a>Video o práci s aktualizacemi třetích stran
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>Další krok
> [!div class="nextstepaction"]
> [Nasazení aktualizací softwaru](./deploy-software-updates.md)
