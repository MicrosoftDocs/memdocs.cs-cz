---
title: Nastavení zařízení s Androidem Enterprise v Microsoft Intune – Azure | Microsoft Docs
description: Na zařízeních s Androidem Enterprise nebo Androidem for Work můžete omezit nastavení zařízení, včetně kopírování a vkládání, zobrazování oznámení, oprávnění aplikací, sdílení dat, délky hesla, neúspěšných přihlášení, použití otisku prstu k odemknutí, opětovného použití hesel a sdílení pracovních kontaktů přes Bluetooth. Nakonfigurovat zařízení jako veřejný terminál zařízení, aby spouštěl jednu aplikaci nebo více aplikací.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b81686f645d9fce610c39266feb2675fd35cc280
ms.sourcegitcommit: 6f67c864cf71b4a6a316f4d04a6cc43cf28b4277
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/01/2020
ms.locfileid: "84257031"
---
# <a name="android-enterprise-device-settings-to-allow-or-restrict-features-using-intune"></a>Nastavení zařízení s Androidem Enterprise pro povolení nebo omezení funkcí pomocí Intune

Tento článek obsahuje seznam a popisuje různá nastavení, která můžete řídit na zařízeních s Androidem Enterprise. Jako součást řešení správy mobilních zařízení (MDM) pomocí těchto nastavení můžete povolit nebo zakázat funkce, spouštět aplikace na vyhrazených zařízeních, zabezpečení řízení a další.

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil konfigurace zařízení](device-restrictions-configure.md).

## <a name="device-owner-only"></a>Pouze vlastník zařízení

Tato nastavení se vztahují na typy registrace Androidu Enterprise, kde Intune řídí celé zařízení, jako jsou například plně spravovaná nebo vyhrazená zařízení se systémem Android Enterprise.

### <a name="general"></a>Obecné

- **Snímek obrazovky**: **Block** zabraňuje tomu, aby se snímky obrazovky nebo obrazovka na zařízení nasnímání. Brání tím také zobrazení obsahu na zobrazovacích zařízeních, která nemají bezpečný výstup videa. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožnit zachytit obsah obrazovky v podobě obrázku.
- **Kamera**: **Block** zabrání přístupu k fotoaparátu na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k fotoaparátu.

  Intune spravuje jenom přístup k kameře zařízení. Nemá přístup k obrázkům a videím.

- **Výchozí zásady oprávnění**: Toto nastavení definuje výchozí zásady oprávnění pro žádosti o oprávnění za běhu. Vaše možnosti
  - **Výchozí nastavení zařízení**: použijte výchozí nastavení zařízení.
  - **Výzva**: uživatelům se zobrazí výzva ke schválení oprávnění.
  - **Automaticky udělit**: Oprávnění jsou udělena automaticky.
  - **Automaticky odepřít**: Oprávnění jsou odepřena automaticky.
- **Změny data a času**: **blok** zabraňuje uživatelům v ručním nastavení data a času. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby na zařízení nastavili datum a čas.
- **Změny svazku**: **blok** znemožní uživatelům měnit svazek zařízení a také mutes hlavní svazek. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém použít nastavení svazku na zařízení.
- **Obnovení továrního**nastavení: **blok** znemožní uživatelům používat v nastavení zařízení možnost továrního obnovení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit použít toto nastavení na zařízení.
- **Bezpečné spuštění**: **blok** zabraňuje uživatelům v restartování zařízení v nouzovém režimu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit restartovat zařízení v nouzovém režimu.
- **Stavový řádek**: **blok** zabraňuje přístupu ke stavovým řádku, včetně oznámení a rychlých nastavení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit přístup ke stavovým řádkům.
- **Roamingové datové služby**: **blokování** brání datovým roamingu v mobilní síti. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat datový roaming, když je zařízení v mobilní síti.
- **Změny nastavení sítě Wi-Fi**: **blok** zabraňuje uživatelům měnit nastavení Wi-Fi vytvořená vlastníkem zařízení. Uživatelé můžou vytvářet své vlastní konfigurace Wi-Fi. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit změnit nastavení Wi-Fi na zařízení.
- **Konfigurace přístupového bodu sítě Wi-Fi**: **blok** znemožní uživatelům vytvářet nebo měnit jakékoli konfigurace Wi-Fi. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit změnit nastavení Wi-Fi na zařízení.
- **Konfigurace Bluetooth**: **blok** znemožní uživatelům konfigurovat Bluetooth na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na zařízení používat Bluetooth.
- **Sdílení a přístup k hotspotům**: **blok** znemožňuje sdílení a přístup k přenosným hotspotům. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat sdílení a přístup k přenosným hotspotům.
- **Úložiště USB**: vyberte možnost **povoluje** přístup k úložišti USB na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit přístupu k úložišti USB.
- **Přenos souborů USB**: **blok** zabraňuje přenosu souborů přes USB. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přenos souborů.
- **Externí média**: **blok** zabraňuje použití nebo připojení libovolného externího média na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na zařízení umožňovat externí média.
- **Data ze nosníku pomocí NFC**: **blok** zabraňuje použití technologie NFC (Near Field Communication) pro světlou dat z aplikací. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém standardně umožňovat sdílení dat mezi zařízeními pomocí technologie NFC.
- **Funkce ladění**: Pokud chcete, aby uživatelé mohli používat funkce ladění na zařízení, vyberte **Povolit** . Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit uživatelům v používání funkcí ladění na zařízení.
- **Úpravy mikrofonu**: **blok** zabraňuje uživatelům v odztlumení mikrofonu a nastavení hlasitosti mikrofonu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby na zařízení používali a upravili hlasitost mikrofonu.
- E- **maily pro obnovení továrního nastavení**: zvolit **e-mailové adresy účtu Google** Zadejte e-mailové adresy správců zařízení, které můžou zařízení odemknout po jeho vymazání. Tyto e-mailové adresy oddělujte středníkem, například `admin1@gmail.com;admin2@gmail.com` . Pokud nezadáte e-mail, může kdokoli zařízení po obnovení do továrního nastavení odemknout. Tyto e-maily se použijí jenom v případě, že se spustí obnovení z výroby bez uživatele, jako je třeba spuštění obnovení továrního nastavení pomocí nabídky obnovení.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

- **Únikovou řídicí znak sítě**: **možnost Povolit** uživatelům umožní zapnout funkci úniku řídicích panelů sítě. Pokud se po spuštění zařízení nevytvoří síťové připojení, pak se řídicí šrafování vyzve k dočasnému připojení k síti a aktualizaci zásad zařízení. Po uplatnění zásad se tato dočasná síť zapomene a zařízení pokračuje ve spouštění. Tato funkce připojuje zařízení k síti, pokud:
  - V poslední zásadě není vhodná síť.
  - Zařízení se spustí do aplikace v režimu uzamčení úlohy.
  - Uživatelé nemůžou kontaktovat nastavení zařízení.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit uživatelům v zapínání řídicích funkcí v síti v zařízení.

- **Aktualizace systému**: vyberte možnost pro definování způsobu, jakým zařízení zpracovává aktualizace přes Air. Vaše možnosti
  - **Výchozí ze zařízení**: Použije se výchozí nastavení zařízení.
  - **Automaticky**: Aktualizace se instalují automaticky bez zásahu uživatele. Po nastavení této zásady se hned nainstalují všechny čekající aktualizace.
  - **Odloženo**: Aktualizace se odloží o 30 dní. Po uplynutí 30 dnů vyzve Android uživatele k instalaci aktualizace. Výrobci zařízení nebo mobilní operátoři mohou zakázat (vyloučit) odklad důležitých aktualizací zabezpečení. Vyloučená aktualizace zobrazuje systémová oznámení pro uživatele na zařízení.
  - **Časové období údržby**: Aktualizace se instalují automaticky během časového období údržby, které nastavíte v Intune. Instalace probíhá denně po dobu 30 dnů a může selhat, pokud není dostatek místa nebo úrovně baterie. Po 30 dnech systém Android vyzve uživatele k instalaci. Toto okno se také používá k instalaci aktualizací aplikací Play. Tuto možnost použijte pro vyhrazená zařízení, jako jsou veřejné terminály, protože je možné aktualizovat aplikace v popředí vyhrazené pro jednotlivé aplikace.

- **Okna oznámení**: Pokud je nastavení **zakázané**, oznámení oken, včetně informačních zpráv, příchozích volání, odchozích volání, systémových výstrah a systémových chyb, se na zařízení nezobrazují. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazovat oznámení.
- **Přeskočit první tipy k použití**: **Povolit** skryje nebo přeskočí návrhy z aplikací, které procházejí kurzy, nebo když se aplikace spustí. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tyto návrhy zobrazit při spuštění aplikace.

### <a name="system-security"></a>Zabezpečení systému

- **Kontrola hrozeb v aplikacích**: **vyžadovat** (výchozí) umožňuje Google Play chránit před instalací a po jejich instalaci. Pokud zjistí hrozbu, může upozornit uživatele na odebrání aplikace ze zařízení. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje. Ve výchozím nastavení operační systém nemusí povolit nebo spustit Google Play chránit pro prohledávání aplikací.

### <a name="dedicated-devices"></a>Vyhrazená zařízení

Pomocí těchto nastavení můžete nakonfigurovat možnosti veřejného terminálu na vyhrazených zařízeních. Můžete nakonfigurovat zařízení tak, aby spouštěla jednu aplikaci nebo spouštěla spoustu aplikací. Když je zařízení nastavené s beznabídkovým režimem, k dispozici jsou jenom aplikace, které přidáte. Tato nastavení platí pro zařízení s Androidem Enterprise vyhrazená. Nevztahují se na zařízení s plně spravovaným systémem Android Enterprise.

**Celoobrazovkový režim**: vyberte, jestli má zařízení spuštěnou jednu aplikaci, nebo spustí víc aplikací.

- **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
- **Jediná aplikace**: uživatelé mají přístup jenom k jedné aplikaci na zařízení. Po spuštění zařízení se spustí jenom konkrétní aplikace. Uživatelé nemůžou otevírat nové aplikace ani měnit spuštěnou aplikaci.

  - **Vyberte spravovanou aplikaci**: ze seznamu vyberte spravovanou aplikaci Google Play.

    Pokud nemáte uvedené žádné aplikace, přidejte do zařízení [některé aplikace pro Android](../apps/apps-add-android-for-work.md) . Nezapomeňte [aplikaci přiřadit ke skupině zařízení vytvořené pro vaše vyhrazená zařízení](../apps/apps-deploy.md).

  > [!IMPORTANT]
  > Pokud používáte celoobrazovkový režim s jednou aplikací, aplikace Dial/Phone nemusí správně fungovat.
  
- **Multi-aplikace**: uživatelé mají přístup k omezené sadě aplikací na zařízení. Po spuštění zařízení se spustí jenom aplikace, které přidáte. Můžete také přidat některé webové odkazy, které mohou uživatelé otevřít. Když se zásada použije, uživatelé uvidí na domovské obrazovce ikony povolených aplikací.

  > [!IMPORTANT]
  > U vyhrazených zařízení s více aplikacemi **musí být** [aplikace spravované domovské obrazovky](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise) z Google Play:
  >   - [Přidáno jako klientská aplikace](../apps/apps-add-android-for-work.md) v Intune
  >   - [Přiřazeno ke skupině zařízení](../apps/apps-deploy.md) vytvořené pro vyhrazená zařízení
  >
  > Aplikace **spravované domovské obrazovky** nemusí být v konfiguračním profilu, ale je nutné ji přidat jako klientskou aplikaci. Když se **spravovaná aplikace pro domovskou obrazovku** přidá jako klientská aplikace, všechny ostatní aplikace, které přidáte do konfiguračního profilu, se zobrazí jako ikony v aplikaci **spravované domovské obrazovky** .
  >
  > Při použití celoobrazovkového režimu s více aplikacemi nemusí aplikace Dial/Phone fungovat správně. 

  - **Přidat**: vyberte své aplikace ze seznamu.

    Pokud není uvedená aplikace **spravované na domovské obrazovce** , [přidejte ji z Google Play](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise). Nezapomeňte [aplikaci přiřadit](../apps/apps-deploy.md) ke skupině zařízení vytvořené pro vaše vyhrazená zařízení.

    Do zařízení můžete přidat i další [aplikace pro Android](../apps/apps-add-android-for-work.md) a [webové aplikace](../apps/web-app.md) , které vytvořila vaše organizace. Nezapomeňte [aplikaci přiřadit ke skupině zařízení vytvořené pro vaše vyhrazená zařízení](../apps/apps-deploy.md).

  - **Tlačítko virtuální domů**: tlačítko měkkého klíče, které vrátí uživatele do spravované domovské obrazovky, aby uživatelé mohli přepínat mezi aplikacemi. Možnosti:

    - **Nenakonfigurováno** (výchozí): tlačítko domů není zobrazeno. Uživatelé musí použít tlačítko zpět k přepínání mezi aplikacemi.
    - **Potažení nahoru**: na domovském tlačítku se zobrazí, když uživatel na zařízení potáhne.
    - **Float**: zobrazuje na zařízení trvalé a plovoucí tlačítko domů.

  - **Opustit celoobrazovkový režim**: **Povolit** umožňuje správcům dočasně pozastavit celoobrazovkový režim a aktualizovat zařízení. Chcete-li použít tuto funkci, správce:
  
    1. Pokračuje v výběru tlačítka zpět, dokud se nezobrazí tlačítko **ukončit veřejný terminál** . 
    2. Vybere tlačítko **ukončit veřejný terminál** a přejde do kódu PIN pro **celoobrazovkový režim** .
    3. Po dokončení vyberte aplikaci **spravovaná domovskou obrazovku** . Tento krok znovu zamkne zařízení do celoobrazovkového režimu s více aplikacemi.

      Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit správcům v pozastavení celoobrazovkového režimu. Pokud správce pokračuje v výběru tlačítka zpět a vybere tlačítko **ukončit veřejný terminál** , pak se zobrazí zpráva, že je vyžadováno heslo.

    - **Opustit beznabídkový režim**: zadejte číslici a kód PIN pro číslo 4-6. Správce použije tento PIN kód k dočasnému pozastavení celoobrazovkového režimu.

  - **Nastavit vlastní adresu URL pozadí**: zadejte adresu URL pro přizpůsobení obrazovky na pozadí na vyhrazeném zařízení. Zadejte například `http://contoso.com/backgroundimage.jpg`.

    > [!NOTE]
    > Ve většině případů doporučujeme začít s imagemi alespoň následujících velikostí:
    >
    > - Telefon: 1080x1920 px
    > - Tablet: 1080 px
    >
    > Pro dosažení co nejlepších výsledků a zaostření podrobností je navrženo, že se pro jednotlivé položky obrázku zařízení vytvořily specifikace zobrazení.
    >
    > Moderní displeje mají vyšší hustotu pixelů a můžou zobrazovat ekvivalentní image definice 2K/4K.

  - **Konfigurace Wi-Fi**: **možnost Povolit** zobrazí ovládací prvek Wi-Fi na spravované domovské obrazovce a umožňuje uživatelům připojit zařízení k různým sítím Wi-Fi. Povolením této funkce se taky zapne umístění zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí na spravované domovské obrazovce zobrazit ovládací prvek Wi-Fi. Zabraňuje uživatelům v připojení k sítím Wi-Fi při použití spravované domovské obrazovky.

  - **Konfigurace Bluetooth**: **Povolit** zobrazí ovládací prvek Bluetooth na spravované domovské obrazovce a umožní uživatelům párovat zařízení přes Bluetooth. Povolením této funkce se taky zapne umístění zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení se operační systém nemusí na spravované domovské obrazovce zobrazovat na ovládacím prvku Bluetooth. Brání tak uživatelům v konfiguraci zařízení Bluetooth a párování zařízení při použití spravované domovské obrazovky.

  - **Svítící Access**: **Enable** zobrazí ovládací prvek svítící na spravované domovské obrazovce a umožňuje uživatelům zapnout nebo vypnout svítící. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení se operační systém nemusí na spravované domovské obrazovce zobrazovat na ovládacím prvku svítící. Zabraňuje uživatelům v používání svítící při použití spravované domovské obrazovky.

  - **Ovládání hlasitosti médií**: **Povolit** zobrazí ovládací prvek hlasitost média na spravované domovské obrazovce a umožňuje uživatelům upravit hlasitost média zařízení pomocí posuvníku. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení se operační systém nemusí na spravované domovské obrazovce zobrazovat na ovládacím prvku Media Volume Control. Zabraňuje uživatelům upravovat hlasitost médií zařízení při použití spravované domovské obrazovky, pokud jim jejich hardwarová tlačítka nepodporují.

  - **Režim spořiče obrazovky**: **možnost Povolit** zobrazí na spravované domovské obrazovce spořič obrazovky, když je zařízení uzamčeno nebo vypršel časový limit. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení se v operačním systému na spravované domovské obrazovce nemusí zobrazovat spořič obrazovky.

    Pokud je tato možnost povolená, nakonfigurujte taky:

    - **Nastavit vlastní obrázek spořiče obrazovky**: zadejte adresu URL pro vlastní PNG, jpg, JPEG, GIF, BMP, WEBP nebo ICOimage. Zadejte například .

      - `http://www.contoso.com/image.jpg`
      - `www.contoso.com/image.bmp`
      - `https://www.contoso.com/image.webp`

      Pokud adresu URL nezadáte, použije se výchozí image zařízení, pokud je k dispozici výchozí image.

      > [!TIP]
      > Je podporována jakákoli adresa URL prostředku souboru, která může být převedena do rastrového obrázku.

    - **Počet sekund, po které zařízení zobrazuje spořič obrazovky před**vypnutím obrazovky: vyberte, jak dlouho zařízení zobrazí spořič obrazovky. Zadejte hodnotu v rozmezí 0-9999999 sekund. Výchozí hodnota je `0` sekund. Pokud je ponecháno prázdné nebo je nastaveno na hodnotu nula ( `0` ), je spořič obrazovky aktivní, dokud uživatel nekomunikuje se zařízením.
    - **Počet sekund neaktivních zařízení před zobrazením spořiče obrazovky**: vyberte, jak dlouho bude zařízení nečinné, než se zobrazí. Zadejte hodnotu v rozmezí 1-9999999 sekund. Výchozí hodnota je `30` sekund. Je nutné zadat číslo větší než nula ( `0` ).
    - **Rozpoznat médium před spuštěním spořiče obrazovky**: **Povolit** (výchozí) nezobrazuje spořič obrazovky, pokud se na zařízení přehrává zvuk nebo video. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit spořič obrazovky i v případě, že přehrávání zvuku nebo videa.

### <a name="password"></a>Heslo

- **Zakázat zamykací obrazovku**: Pokud chcete zabránit uživatelům používat na zařízení funkci zámku zamykací obrazovky, vyberte **Zakázat** . Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožňovat použití funkcí ochrany před ochranou.
- **Zakázané funkce zamykací obrazovky**: Pokud je na zařízení povolená klávesa Guard, vyberte, které funkce se mají zakázat. Pokud je například zaškrtnuto políčko **Zabezpečená kamera** , funkce kamery je na zařízení zakázaná. Na zařízení jsou povolené všechny funkce, které nejsou zaškrtnuté.

  Tyto funkce jsou uživatelům k dispozici, když je zařízení zamčené. Uživatelům se nezobrazí nebo nebudou mít přístup k vybraným funkcím.

- **Vyžadovaný typ hesla**: zadejte požadovanou úroveň složitosti hesla a to, jestli se můžou používat biometrická zařízení. Možnosti:
  - **Výchozí ze zařízení**
  - **Vyžaduje se heslo, žádná omezení.**
  - **Slabý biometrika**: [silný vs. slabý biometrika](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (otevře web v Androidu)
  - **Číselná**: heslo musí obsahovat pouze čísla, například `123456789` . Dále zadejte:
    - **Minimální délka hesla**: zadejte minimální délku hesla, která musí být delší než 4 až 16 znaků.
  - **Číselná složitá**: opakující se nebo po sobě jdoucí čísla, například "1111" nebo "1234", nejsou povolena. Dále zadejte:
    - **Minimální délka hesla**: zadejte minimální délku hesla, která musí být delší než 4 až 16 znaků.
  - **Abecedy**: jsou vyžadovány písmena v abecedě. Čísla a symboly nejsou požadovány. Dále zadejte:
    - **Minimální délka hesla**: zadejte minimální délku hesla, která musí být delší než 4 až 16 znaků.
  - **Alfanumerické**znaky: obsahuje velká písmena, malá písmena a číslice. Dále zadejte:
    - **Minimální délka hesla**: zadejte minimální délku hesla, která musí být delší než 4 až 16 znaků.
  - **Alfanumerické znaky se symboly**: zahrnují velká písmena, malá písmena, číslice, interpunkční znaménka a symboly. Dále zadejte:

    - **Minimální délka hesla**: zadejte minimální délku hesla, která musí být delší než 4 až 16 znaků.
    - **Požadovaný počet znaků**: zadejte počet znaků, které musí heslo obsahovat, a to v rozmezí 0 až 16 znaků.
    - **Počet požadovaných malých**písmen: zadejte počet malých písmen, které musí heslo obsahovat, a to v rozmezí 0 až 16 znaků.
    - **Počet požadovaných velkých znaků**: zadejte počet velkých písmen, které musí heslo obsahovat, a to v rozmezí 0 až 16 znaků.
    - **Počet požadovaných znaků bez**písmen: zadejte počet jiných než písmen (kromě písmen v abecedě), které musí heslo obsahovat, 0 až 16 znaků.
    - **Požadovaný počet**číslic: zadejte počet číselných znaků ( `1` , `2` , `3` atd.), které musí heslo obsahovat, a to v rozmezí 0 až 16 znaků.
    - **Požadovaný počet znaků symbolů**: zadejte počet znaků symbolu (,, atd `&` `#` `%` .), které musí heslo obsahovat, 0 až 16 znaků.

- **Počet dní do vypršení platnosti hesla**: zadejte počet dní, než bude nutné změnit heslo zařízení, od 1-365. Zadejte například `90` platnost hesla po 90 dnech. Po vypršení platnosti hesla se uživatelům zobrazí výzva k vytvoření nového hesla. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Počet hesel vyžadovaných před opětovným použitím hesla uživatelem**: Toto nastavení použijte, pokud chcete uživatelům zabránit ve vytváření hesel, která používali dřív. Zadejte počet dříve použitých hesel, která se nedají použít, od 1-24. Například zadejte, `5` že uživatelé nemůžou nastavit nové heslo na aktuální heslo ani na žádná z předchozích čtyř hesel. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Počet neúspěšných přihlášení před vymazáním zařízení**: zadejte počet chybných hesel povolených před vymazáním zařízení, od 4-11. `0`(nula) může zakázat funkci vymazání zařízení. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.

  > [!NOTE]
  > Zařízení vlastníka zařízení nebudou vyzvána k nastavení hesla. Nastavení se vynutilo a budete muset heslo nastavit ručně. Zásady, které vynucují tuto zásadu, budou hlásit jako neúspěšné, dokud nenastavíte heslo, které vyhovuje vašim požadavkům.

### <a name="power-settings"></a>Nastavení napájení

- **Čas na zamykací obrazovku**: zadejte maximální dobu, kterou může uživatel nastavit, dokud se zařízení nezamkne. Pokud například nastavíte toto nastavení na `10 minutes` , uživatelé můžou nastavit čas od 15 sekund až po 10 minut. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

- **Zapnutá obrazovka, když se zařízení napájí ze sítě**: Zvolte zdroje napájení, při jejichž použití zůstane obrazovka zařízení zapnutá.

### <a name="users-and-accounts"></a>Uživatelé a účty

- **Přidat nové uživatele**: **blokování** brání uživatelům v přidávání nových uživatelů. Každý uživatel má v zařízení osobní místo pro vlastní domovské obrazovky, účty, aplikace a nastavení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit přidat další uživatele do zařízení.
- **Odebrání uživatele**: **blok** zabraňuje uživatelům v odebírání uživatelů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby ze zařízení odstranili jiné uživatele.
- **Změny účtu** (jenom vyhrazená zařízení): **blok** brání uživatelům v úpravách účtů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit aktualizovat uživatelské účty v zařízení.

  > [!NOTE]
  > Toto nastavení se nedodržuje u zařízení vlastníka zařízení (plně spravovaná). Pokud toto nastavení nakonfigurujete, nastavení se ignoruje a nemá žádný vliv.

- **Uživatel může nakonfigurovat přihlašovací údaje**: **blok** znemožní uživatelům konfigurovat certifikáty přiřazené k zařízením, dokonce i zařízení, která nejsou přidružená k uživatelskému účtu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožnit uživatelům konfigurovat nebo měnit své přihlašovací údaje, když k nim přistupují v úložišti klíčů.
- **Osobní účty Google**: **blok** zabraňuje uživatelům v přidávání osobního účtu Google do zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit přidat svůj osobní účet Google.

### <a name="applications"></a>Aplikace

- **Povolit instalaci z neznámých zdrojů**: **Povolit** umožňuje uživatelům zapnout **neznámé zdroje**. Toto nastavení umožňuje aplikacím instalovat z neznámých zdrojů, včetně jiných zdrojů než Obchod Google Play. Umožňuje uživatelům načítat aplikace na zařízení pomocí jiných prostředků než Obchod Google Play. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit uživatelům v zapnutí **neznámých zdrojů**.
- **Povolení přístupu ke všem aplikacím v Google Play Storu**: Pokud je nastavení **povolené**, uživatelé získají přístup ke všem aplikacím v obchodě Google Play Store. Nezískají přístup k aplikacím, které správce zablokuje v [klientských aplikacích](../apps/apps-add-android-for-work.md).

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém:
  
  - Přinutí uživatelům přístup jenom k aplikacím, které správce zpřístupní v Google Play Storu, nebo aplikace vyžadované v [klientských aplikacích](../apps/apps-add-android-for-work.md). 
  - Automaticky odinstalujte všechny aplikace zjištěné jako nainstalované uživateli mimo Google Play Store.

  Pokud chcete povolit souběžné načítání, nastavte možnost **Povolit instalaci z neznámých zdrojů** a **povolte přístup ke všem aplikacím v** nastavení služby Google Play Store **Povolit**.

- **Automatické aktualizace aplikací**: zařízení kontrolují aktualizace aplikací denně. Vyberte, kdy se mají nainstalovat automatické aktualizace. Možnosti:
  - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje.
  - **Volba uživatele**: operační systém může tuto možnost výchozí. Uživatelé můžou nastavit své předvolby v aplikaci Managed Google Play.
  - **Nikdy**: aktualizace nejsou nikdy nainstalovány. Tato možnost se nedoporučuje.
  - **Jenom Wi-Fi**: aktualizace se nainstalují jenom v případě, že je zařízení připojené k síti Wi-Fi.
  - **Always**: aktualizace se instalují, když jsou k dispozici.

### <a name="connectivity"></a>Připojení

- **Vždy zapnutá síť VPN**: **možnost Povolit** nastaví klienta VPN tak, aby se automaticky připojoval a znovu připojil k síti VPN. Připojení k síti VPN Always On zůstane připojené. Nebo se okamžitě připojí, když uživatelé uzamkne zařízení, dojde k restartování zařízení nebo ke změně bezdrátové sítě.

  Výběrem možnosti **Nenakonfigurováno** zakažte neustále aktivní připojení VPN pro všechny klienty VPN.

  > [!IMPORTANT]
  > Nezapomeňte nasadit jenom jednu zásadu trvalého připojení k síti VPN na jedno zařízení. Nasazení několika zásad trvalého připojení k síti VPN na jedno zařízení se nepodporuje.

- **Klient VPN**: vyberte klienta VPN, který podporuje neustále aktivní připojení VPN. Možnosti:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Vlastní
    - **ID balíčku**: zadejte ID balíčku aplikace v obchodu Google Play. Pokud je například adresa URL aplikace v obchodu Play `https://play.google.com/store/details?id=com.contosovpn.android.prod`, potom je ID balíčku `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - Klient VPN, kterého zvolíte, musí být nainstalovaný na zařízení a musí podporovat VPN pro jednotlivé aplikace v pracovních profilech. V opačném případě dojde k chybě. 
  > - Aplikaci klienta VPN je potřeba schválit ve **spravovaném obchodu Google Play**, synchronizovat ji do Intune a nasadit ji do zařízení. Až to vše uděláte, bude aplikace nainstalovaná v pracovním profilu uživatele.
  > - Pořád musíte nakonfigurovat klienta VPN s [profilem sítě VPN](vpn-settings-android-enterprise.md)nebo prostřednictvím [konfiguračního profilu aplikace](../apps/app-configuration-policies-use-android.md).
  > - Při použití sítě VPN pro aplikaci s přístupem F5 pro Android 3.0.4 můžou nastat známé problémy. Další informace najdete v tématu [poznámky k verzi F5's pro přístup F5 pro Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Režim uzamčení**: **Povolit** u všech síťových přenosů, aby používaly tunelové propojení VPN. Pokud připojení k VPN není vytvořené, potom nebude mít zařízení přístup k síti. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přenos přes tunelové připojení VPN nebo přes mobilní síť.

- **Doporučený globální proxy server**: **možnost Povolit** přidá do zařízení globální proxy server. Pokud je povolený přenos přes protokol HTTP a HTTPS, včetně některých aplikací v zařízení, použijte proxy, který zadáte. Tato proxy je jenom doporučení. Je možné, že některé aplikace nepoužívají proxy server. **Nenakonfigurováno** (výchozí) nepřidá doporučený globální proxy server.

  Další informace o této funkci najdete v tématu [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (otevře web s Androidem).

  Pokud je povoleno, zadejte také **typ** proxy serveru. Možnosti:

  - **Direct**: zadejte informace o proxy server ručně, včetně:
    - **Hostitel**: zadejte název hostitele nebo IP adresu vašeho proxy server. Zadejte například `proxy.contoso.com` nebo `127.0.0.1`.
    - **Číslo portu**: zadejte číslo portu TCP používaného proxy server. Zadejte například `8080`.
    - **Vyloučení hostitelé**: Zadejte seznam názvů hostitelů nebo IP adres, které nepoužívají proxy server. Tento seznam může obsahovat zástupný znak hvězdičky ( `*` ) a několik hostitelů oddělených středníky ( `;` ) bez mezer. Zadejte například `127.0.0.1;web.contoso.com;*.microsoft.com`.

  - **Automatická konfigurace proxy serveru**: zadejte **adresu URL PAC** do skriptu pro automatickou konfiguraci proxy serveru. Zadejte například `https://proxy.contoso.com/proxy.pac`.

    Další informace o souborech PAC najdete v tématu [soubor automatické konfigurace proxy serveru](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (otevře se na webu, který není Microsoft).

  Další informace o této funkci najdete v tématu [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (otevře web s Androidem).

## <a name="work-profile-only"></a>Pouze pracovní profil

Tato nastavení se vztahují na typy registrace Androidu Enterprise, kde Intune řídí jenom pracovní profil, jako je například registrace v systému Android Enterprise Worker na osobním zařízení (BYOD).

### <a name="work-profile-settings"></a>Nastavení pracovního profilu

- **Kopírování a vkládání mezi pracovními a osobními profily**: **blok** zabraňuje kopírování a vkládání mezi pracovními a osobními aplikacemi. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit sdílet data pomocí kopírování a vkládání s aplikacemi v osobním profilu.
- **Sdílení dat mezi pracovními a osobními profily**: vyberte, jestli aplikace v pracovním profilu můžou sdílet s aplikacemi v osobním profilu. Můžete například řídit akce sdílení v aplikacích, jako je například **sdílená složka...** v aplikaci prohlížeče Chrome. Toto nastavení se nevztahuje na chování schránky při kopírování/vkládání. Možnosti:
  - **Výchozí nastavení zařízení**: výchozí chování zařízení při sdílení, které se liší v závislosti na verzi Androidu. Ve výchozím nastavení je povolené sdílení z osobního profilu do pracovního profilu. Ve výchozím nastavení je také blokované sdílení z pracovního profilu do osobního profilu. Toto nastavení zabraňuje sdílení dat z pracovního do osobního profilu. Google neblokuje sdílení z osobního do pracovního profilu na zařízeních, která používají verze 6.0 a novější.
  - **Zabránit jakémukoli sdílení přes hranice**: zabraňuje sdílení mezi pracovními a osobními profily.
  - **Aplikace v pracovním profilu můžou zpracovat žádost o sdílení z osobního profilu**: povoluje integrovanou funkci Androidu, která umožňuje sdílet data z osobního do pracovního profilu. Pokud je tato možnost povolená, žádost o sdílení z aplikace v osobním profilu může sdílet data s aplikacemi v pracovním profilu. Toto nastavení je výchozí chování zařízení s Androidem, která používají verze starší než 6.0.
  - **Žádná omezení sdílení**: umožňuje sdílení přes hranice pracovního profilu v obou směrech. Když vyberete toto nastavení, můžou aplikace v pracovním profilu sdílet data s neoznačenými aplikacemi v osobním profilu. Toto nastavení povoluje spravovaným aplikacím v pracovním profilu sdílení s aplikacemi v nespravované oblasti zařízení. Proto ho používejte opatrně.

- **Oznámení pracovního profilu, když je zařízení zamknuté**: **blok** zabraňuje oznámením oken, včetně informačních zpráv, příchozích volání, odchozích volání, výstrah systému a systémových chyb, které se zobrazují na zamčených zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazovat oznámení.
- **Výchozí oprávnění aplikace**: umožňuje nastavit zásady výchozích oprávnění pro všechny aplikace v pracovním profilu. Od Androidu 6 se uživatelům zobrazí výzva, aby při spuštění aplikace udělila určitá oprávnění požadovaná aplikacemi. Nastavení této zásady vám umožňuje určit, jestli se uživatelům zobrazí výzva k udělení oprávnění všem aplikacím v pracovním profilu. Můžete například přiřadit do pracovního profilu aplikaci, která vyžaduje přístup k poloze. Obvykle aplikace vyzývá uživatele ke schválení nebo zamítnutí přístupu k poloze aplikace. Pomocí této zásady můžete automaticky udělit oprávnění bez výzvy, automaticky odepřít oprávnění bez výzvy nebo se uživatelé můžou rozhodnout. Možnosti:
  - **Výchozí ze zařízení**
  - **Výzva**
  - **Automaticky udělit**
  - **Automaticky odepřít**

  Zásady konfigurace aplikací můžete použít také k udělení oprávnění pro jednotlivé aplikace (**Client Apps**  >  **zásady konfigurace aplikací**klientských aplikací).

- **Přidat a odebrat účty**: **blok** zabraňuje uživatelům v ručním přidávání a odebírání účtů v pracovním profilu. Pokud například nasadíte aplikaci Gmail do pracovního profilu Android, můžete uživatelům zabránit v přidávání a odebírání účtů v tomto pracovním profilu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém přidávat účty v pracovním profilu.  

  > [!NOTE]
  > Účty Google se nedají přidat do pracovního profilu.

- **Sdílení kontaktů přes Bluetooth**: **Povolit** umožňuje sdílení a přístup k kontaktům pracovního profilu z jiného zařízení, včetně auta, které se spáruje pomocí Bluetooth. Když toto nastavení povolíte, budou určitá zařízení Bluetooth ukládat pracovní kontakty do mezipaměti při prvním připojení. V případě jejího zakázání po počátečním zpárování/synchronizaci se pracovní kontakty ze zařízení Bluetooth nemusí odstranit.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí sdílet pracovní kontakty.

  Toto nastavení platí pro:

  - Zařízení pracovní profil Androidu, na kterých běží Android OS v 6.0 a novější

- **Snímek obrazovky**: Block zabraňuje tomu, aby se snímky obrazovky nebo snímky na zařízení v pracovním profilu **zablokovaly** . Brání tím také zobrazení obsahu na zobrazovacích zařízeních, která nemají bezpečný výstup videa. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém získat snímky obrazovky.

- **Zobrazit ID volajícího pracovního kontaktu v osobním profilu**: **blok** nezobrazuje číslo volajícího pracovního kontaktu v osobním profilu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit podrobnosti o volajícím pracovních kontaktů.

  Toto nastavení platí pro:

  - Android OS v 6.0 a novější verze

- **Hledat pracovní kontakty z osobního profilu**: **blok** znemožní uživatelům vyhledávat pracovní kontakty v aplikacích v osobním profilu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat hledání pracovních kontaktů v osobním profilu.

- **Kamera**: **Block** zabrání přístupu k fotoaparátu na zařízení v pracovním profilu. Nastavení nemá vliv na kameru v osobním profilu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k fotoaparátu.

- **Povolit widgety z pracovních profilů aplikace**: **možnost Povolit** umožňuje uživatelům vkládat widgety na domovské obrazovce pomocí aplikací. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci zakázat.

  Například Outlook se nainstaluje do pracovních profilů uživatelů. Když je tato možnost nastavená na **Povolit**, můžou uživatelé na domovské obrazovce zařízení umístit widget agendy.

- **Vyžadovat heslo pracovního profilu**: **vyžadovat** vynutí zásadu hesla, která se vztahuje pouze na aplikace v pracovním profilu. Ve výchozím nastavení mohou uživatelé použít dva samostatně definované PIN kódy. Nebo uživatelé můžou kombinovat PIN kódy do silnějšího z těchto kódů PIN. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby používali pracovní aplikace bez zadání hesla.

  Toto nastavení platí pro:

  - Android 7,0 a novější s povoleným pracovním profilem

- **Minimální délka hesla**: zadejte minimální délku hesla, která musí být delší než 4 až 16 znaků.
- **Maximální počet minut nečinnosti, po kterém se zamkne pracovní profil**: zadejte dobu, po kterou musí být zařízení nečinné, než se automaticky uzamkne obrazovka. Uživatelé musí zadat své přihlašovací údaje, aby získali přístup. Zadejte například, `5` Pokud chcete zařízení uzamknout po 5 minutách nečinnosti. Když je hodnota prázdná nebo nastavená na **nenakonfigurovaná**, Intune se nezmění ani neaktualizuje.

  V zařízeních uživatelé nemůžou nastavit časovou hodnotu větší než nakonfigurovanou dobu v profilu. Uživatelé můžou nastavit nižší časovou hodnotu. Pokud je profil nastavený například na `15` minuty, uživatelé můžou hodnotu nastavit na 5 minut. Uživatelé nemůžou hodnotu nastavit na 30 minut.

- **Počet neúspěšných přihlášení před vymazáním zařízení**: zadejte počet chybných hesel povolených před vymazáním zařízení, od 4-11. `0`(nula) může zakázat funkci vymazání zařízení. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.

- **Vypršení platnosti hesla (dny)**: zadejte počet dní, než se musí změnit uživatelská hesla (od **1** - **365**).
- **Vyžadovaný typ hesla**: zadejte požadovanou úroveň složitosti hesla a to, jestli se můžou používat biometrická zařízení. Možnosti:
  - **Výchozí ze zařízení**
  - **Biometrika s nízkou úrovní zabezpečení**: [silný vs. slabý biometrika](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (otevře web v Androidu)
  - **Požadováno**
  - **Aspoň číslice**: obsahuje číselné znaky, například `123456789` .
  - **Číselná složitá**: opakující se nebo po sobě jdoucí čísla, například `1111` nebo `1234` , nejsou povolena.
  - **Aspoň abecední**znaky: obsahuje písmena v abecedě. Čísla a symboly nejsou požadovány.
  - **Aspoň alfanumerické**znaky: obsahuje velká písmena, malá písmena a číslice.
  - **Aspoň alfanumerické se symboly**: obsahuje velká písmena, malá písmena, číslice, interpunkční znaménka a symboly.

- **Zakázat opakované použití předchozích hesel**: pomocí tohoto nastavení můžete uživatelům zabránit ve vytváření hesel, která používali dřív. Zadejte počet dříve použitých hesel, která se nedají použít, od 1-24. Například zadejte, `5` že uživatelé nemůžou nastavit nové heslo na aktuální heslo ani na žádná z předchozích čtyř hesel. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Odemknutí otiskem prstu**: **blok** znemožní uživatelům používat skener otisků prstů zařízení k odemknutí zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby zařízení odemkli pomocí otisku prstu.
- **Smart Lock a jiní agenti**pro určování důvěryhodnosti: **blok** brání Smart Lock nebo jiným agentům pro určování důvěryhodnosti v nastavení zamykací obrazovky na kompatibilních zařízeních. Pokud jsou zařízení v důvěryhodném umístění, pak tato funkce, označovaná také jako agent pro určování důvěryhodnosti, umožňuje zakázat nebo obejít heslo zamykací obrazovky zařízení. Můžete například obejít heslo pracovního profilu, když jsou zařízení připojená k určitému zařízení Bluetooth nebo když jsou zařízení blízko značky NFC. Pomocí tohoto nastavení můžete uživatelům zabránit v konfiguraci funkce Smart Lock.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

### <a name="password"></a>Heslo

Tato nastavení hesla platí pro osobní profily na zařízeních, která používají pracovní profil.

- **Minimální délka hesla**: zadejte minimální délku hesla, která musí být delší než 4 až 16 znaků.
- **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka**: zadejte dobu, po kterou musí být zařízení nečinné, než se obrazovka automaticky zamkne. Uživatelé musí zadat své přihlašovací údaje, aby získali přístup. Zadejte například, `5` Pokud chcete zařízení uzamknout po 5 minutách nečinnosti. Když je hodnota prázdná nebo nastavená na **nenakonfigurovaná**, Intune se nezmění ani neaktualizuje.

  V zařízeních uživatelé nemůžou nastavit časovou hodnotu větší než nakonfigurovanou dobu v profilu. Uživatelé můžou nastavit nižší časovou hodnotu. Pokud je profil nastavený například na `15` minuty, uživatelé můžou hodnotu nastavit na 5 minut. Uživatelé nemůžou hodnotu nastavit na 30 minut.

- **Počet neúspěšných přihlášení před vymazáním zařízení**: zadejte počet chybných hesel povolených před vymazáním zařízení, od 4-11. `0`(nula) může zakázat funkci vymazání zařízení. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Vypršení platnosti hesla (dny)**: zadejte počet dní, než bude nutné změnit heslo zařízení, od 1-365. Zadejte například `90` platnost hesla po 90 dnech. Po vypršení platnosti hesla se uživatelům zobrazí výzva k vytvoření nového hesla. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Vyžadovaný typ hesla**: zadejte požadovanou úroveň složitosti hesla a to, jestli se můžou používat biometrická zařízení. Možnosti:
  - **Výchozí ze zařízení**
  - **Biometrika s nízkou úrovní zabezpečení**: [silný vs. slabý biometrika](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (otevře web v Androidu)
  - **Požadováno**
  - **Aspoň číslice**: obsahuje číselné znaky, například `123456789` .
  - **Číselná složitá**: opakující se nebo po sobě jdoucí čísla, například `1111` nebo `1234` , nejsou povolena.
  - **Aspoň abecední**znaky: obsahuje písmena v abecedě. Čísla a symboly nejsou požadovány.
  - **Aspoň alfanumerické**znaky: obsahuje velká písmena, malá písmena a číslice.
  - **Aspoň alfanumerické se symboly**: obsahuje velká písmena, malá písmena, číslice, interpunkční znaménka a symboly.

- **Zakázat opakované použití předchozích hesel**: pomocí tohoto nastavení můžete uživatelům zabránit ve vytváření hesel, která používali dřív. Zadejte počet dříve použitých hesel, která se nedají použít, od 1-24. Například zadejte, `5` že uživatelé nemůžou nastavit nové heslo na aktuální heslo ani na žádná z předchozích čtyř hesel. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Odemknutí otiskem prstu**: **blok** znemožní uživatelům používat skener otisků prstů zařízení k odemknutí zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby zařízení odemkli pomocí otisku prstu.
- **Smart Lock a jiní agenti**pro určování důvěryhodnosti: **blok** brání Smart Lock nebo jiným agentům pro určování důvěryhodnosti v nastavení zamykací obrazovky na kompatibilních zařízeních. Pokud jsou zařízení v důvěryhodném umístění, pak tato funkce, označovaná také jako agent pro určování důvěryhodnosti, umožňuje zakázat nebo obejít heslo zamykací obrazovky zařízení. Můžete například obejít heslo pracovního profilu, když jsou zařízení připojená k určitému zařízení Bluetooth nebo když jsou zařízení blízko značky NFC. Pomocí tohoto nastavení můžete uživatelům zabránit v konfiguraci funkce Smart Lock.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

### <a name="system-security"></a>Zabezpečení systému

- **Kontrola hrozeb u aplikací**: **vyžaduje** vynucení, že nastavení **ověřování aplikací** je povolené pro pracovní a osobní profily. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  Toto nastavení platí pro:

  - Android 8 (Oreo) a vyšší

- **Zabránění instalaci aplikací z neznámých zdrojů v osobním profilu**: podle návrhu zařízení s Androidem Enterprise Work profilování nemůžou instalovat aplikace ze zdrojů, které nejsou obchod Play. Toto nastavení umožňuje správcům větší kontrolu nad instalací aplikací z neznámých zdrojů. **Blok** zabraňuje instalaci aplikací z jiných zdrojů než obchod Google Play v osobním profilu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat instalaci aplikací z neznámých zdrojů v osobním profilu. Zařízení pracovního profilu mají podle povahy možnost duální profil:

  - Pracovní profil spravovaný pomocí MDM.
  - Osobní profil, který je izolovaný od správy MDM.

### <a name="connectivity"></a>Připojení

- **Vždycky zapnutá síť VPN**: **Povolit** nastaví klienta VPN tak, aby se automaticky připojoval a znovu připojil k síti VPN. Připojení k síti VPN Always On zůstane připojené. Nebo se okamžitě připojí, když uživatelé uzamkne zařízení, dojde k restartování zařízení nebo ke změně bezdrátové sítě.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zakázat vždycky zapnutou síť VPN pro všechny klienty VPN.

  > [!IMPORTANT]
  > Ujistěte se, že na jedno zařízení nasadíte pouze jednu zásadu neustále aktivního připojení VPN. Nasazení více zásad neustále aktivního připojení VPN na jedno zařízení se nepodporuje.

- **Klient VPN**: vyberte klienta VPN, který podporuje neustále aktivní připojení VPN. Možnosti:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Vlastní
    - **ID balíčku**: zadejte ID balíčku aplikace v obchodu Google Play. Pokud je například adresa URL aplikace v obchodu Play `https://play.google.com/store/details?id=com.contosovpn.android.prod`, potom je ID balíčku `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - Klient VPN, kterého zvolíte, musí být nainstalovaný na zařízení a musí podporovat VPN pro jednotlivé aplikace v pracovních profilech. V opačném případě dojde k chybě.
  > - Aplikaci klienta VPN je potřeba schválit ve **spravovaném obchodu Google Play**, synchronizovat ji do Intune a nasadit ji do zařízení. Až to vše uděláte, bude aplikace nainstalovaná v pracovním profilu uživatele.
  > - Při použití sítě VPN pro aplikaci s přístupem F5 pro Android 3.0.4 můžou nastat známé problémy. Další informace najdete v [poznámkách k verzi F5's pro přístup F5 pro Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android) .

- **Režim uzamčení**: **Povolit** u všech síťových přenosů, aby používaly tunelové propojení VPN. Pokud připojení k VPN není vytvořené, potom nebude mít zařízení přístup k síti.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přenos přes tunelové připojení VPN nebo přes mobilní síť.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Pro zařízení s [Androidem](device-restrictions-android.md#kiosk) a [Windows 10](kiosk-settings.md) můžete také vytvořit profily pro celoobrazovkový terminály na vyhrazené zařízení.

[Konfigurace a řešení potíží se zařízeními s Androidem Enterprise v Microsoft Intune](https://support.microsoft.com/help/4476974).
