---
title: Instalace a konfigurace řešení Microsoft Tunnel VPN pro Microsoft Intune – Azure | Microsoft Docs
description: Nainstalujte a nakonfigurujte Microsoft Tunnel Gateway, server VPN, který běží na Linux. Cloudová zařízení, která spravujete pomocí Intune, můžou mít přístup k místní infrastruktuře.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/23/2020
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
ms.openlocfilehash: c3ed686ff7d3489cb73a992d58aafd041f89df60
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "91017709"
---
# <a name="configure-microsoft-tunnel-for-intune"></a>Konfigurace tunelového propojení Microsoft pro Intune

Tento článek vám může pomáhat při instalaci brány VPN pro Microsoft Tunneling pro Microsoft Intune. Nainstalujete software pro tunelování na server Linux a potom pomocí centra pro správu Microsoft Endpoint Manageru nakonfigurujete tunel pro použití s infrastrukturou. Nakonfigurujete také profily sítě VPN v Intune pro nasazení konfigurace tunelu na podporovaná zařízení a musíte zřizovat zařízení pomocí Microsoft Tunnel aplikace.

*Tunelové propojení Microsoft je ve verzi Public Preview*.

Pokud chcete nainstalovat Microsoft Tunnel Gateway, budete potřebovat aspoň jeden server pro Linux s nainstalovanou službou Docker, který běží v místním prostředí nebo v cloudu. V závislosti na prostředí a infrastruktuře můžou být potřeba další konfigurace a software, jako je například Azure ExpressRoute.

Před zahájením instalace se ujistěte, že jste dokončili následující úlohy:

- Zkontrolujte a [nakonfigurujte předpoklady pro tunelové propojení Microsoft](../protect/microsoft-tunnel-configure.md).
- Spusťte nástroj Microsoft Tunnel [Readiness Tool](../protect/microsoft-tunnel-overview.md#run-the-readiness-tool) a potvrďte, že je vaše prostředí připravené podporovat používání tunelu.

Po dokončení požadovaných součástí se vraťte k tomuto článku a začněte s instalací a konfigurací tunelu.

Když instalujete tunel Microsoft, přebírá informace o lokalitách tunelu, které jste definovali pro vašeho tenanta. Tyto informace zahrnují konfigurace serveru pro tyto lokality. Proto je nutné před instalací tunelu Microsoft na server se systémem Linux nakonfigurovat alespoň jednu lokalitu a jednu konfiguraci serveru.

## <a name="create-a-server-configuration"></a>Vytvoření konfigurace serveru

Použití *Konfigurace serveru* vám umožní nastavit konfiguraci v jednom okamžiku a tuto konfiguraci využívané více servery. Tato konfigurace zahrnuje rozsahy IP adres, servery DNS a pravidla dělení na dělené tunelové propojení. Později přiřadíte konfiguraci serveru k lokalitě, která tuto konfiguraci automaticky použije pro každý server, který se připojí k dané lokalitě.

### <a name="to-create-a-server-configuration"></a>Vytvoření konfigurace serveru

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Správa tenanta**  >  **Microsoft Tunnel Gateway**  >  *Vyberte* **kartu Konfigurace serveru** *tab*  >  **vytvořit nové**.

2. Na kartě **základy** zadejte *název* a *Popis* *(volitelné)* a **pak vyberte další**.

3. Na kartě **Nastavení** nakonfigurujte následující položky:
   - **Rozsah IP adres**: IP adresy v tomto rozsahu se zapůjčují do zařízení, když se připojí k bráně tunelového připojení. Například *169.254.0.0/16*.
   - **Servery DNS**: tyto servery se používají, když požadavek DNS pochází ze zařízení, které je připojené k bráně tunelového připojení.
   - **Hledání přípon DNS** *(volitelné)*: Tato doména je poskytována klientům jako výchozí doména při připojování k bráně tunelového připojení.
   - **Dělené tunelové propojení** *(volitelné)*: zahrnout nebo vyloučit adresy. Zahrnuté adresy jsou směrovány do brány tunelového připojení. Vyloučené adresy nejsou směrované do brány tunelového připojení. Můžete například nakonfigurovat pravidlo zahrnutí pro 255.255.0.0 * nebo *192.168.0.0/16*.

     Dělené tunelové propojení podporuje celkem 500 pravidel mezi zahrnutím i vyloučením pravidel. Pokud například nakonfigurujete pravidla zahrnutí 300, můžete mít pouze 200 pravidel pro vyloučení.

   - **Port serveru**: zadejte port, na který server naslouchá pro připojení.

4. Na kartě **Revize + vytvořit** Zkontrolujte konfiguraci a pak ji kliknutím na **vytvořit** uložte.

## <a name="create-a-site"></a>Vytvoření webu

Lokality jsou logické skupiny serverů, které hostují tunel od Microsoftu. Pro každou lokalitu, kterou vytvoříte, přiřadíte konfiguraci serveru. Tato konfigurace se aplikuje na každý server, který se připojuje k lokalitě nástroje.

### <a name="to-create-a-site-configuration"></a>Vytvoření konfigurace lokality

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Správa tenanta**  >  **Microsoft Tunnel Gateway**  >  *Vyberte* **Sites** *kartu*lokality  >  **vytvořit**.

2. V podokně **vytvořit web** zadejte následující vlastnosti:

   - **Název**: zadejte název pro tento web.
   - **Popis** *(volitelné)*
   - **Veřejná IP adresa nebo plně kvalifikovaný název domény**: zadejte veřejnou IP adresu nebo plně kvalifikovaný název domény, což je bod připojení pro zařízení, která používají tunel. Tato IP adresa může být individuální Server nebo IP adresa nebo plně kvalifikovaný název domény serveru pro vyrovnávání zatížení. IP adresa musí být veřejně směrovatelné a plně kvalifikovaný název domény musí být ve veřejném DNS přeložitelný.
   - **Konfigurace serveru**: pomocí rozevíracího seznamu vyberte konfiguraci serveru, kterou chcete přidružit k tomuto webu.

3. Vyberte **vytvořit** a lokalitu se uloží.

## <a name="install-microsoft-tunnel-gateway"></a>Nainstalovat bránu Microsoft Tunnel Gateway

Před instalací brány Microsoft Tunnel Gateway na server se systémem Linux nakonfigurujte tenanta pomocí aspoň jedné [Konfigurace serveru](#create-a-server-configuration)a pak vytvořte [lokalitu](#create-a-site). Později zadáte lokalitu, kterou server připojí při instalaci tunelu na tento server.

### <a name="use-the-script-to-install-microsoft-tunnel"></a>Použití skriptu k instalaci tunelu Microsoft

1. Ke stažení instalačního skriptu Microsoft Tunneling použijte jednu z následujících metod:

   - Stáhněte si nástroj přímo pomocí webového prohlížeče.  Pro https://aka.ms/microsofttunneldownload Stažení souboru **mstunnel-Setup použijte příkaz**.

   - Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Správa tenanta**  >  **Microsoft Tunnel Gateway**, vyberte kartu **servery** , vyberte **vytvořit** a otevřete podokno *vytvořit server* a pak vyberte **stáhnout skript**.

     ![Snímek obrazovky pro stažení instalačního skriptu](./media/microsoft-tunnel-configure/download-installation-script.png)

   - K získání nástroje Readiness použijte příkaz pro Linux přímo. Například na serveru, kam budete tunel instalovat, můžete k otevření odkazu použít **wget** nebo **kudrlinkou** https://aka.ms/microsofttunneldownload .

2. Chcete-li spustit instalaci serveru, spusťte skript jako **kořenový adresář** s následujícím příkazovým řádkem: `./mstunnel-setup`

   > [!TIP]  
   > Pokud instalaci a skript zastavíte, můžete ji znovu spustit spuštěním příkazového řádku. Instalace pokračuje od místa, kde jste skončili.

   Když spustíte skript, stáhne image kontejneru z Docker a na serveru se vytvoří potřebné složky a soubory.

   Během instalace vás skript vyzve k dokončení několika úloh správce.

3. Po zobrazení výzvy skriptem přijměte licenční smlouvu (EULA).

4. Zkontrolujte a nakonfigurujte proměnné v následujících souborech pro podporu vašeho prostředí.

   - Soubor prostředí: **/etc/mstunnel/env.sh**. Další informace o těchto proměnných naleznete v tématu [proměnné prostředí](../protect/microsoft-tunnel-reference.md#environment-variables) v článku referenční informace pro Microsoft Tunnel.

5. Po zobrazení výzvy zkopírujte úplný řetěz souboru certifikátu TLS na server Linux. Skript zobrazí správné umístění pro použití na serveru Linux.

   Certifikát TLS zabezpečuje připojení mezi zařízeními, která používají tunel a koncový bod služby tunelového propojení. Certifikát musí mít IP adresu nebo plně kvalifikovaný název domény serveru brány tunelového připojení ve své síti SAN.

   Privátní klíč zůstane k dispozici na počítači, kde vytvoříte žádost o podepsání certifikátu pro certifikát TLS. Tento soubor musí být exportován s názvem **Web. Key**.

   Nainstalujte certifikát TLS a privátní klíč. Použijte následující doprovodné materiály, které odpovídají formátu souboru:

   - **PFX**:
     - Název souboru certifikátu musí být **site. pfx**. Zkopírujte soubor certifikátu do **/etc/mstunnel/Private/site.pfx**.

   - **PEM**:
     - Úplný řetěz (root, zprostředkující, koncová entita) musí být v jednom souboru s názvem **site. CRT**. Pokud používáte certifikát vydaný veřejným poskytovatelem, jako je DigiCert, máte možnost stahovat celý řetězec jako jeden soubor. pem.

     - Název souboru certifikátu musí být **site. CRT*. Zkopírujte úplný řetězový certifikát do **/etc/mstunnel/certs/site.CRT**. Příklad: `cp [full path to cert] /etc/mstunnel/certs/site.crt`

       Případně můžete vytvořit odkaz na certifikát úplného řetězu v **/etc/mstunnel/certs/site.CRT**. Příklad: `ln -s [full path to cert] /etc/mstunnel/certs/site.crt`

     - Zkopírujte soubor privátního klíče do **/etc/mstunnel/Private/site.Key**. Příklad: `cp [full path to key] /etc/mstunnel/private/site.key`

       Případně můžete vytvořit odkaz na soubor privátního klíče v **/etc/mstunnel/Private/site.Key**. Například: `ln -s [full path to key file] /etc/mstunnel/private/site.key` Tento klíč by neměl být zašifrovaný pomocí hesla. Název souboru privátního klíče musí být **site. Key**.

6. Až instalační program nainstaluje certifikát a vytvoří služby tunelového připojení, budete vyzváni k přihlášení a ověření pomocí Intune. Uživatelský účet musí mít přiřazené role správce Intune nebo globální správce. Účet, který použijete k dokončení ověřování, musí mít licenci Intune, nebo musíte vypnout požadavky na účty správců k vyžadování licencí. Přihlašovací údaje tohoto účtu se neukládají a používají se k počátečnímu přihlášení Azure Active Directory. Po úspěšném ověření se pro ověřování mezi tunelovou bránou a Azure Active Directory používají tajné klíče a ID aplikací Azure.

   > [!TIP]  
   > Pokud chcete vypnout požadavky na licence správce, přejděte v centru pro správu Microsoft Endpoint Manageru na **Tenant Administration**  >  **role**  >  **správce** klienta Správa licencí a zakažte licencování správců.

   Toto ověřování registruje tunelovou bránu pomocí Microsoft Endpoint Manageru a vašeho tenanta Intune.

   1. Z webového prohlížeče. Přejděte na adresu https://Microsoft.com/devicelogin a zadejte kód zařízení, který je k dispozici v instalačním skriptu, a pak se přihlaste pomocí přihlašovacích údajů správce Intune.

   2. Po registraci brány Microsoft Tunnel Gateway do Intune skript získá informace o konfiguracích vašich lokalit a serverů z Intune. Skript pak vyzve k zadání identifikátoru GUID webu tunelového propojení, ke kterému se má tento server připojit. Skript zobrazí seznam dostupných webů.

   3. Po výběru lokality instalační program nainstaluje konfiguraci serveru pro danou lokalitu a použije ji na nový server pro dokončení instalace tunelu Microsoft.

7. Po dokončení instalačního skriptu můžete přejít do centra pro správu Microsoft Endpoint Manageru na kartu **Microsoft Tunnel Gateway** a zobrazit tak stav vysoké úrovně tunelu. Můžete také otevřít kartu **stav** a potvrdit, že je server online.

## <a name="deploy-the-microsoft-tunnel-app"></a>Nasazení aplikace tunelu Microsoft

Pokud chcete používat tunelové propojení Microsoftu, zařízení potřebují přístup k aplikaci Microsoft Tunnel. Aplikaci můžete nasadit do zařízení tak, že ji přiřadíte uživatelům. K dispozici jsou následující aplikace:

- V případě Androidu si stáhněte aplikaci **Microsoft Tunnel** z **Google Play** Storu. Přečtěte si téma Přidání aplikací pro Android Store do Microsoft Intune.
- Pro iOS/iPadOS si stáhněte aplikaci **Microsoft Tunneler** z Apple **App Storu**. Přečtěte si téma Přidání aplikací pro iOS Store do Microsoft Intune.

Další informace o nasazování aplikací do Intune najdete v tématu Přidání aplikací do Microsoft Intune.

## <a name="create-a-vpn-profile"></a>Vytvoření profilu sítě VPN

Po instalaci tunelu Microsoft na server a zařízení s nainstalovanou aplikací tunelového propojení Microsoftu můžete nasadit profily sítě VPN, aby zařízení používala k přímému tunelu. Provedete to tak, že vytvoříte profily sítě VPN s typem připojení tunelu Microsoft.

### <a name="android"></a>Android

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **zařízení**  >  **Konfigurace profily**  >  **vytvořit profil**.

2. V případě *platformy*vyberte možnost **Android Enterprise**a potom pro *možnost Profil* vyberte **síť VPN** *pouze pro vlastníka zařízení* nebo *pouze pro pracovní profil*a poté vyberte možnost **vytvořit**.

3. Na kartě **základy** zadejte *název* a *Popis* *(volitelné)* a **pak vyberte další**.

4. Jako *Typ připojení* vyberte **tunel Microsoft**a potom nakonfigurujte následující podrobnosti:
   - **Základní síť VPN**:  
     - Jako *název připojení*zadejte název, který se uživatelům zobrazí.
     - U *webu Microsoft Tunneling*vyberte lokalitu tunelu, kterou bude tento profil sítě VPN používat.
   - **Síť VPN pro jednotlivé aplikace**:  
     - Aplikace, které jsou přiřazené v profilu sítě VPN pro jednotlivé aplikace, odesílají provoz aplikace do tunelového propojení.
     - Pokud chcete povolit síť VPN pro jednotlivé aplikace, vyberte **Přidat** a potom přejděte do aplikací, které jste naimportovali do Intune. Můžou to být vlastní nebo veřejné aplikace.
   - **Vždycky zapnutá síť VPN**:  
     - V případě *sítě VPN s trvalou*připojením vyberte *Povolit* a nastavte klienta VPN tak, aby se automaticky připojoval a znovu připojil k síti VPN. Připojení k síti VPN Always On zůstane připojené. Pokud je povolená síť VPN pro jednotlivé aplikace, prochází se přes tunel jenom provoz z vybraných aplikací.
   - **Proxy server**:  
     - Nakonfigurujte proxy server podrobnosti pro vaše prostředí.  

   Další informace o nastavení sítě VPN najdete v tématu [nastavení zařízení s Androidem Enterprise pro konfiguraci sítě VPN](../configuration/vpn-settings-android-enterprise.md) .

5. Na kartě **přiřazení** nakonfigurujte skupiny, které obdrží tento profil.

6. Na kartě **Revize + vytvořit** Zkontrolujte konfiguraci a pak ji kliknutím na **vytvořit** uložte.

### <a name="ios"></a>iOS

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **zařízení**  >  **Konfigurace zařízení**  >  **vytvořit profil**.

2. V případě *platformy*vyberte **iOS/iPadOS**a potom pro *profil* vyberte **síť VPN**a pak **vytvořit**.

3. Na kartě **základy** zadejte *název* a *Popis* *(volitelné)* a **pak vyberte další**.

4. Jako *Typ připojení* vyberte **tunel Microsoft**a potom nakonfigurujte následující položky:
   - **Základní síť VPN**:  
     - Jako *název připojení*zadejte název, který se uživatelům zobrazí.
     - U *webu Microsoft Tunneling*vyberte lokalitu tunelu, kterou bude tento profil sítě VPN používat.  
   - **Síť VPN pro jednotlivé aplikace**:  
     - Pokud chcete povolit síť VPN pro jednotlivé aplikace, vyberte **Povolit**. Pro sítě VPN pro iOS pro aplikace se vyžadují další kroky konfigurace. Další informace najdete v tématu [síť VPN pro jednotlivé aplikace pro iOS/iPadOS](../configuration/vpn-setting-configure-per-app.md).
     - **Proxy server**:  
       - Nakonfigurujte proxy server podrobnosti pro vaše prostředí.  

## <a name="upgrade-microsoft-tunnel"></a>Upgrade tunelu Microsoft

Pokud jsou k dispozici aktualizace pro tunelové propojení Microsoft, je upgrade nainstalovaných tunelů Microsoft automaticky spravovaný Intune v rámci postupného upgradu:

- Intune upgraduje servery Microsoft Tunneling Server v jednom okamžiku.

- Po úspěšném upgradu serveru Intune počká krátkou dobu před zahájením upgradu dalšího serveru.

- Tento proces pokračuje, dokud se všechny servery v lokalitě neaktualizují na novou verzi.

## <a name="uninstall-the-microsoft-tunnel"></a>Odinstalace tunelu Microsoft

Chcete-li odinstalovat produkt, spusťte příkaz **./mst-CLI Uninstall** ze serveru se systémem Linux jako kořenový adresář.

## <a name="next-steps"></a>Další kroky

[Monitorování tunelu Microsoft](microsoft-tunnel-monitor.md)
