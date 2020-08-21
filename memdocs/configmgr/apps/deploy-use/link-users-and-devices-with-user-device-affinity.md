---
title: Propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení
titleSuffix: Configuration Manager
description: Propojte uživatele a zařízení pomocí spřažení uživatelských zařízení a automaticky nasaďte aplikace do všech zařízení přidružených k uživateli.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8e1a55efa6b23aa489ea65b3296e33847163a5c4
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695235"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-configuration-manager"></a>Propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Spřažení uživatelských zařízení v Configuration Manager přidruží uživatele k jednomu nebo více zařízením. Toto chování může eliminovat nutnost znát názvy zařízení uživatele k nasazení aplikace pro uživatele. Místo nasazení aplikace na každé zařízení uživatele nasadíte aplikaci pro uživatele. Spřažení uživatelských zařízení pak automaticky zajistí, že se aplikace nainstaluje na všechna zařízení, která jsou k tomuto uživateli přidružená.  

Definujte primární zařízení, která uživatelé používají každý den pro svou práci. Když vytvoříte spřažení mezi uživatelem a zařízením, získáte víc možností pro nasazení aplikací. Například pokud uživatel vyžaduje aplikaci Microsoft Visio, můžete ji nainstalovat na primární zařízení uživatele pomocí Instalační služba systému Windows nasazení. Ale na zařízení, které není primárním zařízením, můžete aplikaci Visio nasadit jako virtuální aplikaci. Spřažení zařízení a uživatele můžete použít také k předvedení softwaru na zařízení uživatele, když uživatel není přihlášený. Když se uživatel přihlásí, aplikace je už nainstalovaná a připravená ke spuštění.  

Informace o spřažení uživatelských zařízení se spravují jenom pro počítače. Configuration Manager automaticky spravuje spřažení zařízení a uživatelů pro mobilní zařízení, která se registrují.  

## <a name="manually-set-up-user-device-affinity"></a>Ruční nastavení spřažení uživatelských zařízení  

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** .  

1. Vyberte zařízení. Na kartě **Domů** na pásu karet ve skupině **zařízení** klikněte na možnost **Upravit primární uživatele**.  

1. V dialogovém okně **Upravit primární uživatele** vyhledejte a vyberte uživatele, které chcete přidat jako primární uživatele pro vybrané zařízení. Klikněte na tlačítko **Přidat**.  

    > [!NOTE]  
    > Seznam **primární uživatelé** zobrazuje uživatele, kteří jsou již primárními uživateli tohoto zařízení, a metodu, pomocí níž byl přiřazen každý vztah uživatel-zařízení.  

## <a name="set-up-primary-devices-for-a-user"></a>Nastavení primárních zařízení pro uživatele  

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **Uživatelé** .  

1. Vyberte uživatele. Na kartě **zařízení** na pásu karet vyberte možnost **Upravit primární zařízení**.  

1. V dialogovém okně **Upravit primární zařízení** vyhledejte a vyberte zařízení, která chcete přidat jako primární zařízení pro vybraného uživatele. Klikněte na tlačítko **Přidat**.  

    > [!NOTE]  
    > Seznam **primární zařízení** zobrazuje zařízení, která jsou už nastavená jako primární zařízení pro tohoto uživatele, a metodu, pomocí které se přiřazují jednotlivé vztahy mezi uživateli a zařízeními.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Automatické vytváření spřažení uživatelských zařízení (jenom osobní počítače s Windows)

Configuration Manager čte data o událostech přihlášení uživatele z protokolu událostí systému Windows. Chcete-li automaticky vytvářet spřažení uživatelských zařízení, zapněte tyto dvě možnosti v místních zásadách zabezpečení na klientských počítačích k ukládání událostí přihlášení do protokolu událostí systému Windows:  

- **Kontrola událostí přihlášení k účtu**  
- **Kontrola událostí přihlášení**  

Pro konfiguraci těchto nastavení použijte Windows Zásady skupiny.  

> [!IMPORTANT]  
> Pokud chyba způsobí, že protokol událostí systému Windows vytvoří velký počet položek, může dojít k vytvoření nového protokolu událostí. Pokud k tomuto chování dojde, nemusí být existující události přihlášení k dispozici Configuration Manager.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Nastavení lokality pro automatické vytváření spřažení uživatelských zařízení  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **nastavení klienta** .  

1. Chcete-li změnit výchozí nastavení klienta, vyberte možnost **výchozí nastavení klienta**. Na kartě **Domů** na pásu karet ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.

    Chcete-li vytvořit vlastní nastavení agenta klienta, klikněte na kartě **Domů** na pásu karet ve skupině **vytvořit** na možnost **vytvořit vlastní nastavení klientského zařízení**.

    > [!NOTE]  
    > Pokud upravíte výchozí nastavení klienta, lokalita je nasadí na všechny počítače v hierarchii. Další informace najdete v tématu [Konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).  

1. Ve skupině **spřažení uživatele a zařízení** nastavte následující nastavení:  

    - **Prahová hodnota spřažení uživatelského zařízení (minuty)**: nastavte počet minut používání zařízení předtím, než lokalita vytvoří spřažení uživatelského zařízení.  

    - **Prahová hodnota spřažení uživatelského zařízení (dny)**: nastavte počet dní, po které lokalita měří prahovou hodnotu spřažení na základě využití.  

    - **Automaticky konfigurovat spřažení zařízení a uživatele z dat o využití**: vyberte **true** , pokud chcete, aby lokalita automaticky vytvářela spřažení uživatelských zařízení. Pokud vyberete **hodnotu false**, bude nutné ručně schválit všechna přiřazení spřažení uživatelských zařízení.  

    > [!TIP]  
    > Pokud například nastavíte **prahovou hodnotu spřažení uživatelského zařízení (minuty)** na **60** minut a nastavíte **prahovou hodnotu spřažení uživatelského zařízení (dny)** na **5** dní, uživatel musí zařízení používat po dobu nejméně 60 minut během období 5 dní, aby se automaticky vytvořilo spřažení uživatelských zařízení.  

Jakmile Configuration Manager vytvoří automatické spřažení uživatelských zařízení, bude nadále monitorovat prahové hodnoty spřažení uživatelských zařízení. Pokud aktivita uživatele pro zařízení spadá pod prahové hodnoty, které jste nastavili, lokalita odebere spřažení uživatelských zařízení. Nastavte **prahovou hodnotu spřažení uživatelského zařízení (dny)** na hodnotu minimálně sedm dní. Tato konfigurace zabrání situacím, kdy může dojít ke ztrátě automaticky nakonfigurovaného spřažení uživatelského zařízení, když uživatel není přihlášený, například během víkendu.  


## <a name="import-user-device-affinities-from-a-file"></a>Import spřažení uživatelských zařízení ze souboru

Pokud chcete vytvořit mnoho relací najednou, importujte soubor, který obsahuje podrobnosti o několika spřaženích uživatelských zařízení. Ujistěte se, že je cílová zařízení již zjištěna lokalitou a zda existují jako prostředky v databázi Configuration Manager.  

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **Uživatelé** nebo **zařízení** .  

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **importovat spřažení uživatelských zařízení**.  

1. V Průvodci importem spřažení uživatelského zařízení na stránce **Vybrat mapování** nastavte tyto informace:  

    - **Název souboru**. Zadejte soubor hodnot oddělených čárkami (CSV), který obsahuje seznam uživatelů a zařízení, mezi kterými chcete vytvořit spřažení. V tomto souboru musí být každý pár uživatel-zařízení na samostatném řádku s hodnotami oddělenými čárkou. Použijte tento formát: `<domain>\<username>,<device NetBIOS name>`  

    - **Tento soubor má záhlaví sloupců pro referenční účely**. Pokud má soubor. csv záhlaví horního řádku, vyberte tuto možnost. Lokalita během importu ignoruje řádek záhlaví.  

1. Pokud importovaný soubor obsahuje více než dvě položky v každém řádku, použijte **sloupec** a **přiřadit** k určení, které sloupce reprezentují uživatele a zařízení a které sloupce budou během importu ignorovány.  

1. Dokončete průvodce.  


## <a name="let-users-create-their-own-device-affinities"></a>Umožněte uživatelům vytvářet vlastní spřažení zařízení.

Nastavte uživatele pro vytvoření vlastního spřažení uživatelských zařízení v centru softwaru.

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Nastavte lokalitu tak, aby povolovala požadavky spřažení uživatelských zařízení na uživatele.  

1 v konzole Configuration Manager přejdete do pracovního prostoru **Správa** a vyberete uzel **nastavení klienta** .  

1. Chcete-li změnit výchozí nastavení klienta, vyberte možnost **výchozí nastavení klienta**. Na kartě **Domů** na pásu karet ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.

    Chcete-li vytvořit vlastní nastavení agenta klienta, klikněte na kartě **Domů** na pásu karet ve skupině **vytvořit** na možnost **vytvořit vlastní nastavení uživatele klienta**.

    > [!NOTE]  
    > Pokud upravíte výchozí nastavení klienta, lokalita je nasadí na všechny počítače v hierarchii. Další informace najdete v tématu [Konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).  

1. Ve skupině **spřažení uživatele a zařízení** povolte nastavení povolit **uživateli definovat svá primární zařízení**.  

### <a name="set-up-a-user-device-affinity-in-software-center"></a>Nastavení spřažení uživatelských zařízení v centru softwaru

Od verze 1902 použijte centrum softwaru k nastavování spřažení.

1. V centru softwaru otevřete kartu **Možnosti** .

1. V části **pracovní informace** vyberte možnost **pravidelně používat tento počítač k práci**.

### <a name="set-up-a-user-device-affinity-in-the-application-catalog"></a>Nastavení spřažení uživatelských zařízení v katalogu aplikací

> [!Important]
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v následujících článcích:
>
> - [Konfigurace centra softwaru](../plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

1. V katalogu aplikací klikněte na možnost **Moje systémy**.  

1. Vyberte možnost, že **má tento počítač pravidelně používat k práci**.  


## <a name="manage-user-device-affinity-requests-from-users"></a>Správa uživatelských žádostí o spřažení uživatelských zařízení

Když zakážete nastavení klienta, aby se **automaticky nakonfigurovalo spřažení uživatelských zařízení z dat o využití**, musíte ručně schválit všechna přiřazení spřažení uživatelských zařízení.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Schválí nebo zamítne žádost o spřažení uživatelského zařízení.  

1. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** .  

1. Vyberte kolekci uživatelů nebo zařízení, pro kterou chcete spravovat požadavky na spřažení.  

1. Na kartě **Domů** na pásu karet ve skupině **kolekce** vyberte možnost **Spravovat požadavky na spřažení**.  

1. V dialogovém okně **Spravovat požadavky na spřažení uživatelských zařízení** vyberte požadavek na spřažení a pak zvolte **schválit** nebo **zamítnout**.  


## <a name="next-steps"></a>Další kroky

K vyhledání primárního použití zaregistrovaného zařízení můžete použít taky Microsoft Intune. Další informace najdete v tématu [vyhledání primárního uživatele zařízení v Intune](/intune/find-primary-user) v dokumentaci k Intune.