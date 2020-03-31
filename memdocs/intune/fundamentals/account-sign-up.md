---
title: Registrace nebo přihlášení k Microsoft Intune
description: Jak se zaregistrovat k předplatnému Microsoft Intune nebo se přihlásit, abyste mohli začít s vaším předplatným.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0f3ce07a-b718-42a9-bace-f99a8b8abd94
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: e4bec3347ec45f020fd4c8e128278dc619335442
ms.sourcegitcommit: e7fb8cf2ffce29548b4a33b2a0c33a3a227c6bc4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2020
ms.locfileid: "80401449"
---
# <a name="sign-up-or-sign-in-to-microsoft-intune"></a>Registrace nebo přihlášení k Microsoft Intune

V tomto tématu najdou správci systému informace o tom, jak se můžou zaregistrovat a získat účet Intune.

Před přihlášením do Intune si zjistěte, jestli máte účet služeb Microsoft Online Services, smlouvu Enterprise nebo jinou rovnocennou multilicenční smlouvu. Multilicenční smlouva se společností Microsoft nebo jiné předplatné cloudových služeb Microsoft, jako je Office 365, obvykle zahrnují pracovní nebo školní účet.

Pokud už máte svůj pracovní nebo školní účet, **přihlaste se** s jeho použitím a přidejte Intune k svému předplatnému. V opačném případě si můžete **zaregistrovat** pro svoji organizaci nový účet Intune.

>[!WARNING]
>Když si zaregistrujete nový účet, nebude možné s ním kombinovat stávající pracovní nebo školní účet.

## <a name="how-to-sign-up-for-intune"></a>Jak se zaregistrovat k Intune

1. Přejděte na [stránku pro registraci k Intune](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20).

   ![Snímek obrazovky s webovou stránkou registrace účtu zkušební verze Microsoft Intune](./media/account-sign-up/account-sign-up-site.png)

2. Na stránce pro registraci se přihlaste nebo zaregistrujte ke správě nového předplatného služby Intune.

## <a name="post-sign-up-considerations"></a>Aspekty ke zvážení po registraci

Pokud se zaregistrujete k novému předplatnému, přijde vám na e-mailovou adresu, kterou jste zadali během procesu registrace, e-mailová zpráva s informacemi o účtu. Ta potvrzuje, že je vaše předplatné aktivní.

Po dokončení procesu registrace budete přesměrováni na centrum pro správu Microsoft 365, které se používá k přidání uživatelů a přiřazení licencí. Pokud budete používat jen cloudové účty ve výchozí doméně onmicrosoft.com, můžete ihned začít přidávat uživatele a přidělovat jim licence. Pokud ale budete chtít používat [vlastní název domény](custom-domain-name-configure.md) nebo [synchronizovat informace o uživatelských účtech](users-add.md#sync-active-directory-and-add-users-to-intune) s místní službou Active Directory, můžete toto okno prohlížeče zavřít.

## <a name="sign-in-to-microsoft-intune"></a>Přihlášení k Microsoft Intune

Jakmile se zaregistrujete do služby Intune, můžete pomocí libovolného zařízení s [podporovaným prohlížečem](supported-devices-browsers.md#intune-supported-web-browsers) přihlásit se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a službu spravovat.

Ve výchozím nastavení má váš účet ve službě Azure AD jedno z následujících oprávnění:

- Globální správce
- Správce služby Intune (označovaný také jako správce Intune)

Pokud chcete udělit přístup ke správě služby pro uživatele s dalšími oprávněními, podívejte se na téma [Role Access Control](role-based-access-control.md)

### <a name="intune-admin-portal-url"></a>Adresa URL portálu pro správu Intune

Centrum pro správu Microsoft Endpoint Manager: https://endpoint.microsoft.com

Azure Portal Intune: https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade

Intune for Education: https://intuneeducation.portal.azure.com

Klasický portál Intune: https://manage.microsoft.com klasický portál Intune se používá jenom pro správu zařízení zaregistrovaných pomocí klientského softwaru Intune pro počítače.

### <a name="urls-for-intune-services-provided-by-office-365"></a>Adresy URL pro služby Intune poskytované sadou Office 365

Microsoft 365 Business: https://portal.microsoft.com/adminportal

Správa mobilních zařízení s Office 365: https://admin.microsoft.com/adminportal/home#/MifoDevices

## <a name="see-also"></a>Viz také

[Nemůžete se přihlásit k Office 365, Azure nebo Intune.](https://support.microsoft.com/help/2412085)
