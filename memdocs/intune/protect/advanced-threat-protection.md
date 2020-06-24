---
title: Používání ATP v programu Microsoft Defender v Microsoft Intune – Azure | Microsoft Docs
description: Použijte Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) s Intune, včetně nastavení a konfigurace, zprovoznění zařízení Intune s ATP a pak použijte hodnocení rizik ATP pro zařízení se zásadami dodržování předpisů a zásad podmíněného přístupu v zařízeních k ochraně síťových prostředků.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1141879a282219cdac72273e47c84b51df172d04
ms.sourcegitcommit: 397ec824f1368dcf06c3870c89f52347852062bd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/23/2020
ms.locfileid: "85264052"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Vymáhání dodržování předpisů pro Microsoft Defender ATP pomocí podmíněného přístupu v Intune

Integraci rozšířené ochrany před internetovými útoky v programu Microsoft Defender (Microsoft Defender ATP) můžete integrovat s Microsoft Intune jako řešení ochrany před mobilními hrozbami. Integrace vám může přispět k tomu, abyste zabránili narušení zabezpečení a omezili dopad narušení v rámci organizace. Ochrana ATP v programu Microsoft Defender spolupracuje se zařízeními se systémem Windows 10 nebo novějším a se zařízeními s Androidem.

Chcete-li být úspěšné, použijte následující konfigurace ve vzájemné součinnosti:

- **Navažte spojení mezi službou Intune a ATP v programu Microsoft Defender**. Toto připojení umožňuje službě Microsoft Defender ATP shromažďovat data o rizikech počítačů z podporovaných zařízení, která spravujete pomocí Intune.
- **Pomocí profilu konfigurace zařízení připojte zařízení s ATP Microsoft Defender**. Připojíte zařízení, abyste je mohli nakonfigurovat tak, aby komunikovala s ATP Microsoft Defender a poskytovali data, která vám pomůžou vyhodnotit jejich úroveň rizika.
- **Pomocí zásad dodržování předpisů pro zařízení nastavte úroveň rizika, které chcete udělit**. Úrovně rizika jsou hlášeny v ochraně ATP v programu Microsoft Defender. Zařízení, která překračují povolenou úroveň rizika, se označují jako nedodržující předpisy.
- **Pomocí zásad podmíněného přístupu** můžete uživatelům zablokovat přístup k podnikovým prostředkům ze zařízení, která nedodržují předpisy.

Při integraci Intune s modulem Microsoft Defender ATP můžete využít výhod programu Microsoft Defender ATPs Threat Management & (TVM) a [pomocí Intune napravit slabiny koncových bodů identifikované systémem TVM](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Příklad používání služby Microsoft Defender ATP s Intune

Následující příklad vám pomůže vysvětlit, jak tato řešení společně pomáhají chránit vaši organizaci. V tomto příkladu jsou služby Microsoft Defender ATP a Intune už integrované.

Vezměte v úvahu událost, kdy někdo pošle Wordovou přílohu s vloženým škodlivým kódem uživateli v rámci vaší organizace.

- Uživatel přílohu otevře a povolí obsah.
- Spustí se útok se zvýšenými oprávněními a útočník ze vzdáleného počítače má práva správce k zařízení oběti.
- Z tohoto zařízení získá vzdálený přístup i k dalším zařízením uživatele. Toto porušení zabezpečení může mít dopad na celou organizaci.

Ochrana ATP v programu Microsoft Defender může pomáhat vyřešit události zabezpečení, jako je tento scénář.

- V našem příkladu ATP Microsoft Defender detekuje, že zařízení provedlo neobvyklý kód, narazilo na eskalaci s oprávněním procesu, vložil škodlivý kód a vystavilo podezřelé vzdálené prostředí.
- Na základě těchto akcí ze zařízení klasifikuje ATP v programu Microsoft Defender [zařízení jako vysoce rizikové](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) a obsahuje podrobnou zprávu o podezřelé aktivitě na portálu Microsoft Defender Security Center.

Vzhledem k tomu, že máte zásady dodržování předpisů pro zařízení v Intune ke klasifikaci zařízení se *střední* nebo *vysokou* úrovní rizika při nedodržení předpisů, je ohrožené zařízení klasifikované jako nedodržující předpisy. Tato klasifikace umožňuje zásadám podmíněného přístupu vykázat a zablokovat přístup z tohoto zařízení k firemním prostředkům.

Pomocí zásad Intune můžete také upravit některé konfigurace pro Microsoft Defender ATP na Androidu. Další informace najdete v části [Konfigurace webové ochrany na zařízeních se systémem Android](#configure-web-protection-on-devices-that-run-android)dále v tomto článku.

## <a name="prerequisites"></a>Požadavky

Pokud chcete používat Microsoft Defender ATP s Intune, ujistěte se, že máte nakonfigurované a připravené k použití:

- Tenant s licencí pro Enterprise Mobility + Security E3 a Windows E5 (nebo Microsoft 365 Enterprise E5)
- Prostředí Microsoft Intune s využitím zařízení s Windows 10 [spravovaných pomocí Intune](../enrollment/windows-enroll.md) nebo zařízení s Androidem, která jsou taky připojená k Azure AD
- Ochrana [ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) a přístup k Security Center programu Microsoft Defender (portál ATP)

> [!NOTE]
> Ochrana ATP v programu Microsoft Defender není podporována zásadami ochrany aplikací pro iOS/iPadOS a Android Intune.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Povolení ochrany ATP v Microsoft Defenderu v Intune

Prvním krokem je nastavení propojení mezi službou Intune a ATP v programu Microsoft Defender. To vyžaduje přístup správce k Security Center programu Microsoft Defender i k Intune.

### <a name="to-enable-microsoft-defender-atp"></a>Povolení služby Microsoft Defender ATP

Pro každého tenanta stačí pouze povolit Microsoft Defender ATP v jednom okamžiku.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Endpoint Security**  >  **Microsoft Defender ATP**a pak vyberte **Otevřít Microsoft Defender Security Center**.

   ![Výběrem otevřete Security Center programu Microsoft Defender.](./media/advanced-threat-protection/atp-device-compliance-open-microsoft-defender.png)

3. V **programu Microsoft Defender Security Center**:
   1. Vyberte **Nastavení**  >  **Rozšířené funkce**.
   2. Přepínač pro **připojení Microsoft Intune** přepněte do polohy **Zapnuto**:

      ![Povolení připojení k Intune](./media/advanced-threat-protection/atp-security-center-intune-toggle.png)

   3. Vyberte **Uložit předvolby**.

4. V centru pro správu Microsoft Endpoint Manageru se vraťte do **ATP Microsoft Defender** . V části **nastavení zásad dodržování předpisů MDM**v závislosti na potřebách vaší organizace:
   - Nastavte **připojit zařízení s Windows verze 10.0.15063 a novější pro Microsoft Defender ATP** na **on** .
   - Nastavte **připojit zařízení s Androidem verze 6.0.0 a vyšší pro Microsoft Defender ATP** na **on** .

5. Vyberte **Uložit**.

> [!TIP]
> Když integrujete novou aplikaci do ochrany před mobilními hrozbami Intune a povolíte připojení k Intune, vytvoří Intune v Azure Active Directory zásady klasického podmíněného přístupu. Každá aplikace MTD, kterou integrujete, včetně [ATP Microsoft Defenderu](advanced-threat-protection.md) nebo kteréhokoli z našich dalších [partnerů MTD](mobile-threat-defense.md#mobile-threat-defense-partners), vytvoří nové zásady podmíněného přístupu v klasickém rozhraní. Tyto zásady je možné ignorovat, ale neměly by být upravované, odstraňující ani zakázané.
>
> Pokud se klasické zásady odstraní, budete muset odstranit připojení k Intune, které bylo zodpovědné za jeho vytvoření, a pak ho nastavit znovu. Tím se znovu vytvoří klasické zásady. Nepodporovaná migrace klasických zásad pro aplikace MTD na nový typ zásad pro podmíněný přístup.
>
> Klasické zásady podmíněného přístupu pro aplikace MTD:
>
> - Používají Intune MTD k tomu, aby vyžadovaly, aby byla zařízení zaregistrovaná ve službě Azure AD, aby měla ID zařízení před komunikací s partnery MTD. IDENTIFIKÁTOR je povinný, aby zařízení a mohl úspěšně ohlásit svůj stav do Intune.
> - Nemusíte mít žádný vliv na žádné jiné cloudové aplikace ani prostředky.
> - Liší se od zásad podmíněného přístupu, které byste mohli vytvořit, abyste mohli lépe spravovat MTD.
> - Ve výchozím nastavení nekomunikujete s dalšími zásadami podmíněného přístupu, které používáte pro vyhodnocení.
>
> Pokud chcete zobrazit klasické zásady podmíněného přístupu, přejděte v [Azure](https://portal.azure.com/#home)na **Azure Active Directory**  >  klasické zásady**podmíněného přístupu**  >  **Classic policies**.

## <a name="onboard-windows-devices-by-using-a-configuration-profile"></a>Připojování zařízení s Windows pomocí konfiguračního profilu

V případě platformy Windows můžete po navázání připojení mezi službami Intune a ATP v programu Microsoft Defender připojit zařízení spravovaná pomocí Intune do ATP, aby bylo možné shromažďovat data o jejich úrovni rizika. K připojení zařízení použijete profil konfigurace zařízení pro Microsoft Defender ATP.

Po navázání připojení k Microsoft Defender ATP obdržela Intune konfigurační balíček pro připojování ATP společnosti Microsoft Defender z ochrany ATP v programu Microsoft Defender. Tento balíček se nasadí do zařízení s profilem konfigurace zařízení. Konfigurační balíček konfiguruje zařízení ke komunikaci se [službami ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) , aby kontrolovala soubory, zjišťoval hrozby a nahlásila rizika pro ATP v programu Microsoft Defender. Po připojení zařízení pomocí konfiguračního balíčku to nemusíte dělat znovu. Zařízení můžete také připojit pomocí [zásad skupiny nebo Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

### <a name="create-the-device-configuration-profile"></a>Vytvoření profilu konfigurace zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte **Název** a **Popis**.
4. V části **Platforma** vyberte **Windows 10 a novější**.
5. Jako **typ profilu**vyberte **ATP Microsoft Defender (Windows 10 Desktop)**.
6. Nakonfigurujte nastavení:

   - **Typ balíčku konfigurace klienta ATP v programu Microsoft Defender**: vyberte možnost připojit a přidejte konfigurační **balíček do profilu** . Výběrem možnosti **Zrušit zprovoznění** konfigurační balíček odeberete.
  
     > [!NOTE]
     > Pokud jste správně navázali připojení k ochraně ATP v programu Microsoft Defender, Intune **se automaticky připojí** ke konfiguračnímu profilu a nastavení **typu balíčku konfigurace klienta služby Microsoft Defender ATP** nebude k dispozici.
  
   - **Sdílení ukázek pro všechny soubory**: **Povolit** umožňuje shromažďovat vzorky a sdílet je s Microsoft Defender atp. Pokud se například zobrazí podezřelý soubor, můžete ho odeslat do ochrany ATP v programu Microsoft Defender pro hloubkovou analýzu. **Nenakonfigurováno** nesdílí žádné ukázky do ochrany ATP v programu Microsoft Defender.
   - **Urychlení generování sestav telemetrie**: u zařízení, která mají vysoké riziko, toto nastavení **Povolte** , aby se častěji nahlášení telemetrie do služby ATP v programu Microsoft Defender.

     Připojení [počítačů s Windows 10 pomocí služby Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) obsahuje další podrobnosti o těchto nastaveních ATP v programu Microsoft Defender.

7. Vyberte **OK**a pak **vytvořit** a uložte změny, které vytvoří profil.
8. [Přiřaďte konfigurační profil zařízení](../configuration/device-profile-assign.md) k zařízením, která chcete vyhodnotit pomocí ATP programu Microsoft Defender.

## <a name="onboard-android-devices"></a>Připojit zařízení s Androidem
Po navázání připojení Service-to-Service mezi službou Intune a ANALYTICKÝm modulem Microsoft Defenderu je potřeba připojit spravovaná zařízení ke službě Microsoft Defender ATP, aby bylo možné shromažďovat a používat data o jejich úrovni rizika.

Podrobné pokyny pro připojování zařízení s Androidem, včetně požadavků pro koncové uživatele a správce, najdete v tématu [Rozšířená ochrana před internetovými útoky v programu Microsoft Defender pro Android](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) v dokumentaci ke službě Microsoft Defender atp.

## <a name="create-and-assign-compliance-policy-to-set-device-risk-level"></a>Vytvoření a přiřazení zásad dodržování předpisů pro nastavení úrovně rizika zařízení

V případě zařízení se systémem Windows i Android určuje zásada dodržování předpisů úroveň rizika, které považujete za přijatelné pro zařízení.

Pokud nejste obeznámeni s vytvářením zásad dodržování předpisů, v [článku Vytvoření zásady](../protect/create-compliance-policy.md#create-the-policy) *dodržování předpisů v Microsoft Intune* postupujte podle pokynů. Následující informace jsou specifické pro konfiguraci ochrany ATP v programu Microsoft Defender v rámci zásad dodržování předpisů.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení**zásady  >  **zásad dodržování předpisů**  >  **Policies**  >  **vytvořit zásadu**.

3. Pro **platformu**vyberte v rozevíracím seznamu jednu z následujících možností:
   - **Windows 10 a novější**
   - **Správce zařízení s Androidem**
   - **Android Enterprise**

   V dalším kroku vyberte **vytvořit** a otevřete tak okno **vytvořit konfiguraci zásad** .

4. Zadejte **název** , který vám pomůže tuto zásadu později identifikovat. Můžete také zvolit, že chcete zadat **Popis**.
  
5. Na kartě **Nastavení dodržování předpisů** rozbalte skupinu **ATP v programu Microsoft Defender** a nastavte možnost **vyžadovat, aby zařízení bylo na nebo pod hodnocením rizika počítače** na upřednostňovanou úroveň.

   Klasifikace úrovně hrozeb určují služby [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Vymazat:** Tato úroveň poskytuje nejvyšší zabezpečení. Zařízení nemůže mít žádné existující hrozby a bude mít přístup k prostředkům společnosti. Pokud se najde jakákoli hrozba, zařízení se vyhodnotí jako nevyhovující. (Ochrana ATP v programu Microsoft Defender používá hodnotu *Secure*.)
   - **Nízká:** Zařízení se vyhodnotí jako vyhovující, pokud se v něm nacházejí jenom hrozby nízké úrovně. Zařízení se středními nebo vysokou úrovní hrozeb nejsou kompatibilní.
   - **Střední:** Zařízení vyhovuje, pokud se v něm vyskytují hrozby na střední nebo nízké úrovni. Pokud se v zařízení zjistí hrozby vysoké úrovně, vyhodnotí se jako nevyhovující.
   - **Vysoká**: Tato úroveň je nejméně bezpečná a umožňuje všechny úrovně hrozeb. Zařízení s vysokou, střední nebo nízkou úrovní hrozeb se považují za vyhovující.

6. Dokončete konfiguraci zásady, včetně přiřazení zásad k příslušným skupinám.

## <a name="configure-web-protection-on-devices-that-run-android"></a>Konfigurace webové ochrany na zařízeních se systémem Android

Ve výchozím nastavení služba Microsoft Defender ATP pro Android zahrnuje a povoluje funkci webové ochrany. [Webové ochrany](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) pomáhají zabezpečit zařízení proti webovým hrozbám a chránit uživatele před útoky typu phishing.

Přestože je ve výchozím nastavení povolená, existují důvody, proč tuto ochranu na některých zařízeních s Androidem zakázat. Můžete se třeba rozhodnout, že použijete jenom funkci pro kontrolu aplikace v programu Microsoft Defender ATP, nebo můžete zabránit webové ochraně v používání sítě VPN během vyhledávání škodlivých adres URL.

Intune podporuje vypnutí všech funkcí webové ochrany nebo jejich části. Použitá metoda a možnosti, které můžete zakázat, závisí na tom, jak je zařízení s Androidem zaregistrované v Intune:

- **Správce zařízení s Androidem**: pomocí konfiguračního profilu můžete na zařízení nastavit vlastní nastavení OMA-URI, které zakazuje celou funkci webové ochrany nebo zakáže jenom používání VPN. Obecné informace o vlastním nastavení pro zařízení s Androidem najdete v tématu [vlastní nastavení](../configuration/custom-settings-android.md).

- **Pracovní profil Android Enterprise**: k zakázání webové ochrany použijte konfigurační profil aplikace a *Návrháře konfigurace* . Tato metoda a typ registrace podporují zákaz všech funkcí webové ochrany, ale nepodporují zákaz použití sítě VPN. Obecné informace o zásadách konfigurace aplikací najdete v tématu [použití návrháře konfigurace](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer).

Ke konfiguraci webové ochrany na zařízeních použijte následující postupy k vytvoření a nasazení příslušné konfigurace.

### <a name="disable-web-protection-for-android-device-administrator"></a>Zakázat web Protection pro správce zařízení s Androidem

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.

3. Zadejte následující nastavení:

   - **Platforma**: vyberte **Správce zařízení s Androidem** .
   - **Profil**: vyberte **vlastní** .

   Vyberte **Vytvořit**.

4. V části **základy**zadejte následující podrobnosti:

   - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Například *vlastní profil Androidu pro ochranu ATP na webu Microsoft Defender*
   - **Popis**: Zadejte popis profilu. Toto nastavení je volitelné, ale doporučuje se.

5. V **nastavení konfigurace**vyberte **Přidat**.

   Zadejte nastavení pro konfiguraci, kterou chcete nasadit:

   - **Zakázat web Protection**:
     - **Název**: Zadejte jedinečný název pro toto nastavení OMA-URI, abyste ho mohli snadno najít. Například *Zakázat web Protection ATP Microsoft Defender*
     - **Popis**: (volitelné) zadejte popis, který obsahuje přehled nastavení a další důležité podrobnosti.
     - **OMA-URI**: zadejte **./Vendor/MSFT/DefenderATP/AntiPhishing.**
     - **Datový typ**: použijte rozevírací nabídku a vyberte **celé číslo** .
     - **Hodnota**: Pokud chcete zakázat webovou ochranu, včetně kontroly založené na síti VPN, zadejte hodnotu **0** .
       > [!NOTE]
       > Zadejte hodnotu **1** pro povolení webové ochrany, což je výchozí nastavení pro webovou ochranu.

   - **Zakázat pouze používání sítě VPN pomocí webové ochrany**:
     - **Název**: Zadejte jedinečný název pro toto nastavení OMA-URI, abyste ho mohli snadno najít. Například *zakažte Microsoft Defender ATP web Protection VPN* .
     - **Popis**: (volitelné) zadejte popis, který obsahuje přehled nastavení a další důležité podrobnosti.
     - **OMA-URI**: zadejte **./Vendor/MSFT/DefenderATP/VPN.**
     - **Datový typ**: použijte rozevírací nabídku a vyberte **celé číslo** .
     - **Hodnota**: zadáním hodnoty **0** zakážete kontrolu založenou na síti VPN.
       > [!NOTE]
       > Zadejte hodnotu **1** pro povolení webové ochrany, což je výchozí nastavení pro webovou ochranu.

   Vyberte **Přidat** a uložte konfiguraci nastavení OMA-URI a pak pokračujte výběrem možnosti **Další** .

6. V části **přiřazení**určete skupiny, které obdrží tento profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](../configuration/device-profile-assign.md).

7. Pokud jste hotovi, klikněte na tlačítko **vytvořit**a po dokončení **Revize + vytvořit**. Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Zakázat web Protection pro Enterprise Working Profile v Androidu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **aplikace**  >  **zásady konfigurace aplikace**  >  **Přidat**a pak vyberte spravovaná zařízení.

3. V části **základy**zadejte následující podrobnosti:

   - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Například *Konfigurace aplikací pro Android pro ochranu ATP na webu Microsoft Defender ATP*.
   - **Popis**: Zadejte popis profilu. Toto nastavení je volitelné, ale doporučuje se.
   - **Platforma**: vyberte **Android Enterprise**
   - **Typ profilu**: **pouze vybrat pracovní profil**
   - **Cílová aplikace**: klikněte na **Vybrat aplikaci**.

4. V poli **přidružená aplikace**vyhledejte a vyberte **ATP**a pak vyberte **OK**  >  **Další**.

5. V **Nastavení**použijte rozevírací nabídku **formát nastavení konfigurace**, vyberte **použít Návrhář konfigurace**a pak klikněte na **Přidat**. Otevře se Editor JSON.

6. Vyhledejte a vyberte možnost **Webová ochrana**a potom kliknutím na **tlačítko OK** se vraťte na stránku **Nastavení** .

7. Pro **hodnotu konfigurace**zakažte web Protection zadáním hodnoty **0** .

   > [!NOTE]
   > Zadejte hodnotu **1** pro povolení webové ochrany, což je výchozí nastavení pro webovou ochranu.

   Pokračujte výběrem tlačítka **Next** (Další).

8. V části **přiřazení**určete skupiny, které obdrží tento profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](../configuration/device-profile-assign.md).

9. Pokud jste hotovi, klikněte na tlačítko **vytvořit**a po dokončení **Revize + vytvořit**. Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

## <a name="create-a-conditional-access-policy"></a>Vytvoření zásad podmíněného přístupu

Zásady podmíněného přístupu můžou používat data z ochrany ATP v programu Microsoft Defender k blokování přístupu k prostředkům pro zařízení, která přesahují nastavenou úroveň hrozeb. Můžete blokovat přístup ze zařízení k firemním prostředkům, jako je SharePoint nebo Exchange Online.

> [!TIP]
> Podmíněný přístup je technologie Azure Active Directory (Azure AD). Uzel *podmíněný přístup* , který najdete v centru pro správu Microsoft Endpoint Manageru, je uzel z *Azure AD*.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte položku **Endpoint Security**  >  **podmíněný přístup**  >  **nové zásady**.

3. Zadejte **Název** zásady a zvolte **Uživatelé a skupiny**. Pomocí možností Zahrnout a Vyloučit vyberte požadované skupiny pro nasazení zásady a zvolte **Hotovo**.

4. Zvolte **Cloudové aplikace** a vyberte aplikace, které chcete chránit. Zvolte například **Vybrat aplikace** a pak vyberte **Office 365 SharePoint Online** a **Office 365 Exchange Online**.

   Zvolením možnosti **Hotovo** uložte změny.

5. Vyberte **podmínky**,  >  které**klientské aplikace** použijí pro použití zásad pro aplikace a prohlížeče. Zvolte například **Ano** a pak povolte **Prohlížeč** a **Mobilní aplikace a desktopoví klienti**.

   Zvolením možnosti **Hotovo** uložte změny.

6. Vyberte **udělit** pro uplatnění podmíněného přístupu na základě dodržování předpisů zařízením. Vyberte například **udělit přístup**  >  **vyžadovat, aby zařízení bylo označené jako vyhovující**.

    Zvolením možnosti **Vybrat** uložte změny.

7. Zvolte **Povolit zásadu** a potom **Vytvořit**. Tím uložíte provedené změny.

## <a name="monitor-device-compliance"></a>Monitorování dodržování předpisů zařízením

Monitorujte stav zařízení, která mají zásady dodržování předpisů ATP v programu Microsoft Defender.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení**  >  **monitorování**  >  **dodržování zásad**.

3. Vyhledejte v seznamu Zásady ochrany ATP v programu Microsoft Defender a podívejte se, která zařízení jsou kompatibilní nebo nekompatibilní.

Můžete také použít *provozní* sestavu pro zařízení nedodržující předpisy ze stejného umístění:

1. Vyberte **zařízení**  >  **monitorovat**  >  **zařízení, která nedodržují předpisy**.

Další informace o sestavách najdete v tématu [sestavy Intune](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Zobrazit stav zprovoznění

Pokud chcete zobrazit stav připojování všech zařízení spravovaných přes Intune, můžete přejít na **Security Endpoint Security**v  >  **Microsoft Defenderu**. Na této stránce můžete také začít vytvářet konfigurační profil zařízení pro připojování více zařízení do ATP programu Microsoft Defender.

## <a name="next-steps"></a>Další kroky

[Podmíněný přístup Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)

[Řídicí panel rizik pro ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

[K nápravě problémů na zařízeních použijte úlohy zabezpečení se správou ohrožení zabezpečení ATPs](atp-manage-vulnerabilities.md).

[Začínáme se zásadami dodržování předpisů zařízeními](device-compliance-get-started.md)
