---
title: Postup vytvoření profilů sítě Wi-Fi
titleSuffix: Configuration Manager
description: Naučte se používat profily sítě Wi-Fi v Configuration Manager k nasazení nastavení bezdrátové sítě uživatelům ve vaší organizaci.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21dffd1201b04846a9fffcdc7cc917465daa5905
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710766"
---
# <a name="create-wi-fi-profiles"></a>Vytváření profilů sítě Wi-Fi

*Platí pro: Configuration Manager (Current Branch)*

Pomocí profilů sítě Wi-Fi v Configuration Manager nasaďte nastavení bezdrátové sítě uživatelům ve vaší organizaci. Nasazením těchto nastavení usnadníte uživatelům připojení k Wi-Fi.  

Máte například síť Wi-Fi, ke které chcete povolit připojení všech přenosných počítačů se systémem Windows. Vytvořte profil sítě Wi-Fi obsahující nastavení potřebná pro připojení k bezdrátové síti. Pak nasaďte profil pro všechny uživatele, kteří mají přenosné počítače se systémem Windows ve vaší hierarchii. Uživatelé těchto zařízení uvidí vaši síť v seznamu bezdrátových sítí a můžou se snadno připojit k této síti.  

Profily sítě Wi-Fi můžete nakonfigurovat pro následující verze operačních systémů:

- Windows 8.1 32-bit nebo 64-bit

- Windows RT 8.1

- Windows 10 nebo Windows 10 Mobile

Můžete také použít Configuration Manager k nasazení nastavení bezdrátové sítě na mobilní zařízení pomocí místní správy mobilních zařízení (MDM). Obecnější informace najdete v tématu [co je místní](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)Správa mobilních zařízení (MDM).

Když vytváříte profil Wi-Fi, můžete zahrnout široký rozsah nastavení zabezpečení. Tato nastavení zahrnují certifikáty pro ověřování serveru a klienta, které byly vloženy pomocí Configuration Manager profily certifikátů. Další informace o profilech certifikátů najdete v tématu [profily certifikátů](introduction-to-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a>Vytvoření profilu sítě Wi-Fi

1. V konzole Configuration Manager přejděte do pracovního prostoru **prostředky a kompatibilita** , rozbalte položku **Nastavení dodržování předpisů**, rozbalte položku **přístup k prostředkům společnosti**a vyberte uzel **Profily sítě Wi-Fi** .

1. Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit profil sítě Wi-Fi**.

1. Na stránce **Obecné** v Průvodci vytvořením profilu sítě Wi-Fi zadejte následující informace:

    - **Název**: Zadejte jedinečný název pro identifikaci profilu v konzole nástroje.

    - **Popis**: Volitelně můžete přidat popis, který poskytne další informace pro profil sítě Wi-Fi.

    - **Importovat stávající položku profilu sítě Wi-Fi ze souboru**: tuto možnost vyberte, pokud chcete použít nastavení z jiného profilu sítě Wi-Fi. Když vyberete tuto možnost, zbývající stránky průvodce se zjednoduší na dvě stránky: **Importovat profil sítě Wi-Fi** a **podporované platformy**.

        > [!IMPORTANT]
        > Ujistěte se, že profil Wi-Fi, který importujete, obsahuje platný kód XML pro profil sítě Wi-Fi. Při importu souboru Configuration Manager neověřuje profil.

    - **Závažnost neshody pro sestavy**: vyberte jednu z následujících úrovní závažnosti, kterou zařízení hlásí, pokud vyhodnocuje profil sítě Wi-Fi, aby nebyl kompatibilní. Například pokud se instalace profilu nezdařila, nedodržuje předpisy.

        - **Žádné**: počítače, které nesplní toto pravidlo dodržování předpisů, nehlásí pro sestavy Configuration Manager žádné závažnost selhání.

        - **Informace**

        - **Upozornění**

        - **Kritická**

        - **Kritické s událostí**: počítače, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **kritické** . Zařízení také protokolují stav nedodržující předpisy jako událost systému Windows v protokolu událostí aplikace.

1. Na stránce **profil sítě Wi-Fi** v průvodci zadejte následující informace:

    - **Název sítě**: zadejte název, který budou zařízení zobrazovat jako název sítě.

        > [!IMPORTANT]
        > Configuration Manager nepodporuje použití apostrofů (`'`) nebo čárky (`,`) v názvu sítě.

    - **SSID**: Zadejte ID bezdrátové sítě citlivé na velká a malá písmena.

    - **Připojit automaticky, pokud je tato síť v dosahu**
    - **Vyhledat další bezdrátové sítě během připojení k této síti**
    - **Připojit, pokud síť nevysílá svůj název (SSID)**

1. Na stránce **Konfigurace zabezpečení** zadejte následující informace:

    > [!IMPORTANT]
    > Pokud vytváříte profil Wi-Fi pro místní správu mobilních [zařízení (MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)), aktuální větev Configuration Manager podporuje jenom tyto konfigurace zabezpečení Wi-Fi:  
    >
    > - Typy zabezpečení: **WPA2-podnikové** nebo **WPA2-osobní**  
    > - Typy šifrování: **AES** nebo **TKIP**  
    > - Typy protokolu EAP: **Čipová karta nebo jiný certifikát** nebo **PEAP**  

    - **Typ zabezpečení**: Vyberte protokol zabezpečení používaný bezdrátovou sítí, nebo vyberte **bez ověřování (otevřené)** , pokud síť není zabezpečená.

    - **Šifrování**: Pokud typ zabezpečení podporuje, nastavte metodu šifrování pro bezdrátovou síť.

    - **Typ protokolu EAP**: Vyberte protokol ověřování pro vybranou metodu šifrování.

        > [!NOTE]
        > Jenom pro zařízení Windows Phone: typy protokolu EAP **přestupní** a **EAP-FAST** se nepodporují.

        Vyberte **Konfigurovat** a zadejte vlastnosti pro vybraný typ protokolu EAP. Tato možnost není k dispozici pro některé vybrané typy protokolu EAP.

        > [!IMPORTANT]
        > Okno Konfigurace typu protokolu EAP je z Windows. Ujistěte se, že spouštíte konzolu Configuration Manager v počítači, který podporuje vybraný typ protokolu EAP.

    - **Pamatovat přihlašovací údaje uživatele při každém přihlašování**: tuto možnost vyberte, pokud chcete ukládat přihlašovací údaje uživatele, aby uživatelé nemuseli zadávat přihlašovací údaje k bezdrátové síti pokaždé, když se přihlásí k Windows.

1. Na stránce **Rozšířená nastavení** v průvodci zadejte další nastavení profilu sítě Wi-Fi. Rozšířená nastavení nemusí být k dispozici nebo se mohou lišit v závislosti na možnostech, které jste vybrali na stránce **Konfigurace zabezpečení** v průvodci. Například režim ověřování nebo možnosti jednotného přihlašování.

1. Pokud vaše bezdrátová síť používá proxy server, na stránce **nastavení proxy** vyberte možnost **Konfigurace nastavení proxy serveru pro tento profil sítě Wi-Fi**. Pak zadejte informace o konfiguraci proxy serveru.

1. Na stránce **podporované platformy** vyberte verze operačních systémů, ve kterých je tento profil sítě Wi-Fi použitelný.

1. Dokončete průvodce.

## <a name="next-step"></a>Další krok

> [!div class="nextstepaction"]
> [Postup nasazení profilů sítě Wi-Fi](deploy-wifi-vpn-email-cert-profiles.md)
