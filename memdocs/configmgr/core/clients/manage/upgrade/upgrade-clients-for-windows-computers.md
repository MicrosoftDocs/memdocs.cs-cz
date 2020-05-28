---
title: Upgrade klientů ve Windows
titleSuffix: Configuration Manager
description: Upgradujte klienty v počítačích se systémem Windows v Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3849f360b2f22f2f48bbe49159b610399158b29
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427767"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>Postup upgradu klientů pro počítače se systémem Windows v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Upgradujte klienta Configuration Manager v počítačích s Windows pomocí metod instalace klienta nebo funkce automatického upgradu klienta. Následující metody instalace klienta jsou platné způsoby upgradu klientského softwaru v počítačích se systémem Windows:  

- Instalace zásad skupiny  

- Instalace skriptu přihlášení  

- Ruční instalace  

- Instalace upgradu  

Další informace najdete v tématu [nasazení klientů do počítačů se systémem Windows](../../deploy/deploy-clients-to-windows-computers.md).

Vylučte klienty z upgradu zadáním kolekce vyloučení. Další informace najdete v tématu [jak vyloučit klienty z upgradu](exclude-clients-windows.md). Vyloučení klienti si pořád stahují a spouštějí CCMSETUP, ale neupgradují.

> [!TIP]  
> Pokud upgradujete serverovou infrastrukturu z předchozí verze Configuration Manager, před upgradem klientů Configuration Manager dokončete upgrade serveru. Tento proces zahrnuje instalaci všech aktualizací aktuální větve. Nejnovější aktualizace aktuální větve obsahuje nejnovější verzi klienta. Upgradujte klienty po instalaci všech aktualizací Configuration Manager.

> [!NOTE]
> Pokud plánujete změnit přiřazení lokality pro klienty během upgradu, zadejte novou lokalitu pomocí `SMSSITECODE` vlastnosti Client. msi. Použijete-li hodnotu `AUTO` pro `SMSSITECODE` , zadejte také `SITEREASSIGN=TRUE` . Tato vlastnost umožňuje automatické opětovné přiřazení lokality během upgradu. Další informace najdete v tématu [vlastnosti instalace klienta – SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="about-automatic-client-upgrade"></a><a name="bkmk_autoupdate"></a>Informace o automatickém upgradu klientů

Nakonfigurujte lokalitu tak, aby automaticky upgradovali klienty na nejnovější verzi Configuration Manager. Když Configuration Manager identifikuje přiřazenou verzi klienta starší než verze hierarchie, automaticky upgraduje klienta. Tento scénář zahrnuje upgrade klienta na nejnovější verzi při pokusu o přiřazení k Configuration Manager lokalitě.  

Klient nástroje se může automaticky upgradovat v následujících scénářích:  

- Verze klienta je starší než verze použitá v hierarchii.  

- V klientovi v lokalitě centrální správy (CAS) je nainstalována jazyková sada a stávající klient nástroje nikoli.  

- Požadavek klienta v hierarchii má jinou verzi než požadavek nainstalovaný v klientovi.  

- Verze jednoho nebo více instalačních souborů klienta se liší.  

> [!NOTE]  
> Chcete-li identifikovat různé verze klienta Configuration Manager ve vaší hierarchii, použijte **Počet sestav Configuration Manager klientů podle verzí klientů** ve složce sestav **lokalita-informace o klientech**.  

Ve výchozím nastavení vytvoří Configuration Manager balíček s upgradem. Tento balíček automaticky odešle do všech distribučních bodů v hierarchii. Pokud provedete změny klientského balíčku na certifikačních autoritách, Configuration Manager balíček automaticky aktualizuje a znovu ho distribuuje. Tato změna je příkladem, když přidáte jazykovou sadu klienta. Pokud povolíte automatický upgrade klienta, každý klient automaticky nainstaluje nový balíček jazyka klienta.

> [!NOTE]  
> Configuration Manager automaticky neodešle balíček upgradu klienta, aby Configuration Manager cloudové distribuční body.  

Povolte automatický upgrade klienta napříč vaší hierarchií. Tato konfigurace udržuje klienty v aktuálním stavu s menší námahou.  

Pokud spravujete Configuration Manager systémy lokality jako klienty, určete, jestli se mají zahrnout jako součást procesu automatického upgradu. Z upgradu klienta můžete vyloučit všechny servery nebo konkrétní kolekci. Některé Configuration Manager role lokality sdílejí rozhraní klienta. Například bod správy a distribuční bod pro vyžádání obsahu. Tyto role se při aktualizaci lokality aktualizují, takže se verze klienta na těchto serverech aktualizuje současně.

## <a name="configure-automatic-client-upgrade"></a><a name="bkmk_configure"></a>Konfigurace automatického upgradu klienta

Pomocí následujícího postupu můžete nakonfigurovat automatický upgrade klienta v certifikačních autoritách. Tato konfigurace platí pro všechny klienty ve vaší hierarchii.  

1. V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a pak vyberte uzel **lokality** .  

1. Na kartě **Domů** na pásu karet ve skupině **lokality** vyberte **Nastavení hierarchie**.  

1. Přepněte na kartu **upgrade klienta** . Zkontrolujte verzi a datum produkčního klienta. Ujistěte se, že se jedná o verzi, kterou chcete použít k upgradu klientů. Pokud to není očekávaná verze klienta, budete možná muset zvýšit úroveň předprodukčního klienta na produkční. Další informace najdete v tématu [testování upgradu klienta v předprodukční kolekci](test-client-upgrades.md).  

1. Vyberte **upgradovat všechny klienty v hierarchii pomocí produkčního klienta**. Vyberte **OK**. Tím akci potvrdíte.  

1. Pokud nechcete, aby se upgrady klientů na servery projevily, vyberte možnost **neupgradovat servery**.  

1. Zadejte počet dní, ve kterých musí zařízení upgradovat klienta. Jakmile zařízení obdrží zásadu, upgraduje klienta v náhodném intervalu během tohoto počtu dnů. Toto chování brání současnému upgradu velkého počtu klientů.

    > [!NOTE]
    > Aby bylo možné upgradovat klienta nástroje, musí být spuštěný počítač. Pokud počítač neběží, když je naplánováno přijetí upgradu, upgrade se neprojeví. Když se počítač zapne a obdrží zásadu, naplánuje upgrade na náhodný čas během povoleného počtu dnů. Pokud k tomu dojde po vypršení časového limitu pro uplynulý počet dní k upgradu, naplánujte upgrade na náhodný čas během 24 hodin po zapnutí počítače.
    >
    > Kvůli tomuto chování mohou počítače, které jsou rutinně vypnuty, trvat déle, než se očekává, pokud čas náhodného upgradu není v normální pracovní době.

1. Chcete-li vyloučit klienty z upgradu, vyberte možnost **vyloučit zadané klienty z upgradu**a určete kolekci, která má být vyloučena. Další informace najdete v tématu [vyloučení klientů z upgradu](exclude-clients-windows.md).

1. Pokud chcete, aby lokalita zkopírovala instalační balíček klienta do distribučních bodů, které jste povolili pro [připravený obsah](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent), vyberte možnost **automaticky distribuovat klientský instalační balíček do distribučních bodů, které jsou povoleny pro připravený obsah**.  

1. Výběrem **OK** uložte nastavení a zavřete vlastnosti nastavení hierarchie.

Klienti obdrží tato nastavení při dalším stažení zásady.

> [!NOTE]
> Upgrady klientů dodržují všechna Configuration Manager okna údržby, která jste nakonfigurovali. Vlákno Execmgr spustí během časového období údržby pouze zaváděcí program pro instalaci klienta (CCMSetup. exe). Pokud zařízení používá edici Windows s filtrem zápisu, program CCMSetup se pokusí stáhnout a nainstalovat současně. V opačném případě bude program CCMSetup náhodně vymezit čas ke stažení obsahu. Po stažení obsahu a kompilování místních zásad Execmgr plánuje upgrade klienta během příštího časového období údržby.<!-- SCCMDocs#896 -->

## <a name="next-steps"></a>Další kroky

Alternativní metody upgradu klientů najdete v tématu [nasazení klientů do počítačů se systémem Windows](../../deploy/deploy-clients-to-windows-computers.md).

Vylučte z automatického upgradu konkrétní klienty. Další informace najdete v tématu [jak vyloučit klienty z upgradu](exclude-clients-windows.md).
