---
title: Povolit aplikace Win32 na zařízeních S režimem S
titleSuffix: Microsoft Intune
description: Naučte se, jak povolit aplikace Win32 na zařízeních S režimem S pomocí Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/08/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 796e95b09193228fdc4612a370658e532fbbd2c6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80324372"
---
# <a name="enable-win32-apps-on-s-mode-devices"></a>Povolit aplikace Win32 na zařízeních S režimem S

[Režim Windows 10 S](https://docs.microsoft.com/windows/deployment/s-mode) je zamčený operační systém, který spouští jenom aplikace pro Store. Ve výchozím nastavení zařízení S Windows S nedovolují instalaci a spouštění aplikací Win32. Mezi tato zařízení patří jediná *základní zásada desítkách*, která uzamkne zařízení režimu S režimem pro spouštění aplikací Win32. Vytvořením a použitím **doplňkové zásady v režimu S** v Intune ale můžete nainstalovat a spustit aplikace Win32 na zařízeních spravovaných v režimu Windows 10 S. Pomocí nástrojů prostředí PowerShell pro [řízení aplikací v programu Microsoft Defender (WDAC)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) můžete vytvořit jednu nebo více doplňkových zásad pro režim systému Windows S. Doplňkové zásady musíte podepsat pomocí [služby Device Guard Signing Service (DGSS)](https://go.microsoft.com/fwlink/?linkid=2095629) nebo pomocí nástroje [SignTool. exe](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/use-signed-policies-to-protect-windows-defender-application-control-against-tampering) a pak tyto zásady nahrát a distribuovat prostřednictvím Intune. Alternativně můžete podepsat doplňkové zásady s certifikátem pro podepisování z vaší organizace, ale upřednostňovanou metodou je použití DGSS. V případě, že používáte certifikát pro podepisování kódu z vaší organizace, musí být v zařízení přítomen kořenový certifikát, ke kterému je zřetězený certifikát.

Když v Intune přiřadíte doplňkovou zásadu režimu S, povolíte zařízení, aby vyvolalo výjimku z existujících zásad režimu pro zařízení, což umožňuje nahraný odpovídající podepsaný katalog aplikací. Zásady nastaví seznam povolených aplikací (katalog aplikací), který se dá použít na zařízení v režimu S.

> [!NOTE]
> Aplikace Win32 na zařízeních S režimem S se podporují jenom ve Windows 10 listopadu 2019 Update (Build 18363) nebo novějších verzích.

<!-- Add WDAC tooling diagram  -->

Postup pro povolení spouštění aplikací Win32 v zařízení S Windows 10 v režimu S jsou následující:

1. Povolit zařízení S režimem S v Intune jako součást procesu registrace Windows 10 S.
2. Vytvořte doplňkovou zásadu, která povolí aplikace Win32:
   - K vytvoření doplňkové zásady můžete použít nástroje [Microsoft Defender Application Control (WDAC)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) . Základní ID zásad v rámci této zásady se musí shodovat s ID základní zásady režimu S (pevně zakódovaným na klientovi). Také se ujistěte, že je verze zásad vyšší než předchozí verze.
   - K podepsání doplňkové zásady se používá DGSS. Další informace najdete v tématu [podepisování zásad integrity kódu pomocí podepisování zařízení před ochranou](https://docs.microsoft.com/microsoft-store/sign-code-integrity-policy-with-device-guard-signing).
   - Do Intune se nahrávají přihlášené doplňkové zásady vytvořením doplňkové zásady režimu Windows 10 S (viz níže).
3. Povolíte katalogy aplikací Win32 prostřednictvím Intune:
   - Vytvoříte katalogové soubory (1 pro každou aplikaci) a podepíšete je pomocí DGSS nebo jiné infrastruktury certifikátů.
   - Podepsaný katalog zabalíte do souboru *. intunewin* pomocí nástroje pro [přípravu obsahu Microsoft Win32](https://go.microsoft.com/fwlink/?linkid=2065730). Při vytváření souboru katalogu pomocí [Nástroje pro přípravu obsahu Microsoft Win32](https://go.microsoft.com/fwlink/?linkid=2065730)neexistují žádná omezení pojmenování. Při generování souboru *. intunewin* ze zadané zdrojové složky a instalačního souboru můžete zadat samostatnou složku obsahující pouze soubory katalogu pomocí možnosti-a cmdline. Další informace najdete v tématu [Správa aplikací Win32 – Příprava obsahu aplikace Win32 pro nahrání](apps-win32-app-management.md#prepare-the-win32-app-content-for-upload).
   - Intune použije podepsaný katalog aplikací k instalaci aplikace Win32 do zařízení v režimu S pomocí [rozšíření pro správu Intune](intune-management-extension.md).

> [!NOTE]
> Obchodní aplikace (LOB) `.appx` a `.appx` sady v režimu Windows 10 S se budou podporovat prostřednictvím podepisování Microsoft Store pro firmy (MSFB).
>
> **Doplňkové zásady** pro aplikace se musí doručovat prostřednictvím rozšíření pro správu Intune.
>
> Zásady režimu S jsou vynutily na úrovni zařízení. Na zařízení se sloučí několik cílových zásad. Na zařízení se vynutila Sloučená zásada.

Chcete-li vytvořit doplňkové zásady režimu Windows 10 S, použijte následující postup:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > v**režimu doplňkové zásady** > **vytvořit zásadu**.
3. Před přidáním **souboru zásad**je nutné ho vytvořit a podepsat. Další informace naleznete v tématu:
    - [Vytvoření zásady WDAC pomocí nástrojů PowerShellu a její převedení do binárního formátu](https://go.microsoft.com/fwlink/?linkid=2095387)
    - [Podepsat pomocí služby podepisování zařízení Guard](https://go.microsoft.com/fwlink/?linkid=2095629) **(doporučeno)**

4. Na stránce **základy** přidejte následující hodnoty:

    | Hodnota | Popis |
    |--------------|------------------------------------------------|
    | Soubor zásad | Soubor, který obsahuje zásady WDAC. |
    | Název | Název této zásady. |
    | Popis | Volitelné Popis této zásady |

5. Klikněte na tlačítko **Další: značky oboru**.<br>
   Na stránce **značky oboru** můžete volitelně nakonfigurovat značky oboru, abyste zjistili, kdo může zásady aplikace zobrazit v Intune. Další informace o značkách oboru najdete v tématu [použití značek řízení přístupu na základě role a rozsahu pro distribuci IT](../fundamentals/scope-tags.md).

6. Klikněte na **Další: přiřazení**.<br>
   Na stránce **přiřazení** můžete přiřadit zásady pro uživatele a zařízení. Je důležité si uvědomit, že k zařízení můžete přiřadit zásadu bez ohledu na to, jestli zařízení spravuje Intune.
7. Klikněte na **Další: zkontrolovat + vytvořit** a zkontrolujte hodnoty, které jste zadali pro profil.
8. Až skončíte, klikněte na **vytvořit** a vytvořte doplňkovou zásadu v režimu S v Intune.

Jakmile se zásada vytvoří, zobrazí se její přidání do seznamu doplňkových zásad v režimu S v Intune. Po přiřazení zásady se zásada nasadí do zařízení. Všimněte si, že je nutné nasadit aplikaci do stejné skupiny zabezpečení jako doplňkovou zásadu. Můžete začít cílit a přiřazovat aplikace těmto zařízením. To umožní koncovým uživatelům instalovat a spouštět aplikace na zařízeních v režimu S.

## <a name="removal-of-s-mode-policy"></a>Odebrání zásad režimu S S

Pokud v současné době chcete ze zařízení odebrat doplňkovou zásadu v režimu S, musíte přiřadit a nasadit prázdnou zásadu a přepsat stávající doplňkové zásady v režimu S.

## <a name="policy-reporting"></a>Vytváření sestav zásad

Doplňkové zásady v režimu S, které jsou vynutily na úrovni zařízení, mají jenom vytváření sestav na úrovni zařízení. Vytváření sestav na úrovni zařízení je k dispozici pro stavy úspěch a chyby.

Vytváření sestav hodnot, které se zobrazují v konzole Intune pro zásady vytváření sestav v režimu S:
- **Úspěch**: platná doplňková zásada v režimu S.
- **Neznámé**: stav doplňkových zásad v režimu S není známý.
- **TokenError**: doplňkové zásady v režimu S jsou strukturálně v pořádku, ale při autorizaci tokenu dojde k chybě.
- **NotAuthorizedByToken**: token neautorizuje tuto doplňkovou zásadu v režimu S.
- **PolicyNotFound**: nebyla nalezena doplňková zásada v režimu S.

## <a name="next-steps"></a>Další kroky

- Další informace najdete v části [aplikace Win32 v režimu s](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/lob-win32-apps-on-s).
- Další informace o přidávání aplikací do Intune najdete v článku [Přidání aplikací do Microsoft Intune](apps-add.md).
- Další informace o aplikacích Win32 najdete v tématu [Správa aplikací Win32 v Intune](apps-win32-app-management.md).
