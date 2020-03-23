---
title: Vytvoření zásad ochrany aplikací ochrany před mobilními hrozbami (MTD) v Intune
titleSuffix: Microsoft Intune
description: Vytvořte zásady ochrany aplikací ochrany před mobilními hrozbami (MTD) pomocí Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0fc25aa915762e0e1df9446c9fb14513bdf20352
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329163"
---
# <a name="create-mobile-threat-defense-app-protection-policy-with-intune"></a>Vytvoření zásad ochrany aplikací ochrany před mobilními hrozbami v Intune

Intune s ochranou před mobilními hrozbami (MTD) pomáhá detekovat hrozby a hodnotit rizika na mobilních zařízeních. Můžete vytvořit zásady ochrany aplikací Intune, které posuzují riziko, aby bylo možné zjistit, jestli má zařízení povolený přístup k podnikovým datům.

> [!NOTE]
> Tento článek se týká všech partnerů ochrany před mobilními hrozbami, které podporují zásady ochrany aplikací:
>
> - Lepší mobilní zařízení (Android, iOS/iPadOS)
> - Zimperium (Android, iOS/iPadOS)
> - Lookout for Work (Android, iOS/iPadOS).

## <a name="before-you-begin"></a>Před zahájením

V rámci nastavení ochrany před mobilními hrozbami (MTD) jste v konzole partnera MTD vytvořili zásadu, která klasifikuje různé hrozby jako vysoké, střední nebo nízké. V zásadách ochrany aplikací Intune je teď potřeba nastavit úroveň ochrany před mobilními hrozbami.

Předpoklady pro zásady ochrany aplikací pomocí MTD:

- Nastavte integraci MTD s Intune. Bez této integrace nebudou zásady ochrany aplikací MTD nijak ovlivněny.

## <a name="to-create-an-mtd-app-protection-policy"></a>Vytvoření zásady ochrany aplikací MTD

Pomocí postupu [Vytvořte zásady ochrany aplikací pro iOS/iPadOS nebo Android](../apps/app-protection-policies.md#app-protection-policies-for-iosipados-and-android-apps)a na stránkách *aplikace*, *podmíněné spouštění*a *přiřazení* použijte následující informace:

- **Aplikace**: Vyberte aplikace, na které chcete cílit zásady ochrany aplikací. Pro tuto sadu funkcí se tyto aplikace zablokují nebo selektivně vymažou na základě posouzení rizik zařízení od zvoleného dodavatele ochrany před mobilními hrozbami.
- **Podmíněné spuštění**: pod *podmínkami zařízení*, v rozevíracím seznamu vyberte **maximální povolenou úroveň hrozby zařízení**.

  Možnosti pro **hodnotu**úrovně hrozby:

  - **Zabezpečeno:** Tato úroveň poskytuje nejvyšší zabezpečení. Zařízení nemůže mít k dispozici žádné hrozby a bude mít přístup k prostředkům společnosti. Pokud se najde jakákoli hrozba, zařízení se vyhodnotí jako nevyhovující.
  - **Nízká:** Zařízení se vyhodnotí jako vyhovující i v případě, že se v něm nachází jenom hrozby nízké úrovně. Jakákoliv vyšší úroveň zařízení zařadí do stavu nedodržující předpisy.
  - **Střední:** Zařízení vyhovuje, pokud se v něm přítomné hrozby pohybují na střední nebo nízké úrovni. Pokud se v zařízení zjistí hrozby vysoké úrovně, vyhodnotí se jako nevyhovující.
  - **Vysoká**: Tato úroveň je nejméně bezpečná a umožňuje všechny úrovně hrozeb s využitím ochrany před mobilními hrozbami pouze pro účely vytváření sestav. Při tomto nastavení musejí mít zařízení aplikaci pro ochranu před mobilními hrozbami aktivovanou.

  Možnosti pro **akci**:

  - **Blokovat přístup**
  - **Vymazat data**

- **Přiřazení**: přiřaďte zásady skupinám uživatelů.  Zařízení, která používají členové skupiny, se vyhodnocují pro přístup k podnikovým datům na cílových aplikacích prostřednictvím ochrany aplikací Intune.

## <a name="next-steps"></a>Další kroky

- Přečtěte si další informace o [ochrany před mobilními hrozbami](mobile-threat-defense.md) v Microsoft Intune.