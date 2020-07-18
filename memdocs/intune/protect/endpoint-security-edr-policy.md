---
title: Správa nastavení zjišťování koncových bodů a odpovědí pomocí zásad zabezpečení Endpoint v Microsoft Intune | Microsoft Docs
description: Nakonfigurujte a nasaďte zásady pro zařízení, která spravujete pomocí zásad zjišťování koncových bodů zabezpečení koncového bodu a zásad odezvy ve službě Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: b1711dad8163409d05c5299e8d3b54ad619b48ec
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462061"
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

**Podpora zařízení z Configuration Manager**:

Aby bylo možné podporovat používání zásad EDR se zařízeními Configuration Manager, vyžaduje Configuration Manager prostředí následující další konfigurace. [Pokyny k konfiguraci](#set-up-configuration-manager-to-support-edr-policy) jsou k dispozici v tomto článku:

- **Configuration Manager verze 2002 nebo novější** – váš web musí běžet Configuration Manager 2002 nebo novější.

- **Instalace aktualizace Configuration Manager** – Pokud chcete povolit podporu v Configuration Manager 2002 pro používání zásad EDR, které vytvoříte v centru pro správu Microsoft Endpoint Manageru, nainstalujte v konzole Configuration Manager konzoly tuto aktualizaci:
  - **Oprava hotfix Configuration Manager 2002 (KB4563473)**

- **Konfigurace připojení tenanta** – připojení tenanta umožňuje synchronizovat kolekce zařízení z Configuration Manager do centra pro správu Microsoft Endpoint Manager. Pak můžete použít Centrum pro správu k nasazení zásad EDR do těchto kolekcí.

  Připojení klienta se často konfiguruje se spolusprávou, ale můžete nakonfigurovat připojení tenanta sami.

- **Synchronizovat kolekce Configuration Manager** – když konfigurujete připojení tenanta, můžete vybrat kolekce Configuration Managerch zařízení, které se mají synchronizovat s centrem pro správu Microsoft Endpoint Manageru. Můžete se také vrátit později a upravit kolekce zařízení, které synchronizujete. Zásady EDR pro zařízení Configuration Manager se dají přiřadit jenom ke kolekcím, které jste synchronizovali.

  Po výběru kolekcí k synchronizaci je musíte povolit pro použití s Microsoft Defender ATP.

- **Oprávnění ke službě Azure AD** – k dokončení nastavení připojení tenanta a ke konfiguraci kolekcí Configuration Manager budete synchronizovat s centrem pro správu Microsoft Endpoint Manageru, budete potřebovat účet s oprávněním globálního správce k vašemu předplatnému Azure.

## <a name="edr-profiles"></a>Profily EDR

[Zobrazte si nastavení](endpoint-security-edr-profile-settings.md) , která můžete nakonfigurovat pro následující platformy a profily.

**Intune** – pro zařízení, která spravujete pomocí Intune, se podporují následující možnosti:

- Platforma: **Windows 10 a novější** – Intune nasadí zásady do zařízení ve skupinách Azure AD.
- Profil: **detekce a odpověď koncového bodu (MDM)**

**Configuration Manager** – pro zařízení, která spravujete pomocí nástroje Configuration Manager, se podporují tyto možnosti:

- Platforma: **Windows 10 a Windows Server** – Configuration Manager nasadí zásady do zařízení v kolekcích Configuration Manager.
- Profil: **detekce a odpověď koncového bodu (ConfigMgr)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>Nastavit Configuration Manager pro podporu zásad EDR

Před nasazením zásad EDR pro Configuration Manager zařízení dokončete konfigurace popsané v následujících částech.

Tyto konfigurace se provádějí v rámci konzoly Configuration Manager a do nasazení Configuration Manager. Pokud nejste obeznámeni s Configuration Manager, naplánujte spolupráci se správcem Configuration Manager a dokončete tyto úlohy.  

Požadované úlohy jsou pokryté v následujících částech:

1. [Instalace aktualizace pro Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Povolení připojení tenanta](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Vybrat kolekce, které se mají synchronizovat](#task-3-select-collections-to-synchronize)
4. [Povolení kolekcí pro ATP v programu Microsoft Defender](#task-4-enable-collections-for-microsoft-defender-atp)

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

Pokud byla společná správa dříve povolená, připojení tenanta je už nastavené a můžete přejít k [úloze 3](#task-3-select-collections-to-synchronize).

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

   2. Ujistěte se, že je na stránce pro **registraci tenanta** vybraná možnost **nahrajte do centra pro správu Microsoft Endpoint Manageru** .

   3. Odstraňte kontrolu z **Povolení automatického zápisu klientů pro spolusprávu**.

      Pokud je vybrána tato možnost, průvodce nabídne další stránky k dokončení nastavení spolusprávy. Další informace najdete v tématu [Povolení spolusprávy](../../configmgr/comanage/how-to-enable.md) v obsahu Configuration Manager.

     ![Konfigurovat připojení tenanta](media/endpoint-security-edr-policy/tenant-onboarding.png)

4. Klikněte na tlačítko **Další** a pak na **Ano** , pokud chcete přijmout oznámení o **Vytvoření aplikace AAD** . Tato akce zřídí instanční objekt a vytvoří registraci aplikace služby Azure AD, aby se usnadnila synchronizace kolekcí do centra pro správu služby Microsoft Endpoint Manager.

5. Na stránce **Konfigurace nahrávání** nakonfigurujte, které kolekce se mají synchronizovat. Můžete omezit konfiguraci na jednu nebo několik kolekcí zařízení nebo použít nastavení Doporučené nahrávání zařízení pro **všechna moje zařízení spravovaná službou Microsoft Endpoint Configuration Manager**.

6. Kliknutím na **Souhrn** zkontrolujte výběr a pak klikněte na **Další**.

7. Po dokončení průvodce klikněte na tlačítko **Zavřít**.

   Připojení tenanta je teď nakonfigurované a vybrané kolekce se synchronizují do centra pro správu Microsoft Endpoint Manageru.

#### <a name="enable-tenant-attach-when-you-use-co-management"></a>Povolit připojení tenanta, když používáte spolusprávu

1. V konzole pro správu Configuration Manager najdete v části **Administration**  >  **Přehled**správy  >  **Cloud Services**  >  **spoluspráva**.

2. Klikněte pravým tlačítkem na nastavení spolusprávy a vyberte **vlastnosti**.

3. Na kartě **Konfigurovat nahrávání** vyberte **Odeslat do centra pro správu služby Microsoft Endpoint Manager**. Klikněte na **Použít**.
   - Výchozím nastavením pro nahrávání zařízení jsou **všechna moje zařízení spravovaná pomocí koncového bodu Microsoft Configuration Manager**. Můžete taky zvolit omezení konfigurace na jednu nebo několik kolekcí zařízení.

     ![Zobrazit kartu vlastnosti spolusprávy](media/endpoint-security-edr-policy/configure-upload.png)

4. Po zobrazení výzvy se přihlaste pomocí účtu *globálního správce* .

5. Kliknutím na **Ano** přijměte oznámení o **Vytvoření aplikace AAD** . Tato akce zřídí instanční objekt a vytvoří registraci aplikace služby Azure AD, která usnadňuje synchronizaci.

6. Kliknutím na tlačítko **OK** zavřete vlastnosti spolusprávy poté, co provedete změny.

   Připojení tenanta je teď nakonfigurované a vybrané kolekce se synchronizují do centra pro správu Microsoft Endpoint Manageru.

### <a name="task-3-select-collections-to-synchronize"></a>Úloha 3: Vyberte kolekce, které chcete synchronizovat.

Když je nakonfigurované připojení tenanta, můžete vybrat kolekce, které se mají synchronizovat. Pokud jste ještě nesynchronizoval kolekce nebo potřebujete změnit konfiguraci těch, které synchronizujete, můžete upravit vlastnosti spolusprávy v konzole Configuration Manager.

#### <a name="select-collections"></a>Vybrat kolekce

1. V konzole pro správu Configuration Manager najdete v části **Administration**  >  **Přehled**správy  >  **Cloud Services**  >  **spoluspráva**.

2. Klikněte pravým tlačítkem na nastavení spolusprávy a vyberte **vlastnosti**.

3. Na kartě **Konfigurovat nahrávání** vyberte **Odeslat do centra pro správu služby Microsoft Endpoint Manager**. Klikněte na **Použít**.

   Výchozím nastavením pro nahrávání zařízení jsou **všechna moje zařízení spravovaná pomocí koncového bodu Microsoft Configuration Manager**. Můžete taky zvolit omezení konfigurace na jednu nebo několik kolekcí zařízení.

### <a name="task-4-enable-collections-for-microsoft-defender-atp"></a>Úloha 4: povolení kolekcí pro ATP v programu Microsoft Defender

Až nakonfigurujete kolekce, které se mají synchronizovat s centrem pro správu Microsoft Endpoint Manageru, musíte pořád povolit, aby tyto kolekce byly vhodné pro připojování a zásady ochrany ATP v programu Microsoft Defender.  Uděláte to tak, že upravíte vlastnosti každé kolekce v konzole Configuration Manager.

#### <a name="enable-collections-for-use-with-advanced-threat-protection"></a>Povolit kolekce pro použití s pokročilou ochranou hrozeb

1. Z konzoly Configuration Manager připojené k lokalitě nejvyšší úrovně klikněte pravým tlačítkem na kolekci zařízení, kterou synchronizujete do centra pro správu Microsoft Endpoint Manageru, a vyberte **vlastnosti**.

2. Na kartě **synchronizace cloudu** povolte možnost **zpřístupnit tuto kolekci, aby bylo možné přiřadit zásady ochrany ATP v programu Microsoft Defender v Intune**.

   - Tuto možnost nemůžete vybrat, pokud Configuration Manager hierarchie není připojená ke klientovi.
  
   ![Konfigurace synchronizace cloudu](media/endpoint-security-edr-policy/cloud-sync.png)

3. Kliknutím na **OK** uložte konfiguraci.

   Zařízení v této kolekci teď můžou přijímat zásady ochrany ATP v programu Microsoft Defender.

## <a name="create-and-deploy-edr-policies"></a>Vytvoření a nasazení zásad EDR

Když je předplatné služby Microsoft Defender ATP integrováno do Intune, můžete vytvářet a nasazovat zásady EDR. Existují dva různé typy zásad EDR, které můžete vytvořit. Jeden typ zásad pro zařízení, která spravujete pomocí Intune prostřednictvím MDM. Druhý typ je pro zařízení, která spravujete pomocí Configuration Manager.

Zvolíte typ zásady, který vytvoříte při vytváření nových zásad EDR při výběru platformy pro danou zásadu.

Než budete moct nasadit zásady do zařízení spravovaných pomocí Configuration Manager, [nastavte Configuration Manager tak, aby podporovala zásady EDR](#set-up-configuration-manager-to-support-edr-policy) z centra pro správu Microsoft Endpoint Manageru.

### <a name="create-edr-policies"></a>Vytvoření zásad EDR

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte zásady zjišťování koncových bodů **zabezpečení koncového bodu**  >  **a odpověď**  >  **vytvořit**.

3. Vyberte platformu a profil pro zásady. Následující informace určují vaše možnosti:

   - Intune – Intune nasadí zásady do zařízení ve skupinách Azure AD. Když vytváříte zásadu, vyberte:
     - Platforma: **Windows 10 a novější**
     - Profil: **detekce a odpověď koncového bodu (MDM)**

   - Configuration Manager – Configuration Manager nasadí zásady do zařízení v kolekcích Configuration Manager. Když vytváříte zásadu, vyberte:
     - Platforma: **Windows 10 a Windows Server**
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

  U **zařízení s grafem senzorů ATP** se zobrazí jenom zařízení, která se úspěšně připojila k ochraně ATP programu Microsoft Defender prostřednictvím použití profilu **Windows 10 a novějšího** . Abyste měli jistotu, že máte v tomto grafu úplná reprezentace svých zařízení, nasaďte profil registrace na všechna vaše zařízení. Zařízení, která docházejí do ochrany ATP Microsoft Defenderu externím způsobem, jako je například Zásady skupiny nebo PowerShell, se počítají jako **zařízení bez senzoru ATP**.

- V případě zásad, které cílí na platformu **Windows 10 a Windows Server** (Configuration Manager), uvidíte přehled dodržování zásad, ale nemůžete přejít k podrobnostem a zobrazit další podrobnosti. Zobrazení je omezené, protože centrum pro správu přijímá informace o omezeném stavu od Configuration Manager, které spravuje nasazení zásad pro Configuration Manager zařízení.


[Prohlédněte si nastavení](endpoint-security-edr-profile-settings.md) , která můžete nakonfigurovat pro platformy i profily.

## <a name="next-steps"></a>Další kroky

- [Konfigurace zásad zabezpečení koncového bodu](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Přečtěte si další informace o [detekci a odezvě koncových bodů](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) v dokumentaci ke službě Microsoft Defender atp.
