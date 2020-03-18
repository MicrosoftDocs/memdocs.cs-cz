---
title: Vyřazení počítače s Windows
titleSuffix: Microsoft Intune
description: Jak vyřadit počítač s Windows spravovaný pomocí Intune
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 5c916182-d99c-44c5-a779-3f596f261c40
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: e7d88b5ba8f5071821d1a9901a26bfb4a5a6fbd3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330675"
---
# <a name="retire-a-windows-pc"></a>Vyřazení počítače s Windows

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Následujícím postupem můžete vyřadit počítače, které spravujete tak, že na nich běží klientský software Intune. Při vyřazení počítače se daný počítač odebere ze správy Intune. Počítač nelze obnovit do původního továrního nastavení vymazáním z Intune.

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/)vyberte **skupiny** &gt; **všechna zařízení** (nebo jinou skupinu obsahující počítač, který chcete vyřadit).

2. Vyberte zařízení, která chcete vyřadit, a potom zvolte **Vyřadit z provozu či vymazat**.

Když budete chtít počítač do Intune znovu zaregistrovat, nainstalujte na počítači znovu klientský software, a to podle pokynů uvedených v tématu [Instalace klienta na počítači s Windows pomocí Microsoft Intune](install-the-windows-pc-client-with-microsoft-intune.md).

Když se nějaký počítač nemůže k Intune připojit, v pracovním prostoru **Řídicí panel** se zobrazí zpráva.

Při vyřazení počítače se stane toto:

- Počítač se odebere z inventáře a správy Intune a licence, které jsou k němu přiřazené, se uvolní pro nové použití. Vyřazení z provozu či vymazání odebere klientský software Intune, ale neodebere z počítače aplikace a data. Při vyřazení se neprovede úplné vymazání počítače.

- Jeho stav se už nebude zobrazovat v konzole Intune.

- Intune odebere z počítače klientský software. Pokud počítač není ke službě Intune připojený, klientský software se odebere, až se počítač zase připojí.

- Z počítače se odebere Microsoft Intune Endpoint Protection. Pokud je na počítači nainstalovaná jiná aplikace ochrany koncových bodů a je zakázaná, může se tato aplikace po odebrání Microsoft Intune Endpoint Protection zase povolit, aby se zajistila ochrana počítače.

- Z počítače se odeberou všechny zásady a hodnoty nastavené těmito zásadami se změní.

- Počítač už nebude z Intune dostávat aktualizace softwaru ani aktualizace definic malwaru.

- V závislosti na tom, jak je vyřazený počítač nakonfigurovaný, může nadále získávat aktualizace pomocí služeb Windows Server Update Services, Windows Update nebo Microsoft Update.

    > [!IMPORTANT]
    > Když byl klientský software nainstalován pomocí objektu zásad skupiny, musíte tento objekt před odebráním klientského softwaru odebrat, abyste zabránili přeinstalaci softwaru.

    Pokud se odinstalace klienta služby Endpoint Protection nepovede, přečtěte si další nápovědu v tématu [Řešení potíží se službou Endpoint Protection](/intune/troubleshoot-endpoint-protection-in-microsoft-intune).

## <a name="see-also"></a>Viz také

[Běžné úlohy správy počítačů s Windows pomocí klientského softwaru Intune](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
