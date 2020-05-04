---
title: Nastavení registrace pro zařízení s macOSem
titleSuffix: Microsoft Intune
description: Přečtěte si, jak nastavit registraci zařízení s macOSem v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 46429114-2e26-4ba7-aa21-b2b1a5643e01
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 410911a44ca84230c30ccbea394c24b539b77c4f
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327037"
---
# <a name="set-up-enrollment-for-macos-devices-in-intune"></a>Nastavení registrace pro zařízení s macOSem v Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune umožňuje spravovat zařízení s macOS tak, abyste uživatelům umožnili přístup k firemnímu e-mailu a aplikacím.

Jako správce Intune můžete nastavit registraci zařízení s macOS ve vlastnictví společnosti a zařízení s macOS v osobním vlastnictví (možnost Přineste si vlastní zařízení neboli BYOD). 

## <a name="prerequisites"></a>Požadavky

Před nastavením registrace zařízení s macOS zajistěte splnění následujících požadavků:

- Ujistěte [se, že vaše zařízení má nárok na registraci zařízení Apple](https://support.apple.com/en-us/HT204142#eligibility).
- [Konfigurace domén](../fundamentals/custom-domain-name-configure.md)
- [Nastavení autority MDM](../fundamentals/mdm-authority-set.md)
- [Vytváření skupin](../fundamentals/groups-add.md)
- [Konfigurace Portálu společnosti](../apps/company-portal-app.md)
- Přiřazení uživatelských licencí v [centru pro správu Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Získání certifikátu Apple MDM push Certificate](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="user-owned-macos-devices-byod"></a>Zařízení se systémem macOS vlastněná uživatelem (BYOD)

Uživatelům můžete umožnit registraci vlastních osobních zařízení do správy Intune. To se označuje jako "Přineste si vlastní zařízení" nebo BYOD. Po dokončení požadavků a přiřazení uživatelských licencí si uživatelé můžou svoje zařízení zaregistrovat:
- přechodem na [web Portál společnosti](https://portal.manage.microsoft.com) nebo
- Stahuje se aplikace Portál společnosti Mac na adrese [aka.MS/EnrollMyMac](https://aka.ms/EnrollMyMac).

Uživatelům můžete také poslat odkaz na postup online registrace: [registrace zařízení MacOS v Intune](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp).

Informace o dalších úlohách koncových uživatelů najdete v článcích:

- [Materiály o prostředí Microsoft Intune pro koncové uživatele](../fundamentals/end-user-educate.md)
- [Použití zařízení s macOS s Intune](../user-help/enroll-your-device-in-intune-macos-cp.md)

## <a name="company-owned-macos-devices"></a>Zařízení s macOS ve vlastnictví společnosti
U organizací, které svým uživatelům zařízení pořizují, Intune podporuje následující způsoby registrace zařízení s macOS ve vlastnictví společnosti:
- [Automatický zápis zařízení (ADE) společnosti Apple](device-enrollment-program-enroll-macos.md): organizace si můžou koupit zařízení MACOS přes ADE. ADE umožňuje nasadit registrační profil přes Air, aby bylo možné zařízení spravovat.
- [Správce registrace zařízení (DEM)](device-enrollment-manager-enroll.md): Pomocí účtu DEM můžete zaregistrovat až 1 000 zařízení.

## <a name="block-macos-enrollment"></a>Blokování registrace zařízení s macOS
Intune ve výchozím nastavení umožňuje registraci zařízení s macOS. Pokud chcete u zařízení se systémem macOS registraci blokovat, přečtěte si téma [Nastavení omezení typu zařízení](enrollment-restrictions-set.md).

## <a name="enroll-virtual-macos-machines-for-testing"></a>Registrace virtuálních počítačů s macOS pro účely testování

> [!NOTE]
> Virtuální počítače s macOS se podporují pouze pro testování. Neměli byste je používat jako produkční zařízení pro koncové uživatele. 

Virtuální počítače s macOS pro testování můžete zaregistrovat pomocí softwaru Parallels Desktop nebo VMware Fusion. 

Pro Parallels Desktop musíte nastavit typ hardwaru a sériové číslo virtuálního počítače, aby ho služba Intune mohla rozpoznat. Podle pokynů softwaru Parallels k nastavení typu hardwaru a [sériového čísla](http://kb.parallels.com/123455) nakonfigurujte potřebná nastavení pro testování. Doporučujeme, abyste nastavili stejný typ hardwaru u zařízení, na kterém běží virtuální počítače, i u samotných virtuálních počítačů, které vytváříte. Tento typ hardwaru můžete najít v **nabídce** > Apple**o tomto** > **identifikátoru modelu****sestavy** > systému Mac. 

U softwaru VMware Fusion musíte [upravit soubor .vmx](https://kb.vmware.com/s/article/1014782), abyste mohli nastavit model hardwaru a sériové číslo virtuálního počítače. Doporučujeme, abyste nastavili stejný typ hardwaru u zařízení, na kterém běží virtuální počítače, i u samotných virtuálních počítačů, které vytváříte. Tento typ hardwaru můžete najít v **nabídce** > Apple**o tomto** > **identifikátoru modelu****sestavy** > systému Mac. 

## <a name="user-approved-enrollment"></a>Registrace schválená uživatelem
Registrace MDM schválená uživatelem je typ registrace macOS, kterou můžete využít ke správě určitých nastavení citlivých na zabezpečení. Další informace najdete v [dokumentaci podpory Apple](https://support.apple.com/HT208019).  
 
Během procesu registrace BYOD se uživateli zobrazí výzva k ručnímu schválení profilu Apple Management. Pokyny jsou k dispozici v aplikaci Portál společnosti pro macOS. I když schválení profilu správy není vyžadováno k dokončení registrace, Intune doporučuje uživatele schválené registrace. Pokud uživatel během registrace neschválí profil, uživatel může přejít do**profilů** **systémových předvoleb** > , zvolit profil správy a vybrat **schválit**.    

### <a name="find-out-if-a-device-is-user-approved"></a>Zjistit, jestli je zařízení schválené uživatelem
1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **všechna zařízení**> vyberte **hardware**> zařízení.
3. Podívejte se na pole **registrace schválená uživatelem** .


## <a name="next-steps"></a>Další kroky

Až budou zařízení s macOS zaregistrovaná, můžete [pro zařízení s macOS vytvořit vlastní nastavení](../configuration/custom-settings-macos.md).
