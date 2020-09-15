---
title: Přidání a přiřazení aplikací Win32 k Microsoft Intune
titleSuffix: ''
description: Naučte se, jak přidávat, přiřazovat a spravovat aplikace Win32 pomocí Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5266f354ea5806743813d1aeb4c456890fa46b19
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083943"
---
# <a name="add-assign-and-monitor-a-win32-app-in-microsoft-intune"></a>Přidání, přiřazení a monitorování aplikace Win32 v Microsoft Intune

Po [přípravě aplikace Win32, která se má nahrát do Intune](apps-win32-prepare.md) , pomocí nástroje pro [přípravu obsahu Microsoft Win32](https://go.microsoft.com/fwlink/?linkid=2065730), můžete aplikaci přidat do Intune. Další informace o přípravě aplikace Win32, která se má nahrát, najdete v tématu [Příprava obsahu aplikace Win32 pro nahrání](apps-win32-prepare.md).

## <a name="prerequisites"></a>Předpoklady

Pokud chcete používat správu aplikací Win32, ujistěte se, že splňujete následující kritéria:

- Použijte Windows 10 verze 1607 nebo novější (verze Enterprise, pro a školství).
- Zařízení musí být připojená k Azure Active Directory (Azure AD) a automaticky zaregistrovaná. Rozšíření správy Intune podporuje zařízení, která jsou připojená k Azure AD, připojené k hybridní doméně a zaregistrované zásady skupiny. 
  > [!NOTE]
  > V případě registrace zásad skupiny uživatel používá místní uživatelský účet ke službě Azure AD připojit své zařízení s Windows 10. Uživatel se musí přihlásit k zařízení pomocí svého uživatelského účtu Azure AD a zaregistrovat se v Intune. Intune nainstaluje na zařízení rozšíření pro správu Intune, pokud je skript PowerShellu nebo aplikace Win32 cílené na uživatele nebo zařízení.
- Velikost aplikace systému Windows je omezené na 8 GB na aplikaci.

Podobně jako u standardní obchodní aplikace (LOB) můžete přidat aplikaci Win32 do Microsoft Intune. Tento typ aplikace se obvykle zapisuje za interní nebo třetí stranou. 

## <a name="process-flow-to-add-a-win32-app-to-intune"></a>Tok procesu pro přidání aplikace Win32 do Intune

<img alt="Flow chart of the process to add a Win32 app to Intune." src="./media/apps-win32-app-management/add-win32-app.svg" width="500">

## <a name="add-a-win32-app-to-intune"></a>Přidání aplikace Win32 do Intune

Následující kroky vám pomůžou přidat aplikaci pro Windows do Intune:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **všechny aplikace**  >  **Přidat**.
3. V podokně **Vybrat typ aplikace** v části **ostatní** typy aplikací vyberte **aplikace pro Windows (Win32)**.

    > [!IMPORTANT]
    > Nezapomeňte použít nejnovější verzi nástroje pro přípravu obsahu Microsoft Win32. Pokud nepoužíváte nejnovější verzi, zobrazí se upozornění, že aplikace byla zabalená pomocí starší verze nástroje. 

4. Klikněte na **Vybrat**. Zobrazí se postup **Přidání aplikace** .

## <a name="step-1-app-information"></a>Krok 1: informace o aplikaci

### <a name="select-the-app-package-file"></a>Vyberte soubor balíčku aplikace.

1. V podokně **Přidat aplikaci** klikněte na **Vybrat soubor balíčku aplikace**. 
2. V podokně **soubor balíčku aplikace** klikněte na tlačítko Procházet. Potom vyberte instalační soubor Windows s příponou *.intunewin*.
   Zobrazí se podrobnosti o aplikaci.
3. Až budete hotovi, vyberte **OK** v podokně **soubor balíčku aplikace** .

### <a name="set-app-information"></a>Nastavení informací o aplikaci

Na stránce **informace o aplikaci** přidejte podrobnosti o aplikaci. V závislosti na aplikaci, kterou jste zvolili, mohou být některé hodnoty na této stránce automaticky vyplněny.

- **Název**: Zadejte název aplikace, který se zobrazí na portálu společnosti. Ověřte, že názvy všech používaných aplikací jsou jedinečné. Pokud stejný název aplikace existuje dvakrát, zobrazí se na portálu společnosti jen jedna z aplikací.
- **Popis**: Zadejte popis aplikace. Popis se zobrazí na portálu společnosti.
- **Vydavatel**: zadejte název vydavatele aplikace.
- **Kategorie**: vyberte jednu nebo více předdefinovaných kategorií aplikací nebo vyberte kategorii, kterou jste vytvořili. Díky kategoriím uživatelé aplikaci při procházení portálu společnosti snadněji najdou.
- **Zobrazit tuto aplikaci jako doporučenou aplikaci v portál společnosti**: když uživatelé vyhledávají aplikace, zobrazí se na hlavní stránce portálu společnosti výrazně.
- **Adresa URL informací**: Volitelně můžete zadat adresu URL webu, který obsahuje informace o této aplikaci. Adresa URL se zobrazí na portálu společnosti.
- **Adresa URL informací o ochraně osobních údajů**: Volitelně zadejte adresu URL webu, který obsahuje informace o ochraně osobních údajů v této aplikaci. Adresa URL se zobrazí na portálu společnosti.
- **Vývojář**: Volitelně zadejte jméno vývojáře aplikace.
- **Vlastník**: Volitelně zadejte jméno vlastníka aplikace. Zadat můžete například **Personální oddělení**.
- **Poznámky**: Zadejte jakékoli poznámky, které chcete k aplikaci přidružit.
- **Logo**: Nahrajte ikonu, která je přidružená k aplikaci. Tato ikona se u aplikace zobrazí, když uživatelé procházejí portál společnosti.

Kliknutím na tlačítko **Další** zobrazíte stránku **programu** .

## <a name="step-2-program"></a>Krok 2: program

Na stránce **program** nakonfigurujte příkazy instalace a odebrání aplikace pro aplikaci:

- **Install – příkaz**: přidejte k instalaci aplikace úplný příkazový řádek instalace. 

    Například pokud je název souboru vaší aplikace **MyApp123**, přidejte následující:

    `msiexec /p "MyApp123.msp"`
    
    Pokud je aplikace `ApplicationName.exe` , příkaz by představoval název aplikace následovaný argumenty příkazu (přepínači), které balíček podporuje. Příklad:

    `ApplicationName.exe /quiet`
    
    V předchozím příkazu `ApplicationName.exe` balíček podporuje `/quiet` argument příkazu. 
    
    Konkrétní argumenty, které balíček aplikace podporuje, získáte od dodavatele aplikace.

    > [!IMPORTANT]
    > Správci musí být opatrní při použití příkazových nástrojů. Neočekávané nebo škodlivé příkazy mohou být předány prostřednictvím **příkazu install** a **příkazového řádku pro odinstalaci** .

- **Příkaz uninstall**: přidejte úplný příkazový řádek pro odinstalaci aplikace na základě identifikátoru GUID aplikace. 

    Příklad:
    
    `msiexec /x "{12345A67-89B0-1234-5678-000001000000}"`

- **Chování při instalaci**: nastavte chování pro instalaci buď na **systém** , nebo na **uživatele**.

    > [!NOTE]
    > Aplikaci Win32 můžete nakonfigurovat tak, aby se nainstalovala v kontextu **uživatele** nebo **systému**. **Uživatelský** kontext odkazuje pouze na konkrétního uživatele. Kontext **Systém** se vztahuje ke všem uživatelům zařízení s Windows 10.
    >
    > Pro instalaci aplikací Win32 není nutné, aby se uživatelé přihlásili k zařízení.
    > 
    > Instalace a odinstalace aplikace Win32 proběhne v části oprávnění správce (ve výchozím nastavení), když je aplikace nastavená na instalaci v uživatelském kontextu a uživatel na zařízení má oprávnění správce.
    
- **Chování při restartování zařízení**: vyberte jednu z následujících možností:
    - **Určete chování na základě návratových kódů**: tuto možnost vyberte, pokud chcete zařízení restartovat na základě návratových kódů.
    - **Žádná konkrétní akce**: tuto možnost vyberte, pokud chcete potlačit restartování zařízení během instalace aplikace založené na MSI.
    - **Instalace aplikace může vynutit restartování zařízení**: tuto možnost vyberte, pokud chcete, aby se instalace aplikace mohla dokončit bez potlačení restartování.
    - **Intune vynutí povinné restartování zařízení**: tuto možnost vyberte, když chcete zařízení po úspěšné instalaci aplikace vždycky restartovat.

- **Zadání návratových kódů pro indikaci chování po instalaci**: přidejte návratové kódy, které se používají k určení chování při instalaci aplikace nebo chování po instalaci. Položky návratových kódů se standardně přidají při vytváření aplikace. Můžete ale přidat více návratových kódů nebo změnit existující návratové kódy.
    1. Ve sloupci **typ kódu** nastavte **typ kódu** na jednu z následujících možností:
        - **Nepovedlo se**: vrácená hodnota, která označuje selhání při instalaci aplikace.
        - **Pevný restart**: návratový kód při pevném restartování neumožňuje instalaci další aplikace Win32 do klienta bez restartování. 
        - **Obnovitelné restartování**: návratový kód obnovitelného restartování umožňuje nainstalovat další aplikaci Win32 bez nutnosti restartování klienta. Restartování je důležité pro instalaci aktuální aplikace.
        - **Opakovat**: Agent návratového kódu opakování se pokusí aplikaci nainstalovat třikrát. Bude se čekat pět minut mezi jednotlivými pokusy. 
        - **Úspěch**: vrácená hodnota, která indikuje, že aplikace byla úspěšně nainstalována.
    2. V případě potřeby vyberte **Přidat** a přidejte další návratové kódy nebo upravte existující návratové kódy.

Kliknutím na tlačítko **Další** zobrazíte stránku **požadavky** .    

## <a name="step-3-requirements"></a>Krok 3: požadavky

Na stránce **požadavky** zadejte požadavky, které zařízení musí splnit, než bude aplikace nainstalována:

- **Architektura operačního systému**: vyberte architektury potřebné k instalaci aplikace.
- **Minimální operační systém**: Vyberte minimální operační systém potřebný k instalaci aplikace.
- **Požadované místo na disku (MB)**: Volitelně přidejte volné místo na systémové jednotce pro instalaci aplikace.
- **Požadovaná fyzická paměť (MB)**: Volitelně přidejte fyzickou paměť (RAM) nutnou pro instalaci aplikace.
- **Minimální požadovaný počet logických procesorů**: Volitelně přidejte minimální počet logických procesorů požadovaných k instalaci aplikace.
- **Minimální požadovaná rychlost CPU (MHz)**: Volitelně přidejte minimální rychlost procesoru, která se požaduje pro instalaci aplikace.
- **Konfigurovat další pravidla požadavků**: 
    1. Výběrem **Přidat** zobrazíte podokno **Přidat pravidlo požadavku** a nakonfigurujete další pravidla požadavků. Vyberte hodnotu **typ požadavku** a zvolte typ pravidla, pomocí kterého určíte, jak je požadavek ověřený. Pravidla požadavků můžou být založená na informacích o systému souborů, hodnotách registru nebo skriptech PowerShellu. 
        - **Soubor**: když jako hodnotu **typu požadavku** zvolíte **soubor** , pravidlo požadavku musí detekovat soubor nebo složku, datum, verzi nebo velikost. 
            - **Cesta**: úplná cesta ke složce obsahující soubor nebo složku, která se má zjistit.
            - **Soubor nebo složka**: soubor nebo složka, které se mají zjistit.
            - **Vlastnost**: Vyberte typ pravidla, které se použije k ověření přítomnosti aplikace.
            - **Přidružená k 32 aplikaci na 64 klientech**: výběrem **Ano** rozbalíte všechny proměnné prostředí PATH v kontextu 32-bit v počítačích s 64. Výchozí možnost **Ne** vyberte, pokud chcete rozbalit všechny proměnné cesty ve 64bitovém kontextu na 64bitových klientech. 32bitoví klienti budou vždy používat 32bitový kontext.
        - **Registr**: když jako hodnotu **typu požadavku** zvolíte možnost **registr** , pravidlo požadavku musí zjistit nastavení registru na základě hodnoty, řetězce, celého čísla nebo verze.
            - **Cesta ke klíči**: úplná cesta k položce registru, která obsahuje hodnotu, která se má zjistit.
            - **Název hodnoty**: název hodnoty registru, která se má detekovat. Pokud je tato hodnota prázdná, provede se zjišťování u klíče. Hodnota klíče (výchozí) se použije jako hodnota zjišťování v případě, že se metoda zjišťování liší od metody zjišťování existence souboru nebo složky.
            - **Požadavek na klíč registru**: Vyberte typ porovnání klíče registru, který se používá k určení způsobu ověření pravidla požadavku.
            - **Přidružená k 32 aplikaci na 64 klientech**: vyberte **Ano** , pokud chcete hledat v 64 počítačích s 64bitovým systémem na 32. Pokud chcete vyhledat 64 registr na 64 klientech, vyberte **ne** (výchozí). 32bitoví klienti budou vždy vyhledávat 32bitový registr.
        - **Skript**: Pokud nemůžete vytvořit pravidlo požadavku na základě souboru, registru nebo jakékoli jiné metody, kterou máte k dispozici v konzole Intune, vyberte **skript** jako hodnotu **typu požadavku** .
            - **Soubor skriptu**: pro pravidlo založené na požadavku skriptu PowerShellu, pokud je stávající kód 0, detekujeme ve více podrobnostech standardní výstup (stdout). Můžete například detekovat STDOUT jako celé číslo s hodnotou 1.
            - **Spustit skript jako 32ový proces na 64 klientech**: vyberte **Ano** , pokud chcete skript spustit 32 v 16bitovém procesu 64 na 64bitových klientech. Pokud chcete spustit skript v 64 procesech na 64 klientech, vyberte **ne** (výchozí). 32-bitoví klienti spouštějí skript v procesu 32.
            - **Spusťte tento skript pomocí přihlašovacích údajů přihlášeného**: vyberte **Ano** , pokud chcete skript spustit pomocí přihlašovacích údajů pro zařízení, které jste přihlásili.
            - **Vynutilo kontrolu podpisu skriptu**: vyberte **Ano** , pokud chcete ověřit, jestli má důvěryhodný vydavatel podpis skriptu. Tím umožníte, aby se skript spouštěl bez upozornění, nebo se zobrazí žádné výzvy. Skript se bude spouštět odblokovaný. Pokud chcete spustit skript s potvrzením uživatele bez ověření podpisu, vyberte **ne** (výchozí).
            - **Vyberte typ výstupních dat**: vyberte datový typ, který se používá k určení shody pravidla požadavku.
    2. Až budete s nastavením pravidel požadavků hotovi, vyberte **OK**.

Kliknutím na tlačítko **Další** zobrazíte stránku **pravidla detekce** . 

## <a name="step-4-detection-rules"></a>Krok 4: pravidla detekce

Na stránce **pravidla detekce** nakonfigurujte pravidla pro detekci přítomnosti aplikace:
    
- **Formát pravidel**: vyberte, jak se bude detekovat přítomnost aplikace. Pravidla detekce můžete nakonfigurovat ručně, ale můžete použít i vlastní skript, který zjistí přítomnost aplikace. Musíte zvolit alespoň jedno pravidlo detekce. 

  > [!NOTE]
  > V podokně **pravidla detekce** se můžete rozhodnout přidat několik pravidel. Podmínky *všech* pravidel se musí splnit, aby bylo možné aplikaci zjistit.
  >
  > Pokud Intune zjistí, že se aplikace v zařízení nenachází, Intune tuto aplikaci nabídne znovu za 24 hodin. K tomu dojde jenom u aplikací, které cílí na požadovaný záměr.

- **Ruční konfigurace pravidel detekce**: můžete vybrat jeden z následujících typů pravidel:
    - **MSI**: ověření na základě kontroly verze MSI. Tuto možnost lze přidat pouze jednou. Když zvolíte tento typ pravidla, máte dvě nastavení:
        - **Kód produktu MSI**: přidejte do aplikace platný kód produktu MSI.
        - **Kontrola verze produktu MSI**: vyberte **Ano** , pokud chcete kromě kódu produktu MSI ověřit i verzi produktu MSI.
    - **Soubor**: ověření na základě zjištění souboru nebo složky, data, verze nebo velikosti.
        - **Cesta**: zadejte úplnou cestu ke složce, která obsahuje soubor nebo složku ke zjištění.
        - **Soubor nebo složka**: Zadejte soubor nebo složku, které chcete zjistit.
        - **Metoda detekce**: Vyberte typ metody detekce, který se používá k ověření přítomnosti aplikace.
        - **Přidružená k 32 aplikaci na 64 klientech**: výběrem **Ano** rozbalíte všechny proměnné prostředí PATH v kontextu 32-bit v počítačích s 64. Výchozí možnost **Ne** vyberte, pokud chcete rozbalit všechny proměnné cesty ve 64bitovém kontextu na 64bitových klientech. 32bitoví klienti budou vždy používat 32bitový kontext.
            
        **Příklady zjišťování na základě souboru**

        Zkontrolujte, zda soubor existuje.
         
        ![Snímek obrazovky s podoknem pravidel detekce – existence souboru](./media/apps-win32-app-management/apps-win32-app-03.png)
        
        Zkontrolujte, zda složka existuje.
        
        ![Snímek obrazovky s podoknem pravidla detekce – existence složky](./media/apps-win32-app-management/apps-win32-app-04.png)
        
    - **Registr**: ověření na základě hodnoty, řetězce, celého čísla nebo verze.
        - **Cesta ke klíči**: úplná cesta k položce registru, která obsahuje hodnotu, která se má zjistit. Platná syntaxe je HKEY_LOCAL_MACHINE \Software\WinRAR nebo HKLM\Software\WinRAR..
        - **Název hodnoty**: název hodnoty registru, která se má detekovat. Pokud je tato hodnota prázdná, provede se zjišťování u klíče. Hodnota klíče (výchozí) se použije jako hodnota zjišťování v případě, že se metoda zjišťování liší od metody zjišťování existence souboru nebo složky.
        - **Metoda detekce**: Vyberte typ metody detekce, který se používá k ověření přítomnosti aplikace.
        - **Přidružená k 32 aplikaci na 64 klientech**: vyberte **Ano** , pokud chcete hledat v 64 počítačích s 64bitovým systémem na 32. Pokud chcete vyhledat 64 registr na 64 klientech, vyberte **ne** (výchozí). 32bitoví klienti budou vždy vyhledávat 32bitový registr.
            
        **Příklady zjišťování na základě registru**
        
        Ověřte, zda klíč registru existuje.
            
        ![Snímek obrazovky s podoknem pravidla detekce – klíč registru existuje.](./media/apps-win32-app-management/apps-win32-app-05.png)    
            
        Ověřte, zda hodnota registru existuje.
        
        ![Snímek obrazovky s podoknem pravidel detekce – hodnota registru existuje.](./media/apps-win32-app-management/apps-win32-app-06.png)    
        
        Zkontrolujte, zda se řetězec hodnoty registru rovná.
        
        ![Snímek obrazovky s podoknem pravidla detekce – řetězec hodnoty registru se rovná.](./media/apps-win32-app-management/apps-win32-app-07.png)    
     
- **Použijte vlastní skript detekce**: zadejte powershellový skript, který se použije k detekci této aplikace. 
    
   - **Soubor skriptu**: vyberte powershellový skript, který zjistí přítomnost aplikace na klientovi. Aplikace bude detekována, když skript vrátí ukončovací kód **0** a zapíše hodnotu řetězce do STDOUT.

   - **Spustit skript jako 32ový proces na 64 klientech**: vyberte **Ano** , pokud chcete skript spustit 32 v 16bitovém procesu 64 na 64bitových klientech. Pokud chcete spustit skript v 64 procesech na 64 klientech, vyberte **ne** (výchozí). 32-bitoví klienti spouštějí skript v procesu 32.

   - **Vynutilo kontrolu podpisu skriptu**: vyberte **Ano** , pokud chcete ověřit, jestli má důvěryhodný vydavatel podpis skriptu. Tím umožníte, aby se skript spouštěl bez upozornění, nebo se zobrazí žádné výzvy. Skript se bude spouštět odblokovaný. Pokud chcete spustit skript s potvrzením uživatele bez ověření podpisu, vyberte **ne** (výchozí).
    
   Agent Intune kontroluje výsledky ze skriptu. Přečte hodnoty zapsané skriptem do datového proudu STDOUT, do datového proudu "Standard Error" (STDERR) a ukončovacího kódu. Pokud kód končí nenulovou hodnotu, skript selže a stav zjišťování aplikace je Nenainstalováno. Pokud je ukončovací kód nula a STDOUT obsahuje data, je stav detekce aplikace nainstalován. 

   > [!NOTE]
   > Doporučujeme kódování skriptu jako UTF-8. Když se skript ukončí s hodnotou **0**, spuštění skriptu bylo úspěšné. Druhý výstupní kanál označuje, že aplikace byla zjištěna. Data STDOUT označují, že se aplikace našla na klientovi. Nehledáme konkrétní řetězec z STDOUT.

Po přidání pravidel vyberte **Další** pro zobrazení stránky **závislosti** .

## <a name="step-5-dependencies"></a>Krok 5: závislosti

Závislosti aplikací jsou aplikace, které je třeba nainstalovat, než bude možné nainstalovat aplikaci Win32. Můžete vyžadovat, aby byly další aplikace nainstalovány jako závislosti. 

Konkrétně musí zařízení před instalací aplikace Win32 nainstalovat závislé aplikace. Existuje maximálně 100 závislostí, které zahrnují závislosti všech zahrnutých závislostí a také samotnou aplikaci. 

Závislosti aplikace Win32 můžete přidat až po přidání a nahrání aplikace Win32 do Intune. Po přidání aplikace Win32 se zobrazí možnost **závislosti** v podokně aplikace Win32. 

Jakákoli závislost aplikace Win32 musí být také aplikace Win32. Nepodporuje se v závislosti na dalších typech aplikací, jako jsou například samostatné aplikace typu MSI LOB nebo aplikace Microsoft Store.

Když přidáváte závislost aplikace, můžete vyhledávat podle názvu aplikace a vydavatele. Přidané závislosti můžete seřadit také na základě názvu a vydavatele aplikace. V seznamu přidaných závislostí aplikací nelze vybrat dříve přidané závislosti aplikací. 

Můžete zvolit, jestli se mají automaticky instalovat jednotlivé závislé aplikace. Ve výchozím nastavení je možnost **automaticky instalovat** nastavená na **hodnotu Ano** pro každou závislost. Při automatické instalaci závislé aplikace, i když není závislá aplikace cílena na uživatele nebo zařízení, Intune nainstaluje aplikaci na zařízení, aby před instalací aplikace Win32 splňovala závislost. 

Je důležité si uvědomit, že závislost může mít rekurzivní závislosti a každá podřízená závislost bude nainstalována před instalací hlavní závislosti. Kromě toho instalace závislostí nedodržuje konkrétní pořadí na úrovni závislosti.

### <a name="select-the-dependencies"></a>Vybrat závislosti

Na stránce **závislosti** vyberte aplikace, které se musí nainstalovat, aby bylo možné nainstalovat aplikaci Win32:
1. Vyberte **Přidat** a zobrazte tak podokno **Přidat závislost** .
3. Přidejte závislé aplikace a pak klikněte na **Vybrat**.
4. Zvolte, jestli se mají automaticky instalovat závislé aplikace, a to tak, že ve sloupci **automaticky instalovat** vyberete **Ano** nebo **ne** .

Po výběru závislostí vyberte **Další** pro zobrazení stránky **značky oboru** .

### <a name="understand-additional-dependency-details"></a>Vysvětlení dalších podrobností o závislostech

Uživateli se zobrazí oznámení systému Windows, která označují, že se stahují a instalují závislé aplikace jako součást procesu instalace aplikace Win32. Kromě toho, když není nainstalovaná závislá aplikace, uživateli se obvykle zobrazí jedno z následujících oznámení:
- Jednu nebo víc závislých aplikací se nepovedlo nainstalovat.
- Nejméně jeden požadavek závislé aplikace není splněn.
- Jedna nebo více závislých aplikací čeká na restartování zařízení.

Pokud se rozhodnete neumístit závislost do sloupce **automaticky instalovat** , instalace aplikace Win32 se nepokusí. Kromě toho se v hlášení aplikace zobrazí, že závislost byla označena jako `failed` a že má důvod selhání. Selhání instalace závislosti můžete zobrazit tak, že vyberete chybu (nebo upozornění), která je k dispozici v [podrobnostech o instalaci](troubleshoot-app-install.md#win32-app-installation-troubleshooting)aplikace Win32.

Každá závislost bude odpovídat logice opakování aplikace Intune Win32 (pokus o instalaci třikrát po pěti minutách) a na globální plán opakovaného vyhodnocení. Závislosti se taky vztahují jenom na dobu instalace aplikace Win32 do zařízení. Závislosti nejsou k dispozici pro odinstalaci aplikace Win32. Chcete-li odstranit závislost, je nutné vybrat tři tečky vlevo od závislé aplikace umístěné na konci řádku seznamu závislostí. 

## <a name="step-6-select-scope-tags-optional"></a>Krok 6: výběr značek oboru (volitelné)
Pomocí značek Scope můžete určit, kdo může v Intune zobrazit informace o klientské aplikaci. Úplné podrobnosti o značkách oboru najdete v tématu [použití značek řízení přístupu na základě role a rozsahu pro distribuci IT](../fundamentals/scope-tags.md).

Klikněte na **Vybrat značky oboru** a volitelně přidejte značky oboru pro aplikaci. Pak kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .

## <a name="step-7-assignments"></a>Krok 7: přiřazení

Můžete vybrat **požadované**, **dostupné pro zaregistrovaná zařízení**nebo **odinstalaci** přiřazení skupin pro aplikaci. Další informace najdete v tématech [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md) a [přiřazení aplikací do skupin pomocí Microsoft Intune](apps-deploy.md).

1. Pro konkrétní aplikaci vyberte typ přiřazení:
    - **Povinné**: Aplikace se nainstaluje na zařízení ve vybraných skupinách.
    - **K dispozici pro zaregistrovaná zařízení**: uživatelé aplikaci nainstalují z aplikace Portál společnosti nebo z webu portál společnosti.
    - **Odinstalovat**: Aplikace se odinstaluje ze zařízení ve vybraných skupinách.
2. Vyberte **Přidat skupinu** a přiřaďte skupiny, které budou používat tuto aplikaci.
3. V podokně **Vybrat skupiny** vyberte skupiny, které chcete přiřadit podle uživatelů nebo zařízení.
4. Po výběru skupin můžete také nastavit **oznámení koncových uživatelů**, **dostupnost**a **konečný termín instalace**. Další informace najdete v tématu [Nastavení dostupnosti a oznámení aplikace Win32](apps-win32-app-management.md#set-win32-app-availability-and-notifications).
5. Pokud nechcete, aby toto přiřazení aplikace ovlivnilo skupiny uživatelů, vyberte **zahrnout do** sloupce **režim** . V podokně **Upravit přiřazení** změňte hodnotu **režim** z  **zahrnuto** na **vyloučeno**. Kliknutím na **tlačítko OK** zavřete podokno **Upravit přiřazení** .
6. V části **nastavení aplikace** vyberte pro aplikaci hodnotu **priority Optimalizace doručení** . Toto nastavení určuje, jak se bude obsah aplikace stahovat. Můžete si stáhnout obsah aplikace v režimu na pozadí nebo v režimu popředí na základě přiřazení. 

Po dokončení nastavení přiřazení pro aplikace vyberte **Další** pro zobrazení stránky **Revize + vytvořit** .

## <a name="step-8-review-and-create"></a>Krok 8: Kontrola a vytváření

1. Zkontrolujte hodnoty a nastavení, které jste zadali pro aplikaci. Ověřte, jestli jste správně nakonfigurovali informace o aplikaci.
2. Vyberte **vytvořit** a přidejte tak aplikaci do Intune.

    Zobrazí se podokno **přehledu** aplikace LOB.

V tuto chvíli jste dokončili kroky pro přidání aplikace Win32 do Intune. Informace o přiřazení a monitorování aplikace najdete v článku [Přiřazení aplikací do skupin pomocí Microsoft Intune](apps-deploy.md) a [Monitorování informací a přiřazení aplikace pomocí Microsoft Intune](apps-monitor.md).

## <a name="next-steps"></a>Další kroky

- [Monitorování informací a přiřazení aplikace pomocí Microsoft Intune](apps-monitor.md)
- [Řešení potíží s aplikacemi Win32](apps-win32-troubleshoot.md)
