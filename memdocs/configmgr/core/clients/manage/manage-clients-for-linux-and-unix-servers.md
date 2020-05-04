---
title: Správa klientů se systémy Linux a UNIX
titleSuffix: Configuration Manager
description: Správa klientů na serverech se systémy Linux a UNIX v Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 716441bd146e9172b3f183c497fcaa4036ad0084
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710640"
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Správa klientů pro servery se systémy Linux a UNIX v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

> [!Important]  
> Počínaje verzí 1902 Configuration Manager nepodporuje klienty se systémy Linux a UNIX. 
> 
> Zvažte Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.

Když spravujete servery se systémy Linux a UNIX pomocí Configuration Manager, můžete nakonfigurovat kolekce, časová období údržby a nastavení klienta, která vám pomůžou se správou serverů. I když klient Configuration Manager pro systémy Linux a UNIX nemá uživatelské rozhraní, můžete vynutit ruční dotazování klienta na zásady klienta.

##  <a name="collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 Kolekce se používají ke správě skupin serverů se systémy Linux a UNIX stejným způsobem jako při správě jiných typů klientů. Kolekce můžou mít přímé kolekce členství nebo kolekce založené na dotazech. Kolekce založené na dotazech identifikují klientské operační systémy, hardwarové konfigurace nebo další podrobnosti o klientovi, které jsou uložené v databázi lokality. Můžete například použít kolekce, které obsahují servery se systémy Linux a UNIX, ke správě následujících nastavení:  

- Nastavení klienta  

- Nasazení softwaru  

- Vynucení časových období údržby  

  Než budete moct identifikovat klienta Linux nebo UNIX podle jeho operačního systému nebo distribuce, musíte z klienta shromáždit [inventář hardwaru](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) .  

  Výchozí nastavení klienta pro inventář hardwaru obsahují informace o operačním systému klientského počítače. K identifikaci operačního systému serveru se systémem Linux nebo UNIX můžete použít vlastnost **Caption** třídy **Operační systém** .  

  Podrobnosti o počítačích, na kterých běží klient Configuration Manager pro systémy Linux a UNIX, najdete v uzlu **zařízení** v pracovním prostoru prostředky **a kompatibilita** v konzole Configuration Manager. V pracovním prostoru prostředky **a kompatibilita** konzoly Configuration Manager můžete zobrazit název operačního systému každého počítače ve sloupci **operační systém** .  

  Ve výchozím nastavení jsou servery Linux a UNIX členy kolekce **Všechny systémy** . Doporučujeme vytvořit vlastní kolekce, které zahrnují pouze servery se systémy Linux a UNIX nebo jejich podmnožinu. Vlastní kolekce umožňují spravovat operace, jako je například nasazení softwaru nebo přiřazení nastavení klienta, skupinám podobných počítačů, abyste mohli přesně měřit úspěšnost nasazení.   

  Při vytváření vlastní kolekce pro servery se systémy Linux a UNIX použijte dotazy na pravidlo členství, které zahrnují atribut Caption atributu operačního systému. Informace o vytváření kolekcí najdete v tématu [vytváření kolekcí](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 Klient Configuration Manager pro servery se systémy Linux a UNIX podporuje použití [časových období údržby](../../../core/clients/manage/collections/use-maintenance-windows.md). Tato podpora se nemění od klientů se systémem Windows.  

##  <a name="client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 [Nastavení klienta](../../../core/clients/deploy/configure-client-settings.md) , která se vztahují na servery se systémy Linux a UNIX, můžete nakonfigurovat stejným způsobem jako nastavení pro ostatní klienty.  

 Ve výchozím nastavení platí **Výchozí nastavení klientského agenta** i pro servery se systémy Linux a UNIX. Můžete také vytvořit vlastní nastavení klienta a nasadit je do kolekcí konkrétních klientů.  

 Neexistují žádná další klientská nastavení, která by se vztahovala jenom na klienty se systémy Linux a UNIX. Existují však výchozí nastavení klienta, která se nevztahují na klienty se systémy Linux a UNIX. Klient pro systémy Linux a UNIX používá nastavení jenom pro funkce, které podporuje.  

 Například vlastní nastavení klientského zařízení, které umožňuje a konfiguruje nastavení vzdáleného řízení, budou servery se systémy Linux a UNIX ignorovat, protože klient pro systémy Linux a UNIX nepodporuje vzdálené řízení.  

##  <a name="computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a>Zásady počítače pro servery se systémy Linux a UNIX  
 Klient pro servery se systémy Linux a UNIX se pravidelně dotazuje svého webu na zásady počítače, aby se dozvěděl o požadovaných konfiguracích a kontroloval nasazení.  

 Klienta na serveru se systémem Linux nebo UNIX můžete také vyzvat k okamžitému dotázání na zásady počítače. Pokud to chcete provést, použijte přihlašovací údaje uživatele **root** na serveru a spusťte následující příkaz: **/opt/microsoft/configmgr/bin/ccmexec-RS Policy** .  

 Podrobnosti o dotazování zásad počítače budou uložené do sdíleného souboru protokolu klienta, **scxcm.log**.  

> [!NOTE]  
>  Klient Configuration Manager pro systémy Linux a UNIX nikdy nepožaduje ani nezpracovává zásady uživatele.  

##  <a name="how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a>Správa certifikátů v klientovi pro systémy Linux a UNIX  
 Po instalaci klienta pro Linux a UNIX, můžete použít nástroj **certutil** k aktualizaci klienta pomocí nového certifikátu PKI a k importování nového seznamu odvolaných certifikátů (CRL). Když instalujete klienta pro Linux a UNIX, tento nástroj je umístěný v `/opt/microsoft/configmgr/bin/certutil`. 

 Správu certifikátů provedete spuštěním příkazu certutil v každém klientském počítači s jedním z následujících parametrů:  

|Možnost|Další informace|  
|------------|----------------------|  
|`importPFX`|Tuto možnost použijte k určení certifikátu, který má nahradit certifikát, který právě klient používá.<br /><br /> Když použijete `-importPFX`, musíte použít také parametr `-password` příkazového řádku k zadání hesla přidruženého k souboru PKCS # 12.<br /><br /> Použijte `-rootcerts` k určení jakýchkoli dalších požadavků na kořenový certifikát.<br /><br /> Příklad: `certutil -importPFX <path to the PKCS#12 certificate> -password <certificate password> [-rootcerts <comma-separated list of certificates>]`|  
|`importsitecert`|Tuto možnost použijte k aktualizaci podpisového certifikátu serveru lokality, který je na serveru pro správu.<br /><br /> Příklad: `certutil -importsitecert <path to the DER certificate>`|  
|`importcrl`|Tato možnost aktualizuje seznam odvolaných certifikátů (CRL) na straně klienta podle jednoho nebo několika souborů se seznamem CRL.<br /><br /> Příklad: `certutil -importcrl <comma separated CRL file paths>`|  
