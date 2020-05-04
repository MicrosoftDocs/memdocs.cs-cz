---
title: Plánování nasazení klienta na počítače se systémy Linux a UNIX
titleSuffix: Configuration Manager
description: Naplánujte nasazení klientů na počítače se systémy Linux a UNIX v Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dfede7594224ff48af2a1e4066e69d551c3c576e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713230"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-configuration-manager"></a>Plánování nasazení klientů na počítače se systémy Linux a UNIX v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

> [!Important]  
> Počínaje verzí 1902 Configuration Manager nepodporuje klienty se systémy Linux a UNIX. 
> 
> Zvažte Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.

Klienta Configuration Manager můžete nainstalovat do počítačů se systémem Linux nebo UNIX. Tento klient je navržený pro servery, které pracují jako počítač pracovní skupiny, a klient nepodporuje interakci s přihlášenými uživateli. Po instalaci klientského softwaru a navázání komunikace s Configuration Manager bude klient spravovat pomocí konzoly Configuration Manager a sestav.  

> [!NOTE]
>  Klient Configuration Manager pro počítače se systémy Linux a UNIX nepodporuje následující možnosti správy:  
> 
> - Klientská nabízená instalace  
>   -   Nasazení operačního systému  
>   -   Nasazení aplikace, místo toho nasaďte software pomocí balíčků a programů.  
>   -   Inventář softwaru  
>   -   Aktualizace softwaru  
>   -   Nastavení dodržování předpisů  
>   -   Vzdálené řízení  
>   -   Řízení spotřeby  
>   -   Kontrola a náprava stavu klienta  
>   -   Internetová správa klientů  

 Informace o podporovaných distribucích systémů Linux a UNIX a o hardwaru potřebném k podpoře klienta pro Linux a UNIX najdete v části [doporučený hardware pro Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Informace v tomto článku vám pomůžou při plánování nasazení klienta Configuration Manager pro systémy Linux a UNIX.  

##  <a name="prerequisites-for-client-deployment-to-linux-and-unix-servers"></a><a name="BKMK_ClientDeployPrereqforLnU"></a>Předpoklady pro nasazení klienta na servery se systémy Linux a UNIX  
 Pomocí následujících informací můžete určit předpoklady, které je potřeba splnit, abyste mohli úspěšně nainstalovat klienta pro Linux a UNIX.  

###  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ClientDeployExternalforLnU"></a>Vnější závislosti Configuration Manager:  
 V níže uvedených tabulkách najdete popis požadovaných operačních systémů UNIX a Linux a závislostí balíčků.  

 **Systém Red Hat Enterprise Linux Server verze 5.1 (Tikanga)**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|glibc|Standardní knihovny jazyka C|2.5-12|  
|Openssl|Knihovny OpenSSL; protokol Secure Network Communications|0.9.8b-8.3.el5|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14.el5|  

 **Systém Red Hat Enterprise Linux Server verze 6**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|glibc|Standardní knihovny jazyka C|2.12-1.7|  
|Openssl|Knihovny OpenSSL; protokol Secure Network Communications|1.0.0-4|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

 **Red Hat Enterprise Linux Server verze 7**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|glibc|Standardní knihovny jazyka C|2.17|  
|Openssl|Knihovny OpenSSL; protokol Secure Network Communications|1.0.1|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

 **Solaris 10 SPARC**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|Požadovaná oprava operačního systému|Nevrácená paměť systému PAM|117463-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Matematické & mikrotaskingové knihovny (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Matematické & mikrotaskingové knihovny (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Základní knihovny systému Solaris (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Základní knihovny systému Solaris (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|OpenSSL|SUNopenssl-libraries (Usr)<br /><br /> Sun poskytuje knihovny OpenSSL pro platformy Solaris 10 SPARC. Jsou dodávané společně s operačním systémem.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Pluggable Authentication Modules<br /><br /> SUNWcsr, Core Solaris (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|Požadovaná oprava operačního systému|Nevrácená paměť systému PAM|117464-04|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Knihovny Math & Microtasking (uživatel root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Základní systém Solaris, (sdílené knihovny) (i386)|11.10.0,REV=2005.01.21.16.34|  
|SUNWcslr|Základní knihovny systému Solaris (uživatel root) (i386)|11.10.0, REV=2005.01.21.16.34|  
|OpenSSL|SUNWopenssl-libraries; knihovny OpenSSL (uživatel) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Pluggable Authentication Modules<br /><br /> Základní systém Solaris SUNWcsr, (uživatel root) (i386)|11.10.0,REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Knihovny Math a Microtasking (uživatel root)|5.11, REV=2011.04.11|  
|SUNWcslr|Základní knihovny systému Solaris (uživatel root)|11.11, REV=2009.11.11|  
|SUNWcsl|Základní systém Solaris, (sdílené knihovny)|11.11, REV=2009.11.11|  
|SUNWcsr|Základní systém Solaris (uživatel root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|Knihovny OpenSSL (uživatel)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Knihovny Math a Microtasking (uživatel root)|5.11, REV=2011.04.11|  
|SUNWcslr|Základní knihovny systému Solaris (uživatel root)|11.11, REV=2009.11.11|  
|SUNWcsl|Základní systém Solaris, (sdílené knihovny)|11.11, REV=2009.11.11|  
|SUNWcsr|Základní systém Solaris (uživatel root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|Knihovny OpenSSL (uživatel)|11.11.0,REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|glibc-2.4-31.30|Standardní sdílená knihovna jazyka C|2.4-31.30|  
|OpenSSL|Knihovny OpenSSL; protokol Secure Network Communications|0.90,8a-18,15|  
|PAM|Pluggable Authentication Modules|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Standardní sdílená knihovna jazyka C|2.9-13.2|  
|PAM|Pluggable Authentication Modules|pam-1.0.2-20.1|  

 **Univerzální systém Linux (balíček Debian) Debian, nástroj Ubuntu Server**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|libc6|Standardní sdílená knihovna jazyka C|2.3.6|  
|OpenSSL|Knihovny OpenSSL; protokol Secure Network Communications|0.9.8 nebo 1.0|  
|PAM|Pluggable Authentication Modules|0.79-3|  

 **Univerzální systém Linux (balíček RPM) CentOS, Oracle Linux**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|glibc|Standardní sdílená knihovna jazyka C|2.5-12|  
|OpenSSL|Knihovny OpenSSL; protokol Secure Network Communications|0.9.8 nebo 1.0|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|Verze operačního systému|Verze operačního systému|AIX 6,1: jakákoli úroveň technologie a aktualizace Service Pack|  
|xlC.rte|Modul XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|Knihovny OpenSSL; protokol Secure Network Communications|0.9.8.4|  

 **IBM AIX 7,1 (Power)**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|Verze operačního systému|Verze operačního systému|AIX 7,1: jakákoli úroveň technologie a aktualizace Service Pack|  
|xlC.rte|Modul XL C/C++ Runtime||  
|OpenSSL/openssl.base|Knihovny OpenSSL; protokol Secure Network Communications||  


 **HP-UX 11i v3 IA64**  

|Požadovaný balíček|Popis|Minimální verze|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.110,310,0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Specifické vývojářské knihovny IA|B.110,31|  
|SysMgmtMin|Minimální nástroje pro nasazení softwaru|B.110,310,0709|  
|SysMgmtMin.openssl|Knihovny OpenSSL; protokol Secure Network Communications|A.00.09.08d.002|  
|PAM|Pluggable Authentication Modules|V systému HP-UX je PAM součástí základních komponent operačního systému. Neexistují žádné další závislosti.|  

 **Configuration Manager závislosti:** Následující tabulka uvádí role systému lokality, které podporují klienty se systémy Linux a UNIX. Další informace o těchto rolích systému lokality najdete v tématu [Určení rolí systému lokality pro klienty Configuration Manager](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Configuration Manager systém lokality|Další informace|  
|---------------------------------------|----------------------|  
|Bod správy|I když bod správy není vyžadován k instalaci klienta Configuration Manager pro systémy Linux a UNIX, musíte mít bod správy pro přenos informací mezi klientskými počítači a servery Configuration Manager. Bez bodu správy nemůžete spravovat klientské počítače.|  
|Distribuční bod|Distribuční bod není vyžadován k instalaci klienta Configuration Manager pro systémy Linux a UNIX. Role systému lokality je ale potřeba k nasazení softwaru na servery se systémy Linux a UNIX.<br /><br /> Protože klient Configuration Manager pro systémy Linux a UNIX nepodporuje komunikaci, která používá protokol SMB, musí distribuční body, které s klientem používáte, podporovat komunikaci pomocí protokolu HTTP nebo HTTPS.|  
|Bod záložního stavu|Pro instalaci klienta Configuration Manager pro systémy Linux a UNIX není vyžadován záložní stavový bod. Bod stavu pro použití náhradní lokality ale umožňuje počítačům v Configuration Manager lokality odesílat stavové zprávy, když nemůžou komunikovat s bodem správy. Client také může do bodu stavu pro použití náhradní lokality odesílat stav instalace.|  

 **Požadavky na bránu firewall**: Ujistěte se, že brány firewall neblokují komunikaci mezi porty, které zadáte jako porty požadavků klientů. Klient pro Linux a UNIX komunikuje přímo s body správy, distribučními body a body stavu pro použití náhradní lokality.  

 Informace o komunikaci klienta a portech požadavku najdete v tématu [Konfigurace klienta pro Linux a UNIX, aby vyhledal body správy](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="planning-for-communication-across-forest-trusts-for-linux-and-unix-servers"></a><a name="BKMK_PlanningforCommunicationsforLnU"></a>Plánování komunikace mezi vztahy důvěryhodnosti mezi doménovými strukturami pro servery se systémy Linux a UNIX  
 Servery se systémy Linux a UNIX, které spravujete pomocí Configuration Manager fungují jako klienti pracovní skupiny a vyžadují podobné konfigurace jako klienti se systémem Windows, kteří jsou v pracovní skupině. Informace o komunikaci z počítačů, které jsou v pracovních skupinách, najdete v tématu [komunikace napříč doménovými strukturami služby Active Directory](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).  

###  <a name="service-location-by-the-client-for-linux-and-unix"></a><a name="BKMK_ServiceLocationforLnU"></a>Umístění služby klientem pro systémy Linux a UNIX  
 Úloha vyhledání serveru systému lokality, který poskytuje služby klientům, se označuje jako umístění služby. Na rozdíl od klienta se systémem Windows klient pro Linux a UNIX nepoužívá k umístění služby službu Active Directory. Kromě toho klient Configuration Manager pro systémy Linux a UNIX nepodporuje vlastnost klienta, která určuje příponu domény bodu správy. Místo toho se klient dozví o dalších serverech systému lokality, které poskytují služby klientům, ze známého bodu správy, který přiřadíte při instalaci softwaru klienta.  

 Další informace najdete v tématu věnovaném [umístění služby a způsobu, jakým klienti určují přiřazený bod správy](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

##  <a name="planning-for-security-and-certificates-for-linux-and-unix-servers"></a><a name="BKMK_SecurityforLnU"></a>Plánování zabezpečení a certifikátů pro servery se systémy Linux a UNIX  
 Pro zabezpečenou a ověřenou komunikaci s Configuration Manager lokalit používá klient Configuration Manager pro systémy Linux a UNIX stejný model pro komunikaci jako klient služby Configuration Manager pro systém Windows.  

 Když nainstalujete klienta se systémem Linux a UNIX, můžete klientovi přiřadit certifikát PKI, který mu umožní komunikovat s Configuration Manager lokalitami pomocí protokolu HTTPS. Pokud nepřiřazujete certifikát PKI, klient vytvoří certifikát podepsaný svým držitelem a bude komunikovat pouze pomocí protokolu HTTP.  

 Klienti, kterým se při instalaci přiřadí certifikát PKI, používají ke komunikaci s body správy protokol HTTPS. Pokud klient nemůže najít bod správy, který podporuje protokol HTTPS, použije místo toho protokol HTTP se zadaným certifikátem PKI.  

 Když klient se systémem Linux nebo UNIX používá certifikát PKI, nemusíte ho schvalovat. Pokud klient používá certifikát podepsaný svým držitelem, zkontrolujte nastavení hierarchie pro schválení klienta v konzole Configuration Manager. Pokud není nastavená metoda schvalování klientů na **Automaticky schválit všechny počítače (nedoporučuje se)**, musíte klienta schválit ručně.  

 Další informace o tom, jak ručně schválit klienta, najdete v tématu [Správa klientů z uzlu zařízení](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 Informace o používání certifikátů v Configuration Manager najdete v tématu požadavky na [certifikát PKI](../../../plan-design/network/pki-certificate-requirements.md).  

###  <a name="about-certificates-for-use-by-linux-and-unix-servers"></a><a name="BKMK_AboutCertsforLnU"></a>O certifikátech pro použití servery se systémy Linux a UNIX  
 Klient Configuration Manager pro systémy Linux a UNIX používá certifikát podepsaný svým držitelem nebo certifikát PKI X. 509, stejně jako klienti se systémem Windows. Při správě klientů se systémy Linux a UNIX se nemění požadavky na infrastrukturu veřejných klíčů pro Configuration Manager systémy lokality.  

 Certifikáty, které použijete pro klienty se systémy Linux a UNIX, kteří komunikují s Configuration Manager systémy lokalit, musí být ve formátu PKCS # 12 (Public Key Certificate Standard) a musí být známé heslo, abyste ho mohli určit klientovi při zadání certifikátu PKI.  

 Klient Configuration Manager pro systémy Linux a UNIX podporuje jeden certifikát PKI a nepodporuje více certifikátů. Proto se nevztahují na kritéria výběru certifikátů, která nakonfigurujete pro lokalitu Configuration Manager.  

###  <a name="configuring-certificates-for-linux-and-unix-servers"></a><a name="BKMK_ConfigCertsforLnU"></a>Konfigurace certifikátů pro servery se systémy Linux a UNIX  
 Pokud chcete nakonfigurovat klienta Configuration Manager pro servery se systémy Linux a UNIX, aby používal komunikaci pomocí protokolu HTTPS, musíte klienta nakonfigurovat tak, aby používal certifikát PKI v době instalace klienta. Certifikát nemůžete zřídit před instalací klientského softwaru.  

 Když instalujete klienta, který používá certifikát PKI, pomocí parametru `-UsePKICert` příkazového řádku můžete zadat umístění a název souboru PKCS # 12, který obsahuje certifikát PKI. Kromě toho musíte použít parametr `-certpw` příkazového řádku k zadání hesla pro certifikát.  

 Pokud nezadáte `-UsePKICert`, klient vygeneruje certifikát podepsaný svým držitelem a pokusí se komunikovat se servery systému lokality pouze pomocí protokolu HTTP.  

##  <a name="versions-that-dont-support-sha-256"></a><a name="BKMK_NoSHA-256"></a>Verze, které nepodporují algoritmus SHA-256  
 Následující operační systémy Linux a UNIX, které jsou podporované jako klienti pro Configuration Manager, byly vydané s verzemi OpenSSL, které nepodporují algoritmus SHA-256:  

-   Solaris verze 10 (SPARC/x86)  


 Chcete-li spravovat tyto operační systémy pomocí Configuration Manager, je nutné nainstalovat klienta Configuration Manager pro systémy Linux a UNIX s přepínačem příkazového řádku, který klienta přesměruje na přeskočení ověřování algoritmu SHA-256. Configuration Manager klienti, kteří běží na těchto verzích operačních systémů, pracují v méně zabezpečeném režimu než klienti, kteří podporují SHA-256. Tento méně zabezpečený režim má následující chování:  

-   Klienti neověřují podpis serveru lokality přidružené k zásadě, kterou vyžadují z bodu správy.  

-   Klienti neověřují hodnotu hash pro balíčky, které stáhnou z distribučního bodu.  

> [!IMPORTANT]  
>  `ignoreSHA256validation` Možnost umožňuje spustit klienta pro počítače se systémem Linux a UNIX v méně zabezpečeném režimu. To je určené pro použití na starších platformách, které nenabízely podporu algoritmu SHA-256. Toto chování potlačuje zabezpečení a Microsoft ho nedoporučuje, ale přesto podporuje jeho použití v zabezpečeném a důvěryhodném prostředí datového centra.  

 Při instalaci klienta Configuration Manager pro systémy Linux a UNIX instalační skript zkontroluje verzi operačního systému. Ve výchozím nastavení platí, že pokud je verze operačního systému identifikována jako uvolněná bez verze OpenSSL, která podporuje SHA-256, instalace klienta Configuration Manager se nezdařila.  

 Chcete-li nainstalovat klienta Configuration Manager v operačních systémech Linux a UNIX, které nebyly vydány s verzí OpenSSL s podporou algoritmu SHA-256, je nutné použít přepínač `ignoreSHA256validation`příkazového řádku Install. Použijete-li tuto možnost příkazového řádku v příslušném operačním systému Linux nebo UNIX, klient Configuration Manager přeskočí ověřování SHA-256 a po instalaci nebude klient používat algoritmus SHA-256 k podepsání dat, která odesílá do systémů lokality pomocí protokolu HTTP. Informace o konfiguraci klientů se systémy Linux a UNIX na používání certifikátů najdete v tématu [Plánování zabezpečení a certifikátů pro servery se systémy Linux a UNIX](#BKMK_SecurityforLnU). Další informace o vyžadování algoritmu SHA-256 najdete v tématu [Konfigurace podepisování a šifrování](../../../plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption).  

> [!NOTE]  
>  Možnost `ignoreSHA256validation` příkazového řádku se ignoruje na počítačích, na kterých běží verze systémů Linux a UNIX, která byla vydaná s verzemi OpenSSL, které podporují algoritmus SHA-256.  
