---
title: Sestava šifrování pro zašifrovaná zařízení v Microsoft Intune
titleSuffix: Microsoft Intune
description: Zobrazte si sestavu ve svém stavu šifrování zařízení s iOS/iPadOS nebo Windows a získejte přístup k trezoru objektů a obnovovacím klíčům BitLockeru z portálu Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: d14ee52decf1b6ef9b2566b3233a385c1331bcc5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910974"
---
# <a name="monitor-device-encryption-with-intune"></a>Monitorování šifrování zařízení pomocí Intune

Sestava Microsoft Intuneho šifrování je centralizované umístění pro zobrazení podrobností o stavu šifrování zařízení a možnosti hledání pro správu klíčů pro obnovení zařízení. Možnosti obnovovacího klíče, které jsou k dispozici, závisí na typu zařízení, které si prohlížíte.

Sestavu můžete najít tak, že se přihlásíte do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431). Vyberte **Devices**  >  **monitorování**zařízení a potom v části *Konfigurace*vyberte **Sestava šifrování**.

## <a name="view-encryption-details"></a>Zobrazit podrobnosti o šifrování

Sestava šifrování zobrazuje společné podrobnosti napříč podporovanými zařízeními, která spravujete. Následující části obsahují podrobné informace o informacích, které Intune prezentuje v sestavě.

### <a name="prerequisites"></a>Předpoklady

Sestava šifrování podporuje vytváření sestav na zařízeních, na kterých běží následující verze operačního systému:

- macOS 10,13 nebo novější
- Windows verze 1607 nebo novější

### <a name="report-details"></a>Podrobnosti sestavy

Podokno sestava šifrování zobrazuje seznam zařízení, která spravujete, s podrobnými podrobnostmi o těchto zařízeních. Můžete vybrat zařízení ze seznamu a přejít k němu a zobrazit další podrobnosti v podokně [stav šifrování zařízení](#device-encryption-status) zařízení.

- **Název zařízení** – název zařízení.
- **OS** – platforma zařízení, například Windows nebo MacOS.
- **Verze operačního systému** – verze Windows nebo MacOS na zařízení.
- **Verze TPM** *(platí jenom pro Windows 10)* – verze čipu TPM (Trusted Platform Module) na zařízení s Windows 10.
- **Připravenost na šifrování** – vyhodnocení připravenosti na zařízení pro podporu vhodné šifrovací technologie, jako je například BitLocker nebo šifrování trezoru. Zařízení jsou označena jako:
  - **Připraveno**: zařízení se dá zašifrovat pomocí zásad MDM, což vyžaduje, aby zařízení splňovalo následující požadavky:

    **Pro zařízení MacOS**:
    - macOS verze 10,13 nebo novější

    **Pro zařízení s Windows 10**:
    - Verze 1709 nebo novější, *obchodní*, *podnikové*, *vzdělávací*nebo verze 1809 nebo novější *pro*
    - Zařízení musí mít čip TPM.

    Další informace najdete v dokumentaci k Windows v dokumentaci k [poskytovateli služby BitLocker Configuration Service Provider (CSP)](/windows/client-management/mdm/bitlocker-csp) .

  - **Nepřipraveno**: zařízení nemá úplné možnosti šifrování, ale pořád podporuje šifrování. Například zařízení s Windows může být zašifrováno ručně uživatelem nebo prostřednictvím Zásady skupiny, které lze nastavit tak, aby povolovalo šifrování bez čipu TPM.
  - **Nelze použít**: pro klasifikaci tohoto zařízení není k dispozici dostatek informací.

- **Stav šifrování** – určuje, jestli je jednotka operačního systému zašifrovaná.

- **Hlavní název uživatele** – primární uživatel zařízení.

### <a name="device-encryption-status"></a>Stav šifrování zařízení

Když vyberete zařízení ze sestavy šifrování, Intune zobrazí podokno **stav šifrování zařízení** . V tomto podokně jsou k dispozici následující podrobnosti:

- **Název zařízení** – název zařízení, které si prohlížíte.

- **Připravenost na šifrování** – vyhodnocení připravenosti na zařízení pro podporu šifrování prostřednictvím zásad MDM.

  Příklad: Pokud má zařízení s Windows 10 připravenosti *Nepřipraveno*, může i nadále podporovat šifrování. Aby bylo možné označení *připravit* , musí mít zařízení s Windows 10 čip TPM. Čipy TPM nejsou nutné k podpoře šifrování. (Další informace najdete v tématu *připravenost na šifrování* v předchozí části.)

- **Stav šifrování** – určuje, jestli je jednotka operačního systému zašifrovaná. Může trvat až 24 hodin, než Intune nahlásí stav šifrování zařízení nebo změní stav. Tato doba zahrnuje dobu, po kterou má operační systém zašifrování, a čas, kdy se má zařízení nahlásit zpátky do Intune.

  Pokud chcete zrychlit hlášení stavu šifrování trezoru služby, než se zařízení normálně objevuje, uživatelé budou po dokončení šifrování synchronizovat svá zařízení.

- **Profily** – seznam profilů *Konfigurace zařízení* , které se vztahují k tomuto zařízení a jsou nakonfigurované s následujícími hodnotami:

  - MacOS
    - Typ profilu = *Endpoint Protection*
    - Nastavení > trezoru úložiště > trezor = *Enable*

  - Windows 10:
    - Typ profilu = *Endpoint Protection*
    - Nastavení > šifrování Windows > šifrovat zařízení = *vyžadovat*

  Seznam profilů můžete použít k identifikaci jednotlivých zásad pro kontrolu, aby *souhrn stavu profilu* označoval problémy.

- **Shrnutí stavu profilu** – souhrn profilů, které se vztahují k tomuto zařízení. Souhrn představuje nejmenší příznivou podmínku v rámci platných profilů. Pokud například výsledkem pouze jednoho z několika použitelných profilů je chyba, zobrazí se v *souhrnu stavu profilu* *Chyba*.

  Pokud chcete zobrazit podrobnosti o stavu, přejít na **Intune**  >  **profily konfigurace zařízení**  >  **Profiles**v Intune a vybrat profil. Volitelně můžete vybrat možnost **stav zařízení** a pak vybrat zařízení.

- **Podrobnosti o stavu** – rozšířené informace o stavu šifrování zařízení.

  > [!IMPORTANT]
  > V případě zařízení s Windows 10 Intune zobrazí *Podrobnosti o stavu* jenom pro zařízení s *Windows 10 duben 2019 Update* nebo novějším.

  V tomto poli se zobrazují informace o každé příslušné chybě, kterou je možné zjistit. Pomocí těchto informací můžete pochopit, proč nemusí být zařízení připravené k šifrování.

  Následují příklady podrobností o stavu, které může Intune hlásit:

  **macOS**:
  - Obnovovací klíč nebyl dosud načten a uložen. Pravděpodobně zařízení není odemknuté nebo nebylo vráceno se změnami.

    *Vezměte v úvahu: Tento výsledek nemusí nutně představovat chybový stav, ale dočasný stav, který může být z důvodu časování na zařízení, kde v úschově pro obnovovací klíče musí být nastavené před odesláním požadavku na šifrování do zařízení. Tento stav může také indikovat, že zařízení zůstává uzamčené nebo se v nedávné době nevrátilo s Intune. Vzhledem k tomu, že šifrování trezoru se nespustí, dokud není zařízení zapojené do elektrické sítě (zpoplatněné), může uživatel obdržet obnovovací klíč pro zařízení, které ještě není zašifrované*.

  - Uživatel odvozuje šifrování nebo právě probíhá šifrování.

    *Vezměte v úvahu: uživatel se ještě odhlásil po přijetí požadavku na šifrování, který je nutný k tomu, aby mohl trezor zařízení zašifrovat zařízení, nebo jestli uživatel zařízení ručně dešifroval. Intune nemůže zabránit uživateli v dešifrování svého zařízení.*

  - Zařízení je už zašifrované. Aby bylo možné pokračovat, musí uživatel zařízení zařízení dešifrovat.

    *Vezměte v úvahu: Intune nemůže na zařízení, které je už zašifrované, nastavit trezor. Když ale zařízení obdrží zásadu, která povoluje trezor souborů, může uživatel [nahrát svůj osobní obnovovací klíč, aby Intune mohl spravovat šifrování na tomto zařízení](../protect/encrypt-devices-filevault.md#assume-management-of-filevault-on-previously-encrypted-devices). Alternativně, ale nedoporučujeme, aby se zařízení po určitou dobu nešifroval, uživatel může zařízení před tím, než ho bude zašifrovat pomocí zásad Intune, ručně dešifrovat.*

  - Trezor úložiště potřebuje, aby uživatel schválil svůj profil pro správu v macOS Catalina a vyšších.

    *Zvažte: počínaje verzí macOS 10,15 (Catalina) může nastavení registrace schválená uživatelem způsobit požadavek, aby uživatelé ručně schválili šifrování trezoru. Další informace najdete v dokumentaci k [registraci schválené uživatelem](../enrollment/macos-enroll.md) v dokumentaci k Intune*.

  - Neznámý

    *Vezměte v úvahu: možnou příčinou neznámého stavu je to, že zařízení je uzamčené a Intune nemůže spustit v úschově nebo proces šifrování. Po odemknutí zařízení může pokračovat průběh*.

  **Windows 10**:
  - Zásada BitLockeru vyžaduje souhlas uživatele, aby mohl spustit Průvodce nástroj BitLocker Drive Encryption pro spuštění šifrování svazku s operačním systémem, ale uživatel nesouhlasí.

  - Metoda šifrování svazku operačního systému neodpovídá zásadám BitLockeru.

  - Zásada BitLockeru pro ochranu svazku operačního systému vyžaduje ochranu čipem TPM, ale čip TPM se nepoužívá.

  - Zásady BitLockeru vyžadují pro svazek operačního systému ochranu jenom čipem TPM, ale ochrana TPM se nepoužívá.

  - Zásady BitLockeru vyžadují ochranu pomocí TPM a PIN kódu pro svazek operačního systému, ale ochrana pomocí čipu TPM a PIN kódu se nepoužívá.

  - Zásady BitLockeru vyžadují ochranu pomocí čipu TPM a spouštěcího klíče pro svazek operačního systému, ale ochrana pomocí čipu TPM a spouštěcího klíče se nepoužívá.

  - Zásady BitLockeru vyžadují pro svazek s operačním systémem ochranu pomocí čipu TPM + PIN a spouštěcího klíče, ale nepoužije se ochrana pomocí čipu TPM + PIN a spouštěcího klíče.

  - Svazek s operačním systémem není chráněn.

  - Nepovedlo se zálohovat klíč obnovení.

  - Pevná jednotka není chráněná.

  - Metoda šifrování pevné jednotky neodpovídá zásadám BitLockeru.

  - Pro šifrování jednotek vyžaduje zásada BitLockeru, aby se uživatel přihlásil jako správce, nebo pokud je zařízení připojené ke službě Azure AD, musí být zásada AllowStandardUserEncryption nastavená na hodnotu 1.

  - Prostředí Windows Recovery Environment (WinRE) není nakonfigurováno.

  - ČIP TPM není k dispozici pro BitLocker, protože není k dispozici, je v registru nedostupný, nebo je operační systém na vyměnitelném disku.

  - ČIP TPM není připravený na BitLocker.

  - Síť není k dispozici, což je vyžadováno pro zálohování klíče obnovení.

## <a name="export-report-details"></a>Exportovat podrobnosti sestavy

Při prohlížení podokna sestavy šifrování můžete vybrat **exportovat** a vytvořit soubor *. csv* stažení podrobností sestavy. Tato sestava obsahuje podrobné informace o podrobnostech z podokna *sestavy šifrování* a podrobností o *stavu šifrování zařízení* pro každé zařízení, které spravujete.

![Exportovat podrobnosti](./media/encryption-monitor/export.png)

Tato sestava může být používána při identifikaci problémů pro skupiny zařízení. Můžete například použít sestavu k identifikaci seznamu zařízení macOS, která *je už povolená uživatelem*, což znamená, že zařízení, která se musí ručně dešifrovat, než může Intune spravovat jeho nastavení trezoru.

## <a name="manage-recovery-keys"></a>Správa klíčů pro obnovení

Podrobnosti o správě klíčů pro obnovení najdete v dokumentaci k Intune v následujících tématech:

macOS úložiště:
- [Načíst osobní obnovovací klíč](../protect/encrypt-devices-filevault.md#retrieve-a-personal-recovery-key)
- [Otočení obnovovacích klíčů](../protect/encrypt-devices-filevault.md#rotate-recovery-keys)
- [Obnovit obnovovací klíče](../protect/encrypt-devices-filevault.md#recover-recovery-keys)

Windows 10 BitLocker:
- [Otočit obnovovací klíče BitLockeru](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys)

## <a name="next-steps"></a>Další kroky

[Správa zásad nástroje BitLocker](../protect/encrypt-devices.md)

[Správa zásad pro FileVault](encrypt-devices-filevault.md)