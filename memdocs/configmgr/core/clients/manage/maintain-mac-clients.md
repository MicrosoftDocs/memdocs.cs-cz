---
title: Údržba klientů Mac
titleSuffix: Configuration Manager
description: Úlohy údržby pro klienty Configuration Manager Mac.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 520315c4bb740f23a9534e532f75c3bd3ee66a2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710647"
---
# <a name="maintain-mac-clients"></a>Údržba klientů Mac
*Platí pro: Configuration Manager (Current Branch)*

Tady jsou postupy pro odinstalaci klientů se systémem Mac a obnovení certifikátů.

##  <a name="uninstalling-the-mac-client"></a> Uninstalling the Mac client  

1.  V počítači Mac otevřete okno terminálu a přejděte do složky, která obsahuje **Macclient. dmg**.  

2.  Přejděte do složky Nástroje a zadejte následující text do příkazového řádku:  

     `./CMUninstall -c`

    > [!NOTE]  
    >  Vlastnost **-c** vydá pokyn k odinstalaci klienta, aby také odebrala soubory protokolů o selhání klienta. Doporučujeme, abyste zabránili nejasnostem při pozdějším přeinstalaci klienta.  

3.  V případě potřeby ručně odeberte certifikát ověření klienta, který Configuration Manager používal, nebo ho Odvolejte. Nástroj CMUnistall tento certifikát neodebere ani nezablokuje.  

##  <a name="renewing-the-mac-client-certificate"></a>Obnovení certifikátu klienta pro systém Mac  
 Pokud chcete obnovit certifikát klienta pro systém Mac, použijte některou z následujících metod:  

-   [Průvodce obnovením certifikátu](#renew-certificate-wizard)  

-   [Ruční obnovení certifikátu](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Průvodce obnovením certifikátu  

1. Nakonfigurujte následující hodnoty jako *řetězce* v souboru ccmclient. plist, který řídí, kdy se otevře Průvodce obnovením certifikátu:  

   - **Hodnota RenewalPeriod1** – určuje první dobu obnovení v sekundách, během které můžou uživatelé certifikát obnovit. Aktuální hodnota je 3 888 000 sekund (45 dní). Nekonfigurujte hodnotu menší než 300, protože perioda se vrátí k výchozímu. 

   - **RenewalPeriod2** – určuje druhou dobu obnovení v sekundách, během které můžou uživatelé certifikát obnovit. Aktuální hodnota je 259 200 sekund (3 dny). Pokud je tato hodnota nakonfigurovaná a je větší nebo rovna 300 sekund a je menší nebo rovna hodnotě **hodnota RenewalPeriod1**, použije se hodnota. Pokud je hodnota **RenewalPeriod1** delší než 3 dny, použije se pro hodnotu **RenewalPeriod2**hodnota 3 dny.  Pokud je hodnota **RenewalPeriod1** kratší než 3 dny, pak se hodnota **RenewalPeriod2** nastaví na stejnou hodnotu jako hodnota **RenewalPeriod1**.  

   - **RenewalReminderInterval1** – určuje frekvenci, během které se Průvodce obnovením certifikátu zobrazí uživatelům během první doby obnovení. Aktuální hodnota je 86 400 sekund (1 den). Pokud je hodnota **RenewalReminderInterval1** větší nebo rovna 300 sekundám a menší než nakonfigurovaná hodnota **RenewalPeriod1**, použije se konfigurovaná hodnota. V opačném případě se použije výchozí hodnota 1 den.  

   - **Hodnota RenewalReminderInterval2** – Určuje četnost, s jakou se v sekundách zobrazí Průvodce obnovením certifikátu pro uživatele v průběhu druhé doby obnovení. Aktuální hodnota je 28 800 sekund (8 hodin). Pokud je hodnota **RenewalReminderInterval2** větší než 300 sekund, menší nebo rovna hodnotě **RenewalReminderInterval1** a menší nebo rovna hodnotě **RenewalPeriod2**, použije se konfigurovaná hodnota. V opačném případě se použije hodnota 8 hodin.  

     **Příklad** : Pokud jsou hodnoty ponechané jako výchozí, 45 dní před vypršením platnosti certifikátu se průvodce otevře každých 24 hodin.  V období 3 dní do vypršení platnosti certifikátu se průvodce otevře každých 8 hodin.  

     **Příklad:** K nastavení prvního období obnovení na 20 dní použijte následující příkazový řádek.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2. Po otevření Průvodce obnovením certifikátu budou pole **uživatelské jméno** a **název serveru** obvykle předem vyplněná a uživatel může pouze zadat heslo pro obnovení certifikátu.  

   > [!NOTE]  
   >  Pokud se průvodce neotevře nebo pokud náhodně průvodce uzavřete, klikněte na **Obnovit** na stránce předvoleb **Configuration Manager** a průvodce otevřete.  

###  <a name="renew-certificate-manually"></a>Ruční obnovení certifikátu  
 Typická doba platnosti certifikátu klienta se systémem Mac je 1 rok. Configuration Manager neobnoví automaticky certifikát uživatele, který požaduje při registraci, takže je nutné pomocí následujícího postupu obnovit certifikát ručně.  

> [!IMPORTANT]  
>  Pokud platnost certifikátu vyprší, je nutné odinstalovat, přeinstalovat a pak znova zapsat klienta pro systém Mac.  

 Tento postup odebere SMSID, které je nezbytné k vyžádání nového certifikátu pro stejný počítač Mac. Když odeberete a nahradíte SMSID klienta, odstraní se po odstranění klienta z konzoly Configuration Manager všechny uložené historie klienta, například inventář.  

1.  Vytvořte a naplňte kolekci zařízení pro počítače Mac, které musí obnovit certifikáty uživatelů.  

    > [!WARNING]  
    >  Configuration Manager nesleduje období platnosti certifikátu, který zapisuje pro počítače Mac. Je nutné monitorovat nezávisle na Configuration Manager k identifikaci počítačů Mac, které mají být přidány do této kolekce.  

2.  V pracovním prostoru **Prostředky a kompatibilita** spusťte **Průvodce vytvořením položky konfigurace**.  

3.  Na stránce **Obecné** určete následující informace:  

    -   **Název:Odeberte SMSID pro Mac**  

    -   **Typ:Mac OS X**  

4.  Na stránce **podporované platformy** zajistěte, aby byly vybrány všechny verze Mac OS X.  

5.  Na stránce **Nastavení** klikněte na možnost **Nový** a potom v dialogovém okně **vytvořit nastavení** zadejte následující informace:  

    -   **Název:Odeberte SMSID pro Mac**  

    -   **Typ nastavení:Skript**  

    -   **Datový typ:String**  

6.  V dialogovém okně **vytvořit nastavení** pro **skript zjišťování**zvolte možnost **Přidat skript** a zadejte skript, který zjistí počítače se systémem Mac s nakonfigurovaným SMSID.  

7.  Do dialogového okna **Úpravy skriptu zjišťování** zadejte následující skript prostředí:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Kliknutím na **tlačítko OK** zavřete dialogové okno **Úpravy skriptu zjišťování** .  

9. V dialogovém okně **vytvořit nastavení** pro skript napravení **(volitelné)** zvolte **Přidat skript** a určete skript, který odebere SMSID, když se najde v počítačích Mac.  

10. Do dialogového okna **Vytvoření skriptu napravení** zadejte následující skript prostředí:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Kliknutím na **tlačítko OK** zavřete dialogové okno **Vytvoření skriptu** napravení.  

12. Na stránce **Pravidla shody** průvodce klikněte na tlačítko **Nový**a pak do dialogového okna **Vytvořit pravidlo** zadejte následující údaje:  

    -   **Název:Odeberte SMSID pro Mac**  

    -   **Vybrané nastavení:** Zvolte **Procházet** a potom vyberte skript zjišťování, který jste zadali dříve.  

    -   Do **následujícího** pole zadejte **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Povolte možnost **Je-li toto nastavení neshodné, spusťte zadaný skript pro nápravu**.  

13. Dokončete průvodce vytvořením položky konfigurace.  

14. Vytvořte standardní hodnoty konfigurace obsahující položku konfigurace, kterou jste právě vytvořili, a nasaďte ji do kolekce zařízení, kterou jste vytvořili v kroku 1.  

     Další informace o vytváření a nasazování standardních hodnot konfigurace najdete v tématech [Vytvoření standardních hodnot konfigurace](../../../compliance/deploy-use/create-configuration-baselines.md) a [postup nasazení standardních hodnot konfigurace](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. V počítačích Mac, které mají odstraněné SMSID, spusťte následující příkaz a nainstalujte nový certifikát:  

    ``` Shell
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Po vyzvání zadejte heslo účtu superuživatele a spusťte příkaz a pak heslo pro uživatelský účet služby Active Directory.  

16. Pokud chcete omezit zaregistrovaný certifikát na Configuration Manager, otevřete na počítači Mac okno terminálu a proveďte následující změny:  

    a.  Zadejte příkaz.`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`

    b.  V dialogovém okně **přístup do řetězce klíčů** v **části řetězy** klíčů zvolte **systém**a pak v části **kategorie** zvolte **klíče**.  

    c.  Rozbalte klíče a zobrazte certifikáty klientů. Po identifikaci certifikátu obsahujícího právě nainstalovaný soukromý klíč na klíč dvakrát klikněte.  

    d.  Na kartě **Access Control** pro **Povolení přístupu vyberte potvrdit**.  

    e.  Přejděte na **/Library/Application Support Support/Microsoft/ccm**, vyberte **ccmclient**a pak zvolte **Přidat**.  

    f.  Vyberte **Uložit změny** a zavřete dialogové okno **přístup do řetězce klíčů** .  

17. Restartujte počítač Mac.  

