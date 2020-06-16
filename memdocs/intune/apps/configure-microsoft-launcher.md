---
title: Konfigurace spouštěče Microsoft pro Android Enterprise s Intune
titleSuffix: ''
description: Použijte zásady konfigurace Intune s spouštěčem Microsoftu.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 09ebf7fde0cedb907e105e42abe7338237d231af
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795699"
---
# <a name="configure-microsoft-launcher"></a>Konfigurace Microsoft Launcheru

Spouštěč Microsoftu je aplikace pro Android, která uživatelům umožňuje přizpůsobit svůj telefon, zůstat uspořádaná na cestách a přenos z provozu z telefonu na svůj počítač. 

Na zařízeních s plnou správou Androidu Enterprise umožňuje spouštěč podnikových správců IT přizpůsobit si domovské obrazovky spravovaných zařízení tím, že vybere jeho tapetu, aplikace a umístění ikon. To standardizovat vzhled a chování všech spravovaných zařízení s Androidem v různých zařízeních OEM a verzích systému. 

## <a name="how-to-configure-the-microsoft-launcher-app"></a>Konfigurace aplikace spouštěče Microsoft 

Po přidání aplikace spouštěče Microsoft [do Intune](../apps/apps-add.md)přejděte do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte **aplikace**  >  **zásady konfigurace**aplikací. Přidejte zásady konfigurace pro **spravovaná zařízení** s **Androidem** a jako přidruženou aplikaci vyberte **spouštěč Microsoftu** . Kliknutím na **nastavení konfigurace** můžete nakonfigurovat různá dostupná nastavení spouštěče Microsoftu. 

## <a name="choosing-a-configuration-settings-format"></a>Výběr formátu nastavení konfigurace 

Existují dvě metody, které můžete použít k definování nastavení konfigurace pro spouštěč Microsoftu: 

- **Configuration Designer** umožňuje nakonfigurovat nastavení pomocí snadno POUŽITELNÉHO uživatelského rozhraní, které umožňuje přepínat a nastavovat funkce a nastavit hodnoty. V této metodě je k dispozici několik zakázaných konfiguračních klíčů s typem hodnoty BundleArray. Tyto konfigurační klíče lze nakonfigurovat pouze zadáním dat JSON. 

- **Data JSON** umožňují definovat všechny možné konfigurační klíče pomocí skriptu JSON. 

Pokud přidáte vlastnosti pomocí **Návrháře konfigurace**, můžete tyto vlastnosti automaticky převést na formát JSON, a to tak, že v rozevíracím seznamu **formát nastavení konfigurace** vyberete možnost **zadat data JSON** , jak je uvedeno níže.

   ![Formát nastavení konfigurace – použít návrháře konfigurace](./media/configure-microsoft-launcher/configure-microsoft-launcher-01.png)

   > [!NOTE]
   > Po nakonfigurování vlastností pomocí návrháře konfigurace budou data JSON aktualizována také tak, aby odrážela tyto vlastnosti. K přidání dalších konfiguračních klíčů do dat JSON použijte [Příklad skriptu JSON](../apps/configure-microsoft-launcher.md#microsoft-launcher-configuration-example) ke zkopírování potřebných řádků pro každý konfigurační klíč. 

Při úpravách dříve vytvořených zásad konfigurace aplikací, pokud byly nakonfigurovány složité vlastnosti, proces úprav zobrazí Editor dat JSON. Všechna dříve nakonfigurovaná nastavení budou zachována a můžete přepnout na použití nástroje Configuration Designer a upravit podporovaná nastavení.

## <a name="using-configuration-designer"></a>Použití návrháře konfigurace

Návrhář konfigurace umožňuje vybrat předem vyplněná nastavení a jejich přidružené hodnoty.

   ![Formát nastavení konfigurace – zadejte data JSON.](./media/configure-microsoft-launcher/configure-microsoft-launcher-02.png)

V následující tabulce jsou uvedeny dostupné konfigurační klíče pro spouštěč Microsoftu, typy hodnot, výchozí hodnoty a popisy. Popis poskytuje očekávané chování zařízení na základě vybraných hodnot. Konfigurační klíče, které jsou zakázány v Návrháři konfigurace, nejsou uvedeny v tabulce.

|    Konfigurační klíč    |    Typ hodnoty    |    Výchozí hodnota    |    Popis     |
|---------------------------------------------------|------------------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Typ registrace    |    Řetězec     |    Výchozí    |    Umožňuje nastavit typ registrace, na kterou by tyto zásady měly platit. V současné době **výchozí** hodnota odkazuje na **CorporateOwnedBuisnessOnly**. K dispozici nejsou žádné další podporované typy registrace.        Název klíče JSON: management_mode_key        |
|    Změna uživatele v pořadí aplikace domovské obrazovky povolena    |    Logická hodnota    |    True    |    Umožňuje určit, zda je možné změnit nastavení **pořadí aplikace domovské obrazovky** koncovým uživatelem.<ul><li>Pokud je nastavená **hodnota true**, pořadí aplikací definované v zásadě se vynutilo jenom pro počáteční nasazení. Následně se zásada neuplatní, aby se projevily změny, které uživatel mohl udělat.</li><li>Pokud je nastavená **hodnota false**, bude se při každé synchronizaci vyžadovat pořadí aplikací.</li></ul><br>**Poznámka:** Pořadí aplikace domovské obrazovky lze nakonfigurovat pouze pomocí editoru JSON.<br><br>Název klíče JSON:<br>`com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed`    |
|    Nastavit velikost mřížky    |    Řetězec    |    Auto    |    Umožňuje nastavit velikost mřížky pro aplikace, které mají být umístěny na domovské obrazovce. Počet řádků a sloupců aplikace můžete nastavit tak, aby se definovala velikost mřížky v následujícím formátu: `columns;rows` . Pokud definujete velikost mřížky, maximální počet aplikací, které se zobrazí na řádku na domovské obrazovce, bude počet řádků, které jste nastavili, a maximální počet aplikací, které se zobrazí ve sloupci na domovské obrazovce, bude počet sloupců, které jste nastavili.<br><br>        Název klíče JSON:<br>`com.microsoft.launcher.HomeScreen.GridSize`    |
|    Nastavit tapetu zařízení    |    Řetězec    |    Null    |    Umožňuje nastavit tapetu podle vlastního výběru zadáním adresy URL obrázku, který chcete nastavit jako tapetu.<br><br>Název klíče JSON:<br>`com.microsoft.launcher.Wallpaper.URL`    |
|    Nastavit, aby se změna uživatele na tapetě zařízení povolila    |    Logická hodnota    |    True    |    Umožňuje určit, zda může koncový uživatel změnit nastavení tapety zařízení.<ul><li>Pokud je nastavená **hodnota true**, Tapeta v zásadách se vynutila jenom při počátečním nasazení. Následně se zásada neuplatní, aby se projevily změny, které uživatel mohl udělat.</li><li>Pokud je nastavena **hodnota false**, bude při každé synchronizaci vynutila tapeta.</li></ul><br>Název klíče JSON:<br>`com.microsoft.launcher.Wallpaper.URL.UserChangeAllowed`        |
|    Povolení informačního kanálu    |    Logická hodnota    |    True    |    Umožňuje povolit informační kanál spouštěče zařízení v případě, že uživatel přetáhne přímo na domovské obrazovce.<ul><li>Pokud je nastaveno na **true**, kanál bude povolen.</li><li>Pokud je hodnota nastavena na **false**, kanál bude zakázán.</li></ul><br>Název klíče JSON:<br>`com.microsoft.launcher.Feed.Enabled`    |
|    Povolit změnu uživatele v informačním kanálu povolen    |    Logická hodnota    |    True    |     Umožňuje určit, jestli může koncový uživatel změnit nastavení **Povolení kanálu** .<ul><li>Pokud je nastavená **hodnota true**, informační kanál se vynutil jenom pro počáteční nasazení. Následně se zásada neuplatní, aby se projevily změny, které uživatel mohl udělat.</li><li>Pokud je nastavená **hodnota false**, bude se při každé synchronizaci vyžadovat informační kanál.</li></ul><br>Název klíče JSON:`com.microsoft.launcher.Feed.Enabled.UserChangeAllowed`    |
|    Umístění panelu hledání   |    Řetězec    |    Dole    |  Umožňuje určit **umístění panelu hledání** na domovské obrazovce. <ul><li>Pokud je nastavené na **konec**, panel hledání se umístí do dolní části domovské obrazovky.</li><li>Pokud je nastaveno na **začátek**, panel hledání bude umístěn v horní části domovské obrazovky.</li><li>Pokud je nastavené na hodnotu **Skrýt**, panel hledání se odebere z domovské obrazovky.</li></ul><br>Název klíče JSON:<br>`com.microsoft.launcher.Search.SearchBar.Placement`    |
|    Umístění panelu hledání povolených změn uživatele   |    Logická hodnota    |    True    |  Umožňuje určit, jestli může koncový uživatel změnit nastavení **umístění panelu hledání** . <ul><li>Pokud je nastavená **hodnota true**, umístění panelu hledání se vynutilo jenom při počátečním nasazení. Následně se zásada neuplatní, aby se projevily změny, které uživatel mohl udělat.</li><li>Pokud je nastavena **hodnota false**, bude při každé synchronizaci vyhledáno umístění panelu hledání.</li></ul><br>Název klíče JSON:<br>`com.microsoft.launcher.Search.SearchBar.Placement.UserChangeAllowed`<p>**Poznámka:** U Microsoft spouštěče v 6,2 a novějších se toto nastavení už nebude vymáhat. Proto nastavení této hodnoty na `True` nebude mít žádný vliv. Koncoví uživatelé nebudou moci přizpůsobit umístění umístění panelu hledání na svém zařízení.    |
|    Režim Dock  |    Řetězec    |    Zobrazit    | Umožňuje zapnout Docker na zařízení, když uživatel potáhne přímo na domovské obrazovce.<ul><li>Pokud je nastaveno na hodnotu **Zobrazit**, Dock bude povolen.</li><li>Pokud je tato možnost nastavená na hodnotu **Skrýt**, Docker se skryje z domovské obrazovky, ale uživatel ji může zobrazit, když je to potřeba.</li><li>Pokud je nastavené na **zakázáno**, Dock se zakáže.</li></ul><br>Název klíče JSON:<br>`com.microsoft.launcher.Dock.Mode`    |
|   Změna uživatele režimu Dock Mode povolena   |    Řetězec    |    True    |  Umožňuje určit, zda může být nastavení režimu Docker změněno koncovým uživatelem.<ul><li>Pokud je nastavená **hodnota true**, nastaví se nastavení režimu Docker jenom pro počáteční nasazení. Následně se zásada neuplatní, aby se projevily změny, které uživatel mohl udělat.</li><li>Pokud je nastavena **hodnota false**, bude nastavení režimu Docker při každé synchronizaci vynutilo.</li></ul><br>Název klíče JSON:<br>`com.microsoft.launcher.Dock.Mode.UserChangeAllowed`    |

## <a name="enter-json-data"></a>Zadat data JSON

Zadejte data JSON pro konfiguraci všech dostupných nastavení pro spouštěč Microsoftu a také nastavení zakázaná v **Návrháři konfigurace**, jak je znázorněno níže.

   ![Návrhář konfigurace – data JSON](./media/configure-microsoft-launcher/configure-microsoft-launcher-03.png)

Kromě seznamu konfigurovatelných nastavení uvedených v tabulce návrháře konfigurace (výše) poskytují následující tabulka konfigurační klíče, které lze konfigurovat pouze prostřednictvím dat JSON.

|    Konfigurační klíč    |    Typ hodnoty    |    Výchozí hodnota    |    Popis     |
|----------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Nastavit povolené aplikace v seznamu<br>Klíč JSON:`com.microsoft.launcher.HomeScreen.Applications`    |    BundleArray    | Viz: [Nastavení povolených aplikací](configure-microsoft-launcher.md#set-allow-listed-applications)</sup>    |    Umožňuje definovat sadu aplikací, které jsou viditelné na domovské obrazovce z aplikací nainstalovaných v zařízení. Aplikace můžete definovat tak, že zadáte název balíčku aplikace pro aplikace, které chcete zobrazit, například, `com.android.settings` aby nastavení bylo přístupné na domovské obrazovce. Aplikace, které povolíte – seznam v této části, by už měly být na zařízení nainstalované, aby je bylo možné zobrazit na domovské obrazovce.<p>Vlastnosti:<ul><li>**Balíček:** Název balíčku aplikace</li><li>**Třída:** Aktivita aplikace, která je specifická pro určitou stránku aplikace. Použije výchozí stránku aplikace, pokud je tato hodnota prázdná.</li></ul>      |
|    Pořadí aplikací pro domovskou obrazovku<br>Klíč JSON:`com.microsoft.launcher.HomeScreen.AppOrder`    |    BundleArray    |    Viz: [pořadí aplikací domovské obrazovky](configure-microsoft-launcher.md#home-screen-app-order)      |    Umožňuje zadat pořadí aplikace na domovské obrazovce.<p>Vlastnosti:<br><ul><li>**Zadejte:** Pokud chcete určit pozice aplikací, podporuje se jenom TNelze načíst typ `application` . Pokud chcete zadat pozice webových odkazů, je typ `weblink` .</li><li>**Pozice:** Toto určuje pozici ikony aplikace na domovské obrazovce. Začíná od pozice 1 vlevo nahoře a bude zleva doprava, shora dolů.</li><li>**Balíček:** Toto je název balíčku aplikace, který se používá k zadání pořadí aplikací.</li><li>**Třída:** Je aktivita aplikace, která je specifická pro určitou stránku aplikace. Výchozí stránka aplikace se použije, pokud je tato hodnota prázdná. Tato vlastnost se používá pro aplikaci.</li><li>**Popisek:** Je aktivita aplikace, která je specifická pro určitou stránku aplikace. Výchozí stránka aplikace se použije, pokud je tato hodnota prázdná. Tato vlastnost se používá pro aplikaci.</li><li>**Odkaz:** Adresa URL, která se má spustit poté, co koncový uživatel klikne na ikonu webového odkazu Tato vlastnost se používá pro webový odkaz.</li></ul>    |
|    Nastavit připnuté webové odkazy<br>Klíč JSON:`com.microsoft.launcher.HomeScreen.WebLinks`    |    BundleArray    |    Viz: [Nastavení připnutých webových odkazů](configure-microsoft-launcher.md#set-pinned-web-link)      |    Tento klíč vám umožní připnout web na domovskou obrazovku jako ikonu snadného spuštění. Tímto způsobem se můžete ujistit, že koncový uživatel může mít rychlý a snadný přístup k základním webům. V konfiguraci pořadí aplikací pro domovskou obrazovku můžete změnit umístění každé ikony webového odkazu.<p>Vlastnosti:<br><ul><li>**• Popisek:** Název Weblink zobrazený na domovské obrazovce spouštěče MS</li><li>**Odkaz:** Adresa URL, která se má spustit poté, co koncový uživatel klikne na ikonu webového odkazu</li></ul>    |


### <a name="set-allow-listed-applications"></a>Nastavit povolené aplikace v seznamu

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.Applications",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="home-screen-app-order"></a>Pořadí aplikací pro domovskou obrazovku

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "type",
                    "valueString": "application"
                },
                {
                    "key": "position",
                    "valueInteger": 0
                },
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="set-pinned-web-link"></a>Nastavit připnutý webový odkaz

```JSON
{ 
    "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "label",
                    "valueString": "" 
                },  
                { 
                    "key": "link", 
                    "valueString": "" 
                } 
            ] 
        }
    ] 
},
{ 
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "type",  
                    "valueString": "" 
                },  
                { 
                    "key": "position",  
                    "valueInteger": 
                },  
                { 
                    "key": "label",  
                    "valueString": "" 
                },  
                { 
                    "key": "link",  
                    "valueString": "" 
                } 
            ] 
        }
    ] 
}
```



### <a name="microsoft-launcher-configuration-example"></a>Příklad konfigurace spouštěče Microsoft

Následující příklad obsahuje ukázkový skript JSON se všemi dostupnými konfiguračními klíči:

```JSON
{
    "kind": "androidenterprise#managedConfiguration", 
    "productId": "app:com.microsoft.launcher", 
    "managedProperty": [
        {
            "key": "management_mode_key", 
            "valueString": "Default"
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable", 
            "valueBool": true
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url", 
            "valueBool": "http://www.contoso.com/wallpaper.png"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.GridSize", 
            "valueString": "5;5"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.Applications", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }
            ]
        }, 
        { 
            "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
            "valueBundleArray": [ 
                { 
                    "managedProperty": [ 
                        { 
                            "key": "label",
                            "valueString": "News" 
                        },  
                        { 
                            "key": "link", 
                            "valueString": "https://www.bbc.com" 
                        } 
                    ] 
                }
            ] 
        },
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 17
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 18
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 19
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "weblink"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 20
                        }, 
                        {
                            "key": "label", 
                            "valueString": "News"
                        }, 
                        {
                            "key": "link", 
                            "valueString": "https://www.bbc.com"
                        }
                    ]
                }
            ]
        }
    ]
}

```

## <a name="next-steps"></a>Další kroky

- Další informace o plně spravovaných zařízeních s Androidem Enterprise najdete v tématu [Nastavení registrace v Intune pro Android Enterprise plně spravovat zařízení](../enrollment/android-fully-managed-enroll.md).
