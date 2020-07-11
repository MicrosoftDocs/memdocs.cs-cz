---
title: Vytváření položek konfigurace profilů a dat uživatelů
titleSuffix: Configuration Manager
description: Pomocí položek konfigurace profilů a dat v Configuration Manager můžete spravovat přesměrování složek, offline soubory a profily roamingu.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 51c97ae3cd947e0bdfa82c595cb6446351412d21
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240367"
---
# <a name="create-user-data-and-profiles-configuration-items-in-configuration-manager"></a>Vytvoření položek konfigurace profilů a dat uživatele v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Položky konfigurace profilů a dat uživatele v Configuration Manager obsahují nastavení, která můžou spravovat přesměrování složek, offline soubory a cestovní profily na počítačích se systémem Windows 8 a novějším pro uživatele ve vaší hierarchii. Můžete například:  

- Přesměrujte složku Dokumenty uživatele do sdílené síťové složky.  

- Ujistěte se, že zadané soubory uložené v síti jsou k dispozici v počítači uživatele, když není k dispozici síťové připojení.  

- Konfigurovat, které soubory v cestovním profilu uživatele se synchronizují se sdílenou síťovou složkou, když se uživatel přihlásí nebo vypíná.  

  Na rozdíl od jiných položek konfigurace v Configuration Manager nepřidáte položky konfigurace profilů a dat uživatele do standardních hodnot konfigurace, které potom nasadíte. Místo toho nasadíte položky konfigurace přímo pomocí dialogového okna **Nasadit položku konfigurace profilů a dat uživatele** .  

> [!IMPORTANT]  
>  Položky konfigurace profilů a dat uživatele jde nasadit jenom do kolekce uživatelů.  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>Povolení profilů a dat uživatele pro nastavení dodržování předpisů  
 Pomocí následujícího postupu nakonfigurujete výchozí nastavení klienta pro nastavení dodržování předpisů profilů a dat uživatele, které bude platit pro všechny počítače ve vaší hierarchii. Pokud chcete toto nastavení použít jenom pro některé počítače, vytvořte vlastní nastavení klientského zařízení a přiřaďte ho ke kolekci obsahující počítače, pro které chcete použít nastavení dodržování předpisů profilů a dat uživatele. Další informace o tom, jak vytvořit vlastní nastavení zařízení, najdete v tématu [Postup konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).  

1.  V konzole Configuration Manager klikněte na **Správa**  >  **nastavení klienta**  >  **výchozí nastavení**.  

4.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

5.  V dialogovém okně **Výchozí nastavení** klikněte na **Nastavení dodržování předpisů**.  

6.  Z rozevíracího seznamu **Povolit profily a data uživatelů** vyberte **Ano**.  

7.  Kliknutím na **OK** zavřete dialogové okno **Výchozí nastavení** .  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>Vytvoření položky konfigurace profilů a dat uživatele  

1. V konzole Configuration Manager klikněte na **prostředky a**dodržování předpisů  >  **Nastavení dodržování**předpisů  >  **uživatelská data a profily**.  

2. Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit uživatelská data a položku konfigurace profilu**.  

3. Na stránce **Obecné** v **Průvodci vytvořením položky konfigurace profilů a dat uživatele**zadejte následující informace:  

   -   **Název** : Zadejte jedinečný název položky konfigurace. Opět můžete použít maximálně 256 znaků.  

   -   **Popis:** Zadejte popis, který poskytuje přehled položky konfigurace, a další důležité informace, které ji pomáhají identifikovat v konzole Configuration Manager. Opět můžete použít maximálně 256 znaků.  

   -   **Přesměrování složky:** Toto políčko zaškrtněte, pokud chcete pro tuto položku konfigurace nakonfigurovat nastavení pro přesměrování složky.  

   -   **Offline soubory:** Toto políčko zaškrtněte, pokud chcete pro tuto položku konfigurace nakonfigurovat nastavení pro offline soubory.  

   -   **Uživatelské profily roamingu:** Toto políčko zaškrtněte, pokud chcete pro tuto položku konfigurace nakonfigurovat nastavení pro uživatelské profily roamingu.  

4. Na stránce **Přesměrování složky** v **Průvodci vytvořením položky konfigurace profilů a dat uživatele**zadejte, jak chcete, aby klientské počítače uživatelů, kteří přijmou tuto položku konfigurace, spravovaly přesměrování složky. Můžete nakonfigurovat nastavení pro jakékoli zařízení, na které se uživatel přihlašuje, nebo jenom pro primární zařízení uživatele. Další informace o přesměrování složky najdete v dokumentaci k Windows Serveru.  

   > [!NOTE]  
   >  Tato stránka se zobrazí pouze v případě, že jste kontrolovali **Přesměrování složky** na stránce **Obecné** v průvodci.  

5. Na stránce **Offline soubory** v **Průvodci vytvořením položky konfigurace profilů a dat uživatele**můžete povolit nebo zakázat používání offline souborů pro uživatele, kteří přijmou tuto položku konfigurace a nastavení konfigurace pro chování offline souborů. Můžete také zadat offline soubory, které budou vždy k dispozici na všech počítačích, ke kterým se uživatel přihlásí. Další informace o offline souborech najdete v dokumentaci k Windows Serveru.  

   > [!NOTE]  
   >  Tato stránka se zobrazí pouze v případě, že jste zaškrtli políčko **offline soubory** na stránce **Obecné** v průvodci.  

6. Na stránce **Profily roamingu** v **Průvodci vytvořením položky konfigurace profilů a dat uživatele**můžete nakonfigurovat, jestli budou profily roamingu k dispozici na počítačích, ke kterým se uživatel přihlásí, a taky konfigurovat další informace o chování těchto profilů. Další informace o profilech roamingu najdete v dokumentaci k Windows Serveru.  

   > [!NOTE]  
   >  Tato stránka se zobrazí pouze v případě, že jste zaškrtli políčko **cestovní profily uživatelů** na stránce **Obecné** v průvodci.  

7. Dokončete průvodce.  

   Nová položka konfigurace profilů a dat uživatele se zobrazí v uzlu **Profily a data uživatelů** pracovního prostoru **Prostředky a kompatibilita** .  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>Nasazení položky konfigurace profilů a dat uživatele  

1.  V konzole Configuration Manager klikněte na **prostředky a**dodržování předpisů  >  **Nastavení dodržování**předpisů  >  **uživatelská data a profily**.  

3.  Vyberte položku konfigurace profilů a dat uživatele, kterou chcete nasadit, a potom na kartě **Domů** ve skupině **Nasazení** klikněte na **Nasadit**.  

4.  V dialogovém okně **Nasadit položku konfigurace profilů a dat uživatele** zadejte následující informace.  

    -   **Kolekce** – Kliknutím na **Procházet** vyberte kolekci uživatelů, do které chcete nasadit položku konfigurace.  

        > [!IMPORTANT]  
        >  Položky konfigurace profilů a dat uživatele jde nasadit jenom do kolekce uživatelů.  

    -   **Napravit pravidla nesplňující požadavky, je-li to podporováno** – Tuto možnost povolte, když chcete automaticky opravit všechna pravidla, která se na klientských počítačích vyhodnotí jako nekompatibilní.  

    -   **Povolit nápravu mimo okno údržby** – Pokud je pro kolekci, do které nasazujete položku konfigurace, nakonfigurované časové období údržby, povolením této možnosti umožníte nastavení dodržování předpisů napravit hodnotu mimo časové období údržby. Další informace o časových obdobích údržby najdete v tématu [použití časových období](../../core/clients/manage/collections/use-maintenance-windows.md)údržby.  

    -   **Generovat upozornění** – Tuto možnost povolte, pokud chcete, aby se vygenerovala výstraha v případě, že dodržování předpisů položky konfigurace je k určenému datu a v určeném čase nižší než zadané procento. Také můžete zvolit, zda chcete zasílat výstrahu do nástroje System Center Operations Manager.  

    -   **Zadejte plán vyhodnocení shody pro tuto položku konfigurace** – Určuje plán, podle kterého je nasazená položka konfigurace vyhodnocovaná u klientských počítačů. Může se jednat o jednoduchý nebo vlastní plán.  

5.  Kliknutím na **OK** zavřete dialogové okno **Nasadit položku konfigurace profilů a dat uživatele** a vytvořte nasazení.  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>Monitorování položky konfigurace profilů a dat uživatele  
 Tento typ položky konfigurace můžete monitorovat stejným způsobem, jakým sledujete ostatní nastavení dodržování předpisů.  

 Další informace najdete v tématu [Postup monitorování nastavení dodržování předpisů](../../compliance/deploy-use/monitor-compliance-settings.md).  
