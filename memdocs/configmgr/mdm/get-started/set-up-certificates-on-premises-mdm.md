---
title: Certifikáty pro místní MDM
titleSuffix: Configuration Manager
description: Nastavte certifikáty pro důvěryhodnou komunikaci s místní správou mobilních zařízení (MDM) v Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc63a21970bb522407c86d027690b83894b3cb99
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721826"
---
# <a name="set-up-certificates-for-trusted-communications-with-on-premises-mdm"></a>Nastavení certifikátů pro důvěryhodnou komunikaci s místní MDM

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager místní správy mobilních zařízení (MDM) vyžaduje, abyste nakonfigurovali role systému lokality pro důvěryhodnou komunikaci se spravovanými zařízeními. Potřebujete dva typy certifikátů:

- **Certifikát webového serveru** ve službě IIS na serverech, které jsou hostiteli požadovaných rolí systému lokality. Pokud jeden Server hostuje více rolí systému lokality, budete pro tento server potřebovat jenom jeden certifikát. Pokud je každá role na samostatném serveru, každý server potřebuje samostatný certifikát.

- **Důvěryhodný kořenový certifikát** certifikační autority (CA), která vydává certifikáty webového serveru. Tento kořenový certifikát nainstalujte na všechna zařízení, která se potřebují připojit k rolím systému lokality.

Pro zařízení připojená k doméně, pokud používáte službu AD CS (Active Directory Certificate Services), může tyto certifikáty automaticky nainstalovat na všechna zařízení. U zařízení, která nejsou připojená k doméně, nainstalujte důvěryhodný kořenový certifikát jiným způsobem.

Pro hromadně registrovaná zařízení můžete zahrnout certifikát do registračního balíčku. Do zařízení zaregistrovaných uživatelem budete muset certifikát přenést prostřednictvím e-mailu, stažením z webu nebo jiným způsobem.

Pokud k vydání certifikátů serveru použijete známou veřejnou certifikační autoritu, jako je například VeriSign nebo GoDaddy, můžete nemusíte na každé zařízení ručně nainstalovat důvěryhodný kořenový certifikát. Většina zařízení nativně tyto veřejné autority důvěřuje. Tato metoda je užitečnou alternativou pro uživatelem zaregistrovaná zařízení, místo abyste museli instalovat certifikát jiným způsobem.

> [!IMPORTANT]  
> Existuje mnoho způsobů, jak nastavit certifikáty pro důvěryhodnou komunikaci mezi zařízeními a servery systému lokality pro místní správu mobilních zařízení (MDM). Informace v tomto článku jsou příkladem jednoho ze způsobů, jak to provést. Tato metoda vyžaduje službu AD CS (Active Directory Certificate Services) s certifikační autoritou a rolí webového zápisu certifikační autority. Další informace najdete v tématu Služba [AD CS (Active Directory Certificate Services](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740\(v=ws.11\))).

## <a name="publish-the-crl"></a><a name="bkmk_configCa"></a>Publikování seznamu odvolaných certifikátů

Ve výchozím nastavení používá certifikační autorita (CA) služby Active Directory seznamy odvolaných certifikátů (CRL) založené na protokolu LDAP. Umožňuje připojení k seznamu CRL pro zařízení připojená k doméně. Pokud chcete zařízením, která nejsou připojená k doméně, důvěřovat certifikátům vydaným certifikační autoritou, přidejte seznam CRL založený na protokolu HTTP.

1. Na serveru, na kterém je spuštěná certifikační autorita pro vaši lokalitu, přejděte do nabídky **Start** , vyberte **Nástroje pro správu**a vyberte **certifikační autorita**.

1. V konzole Certifikační autorita klikněte pravým tlačítkem na **CertificateAuthority**a pak vyberte **vlastnosti**.

1. V části vlastnosti CertificateAuthority přepněte na kartu **rozšíření** . Ujistěte se, že je **možnost vybrat rozšíření** nastavena na **distribuční bod seznamu CRL (CDP)**.

1. Vyberte `http://<ServerDNSName>/CertEnroll/<CAName><CRLNameSuffix><DeltaCRLAllowed>.crl`. Pak vyberte následující možnosti:

    - **Zahrnout do seznamů CRL. klienti toto používají k vyhledání umístění rozdílových seznamů CRL.**

    - **Zahrnout do rozšíření CDP vydaných certifikátů.**

    - **Zahrnout do rozšíření IDP vydaných seznamů CRL.**

1. Přepněte na kartu **ukončovací modul** . Vyberte **vlastnosti**a pak vyberte možnost **Povolení publikování certifikátů do systému souborů**. Zobrazí se upozornění k restartování služby AD CS (Active Directory Certificate Services).

1. Klikněte pravým tlačítkem na **odvolané certifikáty**, vyberte **všechny úlohy**a pak zvolte **publikovat**.

1. V okně publikovat seznam odvolaných certifikátů vyberte **jenom rozdílový seznam CRL**a pak kliknutím na **OK** zavřete okno.

## <a name="create-the-certificate-template"></a><a name="bkmk_certTempl"></a>Vytvoření šablony certifikátu

Certifikační autorita používá šablonu certifikátu webového serveru k vystavování certifikátů pro servery hostující role systému lokality. Tyto servery budou koncovými body SSL pro důvěryhodnou komunikaci mezi rolemi systému lokality a registrovanými zařízeními.

1. Vytvořte skupinu zabezpečení domény s názvem **servery CONFIGMGR MDM**. Do skupiny přidejte účty počítačů serverů systému lokality.

1. V konzole Certifikační autorita klikněte pravým tlačítkem na **šablony certifikátů**a vyberte **Spravovat**. Tato akce načte konzolu šablony certifikátů.

1. V podokně výsledků klikněte pravým tlačítkem myši na položku, která zobrazuje **webový server** ve sloupci **Zobrazovaný název šablony** , a pak vyberte možnost **Duplikovat šablonu**.

1. V okně **Duplikovat šablonu** vyberte **Windows 2003 Server, Enterprise edition** nebo **Windows 2008 Server, Enterprise Edition**a pak vyberte **OK**.

    > [!TIP]
    > Configuration Manager podporuje šablony certifikátů Windows 2008 serveru, označované také jako V3 nebo kryptografie: Next Generation (CNG) certifikáty. Další informace najdete v tématu [Přehled certifikátů CNG](../../core/plan-design/network/cng-certificates-overview.md).

    Pokud vaše certifikační autorita běží na Windows Serveru 2012 nebo novějším, v tomto okně se nezobrazí možnost verze šablony certifikátu. Po duplikaci šablony vyberte verzi na kartě **Kompatibilita** ve vlastnostech šablony.

1. V okně **Vlastnosti nové šablony** na kartě **Obecné** zadejte název šablony. Certifikační autorita používá tento název k vygenerování webových certifikátů, které se budou používat v Configuration Manager systémech lokality. Zadejte například **webový server CONFIGMGR MDM**.

1. Přepněte na kartu **název subjektu** a vyberte **sestavovat z informací služby Active Directory**. Jako formát názvu subjektu zadejte **název DNS**. Pokud je vybraná možnost **hlavní název uživatele (UPN)** , zakažte možnost pro alternativní název subjektu.

1. Přepněte na kartu **zabezpečení** .

    1. Odeberte oprávnění **zapsat** ze skupin zabezpečení **Domain Admins** a **Enterprise Admins** .

    1. Vyberte **Přidat**a zadejte název skupiny zabezpečení. Například **servery CONFIGMGR MDM**. Kliknutím na **tlačítko OK** zavřete okno.

    1. Vyberte oprávnění **zapsat** pro tuto skupinu. Neodstraňujte oprávnění **číst** .

1. Výběrem **OK** uložte změny a zavřete konzolu šablony certifikátů.

1. V konzole Certifikační autorita klikněte pravým tlačítkem na **šablony certifikátů**, vyberte **Nový**a pak vyberte **Vystavovaná šablona certifikátu**.

1. V okně **Povolit šablony certifikátů** vyberte novou šablonu. Například **webový server CONFIGMGR MDM**. Pak kliknutím na **OK** okno uložte a zavřete.

## <a name="request-the-certificate"></a><a name="bkmk_requestCert"></a>Požádat o certifikát

Tento postup popisuje, jak požádat o certifikát webového serveru pro službu IIS. Tento postup proveďte pro každý server systému lokality, který je hostitelem jedné z rolí pro místní správu mobilních zařízení (MDM).

1. Na serveru systému lokality, který je hostitelem jedné z rolí, otevřete příkazový řádek jako správce. Zadáním `mmc` otevřete prázdnou konzolu Microsoft Management Console.

1. V okně konzoly přejděte do nabídky **soubor** a vyberte **Přidat nebo odebrat modul snap-in**.

    1. V seznamu dostupných modulů snap-in vyberte **certifikáty** a vyberte **Přidat**.

    1. V okně modulu snap-in certifikáty vyberte možnost **účet počítače**. Vyberte **Další**a potom vyberte **Dokončit** pro správu místního počítače.

    1. Výběrem **OK** zavřete okno Přidat nebo odebrat modul snap-in.

1. Rozbalte položku **certifikáty (místní počítač)** a vyberte **osobní** úložiště. Přejděte do nabídky **Akce** , vyberte **všechny úlohy**a zvolte **požádat o nový certifikát**. Tato akce komunikuje se službou AD CS (Active Directory Certificate Services) a vytvoří nový certifikát pomocí šablony, kterou jste předtím vytvořili.

    1. V Průvodci zápisem certifikátu klikněte na stránce než začnete na tlačítko **Další**.

    1. Na stránce vybrat zásady zápisu certifikátů vyberte možnost **Zásady zápisu služby Active Directory**a pak vyberte **Další**.

    1. Vyberte šablonu certifikátu webového serveru (**webový server CONFIGMGR MDM**) a pak vyberte **zapsat**.

    1. Po podání žádosti o certifikát vyberte **Dokončit**.

Každý server potřebuje jedinečný certifikát webového serveru. Tento postup opakujte pro každý server, který je hostitelem jedné z požadovaných rolí systému lokality. Pokud jeden server hostuje všechny role systému lokality, stačí si vyžádat jen jeden certifikát webového serveru.

## <a name="bind-the-certificate"></a><a name="bkmk_bindCert"></a>Vytvoření vazby certifikátu

Dalším krokem je vytvoření vazby nového certifikátu na webový server. Tento postup použijte pro každý server, který je hostitelem rolí systému lokality *bodu registrace* a *zprostředkujícího bodu registrace* . Pokud jeden Server hostuje všechny role systému lokality, stačí tento proces provést pouze jednou.

> [!NOTE]
> Tento proces není nutné provádět pro role systému lokality distribučního bodu a bodu správy. Automaticky obdrží požadovaný certifikát při registraci.

1. Na serveru, který je hostitelem bodu registrace nebo zprostředkujícího bodu registrace, přejděte do nabídky **Start** , vyberte **Nástroje pro správu**a zvolte **Správce služby IIS**.

1. V seznamu připojení vyberte **výchozí web**a pak vyberte **Upravit vazby**.

    1. V okně vazby webu vyberte **https**a pak vyberte **Upravit**.

    1. V okně Upravit vazbu webu vyberte nově zaregistrovaný certifikát pro **certifikát SSL**. Kliknutím na **tlačítko OK** uložte a pak vyberte **Zavřít**.

1. V konzole Správce služby IIS vyberte v seznamu připojení webový server. Na panelu akcí na pravé straně vyberte **restartovat**. Tato akce restartuje službu webového serveru.

## <a name="export-the-trusted-root-certificate"></a><a name="bkmk_exportCert"></a>Export důvěryhodného kořenového certifikátu

Služba AD CS (Active Directory Certificate Services) automaticky nainstaluje požadovaný certifikát z certifikační autority na všechna zařízení připojená k doméně. Chcete-li získat certifikát, který je vyžadován pro zařízení, která nejsou připojena k doméně, ke komunikaci s rolemi systému lokality, exportujte jej z certifikátu vázaného na webový server.

1. Ve Správci služby IIS vyberte **výchozí web**. Na panelu akcí na pravé straně vyberte **vazby**.

1. V okně vazby webu vyberte **https**a pak vyberte **Upravit**.

1. Vyberte certifikát webového serveru a vyberte **Zobrazit**.

1. V okně Vlastnosti certifikátu webového serveru přepněte na kartu cesta k **certifikátu** . Vyberte kořen cesty certifikátu a vyberte **Zobrazit certifikát**.

1. Ve vlastnostech kořenového certifikátu přepněte na kartu **Podrobnosti** a pak vyberte **Kopírovat do souboru**.

1. V Průvodci exportem certifikátu na úvodní stránce vyberte **Další**.

1. Vyberte **binární soubor kódovaný v kódování der X. 509 (. CER)** jako formát a vyberte **Další**.

1. Zadejte cestu a název souboru pro identifikaci důvěryhodného kořenového certifikátu. V poli název souboru klikněte na **Procházet...**, zvolte umístění, kam chcete soubor certifikátu uložit, zadejte název souboru a vyberte **Další**.

1. Zkontrolujte nastavení a výběrem možnosti **Dokončit** exportujte certifikát do souboru.

V závislosti na návrhu certifikační autority možná budete muset exportovat další kořenové certifikáty podřízené certifikační autority. Opakujte tento postup pro export dalších certifikátů v cestě k certifikátu webového serveru.

## <a name="next-step"></a>Další krok

> [!div class="nextstepaction"]
> [Nastavení registrace zařízení](set-up-device-enrollment-on-premises-mdm.md)
