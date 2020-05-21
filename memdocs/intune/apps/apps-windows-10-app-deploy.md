---
title: Nasazení aplikací pro Windows 10 pomocí Microsoft Intune
titleSuffix: ''
description: Přečtěte si o scénářích nasazení aplikací pro Windows 10, které jsou dostupné v Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: abebfb5e-054b-435a-903d-d1c31767bcf2
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f06a6d6689107c97a80e11149da499ccd51fa755
ms.sourcegitcommit: 6ca5e75ed7a6fd2186fbe51c177960004d5ec81f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/19/2020
ms.locfileid: "83633301"
---
# <a name="windows-10-app-deployment-by-using-microsoft-intune"></a>Nasazení aplikací pro Windows 10 pomocí Microsoft Intune 

Microsoft Intune podporuje různé typy aplikací a scénáře nasazení na zařízeních s Windows 10. Po přidání aplikace do Intune ji můžete přiřadit uživatelům a zařízením. Tento článek obsahuje další informace o podporovaných scénářích Windows 10 a také obsahuje důležité informace, které je třeba poznamenat při nasazování aplikací do systému Windows. 

Obchodní aplikace (LOB) a aplikace pro Microsoft Store pro firmy jsou na zařízeních s Windows 10 podporované. Mezi přípony souborů aplikací pro Windows patří .msi, .appx a .appxbundle.  

> [!Note]
> K nasazení moderních aplikací potřebujete aspoň tyto:
> - Pro Windows 10 1803: [KB4100403 z 23. května 2018 (číslo sestavení operačního systému 17134.81)](https://support.microsoft.com/help/4100403/windows-10-update-kb4100403)
> - Pro Windows 10 1709: [KB4284822 z 21. června 2018 (číslo sestavení operačního systému 16299.522)](https://support.microsoft.com/help/4284822)
>
> Jenom Windows 10 1803 a novější podporují instalaci aplikací, když není přidružený žádný primární uživatel.
>
> Nasazení aplikace LOB se nepodporuje na zařízeních s Windows 10 Home Edition.

## <a name="supported-windows-10-app-types"></a>Podporované typy aplikací pro Windows 10

Konkrétní typy aplikací jsou podporované v závislosti na verzi Windows 10, kterou používají vaši uživatelé. Následující tabulka uvádí typ aplikace a podporu Windows 10.

| Typ aplikace | Domů | Verze Pro | Do zaměstnání | Enterprise | Vzdělávání | S-režim | HoloLens <sup> 1 | Surface Hub | WCOS | Mobilní |
|----------------|------|-----|----------|------------|-----------|--------|-----------|------------|------|--------|
|  . SOUBOR | No | Ano | Ano | Ano | Ano | Ne | Ne | Ne | Ne | Ne |
| . IntuneWin | No | Ano | Ano | Ano | Ano | 19H2 + | Ne | Ne | Ne | Ne |
| C2R Office | No | Ano | Ano | Ano | Ano | RS4 + | Ne | Ne | Ne | Ne |
| LOB: APPX/MSIX | Ano | Ano | Ano | Ano | Ano | Ano | Ano | Ano | Ano | Ano |
| MSFB offline | Ano | Ano | Ano | Ano | Ano | Ano | Ano | Ano | Ano | Ano |
| MSFB online | Ano | Ano | Ano | Ano | Ano | Ano | RS4 + | No | Ano | Ano |
| Web Apps | Ano | Ano | Ano | Ano | Ano | Ano | Ano<sup>2 | Ano<sup>2 | Ano | Ano<sup>2 |
| Odkaz na Store | Ano | Ano | Ano | Ano | Ano | Ano | Ano | Ano | Ano | Ano |
| Microsoft Edge | No | Ano | Ano | Ano | Ano | 19H2 + <sup> 3 | Ne | Ne | Ne | Ne |

<sup>1</sup> Chcete-li odemknout správu aplikací, Upgradujte své zařízení HoloLens na [holografické pro firmy](../fundamentals/windows-holographic-for-business.md).<br />
<sup>2</sup> spustit pouze z portál společnosti.<br />
<sup>3</sup> aby se aplikace Edge mohla nainstalovat úspěšně, musí být zařízení přiřazená taky zásada pro režim S.

> [!NOTE]
> Všechny typy aplikací pro Windows vyžadují registraci.

## <a name="windows-10-lob-apps"></a>Obchodní aplikace pro Windows 10

Do konzoly pro správu Intune můžete podepisovat a nahrávat obchodní aplikace pro Windows 10. Ty můžou zahrnovat moderní aplikace, jako jsou aplikace Univerzální platforma Windows (UWP) a balíčky aplikací pro Windows (AppX), a také aplikace pro Win 32, jako jsou například jednoduché soubory balíčku Instalační služby společnosti Microsoft (MSI). Správce musí ručně nahrávat a nasazovat aktualizace obchodních aplikací. Tyto aktualizace se automaticky nainstalují na uživatelská zařízení, ve kterých je nainstalovaná aplikace. Není vyžadován žádný zásah uživatele a uživatel nemá žádnou kontrolu nad aktualizacemi. 

## <a name="microsoft-store-for-business-apps"></a>Aplikace z Microsoft Storu pro firmy

Microsoft Store pro obchodní aplikace jsou moderní aplikace zakoupené na portálu pro správu Microsoft Store pro firmy. Pak se synchronizují s Microsoft Intune pro správu. Tyto aplikace mohou mít online licenci nebo offline licenci. Microsoft Store přímo spravuje aktualizace bez dalších akcí, které správce vyžaduje. Aktualizace konkrétních aplikací můžete také zabránit pomocí vlastního identifikátoru URI (Uniform Resource Identifier). Další informace najdete v tématu o [správě podnikových aplikací a zabránění jejich automatické aktualizace](https://docs.microsoft.com/windows/client-management/mdm/enterprise-app-management#prevent-app-from-automatic-updates). Uživatel může také zakázat aktualizace pro všechny Microsoft Store pro obchodní aplikace na zařízení. 

### <a name="categorize-microsoft-store-for-business-apps"></a>Kategorizace Microsoft Store pro obchodní aplikace 
Kategorizace Microsoft Store pro obchodní aplikace: 

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **všechny aplikace**. 
3. Vyberte Microsoft Store pro obchodní aplikaci. Pak vyberte **vlastnosti**  >  **kategorie informací o aplikaci**  >  **Category**. 
4. Vyberte kategorii.

## <a name="install-apps-on-windows-10-devices"></a>Instalace aplikací na zařízení s Windows 10
V závislosti na typu aplikace můžete aplikaci nainstalovat na zařízení s Windows 10 jedním ze dvou způsobů:

- **Kontext uživatele**: když se aplikace nasadí v uživatelském kontextu, nainstaluje se tato spravovaná aplikace pro daného uživatele na zařízení, když se uživatel přihlásí k zařízení. Všimněte si, že instalace aplikace neproběhne úspěšně, dokud se uživatel přihlásí k zařízení. 
  - Moderní obchodní aplikace a aplikace Microsoft Store pro firmy (online i offline) se dají nasadit v kontextu uživatele. Aplikace podporují požadovaný i dostupný záměr.
  - Aplikace Win32 sestavené jako uživatelský režim nebo duální režim lze nasadit v kontextu uživatele a podporují jak požadované, tak i dostupné záměry. 
- **Kontext zařízení**: při nasazení aplikace v kontextu zařízení se spravovaná aplikace nainstalují přímo do zařízení pomocí Intune.
  - V kontextu zařízení se dají nasadit jenom moderní obchodní aplikace a offline licencované Microsoft Store pro podnikové aplikace. Tyto aplikace podporují jenom požadovaný záměr.
  - Aplikace Win32 sestavené jako režim počítače nebo duální režim mohou být nasazeny v kontextu zařízení a podporují pouze požadovaný záměr.

> [!NOTE]
> Pro aplikace Win32 sestavené jako aplikace v duálním režimu musí správce zvolit, jestli bude aplikace fungovat jako uživatelský režim nebo aplikace v režimu počítače pro všechna přiřazení přidružená k této instanci. Kontext nasazení nejde změnit na přiřazení.  

Aplikace se dají instalovat jenom v kontextu zařízení, když je podporuje zařízení a typ aplikace Intune. Instalace kontextu zařízení se podporují na zařízeních s Windows 10 desktops a teams, jako je Surface Hub. Nepodporují se na zařízeních s Windows holografickým pro firmy, jako je například Microsoft HoloLens.

V kontextu zařízení můžete nainstalovat následující typy aplikací a přiřadit tyto aplikace ke skupině zařízení:

- Aplikace Win32
- Offline licencované Microsoft Store pro obchodní aplikace
- Obchodní aplikace (MSI, APPX a MSIX)
- Aplikace Microsoft 365 pro podniky

Aplikace LOB pro Windows (konkrétně APPX a MSIX) a Microsoft Store pro firmy (offline aplikace), které jste vybrali k instalaci v kontextu zařízení, musí být přiřazené ke skupině zařízení. Instalace se nezdařila, pokud je jedna z těchto aplikací nasazena v uživatelském kontextu. V konzole pro správu se zobrazí následující stav a chyba:
  - Stav: Neúspěšné.
  - Chyba: uživatel se nemůže zaměřit na instalaci kontextu zařízení.

> [!IMPORTANT]
> Při použití v kombinaci s prázdným scénářem pro šetrnější zřizování autopilotu neexistuje žádný požadavek na obchodní aplikace a Microsoft Store pro podnikové aplikace nasazené v kontextu zařízení pro účely cílení na skupinu zařízení. Další informace najdete v tématu [nasazení White šetrnější (Windows autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove)) pro Windows.

> [!Note]
> Po uložení přiřazení aplikace pomocí konkrétního nasazení nemůžete změnit kontext tohoto přiřazení, s výjimkou moderních aplikací. Pro moderní aplikace můžete změnit kontext z kontextu uživatele na kontext zařízení. 

Pokud dojde ke konfliktu v zásadách pro jednoho uživatele nebo zařízení, platí následující priority:
- Zásady kontextu zařízení mají vyšší prioritu než zásady kontextu uživatele. 
- Zásady instalace mají vyšší prioritu než zásady odinstalace.

Podrobnosti najdete v tématu [Zahrnutí a vyloučení přiřazení aplikací v Microsoft Intune](apps-inc-exl-assignments.md). Další informace o typech aplikací v Intune najdete v tématu [Přidání aplikací do Microsoft Intune](apps-add.md).

## <a name="next-steps"></a>Další kroky

- [Přiřazení aplikací do skupin pomocí Microsoft Intune](apps-deploy.md)
- [Jak monitorovat aplikace](apps-monitor.md)
