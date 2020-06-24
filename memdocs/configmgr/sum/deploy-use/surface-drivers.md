---
title: Správa aktualizací ovladačů Surface
titleSuffix: Configuration Manager
description: Configuration Manager synchronizuje aktualizace ovladačů Surface pro nasazení na zařízeních Surface.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9f9f4e6-5b4f-4b8f-94d6-db9b2b239113
ms.openlocfilehash: 04793a053e85be051ce9ffafd2f15d274cf166f0
ms.sourcegitcommit: c7afcc3a2232573091c8f36d295a803595708b6c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2020
ms.locfileid: "84973073"
---
# <a name="manage-surface-drivers-with-configuration-manager"></a>Správa ovladačů Surface pomocí Configuration Manager

*Platí pro: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager umožňuje synchronizovat ovladače pro zařízení Surface a nasazovat je jako aktualizace softwaru. Tato funkce umožňuje zajistit, aby vaše zařízení Surface používala nejnovější dostupné ovladače. Tato synchronizace byla poprvé představena ve verzi 1706 jako předběžná verze a stala se funkcí v 1710. <!--3684621, 3608197, 1098490-->

## <a name="prerequisites-for-synchronizing-surface-drivers"></a>Předpoklady pro synchronizaci ovladačů Surface

- Internetový bod aktualizace softwaru s připojením nejvyšší úrovně.
- Všechny body aktualizace softwaru musí používat Windows Server 2016 s nainstalovanou kumulativní aktualizací KB4025339 nebo novější.
- Configuration Manager ve výchozím nastavení nepovolí tuto volitelnou funkci. Před použitím této funkce tuto funkci povolte. Další informace naleznete v části [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="enable-sync-for-surface-drivers"></a>Povolit synchronizaci pro ovladače Surface

Pokud chcete povolit synchronizaci ovladačů Surface, postupujte podle následujících kroků:

1. Připojte konzolu Configuration Manageru k serveru lokality nejvyšší úrovně.
1. Přejděte na **Správa**  >  **Konfigurace lokality**  >  **lokality**a pak klikněte na lokalitu nejvyšší úrovně.
1. Na pásu karet vyberte **Nastavení**  >  **Konfigurovat součásti lokality**  >  **bod aktualizace softwaru**.
1. Klikněte na kartu **klasifikace** a potom zaškrtněte políčko **zahrnout ovladače Microsoft Surface a aktualizace firmwaru** a klikněte na **použít**.

     ![Povolit ovladače Surface z vlastností bodu aktualizace softwaru](media/enable-surface-driver-sync.png)

1. Ve vlastnostech komponenty bodu aktualizace softwaru klikněte na kartu **produkty** . Další informace najdete v části [produkty pro ovladače Surface](#bkmk_prod) a [modely Surface](#bkmk_models) .
1. Vyberte produkty pro každou verzi Windows 10, pro kterou chcete podporovat ovladače Surface. Všimněte si, že existují dvě různé verze jednotlivých produktů pro ovladače:

   - Aktualizace *verze* Windows 10 **a novější ovladače pro údržbu**
   - Aktualizace *verze* Windows 10 **a pozdější upgrade & ovladačů pro obsluhu**.

     ![Seznam produktů pro ovladače verzí Windows 10](media/surface-driver-products-sup.png)

1. Po dokončení výběru produktů klikněte na tlačítko **OK**.
1. [Synchronizujte bod aktualizace softwaru](../get-started/synchronize-software-updates.md) , aby se ovladače surface Configuration Manager.
1. Jakmile jsou ovladače Surface synchronizované, nasaďte je stejným způsobem jako ostatní aktualizace.

## <a name="products-for-surface-drivers"></a><a name="bkmk_prod"></a>Produkty pro ovladače Surface

Většina ovladačů patří do následujících skupin produktů:

- Ovladače Windows 10 a novější verze
- Windows 10 a novější upgrade & ovladačů pro obsluhu
- Windows 10 – aktualizace pro výročí a novější – ovladače pro údržbu
- Windows 10 – aktualizace pro výročí a pozdější upgrade & ovladačů pro obsluhu
- Windows 10 Creators Update a novější obslužné ovladače
- Windows 10 Creators Update a novější upgrade & ovladačů pro obsluhu
- Windows 10 zapadá na aktualizace Creators Update a novějších ovladačů údržby
- Windows 10 je Creators Update a novější upgrade & ovladačů pro obsluhu.
- Ovladače pro obsluhu Windows 10 S a novější
- Windows 10 S verze 1709 a novější – ovladače údržby pro testování
- Windows 10 S verze 1709 a novější upgrade & ovladačů pro testování
- Windows 10 S verze 1803 a novější – ovladače pro údržbu
- Windows 10 S verze 1803 a novější upgrade & ovladačů pro obsluhu
- Windows 10 S verze 1809 a novější – ovladače pro obsluhu
- Windows 10 S verze 1809 a novější, upgrade & ovladačů pro obsluhu
- Windows 10 S verze 1903 a novější – ovladače pro obsluhu
- Windows 10 S verze 1903 a novější, upgrade & ovladačů pro obsluhu
- Windows 10 verze 1803 a novější – ovladače pro údržbu
- Windows 10 verze 1803 a novější upgrade & ovladačů pro obsluhu
- Windows 10 verze 1809 a novější – ovladače pro obsluhu
- Windows 10 verze 1809 a novější, upgrade & ovladačů pro obsluhu
- Windows 10 verze 1903 a novější – ovladače pro obsluhu
- Windows 10 verze 1903 a novější, upgrade & ovladačů pro obsluhu

> [!NOTE]
> Většina ovladačů Surface patří do více skupin produktů Windows 10. Možná nemusíte vybírat všechny produkty, které jsou tady uvedené. Chcete-li snížit počet produktů, které naplňují katalog aktualizací, doporučujeme, abyste pro synchronizaci vybrali pouze produkty, které jsou požadovány pro vaše prostředí.

## <a name="surface-models"></a><a name="bkmk_models"></a>Modely Surface

Následující tabulka obsahuje modely Surface a verze Windows 10, na kterých Configuration Manager můžou instalovat ovladače. Aktualizace ovladačů Surface nejsou k dispozici v Configuration Manager stejný den, kdy jsou publikovány do katalogu Microsoft Update. Configuration Manager udržuje svůj vlastní seznam ovladačů Surface, které budou naimportovány. Jsou popsána zařízení, která vyžadují produkty Windows 10 S. Společnost Microsoft se zaměřuje na přidání ovladačů Surface do seznamu povolených druhých úterý každý měsíc, aby byly k dispozici pro synchronizaci Configuration Manager. Další informace najdete v článku [Nejčastější dotazy](#bkmk_faq).

</br>

|Model Surface|Systém Windows 10 1709| Systém Windows 10 1803|Systém Windows 10 1809|Systém Windows 10 1903|Systém Windows 10 1909|
|----|----|----|----|----|----|
|Povrchový pro 3|Ano| Ano| Ano |Ano|Ano|
|Plocha pro 4|Ano| Ano| Ano |Ano|Ano|
|Plocha pro 6|–| Ano| Ano |Ano|Ano|
|Plocha pro 7|–| –| – |Ano|Ano|
|Plocha pro X|–| –| – |Ano|Ano|
|Povrchová kniha|Ano| Ano| Ano |Ano|Ano|
|Povrchový kniha 2|Ano| Ano| Ano |Ano|Ano|
|Povrchový kniha 3|–| –| – |Ano|Ano|
|Surface notebooku|Ano, je vybrána položka "Windows 10 S verze 1709 a novější ovladače pro údržbu".| Ano, je vybrána položka "Windows 10 S verze 1803 a novější ovladače pro údržbu".|Ano, s produktem "Windows 10 S verze 1809 a novější upgrade & vybrané ovladače pro obsluhu"|Ano, s produktem "Windows 10 S verze 1903 a novější upgrade & vybrané ovladače pro obsluhu"|Ano, s produktem "Windows 10 S verze 1903 a novější upgrade & vybrané ovladače pro obsluhu"|
|Surface notebooku 2|–| Ano |Ano|Ano|Ano|
|Surface notebook 3|–| –|–|Ano |Ano|
|Přejít na plochu|–| Ano, je vybrána položka "Windows 10 S verze 1803 a novější ovladače pro údržbu".|Ano, s produktem "Windows 10 S verze 1809 a novější upgrade & vybrané ovladače pro obsluhu"|Ano, s produktem "Windows 10 S verze 1903 a novější upgrade & vybrané ovladače pro obsluhu"|Ano, s produktem "Windows 10 S verze 1903 a novější upgrade & vybrané ovladače pro obsluhu"|
|Plocha – přejít 2|–| –| Ano |Ano|Ano, s produktem "Windows 10 S verze 1903 a novější upgrade & vybrané ovladače pro obsluhu"|
|Plocha – Studio|Ano| Ano| Ano |Ano|Ano|
|Plocha Studio 2|–| Ano| Ano |Ano|Ano|

## <a name="verify-the-configuration"></a>Ověření konfigurace

Chcete-li ověřit, zda je bod aktualizace softwaru správně nakonfigurován, použijte **souboru wsyncmgr. log** a **WCM. log**.

1. Otevřete souboru wsyncmgr. log a vyhledejte následující položku protokolu:

    ```text
    Surface Drivers can be supported in this hierarchy since all software update points are on Windows Server 2016, WCM SCF property Sync Catalog Drivers is set. 
    …
    Sync Catalog Drivers SCF value is set to : 1
    ```

1. Pokud se do **souboru wsyncmgr. log**přihlásí jedna z následujících položek, dvakrát ověřte, že jste ve vlastnostech bodu aktualizace softwaru vybrali možnost **zahrnout ovladače a aktualizace firmwaru společnosti Microsoft** :
   - `Sync Surface Drivers option is not set`
   - `Sync Catalog Drivers SCF value is set to : 0`

1. Otevřete **WCM. log** a vyhledejte položky podobné následujícím položkám:
   ```text
   <Categories>
   <Category Id="Product:05eebf61-148b-43cf-80da-1c99ab0b8699"><![CDATA[Windows 10 and later drivers]]></Category>
   <Category Id="Product:06da2f0c-7937-4e28-b46c-a37317eade73"><![CDATA[Windows 10 Creators Update and Later Upgrade & Servicing Drivers]]></Category>
   <Category Id="Product:c1006636-eab4-4b0b-b1b0-d50282c0377e"><![CDATA[Windows 10 S and Later Servicing Drivers]]></Category>
   … …
   </Categories>
   ```

   Tato položka je element XML, který obsahuje seznam všech skupin produktů a klasifikace, které jsou aktuálně synchronizovány serverem bodu aktualizace softwaru. Pokud nemůžete najít produkty, které jste vybrali, dvakrát ověřte, zda jsou uloženy produkty pro bod aktualizace softwaru.
1. Můžete také počkat na dokončení další synchronizace. Potom zkontrolujte, zda jsou ovladače povrchu a aktualizace firmwaru uvedeny v části aktualizace softwaru v konzole Configuration Manager. Například konzola může zobrazit následující informace: ![ synchronizované ovladače Surface v konzole Configuration Manageru.](media/synchronized-surface-drivers.png)

##  <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a>Nejčastější dotazy – Nejčastější dotazy

### <a name="after-i-follow-the-steps-in-this-article-my-surface-drivers-are-still-not-synchronized-why"></a>Po provedení kroků v tomto článku pořád nejsou synchronizované ovladače Surface. Proč?

Pokud synchronizujete z nadřazeného serveru Windows Server Update Services (WSUS), místo Microsoft Update se ujistěte, že je nadřazený server WSUS nakonfigurovaný tak, aby podporoval a synchronizoval aktualizace ovladačů Surface. Všechny podřízené servery jsou omezené na aktualizace, které jsou k dispozici v nadřazené databázi serveru WSUS.

Existuje více než 68 000 aktualizací, které jsou klasifikovány jako ovladače ve službě WSUS. Abyste zabránili synchronizaci ovladačů nesouvisejících s plochou od Configuration Manager, proveďte synchronizaci ovladačů Microsoft Filters se seznamem povolených. Po publikování a začlenění nového seznamu povolených součástí do nástroje Configuration Manager jsou nové ovladače přidány do konzoly následující při příští synchronizaci. Společnost Microsoft se zaměřuje na přidání ovladačů Surface do seznamu povolených druhých úterý každý měsíc, aby byly k dispozici pro synchronizaci Configuration Manager.

Pokud je prostředí Configuration Manager v režimu offline, importuje se nový seznam povolených pokaždé, když naimportujete [aktualizace údržby](../../core/servers/manage/use-the-service-connection-tool.md) do Configuration Manager. Bude také nutné importovat [Nový katalog služby WSUS](../get-started/synchronize-software-updates-disconnected.md) , který obsahuje ovladače před tím, než se aktualizace zobrazí v konzole Configuration Manager. Protože samostatné prostředí WSUS obsahuje více ovladačů než Configuration Manager SUP, doporučujeme vytvořit Configuration Manager prostředí, které obsahuje možnosti online, a nakonfigurovat ho tak, aby synchronizoval ovladače Surface. To poskytuje menší export služby WSUS, který se velmi podobá prostředí offline.

Pokud je vaše Configuration Manager prostředí online a dokáže detekovat nové aktualizace, automaticky se zobrazí aktualizace tohoto seznamu. Pokud nevidíte očekávané ovladače, přečtěte si prosím v protokolu WCM. log a souboru wsyncmgr. log případné chyby synchronizace.

### <a name="my-configuration-manager-environment-is-offline-can-i-manually-import-surface-drivers-into-wsus"></a>Moje Configuration Manager prostředí je offline, můžu ovladače Surface ručně importovat do služby WSUS?

Ne. I v případě, že je aktualizace naimportována do služby WSUS, aktualizace nebude naimportována do konzoly Configuration Manager pro nasazení, pokud není uvedena v seznamu povolených. Chcete-li aktualizovat seznam povolených služeb, je nutné použít [Nástroj pro připojení služby](../../core/servers/manage/use-the-service-connection-tool.md) k importu aktualizací údržby Configuration Manager.

### <a name="what-alternative-methods-do-i-have-to-deploy-surface-driver-and-firmware-updates"></a>Jaké alternativní metody mám nasadit ovladače a aktualizace firmwaru?

Informace o tom, jak nasadit ovladače Surface a aktualizace firmwaru pomocí alternativních kanálů, najdete v tématu [Správa ovladačů Surface a aktualizací firmwaru](https://docs.microsoft.com/surface/manage-surface-driver-and-firmware-updates). Pokud chcete stáhnout soubor. msi nebo. exe a pak ho nasadit pomocí tradičních kanálů nasazení softwaru, přečtěte si téma [uchování aktualizovaného firmwaru surface Configuration Manager](https://docs.microsoft.com/archive/blogs/thejoncallahan/keeping-surface-firmware-updated-with-configuration-manager).

## <a name="next-steps"></a>Další kroky

Další informace o ovladačích Surface najdete v následujících článcích:

- [Požadavky na Surface a System Center Configuration Manager](https://docs.microsoft.com/surface/considerations-for-surface-and-system-center-configuration-manager#deploy-surface-app-with-configuration-manager)
- [Historie aktualizací povrchu](https://support.microsoft.com/help/4036283/surface-surface-update-history)
- [Stažení nejnovějšího firmwaru a ovladačů pro zařízení Surface](https://docs.microsoft.com/surface/deploy-the-latest-firmware-and-drivers-for-surface-devices)
