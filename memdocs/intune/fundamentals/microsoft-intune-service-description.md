---
title: Popis služby Microsoft Intune
description: Microsoft Intune je cloudová služba, která pomáhá spravovat zařízení s Windows, iOS/iPadOS, Mac OS X, Androidem a Windows Mobile.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 05/30/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 40fa5a2e-6c0f-4150-9740-d5ddc0cdbda0
ms.reviewer: cacamp
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ca133b1995769f1c4cdfdcaf6b3a8256d7e6d5c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078837"
---
# <a name="microsoft-intune-service-description"></a>Popis služby Microsoft Intune

Intune je cloudová služba pro správu mobility velkých organizací (EMM), která pomáhá tomu, aby vaši pracovníci byli produktivní, a současně chrání vaše firemní data. Intune vám umožňuje:
* Spravovat mobilní zařízení, která vaši pracovníci používají pro přístup k datům společnosti
* Spravovat klientské aplikace používané vašimi pracovníky
* Chránit informace vaší společnosti díky řízení způsobu, jak k nim vaši pracovníci přistupují a jak je sdílejí
* Zajistit, aby zařízení a aplikace splňovaly požadavky společnosti na zabezpečení

Intune se úzce integruje se službou Azure Active Directory (Azure AD) kvůli řízení přístupu a identit a se službou Azure Information Protection kvůli ochraně dat. Můžete ji také integrovat s Configuration Manager, abyste mohli širší možnosti správy.

Další informace o správě zařízení, aplikací a ochraně firemních dat v Intune najdete v [dokumentaci k Intune](../index.yml).

## <a name="30-day-free-trial"></a>30denní bezplatná zkušební verze
Můžete začít používat 30denní bezplatnou zkušební verzi Intune, která zahrnuje 100 uživatelských licencí. Jestli chcete začít používat bezplatnou zkušební verzi, [přejděte na registrační stránku Intune](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20). Jestli má organizace uzavřenou smlouvu Enterprise nebo jinou rovnocennou multilicenční smlouvu, požádejte o nastavení bezplatné zkušební verze zástupce Microsoftu.

> [!NOTE]
> Pokud má vaše organizace pracovní nebo školní účet služeb Microsoft Online Services a po skončení zkušební doby budete chtít toto předplatné Intune používat v produkčním prostředí, vyberte na této stránce možnost **Přihlásit se** a přihlaste se pod účtem globálního správce organizace. Tím zajistíte, že se zkušební verze Intune propojí s vaším stávajícím pracovním nebo školním účtem.

<!--- For a list of settings that you can set up on mobile devices, see:

- [Enrolled device management capabilities of Microsoft Intune](introduction-intune.md)

--->
## <a name="intune-onboarding-benefit"></a>Adaptační benefit Intune
Microsoft nabízí pro Intune adaptační benefity pro příslušné služby v rámci příslušných plánů. Adaptační benefity vám umožní vzdáleně pracovat s odborníky Microsoftu na přípravě vašeho prostředí Intune k použití. Další informace o adaptačních benefitech najdete v tématu [Popis adaptačních benefitů pro Microsoft Intune](https://go.microsoft.com/fwlink/?LinkId=619281).


## <a name="learn-how-intune-service-updates-affect-you"></a>Vysvětlení vlivu aktualizací služby Intune

Ekosystém správy mobilních zařízení se často mění. Důvodem jsou aktualizace operačních systémů a nové verze mobilních aplikací. Proto Microsoft službu Intune pravidelně aktualizuje. Existují tři způsoby, jak se dozvědět o změnách ve službě Intune:

- [Co je nového v Microsoft Intune](whats-new.md). Toto téma se aktualizuje nejen při měsíčních aktualizacích služeb, ale také týdně, například při vydání aplikací, jako je Portál společnosti.

- Důležité aktualizace služby se také oznamují v centru pro [správu Microsoft 365](https://admin.microsoft.com/) centra zpráv. Pokud si nainstalujete doprovodnou [mobilní aplikaci pro správu Office 365](https://support.office.com/article/Office-365-Admin-Mobile-App-e16f6421-2a1a-4142-bf9d-9846600a060a), můžete přijímat oznámení na svém mobilním zařízení. Tady si můžete přečíst, jak pracovat s [centrem zpráv Office 365](https://support.office.com/client/results?Shownav=true&ns=O365ENTADMIN&version=15&ver=15&HelpID=O365E_MCManageUpdates).

  Několik užitečných tipů:

  - Zprávy v centru zpráv Office 365 jsou cílené. To znamená, že pokud vaše společnost nemá nabídku Intune pro EDU, nebudeme vám v Intune pro EDU zprávy.

  - Zprávy mají časově omezenou platnost. Například oznámení o tom, že vaše služba byla aktualizována odkazem na stránku co je nového, pravděpodobně vyprší před dalším oznámením o aktualizaci služby. V opačném případě máte velký počet nevyřízených položek příspěvků, které již nemusí být relevantní.

  - Mobilní aplikace pro správce Office 365 umožňuje prohledávat všechny zprávy a přeposílat oznámení, pokud je chcete sdílet se svými spolupracovníky v organizaci.

  - V části upravit předvolby centra zpráv se vám podíváme na **Intune** , abyste se mohli podívat na tyto zprávy, které se publikují do předplatného Intune. Pokud vidíte Správa mobilních zařízení pro Office 365, jde o jinou službu než Intune.

- Ke sdílení zpráv o Enterprise Mobility + Security (EMS) a osvědčených postupů podpory Intune používáme také dva blogy:

  - [Blog Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/)

  - [Blog podpory Intune](https://blogs.technet.microsoft.com/intunesupport/)

> [!Note]
> Stav služby Intune můžete monitorovat v [centru pro správu Microsoft 365](https://admin.microsoft.com). Zvolte **Stav služby** v levém podokně. K prohlížení stavu služby také můžete použít [mobilní aplikaci Office 365 Admin](https://support.office.com/article/Office-365-Admin-Mobile-App-e16f6421-2a1a-4142-bf9d-9846600a060a).

## <a name="types-of-notices-microsoft-provides-about-the-intune-service"></a>Typy oznámení , které Microsoft poskytuje o službě Intune

Abyste mohli počítat se změnami služby ve svých plánech, upozorníme vás na změny minimálně 7–90 dní předem (podle toho, jaký mají dopad). Typy prováděných změn:

- Změny prostředí pro koncové uživatele, které pravděpodobně budete chtít sdílet s pracovníky helpdesku nebo s koncovými uživateli. Poskytujeme obvykle 7 až 30 dnů oznámení o těchto změnách a zdokumentujte je v [uživatelském rozhraní aplikace Intune, co je nového](whats-new-app-ui.md). V případě nějaké chyby jako pravopisné opravy nebudeme obvykle vyzvat v dokumentaci. Ale změna v uživatelském prostředí pro registraci koncových uživatelů je v uživatelském rozhraní dostatečně významná, takže pošleme zprávu zákazníkům v centru zpráv Office 365 a připojíte se k novinkám v uživatelském rozhraní aplikace Intune, abyste byli informováni o tom, co se mění a které mají čas k vyhodnocení a aktualizaci pokynů pro koncové uživatele předtím, než se změny provedou v produkčním prostředí.

- Změny, které vyžadují váš zásah, se nazývají **Plán na změnu** a obvykle na ně upozorňujeme 30 dní předem. V centru zpráv Office 365 je konkrétní kategorie Plán na změnu. Pokud známe přesné datum provedení změny v produkčním prostředí, uvedeme ho v datu **Jednat do**, abyste měli vizuální vodítko a upozornění.

- U většiny vyřazení posíláme upozornění 90 dní předem. Například pokud už nebudeme podporovat určitou verzi IE, je naším cílem poskytování oznámení 90 dnů. Zastaralosti se ale mají složitou, pokud se jedná o jinou společnost, která oznamuje vyřazení. Například společnost, která vyrábí prohlížeč, oznámí, že v nejnovějším buildu přestane podporovat Silverlight. Proto informujeme zákazníky, že tento prohlížeč přestaneme podporovat, ale oznámíme jim to v kratší době než 90 dní.

- V případě vyřazení služby Intune byste dostali upozornění 12 měsíců předem.

V nečastém případě je v některých případech nějaká akce po incidentu potřebná k tomu, aby se vaše služba vrátila zpět do normálního stavu, nebo velkou změnu, kterou jsme v závislosti na zpětné vazbě na zákazníky mohli rušit, pošleme správcům služby e-mail podle toho, jak jsou nastavené vaše [Předvolby komunikace Office 365](https://support.office.com/article/Change-your-contact-preferences-for-communications-from-Microsoft-6f70de1b-a64d-4498-bfbd-be8c83a9c0fc) a jestli jste zahrnuli platnou (a případně pracovní) e-  


<!--- ## Choose the management solution that's right for you
You can set up Intune in several ways to manage and help protect your company's mobile devices and computers (referred to as **devices** in this article).

- **Intune stand-alone configuration.** Use the web-based admin console in Intune to manage devices in your organization. Intune can be used without any on-premises IT infrastructure. If you use Intune with Active Directory Domain Services, you can use domain user accounts that you manage with Domain Services with Intune.

--->

## <a name="language-support"></a>Podpora jazyků
Intune běží na portálu Azure, který podporuje tyto jazyky: angličtina, čeština, čínština (tradiční), čínština (zjednodušená), francouzština, nizozemština, italština, japonština, korejština, maďarština, němčina, polština, portugalština (Brazílie), portugalština (Portugalsko), ruština, španělština, švédština a turečtina.

Konzola pro správu Intune a mobilní prostředí pro uživatele podporují kromě všech jazyků podporovaných webem Azure Portal také dánštinu, řečtinu, finštinu, norštinu a rumunštinu.

<!--- ## Learn more about Intune
Use these resources to learn more about Intune:

- The [Microsoft Intune Trust Center](https://www.microsoft.com/server-cloud/products/intune-trust-center/) provides information about the security, privacy, and compliance practices of Intune, and it describes some of Intune's certifications.

- [Enrolled device management capabilities of Microsoft Intune](introduction-intune.md)--->
