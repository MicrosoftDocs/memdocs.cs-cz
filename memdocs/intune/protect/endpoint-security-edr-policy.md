---
title: Správa nastavení zjišťování koncových bodů a odpovědí pomocí zásad zabezpečení Endpoint v Microsoft Intune | Microsoft Docs
description: Nakonfigurujte a nasaďte zásady pro zařízení, která spravujete pomocí zásad zjišťování koncových bodů zabezpečení koncového bodu a zásad odezvy ve službě Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: ff880b564562b3e6d67dc852f97ef7a9f5d6b814
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915037"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Zjišťování koncových bodů a zásady odezvy pro zabezpečení koncového bodu v Intune

Když integrujete integraci programu Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) s Intune, můžete použít zásady zabezpečení koncového bodu pro zjišťování koncových bodů a odpověď (EDR) ke správě nastavení EDR a připojení zařízení k ATP v programu Microsoft Defender.

Možnosti detekce a reakce koncových bodů ATP v programu Microsoft Defender poskytují pokročilé detekce útoků téměř v reálném čase a napadnutelné. Analytici zabezpečení můžou efektivně upřednostňovat výstrahy, získávat přehled o plném rozsahu porušení a reagovat na reakce na nápravu hrozeb.

Zásady EDR obsahují profily specifické pro platformu ke správě nastavení pro EDR. Profily automaticky zahrnují *balíček připojování* pro ATP v programu Microsoft Defender. Balíčky pro připojování jsou konfigurace zařízení pro práci s ATP Microsoft Defenderu. Po zprovoznění zařízení můžete začít používat data o ohroženích z tohoto zařízení.

Zásady EDR se nasazují do skupin zařízení v Azure Active Directory (Azure AD), které spravujete přes Intune, a ke kolekcím místních zařízení, která spravujete pomocí nástroje Configuration Manager, včetně serverů Windows. Zásady EDR pro různé cesty pro správu vyžadují různé balíčky připojování. Proto vytvoříte samostatné zásady EDR pro různé typy zařízení, která spravujete.

Zásady zabezpečení koncového bodu pro EDR najdete v části *Správa* v uzlu **Security Endpoint** v [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Zobrazit [nastavení pro zjišťování koncových bodů a profily odpovědí](endpoint-security-edr-profile-settings.md).

## <a name="prerequisites-for-edr-policies"></a>Předpoklady pro zásady EDR

**Obecné**:

- **Tenant pro Microsoft Defender Advanced Threat Protection** – váš tenant Microsoft Defender ATP musí být integrovaný do vašeho tenanta Microsoft Endpoint Manageru (předplatné Intune), aby bylo možné vytvářet zásady EDR. Viz [Použití ATP v programu Microsoft Defender](advanced-threat-protection.md) v dokumentaci k Intune.

**Podpora pro Configuration Manager klienty**:

- **Nastavení připojení tenanta pro Configuration Manager zařízení** – pro podporu nasazení zásad EDR do zařízení spravovaných pomocí Configuration Manager nakonfigurujte *připojení tenanta*. To zahrnuje konfiguraci Configuration Manager kolekcí zařízení pro podporu zásad zabezpečení koncového bodu služby Intune.

  Pokud chcete nastavit připojení tenanta, včetně synchronizace kolekcí Configuration Manager do centra pro správu Microsoft Endpoint Manageru a jeho povolení pro práci se zásadami zabezpečení koncového bodu, přečtěte si téma [Konfigurace připojení tenanta pro podporu zásad ochrany koncových](../protect/tenant-attach-intune.md)bodů.

## <a name="edr-profiles"></a>Profily EDR

[Zobrazte si nastavení](endpoint-security-edr-profile-settings.md) , která můžete nakonfigurovat pro následující platformy a profily.

**Intune** – pro zařízení, která spravujete pomocí Intune, se podporují následující možnosti:

- Platforma: **Windows 10 a novější** – Intune nasadí zásady do zařízení ve skupinách Azure AD.
- Profil: **detekce a odpověď koncového bodu (MDM)**

**Configuration Manager** – pro zařízení, která spravujete pomocí nástroje Configuration Manager, se podporují tyto možnosti:

- Platforma: **Windows 10 a Windows Server (ConfigMgr)** – Configuration Manager nasadí zásady do zařízení v kolekcích Configuration Manager.
- Profil: **detekce a odpověď koncového bodu (ConfigMgr)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>Nastavit Configuration Manager pro podporu zásad EDR

Před nasazením zásad EDR pro Configuration Manager zařízení dokončete konfigurace popsané v následujících částech.

Tyto konfigurace se provádějí v rámci konzoly Configuration Manager a do nasazení Configuration Manager. Pokud nejste obeznámeni s Configuration Manager, naplánujte spolupráci se správcem Configuration Manager a dokončete tyto úlohy.  

Požadované úlohy jsou pokryté v následujících částech:

1. [Instalace aktualizace pro Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Povolení připojení tenanta](#task-2-configure-tenant-attach-and-synchronize-collections)  

> [!TIP]
> Další informace o používání služby Microsoft Defender ATP s Configuration Manager najdete v následujících článcích v Configuration Managerm obsahu:
>
> - [Připojení klientů Configuration Manager k ochraně ATP v programu Microsoft Defender prostřednictvím centra pro správu Microsoft Endpoint Manageru](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Připojení tenanta Microsoft Endpoint Manageru: synchronizace zařízení a akce zařízení](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Úloha 1: instalace aktualizace pro Configuration Manager

Configuration Manager verze 2002 vyžaduje aktualizaci, která podporuje použití se zjišťováním koncových bodů a zásadami odezvy, které nasazujete z centra pro správu Microsoft Endpoint Manageru.

**Podrobnosti aktualizace**:

- **Oprava hotfix Configuration Manager 2002 (KB4563473)**

Tuto aktualizaci najdete jako *konzolovou aktualizaci* pro Configuration Manager 2002.

Pokud chcete nainstalovat tuto aktualizaci, postupujte podle pokynů v části [instalace konzolových aktualizací](../../configmgr/core/servers/manage/install-in-console-updates.md) v dokumentaci k Configuration Manager.

Po instalaci aktualizace se sem vraťte, abyste mohli pokračovat v konfiguraci prostředí pro podporu zásad EDR z centra pro správu Microsoft Endpoint Manageru.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Úloha 2: Konfigurace tenanta pro připojení a synchronizaci kolekcí

Když se připojíte ke klientovi, určete kolekce zařízení z nasazení Configuration Manager pro synchronizaci s centrem pro správu Microsoft Endpoint Manageru. Po synchronizaci kolekcí použijte centrum pro správu k zobrazení informací o těchto zařízeních a nasazení zásad EDR z Intune do těchto zařízení.  

Další informace o scénáři připojení klienta najdete v tématu [Povolení připojení tenanta](../../configmgr/tenant-attach/device-sync-actions.md) v obsahu Configuration Manager.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Povolit připojení tenanta, když není povolená spoluspráva

> [!TIP]
> Pomocí **Průvodce konfigurací spolusprávy** v konzole Configuration Manager můžete povolit připojení tenanta, ale nemusíte umožňovat spolusprávu.

Pokud plánujete povolit spolusprávu, Seznamte se s spolusprávou, jejich požadavky a správou úloh, než budete pokračovat. Přečtěte si téma [co je spoluspráva?](../../configmgr/comanage/overview.md) v dokumentaci k Configuration Manager.

1. V konzole pro správu Configuration Manager najdete v části **Administration**  >  **Přehled**správy  >  **Cloud Services**  >  **spoluspráva**.
2. Na pásu karet klikněte na **Konfigurovat spolusprávu** a otevřete průvodce.
3. Na stránce registrace **tenanta** vyberte **AzurePublicCloud** pro vaše prostředí. Cloud Azure Government není podporovaný.
   1. Klikněte na **Přihlásit se**. Přihlaste se pomocí účtu *globálního správce* .

Pro zařízení, která spravujete pomocí Intune, se podporují následující možnosti:

- Platforma: **Windows 10 a novější** – Intune nasadí zásady do zařízení ve skupinách Azure AD.
  - Profil: **detekce a odpověď koncového bodu (MDM)**

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Zařízení spravovaná pomocí Configuration Manager *(ve verzi Preview)*

Pro zařízení, která spravujete pomocí Configuration Manager ve scénáři *připojení tenanta* , se podporují následující:

- Platforma: **Windows 10 a Windows Server (ConfigMgr)** – Configuration Manager nasadí zásady do zařízení v kolekcích Configuration Manager.
  - Profil: **detekce a odpověď koncového bodu (ConfigMgr) (Preview)**

## <a name="create-and-deploy-edr-policies"></a>Vytvoření a nasazení zásad EDR

Když integrujete předplatné Microsoft Defender ATP s Intune, můžete vytvářet a nasazovat zásady EDR. Existují dva různé typy zásad EDR, které můžete vytvořit. Jeden typ zásad pro zařízení, která spravujete pomocí Intune prostřednictvím MDM. Druhý typ je pro zařízení, která spravujete pomocí Configuration Manager.

Zvolte typ zásady, která se má vytvořit při konfiguraci nových zásad EDR, a to tak, že vyberete platformu pro zásady.

Než budete moct nasadit zásady do zařízení spravovaných pomocí Configuration Manager, nastavte Configuration Manager tak, aby podporovala zásady EDR z centra pro správu Microsoft Endpoint Manageru. Viz téma [Konfigurace připojení tenanta pro podporu zásad Endpoint Protection](../protect/tenant-attach-intune.md).


### <a name="create-edr-policies"></a>Vytvoření zásad EDR

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte zásady zjišťování koncových bodů **zabezpečení koncového bodu**  >  **a odpověď**  >  **vytvořit**.

3. Vyberte platformu a profil pro zásady. Následující informace určují vaše možnosti:

   - Intune – Intune nasadí zásady do zařízení ve skupinách Azure AD. Když vytváříte zásadu, vyberte:
     - Platforma: **Windows 10 a novější**
     - Profil: **detekce a odpověď koncového bodu (MDM)**

   - Configuration Manager – Configuration Manager nasadí zásady do zařízení v kolekcích Configuration Manager. Když vytváříte zásadu, vyberte:
     - Platforma: **Windows 10 a Windows Server (ConfigMgr)**
     - Profil: **detekce a odpověď koncového bodu (ConfigMgr)**

4. Vyberte **Vytvořit**.

5. Na stránce **základy** zadejte název a popis profilu a pak klikněte na tlačítko **Další**.

6. Na stránce **nastavení konfigurace** nakonfigurujte nastavení, které chcete spravovat pomocí tohoto profilu. Balíček pro registraci je automaticky zahrnutý a není to, co můžete konfigurovat.

   Po dokončení konfigurace nastavení vyberte **Další**.

7. *Tento krok platí jenom pro profil **zjišťování koncových bodů a odpověď (MDM)** *:  

   Na stránce **značky oboru** zvolte **možnost vybrat značky oboru** a otevřete tak podokno *Vybrat značky* , abyste přiřadili značky oboru k profilu.
  
   Pokračujte výběrem tlačítka **Další**.

8. Na stránce **přiřazení** vyberte skupiny nebo kolekce, které tyto zásady dostanou. Volba závisí na zvolené platformě a profilu:

   - V případě Intune vyberete skupiny z Azure AD.
   - V případě Configuration Manager vyberete kolekce z Configuration Manager, které jste synchronizovaly do centra pro správu Microsoft Endpoint Manageru a jsou povolené pro zásady ochrany ATP v programu Microsoft Defender.

   V tuto chvíli se můžete rozhodnout nepřiřazovat skupiny nebo kolekce a později upravit zásadu a přidat přiřazení.

   Až budete připraveni pokračovat, vyberte **Další**.

9. Po dokončení na stránce **Revize + vytvořit** klikněte na **vytvořit**.

   Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

## <a name="edr-policy-reports"></a>Sestavy zásad EDR

Podrobnosti o zásadách EDR, které nasadíte, můžete zobrazit v centru pro správu Microsoft Endpoint Manageru. Pokud si chcete zobrazit podrobnosti, Projděte si nasazení a odpověď koncového bodu **zabezpečení Endpoint**  >  **Endpoint deployment and response**a vyberte zásadu, pro kterou chcete zobrazit podrobnosti o kompatibilitě:

- V případě zásad, které se zaměřují na platformu **Windows 10 a novější** (Intune), uvidíte přehled dodržování zásad. Můžete také vybrat graf pro zobrazení seznamu zařízení, která zásady obdržela, a přejít k jednotlivým zařízením a získat další podrobnosti.

  Graf pro **zařízení s senzorem ATP** zobrazuje jenom zařízení, která se úspěšně připojila k ochraně ATP Microsoft Defenderu prostřednictvím použití profilu **Windows 10 a novějšího** . Abyste měli jistotu, že máte v tomto grafu úplná reprezentace svých zařízení, nasaďte profil registrace na všechna vaše zařízení. Zařízení, která docházejí do ochrany ATP Microsoft Defenderu externím způsobem, jako je například Zásady skupiny nebo PowerShell, se počítají jako **zařízení bez senzoru ATP**.

- Pro zásady, které cílí na platformu **Windows 10 a Windows Server (nástroj ConfigMgr)** (Configuration Manager), uvidíte přehled dodržování zásad, ale nemůžete přejít k podrobnostem a zobrazit další podrobnosti. Zobrazení je omezené, protože centrum pro správu přijímá informace o omezeném stavu od Configuration Manager, které spravuje nasazení zásad pro Configuration Manager zařízení.

[Prohlédněte si nastavení](endpoint-security-edr-profile-settings.md) , která můžete nakonfigurovat pro platformy i profily.

## <a name="next-steps"></a>Další kroky

- [Konfigurace zásad zabezpečení koncového bodu](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Přečtěte si další informace o [detekci a odezvě koncových bodů](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) v dokumentaci ke službě Microsoft Defender atp.