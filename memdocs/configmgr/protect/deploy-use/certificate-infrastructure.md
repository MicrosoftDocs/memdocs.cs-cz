---
title: Konfigurace infrastruktury certifikátu
titleSuffix: Configuration Manager
description: Naučte se konfigurovat zápis certifikátů v Configuration Manager.
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 656cc80c929eb7e829dd06b642a83cb174d3b0c8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697241"
---
# <a name="configure-certificate-infrastructure"></a>Konfigurace infrastruktury certifikátu

*Platí pro: Configuration Manager (Current Branch)*

Naučte se konfigurovat infrastrukturu certifikátů v Configuration Manager. Než začnete, Projděte si všechny požadavky, které jsou uvedené v článku [požadavky pro profily certifikátů](../../protect/plan-design/prerequisites-for-certificate-profiles.md).  

Pomocí těchto kroků můžete nakonfigurovat infrastrukturu pro certifikáty SCEP nebo PFX.

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>Krok 1 – instalace a konfigurace služby zápisu síťových zařízení a závislostí (jenom pro certifikáty SCEP)

 Nainstalujte a nakonfigurujte službu role Služby zápisu síťových zařízení pro službu AD CS (Active Directory Certificate Services), změňte oprávnění zabezpečení v šablonách certifikátu, nasaďte certifikát pro ověřování klientů PKI (infrastruktura veřejného klíče) a v registru zvyšte výchozí limit velikosti URL Internetové informační služby (IIS). Je-li to nutné, nakonfigurujte také vydávající certifikační autoritu (CA) tak, aby umožňovala vlastní období platnosti.  

> [!IMPORTANT]  
>  Než nakonfigurujete Configuration Manager pro práci se službou zápisu síťových zařízení, zkontrolujte instalaci a konfiguraci služby zápisu síťových zařízení. Pokud tyto závislosti nefungují správně, budete mít potíže při řešení potíží s zápisem certifikátu pomocí Configuration Manager.  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Instalace a nastavení Služby zápisu síťových zařízení a závislostí  

1. Na serveru se systémem Windows Server 2012 R2 nainstalujte a nakonfigurujte službu role Služby zápisu síťových zařízení pro roli serveru služby AD CS (Active Directory Certificate Services). Další informace najdete v tématu [pokyny pro službu zápisu síťových zařízení](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).

2. Zkontrolujte a v případě potřeby upravte oprávnění zabezpečení pro šablony certifikátu, které Služba zápisu síťových zařízení využívá:  

   -   Pro účet, který spouští konzolu Configuration Manager: oprávnění **číst** .  

        Toto oprávnění je vyžadováno, abyste po spuštění Průvodce vytvořením profilu certifikátu mohli vyhledat šablonu certifikátu, kterou chcete použít při vytváření profilu nastavení certifikátu SCEP. Výběr šablony certifikátu znamená, že některá nastavení se v průvodci vyplní automaticky. Konfigurace je tak jednodušší a hrozí menší riziko, že budou zvolena nastavení nekompatibilní s šablonami certifikátu, které používá Služba zápisu síťových zařízení.  

   -   Pro účet služby SCEP, který využívá fond aplikací Služby zápisu síťových zařízení: Oprávnění **Číst** a **Zapsat**.  

        Tento požadavek není specifický pro Configuration Manager, ale je součástí konfigurace služby zápisu síťových zařízení. Další informace najdete v tématu [pokyny pro službu zápisu síťových zařízení](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).  

   > [!TIP]  
   >  Pokud chcete zjistit, které šablony certifikátu Služba zápisu síťových zařízení používá, podívejte se do následujícího klíče registru na serveru, na kterém je spuštěná Služba zápisu síťových zařízení: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

   > [!NOTE]  
   >  Toto jsou výchozí oprávnění zabezpečení, která budou vhodná pro většinu prostředí. Můžete však použít také alternativní konfiguraci zabezpečení. Další informace najdete v tématu [Plánování oprávnění šablon certifikátů pro profily certifikátů](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3. Nasaďte na tento server certifikát PKI, který podporuje ověřování klientů. V počítači již můžete mít nainstalován vhodný certifikát, který lze použít, nebo může být nutné (nebo vhodnější) nasadit certifikát speciálně pro tento účel. Další informace o požadavcích na tento certifikát najdete v podrobnostech o serverech se spuštěným modulem zásad Configuration Manager se službou role služby zápisu síťových zařízení v části **certifikáty PKI pro servery** v tématu [požadavky na certifikát PKI pro Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md) téma.  

   > [!TIP]
   >  Pokud potřebujete pomáhat s nasazením tohoto certifikátu, můžete použít pokyny pro [Nasazení certifikátu klienta pro distribuční body](../../core/plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012), protože požadavky na certifikát jsou stejné s jednou výjimkou:  
   > 
   > - Na kartě **Vyřízení žádosti** ve vlastnostech šablony certifikátu nezaškrtávejte políčko **Umožnit export privátního klíče**.  
   > 
   >   Tento certifikát nemusíte exportovat s privátním klíčem, protože budete moct přejít do úložiště v místním počítači a vybrat ho při konfiguraci modulu zásad Configuration Manager.  

4. Vyhledejte kořenový certifikát, k němuž vede řetěz certifikátu pro ověřování klientů. Poté exportujte tento certifikát CA do souboru certifikátu (.cer). Uložte tento soubor do bezpečného umístění, k němuž budete mít bezpečný přístup, až budete později instalovat a konfigurovat server systému lokality pro bod registrace certifikátu.  

5. Na stejném serveru zvyšte pomocí editoru registru výchozí limit velikosti URL služby IIS nastavením následujících hodnot DWORD klíčů registru v HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters:  

   - Klíč **MaxFieldLength** nastavte na hodnotu **65534**.  

   - Klíč **MaxRequestBytes** nastavte na hodnotu **16777216**.  

     Další informace najdete v článku podpora Microsoftu [820129: Http.sys nastavení registru pro Windows](https://support.microsoft.com/help/820129).

6. Na stejném serveru změňte ve Správci Internetové informační služby (IIS) nastavení filtrování požadavků pro aplikaci /certsrv/mscep a poté server restartujte. V dialogovém okně **Upravit nastavení filtrování požadavků** by nastavení **Omezení počtu požadavků** mělo být:  

   - **Maximální povolená délka obsahu (v bajtech)**: **30000000**  

   - **Maximální délka adresy URL (v bajtech)**: **65534**  

   - **Maximální délka řetězce dotazu (v bajtech)**: **65534**  

     Další informace o těchto nastaveních a jejich konfiguraci najdete v tématu [omezení požadavků služby IIS](/iis/configuration/system.webServer/security/requestFiltering/requestLimits/).

7. Pokud chcete mít možnost požádat o certifikát s kratším obdobím platnosti, než má šablona certifikátu, kterou používáte: Toto nastavení je pro podnikovou CA standardně zakázáno. Chcete-li tuto možnost pro podnikovou CA povolit, použijte nástroj příkazového řádku Certutil a poté pomocí následujících příkazů zastavte a restartujte certifikační službu:  

   1. **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

   2. **net stop certsvc**  

   3. **net start certsvc**  

      Další informace najdete v tématu [nástroje a nastavení certifikačních služeb](/previous-versions/windows/it-pro/windows-server-2003/cc780742\(v=ws.10\)).

8. Ověřte, zda služba zápisu síťových zařízení funguje, pomocí následujícího odkazu jako příklad: `https://server.contoso.com/certsrv/mscep/mscep.dll` . Měla by se zobrazit vestavěná webová stránka Služby zápisu síťových zařízení. Tato webová stránka vysvětluje princip služby a obsahuje informaci, že síťová zařízení používají adresu URL k odesílání žádostí o certifikát.  

   Nyní je nakonfigurována Služba zápisu síťových zařízení a závislosti a lze nainstalovat a nakonfigurovat bod registrace certifikátu.


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>Krok 2 – instalace a konfigurace bodu registrace certifikátu

V hierarchii Configuration Manager musíte nainstalovat a nakonfigurovat alespoň jeden bod registrace certifikátu a tuto roli systému lokality můžete nainstalovat v lokalitě centrální správy nebo v primární lokalitě.  

> [!IMPORTANT]  
>  Než nainstalujete bod registrace certifikátu, přečtěte si část **požadavky na systém lokality** v tématu [podporované konfigurace pro Configuration Manager](../../core/plan-design/configs/supported-configurations.md) pro požadavky na operační systém a závislosti pro bod registrace certifikátu.  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>Instalace a konfigurace bodu registrace certifikátu  

1. V konzole Configuration Manager klikněte na možnost **Správa**.  

2. V pracovním prostoru **Správa** rozbalte **Konfigurace lokality**, klikněte na **Servery a role systému lokality**, a poté vyberte server, který chcete použít pro bod registrace certifikátu.  

3. Na kartě **Domů** ve skupině **Server** klikněte na **Přidat role systému lokality**.  

4. Na stránce **Obecné** definujte obecné nastavení systému lokalit a klikněte na **Další**.  

5. Na stránce **Proxy** klikněte na **Další**. Bod registrace certifikátu nepoužívá nastavení proxy Internetu.  

6. Na stránce **Výběr role systému** vyberte ze seznamu dostupných rolí **Bod registrace certifikátu**, a poté klikněte na **Další**. 

7. Na stránce **režim registrace certifikátu** vyberte, jestli chcete, aby bod registrace certifikátu **zpracovával žádosti o certifikát SCEP**, nebo **zpracovat žádosti o certifikát PFX**. Bod registrace certifikátu nemůže zpracovat oba typy požadavků, ale pokud pracujete s oběma typy certifikátů, můžete vytvořit více bodů registrace certifikátu.

   Při zpracování certifikátů PFX budete muset vybrat certifikační autoritu, kterou Microsoft nebo pověřit.

8. Stránka **Nastavení bodu registrace certifikátu** se liší podle typu certifikátu:
   - Pokud jste vybrali možnost **zpracovat žádosti o certifikát SCEP**, nakonfigurujte následující nastavení:
     -   **Název webu**, **číslo portu HTTPS**a **název virtuální aplikace** pro bod registrace certifikátu. Tato pole jsou automaticky vyplněna výchozími hodnotami. 
     -   **Adresa URL služby zápisu síťových zařízení a kořenového certifikátu certifikační autority** – klikněte na **Přidat**a pak v dialogovém okně **Přidat adresu URL a kořenový certifikát certifikační autority** zadejte toto:
         - **Adresa URL Služby zápisu síťových zařízení**: Zadejte adresu URL v tomto formátu: https://*<plně_kvalifikovaný_název_domény_serveru>*/certsrv/mscep/mscep.dll. Pokud je třeba plně kvalifikovaný název domény serveru, na kterém je spuštěná služba zápisu síťových zařízení, server1.contoso.com, zadejte `https://server1.contoso.com/certsrv/mscep/mscep.dll` .
         - **Kořenový certifikát certifikační autority**: Vyhledejte a vyberte soubor certifikátu (.cer), který jste vytvořili a uložili v **Kroku 1: Instalace a konfigurace Služby zápisu síťových zařízení a závislostí**. Tento kořenový certifikát CA umožňuje, aby bod registrace certifikátu ověřil certifikát pro ověřování klientů, který bude používat modul zásad Configuration Manager.  

   - Pokud jste vybrali možnost **zpracovat žádosti o certifikát PFX**, nakonfigurujete podrobnosti připojení a přihlašovací údaje pro vybranou certifikační autoritu.

     - Pokud chcete jako certifikační autoritu použít Microsoft, klikněte na **Přidat** a pak v dialogovém okně **Přidat certifikační autoritu a účet** zadejte toto:
         - **Název serveru certifikační autority** – zadejte název serveru certifikační autority.
         - **Účet certifikační autority** – kliknutím na **nastavit** vyberte nebo vytvořte účet, který má oprávnění k registraci v šablonách certifikační autority.
         - **Účet pro připojení k bodu registrace certifikátu** – vyberte nebo vytvořte účet, který připojuje bod registrace certifikátu k databázi Configuration Manager. Alteratively můžete použít účet místního počítače počítače, který je hostitelem bodu registrace certifikátu.
         - **Účet pro publikování certifikátu služby Active Directory** – vyberte účet nebo vytvořte nový účet, který bude použit k publikování certifikátů v uživatelských objektech ve službě Active Directory.

         - V poli **Adresa URL pro zápis síťových zařízení a certifikát kořenové certifikační autority** zadejte následující příkaz a klikněte na tlačítko **OK**:  

     - Chcete-li použít oprávnění svěřit jako certifikační autorita, zadejte:

       - **Adresa URL webové služby MDM**
       - Přihlašovací údaje uživatelského jména a hesla pro adresu URL

         Při použití rozhraní MDM API k definování adresy URL pověřit webové služby nezapomeňte použít aspoň verzi 9 rozhraní API, jak je znázorněno v následující ukázce:

         `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

         Starší verze rozhraní API nepodporují pověřitelné.

9. Klikněte na **Další** a dokončete průvodce.  

10. Počkejte několik minut, než bude dokončena instalace, a poté některou z následujících metod ověřte, že byl bod registrace certifikátu úspěšně nainstalován:  

    -   V pracovním prostoru **Monitorování** rozbalte **Stav systému**, klikněte na **Stav komponent**, a vyhledejte stavové zprávy z komponenty **SMS_CERTIFICATE_REGISTRATION_POINT**.  

    -   Na serveru systému lokality použijte soubory *<Instalační cesta ConfigMgr\>* \Logs\crpsetup.log a *<Instalační cesta ConfigMgr\>* \Logs\crpmsi.log. Úspěšná instalace vrátí ukončovací kód 0.  

    -   Pomocí prohlížeče ověřte, zda se můžete připojit k adrese URL bodu registrace certifikátu. Například, `https://server1.contoso.com/CMCertificateRegistration`. Měla by se zobrazit stránka **Chyba serveru** pro název aplikace a popis chyby HTTP 404.  

11. Vyhledejte exportovaný soubor certifikátu pro kořenovou certifikační autoritu, který automaticky vytvořil bod registrace certifikátu v následující složce na počítači serveru primární lokality: *<Instalační cesta ConfigMgr\>* \inboxes\certmgr.box. Uložte tento soubor do zabezpečeného umístění, ke kterému budete mít zabezpečený přístup, až budete později instalovat modul zásad Configuration Manager na server, na kterém je spuštěná služba zápisu síťových zařízení.  

    > [!TIP]  
    >  Certifikát není ve složce přítomen okamžitě. Než Configuration Manager zkopíruje soubor do tohoto umístění, možná budete muset počkat (např. půl hodiny).  


## <a name="step-3----install-the-configuration-manager-policy-module-for-scep-certificates-only"></a>Krok 3 – nainstalujte modul zásad Configuration Manager (jenom pro certifikáty SCEP).

Modul zásad Configuration Manager musíte nainstalovat a nakonfigurovat na každém serveru, který jste zadali v **kroku 2: instalace a konfigurace bodu registrace certifikátu** jako **Adresa URL služby zápisu síťových zařízení** ve vlastnostech bodu registrace certifikátu.  

##### <a name="to-install-the-policy-module"></a>Instalace Modulu zásad  

1. Na serveru, na kterém je spuštěna služba zápisu síťových zařízení, se přihlaste jako správce domény a zkopírujte následující soubory ze složky <ConfigMgrInstallationMedia \> \SMSSETUP\POLICYMODULE\X64 na instalačním médiu Configuration Manager do dočasné složky:  

   -   PolicyModule.msi  

   -   PolicyModuleSetup.exe  

   Pokud je na instalačním médiu složka LanguagePack, zkopírujte také tuto složku a její obsah.  

2. Z dočasné složky spusťte PolicyModuleSetup.exe a spusťte Průvodce instalací modulu zásad Configuration Manager.  

3. Na úvodní stránce průvodce klikněte na **Další**, přijměte licenční podmínky, a klikněte na **Další**.  

4. Na stránce **Instalační složka** potvrďte výchozí instalační složku pro modul zásad, nebo zadejte jinou složku, a klikněte na **Další**.  

5. Na stránce **Bod registrace certifikátu** zadejte adresu URL bodu registrace certifikátu pomocí plně kvalifikovaného názvu domény serveru systému lokality a názvu virtuální aplikace zadaného ve vlastnostech bodu registrace certifikátu. Výchozí název virtuální aplikace je CMCertificateRegistration. Například pokud má systémový server lokality plně kvalifikovaný název domény server1.contoso.com a použili jste výchozí název virtuální aplikace, zadejte `https://server1.contoso.com/CMCertificateRegistration` .

6. Potvrďte výchozí port **443**, nebo zadejte jiné číslo portu, který bod registrace certifikátu používá, a poté klikněte na **Další**.  

7. Na stránce **Klientský certifikát pro Modul zásad** vyhledejte a vyberte certifikát pro ověřování klientů, který jste nasadili v **Kroku 1: Instalace a konfigurace Služby zápisu síťových zařízení a závislostí**, a poté klikněte na **Další**.  

8. Na stránce **Certifikát bodu registrace certifikátu** klikněte na **Procházet** a vyberte exportovaný soubor certifikátu pro kořenovou certifikační autoritu, který jste vyhledali a uložili na konci **Kroku 2: Instalace a konfigurace bodu registrace certifikátu**.  

   > [!NOTE]  
   >  Pokud jste tento soubor certifikátu v předchozím kroku neuložili, je umístěný ve složce <Instalační cesta ConfigMgr\>\inboxes\certmgr.box v počítači serveru lokality.  

9. Klikněte na **Další** a dokončete průvodce.  

   Pokud chcete odinstalovat modul zásad Configuration Manager, použijte **programy a funkce** v Ovládacích panelech. 

 
Teď, když jste dokončili kroky konfigurace, jste připraveni k nasazení certifikátů pro uživatele a zařízení, a to vytvořením a nasazením profilů certifikátů. Další informace o tom, jak vytvořit profily certifikátů, najdete v tématu [Postup vytvoření profilů certifikátů](../../protect/deploy-use/create-certificate-profiles.md).