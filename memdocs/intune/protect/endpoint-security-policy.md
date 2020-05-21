---
title: Správa zásad zabezpečení koncového bodu v Microsoft Intune | Microsoft Docs
description: Přečtěte si, jak správci zabezpečení můžou pomocí zásad zabezpečení koncového bodu a profilů Zaměřte se na konfiguraci zabezpečení zařízení ve službě Microsoft Endpoint Manager.
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
ms.openlocfilehash: 0e6a1f30d482e4811e02a8166e87aca4d1f23207
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431281"
---
# <a name="manage-device-security-with-endpoint-security-policies-in-microsoft-intune"></a>Správa zabezpečení zařízení pomocí zásad zabezpečení Endpoint v Microsoft Intune

Jako správce zabezpečení můžete pomocí zásad zabezpečení v rámci *zabezpečení* služby Intune nakonfigurovat zabezpečení zařízení bez režie navigace nad větším textem a rozsahem nastavení nalezených v konfiguračních profilech zařízení a v standardních hodnotách zabezpečení.

Každý typ zásad podporuje jeden nebo více profilů. Profily jsou místo, kde konfigurujete nastavení a můžete seskupovat nastavení pro různé platformy, nebo pro různé oblasti soustředění v oblasti větší zásady.

Tyto zásady najdete v části *Správa* v uzlu **Security Endpoint** v [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

![Správa zásad](./media/endpoint-security-policy/endpoint-security-policies.png)

Níže najdete stručný popis každého typu zásad zabezpečení koncového bodu. Pokud se o nich chcete dozvědět víc, včetně dostupných profilů pro každou z nich, postupujte podle odkazů na obsah vyhrazený pro jednotlivé typy zásad:

- [Antivirová](../protect/endpoint-security-antivirus-policy.md) ochrana – zásady antivirové ochrany se zaměřují na správu diskrétní skupiny nastavení antivirové ochrany pro spravovaná zařízení. Pokud chcete používat zásady antivirové ochrany, Integrujte Intune s pokročilou ochranou před internetovými útoky v programu Microsoft Defender jako řešení ochrany před mobilními hrozbami.

- [Šifrování disku](../protect/endpoint-security-disk-encryption-policy.md) – profily šifrování disku Endpoint Security se zaměřují jenom na nastavení, která jsou relevantní pro vestavěnou metodu šifrování zařízení, jako je trezor úložiště nebo BitLocker. Díky tomuto zaměření můžou správci zabezpečení spravovat nastavení šifrování disků bez nutnosti přecházet na hostitele nesouvisejícího nastavení.

- [Brána firewall](../protect/endpoint-security-firewall-policy.md) – pomocí zásad brány firewall zabezpečení koncového bodu v Intune můžete nakonfigurovat vestavěnou bránu firewall pro zařízení, která používají MacOS a Windows 10. Mezi integrované brány firewall patří BitLocker pro zařízení s Windows a trezor pro macOS.

- [Detekce a reakce koncového bodu](../protect/endpoint-security-edr-policy.md) – při integraci služby Defender ATP s Intune použijte zásady zabezpečení koncového bodu pro zjišťování koncových bodů a odpověď (EDR) ke správě nastavení EDR a připojení zařízení ke službě Defender atp.

- [Omezení možností útoku](../protect/endpoint-security-asr-policy.md) – když se antivirová ochrana používá v zařízeních s Windows 10, použijte zásady zabezpečení koncového bodu služby Intune, abyste mohli spravovat tato nastavení pro vaše zařízení.

- [Ochrana účtů](../protect/endpoint-security-account-protection-policy.md) – zásady ochrany účtů vám pomůžou chránit identitu a účty vašich uživatelů. Zásady ochrany účtů se zaměřují na nastavení pro Windows Hello a Credential Guard, které je součástí správy identit a přístupu Windows.

Následující části se vztahují na všechny zásady zabezpečení koncového bodu.

## <a name="create-an-endpoint-security-policy"></a>Vytvoření zásady zabezpečení koncového bodu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte možnost **zabezpečení koncového bodu** a pak vyberte typ zásady, kterou chcete nakonfigurovat, a pak vyberte **vytvořit zásadu**. Vyberte si z následujících typů zásad:
   - Antivirus
   - Šifrování disků
   - Firewall
   - Zjišťování koncových bodů a odpověď
   - Omezení možností útoku
   - Ochrana účtu

3. Zadejte tyto vlastnosti:
   - **Platforma**: vyberte platformu, pro kterou vytváříte zásady. Dostupné možnosti závisí na zvoleném typu zásady:
     - macOS
     - Windows 10 a novější
   - **Profil**: vyberte z dostupných profilů pro vybranou platformu. Informace o profilech najdete v části vyhrazeno v tomto článku pro zvolený typ zásad.

4. Vyberte **Vytvořit**.

5. Na stránce **základy** zadejte název a popis profilu a pak klikněte na tlačítko **Další**.

6. Na stránce **nastavení konfigurace** rozbalte každou skupinu nastavení a nakonfigurujte nastavení, která chcete spravovat pomocí tohoto profilu.

   Po dokončení konfigurace nastavení vyberte **Další**.

7. Na stránce **značky oboru** zvolte **možnost vybrat značky oboru** a otevřete tak podokno *Vybrat značky* , abyste přiřadili značky oboru k profilu.
  
   Pokračujte výběrem tlačítka **Next** (Další).

8. Na stránce **přiřazení** vyberte skupiny, které získají tento profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](../configuration/device-profile-assign.md).

   Vyberte **Další**.

9. Po dokončení na stránce **Revize + vytvořit** klikněte na **vytvořit**. Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

## <a name="duplicate-a-policy"></a>Duplikace zásady

Zásady zabezpečení koncového bodu podporují duplikaci, aby se vytvořila kopie původních zásad. Scénář odstraňování duplicitních zásad je užitečný, pokud potřebujete přiřadit podobné zásady různým skupinám, ale nechcete ručně znovu vytvořit celou zásadu. Místo toho můžete duplikovat původní zásady a potom zavádět pouze změny, které vyžadují nové zásady. Můžete změnit jenom konkrétní nastavení a skupinu, ke které je zásada přiřazená.

Při vytváření duplicitního názvu přiřadíte kopii nový název. Kopie se vytvoří se stejnou konfigurací nastavení a značkami oboru jako původní, ale nebude mít žádné přiřazení. Nové zásady budete muset později upravit a vytvořit přiřazení.  

Duplicity podporují následující typy zásad:

- Antivirus
- Šifrování disků
- Firewall
- Zjišťování koncových bodů a odpověď
- Omezení možností útoku
- Ochrana účtu

Když vytvoříte novou zásadu, zkontrolujte a upravte zásady, aby se změny konfigurace projevily.

### <a name="to-duplicate-a-policy"></a>Duplikace zásady

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte zásadu, kterou chcete zkopírovat. V dalším kroku vyberte **Duplikovat** nebo vyberte tři tečky (**...**) napravo od zásady a vyberte **Duplikovat**.
3. Zadejte **nový název** zásady a potom vyberte **Uložit**.

### <a name="to-edit-a-policy"></a>Postup úpravy zásady

1. Vyberte novou zásadu a pak vyberte **vlastnosti**.
2. Vyberte nastavení a rozbalte seznam nastavení konfigurace v zásadách. Nastavení z tohoto zobrazení nemůžete změnit, ale můžete zkontrolovat, jak jsou nakonfigurované.
3. Chcete-li upravit zásadu, vyberte možnost **Upravit** pro každou kategorii, u které chcete provést změnu:
   - Základy
   - Přiřazení
   - Značky oboru
   - Nastavení konfigurace
4. Až změny provedete, vyberte **Uložit** a uložte provedené úpravy.  Aby bylo možné zavést úpravy dalších kategorií, je třeba uložit úpravy jedné kategorie.

## <a name="manage-conflicts"></a>Správa konfliktů

Mnohé z nastavení zařízení, která můžete spravovat pomocí zásad zabezpečení koncového bodu (zásady zabezpečení), můžete spravovat prostřednictvím dalších typů zásad v Intune. Mezi tyto typy zásad patří zásady *Konfigurace zařízení* a *směrné plány zabezpečení*. Vzhledem k tomu, že můžete spravovat nastavení s několika různými typy zásad nebo několika instancemi stejného typu zásad, je nutné, aby bylo možné identifikovat a vyřešit konflikty zásad v případě, že zařízení nedodržuje očekávané konfigurace.

- Standardní hodnoty zabezpečení můžou nastavit nevýchozí hodnotu nastavení tak, aby odpovídala Doporučené konfiguraci, kterou základní adresy používají.
- Další typy zásad, včetně zásad zabezpečení koncového bodu, nastavují hodnotu není ve výchozím nastavení *nakonfigurované* . Tyto další typy zásad vyžadují, abyste v zásadě explicitně nakonfigurovali nastavení.

Bez ohledu na metodu zásad, která spravuje stejné nastavení na stejném zařízení prostřednictvím více typů zásad, nebo přes více instancí stejného typu zásad může dojít ke konfliktům, které by se měly vyhnout.

Informace na následujících odkazech vám pomůžou identifikovat a vyřešit konflikty:

- [Řešení potíží se zásadami a profily v Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Monitorování standardních hodnot zabezpečení](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Další kroky

[Správa zabezpečení koncových bodů v Intune](../protect/endpoint-security.md)
