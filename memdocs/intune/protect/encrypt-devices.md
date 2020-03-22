---
title: Šifrovat zařízení pomocí metody šifrování podporované platformou
titleSuffix: Microsoft Intune
description: Zašifrujte zařízení pomocí integrovaných šifrovacích metod, jako je BitLocker nebo trezoru klíčů, a spravujte klíče pro obnovení těchto zašifrovaných zařízení z portálu Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: ac81ceced473eacc32a3fca566f7c36eb7a262e2
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084878"
---
# <a name="use-device-encryption-with-intune"></a>Použití šifrování zařízení s Intune

Použijte Intune ke správě zařízení integrovaných na disku nebo šifrování jednotky, abyste mohli chránit data na svých zařízeních.

Nakonfigurujte šifrování disku jako součást profilu konfigurace zařízení pro službu Endpoint Protection. Intune podporuje následující platformy a šifrovací technologie:

- macOS: trezor
- Windows 10 a novější: BitLocker

Intune také obsahuje integrovanou [sestavu šifrování](encryption-monitor.md) , která poskytuje podrobné informace o stavu šifrování zařízení ve všech spravovaných zařízeních.

## <a name="filevault-encryption-for-macos"></a>Šifrování trezoru úložiště pro macOS

Pomocí Intune můžete na zařízeních se systémem macOS nakonfigurovat šifrování disků trezoru. Pak pomocí sestavy šifrování Intune zobrazte podrobnosti o šifrování těchto zařízení a spravujte klíče pro obnovení pro zařízení zašifrovaná pomocí trezoru.

Pro práci s úložištěm na zařízení se vyžaduje registrace zařízení schválená uživatelem. Uživatel musí ručně schválit profil správy ze systémových předvoleb, aby bylo možné registraci považovat za schválenou uživatelem.

Trezor úložišť je program pro šifrování celého disku, který je součástí macOS. Intune můžete použít ke konfiguraci trezoru úložišť na zařízeních, na kterých běží **macOS 10,13 nebo novější**.

Pro konfiguraci trezoru úložišť vytvořte [profil konfigurace zařízení](../configuration/device-profile-create.md) pro službu Endpoint Protection pro platformu MacOS. Nastavení trezoru úložiště je jednou z dostupných kategorií nastavení pro macOS Endpoint Protection.

Když vytvoříte zásadu pro šifrování zařízení pomocí trezoru, zásada se použije na zařízení ve dvou fázích. Nejdřív je zařízení připravené k tomu, aby Intune mohl načíst a zálohovat obnovovací klíč. Tato akce se označuje jako v úschově. Po uloží klíče se může šifrování disku spustit.

![Nastavení trezoru úložišť](./media/encrypt-devices/filevault-settings.png)

Podrobnosti o nastavení trezoru klíčů, které můžete spravovat pomocí Intune, najdete v tématu [trezor](endpoint-protection-macos.md#filevault) pro MacOS v článku Intune pro nastavení ochrany koncových bodů.

### <a name="permissions-to-manage-filevault"></a>Oprávnění ke správě trezoru úložišť

Aby bylo možné spravovat trezory v Intune, musí mít váš účet příslušné oprávnění [řízení přístupu na základě role](../fundamentals/role-based-access-control.md) (RBAC) Intune.

Níže jsou uvedené oprávnění trezoru úložišť, která jsou součástí kategorie **vzdálené úlohy** , a předdefinované role RBAC, které udělují oprávnění:
 
- **Získat klíč trezoru úložiště**:
  - Operátor helpdesku
  - Správce zabezpečení koncového bodu

- **Otočit klíč trezoru**
  - Operátor helpdesku

### <a name="how-to-configure-macos-filevault"></a>Jak nakonfigurovat macOS trezor

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.

3. Nastavte následující možnosti:

   - Platforma: macOS
   - Typ profilu: Endpoint Protection

4. Vyberte **nastavení** > **trezoru úložišť**.

5. V případě *trezoru úložišť*vyberte **Povolit**.

6. Pro *typ obnovovacího klíče*se podporuje jenom **osobní klíč** .

   Zvažte přidání zprávy do Průvodce nápovědou koncovým uživatelům, jak získat obnovovací klíč pro své zařízení. Tyto informace mohou být užitečné pro koncové uživatele, když použijete nastavení pro rotaci klíče pro obnovení, což může pravidelně automaticky generovat nový obnovovací klíč pro zařízení.

   Příklad: Chcete-li načíst ztracený nebo nedávno otočený obnovovací klíč, přihlaste se k webu Portál společnosti Intune z libovolného zařízení. Na portálu klikněte na *zařízení* a vyberte zařízení s povoleným trezorem úložiště a pak vyberte *získat obnovovací klíč*. Zobrazí se aktuální obnovovací klíč.

7. Nakonfigurujte zbývající [Nastavení trezoru úložišť](endpoint-protection-macos.md#filevault) tak, aby splňovalo vaše obchodní potřeby, a pak vyberte **OK**.

  8. Dokončete konfiguraci dalšího nastavení a potom profil uložte.  

### <a name="manage-filevault"></a>Správa trezoru úložišť

Jakmile Intune zašifruje zařízení macOS s trezorem, můžete zobrazit a spravovat klíče pro obnovení trezoru úložiště, když si zobrazíte [sestavu šifrování](encryption-monitor.md)Intune.

Jakmile Intune zašifruje zařízení macOS s trezorem souborů, můžete si z webu zobrazit jeho osobní obnovovací klíč, který je Portál společnosti na jakémkoli zařízení. Jednou na webu Portál společnosti zvolte šifrované zařízení macOS a pak zvolte možnost "získat klíč pro obnovení" jako akci vzdáleného zařízení.

### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices"></a>Načtení osobního obnovovacího klíče ze zařízení s macOS šifrovaným zařízením MEM

Koncoví uživatelé mohou načíst svůj osobní obnovovací klíč (klíč trezoru) pomocí aplikace Portál společnosti pro iOS, aplikace pro Android Portál společnosti nebo prostřednictvím aplikace Intune pro Android. Zařízení, které má osobní obnovovací klíč, musí být zaregistrované v Intune a zašifrované pomocí trezoru služby prostřednictvím Intune. Pomocí aplikace Portál společnosti pro iOS, aplikace pro Android Portál společnosti, aplikace Intune pro Android nebo webu Portál společnosti může koncový uživatel zobrazit obnovovací klíč **trezoru úložiště** , který je potřebný pro přístup k zařízením Mac. Koncoví uživatelé můžou vybrat **zařízení** > *šifrovaných a zaregistrovaných zařízení MacOS* > **získat obnovovací klíč**. V prohlížeči se zobrazí webová Portál společnosti a zobrazí se obnovovací klíč. 

## <a name="bitlocker-encryption-for-windows-10"></a>Šifrování BitLockeru pro Windows 10

Pomocí Intune můžete nakonfigurovat nástroj BitLocker Drive Encryption na zařízeních s Windows 10. Pak můžete pomocí sestavy šifrování Intune zobrazit podrobnosti o šifrování těchto zařízení. K důležitým informacím z vašich zařízení můžete také přistupovat pomocí nástroje BitLocker, jak se nachází v Azure Active Directory (Azure AD).

BitLocker je k dispozici na zařízeních se **systémem Windows 10 nebo novějším**.

Nakonfigurujte BitLocker při vytváření [profilu konfigurace zařízení](../configuration/device-profile-create.md) pro službu Endpoint Protection pro platformu Windows 10 nebo novější. Nastavení BitLockeru jsou v kategorii nastavení šifrování Windows pro Endpoint Protection pro Windows 10.

![Nastavení BitLockeru](./media/encrypt-devices/bitlocker-settings.png)

### <a name="how-to-configure-windows-10-bitlocker"></a>Jak nakonfigurovat Windows 10 BitLocker

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.

3. Nastavte následující možnosti:

   - Platforma: Windows 10 a novější
   - Typ profilu: Endpoint Protection

4. Vyberte **nastavení** > **šifrování Windows**.

5. Nakonfigurujte nastavení BitLockeru tak, aby vyhovovalo vašim obchodním potřebám, a pak vyberte **OK**.

6. Dokončete konfiguraci dalšího nastavení a potom profil uložte.

### <a name="silently-enable-bitlocker-on-devices"></a>Tiché zapnutí nástroje BitLocker na zařízeních

Můžete nakonfigurovat zásady BitLockeru, které automaticky a tiše povolí BitLocker na zařízení. To znamená, že BitLocker umožňuje úspěšně povolit bez předvádění uživatelského rozhraní koncovému uživateli, a to i v případě, že tento uživatel není místním správcem na zařízení.

**Požadavky na zařízení**:

Zařízení musí splňovat následující podmínky, aby bylo možné tiše povolit nástroj BitLocker:

- Zařízení musí používat Windows 10 verze 1809 nebo novější.
- Zařízení musí být připojené ke službě Azure AD.  

**Konfigurace zásad BitLockeru**:

V zásadách BitLockeru musí být nakonfigurovaná následující dvě nastavení pro [základní nastavení BitLockeru](../protect/endpoint-protection-windows-10.md#bitlocker-base-settings) :

- **Upozornění pro další** = *blok*šifrování disku.
- **Povolit Standard uživatelům povolit šifrování během připojení k Azure AD** = *Povolit*

Zásady BitLockeru **nesmí vyžadovat** použití spouštěcího kódu PIN nebo spouštěcího klíče. Když je *vyžadován*spouštěcí PIN kód TPM nebo spouštěcí klíč, BitLocker nemůže tiše povolit a vyžaduje interakci od koncového uživatele.  Tento požadavek splníte pomocí následujících tří [Nastavení jednotky s operačním systémem BitLocker](../protect/endpoint-protection-windows-10.md#bitlocker-os-drive-settings) ve stejné zásadě:

- **Kompatibilní spouštěcí PIN kód TPM** nesmí být nastavený tak, aby *vyžadoval spouštěcí PIN kód s čipem TPM* .
- **Kompatibilní spouštěcí klíč čipu TPM** nesmí nastavit, aby *vyžadoval spouštěcí klíč s čipem TPM* .
- **Kompatibilní spouštěcí klíč TPM a PIN** nesmí být nastavené tak, aby *vyžadovaly spouštěcí klíč a PIN kód s čipem TPM* .



### <a name="manage-bitlocker"></a>Správa nástroje BitLocker

Jakmile Intune zašifruje zařízení s Windows 10 pomocí nástroje BitLocker, můžete zobrazit a načíst klíče pro obnovení nástroje BitLocker při zobrazení [sestavy šifrování](encryption-monitor.md)Intune.

### <a name="rotate-bitlocker-recovery-keys"></a>Otočit obnovovací klíče BitLockeru

Pomocí akce zařízení v Intune můžete vzdáleně otočit obnovovací klíč BitLockeru zařízení se systémem Windows 10 verze 1909 nebo novějším.

#### <a name="prerequisites"></a>Požadavky

Zařízení musí splňovat následující požadavky, aby podporovaly rotaci obnovovacího klíče nástroje BitLocker:

- Zařízení musí používat Windows 10 verze 1909 nebo novější.

- Zařízení, která jsou připojená k Azure AD a která jsou připojená hybridem, musí mít podporu pro rotaci klíčů:

  - **Otočení hesla pro obnovení na základě klienta**

  Toto nastavení se vztahuje na *šifrování Windows* jako součást zásad konfigurace zařízení pro Windows 10 Endpoint Protection.
  
#### <a name="to-rotate-the-bitlocker-recovery-key"></a>Otočení obnovovacího klíče BitLockeru

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Zařízení** > **Všechna zařízení**.

3. V seznamu zařízení, která spravujete, vyberte zařízení, klikněte na **Další**a pak vyberte vzdálenou akci zařízení pro **střídání klíčů nástrojem BitLocker** .

## <a name="next-steps"></a>Další kroky

Vytvořte zásady [dodržování předpisů pro zařízení](compliance-policy-create-windows.md) .

Pomocí sestavy šifrování můžete spravovat:

- [Obnovovací klíče nástroje BitLocker](encryption-monitor.md#bitlocker-recovery-keys)
- [Klíče obnovení trezoru úložišť](encryption-monitor.md#filevault-recovery-keys)

Zkontrolujte nastavení šifrování, která můžete nakonfigurovat pomocí Intune pro:

- [Zapnut](endpoint-protection-windows-10.md#windows-encryption)
- [FileVault](endpoint-protection-macos.md#filevault)
