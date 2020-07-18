---
title: Konfigurace plně spravovaných zabezpečení pro Android Enterprise
titleSuffix: Microsoft Intune
description: Přečtěte si o navrhovaných nastaveních pro Android Enterprise plně spravované základní, rozšířené a vysoké zabezpečení.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 01c8c0ffba349966c99e1cbd90dbdfc10a5c9782
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461160"
---
# <a name="android-enterprise-fully-managed-security-configurations"></a>Konfigurace plně spravovaných zabezpečení pro Android Enterprise

V [rámci architektury konfigurace podnikového zabezpečení Androidu](android-configuration-framework.md)použijte následující nastavení pro uživatele s plnou správou Androidu Enterprise. Další informace o jednotlivých nastaveních zásad najdete v tématu [Nastavení vlastníka zařízení s Androidem Enterprise a označení zařízení jako kompatibilních nebo nekompatibilních s použitím nastavení Intune](../protect/compliance-policy-create-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile) a [zařízení s Androidem Enterprise k povolení nebo omezení funkcí v Intune](../configuration/device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile).

Při volbě nastavení nezapomeňte zkontrolovat a zařadit do kategorií scénáře používání. Pak nakonfigurujte uživatele podle pokynů pro zvolenou úroveň zabezpečení. Navrhovaná nastavení můžete upravit podle potřeb vaší organizace. Ujistěte se, že váš tým zabezpečení vyhodnotil hrozbu, riziko později a dopad na použitelnost.

U plně spravovaných zařízení ve vlastnictví firmy existují tři Doporučené architektury konfigurace zabezpečení:

- [Plně spravované základní zabezpečení (úroveň 1)](#fully-managed-basic-security) 
- [Plně spravované rozšířené zabezpečení (úroveň 2)](#fully-managed-enhanced-security)
- [Plně spravované vysoké zabezpečení (úroveň 3)](#fully-managed-high-security) 

## <a name="fully-managed-basic-security"></a>Plně spravované základní zabezpečení

Úroveň 1 je doporučená minimální konfigurace zabezpečení pro mobilní zařízení vlastněná organizací.

Zásady na úrovni 1 vynutily rozumnou úroveň přístupu k datům a současně minimalizují dopad na uživatele. K tomu slouží vynucování zásad pro hesla, minimální verzi operačního systému, ověřování zařízení SafetyNet a zakázání určitých funkcí zařízení (jako jsou přenosy souborů USB). 

### <a name="device-compliance"></a>Dodržování předpisů zařízení

| Sekce | Nastavení | Hodnota | Poznámky |
| ----- | ----- | ----- | ----- |
| Ochrana ATP v programu Microsoft Defender | Vyžadovat, aby zařízení bylo na nebo pod hodnocením rizika počítače | Nenakonfigurováno ||
| Stav zařízení | Vyžadovat, aby zařízení bylo na úrovni hrozby pro zařízení nebo pod ní | Nenakonfigurováno||
| Stav zařízení | Ověření zařízení SafetyNet | Kontrola základní integrity & certifikovaných zařízeních | Toto nastavení konfiguruje ověřování SafetyNet Google na zařízeních koncových uživatelů. Základní integrita ověřuje integritu zařízení. Zařízení s rootem, emulátory, virtuální zařízení a zařízení se znaménkem neoprávněného selhání základní integrity.<br>Základní integrita a certifikovaná zařízení ověřují kompatibilitu zařízení se službami Google. Tuto kontrolu můžou předat jenom nezměněná zařízení, která získala certifikace od společnosti Google. |
| Vlastnosti zařízení | Minimální verze operačního systému | Formát: Hlavní_verze. podverze<br>Příklad: 8,0| Microsoft doporučuje nakonfigurovat minimální hlavní verzi Androidu tak, aby odpovídala podporovaným verzím Androidu pro aplikace Microsoftu. Výrobci OEM a zařízení, kteří dodržují doporučené požadavky na Android Enterprise, musí podporovat aktuální dodací verzi a jeden upgrade na jedno písmeno. V současné době Android doporučuje Android 8,0 a novější pro pracovníky znalostní báze. Nejnovější doporučení pro Android najdete v tématu [Doporučené požadavky pro Android Enterprise](https://www.android.com/enterprise/recommended/requirements/). |
| Vlastnosti zařízení | Maximální verze operačního systému | Nenakonfigurováno ||
| Vlastnosti zařízení | Minimální úroveň opravy zabezpečení | Nenakonfigurováno | Zařízení s Androidem můžou přijímat měsíční opravy zabezpečení, ale tato verze závisí na výrobci OEM nebo nosiči. Organizace musí před implementací tohoto nastavení zajistit, aby nasazená zařízení s Androidem přijímala aktualizace zabezpečení. Nejnovější verze oprav najdete v [bulletinech zabezpečení pro Android](https://source.android.com/security/bulletin/). |
| Zabezpečení systému | Vyžadovat heslo k odemknutí mobilních zařízení | Vyžadovat ||
| Zabezpečení systému | Vyžadovaný typ hesla | Číselné komplexní | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Zabezpečení systému | Minimální délka hesla | 6 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Zabezpečení systému | Maximální počet minut nečinnosti před vyžadováním hesla| 5 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel.|
| Zabezpečení systému | Počet dní do vypršení platnosti hesla| Nenakonfigurováno ||
| Zabezpečení systému |    Počet hesel vyžadovaných před opětovným použitím hesla uživatelem | Nenakonfigurováno ||
| Zabezpečení systému | Šifrování datového úložiště na zařízení | Vyžadovat ||
| Akce při nedodržení předpisů | Označit zařízení jako nevyhovující | Okamžitě | Ve výchozím nastavení je zásada nakonfigurovaná tak, aby zařízení označila jako nevyhovující. K dispozici jsou další akce. Další informace najdete v tématu [Konfigurace akcí pro zařízení nedodržující předpisy v Intune](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Omezení zařízení

| Sekce | Nastavení | Hodnota | Poznámky |
| ----- | ----- | ----- | ----- |
| Obecné | Snímek obrazovky | Nenakonfigurováno ||
| Obecné | Camera | Nenakonfigurováno ||
| Obecné | Výchozí zásady oprávnění | Výchozí nastavení zařízení ||
| Obecné | Změny data a času | Nenakonfigurováno ||
| Obecné | Změny svazku | Nenakonfigurováno ||
| Obecné | Obnovení továrního nastavení | Blok ||
| Obecné | Bezpečné spuštění | Blok ||
| Obecné | Stavový řádek | Nenakonfigurováno ||
| Obecné | Roamingové datové služby | Nenakonfigurováno ||
| Obecné | Změny nastavení sítě Wi-Fi | Nenakonfigurováno ||
| Obecné | Konfigurace Bluetooth | Nenakonfigurováno ||
| Obecné | Sdílení a přístup k hotspotům | Nenakonfigurováno ||
| Obecné | Úložiště USB | Nenakonfigurováno ||
| Obecné | Přenos souborů USB | Blok ||
| Obecné | Externí média | Blok ||
| Obecné | Data ze nosníku pomocí NFC | Nenakonfigurováno ||
| Obecné | Funkce ladění | Nenakonfigurováno ||
| Obecné | Úpravy mikrofonu | Nenakonfigurováno ||
| Obecné | E-maily s ochranou továrního nastavení | Nenakonfigurováno ||
| Obecné | Řídicí šrafování sítě | Nenakonfigurováno ||
| Obecné | Aktualizace systému | Automaticky ||
| Obecné | Okna oznámení | Nenakonfigurováno ||
| Obecné | Přeskočit první tipy k použití | Nenakonfigurováno ||
| Zabezpečení systému | Kontrola ohrožení aplikací |Vyžadovat ||
| Prostředí zařízení | Typ profilu registrace | S plnou správou ||
| Prostředí zařízení | Nastavit jako výchozí spouštěč spouštěč Microsoftu | Nenakonfigurováno | Organizace se můžou rozhodnout implementovat spouštěč Microsoftu, aby se zajistilo konzistentní prostředí pro domácí obrazovku na plně spravovaných zařízeních. Další informace najdete v tématu [jak nastavit spouštěč Microsoftu na zařízeních s plnou správou Androidem Enterprise s Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134) . |
| Heslo | Zakázat zamykací obrazovku | Nenakonfigurováno ||
| Heslo | Zakázané funkce zamykací obrazovky | Vybráno: 0 ||
| Heslo | Vyžadovaný typ hesla | Číselné komplexní ||
| Heslo | Minimální délka hesla | 6 ||
| Heslo | Počet dní do vypršení platnosti hesla | Nenakonfigurováno ||
| Heslo | Počet hesel vyžadovaných před opětovným použitím hesla uživatelem | Nenakonfigurováno ||
| Heslo | Počet neúspěšných přihlášení před vymazáním obsahu zařízení | 10 ||
| Nastavení napájení | Čas k uzamknutí obrazovky | 5 ||
| Nastavení napájení | Obrazovka při napájení zařízení | Nenakonfigurováno ||
| Uživatelé a účty | Přidání nových uživatelů | Nenakonfigurováno ||
| Uživatelé a účty | Odebrání uživatele | Nenakonfigurováno ||
| Uživatelé a účty | Změny účtu (jenom vyhrazená zařízení) | Nenakonfigurováno ||
| Uživatelé a účty | Osobní účty Google | Nenakonfigurováno ||
| Uživatelé a účty | Uživatel může nakonfigurovat přihlašovací údaje. | Blok ||
| Aplikace | Povolení instalace z neznámých zdrojů | Nenakonfigurováno ||
| Aplikace | Povolení přístupu ke všem aplikacím v Google Play Storu | Nenakonfigurováno | Ve výchozím nastavení uživatelé nemůžou instalovat osobní aplikace z Obchod Google Play na plně spravovaná zařízení. Pokud organizace chtějí využívat plně spravovaná zařízení pro osobní použití, zvažte možnost změnit toto nastavení. |
| Aplikace | Automatické aktualizace aplikací | Jenom Wi-Fi | Organizace by toto nastavení měli podle potřeby upravovat, protože poplatky za datové tarify se můžou vyskytnout, když dojde k aktualizaci aplikace přes mobilní síť. |

## <a name="fully-managed-enhanced-security"></a>Plně spravované rozšířené zabezpečení

Úroveň 2 je doporučená konfigurace pro zařízení vlastněná společností, kde uživatelé přistupují k citlivým informacím. Tato zařízení jsou v podnicích v současnosti přirozeného cíle. Tato nastavení nepředpokládají velké zaměstnance vysoce kvalifikovaných bezpečnostních pracovníků. Proto by měly být přístupné většině podnikových organizací. Tato konfigurace se rozšíří na konfiguraci na úrovni 1 tím, že vynutí silnější zásady hesel a zakáže možnosti pro uživatele nebo účet.

Nastavení úrovně 2 zahrnuje všechna nastavení zásad doporučená pro úroveň 1. Níže uvedená nastavení však zahrnují pouze ta nastavení, která byla přidána nebo změněna. Tato nastavení mohou mít mírně vyšší dopad na uživatele nebo na aplikace. Vynutily úroveň zabezpečení, která je lépe vhodná pro rizika směřující uživatelům s přístupem k citlivým informacím na mobilních zařízeních.

### <a name="device-compliance"></a>Dodržování předpisů zařízení

| Sekce | Nastavení | Hodnota | Poznámky |
| ----- | ----- | ----- | ----- |
| Zabezpečení systému | Počet dní do vypršení platnosti hesla | 365 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Zabezpečení systému |    Počet hesel vyžadovaných před opětovným použitím hesla uživatelem | 5 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |

### <a name="device-restrictions"></a>Omezení zařízení

| Sekce | Nastavení | Hodnota | Poznámky |
| ----- | ----- | ----- | ----- |
| Obecné | E-maily s ochranou továrního nastavení | E-mailové adresy účtu Google ||
| Obecné | Seznam e-mailových adres (jenom možnost e-mailových adres účtu Google) | example@gmail.com | Ručně aktualizujte tuto zásadu tak, aby určovala e-mailové adresy Google správců zařízení, které můžou zařízení odemknout po vymazání. |
| Heslo zařízení | Počet dní do vypršení platnosti hesla | 365 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Heslo zařízení | Počet hesel vyžadovaných před opětovným použitím hesla uživatelem | 5 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Heslo zařízení | Počet neúspěšných přihlášení před vymazáním obsahu zařízení | 5 ||
| Uživatelé a účty | Přidání nových uživatelů | Blok ||
| Uživatelé a účty | Odebrání uživatele | Blok ||
| Uživatelé a účty | Osobní účty Google | Blok ||

## <a name="fully-managed-high-security"></a>Plně spravované vysoké zabezpečení

Úroveň 3 představuje doporučenou konfiguraci pro:
- organizace s velkými a sofistikovanými bezpečnostními organizacemi.
- konkrétní uživatele a skupiny, na které bude nežádoucí osoby jednoznačně cílit.
Tyto organizace jsou obvykle zaměřené na dobře financované a sofistikované nežádoucí osoby. Proto představují dodatečná omezení a ovládací prvky uvedené níže.

Tato konfigurace se rozšíří na úrovni 2 o:
- zvýšení minimální verze operačního systému.
- zajištění kompatibility zařízení s vynucováním nejbezpečnější úrovně ochrany před mobilními hrozbami v programu Microsoft Defender.
- zvýšení minimální verze operačního systému.
- vynucování dalších omezení zařízení (například zakázání neredigováných oznámení na zamykací obrazovce).
- vyžadování aplikací, které budou vždy aktuální. 

Nastavení zásad vyžadované v úrovni 3 zahrnují všechna nastavení zásad doporučená pro úroveň 2. Níže uvedená nastavení zahrnují pouze ty, které byly přidány nebo změněny. Tato nastavení mohou mít významný vliv na uživatele nebo aplikace. Vynutily úroveň zabezpečení, která je vhodnější pro rizika směřující k cíleným organizacím.


### <a name="device-compliance"></a>Dodržování předpisů zařízení

| Sekce | Nastavení | Hodnota | Poznámky |
| ----- | ----- | ----- | ----- |
| Ochrana ATP v programu Microsoft Defender | Vyžadovat, aby zařízení bylo na nebo pod hodnocením rizika počítače | Vymazat | Toto nastavení vyžaduje ATP programu Microsoft Defender. Další informace najdete v tématu vymáhání dodržování předpisů pro [Microsoft Defender ATP s podmíněným přístupem v Intune](../protect/advanced-threat-protection.md).<p> Zákazníci by měli zvážit implementaci řešení ochrany před mobilními hrozbami v programu Microsoft Defender. Není nutné nasazovat obojí. |
| Stav zařízení | Vyžadovat, aby zařízení bylo na úrovni hrozby pro zařízení nebo pod ní | Psán | Toto nastavení vyžaduje produkt ochrany před mobilními hrozbami. Další informace najdete v tématu Ochrana před [mobilními hrozbami u zaregistrovaných zařízení](../protect/mtd-device-compliance-policy-create.md).<p>Zákazníci by měli zvážit implementaci řešení ochrany před mobilními hrozbami v programu Microsoft Defender. Není nutné nasazovat obojí.|
| Vlastnosti zařízení | Minimální verze operačního systému | Formát: Hlavní_verze. podverze<br>Příklad: 10,0| Microsoft doporučuje nakonfigurovat minimální hlavní verzi Androidu tak, aby odpovídala podporovaným verzím Androidu pro aplikace Microsoftu. Výrobci OEM a zařízení, kteří dodržují doporučené požadavky na Android Enterprise, musí podporovat aktuální dodací verzi a jeden upgrade na jedno písmeno. V současné době Android doporučuje Android 8,0 a novější pro pracovníky znalostní báze. Nejnovější doporučení pro Android najdete v tématu Doporučené požadavky pro Android Enterprise |

### <a name="device-restrictions"></a>Omezení zařízení

| Sekce | Nastavení | Hodnota | Poznámky |
| ----- | ----- | ----- | ----- |
| Obecné | Změny data a času | Blok ||
| Obecné | Sdílení a přístup k hotspotům | Blok ||
| Obecné | Data ze nosníku pomocí NFC | Blok ||
| Heslo zařízení | Zakázané funkce zamykací obrazovky | Důvěryhodní agenti, neredigováná oznámení ||
| Aplikace | Automatické aktualizace aplikací | Vždy | Organizace by toto nastavení měli podle potřeby upravovat, protože poplatky za datové tarify se můžou vyskytnout, když dojde k aktualizaci aplikace přes mobilní síť. |


## <a name="next-steps"></a>Další kroky

Správci můžou zahrnout výše uvedené úrovně konfigurace v rámci své metodiky nasazení do kroužku pro účely testování a produkčního použití importováním ukázkových [šablon JSON pro konfiguraci Android Enterprise Security Framework](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) pomocí [skriptů PowerShellu pro Intune](https://github.com/microsoftgraph/powershell-intune-samples).
