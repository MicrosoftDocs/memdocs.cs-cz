---
title: Vzdálená správa zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na role, které jsou potřeba pro použití TeamVieweru, jak nainstalovat konektor TeamVieweru a přečtěte si podrobné pokyny ke vzdálené správě zařízení pomocí Microsoft Intune na portálu Azure Portal.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 72cdd888-efca-46e6-b2e7-fb9696bb2fba
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b63dbf983872dbbb1c792e1f5d00bb136da973a1
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328327"
---
# <a name="use-teamviewer-to-remotely-administer-intune-devices"></a>Vzdálená správa zařízení s Intune pomocí TeamVieweru

Zařízení spravovaná pomocí Intune je možné spravovat vzdáleně pomocí [TeamVieweru](https://www.teamviewer.com). TeamViewer je program od jiného výrobce, který se kupuje samostatně. V tomto tématu můžete vidět, jak nakonfigurovat TeamViewer v rámci Intune a vzdáleně spravovat zařízení. 

## <a name="prerequisites"></a>Požadavky

- Používejte podporované zařízení. Správa zařízení s Androidem spravovaná přes Intune, pracovní profil Androidu, Windows, iOS/iPadOS a zařízení macOS podporují vzdálenou správu. TeamViewer nemusí podporovat Windows Holographic (HoloLens), Windows Team (Surface Hub) nebo Windows 10 S. Informace týkající se aktualizací podpory najdete v části [TeamViewer](https://www.teamviewer.com).

> [!NOTE]
> Vyhrazená a plně spravovaná pro Android nejsou podporovaná.

- Správce Intune musí mít na portálu Azure Portal tyto [role Intune](../fundamentals/role-based-access-control.md):  

  - **Aktualizovat vzdálenou pomoc**: Umožňuje správcům upravit nastavení konektoru TeamVieweru.
  - **Požádat o vzdálenou pomoc**: Umožňuje správcům zahájit pro libovolného uživatele novou relaci vzdálené pomoci. Uživatele s touto rolí neomezuje žádná role Intune, která je v daném rozsahu. Uživatelé nebo skupiny zařízení, kteří mají přiřazenou roli Intune v rámci rozsahu, si také můžou vyžádat vzdálenou pomoc. 

- Účet [TeamVieweru](https://www.teamviewer.com) s přihlašovacími údaji pro přihlášení. Integraci s Intune můžou podporovat jenom některé licence pro TeamViewer. Konkrétní potřeby TeamVieweru najdete v tématu [partner integrace pro TeamViewer: Microsoft Intune](https://www.teamviewer.com/integrations/microsoft-intune/).

Když použijete TeamViewer, umožníte Konektoru pro TeamViewer služby Intune vytvářet relace TeamVieweru, číst data služby Active Directory a uložit přístupový token účtu TeamVieweru.

## <a name="configure-the-teamviewer-connector"></a>Konfigurace konektoru pro TeamViewer

Abyste mohli poskytovat vzdálenou pomoc pro zařízení, nakonfigurujte si s použitím následujícího postupu konektor pro TeamViewer a Intune:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte možnost **Správa tenanta** > **konektory a tokeny** > **konektor pro TeamViewer**.
3. Vyberte **Připojit** a přijměte podmínky licenční smlouvy.
4. Zvolte **Přihlásit se k TeamVieweru pro autorizaci**.
5. Otevře se webová stránka TeamVieweru. Zadejte přihlašovací údaje pro svoji licenci TeamVieweru a pak se **přihlaste**.

## <a name="remotely-administer-a-device"></a>Vzdálená správa zařízení

Po konfiguraci konektoru jste připravení vzdáleně spravovat zařízení. Postupujte podle následujících pokynů: 

1. V centru pro [správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Zařízení** a potom **Všechna zařízení**.
3. V seznamu vyberte zařízení, které chcete vzdáleně spravovat > **...**  > **novou relaci vzdálené pomoci**.
4. Až se Intune ke službě TeamViewer připojí, zobrazí se některé informace o zařízení. Ke spuštění vzdálené relace použijte možnost **Připojit**.

![Vzdálená správa zařízení s Androidem pomocí TeamVieweru – příklad](./media/teamviewer-support/android-teamviewer.png)

Když spustíte vzdálenou relaci, uživatelé uvidí na svém zařízení příznak oznámení na ikoně aplikace Portál společnosti. Oznámení se zobrazí také při otevření aplikace. Uživatelé pak mohou žádost o vzdálenou pomoc přijmout.

> [!NOTE]
> Zařízení s Windows, která jsou zaregistrovaná pomocí metod bez uživatelů, například DEM a WCD, nezobrazují v aplikaci Portál společnosti oznámení o TeamVieweru. V těchto scénářích doporučujeme k vygenerování relace použít portál TeamViewer.

V TeamVieweru můžete provést na zařízení řadu akcí, včetně převzetí řízení zařízení. Úplné podrobnosti s informacemi, co můžete dělat, najdete v tématu [Pokyny k TeamVieweru](https://www.teamviewer.com/support/documents/).

Až budete mít hotovo, okno TeamVieweru zavřete.