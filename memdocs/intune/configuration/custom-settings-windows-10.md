---
title: Přidání vlastních nastavení pro zařízení s Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte nebo vytvořte vlastní profil, abyste v Microsoft Intune mohli u zařízení s Windows 10 používat nastavení OMA-URI. K přidání vlastního nastavení použijte vlastní profil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b6646c67f9425d395bbec1e33c03f6f29b6af7e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332351"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Použití vlastních nastavení pro zařízení s Windows 10 v Intune

V Microsoft Intune můžete vlastní profily použít k přidání nebo vytvoření vlastního nastavení pro zařízení s Windows 10. Vlastní profily jsou funkcí Intune. Jsou navržené tak, aby bylo možné přidat nastavení a funkce zařízení, které nejsou integrované do Intune.

Vlastní profily zařízení s Windows 10 používají nastavení OMA-URI (Open Mobile Alliance Uniform Resource Identifier) ke konfiguraci různých funkcí. Tato nastavení obvykle používají výrobci mobilních zařízení k řízení funkcí na zařízení. 

Ve Windows 10 je k dispozici řada nastavení od poskytovatelů konfiguračních služeb (CSP), třeba [Poskytovatel konfiguračních služeb pro zásady (CSP pro zásady)](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers).

Pokud hledáte konkrétní nastavení, nezapomeňte, že řada integrovaných nastavení je v [restriktivním profilu zařízení s Windows 10](device-restrictions-windows-10.md). Takže možná nebude potřeba zadávat vlastní hodnoty.

V tomto článku najdete:

- Postup vytvoření vlastního profilu na zařízeních s Windows 10
- Seznam doporučených nastavení OMA-URI
- Příklad vlastního profilu, který otevře připojení k síti VPN

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující nastavení:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **vlastní profil Windows 10**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Windows 10 a novější**.
    - **Typ profilu**: vyberte **vlastní**.

4. V nabídce **Vlastní nastavení OMA-URI** vyberte **Přidat**. Zadejte následující nastavení:

    - **Název:** Zadejte jedinečný název nastavení OMA-URI, abyste ho v seznamu poznali.
    - **Popis:** Zadejte popis, který nastavení stručně charakterizuje, a další důležité podrobnosti.
    - **OMA-URI** (rozlišuje velká a malá písmena): Zadejte nastavení OMA-URI, které chcete použít.
    - **Datový typ**: vyberte datový typ, který budete používat pro toto nastavení OMA-URI. Možnosti:

        - String
        - Řetězec (soubor XML)
        - Datum a čas
        - Celé číslo
        - Číslo s plovoucí desetinnou čárkou
        - Logická hodnota
        - Base64 (soubor)

    - **Hodnota:** Zadejte datovou hodnotu, kterou chcete přidružit k zadanému nastavení OMA-URI. Hodnota závisí na vybraném datovém typu. Pokud například vyberete položku **Datum a čas**, vyberte hodnotu z ovládacího prvku pro výběr data.

    Po přidání nastavení můžete vybrat **Exportovat**. **Export** vytvoří seznam všech hodnot, které jste přidali do souboru hodnot oddělených čárkou (.csv).

5. Výběrem **OK** uložte změny. Podle potřeby přidejte další nastavení.
6. Po dokončení vyberte **OK** > **vytvořit** a vytvořte profil Intune. Po dokončení se Váš profil zobrazí v seznamu **zařízení – konfigurační profily** .

## <a name="example"></a>Příklad

V následujícím příkladu je zapnuté nastavení **Connectivity/AllowVPNOverCellular**. Toto nastavení umožňuje zařízení s Windows 10, které je připojené k mobilní síti, otevřít připojení k síti VPN.

![Příklad vlastní zásady s nastavením VPN](./media/custom-settings-windows-10/custom-policy-example.png)

## <a name="find-the-policies-you-can-configure"></a>Vyhledání zásad, které můžete nakonfigurovat

Úplný seznam všech poskytovatelů konfiguračních služeb (CSP) podporovaných systémem Windows 10 najdete v [referenčních informacích o poskytovatelích konfiguračních služeb](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference).

Ne všechna nastavení jsou kompatibilní se všemi verzemi Windows 10. Informace o tom, jaké verze konfiguračních služeb každý poskytovatel podporuje, najdete v [referenčních informacích o poskytovatelích konfiguračních služeb](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference).

Intune navíc nepodporuje všechna nastavení, která jsou v [referenčních informacích o poskytovatelích konfiguračních služeb](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference). Pokud chcete zjistit, jestli Intune podporuje vámi požadované nastavení, otevřete si článek týkající se daného nastavení. Na každé stránce nastavení se zobrazuje podporovaná operace. Aby bylo možné pracovat s Intune, musí nastavení podporovat operace **Přidat**, **nahradit**a **získat** . Pokud hodnota vrácená operací **Get** neodpovídá hodnotě poskytované operacemi **Přidat** nebo **nahradit** , Intune ohlásí chybu kompatibility.

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).
