---
title: Plánování oprávnění šablon certifikátů
titleSuffix: Configuration Manager
description: Seznamte se s plánováním oprávnění, která potřebujete ke konfiguraci šablon certifikátů, které Configuration Manager používá.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 91434b70ca514430ab4cfd6815186bc6d6bc33db
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210124"
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-configuration-manager"></a>Plánování oprávnění šablon certifikátů pro profily certifikátů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


Následující informace vám pomohou při plánování konfigurace oprávnění pro šablony certifikátů, které Configuration Manager používá při nasazování profilů certifikátů.  

## <a name="default-security-permissions-and-considerations"></a>Výchozí oprávnění zabezpečení a pokyny pro nastavení  
 Výchozí oprávnění zabezpečení požadovaná pro šablony certifikátů, které Configuration Manager použijí pro vyžádání certifikátů pro uživatele a zařízení, jsou následující:  

- Číst a Zapsat pro účet, který používá fond aplikací služby zápisu síťových zařízení  

- Přečíst pro účet, který spouští konzolu Configuration Manager  

  Další informace o těchto oprávněních zabezpečení najdete v tématu [Konfigurace infrastruktury certifikátů](../deploy-use/certificate-infrastructure.md).  

  Při použití této výchozí konfigurace nemohou uživatelé a zařízení přímo požadovat certifikáty ze šablon a všechny požadavky musí být iniciovány službou zápisu síťových zařízení. To je důležité omezení, protože šablony certifikátů musí mít nastaven předmět certifikátu na možnost **Dodán v žádosti** , což s sebou nese riziko zosobnění v případě, že o certifikát požádá neautorizovaný uživatel nebo zařízení s ohroženou bezpečností. Ve výchozí konfiguraci musí takový požadavek iniciovat služba zápisu síťových zařízení. Pokud však dojde k ohrožení bezpečnosti služby zápisu síťových zařízení, riziko zosobnění trvá. Chcete-li toto riziko omezit, použijte všechny osvědčené postupy zabezpečení služby zápisu síťových zařízení a počítače, kde je tato služba role spuštěna.  

  Pokud výchozí oprávnění zabezpečení nevyhovují vašim podnikovým požadavkům, existuje další možnost konfigurace oprávnění zabezpečení pro šablony certifikátů: můžete přidat oprávnění Číst a Zapsat pro uživatele a počítače.  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>Přidání oprávnění Číst a Zapsat pro uživatele a počítače  
 Přidání oprávnění číst a zapsat pro uživatele a počítače může být vhodné v případě, že váš tým infrastruktury certifikační autority (CA) spravuje samostatný tým a že chce od sebe Configuration Manager ověřit, že uživatelé mají platný Active Directory Domain Services účet před odesláním profilu certifikátu pro vyžádání certifikátu uživatele. V této konfiguraci musíte zadat jednu nebo více skupin zabezpečení obsahujících uživatele a následně těmto skupinám udělit oprávnění Číst a Zapsat pro šablony certifikátů. Řízení zabezpečení v tomto scénáři zajišťuje správce certifikační autority.  

 Podobně můžete zadat jednu nebo více skupin zabezpečení obsahujících účty počítačů a udělit těmto skupinám oprávnění Číst a Zapsat pro šablony certifikátů. Nasadíte-li profil certifikátu počítače do počítače, který je členem domény, účet tohoto počítače musí mít udělena oprávnění Číst a Zapisovat. Tato oprávnění nejsou vyžadována, pokud počítač není členem domény. Například pokud se jedná o počítač pracovní skupiny nebo osobní mobilní zařízení.  

 I když tato konfigurace používá další prvek zabezpečení, nedoporučujeme ji jako osvědčený postup. Důvodem je, že zadaní uživatelé nebo vlastníci zařízení si mohou vyžádat certifikáty nezávisle na Configuration Manager a zadat hodnoty pro předmět certifikátu, který by se mohl použít k zosobnění jiného uživatele nebo zařízení.  

 Pokud kromě toho zadáte účty, které nelze v době vznesení požadavku na certifikát ověřit, požadavek na certifikát se ve výchozím nastavení nezdaří. Požadavek na certifikát se například nezdaří, pokud se server provozující službu zápisu síťových zařízení nachází v doménové struktuře služby Active Directory, která je ze strany doménové struktury obsahující systémový server lokality bodu registrace certifikátu považována za nedůvěryhodnou. Bod registrace certifikátu můžete nastavit, aby pokračoval, pokud účet nelze ověřit z důvodu nepřítomnosti odpovědi od řadiče domény. Tento postup však z hlediska zabezpečení nepatří mezi osvědčené.  

 Je-li bod registrace certifikátu nastaven, aby kontroloval oprávnění účtu, a dostupný řadič domény požadavek na ověření odmítne (například pokud je účet uzamčen nebo byl odstraněn), požadavek na zápis certifikátu se nezdaří.  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>Kontrola oprávnění Číst a Zapsat pro uživatele a členské počítače domény  

1.  Na serveru systému lokality, který je hostitelem bodu registrace certifikátu, vytvořte následující klíč registru typu DWORD s hodnotou 0: HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  Pokud účet nelze ověřit, protože řadič domény neodpovídá, a pokud chcete obejít kontrolu oprávnění:  

    -   Na serveru systému lokality, který je hostitelem bodu registrace certifikátu, vytvořte následující klíč registru typu DWORD s hodnotou 1: HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  U vydávající certifikační autority na kartě **Zabezpečení** ve vlastnostech šablony certifikátu přidejte jednu nebo více skupin zabezpečení a udělte tak účtům uživatelů nebo zařízení oprávnění Číst a Zapsat.  
