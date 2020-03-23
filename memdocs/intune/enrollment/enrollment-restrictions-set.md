---
title: Nastavení omezení registrace v Microsoft Intune
titleSuffix: ''
description: Omezení registrace podle platformy a nastavení limitu počtu zařízení pro registraci zařízení v Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/17/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9691982c-1a03-4ac1-b7c5-73087be8c5f2
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f68278e936a85ab21407e55c8d5c18529457938a
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331543"
---
# <a name="set-enrollment-restrictions"></a>Nastavení omezení registrace

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Jako správce Intune můžete vytvořit a spravovat omezení registrace, která definují, jaká zařízení se můžou registrovat ke správě pomocí Intune, včetně těchto:
- Počet zařízení.
- Operační systémy a verze.

Můžete vytvořit více omezení a použít je u různých skupin uživatelů. Pro různá omezení můžete nastavit [pořadí priority](#change-enrollment-restriction-priority).

>[!NOTE]
>Omezení registrací nepatří k funkcím zabezpečení. Ohrožená zařízení mohou poskytovat zavádějící informace. Tato omezení jsou jen určitou bariérou pro uživatele bez zlých úmyslů.

Mezi konkrétní omezení registrace, která můžete vytvořit, patří:

- Maximální počet zaregistrovaných zařízení
- Platformy zařízení, které se mohou zaregistrovat:
  - Správce zařízení s Androidem
  - Pracovní profil Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows
  - Windows Mobile
- Verze operačního systému platformy pro iOS/iPadOS, Správce zařízení s Androidem, pracovní profil Android Enterprise, Windows a Windows Mobile. (Je možné použít jenom verze Windows 10. Pokud jsou povolená Windows 8.1., nechejte prázdné.)
  - Minimální verze
  - Maximální verze
- Omezte [zařízení v osobním vlastnictví](device-enrollment.md#bring-your-own-device) (jenom iOS, Správce zařízení s Androidem, pracovní profil Android Enterprise, MacOS, Windows a Windows Mobile).

## <a name="default-restrictions"></a>Výchozí omezení

Pro omezení registrace typu i limitu počtu zařízení se automaticky poskytnou výchozí omezení. Možnosti výchozích omezení můžete změnit. Výchozí omezení se použijí pro všechny registrace zařízení s uživateli i bez uživatelů. Tato výchozí omezení můžete přepsat tak, že vytvoříte nová omezení s vyšší prioritou.

## <a name="create-a-device-type-restriction"></a>Vytvoří omezení typu zařízení.

1. Přihlaste se [k centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **zařízení** > **omezení registrace** > **vytvořit omezení** > **omezení typu zařízení**.
2. Na stránce **základy** poskytněte omezení **název** a volitelný **Popis**.
3. Kliknutím na tlačítko **Další** přejdete na stránku **Nastavení platformy** .
4. V části **platforma**vyberte možnost **Povolení** pro platformy, u kterých chcete toto omezení omezit.
    ![zakončení obrazovky pro výběr nastavení platformy](./media/enrollment-restrictions-set/choose-platform-settings.png)
5. V části **verze**vyberte minimální a maximální verze, které mají povolené platformy podporovat. Omezení verze se vztahují jenom na zařízení zaregistrovaná ve Portál společnosti.
     Podporované formáty verzí:
    - Správce zařízení s Androidem a pracovní profil Android Enterprise podporují hlavní. podverze. rev. Build.
    - iOS/iPadOS podporuje hlavní_verze. podverze. rev. Verze operačního systému se nevztahují na zařízení Apple, která se registrují pomocí Program registrace zařízení, Apple School Manageru nebo aplikace Apple Configuratoru.
    - Windows podporuje jenom hlavní_verze. podverze. Build. rev jenom pro Windows 10.
    
    > [!IMPORTANT]
    > Android Enterprise (pracovní profil) a platformy pro správce zařízení s Androidem mají následující chování:
    > - Pokud jsou obě platformy pro stejnou skupinu povolené, budou se uživatelé registrovat s pracovním profilem, pokud ho jejich zařízení podporuje. v opačném případě se budou registrovat jako DA. 
    > - Pokud jsou obě platformy pro skupinu a upřesnění pro konkrétní a překrývající se verze, budou uživatelé dostávat tok registrace definovaný pro svou verzi operačního systému. 
    > - Pokud jsou obě platformy povolené, ale blokované pro stejné verze, budou se uživatelé na zařízeních s blokovanými verzemi považovat za tok registrace Správce zařízení s Androidem a pak se zablokuje a zobrazí se výzva k odhlášení. 
    >
    > Poznamenat si, že registrace pracovního profilu nebo Správce zařízení nebude fungovat, pokud se příslušné informace nedokončí při registraci Androidu. 
    
   > [!Note]
   > Windows 10 neposkytuje během registrace číslo rev, takže pokud zadáte v 10.0.17134.100 a zařízení bude 10.0.17134.174, bude během registrace zablokované.

6. V části **osobní vlastnictví**vyberte **Povolit** pro platformy, které chcete povolit jako zařízení v osobním vlastnictví.
7. V části **výrobce zařízení**Zadejte čárkami oddělený seznam výrobců, které chcete blokovat.
8. Kliknutím na tlačítko **Další** přejdete na stránku **přiřazení** .
9. Zvolte **Vybrat skupiny, které chcete zahrnout** , a potom pomocí vyhledávacího pole vyhledejte skupiny, které chcete zahrnout do tohoto omezení. Omezení platí jenom u skupin, ke kterým je přiřazené. Pokud omezení nepřiřadíte alespoň k jedné skupině, nebude mít žádný efekt. Pak zvolte **Vybrat**. 
    ![zakončení obrazovky pro výběr nastavení platformy](./media/enrollment-restrictions-set/select-groups.png)
10. Kliknutím na tlačítko **Další** přejdete na stránku **Revize + vytvořit** .
11. Vyberte **vytvořit** a vytvořte tak omezení.
12. Priorita nově vytvořeného omezení bude o jeden stupeň vyšší než výchozí omezení. [Prioritu můžete změnit](#change-enrollment-restriction-priority).


## <a name="create-a-device-limit-restriction"></a>Vytvoření omezení limitu počtu zařízení

1. Přihlaste se [k centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **zařízení** > **omezení registrace** > **vytvořit** omezení > omezení **limitu počtu zařízení**.
2. Na stránce **základy** poskytněte omezení **název** a volitelný **Popis**.
3. Kliknutím na tlačítko **Další** přejdete na stránku **omezení počtu zařízení** .
4. V poli **limit počtu zařízení**vyberte maximální počet zařízení, která může uživatel zaregistrovat.
    ![zakončení obrazovky pro výběr limitu zařízení](./media/enrollment-restrictions-set/choose-device-limit.png)
5. Kliknutím na tlačítko **Další** přejdete na stránku **přiřazení** .
6. Zvolte **Vybrat skupiny, které chcete zahrnout** , a potom pomocí vyhledávacího pole vyhledejte skupiny, které chcete zahrnout do tohoto omezení. Omezení platí jenom u skupin, ke kterým je přiřazené. Pokud omezení nepřiřadíte alespoň k jedné skupině, nebude mít žádný efekt. Pak zvolte **Vybrat**. 
    ![zakončení obrazovky pro výběr skupin](./media/enrollment-restrictions-set/select-groups-device-limit.png)
7. Kliknutím na tlačítko **Další** přejdete na stránku **Revize + vytvořit** .
8. Vyberte **vytvořit** a vytvořte tak omezení.
9. Priorita nově vytvořeného omezení bude o jeden stupeň vyšší než výchozí omezení. [Prioritu můžete změnit](#change-enrollment-restriction-priority).

Během registrace BYOD uživatelům se zobrazí oznámení, že se při dosažení limitu počtu zaregistrovaných zařízení. Například v systému iOS:

![Oznámení o dosažení limitu počtu zařízení s iOSem](./media/enrollment-restrictions-set/enrollment-restrictions-ios-set-limit-notification.png)

> [!IMPORTANT]
> Omezení limitu počtu zařízení se nevztahují na tyto typy zápisu Windows:
> - Spoluspravované registrace
> - Registrace objektů zásad skupiny
> - Azure Active Directory připojené registrace
> - Registrace do hromadné Azure Active Directory připojené
> - Registrace autopilotu
> - Registrace správce registrace zařízení
>
> Omezení limitu počtu zařízení pro tyto typy registrace se neuplatňují, protože se považují za scénáře sdíleného zařízení.
> Můžete nastavit omezení pro tyto typy zápisu [v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings).


## <a name="change-enrollment-restrictions"></a>Změna omezení registrace

Nastavení omezení registrace můžete změnit podle následujících kroků. Tato omezení neovlivňují zařízení, která jsou už zaregistrovaná. Pomocí této funkce se nedají blokovat zařízení zaregistrovaná prostřednictvím [agenta Intune pro počítače](../fundamentals/manage-windows-pcs-with-microsoft-intune.md).

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **zařízení** > **omezení registrace** > vyberte omezení, které chcete v > **vlastnostech**změnit.
2. Klikněte na tlačítko **Upravit** vedle nastavení, které chcete změnit.
3. Na stránce **Upravit** proveďte požadované změny a přejděte na stránku **Revize + Uložit** a pak zvolte **Uložit**.


## <a name="blocking-personal-android-devices"></a>Blokování osobních zařízení s Androidem
- Pokud zablokujete registraci zařízení s osobním vlastnictvím zařízení s Androidem, můžou se zařízení s Androidem Enterprise Work profilů pořád zaregistrovat.
- Ve výchozím nastavení jsou nastavení zařízení vašeho pracovního profilu Android Enterprise shodná s nastavením vašich zařízení pro správce zařízení s Androidem. Až změníte pracovní profil pro Android Enterprise nebo nastavení Správce zařízení s Androidem, to už neplatí.
- Pokud zablokujete osobní registraci pracovních profilů pro Android Enterprise, můžou se registrovat jenom zařízení s Androidem ve vlastnictví firmy v Android Enterprise Working Profiles.

## <a name="blocking-personal-windows-devices"></a>Blokování osobních zařízení s Windows
Když zablokujete registraci osobních zařízení s Windows, Intune u každého nového požadavku na registraci zařízení s Windows zkontroluje, jestli se autorizoval jako firemní registrace. Neautorizované registrace se zablokují.

K registraci zařízení s Windows ve společnosti jsou povoleny následující metody:
- Uživatel se registruje pomocí [účtu správce registrace zařízení]( device-enrollment-manager-enroll.md).
- Zařízení se registruje prostřednictvím programu [Windows AutoPilot](enrollment-autopilot.md).
- Zařízení se zaregistruje u automatického pilotního nasazení Windows, ale v nastavení Windows se nejedná o možnost jenom registrace MDM.
- Číslo IMEI zařízení je uvedené v seznamu **Registrace zařízení** >  **[Identifikátory podnikových zařízení](corporate-identifiers-add.md)** . (Nepodporuje se ve Windows Phone 8.1.)
- Zařízení se registruje v rámci [balíčku hromadného zřizování](windows-bulk-enroll.md).
- Zařízení se registruje prostřednictvím objektu zásad skupiny nebo [automatického zápisu z Configuration Manager pro spolusprávu](https://docs.microsoft.com/configmgr/comanage/quickstart-paths#bkmk_path1).
 
Intune označí jako firemní tyto registrace. Protože ale nenabízí řízení Intune pro správu jednotlivých zařízení, zablokují se:
- [Automatická registrace MDM](windows-enroll.md#enable-windows-10-automatic-enrollment) s [připojením k Azure Active Directory během instalace Windows](https://docs.microsoft.com/azure/active-directory/device-management-azuread-joined-devices-frx)\*.
- [Automatická registrace MDM](windows-enroll.md#enable-windows-10-automatic-enrollment) s [připojením k Azure Active Directory z nastavení Windows](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network).*
 
Zablokují se také následující metody osobní registrace:
- [Automatická registrace MDM](windows-enroll.md#enable-windows-10-automatic-enrollment) s [přidáním pracovního účtu z nastavení Windows](https://docs.microsoft.com/azure/active-directory/user-help/user-help-join-device-on-network)\*.
- Volba [Jen registrace MDM]( https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) v nastavení Windows.

\*Nezablokují se, pokud se k registraci použije Autopilot.


## <a name="blocking-personal-iosipados-devices"></a>Blokování osobních zařízení s iOS/iPadOS
Ve výchozím nastavení Intune klasifikuje zařízení s iOS/iPadOS jako osobně vlastněná. Aby bylo možné klasifikovat zařízení se systémem iOS nebo iPadOS ve vlastnictví firmy, musí splňovat jednu z následujících podmínek:
- Registrováno se sériovým číslem nebo IMEI.
- Zaregistrováno pomocí automatického zápisu zařízení (dříve Program registrace zařízení)


## <a name="change-enrollment-restriction-priority"></a>Změna priority omezení registrace

Priorita se používá, když uživatel existuje v několika skupinách, ke kterým jsou přiřazena omezení. Uživatelé podléhají jenom omezení s nejvyšší prioritou přiřazenému ke skupině, ve které se nacházejí. Jan je například ve skupině A, která má přiřazena omezení s prioritou 5, a také ve skupině B, na kterou se vztahují omezení s prioritou 2. U Jana se uplatní jenom omezení s prioritou 2.

Když vytvoříte omezení, přidá se do seznamu bezprostředně nad výchozí omezení.

Registrace zařízení obsahuje výchozí omezení jak pro omezení typu zařízení, tak pro omezení limitu počtu zařízení. Tato dvě omezení platí pro všechny uživatele, pokud je nepřepíšete omezeními s vyšší prioritou.

Prioritu kteréhokoli nevýchozího omezení můžete změnit.

1. Přihlaste se k portálu Azure Portal.
2. Zvolte **Další služby**, vyhledejte **Intune** a zvolte **Intune**.
3. Zvolte **Registrace zařízení** > **Omezení registrace**.
4. Najeďte kurzorem myši na omezení v seznamu priorit.
5. Pomocí tří svislých teček přetáhněte prioritu na požadované místo v seznamu.