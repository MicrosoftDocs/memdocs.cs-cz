---
title: Správa počítačů s klientským softwarem v Microsoft Intune – Azure | Microsoft Docs
description: Spravujte počítače s Windows pomocí instalace klientského softwaru Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/15/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 3b8d22fe-c318-4796-b760-44f1ccf34312
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: e4e917ca63bb671e8dfa46b280a4130051e75ef0
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326499"
---
# <a name="manage-windows-pcs-as-computers-via-intune-software-client"></a>Správa počítačů s Windows jako počítačů prostřednictvím softwarového klienta Intune

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!WARNING]
> Microsoft oznámil, že [podpora Windows 7 končí 14 ledna 2020](https://support.microsoft.com/help/4057281/windows-7-support-will-end-on-january-14-2020). K tomuto datu přestane také Intune podporovat zařízení s Windows 7. Microsoft důrazně doporučuje přechod na Windows 10, abyste zabránili přerušení služeb a podpory.
> 
> Další informace najdete v [příspěvku na blogu o plánu změn](https://aka.ms/Windows7_Intune).

> [!NOTE]
> V Microsoft Intune můžete spravovat počítače s Windows buď [jako mobilní zařízení prostřednictvím správy mobilních zařízení (MDM)](../enrollment/windows-enroll.md), nebo jako počítače se softwarovým klientem Intune, jak je popsáno níže. Microsoft však zákazníkům doporučuje, aby pokud možno [používali řešení pro správu MDM](../enrollment/windows-enroll.md). Další informace najdete v tématu [porovnání správy počítačů s Windows jako počítačů nebo mobilních zařízení](pc-management-comparison.md) .

Intune poskytuje organizacím ucelené řešení pro správu mobilních zařízení. Pomocí moderních funkcí pro správu zařízení, které jsou součástí operačního systému Windows 10, dokáže Intune spravovat počítače s Windows 10 jako mobilní zařízení. Pro splnění potřeb správy vaší organizace může Intune také spravovat počítače s Windows jako počítače pomocí softwarového klienta Intune. Tato metoda správy využívá tradiční funkce pro správu počítačů ve starších operačních systémech Windows.

Softwarový klient Intune je nejvhodnější pro počítače se staršími operačními systémy Windows (například Windows 7), které nelze spravovat jako mobilní zařízení. Ke správě počítačů z cloudu používá softwarový klient Intune funkce správy, jako jsou například Zásady skupiny.

S využitím tohoto softwarového klienta můžete přes Intune spravovat až 7 000 počítačů s Windows jako počítače. V rozsáhlejších nasazeních spravujte počítače s Windows 10 jako mobilní zařízení. Každá verze Intune a aktualizace Windows 10 obsahuje funkce pro správu založené na architektuře pro správu mobilních zařízení. Důrazně proto doporučujeme, aby vaše organizace přešla na systém Windows 10, který se spravuje jako mobilní zařízení.

> [!NOTE]
> Zařízení s Windows 8.1 a novějšími systémy můžete spravovat jako počítače pomocí klientského softwaru Intune, nebo jako mobilní zařízení. Na jednom zařízení nelze použít obě metody. Pečlivě zvažte, než se rozhodnete počítače spravovat pomocí klientského softwaru Intune. Toto téma se týká jenom správy zařízení jako počítačů pomocí klientského softwaru Intune.

## <a name="requirements-for-intune-pc-client-management"></a>Požadavky na správu počítačového klienta Intune

**Hardware:** :  
Níže jsou uvedené minimální požadavky na hardware pro instalaci klientského softwaru Intune:

|Požadavek|Další informace|
|---------------|--------------------|
|Síť|Klient vyžaduje, aby byl počítač připojený k Internetu.|
|Procesor a paměť|Viz požadavky na procesor a paměť RAM pro operační systém počítače.|
|Místo na disku|200 MB volného místa na disku před instalací klientského softwaru.|

**Software**:  
Níže jsou uvedené požadavky na software pro instalaci klientského softwaru:

|Požadavek|Další informace|
|---------------|--------------------|
|Operační systém | Zařízení s Windows se systémem Windows 7 SP1 a Windows 8.1 nebo novějším. </br></br>**Verze Home Edition nejsou podporovány.**|
|Oprávnění správce|Účet, který instaluje klientský software, musí mít oprávnění místního správce pro toto zařízení.|
|Instalační služba systému Windows verze 3.1|Na počítači musí být Instalační služba systému Windows minimálně verze 3.1.<br /><br />Pokud chcete zobrazit verzi Instalační služby systému Windows na počítači:<br /><br />  Na počítači klikněte pravým tlačítkem myši na **%windir%\System32\msiexec.exe** a potom klikněte na **Vlastnosti**.<br /><br />Nejnovější verzi Instalační služby systému Windows můžete stáhnout ze stránky [Windows Installer Redistributables](https://go.microsoft.com/fwlink/?LinkID=234258) na webu Microsoft Developer Network.|
|Odebrání nekompatibilního klientského softwaru|Před instalací klientského softwaru Intune odinstalujte z počítače tento klientský software: Configuration Manager, Operations Manager a Service Manager.|

## <a name="deploying-the-intune-software-client"></a>Nasazení softwarového klienta Intune
Jako správce Intune můžete softwarového klienta Intune zpřístupnit uživatelům různými způsoby. Pokyny najdete v článku [Instalace softwarového klienta Intune na počítače s Windows](install-the-windows-pc-client-with-microsoft-intune.md).

## <a name="computer-management-capabilities-with-the-intune-client-software"></a>Možnosti správy počítačů pomocí klientského softwaru Intune
Ve většině scénářů si svoje zařízení zaregistrujete v Microsoft Intune. Tato služba poskytuje větší sadu funkcí. Ke správě počítačů můžete ale také použít softwarového klienta Intune, který poskytuje následující funkce:

- **[Správa aktualizací softwaru](keep-windows-pcs-up-to-date-with-software-updates-in-microsoft-intune.md)** – Počítače můžete udržovat stále aktuální a můžete rozhodnout, kdy se mají aktualizace instalovat.

- **[Zásady brány Windows Firewall](help-protect-windows-pcs-using-windows-firewall-policies-in-microsoft-intune.md)** – Tyto zásady pomáhají zajistit, že v žádném počítači používaném ve vaší společnosti není neaktivní nebo nesprávně nakonfigurovaná brána Windows Firewall.

- **[Ochrana proti malwaru](help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune.md)** – Součástí Intune je služba Endpoint Protection, která pomáhá chránit počítače před malwarem.

- **[Vzdálená pomoc](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)** – Intune umožňuje uživatelům kontaktovat pracovníky technické podpory, kteří jim pak můžou pomoct prostřednictvím funkce vzdálené plochy, která je součástí Intune (vyžaduje software TeamViewer).

- **[Správa licencí na software](manage-license-agreements-for-windows-pc-software-in-microsoft-intune.md)** – Můžete sledovat, kolik licencí softwaru je dostupných a kolik z nich se právě používá.
- **[Nasazení aplikací](add-apps-for-windows-pcs-in-microsoft-intune.md)** – Do počítačů, které spravujete, můžete nasadit software. Pokud ke správě počítačů použijete softwarového klienta, některé funkce správy nejsou dostupné.

<!-- - **Compliance settings reporting** -->

## <a name="policies-and-app-deployments-for-the-intune-software-client"></a>Zásady a nasazení aplikace pro klientský software Intune

I když klientský software Intune podporuje [možnosti správy, které pomáhají chránit počítače](policies-to-protect-windows-pcs-in-microsoft-intune.md) pomocí správy aktualizací softwaru, brány Windows Firewall a služby Endpoint Protection, nemůžou být na počítače spravované pomocí klientského softwaru Intune zacílené jiné zásady Intune, včetně nastavení zásad **Windows**, která jsou specifická pro správu mobilních zařízení.

Pokud ke správě počítačů s Windows používáte klientský software Intune, můžete používat jenom zásady, které jsou uvedené v části **Správa počítače**.

Intune spravuje počítače s Windows pomocí zásad, podobně jako to dělají objekty zásad skupiny (GPO) služby AD DS (Active Directory Domain Services) Windows Serveru. Pokud počítače připojené k doméně Active Directory spravujete pomocí Intune, [zajistěte, aby zásady Intune nekolidovaly s jinými objekty zásad skupiny](resolve-gpo-and-microsoft-intune-policy-conflicts.md) používanými ve vaší organizaci. Další informace najdete v článku [Zásady skupiny pro začátečníky](https://technet.microsoft.com/library/hh147307.aspx).

  ![Výběr šablony pro nové zásady počítačů PC se systémem Windows](./media/manage-windows-pcs-with-microsoft-intune/select-template-for-pc-policy.png)

K nasazování aplikací můžete použít pouze Instalační službu systému Windows (.exe, .msi).

  ![Výběr platformy a umístění softwarových souborů klientského počítače](./media/manage-windows-pcs-with-microsoft-intune/select-platform-of-software-files-for-pc-agent.png)

## <a name="common-tasks-for-windows-pcs"></a>Běžné úlohy pro počítače s Windows

Konzolu správce Intune můžete použít k dalším běžným úlohám správy u počítačů s Windows s nainstalovaným klientem:
- [Zjednodušení správy počítačů pomocí zásad](use-policies-to-simplify-windows-pc-management.md) –Popisuje zásady **Správa počítače** v Intune a uvádí nastavení pro Microsoft Intune Center.

- [Zobrazení inventáře hardwaru a softwaru u počítačů s Windows](view-hardware-and-software-inventory-for-windows-pcs-in-microsoft-intune.md) – Vysvětluje, jak vytvořit sestavu s informacemi o hardwarových možnostech počítačů a o softwaru, který je na nich nainstalovaný. Vysvětluje také, jak obnovit inventář počítačů tak, aby byl aktuální.
- [Vyřazení počítače s Windows](retire-a-windows-pc-with-microsoft-intune.md) – Uvádí postup, jak vyřadit počítač s Windows, a popisuje, co se stane při vyřazení počítače.
- [Správa propojení uživatelů se zařízeními u počítačů s Windows](manage-user-device-linking-for-windows-pcs-with-microsoft-intune.md) – Vysvětluje, kdy a jak je nutné propojit uživatele s počítačem před nasazením softwaru uživateli.
- [Vyžádání a poskytnutí vzdálené pomoci na počítačích s Windows](request-and-provide-remote-assistance-for-windows-pcs-in-microsoft-intune.md) – Vysvětluje, jak můžete uživatelům počítačů s Intune poskytnout vzdálenou pomoc, a popisuje požadavky a instalaci softwaru TeamViewer.

Další informace o výše uvedených úkolech najdete v části, která se týká [běžných úloh správy počítače](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md).

## <a name="management-limitations-of-the-intune-client-software"></a>Omezení správy klientského softwaru Intune

Některé možnosti správy, které je možné použít ke správě počítačů PC jako mobilních zařízení, není možné použít u počítačů PC, které se spravují pomocí klientského softwaru Intune:

- Úplné vymazání (selektivní vymazání je k dispozici)
- Podmíněný přístup

Uvědomte si také, že v konzole správce Intune se některé části, jako například **Aktualizace**, **Ochrana** a **Licence**, zobrazí jen v případě, že jsou vaše zařízení zaregistrovaná pomocí klientského softwaru Intune.

  ![Položky konzoly správce, které se zobrazují pouze pro počítačového klienta](./media/manage-windows-pcs-with-microsoft-intune/admin-console-settings-only-for-pc-agent.png)

## <a name="help-with-troubleshooting"></a>Pomoc s odstraňováním problémů

Klientský software Intune obvykle běží tiše na pozadí a nevyžaduje skoro žádnou interakci ze strany uživatele ani řešení potíží. Pokud potřebujete vyřešit problémy týkající se správy počítačů PC, můžete si projít informace v protokolech. Klientský software Intune a odpovídající protokoly jsou nainstalované v adresáři %Program Files%\Microsoft\OnlineManagement.

Další informace o registraci zařízení pomocí Microsoft Intune najdete v článku o [registraci zařízení](../enrollment/device-enrollment.md).
