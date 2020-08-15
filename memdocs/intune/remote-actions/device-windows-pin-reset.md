---
title: Resetování hesla na zařízeních s Windows v Microsoft Intune – Azure | Microsoft Docs
description: Abyste mohli resetovat heslo na zařízeních s Windows, nainstalujte Microsoft Pin Reset Service a Microsoft Pin Reset Client, vytvořte zásadu pro zařízení pomocí svého ID adresáře Azure Active Directory a pak heslo resetujte na portálu Azure Portal pomocí Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/07/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5027d012-d6c2-4971-a9ac-217f91d67d87
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d74a89cf9a2a049d067205ef556d1a178bfc69fd
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252737"
---
# <a name="reset-the-passcode-on-windows-devices-using-intune"></a>Resetování hesla na zařízeních s Windows pomocí Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

Heslo pro zařízení s Windows můžete resetovat. Funkce resetování hesla využívá Microsoft Pin Reset Service k vygenerování nového hesla pro zařízení s Windows 10 Mobile. 

## <a name="supported-platforms"></a>Podporované platformy

- Windows 10 Mobile s Creators Update a novější (připojené k Azure AD)

Následující platformy **nejsou** podporované:
- Windows
- iOS
- macOS
- Android

## <a name="authorize-the-pin-reset-services"></a>Autorizace služeb pro resetování kódu PIN

Abyste mohli heslo zařízení s Windows resetovat, zaveďte do svého tenanta Intune službu pro resetování kódu PIN.

1. Přejděte na [Microsoft PIN Reset Service](https://login.windows.net/common/oauth2/authorize?response_type=code&client_id=b8456c59-1230-44c7-a4a2-99b085333e84&resource=https%3A%2F%2Fgraph.windows.net&redirect_uri=https%3A%2F%2Fcred.microsoft.com&state=e9191523-6c2f-4f1d-a4f9-c36f26f89df0&prompt=admin_consent) a přihlaste se pomocí účtu správce tenanta.
2. **Přijměte** souhlas, že služba pro resetování kódu PIN získá přístup k vašemu účtu: ![Přijmutí žádosti PIN Reset Serveru o oprávnění](./media/device-windows-pin-reset/pin-reset-service-home-screen.png)
3. Přejděte na [Microsoft PIN Reset Client](https://login.windows.net/common/oauth2/authorize?response_type=code&client_id=9115dd05-fad5-4f9c-acc7-305d08b1b04e&resource=https%3A%2F%2Fcred.microsoft.com%2F&redirect_uri=ms-appx-web%3A%2F%2FMicrosoft.AAD.BrokerPlugin%2F9115dd05-fad5-4f9c-acc7-305d08b1b04e&state=6765f8c5-f4a7-4029-b667-46a6776ad611&prompt=admin_consent) a přihlaste se pomocí účtu správce tenanta. **Přijměte** souhlas, že klient pro resetování kódu PIN získá přístup k vašemu účtu.
4. Na portálu [Azure Portal](https://portal.azure.com) ověřte, že služby pro resetování kódu PIN jsou uvedené v podnikových aplikacích (Všechny aplikace): ![Stránka oprávnění služby pro resetování kódu PIN](./media/device-windows-pin-reset/pin-reset-service-application.png)

> [!NOTE]
> Po přijetí žádosti o resetování kódu PIN se může zobrazit zpráva `Page not found` nebo se může zdát, že se nic nestalo. Toto chování je normální. Zkontrolujte, jestli jsou obě aplikace pro resetování kódu PIN pro vašeho tenanta uvedené.

## <a name="configure-windows-devices-to-use-pin-reset"></a>Konfigurace zařízení s Windows, aby používaly službu PIN Reset Service

Pokud chcete nakonfigurovat resetování kódu PIN na zařízeních s Windows, která spravujete, použijte [vlastní zásady zařízení s Windows 10 v Intune](../configuration/custom-settings-windows-10.md). Zásady nakonfigurujte pomocí následujících poskytovatelů konfiguračních služeb (CSP) pro zásady Windows:

**Použití zásad zařízení** - `./Device/Vendor/MSFT/PassportForWork/*tenant ID*/Policies/EnablePinRecovery`

Místo *tenant ID* použijte své ID adresáře Azure, které je uvedené ve **Vlastnostech** Azure Active Directory na portálu [Azure Portal](https://portal.azure.com).

Nastavte hodnotu pro tohoto poskytovatele konfiguračních služeb na **True**.

> [!TIP]
> Po vytvoření zásady ji přiřadíte (nebo nasadíte) ke skupině. Zásada se dá přiřadit ke skupině uživatelů nebo skupině zařízení. Pokud ho přiřadíte ke skupině uživatelů, může skupina obsahovat uživatele, kteří mají jiná zařízení, jako je například iOS/iPadOS. Technicky se na ně zásada neaplikuje, ale tato zařízení jsou zahrnutá do podrobností o stavu.

## <a name="reset-the-passcode"></a>Resetování hesla

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). 
2. Vyberte **Zařízení** a potom **Všechna zařízení**.
3. Vyberte zařízení, jehož heslo chcete resetovat. Ve vlastnostech zařízení vyberte **resetovat heslo**.
4. Akci potvrďte výběrem **Ano**. Vygeneruje se heslo, které zůstane na portálu zobrazeno dalších sedm dní.

## <a name="next-step"></a>Další krok

Pokud se resetování hesla nepodaří, zobrazí se na portálu odkaz, který poskytne podrobnější informace.
