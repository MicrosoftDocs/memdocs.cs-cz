---
title: Řešení potíží s e-mailovými profily v Microsoft Intune – Azure | Microsoft Docs
description: V tématu běžné problémy a řešení se e-mailovými profily v Microsoft Intune, včetně duplicitních e-mailových profilů a chyb na zařízeních se Samsung KNOX standardem.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d011d6111ede4bb5879e53e771d20b792bf00d3
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995122"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Běžné problémy a řešení v e-mailových profilech v Microsoft Intune

Projděte si některé běžné problémy s e-mailovými profily a zjistěte, jak je řešit.

## <a name="users-are-repeatedly-prompted-to-enter-their-password"></a>Uživatelům se opakovaně zobrazí výzva k zadání hesla.

Uživatelům se opakovaně zobrazí výzva k zadání hesla pro e-mailový profil. Pokud se k ověřování a autorizaci uživatele používají certifikáty, Projděte si přiřazení všech profilů certifikátů. Tyto profily certifikátů se obvykle přiřazují skupinám uživatelů, nikoli ke skupinám zařízení. Pokud jeden z profilů certifikátů není zaměřený na uživatele, Intune se znovu pokusí o nasazení e-mailového profilu.

Pokud je tento řetězec e-mailového profilu přiřazen skupinám uživatelů, ujistěte se, že jsou profily certifikátů také přiřazeny skupinám uživatelů.

## <a name="profiles-deployed-to-device-groups-show-errors-and-latency"></a>Profily nasazené do skupin zařízení zobrazují chyby a latenci.

E-mailové profily se obvykle přiřazují skupinám uživatelů. Mohou nastat případy, kdy jsou přiřazeny ke skupinám zařízení.

- Například chcete nasadit e-mailový profil založený na certifikátech jenom na Surface zařízení, ne na stolních počítačích. V tomto scénáři můžou být smysl skupiny zařízení. Víte, že tato zařízení se mohou zobrazovat jako nevyhovující předpisům, může vracet chyby a nemusí okamžitě dostávat e-mailové profily.

  V tomto příkladu vytvoříte e-mailový profil a přiřadíte tento profil ke skupinám zařízení. Zařízení se restartuje a před přihlášením uživatele nastane prodleva. Během této prodlevy se nasadí váš profil certifikátu PKCS, který je přiřazený skupinám uživatelů. Vzhledem k tomu, že zatím není žádný uživatel, profil certifikátu PKCS způsobí, že zařízení nedodržuje předpisy. Prohlížeč událostí může také na zařízení zobrazovat chyby.

  Aby bylo možné získat vyhovující předpisy, uživatel se přihlásí k zařízení a synchronizuje se se službou Intune, aby přijímala zásady. Uživatelé se můžou znovu synchronizovat ručně nebo počkat na další synchronizaci.

- Například používáte dynamické skupiny. Pokud Azure AD okamžitě neaktualizuje dynamické skupiny, pak se tato zařízení můžou zobrazovat jako nekompatibilní.

V těchto scénářích se rozhodujete, jestli je pro používání skupin zařízení důležitější, nebo je důležitější Zobrazit všechny zásady jako vyhovující předpisům.

## <a name="device-already-has-an-email-profile-installed"></a>Zařízení už má nainstalovaný e-mailový profil

Pokud uživatelé vytvoří e-mailový profil před registrací v Intune nebo Microsoft 365 MDM, e-mailový profil nasazený službou Intune nemusí fungovat podle očekávání:

- **iOS/iPadOS**: Intune detekuje stávající duplicitní e-mailový profil na základě názvu hostitele a e-mailové adresy. Uživatelem vytvořený e-mailový profil zablokuje nasazení profilu vytvořeného v Intune. Tento scénář je běžným problémem, protože uživatelé iOS/iPadOS obvykle vytvoří e-mailový profil a potom se zaregistrují. Portál společnosti aplikace uvádí, že uživatel není kompatibilní, a může uživateli požádat o odebrání e-mailového profilu.

  Uživatel by měl odebrat svůj e-mailový profil, aby bylo možné nasadit profil Intune. Pokud chcete tomuto problému zabránit, řekněte uživatelům, aby si zaregistrovali a povolili v Intune nasazení e-mailového profilu. Pak uživatelé můžou vytvořit svůj e-mailový profil.

- **Windows**: Intune detekuje stávající duplicitní e-mailový profil na základě názvu hostitele a e-mailové adresy. Intune přepíše existující e-mailový profil vytvořený uživatelem.

- **Samsung KNOX Standard**: Intune identifikuje duplicitní e-mailový účet na základě e-mailové adresy a přepíše ho profilem Intune. Pokud uživatel tento účet nakonfiguruje, profil Intune ho znovu přepíše. Toto chování může způsobit nejasnost uživatele, jehož konfigurace účtu bude přepsána.

Samsung KNOX nepoužívá k identifikaci profilu název hostitele. Doporučujeme nevytvářet více e-mailových profilů pro nasazení na stejné e-mailové adresy na různých hostitelích, protože se navzájem přepíší.

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>Chyba 0x87D1FDE8 pro zařízení KNOX Standard

**Problém**: po vytvoření a nasazení e-mailového profilu Exchange Active Sync pro Samsung KNOX standard pro různá zařízení s Androidem **se neúspěšná** Chyba **0x87D1FDE8** nebo nápravy zobrazuje na kartě Vlastnosti zařízení > zásady.

Zkontrolujte konfiguraci svého profilu EAS pro zařízení Samsung KNOX a zdroj zásad. Možnost synchronizace poznámek Samsung už není podporovaná a tato možnost by se ve vašem profilu neměla vybrat. Ujistěte se, že zařízení mají dostatek času na zpracování zásady, a to až 24 hodin.

## <a name="unable-to-send-images-from--email-account"></a>Z e-mailového účtu nelze odesílat obrázky

Uživatelé, kteří mají automaticky nastavené e-mailové účty, nemůžou ze svých zařízení odesílat obrázky ani obrázky. K tomuto scénáři může dojít, pokud není povolená **možnost povolit odesílání e-mailů z aplikací třetích stran** .

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**možnost  >  **profily konfigurace**zařízení.
3. Vyberte váš e-mailový profil > **Properties**  >  **Nastavení**vlastností.
4. Nastavte povolení **odesílání e-mailů z aplikací třetích stran** na hodnotu **Povolit**.

## <a name="next-steps"></a>Další kroky

Získejte pomoc [od Microsoftu](../fundamentals/get-support.md)nebo využijte [komunitní fóra](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
