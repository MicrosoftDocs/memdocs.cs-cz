---
title: Vzdálená akce s spolusprávou
titleSuffix: Configuration Manager
description: Spuštění vzdálených akcí z Intune pro spoluspravovaná zařízení
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ca37a4e15f5da63ed743b541eeabc43708b0be1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075315"
---
# <a name="remote-actions-with-co-management"></a>Vzdálená akce s spolusprávou

Musíte zajistit, aby každé zařízení, které spravujete, bylo dosažitelné, bez ohledu na to, kde je, kdykoli se připojí. Je také potřeba poskytnout každému uživateli vše, co potřebují k udržení produktivity, a současně chránit aplikace a data. Pomocí akcí zařízení podporovaných službou Intune můžete tyto důležité funkce vzdáleně vyřešit.

V následujícím videu hlavní správce programu Heidi Cheng a vedoucí program Manager Danny Guillory diskutovat a demonstrační vzdálené akce pomocí spolusprávy:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Výhody

Akce se vzdáleným zařízením poskytují ovládací prvky pro správu na zařízení bez rušivého vlivu na osobní údaje. Tyto akce se vzdáleným zařízením umožňují: 
- Odstranění firemních dat na ztracených nebo odcizených zařízeních  
- Přejmenování zařízení  
- Restart zařízení  
- Kontrola inventáře zařízení  
- Vzdálené řízení zařízení  
- Vymazání předem nainstalovaných aplikací od výrobců OEM pomocí nového spuštění restartování  
- Obnovení továrního nastavení v jakémkoli zařízení s Windows 10  

Tyto funkce jsou důležitým a jednoduchým způsobem, jak chránit podniková data uložená na těchto zařízeních, ať už v e-mailu, nebo na OneDrivu.

Další informace o těchto akcích najdete v tématu [dostupné vzdálené akce](#available-remote-actions). 



## <a name="case-studies"></a>Případové studie

Globální konzultační program Avanade pravidelně používá vzdálené akce ke správě zařízení používaných zaměstnanci 30 000. V [nedávný příspěvek blogu](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/)CIO Avanade:

> *Naším okamžitým souborem Win z toho, že funkce Intune byla možnost vzdáleně resetovat Windows na počítači. To je důležité pro ztracené nebo odcizené počítače, které jsou běžnější v našich vysoce mobilních pracovních zařízeních.* 
>  *To je funkce, kterou bychom jinak museli sestavovat a udržovat ve vlastním balíčku nástroje ConfigMgr.*

Další informace o tom, jak tyto vzdálené akce použít, najdete v tématu [Dostupné akce zařízení](../../intune/remote-actions/device-management.md#available-device-actions).


## <a name="value-proposition"></a>Pozice hodnoty

Když se zařízení Configuration Manager spoluspravuje, okamžitě přidá tyto funkce, které Configuration Manager nemají nativně. Nyní teď můžete provádět všechny vzdálené akce, které Intune podporuje. 

V případě spolusprávy se zařízení Configuration Manager nyní stejně jako jiná zařízení spravovaná přes Intune. Například mají úplnou přítomnost v cloudu a můžete je kontaktovat, pokud mají přístup k Internetu. Všechny tyto akce můžete provádět bez nutnosti provádět další kroky nad rámec povolení spolusprávy.

Vzhledem k tomu, že proces automatického zápisu je pro uživatele transparentní, neexistuje žádný vliv na jejich produktivitu. Uživatel nemusí provádět žádné akce.


### <a name="available-remote-actions"></a>Dostupné vzdálené akce

Po [Povolení spolusprávy](how-to-enable.md) v Configuration Manager použijte tyto vzdálené akce z Intune.

#### <a name="remove-devices"></a>Odebrání zařízení
- **Vyřazení**: Tato akce odebere spravované aplikace a data (kde jsou k dispozici), nastavení a e-mailové profily, které byly přiřazeny k tomuto zařízení. Zařízení se pak odebere ze správy Intune. K tomuto procesu dochází při příštím ověření zařízení a přijetí akce vzdálené vyřazení. Funkce vyřadit ze zařízení opustí osobní údaje uživatele.  

- **Vymazání**: Tato akce obnoví zařízení do výchozího továrního nastavení. Pokud zvolíte možnost **zachovat stav registrace a uživatelský účet**, budou se data uživatele uchovávat. V opačném případě bude jednotka bezpečně smazána.  

- **Odstranit**: Pokud chcete zařízení odebrat z Intune na Azure Portal, odstraňte je z konkrétního podokna zařízení. Až se zařízení příště vrátí, odebere všechna data organizace, která jsou v něm uložená.  

Další informace najdete v tématu [odebrání zařízení pomocí vymazání, vyřazení nebo ručnímu zrušení registrace zařízení](../../intune/remote-actions/devices-wipe.md).

#### <a name="selective-wipe"></a>Selektivní vymazání
<!--SCCMDocs issue 973-->
Když zvolíte **selektivní vymazání aplikace**, odstraní se data firemních aplikací bez odebrání osobních údajů. Tuto akci použijte, když se zařízení hlásí jako ztracené nebo odcizené. 

Další informace najdete v tématu [jak vymazat jenom firemní data z aplikací spravovaných přes Intune] (.. /.. /intune/apps/apps-selective-wipe.md.

#### <a name="sync"></a>Sync
Akce zařízení **Synchronizovat** vybrané zařízení donutí se okamžitě ohlásit ve službě Intune. Když se zařízení vrátí se změnami, okamžitě obdrží všechny nedokončené akce nebo zásady, které jste jim přiřadili.

Tato funkce vám může pomoct okamžitě ověřit a řešit potíže se zásadami, které jste přiřadili, aniž byste čekali na další plánované vrácení se změnami.

Další informace najdete v tématu [synchronizace zařízení s cílem získat nejnovější zásady a akce s Intune](../../intune/remote-actions/device-sync.md).

#### <a name="restart"></a>Restartování
Akce **restartovat** zařízení způsobí, že se zařízení rozhodnete restartovat. Tato akce je užitečná v případě, že se čeká na restartování, ale uživatel není k tomu k dispozici.

Další informace najdete v tématu [vzdálené restartování zařízení v Intune](../../intune/remote-actions/device-restart.md).

#### <a name="fresh-start"></a>Začít znovu
Akce zařízení **začít** znovu odebere všechny aplikace nainstalované v zařízení se systémem Windows 10 verze 1703 nebo novějším. Nový start pomáhá odebrat předem nainstalované aplikace (OEM), které se obvykle instalují s novým zařízením.

Pokud se rozhodnete Neuchovávat data uživatelů, zařízení se obnoví do stavu, ve kterém se nachází. Zruší se registrace z Azure AD a MDM.

Pokud jste předem určili, jaké aplikace by měly být na zařízení, pak tato akce eliminuje ty, které nesplňují vaše kritéria.

Další informace najdete v tématu [použití funkce začít znovu k resetování zařízení s Windows 10 pomocí Intune](../../intune/remote-actions/device-fresh-start.md). 

#### <a name="remote-control"></a>Vzdálené řízení
Zařízení spravovaná pomocí Intune je možné spravovat vzdáleně pomocí [TeamVieweru](https://www.teamviewer.com/). TeamViewer je program třetí strany, který získáte samostatně.

Další informace najdete v tématu věnovaném [vzdálené správě zařízení Intune pomocí TeamVieweru](../../intune/remote-actions/teamviewer-support.md).



## <a name="configure"></a>Konfigurace

Kromě vzdáleného řízení přes TeamViewer, aby bylo možné začít používat tyto akce vzdálených zařízení v Intune, není po [Povolení spolusprávy](how-to-enable.md)nutné žádné další nastavení.

Další informace o použití TeamVieweru pro vzdálené řízení najdete v tématu věnovaném [vzdálené správě zařízení Intune pomocí TeamVieweru](../../intune/remote-actions/teamviewer-support.md).
