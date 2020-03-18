---
title: Operační systémy a prohlížeče podporované v Microsoft Intune
titleSuffix: ''
description: Seznam podporovaných platforem zařízení a prohlížečů pro správu zařízení přes Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/19/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d1ac59c-a885-4276-8576-f3cf81c2d268
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7f2fd16e0d4130fcc13b69a34d17777f1fd3d0f4
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330499"
---
# <a name="supported-operating-systems-and-browsers-in-intune"></a>Podporované operační systémy a prohlížeče v Intune

Před nastavením Microsoft Intune zkontrolujte podporované operační systémy a prohlížeče.

Nápovědu k instalaci Intune na zařízení najdete v tématu [použití spravovaných zařízení k tomu, abyste mohli provádět práce](https://docs.microsoft.com/user-help/company-portal-frequently-asked-questions) a [využití šířky pásma Intune](network-bandwidth-use.md).

Další informace o podpoře poskytovatele konfigurační služby najdete v referenčních informacích o [poskytovateli služby konfigurace](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).

> [!NOTE]
> Intune teď pro aplikace a zařízení vyžaduje Android 5. x (Lupa) nebo vyšší. pro přístup k prostředkům společnosti prostřednictvím aplikace Portál společnosti pro Android a sady Intune App SDK pro Android. Tento požadavek neplatí pro Polycomch týmů založených na Androidu se systémem 4,4. Tato zařízení budou nadále podporována. 

## <a name="intune-supported-operating-systems"></a>Operační systémy podporované službou Intune

Můžete spravovat zařízení, která používají následující operační systémy:

[!INCLUDE [mdm-supported-devices](../includes/mdm-supported-devices.md)]

### <a name="supported-samsung-knox-standard-devices"></a>Podporovaná zařízení Samsung Knox Standard

Aby při aktivaci Knox nedošlo k chybám, které brání registraci ke správě mobilních zařízení, pokusí se aplikace Portál společnosti o aktivaci Samsung Knox během registrace ke správě mobilních zařízení, jen pokud je zařízení uvedené v [seznamu podporovaných zařízení Knox](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Zařízení, která nepodporují aktivaci Samsung Knox, se zaregistrují jako standardní zařízení s Androidem. Některá čísla modelů zařízení Samsung mohou podporovat Knox, některá nemusí. Než zařízení Samsung koupíte a nasadíte, ověřte si u prodejce, jestli je kompatibilní se systémem Knox.

> [!NOTE]
> Registrace zařízení Samsung Knox může vyžadovat, abyste [povolili přístup k serverům Samsung](https://support.samsungknox.com/hc/articles/115013833108-Our-corporate-devices-are-behind-a-firewall-How-do-I-enable-Knox-Workspace-devices-to-contact-Samsung-servers).

Modely zařízení Samsung v následujícím seznamu nepodporují Knox. Aplikace Portál společnosti pro Android je zaregistruje jako nativní zařízení s Androidem:

| **Název zařízení** | **Číslo modelu zařízení** |
| --- | --- |
| Galaxy Avant | SM-G386T |
| Galaxy Core 2/Core 2 Duos | SM-G355H<br>SM-G355M |
| Galaxy Core Lite | SM-G3588V |
| Galaxy Core Prime | SM-G360H |
| Galaxy Core LTE | SM-G386F<br>SM-G386W |
| Galaxy Grand | GT-I9082L<br>GT-I9082<br>GT-I9080L |
| Galaxy Grand 3 | SM-G7200 |
| Galaxy Grand Neo | GT-I9060I |
| Galaxy Grand Prime Value Edition | SM-G531H |
| Galaxy J Max | SM-T285YD |
| Galaxy J1 | SM-J100H<br>SM-J100M<br>SM-J100ML |
| Galaxy J1 Ace | SM-J110F<br>SM-J110F |
| Galaxy J1 Mini | SM-J105M |
| Galaxy J2/J2 Pro | SM-J200H<br>SM-J210F |
| Galaxy J3 | SM-J320F<br>SM-J320FN<br>SM-J320H<br>SM-J320M |
| Galaxy K Zoom | SM-C115 |
| Galaxy Light | SGH-T399N |
| Galaxy Note 3 | SM-N9002<br>SM-N9009 |
| Galaxy Note 7/Note 7 Duos | SM-N930S<br>SM-N9300<br>SM-N930F<br>SM-N930T<br>SM-N9300<br>SM-N930F<br>SM-N930S<br>SM-N930T |
| Galaxy Note 10.1 3G | SM-P602 |
| Galaxy S2 Plus | GT-I9105P |
| Galaxy S3 Mini | SM-G730A<br>SM-G730V |
| Galaxy S3 Neo | GT-I9300<br>GT-I9300I |
| Galaxy S4 | SM-S975L |
| Galaxy S4 Neo | SM-G318ML |
| Galaxy S5 | SM-G9006W |
| Galaxy S6 Edge | 404SC |
| Galaxy Tab A 7.0&quot; | SM-T280<br>SM-T285 |
| Galaxy Tab 3 7&quot;/Tab 3 Lite 7&quot; | SM-T116<br>SM-T210<br>SM-T211 |
| Galaxy Tab 3 8.0&quot; | SM-T311 |
| Galaxy Tab 3 10.1&quot; | GT-P5200<br>GT-P5210<br>GT-P5220 |
| Galaxy Trend 2 Lite | SM-G318H |
| Galaxy V Plus | SM-G318HZ |
| Galaxy Young 2 Duos | SM-G130BU |

### <a name="windows-pc-software-client"></a>Softwarový klient pro počítače s Windows

Jako alternativní metodu registrace jde na počítače s Windows nasadit a nainstalovat [softwarového klienta Intune](manage-windows-pcs-with-microsoft-intune.md). Tato funkce je dostupná jen při používání klasického portálu Intune. Softwarového klienta Intune můžete použít ke správě 10 a novějších počítačů s výjimkou Windows 10 Home Edition.

> [!Note]
> Společnost Microsoft oznámila, že podpora Windows 7 končí od ledna 14 2020. K tomuto datu přestane také Intune podporovat zařízení s Windows 7.
>
> Další informace najdete v tématu [plán pro změny v Intune: konec podpory pro Windows 7](whats-new.md#windows-7-ends-extended-support).
>
> Microsoft Intune vyřadí podporu pro konzolu Intune založenou na Silverlightu 15. října 2020. Toto vyřazení zahrnuje koncovou podporu konzoly Silverlight nakonfigurovaného POČÍTAČového softwaru klienta (označuje se také jako agent pro počítače).
>
> Další informace najdete v tématu [Microsoft Intune ukončení podpory pro konzolu pro správu na bázi Silverlight](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Take-Action-Microsoft-Intune-ending-support-for-the-Silverlight/ba-p/916249).

<!--  ### Exchange ActiveSync management

You can manage [Exchange ActiveSync devices](../enrollment/device-enrollment.md#mobile-device-management-with-exchange-activesync-and-intune) from the Intune console. This option provides a limited set of management capabilities when compared to the other methods. See [Capabilities of built-in Mobile Device Management in Office 365](https://support.office.com/article/Capabilities-of-built-in-Mobile-Device-Management-for-Office-365-a1da44e5-7475-4992-be91-9ccec25905b0) for a list of supported devices.  -->

## <a name="intune-supported-web-browsers"></a>Podporované webové prohlížeče Intune

Různé úlohy správy vyžadují, abyste použili některý z následujících webů pro správu.

- [Centrum pro správu Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Azure Portal](https://portal.azure.com/)

Portály podporují následující prohlížeče:

- Microsoft Edge (nejnovější verze)
- Microsoft Internet Explorer 11
- Safari (nejnovější verze, jen Mac)
- Chrome (nejnovější verze)
- Firefox (nejnovější verze)

### <a name="intune-classic-portal"></a>Klasický portál Intune

Klasický portál Intune se používá jenom ke správě zařízení zaregistrovaných pomocí klientského softwaru Intune pro počítače (https://manage.microsoft.com). Klasický portál Intune vyžaduje, aby prohlížeč podporoval Silverlight.

Konzolu Intune podporují následující prohlížeče vybavené technologií Silverlight:

- Internet Explorer 10 nebo novější
- Google Chrome (verze starší než verze 42)
- Mozilla Firefox s povoleným programem Silverlight (verze starší než verze 56)

> [!Note]
> Klasický portál Intune nepodporuje Microsoft Edge ani mobilní prohlížeče, protože nepodporují [Microsoft Silverlight](https://msdn.microsoft.com/library/cc838158(v=vs.95).aspx).

K tomuto portálu se můžou přihlásit jen uživatelé, kteří mají oprávnění správce služeb nebo jsou správcem tenanta s rolí globálního správce. Abyste získali přístup ke konzole pro správu, musí mít váš účet licenci k používání Intune a stav registrace **Povoleno**.
