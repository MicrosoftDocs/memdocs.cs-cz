---
title: Šifrování zařízení s Windows 10 pomocí nástroje BitLocker v Intune
titleSuffix: Microsoft Intune
description: Zašifrujte zařízení pomocí integrované metody šifrování BitLockeru a spravujte klíče pro obnovení těchto zašifrovaných zařízení z portálu Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 4c652907d105b4b0363b2113916e892360feab39
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564257"
---
# <a name="manage-bitlocker-policy-for-windows-10-in-intune"></a>Správa zásad BitLockeru pro Windows 10 v Intune

Pomocí Intune můžete nakonfigurovat nástroj BitLocker Drive Encryption na zařízeních s Windows 10.

BitLocker je k dispozici na zařízeních se systémem Windows 10 nebo novějším. Některá nastavení nástroje BitLocker vyžadují, aby zařízení mělo podporovaný čip TPM.

Ke konfiguraci BitLockeru na spravovaných zařízeních použijte jeden z následujících typů zásad

- **[Zásada šifrování disku Endpoint Security pro Windows 10 BitLocker](#create-an-endpoint-security-policy-for-bitlocker)** Profil nástroje BitLocker v *Endpoint Security* je zaměřený na skupinu nastavení, která je vyhrazená pro konfiguraci nástroje BitLocker.

  Prohlédněte si nastavení BitLockeru, která jsou k dispozici v [profilech nástroje BitLocker ze zásad šifrování disku](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker).

- **[Konfigurační profil zařízení pro službu Endpoint Protection pro Windows 10 BitLocker](#create-an-endpoint-security-policy-for-bitlocker)** Nastavení BitLockeru jsou jedna z kategorií dostupných nastavení pro ochranu koncových bodů Windows 10.

  Prohlédněte si nastavení nástroje BitLocker, která jsou k dispozici pro [Nástroj BitLocker v profilech Endpoint Protection zásady konfigurace zařízení](../protect/endpoint-protection-windows-10.md#windows-settings).

> [!TIP]
> Intune poskytuje integrovanou [sestavu šifrování](encryption-monitor.md) , která obsahuje podrobnosti o stavu šifrování zařízení ve všech spravovaných zařízeních. Jakmile Intune zašifruje zařízení s Windows 10 pomocí nástroje BitLocker, můžete při zobrazení sestavy šifrování zobrazit a načíst klíče pro obnovení nástroje BitLocker.
>
> K důležitým informacím z vašich zařízení můžete také přistupovat pomocí nástroje BitLocker, jak se nachází v Azure Active Directory (Azure AD).
[Zpráva o šifrování](encryption-monitor.md) , která obsahuje podrobnosti o stavu šifrování zařízení ve všech spravovaných zařízeních.

## <a name="permissions-to-manage-bitlocker"></a>Oprávnění ke správě nástroje BitLocker

Aby bylo možné spravovat BitLocker v Intune, musí mít váš účet příslušné oprávnění [řízení přístupu na základě role](../fundamentals/role-based-access-control.md) (RBAC) služby Intune.

Níže jsou uvedené oprávnění nástroje BitLocker, která jsou součástí kategorie vzdálené úlohy, a předdefinované role RBAC, které udělují oprávnění:

- **Otočení klíčů BitLockeru**
  - Operátor helpdesku

## <a name="create-and-deploy-policy"></a>Vytvoření a nasazení zásad

Použijte jeden z následujících postupů k vytvoření typu zásad, které dáváte přednost.

### <a name="create-an-endpoint-security-policy-for-bitlocker"></a>Vytvoření zásady zabezpečení koncového bodu pro BitLocker

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Endpoint Security**  >  **šifrování disku**  >  **vytvořit zásadu**.

3. Nastavte následující možnosti:
   1. **Platforma**: Windows 10 nebo novější
   2. **Profil**: BitLocker

   ![Vyberte profil BitLockeru.](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. Na stránce **nastavení konfigurace** nakonfigurujte nastavení BitLockeru tak, aby vyhovovalo vašim obchodním potřebám.  

   Pokud chcete BitLocker zapnout Tichě, přečtěte si téma [bezobslužné zapnutí nástroje BitLocker na zařízeních](#silently-enable-bitlocker-on-devices). v tomto článku najdete další požadavky a konkrétní konfigurace nastavení, které musíte použít.

   Vyberte **Další**.

5. Na stránce **obor (značky)** zvolte **Vybrat značky oboru** a otevřete tak podokno vybrat značky, abyste přiřadili značky oboru k profilu.

   Pokračujte výběrem tlačítka **Další**.

6. Na stránce **přiřazení** vyberte skupiny, které získají tento profil. Další informace o přiřazování profilů najdete v tématu Přiřazení profilů uživatelů a zařízení.

   Vyberte **Další**.

7. Po dokončení na stránce **Revize + vytvořit** klikněte na **vytvořit**. Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

### <a name="create-a-device-configuration-profile-for-bitlocker"></a>Vytvoření profilu konfigurace zařízení pro nástroj BitLocker

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.

3. Nastavte následující možnosti:
   1. **Platforma**: Windows 10 a novější
   2. **Typ profilu**: Endpoint Protection

   ![Vyberte profil BitLockeru.](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. Vyberte **Nastavení**  >  **šifrování systému Windows**.

   ![Nastavení BitLockeru](./media/encrypt-devices/bitlocker-settings.png)

5. Nakonfigurujte nastavení BitLockeru tak, aby vyhovovalo vašim obchodním potřebám.

   Pokud chcete BitLocker zapnout Tichě, přečtěte si téma [bezobslužné zapnutí nástroje BitLocker na zařízeních](#silently-enable-bitlocker-on-devices). v tomto článku najdete další požadavky a konkrétní konfigurace nastavení, které musíte použít.

6. Vyberte **OK**.

7. Dokončete konfiguraci dalšího nastavení a potom profil uložte.

## <a name="manage-bitlocker"></a>Správa nástroje BitLocker

Informace o zařízeních, která přijímají zásady BitLockeru, najdete v tématu [monitorování šifrování disku](../protect/encryption-monitor.md). Klíče pro obnovení nástroje BitLocker můžete zobrazit a načíst i při zobrazení sestavy šifrování.

### <a name="silently-enable-bitlocker-on-devices"></a>Tiché zapnutí nástroje BitLocker na zařízeních

Můžete nakonfigurovat zásady BitLockeru, které automaticky a tiše povolí BitLocker na zařízení. To znamená, že BitLocker umožňuje úspěšně povolit bez předvádění uživatelského rozhraní koncovému uživateli, a to i v případě, že tento uživatel není místním správcem na zařízení.

**Požadavky na zařízení**:

Zařízení musí splňovat následující podmínky, aby bylo možné tiše povolit nástroj BitLocker:

- Pokud se koncoví uživatelé přihlásí k zařízením jako správci, musí zařízení používat Windows 10 verze 1803 nebo novější.
- Pokud se koncoví uživatelé přihlašují k zařízením jako standardní uživatelé, musí zařízení používat Windows 10 verze 1809 nebo novější.
- Zařízení musí být připojené ke službě Azure AD.  

**Konfigurace zásad BitLockeru**:

V zásadách BitLockeru musí být nakonfigurovaná následující dvě nastavení pro *základní nastavení BitLockeru* :

- **Upozornění pro jiné šifrování disku**  =  *Blok*.
- **Povolit Standard uživatelům povolit šifrování během připojení ke**  =  službě Azure AD *Povolení*

Zásady BitLockeru **nesmí vyžadovat** použití spouštěcího kódu PIN nebo spouštěcího klíče. Když je *vyžadován*spouštěcí PIN kód TPM nebo spouštěcí klíč, BitLocker nemůže tiše povolit a vyžaduje interakci od koncového uživatele.  Tento požadavek splníte pomocí následujících tří *Nastavení jednotky s operačním systémem BitLocker* ve stejné zásadě:

- **Kompatibilní spouštěcí PIN kód TPM** nesmí být nastavený tak, aby *vyžadoval spouštěcí PIN kód s čipem TPM* .
- **Kompatibilní spouštěcí klíč čipu TPM** nesmí nastavit, aby *vyžadoval spouštěcí klíč s čipem TPM* .
- **Kompatibilní spouštěcí klíč TPM a PIN** nesmí být nastavené tak, aby *vyžadovaly spouštěcí klíč a PIN kód s čipem TPM* .

### <a name="view-details-for-recovery-keys"></a>Zobrazit podrobnosti pro obnovovací klíče

Intune poskytuje přístup k oknu Azure AD pro BitLocker, takže můžete na portálu Intune zobrazit ID klíčů a obnovovací klíče BitLockeru pro zařízení s Windows 10. Aby bylo možné získat přístup k zařízení, musí mít uloží klíče ke službě Azure AD.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení**  >  **všechna zařízení**.

3. V seznamu vyberte zařízení a potom v části *monitorování*vyberte **klíče pro obnovení**.

4. Stiskněte **klávesu pro obnovení**. Když se tato možnost vybere, vygeneruje se položka protokolu auditu v rámci aktivity Správa služby.
  
   Pokud jsou ve službě Azure AD k dispozici klíče, jsou k dispozici tyto informace:
   - ID klíče BitLockeru
   - Obnovovací klíč nástroje BitLocker
   - Typ jednotky

   Pokud klíče nejsou v Azure AD, zobrazí se v Intune *pro toto zařízení nenašel žádný klíč BitLockeru*.

Informace pro BitLocker se získávají pomocí [poskytovatele služby BitLocker Configuration Service Provider](/windows/client-management/mdm/bitlocker-csp) (CSP). CSP nástroje BitLocker podporuje Windows 10 verze 1703 a novější a pro Windows 10 pro verze 1809 a novější.

Další informace o položkách protokolu auditu najdete v tématu [protokoly auditu na webu Azure Portal](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#audit-logs).

### <a name="rotate-bitlocker-recovery-keys"></a>Otočit obnovovací klíče BitLockeru

Pomocí akce zařízení v Intune můžete vzdáleně otočit obnovovací klíč BitLockeru zařízení se systémem Windows 10 verze 1909 nebo novějším.

#### <a name="prerequisites"></a>Požadavky

Zařízení musí splňovat následující požadavky, aby podporovaly rotaci obnovovacího klíče nástroje BitLocker:

- Zařízení musí používat Windows 10 verze 1909 nebo novější.

- Zařízení připojená k Azure AD, která jsou připojená k Azure AD, musí mít podporu pro rotaci klíčů povolenou pomocí konfigurace zásad BitLockeru:

  - **Otočení hesla pro obnovení na základě klienta** pro *umožnění rotace na zařízeních připojených k Azure AD* nebo *umožnění rotace na Azure AD a zařízeních s hybridem připojená*
  - **Uložit informace pro obnovení BitLockeru do Azure Active Directory** *povolených*
  - **Před povolením BitLockeru ukládat informace pro obnovení do Azure Active Directory** *Required*

#### <a name="to-rotate-the-bitlocker-recovery-key"></a>Otočení obnovovacího klíče BitLockeru

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení**  >  **všechna zařízení**.

3. V seznamu zařízení, která spravujete, vyberte zařízení, klikněte na **Další**a pak vyberte vzdálenou akci zařízení pro **střídání klíčů nástrojem BitLocker** .

4. Na stránce **Přehled** zařízení vyberte **otočení klíče BitLockeru**. Pokud tuto možnost nevidíte, vyberte tři tečky (**...**) a zobrazte další možnosti a pak vyberte vzdálenou akci zařízení pro **otočení klíče BitLockeru** .

   ![Pokud chcete zobrazit další možnosti, vyberte tři tečky.](./media/encrypt-devices/select-more.png)

## <a name="next-steps"></a>Další kroky

[Správa zásad pro FileVault](../protect/encrypt-devices-filevault.md)

[Monitorování šifrování disků](../protect/encryption-monitor.md)
