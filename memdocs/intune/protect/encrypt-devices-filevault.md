---
title: Šifrování zařízení macOS pomocí šifrování disku trezoru úložiště s Intune
titleSuffix: Microsoft Intune
description: Zašifrujte zařízení macOS pomocí integrovaného trezoru klíčů pro šifrování a spravujte klíče pro obnovení těchto zašifrovaných zařízení z portálu Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/24/2020
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
ms.openlocfilehash: 1f2a6955a430427fe3f4e2791da6bbaecdd90523
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353563"
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

Pro práci s úložištěm na zařízení se vyžaduje registrace zařízení schválená uživatelem. Uživatel musí ručně schválit profil správy ze systémových předvoleb, aby bylo možné registraci považovat za schválenou uživatelem.

## <a name="permissions-to-manage-filevault"></a>Oprávnění ke správě trezoru úložišť

Aby bylo možné spravovat trezory v Intune, musí mít váš účet příslušné oprávnění [řízení přístupu na základě role](../fundamentals/role-based-access-control.md) (RBAC) Intune.

Níže jsou uvedené oprávnění trezoru úložišť, která jsou součástí kategorie **vzdálené úlohy** , a předdefinované role RBAC, které udělují oprávnění:

- **Získat klíč trezoru úložiště**:
  - Operátor helpdesku
  - Správce zabezpečení koncového bodu

- **Otočit klíč trezoru**
  - Operátor helpdesku

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

   Zvažte přidání zprávy, která pomůže uživatelům získat obnovovací klíč pro zařízení. Tato informace může být užitečná pro uživatele, když použijete nastavení pro rotaci klíče pro obnovení, což může pravidelně automaticky generovat nový obnovovací klíč pro zařízení.

   Příklad: Chcete-li načíst ztracený nebo nedávno otočený obnovovací klíč, přihlaste se k webu Portál společnosti Intune z libovolného zařízení. Na portálu klikněte na zařízení a vyberte zařízení s povoleným trezorem úložiště a pak vyberte *získat obnovovací klíč*. Zobrazí se aktuální obnovovací klíč.

5. Po dokončení konfigurace nastavení vyberte **Další**.

6. Na stránce **obor (značky)** zvolte **Vybrat značky oboru** a otevřete tak podokno vybrat značky, abyste přiřadili značky oboru k profilu.

   Pokračujte výběrem tlačítka **Next** (Další).

7. Na stránce **přiřazení** vyberte skupiny, které získají tento profil. Další informace o přiřazování profilů najdete v tématu Přiřazení profilů uživatelů a zařízení.
Vyberte **Další**.

8. Po dokončení na stránce **Revize + vytvořit** klikněte na **vytvořit**. Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

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

   - V *části umístění v úschově popis osobního obnovovacího klíče*přidejte zprávu, která uživatelům pomůže získat obnovovací klíč pro svoje zařízení. Tato informace může být užitečná pro uživatele, když použijete nastavení pro rotaci klíče pro obnovení, což může pravidelně automaticky generovat nový obnovovací klíč pro zařízení.

     Příklad: Chcete-li načíst ztracený nebo nedávno otočený obnovovací klíč, přihlaste se k webu Portál společnosti Intune z libovolného zařízení. Na portálu klikněte na *zařízení* a vyberte zařízení s povoleným trezorem úložiště a pak vyberte *získat obnovovací klíč*. Zobrazí se aktuální obnovovací klíč.

   Nakonfigurujte zbývající [Nastavení trezoru úložišť](endpoint-protection-macos.md#filevault) tak, aby splňovalo vaše obchodní potřeby, a pak vyberte **Další**.

7. Na stránce **obor (značky)** zvolte **Vybrat značky oboru** a otevřete tak podokno vybrat značky, abyste přiřadili značky oboru k profilu.

   Pokračujte výběrem tlačítka **Next** (Další).

8. Na stránce **přiřazení** vyberte skupiny, které získají tento profil. Další informace o přiřazování profilů najdete v tématu Přiřazení profilů uživatelů a zařízení.
Vyberte **Další**.

9. Po dokončení na stránce **Revize + vytvořit** klikněte na **vytvořit**. Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

## <a name="manage-filevault"></a>Správa trezoru úložišť

Postup zobrazení informací o zařízeních, která přijímají zásady trezoru úložišť, najdete v tématu [monitorování šifrování disku](../protect/encryption-monitor.md).

Když Intune nejdřív zašifruje zařízení macOS s trezorem, vytvoří se osobní obnovovací klíč. Po zašifrování zařízení zobrazí pro uživatele zařízení tento osobní klíč jednou.

U spravovaných zařízení může Intune v úschově kopii osobního obnovovacího klíče. V úschově klíčů umožňuje správcům Intune otáčet klíče, aby lépe chránily zařízení a uživatelé obnovili ztracený nebo otočený osobní obnovovací klíč.

Po zašifrování zařízení macOS pomocí trezoru služby Intune:

- Správci můžou klíče pro obnovení trezoru úložišť zobrazovat a spravovat pomocí sestavy šifrování Intune.
- Uživatelé si můžou z webu Portál společnosti na zařízení zobrazit osobní obnovovací klíč zařízení. V rámci webového Portál společnosti zvolte šifrované zařízení macOS a pak zvolte možnost získat klíč pro obnovení jako akci vzdáleného zařízení.

> [!IMPORTANT]
> Zařízení, která jsou zašifrovaná uživateli, a ne Intune, se nedají spravovat přes Intune. To znamená, že Intune nemůže v úschově osobní obnovení těchto zařízení ani spravovat rotaci obnovovacího klíče. Aby mohla Intune spravovat trezory a obnovovací klíče pro zařízení, musí si uživatel dešifrovat svoje zařízení a pak nechat Intune šifrování zařízení.

### <a name="retrieve-personal-recovery-key"></a>Načíst osobní obnovovací klíč

Pro zařízení macOS, která byla zašifrovaná službou Intune, mohou koncoví uživatelé načíst svůj osobní obnovovací klíč (klíč trezoru) pomocí aplikace Portál společnosti pro iOS, aplikace pro Android Portál společnosti nebo prostřednictvím aplikace Intune pro Android.

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
