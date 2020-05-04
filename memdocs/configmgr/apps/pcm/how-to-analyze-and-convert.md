---
title: Jak analyzovat a převést balíčky
titleSuffix: Configuration Manager
description: Naučte se analyzovat a převádět balíčky pomocí Package Conversion Manageru v Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f3bf1737-827d-48fa-8bb1-f48fe71afe0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f72e7330909bc5653e69790e38ae043e539cc239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709933"
---
# <a name="how-to-analyze-and-convert-packages-with-package-conversion-manager"></a>Jak analyzovat a převádět balíčky pomocí Package Conversion Manageru

*Platí pro: Configuration Manager (Current Branch)*

<!--1357861-->

Než budete moct balíček převést, nejdřív ho Analyzujte. V závislosti na výsledcích analýzy pak můžete provést jednu z následujících úloh:

- **Převeďte** balíček na aplikaci. V seznamu **balíčků** v konzole se stav připravenosti zobrazí **automaticky**.  

- **Opravte a Převeďte** balíček, připojte kolekce a vytvořte globální podmínky. V seznamu **balíčků** v konzole se stav připravenosti zobrazí **automaticky**.  

- **Opravte a Převeďte** balíček. V seznamu **balíčků** v konzole se stav připravenosti zobrazí **ručně**.  

- Nechejte balíček převedený. V seznamu **balíčků** v konzole se stav připravenosti zobrazuje **nepoužitelné**.  



## <a name="how-to-analyze-packages"></a><a name="bkmk_analyze"></a>Jak analyzovat balíčky

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **Správa aplikací**a vyberte uzel **balíčky** .  

2. Vyberte balíček, který chcete převést. Na kartě **Domů** na pásu karet ve skupině **Převod balíčku** vyberte **analyzovat balíček**. Package Conversion Manager analyzuje balíček.  

3. Chcete-li zobrazit stav připravenosti balíčku, přidejte do seznamu balíčků sloupec **připravenosti** . Stav připravenosti balíčku určuje vaši další akci:  

    - **Automaticky**: [Jak převést balíčky](#bkmk_convert)  

        Chcete-li také připojit kolekce a vytvořit globální podmínky s **automatickým** stavem připravenosti, přečtěte si téma [Jak opravit a převést balíčky](#bkmk_fix).  

    - **Ruční**: [Jak opravit a převést balíčky](#bkmk_fix)

    - **Nelze použít**: v tomto balíčku chybí požadovaný obsah nebo program. Přidejte všechny chybějící obsahy nebo programy a proveďte analýzu znovu. Nebo ho nechte v nepřevedeném stavu a pokračujte v jeho nasazení jako balíček.  

    - **Neznámé**: Nejdřív spusťte úlohu **analyzovat** nebo počkejte na další naplánovanou analýzu. Pokud se stav nezmění, přečtěte si téma [řešení potíží s balíčkem Package Conversion Manager](troubleshoot-pcm.md).<!-- SCCMDocs#2044 -->

## <a name="how-to-convert-packages"></a><a name="bkmk_convert"></a>Jak převést balíčky

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **Správa aplikací**a vyberte uzel **balíčky** .  

2. Vyberte balíček, který se má převést se stavem připravenosti **automaticky**. Na kartě **Domů** na pásu karet ve skupině **Převod balíčku** vyberte **převést balíček**. Otevře se Průvodce převodem balíčku do aplikace.  

3. V Průvodci převodem balíčku do aplikace zkontrolujte seznam vybraných balíčků. Odeberte všechny balíčky, které nechcete převést, a vyberte **OK**. Package Conversion Manager převede balíček. V okně převod je dokončen seznam stavů převodu nových aplikací.  

    > [!Note]  
    > Když balíček převedete, lokalita zaznamená datum a čas převodu jako čas UTC.  

4. Postupujte podle pokynů v okně. Vyberte možnost **Zobrazit aplikace** nebo **Zavřít**.  



## <a name="how-to-fix-and-convert-packages"></a><a name="bkmk_fix"></a>Oprava a převod balíčků

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **Správa aplikací**a vyberte uzel **balíčky** .  

2. Vyberte balíček se stavem připravenosti **ručně** nebo **automaticky**. Na kartě **Domů** na pásu karet ve skupině **Převod balíčku** vyberte **opravit a převést**.  

3. V Průvodci převodem balíčku si přečtěte informace na stránce **Výběr balíčku** , kde najdete seznam **položek, které se mají opravit**. Pak vyberte **Další**.  

4. Na stránce **Kontrola závislosti** zkontrolujte, jestli je balíček závislý na jiných uvedených balíčcích, a pak vyberte **Další**.  

    > [!Note]  
    > Pokud jste nepřevedli žádný z uvedených závislých balíčků, nejprve tyto balíčky převeďte. Pak restartujte proces převodu balíčku.  
    >  
    > Pokud závislost není povinná, odstraňte ji nebo ji ignorujte a pokračujte v procesu převodu.  

5. Na stránce **typ nasazení** Zkontrolujte typy nasazení pro novou aplikaci. Změňte jejich priority nebo odstraňte typy nasazení.  

6. Pokud některý z nových typů nasazení nemá přidruženou metodu detekce, ve sloupci **Metoda zjišťování** se zobrazí ikona upozornění. Proveďte následující akce:  

    1. Vyberte možnost **Upravit metodu detekce**.  

    2. Vyberte **Přidat**.  

    3. V dialogovém okně pravidlo detekce zadejte **Typ nastavení**.  

    4. Pro zadaný typ nastavení zadejte další informace požadované pro pravidlo zjišťování.  

    5. Vyberte **OK**. V případě potřeby tento postup opakujte, chcete-li do každého typu nasazení přidat více metod detekce.  

    6. Vyberte **OK**. Ověřte, zda se ve sloupci **Metoda zjišťování** zobrazuje ikona potvrzující správně zadanou metodu zjišťování.  

7. Vyberte **Další**.  

8. Na stránce **Výběr požadavků** Zkontrolujte typy nasazení nové aplikace. Vyberte typ nasazení a zkontrolujte požadavky pro daný typ nasazení.  

    > [!Note]  
    > Průvodce zobrazí pouze požadavky, které převádí Package Conversion Manager. Nepřevádí všechny dotazy WQL v kolekcích zařízení na požadavky.  

9. V případě potřeby přidejte požadavky pro vybraný typ nasazení.  

10. Vyberte **Další**.  

11. Dokončete průvodce, aby se vytvořila aplikace.  

    > [!Note]  
    > Když balíček převedete, lokalita zaznamená datum a čas převodu jako čas UTC.  



## <a name="monitor"></a><a name="bkmk_monitor"></a>Sledován

V konzole Configuration Manager otevřete pracovní prostor **monitorování** a vyberte **stav konverze balíčku**. Tento řídicí panel zobrazuje celkový stav analýzy a převodu balíčků v lokalitě. Nová úloha na pozadí automaticky shrnuje data analýzy.

> [!Tip]  
> Package Conversion Manager integrovaný s Configuration Manager nevyžaduje, abyste naplánovali analýzu balíčků. Tato akce je zpracována integrovanou úlohou Shrnutí.

![Snímek obrazovky ukázkového řídicího panelu stavu převodu balíčku](media/1357861-pcm-dashboard.png)
