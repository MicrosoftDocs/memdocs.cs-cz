---
title: Endpoint Protection definice malwaru ze služby WSUS
titleSuffix: Configuration Manager
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Přečtěte si, jak nakonfigurovat službu Windows Server Update Services pro automatické schvalování aktualizací definic.
manager: dougeby
ms.openlocfilehash: 235caff52b877177b92792bf8d9fb3a2007127a5
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126029"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-wsus-for-configuration-manager"></a>Povolit Endpoint Protection definice malwaru ke stažení ze služby WSUS pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pokud udržujete antimalwarové definice aktuální pomocí služby WSUS, můžete ji nakonfigurovat tak, aby automaticky schvalovala aktualizace definic. I když použití Configuration Manager aktualizace softwaru doporučuje způsob aktuálnosti definic v aktuálním stavu, můžete službu WSUS nakonfigurovat taky jako metodu, která uživatelům umožní ručně aktualizovat definice. Službu WSUS můžete nakonfigurovat jako zdroj aktualizací pomocí následujícího postupu.

## <a name="synchronize-definition-updates-for-configuration-manager"></a>Synchronizovat aktualizace definice pro Configuration Manager

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a pak vyberte možnost **lokality**.

1. Vyberte lokalitu, která obsahuje váš bod aktualizace softwaru. Ve skupině **Nastavení** na pásu karet vyberte možnost **Konfigurovat součásti lokality**a pak vyberte možnost **bod aktualizace softwaru**.

1. V okně **Vlastnosti komponenty bodu aktualizace softwaru** přepněte na kartu **klasifikace** . Vyberte **aktualizace definic**.

1. Chcete-li určit **produkty** aktualizované pomocí služby WSUS, přepněte na kartu **produkty** .

    - Pro Windows 10 a novější: v části Microsoft > Windows vyberte **Windows Defender**.

    - Pro Windows 8.1 a starší verze: v části Microsoft > Forefront vyberte možnost **System Center Endpoint Protection**.

1. Kliknutím na **tlačítko OK** zavřete okno **Vlastnosti komponenty bodu aktualizace softwaru** .

## <a name="synchronize-definition-updates-for-standalone-wsus"></a>Synchronizovat aktualizace definic pro samostatnou službu WSUS

Pomocí následujícího postupu můžete nakonfigurovat Endpoint Protection aktualizace, když server WSUS není integrovaný do vašeho Configuration Manager prostředí.

1. V konzole pro správu služby WSUS rozbalte položku **počítače**, vyberte **Možnosti**a pak vyberte **produkty a klasifikace**.

1. Chcete-li určit **produkty** aktualizované pomocí služby WSUS, přepněte na kartu **produkty** .

    - Pro Windows 10 a novější: v části Microsoft > Windows vyberte **Windows Defender**.

    - Pro Windows 8.1 a starší verze: v části Microsoft > Forefront vyberte možnost **System Center Endpoint Protection**.

1. Přepněte na kartu **klasifikace** . Vyberte aktualizace a **aktualizace** **definic** .

## <a name="approve-definition-updates"></a>Schválit aktualizace definic

Aktualizace definic Endpoint Protection musí být schváleny a staženy na server služby WSUS, aby byly nabídnuty klientům, kteří požadují seznam dostupných aktualizací. Klienti se připojují k serveru WSUS, aby zkontrolovali dostupnost použitelných aktualizací, a potom si vyžádají nejnovější schválené aktualizace definic.

### <a name="approve-definitions-and-updates-in-wsus"></a>Schválení definic a aktualizací ve službě WSUS

1. V konzole pro správu služby WSUS vyberte **aktualizace**. Pak vyberte **všechny aktualizace** nebo klasifikace aktualizací, které chcete schválit.

1. V seznamu aktualizací klikněte pravým tlačítkem na aktualizaci nebo aktualizace, které chcete schválit pro instalaci, a pak vyberte **schválit**.

1. V okně **schválit aktualizace** vyberte skupinu počítačů, pro kterou chcete aktualizace schválit, a pak vyberte **schváleno pro instalaci**.

### <a name="configure-an-automatic-approval-rule"></a>Konfigurace pravidla automatického schvalování

Můžete také nastavit pravidlo automatického schvalování pro aktualizace definic a aktualizace Endpoint Protection. Tato akce nakonfiguruje službu WSUS tak, aby automaticky schválila Endpoint Protection aktualizace definic stažené službou WSUS.

1. V konzole pro správu služby WSUS vyberte **Možnosti**a pak vyberte **Automatická schválení**.

1. Na kartě **pravidla aktualizace** vyberte **nové pravidlo**.

1. V okně **Přidat pravidlo** v části **Krok 1: vyberte vlastnosti**vyberte možnost: **Pokud je aktualizace v konkrétní klasifikaci**.

    1. V části **Krok 2: Upravte vlastnosti**vyberte **libovolná klasifikace**.

    1. Zrušte zaškrtnutí všech možností kromě **aktualizace definic**a pak vyberte **OK**.

1. V okně **Přidat pravidlo** v části **Krok 1: vyberte vlastnosti**vyberte možnost: **Pokud je aktualizace v konkrétním produktu**.

    1. V části **Krok 2: Upravte vlastnosti**vyberte **libovolný produkt**.

    1. Vymažte všechny možnosti Kromě nástroje **System Center Endpoint Protection** pro Windows 8.1 a starší nebo **Windows Defender** pro Windows 10 a novější. Pak vyberte **OK**.

1. V části **Krok 3: zadejte název**zadejte název pravidla a potom vyberte **OK**.

1. V dialogovém okně **automatické schvalování** vyberte nově vytvořené pravidlo a pak vyberte **Spustit pravidlo**.

> [!NOTE]
> V zájmu maximálního výkonu na serveru WSUS a klientských počítačích odmítněte staré aktualizace definic. To můžete provést tak, že nakonfigurujete automatické schválení pro revize a automatické odmítnutí aktualizací s vypršenou dobou platnosti. Další informace najdete v tématu [Podpora Microsoftu článku 938947](https://support.microsoft.com/kb/938947).

> [!div class="nextstepaction"]
> [Vytvoření a nasazení antimalwarových zásad](endpoint-antimalware-policies.md)
