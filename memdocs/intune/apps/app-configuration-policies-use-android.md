---
title: Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem Enterprise
titleSuffix: Microsoft Intune
description: Zásady konfigurace aplikací v Microsoft Intune slouží k zadávání nastavení, když uživatelé spustí spravovanou aplikaci Google Play.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d0b6f3fe-2bd4-4518-a6fe-b9fd115ed5e0
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f61f0dd7f0f3b343b8f68de0b20b06d0f69212ac
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81397777"
---
# <a name="add-app-configuration-policies-for-managed-android-enterprise-devices"></a>Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem Enterprise

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Zásady konfigurace aplikací v Microsoft Intune poskytují nastavení spravovaných Google Play aplikací na spravovaných zařízeních s Androidem Enterprise. Vývojář aplikace zveřejňuje nastavení konfigurace aplikace spravované v Androidu. Intune pomocí těchto vydaných nastavení umožní správci nakonfigurovat funkce pro aplikaci. Zásady konfigurace aplikací jsou přiřazené k vašim skupinám uživatelů. Nastavení zásad se používá, když je aplikace kontroluje, obvykle při prvním spuštění aplikace.

> [!NOTE]  
> Některé aplikace konfiguraci aplikací nepodporují. Obraťte se na vývojáře aplikace a zjistěte, jestli jejich aplikace podporuje zásady konfigurace aplikací.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2.  > Vyberte zásady **Apps** > **Konfigurace aplikací**aplikace**Přidat** > **spravovaná zařízení**. Všimněte si, že si můžete vybrat mezi **spravovanými zařízeními** a **spravovanými aplikacemi**. Další informace najdete v tématu [aplikace, které podporují konfiguraci aplikací](app-configuration-policies-overview.md#apps-that-support-app-configuration).
3. Na stránce **základy** nastavte následující podrobnosti:
    - **Název**: Název profilu, který se zobrazí na portálu Azure Portal
    - **Popis**: Popis profilu, který se zobrazí na portálu Azure Portal
    - **Typ registrace zařízení** – toto nastavení je nastavené na **spravovaná zařízení**.
4. Jako **platformu**vyberte **Android Enterprise** .
5. Klikněte na **Vybrat aplikaci** vedle **cílové aplikace**. Zobrazí se podokno **přidružená aplikace** . 
6. V podokně **přidružená aplikace** vyberte spravovanou aplikaci, kterou chcete přidružit k zásadám konfigurace, a klikněte na **OK**.
7. Kliknutím na **Další** zobrazte stránku **Nastavení** .
8. Kliknutím na tlačítko **Přidat** zobrazte podokno **Přidat oprávnění** .
9. Klikněte na oprávnění, která chcete přepsat. Udělená oprávnění přepíšou u vybraných aplikací zásadu výchozí oprávnění aplikace.
10. Nastavte **stav oprávnění** pro každé oprávnění. Můžete si vybrat z **příkazového řádku**, **automatického udělení**nebo **automaticky odepřít**. Další informace o oprávněních najdete v tématu [nastavení pro Android Enterprise a označení zařízení jako kompatibilních nebo nekompatibilních s Intune](../protect/compliance-policy-create-android-for-work.md).
11. Pokud spravovaná aplikace podporuje nastavení konfigurace, zobrazí se rozevírací okno **formát nastavení konfigurace** . Chcete-li přidat informace o konfiguraci, vyberte jednu z následujících metod:
    - **Použití návrháře konfigurace**
    - **Zadat data JSON**<br><br>
    Podrobnosti o používání návrháře konfigurace najdete v části [Použití návrháře konfigurace](#use-the-configuration-designer). Podrobnosti o zadávání dat XML naleznete v tématu [ENTER data JSON](#enter-json-data).
12. Kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .
13. V rozevíracím seznamu vedle pole **přiřadit k**vyberte možnost **vybrané skupiny**, **Všichni uživatelé**, **všechna zařízení**nebo **Všichni uživatelé a všechny** oddálení, aby bylo možné zásadu konfigurace aplikace přiřadit k.

    ![Snímek obrazovky s přiřazením zásad – karta Zahrnout](./media/app-configuration-policies-use-ios/app-config-policy01.png)

14. Vyberte možnost **Všichni uživatelé** v rozevíracím seznamu.

    ![Snímek obrazovky s přiřazením zásad – možnost rozevírací nabídky Všichni uživatelé](./media/app-configuration-policies-use-ios/app-config-policy02.png)

15. Klikněte na možnost **Vybrat skupiny, které se vyloučí** a zobrazte tak související podokno.

    ![Snímek obrazovky s přiřazením zásad – vyberte skupiny, které chcete vyloučit.](./media/app-configuration-policies-use-ios/app-config-policy03.png)

16. Vyberte skupiny, které chcete vyloučit, a potom klikněte na **Vybrat**.

    >[!NOTE]
    >Pokud přidáváte skupinu a pro daný typ přiřazení už byla zahrnuta jakákoliv jiná skupina, je pro ostatní typy zahrnutí přiřazení předem vybraná a není ji možné změnit. Tato použitá skupina se tedy nedá použít jako vyloučená skupina.

17. Kliknutím na **Další** zobrazte stránku **Revize + vytvořit** .
18. Kliknutím na **vytvořit** přidejte zásady konfigurace aplikací do Intune.

## <a name="use-the-configuration-designer"></a>Použití návrháře konfigurace

Pokud je aplikace navržená tak, aby podporovala nastavení konfigurace, můžete použít návrháře konfigurace pro spravované aplikace Google Play. Konfigurace se týká zařízení zaregistrovaných v Intune. Návrhář vám umožní nakonfigurovat konkrétní hodnoty konfigurace pro nastavení vystavené aplikací.

1. Vyberte **Přidat**. Vyberte seznam nastavení konfigurace, která chcete pro aplikaci zadat.

    Pokud pro e-mailovou aplikaci používáte GMail nebo devět práce, v části [nastavení zařízení s Androidem Enterprise nakonfigurujte e-mail](../configuration/email-settings-android-enterprise.md) , kde najdete další informace o těchto nastaveních.

2. Pro každý klíč a hodnotu v konfiguraci nastavte:

    - **Typ hodnoty**: datový typ konfigurační hodnoty. U hodnot typu Řetězec můžete případně vybrat jako typ hodnoty proměnnou nebo profil certifikátu.
    - **Hodnota konfigurace**: hodnota pro konfiguraci. Pokud pro **typ hodnoty**vyberete možnost proměnná nebo certifikát, vyberte ze seznamu proměnných nebo profilů certifikátů. Pokud zvolíte certifikát, pak se za běhu naplní alias certifikátu nasazeného do zařízení.

### <a name="supported-variables-for-configuration-values"></a>Podporované proměnné u hodnot konfigurace

Pokud jako typ hodnoty zvolíte proměnnou, můžete vybírat z následujících možností:

| Možnost | Příklad |
|----|----|
| ID zařízení AAD | dc0dc142-11d8-4b12-bfea-cae2a8514c82 |
| Account ID | fc0dc142-71d8-4B12-bbea-bae2a8514c81 |
| ID zařízení Intune | b9841cd9-9843-405F-be28-b2265c59ef97 |
| Domain (Doména) | contoso.com |
| Pošta | john@contoso.com |
| Částečný hlavní název uživatele | Jan |
| ID uživatele | 3ec2c00f-b125-4519-acf0-302ac3761822 |
| Uživatelské jméno | Jan Karásek |
| Hlavní název uživatele | john@contoso.com |

### <a name="allow-only-configured-organization-accounts-in-multi-identity-apps"></a>Povolte jenom nakonfigurované účty organizace v aplikacích s více identitami 

Jako správce Microsoft Intune můžete určit, které uživatelské účty se přidají do aplikací Microsoftu na spravovaných zařízeních. Můžete omezit přístup jenom na povolené uživatelské účty organizace a zablokovat osobní účty na zaregistrovaných zařízeních. Pro zařízení s Androidem použijte následující dvojice klíč/hodnota:

| **Key** | com.microsoft.intune.mam.AllowedAccountUPNs |
|---|---|
| **Hodnoty** | <ul><li>Jeden nebo více hlavních názvů uživatele (UPN) oddělených <code>;</code>.</li><li>Jediné povolené účty jsou spravované uživatelské účty definované pomocí tohoto klíče.</li><li> Pro zařízení zaregistrovaná v Intune se může použít token <code>{{userprincipalname}}</code>, aby představoval účet zaregistrovaného uživatele.</li></ul> |

   > [!NOTE]
   > Následující aplikace zpracovávají výše uvedenou konfiguraci aplikace a povolují jenom účty organizace:
   > - Edge pro Android (42.0.4.4048 a novější)
   > - Office, Word, Excel, PowerPoint pro Android (16.0.9327.1000 a novější)
   > - OneDrive pro Android (5,28 a novější)
   > - Outlook pro Android (2.2.222 a novější)

## <a name="enter-json-data"></a>Zadat data JSON

Některá nastavení konfigurace aplikací (jako jsou aplikace s typy sad) se nedají konfigurovat pomocí návrháře konfigurace. Pro tyto hodnoty použijte Editor JSON. Nastavení se aplikaci poskytne automaticky při její instalaci.

1. U položky **Formát nastavení konfigurace** zvolte možnost pro **otevření editoru JSON**.
2. V editoru můžete definovat hodnoty JSON pro nastavení konfigurace. Výběrem možnosti **Stáhnout šablonu JSON** stáhnete vzorový soubor, který můžete následně nakonfigurovat.
3. Zvolte **OK** a pak **Přidat**.

Zásada se vytvoří a zobrazí se v seznamu.

Když se přiřazená aplikace na zařízení spustí, použijí se nastavení, která jste nakonfigurovali v zásadách konfigurace aplikací.

## <a name="preconfigure-the-permissions-grant-state-for-apps"></a>Konfigurace stavu udělení oprávnění aplikacím

Pro přístup k funkcím zařízení s Androidem můžete také předem nakonfigurovat oprávnění aplikace. Aplikace pro Android, které vyžadují oprávnění zařízení, jako je například přístup k umístění nebo fotoaparátu zařízení, ve výchozím nastavení vyzvat uživatele k přijetí nebo odmítnutí oprávnění.

Aplikace například používá mikrofon zařízení. Uživatel je vyzván, aby aplikaci udělil oprávnění používat mikrofon.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace** > **zásady** >  konfigurace aplikace**Přidat** > **spravovaná zařízení**.
2. Přidejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je třeba, aby se **pro celou firmu zobrazila zásada aplikace s oprávněním pro Android Enterprise**.
    - **Popis**. Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Typ registrace zařízení**: Toto nastavení je nastavené na **spravovaná zařízení**.
    - **Platforma**: vyberte **Android**.

3. Vyberte **přidružená aplikace**. Vyberte aplikaci, pro kterou chcete definovat zásady konfigurace. Vyberte ze seznamu aplikací pro pracovní profil Androidu, které jste schválili a synchronizovali s Intune.
4. Vyberte **oprávnění** > **Přidat**. V seznamu vyberte dostupná oprávnění aplikace > **OK**.
5. U každého oprávnění vyberte způsob, jakým se bude v rámci této zásady udělovat:
    - **Vyzvat**. Vyzval uživatele ke schválení nebo zamítnutí
    - **Automaticky udělit**: Automaticky schválí bez upozornění uživatele.
    - **Automaticky odepřít**: Automaticky zamítne bez upozornění uživatele.
6. Zásady konfigurace aplikací přiřadíte tak, že vyberete zásady konfigurace aplikace > **přiřazení** > **skupiny**. Vyberte skupiny uživatelů, které chcete přiřadit > **Vybrat**.
7. Kliknutím na **Uložit** zásadu přiřaďte.

## <a name="additional-information"></a>Další informace

- [Přiřazení spravované aplikace Google Play k zařízením s Androidem Enterprise](apps-add-android-for-work.md#assigning-a-managed-google-play-app-to-android-enterprise-work-profile-devices)
- [Nasazení Outlooku pro iOS/iPadOS a nastavení konfigurace aplikací pro Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

## <a name="next-steps"></a>Další kroky

Pokračujte s [přiřazením](apps-deploy.md) a [sledováním](apps-monitor.md) aplikace.
