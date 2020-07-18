---
title: Řešení potíží se zařízeními s Androidem Enterprise v Microsoft Intune
description: Návrhy pro řešení některých nejběžnějších problémů při registraci zařízení s Androidem v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/25/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b51ed6653dff5b7d0aeef40892e16e2826f30204
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461245"
---
# <a name="troubleshoot-android-enterprise-device-problems-in-microsoft-intune"></a>Řešení potíží se zařízeními s Androidem Enterprise v Microsoft Intune

Tento článek pomáhá správcům Intune pochopit a řešit problémy, když se zařízení s Androidem Enterprise v Intune nacházejí.

## <a name="apps-on-android-enterprise-devices"></a>Aplikace na zařízeních s Androidem Enterprise

### <a name="managed-google-play-apps-that-arent-deployed-through-intune-are-displayed-in-the-work-profile"></a>Spravované Google Play aplikace, které nejsou nasazené prostřednictvím Intune, se zobrazují v pracovním profilu.
Systémové aplikace můžete v pracovním profilu povolit výrobcem OEM zařízení v době, kdy se pracovní profil vytvoří. Toto neřídí poskytovatel MDM.

K řešení potíží použijte následující postup:

  1. Shromáždí protokoly Portál společnosti.
  2. Všimněte si neočekávaných aplikací, které se zobrazují v pracovním profilu.
  3. Zruší registraci zařízení v Intune a odinstalace Portál společnosti.
  4. Nainstalujte aplikaci [test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc) , která umožňuje vytvořit pracovní profil bez modulu EMM pro testování.
  5. Podle pokynů v části [test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc) vytvořte pracovní profil na zařízení.
  6. Zkontrolujte aplikace, které se zobrazují v pracovním profilu. 
  7. Pokud se stejné aplikace zobrazují v aplikaci test DPC, aplikace je pro toto zařízení očekávána výrobcem OEM.

### <a name="unapproved-managed-google-play-for-work-store-apps-arent-being-removed-from-the-client-apps-page-in-intune"></a>Neschválené aplikace spravované Google Play pro pracovní úložiště se neodstraňují na stránce klientské aplikace v Intune.
Toto chování je očekávané.

### <a name="managed-google-play-apps-arent-being-reported-under-the-discovered-apps-blade-in-the-intune-portal"></a>Spravované Google Play aplikace nejsou hlášeny v okně zjištěné aplikace na portálu Intune.
Toto chování je očekávané. V okně zjištěné aplikace jsou v inventáři pouze systémové aplikace nainstalované v pracovním profilu. Pokud chcete zobrazit nainstalované spravované aplikace Google Play, použijte okno **spravované aplikace** .

### <a name="are-web-applications-supported-for-work-profile-enrolled-devices"></a>Jsou webové aplikace podporované pro zařízení zaregistrovaná v pracovním profilu?
Yes. Další informace najdete v tématu [spravované Google Play webové odkazy](../apps/apps-add-android-for-work.md#managed-google-play-web-links) .

## <a name="device-management"></a>Správa zařízení

### <a name="file-path-internal-storageandroiddatacommicrosoftwindowsintunecompanyportalfiles-missing-on-work-profile-enrolled-devices"></a>Cesta k souboru interní úložiště/Android/data. com. Microsoft. WindowsIntune. CompanyPortal/soubory chybějící v zaregistrovaných zařízeních pracovního profilu

  **Odpověď**: Toto chování je očekávané. Tato cesta je vytvořená jenom pro scénář Správce zařízení (starší verze registrace Androidu).

  Pokud chcete shromažďovat protokoly Portál společnosti, postupujte takto:

  1. V aplikaci Portál společnosti s označením klepněte na **nabídku**  >  **pomocná**  >  **e-mailová podpora**a potom klepněte na **Odeslat e-mail & Odeslat protokoly**. 
  2. Až se vám zobrazí výzva k **odeslání žádosti o podporu**, vyberte jednu z e-mailových aplikací.
  3. Správci IT se vygeneruje e-mail s ID incidentu, které je možné poskytnout podpoře produktů Microsoftu.

### <a name="managed-google-play-last-sync-time--hasnt-been-updated-in-days"></a>Čas poslední synchronizace spravovaného Google Play se neaktualizoval ve dnech.
Toto chování je očekávané. Synchronizace se spustí, jenom když to uděláte ručně.

### <a name="encryption-is-required-when-a-device-is-enrolled-can-it-be-turned-off"></a>Když je zařízení zaregistrované, vyžaduje se šifrování. Může být vypnutá?
Ne, Google vyžaduje, aby zařízení bylo zašifrované, aby bylo možné vytvořit pracovní profil. 

### <a name="samsung-devices-are-blocking-the-use-of-third-party-keyboards-like-swiftkey"></a>Zařízení Samsung blokují použití klávesnic třetích stran, jako je SwiftKey.
Společnost Samsung začala toto omezení na zařízeních s Androidem 8.0 a novějším vynucovat. Společnost Microsoft v současnosti pracuje s Samsung na tomto problému a bude publikovat nové informace, jakmile bude k dispozici.

## <a name="remote-actions"></a>Vzdálené akce

### <a name="wipe-factory-reset-option-isnt-available-for-work-profile-enrolled-device"></a>Možnost vymazání (obnovení továrního nastavení) není k dispozici pro zařízení zaregistrovaná v pracovním profilu.
Toto chování je očekávané. Ve scénáři pracovního profilu nemá poskytovatel MDM úplnou kontrolu nad zařízením. Jediná dostupná možnost je vyřadit z provozu (odebrat firemní data), která odebere celý pracovní profil a veškerý jeho obsah.

Vymazání je podporované pro [podnikovou firmu v Androidu, která je vlastněná pomocí zařízení s pracovním profilem](android-corporate-owned-work-profile-enroll.md).

### <a name="is-device-passcode-reset-supported"></a>Podporuje se resetování hesla zařízení?
U zaregistrovaných zařízení pracovního profilu můžete resetovat jenom heslo pracovního profilu na zařízeních s Androidem 8,0 a novějším, když:
- heslo k pracovnímu profilu je spravované.
- koncový uživatel ho může resetovat.

Pro vyhrazená zařízení (COSU) a plně spravovaná se podporuje resetování hesla zařízení.


## <a name="next-steps"></a>Další kroky

- [Řešení potíží s registrací zařízení v Intune](troubleshoot-device-enrollment-in-intune.md)
- [Zeptejte se fóra služby Intune](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Podívejte se na blog týmu podpory Microsoft Intune.](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Podívejte se na blog Microsoft Enterprise mobility and Security.](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)