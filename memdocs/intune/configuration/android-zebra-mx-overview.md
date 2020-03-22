---
title: Používání rozšíření Zebra mobility na zařízeních s Androidem v Microsoft Intune – Azure | Microsoft Docs
description: Pomocí Microsoft Intune můžete spravovat a používat zařízení Zebra se systémem Android s rozšířeními mobility Zebra (MX). Podívejte se na všechny kroky, včetně instalace aplikace Portál společnosti, bokem aplikace, přiřazení role Správce zařízení, vytvoření profilu StageNow a dalších.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: dbb8e5644390c589756af5a69f2fdd5a829866a1
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084009"
---
# <a name="use-and-manage-zebra-devices-with-zebra-mobility-extensions-in-microsoft-intune"></a>Používání a Správa zařízení Zebra s rozšířeními mobility Zebra v Microsoft Intune

Intune obsahuje bohatou sadu funkcí, včetně správy aplikací a konfigurace nastavení zařízení. Tyto integrované funkce a nastavení spravují zařízení s Androidem vyráběná technologiemi Zebra, označovaná také jako "Zebra zařízení".

Na zařízeních s Androidem použijte profily **MX (Zebra)** pro přizpůsobení nebo přidání dalších nastavení specifických pro zebra.

V tomto článku se dozvíte, jak používat rozšíření Zebra mobility (MX) na zařízeních Zebra v Microsoft Intune.

Tato funkce platí pro:

- Správce zařízení s Androidem

Pro zařízení s Androidem Enterprise použijte [OEMConfig](android-oem-configuration-overview.md).

Vaše společnost může používat zařízení Zebra pro maloobchodní prodej, v produkčním patře a dalších. Například jste maloobchodníka a vaše prostředí zahrnuje tisíce Zebrach mobilních zařízení, která používá Sales Associates. Intune může pomáhat spravovat tato zařízení jako součást řešení správy mobilních zařízení (MDM).

Pomocí Intune můžete zaregistrovat zařízení Zebra, abyste mohli do zařízení nasazovat obchodní aplikace. Profily "konfigurace zařízení" umožňují vytvořit profily MX ke správě nastavení specifických pro zebra.

> [!NOTE]
> Ve výchozím nastavení nejsou rozhraní API Zebra MX na zařízeních uzamčena. Předtím, než se zařízení zaregistruje do Intune, je možné, že je zařízení ohrožené škodlivým způsobem. Když je zařízení v čistém stavu, doporučujeme, abyste rozhraní MX API zamkli pomocí Správce přístupu (AccessMgr). Můžete třeba vybrat, aby se vám při volání rozhraní API MX povolily jenom aplikace Portál společnosti a aplikace, kterým důvěřujete.
>
> Další informace najdete v tématu [uzamčení zařízení](https://developer.zebra.com/community/home/blog/2017/04/11/locking-down-your-device) na webu zebra.

## <a name="before-you-begin"></a>Před zahájením

- Ujistěte se, že máte nejnovější verzi aplikace StageNow Desktop z technologií zebra.
- Ujistěte se, že jste zkontrolovali [úplnou matrici funkcí Zebra](http://techdocs.zebra.com/mx/compatibility) (otevře web Zebra), abyste potvrdili, že profily, které vytvoříte, jsou kompatibilní s verzí MX zařízení, verzí operačního systému a modelu.
- Některá zařízení, například TC20/25 zařízení, nepodporují všechny dostupné funkce MX v StageNow. Nezapomeňte zkontrolovat [Zebraou matrici funkcí](http://techdocs.zebra.com/mx/tc2x/) (otevře web Zebra), kde najdete aktualizované informace o podpoře.

## <a name="step-1-install-the-latest-company-portal-app"></a>Krok 1: Instalace nejnovější aplikace Portál společnosti

V zařízení otevřete Google Play Store. Stáhněte si a nainstalujte aplikaci Portál společnosti Intune od Microsoftu. Při instalaci z Google Play aplikace Portál společnosti automaticky získá aktualizace a opravy.

Pokud Google Play není k dispozici, Stáhněte si [Microsoft Intune portál společnosti pro Android](https://www.microsoft.com/download/details.aspx?id=49140) (otevře se další web Microsoftu) a [bokem ho](#sideload-the-company-portal-app) (v tomto článku). Při instalaci tímto způsobem aplikace neobdrží aktualizace nebo opravy automaticky. Nezapomeňte aplikaci pravidelně aktualizovat a opravit ručně.

### <a name="sideload-the-company-portal-app"></a>Bokem aplikaci Portál společnosti

Zkušební načtení je, když nepoužíváte Google Play k instalaci aplikace. K bokem aplikace Portál společnosti použijte StageNow. 

Následující kroky poskytují přehled. Konkrétní podrobnosti najdete v dokumentaci k zebra. [Registrace v MDM pomocí StageNow](http://techdocs.zebra.com/stagenow/3-1/Profiles/enrollmdm/) (otevření webu Zebra) může být dobrým prostředkem.

1. V StageNow vytvořte profil pro **registraci v MDM**.
2. V části **nasazení**vyberte možnost stáhnout soubor agenta MDM.
3. Nastavte **aplikaci podpory** a **Stáhněte kroky konfigurace** na **ne**.
4. V souboru **Stáhnout MDM**vyberte **přenést/kopírovat soubor**. Přidejte zdroj a cíl balíčku Portál společnosti pro Android (APK).
5. V části **Spustit MDM**ponechte výchozí hodnoty tak, jak jsou. Přidejte následující podrobnosti:

    - **Název balíčku**: `com.microsoft.windowsintune.companyportal`
    - **Název třídy**: `com.microsoft.windowsintune.companyportal.views.SplashActivity`

Pokračujte v publikování profilu a využijte ho u aplikace StageNow na zařízení. Aplikace Portál společnosti je nainstalovaná a otevřená na zařízení.

> [!TIP]
> Další informace o StageNow a o tom, co to dělá, najdete v článku [Příprava zařízení s Androidem](https://www.zebra.com/us/en/products/software/mobile-computers/mobile-app-utilities/stagenow.html) (otevření webu Zebra).

## <a name="step-2-confirm-the-company-portal-app-has-device-administrator-role"></a>Krok 2: potvrzení, že aplikace Portál společnosti má roli Správce zařízení

Aplikace Portál společnosti vyžaduje, aby správce zařízení spravoval zařízení se systémem Android. Pokud chcete aktivovat roli Správce zařízení, některá zařízení Zebra zahrnují uživatelské rozhraní (UI) na zařízení. Pokud zařízení obsahuje uživatelské rozhraní, aplikace Portál společnosti vyzve koncového uživatele k udělení Správce zařízení během [zápisu](#step-3-enroll-the-device-in-to-intune) (v tomto článku).

Pokud není k dispozici uživatelské rozhraní, pomocí **DevAdmin Manageru** v StageNow vytvořte profil, který ručně udělí správci zařízení portál společnosti aplikaci.

Následující kroky poskytují přehled. Konkrétní podrobnosti najdete v dokumentaci k zebra. 
[Nastavit režim odkládacích baterií jako správce zařízení](https://zebratechnologies.force.com/s/article/Set-Battery-Swap-Mode-as-Device-Administrator-using-StageNow-Tool) (otevře se webová stránka Zebra) může být dobrým prostředkem.

1. V StageNow vytvořte profil a vyberte **režim Xpert**.
2. Přidejte do profilu **DevAdmin Manager** .
3. Nastavení **Akce Správa zařízení** **zapněte jako správce zařízení**.
4. Nastavte **název balíčku Správce zařízení** na `com.microsoft.windowsintune.companyportal`.
5. Nastavte **název třídy Správce zařízení** na `com.microsoft.omadm.client.PolicyManagerReceiver`.

Pokračujte v publikování profilu a využijte ho u aplikace StageNow na zařízení. Aplikaci Portál společnosti je udělená role Správce zařízení.

## <a name="step-3-enroll-the-device-in-to-intune"></a>Krok 3: registrace zařízení do služby Intune

Po dokončení prvního dvou kroků se Portál společnosti aplikace nainstaluje do zařízení. Zařízení je připravené k registraci do Intune.

[Registrace zařízení s Androidem](../enrollment/android-enroll.md) : seznam kroků. Pokud máte mnoho zařízení Zebra, možná budete chtít použít [účet správce registrace zařízení (DEM)](../enrollment/device-enrollment-manager-enroll.md). Když použijete účet DEM, odeberete taky možnost zrušit registraci z aplikace Portál společnosti, aby uživatelé nemohli zrušit registraci zařízení snadno.

## <a name="step-4-create-a-device-management-profile-in-stagenow"></a>Krok 4: vytvoření profilu správy zařízení v StageNow

Pomocí StageNow vytvořte profil, který konfiguruje nastavení, která chcete na zařízení spravovat. Konkrétní podrobnosti najdete v dokumentaci k zebra. [Profily](http://techdocs.zebra.com/stagenow/3-2/stagingprofiles/) (otevře se webová stránka Zebra) může být dobrým prostředkem.

Když vytvoříte profil v StageNow, vyberte v posledním kroku možnost **exportovat do MDM**. Tento krok generuje soubor XML. Soubor uložte. Budete ho potřebovat v pozdějším kroku.

- Doporučuje se profil otestovat předtím, než ho nasadíte do zařízení ve vaší organizaci. K otestování v posledním kroku při vytváření profilů s StageNow v počítači použijte možnosti **testu** . Pak na zařízení využívejte soubor generovaný StageNow a aplikaci StageNow.

  Aplikace StageNow v zařízení zobrazuje protokoly generované při testování profilu. [Použití protokolů StageNow na zařízeních Zebra s Androidem v Intune](android-zebra-mx-logs-troubleshoot.md) obsahuje informace o použití protokolů StageNow pro pochopení chyb.

- Pokud odkazujete na aplikace, balíčky aktualizací nebo aktualizujete jiné soubory v profilu StageNow, chcete, aby zařízení tyto aktualizace získalo. Aby se aktualizace získaly, musí se zařízení při použití profilu připojit k serveru pro nasazení StageNow. 

  Nebo můžete pomocí integrovaných funkcí v Intune získat tyto změny, včetně:

  - Funkce správy aplikací, které umožňují [přidávat](../apps/apps-add.md), [nasazovat](../apps/apps-deploy.md), aktualizovat a [monitorovat](../apps/apps-monitor.md) aplikace.
  - Správa [aktualizací systému a aplikací](device-restrictions-android-for-work.md#device-owner-only) na zařízeních s Androidem Enterprise

Po otestování souboru je dalším krokem nasazení profilu do zařízení pomocí Intune.

- Do zařízení můžete nasadit jeden nebo několik profilů MX.
- Můžete také exportovat více profilů StageNow a zkombinovat nastavení do jednoho souboru XML. Pak nahrajte soubor XML do Intune a nasaďte ho do svých zařízení.

  > [!WARNING]
  > Pokud je pro stejnou skupinu cíleno více profilů MX a nakonfigurujete stejnou vlastnost, budou v zařízení konflikty.
  >
  > Pokud je stejná vlastnost nakonfigurovaná několikrát v jednom profilu MX, poslední konfigurace služby WINS.

## <a name="step-5-create-a-profile-in-intune"></a>Krok 5: vytvoření profilu v Intune

V Intune vytvořte profil konfigurace zařízení:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující vlastnosti:

    - **Název**: Zadejte popisný název nového profilu.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Správce zařízení s Androidem**.
    - **Typ profilu**: vyberte možnost **profil MX (jenom Zebra)** .

4. V **profilu MX ve formátu. XML**přidejte soubor profilu XML, [který jste exportovali z StageNow](#step-4-create-a-device-management-profile-in-stagenow) (v tomto článku).
5. Vyberte **OK** > **Vytvořit** a změny uložte. Zásada se vytvoří a zobrazí se v seznamu.

    > [!TIP]
    > Z bezpečnostních důvodů nebude po uložení zobrazený text profilu XML. Text je zašifrovaný a zobrazují se jenom hvězdičky (`****`). Pro referenci doporučujeme uložit kopie profilů MX ještě před jejich přidáním do Intune.

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Až zařízení příště zkontroluje aktualizace konfigurace, nasadí se do zařízení profil MX. Zařízení se po registraci zařízení synchronizují s Intune a přibližně každých 8 hodin. Můžete taky [Vynutit synchronizaci v Intune](../remote-actions/device-sync.md). Nebo na zařízení otevřete Portál společnosti > **Nastavení** **aplikace** > **synchronizace**. 

## <a name="update-a-zebra-mx-configuration-after-its-assigned"></a>Aktualizace konfigurace MX Zebra po jejím přiřazení

Pokud chcete aktualizovat konfiguraci specifické pro MX zařízení Zebra, můžete: 

- Vytvořte aktualizovaný soubor XML StageNow, upravte stávající profil Intune MX a nahrajte nový soubor XML StageNow. Tento nový soubor přepíše předchozí zásadu v profilu a nahradí předchozí konfiguraci.
- Vytvořte nový soubor XML StageNow s konfigurací různých nastavení, vytvořte nový profil Intune MX, nahrajte nový soubor XML StageNow a přiřaďte ho ke stejné skupině. Nasazuje se víc profilů. Pokud nový profil konfiguruje nastavení, která již existují v existujících profilech, dojde ke konfliktům.

## <a name="next-steps"></a>Další kroky

- [Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).
- [K řešení potíží se zařízeními Zebra použijte protokoly StageNow](android-zebra-mx-logs-troubleshoot.md).
