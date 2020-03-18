---
title: Odebrání zařízení s Androidem z Intune | Microsoft Docs
description: Odebrání zařízení s Androidem z Portál společnosti Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: f40aab26-7613-48cc-a74e-de83df9465a4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 77c8a972020113b36b57c992b64a6965f733d119
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79324211"
---
# <a name="unenroll-your-android-device-from-management"></a>Zrušení správy registrovaného zařízení s Androidem  

Pokud organizace nechce zaregistrované zařízení s Androidem dále spravovat, může ho odebrat. V tomto článku je popsané, jak zařízení odebrat z aplikace Portál společnosti. Po odebrání zařízení:  

* Zařízení ztratí přístup k chráněným datům a prostředkům organizace.
* Zařízení se přestane zobrazovat na Portálu společnosti.
* Z Portálu společnosti nebude možné instalovat aplikace.
* Už nebudou platit nastavení, která se v zařízení změnila od jeho přidání (třeba zakázání fotoaparátu/kamery nebo vyžadování určité délky hesla).  

> [!NOTE]
> Z aplikace Microsoft Intune nemůžete zrušit registraci zařízení vlastněných společností nebo ho z ní odebrat. Zařízení bylo zaregistrováno během počátečního nastavení zařízení a musí být zaregistrováno pro přístup k prostředkům vaší organizace.  

1. Na Portálu společnosti přejděte do pravého horního rohu a klepněte na tři svislé tečky. Otevře se nabídka akcí.

   ![Snímek obrazovky aplikace pro Android Portál společnosti s nabídkou akce otevřenou v pravém horním rohu. Nová možnost Odebrat portál společnosti je k dispozici jako třetí pod možnostmi Můj profil a Nastavení a nad možnostmi Podmínky, Nápověda a váš názor a O produktu.](./media/android_remove_cp_menu_action_after_1705.png)

2. Klepněte na **Odebrat Portál společnosti**.  

3. Zobrazí se zpráva s informacemi o tom, co se stane, když zrušíte registraci zařízení. Pokud chcete potvrdit, že chcete zařízení z Portálu společnosti odebrat, klepněte na **OK**.

   ![Snímek obrazovky s potvrzením, který je k dispozici po výběru možnosti "odebrat portál společnosti" v nabídce Akce.](./media/android_remove_cp_menu_confirmation_after_1705.png)

## <a name="remove-data-collected-by-the-company-portal-app"></a>Odebrat data shromážděná aplikací Portál společnosti  

Postup odebrání všech dat, která do zařízení uložila aplikace Portál společnosti pro Android:

- Vymažte data aplikace klepnutím na **aplikace** > **[*název aplikace*]**  > **Vymazat data**.
- Odstraňte následující složku: \storage\internal storage\Android\data\com.microsoft.windowsintune.companyportal.

## <a name="uninstall-the-company-portal-app"></a>Odinstalace aplikace Portál společnosti

Portál společnosti je aplikace pro správu zařízení. Nedá se odinstalovat, dokud zrušíte registraci zařízení od jeho správy. Jakmile registraci zrušíte, klepněte na ikonu aplikace Portál společnosti a podržte ji, dokud se nezobrazí **Odinstalovat**. Klepněte na **Odinstalovat** a aplikaci ze zařízení odeberte.  

Případně klepněte na **nastavení** > **aplikace** > **portál společnosti** > **odinstalovat**.  

### <a name="remove-the-company-portal-app-as-a-device-administrator"></a>Odebrání aplikace Portál společnosti jako správce zařízení

Jako poslední možnost můžete aplikaci odinstalovat ze zařízení jako správce zařízení.  

Pokud máte zařízení vlastněné společností, může vaše organizace vyžadovat, aby na zařízení Portál společnosti. Pokud ho odinstalujete, může dojít ke ztrátě přístupu k chráněným prostředkům společnosti, jako je e-mail, aplikace, Wi-Fi nebo VPN, až do opětovné instalace aplikace. Další informace o instalaci, aktualizaci nebo odebrání požadovaných aplikací najdete v tématu [Přidání aplikací do Microsoft Intune](/intune/apps/apps-add#apps-that-are-added-automatically-by-intune).

Tady je postup, jak zakázat Portál společnosti jako správce zařízení. Skutečné názvy jednotlivých nastavení se můžou v zařízení s Androidem lišit.  

**Možnost 1**:  

1. Vyberte **nastavení** > **zabezpečení** > **Další nastavení zabezpečení** > **Správci zařízení**.  
2. Zrušte zaškrtnutí **portál společnosti** výběru.  

**Možnost 2**:

1. Vyberte **nastavení** > **zamykací obrazovce a zabezpečení** > **Další nastavení zabezpečení** > **aplikace pro správu zařízení**.
2. Zrušte zaškrtnutí **portál společnosti** výběru.

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
