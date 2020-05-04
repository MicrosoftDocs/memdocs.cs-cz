---
title: Vzdálená správa počítače se systémem Windows
titleSuffix: Configuration Manager
description: Správa vzdáleného klientského počítače se systémem Windows pomocí Configuration Manager.
ms.date: 11/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801654b95470889d0b661315d40d3e00efa8e542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715106"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-configuration-manager"></a>Vzdálená správa klientského počítače se systémem Windows pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)* Configuration Manager umožňuje připojit se k klientským počítačům pomocí **Configuration Managerho vzdáleného řízení**. Než začnete používat vzdálené řízení, zkontrolujte informace v následujících článcích:  

-   [Předpoklady pro vzdálené řízení](prerequisites-for-remote-control.md)  

-   [Konfigurace vzdáleného řízení](configuring-remote-control.md)  

Tady jsou tři způsoby, jak spustit prohlížeč vzdáleného řízení:  

-   V konzole Configuration Manager.  

-   V příkazovém řádku systému Windows.  

-   V nabídce **Start** systému Windows v počítači, na kterém je spuštěna konzola Configuration Manager, ve skupině programu **Microsoft System Center** .  

## <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Pokud chcete vzdáleně spravovat klientský počítač z konzoly nástroje Configuration Manager  

1.  V konzole Configuration Manager vyberte prostředky a**zařízení** **dodržování předpisů** > nebo **kolekce zařízení**.  

3.  Vyberte počítač, který chcete vzdáleně spravovat, a pak na kartě **Domů** ve skupině **zařízení** zvolte **Spustit** > **vzdálené řízení**.  

    > [!IMPORTANT]  
    >  Pokud má nastavení klienta **Zobrazit výzvu uživateli pro oprávnění ke Vzdálenému řízení** hodnotu **Pravda**, připojení se nespustí, dokud uživatel na vzdáleném počítači vzdálené řízení nepotvrdí. Další informace najdete v tématu [Konfigurace vzdáleného řízení](configuring-remote-control.md).  

4.  Po otevření okna **Vzdálené řízení nástroje Configuration Manager** můžete klientský počítač vzdáleně spravovat. Pomocí následujících možností nakonfiguruje připojení:  

    > [!NOTE]  
    >  Pokud má počítač, ke kterému se připojujete, více monitorů, zobrazí se v okně vzdálené řízení zobrazení ze všech monitorů.  

    -   **Soubor**
        - **Připojit** -připojit se k jinému počítači. Tato možnost není dostupná, když je aktivní relace vzdáleného řízení.  
        -   **Odpojit** – odpojí aktivní relaci vzdáleného řízení, ale nezavře okno **Configuration Manager vzdáleného řízení** .  
        - **Exit** – odpojí aktivní relaci vzdáleného řízení a zavře okno **Configuration Manager vzdáleného řízení** .  

        > [!NOTE]  
        >  Pokud odpojíte relaci vzdáleného řízení, vymaže se obsah schránky systému Windows v počítači, ke kterému jste byli připojeni.


    - **Zobrazit**
      - **Barevná hloubka** – vyberte buď 16 bitů, nebo 32 bitů na pixel.
      -  **Celá obrazovka** – maximalizuje okno **Configuration Manager vzdáleného řízení** . Režim celé obrazovky ukončíte stisknutím Ctrl+Alt+Break.  
      - **Optimalizovat pro připojení s malou šířkou pásma** – tuto možnost vyberte, pokud má připojení malou šířku pásma.
      - **Otevřete**
        - **Všechny obrazovky** – přidáno v Configuration Manager 1902. Pokud má počítač, ke kterému se připojujete, více monitorů, zobrazí se v okně vzdálené řízení zobrazení ze všech monitorů. **Všechny obrazovky** jsou jediným zobrazením pro počítače s více monitory před 1902.
        -  **První obrazovka** – přidala se do Configuration Manager 1902. *První obrazovka* je nahoře a úplně vlevo, jak je znázorněno v nastavení zobrazení systému Windows. Nemůžete vybrat konkrétní obrazovku. Když přepnete konfiguraci prohlížeče, znovu připojte vzdálenou relaci. Prohlížeč uloží předvolby pro budoucí připojení.
        -  **Škálovat tak, aby odpovídaly** velikosti zobrazení vzdáleného počítače tak, aby se vešlo do **Configuration Manager okna vzdáleného řízení** .
        - **Stavový řádek** – Přepíná zobrazení Configuration Manager stavového řádku okna **vzdáleného řízení** .  

       > [!NOTE]  
       >  Prohlížeč uloží předvolby pro budoucí připojení.

    -   **Akce**
        - **Poslat klávesu Ctrl + Alt + Del** – odešle kombinaci kláves CTRL + ALT + DEL na vzdálený počítač. 
        - **Povolit sdílení schránky** – umožňuje kopírovat a vkládat položky do a ze vzdáleného počítače. Pokud toto nastavení změníte, bude třeba restartovat relaci vzdáleného řízení, aby se změna projevila.   
          - Pokud nechcete, aby sdílení schránky bylo povolené v konzole Configuration Manager, v počítači, na kterém je spuštěna konzola nástroje, nastavte hodnotu klíče registru **HKEY_CURRENT_USER \Software\microsoft\configmgr10\remote sdílení Control\Clipboard** na hodnotu **0**.
        - **Povolit překlad klávesnice** – přeloží rozložení klávesnice počítače, na kterém je spuštěná konzola, na rozložení připojeného zařízení.
        - **Zamknout vzdálenou klávesnici a myš** – uzamkne vzdálenou klávesnici a myš, aby se zabránilo uživateli v provozu na vzdáleném počítači.  

    -   **Nápověda**
        - **O vzdáleném řízení** – zobrazí aktuální verzi prohlížeče.  

5.  Uživatelé ve vzdáleném počítači mohou zobrazit další informace o relaci vzdáleného řízení při kliknutí na ikonu Configuration Manager **vzdáleného řízení** . Ikona se nachází v oznamovací oblasti systému Windows nebo v ikoně na panelu relace vzdáleného řízení.  

## <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Spuštění prohlížeče vzdáleného řízení z příkazového řádku Windows.  

-   Do příkazového řádku Windows zadejte _<Configuration Manager instalační\>složka_**\AdminConsole\Bin\i386\CmRcViewer.exe**  

CmRcViewer.exe podporuje následující možnosti příkazového řádku:  

- *Adresa* – Určuje název rozhraní NetBIOS, plně kvalifikovaný název domény (FQDN) nebo IP adresu klientského počítače, ke kterému se chcete připojit.
- *Název serveru lokality* – Určuje název serveru Configuration Manager lokality, na který chcete odesílat stavové zprávy související s relací vzdáleného řízení.
- **/?** – Zobrazí možnosti příkazového řádku pro prohlížeč vzdáleného řízení.  
     
**Příklad: CmRcViewer. exe** *<address\> * * < \\\Site název serveru>* 

> [!NOTE]  
> Prohlížeč vzdáleného řízení je podporován ve všech operačních systémech podporovaných konzolou Configuration Manager. Další informace najdete v tématu [podporované konfigurace pro Configuration Manager konzolu](../../../plan-design/configs/supported-operating-systems-consoles.md) a [požadavky pro vzdálené řízení](prerequisites-for-remote-control.md).

## <a name="next-steps"></a>Další kroky

[Auditovat využití vzdáleného řízení](audit-remote-control-usage.md)
