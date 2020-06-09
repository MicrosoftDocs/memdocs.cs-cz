---
title: Začínáme s nastavením dodržování předpisů
titleSuffix: Configuration Manager
description: Přečtěte si o základních konceptech a o tom, jak funguje nastavení dodržování předpisů
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f0a26d02770ff8460787ee9897bdc8f1218a2c12
ms.sourcegitcommit: 7f542c97ac55bbd329f5befda97d671213c24e9a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/08/2020
ms.locfileid: "84506158"
---
# <a name="get-started-with-compliance-settings-in-configuration-manager"></a>Začínáme s nastavením dodržování předpisů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Než začnete vytvářet nastavení dodržování předpisů Configuration Manager, nejdřív se seznamte s základními koncepty a pochopte, jak fungují.  



## <a name="how-compliance-settings-work"></a>Jak funguje nastavení dodržování předpisů  
Nastavení dodržování předpisů vám umožní spravovat konfiguraci a dodržování předpisů klientů ve vaší organizaci.  

Položky konfigurace se dělí do dvou hlavních kategorií:  

- **Nastavení pro zařízení, která jsou spravovaná pomocí Configuration Manager klienta** – obvykle zařízení, na kterých jste nainstalovali Configuration Manager klientského softwaru, abyste mohli zařízení spravovat.  

- **Nastavení pro zařízení, která jsou spravovaná bez Configuration Manager klienta** , obvykle spravovaná pomocí Microsoft Intune nebo se správou Configuration Manager místních zařízení.  



## <a name="what-devices-are-supported"></a>Jaká zařízení jsou podporovaná?  

| Typ zařízení | Další informace |  
|------------|----------------------|  
| Počítače s Windows (s klientem Configuration Manager) | Vytvořte vlastní položky konfigurace pro vyhodnocení objektů, jako jsou klíče registru, soubory a atributy služby Active Directory.<br /><br /> Když použijete typ položky konfigurace Windows 10, vyberte nastavení z předdefinovaného seznamu. |  
| Počítače s Windows (zaregistrované v místní MDM) | Vyberte nastavení z předdefinovaného seznamu. |  
| Zařízení Windows Phone (zaregistrovaná v místní MDM) | Vyberte nastavení z předdefinovaného seznamu. |  
| Počítače Mac (s klientem Configuration Manager) | Vytvořte vlastní položky konfigurace pro vyhodnocení objektů, jako jsou macOS předvolby a výsledky vrácené skriptem. |  



## <a name="what-is-a-configuration-item"></a>Co je položka konfigurace?  
Položka konfigurace je kontejner, který ukládá konkrétní informace. Informace, které nakonfigurujete, závisí na typu položky konfigurace. Položky konfigurace mohou obsahovat následující informace:

- **Informace o metodách detekce** jsou jenom pro položky konfigurace systému Windows, které obsahují nastavení aplikace. Zjišťuje, jestli je aplikace nainstalovaná. Tato detekce používá soubor Instalační služby systému Windows pro aplikaci nebo pomocí vlastního skriptu.  

- **Nastavení** představuje obchodní nebo technické podmínky pro vyhodnocení dodržování předpisů na klientských zařízeních. Nakonfigurovat nové nastavení nebo přejít na existující nastavení v referenčním počítači.  

- **Pravidla dodržování předpisů** určují podmínky, které definují dodržování předpisů u nastavení položky konfigurace. Předtím, než klient vyhodnotí nastavení pro dodržování předpisů, musí mít alespoň jedno pravidlo dodržování předpisů. Některá nastavení napravují nekompatibilní hodnoty. Vytvořit nová pravidla nebo přejít na existující nastavení v libovolné položce konfigurace a vybrat pravidla v ní.  

- **Podporované platformy** jsou platformy zařízení, které definujete, na kterých klient vyhodnocuje dodržování předpisů v položkách konfigurace. Pokud položku konfigurace nasadíte do zařízení, které není v seznamu podporovaných platforem, nevyhodnotí se dodržování předpisů.  



## <a name="what-is-a-configuration-baseline"></a>Co jsou standardní hodnoty konfigurace?  
Definujte standardní hodnoty konfigurace, které obsahují položky konfigurace, které se mají vyhodnotit. Také zahrňte nastavení a pravidla, která popisují požadovanou úroveň dodržování předpisů. Importujte Tato konfigurační data z Configuration Manager konfigurační balíčky. Tyto konfigurační balíčky definuje společnost Microsoft a jiní dodavatelé. Nebo vytvořte nové položky konfigurace a standardní hodnoty konfigurace.  

Po definování standardních hodnot konfigurace je můžete nasadit do kolekcí uživatelů a zařízení. Klient pak vyhodnotí základní nastavení pro dodržování předpisů podle plánu. Do zařízení můžete nasadit více než jednu standardní hodnotu konfigurace. Tato členitost nabízí větší kontrolu nad dodržováním předpisů. 

Klientská zařízení vyhodnocují dodržování předpisů na základě všech nasazených standardních hodnot konfigurace a výsledky okamžitě hlásí lokalitě pomocí stavových zpráv. Pokud je zařízení aktuálně odpojeno od sítě, ale stáhlo standardní hodnoty konfigurace, vyhodnotí se tím dodržování předpisů u položek konfigurace. Po opětovném připojení pošle informace o kompatibilitě.  

### <a name="monitoring-configuration-baselines"></a>Monitorování standardních hodnot konfigurace
- Výsledky vyhodnocení dodržování předpisů Sledujte v konzole Configuration Manager v pracovním prostoru **monitorování** v uzlu **nasazení** . Příklad:
  - Běžné příčiny nedodržení předpisů
  - chyby
  - Počet ovlivněných uživatelů a zařízení
- Spustit sestavy nastavení dodržování předpisů s dalšími podrobnostmi. Příklad:
  - Která zařízení splňují nebo nesplňují předpisy
  - Který prvek standardních hodnot konfigurace způsobuje, že počítač není kompatibilní.
- Zobrazí výsledky vyhodnocení dodržování předpisů z počítačů s Windows, na kterých běží klient Configuration Manager. Otevřete ovládací panel **Configuration Manager** a přepněte na kartu **Konfigurace** .  



## <a name="user-data-and-profiles-configuration-items"></a>Položky konfigurace uživatelských dat a profilů  
Položky konfigurace pro profily a data uživatelů zahrnují nastavení, které řídí, jak uživatelé v počítačích se systémem Windows 8 a novějším spravují:  
- Přesměrování složek
- Offline soubory
- Profily roamingu  

Nasaďte tyto položky konfigurace do kolekcí uživatelů. Monitorujte jejich dodržování předpisů z uzlu **monitorování** konzoly Configuration Manager. Na rozdíl od jiných položek konfigurace je před nasazením přidejte do standardních hodnot konfigurace. Nasaďte je přímo kliknutím na **nasadit** na pásu karet.  

Další informace najdete v tématu [Vytvoření položek konfigurace profilů a dat uživatele](../deploy-use/create-user-data-and-profiles-configuration-items.md).  



## <a name="remote-connection-profiles"></a>Profily vzdáleného připojení  
Profily vzdáleného připojení poskytují sadu nástrojů a prostředků, které vám pomůžou vytvořit, nasadit a monitorovat nastavení vzdáleného připojení. Nasazením těchto nastavení do zařízení minimalizujete úsilí, které koncoví uživatelé potřebují k připojení svých počítačů k podnikové síti.  

Další informace najdete v tématu [vytváření profilů vzdáleného připojení](../deploy-use/create-remote-connection-profiles.md).  



## <a name="windows-edition-upgrade"></a>Upgrade edice Windows
Zásady upgradu edice automaticky upgradují zařízení, na kterých běží některé verze Windows 10, na novější edici. Tato zásada poskytuje nový kód Product Key nebo soubor s licencí, který zařízení spotřebovává k upgradu.

Další informace najdete v tématu [upgrade zařízení s Windows pomocí zásad upgradu edice](../deploy-use/upgrade-windows-version.md) .

## <a name="microsoft-edge-legacy-browser-profiles"></a>Profily prohlížeče starší verze Microsoft Edge
<!-- 1357310 -->
Pro zákazníky, kteří používají [starší verzi webového prohlížeče Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/) v klientech Windows 10, vytvořte Configuration Manager zásady dodržování předpisů pro konfiguraci nastavení prohlížeče.

Další informace najdete v tématu [profily prohlížeče starší verze Microsoft Edge](../deploy-use/browser-profiles.md).
