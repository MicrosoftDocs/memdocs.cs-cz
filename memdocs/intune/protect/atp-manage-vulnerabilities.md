---
title: Použití Intune k nápravě ohrožení zjištěných v Microsoft Defender ATP – Azure | Microsoft Docs
description: Podívejte se, jak spravovat úlohy zabezpečení ze správy ohrožení zabezpečení a & hrozeb v programu Microsoft Defender Advanced Threat Protection (ATP) z konzoly Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f57f4c31d0293997088db972cc4f370b77336567
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329959"
---
# <a name="use-intune-to-remediate-vulnerabilities-identified-by-microsoft-defender-atp"></a>Použití Intune k nápravě ohrožení zabezpečení identifikovaných ATP v programu Microsoft Defender

Když integruje Intune s rozšířenou ochranou před internetovými útoky v programu Microsoft Defender (ATP), můžete využít výhod správy ohrožení zabezpečení ATPs Threat & (TVM) a pomocí Intune napravit slabiny koncových bodů identifikované systémem TVM. Tato integrace přináší přístup na základě rizika pro zjišťování a stanovení priorit ohrožení zabezpečení, která můžou zlepšit dobu odezvy nápravy napříč vaším prostředím.

[Správa ohrožení zabezpečení & hrozeb](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/next-gen-threat-and-vuln-mgt) je součástí [rozšířené ochrany před internetovými útoky v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/windows-defender-advanced-threat-protection).

## <a name="how-integration-works"></a>Jak funguje integrace

Po připojení Intune k Rozšířené ochraně před internetovými útoky v programu Microsoft Defender obdrží ATP podrobnosti o hrozbách a ohroženích zabezpečení ze spravovaných zařízení.

V konzole Security Center Microsoft Defenderu správci zabezpečení ATP kontrolují data o chybách zabezpečení koncových bodů. Správci pak pomocí jediného kliknutí vytvoří bezpečnostní úkoly, které označí zranitelná zařízení k nápravě. Úkoly zabezpečení se okamžitě předávají do konzoly Intune, kde je můžou správci Intune zobrazit. Úloha zabezpečení identifikuje typ ohrožení zabezpečení, priority, stav a postup pro nápravu ohrožení zabezpečení. Správce Intune se rozhodne přijmout nebo odmítnout úlohu.

Když se úkol přijme, správce Intune pak vymění chybu zabezpečení i přes Intune, a to pomocí pokynů uvedených v rámci úlohy zabezpečení.

Mezi běžné akce týkající se nápravy patří:

- **Blokování** spuštění aplikace
- **Nasazením** aktualizace operačního systému snížíte riziko ohrožení zabezpečení.
- **Upravte** hodnotu registru.
- **Zakažte** nebo **Povolte** konfiguraci, aby ovlivnila chybu zabezpečení.
- Pokud není k dispozici žádná vhodná doporučení, **vyžadovat pozornost** upozornění pro správce k hrozbě.

Příklad pracovního postupu:

- V rámci služby Microsoft Defender ATP se zjistila Chyba aplikace s názvem contoso Media Player v4 a správce vytvoří úlohu zabezpečení pro aktualizaci této aplikace. Contoso Media Player je nespravovaná aplikace, která byla nasazena s Intune.

  Tato úloha zabezpečení se zobrazí v konzole Intune se stavem čeká na vyřízení:

  ![Zobrazení seznamu úloh zabezpečení v konzole Intune](./media/atp-manage-vulnerabilities/temp-security-tasks.png)

- Správce Intune vybere úlohu zabezpečení a zobrazí podrobnosti o této úloze.  Správce pak vybere **přijmout**, který aktualizuje stav v Intune a v ATP, *aby se přijímal.*

  ![Přijmout nebo odmítnout úlohu zabezpečení](./media/atp-manage-vulnerabilities/temp-accept-task.png)

- Správce pak úlohu opraví na základě poskytnutého návodu. Pokyny se liší v závislosti na typu nápravy, který je potřeba. Pokyny k nápravě v případě, že jsou k dispozici, obsahují odkazy, které otevřou relevantní podokna pro konfigurace v Intune.

  Protože přehrávač médií v tomto příkladu není spravovaná aplikace, může Intune zadat jenom textové pokyny. Pokud byla aplikace spravovaná, může Intune poskytnout pokyny ke stažení aktualizované verze a poskytnout odkaz pro otevření nasazení pro aplikaci, aby bylo možné do nasazení přidat aktualizované soubory.

- Po dokončení nápravy správce Intune otevře úlohu zabezpečení a vybere **dokončit úlohu**.  Stav nápravy se aktualizuje pro Intune a ATP, kde správci zabezpečení potvrzují revidovaný stav ohrožení zabezpečení.

## <a name="prerequisites"></a>Požadavky  

**Předplatná**:

- Microsoft Intune  
- Rozšířená ochrana před internetovými útoky v programu Microsoft Defender ([Zaregistrujte se k bezplatné zkušební verzi](https://www.microsoft.com/WindowsForBusiness/windows-atp?ocid=docs-wdatp-main-abovefoldlink).)

**Konfigurace Intune pro ATP**:

- Konfigurace služby pro připojení k Microsoft Defender ATP.
- Nasaďte zásady konfigurace zařízení s typem profilu **ATP Microsoft Defender (Windows 10 Desktop)** do zařízení, která budou mít riziko vyhodnocené atp.

  Informace o tom, jak nastavit Intune pro práci s ATP, najdete v tématu [vymáhání dodržování předpisů pro Microsoft Defender ATP s podmíněným přístupem v Intune](advanced-threat-protection.md#enable-microsoft-defender-atp-in-intune).

## <a name="work-with-security-tasks"></a>Práce s úlohami zabezpečení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Endpoint security** > **Security Security**.

3. Vyberte úlohu ze seznamu a otevřete tak okno prostředků, které zobrazí další podrobnosti pro tuto úlohu zabezpečení.

   Při prohlížení okna prostředku úlohy zabezpečení můžete vybrat další odkazy:

   - SPRAVOVANÉ aplikace – Prohlédněte si aplikaci, která je zranitelná. Pokud se ohrožení zabezpečení týká více aplikací, zobrazí se filtrovaný seznam aplikací.
   - ZAŘÍZENÍ – Prohlédněte si seznam *ohrožených zařízení*, ze kterých se můžete připojit k položce s dalšími podrobnostmi o ohrožení zabezpečení v tomto zařízení.
   - ŽADATEL – použijte odkaz k odeslání e-mailu správci, který tuto úlohu zabezpečení odeslal.
   - POZNÁMKY – při otevření úlohy zabezpečení si přečtěte vlastní zprávy odeslané žadatelem.

4. Vyberte **přijmout** nebo **odmítnout** pro odeslání oznámení do ATP pro plánovanou akci. Když přijmete nebo odmítnete úlohu, můžete odeslat poznámky, které jsou odesílány do ATP.

5. Po přijetí úlohy znovu otevřete úlohu zabezpečení (Pokud je uzavřená) a podle jejich podrobností OPRAVte chybu zabezpečení. Pokyny poskytované ATP v podrobnostech úlohy zabezpečení se liší v závislosti na ohrožení zabezpečení.

   Pokud je to možné, pokyny k nápravě zahrnují odkazy, které otevřou relevantní konfigurační objekty v konzole Intune.

6. Po dokončení nápravných kroků otevřete úlohu zabezpečení a vyberte **dokončit úlohu**.  Tato akce aktualizuje stav úlohy zabezpečení v Intune i v ATP.

Po úspěšné opravě se může skóre rizika v ATP na základě nových informací z opravených zařízení vyřadit.

## <a name="next-steps"></a>Další kroky
Přečtěte si další informace o službě Intune a [ATP Microsoft Defender](advanced-threat-protection.md).

Zkontrolujte ochranu před [mobilními hrozbami](mobile-threat-defense.md)Intune.

Projděte si [řídicí panel pro správu ohrožení zabezpečení & hrozeb](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/tvm-dashboard-insights) v ochraně ATP v programu Microsoft Defender.
