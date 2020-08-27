---
title: Přidání vlastních nastavení pro zařízení s Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte nebo vytvořte vlastní profil, abyste v Microsoft Intune mohli u zařízení s Windows 10 používat nastavení OMA-URI. K přidání vlastního nastavení použijte vlastní profil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28a867c735a05cfa4a4765534d200b806711f9b5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913014"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Použití vlastních nastavení pro zařízení s Windows 10 v Intune

Tento článek obsahuje seznam a popis všech různých vlastních nastavení, která můžete řídit na zařízeních s Windows 10 a novějším. Jako součást řešení správy mobilních zařízení (MDM) pomocí těchto nastavení můžete nakonfigurovat nastavení, která nejsou integrovaná do Intune.

Další informace o vlastních profilech najdete v tématu [Vytvoření profilu s vlastním nastavením](custom-settings-configure.md).

Tato nastavení se přidají do konfiguračního profilu zařízení v Intune a pak se přiřadí nebo nasadí na vaše zařízení s Windows 10.

Tato funkce platí pro:

- Windows 10 a novější

Vlastní profily zařízení s Windows 10 používají nastavení OMA-URI (Open Mobile Alliance Uniform Resource Identifier) ke konfiguraci různých funkcí. Tato nastavení obvykle používají výrobci mobilních zařízení k řízení funkcí na zařízení.

Ve Windows 10 je k dispozici řada nastavení od poskytovatelů konfiguračních služeb (CSP), třeba [Poskytovatel konfiguračních služeb pro zásady (CSP pro zásady)](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers).

Pokud hledáte konkrétní nastavení, nezapomeňte, že řada integrovaných nastavení je v [restriktivním profilu zařízení s Windows 10](device-restrictions-windows-10.md). Takže možná nebude potřeba zadávat vlastní hodnoty.

## <a name="before-you-begin"></a>Než začnete

[Vytvořte vlastní profil Windows 10](custom-settings-configure.md#create-the-profile).

## <a name="oma-uri-settings"></a>Nastavení OMA-URI

**Přidat**: zadejte následující nastavení:

- **Název:** Zadejte jedinečný název nastavení OMA-URI, abyste ho v seznamu poznali.
- **Popis:** Zadejte popis, který nastavení stručně charakterizuje, a další důležité podrobnosti.
- **OMA-URI** (rozlišuje velká a malá písmena): Zadejte nastavení OMA-URI, které chcete použít.
- **Datový typ**: vyberte datový typ, který budete používat pro toto nastavení OMA-URI. Možnosti:

  - Base64 (soubor)
  - Logická hodnota
  - Řetězec (soubor XML)
  - Datum a čas
  - Řetězec
  - Plovoucí desetinná čárka
  - Integer

- **Hodnota:** Zadejte datovou hodnotu, kterou chcete přidružit k zadanému nastavení OMA-URI. Hodnota závisí na vybraném datovém typu. Pokud například vyberete položku **Datum a čas**, vyberte hodnotu z ovládacího prvku pro výběr data.

Po přidání nastavení můžete vybrat **Exportovat**. **Export** vytvoří seznam všech hodnot, které jste přidali do souboru hodnot oddělených čárkou (.csv).

## <a name="find-the-policies-you-can-configure"></a>Vyhledání zásad, které můžete nakonfigurovat

Úplný seznam všech poskytovatelů konfiguračních služeb (CSP) podporovaných systémem Windows 10 najdete v [referenčních informacích o poskytovatelích konfiguračních služeb](/windows/client-management/mdm/configuration-service-provider-reference).

Ne všechna nastavení jsou kompatibilní se všemi verzemi Windows 10. Informace o tom, jaké verze konfiguračních služeb každý poskytovatel podporuje, najdete v [referenčních informacích o poskytovatelích konfiguračních služeb](/windows/client-management/mdm/configuration-service-provider-reference).

Intune navíc nepodporuje všechna nastavení, která jsou v [referenčních informacích o poskytovatelích konfiguračních služeb](/windows/client-management/mdm/configuration-service-provider-reference). Pokud chcete zjistit, jestli Intune podporuje vámi požadované nastavení, otevřete si článek týkající se daného nastavení. Na každé stránce nastavení se zobrazuje podporovaná operace. Aby bylo možné pracovat s Intune, musí nastavení podporovat operace **Přidat**, **nahradit**a **získat** . Pokud hodnota vrácená operací **Get** neodpovídá hodnotě poskytované operacemi **Přidat** nebo **nahradit** , Intune ohlásí chybu kompatibility.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

[Přečtěte si další informace o vlastních profilech v Intune](custom-settings-configure.md).