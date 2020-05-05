---
title: Možnosti ve verzi Technical Preview 1606
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1606.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 05e7bbe6373ed91de5a2bb8e99a8425e733274f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721616"
---
# <a name="capabilities-in-technical-preview-1606-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1606 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1606. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview.      Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    

**Známé problémy v této verzi Technical Preview:**  
*  Když aktualizujete z verze Technical Preview 1604 na 1605 a pak na verzi 1606, může aktualizace selhat a v **protokolu CMUpdate. log**se zaznamená chyba podobná této:

    ``` Log
    ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END
    ```

    Pokud k tomu dojde, v uzlu **aktualizace a údržba** klikněte na **Vyhledat aktualizace**a pak zkuste instalaci aktualizace **zopakovat** .
    ***

**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

## <a name="automatically-categorize-devices-into-collections"></a><a name="dmp_category"></a>Automatické kategorizace zařízení do kolekcí
Můžete vytvořit kategorie zařízení, které se dají použít k automatickému umístění zařízení do kolekcí zařízení, když používáte Configuration Manager s Microsoft Intune. Uživatelé pak při registraci zařízení v Intune potřebují zvolit kategorii zařízení. Kategorii zařízení můžete také změnit z konzoly Configuration Manager.

**Důležité informace:** Tato funkce funguje s vydáním Microsoft Intune od **června 2016** . Než si vyzkoušíte tyto postupy, ujistěte se, že jste tuto verzi aktualizovali.

### <a name="try-it-out"></a>Určitě to udělejte!

### <a name="create-a-set-of-device-categories"></a>Vytvoření sady kategorií zařízení
1.  V pracovním prostoru **prostředky a kompatibilita** konzoly Configuration Manager rozbalte **Přehled**a pak klikněte na **kolekce zařízení**.
2.  Na kartě **Domů** ve skupině **kategorie** klikněte na možnost **spravovat kategorie zařízení**.
3.  V dialogovém okně **spravovat kategorie zařízení** můžete kategorie vytvářet, upravovat nebo odebírat. Zkuste vytvořit novou kategorii.

### <a name="associate-a-collection-with-a-device-category"></a>Přidružení kolekce ke kategorii zařízení
Když přidružíte kolekci ke kategorii zařízení, všechna zařízení v kategorii, kterou zadáte, se do této kolekce přidají.
1.  V dialogovém okně **vlastnosti** pro kolekci zařízení klikněte na **Přidat** > pravidlo**kategorie zařízení**.
2.  V dialogovém okně **vytvořit pravidlo členství v kategorii zařízení** vyberte kategorii, která bude použita pro všechna zařízení v kolekci.
3.  Zavřete dialogové okno **vytvořit pravidlo členství kategorie zařízení** a dialogové okno Vlastnosti kolekce.

### <a name="change-the-category-of-a-device"></a>Změna kategorie zařízení
1.  V pracovním prostoru **prostředky a kompatibilita** konzoly Configuration Manager rozbalte **Přehled**a pak klikněte na **zařízení**.
2.  V seznamu **zařízení** vyberte zařízení a pak na kartě **Domů** ve skupině **zařízení** klikněte na **změnit kategorii**.
3.  V dialogovém okně **Upravit kategorii zařízení** zvolte kategorii, kterou chcete použít pro toto zařízení, a pak klikněte na **OK**.

## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a><a name="dmp_grace"></a>Poskytnutá lhůta vynucení pro požadovaná nasazení aplikací a aktualizací softwaru

V některých případech můžete chtít dát uživatelům více času na instalaci požadovaných nasazení aplikace nebo aktualizací softwaru nad rámec všech nakonfigurovaných termínů. To se obvykle vyžaduje v případě, že počítač byl po delší dobu vypnutý a potřebuje nainstalovat velký počet nasazení aplikace nebo aktualizace.
Například pokud se koncový uživatel vrátil jenom z dovolené, může se stát, že budou muset počkat delší dobu, než se nainstalují opožděná nasazení aplikací.
Chcete-li tento problém vyřešit, můžete nyní definovat dobu odkladu vynucení nasazením Configuration Manager nastavení klienta do kolekce.

### <a name="try-it-out"></a>Určitě to udělejte!

Pokud chcete nastavit dobu odkladu, proveďte následující akce:

1.  Na stránce **Počítačový agent** v nastavení klienta nakonfigurujte **po konečném termínu nasazení (hodiny) novou dobu odkladu** vlastnosti na hodnotu **1** až **120** hodin.
2.  V novém požadovaném nasazení aplikace nebo ve vlastnostech stávajícího nasazení na stránce **plánování** zaškrtněte políčko **zpoždění vynucení tohoto nasazení podle uživatelských předvoleb**, až do období odkladu definovaného v nastavení klienta.
Všechna nasazení, u nichž je toto políčko zaškrtnuté a které jsou zaměřená na zařízení, na která jste nasadili nastavení klienta, bude používat dobu odkladu vynucení.

Pokud nakonfigurujete dobu odkladu vynucení a zaškrtnutím políčka po dosažení konečného termínu instalace aplikace nasadíte do prvního nefiremního okna, které uživatel nakonfigurovali do této lhůty odkladu. Uživatel ale přesto může otevřít Centrum softwaru a nainstalovat aplikaci kdykoli. Jakmile vyprší lhůta odkladu, vynucení se vrátí do normálního chování pro zpožděná nasazení.
Podobné možnosti byly přidány do Průvodce nasazením aktualizací softwaru, Průvodce pravidly automatického nasazení a stránky vlastností.

##  <a name="using-configuration-manager-as-a-managed-installer-with-device-guard"></a><a name="dmp_devg"></a>Použití Configuration Manager jako spravovaného instalačního programu s ochranou zařízení

Device Guard je funkce Windows 10, která využívá hardwarovou a softwarovou funkci k striktnímu řízení toho, co je možné na zařízení spouštět.

Můžete si přečíst podrobný přehled toho, co dělá Ochrana zařízení a jak funguje v [tomto článku na TechNetu](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview).

V této verzi může Configuration Manager spolupracovat s ochranou zařízení a nástrojem [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) , aby spustitelné soubory a soubory DLL nasazené s Configuration Manager byly automaticky důvěryhodné, protože pocházejí ze spravovaného instalačního programu, což znamená, že budou moci běžet na cílovém zařízení a jiný software nebude možné spustit, pokud není explicitně povoleno spouštět pomocí jiných pravidel nástroje AppLocker.  

V současné době se tato možnost nedá konfigurovat z konzoly Configuration Manager. Chcete-li nakonfigurovat zásady, je nutné nakonfigurovat klíč registru v každém klientovi a nakonfigurovat služby systému Windows v klientovi.
Až to uděláte, nakonfigurujte soubor zásad AppLockeru. Když nakonfigurujete soubor zásad, můžete ho nasadit do libovolného kompatibilního klientského zařízení.


Stejně jako všechny zásady nástroje AppLocker můžou zásady s pravidly spravovaného instalačního programu běžet ve dvou režimech:

- Režim auditování – aplikace se nedají spouštět, ale všechny aplikace, které by byly blokované, se nahlásí v souboru protokolu (Tato operace bude podporovaná v pozdější verzi Configuration Manager).
- Vynucení povoleno – aplikace se zablokují jako spuštěné.

Další informace o používání ochrany zařízení pomocí Configuration Manager najdete na [blogu Enterprise mobility and Security blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10).

Další čtení:

- [Úvod do zařízení Guard](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Certifikace a dodržování předpisů zařízení](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [Průvodce nasazením zařízení Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

  ##  <a name="multiple-device-management-points-for-on-premises-mobile-device-management"></a><a name="dmp_onprem"></a>Více bodů správy zařízení pro místní správu mobilních zařízení  
  V\-rámci Technical Preview 1606 podporuje místní správa mobilních zařízení ve Windows 10 pro registraci nových verzí novou funkci, která automaticky konfiguruje zaregistrované zařízení, aby bylo možné používat více než jeden bod správy zařízení. Tato možnost umožňuje zařízení přejít na jiný bod správy zařízení, když normální použití není dostupné. Tato možnost funguje jenom pro počítače s nainstalovanou aktualizací Windows 10 pro výročí.  

### <a name="try-it-out"></a>Určitě to udělejte!  

1.  Nainstalujte ve vaší hierarchii více než jeden bod správy zařízení.  

2.  Zaregistrujte zařízení aktualizace pro Windows 10 pro\-místní správu mobilních zařízení.  

Informace o tom, jak připravit lokalitu a registrovat zařízení pro\-místní správu mobilních zařízení, najdete v tématu [Správa mobilních zařízení s místní infrastrukturou](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud-proxy-service-for-managing-clients-on-the-internet"></a><a name="cloud_proxy"></a>Cloudová proxy služba pro správu klientů na internetu

Cloudová proxy služba poskytuje jednoduchý způsob správy Configuration Manager klientů na internetu. Služba, která je nasazená do Microsoft Azure a vyžaduje předplatné Azure, se připojí k místní infrastruktuře Configuration Manager pomocí nové role, která se nazývá bod cloudového proxy konektoru. Po úplném nasazení a konfiguraci budou mít klienti přístup k místním Configuration Manager rolím systému lokality bez ohledu na to, jestli jsou připojené k interní privátní síti nebo na internetu.

K nasazení služby do Azure použijete konzolu Configuration Manager, přidáte roli bodu cloudového proxy konektoru a nakonfigurujete role systému lokality tak, aby umožňovaly přenos cloudového proxy serveru. Cloudová proxy služba aktuálně podporuje jenom role bodu správy, distribučního bodu a bodu aktualizace softwaru.

Certifikáty klienta a certifikáty SSL (Secure Socket Layer) se vyžadují k ověřování počítačů a k šifrování komunikace mezi různými vrstvami služby. Klientské počítače obvykle přijímají klientský certifikát prostřednictvím vynucení zásad skupiny. K šifrování provozu mezi klienty a serverem systému lokality, který je hostitelem rolí, je nutné vytvořit vlastní certifikát SSL z certifikační autority. Kromě těchto dvou typů certifikátů potřebujete také nastavit certifikát pro správu v Azure, který umožňuje Configuration Manager nasadit cloudovou proxy službu.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Požadavky na cloudovou proxy službu v TRANSAKČNÍm programu 1606
- Klientské počítače a server systému lokality, kde je spuštěný bod cloudového proxy konektoru.
- Vlastní certifikáty SSL z interní certifikační autority – slouží k šifrování komunikace z klientských počítačů a k ověření identity cloudové proxy služby.
- Předplatné Azure pro Cloud Services.
- Certifikát správy Azure – používá se k ověřování Configuration Manager s Azure.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Omezení cloudové proxy služby v TRANSAKČNÍm systému 1606

- Podporuje pouze role bodu správy, distribučního bodu a bodu aktualizace softwaru.
- Zásady uživatele nejsou podporovány.
- Nelze použít s [místní správou mobilních zařízení](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) v Configuration Manager.
- Podporuje se jenom na veřejné cloudové platformě Azure.


### <a name="try-it-out"></a>Určitě to udělejte!

Proces nasazení cloudové proxy služby zahrnuje následující kroky:

1. Vytvořte a vydejte vlastní certifikát SSL pro cloudovou proxy službu.
1. Exportujte kořenový adresář klientského certifikátu.
2. Nahrajte certifikát pro správu do Azure.
3. V konzole Configuration Manager nastavte cloudovou proxy službu.
4. Nakonfigurujte primární lokalitu tak, aby používala ověřování klientským certifikátem.
5. Přidejte bod cloudového proxy konektoru do svého webu.
6. Nakonfigurujte role systému lokality pro příjem přenosů cloudového proxy serveru.

Následující části obsahují další informace o provedení těchto kroků.

#### <a name="create-a-custom-ssl-certificate"></a>Vytvoření vlastního certifikátu SSL

Vlastní certifikát SSL pro cloudovou proxy službu můžete vytvořit stejným způsobem jako u cloudového distribučního bodu. Postupujte podle pokynů pro [Nasazení certifikátu služby pro cloudové distribuční body](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) , ale proveďte následující akce:

* Při nastavování nové šablony certifikátu udělte oprávnění **ke čtení** a **zápisu** do skupiny zabezpečení, kterou jste nastavili pro Configuration Manager servery.

#### <a name="export-the-client-certificates-root"></a>Exportovat kořen certifikátu klienta

Nejjednodušší způsob, jak získat export kořenového adresáře klientských certifikátů, které se používají v síti, je otevřít klientský certifikát na jednom z počítačů připojených k doméně, které mají jednu a kopírovat.

>[!NOTE]
>Klientské certifikáty jsou vyžadovány na jakémkoli počítači, který chcete spravovat pomocí cloudové proxy služby, a na serveru systému lokality, který je hostitelem bodu cloudového proxy konektoru. Pokud potřebujete přidat klientský certifikát do některého z těchto počítačů, přečtěte si téma [Nasazení certifikátu klienta pro počítače se systémem Windows](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).

1. V okně Spustit zadejte **MMC** a stiskněte vrátit.
2. V nabídce soubor v konzole pro správu klikněte na tlačítko **Přidat nebo odebrat modul snap-in**....
3. V dialogovém okně Přidat nebo odebrat moduly snap-in klikněte na **certifikáty**, klikněte **na Přidat >**, **účet počítače**, **Další**, **místní počítač**a pak klikněte na **Dokončit**. Kliknutím na **OK** zavřete dialogové okno.
4. Přejít na **certifikáty > osobním certifikátem >**.
5. Dvakrát klikněte na certifikát pro ověřování klientů v počítači, klikněte na kartu cesta k certifikátu a dvakrát klikněte na kořenovou autoritu (v horní části cesty).
6.  Klikněte na kartu Podrobnosti a pak klikněte na **Kopírovat do souboru...**.
7. Dokončete Průvodce exportem certifikátu s použitím výchozího formátu certifikátu. Poznamenejte si název a umístění kořenového certifikátu, který vytvoříte. Budete ho potřebovat ke konfiguraci cloudové proxy služby v pozdějším kroku.

#### <a name="upload-the-management-certificate-to-azure"></a>Nahrajte certifikát pro správu do Azure.

Pro Configuration Manager přístupu k rozhraní API Azure a konfiguraci cloudové proxy služby se vyžaduje certifikát pro správu Azure. Další informace a pokyny, jak nahrát certifikát pro správu, najdete v následujících článcích v dokumentaci k Azure:
- [Přehled certifikátů pro Azure Cloud Services](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Nahrajte certifikát API Management správy Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Nezapomeňte zkopírovat ID předplatného přidruženého k certifikátu pro správu. Budete ho potřebovat pro konfiguraci cloudové proxy služby v konzole Configuration Manager.

#### <a name="set-up-cloud-proxy-service"></a>Nastavení cloudové proxy služby

1. V konzole Configuration Manager klikněte na **správa > Cloud Services > cloudová proxy služba**.
2. Klikněte na **vytvořit cloudovou proxy službu**.
3. V Průvodci vytvořením cloudové proxy služby zadejte ID předplatného Azure (zkopírované na portálu pro správu Azure), klikněte na Procházet a vyberte soubor certifikátu, který jste použili k nahrání jako certifikát pro správu Azure. Klikněte na **Další**. Chvíli počkejte, než se konzola připojí k Azure.
4. Vyplňte další podrobnosti v průvodci:
    - Zadejte privátní klíč (soubor. pfx), který jste exportovali z vlastního certifikátu SSL.
    - Zadejte kořenový certifikát exportovaný z klientského certifikátu.
    - Zadejte stejný plně kvalifikovaný název domény služby, který jste použili při vytváření nové šablony certifikátu.
    - Zrušte zaškrtnutí políčka pro **ověření odvolání klientského certifikátu** (Pokud nejste veřejně publikování informací o seznamu CRL).
    - Až budete hotovi, klikněte na **Další** .
5. Zkontrolujte nastavení a klikněte na tlačítko **Další**. Configuration Manager spustí nastavování služby. Po dokončení průvodce můžete kliknout na **Zavřít**, ale bude trvat 5 až 15 minut, než se služba zřídí v Azure. Pokud chcete zjistit, jestli je služba připravená, zkontrolujte ve sloupci **stav** tuto službu cloudového proxy serveru pro nově nastavenou.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Konfigurovat primární lokalitu pro ověření certifikátu klienta

1. V konzole Configuration Manager klikněte na **správa > Konfigurace lokality > lokality**.
2. Vyberte primární lokalitu pro klienty, které chcete spravovat prostřednictvím cloudové proxy služby, a klikněte na **vlastnosti**.
3. Na kartě komunikace klientského počítače v seznamu vlastností primární lokality zaškrtněte políčko **při použití klientského certifikátu PKI (ověřování klientů), pokud je k dispozici**.
4. Nezapomeňte zrušit zaškrtnutí políčka u **klientů zkontrolovat seznam odvolaných certifikátů (CRL) pro systémy lokality**. Tato možnost se vyžaduje jenom v případě, že jste si seznam CRL veřejně publikujete.
5. Klikněte na tlačítko **OK**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Přidat bod cloudového proxy konektoru

Bod cloudového proxy konektoru je nová role systému lokality pro komunikaci s cloudovou proxy službou. Pokud chcete přidat bod cloudového proxy konektoru, postupujte podle pokynů v tématu [Přidání rolí systému lokality pro Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md).

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Konfigurace rolí pro přenos cloudového proxy serveru

Posledním krokem při nastavení cloudové proxy služby je konfigurace rolí systému lokality pro příjem přenosů cloudového proxy serveru. Pro verzi Tech Preview 1606 jsou pro cloudovou službu proxy podporovány pouze role bod správy, distribuční bod a bod aktualizace softwaru. Každou roli musíte nakonfigurovat samostatně.

1. V konzole Configuration Manager klikněte na **správa > Konfigurace lokality > servery a role systému lokality**.
2. Klikněte na server systému lokality pro roli, kterou chcete nakonfigurovat pro přenos cloudového proxy serveru.
3. Klikněte na roli a pak klikněte na **vlastnosti**.
4. V seznamu vlastnosti role v části připojení klienta zvolte **https**, zaškrtněte políčko vedle možnosti **Povolení Configuration Manager cloudového proxy serveru**a pak klikněte na **OK**. Opakujte tyto kroky u zbývajících rolí.

#### <a name="check-status-on-a-client-on-the-internet"></a>Kontrolovat stav klienta na internetu

Po dokončení konfigurace služby a rolí obdrží interní klienti umístění cloudové proxy služby v žádosti o další umístění. Klienti s aktualizovanými informacemi o umístění potom můžou komunikovat s Configuration Manager na internetu. Cyklus cyklického dotazování na požadavky na umístění je každých 24 hodin. Pokud nechcete čekat na běžně naplánovaný požadavek na umístění, můžete žádost vynutit restartováním služby Hostitel agenta serveru SMS (Ccmexec. exe) v počítači.

Jakmile klienti mají nové informace o umístění pro cloudovou službu proxy, zkuste zkontrolovat stav klientů, kteří už nejsou v interní privátní síti, ale mají přístup k Internetu. Provoz na cloudové proxy službě můžete také monitorovat tak, že v podokně se seznamem **> Cloud Services > cloudovou službu proxy serveru**, vyberete službu a zobrazíte informace o přenosech v podokně podrobností.   

## <a name="manage-the-office-365-client-agent-in-configuration-manager"></a><a name="manage_o365"></a>Správa klientského agenta Office 365 v Configuration Manageru  

Od verze Technical Preview 1606 můžete místo zásad skupiny použít Configuration Managerho klientského agenta, aby klienti Office 365 mohli dostávat aktualizace z Configuration Manager. Po nakonfigurování tohoto nastavení a nasazení aktualizací Office 365 komunikuje klientský Agent Configuration Manager s agentem klienta Office 365 ke stažení aktualizací Office 365 z distribučního bodu a jejich instalaci. Configuration Manager také převezme inventář nastavení agenta klienta.

Další informace najdete v tématu [Správa aktualizací Office 365 ProPlus](https://technet.microsoft.com/library/mt741983.aspx).

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Nastavení Configuration Manager klienta pro správu klientského agenta Office 365
1.  V konzole Configuration Manager klikněte na **Správa** > **Přehled** > **nastavení klienta**.
2. Otevřete příslušné nastavení zařízení a povolte agenta klienta. Další informace o výchozích a vlastních nastaveních klienta najdete v tématu [Konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).
3. Klikněte na možnost **aktualizace softwaru** a u nastavení **Povolit správu klientského agenta systému Office 365** vyberte **Ano** .  


## <a name="the-osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a><a name="osdpreservedriveletter"></a>Vyřazení proměnné pořadí úkolů OSDPreserveDriveLetter
Proměnná pořadí úloh OSDPreserveDriveLetter určuje, jestli pořadí úkolů používá písmeno jednotky zaznamenané v souboru WIM bitové kopie operačního systému při použití této bitové kopie na cílový počítač.
- Tato proměnná pořadí úloh se v Technical Preview 1606 už nepoužívá.

Při nasazení operačního systému ve výchozím nastavení instalační program systému Windows nyní určuje nejvhodnější písmeno jednotky, které se má použít (obvykle C:). Pokud chcete určit jinou jednotku, kterou chcete použít, můžete změnit umístění v kroku pořadí úkolů použít operační systém. V části **Vyberte umístění, kde chcete použít toto nastavení operačního systému** , vyberte **konkrétní písmeno logické jednotky**a zvolte jednotku, kterou chcete použít. Musí být přiřazená jednotka s písmenem, které zvolíte v cílovém počítači. 

## <a name="changes-for-the-updates-and-servicing-node"></a><a name="updatesandservicing"></a>Změny uzlu Aktualizace a údržba
V Technical Preview 1606 byly v konzole Configuration Manager k dispozici některé změny, které se týkají aktualizací a údržby:
- **Změna názvu uzlu:**

    V pracovním prostoru **sledování** byl uzel **stav údržby lokality** přejmenován na **stav aktualizace a údržba**.
- **Další stav instalace:**

    Po zobrazení stavu instalace aktualizace lokality teď konzola zobrazuje samostatné podrobnosti pro následující akce:
    - **Stáhnout** (platí jenom pro lokalitu nejvyšší úrovně, kde je nainstalovaná role systému lokality spojovacího bodu služby)
    - **Replikace**
    - **Kontrola předpokladů**
    - **Instalace**

  K dispozici jsou také podrobnější informace o jednotlivých krocích, včetně informací o tom, ve kterém souboru protokolu můžete zobrazit další informace.  
-   **Nová možnost pro opakování neúspěšných požadavků:**

    V pracovních prostorech **Správa** a **monitorování** obsahuje uzel **aktualizace a údržba** na pásu karet nové tlačítko s názvem **Ignorovat upozornění na předpoklady**.

    Když instalujete aktualizace bez použití možnosti ignorovat upozornění na předpoklady (v rámci průvodce aktualizacemi) a tato instalace aktualizace se zastaví se stavem **Upozornění požadavků ohlásila**, můžete vybrat možnost **Ignorovat upozornění na předpoklady** z pásu karet a aktivovat automatické pokračování instalace aktualizace, která ignoruje upozornění na požadavky.  



- **Zobrazení čisticích aktualizací:**

    Po zobrazení uzlu **aktualizace a údržba** se zobrazí pouze poslední nainstalovaná aktualizace a všechny nové aktualizace, které jsou k dispozici pro instalaci. Chcete-li zobrazit dříve nainstalované aktualizace, klikněte na tlačítko nové **Historie** , které se zobrazí na pásu karet.  

-   **Přejmenovaná možnost pro předprodukční:**

    V uzlu aktualizace a údržba je nyní přejmenováno tlačítko s názvem **Možnosti klienta** , aby bylo možné **zvýšit úroveň předprodukčního klienta**.
