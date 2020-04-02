---
title: Sady zásad
titleSuffix: Microsoft Intune
description: Pomocí sad zásad můžete seskupovat kolekce objektů pro správu v Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: craigma
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 82e02795dc9dbcbc0598218418404fe74fdf1226
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551618"
---
# <a name="use-policy-sets-to-group-collections-of-management-objects"></a>Použití sad zásad k seskupení kolekcí objektů pro správu

Sady zásad umožňují vytvořit sadu odkazů na již existující entity správy, které je třeba identifikovat, cílit a monitorovat jako jednu koncepční jednotku. Sada zásad je přiřaditelné kolekce aplikací, zásad a dalších objektů pro správu, které jste vytvořili. Vytvořením sady zásad můžete vybrat mnoho různých objektů najednou a přiřadit je z jednoho místa. Při změně vaší organizace můžete sadu zásad znovu navštívit a přidat nebo odebrat její objekty a přiřazení. Pomocí sady zásad můžete přidružit a přiřadit existující objekty, jako jsou aplikace, zásady a sítě VPN, v jediném balíčku. 

> [!IMPORTANT]
> Seznam známých problémů, které souvisejí se sadami zásad, [nastavuje zásady známé problémy](policy-sets.md#policy-sets-known-issues).

Sady zásad nenahrazují existující koncepty ani objekty. Můžete dál přiřazovat jednotlivé objekty a v rámci sady zásad můžete také odkazovat na jednotlivé objekty. Proto se v sadě zásad projeví všechny změny těchto jednotlivých objektů.

Sady zásad můžete použít k těmto akcím:

- Seskupit objekty, které je potřeba přiřadit dohromady
- Přiřazení minimálních požadavků na konfiguraci vaší organizace pro všechna spravovaná zařízení
- Přiřazení běžně používaných nebo relevantních aplikací všem uživatelům

V sadě zásad můžete zahrnout následující objekty správy:

- Aplikace
- Zásady konfigurace aplikací
- Zásady ochrany aplikace
- Konfigurační profily zařízení
- Zásady dodržování předpisů pro zařízení
- Omezení typu zařízení
- Profily nasazení Windows autopilotu
- Obrazovka stavu registrace (zápisu)

Při vytváření sady zásad můžete vytvořit jednu jednotku přiřazení a spravovat přidružení mezi různými objekty. Sada zásad bude odkazovat na externí objekty. Všechny změny v zahrnutých objektech ovlivní také sadu zásad. Po vytvoření sady zásad můžete opakované zobrazení a úpravu svých objektů a přiřazení. 

> [!NOTE]
> Sady zásad podporují nastavení Windows, Androidu, macOS a iOS/iPadOS a dají se přiřadit pro různé platformy.

## <a name="how-to-create-a-policy-set"></a>Postup vytvoření sady zásad

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **sady zásad** > **sady zásad** > **vytvořit**.
3. Na stránce **základy** přidejte následující hodnoty:
    - **Název sady zásad** – zadejte název pro tuto sadu zásad.
    - **Popis** – Volitelně můžete zadat popis sady zásad.
   <p>
      <img alt="Create policy set - Basics" src="./media/policy-sets/policy-sets-01.png">

4. Klikněte na **Další: Správa aplikací**.<br>
   Na stránce **Správa aplikací** můžete volitelně přidat do sady zásad [aplikace](../apps/apps-add.md), [zásady konfigurace aplikací](../apps/app-configuration-policies-overview.md)a [Zásady ochrany aplikací](../apps/app-protection-policy.md) . Informace o správě aplikací najdete v tématu [co je Správa aplikací Microsoft Intune?](../apps/app-management.md).
5. Klikněte na **Další: Správa zařízení**.<br>
   Stránka **Správa zařízení** umožňuje přidat objekty správy zařízení do sady zásad, jako jsou například [konfigurační profily zařízení](../configuration/device-profiles.md) a [zásady dodržování předpisů zařízením](../protect/device-compliance-get-started.md). Nezapomeňte zahrnout všechny přidružené objekty, jako jsou další zásady, certifikáty a profily standardních hodnot zabezpečení.
6. Klikněte na **Další: registrace zařízení**.<br>
   Stránka **registrace zařízení** umožňuje přidat objekty registrace zařízení do sady zásad, jako jsou například [omezení typu zařízení](../enrollment/enrollment-restrictions-set.md), [profily nasazení Windows autopilot](../enrollment/enrollment-autopilot.md)a [profily stránky stavu registrace](../enrollment/windows-enrollment-status.md).
7. Klikněte na **Další: přiřazení**.<br>
   Na stránce **přiřazení** můžete přiřadit sadu zásad pro uživatele a zařízení. Je důležité si uvědomit, že můžete přiřadit sadu zásad k zařízení bez ohledu na to, jestli je zařízení spravované přes Intune.
8. Klikněte na **Další: zkontrolovat + vytvořit** a zkontrolujte hodnoty, které jste zadali pro profil.
9. Po dokončení klikněte na **vytvořit** a vytvořte sadu zásad v Intune.

## <a name="policy-sets-known-issues"></a>Sady zásad – známé problémy

U sad zásad, které jsou novinkou 1910, se zobrazí následující známé problémy.

- Pokud při vytváření sady zásad dojde k pokusu o vytvoření sady zásad bez výběru značek oboru, ověření se při dosažení stránky **Kontrola a vytvoření** nezdaří a na stavovém řádku se zobrazí chyba. Správce musí v procesu přepnout na jinou stránku a pak se vrátit na stránku **Revize + vytvořit** . Tím se povolí možnost **vytvořit** .  

- Sady zásad aktuálně podporují následující typy aplikací:
  - aplikace pro iOS/iPadOS Store
  - obchodní aplikace pro iOS/iPadOS
  - Spravovaná obchodní aplikace pro iOS/iPadOS
  - Aplikace z obchodu pro Android
  - Obchodní aplikace pro Android
  - Spravovaná obchodní aplikace pro Android
  - Sada Office 365 ProPlus (Windows 10)
  - Webový odkaz
  - Integrovaná aplikace pro iOS/iPadOS
  - Integrovaná aplikace pro Android

- Nastavení přiřazení sady zásad pro **všechny uživatele** na **profil autopilotu** se nepodporuje.

- Pro sady zásad jsou k dispozici následující omezení registrace a problémy se stránkou stavu registrace (ESP):
  - Omezení a ESP nepodporují přiřazení virtuálních skupin.
  - Omezení a ESP nepodporují výhradně přiřazení skupin vyloučení. 
  - Omezení a ESP používají řešení konfliktů založené na prioritách. Omezení a ESP se nemusí použít pro stejné uživatele jako zbytek datových částí sady zásad, pokud jsou omezení a ESP také zaměřená omezeními s vyšší prioritou a ESP.
  - Do sady zásad nelze přidat výchozí omezení a ESP.

- Typy zásad MAM, které podporují sady zásad, zahrnují následující: 
  - Ochrana MAM NV (Windows) cílené spravované aplikace na MDM 
  - Ochrana cílené spravované aplikace MAM iOS/iPadOS
  - Ochrana cílené spravované aplikace MAM pro Android
  - Konfigurace cílené spravované aplikace MAM iOS/iPadOS
  - Konfigurace cílené spravované aplikace MAM pro Android

- Typy zásad MAM, které nepodporují sady zásad, zahrnují následující: 
  - MAMá Ochrana aplikace cílené na správu nedokončené výroby (Windows)

- MAM zpracovává přiřazení sady zásad jako přímá přiřazení pro následující typy zásad:
  - Ochrana cílené spravované aplikace MAM iOS/iPadOS
  - Ochrana cílené spravované aplikace MAM pro Android
  - Konfigurace cílené spravované aplikace MAM iOS/iPadOS
  - Konfigurace cílené spravované aplikace MAM pro Android

    Pokud se do sady zásad, která je nasazená do skupiny, přidá zásada, bude se tato skupina zobrazovat jako přímo přiřazená v rámci úlohy, nikoli přiřazená prostřednictvím sady zásad. V důsledku toho MAM nezpracovává odstranění přiřazení skupin pocházející ze sad zásad.

- MAM nepodporuje nasazení u všech typů zásad pro **všechny uživatele** a všechny virtuální skupiny **zařízení** .

## <a name="next-steps"></a>Další kroky

- [Registrace zařízení v Microsoft Intune](../enrollment/index.yml)
