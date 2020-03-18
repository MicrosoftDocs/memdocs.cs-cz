---
title: Konfigurace vlastního názvu domény
titleSuffix: Microsoft Intune
description: Přidání názvu vlastní domény do předplatného Microsoft Intune
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/26/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 2382f36f-13d8-4a32-81ad-6cfa604889c3
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e9cf01f9ddf7d9d984a99a2d74e0d3294d05e95
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332707"
---
# <a name="configure-a-custom-domain-name"></a>Konfigurace vlastního názvu domény

V tomto tématu najdou správci informace o tom, jak vytvořit záznam DNS CNAME pro zjednodušení a přizpůsobení možností přihlašování v Microsoft Intune.

Pokud si vaše organizace zaregistruje cloudovou službu Microsoftu, třeba Intune, získáte počáteční název domény, jejímž hostitelem je Azure Active Directory (AD). Název může vypadat takto: **vaše_doména.onmicrosoft.com**. V tomto příkladu je **vaše_doména** název domény, který jste si zvolili při registraci. **onmicrosoft.com** je přípona přiřazená účtům přidaným do vašeho předplatného. Místo názvu domény, který získáte s předplatným, můžete pro přístup k Intune nakonfigurovat vlastní doménu vaší organizace.

Než vytvoříte uživatelské účty nebo synchronizujete místní službu Active Directory, důrazně doporučujeme, abyste se rozhodli, jestli chcete používat jenom doménu .onmicrosoft.com, nebo jestli chcete přidat jeden nebo více názvů vlastních domén. Pokud nastavíte vlastní doménu před přidáním uživatelů, správa uživatelů se zjednoduší. Když nastavíte doménu zákazníka, umožníte uživatelům přihlásit se pomocí přihlašovacích údajů, které používají pro přístup k jiným prostředkům domény.

Když se přihlásíte k odběru cloudové služby od Microsoftu, stane se instance této služby [tenantem služby Microsoft Azure AD](https://technet.microsoft.com/library/jj573650.aspx#BKMK_WhatIsAnAzureADTenant), která bude vašim cloudovým službám poskytovat identitu a adresářové služby. Vzhledem k tomu, že postup konfigurace Intune pro používání vlastního názvu domény vaší organizace je stejný jako u jiných tenantů Azure AD, můžete použít informace a postupy uvedené v tématu [Přidání domény](https://azure.microsoft.com/documentation/articles/active-directory-add-domain/).

> [!TIP]
> Další informace o vlastních doménách najdete v části [Přehled pojmů k vlastním názvům domén v Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-add-domain-concepts/).

Tento počáteční název domény onmicrosoft.com nelze přejmenovat ani odebrat. Můžete přidat, ověřit nebo odebrat vlastní názvy domén používané v Intune, abyste zachovali, že vaše obchodní identita bude jasná.

## <a name="to-add-and-verify-your-custom-domain"></a>Přidání a ověření vlastní domény

1. Přejít do [centra pro správu Microsoft 365](https://admin.microsoft.com/) a přihlaste se k účtu správce.

2. V navigačním podokně vyberte **nastavení** &gt; **domény**.

3. Zvolte **Přidat doménu** a zadejte vlastní název domény. Vyberte **Další**.
   ![snímku obrazovky centra pro správu Microsoft 365 s vybraným nastavením > domény a přidáním nového názvu domény](./media/custom-domain-name-configure/domain-custom-add.png)
4. Otevře se dialogové okno **Ověřit doménu** s hodnotami pro vytvoření záznamu TXT u poskytovatele hostingu DNS.
    - **GoDaddy Users**: centrum pro správu Microsoft 365 vás přesměruje na přihlašovací stránku GoDaddy. Po zadání přihlašovacích údajů a přijetí smlouvy o oprávnění ke změně domény se záznam TXT vytvoří automaticky. Případně můžete [záznam TXT vytvořit](https://support.office.com/article/Create-DNS-records-at-GoDaddy-for-Office-365-f40a9185-b6d5-4a80-bb31-aa3bb0cab48a).
    - **Uživatelé Register.com:** Postupujte podle [podrobných pokynů](https://support.office.com/article/Create-DNS-records-at-Register-com-for-Office-365-55bd8c38-3316-48ae-a368-4959b2c1684e#BKMK_verify) k vytvoření záznamu TXT.
5. [Možná budete muset vytvořit další záznamy DNS pro registrace v Intune](../enrollment/windows-enroll.md#simplify-windows-enrollment-without-azure-ad-premium).

Postup pro přidání a ověření vlastní domény může být také [proveden v Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-add-domain/).

Další informace najdete v článku [Informace o vaší počáteční doméně onmicrosoft.com v Office 365](https://support.office.com/article/About-your-initial-onmicrosoft-com-domain-in-Office-365-B9FC3018-8844-43F3-8DB1-1B3A8E9CFD5A).

Další informace o tom, jak [zjednodušit registraci Windows bez Azure AD Premium](../enrollment/windows-enroll.md#simplify-windows-enrollment-without-azure-ad-premium) vytvořením DNS CNAME, který přesměruje registraci na servery Intune.
