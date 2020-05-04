---
title: Žádost a poskytnutí vzdálené pomoci na počítačích s Windows
titleSuffix: Microsoft Intune
description: Popisuje kroky koncových uživatelů a správců IT potřebné k poskytnutí vzdálené pomoci na počítačích s Windows, které se spravují jako počítače, a kroky potřebné k vzdálenému spuštění počítače.
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
ms.assetid: c2654491-5144-408a-a45a-644eb91ac1bb
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 901064b4902ad9a0de490596d10f99a7507fa5e2
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330699"
---
# <a name="request-and-provide-remote-assistance-for-windows-pcs"></a>Žádost a poskytnutí vzdálené pomoci na počítačích s Windows

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Informace v tomto tématu se vztahují jenom na desktopové systémy Windows, které spravujete jako počítače (PC) pomocí softwarového klienta Intune.

Microsoft Intune může využívat software [TeamViewer](https://www.teamviewer.com), který se kupuje zvlášť. Díky tomu vám umožní poskytovat vzdálenou pomoc uživatelům, kteří používají softwarového klienta Intune. Když si uživatel vyžádá pomoc od centra Microsoft Intune Center, budete o tom informováni prostřednictvím výstrahy. Můžete tuto žádost přijmout a potom poskytnout pomoc. Tato funkce nahrazuje stávající funkci Vzdálená pomoc pro Windows v Intune.


## <a name="before-you-start"></a>Než začnete

Než začnete reagovat na požadavky na vzdálenou pomoc, zajistěte splnění těchto požadavků:

- Musíte mít [zaregistrovaný účet TeamViewer](https://login.teamviewer.com/LogOn#register) pro přihlášení k webu TeamViewer.
- Počítače s Windows, které chcete spravovat, se musí [spravovat přes softwarového klienta Windows](manage-windows-pcs-with-microsoft-intune.md).
- Spravovat je možné všechny operační systémy Windows pro počítače, které Intune podporuje.

## <a name="configure-the-teamviewer-connector"></a>Konfigurace Konektoru pro TeamViewer

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com) zvolte **Správce**.
2. V pracovním prostoru **Správa** zvolte **TeamViewer**.
3. Na stránce **TeamViewer** vyberte v části **Konektor pro TeamViewer** možnost **Povolit**.
4. V dialogovém okně **Povolit TeamViewer** si přečtěte licenční podmínky a potom je **přijměte**. Pokud ještě nemáte licenci TeamVieweru, zvolte **Koupit licenci na TeamViewer**.
5. Když se otevře okno prohlížeče TeamViewer, přihlaste se k tomuto webu pomocí svých přihlašovacích údajů pro TeamViewer.
6. Na webu TeamVieweru si přečtěte a potom přijměte možnosti, které službě Intune umožňují připojit se k TeamVieweru.
7. V konzole Intune ověřte, že se položka **Konektor pro TeamViewer** zobrazuje jako **povolená**.


## <a name="open-a-remote-assistance-request-end-user"></a>Otevření žádosti o vzdálenou pomoc (koncový uživatel)

1. Na klientském počítači s Windows otevřete **Microsoft Intune Center**.
2. V části **Vzdálená pomoc** zvolte **Požádat o vzdálenou pomoc**.
3. Jakmile žádost schválíte (viz níže), na klientovi se otevře TeamViewer. Uživatel musí přijmout všechny zprávy informující o tom, že se webový prohlížeč pokouší otevřít aplikaci TeamViewer.
4. Uživateli se zobrazí zpráva s dotazem, jestli můžete převzít kontrolu nad jeho počítačem. Tuto zprávu musí přijmout, aby bylo možné pokračovat.
5. Během relace vzdálené pomoci se uživateli zobrazí okno, které ukazuje, že jste připojeni. Pokud toto okno zavře, vzdálená relace se ukončí.

## <a name="respond-to-a-remote-assistance-request"></a>Odpověď na žádost o vzdálenou pomoc

1. Když uživatel odešle žádost o vzdálenou pomoc, můžete ji zobrazit v pracovním prostoru **Výstrahy** v části **Monitorování** > **Vzdálená pomoc**. Příklad:
   > ![Snímek obrazovky žádosti o vzdálenou pomoc](./media/request-and-provide-remote-assistance-for-windows-pcs-in-microsoft-intune/team-viewer.png)

<br>Pokud žádost zůstane nezodpovězená víc než 4 hodiny, odebere se.
2. Pokud chcete žádost přijmout, zvolte **Schválit požadavek a spustit vzdálenou pomoc**.
3. V dialogovém okně **Nová žádost o vzdálenou pomoc čeká na vyřízení** zvolte **Žádost o vzdálenou pomoc přijměte**. Pokud ještě na počítači nemáte nainstalované všechny potřebné aplikace, TeamViewer je nainstaluje.
4. TeamViewer potom upozorní koncového uživatele, že chcete převzít kontrolu nad jeho počítačem. Když uživatel tuto žádost přijme, otevře se okno TeamViewer a máte kontrolu nad jeho počítačem.

Během relace vzdálené pomoci můžete k řízení vzdáleného počítače využívat všechny dostupné příkazy TeamVieweru. Pokud s těmito příkazy potřebujete pomoci, stáhněte si [příručku pro vzdálené řízení](http://www.teamviewer.com/en/support/documents/) z webu TeamVieweru.

## <a name="close-the-remote-assistance-session"></a>Zavření relace vzdálené pomoci

V nabídce **Akce** v okně **TeamViewer** zvolte **Ukončit relaci**.

## <a name="remotely-restart-a-windows-pc"></a>Vzdálené restartování počítače s Windows
Při pomáhání uživatelům s problémy můžete občas potřebovat vzdáleně restartovat jejich počítač. Počítač s Windows můžete vzdáleně restartovat pomocí následujícího postupu.

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/) zvolte **Skupiny** &gt; **Všechna zařízení** (nebo jinou skupinu obsahující počítač, který chcete restartovat).

2. Vyberte jeden nebo více počítačů a zvolte **Vzdálené úlohy** &gt; **Restartovat počítač**.

3. Pokud chcete zobrazit stav úlohy, v pravém dolním rohu stránky zvolte **Vzdálené úlohy**.

4. V dialogovém okně **Stav úlohy** se můžete podívat na aktuální vzdálené úlohy, stav úloh, název zařízení a všechny hlášené chyby.

## <a name="see-also"></a>Viz také

[Běžné úlohy správy počítačů s Windows pomocí klientského softwaru Intune](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
