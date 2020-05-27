---
title: Konfigurace infrastruktury pro podporu profilů certifikátů SCEP pomocí Microsoft Intune – Azure | Microsoft Docs
description: Pokud chcete použít SCEP v Microsoft Intune, nakonfigurujte místní doménu AD, vytvořte certifikační autoritu, nastavte Server NDES a nainstalujte Intune Certificate Connector.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 45f649a99f6b3d632fea9e46dfdaee89450ebd23
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989284"
---
# <a name="configure-infrastructure-to-support-scep-with-intune"></a>Konfigurace infrastruktury pro podporu SCEP s Intune

Intune podporuje použití Simple Certificate Enrollment Protocol (SCEP) k [ověřování připojení k vašim aplikacím a podnikovým prostředkům](certificates-configure.md). SCEP používá certifikát certifikační autority (CA) k zabezpečení výměny zpráv pro žádost o podepsání certifikátu (CSR). Když vaše infrastruktura podporuje SCEP, můžete k nasazení certifikátů do zařízení použít profily certifikátů v Intune *SCEP* (typ profilu zařízení v Intune). Microsoft Intune Certificate Connector se vyžaduje pro použití profilů certifikátů SCEP s Intune při použití certifikační autority služby AD CS (Active Directory Certificate Services). Konektor není při používání [certifikačních autorit třetích stran](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration)vyžadován. 

Informace v tomto článku vám pomůžou při konfiguraci infrastruktury pro podporu protokolu SCEP při používání služby Active Directory Certificate Services. Po nakonfigurování infrastruktury můžete [vytvořit a nasadit profily certifikátů SCEP](certificates-profile-scep.md) pomocí Intune.

> [!TIP]
> Intune také podporuje použití [standardů kryptografie s veřejným klíčem #12 certifikátů](certficates-pfx-configure.md).

## <a name="prerequisites-for-using-scep-for-certificates"></a>Předpoklady použití protokolu SCEP pro certifikáty

Než budete pokračovat, ujistěte se, že jste [vytvořili a nasadili profil *důvěryhodného certifikátu* ](certificates-configure.md#export-the-trusted-root-ca-certificate) do zařízení, která budou používat profily certifikátů SCEP. Profily certifikátů SCEP přímo odkazují na profil důvěryhodného certifikátu, který používáte ke zřízení zařízení s certifikátem důvěryhodné kořenové certifikační autority.

### <a name="servers-and-server-roles"></a>Servery a role serveru

Následující místní infrastruktura musí běžet na serverech, které jsou připojené k doméně služby Active Directory, s výjimkou proxy serveru webových aplikací.

- **Certifikační autorita** – použijte certifikační autoritu rozlehlé sítě služby Microsoft Active Directory Certificate Services (CA), která je spuštěna v edici Enterprise systému Windows Server 2008 R2 s aktualizací Service Pack 1 nebo novější. Verze systému Windows Server, kterou používáte, musí zůstat v rámci podpory společnosti Microsoft. Samostatná certifikační autorita není podporovaná. Další informace najdete v tématu [instalace certifikační autority](https://technet.microsoft.com/library/jj125375.aspx). Pokud vaše certifikační autorita používá Windows Server 2008 R2 SP1, musíte [nainstalovat opravu hotfix z KB2483564](https://support.microsoft.com/kb/2483564/).

- **Role serveru NDES** – je nutné nakonfigurovat roli serveru služby zápisu síťových zařízení (NDES) v systému Windows Server 2012 R2 nebo novějším. V pozdější části tohoto článku Vás provedeme [instalací NDES](#set-up-ndes).

  - Server, který je hostitelem NDES, musí být připojený k doméně a ve stejné doménové struktuře jako vaše podniková certifikační autorita.
  - Nemůžete použít NDES, který je nainstalovaný na serveru, který hostuje certifikační autoritu organizace.
  - Microsoft Intune Certificate Connector nainstalujete na stejný server, který je hostitelem NDES.

  Další informace o NDES najdete v tématu [pokyny ke službě zápisu síťových zařízení](https://technet.microsoft.com/library/hh831498.aspx) v dokumentaci k Windows serveru a [používání modulu zásad se službou zápisu síťových zařízení](https://technet.microsoft.com/library/dn473016.aspx).

- **Microsoft Intune Certificate Connector** – k používání profilů certifikátů SCEP s Intune se vyžaduje Microsoft Intune Certificate Connector. Tento článek vás provede [instalací tohoto konektoru](#install-the-intune-certificate-connector).

  Konektor podporuje režim FIPS (Federal Information Processing Standard). FIPS není požadovaná, ale když je povolená, můžete certifikáty vystavovat a odvolávat.
  - Konektor má stejné požadavky na síť jako [spravovaná zařízení](../fundamentals/intune-endpoints.md#access-for-managed-devices).
  - Konektor musí běžet na stejném serveru jako role serveru NDES a na serveru se systémem Windows Server 2012 R2 nebo novějším.
  - Konektor vyžaduje rozhraní .NET 4,5 a je automaticky zahrnutý v systému Windows Server 2012 R2.
  - Konfigurace rozšířeného zabezpečení aplikace Internet Explorer [musí být zakázána na serveru, který je hostitelem NDES](https://technet.microsoft.com/library/cc775800(v=WS.10).aspx) a Microsoft Intune Certificate Connector.

Následující místní infrastruktura je volitelná:

Pokud chcete, aby zařízení v Internetu získala certifikáty, musíte publikovat adresu URL služby NDES mimo vaši podnikovou síť. Můžete použít buď Azure Proxy aplikací služby AD, proxy server webové aplikace, nebo jiný reverzní proxy server.

- **Azure proxy aplikací služby AD** (volitelné) – k publikování adresy URL služby NDES na Internet můžete použít proxy aplikací služby AD Azure místo vyhrazeného serveru proxy webových aplikací (WAP). To umožňuje intranetové i internetové zařízení získat certifikáty. Další informace najdete v tématu [Jak poskytnout zabezpečený vzdálený přístup k místním aplikacím](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).

- **Proxy server webových aplikací** (volitelné) – pomocí serveru se systémem Windows Server 2012 R2 nebo novějším jako serveru proxy webové aplikace (WAP) PUBLIKUJTE adresu URL služby NDES na Internet.  To umožňuje intranetové i internetové zařízení získat certifikáty.

  Server, který je hostitelem WAP, [musí nainstalovat aktualizaci](https://blogs.technet.com/b/ems/archive/2014/12/11/hotfix-large-uri-request-in-web-application-proxy-on-windows-server-2012-r2.aspx) umožňující podporu dlouhých adres URL, které používá služba zápisu síťových zařízení. Tato aktualizace je součástí [kumulativní aktualizace z prosince 2014](https://support.microsoft.com/kb/3013769)nebo jde instalovat jednotlivě z [KB3011135](https://support.microsoft.com/kb/3011135).

  Server WAP musí mít certifikát SSL, který odpovídá názvu publikovanému na externích klientech, a důvěřovat certifikátu SSL, který se používá v počítači, který je hostitelem služby NDES. Tyto certifikáty umožňují serveru WAP ukončit připojení SSL od klientů a vytvořit nové připojení SSL ke službě NDES.

  Další informace najdete v [plánování certifikátů pro WAP](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383650(v=ws.11)#plan-certificates) a [obecných informacích o serverech WAP](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn584113(v=ws.11)).

### <a name="accounts"></a>Účty

- **Účet služby NDES** – před nastavením NDES určete účet uživatele domény, který chcete použít jako účet služby NDES. Tento účet zadáte při konfiguraci šablon ve vydávající certifikační autoritě před konfigurací NDES.

  Tento účet musí mít na serveru, který je hostitelem NDES, následující práva:

  - **Místní přihlášení**
  - **Přihlášení jako služba**
  - **Přihlášení jako dávková úloha**

  Další informace najdete v tématu [Vytvoření doménového uživatelského účtu, který bude fungovat jako účet služby NDES](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)#to-create-a-domain-user-account-to-act-as-the-ndes-service-account).

- **Přístup k počítači, který je hostitelem služby NDES** – budete potřebovat účet uživatele domény s oprávněními k instalaci a konfiguraci rolí Windows serveru na serveru, na který instalujete NDES.

- **Přístup k certifikační autoritě** : budete potřebovat účet uživatele domény, který má práva ke správě vaší certifikační autority.

### <a name="network-requirements"></a>Požadavky sítě

Službu NDES doporučujeme publikovat prostřednictvím reverzního proxy serveru, jako je například [proxy aplikace služby Azure AD, Web Access proxy server](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-publish/)nebo proxy třetí strany. Pokud nepoužíváte reverzní proxy server, povolte provoz TCP na portu 443 od všech hostitelů a IP adres na internetu ke službě NDES.

Povolí všechny porty a protokoly, které jsou nezbytné pro komunikaci mezi službou NDES a jakoukoli podpůrnou infrastrukturou ve vašem prostředí. Například počítač, který je hostitelem služby NDES, musí komunikovat s certifikační autoritou, servery DNS, řadiči domény a případně dalšími službami nebo servery ve vašem prostředí, jako je Configuration Manager.

### <a name="certificates-and-templates"></a>Certifikáty a šablony

Při použití SCEP se používají následující certifikáty a šablony.

|Objekt    |Podrobnosti    |
|----------|-----------|
|**Šablona certifikátu SCEP**         |Šablona, kterou nakonfigurujete ve vaší vydávající certifikační autoritě, která se používá k sestavování požadavků SCEP zařízení. |
|**Certifikát pro ověřování klientů** |Požadováno od vaší vydávající certifikační autority nebo veřejné certifikační autority.<br /> Tento certifikát nainstalujete do počítače, který je hostitelem služby NDES a používá ho Intune Certificate Connector.<br /> Pokud má certifikát nastavené použití klíče *klienta* a *serveru* (**rozšířené použití klíčů**) na šabloně certifikační autority, kterou používáte k vystavení tohoto certifikátu. Pak můžete použít stejný certifikát pro ověřování serverů a klientů. |
|**Certifikát ověřování serveru** |Certifikát webového serveru vyžádaný z vaší vydávající certifikační autority nebo veřejné certifikační autority.<br /> Tento certifikát SSL nainstalujete a navážete ve službě IIS na počítači, který je hostitelem NDES.<br />Pokud má certifikát nastavené použití klíče *klienta* a *serveru* (**rozšířené použití klíčů**) na šabloně certifikační autority, kterou používáte k vystavení tohoto certifikátu. Pak můžete použít stejný certifikát pro ověřování serverů a klientů. |
|**Certifikát důvěryhodné kořenové certifikační autority**       |Chcete-li použít profil certifikátu SCEP, musí zařízení důvěřovat vaší důvěryhodné kořenové certifikační autoritě (CA). Použijte *profil důvěryhodného certifikátu* v Intune a zřiďte certifikát důvěryhodné kořenové certifikační autority pro uživatele a zařízení. <br/><br/> **-** Použijte jeden certifikát důvěryhodné kořenové certifikační autority na každou platformu operačního systému a přidružte tento certifikát ke každému profilu důvěryhodného certifikátu, který vytvoříte. <br /><br /> **-** V případě potřeby můžete použít další certifikáty důvěryhodných kořenových certifikačních autorit. Můžete například použít další certifikáty k poskytnutí vztahu důvěryhodnosti certifikační autoritě, která podepisuje ověřovací certifikáty serverů pro vaše přístupové body Wi-Fi. Vytvořte další certifikáty důvěryhodných kořenových certifikačních autorit pro vydávání certifikačních autorit.  V profilu certifikátu SCEP, který jste vytvořili v Intune, nezapomeňte zadat profil důvěryhodné kořenové certifikační autority pro vydávající certifikační autoritu.<br/><br/> Informace o profilu důvěryhodného certifikátu najdete v tématech [Export certifikátu důvěryhodné kořenové certifikační autority](certificates-configure.md#export-the-trusted-root-ca-certificate) a [Vytvoření profilů důvěryhodných certifikátů](certificates-configure.md#create-trusted-certificate-profiles) v tématu *použití certifikátů pro ověřování v Intune*. |

## <a name="configure-the-certification-authority"></a>Konfigurace certifikační autority

V následujících částech:

- Konfigurace a publikování požadované šablony pro NDES
- Nastavte požadovaná oprávnění pro odvolání certifikátu.

Následující části vyžadují znalost systému Windows Server 2012 R2 nebo novějšího a služby Active Directory Certificate Services (AD CS).

### <a name="access-your-issuing-ca"></a>Přístup k vystavující certifikační autoritě

1. Přihlaste se k vydávající certifikační autoritě pomocí účtu domény s právy dostatečnými pro správu certifikační autority.

2. Otevřete konzolu Microsoft Management Console (MMC) certifikační autorita. Buď **Spusťte** příkaz certsrv. msc, nebo v **Správce serveru**klikněte na **nástroje**a pak na **certifikační autorita**.

3. Vyberte uzel **šablony certifikátů** , klikněte na **Akce**  >  **Spravovat**.

### <a name="create-the-scep-certificate-template"></a>Vytvoření šablony certifikátu SCEP

1. Vytvořte šablonu certifikátu v2 (s kompatibilitou systému Windows 2003), která se použije jako šablona certifikátu SCEP. Můžete:

   - Pomocí modulu snap-in *šablony certifikátů* vytvořte novou vlastní šablonu.
   - Zkopírujte existující šablonu (třeba šablonu Uživatel) a pak aktualizujte kopii, která se má použít jako šablona NDES.

2. Na zadaných kartách šablony nakonfigurujte následující nastavení:

   - **Obecné**:

     - Zrušte kontrolu **publikování certifikátu ve službě Active Directory**.
     - Zadejte popisný **Zobrazovaný název šablony** , abyste mohli tuto šablonu později identifikovat.

   - **Název předmětu**:

     - **V žádosti vyberte dodat**. Zabezpečení se vynutilo modulem zásad Intune pro NDES.

       ![Šablona, karta Název subjektu](./media/certificates-scep-configure/scep-ndes-subject-name.jpg)

   - **Rozšíření**:

     - Ujistěte se, že **Popis zásad použití** obsahuje **ověření klienta**.

       > [!IMPORTANT]
       > Přidejte pouze zásady pro aplikace, které požadujete. Správnost zadaných voleb zkontrolujte se správci zabezpečení.

     - Pro šablony certifikátů iOS/iPadOS a macOS také upravte **použití klíče** a ujistěte se, že není vybraná možnost **podpis je důkazem původu** .

     ![Šablona, karta Rozšíření](./media/certificates-scep-configure/scep-ndes-extensions.jpg)  

   - **Zabezpečení**:

     - Přidejte **účet služby NDES**. Tento účet vyžaduje pro tuto šablonu oprávnění **ke čtení** a **zápisu** .

     - Přidejte další účty pro správce Intune, kteří budou vytvářet profily SCEP. Tyto účty vyžadují pro šablonu oprávnění **ke čtení** , aby tito správci mohli při vytváření profilů SCEP přejít k této šabloně.

     ![Šablona, karta Zabezpečení](./media/certificates-scep-configure/scep-ndes-security.jpg)

   - **Zpracování žádosti**:

     Následující obrázek je příklad. Vaše konfigurace se může lišit.  

     ![Šablona, karta Vyřízení žádosti](./media/certificates-scep-configure/scep-ndes-request-handling.png)

   - **Požadavky na vystavení**:

     Následující obrázek je příklad. Vaše konfigurace se může lišit.

     ![Šablona, karta Požadavky na vystavování](./media/certificates-scep-configure/scep-ndes-issuance-reqs.jpg)

3. Uložte šablonu certifikátu.

### <a name="create-the-client-certificate-template"></a>Vytvoření šablony certifikátu klienta

Intune Certificate Connector vyžaduje certifikát s rozšířeným použitím klíče *ověřování klienta* a názvem subjektu, který se rovná plně kvalifikovanému názvu domény počítače, ve kterém je konektor nainstalovaný. Vyžaduje se šablona s následujícími vlastnostmi:

- **Rozšíření**  >  **Zásady použití** musí obsahovat **ověřování klientů** .
- **Název subjektu**  >  **Zadejte v žádosti**.

Pokud již máte šablonu, která obsahuje tyto vlastnosti, můžete ji znovu použít, jinak vytvořit novou šablonu buď duplikováním existující šablony, nebo vytvořením vlastní šablony.

### <a name="create-the-server-certificate-template"></a>Vytvoření šablony certifikátu serveru

Komunikace mezi spravovanými zařízeními a službou IIS na serveru NDES používá protokol HTTPS, který vyžaduje použití certifikátu. K vystavení tohoto certifikátu můžete použít šablonu certifikátu **webového serveru** . Pokud ale dáváte přednost vyhrazené šabloně, vyžadují se následující vlastnosti:

- **Rozšíření**  >  **Zásady použití** musí obsahovat **ověření serveru** .
- **Název subjektu**  >  **Zadejte v žádosti**.

> [!NOTE]
> Pokud máte certifikát, který splňuje obě požadavky ze šablon certifikátu klienta i serveru, můžete použít jeden certifikát pro službu IIS i pro Certificate Connector Intune.

### <a name="grant-permissions-for-certificate-revocation"></a>Udělení oprávnění pro odvolání certifikátu

Aby Intune mohl odvolávat certifikáty, které už nepotřebujete, musíte udělit oprávnění v certifikační autoritě.

V Intune Certificate Connectoru můžete použít **účet systému** serveru NDES nebo konkrétní účet, jako je třeba **účet služby NDES**.

1. V konzole Certifikační autorita klikněte pravým tlačítkem myši na název certifikační autority a vyberte možnost **vlastnosti**.

2. Na kartě **zabezpečení** klikněte na tlačítko **Přidat**.

3. Udělení oprávnění k **vydávání a správě certifikátů** :

   - Pokud se rozhodnete použít **systémový účet**serveru NDES, poskytněte mu oprávnění k serveru NDES.
   - Pokud se rozhodnete použít **účet služby NDES**, místo toho zadejte oprávnění pro tento účet.

### <a name="modify-the-validity-period-of-the-certificate-template"></a>Úprava doby platnosti šablony certifikátu

Je volitelné upravit dobu platnosti šablony certifikátu.  

Po [Vytvoření šablony certifikátu SCEP](#create-the-scep-certificate-template)můžete tuto šablonu upravit a zkontrolovat **dobu platnosti** na kartě **Obecné** .

Ve výchozím nastavení Intune používá hodnotu nakonfigurovanou v šabloně. Můžete ale nakonfigurovat certifikační autoritu, aby žadateli umožňovala zadat jinou hodnotu a tato hodnota se dá nastavit v konzole Intune.

> [!IMPORTANT]
> Pro iOS/iPadOS a macOS vždycky použijte hodnotu nastavenou v šabloně.

#### <a name="to-configure-a-value-that-can-be-set-from-within-the-intune-console"></a>Konfigurace hodnoty, kterou je možné nastavit v konzole Intune

1. V certifikační autoritě spusťte tyto příkazy:

   -**certutil-setreg policy\EditFlags + EDITF_ATTRIBUTEENDDATE** 
   - **net stop certsvc** 
   - **net start certsvc**

2. Ve vydávající certifikační autoritě použijte modul snap-in Certifikační autorita k publikování šablony certifikátu. Vyberte uzel **šablony certifikátů** , vyberte **akci**  >  **New**  >  **vydávat novou šablonu certifikátu**a potom vyberte šablonu certifikátu, kterou jste vytvořili v předchozí části.

3. Ověřte, zda byla šablona publikována, zobrazením ve složce **šablony certifikátů** .

## <a name="set-up-ndes"></a>Nastavení NDES

Následující postupy vám pomůžou nakonfigurovat službu zápisu síťových zařízení (NDES) pro použití s Intune. Další informace o NDES najdete v tématu [pokyny pro službu zápisu síťových zařízení](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v%3dws.11)).

### <a name="install-the-ndes-service"></a>Instalace služby NDES

1. Na serveru, který bude hostovat službu NDES, se přihlaste jako **správce podnikové sítě**a potom pomocí [Průvodce přidáním rolí a funkcí](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11)) nainstalujte NDES:

   1. V průvodci vyberte možnost **Služba AD CS (Active Directory Certificate Services)** , abyste získali přístup ke službám rolí ve službě AD CS. Vyberte **Služba zápisu síťových zařízení**, zrušte zaškrtnutí políčka **certifikační autorita**a pak dokončete průvodce.

      > [!TIP]
      > V **průběhu instalace**nevybírejte možnost **Zavřít**. Místo toho vyberte odkaz **Konfigurovat službu AD CS (Active Directory Certificate Services) na cílovém serveru**. Otevře se průvodce **konfigurací služby AD CS** , který použijete pro další postup v tomto článku, a *nakonfigurujte službu NDES*. Po otevření Konfigurace služby AD CS můžete zavřít Průvodce přidáním rolí a funkcí.

   2. Když se na server přidá NDES, průvodce nainstaluje taky službu IIS. Ověřte, zda má služba IIS následující konfigurace:

      - **Webový server**  >  **Zabezpečení**  >  **Filtrování žádostí**
      - **Webový server**  >  **Vývoj aplikací**  >  **ASP.NET 3,5**

        Instalace technologie ASP.NET 3.5 nainstaluje rozhraní .NET Framework 3.5. Při instalaci rozhraní .NET Framework 3.5 nainstalujte základní **rozhraní .NET Framework 3.5** i **Aktivaci protokolem HTTP**.

      - **Webový server**  >  **Vývoj aplikací**  >  **ASP.NET 4,5**

        Instalace technologie ASP.NET 4.5 nainstaluje rozhraní .NET Framework 4.5. Při instalaci .NET Framework 4.5 nainstalujte základní rozhraní **.NET Framework 4.5**, **ASP.NET 4.5** a funkci **Služby WCF** > **Aktivace protokolem HTTP**.

      - **Nástroje**  >  pro správu Kompatibilita správy služby **IIS 6**  >  **Kompatibilita metabáze služby IIS 6**
      - **Nástroje**  >  pro správu Kompatibilita správy služby **IIS 6**  >  **Kompatibilita rozhraní WMI služby IIS 6**
      - Na serveru přidejte účet služby NDES jako člena místní skupiny **IIS_IUSR**.

2. V počítači, který je hostitelem služby NDES, spusťte na příkazovém řádku se zvýšenými oprávněními následující příkaz. Následující příkaz nastaví hlavní název služby (SPN) účtu služby NDES:

   `setspn -s http/<DNS name of the computer that hosts the NDES service> <Domain name>\<NDES Service account name>`

   Pokud má například počítač, který je hostitelem služby NDES, název **Server01**, vaše doména je **contoso.com**a účet služby je **NDESService**, použijte:

   `setspn –s http/Server01.contoso.com contoso\NDESService`  

### <a name="configure-the-ndes-service"></a>Konfigurace služby NDES

1. V počítači, který je hostitelem služby NDES, spusťte průvodce **konfigurací služby AD CS** a proveďte následující aktualizace:

   > [!TIP]
   > Pokud budete pokračovat od posledního postupu a kliknete na odkaz **Konfigurovat službu AD CS (Active Directory Certificate Services) na cílovém serveru** , měl by být tento průvodce už otevřený. Jinak spusťte Správce serveru, abyste získali přístup ke konfiguraci po nasazení pro službu AD CS (Active Directory Certificate Services).

   - V části **služby rolí**vyberte **Služba zápisu síťových zařízení**.
   - V části **účet služby pro službu NDES**zadejte účet služby NDES.
   - V části **certifikační autorita pro NDES**klikněte na **Vybrat**a pak vyberte vydávající certifikační autoritu, kam jste nakonfigurovali šablonu certifikátu.
   - V části **Kryptografie pro službu NDES** nastavte délku klíče podle požadavků vaší společnosti.
   - V části **Potvrzení** vyberte **Konfigurovat** a dokončete průvodce.

2. Po dokončení průvodce aktualizujte následující klíč registru v počítači, který je hostitelem služby NDES:

   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP\`

   Chcete-li aktualizovat tento klíč, identifikujte **účel** šablony certifikátu (na kartě **vyřízení žádosti** byl nalezen). Pak aktualizujte odpovídající položku registru nahrazením stávajících dat názvem šablony certifikátu (nikoli zobrazovaným názvem šablony), který jste zadali při [vytváření šablony certifikátu](#create-the-scep-certificate-template).

   Následující tabulka mapuje účel šablony certifikátu na hodnoty v registru:

   |Účel šablony certifikátu (na kartě Vyřízení žádosti)|Upravovaná hodnota registru|Hodnota zobrazená v konzole pro správu Intune pro profil SCEP|
   |------------------------|-------------------------|---|
   |Podpis               |SignatureTemplate        |Digitální podpis |
   |Šifrování              |EncryptionTemplate       |Šifrování klíče  |
   |Podpis a šifrování|GeneralPurposeTemplate   |Šifrování klíče <br/> Digitální podpis |

   Pokud je třeba účelem šablony certifikátu **Šifrování**, pak upravte hodnotu **EncryptionTemplate** , aby byla názvem vaší šablony certifikátu.

3. Nakonfigurujte filtrování požadavků služby IIS a přidejte podporu služby IIS pro dlouhé adresy URL (dotazy), které služba NDES obdrží.

   1. Ve Správci služby IIS vyberte **výchozí webová**  >  Stránka**filtrování požadavků**  >  **Upravit nastavení funkce** a otevřete stránku **Upravit nastavení filtrování požadavků** .

   2. Nakonfigurujte tahle nastavení:

      - **Maximální délka adresy URL (bajty)** = 65534
      - **Maximální délka řetězce dotazu (bajty)** = 65534

   3. Výběrem **OK** tuto konfiguraci uložte a zavřete Správce služby IIS.

   4. Ověřte tuto konfiguraci tak, že zobrazíte následující klíč registru, abyste ověřili, že má uvedené hodnoty:

      `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HTTP\Parameters`

      Následující hodnoty jsou nastavené jako položky DWORD:

      - Název: **MaxFieldLength**, s desetinnou hodnotou **65534**
      - Název: **MaxRequestBytes**, s desetinnou hodnotou **65534**

4. Restartujte server, který je hostitelem služby NDES. Nepoužívat **iisreset**; IIRESET nedokončí požadované změny.

5. Přejděte na *http://* Server_FQDN */certsrv/mscep/mscep.dll*. Měla by se zobrazit stránka NDES podobná následujícímu obrázku:

   ![Test NDES](./media/certificates-scep-configure/scep-ndes-url.png)

   Pokud webová adresa vrátí **nedostupnou službu 503**, podívejte se do prohlížeče událostí počítače. K této chybě obvykle dochází v případě, že se fond aplikací zastavil z důvodu chybějícího [oprávnění pro účet služby NDES](#accounts).
  
### <a name="install-and-bind-certificates-on-the-server-that-hosts-ndes"></a>Instalace a vázání certifikátů na serveru, který je hostitelem NDES

> [!TIP]
> V následujícím postupu můžete použít jeden certifikát pro *ověřování serverů* i pro *ověřování klientů* , pokud je tento certifikát nakonfigurovaný tak, aby splňoval kritéria obou použití. Kritéria pro jednotlivá použití jsou popsána v krocích 1 a 3 následujícího postupu.

1. Vyžádejte si **ověřovací certifikát serveru** z vaší interní certifikační autority nebo veřejné certifikační autority a pak na server nainstalujte certifikát.

   Pokud server používá externí a interní název pro jednu síťovou adresu, musí mít ověřovací certifikát serveru:

   - **Název subjektu** s názvem externího veřejného serveru.
   - **Alternativní název subjektu** , který obsahuje název interního serveru.

2. Vytvoření vazby ověřovacího certifikátu serveru ve službě IIS:

   1. Po instalaci ověřovacího certifikátu serveru otevřete **Správce služby IIS**a vyberte **výchozí web**. V podokně **Akce** vyberte **Vazby**.

   1. Vyberte **Přidat**, nastavte **Typ** na **https** a potom zkontrolujte, že port je **443**.
   
   1. Jako **Certifikát SSL**zadejte ověřovací certifikát serverů.

3. Na serveru NDES vyžádejte a nainstalujte certifikát pro **ověřování klientů** z vaší interní certifikační autority nebo z veřejné certifikační autority.

   Certifikát pro ověřování klientů musí mít následující vlastnosti:

   - **Rozšířené použití klíče**: Tato hodnota musí zahrnovat **ověřování klientů**.
   - **Název subjektu**: hodnota musí být stejná jako název DNS serveru, na který instalujete certifikát (Server NDES).

4. Server, který je hostitelem služby NDES, je teď připravený na podporu Intune Certificate Connectoru.

## <a name="install-the-intune-certificate-connector"></a>Instalace Intune Certificate Connectoru

Microsoft Intune Certificate Connector se nainstaluje na server, na kterém běží služba NDES. Na stejném serveru jako vydávající certifikační autorita (CA) se nepodporuje použití NDES nebo Certificate Connectoru Intune.

### <a name="to-install-the-certificate-connector"></a>Instalace Certificate Connectoru

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte možnost konektory **správy tenanta**  >  **a tokeny**  >  **certifikátů**  >  **Přidat**.

3. Stáhněte a uložte konektor pro soubor SCEP. Uložte ho do umístění přístupné ze serveru, na který chcete konektor nainstalovat.

   ![ConnectorDownload](./media/certificates-scep-configure/download-certificates-connector.png)

4. Jakmile se soubor stáhne, přejděte na server hostující roli NDES (Network Device Enrollment Service). Potom:

   1. Ověřte, že je nainstalovaná platforma .NET 4,5, jak je vyžaduje Intune Certificate Connector. Rozhraní .NET 4,5 je automaticky součástí systému Windows Server 2012 R2 a novějších verzí.

   2. Spusťte instalační program (**NDESConnectorSetup.exe**). Instalační program nainstaluje také modul zásad pro NDES a webovou službu bodu registrace certifikátu IIS (CRP). Webová služba CRP, *CertificateRegistrationSvc*, běží jako aplikace ve službě IIS.

      Při instalaci NDES pro samostatnou službu Intune se s konektorem Certificate Connector automaticky nainstaluje služba CRP.

5. Až se zobrazí výzva k zadání klientského certifikátu pro Certificate Connector, zvolte **Vybrat**a vyberte certifikát pro **ověřování klientů** , který jste nainstalovali na server NDES během kroku #3 postupu [instalace a vázání certifikátů na serveru, který hostuje NDES](#install-and-bind-certificates-on-the-server-that-hosts-ndes) z výše v tomto článku.

   Po vybrání certifikátu pro ověřování klientů se vrátíte do **klientského certifikátu pro Microsoft Intune Certificate Connector** Surface. I když vybraný certifikát není zobrazený, kliknutím na **Další** zobrazte vlastnosti certifikátu. Vyberte **Další** a potom **Nainstalovat**.

> [!NOTE]
> Před spuštěním Intune Certificate Connectoru je potřeba provést následující změny pro klienty RSZ s vysokou úrovní.
> 
> Proveďte úpravy dvou konfiguračních souborů uvedených níže, které aktualizují koncové body služby pro vysoké prostředí RSZ. Všimněte si, že tyto aktualizace mění identifikátory URI z **. com** na příponu **. us** . K dispozici je celkem tři aktualizace identifikátorů URI, dvě aktualizace v rámci konfiguračního souboru NDESConnectorUI. exe. config a jedna aktualizace v souboru NDESConnector. exe. config.
> 
> - Název souboru: < install_Path > \Microsoft Intune\NDESConnectorUI\NDESConnectorUI.exe.config
> 
>   Příklad: (%programfiles%\Microsoft Intune\NDESConnectorUI\NDESConnectorUI.exe.config)
>   ```
>    <appSettings>
>        <add key="SignInURL" value="https://portal.manage.microsoft.us/Home/ClientLogon"/>
>        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
>        <add key="AccountPortalURL" value="https://manage.microsoft.us"/>
>    </appSettings>
>   ```
> 
> - Název souboru: < install_Path > \Microsoft Intune\NDESConnectorSvc\NDESConnector.exe.config
>
>   Příklad: (%programfiles%\Microsoft Intune\NDESConnectorSvc\NDESConnector.exe.config)
>    ```
>    <appSettings>
>        <add key="BaseServiceAddress" value="https://manage.microsoft.us/" />
>    ```
>
> Pokud tyto úpravy nejsou dokončené, budou se vám v případě vysokého tenanta RSZ zobrazovat tyto chyby: "přístup byl odepřen", nemáte oprávnění k zobrazení této stránky "

6. Po dokončení průvodce klikněte před jeho zavřením na **Spustit uživatelské rozhraní konektoru Certificate Connector**.

   Pokud průvodce zavřete před spuštěním uživatelského rozhraní konektoru Certificate Connector, můžete ho znovu otevřít spuštěním následujícího příkazu:

   *< install_Path > \NDESConnectorUI\NDESConnectorUI.exe*

7. V uživatelském rozhraní **Certificate Connectoru** :

   1. Vyberte **Přihlásit** a zadejte své přihlašovací údaje správce služby Intune nebo přihlašovací údaje správce klienta s oprávněním pro globální správu.

   2. K účtu, který použijete, se musí přiřadit platná licence Intune.

   3. Po přihlášení stáhne Intune Certificate Connector certifikát z Intune. Tento certifikát se používá k ověřování mezi konektorem a Intune. Pokud účet, který jste použili, nemá licenci Intune, konektor (NDESConnectorUI. exe) se nepodaří získat certifikát z Intune.  

      Pokud vaše organizace používá proxy server a ten je vyžadovaný pro přístup serveru NDES k internetu, vyberte **Použít proxy server**. Pak zadejte název proxy serveru, port a přihlašovací údaje účtu pro připojení.

   4. Vyberte kartu **Upřesnit** a pak zadejte přihlašovací údaje pro účet, který má oprávnění **vydávat a spravovat certifikáty** ve vaší vydávající certifikační autoritě. Provedené změny **použijte**.  

    5. Teď můžete zavřít uživatelského rozhraní Certificate Connectoru.

8. Otevřete příkazový řádek, zadejte **services.msc** a stiskněte **Enter**. Klikněte pravým tlačítkem na restartovat **službu Intune Connector**  >  **Restart**.

Pokud chcete ověřit, že je služba spuštěná, spusťte prohlížeč a zadejte následující adresu URL. Měla by vrátit chybu **403** :`https://<FQDN_of_your_NDES_server>/certsrv/mscep/mscep.dll`

> [!NOTE]
> Intune Certificate Connector podporuje TLS 1,2. Pokud server, který je hostitelem konektoru, podporuje protokol TLS 1,2, použije se protokol TLS 1,2. Pokud server nepodporuje TLS 1.2, použije se TLS 1.1. V současnosti se k ověřování zařízení a serveru používá protokol TLS 1.1.

## <a name="next-steps"></a>Další kroky

[Vytvoření profilu certifikátu SCEP](certificates-profile-scep.md)  
[Řešení potíží s Intune Certificate Connectorem](troubleshoot-certificate-connector-events.md)
