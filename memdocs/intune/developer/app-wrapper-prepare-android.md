---
title: Zabalení aplikací pro Android nástrojem Intune App Wrapping Tool
description: Naučte se balit aplikace pro Android beze změny samotného kódu aplikace. Připravte aplikace, abyste mohli použít zásady správy mobilních aplikací.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e9c349c8-51ae-4d73-b74a-6173728a520b
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6c0dab3c84e3a87048a8071c591722c63d89ad69
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078120"
---
# <a name="prepare-android-apps-for-app-protection-policies-with-the-intune-app-wrapping-tool"></a>Příprava aplikací pro Android na zásady ochrany aplikací pomocí nástroje Intune App Wrapping Tool

Pokud chcete změnit chování interních aplikací pro Android tím, že omezíte jejich funkce – beze změny samotného kódu aplikace – použijte nástroj Microsoft Intune App Wrapping Tool for Android.

Jde o nástroj příkazového řádku Windows, který běží v PowerShellu a který vytvoří okolo vaší aplikace pro Android obálku. Po zabalení aplikace můžete změnit funkčnost aplikace konfigurací [zásad správy mobilních aplikací](../apps/app-protection-policies.md) v Intune.

Před spuštěním nástroje si přečtěte část [Důležité informace o zabezpečení při spuštění nástroje App Wrapping Tool](#security-considerations-for-running-the-app-wrapping-tool). Nástroj si můžete stáhnout ze stránky [Microsoft Intune App Wrapping Tool for Android](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android) na GitHubu.

## <a name="fulfill-the-prerequisites-for-using-the-app-wrapping-tool"></a>Splnění požadavků používání nastroje App Wrapping

- Nástroj App Wrapping Tool je možné spustit na počítači se systémem Windows 7 nebo novějším.

- Vstupní aplikace musí být platný balíček aplikace pro Android, který má příponu souboru .apk a splňuje následující požadavky:

  - Nesmí být zašifrovaný.
  - Nesmí být už jednou zabalený nástrojem Intune App Wrapping Tool.
  - Musí být napsaný pro systém Android 4.0 nebo novější.

- Aplikaci musí vyvinout vaše společnost nebo je tato aplikace vyvinuta pro ni. Tento nástroj se nedá používat u aplikací stažených z obchodu Google Play.

- Chcete-li spustit nástroj pro zabalení aplikace, je třeba nainstalovat nejnovější verzi [Java Runtime Environment](https://java.com/download/) a poté zkontrolovat, zda byla proměnná cesty Java v proměnných prostředí systému Windows nastavena na hodnotu C:\ProgramData\Oracle\Java\javapath. Další nápovědu najdete v [dokumentaci k Javě](https://java.com/download/help/).

    > [!NOTE]
    > V některých případech může 32bitová verze Javy způsobit potíže s pamětí. Proto je vhodné nainstalovat 64bitovou verzi.

- Android vyžaduje, aby byly všechny balíčky aplikací (.apk) podepsané. Informace o **opětovném použití** existujících certifikátů a celkové pokyny k podpisovým certifikátům najdete v tématu [Opětovné použití podpisových certifikátů a balení aplikací](app-wrapper-prepare-android.md#reusing-signing-certificates-and-wrapping-apps). Ke generování **nových** přihlašovacích údajů potřebných k podpisu zabalené výstupní aplikace se používá spustitelný soubor Java keytool.exe. Nastavená hesla musí být bezpečná, ale nezapomeňte si je poznamenat, protože je budete potřebovat ke spuštění nástroje App Wrapping Tool.

    > [!NOTE]
    > Nástroj Intune App Wrapping Tool nepodporuje pro podepisování aplikací podpisová schémata v2 a nadcházející v3 od Googlu. Po zabalení souboru .apk pomocí nástroje Intune App Wrapping Tool se doporučuje použít [nástroj Apksigner od Googlu]( https://developer.android.com/studio/command-line/apksigner). Tím se zajistí, že když se vaše aplikace dostane na zařízení koncových uživatelů, bude ji možné spustit správně podle standardů Androidu. 

- Volitelné Někdy může aplikace dosáhnout limitu velikosti spustitelného souboru Dalvik (DEX), protože třídy sady Intune MAM SDK, které jsou přidány během zabalení. Soubory DEX jsou součástí kompilace aplikace pro Android. Nástroj pro zabalení aplikace Intune automaticky zpracovává přetečení souborů DEX při zabalení pro aplikace s minimální úrovní rozhraní API 21 nebo vyšší (jako [v. 1.0.2501.1](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android/releases)). Pro aplikace s minimální úrovní rozhraní API < 21 doporučujeme zvýšit minimální úroveň rozhraní API pomocí `-UseMinAPILevelForNativeMultiDex` příznaku obálky. Aby zákazníci nemohli zvýšit minimální úroveň rozhraní API aplikace, jsou k dispozici následující alternativní DEX přetečení. V některých organizacích to může vyžadovat spolupráci s tím, že aplikace kompiluje (tj. tým sestavení aplikace):

  - Pomocí ProGuard můžete eliminovat nepoužívané odkazy na třídy z primárního souboru DEX aplikace.
  - Pro zákazníky, kteří používají 3.1.0 nebo novější modul plug-in Android Gradle, zakažte [D8 dexer](https://android-developers.googleblog.com/2018/04/android-studio-switching-to-d8-dexer.html).  

## <a name="install-the-app-wrapping-tool"></a>Instalace nástroje App Wrapping Tool

1. Z [úložiště GitHubu](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android) si do počítače s Windows stáhněte instalační soubor InstallAWT.exe nástroje Intune App Wrapping Tool for Android. Otevřete instalační soubor.

2. Přijměte licenční smlouvu a dokončete instalaci.

Poznamenejte si složku, do které jste nainstalovali nástroj. Výchozí umístění je: C:\Program Files (x86)\Microsoft Intune Mobile Application Management\Android\App Wrapping Tool.

## <a name="run-the-app-wrapping-tool"></a>Spuštění nástroje App Wrapping Tool

1. Na počítači s Windows, na který jste nainstalovali nástroj App Wrapping Tool, otevřete okno PowerShell.

2. Ze složky, do které jste nástroj nainstalovali, naimportujte modul PowerShell nástroje App Wrapping Tool:

   ```PowerShell
   Import-Module .\IntuneAppWrappingTool.psm1
   ```

3. Spusťte nástroj příkazem **invoke-AppWrappingTool**, který má následující syntaxi použití:

   ```PowerShell
   Invoke-AppWrappingTool [-InputPath] <String> [-OutputPath] <String> -KeyStorePath <String> -KeyStorePassword <SecureString>
   -KeyAlias <String> -KeyPassword <SecureString> [-SigAlg <String>] [<CommonParameters>]
   ```

   Podrobný popis vlastností příkazu **invoke-AppWrappingTool** uvádí následující tabulka:

|Vlastnost|Informace|Příklad|
|-------------|--------------------|---------|
|**– InputPath**&lt;řetězec&gt;|Cesta ke zdrojové aplikaci pro Android (.apk).| |
 |**– OutputPath**&lt;řetězec&gt;|Cesta k výstupní aplikaci pro Android. Když je to cesta ke stejnému adresáři jako InputPath, vytváření balíčků selže.| |
|**– KeyStorePath**&lt;řetězec&gt;|Cesta k souboru v úložišti klíčů s dvojicí veřejného a privátního klíče, které se používají k podpisu.|Ve výchozím nastavení jsou soubory v úložišti klíčů uložené ve složce „C:\Program Files (x86)\Java\jreX.X.X_XX\bin“. |
|**– KeyStorePassword**&lt;SecureString&gt;|Heslo použité k dešifrování úložiště klíčů. Android vyžaduje, aby všechny balíčky aplikace (.apk) byly podepsané. Ke generování hesla k úložišti klíčů (parametr KeyStorePassword) použijte nástroj Java keytool. Další informace o úložišti klíčů Java si můžete přečíst [tady](https://docs.oracle.com/javase/7/docs/api/java/security/KeyStore.html).| |
|**-Jiné –**&lt;řetězec&gt;|Název klíče, který se má použít pro podepisování.| |
|**-SecureString hesla**&lt;&gt;|Heslo použité k dešifrování privátního klíče, který se použije pro podepisování.| |
|**– SigAlg**&lt;SecureString&gt;| (Volitelně) Název podpisového algoritmu, který se má použít k podepsání. Algoritmus musí být kompatibilní s privátním klíčem.|Příklady: SHA256withRSA, SHA1withRSA|
|**-UseMinAPILevelForNativeMultiDex**| Volitelné Pomocí tohoto příznaku zvyšte minimální úroveň rozhraní API u zdrojové aplikace pro Android na 21. Tento příznak zobrazí výzvu k potvrzení, protože bude omezen na to, kdo může tuto aplikaci nainstalovat. Uživatelé můžou potvrzovací dialog přeskočit připojením parametru-Confirm: $false ke svému příkazu PowerShellu. Příznak by měli používat jenom zákazníci v aplikacích s minimálním rozhraním API < 21, které se nepodařilo úspěšně zabalit kvůli chybám přetečení DEX. | |
| **&lt;CommonParameters&gt;** | (Volitelně) Příkaz podporuje běžné parametry PowerShellu, jako je verbose a debug. |


- Seznam společných parametrů najdete v [Centru skriptů Microsoftu](https://technet.microsoft.com/library/hh847884.aspx).

- Pokud chcete zobrazit podrobné informace o použití tohoto nástroje, zadejte tento příkaz:

    ```PowerShell
    Help Invoke-AppWrappingTool
    ```

**Případě**

Naimportujte modul PowerShellu.

```PowerShell
Import-Module "C:\Program Files (x86)\Microsoft Intune Mobile Application Management\Android\App Wrapping Tool\IntuneAppWrappingTool.psm1"
```

Spusťte nástroj App Wrapping Tool na nativní aplikaci HelloWorld.apk.

```PowerShell
invoke-AppWrappingTool -InputPath .\app\HelloWorld.apk -OutputPath .\app_wrapped\HelloWorld_wrapped.apk -KeyStorePath "C:\Program Files (x86)\Java\jre1.8.0_91\bin\mykeystorefile" -keyAlias mykeyalias -SigAlg SHA1withRSA -Verbose
```

Zobrazí se výzva k zadání parametrů **KeyStorePassword** a **KeyPassword**. Zadejte uživatelské jméno a heslo, které jste použili k vytvoření souboru úložiště klíčů.

Zabalená aplikace a soubor protokolu se vygenerují a uloží do zadané výstupní cesty.

## <a name="how-often-should-i-rewrap-my-android-application-with-the-intune-app-wrapping-tool"></a>Jak často mám balit svoji aplikaci pro Android pomocí nástroje Intune App Wrapping Tool?
Hlavní situace, ve kterých potřebujete znovu zabalit svoje aplikace, jsou tyto:
* Aplikace sama vydala novou verzi. Do konzoly Intune byla zabalena a nahrána předchozí verze aplikace.
* Nástroj Intune App Wrapping Tool for Android vydal novou verzi, která přináší důležité opravy chyb nebo nové specifické funkce zásad ochrany aplikace Intune. Pro [Microsoft Intune App Wrapping Tool for Android](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android) se toto děje každých 6–8 týdnů prostřednictvím úložiště GitHub.

Mezi osvědčené postupy pro opětovné balení patří: 
* Zachování podpisových certifikátů, které se používají při sestavování. Informace najdete v části [Opětovné použití podpisových certifikátů a balení aplikací](app-wrapper-prepare-android.md#reusing-signing-certificates-and-wrapping-apps).

## <a name="reusing-signing-certificates-and-wrapping-apps"></a>Opětovné použití podpisových certifikátů a balení aplikací
Android vyžaduje, že všechny aplikace musí být podepsané platným certifikátem, aby je bylo možné nainstalovat na zařízení s Androidem.

Zabalené aplikace je možné podepsat jako součást procesu zabalení nebo *po* zabalení pomocí stávajících podpisových nástrojů (veškeré podpisové informace v aplikaci budou před zabalením zahozeny). Pokud je to možné, měly by se během balení použít podpisové informace použité již během sestavování buildu. V některých organizacích to může vyžadovat spolupráci s těmi, kdo vlastní informace o úložišti klíčů (tedy s týmem, který vytvořil build aplikace). 

Pokud předchozí podpisový certifikát nelze použít nebo aplikace zatím nebyla nasazena, můžete vytvořit nový podpisový certifikát podle pokynů v [Příručce pro vývojáře pro Android](https://developer.android.com/studio/publish/app-signing.html#signing-manually).

Pokud už aplikace byla dříve nasazena s jiným podpisovým certifikátem, není ji možné po upgradu nahrát do Intune. Pokud bude aplikace podepsána s jiným certifikátem, než je ten, se kterým byla sestavena, naruší se scénáře upgradu aplikace. Všechny nové podpisové certifikáty je tedy nutné uchovat pro upgrady aplikací. 

## <a name="security-considerations-for-running-the-app-wrapping-tool"></a>Důležité informace o zabezpečení při spuštění nástroje App Wrapping Tool
Pro zabránění potenciálnímu falšování identity, zpřístupnění informací a zvýšení oprávnění pro útoky zajistěte toto:

- Vstupní obchodní aplikace (LOB), výstupní aplikace a úložiště klíčů Java KeyStore musí být na stejném počítači s Windows, na kterém běží nástroj App Wrapping Tool.

- Výstupní aplikaci naimportujte do Intune na stejném počítači, na kterém je spuštěný tento nástroj. Další informace o nástroji Java keytool viz [keytool](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/keytool.html).

- Pokud se výstupní aplikace a nástroj sice nacházejí v cestě UNC (Universal Naming Convention), ale vy nespouštíte nástroj a vstupní soubory na stejném počítači, použijte k nastavení zabezpečení prostředí podpis [protokolu IPsec (Internet Protocol Security)](https://wikipedia.org/wiki/IPsec) nebo [protokolu SMB (Server Message Block)](https://support.microsoft.com/kb/887429).

- Aplikace musí pocházet z důvěryhodného zdroje.

- Zabezpečte výstupní adresář se zabalenou aplikací. Zvažte použití adresáře na úrovni uživatele pro výstup.

## <a name="see-also"></a>Viz také
- [Rozhodování o způsobu přípravy aplikací na správu mobilních aplikací v Microsoft Intune](../developer/apps-prepare-mobile-application-management.md)

- [Microsoft Intune App SDK pro Android – Příručka pro vývojáře](../developer/app-sdk-android.md)
