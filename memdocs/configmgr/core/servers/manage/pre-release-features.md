---
title: Předběžné verze funkcí
titleSuffix: Configuration Manager
description: Předběžné verze funkcí jsou funkce, které jsou v aktuální větvi pro prvotní testování v produkčním prostředí.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e341fab9f76ab6994f051dbd5e2333c3f521b4d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720153"
---
# <a name="pre-release-features-in-configuration-manager"></a>Funkce předběžné verze v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Předběžné verze funkcí jsou funkce, které jsou v aktuální větvi pro prvotní testování v produkčním prostředí. Tyto funkce jsou plně podporovány, ale stále v aktivním vývoji. Mohou obdržet změny, dokud nebudou přesunuty mimo kategorii před prodejem.

## <a name="give-consent"></a>Udělení souhlasu  

Než začnete používat předběžné verze funkcí, poskytněte souhlas s používáním předběžných verzí funkcí. Poskytnutí souhlasu je jednorázová akce na hierarchii, kterou nelze vrátit zpět. Dokud neudělíte souhlas, nebudete moci povolit nové předběžné verze funkcí, které jsou součástí aktualizací. Když zapnete funkci před vydáním, nebudete ji moct vypnout.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2. Na pásu karet klikněte na **Nastavení hierarchie** .  

3. Na kartě **Obecné** ve vlastnostech nastavení hierarchie povolte možnost **souhlasu s používáním předběžných verzí funkcí**. Klikněte na tlačítko **OK**.  

## <a name="enable-pre-release-features"></a>Povolit funkce předběžné verze

Když nainstalujete aktualizaci, která zahrnuje předběžné verze funkcí, tyto funkce se zobrazí v průvodci aktualizacemi a údržbou s běžnými funkcemi, které jsou součástí aktualizace.

### <a name="if-you-have-given-consent"></a>Pokud jste udělili souhlas

V průvodci aktualizacemi a údržbou povolte předběžné verze funkcí. Vyberte předběžné verze funkcí stejně jako u jakékoli jiné funkce.

Volitelně můžete počkat na povolení předběžných verzí funkcí později v uzlu **funkce** v části **aktualizace a údržba** v pracovním prostoru **Správa** . Vyberte funkci a pak na pásu karet klikněte na **zapnout** . Dokud neudělíte souhlas, tato možnost není k dispozici pro použití.

### <a name="if-you-havent-given-consent"></a>Pokud jste neudělili souhlas

V průvodci aktualizacemi a údržbou jsou předběžné verze funkcí viditelné, ale nemůžete je povolit. Po instalaci aktualizace jsou tyto funkce viditelné v uzlu **funkce** . Nemůžete je ale povolit, dokud neudělíte souhlas.

> [!IMPORTANT]  
> V hierarchii s více lokalitami můžete povolit jenom volitelné nebo předběžné verze funkcí z lokality centrální správy. Toto chování zajistí, že v hierarchii nejsou žádné konflikty. <!--507197-->  
>
> Pokud jste udělili souhlas se samostatnou primární lokalitou a pak hierarchii rozbalíte instalací nové lokality centrální správy, musíte znovu udělit souhlas v lokalitě centrální správy.  

Pokud povolíte funkci předběžného vydání, nástroj Configuration Manager Hierarchy Manager (HMAN) musí před tím, než bude tato funkce k dispozici, zpracovat změnu. Zpracování změny je často okamžité. V závislosti na cyklu zpracování HMAN může trvat až 30 minut, než se dokončí. Po zpracování změny před použitím této funkce restartujte konzolu.

## <a name="list-of-pre-release-features"></a><a name="bkmk_table"></a>Seznam funkcí předběžné verze

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](pre-release-features.md).  

> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| Funkce          | Přidáno jako předběžná verze | Přidáno jako plná funkce |
|------------------|----------------------|-------------------------|
| [Skupiny orchestrace](../../../sum/deploy-use/orchestration-groups.md) <!--3098816--> | Verze 2002 | ![Zatím ne](media/red_x.png) |
| [Typ nasazení pořadí úloh](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!--3555953--> | Verze 2002 | ![Zatím ne](media/red_x.png) |
| [Odebrat lokalitu centrální správy](../deploy/install/remove-central-administration-site.md) <!-- 3607277 --> | Verze 2002 | ![Zatím ne](media/red_x.png) |
| [Ladicí program pořadí úloh](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | Verze 1906 | ![Zatím ne](media/red_x.png) |
| [Skupiny aplikací](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | Verze 1906 | ![Zatím ne](media/red_x.png) |
| [Azure Active Directory zjišťování skupiny uživatelů](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| Verze 1906 | Verze 2002 |
| [Synchronizovat výsledky členství kolekce s Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| Verze 1906| Verze 2002 |
| [CMPivot samostatná](cmpivot.md#bkmk_standalone) <!--3555890/4692885,no GUID--> | Verze 1906 | Verze 2002 |
| [Služba pro správu poskytovatele serveru SMS](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service) <!--1359052--> | Verze 1810 | Verze 1906 |
| [Vylepšený systém lokality HTTP](../../plan-design/hierarchy/enhanced-http.md) <!--1356889,1358228--> | Verze 1806 | Verze 1810 |
| [Klientské aplikace pro společně spravovaná zařízení](../../../comanage/workloads.md#client-apps) <br/> (dříve označované jako *mobilní aplikace pro spoluspravovaná zařízení*) <!--1357892/3600959,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | Verze 1806 | Verze 2002 |
| [Package Conversion Manager](../../../apps/pcm/package-conversion-manager.md) <!--1357861--> | Verze 1806 | Verze 1810 |
| [Postupná nasazení](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) <!--1356837--> | Verze 1802 | Verze 1806 |
| [Správa Řízení aplikací v programu Windows Defender](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) <!--3600958 (fka 1355092 & 1319346)--> | Verze 1702 | Verze 1906 |
| [Údržba kolekce podporující clustery (skupiny serverů)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | Verze 1602 | ![Zatím ne](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!TIP]  
> Další informace o nepředem vydaných funkcích, které musíte nejdřív povolit, najdete v tématu [Povolení volitelných funkcí z aktualizací](install-in-console-updates.md#bkmk_options).  
>
> Další informace o funkcích, které jsou k dispozici pouze ve větvi Technical Preview, najdete v tématu [Technical Preview](../../get-started/technical-preview.md).  
