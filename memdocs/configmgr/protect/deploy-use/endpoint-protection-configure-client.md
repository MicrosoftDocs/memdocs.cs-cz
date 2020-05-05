---
title: Endpoint Protection nastavení klienta
titleSuffix: Configuration Manager
description: Přečtěte si, jak nakonfigurovat vlastní nastavení klienta pro Endpoint Protection.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25a1803d7a2feebe7947478c0671e0112830b0d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724318"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Konfigurace vlastních nastavení klienta pro bod Endpoint Protection

*Platí pro: Configuration Manager (Current Branch)*

Tento postup umožňuje nakonfigurovat vlastní nastavení klienta pro Endpoint Protection, které můžete nasadit do kolekcí zařízení ve vaší hierarchii.

> [!IMPORTANT]  
>  Výchozí Endpoint Protection nastavení klienta konfigurujte pouze v případě, že jste si jisti, že se mají použít pro všechny počítače ve vaší hierarchii. 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Postup povolení aplikace Endpoint Protection a konfigurace vlastního nastavení klienta

1. V konzole Configuration Manager klikněte na možnost **Správa**.  

2. V pracovním prostoru **Správa** klikněte na **Nastavení klienta**.  

3. Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit vlastní nastavení klientského zařízení**.  

4. V dialogu **Vytvořit vlastní nastavení klientského zařízení** zadejte název a popis skupiny nastavení a potom vyberte **Endpoint Protection**.  

5. Nakonfigurujte Endpoint Protection nastavení klienta, které požadujete. Úplný seznam Endpoint Protection nastavení klienta, která můžete konfigurovat, najdete v části Endpoint Protection v tématu [informace o nastavení klienta](../../core/clients/deploy/about-client-settings.md#endpoint-protection).  

   > [!IMPORTANT]  
   >  Než nakonfigurujete nastavení klienta pro Endpoint Protection, nainstalujte roli systému lokality Endpoint Protection.  

6. Kliknutím na tlačítko **OK** zavřete dialog **Vytvořit vlastní nastavení klientského zařízení** . Nové nastavení klienta se zobrazí v uzlu **Nastavení klienta** v pracovním prostoru **Správa** .  

7. Dále nasaďte vlastní nastavení klienta do kolekce. Vyberte vlastní nastavení klienta, které chcete nasadit. Na kartě **Domů** ve skupině **nastavení klienta** klikněte na **nasadit**.  

8. V dialogu **Vybrat kolekci** vyberte kolekci, do které chcete nasadit nastavení klienta, a klikněte na **OK**. Nová nasazení se zobrazí na kartě **Nasazení** v podokně podrobností.  

Klienti se při příštím stažení zásad klienta nakonfigurují pomocí těchto nastavení. Další informace najdete v tématu [spuštění načtení zásad pro klienta Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>Postup zřízení klienta Endpoint Protection v imagi disku

Nainstalujte klienta Endpoint Protection do počítače, který máte v úmyslu použít jako zdroj bitové kopie disku pro nasazení Configuration Managerho operačního systému. Tento počítač se obvykle nazývá referenční počítač. Po vytvoření image operačního systému použijte k nasazení image Configuration Manager nasazení operačního systému.

> [!Important]  
> Windows 10 a Windows Server 2016 mají ve výchozím nastavení nainstalován program Windows Defender. Tento postup nebudete potřebovat v těchto verzích Windows.  

Následující postupy vám pomůžou nainstalovat a nakonfigurovat klienta Endpoint Protection v referenčním počítači.


### <a name="prerequisites"></a>Požadavky

Následující seznam obsahuje požadované předpoklady pro instalaci Endpoint Protection klientského softwaru do referenčního počítače.

- Musíte mít přístup k instalačnímu balíčku klienta Endpoint Protection **scepinstall. exe**. Vyhledá tento balíček ve složce **klienta** instalační složky nástroje Configuration Manager na serveru lokality.  

- Pokud chcete nasadit klienta Endpoint Protection s požadovanou konfigurací vaší organizace, vytvořte a exportujte Antimalwarové zásady. Pak tuto zásadu zadejte při ruční instalaci klienta Endpoint Protection. Další informace najdete v tématu [Vytvoření a nasazení antimalwarových zásad](endpoint-antimalware-policies.md).  

  > [!NOTE]  
  >  Nemůžete exportovat **výchozí antimalwarové zásady klienta**.  

- Pokud chcete nainstalovat klienta Endpoint Protection s nejnovějšími definicemi, Stáhněte si je z části [Security Intelligence v programu Windows Defender](https://www.microsoft.com/wdsi).  

> [!NOTE]  
> Od Configuration Manager 1802 není nutné instalovat agenta Endpoint Protection (SCEPInstall) na zařízeních s Windows 10. Pokud je už na zařízeních s Windows 10 nainstalovaná, Configuration Manager neodebere. Správci můžou odebrat agenta Endpoint Protection v zařízeních s Windows 10, na kterých běží aspoň verze klienta 1802. SCEPInstall. exe může být v C:\Windows\ccmsetup na některých počítačích stále přítomen, ale nové instalace klientů by si ho neměli stáhnout. <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>Jak nainstalovat klienta Endpoint Protection do referenčního počítače

Nainstalujte klienta Endpoint Protection v místním počítači do referenčního počítače z příkazového řádku. Nejprve Získejte instalační soubor **scepinstall. exe**. Další informace najdete v tématu [instalace klienta Endpoint Protection z příkazového řádku](#bkmk_manual-install).

V případě potřeby také zahrňte předem nakonfigurované antimalwarové zásady nebo antimalwarové zásady, které jste předtím exportovali. 



## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a><a name="bkmk_manual-install"></a>Instalace klienta Endpoint Protection z příkazového řádku

1. Zkopírujte **scepinstall. exe** ze složky **klienta** instalační složky Configuration Manager do počítače, do kterého chcete nainstalovat Endpoint Protection klientský software.  

2. Otevřete příkazový řádek jako správce. Změňte adresář na složku pomocí instalačního programu. Pak spusťte `scepinstall.exe`a přidejte všechny další požadované vlastnosti příkazového řádku:


   |  Vlastnost   |                                  Popis                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Spustit instalační program v tichém režimu                           |
   |    `/q`     |                        Tiché extrahování instalačních souborů                        |
   |    `/i`     |                           Spustit instalační program normálně                           |
   |  `/policy`  | Zadání souboru antimalwarové zásady pro konfiguraci klienta během instalace |
   | `/sqmoptin` |     Přihlášení k Microsoft program Zlepšování softwaru a služeb na základě zkušeností uživatelůu (CEIP)     |


3. Dokončete instalaci klienta podle pokynů na obrazovce.  

4. Pokud jste stáhli nejnovější balíček aktualizace definic, zkopírujte balíček do klientského počítače a poté dvakrát klikněte na balíček definic, čímž jej nainstalujete.  

   > [!NOTE]  
   >  Po dokončení instalace klienta Endpoint Protection klient automaticky provede kontrolu aktualizace definice. Pokud je tato aktualizace úspěšná, není nutné ručně instalovat nejnovější balíček aktualizace definic.  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>Příklad: instalace klienta s antimalwarovou zásadou

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>Ověření instalace klienta Endpoint Protection

Po instalaci klienta Endpoint Protection do referenčního počítače ověřte, zda klient pracuje správně.

1.  V referenčním počítači otevřete v oznamovací oblasti systému Windows **System Center Endpoint Protection** .  

2.  Na kartě **Domů** v dialogovém okně **System Center Endpoint Protection** ověřte, že je **ochrana v reálném čase** nastavená na **zapnuto**.  

3.  Ověřte, jestli se pro **definice virů a spywaru**zobrazuje **aktuální stav** .  

4.  Chcete-li zkontrolovat, zda je referenční počítač připraven na vytvoření bitové kopie, vyberte v části **Možnosti kontroly**možnost **úplné**a pak klikněte na tlačítko **Zkontrolovat nyní**.  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>Příprava Endpoint Protection klienta na vytvoření bitové kopie

Proveďte následující kroky a připravte klienta Endpoint Protection pro vytváření imagí:

1. V referenčním počítači se přihlaste jako správce.  

2. Stáhněte si a nainstalujte **PsExec** ze [systému Windows Sysinternals](https://docs.microsoft.com/sysinternals/downloads/psexec).  

3. Spusťte příkazový řádek jako správce, změňte adresář na složku, do které jste nainstalovali nástroj PsTools, a potom zadejte následující příkaz:  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Pomocí tohoto způsobu spusťte Editor registru opatrně. PsExec. exe ho spustí v kontextu LocalSystem.  

4. V editoru registru odstraňte následující klíče registru:  

   > [!IMPORTANT]  
   >  Odstraňte tyto klíče registru jako poslední krok před vytvořením bitové kopie v referenčním počítači. Klient Endpoint Protection po spuštění znovu vytvoří tyto klíče. Pokud restartujete referenční počítač, odstraňte klíče registru znovu.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

Nyní jste připraveni připravit referenční počítač na vytvoření bitové kopie.

Když nasadíte bitovou kopii operačního systému, která obsahuje klienta Endpoint Protection, automaticky nahlásí informace do přiřazené lokality Configuration Manager zařízení. Klient stáhne a použije všechny cílené antimalwarové zásady.  



## <a name="see-also"></a>Viz také

Další informace o nasazení operačního systému v Configuration Manager najdete v tématu [Správa imagí operačního systému](../../osd/get-started/manage-operating-system-images.md).

