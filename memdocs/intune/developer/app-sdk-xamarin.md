---
title: Xamarinové vazby sady Microsoft Intune App SDK
description: Xamarinové vazby sady Intune App SDK umožňují v aplikacích pro iOS a Android vytvořených v Xamarinu povolit zásady ochrany aplikací Intune.
keywords: SDK, Xamarin, Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 275d574b-3560-4992-877c-c6aa480717f4
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: 82ee499689a7c7ae85fb72cc4fc9b5f6d5ffc939
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908866"
---
# <a name="microsoft-intune-app-sdk-xamarin-bindings"></a>Xamarinové vazby sady Microsoft Intune App SDK

> [!NOTE]
> Možná si budete chtít nejdřív přečíst článek [Začínáme s Intune App SDK](app-sdk-get-started.md), který vysvětluje postup přípravy integrace na jednotlivých podporovaných platformách.

## <a name="overview"></a>Přehled
[Xamarinové vazby sady Intune App SDK](https://github.com/msintuneappsdk/intune-app-sdk-xamarin) umožňují v aplikacích pro iOS a Android vytvořených v Xamarinu povolit [zásady ochrany aplikací Intune](../apps/app-protection-policy.md). Tyto vazby umožňují vývojářům jednoduše do aplikací založených na Xamarinu začlenit funkce ochrany aplikace Intune.

Xamarinové vazby sady Microsoft Intune App SDK umožňují začlenit do vašich aplikací vyvíjených v Xamarinu zásady ochrany aplikací Intune (také označované jako zásady APP nebo MAM). Aplikace s povolenou funkcí MAM je integrovaná se sadou Intune App SDK. Správci IT můžou zásady ochrany aplikací nasadit do vaší mobilní aplikace, když Intune tuto aplikaci aktivně spravuje.

## <a name="whats-supported"></a>Co je podporováno?

### <a name="developer-machines"></a>Počítače pro vývojáře
* Windows (Visual Studio verze 15.7+)
* macOS

### <a name="mobile-app-platforms"></a>Platformy pro mobilní aplikace
* Android
* iOS

### <a name="intune-mobile-application-management-scenarios"></a>Scénáře Správy mobilních aplikací Intune

* Intune APP-WE (bez registrace zařízení)
* Zařízení zaregistrovaná v Intune MDM
* Zařízení zaregistrovaná v EMM třetích stran

Xamarinové aplikace vytvořené xamarinovými vazbami sady Intune App SDK přijímají zásady ochrany aplikací Intune na zařízeních zaregistrovaných ve správě mobilních zařízení (MDM) Intune i na neregistrovaných zařízeních.

## <a name="prerequisites"></a>Předpoklady

Přečtěte si [licenční smlouvy](https://github.com/msintuneappsdk/intune-app-sdk-xamarin/blob/master/Microsoft%20License%20Terms%20Intune%20App%20SDK%20Xamarin%20Component.pdf). Licenční podmínky si vytiskněte a uchovejte pro své záznamy. Stažením a použitím xamarinových vazeb sady Intune App SDK přijímáte tyto licenční podmínky. Pokud je nepřijímáte, software nepoužívejte.

Sada Intune SDK se spoléhá na [knihovnu Microsoft Authentication Library (MSAL)](/azure/active-directory/develop/v2-overview) pro své scénáře [ověřování](/azure/active-directory/develop/authentication-vs-authorization) a podmíněného spuštění, které vyžadují konfiguraci aplikací pomocí [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis). 

Pokud je vaše aplikace už nakonfigurovaná tak, aby používala MSAL, a má své vlastní ID klienta, které se používá k ověřování pomocí Azure Active Directory, zajistěte, aby se použila vaše oprávnění aplikace Xamarin pro správu mobilních aplikací (MAM) služby Intune. Postupujte podle pokynů v části "[poskytnutí přístupu aplikace ke službě Intune App Protection](app-sdk-get-started.md#give-your-app-access-to-the-intune-app-protection-service-optional)" v tématu [Začínáme s Intune SDK](app-sdk-get-started.md).

## <a name="security-considerations"></a>Aspekty zabezpečení

Pro zabránění potenciálnímu falšování identity, zpřístupnění informací a zvýšení oprávnění pro útoky zajistěte toto:

* Ujistěte se, že vývoj aplikací Xamarin se provádí na zabezpečené pracovní stanici.
* Zajistěte, aby vazby byly z platného zdroje společnosti Microsoft:
  * [Profil NuGet sady Microsoft Intune App SDK](https://www.nuget.org/profiles/msintuneappsdk)
  * [Úložiště GitHub sady Intune App SDK Xamarin](https://github.com/msintuneappsdk/intune-app-sdk-xamarin)
* Nakonfigurujte konfiguraci NuGet pro váš projekt tak, aby důvěřovala podepsaným, nezměněným balíčkům NuGet.
Další informace najdete v tématu [instalace podepsaných balíčků](/nuget/consume-packages/installing-signed-packages) .
* Zabezpečte výstupní adresář, který obsahuje aplikaci Xamarin. Zvažte použití adresáře na úrovni uživatele pro výstup.


## <a name="enabling-intune-app-protection-polices-in-your-ios-mobile-app"></a>Povolení zásad ochrany aplikací Intune v mobilní aplikaci pro iOS
1. Do svého projektu Xamarin.iOS přidejte [balíček NuGet Microsoft.Intune.MAM.Xamarin.iOS](https://www.nuget.org/packages/Microsoft.Intune.MAM.Xamarin.iOS).
2. Při integraci sady Intune App SDK do mobilní aplikace pro iOS dodržujte obecné pokyny. Začněte od 3. kroku popsaného v [příručce pro vývojáře k sadě Intune App SDK pro iOS](app-sdk-ios.md#build-the-sdk-into-your-mobile-app). Poslední krok v této části spuštění nástroje IntuneMAMConfigurator můžete přeskočit, protože tento nástroj je součástí balíčku Microsoft.Intune.MAM.Xamarin.iOS a spustí se automaticky při sestavení.
    **Důležité:** Povolení sdílení klíčenky aplikace je v sadě Visual Studio trochu jiné než v Xcode. Otevřete soubor Entitlements.plist aplikace a zkontrolujte, že je povolená možnost „Enable Keychain“ (Povolit klíčenku) a že jsou do oddílu přidané odpovídající skupiny pro sdílení klíčenky. Zkontrolujte, že je v poli „Custom Entitlements“ (Vlastní oprávnění) v možnostech podepsání sady prostředků aplikace pro iOS zadaný soubor Entitlements.plist, a to pro všechny kombinace konfigurace a platformy, které připadají v úvahu.
3. Jakmile přidáte vazby a aplikaci správně nakonfigurujete, může aplikace začít používat rozhraní API sady Intune SDK. Aby to bylo možné, musíte přidat následující obor názvů:

      ```csharp
      using Microsoft.Intune.MAM;
      ```

4. Aby aplikace mohly začít přijímat zásady ochrany, musíte je zaregistrovat do služby Intune MAM. Pokud vaše aplikace nepoužívá k ověřování uživatelů [knihovnu Microsoft Authentication Library](https://www.nuget.org/packages/Microsoft.Identity.Client) (MSAL) a vy chcete, aby sada Intune SDK zpracovávala ověřování, měla by vaše aplikace poskytnout hlavní název uživatele (UPN) k LoginAndEnrollAccount metodě IntuneMAMEnrollmentManager:

      ```csharp
       IntuneMAMEnrollmentManager.Instance.LoginAndEnrollAccount([NullAllowed] string identity);
      ```

      Aplikace mohou předat hodnotu null, pokud hlavní název uživatele není v době volání známý. V takovém případě budou uživatelé vyzváni k zadání e-mailové adresy a hesla.
      
      Pokud už vaše aplikace používá MSAL k ověřování uživatelů, můžete nakonfigurovat jednotné přihlašování (SSO) mezi vaší aplikací a sadou Intune SDK. Nejdřív budete muset přepsat výchozí nastavení AAD používané sadou Intune SDK pomocí těch, které vaše aplikace používá. To můžete provést prostřednictvím slovníku IntuneMAMSettings v souboru info. plist aplikace, jak je uvedeno v [sadě Intune App SDK pro iOS](app-sdk-ios.md#configure-settings-for-the-intune-app-sdk), nebo to můžete provést v kódu prostřednictvím vlastností přepisu AAD třídy IntuneMAMSettings. Přístup k informacím. plist se doporučuje u aplikací, jejichž nastavení MSAL je statické, zatímco vlastnosti přepsání jsou doporučené pro aplikace, které tyto hodnoty určují za běhu. Po konfiguraci všech nastavení jednotného přihlašování by vaše aplikace měla metodě RegisterAndEnrollAccount třídy IntuneMAMEnrollmentManager po úspěšném ověření poskytnout hlavní název uživatele (UPN):

      ```csharp
      IntuneMAMEnrollmentManager.Instance.RegisterAndEnrollAccount(string identity);
      ```

      Aplikace mohou určit výsledek pokusu o registraci implementací metody EnrollmentRequestWithStatus v podtřídě IntuneMAMEnrollmentDelegate a nastavením vlastnosti Delegate třídy IntuneMAMEnrollmentManager na instanci této třídy. 

      Po úspěšné registraci mohou aplikace určit hlavní název uživatele zaregistrovaného účtu (pokud předtím nebyl známý) dotazem na následující vlastnost: 

      ```csharp
       string enrolledAccount = IntuneMAMEnrollmentManager.Instance.EnrolledAccount;
      ```      
### <a name="sample-applications"></a>Ukázkové aplikace
Ukázkové aplikace zvýrazňování MAM funkcí v aplikacích Xamarin. iOS jsou k dispozici na [GitHubu](https://github.com/msintuneappsdk/sample-intune-xamarin-ios).

> [!NOTE] 
> Pro iOS/iPadOS neexistuje žádné přemapování. Integrace do aplikace Xamarin.Forms by měla být stejná jako u normálního projektu Xamarin.iOS. 

## <a name="enabling-intune-app-protection-policies-in-your-android-mobile-app"></a>Povolení zásad Intune App Protection v mobilní aplikaci pro Android
1. Do svého projektu Xamarin.Android přidejte [balíček NuGet Microsoft.Intune.MAM.Xamarin.Android](https://www.nuget.org/packages/Microsoft.Intune.MAM.Xamarin.Android).
    1. V případě aplikace Xamarin. Forms přidejte do projektu Xamarin. Android také [balíček NuGet Microsoft. Intune. mam. remapper. Tasks. Tasks](https://www.nuget.org/packages/Microsoft.Intune.MAM.Remapper.Tasks) . 
2. Postupujte podle obecných kroků nezbytných pro [integraci sady Intune App SDK](app-sdk-android.md) do mobilní aplikace pro Android a při odkazování na tento dokument, kde najdete další podrobnosti.

### <a name="xamarinandroid-integration"></a>Integrace Xamarin.Android

Úplný přehled integrace sady Intune App SDK najdete v [příručce pro vývojáře sady Microsoft Intune App SDK pro Android](app-sdk-android.md). Jak si přečtete příručku a integrujte sadu Intune App SDK s vaší aplikací Xamarin. následující oddíly jsou určené k zdůraznění rozdílů mezi implementací nativní aplikace pro Android vyvinuté v jazyce Java a aplikací Xamarin vyvinutou v jazyce C#. Tyto části by se měly považovat za doplňkové a nemůžou fungovat jako náhrada za celý průvodce.

#### <a name="remapper"></a>Remapper
Od verze 1.4428.1 se `Microsoft.Intune.MAM.Remapper` balíček dá přidat do aplikace Xamarin. Android jako [Nástroje pro vytváření](app-sdk-android.md#build-tooling) , aby se prováděly přemístění třídy, metody a služeb systému mam. Pokud je přemapování zahrnuto, MAM ekvivalentní části přejmenovaných metod a oddílů aplikace MAM budou automaticky provedeny při sestavení aplikace.

Chcete-li vyloučit třídu z MAM sjednocení přemapováním, lze do souboru projektu přidat následující vlastnost `.csproj` .

```xml
  <PropertyGroup>
    <ExcludeClasses>Semicolon separated list of relative class paths to exclude from MAM-ification</ExcludeClasses>
  </PropertyGroup>
```

> [!NOTE]
> Remapovače aktuálně brání ladění v aplikacích Xamarin. Android. Pro ladění aplikace se doporučuje ruční integrace.

#### <a name="renamed-methods"></a>[Přejmenované metody](app-sdk-android.md#renamed-methods)
V mnoha případech je metoda dostupná ve třídě Androidu označená v náhradní třídě MAM jako finální. Náhradní třída MAM pak poskytuje metodu s podobným názvem (s příponou `MAM`), kterou byste měli přepsat místo toho. Třeba při odvozování od třídy `MAMActivity` musí `Activity` místo přepsání `OnCreate()` a volání `base.OnCreate()` přepsat `OnMAMCreate()` a volat `base.OnMAMCreate()`.

#### <a name="mam-application"></a>[Aplikace MAM](app-sdk-android.md#mamapplication)
Vaše aplikace musí definovat `Android.App.Application` třídu. Pokud manuálně integruje MAM, musí dědit z `MAMApplication` . Zkontrolujte, že podtřída je správně doplněna o atribut `[Application]` a že přepisuje konstruktor `(IntPtr, JniHandleOwnership)`.

```csharp
    [Application]
    class TaskrApp : MAMApplication
    {
    public TaskrApp(IntPtr handle, JniHandleOwnership transfer)
        : base(handle, transfer) { }
```

> [!NOTE]
> Problém s MAMmi vazbami Xamarin může způsobit chybu aplikace při nasazení v režimu ladění. Alternativním řešením je, že `Debuggable=false` atribut musí být přidán do `Application` třídy a `android:debuggable="true"` příznak musí být odebrán z manifestu, pokud byl ručně nastaven.

#### <a name="enable-features-that-require-app-participation"></a>[Povolení funkcí, které vyžadují účast aplikace](app-sdk-android.md#enable-features-that-require-app-participation)
Příklad: Určení, jestli aplikace vyžaduje PIN

```csharp
MAMPolicyManager.GetPolicy(currentActivity).IsPinRequired;
```

Příklad: Určení primárního uživatele Intune

```csharp
IMAMUserInfo info = MAMComponents.Get<IMAMUserInfo>();
return info?.PrimaryUser;
```

Příklad: Určení, jestli je povoleno ukládání na zařízení nebo do cloudového úložiště

```csharp
MAMPolicyManager.GetPolicy(currentActivity).GetIsSaveToLocationAllowed(SaveLocation service, String username);
```

#### <a name="register-for-notifications-from-the-sdk"></a>[Registrace k oznámením z SDK](app-sdk-android.md#register-for-notifications-from-the-sdk)
Vaše aplikace se musí zaregistrovat pro oznámení ze sady SDK vytvořením `MAMNotificationReceiver` a registrací v `MAMNotificationReceiverRegistry` . To se provádí tím, že poskytne přijímač a typ oznámení požadované v `App.OnMAMCreate` , jak ukazuje následující příklad:

```csharp
public override void OnMAMCreate()
{
    // Register the notification receivers
    IMAMNotificationReceiverRegistry registry = MAMComponents.Get<IMAMNotificationReceiverRegistry>();
    foreach (MAMNotificationType notification in MAMNotificationType.Values())
    {
        registry.RegisterReceiver(new ToastNotificationReceiver(this), notification);
    }
    ...
```

#### <a name="mam-enrollment-manager"></a>[Správce registrace MAM](app-sdk-android.md#mamenrollmentmanager)

```csharp
IMAMEnrollmentManager mgr = MAMComponents.Get<IMAMEnrollmentManager>();
```

### <a name="xamarinforms-integration"></a>Integrace Xamarin.Forms

Pro `Xamarin.Forms` aplikace `Microsoft.Intune.MAM.Remapper` balíček provádí nahrazení třídy mam automaticky vložením `MAM` tříd do hierarchie tříd běžně používaných `Xamarin.Forms` tříd. 

> [!NOTE]
> Integraci Xamarin. Forms je třeba provést společně s výše podrobnější integrací Xamarin. Android. Remapovače se chová jinak než u aplikací Xamarin. Forms, takže je nutné ruční MAM náhrady provést.

Po přidání remapovače do projektu budete muset provést přemístění ekvivalenty MAM. Například `FormsAppCompatActivity` a `FormsApplicationActivity` lze nadále používat ve vaší aplikaci, která poskytuje přepsání k `OnCreate` a `OnResume` jsou nahrazena ekvivalenty mam `OnMAMCreate` a v `OnMAMResume` uvedeném pořadí.

```csharp
    public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
    {
        protected override void OnMAMCreate(Bundle savedInstanceState)
        {
            base.OnMAMCreate(savedInstanceState);
            global::Xamarin.Forms.Forms.Init(this, savedInstanceState);
            LoadApplication(new App());
        }
```

Pokud nejsou náhrady provedeny, může dojít k následujícím chybám při kompilaci, dokud neprovedete náhrady:
* [Chyba kompilátoru CS0239](/dotnet/csharp/misc/cs0239). Tato chyba se obvykle objevuje v tomto formuláři ``'MainActivity.OnCreate(Bundle)': cannot override inherited member 'MAMAppCompatActivityBase.OnCreate(Bundle)' because it is sealed`` .
To je očekáváno, protože když přemapování mění dědění tříd Xamarin, budou provedeny určité funkce `sealed` a místo toho je přidána nová varianta mam k přepsání.
* [Chyba kompilátoru CS0507](/dotnet/csharp/language-reference/compiler-messages/cs0507): Tato chyba se běžně zobrazuje v tomto formuláři ``'MyActivity.OnRequestPermissionsResult()' cannot change access modifiers when overriding 'public' inherited member ...`` . Pokud přemapování změní dědění některých tříd Xamarin, budou některé členské funkce změněny na `public` . Pokud přepíšete některou z těchto funkcí, budete muset změnit tyto modifikátory přístupu, aby byly u těchto přepsání `public` také.

> [!NOTE]
> Remapper znovu zapíše závislost, kterou Visual Studio používá pro automatické dokončování IntelliSense. Proto může být nutné znovu načíst a znovu sestavit projekt při přidání nového mapování pro technologii IntelliSense, aby byly změny správně rozpoznány.

#### <a name="troubleshooting"></a>Poradce při potížích
* Pokud narazíte na prázdnou, bílou obrazovku aplikace při spuštění, může být nutné vynutit, aby bylo volání navigace spuštěno v hlavním vlákně.
* Vazby Xamarin sady Intune SDK nepodporují aplikace, které používají architekturu pro víc platforem, jako je například MvvmCross, z důvodu konfliktů mezi MvvmCross a třídami MAM Intune. I když někteří zákazníci mohou mít po přesunu svých aplikací do jednoduchých Xamarin. Forms úspěch s integrací, neposkytujeme pro vývojáře aplikací explicitní pokyny a moduly plug-in, které používají MvvmCross.

### <a name="company-portal-app"></a>Aplikace Portál společnosti
Vazby Xamarin sady Intune SDK spoléhají na přítomnost [portál společnosti](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) aplikace pro Android na zařízení, aby se povolily zásady ochrany aplikací. Portál společnosti načítá zásady ochrany aplikací ze služeb Intune. Při inicializaci načte aplikace z Portálu společnosti zásadu a kód, který ji vynucuje. Uživatel nemusí být přihlášený.

> [!NOTE]
> Když aplikace Portál společnosti není na zařízení s **Androidem** , chová se aplikace spravovaná v Intune stejně jako běžná aplikace, která nepodporuje zásady ochrany aplikací Intune.

U ochrany aplikací bez registrace zařízení _**nemusí**_ uživatel registrovat zařízení přes aplikaci Portál společnosti.

### <a name="sample-applications"></a>Ukázkové aplikace
Ukázkové aplikace zvýrazňování MAM funkcí v aplikacích Xamarin. Android a Xamarin. Forms jsou dostupné na [GitHubu](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Xamarin-Android-Apps).

## <a name="support"></a>Podpora
Pokud je vaše organizace stávajícím zákazníkem Intune, obraťte se na svého zástupce podpory Microsoftu, aby otevřel lístek podpory a [na stránce problémů na GitHubu](https://github.com/msintuneappsdk/intune-app-sdk-xamarin/issues)vytvořil problém. Pomůžeme vám, jakmile budeme.