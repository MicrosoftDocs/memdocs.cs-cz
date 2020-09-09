---
title: Možnosti ve verzi Technical Preview 1702
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1702.
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e9fa71060b8125b7d0872a40d197f1c423217bad
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607944"
---
# <a name="capabilities-in-technical-preview-1702-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1702 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1702. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Odeslat názor z konzoly Configuration Manager

Tato verze Preview přináší nové možnosti zpětné vazby v konzole Configuration Manager. Možnosti zpětné vazby vám umožní odeslat zpětnou vazbu přímo vývojovému týmu, a to prostřednictvím Configuration Manager webu pro odeslání názoru na web UserVoice.  

> Můžete najít možnost **zpětné vazby** :
> -  Na pásu karet úplně vlevo od karty Domů každého uzlu.  
>    ![Pásem](./media/feedback-home.png)

-  Když kliknete pravým tlačítkem na libovolný objekt v konzole nástroje.   
    ![Righ – možnost kliknutí](./media/feedback-option.png)   

Výběr **zpětné vazby** : otevře váš prohlížeč na webu Configuration Manager web pro odeslání názoru na https://configurationmanager.uservoice.com/forums/300492-ideas .
##  <a name="changes-for-updates-and-servicing"></a>Změny aktualizací a údržby
V této verzi Preview jsou představeny následující.

**Jednodušší možnosti aktualizace**  
Až bude vaše infrastruktura u dvou nebo více aktualizací vyhodnocena, stáhne se pouze nejnovější aktualizace. Pokud je například vaše aktuální verze lokality dvě nebo víc starší než nejnovější verze, která je k dispozici, automaticky se stáhne pouze nejnovější verze aktualizace.  

Máte možnost stahovat a instalovat i další dostupné aktualizace, i když nejsou aktuální verze. Zobrazí se však upozornění, že aktualizace byla nahrazena novějším. Chcete-li stáhnout aktualizaci, která je *k dispozici ke stažení*, vyberte aktualizaci v konzole nástroje a klikněte na tlačítko **Stáhnout**.

**Vylepšené vyčištění starších aktualizací**   
Přidali jsme funkci automatického vyčištění, která odstraní nepotřebné soubory ke stažení ze složky EasySetupPayload na vašem serveru lokality.  


## <a name="peer-cache-improvements"></a>Vylepšení sdílené mezipaměti
Od této verze bude zdrojový počítač sdílené mezipaměti zamítnout žádost o obsah, když zdrojový počítač sdílené mezipaměti splňuje některé z následujících podmínek:  
-  Je v režimu nízké baterie.
-  Zatížení procesoru překračuje 80% v době, kdy je požadován obsah.
-  Vstup/výstup disku má *AvgDiskQueueLength* , který překračuje 10.
-  K počítači nejsou k dispozici žádná další připojení.   

Tato nastavení můžete nakonfigurovat pomocí třídy konfigurace klientského agenta pro funkci zdroje peer (*SMS_WinPEPeerCacheConfig*) při použití sady Configuration Manager SDK.

Když počítač žádost o obsah odmítne, bude žádající počítač v rámci fondu dostupných zdrojových umístění obsahu pokračovat ve vyhledávání obsahu v alternativním zdroji.   

## <a name="use-azure-active-directory-domain-services-to-manage-devices-users-and-groups"></a><a name="azurediscovery"></a> Použití Azure Active Directory Domain Services ke správě zařízení, uživatelů a skupin

V této verzi Technical Preview můžete spravovat zařízení, která jsou připojená ke spravované doméně služby Azure Active Directory (AD) Domain Services. V této doméně můžete také zjišťovat zařízení, uživatele a skupiny pomocí různých metod zjišťování Configuration Manager.

Infrastruktura webu Technical Preview, klienti a Azure AD Domain Services domény musí běžet v Azure.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Nastavení Configuration Manager pro použití Azure AD
Pokud chcete používat Azure AD s Configuration Manager, budete potřebovat následující:
- Předplatné Azure.
- Azure AD se službou Domain Services (DS).
- Configuration Manager web, který běží na VIRTUÁLNÍm počítači Azure, který je připojený k vaší službě Azure AD.
- Configuration Manager klienti, kteří běží ve stejném prostředí Azure AD.

Pokud chcete nakonfigurovat službu Azure AD Domain Service, přečtěte si téma Začínáme [s Azure AD Domain Services](/azure/active-directory-domain-services/create-instance).

### <a name="discover-resources"></a>Zjišťování prostředků
Až nastavíte Configuration Manager pro běh ve službě Azure AD, můžete použít následující metody zjišťování služby Active Directory k hledání prostředků v Azure AD:  
- Zjišťování systému aktivního adresáře
- Zjišťování uživatele Active Directory
- Zjišťování skupiny aktivního adresáře  

Pro každou metodu, kterou použijete, upravte dotaz protokolu LDAP tak, aby prohledal struktury organizačních jednotek Azure AD místo kontejnerů, které jsou typické pro místní službu Active Directory. To vyžaduje, abyste dotaz nasměrovali na službu Active Directory ve vašem předplatném Azure.  

V následujících příkladech se používá Azure AD of *contoso.onmicrosoft.com*:
- **Zjišťování systému**   
  Služba Azure AD ukládá zařízení do organizační jednotky **počítačů s AADDC** .  Nakonfigurujte toto:  
  - *LDAP://OU = AADDC Computers, DC = contoso, DC = The Microsoft, DC = com*  


- **Zjišťování uživatelů** AAD ukládá uživatele v rámci organizační jednotky **AADDC Users** .  Nakonfigurujte toto:
  - *LDAP://OU = AADDC Users, DC = contoso, DC = The Microsoft, DC = com*


- **Zjišťování skupin**  
Azure AD nemá organizační jednotku, ve které se ukládají skupiny. Místo toho použijte stejnou obecnou strukturu jako dotaz systému nebo uživatele a nakonfigurujte dotaz protokolu LDAP tak, aby odkazoval na organizační jednotku obsahující skupiny, které chcete zjistit.

Další informace o službě Azure AD najdete v následujících tématech:  
- [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds) v Azure.Microsoft.com.
- [Active Directory Domain Services dokumentaci](/azure/active-directory-domain-services) k docs.Microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Vylepšení zásad dodržování předpisů pro zařízení podmíněného přístupu

K dispozici je nové pravidlo zásad dodržování předpisů pro zařízení, které vám umožní blokovat přístup k firemním prostředkům, které podporují podmíněný přístup, když uživatelé používají aplikace, které jsou součástí seznamu nekompatibilních aplikací. Seznam aplikací, které nedodržují předpisy, může správce definovat při přidávání nových aplikací pro dodržování předpisů **, které se nedají nainstalovat**. Toto pravidlo vyžaduje, aby správce při přidávání aplikace do seznamu nevyhovujících předpisů zadal **název aplikace**, **ID aplikace**a **vydavatele aplikace** (volitelné). Toto nastavení platí jenom pro zařízení s iOS a Androidem.

Kromě toho pomáhá organizacím zmírnit únik dat prostřednictvím nezabezpečených aplikací a zabránit nadměrné spotřebě dat prostřednictvím určitých aplikací.

### <a name="try-it-out"></a>Vyzkoušet

**Scénář:** Identifikujte aplikace, které by mohly způsobovat úniky dat zasíláním podnikových dat mimo vaši společnost, nebo které způsobují nadměrné množství dat, a pak [Vytvořte zásady dodržování předpisů pro zařízení podmíněného přístupu](../../mdm/understand/what-happened-to-hybrid.md) , které tyto aplikace přidá do seznamu neodpovídajících aplikací. Tím se zablokuje přístup k firemním prostředkům, které podporují podmíněný přístup, dokud uživatel nebude moct blokovanou aplikaci odebrat.

## <a name="antimalware-client-version-alert"></a>Výstraha verze antimalwarového klienta
Od této verze Preview Configuration Manager Endpoint Protection poskytuje výstrahu, pokud více než 20% (výchozí) spravovaných klientů používá verzi antimalwarového klienta (tj. Windows Defender nebo Endpoint Protection klienta).

### <a name="try-it-out"></a>Vyzkoušet
Ujistěte se, že je povolená Endpoint Protection na všech klientech desktopu a serveru pomocí zásad nastavení klienta. Teď můžete zobrazit stav nasazení **antimalwarového klienta** a **Endpoint Protection stav nasazení** , a to tak, že převedete Přehled prostředků **a dodržování předpisů**na  >  **Overview**  >  **Devices**  >  **všechna stolní počítače a klienty obsluhy**. Chcete-li zjistit výstrahu, zobrazte **výstrahy** v pracovním prostoru **monitorování** . Pokud je na více než 20% spravovaných klientů spuštěná verze antimalwarového softwaru s vypršenou platností, zobrazí se výstraha verze antimalwarového klienta je zastaralá. Tato výstraha se nezobrazuje **Monitoring**na  >  kartě**Přehled** monitorování. Chcete-li aktualizovat antimalwarové klienty s vypršenou platností, povolte aktualizace softwaru pro klienty antimalwaru.

Chcete-li nakonfigurovat procento, ve kterém je výstraha vygenerována, rozbalte položku **sledování**  >  **výstrahy**  >  **všechny výstrahy**, dvakrát klikněte na **antimalwarové klienty zastaralé** a upravte **výstrahu vyvolat, pokud procento spravovaných klientů s neaktuální verzí antimalwarového klienta je větší než** možnost.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Posouzení dodržování předpisů pro aktualizace web Windows Update pro firmy
V rámci vyhodnocení podmíněného přístupu teď můžete nakonfigurovat pravidlo aktualizace zásad dodržování předpisů tak, aby zahrnovalo výsledek vyhodnocení web Windows Update pro firmy.
> [!IMPORTANT]
> Aby bylo možné používat vyhodnocení dodržování předpisů pro aktualizace web Windows Update pro firmy, musíte mít Windows 10 Insider Preview build 15019 nebo novější.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Umožněte web Windows Update pro firmy spravovat aktualizace Windows 10.
Pokud chcete shromáždit informace o vyhodnocení dodržování předpisů pro aktualizace web Windows Update pro firmy, pomocí následujícího postupu nakonfigurujte nastavení agenta klienta tak, aby explicitně povolovala web Windows Update pro firmy ke správě aktualizací Windows 10.
1. V konzole Configuration Manager klikněte na **Správa**  >  **nastavení klienta**.
2. Ve vlastnostech nastavení klienta klikněte na **aktualizace softwaru**a vyberte **Ano** pro nastavení **spravovat aktualizace Windows 10 pomocí web Windows Update pro firmy** .

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Vytvoření zásady dodržování předpisů pro vyhodnocení web Windows Update pro firmy
1. V konzole Configuration Manager klikněte na **prostředky a**dodržování předpisů  >  **Compliance Settings**  >  **zásady dodržování**předpisů nastavení dodržování předpisů.
2. Klikněte na **vytvořit zásadu dodržování předpisů** nebo vyberte existující zásady dodržování předpisů, které chcete upravit.
3. Na stránce Obecné zadejte název a popis, vyberte **pravidla dodržování předpisů pro zařízení spravovaná pomocí klienta Configuration Manager**, nastavte závažnost neshody pro vytváření sestav a klikněte na tlačítko **Další**.
4. Na stránce podporované platformy vyberte **Windows 10**a potom klikněte na **Další**.
5. Na stránce pravidla klikněte na **Nový....** a pro **podmínky** zvolte **vyžadovat web Windows Update pro obchodní dodržování předpisů**. Nastavení **hodnoty** je automaticky nastaveno na **hodnotu true**.

Nová zásada se zobrazí v uzlu **Zásady dodržování předpisů** pracovního prostoru **Prostředky a kompatibilita**.

### <a name="deploy-a-compliance-policy"></a>Nasazení zásady dodržování předpisů
1. V konzole Configuration Manager přejděte na **prostředky a**dodržování předpisů  >  **Nastavení dodržování**předpisů a pak klikněte na **zásady dodržování předpisů**.
2. Na kartě **Domů** ve skupině **Nasazení** klikněte na možnost **Nasadit**.
3. V dialogovém okně **Nasadit zásady dodržování předpisů** klikněte na **Procházet** a vyberte kolekci uživatelů, do které chcete zásady nasadit.
   Kromě toho můžete vybrat možnosti generování výstrah v případě, že zásady nebudou kompatibilní, a taky nakonfigurovat plán, podle kterého se u této zásady vyhodnotí dodržení předpisů.
4. Po dokončení klikněte na **OK**.

### <a name="monitor-the-compliance-policy"></a>Monitorování zásady dodržování předpisů
Po vytvoření zásady dodržování předpisů můžete monitorovat výsledky dodržování předpisů v konzole Configuration Manager. Podrobnosti najdete v tématu [monitorování zásad dodržování předpisů](../../mdm/understand/what-happened-to-hybrid.md).


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Vylepšení nastavení centra softwaru a oznamovacích zpráv pro pořadí úkolů s vysokým dopadem
Tato verze zahrnuje následující vylepšení nastavení centra softwaru a oznamovacích zpráv pro pořadí úloh s vysokým dopadem na nasazení:

- Ve vlastnostech pořadí úkolů teď můžete nakonfigurovat jakékoli pořadí úkolů, včetně pořadí úkolů neoperačního systému, jako vysoce rizikové nasazení. Pořadí úkolů, které splňuje určité podmínky, je automaticky definováno jako vysoce ovlivněno. Podrobnosti najdete v tématu [Správa nasazení s vysokým rizikem](../servers/manage/settings-to-manage-high-risk-deployments.md).
- Ve vlastnostech pořadí úkolů můžete zvolit použití výchozí zprávy oznámení nebo vytvořit vlastní zprávu oznámení pro nasazení s vysokým dopadem.
- Ve vlastnostech pořadí úkolů můžete nakonfigurovat vlastnosti centra softwaru, které zahrnují nastavení vyžadovaná k restartování, velikost stahování pořadí úkolů a odhadovanou dobu běhu.
- Výchozí zpráva o nasazení s vysokým dopadem pro místní upgrady nyní uvádí, že vaše aplikace, data a nastavení se migrují automaticky. Předchozí zpráva pro jakoukoli instalaci operačního systému ukázala, že všechny aplikace, data a nastavení budou ztraceny, což nebylo pro místní upgrade pravdivé.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Nastavení pořadí úkolů jako vysoce ovlivněné pořadí úkolů
Následující postup slouží k nastavení pořadí úkolů jako vysokého dopadu.
> [!NOTE]
> Pořadí úkolů, které splňuje určité podmínky, je automaticky definováno jako vysoce ovlivněno. Podrobnosti najdete v tématu [Správa nasazení s vysokým rizikem](../servers/manage/settings-to-manage-high-risk-deployments.md).

1. V konzole Configuration Manager v části **softwarová knihovna**  >  **operační systémy**  >  **pořadí úkolů**.
2. Vyberte pořadí úkolů, které chcete upravit, a klikněte na **vlastnosti**.
3. Na kartě **oznámení uživateli** vyberte **Toto pořadí úkolů s vysokým dopadem**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Vytvoření vlastního oznámení pro nasazení s vysokým rizikem
1. V konzole Configuration Manager v části **softwarová knihovna**  >  **operační systémy**  >  **pořadí úkolů**.
2. Vyberte pořadí úkolů, které chcete upravit, a klikněte na **vlastnosti**.
3. Na kartě **oznámení uživateli** vyberte **použít vlastní text**.
   > [!NOTE]
   >  Text upozornění na uživatele můžete nastavit jenom v případě, že je vybraná možnost **pořadí úkolů s vysokým dopadem** .

4. Nakonfigurujte následující nastavení (maximálně 255 znaků pro každé textové pole):

   **Text titulku oznámení uživateli**: Určuje modrý text, který se zobrazí v oznámení o uživateli centra softwaru. Například ve výchozím oznámení uživateli Tato část obsahuje něco jako "potvrzení, že chcete upgradovat operační systém v tomto počítači".

   **Text zprávy oznámení uživateli**: Existují tři textová pole, která poskytují text vlastního oznámení.
   - 1st text box: Určuje hlavní text textu, který obvykle obsahuje pokyny pro uživatele. Například ve výchozím oznámení uživateli Tato část obsahuje něco jako "upgrade operačního systému bude trvat déle a počítač se může několikrát restartovat."
   - 2. textové pole: Určuje tučný text v hlavním těle textu. Například ve výchozím oznámení uživateli Tato část obsahuje něco jako "tento místní upgrade nainstaluje nový operační systém a automaticky migruje vaše aplikace, data a nastavení."
   - 3 textové pole: Určuje poslední řádek textu pod tučným textem. Například ve výchozím oznámení uživateli Tato část obsahuje něco jako "kliknutím na Instalovat zahájíte. V opačném případě klikněte na tlačítko Storno. "   

   Řekněme, že ve vlastnostech nakonfigurujete následující vlastní oznámení.

   ![Vlastní oznámení pro vlastnosti pořadí úloh](./media/user-notification.png)

   Když koncový uživatel otevře instalaci z centra softwaru, zobrazí se následující zpráva s oznámením.

   ![Vlastní oznámení pro pořadí úkolů – Centrum softwaru](./media/user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Konfigurace vlastností centra softwaru
Pomocí následujícího postupu můžete nakonfigurovat podrobnosti o pořadí úloh zobrazeném v centru softwaru. Tyto podrobnosti jsou pouze pro informace.  
1. V konzole Configuration Manager v části **softwarová knihovna**  >  **operační systémy**  >  **pořadí úkolů**.
2. Vyberte pořadí úkolů, které chcete upravit, a klikněte na **vlastnosti**.
3. Na kartě **Obecné** jsou k dispozici následující nastavení pro Centrum softwaru:
   - **Vyžadováno restartování**: umožňuje uživateli zjistit, zda je během instalace vyžadováno restartování.
   - **Velikost ke stažení (MB)**: Určuje, kolik megabajtů se zobrazí v nástroji Software Center pro pořadí úkolů.  
   - **Odhadovaná doba běhu (v minutách)**: Určuje odhadovanou dobu běhu (v minutách), která se zobrazí v centru softwaru pro pořadí úkolů.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Kontrolovat spouštění spustitelných souborů před instalací aplikace

V *\<deployment type name>* dialogovém okně **vlastnosti** typu nasazení můžete na kartě chování při instalaci zadat jeden z více spustitelných souborů, které při spuštění zablokují instalaci typu nasazení. Předtím, než bude možné nainstalovat typ nasazení, musí uživatel zavřít běžící spustitelný soubor (nebo ho lze zavřít automaticky pro nasazení s účelem požadované).

### <a name="try-it-out"></a>Vyzkoušejte si to.

1. Ve vlastnostech typu nasazení Configuration Manager vyberte kartu **chování při instalaci** .
2. Vyberte **Přidat** a přidejte jeden nebo více názvů spustitelných souborů, které chcete kontrolovat. Můžete také přidat zobrazované jméno, které uživatelům usnadní identifikaci aplikací v seznamu.
3. Pokud bude mít nasazení účel požadováno, můžete v Průvodci nasazením softwaru případně **automaticky zavřít všechny spuštěné spustitelné soubory, které jste zadali na kartě chování při instalaci v dialogovém okně vlastnosti typu nasazení**.

Pokud byla aplikace nasazená jako **dostupná**a koncový uživatel se pokusí nainstalovat aplikaci, zobrazí se výzva k zavření všech spuštěných spustitelných souborů, které jste zadali předtím, než budou moci pokračovat v instalaci.

Pokud byla aplikace nasazena jako **povinná**a možnost **automaticky zavře všechny spuštěné spustitelné soubory, které jste zadali na kartě chování při instalaci v dialogovém okně vlastnosti typu nasazení** , zobrazí se dialogové okno, které je informuje o tom, že spustitelné soubory, které jste zadali, budou automaticky uzavřeny po dosažení konečného termínu instalace aplikace. Tato dialogová okna můžete naplánovat v **nastavení klienta**  >  **Počítačový agent**. Pokud nechcete, aby koncový uživatel tyto zprávy viděli, vyberte **Skrýt v nástroji Software Center a všech oznámeních** na kartě **činnost koncového uživatele** ve vlastnostech nasazení.

Pokud byla aplikace nasazena jako **povinná** a možnost **automaticky zavře všechny spuštěné spustitelné soubory, které jste zadali na kartě chování při instalaci v dialogovém okně vlastnosti typu nasazení** , pak nebude instalace aplikace úspěšná, pokud je jedna nebo víc z určených aplikací spuštěná.

## <a name="create-pfx-certificates-with-s-mime-support"></a>Vytváření certifikátů PFX s podporou S MIME

Nyní můžete vytvořit profil certifikátu PFX, který podporuje S/MIME a nasazovat ho uživatelům.  Tento certifikát se pak dá použít pro šifrování S/MIME a dešifrování napříč zařízeními, která uživatel zaregistroval.

Kromě toho teď můžete zadat několik certifikačních autorit (CAs) na více rolí systému lokality bodu registrace certifikátu a pak jim přiřadit žádosti, které zpracovávají požadavky v rámci profilu certifikátu.

Pro zařízení S iOS můžete přidružit profil certifikátu PFX k e-mailovému profilu a povolit šifrování S/MIME.  Tím se pak v nativním e-mailovém klientovi v iOS povolí S/MIME a přidruží se k němu správný šifrovací certifikát S/MIME.

Další informace o certifikátech v Configuration Manager najdete v tématu [Úvod do profilů certifikátů]( /sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>Nové nastavení dodržování předpisů pro zařízení s iOS

Přidali jsme nová nastavení, která můžete použít v položkách konfigurace pro zařízení se systémem iOS. Jedná se o nastavení, která dříve existovala v Microsoft Intune samostatné konfigurace, a jsou teď dostupná, když používáte Intune s Configuration Manager. Pokud potřebujete s některým z těchto nastavení pomáhat, přečtěte si téma [nastavení zásad pro iOS v Microsoft Intune](../../../intune/configuration/device-restrictions-ios.md).

- **Synchronizovat data ze spravovaných aplikací do iCloud**
- **Předání za účelem pokračování aktivit na jiném zařízení**
- **Sdílení fotek iCloud**
- **Knihovna fotografií iCloud**
- **Důvěřovat novým autorům podnikových aplikací**
- **Povolí uživateli stahovat obsah z obchodu iBooks Storu označeného jako erotika** (jenom pod dohledem).
- **Vynutit u spárovaných Apple Watch používání detekce zápěstí**
- **Heslo pro odchozí požadavky AirPlay**
- **Upravit nastavení účtu** (jenom v režimu pod dohledem)
- **Změny nastavení využití mobilních dat v aplikaci** (jenom v režimu pod dohledem)
- **Vymazat veškerý obsah a nastavení** (jenom v režimu pod dohledem)
- **Konfigurace omezení na zařízení** (jenom v režimu pod dohledem)
- **Použití párování hostitelů k řízení zařízení, se kterými se zařízení s iOS může spárovat** (jenom v režimu pod dohledem)
- **Nainstalovat konfigurační profily a certifikáty** (jenom v režimu pod dohledem)
- **Úprava názvu zařízení** (jenom v režimu pod dohledem)
- **Úprava hesla** (jenom v režimu pod dohledem)
- **Párování Apple Watch** (jenom režim pod dohledem)
- **Úprava nastavení oznámení** (jenom v režimu pod dohledem)
- **Úprava tapety** (jenom v režimu pod dohledem)
- **Úprava nastavení odesílání diagnostiky** (jenom režim pod dohledem)
- **Úpravy Bluetooth** (jenom v režimu pod dohledem)
- **Přetažení** (jenom v režimu pod dohledem)
- **Použití Siri k dotazování na uživatelem generovaný obsah z Internetu** (jenom v režimu pod dohledem)
- **Filtr vulgárních výrazů v Siri** (jenom režim pod dohledem)
- **Při vyhledávání Spotlightu vracet výsledky z Internetu** (jenom v režimu pod dohledem)
- **Vyhledávání definic slov** (jenom v režimu pod dohledem)
- **Prediktivní klávesnice** (jenom v režimu pod dohledem)
- **Automatické opravy** (jenom v režimu pod dohledem)
- **Kontrola pravopisu klávesnice** (jenom v režimu pod dohledem)
- **Klávesové zkratky** (jenom v režimu pod dohledem)
  <!--- - **Enterprise app trust settings modification** --->
- **Instalace aplikací jenom pomocí Apple Configuratoru a iTunes** (jenom v režimu pod dohledem)
- **Automatické stahování aplikací** (jenom v režimu pod dohledem)
- **Provedení změn v nastavení aplikace Hledat přátele** (jenom v režimu pod dohledem)
- **Přístup k úložišti iBooks** (jenom v režimu pod dohledem)
- **Aplikace zprávy** (jenom v režimu pod dohledem)
- **Podcasty** (jenom v režimu pod dohledem)
- **Apple Music** (jenom v režimu pod dohledem)
- **přepínač iTunes** (jenom v režimu pod dohledem)
- **Apple News** (jenom v režimu pod dohledem)
- **Game Center** (jenom v režimu pod dohledem)
- **Považovat vztáhnout jako nespravovaný cíl**

## <a name="android-for-work-support"></a>Podpora programu Android for Work

Počínaje verzí Technical Preview 1702 můžete navazovat účet Google na svého hybridního tenanta MDM. K tomu je možné provést následující akce:

- Registrovat [podporovaná zařízení s Androidem](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) jako Android for Work a vytvářet pracovní profily na těchto zaregistrovaných zařízeních
- Schvalte aplikace v obchodě Play for Work, synchronizujte je s konzolou Configuration Manager a pak je nasaďte do pracovních profilů zařízení.
- Vytvoření a nasazení položek konfigurace pro konfiguraci nastavení pracovního profilu a hesla pro tato zařízení
- Vytvořte a nasaďte položky zásad dodržování předpisů a profily přístupu k prostředkům pro zařízení s Androidem for Work, která už máte pro zařízení s Androidem.
- Provádění selektivního vymazání na zařízeních s Androidem for Work

Když zaregistrujete zařízení jako Android for Work, vytvoří pracovní profil na zařízení, které může Intune spravovat. Tento pracovní profil existuje vedle sebe s osobním profilem na zařízení s Androidem. Uživatelé můžou snadno přepínat mezi aplikacemi pracovního profilu a aplikacemi pro osobní Profile. V osobním profilu nemůžete spravovat položky. Osobní aplikace a data zůstávají nespravované. Configuration Manager má úplnou kontrolu nad pracovním profilem a jeho obsahem a může ho ze zařízení odebrat.

Android for Work je samostatná platforma od Androidu a vy budete se muset rozhodnout, jakou formu správy chcete použít pro zařízení s Androidem, která podporují pracovní profily.

### <a name="try-it-out"></a>Určitě to udělejte!
Následující části popisují správu Androidu for Work.

#### <a name="enable-android-for-work-management"></a>Povolit správu Androidu for Work
1. Vytvořte účet Google na https://accounts.google.com/SignUp webu, který se použije jako účet správce Android for Work, který bude přidružený ke všem úlohám správy Androidu for Work pro tohoto tenanta Intune. Může to být účet Google sdílený mezi správci, kteří spravují zařízení s Androidem. Jedná se o účet Google, který vaše organizace používá ke správě a publikování aplikací v konzole Play for Work. Pomocí tohoto účtu budete schvalovat aplikace v obchodě Play for Work, takže Sledujte název účtu a heslo.
2. Povolení registrace zařízení s Androidem pomocí vazby účtu Google k tenantovi Intune spravovanému v Configuration Manager:
   1. V článku **Administration**  >  **Přehled**správy  >  **Cloud Services**  >  **Microsoft Intune předplatné** a vyberte své předplatné Intune.
   2. Na pásu karet klikněte na **Konfigurovat platformy**  >  **Android** a ujistěte se, že je zaškrtnuté políčko **Povolit registraci zařízení se systémem Android** .
   3. Na pásu karet klikněte na **Konfigurovat platformy**  >  **Android for Work**.
   4. V dialogovém okně klikněte v **konzole Intune na konfigurovat Android for Work**. Konzola Intune se otevře ve webovém prohlížeči.
   5. Pomocí přihlašovacích údajů správce Intune se přihlaste k portálu Intune.
   6. Kliknutím na **Konfigurovat** otevřete web Android for Work Google Play.
   7. Na přihlašovací stránce Google zadejte přihlašovací údaje účtu Google z kroku 1 a potom zadejte informace o vaší společnosti.
3. Když se vrátíte na portál Intune, bude Android for Work povolený a máte k dispozici tři možnosti registrace pro zařízení s Androidem for Work:
   - **Spravovat všechna zařízení jako Android** – (zakázáno) všechna zařízení s Androidem, včetně zařízení podporujících Android for Work, se zaregistrují jako zařízení s konvenčním Androidem.
   - **Spravovat podporovaná zařízení jako Android for Work** – (povoleno): Všechna zařízení, která podporují Android for Work, se zaregistrují jako zařízení s Androidem for Work. Jakékoli zařízení s Androidem, které nepodporuje Android for Work, se zaregistruje jako zařízení s konvenčním Androidem.
   - **Spravovat podporovaná zařízení pro uživatele v těchto skupinách jako Android for Work** – (testování) umožňuje zacílit správu Androidu for Work na omezené skupiny uživatelů. Jen zařízení členů vybraných skupin, kteří zaregistrují zařízení podporující Android for Work, se zaregistrují jako zařízení s Androidem for Work. Všechna ostatní se zaregistrují jako zařízení s Androidem.
  
> [!NOTE]
> Známý problém brání tomu, aby **zařízení pro správu podporovaná pro uživatele v těchto skupinách jako možnost Android for Work** fungovala podle očekávání. Zařízení uživatelů v zadaných skupinách Azure AD se budou registrovat jako Android místo Android for Work. K otestování Androidu for Work musíte použít **spravovat všechna podporovaná zařízení jako Android for Work**.


  Aby bylo možné povolit registraci Androidu for Work, musíte zvolit jednu z následujících možností. Možnost **Spravovat podporovaná zařízení pro uživatele v těchto skupinách jako možnost Android for Work** vyžaduje, abyste nejdřív nastavili Azure Active Directory skupiny zabezpečení.

Až se vazba dokončí, uvidíte název účtu a název organizace na portálu Intune. v tomto okamžiku můžete zavřít oba prohlížeče.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Schvalování a nasazování aplikací pro Android for Work
Pomocí těchto kroků schválíte aplikace v obchodě Play for Work, synchronizujete je s konzolou Configuration Manager a nasadíte je na spravovaná zařízení s Androidem for Work. Pokud chcete nasadit aplikace do pracovních profilů uživatelů, budete muset aplikace schválit v programu Play for Work a pak aplikace synchronizovat s konzolou Configuration Manager.

1. Otevřete prohlížeč a pokračujte na: https://play.google.com/work .
2. Přihlaste se pomocí účtu správce Google, který se váže k vašemu tenantovi Intune.
3. Vyhledejte aplikace, které chcete ve svém prostředí nasadit, a pro každou z nich klikněte na **schválit** .
4. V konzole Configuration Manager přejděte na přehled **správce**  >  **Overview**  >  **Cloud Services**  >  **Android for Work** a klikněte na **synchronizovat**.
5. Počkejte po dobu až 10 minut, než se aplikace synchronizuje, a pak navštivte App **Library**  >  **Přehled**  >  **Application Management**  >  **informace o licencích pro**správu aplikací pro aplikace Store.
6. Klikněte na aplikaci synchronizovaná z Play for Work a pak klikněte na **vytvořit aplikaci**.
7. Dokončete průvodce a klikněte na **Zavřít**.
8. Přejít na **softwarová knihovna**  >  **Přehled**aplikace  >  **Správa aplikací**  >  **Applications**, vyberte aplikace pro Android for Work a nasaďte je obvyklým způsobem.

Chcete-li synchronizovat aplikace Play for Work s Configuration Manager, je nutné schválit alespoň jednu aplikaci na webu Play for Work.

#### <a name="enroll-an-android-for-work-device"></a>Registrace zařízení s Androidem for Work
Způsob registrace zařízení s Androidem for Work se podobá registraci pro Android. Stáhněte a spusťte aplikaci Portál společnosti pro Android na svém mobilním zařízení. V rámci procesu registrace se zobrazí výzva k vytvoření pracovního profilu.  Po vytvoření pracovního profilu je nutné přepnout do spravované verze Portál společnosti. Spravovaná Portál společnosti je označena malou oranžovou aktovkou v pravém dolním rohu.

#### <a name="create-and-deploy-a-configuration-item"></a>Vytvoření a nasazení položky konfigurace
Android for Work má dvě skupiny nastavení pro položky konfigurace:
- Heslo
- Pracovní profil

Sdílení obsahu mezi pracovními profily a na zařízeních s Androidem 6 nebo novějším můžete nakonfigurovat i na následujících položkách konfigurace:
- Chování aplikací, které žádají o specifická oprávnění
- Zda jsou oznámení pro aplikace v pracovním profilu viditelná na zamykací obrazovce

To můžete provést tak, že vytvoříte položku Konfigurace přes standardní pracovní postup, zvolíte možnost **Android for Work** na stránce **Obecné** a nakonfigurujete nastavení pro každou skupinu nastavení, přidáte položku konfigurace do směrného plánu a nasadíte ji obvyklým způsobem. Tato nastavení se budou vztahovat jenom na zařízení zaregistrovaná v Androidu for Work, a ne na ta zaregistrovaná jako Android.

#### <a name="perform-selective-wipe"></a>Provést selektivní vymazání
Zařízení zaregistrovaná jako Android for Work se dají selektivně vymazat, protože jenom spravujete pracovní profil. Tím se chrání osobní profil před vymazáním. Při selektivním vymazání na zařízení s Androidem for Work dojde k odebrání pracovního profilu, včetně všech aplikací a dat, a zrušení registrace zařízení.

Pokud chcete selektivně vymazat zařízení s Androidem for Work, použijte normální [proces selektivního vymazání](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) v konzole Configuration Manager.

#### <a name="known-issues-for-android-for-work"></a>Známé problémy pro Android for Work
**Konfigurace plánu synchronizace v e-mailových profilech Androidu for Work způsobuje selhání nasazení** Jedna z možností v uživatelském rozhraní nástroje ConfigMgr pro e-mailové profily pro Android for Work je "plán". Na jiných platformách může správce nakonfigurovat plán pro synchronizaci e-mailů a dalších e-mailových účtů na mobilní zařízení, na která se nasazují. Nefunguje ale pro e-mailové profily Androidu for Work a výběr jiné možnosti než "není nakonfigurováno" způsobí, že se profil nebude nasazovat na žádná zařízení.