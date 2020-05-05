---
title: Správa zařízení pomocí místní správy MDM
titleSuffix: Configuration Manager
description: Pomocí Configuration Manager místní správy mobilních zařízení (MDM) Chraňte data zařízení pomocí úplného vymazání, selektivního vymazání, vzdáleného zámku nebo resetování hesla.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9849f3bef5aa67dcc45b00f64487242230edc2e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721868"
---
# <a name="manage-devices-and-protect-data-with-on-premises-mdm-in-configuration-manager"></a>Správa zařízení a ochrana dat pomocí místní správy mobilních zařízení (MDM) v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Mobilní zařízení můžou ukládat citlivá data a poskytovat snadný přístup k mnoha prostředkům organizace. Pro lepší ochranu zařízení a dat použijte Configuration Manager pro následující akce správy zařízení:

- **Úplné vymazání**: obnovení továrního nastavení zařízení

- **Selektivní vymazání**: odebrání pouze organizačních dat

- **Resetování hesla**: odebrání nebo resetování hesla, když ho uživatel zapomene

- **Vzdálené uzamčení**: zabezpečení zařízení, které může být ztraceno

## <a name="full-wipe"></a>Úplné vymazání  

Pokud potřebujete zabezpečit ztracené zařízení nebo vyřadit zařízení z aktivního používání, můžete na něm začít úplné vymazání. Tato akce obnoví zařízení do výchozího továrního nastavení. Odstraní všechna organizační a uživatelská data a nastavení.

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** . Můžete také zvolit **kolekce zařízení** a vybrat kolekci, ze které je zařízení členem.

1. Vyberte zařízení, které chcete vymazat.

1. Na pásu karet ve skupině zařízení vyberte **Akce se vzdáleným zařízením**a potom zvolte **vyřadit z provozu nebo vymazat**.

1. V okně **vyřadit z Configuration Manager** vyberte možnost **vymazání mobilního zařízení a vyřazení z Configuration Manager**.

## <a name="selective-wipe"></a>Selektivní vymazání

Pokud chcete ze zařízení odebrat jenom data organizace, spusťte selektivní vymazání.

### <a name="behaviors-by-os-version"></a>Chování podle verze OS

Následující tabulky popisují, jaká data se odeberou, a vliv na data, která v zařízení po selektivním vymazání zůstanou.

#### <a name="windows-10-windows-81-windows-rt-81-and-windows-rt"></a>Windows 10, Windows 8.1, Windows RT 8,1 a Windows RT

|Obsah|Chování selektivního vymazání|  
|-------|--------|
|Aplikace a související data nainstalovaná pomocí Configuration Manager|Odinstaluje aplikace a odebere všechny klíče pro zkušební načtení. Odvolá šifrovací klíč pro aplikace, které používají selektivní vymazání Windows, a data už nebudou dostupná.|
|Profily VPN a Wi-Fi|Odebere profily.|
|Certifikáty|Odebere a odvolá certifikáty.|
|Nastavení|Odebere požadavky.|
|E-mailové profily.|Odebere e-mail s povoleným systémem souborů EFS, což zahrnuje e-maily a přílohy aplikace Pošta pro Windows.|

#### <a name="windows-10-mobile-windows-phone-80-and-windows-phone-81"></a>Windows 10 Mobile, Windows Phone 8,0 a Windows Phone 8,1

|Obsah|Chování selektivního vymazání|  
|-------|--------|
|Firemní aplikace a související data nainstalovaná pomocí Configuration Manager|Odinstaluje aplikace a odebere data aplikace organizace.|
|Profily VPN a Wi-Fi|Odebere profily pro Windows 10 Mobile a Windows Phone 8,1.|
|Certifikáty|Odebere certifikáty pro Windows Phone 8,1|
|E-mailové profily.|Odebere profily (kromě Windows Phone 8,0).|

Z zařízení s Windows 10 Mobile a Windows Phone 8,1 se odeberou taky tato nastavení:  

- **Vyžadovat heslo k odemknutí mobilních zařízení**  
- **Povolit jednoduchá hesla**  
- **Minimální délka hesla**  
- **Vyžadovaný typ hesla**
- **Vypršení platnosti hesla (dny)**  
- **Pamatovat si historii hesel**  
- **Počet povolených opakovaných neúspěšných přihlášení, než bude zařízení vymazáno**  
- **Počet minut nečinnosti před vyžadováním hesla**  
- **Vyžadovaný typ hesla – minimální počet znakových sad**  
- **Povolit fotoaparát**
- **Vyžadovat šifrování u mobilního zařízení**  
- **Povolit vyměnitelné úložiště**  
- **Povolit webový prohlížeč**  
- **Povolit obchod s aplikacemi**  
- **Povolit snímek obrazovky**  
- **Povolit zeměpisnou polohu**  
- **Povolení účtu Microsoft**  
- **Povolit kopírování a vkládání**  
- **Povolit Wi-Fi tethering**  
- **Povolit automatické připojení k bezplatným Wi-Fi hotspotům**  
- **Povolit oznamování Wi-Fi hotspotů**  
- **Povolit obnovení do výrobního nastavení**
- **Povolit Bluetooth**  
- **Povolit komunikaci NFC**
- **Povolit Wi-Fi**

### <a name="start-a-selective-wipe"></a>Spuštění selektivního vymazání

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** . Můžete také zvolit **kolekce zařízení** a vybrat kolekci, ze které je zařízení členem.

1. Vyberte zařízení, které chcete vymazat.

1. Na pásu karet ve skupině zařízení vyberte **Akce se vzdáleným zařízením**a potom zvolte **vyřadit z provozu nebo vymazat**.

1. V okně **vyřadit z Configuration Manager** vyberte následující možnost: **Vymazat obsah společnosti a vyřadit mobilní zařízení z Configuration Manager**.

### <a name="recommendations-for-selective-wipe"></a>Doporučení pro selektivní vymazání

- Pro úspěšné vymazání e-mailu nastavte e-mailové profily na zařízení Windows Phone 8,1.

- Pro úspěšné vymazání aplikací se ujistěte, že jsou aplikace distribuované přes správu aplikací pro mobilní zařízení.

## <a name="passcode-reset"></a>resetování hesla

Pokud uživatel zapomene heslo, použijte tuto akci k vynucení nového dočasného hesla v zařízení. Heslo taky můžete odebrat úplně. Následující tabulka uvádí, jak resetování hesla funguje na různých mobilních platformách.

| Verze operačního systému | resetování hesla |
|------------|----------------|
| Windows 10 | Nepodporuje se |
| Windows 10 Mobile | Podporováno, s výjimkou zařízení s Azure Active Directory připojená |
| Windows Phone 8 a Windows Phone 8.1 | Podporuje se |
| Windows RT 8.1 | Nepodporuje se |
| Windows 8.1 | Nepodporuje se |

> [!Note]
> Spusťte akci resetování hesla z lokality nejvyšší úrovně. Pokud například použijete lokalitu centrální správy, můžete provést akci pouze na tomto webu. Pokud používáte samostatnou primární lokalitu, můžete provést tuto akci pouze z této lokality.

### <a name="remotely-reset-the-passcode-on-a-mobile-device"></a>Vzdálené resetování hesla na mobilním zařízení

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** . Můžete také zvolit **kolekce zařízení** a vybrat kolekci, ze které je zařízení členem.

1. Vyberte zařízení, na kterých se má resetovat heslo.

1. Na pásu karet ve skupině zařízení vyberte **Akce se vzdáleným zařízením**a pak zvolte **resetování hesla**.  

### <a name="show-the-state-of-the-passcode-reset"></a>Zobrazit stav resetování hesla  

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** . Můžete také zvolit **kolekce zařízení** a vybrat kolekci, ze které je zařízení členem.

1. Vyberte zařízení, na kterých se má zobrazit stav resetování hesla.

1. Na pásu karet ve skupině zařízení vyberte **Akce se vzdáleným zařízením**a pak zvolte **Zobrazit stav hesla**.  

## <a name="remote-lock"></a>vzdálené uzamčení

Pokud uživatel ztratí své zařízení, můžete zařízení vzdáleně zamknout. Následující tabulka uvádí, jak vzdálené uzamčení funguje na různých mobilních platformách.  

|Verze operačního systému|vzdálené uzamčení|
|----------|-----------|
|Windows 10|Nepodporuje se|
|Windows Phone 8 a Windows Phone 8.1|Podporuje se|
|Windows RT 8.1|Podporováno, pokud je aktuální uživatel zařízení stejný jako uživatel, který zařízení zaregistroval.|
|Windows 8.1|Podporováno, pokud je aktuální uživatel zařízení stejný jako uživatel, který zařízení zaregistroval.|

> [!Note]
> Spusťte akci vzdálené uzamčení v lokalitě nejvyšší úrovně. Pokud například použijete lokalitu centrální správy, můžete provést akci pouze na tomto webu. Pokud používáte samostatnou primární lokalitu, proveďte akci z této lokality.

### <a name="remotely-lock-a-mobile-device"></a>Vzdálené uzamčení mobilního zařízení

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** . Můžete také zvolit **kolekce zařízení** a vybrat kolekci, ze které je zařízení členem.

1. Vyberte zařízení, která se mají zamknout.

1. Na pásu karet ve skupině zařízení vyberte **Akce se vzdáleným zařízením**a pak zvolte **vzdálené uzamčení**. Potvrďte akci.

### <a name="show-the-state-of-the-remote-lock"></a>Zobrazit stav vzdáleného zámku

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** . Můžete také zvolit **kolekce zařízení** a vybrat kolekci, ze které je zařízení členem.

1. Vyberte zařízení, na kterém se má zobrazit stav vzdáleného zámku.

1. Na pásu karet ve skupině zařízení vyberte **Akce se vzdáleným zařízením**a pak zvolte možnost **Zobrazit stav vzdáleného zámku**.
