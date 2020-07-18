---
title: Nástroj pro migraci pravidla firewallu služby Endpoint Security pro Microsoft Intune – Azure | Microsoft Docs
description: Informace o použití nástroje pro migraci pravidel firewallu služby Endpoint Security pro Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: mattsha
ms.openlocfilehash: 7dd6d3a01d18e4d8b334bdeee3f72eeaeed67c0a
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86464936"
---
# <a name="endpoint-security-firewall-rule-migration-tool-overview"></a>Přehled nástroje pro migraci pravidla firewallu služby Endpoint Security

Mnoho organizací se pokouší přesunout konfiguraci zabezpečení do Microsoft Endpoint Manageru, aby bylo možné využívat moderní cloudovou správu.

Zabezpečení koncového bodu ve Správci Endpoint nabízí rozsáhlá prostředí pro správu konfigurace brány Windows Firewall a podrobné správy pravidel brány firewall.

V mnoha organizacích již mají zásady skupiny zavedeny, aby bylo možné spravovat pravidla brány Windows Firewall. Přechod na moderní správu může být obtížné, protože ruční vytváření stovek pravidel brány firewall může být tiresome.

Aby zákazníci mohli přesunout konfiguraci pravidel brány firewall na zásady zabezpečení koncového bodu ve Správci koncového bodu, vyvinuli jsme **Nástroj pro migraci pravidel firewallu pro zabezpečení koncového bodu** .

Zákazníci můžou Nástroj pro **migraci pravidla firewallu zabezpečení koncového bodu** spustit na referenčním nebo předem nakonfigurovaném klientovi Windows 10 a automaticky vytvořit zásady pravidla firewallu zabezpečení koncového bodu ve Správci koncových bodů. Po vytvoření můžou správci cílit na tato pravidla do skupin Azure AD, aby mohli nakonfigurovat MDM a spoluspravované klienty.

Stáhněte si [Nástroj pro migraci pravidla firewallu pro Endpoint Security](https://aka.ms/EndpointSecurityFWRuleMigrationTool):<br>
<a href="https://aka.ms/EndpointSecurityFWRuleMigrationTool"><img alt="Download the tool" src="./media/endpoint-security-firewall-rule-tool/downloadtool.png" width="170"></a>

## <a name="tool-usage"></a>Využití nástrojů

Nástroj se spustí na referenčním počítači a migruje aktuální konfiguraci pravidla brány Windows Firewall. Spuštěním tohoto nástroje se vyexportují všechna povolená pravidla brány firewall přítomná v zařízení a automaticky se vytvoří nové zásady Intune s shromážděnými pravidly.

1. Přihlaste se k referenčnímu počítači s oprávněními místního správce.
2. Stáhnout a rozbalit soubor `Export-FirewallRules.zip` . <br>
   Soubor zip obsahuje soubor skriptu `Export-FirewallRules.ps1` . 
3. Spusťte `Export-FirewallRules.ps1` skript na počítači. <br>
   Skript stáhne všechny požadované součásti potřebné ke spuštění. Po zobrazení výzvy zadejte příslušné přihlašovací údaje správce Intune. Další informace o požadovaných oprávněních najdete v tématu [požadovaná oprávnění](#required-permissions).
4. Po zobrazení výzvy zadejte název zásady. <br>
   Tato zásada se zobrazí ve [Správci Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) v podokně **Security Endpoint**  >  **firewall** . 

    > [!IMPORTANT]
    > Název zásady musí být pro tenanta jedinečný.

    Pokud se najde víc než 150 pravidel brány firewall, vytvoří se víc zásad.

    > [!NOTE]
    > Ve výchozím nastavení se migrují jenom povolená pravidla brány firewall a ve výchozím nastavení se migrují jenom pravidla firewallu vytvořená objektem zásad skupiny. Jsou k dispozici přepínače pro úpravu těchto výchozích hodnot. Další informace najdete v tématu [přepínače](#switches).
    >
    > V závislosti na počtu nalezených pravidel brány firewall může trvat nějakou dobu, než se nástroj spustí.

5. Po dokončení nástroj vypíše počet pravidel brány firewall, která se nedala automaticky migrovat. Další informace najdete v tématu [Nepodporovaná konfigurace](#unsupported-configuration).

## <a name="switches"></a>Přepínače

K úpravě výchozích funkcí nástroje můžete použít následující přepínače (parametry).

- `IncludeLocalRules`– Pomocí tohoto přepínače budou do exportu zahrnuta všechna místně vytvořená nebo výchozí pravidla brány Windows Firewall. Všimněte si, že povolení tohoto přepínače může mít za následek mnoho zahrnutých pravidel. 
- `IncludedDisabledRules`-Pomocí tohoto přepínače budou do exportu zahrnuta všechna povolená a zakázaná pravidla brány Windows Firewall. Všimněte si, že povolení tohoto přepínače může mít za následek mnoho zahrnutých pravidel.

## <a name="unsupported-configuration"></a>Nepodporovaná konfigurace

Následující nastavení založená na registru nejsou podporována z důvodu nedostatku podpory MDM ve Windows. Tato nastavení jsou neobvyklá, ale pokud tato nastavení požadujete, přihlaste se prosím k této potřebě prostřednictvím standardních kanálů podpory.

|     Pole objektu zásad skupiny    |     Důvod    |
|-|-|
|      TYPE-VALUE =/"Security =" IFSECURE-VAL    |     Nastavení související s protokolem IPSec není podporováno Windows MDM.    |
|      TYPE-VALUE =/"Security2_9 =" IFSECURE2-9-VAL    |     Nastavení související s protokolem IPSec není podporováno Windows MDM.    |
|      TYPE-VALUE =/"Security2 =" IFSECURE2-10-VAL     |     Nastavení související s protokolem IPSec není podporováno Windows MDM.    |
|      TYP-HODNOTA =/"IF-VAL    |     Identifikátor rozhraní (LUID) nejde spravovat.    |
|      TYP-hodnota =/"pozdržet =" POZDRŽET-VAL    |     Příchozí procházení NAT, které se nezveřejňuje prostřednictvím Zásady skupiny nebo Windows MDM    |
|      TYP-HODNOTA =/"LSM =" BOOL-VAL    |     Volný mapovaný zdroj, který není vystavený prostřednictvím Zásady skupiny nebo Windows MDM    |
|      TYP-hodnota =/"platforma =" platforma – VAL    |     Správa verzí operačního systému, která není dostupná přes Zásady skupiny nebo Windows MDM    |
|      TYPE-VALUE =/"RMauth =" STR-VAL    |     Nastavení související s protokolem IPSec není podporováno Windows MDM.    |
|      TYPE-VALUE =/"RUAuth =" STR-VAL    |     Nastavení související s protokolem IPSec není podporováno Windows MDM.    |
|      TYP-hodnota =/"AuthByPassOut =" BOOL-VAL    |     Nastavení související s protokolem IPSec není podporováno Windows MDM.    |
|      TYP-HODNOTA =/"DVĚMA =" BOOL-VAL    |     Pouze místní mapování nevystavené prostřednictvím Zásady skupiny nebo Windows MDM    |
|      TYP-hodnota =/"Platform2 =" platforma-OP – VAL    |     Redundantní nastavení nevystavené prostřednictvím Zásady skupiny nebo Windows MDM    |
|      TYP-hodnota =/"PCross =" BOOL-VAL    |     Povolení překrytí profilu nedostupného přes Zásady skupiny nebo Windows MDM    |
|      TYPE-VALUE =/"LUOwn =" STR-VAL    |     SID místního vlastníka uživatele není použitelné v MDM.    |
|      TYP-HODNOTA =/"TTK =" TRUST-TUPLE-KLÍČOVÉ SLOVO-VAL    |     Porovnat provoz s klíčovým slovem Trust Tuple, které není vystaveno prostřednictvím Zásady skupiny nebo Windows MDM    |
|      TYP-HODNOTA =/"TTK2_22 =" TRUST-TUPLE-KLÍČOVÉ SLOVO-VAL2-22    |     Porovnat provoz s klíčovým slovem Trust Tuple, které není vystaveno prostřednictvím Zásady skupiny nebo Windows MDM    |
|      TYP-HODNOTA =/"TTK2_27 =" TRUST-TUPLE-KLÍČOVÉ SLOVO-VAL2-27    |     Porovnat provoz s klíčovým slovem Trust Tuple, které není vystaveno prostřednictvím Zásady skupiny nebo Windows MDM    |
|      TYP-HODNOTA =/"TTK2_28 =" TRUST-TUPLE-KLÍČOVÉ SLOVO-VAL2-28    |     Porovnat provoz s klíčovým slovem Trust Tuple, které není vystaveno prostřednictvím Zásady skupiny nebo Windows MDM    |
|      TYPE-VALUE =/"NNm =" STR-ENC-VAL    |     Nastavení související s protokolem IPSec není podporováno Windows MDM.    |
|      TYPE-VALUE =/"SecurityRealmId =" STR-VAL    |     Nastavení související s protokolem IPSec není podporováno Windows MDM.    |

## <a name="unsupported-setting-values"></a>Nepodporované hodnoty nastavení
Následující hodnoty nastavení nejsou podporovány pro migraci:

**Porty**
- `PlayToDiscovery`není podporován jako místní nebo vzdálený rozsah portů.

**Rozsahy adres**
- `LocalSubnet6`není podporován jako místní nebo vzdálený rozsah adres. 
- `LocalSubnet4`není podporován jako místní nebo vzdálený rozsah adres.
- `PlatToDevice`není podporován jako místní nebo vzdálený rozsah adres.

Po spuštění nástroje se vygeneruje sestava s pravidly, která se úspěšně nemigrují. Některá z těchto pravidel můžete zobrazit zobrazením `RulesError.csv` v `C:\<folder needed>` . 

## <a name="required-permissions"></a>Požadovaná oprávnění
Správce Endpoint Security Manager, Správce služby Intune nebo uživatelé globálních správců můžou migrovat pravidla brány Windows Firewall do zásad zabezpečení koncových bodů. Alternativně může být použita vlastní role, kde jsou nastavena oprávnění **pro**standardní hodnoty zabezpečení pomocí funkce **Odstranit**, číst, **přiřadit**, **vytvořit**a **aktualizovat** . Další informace najdete v tématu [udělení oprávnění správce k Intune](../fundamentals/users-add.md#grant-admin-permissions).

## <a name="next-steps"></a>Další kroky

- Přiřaďte pravidla skupinám Azure AD ke konfiguraci MDM a spoluspravovaných klientů. Další informace najdete v tématu [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md).
