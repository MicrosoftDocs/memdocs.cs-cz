---
title: Běžné způsoby použití Microsoft Intune
description: Přečtěte si o šesti nejběžnějších úlohách, které vám Microsoft Intune pomůže spravovat.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 11/29/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1f37d4ff-b5a7-4a89-8884-a6184908b09c
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 644235178d39ff1e7c641383c4fb45dde80cf4b5
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531872"
---
# <a name="common-ways-to-use-microsoft-intune"></a>Běžné způsoby použití Microsoft Intune

Než se začnete do úloh implementace, je důležité, aby zúčastněné strany podnikového mobility vaší společnosti byly v souladu s podnikovými cíli používání Intune. Zarovnání účastníků je důležité, ať už nejste v rámci Enterprise mobility nebo migrujete z jiného produktu.  

Potřeby se z hlediska využívání mobilních zařízení v podnikovém prostředí dynamicky vyvíjejí a jejich řešení od Microsoftu se v některých případech může lišit od ostatních řešení na trhu. Nejlepším způsobem, jak zajistit soulad s obchodními cíli, je vyjádřit cíle za pomoci scénářů, které chcete pro svoje zaměstnance, partnery a IT oddělení povolit.  

Níže najdete krátký přehled šesti nejběžnějších scénářů, pro které je zásadní využívání Intune, společně s odkazy na další informace o způsobech plánování a nasazení pro každý z nich.

>[!NOTE]
>Chcete vědět, jak IT oddělení Microsoftu využívá Intune k tomu, aby měli zaměstnanci Microsoftu přístup k podnikovým prostředkům na mobilních zařízeních a současně podniková data zůstala chráněná? [Přečtěte si tuto technickou případovou studii](https://www.microsoft.com/itshowcase/Article/Content/588), kde najdete podrobné informace o tom, jak IT oddělení společnosti Microsoft používá Intune a další služby ke správě identit, zařízení, aplikací a dat.  

>[!IMPORTANT]
>Chceme zajistit, aby mobilní zařízení byla aktuální na základě nedávných malwarových útoků "Trident" na zařízeních s iOS/iPadOS. Proto jsme publikovali blogový příspěvek o [aktualizaci mobilních zařízení pomocí Microsoft Intune](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/26/ensuring-mobile-devices-are-up-to-date-using-microsoft-intune/). Najdete v něm informace o různých způsobech, jak vám může Intune pomoct s tím, aby vaše zařízení byla stále zabezpečená a aktuální.

## <a name="protecting-your-on-premises-email-and-data-so-it-can-be-safely-accessed-by-mobile-devices"></a>Ochrana místních e-mailů a dat, aby je mohli uživatelé bezpečně používat na mobilních zařízeních

Většina strategií z hlediska využívání mobilních zařízení v podnicích začíná plánem zajistit zabezpečený přístup k e-mailům pro zaměstnance s mobilními zařízeními, která se připojují k internetu. Celá řada organizací ještě v dnešní době využívá místní datové a aplikační servery, jako je Microsoft Exchange, které má hostované ve své podnikové síti.

Intune a Microsoft Enterprise Mobility + Security (EMS) poskytují jedinečně integrované [řešení podmíněného přístupu](../protect/conditional-access.md) pro Exchange Server, které zajišťuje, aby k e-mailu nemohlo přistupovat žádná mobilní aplikace, dokud nebude zařízení zaregistrované v Intune. Tento typ přístupu k e-mailu můžete implementovat bez nutnosti nasazovat jiný počítač brány na hranici vaší podnikové sítě.

Intune podporuje také povolení přístupu k mobilním aplikacím, které vyžadují zabezpečený přístup k místním datům, třeba serverům obchodních aplikací. Tento typ přístupu se obvykle zajišťuje pomocí [certifikátů spravovaných službou Intune](../protect/certificates-configure.md) pro řízení přístupu v kombinaci se standardní bránou sítě VPN nebo proxy serverem v hraniční síti, například Microsoft Azure Active Directory Application Proxy.

V takových případech je možné k podnikovým datům získat přístup jedině po zaregistrování zařízení v systému správy. Po zaregistrování zařízení pak systém pro správu zajišťuje, aby zařízení před přístupem k podnikovým datům splňovala vaše zásady. Kromě toho [Nástroj pro zabalení aplikace Intune a sadu App SDK](../developer/apps-prepare-mobile-application-management.md) může pomáhat s tím, aby data v rámci vaší obchodní aplikace mohla předat podniková data, aby je nemohli předat zákaznickým aplikacím nebo službám.

<!-- Learn more about how to plan and deploy Intune to help secure on-premises email and data. -->

## <a name="protecting-your-office-365-email-and-data-so-it-can-be-safely-accessed-by-mobile-devices"></a>Ochrana vašich e-mailů a dat Office 365, aby je mohli uživatelé bezpečně používat na mobilních zařízeních

Ochrana podnikových dat (e-mailů, dokumentů, rychlých zpráv, kontaktů) v Office 365 je navržena tak, abyste ji mohli co nejjednodušeji nastavit a vaše uživatele nijak neomezovala v práci.

Intune a Microsoft Enterprise Mobility + Security poskytují jedinečné integrované řešení podmíněného přístupu, které nesplňuje žádné uživatele, aplikace nebo zařízení k datům Office 365, pokud nesplňují požadavky vaší společnosti na dodržování předpisů (provedlo se [vícefaktorové ověřování](../enrollment/multi-factor-authentication.md), zaregistrované v Intune, s využitím spravované aplikace, podporované verze operačního systému, PIN kód zařízení, profil nízkého uživatelského rizika atd.).

Mobilní aplikace Office v příslušných obchodech s aplikacemi jsou připravené na vynucování zásad zabránění úniku dat, které můžete nakonfigurovat přes Intune. To umožňuje zabránit sdílení dat s aplikacemi (například s nativními e-mailovými aplikacemi) a umístěními úložiště (například Dropbox), která nejsou spravovaná nástrojem. Tato funkce je integrovaná v Office 365 a EMS. Tuto výhodu získáte bez nutnosti nasazovat další infrastrukturu.

Běžnou praxí při nasazování Office 365 je vyžadovat, aby se zařízení registrovala do systému správy, pokud je nutné jejich kompletní nastavení včetně konfigurací podnikových aplikací, certifikátů, Wi-Fi, VPN, což je běžný scénář pro zařízení ve vlastnictví společnosti.  

Pokud ale uživatel potřebuje přístup k firemnímu e-mailu a dokumentům, což často platí pro zařízení v osobním vlastnictví, můžete vyžadovat, aby uživatel používal mobilní aplikace Office (na které jste použili [Zásady ochrany aplikací](../apps/app-protection-policies.md) , a pokud chcete zařízení úplně zaregistrovat, přeskočte.  

V obou případech budou data Office 365 zabezpečená zásadami, které jste definovali.

<!-- Learn more about how to plan and deploy Intune to help secure Office 365 email and data. -->

## <a name="offer-a-bring-your-own-device-program-to-all-employees"></a>Nabídněte všem zaměstnancům využívání programu Přineste si vlastní zařízení (BYOD)

Využívání tohoto přístupu v organizacích se těší čím dál větší oblibě. Je to pro ně způsob, jak omezit výdaje na hardware nebo pro zaměstnance rozšířit možnosti využívání mobilních zařízení. V dnešní době mají už skoro všichni vlastní telefon, proč jim tedy nutit další? Hlavní těžkostí vždy bylo přimět zaměstnance, aby si svoje vlastní zařízení zaregistrovali do systému správy, a to kvůli obavám, co by pak IT oddělení na jejich telefonech mohlo vidět nebo co by s nimi mohlo dělat.  

Jestliže registrace zařízení není vhodným řešením, nabízí Intune alternativní BYOD přístup, v rámci kterého se jednoduše [spravují pouze aplikace obsahující podniková data](../apps/app-protection-policies.md). Intune chrání podniková data i v případě, že daná aplikace přistupuje jak k podnikovým, tak k osobním datům, což je případ mobilních aplikací Office.  

Z pohledu správce můžete vyžadovat, aby uživatelé pro přístup k Office 365 využívali mobilní aplikace Office. Můžete také pro tyto aplikace nakonfigurovat zásady, které umožní zajistit, aby data zůstala chráněná (třeba šifrováním, ochranou pomocí PIN kódu atd.). Tyto zásady ochrany aplikací zabraňují úniku dat z nespravovaných aplikací a úložišť, a to jak v rámci těchto aplikací, tak mimo ně. Zásady například zabrání uživateli ve zkopírování textu z podnikového e-mailového profilu do soukromého e-mailového profilu, a to i v případě, že jsou oba profily nakonfigurované v rámci Outlooku Mobile. Podobné konfigurace můžou být nasazené i pro další služby a aplikace, které vaši uživatelé vyžadují v rámci programu BYOD.

<!-- Learn more about how to plan and deploy Intune to support BYOD.-->

## <a name="issue-corporate-owned-phones-to-your-employees"></a>Poskytnutí podnikových telefonů zaměstnancům

Řada zaměstnanců je v dnešní době mobilní, což s sebou přináší nutnost, aby byli na těchto mobilních zařízeních stejně produktivní. Tito zaměstnanci potřebují snadný přístup ke všem podnikovým aplikacím a datům, a to kdykoli a bez ohledu na to, kde právě jsou. Je potřeba zajistit zabezpečení podnikových dat a udržet nízké náklady na správu.  

Intune nabízí [řešení hromadného zřizování a správy](../enrollment/device-enrollment.md) , která jsou integrovaná s hlavními platformami pro správu firemních zařízení, které jsou dnes na trhu, včetně Apple program registrace zařízení a platformy Samsung KNOX pro zabezpečení mobilních zařízení. Centralizované vytváření konfigurací zařízení prostřednictvím služby Intune pomáhá zřizování podnikových zařízení do značné míry zautomatizovat.  

Představte si tuto situaci: dáte zaměstnanci nerozbalenou krabičku s nových iPhonem. Zaměstnanec iPhone zapne a je proveden kroky nastavení specifickými pro vaši firmu, v rámci kterých se musí ověřit. iPhone se bez problémů nakonfiguruje pomocí [zásad zabezpečení](../configuration/device-profiles.md).

Zaměstnanec pak spustí aplikaci Portál společnosti Intune a přes tu se dostane k volitelným podnikovým aplikacím, které mu společnost zpřístupnila.

<!-- Learn more about how to plan and deploy Intune to support corporate owned devices. -->

## <a name="issue-limited-use-shared-tablets-to-your-employees"></a>Poskytnutí sdílených tabletů s omezeným použitím zaměstnancům

U zaměstnanců je stále rozšířenější používání mobilní technologií. Zaměstnanci v maloobchodech například dnes běžně využívají sdílené tablety.  Ať už se tablety využívají ke zpracování prodeje, nebo k okamžitému zjištění dostupnosti zboží na skladě, umožňují pracovníkům často daleko rychleji reagovat na požadavky zákazníků.

V tomto případě je velmi důležitá jednoduchost uživatelského prostředí. Z tohoto důvodu se tablety většinou poskytují zaměstnancům v režimu omezeného použití, což znamená, že jediná obchodní aplikace je jediná věc, se kterou může zaměstnanec spolupracovat. Intune umožňuje hromadně zřizovat, zabezpečit a centrálně spravovat tato sdílená zařízení s [iOS a Androidem](../configuration/device-profiles.md) , která je možné nakonfigurovat tak, aby běžela v tomto režimu omezeného použití.

<!-- Learn more about how to plan and deploy Intune to support shared tablets. -->

## <a name="enable-your-employees-to-securely-access-office-365-from-an-unmanaged-public-kiosk"></a>Umožnění zabezpečeného přístupu zaměstnanců k Office 365 z nespravované veřejného terminálu

Někdy potřebují vaši zaměstnanci používat zařízení, aplikace nebo prohlížeče, které nemůžete spravovat, jako jsou například veřejné počítače v obchodu a halách Hotel.

Máte z nich zaměstnancům povolit přístup k podnikovému e-mailu? V Intune a Microsoft Enterprise Mobility + Security může odpověď jednoduše "ne" tím, že [omezí přístup k e-mailu na zařízení spravovaná vaší organizací](../protect/conditional-access.md). Tím se zajistí, aby zaměstnanec, který prochází přísným ověřením, nenechal firemní data na nějakém nedůvěryhodném počítači.
