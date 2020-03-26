---
title: Konfigurace Google Chrome pro zařízení s Androidem pomocí Intune
titleSuffix: Microsoft Intune
description: Použijte zásady konfigurace Intune s Google Chrome pro zařízení s Androidem.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: deca7632c590d63c31f32375bc3f72047ae30807
ms.sourcegitcommit: fe7484e86ec8a109fa5f54fe9cceef8aac94bd9f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/26/2020
ms.locfileid: "80274621"
---
# <a name="configure-google-chrome-for-android-devices-using-intune"></a>Konfigurace Google Chrome pro zařízení s Androidem pomocí Intune 

Pomocí zásad konfigurace aplikací Intune můžete nakonfigurovat Google Chrome pro zařízení s Androidem. Nastavení aplikace lze automaticky použít. Můžete například konkrétně nastavit záložky a adresy URL, které chcete blokovat nebo zakázat.

## <a name="prerequisites"></a>Požadavky

- Zařízení s Androidem Enterprise uživatele musí být zaregistrované v Intune. Další informace najdete v tématu [Nastavení registrace zařízení s pracovním profilem v Androidu Enterprise](../enrollment/android-work-profile-enroll.md).
- Google Chrome se přidá jako spravovaná aplikace Google Play. Další informace o spravovaných Google Play najdete v tématu [připojení účtu Intune k vašemu spravovanému Google Playmu účtu](../enrollment/connect-intune-android-enterprise.md).

## <a name="add-the-google-chrome-app-to-intune"></a>Přidání aplikace Google Chrome do Intune

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **všechny aplikace** > **přidejte** a přidejte **spravovanou Google Play** aplikaci.
3. Přejít na Managed Google Play, hledejte pomocí **Google Chrome** a schvalte.

    ![Hledání a schvalování Google Chrome](./media/apps-configure-chrome-android/search.png)

4. Přiřaďte Google Chrome k skupině uživatelů jako požadovaný typ aplikace. Google Chrome se nasadí automaticky, když se zařízení zaregistruje do Intune.

Další podrobnosti o přidání spravované aplikace Google Play do Intune najdete v tématu [spravované aplikace Google Play Storu](apps-add-android-for-work.md#managed-google-play-store-apps).

## <a name="add-app-configuration-for-managed-ae-devices"></a>Přidat konfiguraci aplikace pro spravovaná zařízení s AE

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace** > **zásady konfigurace aplikací** > **Přidat** > **spravovaná zařízení**.
2. Zadejte tyto podrobnosti:
    - **Název**: Název profilu, který se zobrazí na portálu Azure Portal
    - **Popis**: Popis profilu, který se zobrazí na portálu Azure Portal
    - **Typ registrace zařízení** – toto nastavení je nastavené na **spravovaná zařízení**.
    - **Platforma** – vyberte **Android**.

    ![Přidat zásady konfigurace Google Chrome](./media/apps-configure-chrome-android/add-policy.png)

3. Kliknutím na **přidružená aplikace** zobrazíte podokno **přidružená aplikace** . Najděte a vyberte **Google Chrome**. Tento seznam obsahuje [spravované aplikace Google Play, které jste schválili a synchronizovali s Intune](apps-add-android-for-work.md).

    ![Výběr Google Chrome v části přidružená aplikace](./media/apps-configure-chrome-android/associated-app.png)

4. Klikněte na **nastavení konfigurace**, vyberte **použít Návrhář konfigurací**a pak klikněte na **Přidat** a vyberte konfigurační klíče.

    ![Přidat návrháře konfigurace použití](./media/apps-configure-chrome-android/configuration.png)

    Níže je uveden příklad běžných nastavení:
    - **Zablokovat přístup k seznamu adres URL**: `["*"]`
    - **Povolení přístupu k seznamu adres URL**: `["baidu.com", "youtube.com", "chromium.org", "chrome://*"]`
    - **Spravované záložky**: `[{"toplevel_name": "My managed bookmarks folder"  },  {"url": "baidu.com",   "name": "Baidu"},  {"url": "youtube.com", "name": "Youtube"},  {"name": "Chrome links",  "children": [{"url": "chromium.org", "name": "Chromium"},    {"url": "dev.chromium.org", "name": "Chromium Developers"}]}]`
    - **Dostupnost režimu anonymním**: `Incognito mode disabled`

    Po přidání nastavení konfigurace pomocí návrháře konfigurace budou uvedená v tabulce. 

    ![Společná nastavení](./media/apps-configure-chrome-android/common-settings.png)

    Výše uvedená nastavení vytvoří záložky a zablokuje přístup ke všem adresám URL s výjimkou `baidu.com`, `yahoo.com`, `chromium.org`a `chrome://`.

5. Kliknutím na **OK** a **Přidat** přidejte zásady konfigurace do Intune.
6. Přiřaďte tyto zásady konfigurace ke skupině uživatelů. Další informace najdete v článku [Přiřazení aplikací do skupin pomocí Microsoft Intune](apps-deploy.md).

## <a name="verify-the-device-settings"></a>Ověření nastavení zařízení

Jakmile je zařízení s Androidem zaregistrované v Androidu Enterprise, automaticky se nasadí spravovaná aplikace Google Chrome s ikonou portfolia.

   <img alt="Managed Google Chrome with the portfolio icon" src="./media/apps-configure-chrome-android/chrome-icon.png" width="350">

Spusťte Google Chrome a zobrazí se použitá nastavení.

   Záložky<br>
   <img alt="Bookmarks" src="./media/apps-configure-chrome-android/bookmarks.png" width="350">

   Blokovaná adresa URL:<br>
   <img alt="Blocked URL" src="./media/apps-configure-chrome-android/blocked-url.png" width="350">

   Adresa URL pro povolení:<br>
   <img alt="Allow URL" src="./media/apps-configure-chrome-android/allowed-url.png" width="350">

   Karta anonymním:<br>
   <img alt="Incognito tab" src="./media/apps-configure-chrome-android/incognito-tab.png" width="350">

## <a name="troubleshooting"></a>Odstraňování potíží

1. Podívejte se na portál Intune, kde můžete monitorovat stav nasazení zásad.

    ![Monitorovat stav nasazení zásad](./media/apps-configure-chrome-android/monitor-status.png)

2. Spusťte Google Chrome a navštivte **Chrome://Policy**. Můžeme potvrdit, jestli se nastavení úspěšně používala.

    ![Potvrzení nastavení se úspěšně zavedla.](./media/apps-configure-chrome-android/confirm.png)

## <a name="additional-information"></a>Další informace

- [Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem Enterprise](app-configuration-policies-use-android.md)
- [Seznam zásad pro Chrome Enterprise](https://cloud.google.com/docs/chrome-enterprise/policies/)

## <a name="next-steps"></a>Další kroky

- Další informace o plně spravovaných zařízeních s Androidem Enterprise najdete v tématu [Nastavení registrace v Intune pro Android Enterprise plně spravovat zařízení](../enrollment/android-fully-managed-enroll.md).
