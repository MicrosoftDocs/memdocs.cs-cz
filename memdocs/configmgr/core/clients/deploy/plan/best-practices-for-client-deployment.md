---
title: Osvědčené postupy nasazení klientů
titleSuffix: Configuration Manager
description: Získejte osvědčené postupy pro nasazení klientů v Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28f8bfb2ef012fcd4f19835190b7c042d38fd9e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713335"
---
# <a name="best-practices-for-client-deployment-in-configuration-manager"></a>Osvědčené postupy pro nasazení klientů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Použijte instalaci klienta na základě aktualizace softwaru pro počítače služby Active Directory  
 Tato metoda nasazení klienta používá existující technologie Windows, integruje se s infrastrukturou služby Active Directory, vyžaduje nejmenší konfiguraci v Configuration Manager, je nejjednodušší nakonfigurovat pro brány firewall a je nejbezpečnější. Díky skupinám zabezpečení a filtrování WMI pro konfiguraci Zásady skupiny máte také značnou flexibilitu při řízení, které počítače mají nainstalovat klienta Configuration Manager.  

 Další informace najdete v tématu [Instalace klientů nástroje Configuration Manager metodou instalace na základě aktualizace softwaru](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Rozšiřte schéma služby Active Directory a publikujte lokalitu způsobem umožňujícím spuštění služby CCMSetup bez možností příkazového řádku  
 Když rozšíříte schéma služby Active Directory pro Configuration Manager a lokalita je publikovaná do Active Directory Domain Services, mnoho vlastností instalace klienta se publikuje na Active Directory Domain Services. Pokud počítač dokáže tyto vlastnosti instalace klienta vyhledat, může je použít během Configuration Manager nasazení klienta. Protože jsou tyto informace generovány automaticky, je omezeno riziko lidské chyby související s ručním zadáváním vlastností instalace.  

 Další informace najdete v tématu [o vlastnostech instalace klienta publikovaných na Active Directory Domain Services](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>Použití dvoufázové implementace ke správě využití CPU  
 Minimalizujte vliv požadavků na výpočetní výkon procesoru na serveru lokality pomocí dvoufázové zavedení klientů. Nasaďte klienty mimo pracovní dobu, aby měly jiné služby během dne větší dostupnou šířku pásma, a uživatelé nenarušili, pokud jejich počítač zpomaluje nebo vyžaduje restart.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Po dokončení hlavního nasazení klientů povolte automatický upgrade  
 [Automatické upgrady klientů](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) jsou užitečné v případě, že chcete upgradovat malý počet klientských počítačů, které by mohly být vynechaly vaší hlavní metodou instalace klienta, třeba kvůli tomu, že byly offline. 

> [!NOTE]  
>  Vylepšení výkonu v Configuration Manager vám umožní použít automatické upgrady jako primární metodu upgradu klienta. Výkon však bude záviset na infrastruktuře hierarchie, například na počtu klientů.  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>V případě instalace klienta pomocí vlastností client.msi použijte vlastnost SMSMP a FSP  
 Vlastnost SMSMP určí počáteční bod správy, se kterým bude klient komunikovat, a odebere závislost na řešeních umístění služeb, například AD DS (Active Directory Domain Services), DNS a WINS.  

 Pomocí vlastnosti FSP nainstalujete bod záložního stavu, takže můžete sledovat instalaci a přiřazení klienta a zjistit případné potíže v komunikaci.  

 Další informace o těchto možnostech najdete v tématu [informace o vlastnostech instalace klienta](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>Nainstalovat jazykové sady klienta před instalací klientů  
Před nasazením klienta doporučujeme nainstalovat jazykové sady klienta. Pokud nainstalujete [jazykové sady klienta](../../../../core/servers/deploy/install/language-packs.md) (pro povolení dalších jazyků) na webu po instalaci klientů, musíte klienty přeinstalovat, aby mohli používat tyto jazyky. U klientů mobilních zařízení je nutné mobilní zařízení vymazat a znovu ho zaregistrovat.  

## <a name="prepare-required-pki-certificates-in-advance"></a>Příprava požadovaných certifikátů PKI předem  
 Chcete-li spravovat zařízení na internetu, zaregistrovaná mobilní zařízení a počítače se systémem Mac, je nutné mít v systémech lokality (body správy a distribuční body) a v klientských zařízeních certifikáty PKI. V produkčních sítích můžete pro použití nových certifikátů a restartování serverů systémů lokality vyžadovat schválení správy změn nebo nutnost odhlášení a přihlášení uživatelů za účelem členství v nové skupině. Dále může být zapotřebí povolit dostatek času pro replikaci oprávnění zabezpečení a pro jakékoli nové šablony certifikátů.  

 Další informace o vyžadovaných certifikátech PKI najdete v tématu [požadavky na certifikát PKI pro Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Před instalací klientů nakonfigurujte jakékoli požadované časové intervaly pro nastavení a údržbu klientů  
 I když můžete [nakonfigurovat nastavení klienta](../../../../core/clients/deploy/configure-client-settings.md) a časové intervaly pro správu a údržbu před instalací klientů nebo po nich, je lepší nakonfigurovat požadovaná nastavení před instalací klientů, aby byly použity ihned po instalaci klienta. 

 Nakonfigurujte časové intervaly pro správu a údržbu pro servery a zařízení se systémem Windows Embedded, aby se zajistila kontinuita provozu důležitých zařízení. Časové intervaly pro správu a údržbu zajistí, že požadované aktualizace softwaru a antimalwarový software nerestartují počítač během pracovní doby.  

> [!IMPORTANT]  
>  Pro počítače s Windows 10, které chcete chránit pomocí sjednoceného filtru zápisu (UWF), je nutné nakonfigurovat zařízení pro UWF před instalací klienta. Tato možnost umožňuje Configuration Manager instalovat klienta s vlastním poskytovatelem přihlašovacích údajů, který uživatelům s omezenými právy při přihlášení k zařízení během režimu údržby zamkne uživatele s nízkými právy.  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>Plánování možností registrace uživatelů pro počítače Mac a mobilní zařízení   
 Pokud uživatelé zaregistrují vlastní počítače se systémem Mac a mobilní zařízení pomocí Configuration Manager, naplánujte činnost koncového uživatele. Například můžete skriptovat proces instalace a registrace pomocí webové stránky, takže uživatelé zadají minimální množství nezbytných informací a odesílají pokyny s odkazem e-mailem.  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Použití souborové filtry zápisu pro zařízení se systémem Windows Embedded 
 V integrovaných zařízeních používajících vylepšené filtry zápisu (Enhanced Write Filters, EWF) pravděpodobně dojde k opětovným synchronizacím stavových zpráv. Pokud máte pouze několik integrovaných zařízení používajících vylepšené filtry zápisu (Enhanced Write Filters, EWF), pravděpodobně si toho nevšimnete. Pokud však máte velký počet integrovaných zařízení, která opětovně synchronizují své informace, například odeslání úplného inventáře místo rozdílového inventáře, může dojít k výraznému nárůstu síťových paketů a výpočetního výkonu procesoru na serveru lokality.  

 Pokud máte zvolený typ filtru zápisu, který chcete povolit, zvolte souborové filtry zápisu a nakonfigurujte výjimky tak, aby trval stav klienta a data inventáře mezi restarty zařízení pro síť a efektivitu procesoru klienta Configuration Manager. Další informace o filtrech zápisu najdete v tématu [Plánování nasazení klientů na zařízení se systémem Windows Embedded](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Další informace o maximálním počtu klientů s Windows Embedded, jaký může primární lokalita podporovat, najdete v tématu [Podporované operační systémy pro klienty a zařízení](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  
