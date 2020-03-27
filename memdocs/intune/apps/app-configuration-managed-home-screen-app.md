---
title: Konfigurace aplikace pro domovskou obrazovku spravované Microsoftem
titleSuffix: Microsoft Intune
description: Naučte se konfigurovat aplikaci pro domovskou obrazovku spravovanou Microsoftem.
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
ms.assetid: 865c7f03-f525-4dfa-b3a8-d088a9106502
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 45e1d022f4b8d77684e22ec17cd3b1b169a06216
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80323454"
---
# <a name="configure-the-microsoft-managed-home-screen-app-for-android-enterprise"></a>Konfigurace aplikace pro domovskou obrazovku spravované Microsoftem pro Android Enterprise

Spravovaná Domovská obrazovka je aplikace používaná pro podniková vyhrazená podniková zařízení s Androidem registrovaná přes Intune a běžící v celoobrazovkovém režimu s více aplikacemi. Pro tato zařízení spravovaná Domovská obrazovka funguje jako spouštěč pro jiné schválené aplikace, které by měly běžet nad ní. Spravovaná Domovská obrazovka poskytuje správcům IT možnost přizpůsobit si jejich zařízení a omezit možnosti, ke kterým může koncový uživatel přistupovat. 

## <a name="when-to-configure-the-microsoft-managed-home-screen-app"></a>Kdy se má nakonfigurovat aplikace pro domovskou obrazovku spravovanou Microsoftem

Pokud máte k dispozici nastavení prostřednictvím konfigurace zařízení, nakonfigurujte nastavení tady. Tím ušetříte čas, minimalizujete chyby a získáte lepší možnosti podpory pro Intune. Některá nastavení spravované domovské obrazovky jsou ale v tuto chvíli dostupná jenom přes podokno **zásady konfigurace aplikace** v konzole Intune. Pomocí tohoto dokumentu se dozvíte, jak nakonfigurovat různá nastavení pomocí návrháře konfigurace nebo skriptu JSON. 

> [!NOTE]
> V současné době je možné nastavit povolené aplikace a připnuté webové odkazy prostřednictvím **aplikací** a **Konfigurace zařízení**. Úplný seznam nastavení dostupných v **konfiguraci zařízení** , který se týká spravované domovské obrazovky, najdete v tématu [vyhrazené nastavení zařízení](../configuration/device-restrictions-android-for-work.md#dedicated-device-settings).  

Nejdřív přejděte do centra pro [správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte **aplikace** **zásady konfigurace aplikací** > . Přidejte zásady konfigurace pro **spravovaná zařízení** s **Androidem** a jako přidruženou aplikaci vyberte **spravovaná Domovská obrazovka** . Kliknutím na **nastavení konfigurace** můžete nakonfigurovat různá dostupná nastavení spravovaných domácích obrazovek. 

## <a name="choosing-a-configuration-settings-format"></a>Výběr formátu nastavení konfigurace

Existují dvě metody, které můžete použít k definování nastavení konfigurace pro spravovanou domovskou obrazovku:

- **Configuration Designer** umožňuje nakonfigurovat nastavení pomocí snadno POUŽITELNÉHO uživatelského rozhraní, které umožňuje přepínat a nastavovat funkce a nastavit hodnoty. V této metodě je k dispozici několik zakázaných konfiguračních klíčů s typem hodnoty `BundleArray`. Tyto konfigurační klíče lze nakonfigurovat pouze zadáním dat JSON. 
- **Data JSON** umožňují definovat všechny možné konfigurační klíče pomocí skriptu JSON. 

Pokud přidáte vlastnosti pomocí návrháře konfigurace, můžete tyto vlastnosti automaticky převést na JSON výběrem možnosti **zadat data JSON** z rozevíracího seznamu **formát nastavení konfigurace** .

![Snímek obrazovky s možnostmi formátu nastavení konfigurace](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_01.png)

## <a name="using-configuration-designer"></a>Použití návrháře konfigurace

Návrhář konfigurace umožňuje vybrat předem vyplněná nastavení a jejich přidružené hodnoty. 

![Snímek obrazovky s přidaným nastavením konfigurace](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_02.png)

Následující tabulka uvádí seznam dostupných konfiguračních klíčů, hodnot typu, výchozích hodnot a popisů spravovaných na domovské obrazovce. Popis poskytuje očekávané chování zařízení na základě vybraných hodnot. Konfigurační klíče, které jsou zakázány v Návrháři konfigurace, nejsou uvedeny v tabulce.

| Konfigurační klíč | Typ hodnoty | Výchozí hodnota | Popis |
|---------------------------------------------------------------------------------------------------------------------------|-------------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nastavit velikost mřížky | string | Autom. | Umožňuje nastavit velikost mřížky pro aplikace, které mají být umístěny na spravované domovské obrazovce. Počet řádků a sloupců aplikace můžete nastavit tak, aby se definovala velikost mřížky v následujícím formátu `columns;rows`. Pokud definujete velikost mřížky, maximální počet aplikací, které se zobrazí na řádku na domovské obrazovce, bude počet řádků, které jste nastavili, a maximální počet aplikací, které se zobrazí ve sloupci na domovské obrazovce, bude počet sloupců, které jste nastavili. |
| Povolit oznámení | logick | CHYBNÉ | Povolí oznamovací označení pro ikony aplikací, které zobrazují počet nových oznámení v aplikaci. Pokud povolíte toto nastavení, koncovým uživatelům se zobrazí oznámení o oznámeních v aplikacích, které mají nepřečtená oznámení. Pokud tento konfigurační klíč zachováte, koncovému uživateli se nezobrazí žádná oznámení, která by mohla obsahovat nepřečtená oznámení. |
| Uzamknout domovskou obrazovku | logick | PRAVDA | Odebere koncovému uživateli možnost pohybovat se přes ikony aplikace na domovské obrazovce. Pokud povolíte tento konfigurační klíč, ikony aplikace na domovské obrazovce budou uzamčené a koncový uživatel nebude moct přetahovat do různých pozic mřížky na domovské obrazovce. Pokud je `false`, koncoví uživatelé se budou moci pohybovat na stránce spravovaná Domovská obrazovka na ikonu aplikace a Weblink.  |
| Nastavit papír na zeď zařízení | string | Výchozí | Umožňuje nastavit tapetu podle vlastního výběru zadáním adresy URL obrázku, který chcete nastavit jako tapetu. |
| Nastavit velikost ikony aplikace | celé číslo | 2 | Umožňuje nastavit velikost ikon pro aplikace zobrazené na domovské obrazovce. V této konfiguraci můžete zvolit následující hodnoty pro různé velikosti – 0 (nejmenší), 1 (malé), 2 (Regular), 3 (Velká) a 4 (největší). |
| Ikona nastavení složky aplikace | celé číslo | 0 | Umožňuje definovat vzhled složek aplikace na domovské obrazovce. Můžete zvolit vzhled z následujících hodnot: tmavě čtvercová (0);   Tmavý kroužek (1); Světlá čtvercová (2); Světlý kroužek (3). |
| Nastavení orientace obrazovky | celé číslo | 1 | Umožňuje nastavit orientaci obrazovky domů na režim na výšku, v režimu na šířku nebo povolit automatické otočení. Orientaci můžete nastavit tak, že zadáte hodnoty 1 (pro režim na výšku), 2 (pro režim na šířku), 3 (pro automatické otáčení). |
| Povolit telemetrii zařízení | logick | CHYBNÉ | Povolí veškerou telemetrii, která je zachycena pro spravovanou domovskou obrazovku. Pokud tuto možnost povolíte, Microsoft bude moct zachytit telemetrii využití zařízení, například počet, kolikrát se na tomto zařízení spustí konkrétní aplikace. |
| Nastavit povolené aplikace v seznamu | BundleArray | CHYBNÉ | Umožňuje definovat sadu aplikací, které jsou viditelné na domovské obrazovce z aplikací nainstalovaných v zařízení. Aplikace můžete definovat tak, že zadáte název balíčku aplikace, který chcete zviditelnit, například com. Microsoft. emmx by měl přístup k nastavení na domovské obrazovce. Aplikace, které povolíte – seznam v této části, by už měly být na zařízení nainstalované, aby je bylo možné zobrazit na domovské obrazovce. |
| Nastavit připnuté webové odkazy | BundleArray | CHYBNÉ | Umožňuje připnout weby jako ikony snadného spuštění na domovské obrazovce. Pomocí této konfigurace můžete definovat adresu URL a přidat ji na domovskou obrazovku, aby se koncový uživatel spouštěl v prohlížeči jediným klepnutím. |
| Povolit šetřič obrazovky | logick | CHYBNÉ | Pro povolení režimu spořiče obrazovky, nebo ne. Pokud je nastavená hodnota true, můžete nakonfigurovat **screen_saver_image**, **screen_saver_show_time**, **inactive_time_to_show_screen_saver**a **media_detect_screen_saver**. |
| Obrázek spořiče obrazovky | string |   | Nastavte adresu URL obrázku spořiče obrazovky. Pokud není nastavená žádná adresa URL, zařízení zobrazí výchozí obrázek spořiče obrazovky, když se aktivuje šetřič obrazovky. Výchozí obrázek zobrazuje ikonu spravované aplikace na domovské obrazovce.  |
| Spořič obrazovky – zobrazit čas | celé číslo | 0 | Poskytuje možnost nastavit dobu v sekundách, po kterou zařízení zobrazí spořič obrazovky v režimu spořiče obrazovky. Pokud je nastavené na 0, spořič obrazovky se zobrazí v režimu spořiče obrazovky, dokud se zařízení neaktivuje.  |
| Neaktivní čas pro povolení spořiče obrazovky | celé číslo | 30 | Doba v sekundách, po kterou je zařízení neaktivní, než se aktivuje šetřič obrazovky. Pokud je nastavené na 0, zařízení nebude nikdy přejít do režimu spořiče obrazovky. |
| Detekce multimédií před zobrazením spořiče obrazovky | logick | PRAVDA | Vyberte, jestli má obrazovka zařízení zobrazovat spořič obrazovky, pokud se na zařízení přehrává zvuk/video. Pokud je nastaveno na true, zařízení nebude přehrávat zvuk/video bez ohledu na hodnotu v **inactive_time_to_show_scree_saver**. Pokud je nastaveno na false, obrazovka zařízení zobrazí spořič obrazovky podle hodnoty nastavené v **inactive_time_to_show_screen_saver**.   |
| Tlačítko Povolit virtuální domů | logick | CHYBNÉ | Toto nastavení povolte `True`, pokud chcete, aby měl koncový uživatel přístup k domovskému tlačítku spravované domovské obrazovky, který vrátí uživatele do spravované domovské obrazovky z aktuální úlohy, ve které se nachází.  |
| Typ virtuálního tlačítka Domů | string | swipe_up | Pro přístup k tlačítku Domů pomocí gesta potáhnutí nahoru použijte **swipe_up** . Pomocí **typu float** získáte přístup k rychlému a trvalému domovskému tlačítku, které lze přesunout kolem obrazovky koncovým uživatelem. |
| Indikátor síly baterie a signálu | logick | True  | Když toto nastavení zapnete, `True` se zobrazí indikátor indikátoru síly baterie a signálu. |
| Ukončit uzamčení hesla režimu úlohy | string |   | Zadejte kód 4-6, který se má použít k dočasnému vyřazení režimu uzamčení úlohy pro řešení potíží. |
| Zobrazit nastavení Wi-Fi | logick | CHYBNÉ | Zapnutím tohoto nastavení `True` umožníte koncovému uživateli zapnout nebo vypnout Wi-Fi nebo se připojit k jiným sítím Wi-Fi.  |
| Zobrazit nastavení Bluetooth | logick | CHYBNÉ | Zapnutím tohoto nastavení `True` umožníte koncovému uživateli zapnout nebo vypnout Bluetooth a připojit se k různým zařízením podporujícím Bluetooth.   |
| Aplikace ve složce jsou seřazené podle názvu | logick | PRAVDA | Zapnutím tohoto nastavení `False` umožníte, aby se položky ve složce zobrazovaly v pořadí, ve kterém jsou určené. V opačném případě se zobrazí ve složce abecedně.   |
| Pořadí aplikací povoleno | logick | CHYBNÉ | Zapnutím tohoto nastavení `True` povolíte možnost nastavit pořadí aplikací, weblinks a složek na spravované domovské obrazovce. Po povolení nastavte řazení pomocí **app_order**. koncový uživatel zapíná nebo vypíná Bluetooth a připojovat se k různým zařízením podporujícím technologii Bluetooth.   |
| Pořadí aplikací | BundleArray | CHYBNÉ | Umožňuje zadat pořadí aplikací, weblinks a složek na spravované domovské obrazovce. Chcete-li použít toto nastavení, musí být povoleno **uzamknutí domovské obrazovky** , musí být definována **Velikost mřížky** a **povolený pořadí aplikace** musí být nastaveno na hodnotu `True`.   |

## <a name="enter-json-data"></a>Zadat data JSON

Zadejte data JSON pro konfiguraci všech dostupných nastavení pro spravovanou domovskou obrazovku a také nastavení zakázaná v **Návrháři konfigurace**.

![Snímek obrazovky s přidanými daty JSON](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_03.png)

Kromě seznamu konfigurovatelných nastavení uvedených v tabulce **Návrháře konfigurace** (výše) poskytují následující tabulka konfigurační klíče, které lze konfigurovat pouze prostřednictvím dat JSON.

|    Konfigurační klíč    |    Typ hodnoty    |    Výchozí hodnota    |    Popis    |
|-------------------------------------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Nastavit povolené aplikace v seznamu    |    BundleArray    | <img alt="JSON - Example 1" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson01.png" width="300"> |    Umožňuje definovat sadu aplikací, které jsou viditelné na domovské obrazovce z aplikací nainstalovaných v zařízení. Aplikace můžete definovat tak, že zadáte název balíčku aplikace, který chcete zviditelnit, například com. Android. Settings by nastavení mělo být dostupné na domovské obrazovce. Aplikace, které povolíte – seznam v této části, by už měly být na zařízení nainstalované, aby je bylo možné zobrazit na domovské obrazovce.    |
|    Nastavit připnuté webové odkazy    |    BundleArray    | <img alt="JSON - Example 2" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson02.png" width="300"> |    Umožňuje připnout weby jako ikony snadného spuštění na domovské obrazovce. Pomocí této konfigurace můžete definovat adresu URL a přidat ji na domovskou obrazovku, aby se koncový uživatel spouštěl v prohlížeči jediným klepnutím.    |
|    Vytvoření spravované složky pro seskupování aplikací    |    BundleArray    | <img alt="JSON - Example 3" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson03.png" width="300"> |    Umožňuje vytvářet a pojmenovat složky a seskupit aplikace v těchto složkách. Koncoví uživatelé nebudou moci přesouvat složky, přejmenovávat složky ani přesouvat aplikace v rámci složek.   Složky se zobrazí ve vytvořeném pořadí a aplikace ve složkách se zobrazí abecedně.         Poznámka: všechny aplikace, které chcete seskupovat do složek, se musí přiřadit k zařízení, které je potřeba, a musí být přidané do spravované domovské obrazovky.     |

Následující příklad obsahuje ukázkový skript JSON se všemi dostupnými konfiguračními klíči:

```json
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "com.microsoft.launcher.enterprise",
    "managedProperty": [
        {
            "key": "lock_home_screen",
            "valueBool": true
        },
        {
            "key": "wallpaper",
            "valueString": "default"
        },
        {
            "key": "icon_size",
            "valueInteger": 2
        },
        {
            "key": "app_folder_icon",
            "valueInteger": 0
        },
        {
            "key": "screen_orientation",
            "valueInteger": 1
        },
        {
            "key": "enable_telemetry",
            "valueBool": false
        },
        {
            "key": "applications",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": “app package name here”
                        }
                    ]
                }
            ]
        },
        {
            "key": "weblinks",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "link",
                            "valueString": “link here”
                        },
                        {
                            "key": "label",
                            "valueString": “weblink label here”
                        }
                    ]
                }
            ]
        },
        {
            "key": "show_virtual_home",
            "valueBool": false
        },
        {
            "key": "virtual_home_type",
            "valueString": "swipe_up"
        },
        {
            "key": "show_virtual_status_bar",
            "valueBool": true
        },
        {
            "key": "exit_lock_task_mode_code",
            "valueString": ""
        },
        {
            "key": "show_wifi_setting",
            "valueBool": false
        },
        {
            "key": "show_bluetooth_setting",
            "valueBool": false
        },
        {
            "key": "grid_size",
            "valueString": "4;5"
        },
        {
            "key": "app_order_enabled",
            "valueBool": true
        },
        {
            "key": "apps_in_folder_ordered_by_name",
            "valueBool": true
        },
        {
            "key": "app_orders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.Microsoft.emmx"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 1
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Work"
                        },
                        {
                            "key": "type",
                            "valueString": "managed_folder"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 2
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.microsoft.launcher.enterprise"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "class",
                            "valueString": "com.microsoft.launcher.launcher"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 3
                        }
                    ]
                }
            ]
        },
        {
            "key": "managed_folders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Folder name here"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.emmx"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.bing"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "link",
                                            "valueString": "https://microsoft.com/"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Example folder name 2"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.office.word"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="googles-android-device-policy-app"></a>Aplikace zásad zařízení pro Android Google
Aplikace spravované domovské obrazovky teď poskytuje přístup k aplikaci zásad zařízení s Androidem. Spravovaná aplikace pro domovskou obrazovku je vlastní spouštěč používaný pro zařízení zaregistrovaná v Intune jako vyhrazená zařízení Android Enterprise (AE) pomocí celoobrazovkového režimu s více aplikacemi. K aplikaci zásad pro zařízení s Androidem můžete získat přístup, nebo se uživatelé k aplikaci zásad zařízení s Androidem pořídit pro účely podpory a ladění. Tato funkce je k dispozici v době, kdy se zařízení zaregistruje a zamkne do spravované domovské obrazovky. K použití této funkce nejsou potřeba žádné další instalace.

## <a name="managed-home-screen-debug-screen"></a>Obrazovka pro ladění spravované domovské obrazovky
Kliknutím na tlačítko **zpět** můžete získat přístup k obrazovce ladění spravované domovské obrazovky (klikněte na **tlačítko zpět a** prodloužit). Z této obrazovky pro ladění můžete spustit aplikaci zásad zařízení s Androidem, zobrazit a nahrát protokoly nebo dočasně pozastavit beznabídkový režim, aby bylo možné zařízení aktualizovat. Další informace o pozastavení celoobrazovkového režimu najdete v části **opuštění celoobrazovkového režimu** v [nastavení zařízení](../configuration/device-restrictions-android-for-work.md#dedicated-device-settings)v systému Android Enterprise vyhrazené.

## <a name="next-steps"></a>Další kroky

- Další informace o vyhrazených zařízeních s Androidem Enterprise najdete v tématu [Nastavení registrace Intune u vyhrazených zařízení s Androidem Enterprise](../enrollment/android-kiosk-enroll.md).
