---
title: Správa zařízení pomocí zabezpečení koncového bodu v Microsoft Intune | Microsoft Docs
description: Přečtěte si, jak správci zabezpečení můžou pomocí uzlu zabezpečení koncového bodu (Endpoint Security) zobrazit zařízení a pracovat s nimi při jejich správě ve službě Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 8171eb3cf484c61e2b99046b36553a633d92044e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431245"
---
# <a name="manage-devices-with-endpoint-security-in-microsoft-intune"></a>Správa zařízení pomocí zabezpečení koncového bodu v Microsoft Intune

Jako správce zabezpečení můžete pomocí zobrazení *všechna zařízení* v centru pro správu Microsoft Endpoint Manageru zkontrolovat a reagovat na správu svých zařízení. Zobrazení zobrazuje seznam všech zařízení z Azure Active Directory (Azure AD). To zahrnuje zařízení spravovaná pomocí Intune, Configuration Manager a prostřednictvím [spolusprávy](https://docs.microsoft.com/configmgr/comanage/overview) pomocí intune i Configuration Manager. Zařízení můžou být v cloudu a z místní infrastruktury, pokud jsou integrovaná s Azure AD.

 Pokud chcete toto zobrazení najít, otevřete [Centrum pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte **zabezpečení koncového bodu**  >  **všechna zařízení**.

Úvodní zobrazení *všechna zařízení* zobrazuje vaše zařízení a obsahuje klíčové informace o každém z nich:

- Způsob správy zařízení
- Stav dodržování předpisů
- Podrobnosti o operačním systému
- Kdy se zařízení naposledy vrátilo
- A další

![Zobrazení všech zařízení v centru pro správu](./media/endpoint-security-manage-devices/all-device-view.png)

Při prohlížení podrobností o zařízení můžete pro další informace vybrat zařízení, na které chcete přejít.

## <a name="available-details-by-management-type"></a>Dostupné podrobnosti podle typu správy

Při zobrazování zařízení v centru pro správu Microsoft Endpoint Manageru zvažte, jak se zařízení spravuje. Zdroj správy má vliv na informace, které se zobrazí v centru pro správu a jaké akce jsou k dispozici pro správu zařízení.

Vezměte v úvahu následující pole:

- **Spravované podle** – tento sloupec identifikuje způsob správy zařízení. Možnosti spravované pomocí zahrnují:

  - **MDM** – tato zařízení se spravují přes Intune. Intune shromažďuje a hlásí data o dodržování předpisů do centra pro správu.

  - **ConfigMgr** – tato zařízení se zobrazí v centru pro správu Microsoft Endpoint Manageru, když pomocí možnosti *připojit klienta* přidáte zařízení, která spravujete pomocí nástroje Configuration Manager. Aby bylo možné zařízení spravovat, musí spustit klienta Configuration Manager a být:

    - V pracovní skupině (připojené k AAD a jinak)
    - Připojeno k doméně
    - Připojené k hybridnímu AAD (připojeno k AD a AAD)

    Stav dodržování předpisů pro zařízení, která jsou spravovaná nástrojem Configuration Manager, není zobrazený v centru pro správu Microsoft Endpoint Manageru.

    Další informace najdete v tématu [Povolení připojení klienta](https://docs.microsoft.com/configmgr/tenant-attach/device-sync-actions) v dokumentaci k Configuration Manager.

  - **Agent MDM/ConfigMgr** – tato zařízení jsou spoluspravována mezi Intune a Configuration Manager.

    Díky spolusprávě můžete [zvolit různé úlohy spolusprávy](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) , abyste zjistili, jaké aspekty jsou spravované Configuration Manager nebo Intune. Tyto možnosti budou mít vliv na to, které zásady zařízení použije a jak budou data o dodržování předpisů hlášena v centru pro správu.

    Pomocí Intune můžete například nakonfigurovat zásady pro antivirovou ochranu, bránu firewall a šifrování. Tyto typy zásad se považují za zásady pro *Endpoint Protection*. Pokud chcete, aby spoluspravované zařízení používalo zásady Intune a ne zásady Configuration Manager, nastavte pro Endpoint Protection posuvník pro spolusprávu na *Intune* nebo *pilotní Intune*. Pokud je posuvník nastavený na Configuration Manager, zařízení místo toho použije zásady a nastavení z Configuration Manager.

- **Dodržování předpisů**: dodržování předpisů se vyhodnocuje na základě zásad dodržování předpisů, které jsou přiřazené k zařízení. Zdroj těchto zásad a informace v konzole nástroje závisí na tom, jak je zařízení spravované. Intune, Configuration Manager nebo spoluspráva. Pro spoluspravovaná zařízení pro nahlášení dodržování předpisů nastavte posuvník spolusprávy pro dodržování předpisů zařízením pro Intune nebo pilotní Intune.  

  Po hlášení kompatibility do centra pro správu zařízení můžete přejít k podrobnostem a zobrazit další podrobnosti. Pokud zařízení nedodržuje předpisy, přejděte k podrobnostem o tom, které zásady nejsou kompatibilní. Tyto informace vám pomohou při zkoumání a usnadnění dodržování předpisů pro zařízení.

- **Poslední vrácení se změnami**: Toto pole označuje poslední čas, kdy zařízení nahlásilo svůj stav.

## <a name="review-a-devices-policy"></a>Kontrola zásad zařízení

Při prohlížení seznamu zařízení můžete vybrat zařízení, pro které chcete přejít na Další informace, a to tak, že otevřete stránku *Přehled* tohoto zařízení.

Na stránce Přehled zařízení můžete vybrat možnost **Konfigurace zabezpečení koncového bodu** a zobrazit zásady zabezpečení koncového bodu, které se vztahují k danému zařízení. Podrobnosti o zásadách jsou k dispozici pro zařízení spravovaná MDM a Intune.

![Zobrazit podrobnosti zásad zabezpečení Endpoint](./media/endpoint-security-manage-devices/view-policy-details.png)

Zařízení, která jsou spravovaná nástrojem Configuration Manager, nezobrazují podrobnosti zásad. Chcete-li zobrazit další informace o těchto zařízeních, použijte konzolu Configuration Manager.

## <a name="remote-actions-for-devices"></a>Vzdálené akce pro zařízení

Vzdálené akce jsou akce, které můžete spustit nebo použít na zařízení z centra pro správu Microsoft Endpoint Manageru. Když si zobrazíte podrobnosti o zařízení, můžete získat přístup ke vzdáleným akcím, které se vztahují k zařízení.

Vzdálené akce se zobrazí v horní části stránky s *přehledem* zařízení. Akce, které nelze zobrazit z důvodu omezeného místa na obrazovce, jsou k dispozici výběrem tří teček na pravé straně:

![Zobrazit další akce](./media/endpoint-security-manage-devices/view-additional-actions.png)

Vzdálené akce, které jsou k dispozici, závisí na způsobu správy zařízení:

- **Intune**: k dispozici jsou všechny [vzdálené akce Intune](../remote-actions/device-management.md) , které se vztahují k platformě zařízení.  
- **Configuration Manager**: můžete použít následující akce Configuration Manager:

  - Synchronizovat zásady počítače
  - Synchronizovat zásady uživatele
  - Cyklus hodnocení aplikace

- **Spoluspráva**: můžete přistupovat ke vzdáleným i Configuration Managerm akcím Intune.

Některé ze vzdálených akcí Intune můžou přispět k zabezpečení zařízení nebo k ochraně dat, která se na zařízení můžou nacházet. Pomocí vzdálených akcí můžete:

- Uzamčení zařízení
- Resetování zařízení
- Odebrání firemních dat
- Vyhledávání malwaru mimo plánované spuštění
- Otočení klíčů BitLockeru

Následující vzdálené akce Intune jsou důležité pro správce zabezpečení a jsou podmnožinou [úplného seznamu](../remote-actions/device-inventory.md#view-the-device-details). Ne všechny akce jsou k dispozici pro všechny platformy zařízení. Odkazy odkazují na obsah, který poskytuje podrobné informace o každé akci.

- [Synchronizovat zařízení](../remote-actions/device-sync.md) – zařízení se hned zaregistruje v Intune. Když se zařízení zablokuje, obdrží všechny nevyřízené akce nebo zásady, které mu byly přiřazeny.  

- [Restart](../remote-actions/device-restart.md) – vynutí restartování zařízení s Windows 10 během pěti minut. Vlastník zařízení nebude automaticky upozorňován na restartování a může ztratit práci.

- [Rychlé prověřování](../configuration/device-restrictions-windows-10.md) – program Defender spustí rychlou kontrolu zařízení pro malware a pak výsledky odešle do Intune. Rychlá kontrola vypadá na běžných místech, kde by mohlo být zaregistrované malware, jako jsou klíče registru a známé spouštěcí složky Windows.

- [Úplná kontrola](../configuration/device-restrictions-windows-10.md) – program Defender spustil kontrolu zařízení pro malware a pak výsledky odešle do Intune. Úplná kontrola vypadá na běžných místech, kde by mohlo být zaregistrované malware, a také kontroluje všechny soubory a složky v zařízení.

- Aktualizace funkce Security Intelligence v programu Windows Defender – zařízení aktualizuje definice malwaru pro antivirovou ochranu v programu Microsoft Defender. Tato akce nespustí kontrolu.

- [Střídání klíčů BitLockeru](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key) – vzdáleně otočte obnovovací klíč BitLockeru zařízení s Windows 10 verze 1909 nebo novějším.

**Akce hromadných zařízení** můžete použít také ke správě některých akcí, jako je *vyřazení* a *vymazání* pro více zařízení současně. [Hromadné akce](../remote-actions/bulk-device-actions.md) jsou k dispozici v zobrazení *všechna zařízení* . Vyberete platformu, akci a pak zadáte až 100 zařízení.

![Vybrat hromadné akce](./media/endpoint-security-manage-devices/select-bulk-actions.png)

Možnosti, které spravujete pro zařízení, se neprojeví, dokud se zařízení nevrátí se službou Intune.

## <a name="next-steps"></a>Další kroky

[Správa zabezpečení koncových bodů v Intune](../protect/endpoint-security.md)