---
title: Nastavení autority pro správu mobilních zařízení
titleSuffix: Microsoft Intune
description: Nastavte autoritu pro správu mobilních zařízení v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 8deff871-5dff-4767-9484-647428998d82
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4209c461877786000e01dd03e4e0dea9f76a6e84
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270952"
---
# <a name="set-the-mobile-device-management-authority"></a>Nastavení autority pro správu mobilních zařízení

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Nastavení autority pro správu mobilních zařízení (MDM) určuje způsob správy zařízení. Jako správce IT musíte nastavit autoritu MDM, aby uživatelé mohli registrovat zařízení pro správu.

Možné konfigurace:

- **Intune Standalone** – jedná se o pouze cloudovou správu, kterou můžete nakonfigurovat pomocí portálu Azure Portal. Zahrnuje celou sadu možností, které Intune nabízí. [Nastavte autoritu MDM v konzole Intune](#set-mdm-authority-to-intune).

- **Spoluspráva Intune** – integrace cloudového řešení Intune s Configuration Manager pro zařízení s Windows 10. Intune můžete konfigurovat pomocí konzoly Configuration Manager. [Konfigurace automatického zápisu zařízení do Intune](https://docs.microsoft.com/configmgr/comanage/tutorial-co-manage-clients#configure-auto-enrollment-of-devices-to-intune) 

- **Správa mobilních zařízení pro office 365** – Pokud máte aktivovaný MDM pro Office 365, uvidíte autoritu MDM nastavenou na "Office 365". Pokud chcete začít používat Intune, budete si muset koupit licence Intune.

- **Office 365 MDM koexistence** – službu Intune můžete přidat do svého tenanta, pokud už používáte MDM pro Office 365 a pro každého uživatele nastavíte autoritu pro správu na Intune nebo MDM pro Office 365 pro každého uživatele, který určí, která služba se bude používat ke správě zařízení zaregistrovaných v MDM. Autorita pro správu jednotlivých uživatelů je definována na základě licence přiřazené uživateli: Pokud má uživatel pouze licenci pro Microsoft 365 Basic nebo Standard, budou jejich zařízení spravována MDM pro Office. Pokud má uživatel licenci entitling Intune, jejich zařízení se budou spravovat přes Intune. Pokud přidáte licenci entitling Intune k uživateli, který dřív spravovala služba MDM pro Office, budou jejich zařízení přepnuta do správy Intune. Ujistěte se, že jsou konfigurace Intune přiřazené uživatelům, aby před přepnutím uživatelů do Intune nahradily MDM pro Office, jinak jejich zařízení ztratí konfiguraci MDM pro Office a neobdrží žádné náhrady z Intune.

## <a name="set-mdm-authority-to-intune"></a>Nastavení autority MDM na Intune

Pokud jste ještě nenastavili autoritu MDM, proveďte postup uvedený níže.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte oranžový banner a otevřete nastavení **autority pro správu mobilních zařízení** . Oranžová informační zpráva se zobrazí jenom v případě, že jste autoritu MDM ještě nenastavili.
2. V oblasti **Autorita pro správu mobilních zařízení** zvolte některou autoritu MDM z následujících možností:
   - **Autorita MDM Intune**
   - **Žádné**

   ![Snímek obrazovky Intune s nastavením autority pro správu mobilních zařízení](./media/mdm-authority-set/set-mdm-auth.png)

   Zobrazí se zpráva, že jste úspěšně nastavili autoritu MDM na Intune.

### <a name="workflow-of-intune-administration-ui"></a>Pracovní postup pro uživatelské rozhraní pro správu Intune
Pokud je povolená správa zařízení s Androidem nebo zařízení Apple, odesílá Intune informace o zařízení a uživateli, aby byla možná integrace služeb třetích stran a správa příslušných zařízení.

Mezi scénáře, pro které se přidává souhlas se sdílením dat, patří:
- Povolení pracovních profilů Androidu
- Povolení a nahrání certifikátů Apple MDM Push Certificate
- Povolení některé ze služeb Apple, jako jsou například Program registrace zařízení, School Manager a Volume Purchase Program

V každém případě je vyjádření souhlasu omezeno výhradně na spouštění služby správy mobilního zařízení. Jedná se například o potvrzení, že správce IT má autorizaci k registraci zařízení Google nebo Apple. Dokumentaci obsahující informace, které se po přechodu na nové pracovní postupy budou sdílet, najdete v následujících umístěních:
- [Data z Intune odesílaná Googlu](https://aka.ms/Data-intune-sends-to-google)
- [Data z Intune odesílaná Applu](https://aka.ms/data-intune-sends-to-apple)

## <a name="key-considerations"></a>Klíčové aspekty
Po přechodu na novou autoritu MDM pravděpodobně nastane přechodná doba (až osm hodin), než se zařízení ohlásí a synchronizuje se službou. Je potřeba nakonfigurovat nastavení nové autority MDM a ujistit se, že zaregistrovaná zařízení budou po změně nadále spravovaná a chráněná. 
- Zařízení se musí ke službě po změně připojit, aby nastavení z nové autority MDM (Intune samostatně) nahradila stávající nastavení v zařízení.
- Po změně autority MDM některá základní nastavení (například profily) z předchozí autority MDM zůstanou v zařízení po dobu až sedmi dnů nebo do chvíle, kdy se zařízení ke službě poprvé připojí. Doporučuje se nakonfigurovat aplikace a nastavení (zásady, profily, aplikace atd.) v nové autoritě MDM co nejdříve a nasadit nastavení do skupin uživatelů obsahujících uživatele, kteří mají stávající zaregistrovaná zařízení. Jakmile se zařízení ke službě po změně autority MDM připojí, obdrží nová nastavení z nové autority MDM a zabrání se mezerám ve správě a ochraně.
- Zařízení, která nemají přidružené uživatele (obvykle když máte scénáře pro iOS/iPadOS Program registrace zařízení nebo hromadné registrace), se nemigrují do nové autority MDM. Pro taková zařízení musíte zavolat podporu, aby vám s přesunem do nové autority MDM pomohla.

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>Vyčištění mobilních zařízení po vypršení platnosti certifikátu MDM

Certifikát MDM se obnovuje automaticky, když mobilní zařízení komunikují se službou Intune. Když se mobilní zařízení vymažou nebo se jim po určitou dobu nedaří komunikovat se službou Intune, certifikát MDM se neobnoví. Zařízení se z portálu Azure Portal odebere po uplynutí 180 dnů od vypršení platnosti certifikátu MDM.

## <a name="remove-mdm-authority"></a>Odebrání autority MDM

Autoritu MDM nemůžete změnit zpátky na neznámou. Autorita pro správu mobilních zařízení používá službu k určení, která zařízení zaregistrovaná na portálu se budou hlásit (Microsoft Intune nebo Office 365 MDM).

## <a name="what-to-expect-after-changing-the-mdm-authority"></a>Co očekávat po změně autority MDM

- Když služba Intune zjistí, že se Autorita MDM tenanta změnila, pošle zprávu oznámení všem zaregistrovaným zařízením, aby je bylo možné zaregistrovat a synchronizovat se službou (Toto oznámení je mimo pravidelné plánované vrácení se změnami). Proto po změně autority MDM pro tenanta ze samostatné Intune se všechna zařízení, která jsou zapnutá a online, připojí ke službě, obdrží novou autoritu MDM a budou spravovaná novou autoritou MDM. Správa a ochrana těchto zařízení se nijak nepřeruší.
- I když jsou zařízení při změně autority MDM (nebo krátce po ní) zapnutá a online, může trvat až osm hodin, než se do služby zaregistrují pod novou autoritou MDM (záleží na načasování příští naplánované pravidelné registrace).    

  > [!IMPORTANT]    
  > V době mezi změnou autority MDM a nahráním obnoveného certifikátu APNs do nové autority se nové registrace zařízení a zařízení se systémem iOS/iPadOS nezdaří. Proto je důležité certifikát APNs zkontrolovat a do nové autority nahrát co nejdřív po změně autority MDM.

- Uživatelé můžou na novou autoritu MDM rychle přejít ručním spuštěním registrace zařízení do služby. Tuto změnu uživatelé snadno provedou pomocí aplikace Portál společnosti a inicializováním kontroly dodržování předpisů zařízením.
- Pokud chcete ověřit, jestli správně fungují a když se zařízení zaregistrují a synchronizovaly se službou po změně autority MDM, hledejte zařízení v nové autoritě MDM.
- Během změny autority MDM a ohlašování zařízení do služby bude zařízení přechodně offline. Aby se zajistilo, že zařízení během tohoto přechodného období zůstane chráněné a funkční, zůstanou v zařízení po dobu až sedmi dnů (nebo dokud se zařízení nepřipojí k nové autoritě MDM a neobdrží nová nastavení, která přepíší ta stávající) následující profily:
  - E-mailový profil
  - Profil VPN
  - Profil certifikátu
  - Wi-Fi profil
  - Konfigurační profily
- Po změně na novou autoritu MDM může trvat až týden, než budou data o dodržování předpisů v konzole pro správu Microsoft Intune přesná. Stavy dodržování předpisů v Azure Active Directory a na zařízení však přesné budou, takže zařízení je i nadále chráněné.
- Zajistěte, aby nová nastavení, která mají přepsat stávající nastavení, měla stejný název jako ta předchozí, aby se původní nastavení skutečně přepsala. Jinak může mít zařízení nadbytečné profily a zásady.    

  > [!TIP]    
  > Osvědčený postup je takový, že všechna nastavení a konfigurace správy vytvoříte a nasazení provedete krátce po dokončení změny autority MDM. To vám pomáhá zajistit, aby byla zařízení v přechodném období chráněná a aktivně spravovaná.

- Po změně autority MDM pomocí následujících kroků zkontrolujte, jestli se nová zařízení do nové autority úspěšně zaregistrovala:   
  - Zaregistrujte nové zařízení.
  - Ujistěte se, že se nově zaregistrované zařízení zobrazuje v nové autoritě MDM.
  - Proveďte z konzoly pro správu na zařízení akci, jako je vzdálené uzamčení. Pokud je akce úspěšná, zařízení je spravované novou autoritou MDM.
- Pokud máte problémy s konkrétními zařízeními, můžete zrušit jejich registraci a znovu je zaregistrovat, aby se co nejdříve připojila k nové autoritě a byla spravována.

## <a name="next-steps"></a>Další kroky

Po nastavení autority MDM můžete zahájit [registraci zařízení](../enrollment/device-enrollment.md).
