---
title: Použití šablon pro zařízení s Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Pomocí šablon pro správu v Microsoft Intune a Endpoint Manageru můžete vytvořit skupiny nastavení pro zařízení s Windows 10. Tato nastavení použijte v profilu konfigurace zařízení k řízení programů Office, Microsoft Edge, zabezpečení funkcí v Internet Exploreru, řízení přístupu k OneDrivu, použití funkcí vzdálené plochy, povolení automatického přehrání, nastavení řízení spotřeby, používání tisku HTTP, používání různých možností přihlašování uživatelů a řízení velikosti protokolu událostí.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f609ec62259deffb220c8ee935d0f10a98ae77b5
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254890"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>Pomocí šablon Windows 10 můžete nakonfigurovat nastavení zásad skupiny v Microsoft Intune

Při správě zařízení ve vaší organizaci chcete vytvořit skupiny nastavení, které se vztahují k různým skupinám zařízení. Máte například několik skupin zařízení. Pro skupinu a chcete přiřadit konkrétní sadu nastavení. Pro GroupB chcete přiřadit jinou sadu nastavení. Potřebujete také jednoduché zobrazení nastavení, která můžete konfigurovat.

Tuto úlohu můžete dokončit pomocí **šablony pro správu** v Microsoft Intune. Šablony pro správu obsahují stovky nastavení, která řídí funkce Microsoft Edge verze 77 a novější, Internet Explorer, systém Microsoft Office programů, Vzdálená plocha, OneDrive, hesla a PIN kódy a další. Tato nastavení umožňují správcům skupiny spravovat zásady skupiny pomocí cloudu.

Tato funkce platí pro:

- Windows 10 a novější

Nastavení Windows jsou podobná nastavení zásad skupiny (GPO) ve službě Active Directory (AD). Tato nastavení jsou integrovaná ve Windows a jsou [Nastavení založená na ADMX](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies) , která používají XML. Nastavení Office a Microsoft Edge jsou ingestovaná v ADMX a používají nastavení ADMX v [souborech šablon pro správu Office](https://www.microsoft.com/download/details.aspx?id=49030) a v [souborech šablon pro správu Microsoft Edge](https://www.microsoftedgeinsider.com/enterprise). A šablony Intune jsou 100% cloudu. Nabízí jednoduchý a přímo převedený způsob konfigurace nastavení a vyhledá požadovaná nastavení.

**Šablony pro správu** jsou integrované do Intune a nevyžadují žádné vlastní nastavení, včetně použití OMA-URI. Jako součást řešení pro správu mobilních zařízení (MDM) použijte při správě zařízení s Windows 10 Tato nastavení šablony jako zastávku.

Tento článek obsahuje seznam kroků pro vytvoření šablony pro zařízení s Windows 10 a ukazuje, jak filtrovat všechna dostupná nastavení v Intune. Když vytvoříte šablonu, vytvoří se profil konfigurace zařízení. Pak můžete tento profil přiřadit nebo nasadit do zařízení s Windows 10 ve vaší organizaci.

## <a name="before-you-begin"></a>Před zahájením

- Některá z těchto nastavení jsou k dispozici počínaje verzí Windows 10 1709 (RS2/Build 15063). Některá nastavení nejsou součástí všech edicí systému Windows. Pro dosažení co nejlepších výsledků se doporučuje používat Windows 10 Enterprise verze 1903 (19H1/Build 18362) a novější.

- Nastavení systému Windows používají [zprostředkovatele CSP v zásadách systému Windows](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies). Zprostředkovatelé CSP fungují na různých edicích Windows, jako jsou například Home, Professional, Enterprise atd. Pokud chcete zjistit, jestli zprostředkovatel kryptografických služeb funguje na konkrétní edici, přejděte na [Zásady Windows CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies).

## <a name="create-the-template"></a>Vytvoření šablony

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Konfigurace zařízení** > **profily** > konfigurace**vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **Windows 10 a novější**.
    - **Profil**: vyberte **šablony pro správu**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrý název profilu je například **Šablona správce: Šablona správce Windows 10, která konfiguruje nastavení XYZ v Microsoft Edge**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. V **nastavení konfigurace**nakonfigurujte nastavení, která se vztahují na zařízení (**Konfigurace počítače**), a nastavení, která se vztahují na uživatele **(konfigurace uživatele**):

    > [!div class="mx-imgBorder"]
    > ![Použití nastavení šablony ADMX pro uživatele a zařízení ve Správci služby Microsoft Intune Endpoint Manager](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. Když vyberete položku **Konfigurace počítače**, zobrazí se kategorie nastavení. Dostupná nastavení můžete zobrazit výběrem libovolné kategorie.

    Vyberte například položku **Konfigurace** > počítače**součásti** > systému Windows**Internet Explorer** , aby se zobrazila všechna nastavení zařízení, která platí pro Internet Explorer:

    > [!div class="mx-imgBorder"]
    > ![Zobrazit všechna nastavení zařízení, která platí pro Internet Explorer v Microsoft Intune Endpoint Manager](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

9. Můžete také vybrat **všechna nastavení** , aby se zobrazila všechna nastavení zařízení. Posuňte se dolů a použijte šipky před a další, abyste viděli další nastavení:

    > [!div class="mx-imgBorder"]
    > ![Podívejte se na vzorový seznam nastavení a použijte tlačítka předchozí a další.](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

10. Vyberte libovolné nastavení. Můžete například vyfiltrovat **sadu Office**a vybrat **Aktivovat prohlížení s omezeným přístupem**. Zobrazí se podrobný popis nastavení. Vyberte možnost **povoleno**, **zakázáno**nebo ponechat nastavení jako **Nenakonfigurováno** (výchozí). Podrobný popis také vysvětluje, co se stane, když vyberete možnost **povoleno**, **zakázáno**nebo **není nakonfigurováno**.

    > [!TIP]
    > Nastavení Windows v Intune se koreluje s cestou k místní zásadě skupiny, kterou vidíte v Editor místních zásad skupiny (`gpedit`).

11. Výběrem **OK** uložte změny.

    Přejděte do seznamu nastavení a nakonfigurujte požadovaná nastavení v prostředí. Zde je několik příkladů:

    - Pomocí nastavení pro **oznamování maker v jazyce VBA** můžete zpracovávat makra VBA v různých systém Microsoft Office programech, včetně Wordu a Excelu.
    - Pomocí nastavení **povolení stahování souborů** povolte nebo Zabraňte stažení z aplikace Internet Explorer.
    - Při **probuzení počítače (napájení ze sítě) použít příkaz vyžadovat heslo** , když se zařízení probudí z režimu spánku, vyzvat uživatele k zadání hesla.
    - Pomocí nastavení **Stáhnout nepodepsané ovládací prvky ActiveX** zabráníte uživatelům v Stahování nepodepsaných ovládacích prvků ActiveX z Internet Exploreru.
    - Pomocí nastavení **vypnout obnovení systému** povolíte nebo zabráníte uživatelům v zařízení spouštět obnovení systému.
    - Nastavení **povoluje Import oblíbených položek** použijte, když chcete uživatelům dovolit nebo zablokovat Import oblíbených položek z jiného prohlížeče do Microsoft Edge.
    - A mnohem víc...

12. Vyberte **Další**.
13. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo. `JohnGlenn_ITDepartment` Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](..//fundamentals/scope-tags.md).

    Vyberte **Další**.

14. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Pokud je profil přiřazen skupinám uživatelů, pak se nakonfigurovaná nastavení ADMX vztahují na všechna zařízení, která uživatel zapíše, a přihlásí se k nástroji. Pokud je profil přiřazený ke skupinám zařízení, pak se nakonfigurovaná nastavení ADMX použijí pro všechny uživatele, kteří se přihlásí do daného zařízení. K tomuto přiřazení dojde, pokud je nastavení ADMX nastaveno na konfigurace`HKEY_LOCAL_MACHINE`počítače () nebo na konfiguraci uživatele`HKEY_CURRENT_USER`(). U některých nastavení může mít nastavení počítače přiřazené uživateli vliv i na možnosti ostatních uživatelů v tomto zařízení.
    
    Další informace najdete v tématu [skupiny uživatelů a skupiny zařízení](device-profile-assign.md#user-groups-vs-device-groups).

    Vyberte **Další**.

15. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

Když zařízení příště zkontroluje aktualizace konfigurace, aplikuje se nastavení, která jste nakonfigurovali.

## <a name="find-some-settings"></a>Najít některá nastavení

V těchto šablonách jsou k dispozici stovky nastavení. Aby bylo snazší najít konkrétní nastavení, použijte integrované funkce:

- V šabloně pro řazení seznamu vyberte sloupce **Nastavení**, **stav**, **Typ nastavení**nebo **cesta** . Vyberte například sloupec **cesta** a pomocí šipky Další zobrazte nastavení v `Microsoft Excel` cestě:

- V šabloně vyhledejte konkrétní nastavení pomocí **vyhledávacího** pole. Můžete hledat podle nastavení nebo cesty. Například vyhledejte zprávu `copy`. Zobrazí se všechna nastavení `copy` s těmito možnostmi:

  > [!div class="mx-imgBorder"]
  > ![Vyhledat kopii pro zobrazení všech nastavení zařízení v šablonách pro správu v Intune](./media/administrative-templates-windows/search-copy-settings.png) 

  V jiném příkladu vyhledejte `microsoft word`. Zobrazí se nastavení, která můžete nastavit pro program Microsoft Word. Pokud `explorer` chcete zobrazit nastavení aplikace Internet Explorer, která můžete přidat do šablony, vyhledejte ji.

## <a name="next-steps"></a>Další kroky

Šablona je vytvořena, ale nemusí se ještě nic dělat. Dále [přiřaďte šablonu (označuje se také jako profil)](device-profile-assign.md) a [sledujte její stav](device-profile-monitor.md).

Aktualizujte [Office 365 pomocí šablon pro správu](administrative-templates-update-office.md).

[Kurz: použití cloudu ke konfiguraci zásad skupiny na zařízeních s Windows 10 s šablonami ADMX a Microsoft Intune](tutorial-walkthrough-administrative-templates.md)
