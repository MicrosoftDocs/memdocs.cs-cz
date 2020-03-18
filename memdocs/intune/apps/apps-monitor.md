---
title: Monitorování informací a přiřazení aplikace
titleSuffix: Microsoft Intune
description: Po přiřazení aplikace uživatelům nebo zařízením můžete tyto informace použít, aby vám usnadnily monitorování jejího stavu.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 64e5133d-1e23-4ee6-b556-f5d32c0e95da
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e6d06bade82dcebd170d7594ce25033382a2634
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325783"
---
# <a name="monitor-app-information-and-assignments-with-microsoft-intune"></a>Monitorování informací a přiřazení aplikace pomocí Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune poskytuje několik způsobů, jak monitorovat vlastnosti spravovaných aplikací a spravovat stav jejich přiřazení.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **všech aplikacích**.
3. V seznamu aplikací vyberte aplikaci, která se má monitorovat. Zobrazí se podokno aplikace s přehledem stavu zařízení a uživatele.

> [!NOTE]
> Aplikace z obchodu pro Android, které jsou nasazeny jako **K dispozici**, nehlásí svůj stav instalace.
>
> U spravovaných aplikací Google Play nasazených do zařízení se systémem Android Enterprise Work profilů můžete zobrazit stav a číslo verze aplikace nainstalované na zařízení pomocí Intune. 

## <a name="app-overview-pane"></a>Podokno přehledu aplikace

V podokně aplikace si můžete zkontrolovat podrobnosti o stavu aplikace ve vašem prostředí.

### <a name="essentials"></a>Základy
Část **Základy** obsahuje následující informace o aplikaci:

 | **Podrobnosti aplikace**            | **Popis**                                                      |
|------------------------|------------------------------------------------------------------|
| **Vydavatel**          | Vydavatel aplikace                                            |
| **Operační systém**   | Operační systém aplikace (Windows, iOS/iPadOS, Android atd.). |
| **Vytvořeno**             | Datum a čas vytvoření této revize <b>**Poznámka**: Tato hodnota data se aktualizuje, když správce IT změní metadata aplikace, jako je například změna kategorie aplikace nebo popisu aplikace.                        |
| **Přiřazeno**           | Jestli byla aplikace přiřazena (**Ano** nebo **Ne**)                  |

### <a name="device-and-user-status-graphs"></a>Grafy stavu zařízení a uživatele
Grafy zobrazují počet aplikací pro následující stav:

| **Stav zařízení**       | **Popis**                                       |
|-----------------------|-------------------------------------------------------|
| **Instalováno**         | Počet nainstalovaných aplikací                         |
| **Nenainstalováno**     | Počet nenainstalovaných aplikací                     |
| **Neúspěch**            | Počet neúspěšných instalací                   |
| **Instalace čeká**   | Počet aplikací, které se právě instalují |
| **Není k dispozici**           | Počet aplikací, u nichž není stav k dispozici            |

> [!NOTE]
> Mějte na paměti, že aplikace pro Android LOB (. APK) nasazené jako **k dispozici s registrací nebo bez registrace** stav instalace aplikace pouze u zaregistrovaných zařízení. Pro zařízení, která nejsou zaregistrovaná v Intune, není stav instalace aplikace k dispozici.

### <a name="device-install-status"></a>Stav instalace zařízení

Seznam stavů zařízení se zobrazí, když v části nabídky **Monitorovat** vyberete **Stav instalace zařízení**. Tabulka s podrobnostmi obsahuje následující sloupce:

| **Sloupec zařízení**      | **Popis**                                                                                                                                                                                                                                            |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Název zařízení**      | Název zařízení na platformách, které umožňují pojmenování zařízení. Na ostatních platformách Intune vytvoří název z dalších vlastností. Tento atribut není k dispozici žádnému jinému zařízení.                                                                       |
| **Uživatelské jméno**        | Jméno uživatele                                                                                                                                                                                                                                      |
| **Platforma**         | Operační systém zařízení (Windows, iOS/iPadOS, Android atd.).                                                                                                                                                                                           |
| **Verze**          | Číslo verze aplikace. V případě obchodních aplikací a Microsoft Store pro obchodní aplikace se zobrazí úplné číslo verze aplikace. Celé číslo verze identifikuje konkrétní vydanou verzi aplikace. Číslo se zobrazí jako _Verze_(_build_). Příklad: 2.2(2.2.17560800) V případě aplikací pro standardní úložiště nejsou zobrazeny žádné verze. |
| **Stav**           | Stav aplikace                                                                                                                                                                                                                                     |
| **Podrobnosti stavu**   | Podrobnosti o stavu                                                                                                                                                                                                                                     |
| **Poslední vrácení se změnami**    | Datum, kdy se zařízení naposledy synchronizovalo s Intune                                                                                                                                                                                                                  |


### <a name="user-install-status"></a>Stav instalace uživatele

Seznam stavů uživatele se zobrazí, když v části nabídky **Monitorovat** vyberete **Stav instalace uživatele**. Tabulka s podrobnostmi obsahuje následující sloupce:

| **Sloupec uživatele**     | **Popis**                           |
|---------------------|-------------------------------------------|
| **Název**            | Jméno uživatele ve službě Azure Active Directory         |
| **Uživatelské jméno**       | Jedinečné jméno uživatele              |
| **Instalace**   | Počet aplikací, které nainstaloval uživatel |
| **Chyby**        | Počet nezdařených instalací aplikace pro uživatele     |
| **Nenainstalováno**   | Počet aplikací, které nenainstaloval uživatel |


## <a name="next-steps"></a>Další kroky

- Další informace o práci s daty Intune najdete v článku [Použití datového skladu Intune](../developer/reports-nav-create-intune-reports.md).
- Další informace o zásadách konfigurace aplikací najdete v tématu [Zásady konfigurace aplikací v Intune](app-configuration-policies-overview.md).
