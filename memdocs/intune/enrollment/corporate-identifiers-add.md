---
title: Přidání podnikových identifikátorů do Intune
titleSuffix: ''
description: Zjistěte, jak přidat podnikové identifikátory (způsob registrace, IMEI a sériová čísla) do Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 566ed16d-8030-42ee-bac9-5f8252a83012
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 90c3445110eb9f85493a9280199c70a478f5ef52
ms.sourcegitcommit: 71f26a0756fd40c1a06f885f3d31e49734fe97fe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/25/2020
ms.locfileid: "80256789"
---
# <a name="identify-devices-as-corporate-owned"></a>Identifikace zařízení jako vlastněných společností

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Jako správce Intune můžete identifikovat zařízení jako ve vlastnictví firmy, aby se zlepšila jejich správa a identifikace. Intune můžete provádět další úlohy správy a sbírat další informace, třeba celé telefonní číslo a inventář aplikací ze zařízení ve vlastnictví firmy. Můžete také nastavit omezení zařízení a blokovat tak registraci zařízení, které ve vlastnictví firmy nejsou.

Během registrace Intune automaticky přiřadí některým zařízením stav, který označuje, že tato zařízení jsou ve vlastnictví firmy. Týká se to každého zařízení, které:

- Je registrované pomocí nějakého účtu [správce registrace zařízení](device-enrollment-manager-enroll.md) (všechny platformy)
- Je registrované přes [Program registrace zařízení](device-enrollment-program-enroll-ios.md) od Applu, [Apple School Manager](apple-school-manager-set-up-ios.md) nebo [Apple Configurator](apple-configurator-enroll-ios.md) (jen iOS)
- [Před registrací je identifikované jako ve vlastnictví firmy](#identify-corporate-owned-devices-with-imei-or-serial-number) pomocí čísla IMEI (International Mobile Equipment Identifier) (všechny platformy s čísly IMEI) nebo sériového čísla (iOS a Android)
- Připojí se k Azure Active Directory pomocí pracovních nebo školních přihlašovacích údajů. [Zařízení, která jsou Azure Active Directory registrována](https://docs.microsoft.com/azure/active-directory/devices/overview) , budou označena jako osobní.
- Je na [seznamu vlastností zařízení](#change-device-ownership) označené jako firemní

Po registraci můžete [měnit nastavení vlastnictví](#change-device-ownership) na **Osobní** a **Firemní**.

## <a name="identify-corporate-owned-devices-with-imei-or-serial-number"></a>Identifikace zařízení ve vlastnictví firmy pomocí čísla IMEI nebo sériového čísla

Jako správce Intune můžete vytvořit a importovat textový soubor s oddělovači (. csv), který obsahuje 14 číslic nebo sériová čísla o hodnotě IMEI. Intune pomocí těchto identifikátorů během registrace určuje, že zařízení je ve vlastnictví firmy. Každý kód IMEI nebo sériové číslo může mít v tomto seznamu uvedené podrobnosti pro účely správy.

Tato funkce je podporovaná pro následující platformy:

| Platforma | Čísla IMEI | Sériová čísla |
|---|---|---|
| Windows | Podporováno (Windows Phone) | Není podporované |
| iOS/macOS | Není podporované | Podporuje se |
| V10 za účelem spravovaného operačního systému Android pro správu zařízení | Není podporované | Není podporované |
| Ostatní systémy Android | Není podporované | Podporuje se |

<!-- When you upload serial numbers for corporate-owned iOS/iPadOS devices, they must be paired with a corporate enrollment profile. Devices must then be enrolled using either Apple's Automated Device Enrollment or Apple Configurator to have them appear as corporate-owned. -->

[Přečtete si, jak zjistit sériové číslo zařízení Apple](https://support.apple.com/HT204308).<br>
[Přečtete si, jak zjistit sériové číslo zařízení s Androidem](https://support.google.com/store/answer/3333000).

## <a name="add-corporate-identifiers-by-using-a-csv-file"></a>Přidání podnikových identifikátorů pomocí souboru .csv
Pokud chcete vytvořit seznam, vytvořte seznam hodnot oddělených čárkami se dvěma sloupci (.csv) bez záhlaví. Přidejte do levého sloupce číslo IMEI nebo sériová čísla a podrobnosti v pravém sloupci. V rámci jednoho souboru .csv můžete importovat pouze jeden typ identifikačního čísla: buď IMEI, nebo sériové číslo. Podrobnosti jsou omezené na 128 znaků a používají se jenom pro účely správy. Na zařízení se podrobnosti nezobrazují. Současný limit jednoho souboru CSV je 5 000 řádků.

**Nahráním souboru .csv se sériovými čísly** – Vytvořte seznam oddělený čárkami (.csv), který bude mít dva sloupce, a nebude mít záhlaví. Soubor .csv může obsahovat maximálně 5000 zařízení, ale jeho velikost nesmí překročit 5 MB.

|||
|-|-|
|&lt;ID č. 1&gt;|&lt;Podrobnosti o zařízení č. 1&gt;|
|&lt;ID č. 2&gt;|&lt;Podrobnosti o zařízení č. 2&gt;|

V textovém editoru vypadá soubor .csv takhle:

```
01234567890123,device details
02234567890123,device details
```

> [!IMPORTANT]
> Některá zařízení s Androidem a iOS/iPadOS mají několik čísel IMEI. Intune dokáže přečíst jen jeden kód IMEI na každé zaregistrované zařízení. Pokud importujete číslo IMEI, ale nejedná se o IMEI v inventáři pomocí Intune, zařízení se klasifikuje jako osobní zařízení místo zařízení vlastněné společností. Pokud importujete více kódů IMEI pro jedno zařízení, zobrazí se u kódů, které nejsou v inventáři, stav registrace **Neznámý**.<br>
>Všimněte si také, že sériová čísla jsou doporučená forma identifikace pro zařízení se systémem iOS/iPadOSOS.
>Sériová čísla Androidu nejsou zaručená jako jedinečná nebo současná. Pokud chcete zjistit, jestli je sériové číslo spolehlivým identifikátorem zařízení, obraťte se na dodavatele zařízení.
>Sériová čísla, která službě Intune oznámí zařízení, se nemusí shodovat se zobrazenými identifikátory v nabídkách zařízení Nastavení/ O zařízení. Ověřte si typ sériového čísla oznámeného výrobcem zařízení.
>Pokus o nahrání souborů se sériovými čísly, které obsahují tečky (.), způsobí selhání nahrávání. Sériová čísla s tečkami nejsou podporovaná.

### <a name="upload-a-csv-list-of-corporate-identifiers"></a>Nahrání seznamu podnikových identifikátorů ve formátu .csv

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), vyberte **zařízení** > **registrace zařízení** > **identifikátory podnikových zařízení** > **přidejte** > **nahrát soubor CSV**.

2. V okně **Přidat identifikátory** zadejte typ identifikátoru: **IMEI** nebo **Sériové**.

3. Klikněte na ikonu složky a určete cestu k seznamu, který chcete importovat. Přejděte do souboru .csv a zvolte **Přidat**. 

4. Pokud soubor .csv obsahuje podnikové identifikátory, které už v Intune jsou, ale mají jiné podrobnosti, zobrazí se automaticky otevírané okno **Zkontrolovat duplicitní identifikátory**. Vyberte identifikátory, které chcete v Intune přepsat, a výběrem **OK** tyto identifikátory přidejte. U každého identifikátoru se porovná jenom první duplicita.

## <a name="manually-enter-corporate-identifiers"></a>Ruční zadání podnikových identifikátorů

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), vyberte **zařízení** > **registrace zařízení** > **identifikátory podnikových zařízení** > **přidejte** > **zadat ručně**.

2. V okně **Přidat identifikátory** zadejte typ identifikátoru: **IMEI** nebo **Sériové**.

3. Zadejte **identifikátor** a **Podrobnosti** pro každý identifikátor, který chcete přidat. Až zadávání identifikátorů dokončíte, zvolte **Přidat**.

5. Pokud jste zadali podnikové identifikátory, které už v Intune jsou, ale mají jiné podrobnosti, zobrazí se automaticky otevírané okno **Zkontrolovat duplicitní identifikátory**. Vyberte identifikátory, které chcete v Intune přepsat, a výběrem **OK** tyto identifikátory přidejte. U každého identifikátoru se porovná jenom první duplicita.

Pokud se chcete podívat na identifikátory nového zařízení, můžete kliknout na **Aktualizovat**.

Importovaná zařízení nemusí být nutně zaregistrovaná. Zařízení můžou mít stav **Zaregistrované** nebo **Nekontaktované**. **Nekontaktované** znamená, že toto zařízení nikdy se službou Intune nekomunikovalo.

## <a name="delete-corporate-identifiers"></a>Odstranění podnikových identifikátorů

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)a vyberte **zařízení** > **registrace zařízení** > **identifikátory podnikových zařízení**.
2. Vyberte identifikátory zařízení, které chcete odstranit, a zvolte **Odstranit**.
3. Potvrďte odstranění.

Při odstranění podnikového identifikátoru zaregistrovaného zařízení se nezmění vlastnictví zařízení. Pokud chcete změnit vlastnictví zařízení, přejděte na **Zařízení**, vyberte zařízení, zvolte **Vlastnosti** a změňte **Vlastnictví zařízení**.

## <a name="imei-specifications"></a>Specifikace IMEI
Podrobné specifikace o číslech IMEI najdete na stránce [3GGPP TS 23.003](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=729).

## <a name="change-device-ownership"></a>Změna vlastnictví zařízení

U každého záznamu zařízení v Intune se ve vlastnostech zařízení zobrazuje **Vlastnictví**. Jako správce můžete zařízení označit jako **Osobní** nebo **Firemní**. Když se typ vlastnictví zařízení změní z firemní na osobní, Intune odstraní všechny informace o aplikaci dříve shromážděné z tohoto zařízení do 7 dnů. V případě potřeby bude Intune také odstraňovat telefonní číslo na záznamu. 

**Vlastnictví zařízení změníte takto:**
1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), vyberte **zařízení** > **všechna zařízení** > vyberte zařízení.
2. Zvolte **Vlastnosti**.
3. Určete **Vlastnictví zařízení** jako **Osobní** nebo **Firemní**.

   ![Vlastnosti zařízení s možnostmi Kategorie zařízení a Vlastnictví zařízení](./media/corporate-identifiers-add/device-properties.png)
