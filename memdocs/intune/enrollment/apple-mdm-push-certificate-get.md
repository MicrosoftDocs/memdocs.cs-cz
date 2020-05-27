---
title: Získání certifikátu Apple MDM push Certificate pro Intune
titleSuffix: ''
description: Získání certifikátu Apple MDM push Certificate pro správu zařízení s iOS/iPadOS pomocí Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/08/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a66171d678ffd19e424fb399633c3fed3db9a588
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987006"
---
# <a name="get-an-apple-mdm-push-certificate"></a>Získání certifikátu Apple MDM Push Certificate

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Aby Intune mohl spravovat zařízení se systémem iOS/iPadOS a macOS, vyžaduje se certifikát Apple MDM push Certificate. Po přidání certifikátu do Intune si uživatelé můžou zaregistrovat zařízení pomocí:

- aplikace Portál společnosti,

- nástrojů hromadné registrace Apple, jako je Program registrace zařízení, Apple School Manager nebo Apple Configurator.

Další informace o možnostech registrace najdete v tématu [Volba způsobu registrace zařízení se systémem iOS/iPadOS](ios-enroll.md).

Když platnost certifikátu Push vyprší, je nutné ho obnovit. Při obnovování je třeba použít stejné Apple ID jako při prvním vytvoření certifikátu Push.


## <a name="steps-to-get-your-certificate"></a>Kroky k získání certifikátu
Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), zvolte **zařízení**  >  **Registrovat zařízení**  >  **registrace Apple**  >  **Apple MDM push Certificate**a pak postupujte podle těchto kroků.

### <a name="step-1-grant-microsoft-permission-to-send-user-and-device-information-to-apple"></a>Krok 1. Udělte Microsoftu oprávnění k odesílání informací o uživatelích a zařízeních společnosti Apple.
Vyberte Souhlasím **.** udělte Microsoftu oprávnění odesílat data do společnosti Apple.

![Obrazovka Konfigurace certifikátu MDM Push Certificate s nenastaveným certifikátem MDM Push](./media/apple-mdm-push-certificate-get/create-mdm-push-certificate.png)

### <a name="step-2-download-the-intune-certificate-signing-request-required-to-create-an-apple-mdm-push-certificate"></a>Krok 2. Stáhněte si žádost o podepsání certifikátu (CSR) pro Intune, která je potřebná k vytvoření certifikátu Apple MDM Push Certificate.
Vyberte **Stáhnout CSR** a stáhněte a uložte si soubor žádosti lokálně. Tento soubor slouží k vyžádání certifikátu vztahu důvěryhodnosti z portálu Apple Push Certificates Portal.

### <a name="step-3-create-an-apple-mdm-push-certificate"></a>Krok 3. Vytvořte certifikát Apple MDM Push Certificate.
Vyberte **vytvořit certifikát MDM push Certificate** a přejdete na portál Apple Push Certificates Portal. Přihlaste se pomocí Apple ID vaší společnosti a pak klikněte na **vytvořit certifikát**. Vyberte **zvolit soubor** a vyhledejte soubor žádosti o podepsání certifikátu a pak zvolte **nahrát**. Na stránce potvrzení vyberte **Stáhnout** a Stáhněte si soubor certifikátu (. pem) a uložte soubor místně.

> [!NOTE]
> K certifikátu je přidružené Apple ID použité k jeho vytvoření. Doporučuje se použít firemní Apple ID pro úlohy správy a zajistit monitorování poštovní schránky více než jednou osobou jako v případě distribučního seznamu. Nikdy nepoužívejte osobní Apple ID.

### <a name="step-4-enter-the-apple-id-used-to-create-your-apple-mdm-push-certificate"></a>Krok 4. Zadejte Apple ID, které jste použili k vytvoření certifikátu Apple MDM Push Certificate.
Poznamenejte si toto ID pro případ potřeby obnovení tohoto certifikátu.

### <a name="step-5-browse-to-your-apple-mdm-push-certificate-to-upload"></a>Krok 5. Procházením vyhledejte certifikát Apple MDM Push Certificate, který chcete nahrát.
Vyhledejte soubor certifikátu (. pem), zvolte **otevřít**a pak zvolte **nahrát**. S certifikátem Push Certificate může Intune registrovat a spravovat zařízení Apple.

## <a name="renew-apple-mdm-push-certificate"></a>Obnovení certifikátu Apple MDM Push Certificate
Certifikát Apple MDM push Certificate je platný jeden rok a musí se každoročně obnovovat, aby se zachovala Správa zařízení s iOS/iPadOS a macOS. Pokud vyprší platnost vašeho certifikátu, zaregistrovaná zařízení Apple nebude možné kontaktovat.

K certifikátu je přidružené Apple ID použité k jeho vytvoření. Obnovte certifikát MDM Push Certificate s použitím stejného Apple ID, které se použilo k jeho vytvoření.

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)a vyberte **zařízení**  >  **Registrovat zařízení**  >  **registrace Apple**  >  **Apple MDM push Certificate**.
2. Vyberte **Stáhnout CSR** a stáhněte a uložte si soubor žádosti lokálně. Tento soubor slouží k vyžádání certifikátu vztahu důvěryhodnosti z portálu Apple Push Certificates Portal.
3. Vyberte **vytvořit certifikát MDM push Certificate** a přejdete na portál Apple Push Certificates Portal. Vyhledejte certifikát, který chcete obnovit, a vyberte možnost **obnovit**.
4. Na obrazovce **obnovit certifikát push** zadejte poznámky, které vám v budoucnosti pomůžou certifikát identifikovat, vyberte **zvolit soubor** , přejděte na nový soubor žádosti, který jste stáhli, a zvolte **nahrát**.
   > [!TIP]
   > Certifikát je možné identifikovat podle jeho jedinečného ID. Projděte si **ID subjektu** v podrobnostech certifikátu a vyhledejte část identifikátoru GUID daného identifikátoru. Případně můžete na zaregistrovaném zařízení se systémem iOS/iPadOS přejít na **Nastavení**  >  **Obecné**Správa  >  **zařízení** **Profil správy**  >  **Management Profile**  >  **Další podrobnosti**  >  **Profil správy**. Druhá položka řádku, **téma**, obsahuje jedinečný identifikátor GUID, který můžete porovnat s certifikátem na portálu Apple Push Certificates Portal.
 
6. Na obrazovce **potvrzení** vyberte **Stáhnout** a uložte soubor. pem místně.
7. V [Intune](https://go.microsoft.com/fwlink/?linkid=2090973)vyberte ikonu procházení **Apple MDM push Certificate** , vyberte soubor. pem stažený od společnosti Apple a zvolte **nahrát**.

Váš certifikát Apple MDM push Certificate se zobrazí jako **aktivní** a má 365 dní do vypršení platnosti.
