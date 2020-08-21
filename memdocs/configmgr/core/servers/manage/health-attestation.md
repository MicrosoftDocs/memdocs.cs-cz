---
title: Ověření stavu
titleSuffix: Configuration Manager
description: Přečtěte si informace o funkcích Ověření stavu zařízení zobrazit v konzole Configuration Manager.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d57be201274c347e5dcd492734b2141c64d579b
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700006"
---
# <a name="health-attestation-for-configuration-manager"></a>Ověření stavu pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Správci mohou zobrazit stav [Ověření stavu zařízení s Windows 10](/windows/security/threat-protection/protect-high-value-assets-by-controlling-the-health-of-windows-10-based-devices) v konzole nástroje Configuration Manager.  Ověření stavu zařízení umožňuje správcům zajistit, že klientské počítače mají následující důvěryhodné konfigurace systému BIOS, čipu TPM a spouštěcího softwaru:  

-   Antimalware s raným spuštěním – Antimalware s raným spuštěním (ELAM) chrání počítač při spuštění a před inicializací ovladačů jiných výrobců. [Zapnutí ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker – Windows BitLocker Drive Encryption je software, který umožňuje šifrování všech dat uložených na svazku operačního systému Windows.  [Zapnutí nástroje BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Zabezpečené spouštění – Zabezpečené spuštění je bezpečnostní standard vyvinutý členy počítačového průmyslu, který pomáhá zabezpečit, že váš počítač při spouštění použije pouze software, který je důvěryhodný pro výrobce počítačů. [Další informace o Zabezpečeném spouštění](/previous-versions/windows/it-pro/windows-8.1-and-8/hh824987(v=win.10))  
-   Integrita kódu – Integrita kódu je funkce, která zvyšuje zabezpečení operačního systému tím, že ověří integritu souboru ovladače nebo systémového souboru pokaždé, když je načten do paměti. [Další informace o Integritě kódu](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd348642(v=ws.10))  

Tato funkce je dostupná pro osobní počítače a místní prostředky spravované nástrojem Configuration Manager, a pro mobilní zařízení spravované pomocí Microsoft Intune. Správci mohou určit, zda má vytváření sestav probíhat přes cloudovou nebo místní infrastrukturu. Místní monitorování ověření stavu zařízení umožňuje správcům monitorovat klientské počítače bez přístupu k Internetu.

## <a name="enable-health-attestation"></a>Povolit ověření stavu

 **Požadavků**  

-   Klientská zařízení se systémem Windows 10 verze 1607 nebo Windows Server 2016 verze 1607 s [povoleným ověření stavu zařízení](/windows-server/security/device-health-attestation).
-   Zařízení s povoleným čipem TPM 1,2 nebo TPM 2
-   Pokud používáte správu cloudu, komunikace mezi Configuration Manager klientským agentem a bodem správy s *has.spserv.Microsoft.com* (port 443) služba ověření stavu (cloudová správa). Pokud je místní, klient musí být schopný komunikovat s bodem správy s povoleným ověřením stavu zařízení.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Postup povolení komunikace služby Ověření stavu na klientských počítačích nástroje Configuration Manager

Pomocí tohoto postupu můžete povolit monitorování ověření stavu zařízení pro zařízení, která se připojují k Internetu.

1.  V konzole Configuration Manager klikněte na **Správa**  >  **Přehled**  >  **nastavení klienta**.  Vyberte kartu s nastavením **Počítačový agent**.  
2.  V dialogovém okně **Výchozí nastavení** vyberte **Počítačový agent** a poté přejděte dolů na **Povolit komunikaci se službou ověření stavu**.  
3.  Nastavte hodnotu **Povolit komunikaci se službou Ověření stavu** na **Ano**, a poté klikněte na **OK**.  
4. Cílí na kolekce zařízení, která by měla hlásit stav zařízení.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Povolení komunikace služby Ověření stavu na klientských počítačích nástroje Configuration Manager
Pomocí tohoto postupu můžete povolit monitorování ověření stavu zařízení pro místní zařízení, která se nepřipojují k Internetu.

Od Configuration Manager 1702 se adresa URL místní služby ověření stavu zařízení dá nakonfigurovat v bodu správy tak, aby podporovala klientské zařízení bez přístupu k Internetu.

1. V konzole Configuration Manager přejděte na **Správa**  >  **Přehled**  >  **Konfigurace**  >  **lokality lokality**.
2. Klikněte pravým tlačítkem myši na primární nebo sekundární lokalitu s bodem správy, který podporuje místní klienty ověření stavu zařízení, a vyberte **Konfigurovat**  >  **bod správy**součástí lokality. Otevře se stránka **Vlastnosti komponenty bodu správy** .
3. Na kartě **Upřesnit možnosti** vyberte **Přidat** a zadejte platnou adresu URL místní služby ověření stavu zařízení. Můžete přidat několik adres URL. Pokud je zadáno více místních adres URL, klienti obdrží úplnou sadu a náhodně si zvolí, která z nich se má použít.
4.  V konzole Configuration Manager klikněte na **Správa**  >  **Přehled**  >  **nastavení klienta**.  Vyberte kartu s nastavením **Počítačový agent**.  
5.  Posuňte se dolů, aby **se aktivovala komunikace se službou ověření stavu**, a nastavte na **Ano**.
7.  Klikněte na možnost **použít místní službu Health Attestaion** a nastavte na **Ano**.
8. Zaměřte se na kolekce zařízení, která by měla nahlásit stav zařízení pomocí nastavení agenta klienta, aby se povolilo vytváření sestav ověření stavu zařízení.

Můžete taky **Upravit** nebo **Odebrat** adresy URL služby ověření stavu zařízení.

> [!NOTE]
> Pokud jste před upgradem na Configuration Manager 1702 používali ověření stavu zařízení, jsou místní adresy URL zadané v nastavení agenta klienta předem vyplněné ve vlastnostech bodu správy během upgradu. Místní klienti budou dál používat adresu URL zadanou v nastavení agenta klienta, dokud nebudou upgradováni. Pak budou přepínat na jednu z adres URL uvedených v bodu správy.

## <a name="monitor-device-health-attestation"></a>Monitorovat ověření stavu zařízení

1.  Chcete-li zobrazit zobrazení funkce Ověření stavu zařízení, v konzole nástroje Configuration Manager přejděte do pracovního prostoru **Monitorování** , klikněte na uzel **Zabezpečení** a poté klikněte na **Ověření stavu**.  
2.  Zobrazí se ověření stavu zařízení.  

Ověření stavu zařízení nástroje Configuration Manager zobrazí následující informace:  

-   **Stav ověření stavu** – Zobrazuje podíly zařízení, která jsou ve vyhovujícím, nevyhovujícím, chybovém a neznámém stavu.  
-   **Zařízení udávající ověření stavu** – Zobrazuje procentní podíl zařízení, která hlásí stav ověření stavu.  
-   **Nevyhovující zařízení podle typu klienta** – Zobrazuje podíl mobilních zařízení a počítačů, které nesplňují požadavky.  
-   **Nejčastější chybějící nastavení pro ověření stavu** – Zobrazuje počet zařízení, kterým chybí nastavení ověření stavu, v pořadí podle nastavení.