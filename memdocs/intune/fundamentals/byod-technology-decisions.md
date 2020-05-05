---
title: Rozhodnutí o technologiích pro používání vlastních zařízení uživatelů (BYOD) pomocí řešení EMS
description: Klíčová rozhodnutí o technologiích, která umožní používání vlastních zařízení uživatelů (BYOD) a ochranu firemních dat, pomocí řešení Microsoft Enterprise Mobility + Security
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 12/8/2017
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 297926f6-c029-4003-bda4-9ee031d47dda
ms.reviewer: pfetty
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: f5d0e809e834a82f192128263742bc2b9b0024a2
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079276"
---
# <a name="technology-decisions-for-enabling-byod-with-microsoft-enterprise-mobility--security-ems"></a>Rozhodnutí o technologiích, která umožní používání vlastních zařízení uživatelů (BYOD), pomocí řešení Microsoft Enterprise Mobility + Security (EMS)

Při vývoji strategie umožňující vzdálenou práci zaměstnanců na vlastních zařízeních (BYOD) je potřeba udělat ve scénářích klíčová rozhodnutí, která umožní používání vlastních zařízení uživatelů a určí způsob ochrany firemních dat. Řešení EMS naštěstí nabízí všechny potřebné funkce jako komplexní sadu řešení.  

V tomto tématu prozkoumáme jednoduchý případ použití, ve kterém se povoluje přístup pomocí vlastních zařízení uživatelů k podnikovému e-mailu. Zaměřte se na to, jestli potřebujete spravovat celé zařízení, nebo jenom aplikace, z nichž obě jsou zcela platné volby.

## <a name="assumptions"></a>Předpoklady
* Máte základní znalosti o Azure Active Directory a Microsoft Intune.
* Vaše e-mailové účty jsou hostované v Exchangi Online.

## <a name="common-reasons-to-manage-the-device-mdm"></a>Běžné situace, při kterých se provádí správa zařízení (MDM)
Nasazením zásad [podmíněného přístupu](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) na Exchangi Online můžete snadno řídit uživatelům registraci svých zařízení do správy zařízení. Toto jsou situace, kdy je vhodné spravovat osobní zařízení:

**WiFi/VPN** – Pokud uživatelé potřebují k produktivní práci podnikový profil připojení, je možné ho bezproblémově nakonfigurovat.

**Aplikace** – Pokud uživatelé potřebují do svého zařízení bez vyžádání stáhnout sadu aplikací, je možné je bezproblémově doručit. To zahrnuje i aplikace, které se můžou vyžadovat pro účely zabezpečení, jako je například aplikace pro ochranu před mobilními hrozbami.

**Dodržování předpisů** – Některé organizace musí dodržovat zákonné nebo jiné předpisy, které vyžadují specifické prvky MDM. MDM je například potřeba k šifrování celého zařízení nebo k vytvoření sestavy obsahující všechny aplikace na zařízení.

## <a name="common-reasons-to-only-manage-the-apps-mam"></a>Běžné situace, při kterých se provádí jenom správa aplikací (MAM)
Používání MAM bez MDM je velmi rozšířené v organizacích, které podporují vlastní zařízení uživatelů. Můžete řídit uživatelům přístup k e-mailu z Outlooku Mobile (který podporuje ochrany MAM) nasazením zásad podmíněného přístupu na Exchangi Online. Toto jsou situace, kdy je vhodné spravovat jenom aplikace na osobních zařízeních:

**Uživatelské prostředí** – Součástí registrace MDM je řada výzev s upozorněními (vynucovaných příslušnou platformou), které často mají za následek to, že se uživatel nakonec rozhodne nepřistupovat k e-mailu na svém osobním zařízení. Prostředí MAM není pro uživatele tak znepokojující, protože se jim zobrazí jenom jedno automaticky otevírané okno s oznámením, že se používá ochrana MAM.

**Dodržování předpisů** – Některé organizace musí dodržovat předpisy, které vyžadují, aby na osobních zařízeních bylo méně funkcí pro správu. MAM například umožňuje odebrat firemní data jenom z aplikací, na rozdíl od správy MDM, která umožňuje odebrat všechna data ze zařízení.

![Obrázek s porovnáním správy zařízení a aplikací na mobilních zařízeních](./media/byod-technology-decisions/byod-app-device-mgmt.png)

Přečtěte si další informace o [životních cyklech správy zařízení a aplikací](device-lifecycle.md).

## <a name="mdm-vs-mam-capability-comparison"></a>Porovnání funkcí MDM a MAM
Jak už bylo zmíněno, podmíněný přístup může uživateli řídit registraci svého zařízení nebo použít spravovanou aplikaci, jako je Outlook Mobile. V obou případech lze použít řadu dalších podmínek, například:

* Uživatel, který se pokouší o přístup
* Důvěryhodnost nebo nedůvěryhodnost umístění
* Úroveň rizika přihlášení
* Platforma zařízení

Přesto mnoho organizací má často specifická rizika, o kterých se zajímá.  Následující tabulka obsahuje běžné problémy a reakce MDM a MAM na tyto problémy.

| Problém   |   MDM  |   MAM  |
|------------|--------|--------|
|Neoprávněný přístup k datům | Vyžadování členství ve skupině | Vyžadování členství ve skupině |
|Neoprávněný přístup k datům | Vyžadování registrace zařízení | Vyžadování chráněné aplikace |
|Neoprávněný přístup k datům | Vyžadování konkrétního umístění | Vyžadování konkrétního umístění |
| | | |
|Ohrožení bezpečnosti uživatelského účtu| Vyžadování MFA | Vyžadování MFA|
|Ohrožení bezpečnosti uživatelského účtu | Blokování uživatelů s vysokým rizikem | Blokování uživatelů s vysokým rizikem |
|Ohrožení bezpečnosti uživatelského účtu | PIN kód zařízení | PIN kód aplikace |
| | | |
| Ohrožení bezpečnosti zařízení nebo aplikace | Vyžadování kompatibilního zařízení | Detekce jailbreaku při spuštění aplikace |
| Ohrožení bezpečnosti zařízení nebo aplikace | Zašifrování dat na zařízení | Zašifrovat data aplikací |
| | | |
|Ztráta nebo odcizení zařízení | Odebrání všech dat na zařízení | Odebrání všech dat aplikací|
| | | |
| Nechtěné sdílení dat nebo uložení do nezabezpečených umístění | Zakázání zálohování dat na zařízení | Zakázání funkcí Vyjmout, Kopírovat a Vložit|
| Nechtěné sdílení dat nebo uložení do nezabezpečených umístění | Zakázání funkce Uložit jako | Zakázání funkce Uložit jako |
|Nechtěné sdílení dat nebo uložení do nezabezpečených umístění | Zakázat tisk | neuvedeno|

## <a name="next-steps"></a>Další kroky
Teď je čas rozhodnout, jestli ve vaší organizaci chcete povolit BYOD, a to tak, že se zaměříte na správu zařízení, správu aplikací nebo kombinaci těchto dvou. Volba implementace je na vás, ale bez ohledu na zvolenou možnost máte jistotu, že budete mít k dispozici funkce pro práci s identitami a funkce zabezpečení, které jsou dostupné v Azure AD.  

K navržení další úrovně plánování použijte [průvodce plánováním](planning-guide.md) Intune.
