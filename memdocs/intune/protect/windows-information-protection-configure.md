---
title: Nastavení Windows Information Protection v Microsoft Intune
titleSuffix: Microsoft Intune
description: Přečtěte si o nastaveních Microsoft Intune, pomocí kterých můžete spravovat Windows Information Protection.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 008f750fd15caeac8da9397a1c3ff0684cdf28f7
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914663"
---
# <a name="how-to-configure-windows-information-protection-in-microsoft-intune"></a>Konfigurace nastavení Windows Information Protection v Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Díky nárůstu počtu zařízení vlastněných zaměstnanci v podniku se také zvyšuje riziko náhodných úniků dat prostřednictvím aplikací a služeb, jako jsou e-mail, sociální média a veřejný cloud, které jsou mimo podniková řízení. Jsou to situace, kdy uživatel například odešle nejnovější technické výkresy ze svého osobního e-mailového účtu, zkopíruje informace o produktu a vloží je do tweetu nebo uloží aktuální zprávu o prodeji do veřejného cloudového úložiště.

**Windows Information Protection** pomáhá chránit před potenciálním únikem dat, aniž by bylo v jiném vlivu na práci zaměstnanců. Pomáhá také chránit podnikové aplikace a data před náhodnými úniky dat na zařízeních ve vlastnictví společnosti a osobních zařízeních, která si uživatelé přinesou do práce, a nevyžaduje přitom žádné změny prostředí nebo ostatních aplikací.

Tyto zásady Intune spravují seznam aplikací chráněných službou Windows Information Protection, umístění v podnikové síti, úroveň ochrany a nastavení šifrování.

>[!NOTE]
> Pokud chcete používat aplikaci Portál společnosti pro Windows 10 se službou Windows Information Protection, musíte přidat aplikaci Portál společnosti v režimu služby Windows Information Protection **Výjimka**. 

Další informace najdete tady:
- [Ochrana podnikových dat pomocí sady Windows Information Protection](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Vytvoření zásad pro Windows Information Protection (WIP) pomocí klasické konzoly pro Microsoft Intune](/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune)
- [Vytvoření zásad pro Windows Information Protection (WIP) s MDM pomocí portálu Azure Portal pro Microsoft Intune](/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune-azure)
- [Vytvoření zásad pro Windows Information Protection (WIP) s MAM pomocí portálu Azure Portal pro Microsoft Intune](/windows/threat-protection/windows-information-protection/create-wip-policy-using-mam-intune-azure)