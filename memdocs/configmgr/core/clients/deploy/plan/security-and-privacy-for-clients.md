---
title: Zabezpečení a ochrana osobních údajů klienta
titleSuffix: Configuration Manager
description: Přečtěte si o zabezpečení a ochraně osobních údajů pro klienty Configuration Manager.
ms.date: 07/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84ef4e37ddf756f04101c9cdec0ec7a4ed91688d
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270833"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Zabezpečení a ochrana osobních údajů pro klienty Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek popisuje informace o zabezpečení a ochraně osobních údajů pro klienty Configuration Manager. Obsahuje také informace o mobilních zařízeních, která jsou spravována [konektorem systému Exchange Server](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-clients"></a><a name="BKMK_Security_Clients"></a>Osvědčené postupy zabezpečení pro klienty  

Lokalita Configuration Manager akceptuje data ze zařízení, na kterých běží klient Configuration Manager. Toto chování představuje riziko, že by klienti mohli web napadnout. Například by mohli odesílat poškozený inventář nebo se pokusit přetížit systémy lokality. Nasaďte klienta Configuration Manager jenom na zařízení, kterým důvěřujete. Kromě toho využijte následující osvědčené postupy zabezpečení, které vám pomůžou lokalitu ochránit před podvodnými nebo ohroženými zařízeními:  

### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>Použití certifikátů infrastruktury veřejných klíčů (PKI) pro komunikaci klientů se systémy lokality, na nichž je spuštěna služba IIS  

- Jako vlastnost lokality nakonfigurujte možnost **Nastavení serveru** pro položku **Pouze HTTPS**.  

- Nainstalujte klienty pomocí `UsePKICert` vlastnosti CCMSetup.  

- Použijte seznam odvolaných certifikátů (CRL) a ujistěte se, že klienti a komunikační servery k němu mají vždycky přístup.  

Tyto certifikáty vyžadují klienti mobilních zařízení a někteří internetoví klienti. Společnost Microsoft doporučuje tyto certifikáty pro všechna připojení klientů v intranetu.  

Další informace o požadavcích na certifikát PKI a o tom, jak se používají k ochraně Configuration Manager, najdete v tématu [požadavky na certifikát PKI](../../../plan-design/network/pki-certificate-requirements.md).  

### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>Automatické schválení klientských počítačů z důvěryhodných domén a ruční kontrola a schválení jiných počítačů  

Pokud nemůžete použít ověřování PKI, schválení identifikuje počítač, kterému důvěřujete, aby se spravoval pomocí Configuration Manager. Hierarchie má následující možnosti konfigurace schválení klienta:  

- Ruční
- Automatické pro počítače v důvěryhodných doménách
- Automaticky pro všechny počítače  

Nejbezpečnější metodou schválení je automatické schválení klientů, kteří jsou členy důvěryhodných domén. Tato možnost zahrnuje klienty připojené k cloudovým doménám z připojených tenantů Azure Active Directory (Azure AD).<!-- MEMDocs#318 --> Pak ručně zkontrolujte a schvalte všechny ostatní počítače. Automatické schvalování všech klientů se nedoporučuje, pokud nemáte další řízení přístupu, které brání nedůvěryhodným počítačům v přístupu k síti.  

Další informace o ručním schválení počítačů najdete v tématu [Správa klientů z uzlu zařízení](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>Nespoléhá se na blokování, aby klienti nemohli přistupovat k hierarchii Configuration Manager.  

Zablokované klienty jsou odmítnuté infrastrukturou Configuration Manager. Pokud jsou klienti zablokované, nemůžou komunikovat se systémy lokality za účelem stahování zásad, nahrávání dat inventáře nebo odesílání stavových zpráv.

Blokování je navrženo pro následující scénáře:

- Blokování ztracených nebo ohrožených spouštěcích médií při nasazení operačního systému do klientů
- Když všechny systémy lokality přijímají připojení klientů přes protokol HTTPS

Pokud systémy lokality přijímají připojení klienta pomocí protokolu HTTP, nespoléhá na blokování, aby se chránila Configuration Manager hierarchie z nedůvěryhodných počítačů. V tomto scénáři se může blokovaný klient znovu připojit k lokalitě pomocí nového certifikátu podepsaného svým držitelem a ID hardwaru.

Odvolání certifikátu je primární linií obrany před potenciálně ohroženými certifikáty. Seznam odvolaných certifikátů (CRL) je dostupný jenom z podporované infrastruktury veřejných klíčů (PKI). Blokování klientů v Configuration Manager nabízí druhou linii obrany ochrany vaší hierarchie.  

Další informace najdete v tématu [Určení možnosti blokování klientů](determine-whether-to-block-clients.md).  

### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>Použijte nejbezpečnější metody instalace klienta, které jsou pro vaše prostředí praktické.  

- Pro počítače domény jsou metody instalace klienta na základě zásad skupiny a instalace klienta na základě aktualizace softwaru bezpečnější než klientská nabízená instalace.  

- Pokud použijete řízení přístupu a změníte ovládací prvky, použijte metody pro vytváření a ruční instalaci.  

- Ve verzi 1806 nebo novější použijte vzájemné ověřování pomocí protokolu Kerberos s nabízenou instalací klienta.  

Ze všech metod instalace klienta je klientská nabízená instalace nejméně bezpečná, protože má velký počet závislostí. Tyto závislosti zahrnují místní oprávnění správce, sdílenou složku Admin $ a výjimky brány firewall. Počet a typ těchto závislostí zvyšují plochu útoku.  

Počínaje verzí 1806 platí, že při použití klientské nabízené instalace může lokalita vyžadovat vzájemné ověřování protokolem Kerberos tím, že před vytvořením připojení neumožní přechod na protokol NTLM. Toto vylepšení pomáhá zabezpečit komunikaci mezi serverem a klientem. Další informace najdete v tématu [instalace klientů pomocí klientské nabízené instalace](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!--1358204-->  

Další informace o různých metodách instalace klientů najdete v tématu [metody instalace klientů](client-installation-methods.md).  

Pokud je to možné, vyberte metodu instalace klienta, která vyžaduje minimální oprávnění zabezpečení v Configuration Manager. Omezte administrativní uživatele, kterým jsou přiřazeny role zabezpečení, s oprávněními, která lze použít pro jiné účely než nasazení klienta. Například konfigurace automatického upgradu klienta vyžaduje roli zabezpečení **správce s úplnými** oprávněními, která uděluje administrativnímu uživateli všechna oprávnění zabezpečení.  

Další informace o závislostech a oprávněních zabezpečení pro jednotlivé metody instalace klientů naleznete v části závislosti metod instalace v části [požadavky na klienty počítačů](../prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>Pokud musíte použít klientskou nabízenou instalaci, proveďte další kroky pro zabezpečení účtu klientské nabízené instalace.  

Tento účet musí být členem místní skupiny **Administrators** na každém počítači, který instaluje klienta Configuration Manager. Nikdy nepřidávejte účet klientské nabízené instalace do skupiny **Domain Admins** . Místo toho vytvořte globální skupinu a pak ji přidejte do místní skupiny **Administrators** na svých klientech. Vytvořte objekt zásad skupiny pro přidání nastavení skupiny s omezeným přístupem pro přidání účtu klientské nabízené instalace do místní skupiny **Administrators** .  

Pro zvýšení zabezpečení vytvořte několik účtů klientské nabízené instalace, každý s přístupem správce k omezenému počtu počítačů. Pokud dojde k ohrožení bezpečnosti jednoho účtu, budou ohroženy pouze klientské počítače, ke kterým má tento účet přístup.  

### <a name="remove-certificates-before-imaging-clients"></a>Odebrání certifikátů před použitím klientů pro vytváření imagí  

Pokud nasazujete klienty pomocí bitových kopií operačního systému, před zachytáváním bitové kopie vždy odeberte certifikáty. Tyto certifikáty zahrnují certifikáty PKI pro ověřování klientů a certifikáty podepsané svým držitelem. Pokud tyto certifikáty neodeberete, klienti se můžou zosobnit navzájem. Data pro každého klienta nelze ověřit.  

Další informace najdete v tématu [Vytvoření pořadí úkolů pro zachycení operačního systému](../../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).  

### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>Zajistěte, aby klienti Configuration Manager počítačů získali autorizovanou kopii těchto certifikátů.  

#### <a name="the-configuration-manager-trusted-root-key-certificate"></a>Certifikát důvěryhodného kořenového klíče Configuration Manager  

Pokud jsou splněné oba následující příkazy, klienti při ověřování platných bodů správy spoléhají na Configuration Manager důvěryhodný kořenový klíč:  

- Nerozšířili jste schéma služby Active Directory pro Configuration Manager
- Klienti nepoužívají certifikáty PKI při komunikaci s body správy.  

V tomto scénáři nemají klienti žádný způsob, jak ověřit, že bod správy je pro hierarchii důvěryhodný, pokud nepoužívají důvěryhodný kořenový klíč. Bez důvěryhodného kořenového klíče by mohl zkušený útočník přesměrovat klienty na podvodný bod správy.  

Když klienti nemůžou stahovat Configuration Manager důvěryhodný kořenový klíč z globálního katalogu nebo pomocí certifikátů PKI, předem zřídí klienty s důvěryhodným kořenovým klíčem. Tato akce zajistí, že nemohou být přesměrovány do podvodného bodu správy. Další informace najdete v tématu [Plánování důvěryhodného kořenového klíče](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

#### <a name="the-site-server-signing-certificate"></a>Podpisový certifikát serveru lokality  

Klienti používají tento certifikát k ověření, že server lokality podepsal zásady stažené z bodu správy. Tento certifikát je podepsaný držitelem serveru lokality a zveřejněný ve službě AD DS (Active Directory Domain Services).  

Když klienti nemůžou stáhnout podpisový certifikát serveru lokality z globálního katalogu, ve výchozím nastavení ho stáhnou z bodu správy. Pokud je bod správy vystavený nedůvěryhodné síti, jako je Internet, ručně nainstalujte podpisový certifikát serveru lokality na klienty. Tím se zajistí, že se nemůžou stahovat neoprávněné zásady klienta z ohroženého bodu správy.  

Pokud chcete podpisový certifikát serveru lokality instalovat ručně, použijte vlastnost CCMSetup client.msi **SMSSIGNCERT**. Další informace najdete v tématu [o vlastnostech instalace klienta](../about-client-installation-properties.md).  

### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>Nepoužívejte automatické přiřazení lokality, pokud klient stáhne důvěryhodný kořenový klíč z prvního bodu správy, který kontaktuje.  

Chcete-li zabránit riziku nového klienta stahovat důvěryhodný kořenový klíč z podvodného bodu správy, použijte pouze automatické přiřazení lokality v následujících scénářích:  

- Klient má přístup k informacím o Configuration Manager lokalitě publikovaným na Active Directory Domain Services.  

- Klientovi předem poskytnete důvěryhodný kořenový klíč.  

- Používáte certifikáty PKI od certifikační autority rozlehlé sítě (CA) k vybudování důvěry mezi klientem a bodem správy.  

Další informace o důvěryhodném kořenovém klíči najdete v tématu [Plánování důvěryhodného kořenového klíče](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>Instalujte klientské počítače s možností CCMSetup Client.msi SMSDIRECTORYLOOKUP=NoWINS.  

Nejbezpečnější metodou umístění služby pro klienty, kteří chtějí hledat lokality a body správy, je použití služby AD DS (Active Directory Domain Services). Někdy tato metoda není pro některá prostředí možná. Nemůžete třeba pro Configuration Manager rozšíříte schéma služby Active Directory, nebo protože se klienti nacházejí v nedůvěryhodné doménové struktuře nebo v pracovní skupině. Pokud tato metoda není možná, použijte jako alternativní metodu umístění služby publikování DNS. Pokud tyto metody selžou a když bod správy není nakonfigurovaný pro připojení klientů pomocí protokolu HTTPS, klienti se můžou vrátit k použití služby WINS.  

Publikování do služby WINS je méně bezpečné než jiné metody publikování. Nakonfigurujte klientské počítače tak, aby se nevrátily k použití služby WINS, zadáním **SMSDIRECTORYLOOKUP = WINS**. Pokud musíte pro umístění služby použít službu WINS, použijte **SMSDIRECTORYLOOKUP = WINSSECURE**. Toto nastavení je výchozí. K ověření certifikátu podepsaného svým držitelem v bodu správy používá Configuration Manager důvěryhodný kořenový klíč.  

> [!NOTE]  
> Když nakonfigurujete klienta pro **SMSDIRECTORYLOOKUP = WINSSECURE** a nalezne bod správy ze služby WINS, klient zkontroluje kopii Configuration Manager důvěryhodného kořenového klíče, který je v rozhraní WMI.  
>
> Pokud se podpis na certifikátu bodu správy shoduje s kopií důvěryhodného kořenového klíče klienta, certifikát se ověří. Po ověření certifikátu spustí klient komunikaci s bodem správy, který našel pomocí služby WINS.  
>
> Pokud se podpis na certifikátu bodu správy neshoduje s kopií důvěryhodného kořenového klíče klienta, certifikát není platný. V tomto scénáři klient nekomunikuje s bodem správy, který našel pomocí služby WINS.  

### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Ujistěte se, že časové intervaly pro správu a údržbu jsou pro nasazení důležitých aktualizací softwaru dostatečně velké.  

Časová období údržby pro kolekce zařízení omezují dobu, po kterou Configuration Manager můžou na tato zařízení instalovat software. Pokud nakonfigurujete časový interval pro správu a údržbu, který je příliš malý, klient nemusí instalovat důležité aktualizace softwaru. Díky tomuto chování může klient ohrozit jakýkoli útok, který tato aktualizace softwaru snižuje.  

### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>Další bezpečnostní opatření pro omezení prostoru pro útoky v zařízeních se systémem Windows Embedded s filtry zápisu  

Když povolíte filtry zápisu na zařízeních se systémem Windows Embedded, všechny instalace a změny softwaru se provedou pouze v překrytí. Tyto změny se po restartu zařízení neuloží. Pokud pomocí Configuration Manager zakážete filtry zápisu, v průběhu této doby je integrované zařízení zranitelné se změnami všech svazků. Tyto svazky obsahují sdílené složky.  

Configuration Manager během této doby počítač zamkne, aby se mohli přihlásit jenom místní správci. Kdykoli je to možné, proveďte další bezpečnostní opatření, která vám pomůžou chránit počítač. Můžete například povolit další omezení pro bránu firewall.  

Pokud používáte časové intervaly pro správu a údržbu k zachování změn, naplánujte tato okna pečlivě. Minimalizujte dobu, po kterou jsou filtry zápisu zakázané, ale dostatečně dlouhé, aby bylo možné dokončit instalace softwaru a restarty.  

### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>Použití nejnovější verze klienta s instalací klienta na základě aktualizace softwaru

Pokud používáte instalaci klienta na základě aktualizace softwaru a v lokalitě nainstalujete novější verzi klienta, aktualizujte publikovanou aktualizaci softwaru. Pak klienti získají nejnovější verzi z bodu aktualizace softwaru.  

Když aktualizujete lokalitu, aktualizace softwaru pro nasazení klienta, která je publikovaná v bodě aktualizace softwaru, se automaticky neaktualizuje. Znovu publikujte klienta Configuration Manager do bodu aktualizace softwaru a aktualizujte číslo verze.  

Další informace najdete v tématu [instalace Configuration Manager klientů pomocí instalace na základě aktualizace softwaru](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>Pozastavit jenom položku kódu PIN BitLockeru na zařízeních s omezeným přístupem a s omezeným přístupem  

Nastavte pouze nastavení klienta na možnost **pozastavit zadání kódu PIN nástroje BitLocker při restartu** na hodnotu **vždy** u počítačů, kterým důvěřujete a které mají omezený fyzický přístup.

Když nastavíte toto nastavení klienta na **vždycky**, Configuration Manager může dokončit instalaci softwaru. Toto chování pomáhá nainstalovat kritické aktualizace softwaru a obnovit služby. Pokud útočník zachytí proces restartování, mohl by převzít kontrolu nad počítačem. Toto nastavení použijte pouze v případě, že důvěřujete počítači a je-li omezen fyzický přístup k počítači. Toto nastavení může být vhodné například pro servery v datovém centru.  

Další informace o tomto nastavení klienta najdete v tématu [informace o nastavení klienta](../about-client-settings.md#suspend-bitlocker-pin-entry-on-restart).  

### <a name="dont-bypass-powershell-execution-policy"></a>Obejít zásady spouštění PowerShellu

Pokud nakonfigurujete nastavení klienta Configuration Manager pro **zásady spouštění prostředí PowerShell** tak, aby se **nepoužívalo**, pak systém Windows povolí spuštění nepodepsaných skriptů PowerShellu. Toto chování může způsobit, že se malware na klientských počítačích spustí. Pokud vaše organizace vyžaduje tuto možnost, použijte vlastní nastavení klienta. Přiřaďte ji pouze klientským počítačům, které musí spouštět nepodepsané skripty prostředí PowerShell.  

Další informace o tomto nastavení klienta najdete v tématu [informace o nastavení klienta](../about-client-settings.md#powershell-execution-policy).  


## <a name="security-best-practices-for-mobile-devices"></a><a name="bkmk_mobile"></a>Osvědčené postupy zabezpečení pro mobilní zařízení  

### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>Instalace zprostředkujícího bodu registrace v hraniční síti a bodu zápisu v intranetu  

Pro Internetová mobilní zařízení, která zapíšete pomocí Configuration Manager, nainstalujte zprostředkující bod registrace v hraniční síti a bod registrace v intranetu. Toto rozdělení rolí přispívá k ochraně bodu registrace před útokem. Pokud by útočník napadnout bod registrace, mohl by získat certifikáty pro ověřování. Můžou také ukrást přihlašovací údaje uživatelů, kteří si zaregistrují svá mobilní zařízení.  

### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>Nakonfigurujte nastavení hesla, aby se chránila mobilní zařízení před neoprávněným přístupem.  

*Pro mobilní zařízení, která jsou zaregistrovaná pomocí Configuration Manager*: pomocí položky konfigurace mobilního zařízení nakonfigurujte složitost hesel jako PIN kód. Zadejte alespoň výchozí minimální délku hesla.  

*Pro mobilní zařízení, která nemají nainstalovaného klienta Configuration Manager, ale jsou spravovaná konektorem systému Exchange Server*: Nakonfigurujte **Nastavení hesla** pro konektor systému Exchange Server tak, aby složitost hesla byla PIN kódem. Zadejte alespoň výchozí minimální délku hesla.  

### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>Povolte pouze spouštění aplikací, které jsou podepsané společnostmi, kterým důvěřujete.  

Zabránit manipulaci s informacemi o inventáři a informacemi o stavu tím, že povolíte spouštění aplikací jenom v případě, že jsou podepsané společnostmi, kterým důvěřujete. Nepovolujte zařízením instalaci nepodepsaných souborů.  

*Pro mobilní zařízení zaregistrovaná v Configuration Manager*použijte položku konfigurace mobilního zařízení a nakonfigurujte nastavení zabezpečení **nepodepsané aplikace** na **zakázáno**. Nakonfigurujte **Instalace nepodepsaných souborů** jako důvěryhodný zdroj.  

*Pro mobilní zařízení, která nemají nainstalovaného klienta Configuration Manager, ale jsou spravovaná konektorem systému Exchange Server*: Nakonfigurujte **nastavení aplikace** pro konektor systému Exchange Server tak, aby byla instalace nepodepsaných **souborů** a **nepodepsané aplikace** **zakázaná**.  

### <a name="lock-mobile-devices-when-not-in-use"></a>Zamknout mobilní zařízení, pokud se nepoužívají  

Můžete zabránit zvýšení oprávnění proti útokům tím, že zamknete mobilní zařízení, když se nepoužívá.

*Pro mobilní zařízení, která jsou zaregistrovaná pomocí Configuration Manager*: pomocí položky konfigurace mobilního zařízení nakonfigurujte nastavení hesla **Doba nečinnosti v minutách, než se mobilní zařízení uzamkne**.  

*Pro mobilní zařízení, která nemají nainstalovaného klienta Configuration Manager, ale jsou spravovaná konektorem systému Exchange Server*: Nakonfigurujte **Nastavení hesla** pro konektor systému Exchange Server tak, aby bylo nastaveno **dobu nečinnosti v minutách, než se mobilní zařízení uzamkne**.  

### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>Omezení uživatelů, kteří můžou zaregistrovat svoje mobilní zařízení  

Omezte oprávnění tím, že omezíte uživatele, kteří můžou zaregistrovat svoje mobilní zařízení. Pokud chcete zápis mobilních zařízení povolit jenom autorizovaným uživatelům, použijte vlastní nastavení klienta místo výchozího nastavení klienta.  

### <a name="user-device-affinity-guidance-for-mobile-devices"></a>Doprovodné materiály k spřažení uživatelských zařízení pro mobilní zařízení  

Nesaďte aplikace uživatelům, kteří mají mobilní zařízení zaregistrovaná pomocí Configuration Manager nebo Microsoft Intune v následujících scénářích:  

- Mobilní zařízení používá více než jedna osoba.  

- Zařízení je zaregistrované správcem jménem uživatele.  

- Zařízení se přenáší na jiného uživatele, aniž by bylo nutné vyřazení z provozu, a pak zařízení znovu zaregistrovat.  

Registrace zařízení vytvoří vztah spřažení uživatelských zařízení. Tento vztah namapuje uživatele, který provádí registraci do mobilního zařízení. Pokud mobilní zařízení používá jiný uživatel, může spustit aplikace nasazené pro původního uživatele, což může vést ke zvýšení oprávnění. Obdobně platí, že pokud správce zapíše mobilní zařízení pro uživatele, aplikace nasazené uživateli nejsou nainstalovány v mobilním zařízení. Místo toho se můžou nainstalovat aplikace nasazené pro správce.  

Na rozdíl od spřažení uživatelských zařízení u počítačů s Windows nemůžete ručně definovat informace o spřažení uživatelských zařízení pro mobilní zařízení zaregistrovaná v Microsoft Intune.  

Pokud přenášíte vlastnictví mobilního zařízení, které je zaregistrované v Intune, nejdřív vyřaďte mobilní zařízení z Intune. Tato akce odebere vztah spřažení uživatelských zařízení. Pak požádejte aktuálního uživatele, aby zařízení znovu zaregistroval.  

### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>Ujistěte se, že uživatelé zaregistrovali svoje mobilní zařízení pro Microsoft Intune  

Během registrace se vytvoří vztah spřažení uživatelského zařízení. Tato akce namapuje uživatele, který provádí registraci do mobilního zařízení. Pokud správce zapíše mobilní zařízení pro uživatele, aplikace nasazené uživateli nejsou nainstalovány v mobilním zařízení. Místo toho se můžou nainstalovat aplikace nasazené pro správce.  

### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>Ochrana připojení mezi Configuration Manager serverem lokality a serverem Exchange Server

Pokud je server Exchange místní, použijte protokol IPsec. Hostovaný Exchange automaticky zabezpečuje připojení pomocí protokolu SSL.  

### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>Použijte princip nejnižších oprávnění pro konektor.  

Seznam minimálních rutin, které vyžaduje konektor systému Exchange Server, najdete v tématu [Správa mobilních zařízení pomocí Configuration Manager a Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-macs"></a><a name="bkmk_macs"></a>Osvědčené postupy zabezpečení pro počítače Mac  

### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>Ukládat zdrojové soubory klienta ze zabezpečeného umístění a přistupovat k nim  

Před instalací nebo registrací klienta v počítači Mac Configuration Manager neověřuje, jestli jsou tyto zdrojové soubory klienta úmyslně manipulovány. Stáhněte si tyto soubory z důvěryhodného zdroje. Bezpečné ukládání a přístup k nim.  

### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>Monitorování a sledování doby platnosti certifikátu  

V zájmu zachování nepřetržitého provozu monitorujte a sledujte dobu platnosti certifikátů používaných pro počítače Mac. Configuration Manager nepodporuje automatické obnovení tohoto certifikátu nebo upozorňuje na to, že platnost certifikátu brzy vyprší. Typická doba platnosti je jeden rok.  

Další informace o tom, jak obnovit certifikát, najdete v tématu [Ruční obnovení certifikátu klienta pro počítač Mac](../deploy-clients-to-macs.md#renew-the-mac-client-certificate).  

### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>Konfigurovat důvěryhodný kořenový certifikát jenom pro SSL  

Chcete-li zajistit ochranu proti zvýšení oprávnění, nakonfigurujte certifikát pro důvěryhodnou kořenovou certifikační autoritu, aby byl pouze důvěryhodný pro protokol SSL.

Při zápisu počítačů Mac se automaticky nainstaluje uživatelský certifikát pro správu klienta Configuration Manager. Tento uživatelský certifikát obsahuje certifikáty důvěryhodných kořenových certifikátů ve svém řetězu důvěryhodnosti. Pokud chcete omezit důvěryhodnost tohoto kořenového certifikátu jenom na protokol SSL, použijte následující postup:  

1. Na počítači Mac otevřete okno terminálu.  

2. Zadejte následující příkaz:`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3. V dialogovém okně **přístup do řetězce klíčů** v části **řetězce** klíčů klikněte na **systém**. Pak v části **kategorie** klikněte na **certifikáty**.  

4. Vyhledejte certifikát od kořenové certifikační autority pro klientský certifikát pro počítač Mac a dvakrát na něj klikněte.  

5. V dialogovém okně pro certifikát od kořenové certifikační autority rozbalte část **Důvěryhodnost** a proveďte tyto změny:  

    1. **Při použití tohoto certifikátu**: Změňte nastavení **vždy důvěřovat** na **použít výchozí systémové nastavení**.  

    2. **SSL (Secure Sockets Layer) (SSL)**: Změna **žádné hodnoty** na hodnotu **vždy důvěřovat**.  

6. Zavřete dialogové okno. Po zobrazení výzvy zadejte heslo správce a pak klikněte na **aktualizovat nastavení**.  

Po dokončení tohoto postupu je kořenový certifikát důvěryhodný jenom k ověření protokolu SSL. K dalším protokolům, které jsou teď nedůvěryhodné s tímto kořenovým certifikátem, patří Secure Mail (S/MIME), Extensible Authentication (EAP) nebo podepisování kódu.  

> [!NOTE]  
> Tento postup použijte také v případě, že jste nainstalovali certifikát klienta nezávisle na Configuration Manager.


## <a name="security-issues-for-configuration-manager-clients"></a><a name="BKMK_SecurityIssues_Clients"></a>Problémy se zabezpečením pro klienty Configuration Manager  

Tyto problémy se zabezpečením se nedají zmírnit:  

### <a name="status-messages-arent-authenticated"></a>Stavové zprávy nejsou ověřené.

U stavových zpráv neprobíhá žádné ověřování. Když bod správy přijme připojení klienta HTTP, může stavové zprávy na bod správy posílat jakékoli zařízení. Pokud bod správy přijímá jenom připojení klienta přes protokol HTTPS, musí mít zařízení platný certifikát pro ověřování klientů, ale může také odesílat jakékoli stavové zprávy. Bod správy zahodí jakoukoli neplatnou stavovou zprávu přijatou od klienta.  

Existuje několik možných útoků proti této chybě zabezpečení:

- Útočník by mohl odeslat falešnou stavovou zprávu, aby získal členství v kolekci, která je založena na dotazech na stavové zprávy.
- Jakýkoli klient může zahájit útok DoS proti bodu správy tak, že ho zahltí stavovými zprávami.
- Pokud se stavové zprávy spouštějí akcemi v pravidlech filtru stavových zpráv, útočník může spustit pravidlo filtru stavových zpráv.
- Útočník by mohl odeslat stavovou zprávu, která by generovala informace o vytváření sestav jako nepřesné.  

### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>U zásady se dá změnit cíl na necílené klienty.  

Existuje několik způsobů, které můžou útočníci využít k tomu, aby zásada cílená na jednoho klienta platila i pro úplně jiného klienta. Například útočník na důvěryhodném klientovi může odeslat falešné informace o inventáři nebo zjišťování, aby počítač přidal do kolekce, do které by neměl patřit. Klient pak obdrží všechna nasazení do této kolekce.

Existují ovládací prvky, které zabraňují útočníkům v přímé úpravě zásad. Útočníci ale můžou převzít existující zásadu, která přeformátuje a znovu nasadí operační systém a pošle ho na jiný počítač. Tato přesměrovaná zásada by mohla způsobit odepření služby. Tyto typy útoků by vyžadovaly přesné načasování a rozsáhlé znalosti infrastruktury Configuration Manager.  

### <a name="client-logs-allow-user-access"></a>Klientské protokoly umožňují přístup uživatelů.  

Všechny soubory protokolu klienta umožňují skupině **uživatelů** s oprávněním *ke čtení* a speciálnímu **interaktivnímu** uživateli s přístupem pro *zápis* . Pokud povolíte podrobné protokolování, útočníci můžou číst soubory protokolu a hledat v nich informace o ohrožení zabezpečení systému nebo kompatibility. Procesy, jako je třeba software, který klient nainstaluje v kontextu uživatele, musí zapisovat do protokolů s uživatelským účtem s omezenými právy. Toto chování znamená, že útočník může také zapisovat do protokolů pomocí účtu s omezenými právy.  

Nejzávažnějším rizikem je, že by útočník mohl odebrat informace v souborech protokolu. Správce může tyto informace potřebovat pro auditování a zjišťování neoprávněných vniknutí.  

### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>Počítač se dá použít k získání certifikátu, který je navržený pro zápis mobilního zařízení.  

Když Configuration Manager zpracuje žádost o registraci, nemůže ověřit požadavek pocházející z mobilního zařízení, nikoli z počítače. Pokud je žádost z počítače, může nainstalovat certifikát PKI, který pak umožní registraci v Configuration Manager.

Aby se zabránilo zvýšení oprávnění v tomto scénáři, umožněte jenom důvěryhodným uživatelům registraci svých mobilních zařízení. Pozorně sledujte aktivity registrace zařízení v lokalitě.  

### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>Zablokovaný klient může stále odesílat zprávy do bodu správy

Když zablokujete klienta, kterému už nedůvěřujete, ale navázali jste síťové připojení pro klientské oznámení, Configuration Manager relaci odpojí. Zablokovaný klient může dál pokračovat v odesílání paketů na svůj bod správy, dokud se klient neodpojí ze sítě. Tyto pakety jsou jen malé a keep-alive pakety. Tohoto klienta nelze spravovat pomocí Configuration Manager, dokud nebude odblokováno.  

### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>Automatický upgrade klienta neověřuje bod správy

Pokud používáte automatický upgrade klienta, může být klient přesměrován do bodu správy, aby stahoval zdrojové soubory klienta. V tomto scénáři klient neověřuje bod správy jako důvěryhodný zdroj.  

### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>Když uživatelé poprvé zaregistrují počítače Mac, hrozí riziko falšování identity DNS.  

Když se počítač Mac během registrace připojí ke zprostředkujícímu bodu registrace, není pravděpodobné, že počítač Mac už má certifikát důvěryhodné kořenové certifikační autority. V tomto okamžiku počítač Mac nedůvěřuje serveru a vyzve uživatele k pokračování. Pokud neautorizovaný server DNS přeloží plně kvalifikovaný název domény zprostředkujícího bodu registrace, může počítač Mac nasměrovat na neautorizovaný zprostředkující bod registrace a nainstalovat certifikáty z nedůvěryhodného zdroje. Pokud chcete toto riziko snížit, držte se osvědčených postupů, jak se vyhnout falšování identity serveru DNS ve vašem prostředí.  

### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>Registrace Mac neomezuje žádosti o certifikát.  

Uživatelé můžou počítače Mac znovu zapisovat a pokaždé požadovat nový klientský certifikát. Configuration Manager nekontroluje více požadavků nebo neomezuje počet certifikátů požadovaných z jednoho počítače. Neautorizovaný uživatel by mohl spustit skript, který zopakuje požadavek na zápis do příkazového řádku. Tento útok může způsobit odepření služby v síti nebo vydávající certifikační autoritě (CA). Pokud chcete toto riziko snížit, pečlivě monitorujte vydávající certifikační autoritu pro tento typ podezřelého chování. Okamžitě zablokuje z hierarchie Configuration Manager všechny počítače, které ukazují tento model chování.  

### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>Potvrzení o vymazání neověřuje, jestli se zařízení úspěšně vymazalo.  

Když zahájíte akci vymazání pro mobilní zařízení a Configuration Manager potvrdí vymazání, je ověření, že Configuration Manager zprávu úspěšně *odeslala* . Neověřuje, jestli zařízení v žádosti *projednalo* .

U mobilních zařízení spravovaných konektorem systému Exchange Server ověří potvrzení o vymazání, že byl příkaz přijat serverem Exchange, nikoli zařízením.  

### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Pokud použijete možnosti pro potvrzení změn v zařízeních se systémem Windows Embedded, mohou být účty uzamčeny dřív, než se očekávalo.  

Pokud je v zařízení se systémem Windows Embedded spuštěná verze operačního systému starší než Windows 7 a uživatel se pokusí přihlásit, zatímco Configuration Manager filtry zápisu, umožňuje Windows pouze polovinu nakonfigurovaného počtu nesprávných pokusů před uzamknutím účtu.

Například můžete nakonfigurovat zásady domény pro **mezní hodnotu uzamčení účtu** na šest pokusů. Uživatel třikrát zapíše heslo a účet je uzamčen. Toto chování efektivně vytvoří útok na službu. Pokud se uživatelé v tomto scénáři musí přihlašovat do integrovaných zařízení, upozorněte je, že se jedná o potenciální prahovou hodnotu omezeného uzamčení.  


## <a name="privacy-information-for-configuration-manager-clients"></a><a name="BKMK_Privacy_Clients"></a>Informace o ochraně osobních údajů pro klienty Configuration Manager  

Když nasadíte klienta Configuration Manager, povolíte nastavení klienta pro funkce Configuration Manager. Nastavení, která použijete ke konfiguraci funkcí, se můžou vztahovat na všechny klienty v hierarchii Configuration Manager. Toto chování je stejné, ať už jsou přímo připojené k interní síti, připojené přes vzdálenou relaci nebo připojené k Internetu.  

Informace o klientech jsou uloženy v databázi Configuration Manager na serveru SQL a nejsou odesílány společnosti Microsoft. Informace se uchovávají v databázi, dokud je neodstraní úlohy údržby lokality **Odstranit stará data zjišťování** každých 90 dní. Můžete provést konfiguraci intervalu odstranění. 

Některá sumarizovaná nebo agregovaná diagnostická data a data o využití se odesílají společnosti Microsoft. Další informace najdete v tématu [Diagnostika a data o využití](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Před konfigurací klienta Configuration Manager zvažte své požadavky na ochranu osobních údajů.  

Další informace o shromažďování a používání dat od Microsoftu najdete v [prohlášení Microsoftu o zásadách ochrany osobních údajů](https://privacy.microsoft.com/privacystatement).

### <a name="client-status"></a>Stav klienta  

Configuration Manager monitoruje aktivity klientů. Pravidelně vyhodnocuje Configuration Manager klienta a může opravit problémy s klientem a jeho závislostmi. Stav klienta je ve výchozím nastavení povolen. Pro kontroly aktivity klienta používá metriky na straně serveru. Stav klienta používá akce na straně klienta pro samoobslužné kontroly, nápravu a odesílání informací o stavu klienta do lokality. Klient spustí samočinné kontroly podle plánu, který nakonfigurujete. Klient odesílá výsledky kontrol do lokality Configuration Manager. Informace se při přenosu šifrují.  

Informace o stavu klienta jsou uloženy v databázi Configuration Manager v systému SQL Server a nejsou odesílány společnosti Microsoft. Informace v databázi lokality nejsou uložené v šifrovaném formátu. Tyto informace se uchovávají v databázi, dokud se neodstraní podle hodnoty nakonfigurované pro **uchování historie stavu klienta po dobu, po kterou** se nastaví stav klienta. Výchozí hodnota tohoto nastavení je 31 dní.  

Před instalací klienta Configuration Manager s kontrolou stavu klienta zvažte své požadavky na ochranu osobních údajů.  


## <a name="privacy-information-for-mobile-devices-that-are-managed-with-the-exchange-server-connector"></a><a name="BKMK_Privacy_ExchangeConnector"></a>Informace o ochraně osobních údajů pro mobilní zařízení spravovaná pomocí konektoru systému Exchange Server  

Konektor systému Exchange Server vyhledá a spravuje zařízení, která se připojují k místnímu nebo hostovanému serveru Exchange pomocí protokolu ActiveSync. Záznamy nalezené konektorem systému Exchange Server se ukládají do databáze Configuration Manager ve vašem SQL serveru. Informace se shromažďují ze systému Exchange Server. Neobsahuje žádné další informace, které mobilní zařízení odesílají do systému Exchange Server.  

Informace o mobilním zařízení nejsou odesílány společnosti Microsoft. Informace o mobilních zařízeních jsou uložené v databázi Configuration Manager ve vašem SQL serveru. Informace se uchovávají v databázi, dokud je neodstraní úloha údržby lokality **Odstranit stará data zjišťování** každých 90 dní. Nakonfigurujete interval odstraňování.  

Před instalací a konfigurací konektoru systému Exchange Server zvažte své požadavky na ochranu osobních údajů.  

Další informace o shromažďování a používání dat od Microsoftu najdete v [prohlášení Microsoftu o zásadách ochrany osobních údajů](https://privacy.microsoft.com/privacystatement).
