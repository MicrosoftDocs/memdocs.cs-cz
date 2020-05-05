---
title: Chránit počítače před malwarem
titleSuffix: Configuration Manager
description: Naučte se implementovat Endpoint Protection v Configuration Manager k ochraně počítačů před útoky z malwaru.
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.openlocfilehash: 6e0e350fe490de50a053e93f2922feba5e0ea8c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722386"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>Ukázkový scénář: použití Endpoint Protection k ochraně počítačů před malwarem

*Platí pro: Configuration Manager (Current Branch)*

Tento článek popisuje ukázkový scénář, jak můžete implementovat Endpoint Protection v Configuration Manager k ochraně počítačů ve vaší organizaci před útoky z malwaru.  



## <a name="scenario-overview"></a>Přehled scénáře

 Configuration Manager se instalují a používají v Woodgrove Bank. Banka aktuálně používá nástroj System Center Endpoint Protection k ochraně počítačů před útoky na malware. Banka dál používá zásady skupiny systému Windows k zajištění toho, že je ve všech počítačích společnosti povolená brána Windows Firewall a že uživatelé se upozorní, když brána Windows Firewall blokuje nový program.  

Správci Configuration Manager byli požádáni o upgrade antimalwarového softwaru Woodgrove Bank na System Center Endpoint Protection, aby banka mohla využívat nejnovější antimalwarové funkce a aby bylo možné centrálně spravovat antimalwarová řešení z konzoly Configuration Manager. 


## <a name="business-requirements"></a>Podnikové požadavky

Tato implementace má tyto požadavky:  

- Pomocí Configuration Manager můžete spravovat nastavení brány Windows Firewall, která jsou aktuálně spravovaná pomocí Zásady skupiny.  

- Ke stažení definic malwaru do počítačů použijte Configuration Manager aktualizace softwaru. Pokud nejsou k dispozici aktualizace softwaru, například pokud počítač není připojený k podnikové síti, musí si počítače stáhnout aktualizace definic z Microsoft Update.  

- Počítače uživatelů musí každý den provádět rychlou kontrolu malwaru. Servery ale musí spustit úplnou kontrolu každou sobotu mimo pracovní dobu v 1:00 ráno.  

- Když nastane libovolná z následujících událostí, odešle se e-mailová výstraha:  

  -   V libovolném počítači se zjistí malware.  

  -   Stejná malwarová hrozba se zjistí ve víc než 5 procentech počítačů.  

  -   Stejná hrozba malwaru se během 24 hodin zjistila víc než pětkrát.  

  -   V období 24 hodin se zjistí víc než 3 různé typy malwaru.  

  Správce pak provede následující kroky, které implementují Endpoint Protection:  



##  <a name="steps-to-implement-endpoint-protection"></a> Postup implementace služby Endpoint Protection  

|Proces|Referenční informace|  
|-------------|---------------|  
|Správci si prostudují dostupné informace o základních konceptech Endpoint Protection v Configuration Manager.|Přehled informací o Endpoint Protection najdete v tématu [Endpoint Protection](endpoint-protection.md).|  
|Správci kontrolují a implementují požadované předpoklady pro použití Endpoint Protection.|Informace o požadavcích pro Endpoint Protection najdete v tématu [plánování pro Endpoint Protection](../plan-design/planning-for-endpoint-protection.md).|  
|Správci instalují Endpoint Protection role systému lokality pouze na jeden server systému lokality, a to v horní části hierarchie Woodgrove Bank.|Další informace o tom, jak nainstalovat roli systému lokality Endpoint Protection, najdete v části "požadavky" v tématu [konfigurace Endpoint Protection](endpoint-protection-configure.md).|  
|Správci konfigurují Configuration Manager k posílání e-mailových upozornění pomocí serveru SMTP.<br /><br /> **Poznámka:** Server SMTP je nutné nakonfigurovat pouze v případě, že chcete při vygenerování výstrahy Endpoint Protection odeslat oznámení e-mailem.|Další informace najdete v tématu [Konfigurace výstrah v Endpoint Protection](endpoint-configure-alerts.md).|  
|Správci vytvoří kolekci zařízení, která obsahuje všechny počítače a servery pro instalaci klienta Endpoint Protection. Tuto kolekci pojmenuje **všechny počítače chráněné Endpoint Protection**.<br /><br /> **Tip:** Nemůžete konfigurovat výstrahy pro kolekce uživatelů.|Další informace o vytváření kolekcí najdete v tématu [vytváření kolekcí](../../core/clients/manage/collections/create-collections.md) .|  
|Správci nakonfigurují následující výstrahy pro kolekci: <br /><br />1) **zjištění malwaru**: Správci konfigurují Závažnost výstrahy na **kritickou**. <br /><br />2) **na několika počítačích se zjistil stejný typ malwaru**: Správci nakonfigurují Závažnost výstrahy na **kritickou** a určí, že se tato výstraha vygeneruje, když se malware zjistí na více než 5 procentech počítačů. <br /><br />3) v **zadaném intervalu počítače se opakovaně zjistil stejný typ malwaru**: Správci konfigurují Závažnost výstrahy na kritickou a určí, že se tato výstraha vygeneruje, když se malware během 24 hodin zjistí víc než pětkrát. <br /><br />4) **na stejném počítači v zadaném intervalu je nalezeno více typů malwaru**: Správci nakonfigurují Závažnost výstrahy na kritickou a určí, že se tato výstraha vygeneruje, když se ve 24hodinovém období vygeneruje více než 3 typy malwaru.<br /><br /> Hodnota **závažnosti výstrahy** určuje úroveň výstrahy, která se zobrazí v konzole Configuration Manager a v upozorněních, které obdrží v e-mailové zprávě.<br /><br /> Dále na **řídicím panelu Endpoint Protection vybrat možnost Zobrazit tuto kolekci** , aby mohli výstrahy monitorovat v konzole Configuration Manager.|Viz téma Konfigurace upozornění pro Endpoint Protection v tématu [configuring Endpoint Protection](endpoint-configure-alerts.md).|  
|Správci konfigurují Configuration Manager aktualizace softwaru pro stahování a nasazování aktualizací definic třikrát za den pomocí pravidla automatického nasazení.|Další informace najdete v části "použití Configuration Manager aktualizací softwaru pro doručení aktualizací definic" v tématu [použití Configuration Manager aktualizací softwaru k doručování aktualizací definic](endpoint-definitions-configmgr.md).|  
|Správci prozkoumají nastavení ve výchozích antimalwarových zásadách, která obsahují doporučené nastavení zabezpečení od Microsoftu. Aby počítače každý den provedly rychlou kontrolu, změní následující nastavení:<br /><br /> 1) **Spusťte každodenní rychlou kontrolu na klientských počítačích**: **Ano**.<br /><br /> 2) **čas denního naplánovaného rychlého prohledávání**: **9:00 dop**.<br /><br /> Správci si všimněte, že ve výchozím nastavení je jako zdroj aktualizace definic vybraná možnost **Aktualizace distribuované z Microsoft Update** . Tím se splní požadavek firmy, který počítače stahují definice z Microsoft Update, když nemůžou dostávat Configuration Manager aktualizace softwaru.|Přečtěte si téma [jak vytvořit a nasadit antimalwarové zásady pro Endpoint Protection](endpoint-antimalware-policies.md).|  
|Správci vytvoří kolekci, která obsahuje pouze servery Woodgrove Bank s názvem **Servery Woodgrove Bank**.|Informace [o vytváření kolekcí](../../core/clients/manage/collections/create-collections.md)|  
|Správci vytvoří vlastní antimalwarové zásady s názvem **zásady serveru Woodgrove Bank**. Přidávají jenom nastavení pro **naplánovaná prohledávání** a provedou následující změny:<br /><br /> **Typ prohledávání**:  **Úplné**<br /><br /> **Den prohledávání**:  **sobota**<br /><br /> **Čas prohledávání**: **1:00**<br /><br /> **Spustit denní rychlé prohledávání na klientských počítačích**:  **Ne**|Přečtěte si téma [jak vytvořit a nasadit antimalwarové zásady pro Endpoint Protection](endpoint-antimalware-policies.md).|  
|Správci nasadí vlastní antimalwarové zásady **zásad serveru Woodgrove Bank** do kolekce **Servery Woodgrove Bank** .|Další informace najdete v části nasazení antimalwarových zásad do klientských počítačů v tématu [Vytvoření a nasazení antimalwarových zásad pro Endpoint Protection](endpoint-antimalware-policies.md) článek.|  
|Správci vytvoří novou sadu vlastních nastavení klientských zařízení pro Endpoint Protection a názvy těchto **nastavení Endpoint Protection Woodgrove Bank**.<br /><br /> **Poznámka:** Pokud nechcete instalovat a povolit Endpoint Protection na všech klientech ve vaší hierarchii, ujistěte se, že možnosti **spravovat Endpoint Protection klienta v klientských počítačích** a **instalovat Endpoint Protection klienta v klientských počítačích** jsou ve výchozím nastavení klienta nakonfigurovány jako **ne** .|Další informace najdete v tématu [Konfigurace vlastních nastavení klienta pro Endpoint Protection](endpoint-protection-configure-client.md).|  
|Konfigurují následující nastavení pro Endpoint Protection:<br /><br /> **Spravovat Endpoint Protection klienta na klientských počítačích**: **Ano**<br /><br /> Toto nastavení a hodnota zajistí, že všichni existující Endpoint Protection klient, který je nainstalovaný, bude spravovaný pomocí Configuration Manager.<br /><br /> **Instalovat klienta Endpoint Protection na klientských počítačích**:  **Ano**</br></br>**Poznámka:** Od Configuration Manager 1802 zařízení s Windows 10 nemusí mít nainstalovaného agenta Endpoint Protection. Pokud je už na zařízeních s Windows 10 nainstalovaná, Configuration Manager se neodebere. Správci můžou odebrat agenta Endpoint Protection v zařízeních s Windows 10, na kterých běží aspoň verze klienta 1802.|Další informace najdete v tématu [Konfigurace vlastních nastavení klienta pro Endpoint Protection](endpoint-protection-configure-client.md).|  
|Správci nasadí nastavení klienta **Woodgrove Bank Endpoint Protection nastavení** klienta do **všech počítačů chráněných kolekcí Endpoint Protection** .|Informace najdete v tématu Konfigurace vlastních nastavení klienta pro Endpoint Protection v tématu [konfigurace Endpoint Protection v Configuration Manager](endpoint-antimalware-policies.md).|  
|Správci pomocí Průvodce vytvořením zásad brány Windows Firewall vytvoří zásadu tak, že nakonfiguruje následující nastavení pro profil domény:<br /><br /> 1) **Povolit bránu Windows Firewall**: **Ano**<br /><br /> odst<br />                    **Oznámit uživatelům blokování nového programu bránou Windows Firewall**: **Ano**|Informace najdete v tématu [Vytvoření a nasazení zásad brány Windows Firewall pro Endpoint Protection](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|Správci nasadí nové zásady brány firewall do kolekce **všechny počítače chráněné Endpoint Protection** , které vytvořili dříve.|Další informace najdete v části nasazení zásad brány Windows Firewall v tématu [Vytvoření a nasazení zásad brány Windows Firewall pro Endpoint Protection](create-windows-firewall-policies.md)|  
|Správci používají dostupné úlohy správy pro Endpoint Protection ke správě zásad brány Windows Firewall a antimalwaru, prověřování počítačů na vyžádání v případě potřeby, vynucení stažení nejnovějších definic do počítačů a určení všech dalších akcí, které se mají provést při zjištění malwaru.|Přečtěte si téma [Správa antimalwarových zásad a nastavení brány firewall pro Endpoint Protection](endpoint-antimalware-firewall.md)|  
|Správci používají následující metody k monitorování stavu Endpoint Protection a akcí, které jsou provedeny Endpoint Protection:<br /><br /> 1) pomocí uzlu **stav Endpoint Protection** pod položkou **zabezpečení** v pracovním prostoru **monitorování** .<br /><br /> 2) pomocí uzlu **Endpoint Protection** v pracovním prostoru **prostředky a kompatibilita** .<br /><br /> 3) pomocí integrovaných sestav Configuration Manager.|Viz [jak monitorovat Endpoint Protection](monitor-endpoint-protection.md)|  

 Správci nahlásí úspěšnou implementaci Endpoint Protection ke svému vedoucímu a potvrdí, že počítače v Woodgrove Bank jsou nyní chráněny před antimalwarem podle obchodních požadavků, které byly zadány. 

## <a name="next-steps"></a>Další kroky

Další informace najdete v tématu [konfigurace Endpoint Protection](endpoint-protection-configure.md)