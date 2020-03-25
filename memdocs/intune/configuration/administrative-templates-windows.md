---
title: Použití šablon pro zařízení s Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Pomocí šablon pro správu v Microsoft Intune a Endpoint Manageru můžete vytvořit skupiny nastavení pro zařízení s Windows 10. Tato nastavení použijte v profilu konfigurace zařízení k řízení programů Office, Microsoft Edge, zabezpečení funkcí v Internet Exploreru, řízení přístupu k OneDrivu, použití funkcí vzdálené plochy, povolení automatického přehrání, nastavení řízení spotřeby, používání HTTP tisku. můžete použít různé možnosti přihlašování uživatelů a řídit velikost protokolu událostí.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/23/2020
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
ms.openlocfilehash: 75ef2a03c9f42f0bda78af009f0fb563fbcedb75
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220005"
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

- Některá z těchto nastavení jsou k dispozici počínaje verzí Windows 10 1703 (RS2/Build 15063). Některá nastavení nejsou součástí všech edicí systému Windows. Pro dosažení co nejlepších výsledků se doporučuje používat Windows 10 Enterprise verze 1903 (19H1/Build 18362) a novější.

- Nastavení systému Windows používají [zprostředkovatele CSP v zásadách systému Windows](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies). Zprostředkovatelé CSP fungují na různých edicích Windows, jako jsou například Home, Professional, Enterprise atd. Pokud chcete zjistit, jestli zprostředkovatel kryptografických služeb funguje na konkrétní edici, přejděte na [Zásady Windows CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies).

## <a name="create-the-template"></a>Vytvoření šablony

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující vlastnosti:

    - **Platforma**: vyberte **Windows 10 a novější**.
    - **Profil**: vyberte **šablony pro správu**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrý název profilu je například **Šablona správce: Šablona správce Windows 10, která konfiguruje nastavení XYZ v Microsoft Edge**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. V **nastavení konfigurace**nakonfigurujte nastavení, která se vztahují na zařízení (**Konfigurace počítače**), a nastavení, která se vztahují na uživatele **(konfigurace uživatele**):

    > [!div class="mx-imgBorder"]
    > ![použít nastavení šablony ADMX pro uživatele a zařízení ve Správci služby Microsoft Intune Endpoint](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. Když vyberete položku **Konfigurace počítače**, zobrazí se kategorie nastavení. Dostupná nastavení můžete zobrazit výběrem libovolné kategorie.

    Vyberte například položku **Konfigurace počítače** > **součásti systému Windows** > **Internet Explorer** , aby se zobrazila všechna nastavení zařízení, která platí pro Internet Explorer:

    > [!div class="mx-imgBorder"]
    > ![Zobrazit všechna nastavení zařízení, která se vztahují na Internet Explorer v Microsoft Intune Endpoint Manageru](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

9. Můžete také vybrat **všechna nastavení** , aby se zobrazila všechna nastavení zařízení. Posuňte se dolů a použijte šipky před a další, abyste viděli další nastavení:

    > [!div class="mx-imgBorder"]
    > ![se zobrazí ukázkový seznam nastavení a použití tlačítek předchozí a další](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

10. Vyberte libovolné nastavení. Můžete například vyfiltrovat **sadu Office**a vybrat **Aktivovat prohlížení s omezeným přístupem**. Zobrazí se podrobný popis nastavení. Vyberte možnost **povoleno**, **zakázáno**nebo ponechat nastavení jako **Nenakonfigurováno** (výchozí). Podrobný popis také vysvětluje, co se stane, když vyberete možnost **povoleno**, **zakázáno**nebo **není nakonfigurováno**.

    > [!TIP]
    > Nastavení Windows v Intune se koreluje s cestou k místní zásadě skupiny, kterou vidíte v Editor místních zásad skupiny (`gpedit`).

11. Výběrem **OK** uložte změny.

    Přejděte do seznamu nastavení a nakonfigurujte požadovaná nastavení v prostředí. Následuje několik příkladů:

    - Pomocí nastavení pro **oznamování maker v jazyce VBA** můžete zpracovávat makra VBA v různých systém Microsoft Office programech, včetně Wordu a Excelu.
    - Pomocí nastavení **povolení stahování souborů** povolte nebo Zabraňte stažení z aplikace Internet Explorer.
    - Při **probuzení počítače (napájení ze sítě) použít příkaz vyžadovat heslo** , když se zařízení probudí z režimu spánku, vyzvat uživatele k zadání hesla.
    - Pomocí nastavení **Stáhnout nepodepsané ovládací prvky ActiveX** zabráníte uživatelům v Stahování nepodepsaných ovládacích prvků ActiveX z Internet Exploreru.
    - Pomocí nastavení **vypnout obnovení systému** povolíte nebo zabráníte uživatelům v zařízení spouštět obnovení systému.
    - Nastavení **povoluje Import oblíbených položek** použijte, když chcete uživatelům dovolit nebo zablokovat Import oblíbených položek z jiného prohlížeče do Microsoft Edge.
    - A další funkce...

12. Vyberte **Další**.
13. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu na konkrétní skupiny IT, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment`. Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](..//fundamentals/scope-tags.md).

    Vyberte **Další**.

14. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

15. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

Když zařízení příště zkontroluje aktualizace konfigurace, aplikuje se nastavení, která jste nakonfigurovali.

## <a name="find-some-settings"></a>Najít některá nastavení

V těchto šablonách jsou k dispozici stovky nastavení. Aby bylo snazší najít konkrétní nastavení, použijte integrované funkce:

- V šabloně pro řazení seznamu vyberte sloupce **Nastavení**, **stav**, **Typ nastavení**nebo **cesta** . Vyberte například sloupec **cesta** a pomocí šipky Další zobrazte nastavení v cestě `Microsoft Excel`:

- V šabloně vyhledejte konkrétní nastavení pomocí **vyhledávacího** pole. Můžete hledat podle nastavení nebo cesty. Například vyhledejte zprávu `copy`. Zobrazí se všechna nastavení s `copy`:

  > [!div class="mx-imgBorder"]
  > ![vyhledat kopii a zobrazit všechna nastavení zařízení v šablonách pro správu v Intune](./media/administrative-templates-windows/search-copy-settings.png) 

  V jiném příkladu vyhledejte `microsoft word`. Zobrazí se nastavení, která můžete nastavit pro program Microsoft Word. Vyhledejte `explorer` pro zobrazení nastavení aplikace Internet Explorer, která můžete přidat do šablony.

## <a name="next-steps"></a>Další kroky

Šablona je vytvořena, ale nemusí se ještě nic dělat. Dále [přiřaďte šablonu (označuje se také jako profil)](device-profile-assign.md) a [sledujte její stav](device-profile-monitor.md).

Aktualizujte [Office 365 pomocí šablon pro správu](administrative-templates-update-office.md).

[Kurz: použití cloudu ke konfiguraci zásad skupiny na zařízeních s Windows 10 s šablonami ADMX a Microsoft Intune](tutorial-walkthrough-administrative-templates.md)
