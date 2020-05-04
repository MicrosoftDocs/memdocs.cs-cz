---
title: Automatická kategorizace zařízení do kolekcí
titleSuffix: Configuration Manager
description: Zařaďte zařízení do kolekcí automaticky.
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f91f150a095838484c516226da0d3e44e1f5b331
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714308"
---
# <a name="automatically-categorize-devices-into-collections"></a>Automatická kategorizace zařízení do kolekcí

*Platí pro: Configuration Manager (Current Branch)*

Můžete vytvořit kategorie zařízení, které se dají použít k automatickému umístění zařízení do kolekcí zařízení, když používáte Configuration Manager s Microsoft Intune. Uživatelé pak budou muset při registraci zařízení v Intune zvolit kategorii zařízení. Kategorii zařízení můžete změnit z konzoly Configuration Manager.

> [!IMPORTANT]
>  Tato funkce funguje s vydáním Microsoft Intune a novějším z **června 2016** . Než si vyzkoušíte tyto postupy, ujistěte se, že jste tuto verzi aktualizovali.

## <a name="create-device-categories"></a>Vytvoření kategorií zařízení

1.  Přejít na **prostředky a** > **Přehled** > dodržování předpisů**kolekce zařízení**.
2.  Na kartě **Domů** ve skupině **kolekce zařízení** vyberte možnost **spravovat kategorie zařízení**.
3.  Vytváření, úpravy nebo odebírání kategorií.

## <a name="associate-a-collection-with-a-device-category"></a>Přidružení kolekce ke kategorii zařízení

Když přidružíte kolekci k kategorii zařízení, všechna zařízení v této kategorii budou přidána do kolekce. Do předdefinované kolekce, jako jsou **všechny systémy**, nemůžete přidat pravidlo kategorie zařízení.

1.  Na kartě **pravidla členství** v dialogovém okně **vlastnosti** pro kolekci zařízení vyberte možnost **Přidat** > **pravidlo kategorie zařízení**.
2.  V dialogovém okně **vybrat kategorie zařízení** vyberte jednu nebo více kategorií zařízení, které budou aplikovány na všechna zařízení v kolekci.

## <a name="change-the-category-of-a-device"></a>Změna kategorie zařízení

1.  V**části prostředky**a**Přehled** >  **dodržování předpisů** > vyberte zařízení ze seznamu **zařízení** .
2.  Na kartě **Domů** ve skupině **zařízení** vyberte možnost **změnit kategorii**.
3.  Zvolte kategorii a pak zvolte **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Zobrazení kategorie, do které zařízení patří

V části prostředky a**Přehled** >  **dodržování předpisů** > **se v**seznamu **zařízení** zobrazí kategorie ve sloupci **kategorie zařízení** .

Pokud se sloupec **kategorie zařízení** nezobrazí, klikněte pravým tlačítkem myši na záhlaví jednoho ze sloupců v seznamu **zařízení** (jako **název**) a vyberte **kategorie zařízení**.

Pokud zařízení přiřadíte ke kategorii a následně kategorii odstraníte, zobrazí se v seznamu sestava zařízení **zaregistrovaná na uživatele v Microsoft Intune** ve sloupci **kategorie zařízení** identifikátor GUID místo názvu kategorie.
