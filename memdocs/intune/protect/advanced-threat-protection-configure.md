---
title: Konfigurace ATP v programu Microsoft Defender v Microsoft Intune – Azure | Microsoft Docs
description: Konfigurace rozšířené ochrany před internetovými útoky v programu Microsoft Defender (Microsoft Defender ATP) v Intune, včetně připojení ke službě ATP, zařízení pro registraci, přiřazení dodržování předpisů pro úrovně rizika a zásady podmíněného přístupu.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e19315f07d803e2aab53b3724fde85f1975c0c5
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264474"
---
# <a name="configure-microsoft-defender-atp-in-intune"></a>Konfigurace ochrany ATP v programu Microsoft Defender v Intune

Informace a postupy v tomto článku vám pomůžou nakonfigurovat integraci služby Microsoft Defender ATP s Intune. Konfigurace zahrnuje následující obecné kroky:

- Povolení ochrany ATP v programu Microsoft Defender pro vašeho tenanta
- Připojení zařízení s Windows a Androidem
- Nastavení úrovní rizik zařízení pomocí zásad dodržování předpisů
- Pomocí zásad podmíněného přístupu zablokovat zařízení, která překračují vaše očekávané úrovně rizika

Než začnete, musí vaše prostředí splňovat [požadavky](../protect/advanced-threat-protection.md#prerequisites) na používání služby Microsoft Defender ATP s Intune.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Povolení ochrany ATP v Microsoft Defenderu v Intune

Prvním krokem je nastavení propojení mezi službou Intune a ATP v programu Microsoft Defender. Nastavení vyžaduje přístup pro správu Security Center programu Microsoft Defender i k Intune.

Pro každého tenanta stačí pouze povolit Microsoft Defender ATP v jednom okamžiku.

### <a name="to-enable-microsoft-defender-atp"></a>Povolení služby Microsoft Defender ATP

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Endpoint Security**  >  **Microsoft Defender ATP**a pak vyberte **Otevřít Microsoft Defender Security Center**.

   ![Výběrem otevřete Security Center programu Microsoft Defender.](./media/advanced-threat-protection-configure/atp-device-compliance-open-microsoft-defender.png)

3. V **programu Microsoft Defender Security Center**:
   1. Vyberte **Nastavení**  >  **Rozšířené funkce**.
   2. Přepínač pro **připojení Microsoft Intune** přepněte do polohy **Zapnuto**:

      ![Povolení připojení k Intune](./media/advanced-threat-protection-configure/atp-security-center-intune-toggle.png)

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

## <a name="onboard-devices"></a>Připojení zařízení

Pokud jste povolili podporu pro Microsoft Defender ATP v Intune, navážeme spojení mezi službami Intune a Microsoft Defender ATP. Pak můžete připojit zařízení spravovaná pomocí Intune ke službě Microsoft Defender ATP, která umožňuje shromažďování dat o úrovních rizika zařízení.

### <a name="onboard-windows-devices"></a>Připojování zařízení s Windows

Po navázání spojení mezi Intune a ATP Microsoft Defenderu Intune obdrželo konfigurační balíček aktualizace ATP Microsoft Defenderu z ochrany ATP od Microsoft Defenderu. Tento konfigurační balíček nasadíte do zařízení s Windows s profilem konfigurace zařízení pro Microsoft Defender ATP.

Konfigurační balíček konfiguruje zařízení ke komunikaci se [službami ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) , aby kontrolovala soubory a zjišťoval hrozby. Zařízení je také nakonfigurované tak, aby hlásilo službě Microsoft Defender ATP úroveň rizika zařízení na základě zásad dodržování předpisů, které vytvoříte.

Po připojení zařízení pomocí konfiguračního balíčku to nemusíte dělat znovu. Zařízení můžete také připojit pomocí [zásad skupiny nebo Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

### <a name="create-the-device-configuration-profile-to-onboard-windows-devices"></a>Vytvoření profilu konfigurace zařízení pro připojování zařízení s Windows

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

### <a name="onboard-android-devices"></a>Připojit zařízení s Androidem

Po navázání připojení služby mezi Intune a ATP Microsoft Defender můžete zařízení s Androidem připojit do ATP v programu Microsoft Defender. Připojování zařízení konfiguruje, aby komunikovala s modulem Defender, který pak shromažďuje data o úrovni rizika zařízení.

Na rozdíl od zařízení s Windows není k dispozici konfigurační balíček pro zařízení se systémem Android. Místo toho si přečtěte téma [Přehled služby Microsoft Defender ATP pro Android](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) v dokumentaci ke službě Microsoft Defender ATP pro požadavky a pokyny k registraci pro Android.

U zařízení s Androidem můžete pomocí zásad Intune upravovat ATP Microsoft Defender v Androidu. Další informace najdete v tématu [ochrana ATP na webu Microsoft Defender ATP](../protect/advanced-threat-protection-manage-android.md).

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

## <a name="next-steps"></a>Další kroky

- [Konfigurace nastavení ATP v programu Microsoft Defender v Androidu](../protect/advanced-threat-protection-manage-android.md)
- [Monitorování dodržování předpisů pro úrovně rizika](../protect/advanced-threat-protection-monitor.md)

Další informace najdete v dokumentaci k Intune:

- [Použití úloh zabezpečení se správou ohrožení zabezpečení ATPs k nápravě problémů na zařízeních](atp-manage-vulnerabilities.md)
- [Začínáme se zásadami dodržování předpisů zařízeními](device-compliance-get-started.md)

Další informace najdete v dokumentaci ke službě Microsoft Defender ATP:

- [Podmíněný přístup Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Řídicí panel rizik pro ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
