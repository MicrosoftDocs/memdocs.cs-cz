---
title: Šifrování zařízení macOS pomocí šifrování disku trezoru úložiště s Intune
titleSuffix: Microsoft Intune
description: Zašifrujte zařízení macOS pomocí integrovaného trezoru klíčů pro šifrování a spravujte klíče pro obnovení těchto zašifrovaných zařízení z portálu Intune.
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
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: cdfec1d82d68e97544172c56cecc416846b4a0f6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86460480"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>Použití šifrování disku trezoru pro macOS s Intune

Intune podporuje šifrování disku trezoru macOS. Trezor úložišť je program pro šifrování celého disku, který je součástí macOS. Intune můžete použít ke konfiguraci trezoru úložišť na zařízeních, na kterých běží **macOS 10,13 nebo novější**.

Pro konfiguraci trezoru úložišť na spravovaných zařízeních použijte jeden z následujících typů zásad:

- **[Zásady zabezpečení koncového bodu pro MacOS úložiště](#create-endpoint-security-policy-for-filevault)**. Profil trezoru souborů v *Endpoint Security* je zaměřený na skupinu nastavení, která je vyhrazená pro konfiguraci trezoru souborů.

  Podívejte se na [Nastavení trezoru úložišť, která jsou k dispozici v části profily pro zásady šifrování disku](../protect/endpoint-security-disk-encryption-profile-settings.md).

- **[Konfigurační profil zařízení pro službu Endpoint Protection pro MacOS trezor](#create-endpoint-security-policy-for-filevault)**. Nastavení trezoru úložiště je jednou z dostupných kategorií nastavení pro macOS Endpoint Protection. Další informace o použití profilu konfigurace zařízení najdete v tématu [Vytvoření profilu zařízení v Inunte](../configuration/device-profile-create.md).

  Zobrazit [Nastavení trezoru úložišť, která jsou k dispozici v profilech Endpoint Protection pro zásady konfigurace zařízení](../protect/endpoint-protection-macos.md#filevault).

Informace o správě nástroje BitLocker pro Windows 10 najdete v tématu [Správa zásad BitLockeru](../protect/encrypt-devices.md).

> [!TIP]
> Intune poskytuje integrovanou [sestavu šifrování](encryption-monitor.md) , která obsahuje podrobnosti o stavu šifrování zařízení ve všech spravovaných zařízeních.

Když vytvoříte zásadu pro šifrování zařízení pomocí trezoru, zásada se použije na zařízení ve dvou fázích. Nejdřív je zařízení připravené k tomu, aby Intune mohl načíst a zálohovat obnovovací klíč. Tato akce se označuje jako v úschově. Po uloží klíče se může šifrování disku spustit.

Kromě použití zásad Intune k šifrování zařízení s trezorem úložiště můžete nasadit zásadu na spravované zařízení, aby služba Intune mohla [předpokládat správu trezoru úložiště, když uživatel zařízení zašifroval](#assume-management-of-filevault-on-previously-encrypted-devices). Tento scénář vyžaduje, aby zařízení přijímalo zásady trezoru souborů z Intune a potom uživatel nahrává svůj osobní obnovovací klíč do Intune.

Pro práci s úložištěm na zařízení se vyžaduje registrace zařízení schválená uživatelem. Uživatel musí ručně schválit profil správy ze systémových předvoleb, aby bylo možné registraci považovat za schválenou uživatelem.

## <a name="permissions-to-manage-filevault"></a>Oprávnění ke správě trezoru úložišť

Aby bylo možné spravovat trezory v Intune, musí mít váš účet příslušné oprávnění [řízení přístupu na základě role](../fundamentals/role-based-access-control.md) (RBAC) Intune.

Níže jsou uvedené oprávnění trezoru úložišť, která jsou součástí kategorie **vzdálené úlohy** , a předdefinované role RBAC, které udělují oprávnění:

- **Získat klíč trezoru úložiště**:
  - Operátor helpdesku
  - Správce zabezpečení koncového bodu

- **Otočit klíč trezoru**
  - Operátor helpdesku

## <a name="create-device-configuration-policy-for-filevault"></a>Vytvoření zásad konfigurace zařízení pro trezor úložiště

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.

3. Na stránce **vytvořit profil** nastavte následující možnosti a pak klikněte na **vytvořit**:
   - **Platforma**: MacOS
   - **Profil**: Endpoint Protection

   ![Vyberte profil trezoru úložiště.](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. Na stránce **základy** zadejte následující vlastnosti:

   - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrý název zásad může například zahrnovat typ profilu a platformu.

   - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.

5. Na stránce **nastavení konfigurace** vyberte **trezor úložiště** a rozbalte dostupná nastavení:

   > [!div class="mx-imgBorder"]
   > ![Nastavení trezoru úložišť](./media/encrypt-devices-filevault/filevault-settings.png)

6. Nakonfigurujte tahle nastavení:
  
   - V případě *Povolení trezoru úložišť*vyberte **Ano**.

   - Jako *typ obnovovacího klíče*vyberte **osobní klíč**.

   - V *části umístění v úschově popis osobního obnovovacího klíče*přidejte zprávu, která uživatelům pomůže [získat obnovovací klíč](#retrieve-a-personal-recovery-key) pro svoje zařízení. Tato informace může být užitečná pro uživatele, když použijete nastavení pro rotaci klíče pro obnovení, což může pravidelně automaticky generovat nový obnovovací klíč pro zařízení.

     Příklad: Chcete-li načíst ztracený nebo nedávno otočený obnovovací klíč, přihlaste se k webu Portál společnosti Intune z libovolného zařízení. Na portálu klikněte na *zařízení* a vyberte zařízení s povoleným trezorem úložiště a pak vyberte *získat obnovovací klíč*. Zobrazí se aktuální obnovovací klíč.

   Nakonfigurujte zbývající [Nastavení trezoru úložišť](endpoint-protection-macos.md#filevault) tak, aby splňovalo vaše obchodní potřeby, a pak vyberte **Další**.

7. Na stránce **obor (značky)** zvolte **Vybrat značky oboru** a otevřete tak podokno vybrat značky, abyste přiřadili značky oboru k profilu.

   Pokračujte výběrem tlačítka **Další**.

8. Na stránce **přiřazení** vyberte skupiny, které získají tento profil. Další informace o přiřazování profilů najdete v tématu Přiřazení profilů uživatelů a zařízení.
Vyberte **Next** (Další).

9. Po dokončení na stránce **Revize + vytvořit** klikněte na **vytvořit**. Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

## <a name="create-endpoint-security-policy-for-filevault"></a>Vytvořit zásady zabezpečení Endpoint pro trezor úložiště

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Endpoint Security**  >  **šifrování disku**  >  **vytvořit zásadu**.

3. Na stránce **základy** zadejte následující vlastnosti a pak klikněte na tlačítko **Další**.
   - **Platforma**: MacOS
   - **Profil**: trezor

   ![Vyberte profil trezoru úložiště.](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. Na stránce **nastavení konfigurace** :
   1. Nastavte *možnost Povolit trezor úložiště* pro možnost **Ano**.
   2. Pro *typ obnovovacího klíče*se podporuje jenom **osobní obnovovací klíč** .
   3. Nakonfigurujte další nastavení tak, aby splňovalo vaše požadavky.

   Zvažte přidání zprávy, která pomůže uživatelům [získat obnovovací klíč](#retrieve-a-personal-recovery-key) pro zařízení. Tato informace může být užitečná pro uživatele, když použijete nastavení pro rotaci klíče pro obnovení, což může pravidelně automaticky generovat nový obnovovací klíč pro zařízení.

   Příklad: Chcete-li načíst ztracený nebo nedávno otočený obnovovací klíč, přihlaste se k webu Portál společnosti Intune z libovolného zařízení. Na portálu klikněte na zařízení a vyberte zařízení s povoleným trezorem úložiště a pak vyberte *získat obnovovací klíč*. Zobrazí se aktuální obnovovací klíč.

5. Po dokončení konfigurace nastavení vyberte **Další**.

6. Na stránce **obor (značky)** zvolte **Vybrat značky oboru** a otevřete tak podokno vybrat značky, abyste přiřadili značky oboru k profilu.

   Pokračujte výběrem tlačítka **Další**.

7. Na stránce **přiřazení** vyberte skupiny, které získají tento profil. Další informace o přiřazování profilů najdete v tématu Přiřazení profilů uživatelů a zařízení.
Vyberte **Next** (Další).

8. Po dokončení na stránce **Revize + vytvořit** klikněte na **vytvořit**. Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

## <a name="manage-filevault"></a>Správa trezoru úložišť

Postup zobrazení informací o zařízeních, která přijímají zásady trezoru úložišť, najdete v tématu [monitorování šifrování disku](../protect/encryption-monitor.md).

Když Intune nejdřív zašifruje zařízení macOS s trezorem, vytvoří se osobní obnovovací klíč. Po zašifrování zařízení zobrazí pro uživatele zařízení tento osobní klíč jednou.

U spravovaných zařízení může Intune v úschově kopii osobního obnovovacího klíče. V úschově klíčů umožňuje správcům Intune otáčet klíče, aby lépe chránily zařízení a uživatelé obnovili ztracený nebo otočený osobní obnovovací klíč.

Intune escrows obnovovací klíč, když zásady Intune zašifrují zařízení nebo když uživatel nahraje obnovovací klíč pro zařízení, které ručně zašifrují.

Po Intune escrows klíč pro osobní obnovení:

- Správci můžou spravovat a střídat klíče obnovení trezoru úložiště pro jakékoli spravované zařízení macOS pomocí sestavy šifrování Intune.
- Správci můžou pro osobní obnovovací klíč zobrazit jenom spravovaná zařízení macOS, která jsou označená jako *firemní*. Nemůžou zobrazit obnovovací klíč pro osobní zařízení.
- Uživatelé mohou [z podporovaného umístění zobrazit a načíst svůj osobní obnovovací klíč](#retrieve-a-personal-recovery-key). Například na webu Portál společnosti se může uživatel rozhodnout *získat klíč pro obnovení* jako akci vzdáleného zařízení.

### <a name="assume-management-of-filevault-on-previously-encrypted-devices"></a>Předpokládat správu trezoru úložiště u dříve zašifrovaných zařízení

Intune může spravovat šifrování disků trezoru v macOS zařízeních, která se šifrují pomocí zásad Intune. Intune může také převzít správu trezoru úložišť na zařízeních zašifrovaných uživateli zařízení, a ne prostřednictvím zásad Intune.

#### <a name="prerequisites-to-assume-management-of-filevault"></a>Předpoklady pro předpokládat správu trezoru úložišť

Aby bylo možné předpokládat správu dříve zašifrovaného zařízení, musí být splněny následující podmínky:

1. **Nasaďte do zařízení zásady trezoru**. Dříve zašifrované zařízení musí přijímat zásady z Intune, které zapíná šifrování disku trezoru.

   V tomto scénáři zásada nešifruje ani znovu nešifruje zařízení. Místo toho tato zásada umožňuje službě Intune předpokládat správu šifrování trezoru klíčů, který už je na zařízení povolený.  Můžete použít buď zásady šifrování disku zabezpečení koncového bodu, nebo zásady ochrany koncového bodu konfigurace zařízení k šifrování zařízení pomocí trezoru.

   Viz [Vytvoření a nasazení zásady](#create-device-configuration-policy-for-filevault).

2. **Uživatelé nahrávají svůj osobní obnovovací klíč do Intune**.  Jakmile zařízení obdrží zásady trezoru souborů, nasměrujte uživatele zařízení, které zařízení zašifroval, aby nahrálo svůj osobní obnovovací klíč do Intune. Pokud se klíč úspěšně zadá, Intune předpokládá správu šifrování trezoru úložiště a pro zařízení a uživatele se vytvoří nový osobní obnovovací klíč.

   > [!IMPORTANT]
   > Intune neupozorní uživatele, že musí nahrávat svůj osobní obnovovací klíč, aby bylo možné šifrování dokončit. Místo toho použijte své běžné komunikační kanály IT k upozornění uživatelům, kteří si předtím zašifrovali zařízení macOS pomocí trezoru souborů, že musí odeslat svůj osobní obnovovací klíč do Intune.  
   >
   > Na základě zásad dodržování předpisů můžou být zařízení zablokovaná přístup k podnikovým prostředkům, dokud Intune úspěšně nepředpokládá správu šifrování trezoru v zařízení.

#### <a name="upload-a-personal-recovery-key"></a>Nahrání osobního obnovovacího klíče

Aby mohla Intune Spravovat trezor souborů na dříve zašifrovaném zařízení, musí uživatel zařízení použít web Portál společnosti k nahrání aktuálního osobního obnovovacího klíče zařízení do Intune.  Po nahrání Intune tento klíč otočí a vytvoří nový klíč pro osobní obnovení, který v případě potřeby uloží Intune pro budoucí obnovení.

Na webu Portál společnosti uživatel vyhledá šifrované zařízení macOS a vybere možnost **obnovovací klíč úložiště**. Po zadání osobního obnovovacího klíče se Intune pokusí otočit klíč, aby vygeneroval nový klíč. K ověření, že zadaný klíč byl pro toto zařízení přesný, se provádí rotace. Tento nový klíč je pak uložený a spravovaný službou Intune pro budoucí použití, pokud uživatel potřebuje obnovit své zařízení.

Pokud se rotace klíčů nepovede, pak buď zařízení nezpracovalo zásady trezoru, nebo zadaný klíč není pro zařízení přesný.

Po úspěšném otočení může uživatel [načíst svůj nový osobní obnovovací klíč z podporovaného umístění](#retrieve-a-personal-recovery-key).

 Zobrazit [obsah koncového uživatele pro nahrání osobního obnovovacího klíče](../user-help/store-recovery-key.md).

> [!IMPORTANT]
> Pro zařízení, které je zašifrované uživatelem, a ne Intune, nemůže Intune spravovat šifrování trezoru zařízení, dokud toto zařízení neobdrží zásady trezoru úložišť a uživatel zařízení úspěšně nahrává svůj osobní obnovovací klíč.

### <a name="retrieve-a-personal-recovery-key"></a>Načtení osobního obnovovacího klíče

Pro zařízení macOS, které má šifrování trezoru úložiště spravované službou Intune, mohou koncoví uživatelé načíst svůj osobní obnovovací klíč (klíč trezoru) z následujících umístění pomocí libovolného zařízení:

- Web portálu společnosti
- aplikace Portál společnosti pro iOS/iPadOS
- Aplikace Portál společnosti pro Android
- Aplikace Intune

Správci můžou zobrazit osobní klíče pro obnovení pro šifrovaná zařízení macOS, která jsou označená jako *firemní* zařízení. Nemůžou zobrazit obnovovací klíč pro osobní zařízení.

Zařízení, které má osobní obnovovací klíč, musí být zaregistrované v Intune a zašifrované pomocí trezoru služby prostřednictvím Intune. Pomocí aplikace Portál společnosti pro iOS, aplikace pro Android Portál společnosti, aplikace Intune pro Android nebo webu Portál společnosti může uživatel zobrazit obnovovací klíč **trezoru úložiště** , který je potřebný pro přístup k zařízením Mac.

Uživatelé zařízení můžou vybrat **zařízení**  >  *šifrované a zaregistrované zařízení MacOS*  >  **získat obnovovací klíč**. V prohlížeči se zobrazí webová Portál společnosti a zobrazí se obnovovací klíč.

### <a name="rotate-recovery-keys"></a>Otočení obnovovacích klíčů

Intune podporuje několik možností, jak můžete otáčet a obnovovat osobní klíče pro obnovení. Jedním z důvodů, jak klíč otočit, je, že aktuální osobní klíč je ztracený nebo je pravděpodobně ohrožen.

- **Automatické otočení**: jako správce můžete nakonfigurovat nastavení trezoru klíčů pro automatické vygenerování nového klíče pro obnovení. Když se pro zařízení vygeneruje nový klíč, klíč se uživateli nezobrazí. Místo toho musí uživatel získat klíč buď od správce, nebo pomocí aplikace Portál společnosti.

- **Ruční rotace**: jako správce můžete zobrazit informace o zařízení, které spravujete v Intune a které je zašifrované pomocí trezoru. Pak můžete zvolit ruční otočení obnovovacího klíče pro podniková zařízení. Obnovovací klíče pro osobní zařízení nemůžete otočit.

  Otočení obnovovacího klíče:

  1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

  2. Vyberte **zařízení**   >  **všechna zařízení**.

  3. V seznamu zařízení vyberte zařízení, které je šifrované a pro které chcete otočit jeho klíč. Pak v části monitorování vyberte **klíče pro obnovení**.
  
  4. V podokně klíče pro obnovení vyberte **otočit obnovovací klíč trezoru**.

     Až se zařízení příště vrátí se službou Intune, osobní klíč se otočí. V případě potřeby může uživatel získat nový klíč prostřednictvím portálu společnosti.

### <a name="recover-recovery-keys"></a>Obnovit obnovovací klíče

- **Správce**: Správci nemohou zobrazit osobní klíče pro obnovení pro zařízení, která jsou zašifrovaná pomocí trezoru služby.

- **Koncový uživatel**: koncoví uživatelé používají portál společnosti web z libovolného zařízení k zobrazení aktuálního osobního obnovovacího klíče pro kterékoli ze svých spravovaných zařízení. Nemůžete zobrazit obnovovací klíče z aplikace Portál společnosti.

  Postup zobrazení obnovovacího klíče:
  
  1. Přihlaste se k webu *portál společnosti Intune* z libovolného zařízení.

  2. Na portálu klikněte na **zařízení** a vyberte zařízení MacOS, které je šifrované pomocí trezoru.

  3. Vyberte **získat obnovovací klíč**. Zobrazí se aktuální obnovovací klíč.

## <a name="next-steps"></a>Další kroky

[Správa zásad nástroje BitLocker](../protect/encrypt-devices.md)

[Monitorování šifrování disků](../protect/encryption-monitor.md)
