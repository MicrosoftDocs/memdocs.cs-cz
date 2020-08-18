---
title: Microsoft Intune App SDK pro Android – Příručka pro vývojáře
description: Microsoft Intune App SDK pro Android umožňuje začlenit správu mobilních aplikací (MAM) Intune do vaší aplikace pro Android.
keywords: Sada SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 0100e1b5-5edd-4541-95f1-aec301fb96af
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1ede68097ef3afe0358154ff7b8802a0b3a7285
ms.sourcegitcommit: f6b14e6fe694a2a05c6ed92e67089e80a00a0908
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/17/2020
ms.locfileid: "88501163"
---
# <a name="microsoft-intune-app-sdk-for-android-developer-guide"></a>Microsoft Intune App SDK pro Android – Příručka pro vývojáře

> [!NOTE]
> Možná si budete chtít nejdříve přečíst článek [Přehled sady Intune App SDK](app-sdk.md), který vysvětluje aktuální funkce sady SDK a popisuje postup přípravy integrace na jednotlivých podporovaných platformách.
>
> Chcete-li stáhnout sadu SDK, přečtěte si téma [Stažení souborů sady SDK](../developer/app-sdk-get-started.md#download-the-sdk-files).

Sada Microsoft Intune App SDK pro Android umožňuje začlenit do vaší nativní aplikace pro Android zásady ochrany aplikací Intune (označované také jako **zásady APP** nebo MAM). Aplikace spravovaná prostřednictvím Intune je aplikace integrovaná se sadou Intune App SDK. Správci Intune můžou zásady ochrany aplikací snadno nasadit do vaší aplikace spravované prostřednictvím Intune, když Intune tuto aplikaci aktivně spravuje.


## <a name="whats-in-the-sdk"></a>Co je v sadě SDK

Sada Intune App SDK obsahuje tyto soubory:

* **Microsoft.Intune.MAM.SDK.aar**: Komponenty sady SDK kromě souborů JAR knihovny podpory
* **Microsoft.Intune.MAM.SDK.Support.v4.jar**: Třídy nutné pro povolení MAM v aplikacích, které využívají knihovnu podpory Android v4
* **Microsoft.Intune.MAM.SDK.Support.v7.jar**: Třídy nutné pro povolení MAM v aplikacích, které využívají knihovnu podpory Android v7
* **Microsoft.Intune.MAM.SDK.Support.v17.jar**: Třídy nutné pro povolení MAM v aplikacích, které využívají knihovnu podpory Android v17 
* **Microsoft.Intune.MAM.SDK.Support.Text.jar**: Třídy nutné pro povolení MAM v aplikacích, které využívají třídy knihovny podpory Android v balíčku `android.support.text`
* **Microsoft. Intune. mam. SDK. DownlevelStubs. AAR**: Tento AAR obsahuje zástupné procedury pro systémové třídy Androidu, které jsou k dispozici pouze na novějších zařízeních, ale na které odkazují metody v `MAMActivity` . Novější zařízení budou tyto zástupné třídy ignorovat. Tento AAR je nutný jenom v případě, že vaše aplikace provádí reflexi u tříd odvozených z `MAMActivity` a většina aplikací je nepotřebuje zahrnout. AAR obsahuje pravidla ProGuard pro vyloučení všech jeho tříd.
* **com.microsoft.intune.mam.build.jar**: Modul plug-in Gradle, který [usnadňuje integraci v sadě SDK](#build-tooling)
* **Changelog.MD**: poskytuje záznam změn provedených v každé verzi sady SDK.
* **THIRDPARTYNOTICES.TXT**: Označení autorství kódu OSS nebo kódu třetí strany, který se zkompiluje do vaší aplikace


## <a name="requirements"></a>Požadavky

### <a name="android-versions"></a>Verze Androidu
Sada SDK plně podporuje Android API 21 (Android 5,0) prostřednictvím rozhraní Android API 29 (Android 10,0). Může být integrována do aplikace s Androidem hodnotu minsdkversion, jak je uvedeno na úrovni 14, ale na těchto starších verzích operačního systému nebude možné nainstalovat aplikaci Portál společnosti Intune ani použít zásady MAM.

### <a name="company-portal-app"></a>Aplikace Portál společnosti
Intune App SDK pro Android se při povolení zásad ochrany aplikací spoléhá na přítomnost [Portálu společnosti](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) v zařízení. Portál společnosti načítá zásady ochrany aplikací ze služeb Intune. Při inicializaci načte aplikace z Portálu společnosti zásadu a kód, který ji vynucuje.

> [!NOTE]
> Pokud Portál společnosti na zařízení chybí, chová se aplikace spravovaná prostřednictvím Intune jako běžná aplikace, která nepodporuje zásady ochrany aplikací Intune.

U ochrany aplikací bez registrace zařízení _**nemusí**_ uživatel registrovat zařízení přes aplikaci Portál společnosti.

## <a name="sdk-integration"></a>Integrace sady SDK

### <a name="sample-app"></a>Ukázková aplikace
Příklad, jak integrovat se sadou Intune App SDK správně, je k dispozici na [GitHubu](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Android-App). V tomto příkladu se používá [modul plug-in sestavení Gradle](#gradle-build-plugin).

### <a name="referencing-intune-app-libraries"></a>Odkazování na knihovny Intune App

Intune App SDK je standardní knihovna pro Android, která nemá žádné externí závislosti. Soubor **Microsoft.Intune.MAM.SDK.aar** obsahuje jak rozhraní nutná pro povolení zásad ochrany aplikací, tak kód, který je podmínkou interoperability s Portálem společnosti Microsoft Intune.

Soubor **Microsoft.Intune.MAM.SDK.aar** musí být uváděn jako odkaz na knihovnu pro Android. To provede otevřením projektu aplikace v nástroji Android Studio, kliknutím na **File (Soubor) > New (Nový) > New module (Nový modul)** a výběrem možnosti **Import .JAR/.AAR Package (Importovat balíček .JAR/.AAR)**. Pak vyberte náš archivní balíček pro Android Microsoft. Intune. MAM. SDK. AAR a vytvořte modul pro. AAR. Klikněte pravým tlačítkem na modul nebo moduly obsahující kód vaší aplikace a přejděte na karta **nastavení modulu**  >  **závislosti**a vedle  >  **ikony**  >  >**modulu** mam SDK AAR, kterou jste právě vytvořili > **OK**. Tím se zajistí, že při sestavení projektu se modul zkompiluje se sadou SDK MAM.

Knihovny **Microsoft.Intune.MAM.SDK.Support.XXX.jar** navíc obsahují varianty Intune odpovídajících knihoven `android.support.XXX`. Nejsou součástí souboru Microsoft.Intune.MAM.SDK.aar pro případ, že není nutné, aby aplikace závisela na knihovnách podpory.

#### <a name="proguard"></a>ProGuard

Pokud je jako krok sestavení použitý [ProGuard](https://www.guardsquare.com/en/products/proguard) (případně jiný mechanismus zmenšování nebo obfuskace), obsahuje sada SDK další konfigurační pravidla, která je nutné zahrnout. Při zahrnutí. AAR v sestavení jsou naše pravidla automaticky integrována do kroku ProGuard a jsou zachovány potřebné soubory třídy.

[Knihovna Microsoft Authentication Library (MSAL)](https://docs.microsoft.com/azure/active-directory/develop/msal-overview#languages-and-frameworks) může mít vlastní omezení ProGuard. Pokud vaše aplikace integruje MSAL, musíte postupovat podle těchto omezení v dokumentaci MSAL.

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

### <a name="policy-enforcement"></a>Vynucování zásad
Sada Intune App SDK je knihovna Androidu, která umožňuje vaší aplikaci podporovat zásady Intune a podílet se na jejich vynucení. 

Většina zásad se vynutila automaticky, ale některé zásady vyžadují, [aby se vaše aplikace vynutila explicitní účastí](#enable-features-that-require-app-participation).
Bez ohledu na to, jestli provedete integraci se zdrojem nebo pomocí nástrojů sestavení pro integraci, se musí pro tyto zásady, které vyžadují explicitní účast, kódovat.

Pro zásady, které se automaticky vynutily, se vyžadují, aby se aplikace nahradily dědění z několika základních tříd Androidu s děděním z ekvivalentů MAM a obdobně nahrazují volání na určité třídy služby systému Android s voláními ekvivalentů MAM. Konkrétní požadované náhrady jsou popsané [níže](#class-and-method-replacements) a je možné je ručně provést pomocí integrace zdrojů nebo provádět automaticky prostřednictvím nástrojů sestavení.

### <a name="build-tooling"></a>Nástroje sestavení
Sada SDK poskytuje nástroje pro sestavení (modul plug-in pro Gradle buildy a nástroj příkazového řádku pro sestavení bez Gradle), které provádějí MAM ekvivalentní náhrady automaticky. Tyto nástroje transformují soubory tříd vygenerované při kompilaci Java a nezmění původní zdrojový kód.

Nástroje provádějí pouze [přímé náhrady](#class-and-method-replacements) . Neprovádí žádné složitější integrace sady SDK, jako je například [zásada Save-as](#enable-features-that-require-app-participation), [multi-identity](#multi-identity-optional), [Registrace aplikací](#app-protection-policy-without-device-enrollment)nebo souboru AndroidManifest, takže je třeba tyto [změny](#manifest-replacements)dokončit, aby byla vaše aplikace plně Intune zapnutá. Pečlivě si pročtěte zbývající část této dokumentace, abyste se seznámili s body integrace, které se týkají vaší aplikace.

> [!NOTE]
> Tyto nástroje můžete spustit u projektu, u kterého jste již provedli částečnou nebo úplnou integraci sady SDK MAM prostřednictvím ručních nahrazení. Váš projekt musí i nadále uvádět sadu SDK MAM jako závislost.

### <a name="gradle-build-plugin"></a>Modul plug-in sestavení Gradle
Pokud aplikace neprovádí sestavení pomocí nástroje Gradle, přejděte na část [Integrace s nástrojem příkazového řádku](#command-line-build-tool). 

Modul plug-in App SDK se distribuuje v sadě SDK jako **GradlePlugin/com.microsoft.intune.mam.build.jar**. Aby Gradle mohl vyhledat modul plug-in, musíte ho přidat do cesty ke třídě skriptu sestavení. Modul plug-in závisí na nástroji [Javassist](https://jboss-javassist.github.io/javassist/), který také musíte přidat. Do cesty třídy je přidáte tak, že do kořene `build.gradle` přidáte následující kód.

```groovy
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.javassist:javassist:3.22.0-GA"
        classpath files("$PATH_TO_MAM_SDK/GradlePlugin/com.microsoft.intune.mam.build.jar")
    }
}
```

Potom v souboru `build.gradle` projektu APK jednoduše použijte modul plug in jako

```groovy
apply plugin: 'com.microsoft.intune.mam'
```

Ve výchozím nastavení bude modul plug-in fungovat **pouze** u `project` závislostí.
Na testovací kompilaci nebude mít vliv. Můžete přidat konfiguraci, která zobrazí seznam:
* projektů k vyloučení,
* [externích závislostí k zahrnutí](#usage-of-includeexternallibraries), 
* konkrétních tříd k vyloučení ze zpracování,
* variant k vyloučení ze zpracování. Může se jednat buď o úplný název varianty, nebo o jednu příchuť. Například
  * Pokud má vaše aplikace typy sestavení `debug` a `release` s příchutěmi {`savory`, `sweet`} a {`vanilla`, `chocolate`}, můžete zadat
  * příchuť `savory` a vyloučit tak všechny varianty s příchutí „savory“, nebo zadat příchuť `savoryVanillaRelease` a vyloučit tak pouze tuto jednu přesnou variantu.

#### <a name="example-partial-buildgradle"></a>Ukázkový částečný soubor build.gradle

```groovy

apply plugin: 'com.microsoft.intune.mam'

dependencies {
    implementation project(':product:FooLib')
    implementation project(':product:foo-project')
    implementation fileTree(dir: "libs", include: ["bar.jar"])
    implementation fileTree(dir: "libs", include: ["zap.jar"])
    implementation "com.contoso.foo:zap-artifact:1.0.0"
    implementation "com.microsoft.bar:baz:1.0.0"
    implementation "com.microsoft.qux:foo:2.0"

    // Include the MAM SDK
    implementation files("$PATH_TO_MAM_SDK/Microsoft.Intune.MAM.SDK.aar")
}
intunemam {
    excludeProjects = [':product:FooLib']
    includeExternalLibraries = ['bar.jar', "com.contoso.foo:zap-artifact", "com.microsoft.*", "!com.microsoft.qux*"]
    excludeClasses = ['com.contoso.SplashActivity']
    excludeVariants=['savory']
}
```

Toto by mělo následující důsledky:
* `:product:FooLib` se nepřepíše, protože tato závislost je zahrnuta v `excludeProjects`.
* `:product:foo-project` se přepíše s výjimkou závislosti `com.contoso.SplashActivity`, která se přeskočí, protože je v `excludeClasses`.
* `bar.jar` se přepíše, protože tento soubor je zahrnut v `includeExternalLibraries`.
* `zap.jar` se **nepřepíše**, protože se nejedná o projekt a není zahrnut v `includeExternalLibraries`.
* `com.contoso.foo:zap-artifact:1.0.0` se přepíše, protože je tato závislost zahrnuta v `includeExternalLibraries`.
* `com.microsoft.bar:baz:1.0.0` se přepíše, protože je tato závislost zahrnuta v `includeExternalLibraries` prostřednictvím zástupného znaku (`com.microsoft.*`).
* `com.microsoft.qux:foo:2.0` není přepsán, i když odpovídá stejnému zástupnému znaku jako předchozí položka, protože je explicitně vyloučena prostřednictvím vzoru negace.

#### <a name="usage-of-includeexternallibraries"></a>Použití vlastnosti includeExternalLibraries

Vzhledem k tomu, že ve výchozím nastavení modul plug-in funguje pouze u závislostí projektu (které obvykle poskytuje funkce `project()`), všechny závislosti zadané funkcí `fileTree(...)` nebo získané z Mavenu nebo jiných zdrojů balíčků (např. `com.contoso.bar:baz:1.2.0`) je třeba zadat do vlastnosti `includeExternalLibraries` v případě, že potřebujete, aby je služba MAM zpracovávala na základě kritérií vysvětlených níže. Zástupné znaky (*) se podporují. Položka začínající na `!` je negace a lze ji použít k vyloučení knihoven, které by jinak zahrnoval zástupný znak.

Při zadávání externích závislostí pomocí notace artefaktu doporučujeme vynechat komponentu verze v hodnotě `includeExternalLibraries`. Pokud verzi uvedete, musí se jednat o přesnou verzi. Dynamické specifikace verzí (např. `1.+`) se nepodporují.

Obecné pravidlo, pomocí něhož byste měli určit to, zda potřebujete do `includeExternalLibraries` zahrnout knihovny, se zakládá na dvou otázkách:
1. Má knihovna v sobě třídy, pro které existují ekvivalenty MAM? Příklady: `Activity`, `Fragment`, `ContentProvider`, `Service` atd.
2. Pokud ano, využije aplikace tyto třídy?

Pokud je odpověď na obě otázky Ano, musíte danou knihovnu do `includeExternalLibraries` zahrnout. 

| Scénář | Zahrnout ano či ne? |
|--|--|
| Do aplikace zahrnete prohlížeč PDF a když se uživatelé pokusí zobrazit PDF, použijete v aplikaci prohlížeč `Activity`. | Ano |
| Do aplikace zahrnete knihovnu HTTP za účelem rozšířeného webového výkonu. | Ne |
| Zahrnete knihovnu, jako je React Native, která obsahuje třídy odvozené z `Activity`, `Application` a `Fragment`, a v aplikaci tyto třídy použijete nebo dále odvodíte. | Ano |
| Zahrnete knihovnu, jako je React Native, která obsahuje třídy odvozené z `Activity`, `Application` a `Fragment`, ale použijete pouze statické pomocné rutiny nebo nástrojové třídy. | Ne |
| Zahrnete knihovnu, která obsahuje třídy odvozené z `TextView`, a v aplikaci tyto třídy použijete nebo dále odvodíte. | Ano |

#### <a name="reporting"></a>Vytváření sestav
Modul plug-in sestavení může vygenerovat sestavu HTML změn, které dělá. Chcete-li vyžádat generování této sestavy, zadejte `report = true` v `intunemam` konfiguračním bloku. Pokud je tato sestava vygenerována, bude `outputs/logs` v adresáři buildu zapsána.

```groovy
intunemam {
    report = true
}
```

#### <a name="verification"></a>Ověření
Modul plug-in sestavení může spustit dodatečné ověření a vyhledat možné chyby ve zpracování tříd. Pokud to chcete požádat, zadejte `verify = true` v `intunemam` konfiguračním bloku. Všimněte si, že tato akce může přidat několik sekund do doby trvání úlohy modulu plug-in.

```groovy
intunemam {
    verify = true
}
```


#### <a name="incremental-builds"></a>Přírůstková sestavení
Chcete-li povolit podporu pro sestavení přírůstkově, zadejte `incremental = true` v `intunemam` bloku konfigurace.  Toto je experimentální funkce zaměřená na zvýšení výkonu sestavení tím, že zpracovává pouze vstupní soubory, které se změnily.  Výchozí konfigurace je `false` .

```groovy
intunemam {
    incremental = true
}
```


#### <a name="dependencies"></a>Závislosti

Modul plug-in Gradle má závislost na nástroji [Javassist](https://jboss-javassist.github.io/javassist/), který musí být dostupný pro zjištění závislostí Gradlu (jak jsme popsali výše). Javassist se používá výhradně v době sestavení při spuštění modulu plug-in. Do vaší aplikace se nepřidá žádný kód Javassist.

> [!NOTE] 
> Musíte používat verzi 3.0 nebo novější modulu plug-in Android Gradle a Gradle 4.1 nebo novější.

### <a name="command-line-build-tool"></a>Nástroj příkazového řádku
Pokud sestavení používá Gradle, přejděte na [další oddíl](#class-and-method-replacements).

Nástroj příkazového řádku je k dispozici ve složce `BuildTool` sady SDK. Má stejnou funkci jako modul plug-in Gradle podrobně popsaný výše, ale je možné ho integrovat do vlastních systémů sestavení nebo systémů sestavení, které Gradle nepoužívají. Je sice obecnější, ale současně je také složitější ho vyvolat, a proto byste měli používat modul plug-in Gradle všude tam, kde je to možné.

#### <a name="using-the-command-line-tool"></a>Použití nástroje příkazového řádku

Nástroj příkazového řádku lze vyvolat pomocí zadaných skriptů pomocných rutin, které se nacházejí v adresáři `BuildTool\bin`.

Nástroj očekává následující parametry.

| Parametr | Popis |
| -- | -- |
| `--input` | Seznam středníkem oddělených souborů JAR a adresářů souborů tříd, které se mají změnit. Seznam by měl obsahovat všechny soubory JAR a adresáře, které máte v úmyslu přepsat. |
| `--output` | Seznam středníkem oddělených souborů JAR a adresářů, do kterých se budou ukládat změněné třídy. Pro jednu výstupní položku by měla existovat jedna vstupní položka a položky by měly být uvedeny v pořadí. |
| `--classpath` | Cesta ke třídě sestavení. Může obsahovat jak soubory JAR, tak i adresáře tříd. |
| `--excludeClasses`| Seznam středníkem oddělených názvů tříd, které chcete z přepsání vyloučit. |

Všechny parametry jsou povinné s výjimkou parametru `--excludeClasses`, který je volitelný.

> [!NOTE]
> V případě systémů se systémem UNIX je středníkem příkazu oddělovač příkazů. Chcete-li zabránit prostředí v rozdělování příkazů, nezapomeňte každý středník označit středníkem \' nebo zabalte úplný parametr v uvozovkách.

#### <a name="example-command-line-tool-invocation"></a>Ukázka vyvolání nástroje příkazového řádku

``` batch
> BuildTool\bin\BuildTool.bat --input build\product-foo-project;libs\bar.jar --output mam-build\product-foo-project;mam-build\libs\bar.jar --classpath build\zap.jar;libs\Microsoft.Intune.MAM.SDK\classes.jar;%ANDROID_SDK_ROOT%\platforms\android-27\android.jar --excludeClasses com.contoso.SplashActivity
```

Toto by mělo následující důsledky:

* Adresář `product-foo-project` se přepíše na `mam-build\product-foo-project`.
* `bar.jar` se přepíše na `mam-build\libs\bar.jar`.
* `zap.jar` se **nepřepíše**, protože je uveden pouze v `--classpath`.
* Třída `com.contoso.SplashActivity` se **nepřepíše**, ani když je v `--input`.

> [!NOTE] 
> Nástroj sestavení v současné době nepodporuje soubory AAR. Pokud systém sestavení při zpracování souborů AAR ještě neextrahoval soubor `classes.jar`, musíte ho vyextrahovat dříve, než vyvoláte nástroj sestavení.


## <a name="class-and-method-replacements"></a>Nahrazení tříd a metod
> [!NOTE] 
> Aplikace *by se měly* integrovat s [nástroji pro vytváření sestavení](#build-tooling)sady SDK, které tyto náhrady provádí automaticky (s výjimkou [nahrazení manifestů](#manifest-replacements) ).

Základní třídy Androidu se musí nahradit odpovídajícími ekvivalenty MAM, aby bylo možné povolit správu Intune. Třídy SDK se pohybují mezi základní třídou Androidu a vlastní odvozenou verzí této třídy v aplikaci. Aktivita aplikace by například mohla mít výslednou hierarchii dědičnosti, která vypadá takto: `Activity` > `MAMActivity` >
`AppSpecificActivity`. Filtry vrstvy MAM volají systémové operace, aby mohly vaší aplikaci bez problémů poskytovat spravované zobrazení.

Kromě základních tříd mají povinné ekvivalenty MAM i některé třídy, které vaše aplikace používá bez odvození (např. `MediaPlayer`). [Je třeba nahradit i některé metody](#wrapped-system-services). Přesné podrobnosti jsou uvedeny níže.

> [!NOTE] 
> Pokud je vaše aplikace integrována s [nástroji pro sestavení](#build-tooling)sady SDK, provede se automatické nahrazení následující třídy a metody.

| Základní třída Android | Náhrada ze sady Intune App SDK |
|--|--|
| android.app.Activity | MAMActivity |
| android.app.ActivityGroup | MAMActivityGroup |
| android.app.AliasActivity | MAMAliasActivity |
| android.app.Application | MAMApplication |
| Android. app. dialog | MAMDialog |
| Android. app. AlertDialog. Builder | MAMAlertDialogBuilder |
| android.app.DialogFragment | MAMDialogFragment |
| android.app.ExpandableListActivity | MAMExpandableListActivity |
| android.app.Fragment | MAMFragment |
| android.app.IntentService | MAMIntentService |
| android.app.LauncherActivity | MAMLauncherActivity |
| android.app.ListActivity | MAMListActivity |
| android.app.ListFragment | MAMListFragment |
| android.app.NativeActivity | MAMNativeActivity |
| android.app.PendingIntent | MAMPendingIntent (viz [PendingIntent](#pendingintent)) |
| android.app.Service | MAMService |
| android.app.TabActivity | MAMTabActivity |
| android.app.TaskStackBuilder | MAMTaskStackBuilder |
| android.app.backup.BackupAgent | MAMBackupAgent |
| android.app.backup.BackupAgentHelper | MAMBackupAgentHelper |
| android.app.backup.FileBackupHelper | MAMFileBackupHelper |
| android.app.backup.SharePreferencesBackupHelper | MAMSharedPreferencesBackupHelper |
| android.content.BroadcastReceiver | MAMBroadcastReceiver |
| android.content.ContentProvider | MAMContentProvider |
| android.os.Binder | MAMBinder (nutné jen v případě, že se třída Binder negeneruje z rozhraní AIDL (Android Interface Definition Language)) |
| android.media.MediaPlayer | MAMMediaPlayer |
| android.media.MediaMetadataRetriever | MAMMediaMetadataRetriever |
| android.provider.DocumentsProvider | MAMDocumentsProvider |
| android.preference.PreferenceActivity | MAMPreferenceActivity |
| android.support.multidex.MultiDexApplication | MAMMultiDexApplication |
| android.widget.TextView | MAMTextView |
| android.widget.AutoCompleteTextView | MAMAutoCompleteTextView |
| android.widget.CheckedTextView | MAMCheckedTextView |
| android.widget.EditText | MAMEditText |
| android.inputmethodservice.ExtractEditText | MAMExtractEditText |
| android.widget.MultiAutoCompleteTextView | MAMMultiAutoCompleteTextView |


> [!NOTE]
> I když není nutné, aby vaše aplikace používala vlastní odvozenou třídu `Application`, [přečtěte si část `MAMApplication` níže](#mamapplication).

### <a name="microsoftintunemamsdksupportv4jar"></a>Microsoft.Intune.MAM.SDK.Support.v4.jar:

| Třída Androidu | Náhrada ze sady Intune App SDK |
|--|--|
| android.support.v4.app.DialogFragment | MAMDialogFragment
| android.support.v4.app.FragmentActivity | MAMFragmentActivity
| android.support.v4.app.Fragment | MAMFragment
| android.support.v4.app.JobIntentService | MAMJobIntentService
| android.support.v4.app.TaskStackBuilder | MAMTaskStackBuilder
| android.support.v4.content.FileProvider | MAMFileProvider
| android.support.v4.content.WakefulBroadcastReceiver | MAMWakefulBroadcastReceiver

### <a name="microsoftintunemamsdksupportv7jar"></a>Microsoft.Intune.MAM.SDK.Support.v7.jar:

|Třída Androidu | Náhrada ze sady Intune App SDK |
|--|--|
| Android. support. v7. app. AlertDialog. Builder | MAMAlertDialogBuilder |
| android.support.v7.app.AppCompatActivity | MAMAppCompatActivity |
| android.support.v7.widget.AppCompatAutoCompleteTextView | MAMAppCompatAutoCompleteTextView |
| android.support.v7.widget.AppCompatCheckedTextView | MAMAppCompatCheckedTextView |
| android.support.v7.widget.AppCompatEditText | MAMAppCompatEditText |
| android.support.v7.widget.AppCompatMultiAutoCompleteTextView | MAMAppCompatMultiAutoCompleteTextView |
| android.support.v7.widget.AppCompatTextView | MAMAppCompatTextView |

### <a name="microsoftintunemamsdksupportv17jar"></a>Microsoft.Intune.MAM.SDK.Support.v17.jar:
|Třída Androidu | Náhrada ze sady Intune App SDK |
|--|--|
| android.support.v17.leanback.widget.SearchEditText | MAMSearchEditText |

### <a name="microsoftintunemamsdksupporttextjar"></a>Microsoft.Intune.MAM.SDK.Support.Text.jar:
|Třída Androidu | Náhrada ze sady Intune App SDK |
|--|--|
| android.support.text.emoji.widget.EmojiAppCompatEditText | MAMEmojiAppCompatEditText |
| android.support.text.emoji.widget.EmojiAppCompatTextView | MAMEmojiAppCompatTextView |
| android.support.text.emoji.widget.EmojiEditText | MAMEmojiEditText |
| android.support.text.emoji.widget.EmojiTextView | MAMEmojiTextView |

### <a name="renamed-methods"></a>Přejmenované metody

V mnoha případech je metoda dostupná ve třídě Androidu označená v náhradní třídě MAM jako finální. Náhradní třída MAM pak poskytuje metodu s podobným názvem (obecně s příponou `MAM`), kterou byste měli přepsat místo toho. Třeba při odvozování od třídy `MAMActivity` musí `Activity` místo přepsání `onCreate()` a volání `super.onCreate()` přepsat `onMAMCreate()` a volat `super.onMAMCreate()`. Kompilátor Javy by měl vynutit finální omezení, která zabrání náhodnému přepsání původní metody místo jejího ekvivalentu MAM.

### <a name="mamapplication"></a>MAMApplication
Pokud vaše aplikace vytváří podtřídu `android.app.Application`, **musíte** místo ní vytvořit podtřídu `com.microsoft.intune.mam.client.app.MAMApplication`. Pokud vaše aplikace podtřídu `android.app.Application` nevytváří, **musíte** nastavit `"com.microsoft.intune.mam.client.app.MAMApplication"` jako atribut `"android:name"` ve značce`<application>` souboru AndroidManifest.xml.

### <a name="pendingintent"></a>PendingIntent
Namísto metody `PendingIntent.get*` musíte použít metodu `MAMPendingIntent.get*`. Pak můžete výslednou třídu `PendingIntent` použít obvyklým způsobem.

### <a name="wrapped-system-services"></a>Zabalené systémové služby
U některých tříd systémové služby je třeba volat statickou metodu obálkové třídy MAM místo přímého vyvolání požadované metody u instance služby. Například volání `getSystemService(ClipboardManager.class).getPrimaryClip()` se musí stát voláním `MAMClipboardManager.getPrimaryClip(getSystemService(ClipboardManager.class)`. Nedoporučujeme tato nahrazení provádět ručně. Nechme raději nástroj BuildPlugin, aby to udělal za nás.

| Třída Androidu | Náhrada ze sady Intune App SDK |
|--|--|
| android.content.ClipboardManager | MAMClipboard |
| Android. Content. ContentProviderClient | MAMContentProviderClientManagement |
| Android. Content. ContentResolver | MAMContentResolverManagement |
| android.content.pm.PackageManager | MAMPackageManagement |
| android.app.DownloadManager | MAMDownloadManagement |
| Android. Print. PrintManager | MAMPrintManagement |
| Android. support. v4. Print. PrintHelper | MAMPrintHelperManagement |
| Android. View. View | MAMViewManagement |
| Android. View. DragEvent | MAMDragEventManagement |
| Android. app. NotificationManager | MAMNotificationManagement |
| Android. support. v4. app. NotificationManagerCompat | MAMNotificationCompatManagement |

Některé třídy mají většinu zabalené metody, například,, `ClipboardManager` `ContentProviderClient` `ContentResolver` a `PackageManager` zatímco jiné třídy mají pouze jednu nebo dvě zabalené metody, například, `DownloadManager` `PrintManager` , `PrintHelper` , `View` , a `DragEvent` `NotificationManager` `NotificationManagerCompat` . Pokud nepoužíváte BuildPlugin, Projděte si prosím rozhraní API, které jsou vystavené ekvivalentními třídami MAM, pro přesný způsob.

### <a name="manifest-replacements"></a>Nahrazení manifestů
Některá nahrazení tříd uvedená výše je potřeba provést jak v manifestu, v tak kódu v jazyce Java. Zejména:
* Odkazy manifestu na `android.support.v4.content.FileProvider` je nutné vyměnit za `com.microsoft.intune.mam.client.support.v4.content.MAMFileProvider`.

## <a name="androidx-libraries"></a>Knihovny AndroidX
S příchodem Androidu P Google oznámil novou (přejmenovanou) sadu podpůrných knihoven s názvem AndroidX. Verze 28 je nejnovější hlavní vydanou verzí stávajících podpůrných knihoven Androidu.

Na rozdíl od podpůrných knihoven Androidu neposkytujeme varianty MAM knihoven AndroidX. Místo toho byste měli se sadou AndroidX nakládat jako s kteroukoli jinou externí knihovnou a měli byste ji nakonfigurovat tak, aby ji nástroj nebo modul plug-in sestavení přepsal. Pro Gradle buildy to jde udělat tak, že zahrnete `androidx.*` do `includeExternalLibraries` pole konfigurace modulu plug-in. Volání nástroje příkazového řádku musí vypsat všechny soubory jar explicitně.

### <a name="pre-androidx-architecture-components"></a>Komponenty architektury před AndroidX
Mnoho součástí architektury Androidu, včetně místností, ViewModel a WorkManager, bylo znovu zabalené pro AndroidX. Pokud vaše aplikace používá předem AndroidX varianty těchto knihoven, zajistěte, aby se přepisy použily, a to zahrnutím `android.arch.*` do `includeExternalLibraries` pole konfigurace modulu plug-in. Případně aktualizujte knihovny na jejich ekvivalenty AndroidX.

### <a name="troubleshooting-androidx-migration"></a>Řešení potíží s migrací AndroidX
Při migraci aplikace integrované v sadě SDK do AndroidX se může zobrazit chyba podobná následující:

```log
incompatible types: android.support.v7.app.ActionBar cannot be converted to androidx.appcompat.app.ActionBar
```

K těmto chybám může dojít, protože vaše aplikace odkazuje na třídy MAM support. Třídy podpory MAM zabalí třídy podpory Androidu, které se přesunuly do AndroidX. Chcete-li tyto chyby bojovat, nahraďte všechny odkazy na třídu MAM support odpovídajícími ekvivalenty AndroidX. Toho lze dosáhnout tím, že nejprve odeberete závislosti knihoven MAM support z vašich souborů sestavení Gradle. Příslušné řádky budou vypadat přibližně takto:

```Gradle
implementation "com.microsoft.intune.mam:android-sdk-support-v4:$intune_mam_version"
implementation "com.microsoft.intune.mam:android-sdk-support-v7:$intune_mam_version"
```

Pak opravte výsledné chyby při kompilaci tím, že nahradíte všechny odkazy na třídy MAM v `com.microsoft.intune.mam.client.support.v7` `com.microsoft.intune.mam.client.support.v4` balíčcích a pomocí jejich ekvivalentů AndroidX. Například odkazy na, které `MAMAppCompatActivity` by měly být změněny na AndroidX 's `AppCompatActivity` . Jak je popsáno výše, modul plug-in nebo nástroj pro sestavení MAM automaticky přepíše třídy v knihovnách AndroidX s odpovídajícími ekvivalenty MAM v době kompilace.

## <a name="sdk-permissions"></a>Oprávnění sady SDK

Intune App SDK vyžaduje tři [oprávnění pro systém Android](https://developer.android.com/guide/topics/security/permissions.html) u aplikací, které ji integrují:

* `android.permission.GET_ACCOUNTS` (v případě potřeby se požaduje za běhu)

* `android.permission.MANAGE_ACCOUNTS`

* `android.permission.USE_CREDENTIALS`

Azure Active Directory Authentication Library ([ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/)) vyžaduje tato oprávnění ke zprostředkovanému ověřování. Pokud nejsou tato oprávnění udělená aplikaci nebo je uživatel odvolá, zakážou se toky ověřování, které vyžadují zprostředkovatele (aplikace Portál společnosti).

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

## <a name="logging"></a>protokolování

Abyste ze zaprotokolovaných dat získali co nejvíce, měli byste protokolování zahájit brzy. Nejlepším místem k zahájení protokolování je obvykle `Application.onMAMCreate()`.

Pokud chcete v aplikaci přijímat protokoly MAM, vytvořte [Java Handler](https://docs.oracle.com/javase/7/docs/api/java/util/logging/Handler.html) a přidejte ho do `MAMLogHandlerWrapper`. Tím se pro každou zprávu protokolu vyvolá v obslužné rutině aplikace `publish()`.

```java
/**
 * Global log handler that enables fine grained PII filtering within MAM logs.  
 *
 * To start using this you should build your own log handler and add it via
 * MAMComponents.get(MAMLogHandlerWrapper.class).addHandler(myHandler, false);  
 *
 * You may also remove the handler entirely via
 * MAMComponents.get(MAMLogHandlerWrapper.class).removeHandler(myHandler);
 */
public interface MAMLogHandlerWrapper {
    /**
     * Add a handler, PII can be toggled.
     *
     * @param handler handler to add.
     * @param wantsPII if PII is desired in the logs.    
     */
    void addHandler(final Handler handler, final boolean wantsPII);

    /**
     * Remove a handler.
     *
     * @param handler handler to remove.
     */
    void removeHandler(final Handler handler);
}
```

## <a name="diagnostics-information"></a>Diagnostické informace
Aplikace mohou vyvolat `MAMPolicyManager.showDiagnostics(context)` metodu, která spustí aktivitu zobrazující uživatelské rozhraní pro shromažďování portál společnostich protokolů a zobrazení diagnostiky mam.
Toto je volitelná funkce, která může pomoci při ladění.

Pokud na zařízení není nainstalovaná Portál společnosti, zobrazí se dialogové okno s výzvou, aby uživatel informoval, že tyto informace nejsou aktuálně k dispozici. Když se aplikace spravují pomocí zásad MAM, zobrazí se podrobnosti nastavení zásad MAM.

## <a name="mam-strict-mode"></a>MAM striktní režim
MAM striktní režim poskytuje mechanismus pro detekci "pachy" v použití aplikace MAM API nebo rozhraní API platformy s omezeným přístupem MAM. Po StrictModeu Androidu se bude volně vycházet a spustí sadu kontrol, které vyvolávají chyby, když selžou. V produkčních sestavách není tato možnost ponechána, ale je *velmi doporučována* pro použití v interním vývoji, ladění nebo testování sestavení vaší aplikace.

Chcete-li povolit, zavolejte

```java
MAMStrictMode.enable();
```
 počáteční inicializace aplikace (např. `Application.onCreate` ). 

Pokud se MAM striktního režimu, zkuste zjistit, zda se jedná o skutečný problém, který lze ve vaší aplikaci opravit, nebo falešně pozitivní. Pokud se domníváte, že se jedná o falešně pozitivní nebo nejste si jistí, nechejte prosím tým Intune MAM znám. Tím zajistíme, že budeme souhlasit s falešně pozitivním určením a pokusíte se zlepšit detekci budoucích verzí. Chcete-li potlačit falešně pozitivní hodnoty, zakažte kontrolu při selhání (Další informace níže).

### <a name="handling-violations"></a>Narušení zpracování
Při chybě kontroly se spustí `MAMStrictViolationHandler` . Výchozí obslužná rutina vyvolá výjimku `Error` , která se očekává k selhání aplikace. Důvodem je to, že dochází k chybám, co je možné co nejrychleji, a zapadá do toho, že striktní režim by neměl být povolený v produkčních sestaveních.

Pokud by vaše aplikace chtěla nakládat s porušením odlišně, může poskytovat vlastní obslužnou rutinu voláním:

```java
MAMStrictMode.global().setHandler(handler);
```

kde `handler` implementuje `MAMStrictViolationHandler` :

```java
public interface MAMStrictViolationHandler {
    /**
     * Called when a MAM Strict Mode check fails.
     *
     * @param check
     *         the check that failed
     * @param detail
     *         additional detail. Note that this might contain usernames or filepaths.
     * @param error
     *         error containing a stack trace. The default implementation throws this error
     */
    void checkFailed(@NonNull MAMStrictCheck check, @NonNull String detail, @NonNull Error error);
}
```

### <a name="suppressing-checks"></a>Potlačení kontrol
Pokud se ověření nepovede v situaci, kdy vaše aplikace nefunguje správně, ohlaste ji prosím, jak je uvedeno výše. V některých případech ale může být potřeba zakázat kontrolu, která narazí na falešně pozitivní odpověď aspoň při čekání na aktualizovanou sadu SDK. Ověření, které selhalo, se zobrazí v chybě vyvolané výchozí obslužnou rutinou, nebo bude při nastavení předána vlastní obslužné rutině.

Potlačení lze provést globálně, ale je dočasně zakázáno pro každé vlákno na konkrétním webu volání. Následující příklady znázorňují různé způsoby, jak `MAMStrictCheck.IDENTITY_NO_SUCH_FILE` je zakázat (je-li proveden pokus o ochranu souboru, který neexistuje).


#### <a name="per-thread-temporary-suppression"></a>Dočasné potlačení za vlákno
Toto je preferovaný mechanizmus potlačení.
```java
try (StrictScopedDisable disable = MAMStrictMode.thread().disableScoped(MAMStrictCheck.IDENTITY_NO_SUCH_FILE)) {
    // Perform the operation which raised a violation here
}
// The check is no longer disabled once the block exits
```

#### <a name="per-thread-permanent-suppression"></a>Trvalé potlačení podle vlákna
```java
MAMStrictMode.thread().disable(MAMStrictCheck.IDENTITY_NO_SUCH_FILE);
```

#### <a name="global-process-wide-suppression"></a>Potlačení globálních (na úrovni procesu)
```java
MAMStrictMode.global().disable(MAMStrictCheck.IDENTITY_NO_SUCH_FILE);
```



## <a name="enable-features-that-require-app-participation"></a>Povolení funkcí, které vyžadují účast aplikace

Některé zásady ochrany aplikací nemůže sada SDK implementovat sama o sobě. Aplikace může kontrolovat své chování a dosáhnout těchto funkcí přes několik rozhraní API, která najdete v následujícím rozhraní `AppPolicy`. K načtení instance `AppPolicy` použijte `MAMPolicyManager.getPolicy`.

```java
/**
 * External facing application policies.
 */
public interface AppPolicy {

/**
 * Restrict where an app can save personal data.
 * This function is now deprecated. Use getIsSaveToLocationAllowed(SaveLocation, String) instead
 * @return True if the app is allowed to save to personal data stores; false otherwise.
 */
@Deprecated
boolean getIsSaveToPersonalAllowed();

/**
 * Check if policy prohibits saving to a content provider location.
 *
 * @param location
 *            a content URI to check
 * @return True if location is not a content URI or if policy does not prohibit saving to the content location.
 */
boolean getIsSaveToLocationAllowed(Uri location);

/**
 * Determines if the SaveLocation passed in can be saved to by the username associated with the cloud service.
 *
 * @param service
 *           The SaveLocation the data will be saved to.
 * @param username
 *           The AAD UPN associated with the cloud service being saved to. Use null if a mapping between
 *           the AAD username and the cloud service username does not exist or the username is not known.
 * @return true if the location can be saved to by the identity, false if otherwise.
 */
boolean getIsSaveToLocationAllowed(SaveLocation service, String username);

/**
 * Determines if data from the OpenLocation can be opened for the username associated with the data.
 *
 * @param location
 *      The OpenLocation that the data will be opened from.
 * @param username
 *      The AAD UPN associated with the location the data is being opened from. Use null if a mapping between the
 *      AAD username and the cloud service username does not exist or the username is not known.
 * @return true if the data can be opened from the location for the identity, false if otherwise.
 */
boolean getIsOpenFromLocationAllowed(@NonNull OpenLocation location, @Nullable String username);

/**
 * Checks whether any activities which could handle the given intent are allowed by policy. Returns false only if all
 * activities which could otherwise handle the intent are blocked. If there are no activities which could handle the intent
 * regardless of policy, returns true. If some activities are allowed and others blocked, returns true. Note that it is not
 * necessary to use this method for policy enforcement. If your app attempts to launch an intent for which there are no
 * allowed activities, MAM will display a dialog explaining the situation to the user.
 *
 * @param intent
 *         intent to check
 *
 * @return whether any activities which could handle this intent are allowed.
*/
boolean areIntentActivitiesAllowed(Intent intent);

/**
 * Whether the SDK PIN prompt is enabled for the app.
 *
 * @return True if the PIN is enabled. False otherwise.
 */
boolean getIsPinRequired();

/**
 * Whether the Intune Managed Browser is required to open web links.
 * @return True if the Managed Browser is required, false otherwise
 */
boolean getIsManagedBrowserRequired();

/**
 * Check if policy allows taking screenshots.
 *
 * @return True if screenshots will be blocked, false otherwise
 */
boolean getIsScreenCaptureAllowed();

/**
 * Check if policy allows Contact sync to local contact list.
 *
 * @return True if Contact sync is allowed to save to local contact list; false otherwise.
 */
boolean getIsContactSyncAllowed();

/**
 * Get the notification restriction. If {@link NotificationRestriction#BLOCKED BLOCKED}, the app must not show any notifications
 * for the user associated with this policy. If {@link NotificationRestriction#BLOCK_ORG_DATA BLOCK_ORG_DATA}, the app must show
 * a modified notification that does not contain organization data. If {@link NotificationRestriction#UNRESTRICTED
 * UNRESTRICTED}, all notifications are allowed.
 *
 * @return The notification restriction.
 */
NotificationRestriction getNotificationRestriction();

/**
 * This method is intended for diagnostic/telemetry purposes only. It can be used to discover whether file encryption is in use.
 * File encryption is transparent to the app and the app should not need to make any business logic decisions based on this.
 * @return True if file encryption is in use.
 */
boolean diagnosticIsFileEncryptionInUse();

/**
 * Return the policy in string format to the app.
 *  
 * @return The string representing the policy.
 */
String toString();

}
```

> [!NOTE]
> `MAMPolicyManager.getPolicy` vždy vrátí zásadu aplikace, která není null, i když zařízení nebo aplikace nepodléhají zásadám správy Intune.

### <a name="example-determine-if-pin-is-required-for-the-app"></a>Příklad: Určení, jestli aplikace vyžaduje PIN

Pokud aplikace využívá vlastní kód PIN a správce nastavil sadu SDK tak, aby od uživatele vyžadovala zadání kódu PIN aplikace, možná ho bude potřeba zakázat. K určení, jestli je zásada zadávání PIN pro tuto aplikaci nakonfigurovaná, použijte pro aktuálního koncového uživatele toto volání:

```java

MAMPolicyManager.getPolicy(currentActivity).getIsPinRequired();
```

### <a name="example-determine-the-primary-intune-user"></a>Příklad: Určení primárního uživatele Intune

Kromě rozhraní API zobrazovaných v AppPolicy se pomocí API `getPrimaryUser()` definovaného v rámci rozhraní `MAMUserInfo` také zobrazuje hlavní název uživatele (**UPN**) . Hlavní název uživatele zobrazíte tímto voláním:

```java
MAMComponents.get(MAMUserInfo.class).getPrimaryUser();
```

Kompletní definici rozhraní MAMUserInfo vidíte níže:

```java
/**
 * External facing user information.
 *
 */
public interface MAMUserInfo {
       /**
        * Get the primary user name.
        *
        * @return the primary user name or null if neither the device nor app is enrolled.
        */
       String getPrimaryUser();
}
```

### <a name="example-data-transfer-between-apps-and-device-or-cloud-storage-locations"></a>Příklad: přenos dat mezi aplikacemi a zařízeními nebo cloudovým úložištěm

Mnohé aplikace implementují funkce, které umožňují koncovému uživateli ukládat data do nebo otevírat data z místního úložiště souborů nebo cloudových služeb úložiště.
Intune App SDK umožňuje správcům IT chránit před vstupem a únikem dat pomocí omezení zásad, která se v jejich organizaci hodí.

**K povolení této funkce je nutné zapojení aplikací.**
Pokud vaše aplikace umožňuje ukládání do osobních nebo cloudových umístění přímo z aplikace *nebo* umožňuje, aby se data otevírala přímo do aplikace, musíte implementovat příslušnou funkci, aby správce IT měl kontrolu nad tím, jestli je povolené ukládání do nebo otevírání z umístění.

#### <a name="saving-to-device-or-cloud-storage"></a>Ukládání do zařízení nebo do cloudového úložiště

Rozhraní API níže dá aplikaci vědět, jestli je na základě aktuálních zásad správce Intune povolené ukládání do osobního úložiště.

K určení, jestli je tato zásada vynucená, použije následující volání:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(
SaveLocation service, String username);
```

`service`Parametr musí být jedna z následujících `SaveLocation` hodnot:

* `SaveLocation.ONEDRIVE_FOR_BUSINESS`
* `SaveLocation.SHAREPOINT`
* `SaveLocation.LOCAL`
* `SaveLocation.ACCOUNT_DOCUMENT`
* `SaveLocation.OTHER`

Pro určení, `ACCOUNT_DOCUMENT` jestli `OTHER` se má předávat, aby se `getIsSaveToLocationAllowed` zobrazily další informace o [neznámých nebo neuvedených umístěních](#unknown-or-unlisted-locations) .

`username`Další informace o parametru najdete v tématu [uživatelské jméno pro přenos dat](#username-for-data-transfer) .

Dříve se pro určování, jestli zásady uživatele umožňují ukládání dat do různých umístění, využívala funkce `getIsSaveToPersonalAllowed()` ze stejné třídy **AppPolicy**.
Ta je teď **zastaralá** a neměla by se používat. Vyvolání ekvivalentní k funkci `getIsSaveToPersonalAllowed()` vidíte níže:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(SaveLocation.LOCAL, null);
```

#### <a name="opening-data-from-a-local-or-cloud-storage-location"></a>Otevírání dat z místního nebo cloudového úložiště

Rozhraní API níže umožňuje aplikaci zjistit, jestli aktuální zásady správce Intune dovolují otevírání z osobního úložiště.

K určení, jestli je tato zásada vynucená, použije následující volání:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsOpenFromLocationAllowed(
OpenLocation location, String username);
```

`location`Parametr musí být jedna z následujících `OpenLocation` hodnot:

* `OpenLocation.ONEDRIVE_FOR_BUSINESS`
* `OpenLocation.SHAREPOINT`
* `OpenLocation.CAMERA`
* `OpenLocation.LOCAL`
* `OpenLocation.ACCOUNT_DOCUMENT`
* `OpenLocation.OTHER`

`OpenLocation.CAMERA`Umístění by mělo být předáno, když aplikace otevírá data z kamery.
`OpenLocation.LOCAL`Umístění by mělo být předáno, když aplikace otevírá data z externího úložiště na místním zařízení.
`OpenLocation.ACCOUNT_DOCUMENT`Umístění by mělo být předáno, když aplikace otevírá data, která patří k účtu AAD přihlášenému do aplikace.

Pro určení, `ACCOUNT_DOCUMENT` jestli `OTHER` se má předávat, aby se `getIsOpenFromLocationAllowed` zobrazily další informace o [neznámých nebo neuvedených umístěních](#unknown-or-unlisted-locations) .

`username`Další informace o parametru najdete v tématu [uživatelské jméno pro přenos dat](#username-for-data-transfer) .

#### <a name="unknown-or-unlisted-locations"></a>Neznámé nebo neuvedené umístění

Pokud požadované umístění není uvedeno v `SaveLocation` `OpenLocation` výčtech nebo nebo není známo, existují dvě možnosti pro `service` / `location` parametr `ACCOUNT_DOCUMENT` a `OTHER` .
`ACCOUNT_DOCUMENT` by se měla použít, když data patří do účtu AAD přihlášeného k aplikaci, ale nejsou `ONEDRIVE_FOR_BUSINESS` nebo `SHAREPOINT` `OTHER` by se měla použít, pokud to není případ.

Je důležité odlišit jasné rozlišení mezi spravovaným účtem a účtem, který sdílí hlavní název uživatele spravovaného účtu.
Například spravovaný účet s UPN " user@contoso.com " přihlášený k OneDrivu není stejný jako účet, který má hlavní název uživatele (UPN) " user@contoso.com " přihlášený k Dropboxu.
Pokud se přihlašujete k neznámé nebo neuvedené službě, přihlaste se ke spravovanému účtu (například " user@contoso.com " přihlášenému na OneDrive), mělo by být reprezentované `ACCOUNT_DOCUMENT` umístěním.
Pokud se neznámá nebo neuvedená služba přihlásí prostřednictvím jiného účtu (např. " user@contoso.com " přihlášení k Dropboxu "), nepřistupuje k umístění se spravovaným účtem a mělo by být reprezentované jeho `OTHER` umístěním.

#### <a name="username-for-data-transfer"></a>Uživatelské jméno pro přenos dat

Při kontrole zásad ukládání `username` by měl být hlavní název uživatele (UPN)/uživatelské jméno/e-mail přidružený ke cloudové službě, na kterou se ukládá (*nemusí* nutně platit jako uživatel, který je vlastníkem dokumentu).
`SaveLocation.LOCAL` není cloudová služba, takže by měla být vždy použita s `null` parametrem username.

Při kontrole otevřených zásad `username` by měl být hlavní název uživatele (UPN)/uživatelské jméno/e-mail přidružený ke cloudové službě, ze které se otevírá.
`OpenLocation.LOCAL` a `OpenLocation.CAMERA` nepatří do umístění cloudových služeb, takže by měly být vždy použity s `null` parametrem username.

V následujících umístěních bude vždycky očekávat uživatelské jméno, které obsahuje mapování mezi hlavním jménem služby AAD a uživatelským jménem cloudové služby: `ONEDRIVE_FOR_BUSINESS` , `SHAREPOINT` a `ACCOUNT_DOCUMENT` .

Pokud mapování mezi hlavním názvem uživatele služby AAD a uživatelským jménem cloudové služby neexistuje nebo uživatelské jméno není známé `null` .

#### <a name="sharing-blocked-dialog"></a>Zablokované sdílení – dialogové okno

Sada SDK nabízí dialog, který uživateli upozorní, že akce přenosu dat byla zablokována zásadami MAM.

Dialogové okno by se mělo zobrazit uživateli, když `isSaveToAllowedForLocation` `isOpenFromAllowedForLocation` volání rozhraní API nebo vyvolá akci Uložit/otevřít, která je blokovaná.
V dialogu se zobrazí obecná zpráva a vrátí se do aplikace `Activity` , která ji zavolala po jejím odvolání.

Chcete-li zobrazit dialogové okno, proveďte následující volání:

``` java
MAMUIHelper.showSharingBlockedDialog(currentActivity)
```

### <a name="allow-for-file-sharing"></a>Povolení sdílení souborů

Pokud se ukládání do umístění veřejného úložiště nepovoluje, vaše aplikace by měla uživateli povolit zobrazení souborů jejich stažením do [soukromého úložiště aplikace](https://developer.android.com/training/data-storage) a jejich otevřením pomocí nástroje pro výběr systému.

### <a name="example-determine-if-notifications-with-organization-data-need-to-be-restricted"></a>Příklad: určení, jestli je potřeba omezit oznámení s daty organizace

Pokud vaše aplikace zobrazuje oznámení, musíte před zobrazením oznámení ověřit zásadu omezení oznámení pro uživatele přidruženého k oznámení. Chcete-li zjistit, zda je zásada vynutila, proveďte následující volání.

```java
NotificationRestriction notificationRestriction =
    MAMPolicyManager.getPolicyForIdentity(notificationIdentity).getNotificationRestriction();
```

Pokud je omezení `BLOCKED` , aplikace nesmí zobrazit žádná oznámení pro uživatele přidruženého k této zásadě. `BLOCK_ORG_DATA`V případě, že aplikace musí zobrazit upravené oznámení, které neobsahuje data organizace. `UNRESTRICTED`V případě, že jsou povolena všechna oznámení.

Pokud `getNotificationRestriction` není vyvolána, sada mam SDK se bude snažit vyhradit automatické omezení oznámení pro aplikace s jedinou identitou. Pokud je zapnuté automatické blokování a `BLOCK_ORG_DATA` je nastavené, nebude se vám zobrazovat oznámení. V případě podrobnějšího řízení ověřte hodnotu `getNotificationRestriction` a patřičně upravte oznámení aplikace.

## <a name="register-for-notifications-from-the-sdk"></a>Registrace k oznámením z SDK

### <a name="overview"></a>Přehled
Intune App SDK umožňuje aplikaci, aby měla kontrolu nad chováním určitých zásad, jako je selektivní vymazání, pokud je správce IT nasadil. Jakmile správce IT tuto zásadu nasadí, služba Intune odešle sadě SDK oznámení.

Vaše aplikace se musí k oznámením ze sady SDK registrovat vytvořením třídy `MAMNotificationReceiver` a její registrací pomocí `MAMNotificationReceiverRegistry`. V `App.onCreate` se uvede příjemce a typ požadovaného oznámení, jak ukazuje tento příklad:

```java
@Override
public void onCreate() {
  super.onCreate();
  MAMComponents.get(MAMNotificationReceiverRegistry.class)
    .registerReceiver(
      new ToastNotificationReceiver(),
      MAMNotificationType.WIPE_USER_DATA);
}
```

### <a name="mamnotificationreceiver"></a>MAMNotificationReceiver

Rozhraní `MAMNotificationReceiver` jednoduše dostává oznámení ze služby Intune. Některá oznámení zpracovává přímo sada SDK, jiná vyžadují zapojení aplikace. Aplikace **musí** z oznámení vracet buď true, nebo false. True musí vracet vždycky, pokud neselže některá z akcí, kterou se v důsledku oznámení pokusí provést.

* Toto selhání může být nahlášené službě Intune. Příkladem scénáře nahlášení je situace, kdy správce IT iniciuje vymazání dat uživatele a aplikaci se pak nepodaří data vymazat.

>[!NOTE]
> Blokování v `MAMNotificationReceiver.onReceive` je bezpečné, protože zpětné volání neběží na vlákně uživatelského rozhraní.

Rozhraní `MAMNotificationReceiver` tak, jak je definované v sadě SDK, vidíte níže:

```java
/**
 * The SDK is signaling that a MAM event has occurred.
 *
 */
public interface MAMNotificationReceiver {

    /**
     * A notification was received.
     *
     * @param notification
     *            The notification that was received.
     * @return The receiver should return true if it handled the
     *   notification without error (or if it decided to ignore the
     *   notification). If the receiver tried to take some action in
     *   response to the notification but failed to complete that
     *   action it should return false.
     */
    boolean onReceive(MAMNotification notification);
}
```

### <a name="types-of-notifications"></a>Typy oznámení

Následující oznámení se odesílají do aplikace a některá z nich můžou vyžadovat zapojení aplikace:

* **WIPE_USER_DATA**: Toto oznámení se posílá ve třídě `MAMUserNotification`. Po přijetí tohoto oznámení *musí* aplikace odstranit všechna data přidružená ke spravované identitě (z `MAMUserNotification.getUserIdentity()` ). K oznámení může dojít z různých důvodů, včetně toho, kdy vaše aplikace volá `unregisterAccountForMAM` , když správce IT iniciuje vymazání nebo když zásady podmíněného přístupu vyžadované správcem nejsou splněné. Pokud se vaše aplikace pro toto oznámení neregistruje, provede se výchozí chování při vymazání. Výchozí chování odstraní všechny soubory pro aplikaci s jedinou identitou nebo všechny soubory označené spravovanou identitou pro aplikaci s více identitami. Toto oznámení nebude nikdy odesláno ve vlákně uživatelského rozhraní.

* **WIPE_USER_AUXILIARY_DATA**: Aplikace si můžou zaregistrovat toto oznámení, pokud má sada Intune App SDK provést výchozí selektivní vymazání a mají se při tom odebrat ještě některá pomocná data. Toto oznámení není k dispozici pro jedinou identitu – aplikace – bude odesláno pouze aplikacím s více identitami. Toto oznámení nebude nikdy odesláno ve vlákně uživatelského rozhraní.

* **REFRESH_POLICY**: Toto oznámení se posílá ve třídě `MAMUserNotification`. Po přijetí tohoto oznámení musí být všechna rozhodnutí o zásadách Intune, která vaše aplikace ukládá do mezipaměti, zrušena a aktualizována. Pokud vaše aplikace neukládá žádné předpoklady zásad, nemusí se pro toto oznámení zaregistrovat. Neudělaly se žádné záruky, jako by to vlákno, na které se toto oznámení pošle.

* **REFRESH_APP_CONFIG**: Toto oznámení se posílá v `MAMUserNotification` . Po přijetí tohoto oznámení musí být všechna konfigurační data aplikace uložená v mezipaměti zrušena a aktualizována. Neudělaly se žádné záruky, jako by to vlákno, na které se toto oznámení pošle.

* **MANAGEMENT_REMOVED**: Toto oznámení se posílá ve třídě `MAMUserNotification` a informuje aplikaci, že už nebude spravovaná. Jakmile k ukončení správy dojde, aplikace nebude moct číst šifrované soubory a data zašifrovaná pomocí funkce MAMDataProtectionManager, komunikovat se zašifrovanou schránkou a jinak fungovat v ekosystému spravovaných aplikací. Další podrobnosti najdete níže. Toto oznámení nebude nikdy odesláno ve vlákně uživatelského rozhraní.

* **MAM_ENROLLMENT_RESULT**: Toto oznámení se posílá v rámci `MAMEnrollmentNotification` informování aplikace o tom, že došlo k pokusu o registraci aplikace, a k poskytnutí stavu tohoto pokusu. Neudělaly se žádné záruky, jako by to vlákno, na které se toto oznámení pošle.

* **COMPLIANCE_STATUS**: Toto oznámení se posílá v rámci `MAMComplianceNotification` informování aplikace o výsledku pokusu o nápravu v souladu s dodržováním předpisů. Neudělaly se žádné záruky, jako by to vlákno, na které se toto oznámení pošle.

> [!NOTE]
> Aplikace by nikdy neměla zaregistrovat oznámení `WIPE_USER_DATA` i `WIPE_USER_AUXILIARY_DATA`.

### <a name="management_removed"></a>MANAGEMENT_REMOVED

`MANAGEMENT_REMOVED`Oznámení indikuje, že dřív spravovaný uživatel zásad už nebude spravovat zásada mam Intune. To nevyžaduje vymazání uživatelských dat nebo odhlášení uživatele (pokud bylo vymazávání vyžadováno, `WIPE_USER_DATA` oznámení se pošle). Mnoho aplikací nemusí toto oznámení vůbec zpracovat, ale aplikace, které by používaly, `MAMDataProtectionManager` by [si toto](#data-protection)oznámení musely poznamenat.

Když MAM volá `MANAGEMENT_REMOVED` přijímač aplikace, bude platit následující:
* MAM už dešifroval dříve šifrované soubory (ale ne chráněné vyrovnávací paměti dat) patřící do aplikace. Soubory ve veřejných umístěních na sdcard, které nepatří přímo do aplikace (např. dokumenty nebo složky pro stahování), se nešifrují.
* Nové soubory nebo chráněné vyrovnávací paměti dat vytvořené metodou přijímače (nebo jakýmkoli jiným kódem spuštěným po spuštění příjemce) nebudou zašifrovány.
* Aplikace má stále přístup k šifrovacím klíčům, takže operace, jako jsou například vyrovnávací paměti dat dešifrování, budou úspěšné.

Jakmile se příjemce vaší aplikace vrátí, už nebude mít přístup k šifrovacím klíčům.

## <a name="configure-azure-active-directory-authentication-library-adal"></a>Konfigurace knihovny ADAL (Azure Active Directory Authentication Library)

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

Nejprve si přečtěte pokyny pro integraci knihovny ADAL, které najdete v [úložišti na GitHubu](https://github.com/AzureAD/azure-activedirectory-library-for-android).

Sada SDK spoléhá na [knihovnu ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) s jejími scénáři [ověření](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) a podmíněného spuštění, což vyžaduje, aby byly aplikace nakonfigurovány s [Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-whatis/). Hodnoty konfigurace se předávají sadě SDK prostřednictvím metadat AndroidManifest.

Když chcete konfigurovat svoji aplikaci a povolit správné ověření, přidejte do uzlu aplikace v souboru AndroidManifest.xml následující kód. Některé z těchto konfigurací jsou potřeba, jen když vaše aplikace používá ADAL pro ověřování obecně; v takovém případě budete potřebovat konkrétní hodnoty, které vaše aplikace používá k registraci v AAD. To slouží k zajištění, že koncovému uživateli se nezobrazí výzva k ověření dvakrát kvůli tomu, že AAD rozpozná hodnoty dvou samostatných registrací: jedné z aplikace a jedné ze sady SDK.

```xml
<meta-data
    android:name="com.microsoft.intune.mam.aad.Authority"
    android:value="https://AAD authority/" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.ClientID"
    android:value="your-client-ID-GUID" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.NonBrokerRedirectURI"
    android:value="your-redirect-URI" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.SkipBroker"
    android:value="[true | false]" />
```

### <a name="adal-metadata"></a>Metadata knihovny ADAL

* **Authority** je používaná autorita AAD. Pokud tato hodnota chybí, použije se veřejné prostředí AAD.
    > [!NOTE]
    > Toto pole nenastavujte, pokud aplikace podporuje suverénní cloud.

* **ClientID** je identifikátor AAD ClientID (označovaný také jako ID aplikace), který se má použít. Pokud je zaregistrované ve službě Azure AD, měli byste použít vlastní ClientID vaší aplikace, nebo můžete použít [výchozí registraci](#default-enrollment-optional) , pokud Neintegruje ADAL.

* **NonBrokerRedirectURI** je identifikátor URI pro přesměrování AAD, který se používá, pokud není zprostředkovatel. Pokud není zadaný, použije se výchozí hodnota `urn:ietf:wg:oauth:2.0:oob`. Tato hodnota se hodí pro většinu aplikací.

  * NonBrokerRedirectURI se používá pouze v případě, že SkipBroker je "true".

* **SkipBroker** se používá k přepsání výchozího chování při zapojení jednotného přihlašování do ADAL. SkipBroker by mělo být zadáno pouze pro aplikace, které určují ClientID **a** nepodporují jednotné přihlašování pro jednotné ověřování/pro zařízení. V takovém případě by měl být nastaven na hodnotu "true". Většina aplikací by neměla nastavit parametr SkipBroker.

  * V manifestu **musí** být zadáno ClientID, aby bylo možné zadat hodnotu SkipBroker.

  * Je-li zadán parametr ClientID, je použita výchozí hodnota false (NEPRAVDA).

  * Pokud je SkipBroker "true", bude použit NonBrokerRedirectURI. Aplikace, které neintegrují ADAL (a tudíž nemají žádné ClientID), budou ve výchozím nastavení také "true".

### <a name="common-adal-configurations"></a>Obvyklé konfigurace ADAL

V této části najdete běžné způsoby konfigurace aplikace s knihovnou ADAL. Vyhledejte konfiguraci vaší aplikace a nastavte parametry metadat ADAL (viz výše) na požadované hodnoty. Ve všech případech může být autorita zadána, pokud je požadovaná pro jiná než výchozí prostředí. Pokud tento parametr nezadáte, použije se veřejná provozní autorita AAD.

#### <a name="1-app-does-not-integrate-adal"></a>1. aplikace Neintegruje ADAL.
Metadata ADAL **nesmí** být v manifestu přítomna.

#### <a name="2-app-integrates-adal"></a>2. aplikace integruje ADAL.

|Požadovaný parametr ADAL| Hodnota |
|--|--|
| ClientID | ClientID aplikace (u zaregistrovaných aplikací je generuje AzureAD) |

V případě potřeby může být určena autorita.

Aplikaci musíte zaregistrovat v Azure AD a dát aplikaci přístup ke službě zásady ochrany aplikací:
* Informace o registraci aplikace s Azure AD najdete [tady](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).
* Zajistěte, aby byla dodržena oprávnění aplikace pro Android ke službě zásady ochrany aplikací (APP). Postupujte podle pokynů v [příručce Začínáme s Intune SDK](https://docs.microsoft.com/intune/app-sdk-get-started#next-steps-after-integration) v části "poskytnutí přístupu aplikace ke službě Intune App Protection (volitelné)". 

Podívejte se také na požadavky pro [podmíněný přístup](#conditional-access), které najdete níže.


#### <a name="3-app-integrates-adal-but-does-not-support-brokered-authenticationdevice-wide-sso"></a>3. aplikace integruje ADAL, ale nepodporuje zprostředkované ověřování/jednotné přihlašování pro zařízení.

|Požadovaný parametr ADAL| Hodnota |
|--|--|
| ClientID | ClientID aplikace (u zaregistrovaných aplikací je generuje AzureAD) |
| SkipBroker | **True** |

V případě potřeby můžete zadat pole Authority a NonBrokerRedirectURI.


### <a name="conditional-access"></a>Podmíněný přístup
Podmíněný přístup je [funkce](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer) služby Azure Active Directory, pomocí níž je možné řídit přístup k prostředkům AAD. [Správci Intune mohou definovat pravidla podmíněného přístupu](https://docs.microsoft.com/intune/conditional-access), která umožní přístup k prostředkům pouze ze zařízení nebo aplikací spravovaných v Intune. Pokud chcete zajistit, že aplikace bude mít v případě potřeby přístup k prostředkům, postupujte podle kroků uvedených níže. Pokud vaše aplikace nevyžaduje přístupové tokeny AAD nebo používá pouze prostředky, které nelze chránit podmíněným přístupem, můžete tento postup přeskočit.

1. Postupujte podle [pokynů k integraci ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android#how-to-use-this-library). 
   Zvláštní pozornost věnujte kroku 11, který se týká použití zprostředkovatele.
2. [Zaregistrujte si aplikaci ve službě Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration). 
   Identifikátor URI pro přesměrování najdete v pokynech k integraci ADAL uvedených výše.
3. Nastavte parametry metadat manifestu pro jednotlivé [běžné konfigurace ADAL](#common-adal-configurations), položka 2 výše.
4. Otestujte, že je vše nakonfigurováno správně. Uděláte to tak, že povolíte [podmíněný přístup na základě zařízení](https://docs.microsoft.com/intune/conditional-access-intune-common-ways-use) na portálu [Azure Portal](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExchangeConnectorMenu/aad/connectorType/2) a zkontrolujete následující:
    - Při přihlášení k aplikaci se zobrazí výzva k instalaci registraci Portálu společnosti Intune.
    - Po registraci se přihlášení k aplikaci úspěšně dokončí.
5. Jakmile vaše aplikace dokončí integraci Intune APP SDK, kontaktujte, msintuneappsdk@microsoft.com aby se přidal do seznamu schválených aplikací pro [podmíněný přístup na základě aplikace](https://docs.microsoft.com/intune/conditional-access-intune-common-ways-use#app-based-conditional-access) .
6. Po přidání aplikace do seznamu schválených aplikací ji ověřte pomocí [konfigurace podmíněného přístupu na základě aplikace](https://docs.microsoft.com/intune/app-based-conditional-access-intune-create) a ujistěte se, že se přihlášení k aplikaci úspěšně dokončí.

## <a name="app-protection-policy-without-device-enrollment"></a>Zásady ochrany aplikací bez registrace zařízení

### <a name="overview"></a>Přehled
Zásady ochrany aplikací služby Intune bez registrace zařízení, označované také jako APP-WE nebo MAM-WE, umožňují správu aplikací přes Intune bez nutnosti registrace zařízení do Intune MDM. APP-WE funguje jak s registrací, tak i bez ní. Ačkoliv musí být na zařízení stále nainstalovaná aplikace Portál společnosti, nemusí se k ní uživatel přihlašovat ani dané zařízení registrovat.

> [!NOTE]
> Všechny aplikace musí podporovat zásady ochrany aplikací bez registrace zařízení.

### <a name="workflow"></a>Pracovní postup

Jakmile aplikace vytvoří nový uživatelský účet, měla by ho zaregistrovat ke správě sadou Intune App SDK. Ta zajistí podrobnosti registrace aplikace ke službě APP-WE, a pokud dojde k chybě, bude pokusy o registraci opakovat ve vhodných časových intervalech.

Aplikace se také může sady Intune App SDK dotazovat na stav zaregistrovaného uživatele, pokud potřebuje určit, jestli by měl být takovému uživateli zablokován přístup k podnikovému obsahu. Ke správě je možné zaregistrovat více účtů, ale aktivní registrace ke službě APP-WE je aktuálně možná vždy jen pro jeden účet. To znamená, že zásady ochrany aplikací se nemůžou vztahovat na více účtů aplikace současně.

Aplikace musí provést zpětné volání, aby mohla jménem sady SDK získat z knihovny ADAL příslušné přístupové tokeny. Předpokládá se, že aplikace už pro ověřování uživatelů ADAL využívá a získává vlastní přístupové tokeny.

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

Pokud aplikace zcela odebere účet, měla by ho také odregistrovat a tím aplikaci sdělit, že se na tohoto uživatele už nemají vztahovat zásady. Pokud byl uživatel zaregistrován ke službě MAM, dojde ke zrušení jeho registrace a vymazání aplikace.


### <a name="overview-of-app-requirements"></a>Přehled požadavků na aplikaci

Pro implementaci integrace služby APP-WE musí aplikace zaregistrovat uživatelský účet v sadě MAM SDK:

1. Aplikace _musí_ implementovat a zaregistrovat instanci rozhraní `MAMServiceAuthenticationCallback`. Instance zpětného volání by se měla do životního cyklu aplikace zaregistrovat co nejdříve (obvykle v metodě `onMAMCreate()` třídy aplikace).

2. Po vytvoření uživatelského účtu a úspěšném přihlášení uživatele k ADAL _musí_ aplikace volat `registerAccountForMAM()`.

3. Po odebrání uživatelského účtu by měla aplikace voláním `unregisterAccountForMAM()` odstranit účet ze správy Intune.

    > [!NOTE]
    > Pokud se uživatel z aplikace dočasně odhlásí, není nutné, aby aplikace `unregisterAccountForMAM()` volala. Volání by mohlo inicializovat vymazání, které by uživateli odebralo veškerá podniková data.


### <a name="mamenrollmentmanager"></a>MAMEnrollmentManager

Všechna potřebná rozhraní API pro ověřování a registraci najdete v rozhraní `MAMEnrollmentManager`. Odkaz na `MAMEnrollmentManager` je možné získat tímto způsobem:

```java
MAMEnrollmentManager mgr = MAMComponents.get(MAMEnrollmentManager.class);

// make use of mgr
```

Je zaručeno, že vrácená instance rozhraní `MAMEnrollmentManager` nemá hodnotu null. Metody API spadají do dvou kategorií: **ověřování** a **registrace účtů**.

```java
package com.microsoft.intune.mam.policy;

public interface MAMEnrollmentManager {
    public enum Result {
        AUTHORIZATION_NEEDED,
        NOT_LICENSED,
        ENROLLMENT_SUCCEEDED,
        ENROLLMENT_FAILED,
        WRONG_USER,
        MDM_ENROLLED,
        UNENROLLMENT_SUCCEEDED,
        UNENROLLMENT_FAILED,
        PENDING,
        COMPANY_PORTAL_REQUIRED;
    }

    //Authentication methods
    interface MAMServiceAuthenticationCallback {
        String acquireToken(String upn, String aadId, String resourceId);
    }
    void registerAuthenticationCallback(MAMServiceAuthenticationCallback callback);
    void updateToken(String upn, String aadId, String resourceId, String token);

    //Registration methods
    void registerAccountForMAM(String upn, String aadId, String tenantId);
    void registerAccountForMAM(String upn, String aadId, String tenantId, String authority);
    void unregisterAccountForMAM(String upn);
    Result getRegisteredAccountStatus(String upn);
}
```

### <a name="account-authentication"></a>Ověřování účtů

V této části jsou popsány metody API pro ověřování, které jsou součástí rozhraní `MAMEnrollmentManager`, a způsob jejich použití.

```java
interface MAMServiceAuthenticationCallback {
    String acquireToken(String upn, String aadId, String resourceId);
}
void registerAuthenticationCallback(MAMServiceAuthenticationCallback callback);
void updateToken(String upn, String aadId, String resourceId, String token);
```

1. Aby bylo možné povolit sadě SDK žádat token ADAL pro daného uživatele a ID prostředku, musí aplikace implementovat rozhraní `MAMServiceAuthenticationCallback`. Voláním metody `registerAuthenticationCallback()` musí být rozhraní `MAMEnrollmentManager` poskytnutá instance zpětného volání. V brzké fázi životního cyklu aplikace může být token potřeba k pokusům o registraci nebo ohlášení aktualizací zásad ochrany aplikací, takže zpětné volání je nejlepší zaregistrovat v metodě `onMAMCreate()` podtřídy `MAMApplication` aplikace.

  > [!NOTE]
  > Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

2. Metoda `acquireToken()` by měla získat přístupový token pro požadované ID prostředku daného uživatele. Pokud ho získat nedokáže, měla by vrátit hodnotu null.

    > [!NOTE]
    > Ujistěte se, že vaše aplikace využívá `resourceId` `aadId` parametry a předané do `acquireToken()` tak, aby byl získán správný token.

    ```java
    class MAMAuthCallback implements MAMServiceAuthenticationCallback {
        public String acquireToken(String upn, String aadId, String resourceId) {
            return mAuthContext.acquireTokenSilentSync(resourceId, ClientID, aadId).getAccessToken();
        }
    }
    ```

3. V případě, že aplikace při volání metody `acquireToken()` sady SDK nedokáže token poskytnout (například tehdy, když se nezdaří bezobslužné ověření a není vhodná doba na zobrazení uživatelského rozhraní), může tak učinit později po volání metody `updateToken()`. Volání metody `updateToken()` musí kromě samotného tokenu předat také stejný hlavní název uživatele, ID AAD a ID prostředku, jako požadovalo předchozí volání (`acquireToken()`). Aplikace by měla tuto metodu volat co nejdříve poté, co dané zpětné volání vrátilo hodnotu null.

    > [!NOTE]
    > Sada SDK se bude snažit získat token pravidelným voláním metody `acquireToken()`, takže volání metody `updateToken()` není bezpodmínečně nutné. Důrazně se ale doporučuje, protože může včas pomáhat registraci a vracení zásad ochrany aplikací.


### <a name="account-registration"></a>Registrace účtů

V této části jsou popsány metody API pro registraci účtů, které jsou součástí rozhraní `MAMEnrollmentManager`, a způsob jejich použití.

```java
void registerAccountForMAM(String upn, String aadId, String tenantId);
void registerAccountForMAM(String upn, String aadId, String tenantId, String authority);
void unregisterAccountForMAM(String upn);
Result getRegisteredAccountStatus(String upn);
```

1. Aby bylo možné zaregistrovat účet ke správě, měla by aplikace provést volání metody `registerAccountForMAM()`. Uživatelský účet definuje jeho hlavní název uživatele a ID uživatele služby AAD. K přidružení dat zápisu ke klientovi AAD příslušného uživatele je také potřeba ID klienta. Může být taky poskytnutá autorita uživatele, která umožňuje registraci pro konkrétní cloudy svrchovaného prostředí. Další informace najdete v části [svrchovaná registrace do cloudu](#sovereign-cloud-registration).  Sada SDK se může pokusit zaregistrovat aplikaci pro daného uživatele ve službě MAM. Pokud se registrace nezdaří, bude pokusy o registraci pravidelně opakovat až do doby, než dojde ke zrušení registrace účtu. Časový interval mezi jednotlivými pokusy je obvykle 12 až 24 hodin. Sada SDK informuje o stavu pokusů o registraci asynchronně prostřednictvím oznámení.

2. Vzhledem k tomu, že je vyžadováno ověřování AAD, je nejlepší čas k registraci uživatelského účtu po přihlášení uživatele k aplikaci a úspěšném ověření pomocí ADAL. ID AAD a ID tenanta uživatele se vrátí z ověřovacího volání ADAL jako součást [`AuthenticationResult`](https://github.com/AzureAD/azure-activedirectory-library-for-android) objektu.
    * ID klienta pochází z metody `AuthenticationResult.getTenantID()`.
    * Informace o uživateli se nachází v podobjektu typu `UserInfo`, který pochází z `AuthenticationResult.getUserInfo()`, a ID uživatele AAD se získává z tohoto objektu voláním metody `UserInfo.getUserId()`.

  > [!NOTE]
  > Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

3. Pokud chcete zrušit registraci účtu ve správě Intune, měla by aplikace provést volání metody `unregisterAccountForMAM()`. Pokud byl účet úspěšně zaregistrován a je spravován, sada SDK zruší jeho registraci a vymaže jeho data. Kromě toho se zastaví pravidelné pokusy o registraci. Sada SDK poskytuje asynchronní stav žádosti o zrušení registrace prostřednictvím oznámení.

### <a name="sovereign-cloud-registration"></a>Registrace v suverénním cloudu

Aplikace [podporující suverénní cloud](https://www.microsoft.com/trustcenter/cloudservices/nationalcloud) **musí** poskytovat `authority` metodě `registerAccountForMAM()`.  Toho lze dosáhnout tím, že v parametrech [1.14.0+](https://github.com/AzureAD/azure-activedirectory-library-for-android/releases/tag/v1.14.0) acquireToken extraQueryParameters knihovny ADAL poskytnete `instance_aware=true` a pak vyvoláte metodu `getAuthority()` u výsledku AuthenticationCallback AuthenticationResult.

```java
mAuthContext.acquireToken(this, RESOURCE_ID, CLIENT_ID, REDIRECT_URI, PromptBehavior.FORCE_PROMPT, "instance_aware=true",
        new AuthenticationCallback<AuthenticationResult>() {
            @Override
            public void onError(final Exception exc) {
                // authentication failed
            }

            @Override
            public void onSuccess(final AuthenticationResult result) {
                mAuthority = result.getAuthority();
                // handle other parts of the result
            }
        });
```

> [!NOTE]
> Nenastavujte `com.microsoft.intune.mam.aad.Authority` položku meta-data v AndroidManifest.xml.

> [!NOTE]
> Ujistěte se, že je autorita správně nastavena v metodě `MAMServiceAuthenticationCallback::acquireToken()`.

#### <a name="currently-supported-sovereign-clouds"></a>Momentálně podporované suverénní cloudy

1. Cloud Azure pro státní správu USA
2. Microsoft Azure provozovaný společností 21Vianet (Azure Čína)


### <a name="important-implementation-notes"></a>Důležité poznámky k implementaci

#### <a name="authentication"></a>Authentication

* Když aplikace volá `registerAccountForMAM()`, může brzy poté obdržet zpětné volání na rozhraní `MAMServiceAuthenticationCallback`, ale na odlišném vláknu. V ideálním případě aplikace získala svůj vlastní token z knihovny ADAL před registrací účtu za účelem urychlení získání požadovaného tokenu. Pokud aplikace vrátí platný token ze zpětného volání, registrace bude pokračovat a aplikace získá konečný výsledek prostřednictvím oznámení.

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

* V případě, že aplikace nevrátí platný token AAD, konečný výsledek pokusu o registraci bude `AUTHORIZATION_NEEDED`. Pokud aplikace obdrží tento výsledek prostřednictvím oznámení, důrazně se doporučuje urychlit proces registrace tím, že získá token pro uživatele a prostředek, který si dřív požadoval, `acquireToken()` a zavolá `updateToken()` metodu pro zahájení procesu registrace znovu.

* Zaregistrovaná aplikace `MAMServiceAuthenticationCallback` bude taky volána k získání tokenu pro pravidelná vrácení se změnami zásad ochrany aplikací. Pokud aplikace není schopna poskytnout token, když se požaduje, nebude dostávat oznámení, ale měla by se pokusit získat token a zavolat `updateToken()` v nejbližším možné době k urychlení procesu vrácení se změnami. V případě neposkytnutí tokenu se při dalším pokusu o ohlášení zpětné volání zopakuje.

* Podpora suverénních cloudů vyžaduje poskytování autority.

#### <a name="registration"></a>Registrace

* Pro usnadnění vaší práce jsou metody registrace idempotentní. `registerAccountForMAM()` například zaregistruje účet a pokusí se o registraci aplikace jen v případě, že účet dosud zaregistrovaný není. Podobně `unregisterAccountForMAM()` zruší registraci účtu jen tehdy, že je aktuálně zaregistrovaný. Následná volání nepředstavují operace, takže opakovaná volání těchto metod nejsou na škodu. Kromě toho propojení mezi voláním těchto metod a zasíláním oznámení o výsledku není garantováno – pokud tedy rozhraní `registerAccountForMAM()` volá už zaregistrovanou identitu, oznámení se nemusí pro tuto identitu poslat. Může se stát, že se odešlou oznámení, která neodpovídají žádným voláním těchto metod, protože sada SDK může na pozadí opakovat pokusy o registraci, stejně jako může být zrušení registrace aktivováno žádostí o vymazání odeslanou službou Intune.

* Metody registrace můžou být volány u libovolného počtu identit, ale úspěšně je možné momentálně zaregistrovat vždy jen jeden uživatelský účet. Pokud se současně nebo přibližně ve stejnou dobu registruje více uživatelských účtů s licencí pro službu Intune, na které se vztahují zásady ochrany aplikací, není jisté, který z nich se skutečně zaregistruje.

* Pokud se chcete dozvědět, jestli je účet zaregistrovaný, můžete zadat dotaz na `MAMEnrollmentManager`. Pomocí metody `getRegisteredAccountStatus()` také zjistíte jeho aktuální stav. Pokud účet není zaregistrovaný, vrátí metoda výsledek **null**. V opačném případě vrátí metoda stav účtu v rámci výčtu `MAMEnrollmentManager.Result`.

### <a name="result-and-status-codes"></a>Kódy výsledku a stavové kódy

Po registraci se účet nachází ve stavu `PENDING`, který značí, že prvotní pokus o registraci ve službě MAM ještě není dokončený. Jakmile se pokus o registraci dokončí, odešle se oznámení obsahující některý z kódů výsledku uvedených v tabulce níže. Kromě toho vrátí metoda `getRegisteredAccountStatus()` informaci o stavu účtu, aby mohla aplikace vždy určit, jestli nemá daný uživatel zablokovaný přístup k podnikovému obsahu. Pokud se pokus o registraci nezdaří, stav účtu se může postupem času změnit s tím, jak sada SDK opakuje další pokusy na pozadí.

|Kód výsledku | Vysvětlení |
| -- | -- |
| `AUTHORIZATION_NEEDED` | Tento výsledek indikuje, že se token neposkytl registrovanou `MAMServiceAuthenticationCallback` instancí aplikace, nebo poskytnutý token je neplatný.  Aplikace by měla získat platný token a pokud možno provést volání `updateToken()`. |
| `NOT_LICENSED` | Uživatel nemá licenci na službu Intune, nebo byl pokus o spojení se službou Intune MAM neúspěšný.  Aplikace by měla dál běžet v nespravovaném (normálním) stavu a uživatel by neměl být zablokovaný.  Pro případ, že by uživatel v budoucnu licenci získal, budou pravidelně probíhat pokusy o registraci. |
| `ENROLLMENT_SUCCEEDED` | Pokus o registraci proběhl úspěšně nebo už je uživatel zaregistrovaný.  V případě úspěšné registrace se ještě před tímto oznámením zašle oznámení o aktualizaci zásad.  Uživatel by měl mít povolený přístup k podnikovým datům. |
| `ENROLLMENT_FAILED` | Pokus o registraci selhal.  Další podrobnosti najdete v protokolech zařízení.  Aplikace by neměla umožňovat přístup k podnikovým datům v tomto stavu, protože dříve bylo zjištěno, že uživatel má licenci pro Intune. Všechny aplikace by měly zajistit, aby přístup k podnikovým datům byl neautorizovaný, dokud vaše aplikace nezíská enrollment_succeeded.|
| `WRONG_USER` | Ke službě MAM může aplikaci zaregistrovat jen jeden uživatel na dané zařízení. Tento výsledek indikuje, že uživatel, pro kterého se tento výsledek doručí (druhý uživatel), cílí na zásady MAM, ale už je zaregistrovaný jiný uživatel. Vzhledem k tomu, že zásady MAM nejde pro druhého uživatele vyhovět, musí vaše aplikace neumožňovat přístup k datům tohoto uživatele (případně odebráním uživatele z vaší aplikace), pokud není registrace pro tohoto uživatele v pozdějším čase úspěšná. Při současném doručování tohoto `WRONG_USER` výsledku se mam vyzve s možností odebrat existující účet. Pokud uživatel obdrží odpověď lidského uživatele na zjištěnou hodnotu, bude to opravdu možné později zaregistrovat druhého uživatele. Dokud se druhý uživatel zaregistruje, MAM se bude pravidelně pokoušet o registraci. |
| `UNENROLLMENT_SUCCEEDED` | Zrušení registrace bylo úspěšné.|
| `UNENROLLMENT_FAILED` | Žádost o zrušení registrace selhala.  Další podrobnosti najdete v protokolech zařízení. Obecně platí, že k této chybě nedojde, dokud aplikace předá hlavní název uživatele (UPN) (bez hodnoty null nebo prázdné). Neexistuje žádná přímá a spolehlivá náprava, kterou může aplikace trvat. Pokud se tato hodnota obdrží při zrušení registrace platného hlavního názvu uživatele (UPN), ohlaste ji prosím týmu Intune MAM jako chybu.|
| `PENDING` | Probíhá počáteční pokus o registraci pro daného uživatele.  Aplikace může – ale také nemusí – zablokovat přístup k podnikovým datům až do chvíle, kdy se dozví výsledek registrace. |
| `COMPANY_PORTAL_REQUIRED` | Uživatel má licenci na službu Intune, ale aplikaci není možné zaregistrovat, dokud se na zařízení nenainstaluje aplikace Portál společnosti. Sada Intune App SDK se pokusí zablokovat pro daného uživatele přístup k aplikaci a přesměrovat ho na instalaci Portálu společnosti (podrobnosti najdete níže). |


### <a name="company-portal-requirement-prompt-override-optional"></a>Potlačení výzvy k instalaci aplikace Portál společnosti (volitelné)

Při obdržení výsledku `COMPANY_PORTAL_REQUIRED` zablokuje sada SDK aktivity využívající identitu, pro kterou byla registrace žádána. Místo toho sada SDK zajistí, aby tyto aktivity zobrazily výzvu ke stažení aplikace Portál společnosti. Pokud nechcete, aby k takovému chování došlo, můžou aktivity implementovat metodu `MAMActivity.onMAMCompanyPortalRequired`.

Tato metoda se volá ještě před tím, než sada SDK zobrazí svou výchozí zprávu o blokování. Pokud aplikace změní identitu aktivity nebo zruší registraci uživatele, který se pokusil o registraci, sada SDK tuto aktivitu nezablokuje. V takové situaci je na aplikaci, aby předešla úniku podnikových dat. Identitu aktivity budou moct změnit pouze aplikace s více identitami (popsané dále).

Pokud explicitně nezdědíte `MAMActivity` (protože tuto změnu provedou nástroje sestavení), ale potřebujete toto oznámení zpracovat, můžete místo toho implementovat `MAMActivityBlockingListener`.

### <a name="notifications"></a>Oznámení

Pokud aplikace zaregistruje oznámení typu **MAM_ENROLLMENT_RESULT**, pošle se žádost, aby se `MAMEnrollmentNotification` aplikace informovala o dokončení žádosti o registraci. Prostřednictvím rozhraní `MAMNotificationReceiver` se bude zasílat `MAMEnrollmentNotification` (viz část [Registrace k oznámením z SDK](#register-for-notifications-from-the-sdk)).

```java
public interface MAMEnrollmentNotification extends MAMUserNotification {
    MAMEnrollmentManager.Result getEnrollmentResult();
}
```

Metoda `getEnrollmentResult()` vrací výsledek žádosti o registraci.  Vzhledem k tomu, že `MAMEnrollmentNotification` rozšiřuje `MAMUserNotification`, bude také k dispozici informace o identitě uživatele, za kterého byl pokus o registraci proveden. Aby bylo možné dostávat tato oznámení, musí aplikace implementovat rozhraní `MAMNotificationReceiver`. Další informace o oznámeních najdete v části [Registrace k oznámením z SDK](#register-for-notifications-from-the-sdk).

Stav zaregistrovaného uživatelského účtu se může po přijetí oznámení o registraci změnit, ale ve všech případech se nezmění (například pokud `AUTHORIZATION_NEEDED` je oznámení obdrženo po více informativních výsledcích, jako je například `WRONG_USER` , bude se uchovávat další informativní výsledek jako stav účtu).  Po úspěšné registraci účtu zůstane stav shodný s tím, že se `ENROLLMENT_SUCCEEDED` účet nebude registrovat nebo není smazán.


## <a name="app-ca-with-policy-assurance"></a>CA aplikace se zárukou zásad

### <a name="overview"></a>Přehled
S využitím certifikační autority aplikace (podmíněný přístup) se zásadou zabezpečení je přístup k prostředkům podmíněný na základě zásad Intune App Protection.  Služba AAD to vynutila tím, že vyžaduje, aby se aplikace zaregistrovala a spravovala aplikací předtím, než udělí token pro přístup k CA aplikace s chráněným prostředkem zásad.  Aplikace musí používat zprostředkovatele ADAL pro získání tokenu a instalace je stejná, jak je popsáno výše v části [podmíněný přístup](#conditional-access).

### <a name="adal-changes"></a>ADAL – změny
Knihovna ADAL má nový kód chyby, který informuje aplikaci o tom, že selhání získání tokenu bylo způsobeno tím, že není kompatibilní se správou aplikací.  Pokud aplikace obdrží tento kód chyby, musí volat sadu SDK, aby se pokusila opravit dodržování předpisů tím, že zaregistruje aplikaci a použije zásady. Metodou ADAL bude přijata výjimka, která `onError()` `AuthenticationCallback` bude obsahovat kód chyby `ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED` .  V takovém případě může být výjimka převedena na `IntuneAppProtectionPolicyRequiredException` , ze kterého mohou být extrahovány další parametry pro použití v Oprava dodržování předpisů (viz Ukázka kódu níže). Po úspěšné opravě se aplikace může znovu pokusit o získání tokenu prostřednictvím ADAL.

> [!NOTE]
> Tento nový kód chyby a další podpora pro certifikační autoritu aplikací pomocí zásad správy vyžaduje verzi 1.15.0 (nebo vyšší) knihovny ADAL.

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

### <a name="mamcompliancemanager"></a>MAMComplianceManager

`MAMComplianceManager`Rozhraní se používá v případě, že je v ADAL přijata chyba požadovaná zásadou.  Obsahuje `remediateCompliance()` metodu, která by měla být volána k pokusu o vložení aplikace do stavu kompatibility. Odkaz na `MAMComplianceManager` je možné získat tímto způsobem:

```java
MAMComplianceManager mgr = MAMComponents.get(MAMComplianceManager.class);

// make use of mgr
```

Je zaručeno, že vrácená instance rozhraní `MAMComplianceManager` nemá hodnotu null.

```java
package com.microsoft.intune.mam.policy;

public interface MAMComplianceManager {
    void remediateCompliance(String upn, String aadId, String tenantId, String authority, boolean showUX);
}
```

`remediateCompliance()`Metoda je volána k pokusu o vložení aplikace pod správu, aby splňovala podmínky pro AAD, které udělují požadovaný token.  První čtyři parametry lze extrahovat z výjimky přijaté `AuthenticationCallback.onError()` metodou ADAL (viz Ukázka kódu níže).  Konečný parametr je logická hodnota, která určuje, jestli se při pokusu o dodržování předpisů zobrazuje uživatelské rozhraní.  Toto je jednoduché rozhraní pro zablokování, které se poskytuje jako výchozí pro aplikace, které v průběhu této operace nemusejí zobrazovat přizpůsobené uživatelské prostředí.  Bude blokovat jenom tehdy, když probíhá náprava dodržování předpisů a výsledný výsledek se nezobrazí.  Aplikace by měla zaregistrovat přijímač oznámení, aby zpracovával úspěch nebo neúspěch pokusu o nápravu dodržování předpisů (viz níže).

`remediateCompliance()`Metoda může provést registraci mam jako součást zřizování dodržování předpisů.  Aplikace může obdržet oznámení o registraci, pokud zaregistroval příjemce oznámení pro oznámení o registraci.  Zaregistrovaná aplikace `MAMServiceAuthenticationCallback` bude mít `acquireToken()` zavolanou metodu pro získání tokenu pro registraci mam. `acquireToken()` bude volána před tím, než aplikace získá svůj vlastní token, takže všechny úlohy vytváření účtů nebo účtů, které aplikace provede po úspěšném pořízení tokenu, ještě nemusí být provedeny.  Zpětné volání musí být schopné získat token v tomto případě.  Pokud nemůžete vrátit token z `acquireToken()` , pokus o nápravu kompatibility se nezdaří.  Pokud později zavoláte `updateToken()` s platným tokenem pro požadovaný prostředek, náprava kompatibility se zopakuje okamžitě se zadaným tokenem.

> [!NOTE]
> Získání tichého tokenu bude stále možné v nástroji, `acquireToken()` protože uživatel již byl vytvořen s možností instalace zprostředkovatele a registraci zařízení před `ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED` přijetím chyby.  Výsledkem je, že zprostředkovatel má v mezipaměti platný obnovovací token, který umožňuje úspěšné tiché získání požadovaného tokenu.

Tady je ukázka přijetí chyby vyžadované zásadou v `AuthenticationCallback.onError()` metodě a volání metody, `MAMComplianceManager` která chybu zpracovává.

```java
public void onError(@Nullable Exception exc) {
    if (exc instanceof AuthenticationException && 
        ((AuthenticationException) exc).getCode() == ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED) {

        final IntuneAppProtectionPolicyRequiredException policyRequiredException = 
            (IntuneAppProtectionPolicyRequiredException) ex;

        final String upn = policyRequiredException.getAccountUpn();
        final String aadId = policyRequiredException.getAccountUserId();
        final String tenantId = policyRequiredException.getTenantId();
        final String authority = policyRequiredException.getAuthorityURL();

        MAMComplianceManager complianceManager = MAMComponents.get(MAMComplianceManager.class);
        complianceManager.remediateCompliance(upn, aadId, tenantId, authority, showUX);
    }
}
```

### <a name="status-notifications"></a>Oznámení o stavu

Pokud aplikace zaregistruje oznámení typu **COMPLIANCE_STATUS**, `MAMComplianceNotification` pošle se za účelem informování aplikace o konečném stavu pokusu o nápravu dodržování předpisů. Prostřednictvím rozhraní `MAMNotificationReceiver` se bude zasílat `MAMComplianceNotification` (viz část [Registrace k oznámením z SDK](#register-for-notifications-from-the-sdk)).

```java
public interface MAMComplianceNotification extends MAMUserNotification {
    MAMCAComplianceStatus getComplianceStatus();
    String getComplianceErrorTitle();
    String getComplianceErrorMessage();
}
```

`getComplianceStatus()`Metoda vrátí výsledek pokusu o nápravu kompatibility jako hodnotu z `MAMCAComplianceStatus` výčtu.

|Stavový kód | Vysvětlení |
| -- | -- |
| Neznámý | Stav není známý. To může znamenat neočekávaný důvod selhání. Další informace najdete v protokolech Portál společnosti. |
| KOMPATIBILNÍ | Náprava dodržování předpisů byla úspěšná a aplikace je teď kompatibilní se zásadami. Získání tokenu ADAL by se mělo opakovat. |
| NOT_COMPLIANT | Pokus o nápravu dodržování předpisů se nezdařil.  Aplikace není kompatibilní a získání tokenu ADAL by se nemělo opakovat, dokud neopravíte chybový stav.  Další informace o chybě se odesílají s MAMComplianceNotification. |
| SERVICE_FAILURE | Došlo k chybě při pokusu o načtení dat dodržování předpisů ze služby Intune. Další informace najdete v protokolech Portál společnosti. |
| NETWORK_FAILURE | Při připojování ke službě Intune došlo k chybě. Aplikace by se po obnovení připojení k síti měla znovu pokusit o získání tokenu. |
| CLIENT_ERROR | Pokus o nápravu dodržování předpisů se nezdařil z nějakého důvodu týkajícího se klienta.  Například bez tokenu nebo špatného uživatele. Další informace o chybě se odesílají s MAMComplianceNotification. |
| PENDING | Pokus o nápravu dodržování předpisů se nezdařil, protože při překročení časového limitu nebyla od služby přijata odpověď na stav. Aplikace by se měla znovu pokusit o získání tokenu později. |
| COMPANY_PORTAL_REQUIRED | Aby bylo možné úspěšně provést nápravu dodržování předpisů, musí být na zařízení nainstalovaná Portál společnosti.  Pokud je už Portál společnosti na zařízení nainstalovaná, je potřeba restartovat aplikaci.  V takovém případě se zobrazí dialogové okno s výzvou, aby uživatel aplikaci restartoval. |

Pokud je stav dodržování předpisů `MAMCAComplianceStatus.COMPLIANT` , aplikace by měla znovu iniciovat původní pořízení tokenu (pro svůj vlastní prostředek). Pokud se pokus o nápravu kompatibility nezdařil `getComplianceErrorTitle()` , `getComplianceErrorMessage()` metody a vrátí lokalizované řetězce, které může aplikace zobrazit koncovému uživateli, pokud se rozhodne.  Většina chybových případů není aplikací remediable, takže v případě obecného případu může být nejlepším řešením selhání při vytváření nebo přihlašování účtů a umožnit uživateli opakovat akci později.  Pokud je chyba trvalá, může vám protokol MAM určit příčinu.  Koncový uživatel může protokoly odeslat pomocí pokynů, které najdete [tady](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android "Posílání protokolů e-mailem firemní podpoře").

Vzhledem `MAMComplianceNotification` `MAMUserNotification` k tomu, že služba rozšiřuje, je k dispozici také identita uživatele, pro kterého došlo k pokusu o nápravu.

Tady je příklad registrace přijímače pomocí anonymní třídy pro implementaci rozhraní MAMNotificationReceiver:

```java
final MAMNotificationReceiverRegistry notificationRegistry = MAMComponents.get(MAMNotificationReceiverRegistry.class);
// create a receiver
final MAMNotificationReceiver receiver = new MAMNotificationReceiver() {
    public boolean onReceive(MAMNotification notification) {
        if (notification.getType() == MAMNotificationType.COMPLIANCE_STATUS) {
            MAMComplianceNotification complianceNotification = (MAMComplianceNotification) notification;
            
            // take appropriate action based on complianceNotification.getComplianceStatus()
            
            // unregister this receiver if no longer needed
            notificationRegistry.unregisterReceiver(this, MAMNotificationType.COMPLIANCE_STATUS);
        }
        return true;
    }
};
// register the receiver
notificationRegistry.registerReceiver(receiver, MAMNotificationType.COMPLIANCE_STATUS);
```

> [!NOTE]
> Příjemce oznámení musí být před voláním zaregistrován `remediateCompliance()` , aby nedocházelo ke konfliktu časování, který by mohl způsobit vynechání oznámení.

### <a name="implementation-notes"></a>Poznámky k implementaci

> [!NOTE]
> **Důležitá změna!**  <br>
> `MAMServiceAuthenticationCallback.acquireToken()`Metoda aplikace by měla předat *hodnotu false* pro nový `forceRefresh` příznak `acquireTokenSilentSync()` .
> Dřív se vám doporučuje předat *hodnotu true* , aby se vyřešil problém s aktualizací tokenů od zprostředkovatele, ale byl nalezen problém se službou ADAL, který by mohl v některých scénářích zabránit získání tokenů, pokud je tento příznak *pravdivý*.
```java
AuthenticationResult result = acquireTokenSilentSync(resourceId, clientId, userId, /* forceRefresh */ false);
```

> [!NOTE]
> Pokud chcete při pokusu o nápravu zobrazit vlastní blokující uživatelské rozhraní, měli byste předat *hodnotu false* pro parametr showUX `remediateCompliance()` . Před voláním je nutné zkontrolovat, že jste si vyvolali své uživatelské rozhraní a zaregistrujete naslouchací proces oznámení `remediateCompliance()` .  Tím zabráníte konfliktu časování, ve kterém může být oznámení `remediateCompliance()` neúspěšné, pokud je chyba velmi rychlá.  Například `onCreate()` `onMAMCreate()` Metoda nebo podtřídou Activity je ideální místo pro registraci naslouchacího procesu oznámení a pak volání `remediateCompliance()` .  Parametry pro `remediateCompliance()` může být předány do vašeho uživatelského prostředí jako exTray.  Po přijetí oznámení o stavu dodržování předpisů můžete zobrazit výsledek nebo jednoduše dokončit aktivitu.

> [!NOTE]
> `remediateCompliance()` provede registraci účtu a pokus o registraci.  Po získání hlavního tokenu není volání `registerAccountForMAM()` nezbytné, ale neexistuje žádný škodný postup. Na druhé straně, pokud se aplikaci nepovede získat svůj token a chce odebrat uživatelský účet, musí zavolat `unregisterAccountForMAM()` na odebrání účtu a zabránit opakování registrace na pozadí.

## <a name="protecting-backup-data"></a>Ochrana dat zálohy

Od verze Android Marshmallow (API 23) má Android dvě možnosti, jak může aplikace zálohovat svá data. Obě možnosti se dají použít pro vaši aplikaci a k tomu, aby se zajistila správná implementace ochrany dat Intune, je potřeba udělat různé kroky. Přehled akcí požadovaných pro zajištění správné ochrany dat najdete v tabulce níže.  Další informace o metodách zálohování najdete v [průvodci rozhraním Android API](https://developer.android.com/guide/topics/data/backup.html).

### <a name="auto-backup-for-apps"></a>Automatické zálohování pro aplikace

Na zařízeních s Androidem Marshmallow začal Android nabízet aplikacím [automatické úplné zálohování](https://developer.android.com/guide/topics/data/autobackup.html) na Disk Google bez ohledu na cílové rozhraní API aplikace. Pokud v souboru AndroidManifest.xml, explicitně nastavíte `android:allowBackup` na hodnotu **false**, Android nikdy nezařadí vaši aplikaci do fronty pro zálohy a podniková data zůstanou v aplikaci. V takovém případě není potřeba žádná další akce.

Ve výchozím nastavení je ale atribut `android:allowBackup` nastavený na hodnotu True, i když v souboru manifestu není specifikovaný parametr `android:allowBackup`. To znamená, že všechna data aplikace se automaticky zálohují do účtu Disku Google uživatele. Je to výchozí chování, které představuje určité **riziko úniku dat**. Proto sada SDK vyžaduje níže uvedené změny, které zajistí použití ochrany dat.  Pokud chcete svoji aplikaci spouštět na zařízeních s Androidem Marshmallow, měli byste postupovat podle níže uvedených pokynů k zajištění řádné ochrany zákaznických dat.  

Intune vám umožňuje využívat všechny [funkce automatického zálohování](https://developer.android.com/guide/topics/data/autobackup.html), které nabízí Android, včetně možnosti definovat vlastní pravidla v XML, musíte ale zabezpečit svoje data podle tohoto postupu:

1. Pokud vaše aplikace **nepoužívá** vlastní třídu BackupAgent, můžete použitím výchozí třídy MAMBackupAgent povolit automatické úplné zálohy, které splňují zásady Intune. Vložte do manifestu aplikace tento kód:

    ```xml
    android:fullBackupOnly="true"
    android:backupAgent="com.microsoft.intune.mam.client.app.backup.MAMDefaultBackupAgent"
    ```
    
2. **[Volitelné]** Pokud implementujete nepovinnou vlastní třídu BackupAgent, zkontrolujte, že používáte MAMBackupAgent nebo MAMBackupAgentHelper. Více informací najdete v dalších částech. Zvažte možnost použití agenta Intune **MAMDefaultFullBackupAgent** (viz krok 1), který umožňuje v systému Android M a novějších verzích snadné zálohování.

3. Až se rozhodnete, jaký typ plné zálohy by měla vaše aplikace obdržet (nefiltrovaný, filtrovaný nebo žádný), budete muset v aplikaci nastavit atribut `android:fullBackupContent` na hodnotu True, False nebo prostředek XML.

4. Následně _**musíte**_ do značky metadat s názvem `com.microsoft.intune.mam.FullBackupContent` ve vašem manifestu zkopírovat všechno, co vložíte do `android:fullBackupContent`.

    **Příklad 1**: Pokud chcete, aby měla vaše aplikace úplné zálohy bez vyloučení, nastavte atribut `android:fullBackupContent` i značku metadat `com.microsoft.intune.mam.FullBackupContent` na hodnotu **True**:

    ```xml
    android:fullBackupContent="true"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="true" />  
    ```

    **Příklad 2**: Pokud chcete, aby aplikace využívala vaši vlastní třídu BackupAgent a nechcete úplné automatické zálohy splňující zásady Intune, nastavte atribut a značku metadat na hodnotu **False**:

    ```xml
    android:fullBackupContent="false"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="false" />  
    ```

    **Příklad 3**: Pokud chcete, aby měla aplikace úplné zálohy podle vašich vlastních pravidel definovaných v souboru XML, nastavte atribut a značku metadat na stejný prostředek XML:

    ```xml
    android:fullBackupContent="@xml/my_scheme"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:resource="@xml/my_scheme" />  
    ```


### <a name="keyvalue-backup"></a>Zálohování páru klíč-hodnota

Možnost [zálohování páru klíč-hodnota](https://developer.android.com/guide/topics/data/keyvaluebackup.html) zálohuje data aplikací do služby [Android Backup Service](https://developer.android.com/google/backup/index.html) a je k dispozici pro všechna rozhraní API od verze 8. Objem dat na uživatele aplikace je omezen na 5 MB. Pokud zálohování páru klíč-hodnota využíváte, použijte třídu **BackupAgentHelper** nebo **BackupAgent**.

### <a name="backupagenthelper"></a>BackupAgentHelper

Implementace třídy BackupAgentHelper je jednodušší než implementace třídy BackupAgent, a to jak z hlediska nativních funkcí Androidu, tak z hlediska integrace služby Intune MAM. BackupAgentHelper umožňuje vývojáři registrovat celé soubory a sdílené předvolby do třídy **FileBackupHelper** a **SharedPreferencesBackupHelper**, které se pak při vytvoření přidají do třídy BackupAgentHelper. Postup použití třídy BackupAgentHelper se službou Intune MAM je následující:

1. Pokud chcete využívat zálohu více identit s třídou BackupAgentHelper, přečtěte si pokyny o [rozšíření třídy BackupAgentHelper ](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgentHelper) v příručce pro Android.

2. Rozšiřte třídu BackupAgentHelper, FileBackupHelper nebo SharedPreferencesBackupHelper na příslušný ekvivalent ve službě MAM.

|Třída Androidu | Ekvivalent ve službě MAM |
|--|--|
|BackupAgentHelper |MAMBackupAgentHelper |
|FileBackupHelper | MAMFileBackupHelper
|SharedPreferencesBackupHelper| MAMSharedPreferencesBackupHelper|

Pokud se budete držet těchto pokynů, dosáhněte úspěšného zálohování a obnovy více identit.

### <a name="backupagent"></a>BackupAgent

Třída BackupAgent umožňuje explicitnější určení zálohovaných dat. Protože vývojář za implementaci do velké míry zodpovídá, vyžaduje se pro zajištění odpovídající ochrany dat ze služby Intune více kroků. Většina práce bude na vás jakožto na vývojáři a integrace služby Intune se tak zapojí o něco víc.

**Integrace služby MAM:**

1. Aby byla vaše implementace třídy BackupAgent v souladu s pokyny Androidu, pozorně si v příručce pro Android přečtěte informace o [zálohování páru klíč-hodnota](https://developer.android.com/guide/topics/data/keyvaluebackup.html) a hlavně o [rozšíření třídy BackupAgent](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent).

2. Nechte třídu rozšířit na `MAMBackupAgent`.

**Zálohování více identit:**

1. Před zahájením zálohování zkontrolujte, že soubory nebo datové vyrovnávací paměti, kterých se bude tato akce týkat, **mají správcem IT povolené zálohování** ve scénářích s více identitami. Aby to bylo možné určit, nabízíme vám funkci `isBackupAllowed` v `MAMFileProtectionManager` a `MAMDataProtectionManager`. Pokud soubor nebo datová vyrovnávací paměť nemá zálohování povolené, pak byste neměli pokračovat v jejich zahrnování do zálohování.

2. Když v určitém okamžiku během zálohování chcete zálohovat identity pro soubory zkontrolované v kroku 1, je potřeba volat `backupMAMFileIdentity(BackupDataOutput data, File … files)` se soubory, ze kterých plánujete extrahovat data. Tato akce automaticky vytvoří nové entity zálohování a zapíše je za vás do `BackupDataOutput` . Při obnovení se tyto entity automaticky využijí.

**Obnova více identit:**

V části [Rozšíření třídy BackupAgent](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent) příručky zálohování dat najdete obecný algoritmus pro obnovu dat vaší aplikace a ukázku kódu. Pokud má obnova více identit proběhnout úspěšně, je potřeba dodržet obecnou strukturu danou tímto vzorovým kódem a věnovat zvláštní pozornost těmto bodům:

1. Je nutné použít smyčku `while(data.readNextHeader())`*, která projde entity zálohování.

2. Pokud se `data.getKey()`* neshoduje s klíčem zapsaným v `onBackup`, je nutné volat `data.skipEntityData()`*. Pokud tento krok neprovedete, záloha nemusí proběhnout úspěšně.

3. Při zobrazování entit zálohování se v konstruktoru `while(data.readNextHeader())`* nevracejte, protože automaticky zapsané entity budou ztraceny.

* Kde `data` je název místní proměnné pro **MAMBackupDataInput** předaný aplikaci při obnovení.

## <a name="multi-identity-optional"></a>Více identit (volitelné)

### <a name="overview"></a>Přehled
Intune App SDK ve výchozím nastavení uplatní zásady na aplikaci jako celek. Možnost používat více identit je volitelná funkce ochrany aplikací Intune, kterou můžete zapnout, pokud chcete zásady uplatňovat na úrovni jednotlivých identit. K tomu je od aplikace potřeba mnohem větší účast než u ostatních funkcí ochrany aplikací.

> [!NOTE]
> V případě nesprávného zapojení aplikace může dojít k únikům dat a dalším potížím v souvislosti se zabezpečením.

Jakmile uživatel zařízení nebo aplikaci zaregistruje, zaregistruje tuto identitu také sada SDK a bude ji považovat za primární spravovanou identitu Intune. Ostatní uživatelé v aplikaci budou považováni za nespravované s nastavením zásad bez omezení.

> [!NOTE]
> V současné době je podporována jen jedna spravovaná identita Intune pro každé zařízení.

Identita se definuje jako řetězec. Identity rozlišují **malá**a velká písmena a požadavky na sadu SDK pro identitu nemusí vracet stejnou velikost písmen, která byla původně použita při nastavování identity.

Pokud chce aplikace změnit aktivní identitu, musí informovat sadu *SDK*. V některých případech SDK také upozorní aplikaci, že je nutná změna identity. Ve většině případů však správa MAM nemůže vědět, jaká data se zobrazují v uživatelském rozhraní nebo používají u vlákna v daném okamžiku, a spoléhá na to, že aplikace nastaví správnou identitu, která zabrání úniku dat. V následujících částech najdete některé konkrétní scénáře, které vyžadují akci aplikace.

### <a name="enabling-multi-identity"></a>Povolení více identit

Ve výchozím nastavení se všechny aplikace považují za aplikace s jedinou identitou. U aplikace můžete deklarovat, že dokáže rozpoznat více identit tím, že do souboru AndroidManifest.xml umístíte následující metadata.

```xml
  <meta-data
    android:name="com.microsoft.intune.mam.MAMMultiIdentity"
    android:value="true" />
```

### <a name="setting-the-identity"></a>Nastavení Identity

Vývojáři můžou nastavit identitu uživatele aplikace na těchto úrovních se sestupnou prioritou:

  1. Úroveň vlákna
  2. `Context` (obecně `Activity` ) obsah
  3. Úroveň procesu

Identita nastavená na úrovni vlákna nahrazuje identitu nastavenou na úrovni objektu `Context`, která nahrazuje identitu nastavenou na úrovni procesu. Identita nastavená pro `Context` se používá jenom v příslušných přidružených scénářích. Operace v/v souborů nemají například přidruženy `Context` . Nejčastěji budou aplikace nastavovat `Context` identitu na `Activity` . Aplikace *nesmí* zobrazit data pro spravovanou identitu `Activity` , pokud není identita nastavená na stejnou identitu. Obecně je identita na úrovni procesu užitečná pouze tehdy, když pracuje aplikace ve všech vláknech vždy jen s jediným uživatelem. Řada aplikací tuto možnost nemusí potřebovat využít.

Pokud vaše aplikace používá `Application` kontext k získání systémových služeb, ujistěte se, že byla nastavena identita vlákna nebo procesu nebo zda jste nastavili identitu uživatelského rozhraní v kontextu vaší aplikace `Application` .

Pokud vaše aplikace používá `Service` kontext ke spouštění, použití překladačů obsahu nebo k nastavení identity v kontextu, je nutné použít jiné systémové služby `Service` .

Chcete-li zpracovat zvláštní případy při aktualizaci identity uživatelského rozhraní pomocí `setUIPolicyIdentity` nebo `switchMAMIdentity` , lze obě metody předat sadu `IdentitySwitchOption` hodnot.

* `IGNORE_INTENT`: Použijte, pokud požadujete přepínač identity, který by měl ignorovat záměr přidružený k aktuální aktivitě.
  Příklad:

  1. Vaše aplikace obdrží záměr ze spravované identity obsahující spravovaného dokumentu a aplikace zobrazí dokument.
  2. Uživatel přepne na svou osobní identitu, takže vaše aplikace si vyžádá přepínač identity uživatelského rozhraní. V osobní identitě už aplikace nezobrazuje dokument, takže ho použijete `IGNORE_INTENT` při žádosti o přepínač identity.

  Pokud není nastavená, SDK bude předpokládat, že nejnovější záměr se v aplikaci pořád používá. Tím dojde k tomu, že zásady pro novou identitu budou považovat záměr za příchozí data a používat její identitu.

>[!NOTE]
> Vzhledem k tomu, že se `CLIPBOARD_SERVICE` používá pro operace uživatelského rozhraní, sada SDK používá identitu uživatelského rozhraní aktivity popředí pro `ClipboardManager` operace.

Následující metody u třídy `MAMPolicyManager` můžete použít k nastavení identity a načtení dříve nastavených hodnot identity.

```java
public static void setUIPolicyIdentity(final Context context, final String identity, final MAMSetUIIdentityCallback mamSetUIIdentityCallback,
final EnumSet<IdentitySwitchOption> options);

public static String getUIPolicyIdentity(final Context context);

public static MAMIdentitySwitchResult setProcessIdentity(final String identity);

public static String getProcessIdentity();

public static MAMIdentitySwitchResult setCurrentThreadIdentity(final String identity);

public static String getCurrentThreadIdentity();

/**
 * Get the current app policy. This does NOT take the UI (Context) identity into account.
 * If the current operation has any context (e.g. an Activity) associated with it, use the overload below.
 */
public static AppPolicy getPolicy();

/**
 * Get the current app policy. This DOES take the UI (Context) identity into account.
 * If the current operation has any context (e.g. an Activity) associated with it, use this function.
 */
public static AppPolicy getPolicy(final Context context);


public static AppPolicy getPolicyForIdentity(final String identity);

public static boolean getIsIdentityManaged(final String identity);
```

>[!NOTE]
> Identitu aplikace můžete vymazat tím, že ji nastavíte na hodnotu null.
>
> Prázdný řetězec může sloužit jako identita, která nikdy nebude mít zásady ochrany aplikací.

#### <a name="results"></a>Výsledky
Všechny metody nastavení identity vrátí zpět výsledné hodnoty přes `MAMIdentitySwitchResult`. Vrátit se můžou čtyři hodnoty:

| Vrácená hodnota | Scénář |
|--            |--        |
| `SUCCEEDED`    | Změna identity byla úspěšná. |
| `NOT_ALLOWED`  | Změna identity není povolená. K tomu dojde, pokud je proveden pokus o nastavení identity uživatelského rozhraní ( `Context` ), pokud je v aktuálním vlákně nastavena jiná identita. |
| `CANCELLED`    | Uživatel zrušil změnu identity stisknutím tlačítka Zpět po zobrazení výzvy k zadání kódu PIN / ověřování. |
| `FAILED`       | Změna identity se z neznámého důvodu nezdařila.|

Před zobrazením nebo použitím podnikových dat by aplikace měla zajistit, aby byl přepínač identity úspěšný. V současné době bude přepnutí identit procesů a vláken u aplikací s povolenými více identitami vždy úspěšné, vyhrazujeme si ale právo přidat podmínky týkající se chyb. Přepnutí identity uživatelského rozhraní nemusí být úspěšné při neplatných argumentech, pokud by došlo ke konfliktu s identitou vlákna, nebo v případě, že uživatel zruší akci, když se požaduje podmíněné spuštění (například stiskne tlačítko Zpět na obrazovce PIN kódu). Výchozím chováním při přepnutí identity uživatelského rozhraní na aktivitu je dokončení aktivity (viz `onSwitchMAMIdentityComplete` níže).

V případě nastavení `Context` identity prostřednictvím `setUIPolicyIdentity` je výsledek hlášen asynchronně. Pokud `Context` je to `Activity` , sada SDK neví, zda byla změna identity úspěšná, až po podmíněném spuštění, které může vyžadovat, aby uživatel zadal PIN nebo firemní přihlašovací údaje. Aplikace může implementovat a `MAMSetUIIdentityCallback` získat tento výsledek nebo může pro objekt zpětného volání předat hodnotu null. Všimněte si, že pokud je učiněno volání `setUIPolicyIdentity` , zatímco výsledek z předchozího volání `setUIPolicyIdentity` *na stejný kontext* nebyl dosud doručen, nové zpětné volání nahradí starý a původní zpětné volání nikdy neobdrží výsledek.

```java
  public interface MAMSetUIIdentityCallback {
    void notifyIdentityResult(MAMIdentitySwitchResult identitySwitchResult);
  }
```

Namísto volání `MAMPolicyManager.setUIPolicyIdentity` můžete identitu aktivity také nastavit přímo díky metodě na `MAMActivity`. Použijte tuto metodu:

```java
     public final void switchMAMIdentity(final String newIdentity, final EnumSet<IdentitySwitchOption> options);
```

Metodu na `MAMActivity` můžete také přepsat, aby mohla být aplikace informovaná o výsledku pokusů změnit identitu této aktivity.

``` java
    public void onSwitchMAMIdentityComplete(final MAMIdentitySwitchResult result);
```

Pokud nepřepisujete `onSwitchMAMIdentityComplete` (nebo nevoláte `super` metodu), neúspěšný přepínač identity u aktivity způsobí dokončení aktivity. Pokud přepíšete metodu, musíte se starat o to, aby se podniková data nezobrazovala po neúspěšném přepnutí identity.

>[!NOTE]
> Přepnutí identity může vyžadovat nové vytvoření aktivity. Nové instanci aktivity se pak doručí zpětné volání `onSwitchMAMIdentityComplete`.


### <a name="implicit-identity-changes"></a>Implicitní změny identity

Kromě schopnosti aplikace nastavit identitu se může vlákno nebo identita objektu Context změnit na základě příchozího přenosu dat z jiné aplikace spravované prostřednictvím Intune, která používá zásady ochrany aplikací.

#### <a name="examples"></a>Příklady
1. Pokud se aktivita spustí z `Intent` odesílané jiné aplikace mam, nastaví se identita aktivity na základě efektivní identity v jiné aplikaci v bodě `Intent` odeslání.

2. U služeb se identita vlákna nastaví podobně po dobu volání `onStart` nebo `onBind`. Volání do třídy `Binder` vrácená z `onBind` také dočasně nastaví identitu vlákna.

3. Volání do `ContentProvider` podobně nastaví identitu vlákna po dobu jejich trvání.


  Kromě toho interakce uživatele s aktivitou může způsobit přepnutí implicitní identity.

  **Příklad:** Pokud uživatel zruší výzvu k autorizaci během `Resume`, dojde k implicitnímu přepnutí na prázdnou identitu.

  Aplikace bude moct tyto změny rozpoznat a v případě potřeby je může zakázat. Třídy `MAMService` a `MAMContentProvider` zveřejňují následující metodu, kterou můžou podtřídy přepsat:

  ```java
  public void onMAMIdentitySwitchRequired(final String identity,
          final AppIdentitySwitchResultCallback callback);
  ```

  V třídě `MAMActivity` je v metodě k dispozici další parametr:

  ```java
  public void onMAMIdentitySwitchRequired(final String identity,
          final AppIdentitySwitchReason reason,
          final AppIdentitySwitchResultCallback callback);
  ```

  * `AppIdentitySwitchReason` zachycuje zdroj implicitního přepnutí a může přijmout hodnoty `CREATE`, `RESUME_CANCELLED` a `NEW_INTENT`.  Důvod oznámení `RESUME_CANCELLED` se použije, když obnovení aktivity způsobí zobrazení uživatelského rozhraní pro zadání kódu PIN, ověřování nebo jiné dodržování předpisů a uživatel se pokusí toto uživatelské prostředí zrušit, obvykle použitím tlačítka Zpět.


    * `AppIdentitySwitchResultCallback` vypadá takto:

      ```java
      public interface AppIdentitySwitchResultCallback {
          /**
            * @param result
            *            whether the identity switch can proceed.
            */
          void reportIdentitySwitchResult(AppIdentitySwitchResult result);
        }
        ```

      Kde ```AppIdentitySwitchResult``` je `SUCCESS` nebo `FAILURE`.

Metoda `onMAMIdentitySwitchRequired` se volá u všech implicitních změn identity s výjimkou změn provedených třídou Binder, která se vrátila z `MAMService.onMAMBind`. Výchozí implementace `onMAMIdentitySwitchRequired` okamžitě volají:

* `reportIdentitySwitchResult(FAILURE)` je-li důvod `RESUME_CANCELLED` .

* `reportIdentitySwitchResult(SUCCESS)` ve všech ostatních případech.

  Neočekává se, že většina aplikací bude chtít blokovat nebo zpozdit přepnutí identity jinak. Pokud to ale aplikace chce udělat, musíte vzít v úvahu tyto body:

  * Pokud je přepnutí identity blokované, je výsledek stejný, jako kdyby nastavení sdílení `Receive` zakázala příchozí přenos dat.

  * Pokud služba běží na hlavním vlákně, `reportIdentitySwitchResult` **musí** se volat synchronně nebo vlákno uživatelského rozhraní přestane reagovat.

  * Pro **`Activity`** vytváření se `onMAMIdentitySwitchRequired` bude volat před `onMAMCreate` . Pokud musí aplikace zobrazit uživatelské rozhraní, aby určila, jestli má být povolen přepínač identity, musí se toto uživatelské rozhraní zobrazit pomocí *jiné* aktivity.

  * **`Activity`** Pokud je v případě, že je požadován přepínač na prázdnou identitu s odůvodněním `RESUME_CANCELLED` , aplikace musí upravit obnovenou aktivitu a zobrazit tak data konzistentní s tímto přepínačem identity.  Pokud to není možné, aplikace by měla přepnutí odmítnout a uživatel se znovu vyzve k dodržování zásad pro obnovení identity (například zobrazením obrazovky pro zadání kódu PIN).

    > [!NOTE]
    > Aplikace s více identitami bude vždycky přijímat příchozí data ze spravovaných i nespravovaných aplikací. Aplikace musí zacházet s daty ze spravovaných identit řízeně.

  Pokud je požadovaná identita spravovaná (to si ověříte pomocí `MAMPolicyManager.getIsIdentityManaged`), ale aplikace nemůže tento účet používat (například kvůli tomu, že se v aplikaci musí nejprve nastavit e-mailové nebo jiné účty), mělo by se přepnutí identity odmítnout.

#### <a name="build-plugin--tool-considerations"></a>Důležité informace týkající se nástroje nebo modulu plug-in sestavení
Pokud explicitně nedědíte z `MAMActivity` , `MAMService` nebo `MAMContentProvider` (protože povolíte nástrojům sestavení, aby tuto změnu prováděl), ale stále potřebují zpracovat přepínače identity, můžete místo toho implementovat `MAMActivityIdentityRequirementListener` (pro `Activity` ) nebo `MAMIdentityRequirementListener` (pro `Service` nebo `ContentProviders` ).
K výchozímu chování `MAMActivity.onMAMIdentitySwitchRequired` se dostanete tak, že zavoláte statickou metodu `MAMActivity.defaultOnMAMIdentitySwitchRequired(activity, identity,
reason, callback)`.

A pokud potřebujete přepsat `MAMActivity.onSwitchMAMIdentityComplete`, můžete implementovat `MAMActivityIdentitySwitchListener` bez explicitního dědění z `MAMActivity`.

### <a name="preserving-identity-in-async-operations"></a>Zachování identity v asynchronních operacích
Operace vlákna uživatelského rozhraní běžně odesílají úlohy na pozadí do jiného vlákna. Aplikace s více identitami bude chtít zajistit, že tyto úlohy na pozadí probíhají pod správnou identitou. Často se jedná o stejnou identitu používanou aktivitou, která je odeslala. Z důvodu usnadnění a pomoci při zachování identity sada SDK MAM poskytuje `MAMAsyncTask` a `MAMIdentityExecutors`.
Ty je nutné použít, pokud asynchronní operace může zapisovat podniková data do souboru nebo může komunikovat s jinými aplikacemi.

#### <a name="mamasynctask"></a>MAMAsyncTask

Chcete-li použít `MAMAsyncTask` , jednoduše dědit z něj namísto `AsyncTask` a nahraďte `doInBackground` a `onPreExecute` v `doInBackgroundMAM` a v `onPreExecuteMAM` . Konstruktor `MAMAsyncTask` převezme kontext aktivity. Příklad:

```java
AsyncTask<Object, Object, Object> task = new MAMAsyncTask<Object, Object, Object>(thisActivity) {

    @Override
    protected Object doInBackgroundMAM(final Object[] params) {
        // Do operations.
    }

    @Override
    protected void onPreExecuteMAM() {
        // Do setup.
    };
}
```

### <a name="mamidentityexecutors"></a>MAMIdentityExecutors
`MAMIdentityExecutors` umožňuje zabalit existující instanci `Executor` nebo `ExecutorService` jako `Executor`/`ExecutorService` s metodami `wrapExecutor` a `wrapExecutorService`. Například

```java
Executor wrappedExecutor = MAMIdentityExecutors.wrapExecutor(originalExecutor, activity);
ExecutorService wrappedService = MAMIdentityExecutors.wrapExecutorService(originalExecutorService, activity);
```

### <a name="file-protection"></a>Ochrana souborů
Každý soubor má identitu, která je s ním spojená v době vytvoření, podle identity vláken a procesů. Tato identita se používá pro šifrování souborů i selektivní vymazání. Šifrovat se budou jen soubory, jejichž identita je spravovaná a má zásady vyžadující šifrování. Výchozí selektivní vymazání funkcí sadou SDK vymaže jen soubory spojené s identitou, u které se požaduje vymazání. Aplikace může zadat dotaz na identitu souboru nebo ji změnit pomocí třídy `MAMFileProtectionManager`.

```java
public final class MAMFileProtectionManager {

   /**
    * Protect a file or directory. This will synchronously trigger whatever protection is required for the file, and will tag the
    * file for future protection changes. If an identity is set on a directory, it is set recursively on all files and
    * subdirectories. New files or directories will inherit their parent directory's identity. If MAM is operating in offline mode,
    * this method will silently do nothing.
    *
    * @param identity
    *        Identity to set.
    * @param file
    *        File to protect.
    *
    * @throws IOException
    *         If the file cannot be protected.
    */
   public static void protect(final File file, final String identity) throws IOException;

   /**
     * Protect a file obtained from a content provider. This is intended to be used for
     * sdcard (whether internal or removable) files accessed through the Storage Access Framework.
     * It may also be used with descriptors referring to private files owned by this app.
     * It is not intended to be used for files owned by other apps and such usage will fail. If
     * creating a new file via a content provider exposed by another MAM-integrated app, the new
     * file identity will automatically be set correctly if the ContentResolver in use was
     * obtained via a Context with an identity or if the thread identity is set.
     *
     * This will synchronously trigger whatever protection is required for the file, and will tag
     * the file for future protection changes. If an identity is set on a directory, it is set
     * recursively on all files and subdirectories. If MAM is operating in offline mode, this
     * method will silently do nothing.
     *
     * @param identity
     *            Identity to set.
     * @param file
     *            File to protect.
     *
     * @throws IOException
     *             If the file cannot be protected.
     */
    public static void protect(final ParcelFileDescriptor file, final String identity) throws IOException;

   /**
    * Get the protection info on a file. This method should only be used if the file is located in the calling application's
    * private storage or the device's shared storage. If opening a file with a content resolver, use the overload which
    * takes a ParcelFileDescriptor instead.
    *
    * @param file
    *            File or directory to get information on.
    * @return File protection info, or null if there is no protection info.
    * @throws IOException
    *             If the file cannot be read or opened.
    */
    public static MAMFileProtectionInfo getProtectionInfo(final File file) throws IOException;

   /**
    * Get the protection info on a file descriptor such as one opened through a content resolver.
    *
    * @param file
    *            File or directory to get information on.
    * @return File protection info, or null if there is no protection info.
    * @throws IOException
    *             If the file cannot be read or opened.
    */
    public static MAMFileProtectionInfo getProtectionInfo(final ParcelFileDescriptor file) throws IOException;

}

public interface MAMFileProtectionInfo {
    String getIdentity();
}
 ```

#### <a name="app-responsibility"></a>Odpovědnost aplikace
Správa MAM nemůže automaticky odvodit vztah mezi čtenými soubory a daty zobrazovanými ve třídách `Activity`. Aplikace *musí* před zobrazením podnikových dat správně nastavit identitu uživatelského rozhraní. To platí i pro data čtená ze souborů. Pokud soubor pochází mimo aplikaci ( `ContentProvider` nebo je čten z veřejně zapisovatelného umístění), aplikace se *musí* `MAMFileProtectionManager.getProtectionInfo` před zobrazením informací přečtených ze souboru pokusit určit identitu souboru (pomocí správného přetížení pro zdroj dat). Pokud `getProtectionInfo` oznámí identitu, která nemá hodnotu null a není prázdná, *musí* se identita uživatelského rozhraní nastavit tak, aby odpovídala této identitě (pomocí `MAMActivity.switchMAMIdentity` nebo `MAMPolicyManager.setUIPolicyIdentity`). Pokud se přepnutí identity nezdaří, *nesmí* se data ze souboru zobrazit.

Příklad postupu by mohl vypadat takto:
  * Uživatel vybere dokument, který se otevře v aplikaci.
  * Během otevřeného toku aplikace potvrdí před čtením dat z disku identitu, která by se měla použít k zobrazení obsahu:

    ```java
    MAMFileProtectionInfo info = MAMFileProtectionManager.getProtectionInfo(docPath)
    if (info != null)
        MAMPolicyManager.setUIPolicyIdentity(activity, info.getIdentity(), callback, EnumSet.noneOf<IdentitySwitchOption.class>)
    ```

  * Aplikace počká, dokud se výsledek neohlásí zpětnému volání.
  * Pokud je oznámený výsledek chyba, aplikace dokument nezobrazí.
  * Aplikace otevře a vykreslí soubor.
  
Pokud aplikace stahuje soubory pomocí Androidu `DownloadManager` , sada mam SDK se pokusí tyto soubory automaticky chránit pomocí identity procesu. Pokud stažené soubory obsahují podniková data, je její zodpovědnost vůči volání aplikace, `protect` Pokud jsou soubory po stažení přesunuty nebo znovu vytvořeny.

#### <a name="single-identity-to-multi-identity-transition"></a>Přechod s jednou identitou na více identit
Pokud aplikace, která byla dříve vydaná s integrací Intune s jednou identitou, se později integruje s více identitami, budou mít dříve nainstalované aplikace nějaký přechod (není k dispozici žádné žádné přidružené prostředí). Aplikace není *nutná* k tomu, aby provedla žádné explicitní zpracování tohoto přechodu. Všechny soubory vytvořené před přechodem se budou nadále považovat za spravované (takže zůstanou zašifrované, pokud jsou zapnuté zásady šifrování). V případě potřeby můžete rozpoznat upgrade a použít `MAMFileProtectionManager.protect` ho k označení určitých souborů nebo adresářů s prázdnou identitou (což odebere šifrování, pokud byly zašifrované).

#### <a name="offline-scenarios"></a>Offline scénáře
Označení identity souboru je citlivé na režim offline. Je potřeba vzít v úvahu tyto body:

* Pokud není nainstalovaný portál společnosti, soubory nemůžou mít označenou identitu.

* Pokud je Portál společnosti nainstalovaný, ale aplikace nemá zásady MAM Intune, nedá se u souborů spolehlivě označit identita.

* Jakmile je označování identity souborů k dispozici, považují se všechny dříve vytvořené soubory za osobní/nespravované (patří do identity s prázdným řetězcem), pokud nebyla aplikace dříve nainstalovaná jako spravovaná aplikace s jedinou identitou. V takovém případě se má zato, že soubory patří zaregistrovanému uživateli.

### <a name="directory-protection"></a>Ochrana adresářů

Adresáře je možné chránit pomocí stejné metody `protect`, která se používá k ochraně souborů. Ochrana adresářů ale působí rekurzivně na všechny soubory a podadresáře, které jsou součástí daného adresáře, stejně jako nové soubory vytvořené v tomto umístění. Vzhledem k této vlastnosti může u velkých adresářů trvat volání `protect` delší dobu. Proto je u aplikací využívajících ochranu adresáře s velkým počtem souborů vhodné spustit metodu `protect` asynchronně na vlákně na pozadí.

### <a name="data-protection"></a>Ochrana dat

Soubor se nedá označit jako soubor, který má více identit. Aplikace, které musí ukládat data různých uživatelů ve stejném souboru, to můžou provádět ručně díky funkcím, které poskytuje `MAMDataProtectionManager`. Aplikace tak můžou šifrovat data a spojit je s určitým uživatelem. Šifrovaná data se hodí k ukládání na disk v souboru. Na data, která souvisejí s identitou, můžete zadávat dotazy a později je dešifrovat.

Aplikace využívající `MAMDataProtectionManager` by měly pro oznámení `MANAGEMENT_REMOVED` implementovat příjemce. Po dokončení tohoto oznámení už nebudou vyrovnávací paměti chráněné touto třídou čitelné, pokud bylo v době poskytování ochrany povoleno šifrování souborů. Aplikace může tuto situaci napravit voláním `MAMDataProtectionManager.unprotect` všech vyrovnávacích pamětí během tohoto oznámení. Pokud chcete zachovat informace o identitě, je v této době také bezpečné volat metodu protect, protože při probíhajícím oznámení se zaručuje, že šifrování bude zakázané.


```java

public final class MAMDataProtectionManager {
    /**
     * Protect a stream. This will return a stream containing the protected
     * input.
     *
     * @param identity
     *            Identity to set.
     * @param input
     *            Input data to protect, read sequentially. This function
     *            will change the position of the stream but may not have
     *            read the entire stream by the time it returns. The
     *            returned stream will wrap this one. Calls to read on the
     *            returned stream may cause further reads on the original
     *            input stream. Callers should not expect to read directly
     *            from the input stream after passing it to this method.
     *            Calling close on the returned stream will close this one.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be protected
     */
    public static InputStream protect(final InputStream input, final String identity);

    /**
     * Protect a byte array. This will return protected bytes.
     *
     * @param identity
     *            Identity to set.
     * @param input
     *            Input data to protect.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be protected
     */
    public static byte[] protect(final byte[] input, final String identity) throws IOException;

    /**
     * Unprotect a stream. This will return a stream containing the
     * unprotected input.
     *
     * @param input
     *            Input data to protect, read sequentially.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be unprotected
     */
    public static InputStream unprotect(final InputStream input) throws IOException;

    /**
     * Unprotect a byte array. This will return unprotected bytes.
     *
     * @param input
     *            Input data to protect.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be unprotected
     */
    public static byte[] unprotect(final byte[] input) throws IOException;

    /**
     * Get the protection info on a stream.
     *
     * @param input
     *            Input stream to get information on. Either this input
     *            stream must have been returned by a previous call to
     *            protect OR input.markSupported() must return true.
     *            Otherwise it will be impossible to get protection info
     *            without advancing the stream position. The stream must be
     *            positioned at the beginning of the protected data.
     * @return Data protection info, or null if there is no protection
     *            info.
     * @throws IOException
     *             If the input cannot be read.
     */
    public static MAMDataProtectionInfo getProtectionInfo(final InputStream input) throws IOException;

    /**
     * Get the protection info on a stream.
     *
     * @param input
     *            Input bytes to get information on. These must be bytes
     *            returned by a previous call to protect() or a copy of
     *            such bytes.
     * @return Data protection info, or null if there is no protection
     *            info.
     * @throws IOException
     *             If the input cannot be read.
     */
    public static MAMDataProtectionInfo getProtectionInfo(final byte[] input) throws IOException;
}
```


### <a name="content-providers"></a>Poskytovatelé obsahu

Pokud aplikace poskytuje podniková data kromě přes a `ParcelFileDescriptor` `ContentProvider` , musí aplikace zavolat metodu `isProvideContentAllowed(String)` v, která předá `MAMContentProvider` hlavní název uživatele (UPN) identity vlastníka. Pokud tato funkce vrací hodnotu False, *nesmí* se obsah vrátit zpět volajícímu. Popisovače souborů, které se vrátí přes poskytovatele obsahu, se automaticky zpracují podle identity souboru.

Pokud explicitně nedědíte `MAMContentProvider` a místo toho umožníte nástrojům sestavení provést tuto změnu, můžete zavolat statickou verzi stejné metody: `MAMContentProvider.isProvideContentAllowed(provider,
contentIdentity)` .

### <a name="selective-wipe"></a>Selektivní vymazání

Pokud aplikace s více identitami zaregistruje oznámení `WIPE_USER_DATA`, je odpovědná za odebrání všech dat vymazávaného uživatele, a to včetně všech souborů, jejichž identita označuje, že patří danému uživateli. Pokud aplikace odebere data uživatele ze souboru, ale chce v souboru ponechat ostatní data, *musí* změnit identitu souboru (přes `MAMFileProtectionManager.protect` na osobní identitu uživatele nebo na prázdnou identitu). Pokud se používají zásady šifrování, všechny zbývající soubory, které patří vymazávanému uživateli, zůstanou zašifrované a po vymazání budou pro aplikaci nedostupné.

Aplikace, která zaregistruje `WIPE_USER_DATA`, nezíská výhodu sady SDK výchozího chování sady SDK při selektivním vymazání. U aplikací, které pracují s více identitami, to může být mnohem závažnější, protože výchozí selektivní vymazání MAM vymaže jen soubory, na jejichž identitu vymazání cílí. Pokud si aplikace pracující s více identitami přeje, aby výchozí selektivní vymazání MAM proběhlo, _**a**_ chce při vymazání provádět vlastní akce, měla by si zaregistrovat oznámení `WIPE_USER_AUXILIARY_DATA`. Toto oznámení odešle sada SDK těsně před tím, než provedete výchozí selektivní vymazání MAM. Aplikace by nikdy neměla zaregistrovat pro i `WIPE_USER_DATA` `WIPE_USER_AUXILIARY_DATA` .

Výchozí selektivní vymazání ukončí aplikaci řádným způsobem, dokončuje aktivity a ukončuje proces aplikace. Pokud vaše aplikace přepisuje výchozí selektivní vymazání, možná budete chtít, abyste aplikaci zavřeli ručně, abyste zabránili uživateli v přístupu k datům v paměti, když dojde k vymazání.


## <a name="enabling-mam-targeted-configuration-for-your-android-applications-optional"></a>Povolení konfigurace určené pro správu mobilních aplikací pro Android (nepovinné)
Páry klíč-hodnota specifické pro aplikaci můžou být nakonfigurované v konzole Intune pro [mam](https://docs.microsoft.com/intune/app-configuration-policies-managed-app) a [Android Enterprise](https://docs.microsoft.com/intune/app-configuration-policies-use-android).
Tyto páry klíč-hodnota se v Intune vůbec neinterpretují, ale předávají se do aplikace. Aplikace, které chtějí obdržet takovou konfiguraci, k tomu můžou použít třídy `MAMAppConfigManager` a `MAMAppConfig`. Pokud je stejná aplikace cílem více zásad, může být pro stejný klíč k dispozici více konfliktních hodnot.

> [!NOTE] 
> Nastavení konfigurace pro doručení prostřednictvím MAM – nemůžeme doručovat služby `offline` (když portál společnosti není nainstalovaná).  `MAMUserNotification`V tomto případě se v takovém případě doručí v prázdné identitě jenom Android Enterprise AppRestrictions.

### <a name="get-the-app-config-for-a-user"></a>Získání konfigurace aplikace pro uživatele
Konfigurace aplikace může být načtena takto:
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
```

Pokud není k dispozici žádný MAM uživatel, ale vaše aplikace by stále chtěla načíst konfiguraci Androidu Enterprise (která nebude cílená na konkrétního uživatele), můžete předat hodnotu null nebo prázdný řetězec.

### <a name="conflicts"></a>Konflikty
Hodnota nastavená v konfiguraci aplikace MAM přepíše hodnotu se stejnou klíčovou sadou v konfiguraci Android Enterprise config. 

Pokud správce nakonfiguruje konfliktní hodnoty pro stejný klíč (například tím, že cílí na různé sady konfigurací aplikací se stejným klíčem na více skupin, které obsahují stejného uživatele), Intune nezpůsobí automatický překlad tohoto konfliktu a zpřístupní pro vaši aplikaci všechny dostupné hodnoty. 

Vaše aplikace může požádat o všechny hodnoty daného klíče z `MAMAppConfig` objektu:
```java
List<Boolean> getAllBooleansForKey(String key)
List<Long> getAllIntegersForKey(final String key)
List<Double> getAllDoublesForKey(final String key)
List<String> getAllStringsForKey(final String key)
```

nebo si vyžádejte hodnotu, kterou chcete vybrat:
```java
Boolean getBooleanForKey(String key, BooleanQueryType queryType)
Long getIntegerForKey(String key, NumberQueryType queryType)
Double getDoubleForKey(String key, NumberQueryType queryType)
String getStringForKey(String key, StringQueryType queryType)

enum BooleanQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns true if any of the values are true.
     */
    Or,
    /**
     * In case of conflict, returns false if any of the values are false.
     */
    And
}

enum NumberQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns the minimum Integer.
     */
    Min,
    /**
     * In case of conflict, returns the maximum Integer.
     */
    Max
}

enum StringQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns the first result ordered alphabetically.
     */
    Min,

    /**
     * In case of conflict, returns the last result ordered alphabetically.
     */
    Max
}
```

Aplikace může také vyžádat nezpracovaná data jako seznam sad párů klíč-hodnota.

```java
List<Map<String, String>> getFullData()
```


### <a name="full-example"></a>Úplný příklad
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
String fooValue = null;
if (appConfig.hasConflict("foo")) {
    List<String> values = appConfig.getAllStringsForKey("foo");
    fooValue = chooseBestValue(values);
} else {
    valueToUse = appConfig.getStringForKey("foo", MAMAppConfig.StringQueryType.Any);
}
Long barValue = appConfig.getIntegerForKey("bar", MAMAppConfig.NumberQueryType.Min);
```

### <a name="notification"></a>Notification (Oznámení)
Konfigurace aplikace přidá nový typ oznámení:
* **REFRESH_APP_CONFIG**: Toto oznámení se odesílá v rámci `MAMUserNotification` a do aplikace posílá informace, že jsou k dispozici nová konfigurační data aplikace.

### <a name="further-reading"></a>Další čtení
Další informace o vytváření zásad konfigurace aplikací určených pro MAM v Androidu najdete v části o konfiguraci aplikací určených pro MAM v článku [Použití zásad konfigurace aplikací v Microsoft Intune pro Android](https://docs.microsoft.com/intune/app-configuration-policies-managed-app).

Konfiguraci aplikace je také možné nakonfigurovat pomocí Graph API. Informace najdete v tématu [Graph API docs pro cílenou konfiguraci mam](https://docs.microsoft.com/graph/api/resources/intune-mam-targetedmanagedappconfiguration).

## <a name="custom-themes-optional"></a>Vlastní motivy (volitelné)
Vlastní motiv se dá poskytnout sadě SDK MAM, která se použije pro všechny obrazovky a dialogy MAM. Pokud není zadán motiv, bude použit výchozí motiv MAM.

### <a name="how-to-provide-a-theme"></a>Jak poskytnout motiv
Chcete-li poskytnout motiv, je nutné do metody přidat následující řádek kódu `Application.onCreate` :

```java
MAMThemeManager.setAppTheme(R.style.AppTheme);
```

V předchozím příkladu je třeba nahradit `R.style.AppTheme` motiv styl, který má sada SDK používat.

## <a name="style-customization-deprecated"></a>Přizpůsobení stylu (zastaralé)

Toto je nyní zastaralé a vlastní motivy (výše) jsou preferovaným způsobem přizpůsobení zobrazení.

Vzhled zobrazení vygenerovaných sadou MAM SDK můžete upravit tak, aby lépe odpovídaly aplikaci, do které se budou integrovat. Přizpůsobit můžete primární a sekundární barvu, barvy pozadí i velikost loga aplikace. Přizpůsobení je volitelné, a pokud nenastavíte vlastní styl, použije se výchozí vzhled.


### <a name="how-to-customize"></a>Postup přizpůsobení
Aby se změny stylu použily u zobrazení sady Intune MAM, je potřeba nejprve vytvořit soubor XML s přepsáním stylu. Tento soubor by se měl nacházet v adresáři „/res/xml“ vaší aplikace a může mít jakýkoli název. Níže je uveden příklad formátování, které by měl soubor dodržovat.

```xml
<?xml version="1.0" encoding="utf-8"?>
<styleOverrides>
    <item
        name="foreground_color"
        resource="@color/red"/>
    <item
        name="accent_color"
        resource="@color/blue"/>
    <item
        name="background_color"
        resource="@color/green"/>
    <item
        name="logo_image"
        resource="@drawable/app_logo"/>
</styleOverrides>
```

Je nutné znovu použít prostředky, které už ve vaší aplikaci jsou. To například znamená, že definujete zelenou barvu v souboru colors.xml a v tomto kódu na ni odkážete. Kód barvy v šestnáctkovém formátu „#0000ff“ nejde použít. Maximální velikost loga aplikace je 110 dip (dp). Použít můžete i logo menší velikosti, ale s maximální velikostí dosáhnete nejlepšího vzhledu. Pokud překročíte limit 110 dip, obrázek se zmenší a může se rozmazat.

Níže najdete kompletní seznam povolených atributů stylu, prvků uživatelského rozhraní, které tyto atributy řídí, názvy položek příslušných atributů XML a očekávané typy prostředků.

|Atribut stylu | Ovlivněné prvky uživatelského rozhraní | Název položky atributu | Očekávaný typ prostředku |
| -- | -- | -- | -- |
| Barva pozadí | Barva pozadí obrazovky pro zadání PIN kódu <Br>Barva výplně pole pro zadání PIN kódu | background_color | Color |
| Barva popředí | Barva textu na popředí <br> Ohraničení pole pro zadání PIN kódu ve výchozím stavu <br> Znaky (včetně obfuskovaných znaků) v poli po zadání PIN kódu uživatelem| foreground_color | Color|
| Doplňková barva | Ohraničení pole pro zadání PIN kódu při zvýraznění <br> Hypertextové odkazy |accent_color | Color |
| Logo aplikace | Velká ikona, která se zobrazuje na obrazovce pro zadání PIN kódu aplikace Intune | logo_image | Nákres |

## <a name="default-enrollment-optional"></a>Výchozí registrace (volitelná)

Následující část obsahuje postup pro vyžadování výzvy uživateli při spuštění aplikace pro registraci služby APP-WE (v této části to označujeme jako **výchozí registraci**) a vyžadování zásad ochrany aplikací Intune, aby obchodní aplikaci pro Android, která je integrovaná se sadou SDK, mohli používat jenom uživatelé s ochranou Intune. Obsahuje také postup pro povolení jednotného přihlašování pro obchodní aplikaci pro Android, která je integrovaná se sadou SDK. Tento postup se **nepodporuje** u aplikací pro Store, které můžou používat uživatelé nevyužívající službu Intune.

> [!NOTE] 
> Mezi výhody **výchozí registrace** patří zjednodušený způsob získání zásad ze služby APP-WE pro aplikaci na daném zařízení.

> [!NOTE] 
> **Výchozím zápisem** je vědomá podpora cloudu.

Pomocí následujících kroků povolte výchozí registraci:

1. Pokud vaše aplikace integruje ADAL nebo potřebujete povolit jednotné přihlašování, [nakonfigurujte knihovnu ADAL](#configure-azure-active-directory-authentication-library-adal) po [běžné konfiguraci #2 konfigurace ADAL](#common-adal-configurations) . V takovém případě tento krok můžete přeskočit.

  > [!NOTE]
  > Azure Active Directory (Azure AD) Authentication Library (ADAL) a Azure AD Graph API budou zastaralé. Další informace najdete v tématu [aktualizace aplikací pro použití knihovny Microsoft Authentication Library (MSAL) a rozhraní Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).
   
2. Povolte výchozí registraci přidáním následující hodnoty do manifestu pod `<application>` značku:

   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.DefaultMAMServiceEnrollment" android:value="true" />
   ```

   > [!NOTE] 
   > Musí jít o jedinou integraci MAM-WE v dané aplikaci. Pokud existují další pokusy o volání rozhraní API instance MAMEnrollmentManager, dojde ke konfliktům.

3. Povolte zásady MAM vyžadované přidáním následující hodnoty v manifestu pod `<application>` značku:

   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.MAMPolicyRequired" android:value="true" />
   ```

   > [!NOTE] 
   > Tím vynutíte, aby si uživatel na zařízení stáhl Portál společnosti a před použitím provedl postup výchozí registrace.


## <a name="limitations"></a>Omezení

### <a name="policy-enforcement-limitations"></a>Omezení vynucení zásad

* **Použití překladačů obsahu**: Zásady Intune o přenosu nebo příjmu můžou blokovat nebo částečně blokovat překladače obsahu použité při přístupu k poskytovateli obsahu v jiné aplikaci. To způsobí, že `ContentResolver` metody vrátí hodnotu null nebo vyvolají chybovou hodnotu (například `openOutputStream` vyvolá výjimku, `FileNotFoundException` Pokud se zablokuje). Aplikace může určit, jestli selhání při zápisu dat pomocí překladače obsahu způsobila zásada (nebo by způsobila zásada), a to voláním:

    ```java
    MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(contentURI);
    ```

    nebo pokud není k dispozici žádná přidružená aktivita:

    ```java
    MAMPolicyManager.getPolicy().getIsSaveToLocationAllowed(contentURI);
    ```

    Ve druhém případě musí aplikace s více identitami pečlivě správně nastavit identitu vlákna (nebo předat explicitní identitu do volání `getPolicy`).

### <a name="exported-services"></a>Exportované služby
Soubor AndroidManifest.xml zahrnutý v sadě Intune App SDK obsahuje službu **MAMNotificationReceiverService**, která musí být exportovanou službou, aby umožňovala Portálu společnosti odesílat oznámení do spravované aplikace. Služba zkontroluje volajícího, aby zajistila, že odesílat oznámení může jenom portál společnosti.

### <a name="reflection-limitations"></a>Omezení reflexe
Některé základní třídy MAM (například `MAMActivity` , `MAMDocumentsProvider` ) obsahují metody (založené na původních základních třídách Android), které používají parametry nebo návratové typy, které jsou přítomny jenom nad určitými ÚROVNĚMI rozhraní API. Z tohoto důvodu nemusí být vždycky možné používat reflexi k výčtu všech metod součástí aplikací. Toto omezení se nevztahuje jenom na MAM. Jedná se o stejné omezení, které by se použilo v případě, že by aplikace samotná implementovala tyto metody ze základních tříd Androidu.

### <a name="robolectric"></a>Robolectric
Testování chování sady SDK MAM v rozhraní Robolectric se nepodporuje. V MAM se vyskytly známé problémy, které jsou v Robolectric v důsledku chování přítomného v Robolectric, které je přesně Nenapodobují na skutečných zařízeních nebo emulátorech.

Pokud potřebujete testovat aplikaci v rámci Robolectric, doporučuje se přesunout logiku třídy aplikace do pomocné rutiny a vytvořit APK testování částí pomocí třídy aplikace, která nedědí od MAMApplication.

## <a name="expectations-of-the-sdk-consumer"></a>Očekávání uživatele sady SDK

Intune SDK udržuje kontrakt poskytovaný rozhraním Android API, i když podmínky selhání můžou být vyvolány častěji v důsledku vynucení zásad. Tyto doporučené postupy pro Android sníží pravděpodobnost selhání:

* Funkce sady Android SDK, které můžou vrátit hodnotu null, mají vyšší pravděpodobnost vrácení hodnoty null.  Chcete-li minimalizovat problémy, zajistěte, aby byly na správných místech kontroly hodnoty null.

* Vlastnosti, které jde zkontrolovat, musí být kontrolované pomocí příslušných rozhraní API náhradních sad MAM.

* Všechny odvozené funkce se musí provolat ke svým verzím v nadřazené třídě.

* Vyhněte se použití jakéhokoli rozhraní API nejednoznačný způsobem. Například použití `Activity.startActivityForResult` bez kontroly requestCode způsobí neobvyklé chování.

### <a name="services"></a>Služby
Vynucování zásad může ovlivnit interakce služby.
Metody, které vytváří připojení vázané služby, jako je například `Context.bindService` selhání, mohou být způsobeny vyvynucováním zásad v `Service.onBind` a mohou mít za následek `ServiceConnection.onNullBinding` nebo `ServiceConnection.onServiceDisconnected` .
Interakce se zavedenou vázanou službou může vyvolat výjimku `SecurityException` z důvodu vynucení zásad v nástroji `Binder.onTransact` .

## <a name="telemetry"></a>Telemetrie

Sada Intune App SDK pro Android neřídí shromažďování dat z vaší aplikace. Aplikace Portál společnosti ve výchozím nastavení protokoluje data generovaná systémem. Tato data se odešlou do Microsoft Intune. V rámci zásad Microsoftu neshromažďujeme žádné osobní údaje.

> [!NOTE]
> Pokud se koncoví uživatelé rozhodnou tato data neodesílat, musí v nastavení aplikace Portál společnosti vypnout telemetrii. Další informace najdete v článku [Vypnutí shromažďování dat Microsoftu o využití](https://docs.microsoft.com/mem/intune/user-help/turn-off-microsoft-usage-data-collection-android). 

## <a name="recommended-android-best-practices"></a>Doporučené osvědčené postupy pro Android

* Všechny projekty knihovny by měly sdílet stejný balíček android:package, kde je to možné. Protože je to čistě problém v době vytváření buildu, nedojde k selhání za běhu. Novější verze sady Intune App SDK odeberou některé z redundancí.

* Použijte nejnovější nástroje pro vytváření buildů sady SDK pro Android.

* Odeberte všechny nepotřebné a nepoužívané knihovny (například android.support.v4).

## <a name="testing"></a>Testování
Projděte si [Průvodce testováním](app-sdk-android-testing-guide.md).
