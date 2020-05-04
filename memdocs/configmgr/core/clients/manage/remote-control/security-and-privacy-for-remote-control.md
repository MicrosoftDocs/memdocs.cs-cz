---
title: Ochrana osobních údajů zabezpečení vzdáleného řízení
titleSuffix: Configuration Manager
description: Získejte informace o zabezpečení a ochraně osobních údajů pro vzdálené řízení v Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 83631b331030f9648c3e88a2e101a013cfa0e98f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715099"
---
# <a name="security-and-privacy-for-remote-control-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro vzdálené řízení v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Toto téma obsahuje informace o zabezpečení a ochraně osobních údajů pro vzdálené řízení v Configuration Manager.  

##  <a name="security-best-practices-for-remote-control"></a><a name="BKMK_Security_HardwareInventory"></a> Osvědčené postupy zabezpečení vzdáleného řízení  
 Při správě klientských počítačů prostřednictvím vzdáleného řízení použijte následující osvědčené postupy zabezpečení.  

|Doporučené zabezpečení|Další informace|  
|----------------------------|----------------------|  
|Při připojování ke vzdálenému počítači nepokračujte, pokud se k ověřování používá protokol NTLM a ne Kerberos.|Pokud Configuration Manager zjistí, že relace vzdáleného řízení je ověřena pomocí protokolu NTLM namísto protokolu Kerberos, zobrazí se výzva upozorňující na to, že nelze ověřit identitu vzdáleného počítače. Nepokračujte v relaci vzdáleného řízení. NTLM je slabší ověřovací protokol než Kerberos a může být zranitelný vůči opakování a zosobnění.|  
|Nepovolujte sdílení schránky v prohlížeči vzdáleného řízení.|Schránka podporuje objekty, jako například spustitelné soubory a text a může být uživatelem v hostitelském počítači během relace vzdáleného řízení využita ke spuštění programu ve zdrojovém počítači.|  
|Nezadávejte hesla k privilegovaným účtům při vzdáleném řízení počítače.|Heslo by mohl zachytit software, který zaznamenává vstup z klávesnice. Nebo, pokud program, který je spuštěn v klientském počítači není tím programem, který uživatel funkce vzdáleného řízení očekává, může být heslo také vyzrazeno. Pokud jsou požadované účty a hesla, měli by je zadávat koncoví uživatelé.|  
|Během relace vzdáleného řízení zamkněte klávesnici a myš.|Pokud Configuration Manager zjistí, že bylo připojení vzdáleného řízení ukončeno, Configuration Manager automaticky uzamkne klávesnici a myš, aby uživatel nemohl převzít kontrolu nad otevřenou relací vzdáleného řízení. Toto rozpoznání ale nemusí být okamžité a také nejde rozpoznat ukončení služby vzdáleného řízení na druhé straně.<br /><br /> Vyberte akci **Zamknout vzdálenou klávesnici a myš** v okně **Vzdálené řízení ConfigMgr** .|  
|Nenechte uživatelům možnost konfigurovat nastavení vzdáleného řízení v Centru softwaru.|Nepovolujte nastavení klienta **V Centru softwaru mohou uživatelé změnit zásady nebo nastavení oznamování** , pomůžete tak uživatelům v obraně proti špehování. Pokud ho jeden uživatel změní, může to způsobit, že se na stejném počítači bude vzdáleně zobrazovat jiný uživatel. <br /><br />**Toto nastavení platí pro počítač, nikoli pro přihlášeného uživatele**.|  
|Povolte profil **Doména** brány Windows Firewall.|Povolte nastavení klienta **Povolit vzdálené řízení v profilech výjimky brány firewall u klientů** a pak vyberte **Doména** brány Windows Firewall pro počítače v síti intranet.|  
|Když se odhlásíte během relace vzdáleného řízení a přihlásíte se jako jiný uživatel, nezapomeňte se před odpojením relace vzdáleného řízení odhlásit.|Když to neuděláte, relace zůstane otevřená.|  
|Neudělujte uživatelům oprávnění místního správce.|Pokud uživatelům udělíte oprávnění místního správce, budou moci převzít vaší relaci vzdáleného řízení nebo odhalit přihlašovací údaje.|  
|Pro konfiguraci nastavení vzdálené pomoci použijte buď Zásady skupiny, nebo Configuration Manager, ale ne obojí.|Pomocí Configuration Manager a Zásady skupiny můžete provádět změny konfigurace v nastavení vzdálené pomoci. Při aktualizaci zásad skupiny na straně klienta se ve výchozím nastavení proces optimalizuje tím, že se změní jenom ty zásady, které byly změněné na serveru. Configuration Manager změní nastavení v místních zásadách zabezpečení, které se nemusí přepsat, pokud není Vynucená aktualizace Zásady skupiny.<br /><br /> Nastavení zásad na obou místech může vést k nekonzistentním výsledkům. Vyberte jednu z těchto metod konfigurace nastavení vzdálené pomoci.|  
|Povolte nastavení klienta **Zobrazit výzvu uživateli pro oprávnění ke Vzdálenému řízení**.|I když existují způsoby, jak toto nastavení obejít a výzvu nezobrazit, povolení tohoto nastavení může snížit pravděpodobnost, že budou uživatelé špehovaní při práci s důvěrnými informacemi.<br /><br /> Kromě toho upozorněte uživatele, že je dobrým zvykem zkontrolovat název účtu, který se zobrazí během relace vzdáleného řízení a odpojit relaci, pokud budou mít podezření, že nejde o oprávněný účet.|  
|Omezte seznam povolených prohlížečů.|Uživatelé nepotřebují k používání vzdáleného řízení oprávnění místního správce.|  

### <a name="security-issues-for-remote-control"></a>Otázky zabezpečení vzdáleného řízení  
 Při správě klientských počítačů pomocí vzdáleného řízení vznikají následující otázky související se zabezpečením:  

-   Nepovažujte zprávy auditu vzdáleného řízení za spolehlivé.  

     Když zahájíte relaci vzdáleného řízení a pak se přihlaste s použitím jiných přihlašovacích údajů, bude zprávy o auditu odesílat původní účet, nikoli účet s novými přihlašovacími údaji.  

     Zprávy o auditu se neodesílají, pokud zkopírujete binární soubory pro vzdálené řízení místo instalace konzoly Configuration Manager a pak na příkazovém řádku spustíte vzdálené řízení.  

##  <a name="privacy-information-for-remote-control"></a><a name="BKMK_Privacy_HardwareInventory"></a> Osobní údaje při vzdáleném řízení  
 Vzdálené řízení umožňuje zobrazit aktivní relace na Configuration Manager klientských počítačích a potenciálně prohlížet jakékoli informace uložené v těchto počítačích. Ve výchozím nastavení není vzdálené řízení povolené.  

 Přestože můžete nakonfigurovat vzdálené řízení tak, aby poskytovalo výrazné upozornění a vyžadovat souhlas uživatele se zahájením relace, umožňuje také monitorování uživatelů bez jejich souhlasu nebo vědomí. Můžete nakonfigurovat úroveň přístupu Jenom zobrazení, která neumožňuje provádět na vzdáleném počítači žádné změny, nebo Úplné řízení. Účet připojujícího se správce je zobrazený v relaci vzdáleného řízení, což uživatelům pomáhá identifikovat, kdo se k jejich počítači připojuje.  

 Ve výchozím nastavení Configuration Manager udělí místní skupině Administrators oprávnění ke vzdálenému řízení.  

 Před konfigurací vzdáleného řízení zvažte vaše požadavky na ochranu osobních údajů.  
