---
title: Přiřazení profilů zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Pomocí centra pro správu Microsoft Endpoint Manageru můžete uživatelům a zařízením přiřadit profily a zásady zařízení. Přečtěte si, jak vyloučit skupiny z přiřazení profilu v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f6f5414d-0e41-42fc-b6cf-e7ad76e1e06d
ms.reviewer: altsou
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55835d5ee8527f54e530da5113f841ed108fa6f5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915802"
---
# <a name="assign-user-and-device-profiles-in-microsoft-intune"></a>Přiřazení profilů uživatelů a zařízení v Microsoft Intune

Vytvoříte profil a zahrnete do něj všechna nastavení, která jste zadali. V dalším kroku nasadíte nebo přiřadíte profil pro skupiny uživatelů nebo zařízení. Po přiřazení uživatelé a zařízení obdrží váš profil a nastavení, které jste zadali, se použije.

V tomto článku se dozvíte, jak přiřadit profil, a obsahuje některé informace o použití značek oboru v profilech.

> [!NOTE]  
> Když je profil odebraný nebo už není přiřazený k zařízení, může dojít k různým akcím v závislosti na nastavení v profilu. Nastavení jsou založená na zprostředkovatelích CSP a každý CSP může docházet k odstranění profilu odlišně. Nastavení může například zachovat existující hodnotu a nevracet se zpět na výchozí hodnotu. Chování řídí každý CSP v operačním systému. Seznam zprostředkovatelů kryptografických služeb systému Windows najdete v [referenčních informacích k poskytovateli CSP (Configuration Service Provider)](/windows/client-management/mdm/configuration-service-provider-reference).
>
> Pokud chcete změnit nastavení na jinou hodnotu, vytvořte nový profil, nakonfigurujte nastavení na **Nenakonfigurováno**a přiřaďte profil. Po použití na zařízení by uživatelé měli mít kontrolu nad tím, aby nastavení změnili na upřednostňovanou hodnotu.
>
> Při konfiguraci těchto nastavení doporučujeme nasazení do pilotní skupiny. Další Rady k zavedení Intune najdete v tématu [Vytvoření plánu zavedení](../fundamentals/planning-guide-rollout-plan.md).

## <a name="before-you-begin"></a>Než začnete

Ujistěte se, že máte správnou roli pro přiřazování profilů. Další informace najdete v tématu [řízení přístupu na základě role (RBAC) pomocí Microsoft Intune](../fundamentals/role-based-access-control.md).

## <a name="assign-a-device-profile"></a>Přiřazení profilu zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**možnost  >  **profily konfigurace**zařízení. Zobrazí se všechny profily.
3. Vyberte profil, který chcete přiřadit > **vlastností**  >  **přiřazení**  >  **Edit**:

    :::image type="content" source="./media/device-profile-assign/properties-select-assignments.png" alt-text="Vyberte přiřazení a nasaďte profil pro uživatele a skupiny v Microsoft Intune a ve Správci koncových bodů.":::

4. Vyberte **zahrnuté skupiny** nebo **Vyloučené skupiny**a pak zvolte **Vybrat skupiny, které chcete zahrnout**. Když skupiny vybíráte, zvolíte skupinu Azure AD. Pokud chcete vybrat více skupin, podržte stisknutou klávesu **CTRL** a vyberte vaše skupiny.

    :::image type="content" source="./media/device-profile-assign/select-included-excluded-groups-profile-assignment.png" alt-text="Zahrnutí nebo vyloučení uživatelů a skupin při přiřazování nebo nasazování profilu v Microsoft Intune a v nástroji Endpoint Manager.":::

5. Vyberte **zkontrolovat a uložit**. Tento krok nepřiřazuje váš profil.
6. Vyberte **Uložit**. Když uložíte, váš profil se přiřadí. Vaše skupiny obdrží nastavení vašeho profilu, když se zařízení zaregistrují ve službě Intune.

## <a name="use-scope-tags-or-applicability-rules"></a>Použití značek oboru nebo pravidel použitelnosti

Když vytváříte nebo aktualizujete profil, můžete do profilu přidat také značky oboru a pravidla použitelnosti.

**Značky oboru** jsou skvělým způsobem, jak filtrovat profily na konkrétní skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . [Pro distribuci použijte značky RBAC a Scope](../fundamentals/scope-tags.md) s více informacemi.

Na zařízeních s Windows 10 můžete přidat **pravidla použitelnosti** , aby se profil mohl vztahovat jenom na konkrétní verzi operačního systému nebo na konkrétní edici Windows. [Pravidla použitelnosti](device-profile-create.md#applicability-rules) obsahují další informace.

## <a name="user-groups-vs-device-groups"></a>Skupiny uživatelů a skupiny zařízení

Mnoho uživatelů požaduje používání skupin uživatelů a kdy používat skupiny zařízení. Odpověď závisí na vašem cíli. Tady jsou některé doprovodné materiály, které vám pomohou začít.

### <a name="device-groups"></a>skupiny zařízení.

Pokud chcete použít nastavení na zařízení bez ohledu na to, kdo je přihlášený, přiřaďte své profily ke skupině zařízení. Nastavení použitá pro skupiny zařízení vždy přecházejí na zařízení, nikoli na uživatele.

Příklad:

- Skupiny zařízení jsou užitečné ke správě zařízení, která nemají vyhrazeného uživatele. Máte například zařízení, která tisknou lístky, prohledává inventář, sdílí pracovní procesy, jsou přiřazeny k určitému skladu atd. Vložte tato zařízení do skupiny zařízení a přiřaďte své profily k této skupině zařízení.

- Vytvoříte [profil Intune rozhraní DFCI (Device firmware Configuration Interface)](device-firmware-configuration-interface-windows.md) , který aktualizuje nastavení v systému BIOS. Například můžete nakonfigurovat tento profil, který zakáže fotoaparát zařízení, nebo uzamknout možnosti spouštění, aby uživatelé nemohli spustit jiný operační systém. Tento profil je dobrým scénářem, který se má přiřadit ke skupině zařízení.

- Na některých specifických zařízeních s Windows vždycky chcete řídit některá nastavení Microsoft Edge bez ohledu na to, kdo zařízení používá. Například chcete blokovat všechna stahování, omezit všechny soubory cookie na aktuální relaci procházení a odstranit historii procházení. V tomto scénáři vložte tato konkrétní zařízení s Windows do skupiny zařízení. Pak vytvořte [v Intune šablonu pro správu](administrative-templates-windows.md), přidejte tato nastavení zařízení a přiřaďte tento profil ke skupině zařízení.

Pokud si nejste vědomi, kdo se k zařízení přihlásil, nebo když se někdo přihlásí, můžete ho vytvořit pomocí skupin zařízení. Přejete si, aby na zařízení byla vždycky tato nastavení.

### <a name="user-groups"></a>Skupiny uživatelů

Nastavení profilu použité pro skupiny uživatelů vždycky přejdou na uživatele a při přihlášení ke svému množství zařízení se dostanete k uživateli. Pro uživatele je běžné mít mnoho zařízení, jako je například Surface pro práci, a osobní zařízení s iOS/iPadOS. A je normální pro uživatele, kteří mají přístup k e-mailu a jiným prostředkům organizace z těchto zařízení.

Použijte toto obecné pravidlo: Pokud funkce patří uživateli, například e-mailem nebo uživatelským certifikátům, přiřaďte jim skupiny uživatelů.

Příklad:

- Chcete umístit ikonu helpdesku pro všechny uživatele na všech svých zařízeních. V tomto scénáři vložte tyto uživatele do skupiny uživatelů a přiřaďte k této skupině uživatelů profil ikony helpdesku.
- Uživatel dostane nové zařízení vlastněné organizací. Uživatel se k zařízení přihlásí pomocí svého doménového účtu. Zařízení se automaticky zaregistruje ve službě Azure AD a automaticky se spravuje přes Intune. Tento profil je dobrým scénářem, který se přiřadí skupině uživatelů.
- Pokaždé, když se uživatel přihlásí k zařízení, budete chtít ovládat funkce v aplikacích, jako je třeba OneDrive nebo Office. V tomto scénáři přiřaďte nastavení profilu OneDrive nebo Office ke skupině uživatelů.

  Například chcete v aplikacích Office zablokovat nedůvěryhodné ovládací prvky ActiveX. [V Intune můžete vytvořit šablonu pro správu](administrative-templates-windows.md), nakonfigurovat toto nastavení a potom tento profil přiřadit skupině uživatelů.

Chcete-li vytvořit souhrn, použijte skupiny uživatelů, pokud chcete, aby nastavení a pravidla vždy přešly k uživateli bez ohledu na to, jaké zařízení používají.

## <a name="exclude-groups-from-a-profile-assignment"></a>Vyloučení skupin z přiřazení profilu

Profily konfigurace zařízení v Intune umožňují zahrnout a vyloučit skupiny z přiřazení profilu.

Osvědčeným postupem je vytvořit a přiřadit profily konkrétně pro vaše skupiny uživatelů. A vytvořte a přiřaďte různé profily konkrétně pro vaše skupiny zařízení. Další informace o skupinách najdete v tématu [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md).

Když přiřadíte profily, použijte následující tabulku při zahrnutí a vyloučení skupin. Značka zaškrtnutí znamená, že je přiřazení podporováno:

:::image type="content" source="./media/device-profile-assign/include-exclude-user-device-groups.png" alt-text="Podporované možnosti zahrnují nebo vylučují skupiny z přiřazení profilu.":::

### <a name="what-you-should-know"></a>Co byste měli vědět

- Vyloučení má přednost před zahrnutím do následujících scénářů stejného typu skupiny:

  - Zahrnutí skupin uživatelů a vyloučení skupin uživatelů
  - Zahrnutí skupin zařízení a vyloučení skupiny zařízení

  Například přiřadíte profil zařízení skupině uživatelů **Všichni firemní uživatelé** , ale vyloučíte členy ve skupině uživatelů **správce vyšších zaměstnanců** . Vzhledem k tomu, že obě skupiny jsou skupiny uživatelů, získá profil **Všichni firemní uživatelé** s výjimkou **pracovníků hlavní správy** .

- Intune nevyhodnocuje vztahy mezi uživateli a zařízeními. Pokud přiřadíte profily ke smíšeným skupinám, výsledky nemusí být to, co chcete, nebo očekávat.

  Například přiřadíte profil zařízení skupině uživatelů **Všichni uživatelé** , ale vyloučíte skupinu zařízení **všechna osobní zařízení** . V tomto přiřazení profilu smíšené skupiny získají **Všichni uživatelé** profil. Vyloučení nelze použít.

  V důsledku toho se nedoporučuje přiřazovat profily ke smíšeným skupinám.

## <a name="next-steps"></a>Další kroky

Pokyny k monitorování profilů a zařízení, ve kterých jsou spuštěny vaše profily, najdete v tématu [monitorování profilů zařízení](device-profile-monitor.md) .