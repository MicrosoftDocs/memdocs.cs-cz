---
title: Správa ochrany ATP na webu Microsoft Defender pro zařízení s Androidem v Microsoft Intune – Azure | Microsoft Docs
description: Konfigurace webové ochrany v programu Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) pro Android v Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49423d1d1b887aaf3ed3323ff36678bb7319b1ad
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909461"
---
# <a name="configure-microsoft-defender-atp-on-android-devices-you-manage-with-intune"></a>Konfigurace ATP v programu Microsoft Defender na zařízeních s Androidem, která spravujete pomocí Intune

Když integrujete Microsoft Intune a Microsoft Defender Advanced Threat Protection (ATP), můžete pomocí profilů konfigurace zařízení upravit některá nastavení ATP Microsoft Defenderu na zařízeních s Androidem.

Předtím, než budete pokračovat, musíte úspěšně [nakonfigurovat ATP v programu Microsoft Defender v Intune](../protect/advanced-threat-protection-configure.md) a na zařízeních s Androidem do ATP v programu Microsoft Defender.

## <a name="configure-web-protection-on-devices-that-run-android"></a>Konfigurace webové ochrany na zařízeních se systémem Android

Ve výchozím nastavení služba Microsoft Defender ATP pro Android zahrnuje a povoluje funkci webové ochrany. [Webové ochrany](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) pomáhají zabezpečit zařízení proti webovým hrozbám a chránit uživatele před útoky typu phishing.

Přestože je ve výchozím nastavení povolená, existují důvody, proč tuto ochranu na některých zařízeních s Androidem zakázat. Můžete se třeba rozhodnout, že použijete jenom funkci pro kontrolu aplikace v programu Microsoft Defender ATP, nebo můžete zabránit webové ochraně v používání sítě VPN během vyhledávání škodlivých adres URL.

Intune podporuje vypnutí všech funkcí webové ochrany nebo jejich části. Použitá metoda a možnosti, které můžete zakázat, závisí na tom, jak je zařízení s Androidem zaregistrované v Intune:

- **Správce zařízení s Androidem**: pomocí konfiguračního profilu můžete na zařízení nastavit vlastní nastavení OMA-URI, které zakazuje celou funkci webové ochrany nebo zakáže jenom používání VPN. Obecné informace o vlastním nastavení pro zařízení s Androidem najdete v tématu [vlastní nastavení](../configuration/custom-settings-android.md).

- **Pracovní profil Android Enterprise**: k zakázání webové ochrany použijte konfigurační profil aplikace a *Návrháře konfigurace* . Tato metoda a typ registrace podporují zákaz všech funkcí webové ochrany, ale nepodporují zákaz použití sítě VPN. Obecné informace o zásadách konfigurace aplikací najdete v tématu [použití návrháře konfigurace](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer).

Ke konfiguraci webové ochrany na zařízeních použijte následující postupy k vytvoření a nasazení příslušné konfigurace.

### <a name="disable-web-protection-for-android-device-administrator"></a>Zakázat web Protection pro správce zařízení s Androidem

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.

3. Zadejte následující nastavení:

   - **Platforma**: vyberte **Správce zařízení s Androidem** .
   - **Profil**: vyberte **vlastní** .

   Vyberte **Vytvořit**.

4. V části **základy**zadejte následující podrobnosti:

   - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Například *vlastní profil Androidu pro ochranu ATP na webu Microsoft Defender*
   - **Popis**: Zadejte popis profilu. Toto nastavení je volitelné, ale doporučuje se.

5. V **nastavení konfigurace**vyberte **Přidat**.

   Zadejte nastavení pro konfiguraci, kterou chcete nasadit:

   - **Zakázat web Protection**:
     - **Název**: Zadejte jedinečný název pro toto nastavení OMA-URI, abyste ho mohli snadno najít. Například *Zakázat web Protection ATP Microsoft Defender*
     - **Popis**: (volitelné) zadejte popis, který obsahuje přehled nastavení a další důležité podrobnosti.
     - **OMA-URI**: zadejte **./Vendor/MSFT/DefenderATP/AntiPhishing.**
     - **Datový typ**: použijte rozevírací nabídku a vyberte **celé číslo** .
     - **Hodnota**: Pokud chcete zakázat webovou ochranu, včetně kontroly založené na síti VPN, zadejte hodnotu **0** .
       > [!NOTE]
       > Zadejte hodnotu **1** pro povolení webové ochrany, což je výchozí nastavení pro webovou ochranu.

   - **Zakázat pouze používání sítě VPN pomocí webové ochrany**:
     - **Název**: Zadejte jedinečný název pro toto nastavení OMA-URI, abyste ho mohli snadno najít. Například *zakažte Microsoft Defender ATP web Protection VPN* .
     - **Popis**: (volitelné) zadejte popis, který obsahuje přehled nastavení a další důležité podrobnosti.
     - **OMA-URI**: zadejte **./Vendor/MSFT/DefenderATP/VPN.**
     - **Datový typ**: použijte rozevírací nabídku a vyberte **celé číslo** .
     - **Hodnota**: zadáním hodnoty **0** zakážete kontrolu založenou na síti VPN.
       > [!NOTE]
       > Zadejte hodnotu **1** pro povolení webové ochrany, což je výchozí nastavení pro webovou ochranu.

   Vyberte **Přidat** a uložte konfiguraci nastavení OMA-URI a pak pokračujte výběrem možnosti **Další** .

6. V části **přiřazení**určete skupiny, které obdrží tento profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](../configuration/device-profile-assign.md).

7. Pokud jste hotovi, klikněte na tlačítko **vytvořit**a po dokončení **Revize + vytvořit**. Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Zakázat web Protection pro Enterprise Working Profile v Androidu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **aplikace**  >  **zásady konfigurace aplikace**  >  **Přidat**a pak vyberte spravovaná zařízení.

3. V části **základy**zadejte následující podrobnosti:

   - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Například *Konfigurace aplikací pro Android pro ochranu ATP na webu Microsoft Defender ATP*.
   - **Popis**: Zadejte popis profilu. Toto nastavení je volitelné, ale doporučuje se.
   - **Platforma**: vyberte **Android Enterprise**
   - **Typ profilu**: **pouze vybrat pracovní profil**
   - **Cílová aplikace**: klikněte na **Vybrat aplikaci**.

4. V poli **přidružená aplikace**vyhledejte a vyberte **ATP**a pak vyberte **OK**  >  **Další**.

5. V **Nastavení**použijte rozevírací nabídku **formát nastavení konfigurace**, vyberte **použít Návrhář konfigurace**a pak klikněte na **Přidat**. Otevře se Editor JSON.

6. Vyhledejte a vyberte možnost **Webová ochrana**a potom kliknutím na **tlačítko OK** se vraťte na stránku **Nastavení** .

7. Pro **hodnotu konfigurace**zakažte web Protection zadáním hodnoty **0** .

   > [!NOTE]
   > Zadejte hodnotu **1** pro povolení webové ochrany, což je výchozí nastavení pro webovou ochranu.

   Pokračujte výběrem tlačítka **Další**.

8. V části **přiřazení**určete skupiny, které obdrží tento profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](../configuration/device-profile-assign.md).

9. Pokud jste hotovi, klikněte na tlačítko **vytvořit**a po dokončení **Revize + vytvořit**. Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

## <a name="next-steps"></a>Další kroky

- [Monitorování dodržování předpisů pro úrovně rizika](../protect/advanced-threat-protection-monitor.md)
- [Použití úloh zabezpečení se správou ohrožení zabezpečení ATPs k nápravě problémů na zařízeních](../protect/atp-manage-vulnerabilities.md)

Další informace najdete v dokumentaci ke službě Microsoft Defender ATP:

- [Podmíněný přístup Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Řídicí panel rizik pro ATP v programu Microsoft Defender](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)