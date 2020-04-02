---
title: Používání ATP v programu Microsoft Defender v Microsoft Intune – Azure | Microsoft Docs
description: Použijte Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) s Intune, včetně nastavení a konfigurace, registrace zařízení Intune s využitím ATP, a pak použijte hodnocení rizik ATP pro zařízení s dodržováním předpisů zařízením Intune a podmíněným nastavením. zásady přístupu pro ochranu síťových prostředků.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c5528e5de99e599c968f0c006aa98545b2004e2
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551553"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Vymáhání dodržování předpisů pro Microsoft Defender ATP pomocí podmíněného přístupu v Intune

Integraci rozšířené ochrany před internetovými útoky v programu Microsoft Defender (Microsoft Defender ATP) můžete integrovat s Microsoft Intune jako řešení ochrany před mobilními hrozbami. Integrace vám může přispět k tomu, abyste zabránili narušení zabezpečení a omezili dopad narušení v rámci organizace. Ochrana ATP v programu Microsoft Defender funguje na zařízeních se systémem Windows 10 nebo novějším.

Chcete-li být úspěšné, použijte následující konfigurace ve vzájemné součinnosti:

- **Navažte spojení mezi službou Intune a ATP v programu Microsoft Defender**. Toto připojení umožňuje službě Microsoft Defender ATP shromažďovat data o rizikech počítačů ze zařízení s Windows 10, která spravujete pomocí Intune.
- **Pomocí profilu konfigurace zařízení připojte zařízení s ATP Microsoft Defender**. Připojíte zařízení, abyste je mohli nakonfigurovat tak, aby komunikovala s ATP Microsoft Defender a poskytovali data, která vám pomůžou vyhodnotit jejich úroveň rizika.
- **Pomocí zásad dodržování předpisů pro zařízení nastavte úroveň rizika, které chcete udělit**. Úrovně rizika jsou hlášeny v ochraně ATP v programu Microsoft Defender. Zařízení, která překračují povolenou úroveň rizika, se označují jako nevyhovující.
- **Pomocí zásad podmíněného přístupu** můžete uživatelům zablokovat přístup k podnikovým prostředkům ze zařízení, která nedodržují předpisy.

Při integraci Intune s ATP Microsoft Defenderu můžete využít výhod správy ohrožení zabezpečení ATPs Threat & (TVM) a [pomocí Intune napravit slabiny koncových bodů identifikované pomocí nástroje TVM](atp-manage-vulnerabilities.md).

> [!NOTE]
> Uživatelské rozhraní (UI) Intune se aktualizuje na celé obrazovce a může trvat několik týdnů. Až do chvíle, kdy váš tenant obdrží tuto aktualizaci, budete mít při vytváření nebo úpravách nastavení popsaných v tomto článku mírně odlišný pracovní postup.

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Příklad používání služby Microsoft Defender ATP s Intune

Následující příklad vám pomůže vysvětlit, jak tato řešení společně pomáhají chránit vaši organizaci. V tomto příkladu jsou služby Microsoft Defender ATP a Intune už integrované.

Vezměte v úvahu událost, kdy někdo pošle Wordovou přílohu s vloženým škodlivým kódem uživateli v rámci vaší organizace.

- Uživatel přílohu otevře a povolí obsah.
- Spustí se útok se zvýšenými oprávněními a útočník ze vzdáleného počítače má práva správce k zařízení oběti.
- Z tohoto zařízení získá vzdálený přístup i k dalším zařízením uživatele. Toto porušení zabezpečení může mít dopad na celou organizaci.

Ochrana ATP v programu Microsoft Defender může pomáhat vyřešit události zabezpečení, jako je tento scénář.

- V našem příkladu ATP Microsoft Defender detekuje, že zařízení provedlo neobvyklý kód, narazilo na eskalaci s oprávněním procesu, vložil škodlivý kód a vystavilo podezřelé vzdálené prostředí.
- Na základě těchto akcí ze zařízení klasifikuje ATP v programu Microsoft Defender [zařízení jako vysoce rizikové](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) a obsahuje podrobnou zprávu o podezřelé aktivitě na portálu Microsoft Defender Security Center.

Vzhledem k tomu, že máte zásady dodržování předpisů pro zařízení v Intune ke klasifikaci zařízení se *střední* nebo *vysokou* úrovní rizika jako nevyhovující, je ohrožené zařízení klasifikované jako nevyhovující. Tato klasifikace umožňuje zásadám podmíněného přístupu vykázat a zablokovat přístup z tohoto zařízení k firemním prostředkům.

## <a name="prerequisites"></a>Předpoklady

Pokud chcete používat Microsoft Defender ATP s Intune, ujistěte se, že máte nakonfigurované a připravené k použití:

- Tenant s licencí pro Enterprise Mobility + Security E3 a Windows E5 (nebo Microsoft 365 Enterprise E5)
- Prostředí Microsoft Intune se zařízeními s Windows 10 [spravovanými v Intune](../enrollment/windows-enroll.md), která jsou zároveň připojená k Azure AD
- Ochrana [ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) a přístup k Security Center programu Microsoft Defender (portál ATP)

> [!NOTE]
> Ochrana ATP v programu Microsoft Defender není podporována zásadami ochrany aplikací pro iOS/iPadOS a Android Intune.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Povolení ochrany ATP v Microsoft Defenderu v Intune

Prvním krokem je nastavení propojení mezi službou Intune a ATP v programu Microsoft Defender. To vyžaduje přístup správce k Security Center programu Microsoft Defender i k Intune.

### <a name="to-enable-defender-atp"></a>Povolení ATP programu Defender

Pro každého tenanta stačí pouze povolit v programu Defender ATP pouze jeden čas.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Endpoint security** > **Microsoft Defender ATP**a pak vyberte **Otevřít Microsoft Defender Security Center**.

   ![Výběrem otevřete Security Center programu Microsoft Defender.](./media/advanced-threat-protection/atp-device-compliance-open-microsoft-defender.png)

4. V **programu Microsoft Defender Security Center**:
    1. Zvolte **Nastavení** > **Pokročilé funkce**.
    2. Přepínač pro **připojení Microsoft Intune** přepněte do polohy **Zapnuto**:

        ![Povolení připojení k Intune](./media/advanced-threat-protection/atp-security-center-intune-toggle.png)

    3. Vyberte **Uložit předvolby**.

4. V centru pro správu Microsoft Endpoint Manageru se vraťte do **ATP Microsoft Defender** . V části **nastavení zásad dodržování předpisů pro MDM**nastavte **připojit zařízení s Windows verze 10.0.15063 a vyšší k aplikaci Microsoft Defender ATP** na **zapnuto**.

5. Vyberte **Uložit**.

> [!TIP]
> Když integrujete novou aplikaci do ochrany před mobilními hrozbami Intune a povolíte připojení k Intune, vytvoří Intune v Azure Active Directory zásady klasického podmíněného přístupu. Každá aplikace MTD, kterou integrujete, včetně [ATP ATP](advanced-threat-protection.md) nebo kteréhokoli z našich dalších [partnerů MTD](mobile-threat-defense.md#mobile-threat-defense-partners), vytvoří nové zásady podmíněného přístupu v klasickém rozhraní. Tyto zásady je možné ignorovat, ale neměly by být upravované, odstraňující ani zakázané.
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
> Pokud chcete zobrazit klasické zásady podmíněného přístupu, přejděte v [Azure](https://portal.azure.com/#home)na **Azure Active Directory** > **podmíněný přístup** > **klasické zásady**.

## <a name="onboard-devices-by-using-a-configuration-profile"></a>Připojení zařízení pomocí konfiguračního profilu

Po navázání připojení Service-to-Service mezi Intune a ATP Microsoft Defender se spravovaná zařízení Intune zaregistrují do ATP, aby se mohla shromažďovat a používat data o jejich úrovni rizika. K připojení zařízení použijete profil konfigurace zařízení pro Microsoft Defender ATP.

Po navázání připojení k Microsoft Defender ATP obdržela Intune konfigurační balíček pro připojování ATP společnosti Microsoft Defender z ochrany ATP v programu Microsoft Defender. Tento balíček se nasadí do zařízení s profilem konfigurace zařízení. Konfigurační balíček konfiguruje zařízení ke komunikaci se [službami ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) , aby kontrolovala soubory, zjišťoval hrozby a nahlásila rizika pro ATP v programu Microsoft Defender. Po připojení zařízení pomocí konfiguračního balíčku to nemusíte dělat znovu. Zařízení můžete také připojit pomocí [zásad skupiny nebo Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

### <a name="create-the-device-configuration-profile"></a>Vytvoření profilu konfigurace zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte **Název** a **Popis**.
4. V části **Platforma** vyberte **Windows 10 a novější**.
5. Jako **typ profilu**vyberte **ATP Microsoft Defender (Windows 10 Desktop)** .
6. Nakonfigurujte nastavení:

   - **Typ balíčku konfigurace klienta ATP v programu Microsoft Defender**: vyberte možnost připojit a přidejte konfigurační **balíček do profilu** . Výběrem možnosti **Zrušit zprovoznění** konfigurační balíček odeberete.
  
     > [!NOTE]
     > Pokud jste správně navázali připojení k ochraně ATP v programu Microsoft Defender, Intune **se automaticky připojí** ke konfiguračnímu profilu a nastavení **typu balíčku konfigurace klienta služby Microsoft Defender ATP** nebude k dispozici.
  
   - **Sdílení ukázek pro všechny soubory**: **Povolit** umožňuje shromažďovat vzorky a sdílet je s Microsoft Defender atp. Pokud se například zobrazí podezřelý soubor, můžete ho odeslat do ochrany ATP v programu Microsoft Defender pro hloubkovou analýzu. **Nenakonfigurováno** nesdílí žádné ukázky do ochrany ATP v programu Microsoft Defender.
   - **Urychlení generování sestav telemetrie**: u zařízení, která mají vysoké riziko, toto nastavení **Povolte** , aby se častěji nahlášení telemetrie do služby ATP v programu Microsoft Defender.

     Připojení [počítačů s Windows 10 pomocí služby Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) obsahuje další podrobnosti o těchto nastaveních ATP v programu Microsoft Defender.

7. Zvolte **OK** a pak **Vytvořit**. Tím uložíte změny a vytvoříte profil.
8. [Přiřaďte konfigurační profil zařízení](../configuration/device-profile-assign.md) k zařízením, která chcete vyhodnotit pomocí ATP programu Microsoft Defender.

## <a name="create-and-assign-the-compliance-policy"></a>Vytvoření a přiřazení zásad dodržování předpisů

Zásady dodržování předpisů určují úroveň rizika, kterou považujete za přijatelné pro zařízení.

Pokud jste se neseznámili s vytvářením zásad dodržování předpisů, v článku Vytvoření zásady *dodržování předpisů v Microsoft Intune* [postupujte podle](../protect/create-compliance-policy.md#create-the-policy) pokynů. Následující informace jsou specifické pro konfiguraci ATP v programu Defender v rámci zásad dodržování předpisů.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **zásady dodržování předpisů** > **zásady** > **vytvořit zásadu**.

3. V části **platforma** vyberte *Windows 10 a novější*a potom výběrem **vytvořit** otevřete okno vytvořit konfiguraci **zásad** .

4. Na kartě **základy** zadejte **název** , který vám pomůže ho později identifikovat. Můžete také zvolit, že chcete zadat **Popis**.
  
5. Na kartě **Nastavení dodržování předpisů** rozbalte skupinu **ATP v programu Microsoft Defender** a nastavte možnost **vyžadovat, aby zařízení bylo na základě skóre rizika počítače** na upřednostňovanou úroveň.

   Klasifikace úrovně hrozeb určují služby [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Vymazat:** Tato úroveň poskytuje nejvyšší zabezpečení. Zařízení nemůže mít žádné existující hrozby a bude mít přístup k prostředkům společnosti. Pokud se najde jakákoli hrozba, zařízení se vyhodnotí jako nevyhovující. (Ochrana ATP v programu Microsoft Defender používá hodnotu *Secure*.)
   - **Nízká:** Zařízení se vyhodnotí jako vyhovující, pokud se v něm nacházejí jenom hrozby nízké úrovně. Zařízení se středními nebo vysokou úrovní hrozeb nejsou kompatibilní.
   - **Střední:** Zařízení vyhovuje, pokud se v něm vyskytují hrozby na střední nebo nízké úrovni. Pokud se v zařízení zjistí hrozby vysoké úrovně, vyhodnotí se jako nevyhovující.
   - **Vysoká**: Tato úroveň je nejméně bezpečná a umožňuje všechny úrovně hrozeb. To znamená, že zařízení s vysokou, střední nebo nízkou úrovní hrozeb se považují za vyhovující.

6. Dokončete konfiguraci zásady, včetně přiřazení zásad k příslušným skupinám.

## <a name="create-a-conditional-access-policy"></a>Vytvoření zásady podmíněného přístupu

Zásada podmíněného přístupu blokuje přístup k prostředkům pro zařízení, která přesahují úroveň ohrožení, kterou jste v zásadách dodržování předpisů nastavili. Můžete blokovat přístup ze zařízení k firemním prostředkům, jako je SharePoint nebo Exchange Online.

> [!TIP]
> Podmíněný přístup je technologie Azure Active Directory (Azure AD). Uzel podmíněného přístupu, ke kterému přistupuje z centra pro správu Microsoft Endpoint Manageru, je stejný uzel, ke kterému se přistupuje z *Azure AD*.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte možnost **zabezpečení koncového bodu** > **podmíněný přístup** > **nové zásady**.

3. Zadejte **Název** zásady a zvolte **Uživatelé a skupiny**. Pomocí možností Zahrnout a Vyloučit vyberte požadované skupiny pro nasazení zásady a zvolte **Hotovo**.

4. Zvolte **Cloudové aplikace** a vyberte aplikace, které chcete chránit. Zvolte například **Vybrat aplikace** a pak vyberte **Office 365 SharePoint Online** a **Office 365 Exchange Online**.

   Zvolením možnosti **Hotovo** uložte změny.

5. Když zvolíte **Podmínky** > **Klientské aplikace**, zásady se použijí pro aplikace a prohlížeče. Zvolte například **Ano** a pak povolte **Prohlížeč** a **Mobilní aplikace a desktopoví klienti**.

   Zvolením možnosti **Hotovo** uložte změny.

6. Vyberte **udělit** pro uplatnění podmíněného přístupu na základě dodržování předpisů zařízením. Zvolte například **Udělit přístup** > **Vyžadovat, aby zařízení bylo označené jako vyhovující**.

    Zvolením možnosti **Vybrat** uložte změny.

7. Zvolte **Povolit zásadu** a potom **Vytvořit**. Tím uložíte provedené změny.

## <a name="monitor-device-compliance"></a>Monitorování dodržování předpisů zařízením

Dále Sledujte stav zařízení, která mají zásady dodržování předpisů ATP v programu Microsoft Defender.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **monitorování** **zásady > dodržování předpisů**.

3. Vyhledejte v seznamu Zásady ochrany ATP v programu Microsoft Defender a podívejte se, která zařízení jsou kompatibilní nebo nekompatibilní.

Můžete také použít *provozní* sestavu pro zařízení nedodržující předpisy ze stejného umístění:

1. Vyberte **zařízení** > **monitorování** > **zařízení, která nedodržují předpisy**.

Další informace o sestavách najdete v tématu [sestavy Intune](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Zobrazit stav zprovoznění

Pokud chcete zobrazit stav připojování všech zařízení s Windows 10 spravovaných přes Intune, můžete přejít na **dodržování předpisů zařízením** > **ATP v programu Microsoft Defender**. Na této stránce můžete také zahájit vytváření konfiguračního profilu zařízení pro připojování více zařízení do ATP v programu Microsoft Defender.

## <a name="next-steps"></a>Další kroky

[Podmíněný přístup Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)

[Řídicí panel rizik pro ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

[K nápravě problémů na zařízeních použijte úlohy zabezpečení se správou ohrožení zabezpečení ATPs](atp-manage-vulnerabilities.md).

[Začínáme se zásadami dodržování předpisů zařízeními](device-compliance-get-started.md)
