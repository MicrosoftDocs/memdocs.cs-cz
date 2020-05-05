---
title: Certifikáty a zabezpečení
titleSuffix: Configuration Manager
description: Správa certifikátů a zabezpečení pro System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5f441bc277f9c91cb1a83ce97879bd29b6349481
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718802"
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Správa certifikátů a zabezpečení pro aplikace Updates Publisher

*Platí pro: Configuration Manager (Current Branch)*

Následující postupy vám pomohou nakonfigurovat úložiště certifikátů na serveru aktualizací, nakonfigurovat certifikát pro podpis držitele v klientském počítači a nakonfigurovat Zásady skupiny, aby mohl agent web Windows Update na počítačích vyhledávat publikované aktualizace.

## <a name="configure-the-certificate-store-on-the-update-server"></a>Konfigurace úložiště certifikátů na serveru aktualizací
 Nástroj Updates Publisher používá digitální certifikát k podepsání aktualizací v katalozích, které publikuje. Předtím, než bude možné katalog publikovat na server aktualizací, musí být tento certifikát v úložišti certifikátů na serveru aktualizací a v úložišti certifikátů počítače nástroje Updates Publisher, pokud je tento počítač vzdálený od serveru aktualizací.

Následující postup je jedním z několika možných způsobů, jak přidat certifikát do úložiště certifikátů na serveru aktualizací.

### <a name="to-configure-the-certificate-store"></a>Konfigurace úložiště certifikátů
1.  V počítači, který má přístup k počítači se systémem Publisher i k serveru aktualizací, klikněte na tlačítko **Start**, klikněte na příkaz **Spustit**, do textového pole zadejte příkaz **MMC** a potom kliknutím na tlačítko **OK** otevřete konzolu MMC (Microsoft Management Console).

2.  Klikněte na **soubor**, klikněte na **Přidat nebo odebrat modul snap-in**, klikněte na **Přidat**, klikněte na **certifikáty**, klikněte na **Přidat**, vyberte **účet počítače**a pak klikněte na **Další**.

3.  Vyberte **jiný počítač**, zadejte název serveru aktualizací nebo klikněte na tlačítko **Procházet** a vyhledejte počítač se serverem aktualizací, klikněte na tlačítko **Dokončit**, klikněte na tlačítko **Zavřít**a pak klikněte na tlačítko **OK**.

4.  Rozbalte položku **certifikáty (*aktualizovat název serveru*)**, rozbalte položku **WSUS**a klikněte na položku **certifikáty**.

5.  V podokně výsledků klikněte pravým tlačítkem na požadovaný certifikát, klikněte na **všechny úlohy**a pak klikněte na **exportovat**.

6.  V Průvodci exportem certifikátu použijte výchozí nastavení a vytvořte soubor exportu s názvem a umístěním zadaným v průvodci. Než budete pokračovat k dalšímu kroku, musí být tento soubor dostupný pro server aktualizací.

7.  Klikněte pravým tlačítkem na **Důvěryhodní vydavatelé**, klikněte na **všechny úlohy**a pak klikněte na **importovat**. Dokončete Průvodce importem certifikátu pomocí exportovaného souboru z kroku 6.

8.  Pokud se používá certifikát podepsaný svým držitelem, například **podepsaný držitelem služby WSUS**, klikněte pravým tlačítkem na **Důvěryhodné kořenové certifikační autority**, klikněte na **všechny úlohy**a pak klikněte na **importovat**. Dokončete Průvodce importem certifikátu pomocí exportovaného souboru z kroku 6.

9.  Klikněte pravým tlačítkem na **certifikáty (*aktualizovat název serveru*)**, klikněte na **připojit k jinému počítači**, zadejte název počítače pro aplikaci Updates Publisher a klikněte na **OK**.

10. Pokud je aplikace Update Publisher od serveru aktualizací vzdálená, opakujte kroky 7 až 9, abyste importovali certifikát do úložiště certifikátů na počítači nástroje Updates Publisher.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>Konfigurace certifikátu automatického podepisování v klientských počítačích
V klientských počítačích bude agent web Windows Update (WUA) vyhledat aktualizace z katalogu. Tento proces se nedaří nainstalovat aktualizace, když Agent nemůže najít tento digitální certifikát v úložišti důvěryhodných vydavatelů v místním počítači. Pokud byl certifikát podepsaný svým držitelem použit k publikování katalogu aktualizací, jako je například **Služba WSUS vydavatelů podepsaný držitelem**, musí být certifikát také v úložišti certifikátů důvěryhodných kořenových certifikačních autorit v místním počítači, aby mohl agent ověřit platnost certifikátu.

Pro konfiguraci certifikátů v klientských počítačích můžete použít některou z několika metod, například pomocí Zásady skupiny a **Průvodce importem certifikátu** nebo pomocí nástroje Certutil a distribuce softwaru.

Níže je uveden příklad konfigurace podpisového certifikátu v klientských počítačích.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>Konfigurace certifikátu podepsaného svým držitelem v klientských počítačích
1. V počítači s přístupem k serveru aktualizací klikněte na tlačítko **Start**, klikněte na příkaz **Spustit**, do textového pole zadejte **MMC** a potom kliknutím na tlačítko **OK** otevřete konzolu MMC (Microsoft Management Console).

2. Klikněte na **soubor**, klikněte na **Přidat nebo odebrat modul snap-in**, klikněte na **Přidat**, klikněte na **certifikáty**, klikněte na **Přidat**, vyberte **účet počítače**a pak klikněte na **Další**.

3. Vyberte **jiný počítač**, zadejte název serveru aktualizací nebo klikněte na tlačítko **Procházet** a vyhledejte počítač se serverem aktualizací, klikněte na tlačítko **Dokončit**, klikněte na tlačítko **Zavřít**a pak klikněte na tlačítko **OK**.

4. Rozbalte položku **certifikáty (*aktualizovat název serveru*)**, rozbalte položku **WSUS**a klikněte na položku **certifikáty**.

5. V podokně výsledků klikněte pravým tlačítkem na certifikát, klikněte na **všechny úlohy**a pak klikněte na **exportovat**. Dokončete **Průvodce exportem certifikátu** pomocí výchozího nastavení a vytvořte soubor s exportem certifikátu s názvem a umístěním zadaným v průvodci.

6. Pomocí jedné z následujících metod přidejte certifikát použitý k podepsání katalogu aktualizací do každého klientského počítače, který bude používat agenta WUA ke kontrole aktualizací v katalogu. Přidejte certifikát do klientského počítače následujícím způsobem:

   -   Certifikáty podepsané svým držitelem: přidejte certifikát do úložišť certifikátů důvěryhodných **kořenových certifikačních autorit** a **důvěryhodných vydavatelů** .

   -   Certifikáty vydaných certifikační autoritou (CA): přidejte certifikát do úložiště certifikátů **důvěryhodných vydavatelů** .

   > [!NOTE]
   > Agent WUA také kontroluje, zda je povoleno nastavení **Povolit podepsaný obsah z umístění služby Microsoft Update v intranetu** zásady skupiny v místním počítači. Toto nastavení zásady musí být povoleno, aby mohl nástroj WUA skenovat aktualizace, které byly vytvořeny a publikovány pomocí nástroje Updates Publisher. Další informace o povolení tohoto nastavení Zásady skupiny najdete v tématu [jak nakonfigurovat zásady skupiny na klientských počítačích](https://docs.microsoft.com/previous-versions/bb530967(v=technet.10)).



## <a name="configuring-group-policy-to-allow-wuaon-computers-to-scan-for-published-updates"></a>Konfigurace Zásady skupiny, aby mohl Agent WUA na počítačích Hledat publikované aktualizace
Předtím, než agent web Windows Update (WUA) na počítačích vyhledá aktualizace, které byly vytvořeny a publikovány pomocí nástroje Updates Publisher, je nutné povolit nastavení zásad, aby byl podepsaný obsah z umístění intranetové služby Microsoft Update povolen. Když je povolené nastavení zásad, Agent WUA přijme aktualizace přijaté prostřednictvím umístění v intranetu, pokud jsou aktualizace podepsané v úložišti certifikátů **důvěryhodných vydavatelů** v místním počítači. Existuje několik způsobů konfigurace Zásady skupiny v počítačích v prostředí.

Pro počítače, které nejsou v doméně, se dá nakonfigurovat nastavení klíče registru, které umožňuje podepsaný obsah z umístění intranetové Microsoft Update služby.

Následující postupy obsahují základní kroky, které lze použít ke konfiguraci Zásady skupiny počítačů v doméně a hodnoty klíče registru v počítačích, které nejsou v doméně.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>Konfigurace Zásady skupiny, aby mohl Agent WUA vyhledat publikované aktualizace
1.  Otevřete modul snap-in Editor objektů zásad skupiny konzoly Microsoft Management Console (MMC) s uživatelem, který má příslušná oprávnění zabezpečení ke konfiguraci Zásady skupiny.

2.  Klikněte na **Procházet** a vyberte doménu, organizační jednotku nebo objekty zásad skupiny propojené s lokalitou, do které se nakonfigurované zásady skupiny rozšíří do požadovaných klientských počítačů. Klikněte na tlačítko **OK**, klikněte na tlačítko **Dokončit**, klikněte na tlačítko **Zavřít**a pak klikněte na tlačítko **OK**.

3.  Rozbalte nastavení vybrané zásady ve stromu konzoly, rozbalte položku **Konfigurace počítače**, rozbalte položku **šablony pro správu**, rozbalte položku **součásti systému Windows**a klikněte na možnost **web Windows Update**.

4.  V podokně výsledků klikněte pravým tlačítkem na **Povolit podepsaný obsah z umístění intranetové služby Microsoft Update**, klikněte na **vlastnosti**, klikněte na **povoleno**a pak klikněte na **OK**.
