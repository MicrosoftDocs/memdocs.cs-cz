---
title: Plánování nasazení klienta na zařízení se systémem Windows Embedded
titleSuffix: Configuration Manager
description: Naplánujte nasazení klientů na zařízení se systémem Windows Embedded v Configuration Manager.
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 623125ad64c7ed421ea209137eb68f17891d7a81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714014"
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-configuration-manager"></a>Plánování nasazení klientů na zařízení se systémem Windows Embedded v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<a name="BKMK_DeployClientEmbedded"></a>Pokud zařízení se systémem Windows Embedded neobsahuje klienta Configuration Manager, můžete použít libovolnou metodu instalace klienta, pokud zařízení splňuje požadované závislosti. Pokud integrované zařízení podporuje filtry zápisu, je nutné tyto filtry zakázat, než nainstalujete klienta, a pak filtry znovu povolit po instalaci a přiřazení klienta do lokality.  

 Pokud zakážete filtry, neměli byste zakázat ovladače filtrů. Obvykle se tyto ovladače spouštějí automaticky při spuštění počítače. Zakázání ovladačů buď zabrání instalaci klienta, nebo bude v konfliktu s orchestrací filtrů zápisu, což způsobí selhání operací klienta. Zde jsou uvedené služby přidružené jednotlivým typům filtrů zápisu, které musí zůstat spuštěné:  

|Typ filtru zápisu|Ovladač|Typ|Popis|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|Kernel|Implementuje přesměrování vstupu/výstupu na úrovni sektorů na chráněných svazcích.|  
|FBWF|FBWF|Systém souborů|Implementuje přesměrování vstupu/výstupu na úrovni souborů na chráněných svazcích.|  
|UWF|uwfreg|Kernel|Přesměrovač registru UWF|  
|UWF|uwfs|Systém souborů|Přesměrovač souborů UWF|  
|UWF|uwfvol|Kernel|Správce svazků UWF|  

 Filtry zápisu ovládají způsob, jakým se operační systém v integrovaném zařízení aktualizuje, když provádíte změny, například když instalujete software. Pokud jsou filtry zápisu povolené, místo provedení změn přímo v operačním systému se tyto změny přesměrují do dočasného překrytí. Pokud se změny zapíšou jenom do překrytí, ztratí se, když dojde k vypnutí integrovaného zařízení. Pokud jsou však filtry zápisu dočasně zakázané, budou provedené změny trvalé, takže je nebudete muset provádět znovu (nebo přeinstalovat software) pokaždé, když se integrované zařízení restartuje. Dočasné zakázání a pak znovu povolení filtrů zápisu však vyžaduje jeden nebo více restartů, takže obvykle budete chtít nastavit, kdy k této situaci dojde, pomocí oken konfigurace údržby, aby k restartu docházelo mimo pracovní hodiny.  

 Můžete provést konfiguraci možností a automaticky zakázat a znovu povolit filtry zápisu, když nasadíte software, například aplikace, pořadí úkolů, softwarové aktualizace a klienta aplikace Endpoint Protection. Výjimka platí pro standardní hodnoty konfigurace u položek konfigurace, které používají automatickou nápravu. V takové situaci k nápravě vždy dojde v překrytí, aby byla dostupná pouze do restartu zařízení. Náprava se použije znovu při dalším cyklu hodnocení, ale jenom do překrytí, které se při restartu vymaže. Chcete-li vynutit Configuration Manager potvrzení změn náprav, můžete nasadit standardní hodnoty konfigurace a potom jiné nasazení softwaru, které podporuje změnu v co nejkratší době.  

 Pokud jsou filtry zápisu zakázané, můžete nainstalovat software do integrovaných zařízení se systémem Windows pomocí centra softwaru. Pokud jsou však filtry zápisu povoleny, instalace se nezdařila a Configuration Manager zobrazí chybovou zprávu, že nemáte dostatečná oprávnění k instalaci aplikace.  

> [!WARNING]  
>  I když nevyberete možnost Configuration Manager možnosti pro potvrzení změn, může se stát, že se změny potvrdí, pokud se provede jiná instalace softwaru nebo změna, která provádí změny. V tomto scénáři se původní změny provedou navíc k novým změnám.  

 Když Configuration Manager zakáže filtry zápisu, aby se změny projevily, můžou se přihlásit a používat integrované zařízení jenom uživatelé, kteří mají místní oprávnění správce. Během této doby budou uživatelé s nízkým oprávněním uzamčení a uvidí zprávu, že počítač je nedostupný, protože probíhá údržba. Tato funkce pomáhá chránit zařízení, když se nachází ve stavu, kdy můžou být změny provedené trvale a toto chování uzamčení pomocí servisního režimu je dalším důvodem pro konfiguraci okna údržby v dobu, kdy se uživatelé do těchto zařízení nepřihlašují.  

 Configuration Manager podporuje správu následujících typů filtrů zápisu:  

- Souborový filtr zápisu (FBWF) – Další informace najdete v tématu [filtr zápisu na základě souborů](https://go.microsoft.com/fwlink/?LinkID=204717).  

- Vylepšený filtr zápisu (EWF) RAM – další informace najdete v tématu [vylepšený filtr zápisu](https://go.microsoft.com/fwlink/?LinkId=204718).  

- Sjednocený filtr zápisu (UWF) – Další informace najdete v tématu [Sjednocený filtr zápisu](https://go.microsoft.com/fwlink/?LinkId=309236).  

  Configuration Manager nepodporuje operace filtru zápisu, pokud je zařízení se systémem Windows Embedded v režimu Reg EWF RAM.  

> [!IMPORTANT]
>  Pokud máte možnost volby, použijte souborové filtry zápisu (FBWF) s Configuration Manager pro vyšší efektivitu a vyšší škálovatelnost.
> 
> **Pro zařízení, která používají jenom FBWF:** Nakonfigurujte následující výjimky, aby trvaly stav klienta a data inventáře mezi restarty zařízení:  
> 
> - CCMINSTALLDIR\\*. sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
>   Zařízení se systémem Windows Embedded 8.0 a novějším nepodporují vyloučení, která obsahují zástupné znaky. U těchto zařízení je nutné nakonfigurovat následující vyloučení jednotlivě:  
> 
> - Všechny soubory v adresáři CCMINSTALLDIR s příponou .sdf, obvykle:  
> 
>   -   UserAffinityStore.sdf  
>   -   InventoryStore.sdf  
>   -   CcmStore.sdf  
>   -   StateMessageStore.sdf  
>   -   CertEnrollmentStore.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
> **Pro zařízení, která používají jenom FBWF a UWF:** Když klienti v pracovní skupině používají certifikáty k ověřování na body správy, musíte také vyloučit privátní klíč, abyste zajistili, že klient bude nadále komunikovat s bodem správy. V těchto zařízeních nakonfigurujte následující výjimky:  
> 
> - c:\Windows\System32\Microsoft\Protect  
>   -   c:\ProgramData\Microsoft\Crypto  
>   -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

> [!NOTE]
> Klient Configuration Manager nepotřebuje žádné další výjimky, které jsou popsané v předchozím **důležitém** poli. Přidání dalších výjimek souvisejících s Configuration Manager nebo rozhraním WMI (WBEM) může vést k selhání Configuration Manager, včetně zařízení, která přestanou zablokovat v režimu obsluhy nebo zařízení, ve kterých probíhá restart smyček. Mezi nepotřebné výjimky patří Adresář klienta Configuration Manager, adresář CCMcache, adresář CCMSetup, adresář mezipaměti pořadí úloh, adresář WBEM a Configuration Manager související klíče registru.

 Ukázkový scénář pro nasazení a správu zařízení se systémem Windows Embedded s povolenými filtry zápisu v Configuration Manager najdete v části [ukázkový scénář pro nasazení a správu Configuration Manager klientů v zařízeních se systémem Windows Embedded](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md).  

 Další informace o tvorbě bitových kopií pro integrovaná zařízení se systémem Windows a konfiguraci filtrů zápisu najdete v dokumentaci Windows Embedded nebo se obraťte na vašeho OEM dodavatele.  

> [!NOTE]
>  Když vyberete platné platformy pro nasazení softwaru a položky konfigurace, zobrazí se v nich místo konkrétních verzí spíše rodiny Windows Embedded. Následující seznam použijte k mapování konkrétní verze rodiny Windows Embedded do možností v poli seznamu:  
> 
> - **Integrované operační systémy založené na systému Windows XP (32 bitů)** zahrnují následující položky:  
> 
>   -   Windows XP Embedded  
>   -   Windows Embedded for Point of Service  
>   -   Windows Embedded Standard 2009  
>   -   Windows Embedded POSReady 2009  
>   -   **Integrované operační systémy založené na systému Windows 7 (32 bitů)** zahrnují následující položky:  
> 
>   -   Windows Embedded Standard 7 (32 bitů)  
>   -   Windows Embedded POSReady 7 (32 bitů)  
>   -   Windows ThinPC  
>   -   **Integrované operační systémy založené na systému Windows 7 (64 bitů)** zahrnují následující položky:  
> 
>   -   Windows Embedded Standard 7 (64 bitů)  
>   -   Windows Embedded POSReady 7 (64 bitů)
