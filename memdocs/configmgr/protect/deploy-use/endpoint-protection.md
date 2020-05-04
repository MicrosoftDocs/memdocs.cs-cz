---
title: Funkce Endpoint Protection
titleSuffix: Configuration Manager
description: Naučte se spravovat antimalwarové zásady a zabezpečení brány Windows Firewall pro klienty.
ms.date: 03/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b74a8c1daff31a8ffca8a38e6449aeeef1bb9b2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715645"
---
# <a name="endpoint-protection"></a>Funkce Endpoint Protection

*Platí pro: Configuration Manager (Current Branch)*

Endpoint Protection spravuje antimalwarové zásady a zabezpečení brány Windows Firewall pro klientské počítače ve vaší Configuration Manager hierarchii.  

> [!IMPORTANT]  
>  Abyste mohli spravovat klienty ve vaší Configuration Manager hierarchii, musíte mít licenci, aby používala Endpoint Protection.  

 Pokud používáte Endpoint Protection s Configuration Manager, máte následující výhody:  

-   Konfigurace antimalwarových zásad, nastavení brány Windows Firewall a Správa rozšířené ochrany před internetovými útoky v programu Microsoft Defender na vybrané skupiny počítačů  
-   Pomocí Configuration Manager aktualizace softwaru si stáhněte nejnovější soubory antimalwarových definic, aby byly klientské počítače pořád aktuální.  
-   Odesílat e-mailová oznámení, používat monitorování v konzole a zobrazovat sestavy. Tyto akce informují uživatele s právy pro správu při zjištění malwaru na klientských počítačích.  

Od počítačů s Windows 10 a Windows Server 2016 už je Windows Defender nainstalovaný. Pro tyto operační systémy se klient pro správu pro Windows Defender nainstaluje při instalaci klienta Configuration Manager. V Windows 8.1 a starších počítačích je klient Endpoint Protection nainstalován s Configuration Manager klientem. Windows Defender a klient Endpoint Protection mají tyto možnosti:  

-   Zjišťování a náprava malwaru a spywaru  
-   Zjišťování a náprava rootkitů  
-   Vyhodnocení kritických ohrožení zabezpečení a automatické aktualizace definic a stroje  
-   Zjišťování ohrožení zabezpečení sítě pomocí aplikace Systém kontroly sítě  
-   Integrace se službou Cloud Protection pro hlášení malwaru společnosti Microsoft. Když se připojíte k této službě, klient Endpoint Protection nebo Windows Defender stáhne nejnovější definice z centra ochrany před malwarem, když se v počítači zjistí neidentifikovaný malware.  

> [!NOTE]  
>  Klienta Endpoint Protection můžete nainstalovat na server se spuštěnou technologií Hyper-V a na hostované virtuální počítače s podporovanými operačními systémy. Aby se zabránilo nadměrnému využití procesoru, Endpoint Protection akce mají vestavěnou náhodnou prodlevu, aby se služby ochrany nespouštěly současně.  

 Kromě toho můžete pomocí Endpoint Protection v konzole Configuration Manager spravovat nastavení brány Windows Firewall.  

 [Příklad scénáře: použití System Center Endpoint Protection k ochraně počítačů před malwarem](scenarios-endpoint-protection.md) Endpoint Protection a brány Windows Firewall.  


## <a name="managing-malware-with-endpoint-protection"></a>Správa malwaru pomocí aplikace Endpoint Protection  
 Endpoint Protection v Configuration Manager umožňuje vytvářet antimalwarové zásady, které obsahují nastavení pro Endpoint Protection konfigurace klientů. Tyto antimalwarové zásady nasaďte do klientských počítačů. Pak Sledujte dodržování předpisů v uzlu **stav Endpoint Protection** v části **zabezpečení** v pracovním prostoru **monitorování** . V uzlu **vytváření sestav** také používejte Endpoint Protection sestavy.  

 Další informace:  

-   [Vytvoření a nasazení antimalwarových zásad pro Endpoint Protection](endpoint-antimalware-policies.md) – vytváření, nasazování a sledování antimalwarových zásad se seznamem nastavení, která můžete nakonfigurovat  

-   [Jak monitorovat](monitor-endpoint-protection.md) sestavy aktivit monitorování Endpoint Protection, nakažených klientských počítačů a další.  

-   [Správa antimalwarových zásad a nastavení brány firewall pro Endpoint Protection](endpoint-antimalware-firewall.md) napravení malwaru nalezeného v klientských počítačích  

-   [Soubory protokolu pro Endpoint Protection](../../core/plan-design/hierarchy/log-files.md#BKMK_EPLog)  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Správa brány Windows Firewall pomocí aplikace Endpoint Protection  
 Endpoint Protection v Configuration Manager poskytuje základní správu brány Windows Firewall v klientských počítačích. Pro každý profil sítě můžete nakonfigurovat tato nastavení:  

-   Povolení nebo zákaz brány Windows Firewall  

-   Blokování příchozích připojení včetně těch, která se nachází na seznamu povolených programů  

-   Upozornění uživateli, když brána Windows Firewall zablokuje nový program  

> [!NOTE]  
>  Aplikace Endpoint Protection podporuje jenom správu brány Windows Firewall.  


 Další informace najdete v tématu [Postup vytvoření a nasazení zásad brány Windows Firewall pro Endpoint Protection](create-windows-firewall-policies.md).  


## <a name="microsoft-defender-advanced-threat-protection"></a>Rozšířená ochrana před internetovými útoky v programu Microsoft Defender

Endpoint Protection spravuje a monitoruje program Microsoft Defender Advanced Threat Protection (ATP), dříve označovaný jako ochrana ATP v programu Windows Defender. Služba ATP v programu Microsoft Defender pomáhá podnikům zjišťovat, zkoumat a reagovat na pokročilé útoky v podnikové síti. Další informace najdete v tématu [Rozšířená ochrana před internetovými útoky v programu Microsoft Defender](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Pracovní postup aplikace Endpoint Protection  
 Následující diagram vám pomůže pochopit pracovní postup, který implementuje Endpoint Protection ve vaší Configuration Manager hierarchii.  

 ![Pracovní postup aplikace Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Klient aplikace Endpoint Protection pro počítače Mac a servery se systémem Linux  

> [!Important]  
> Podpora pro System Center Endpoint Protection (SCEP) pro Mac a Linux (všechny verze) končí 31. prosince 2018. Dostupnost nových definic virů pro SCEP pro Mac a SCEP pro Linux se může po skončení podpory přestat používat. Další informace najdete v [příspěvku blogu konec podpory](https://go.microsoft.com/fwlink/?linkid=870182).  

 System Center Endpoint Protection zahrnuje klienta Endpoint Protection pro Linux a počítače Mac. Tito klienti nejsou dodány s Configuration Manager. Stáhnout z [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx)následující produkty:  

-   System Center Endpoint Protection pro Mac  

-   System Center Endpoint Protection pro Linux  


> [!Note]  
>  Ke stažení instalačních souborů aplikace Endpoint Protection pro Linux a počítače Mac potřebujete multilicenci od Microsoftu.  

 Tyto produkty se nedají spravovat z konzoly Configuration Manager. K dispozici je System Center Operations Manager Management Pack s instalačními soubory, které vám umožní spravovat klienta nástroje pro Linux.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Jak získat klienta Endpoint Protection pro počítače Mac a servery se systémem Linux

Pomocí následujících kroků stáhněte soubor bitové kopie obsahující Endpoint Protection klientský software a dokumentaci pro počítače Mac a servery se systémem Linux.
1. Přihlaste se k [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. V horní části webu vyberte kartu **soubory ke stažení a klíče** .
3. Filtruje na produktovém **Endpoint Protection System Center (Current Branch)**.
4. Kliknutím na odkaz **si stáhněte**
5. Klikněte na **Pokračovat**. Mělo by se zobrazit několik souborů, včetně jednoho s názvem: **System Center Endpoint Protection (Current Branch verze 1606) pro operační systémy Linux a Mac OS multilanguage 32/64 bit 1878 MB ISO**.
6. Chcete-li stáhnout soubor, klikněte na ikonu šipky. Název souboru je **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050. ISO**.

Aktualizace z ledna 2018 (X21-67050) obsahuje následující verze:

- System Center Endpoint Protection pro Mac 4.5.32.0 (podpora macOS 10,13 High Sierra)
- System Center Endpoint Protection pro Linux 4.5.20.0 

  Další informace o tom, jak nainstalovat a spravovat klienty Endpoint Protection pro počítače se systémy Linux a Mac, najdete v dokumentaci, která doprovází tyto produkty. Tato dokumentace k produktu je ve složce **dokumentace** nástroje. Soubor ISO.
