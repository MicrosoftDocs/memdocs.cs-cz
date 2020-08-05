---
title: Pracovní profil konfigurace pro Android Enterprise
titleSuffix: Microsoft Intune
description: Přečtěte si o omezeních a nastaveních navrhovaných pro základní a vysoké zabezpečení zařízení s Androidem Enterprise.
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
ms.openlocfilehash: 4283caf8f21e87736b09a3d6c7b31f8daf1f6075
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546822"
---
# <a name="android-enterprise-work-profile-security-configurations"></a>Konfigurace zabezpečení pracovního profilu Android Enterprise

V [rámci architektury konfigurace podnikového zabezpečení Androidu](android-configuration-framework.md)použijte následující nastavení pro mobilní uživatele pracovní profil Androidu Enterprise. Další informace o jednotlivých nastaveních zásad najdete v tématu [nastavení pro Android Enterprise a označení zařízení jako kompatibilních nebo nekompatibilních s použitím nastavení zařízení Intune](../protect/compliance-policy-create-android-for-work.md#work-profile) a [Android Enterprise k povolení nebo omezení funkcí v Intune](../configuration/device-restrictions-android-for-work.md#work-profile-only).

Při volbě nastavení nezapomeňte zkontrolovat a zařadit do kategorií scénáře používání. Pak nakonfigurujte uživatele podle pokynů pro zvolenou úroveň zabezpečení. Navrhovaná nastavení můžete upravit podle potřeb vaší organizace. Ujistěte se, že váš tým zabezpečení vyhodnotil hrozbu, riziko později a dopad na použitelnost.

Pro zařízení pracovních profilů vlastněných osobně jsou k dispozici dvě architektury konfigurace zabezpečení:

- [Základní zabezpečení pracovního profilu (úroveň 1)](#work-profile-basic-security) 
- [Vysoké zabezpečení pracovního profilu (úroveň 3)](#work-profile-high-security) 

> [!Note]
> Vzhledem k tomu, že jsou dostupná nastavení pro zařízení s Androidem Enterprise Work Profile, neexistuje žádná nabídka Rozšířené zabezpečení (úroveň 2). Dostupná nastavení neopravňují k rozdílu mezi úrovní 1 a úrovní 2.

## <a name="work-profile-basic-security"></a>Základní zabezpečení pracovního profilu

Úroveň 1 je doporučená minimální konfigurace zabezpečení pro osobní zařízení, kde uživatelé přistupují k pracovním nebo školním datům. Tato konfigurace se může vztahovat na většinu mobilních uživatelů. Některé ovládací prvky mohou ovlivnit činnost koncového uživatele.

### <a name="device-compliance"></a>Dodržování předpisů zařízení

| Sekce | Nastavení | Hodnota | Poznámky |
| ----- | ----- | ----- | ----- |
| Ochrana ATP v programu Microsoft Defender | Vyžadovat, aby zařízení bylo na nebo pod hodnocením rizika počítače | Nenakonfigurováno ||
| Stav zařízení | Zařízení s rootem | Blok ||
| Stav zařízení | Vyžadovat, aby zařízení bylo na úrovni hrozby pro zařízení nebo pod ní | Nenakonfigurováno||
| Stav zařízení | Aplikace Služby Google Play je nakonfigurovaná | Vyžadovat ||
| Stav zařízení | Aktualizovaný poskytovatel zabezpečení | Vyžadovat ||
| Stav zařízení | Ověření zařízení SafetyNet | Kontrola základní integrity & certifikovaných zařízeních | Toto nastavení konfiguruje ověřování SafetyNet Google na zařízeních koncových uživatelů. Základní integrita ověřuje integritu zařízení. Zařízení s rootem, emulátory, virtuální zařízení a zařízení se znaménkem neoprávněného selhání základní integrity.<p>Základní integrita a certifikovaná zařízení ověřují kompatibilitu zařízení se službami Google. Tuto kontrolu můžou předat jenom nezměněná zařízení, která získala certifikace od společnosti Google. |
| Vlastnosti zařízení | Minimální verze operačního systému | Formát: Hlavní_verze. podverze<br>Příklad: 5,0| Microsoft doporučuje nakonfigurovat minimální hlavní verzi Androidu tak, aby odpovídala podporovaným verzím Androidu pro aplikace Microsoftu. Výrobci OEM a zařízení, kteří dodržují doporučené požadavky na Android Enterprise, musí podporovat aktuální dodací verzi a jeden upgrade na jedno písmeno. V současné době Android doporučuje Android 8,0 a novější pro pracovníky znalostní báze. Nejnovější doporučení pro Android najdete v tématu [Doporučené požadavky pro Android Enterprise](https://www.android.com/enterprise/recommended/requirements/). |
| Vlastnosti zařízení | Maximální verze operačního systému | Nenakonfigurováno ||
| Zabezpečení systému | Vyžadovat heslo k odemknutí mobilních zařízení | Vyžadovat ||
| Zabezpečení systému | Vyžadovaný typ hesla | Číselné komplexní | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Zabezpečení systému | Minimální délka hesla | 6 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Zabezpečení systému | Maximální počet minut nečinnosti před vyžadováním hesla| 5 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel.|
| Zabezpečení systému | Počet dní do vypršení platnosti hesla| Nenakonfigurováno | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Zabezpečení systému | Počet předchozích hesel, která se zabrání použití | Nenakonfigurováno | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Zabezpečení systému | Šifrování datového úložiště na zařízení | Vyžadovat ||
| Zabezpečení systému | Blokovat aplikace z neznámých zdrojů | Blok ||
| Zabezpečení systému | Portál společnosti integrita modulu runtime aplikace | Vyžadovat ||
| Zabezpečení systému | Blokovat na zařízení ladění USB | Blok | I když toto nastavení blokuje ladění pomocí zařízení USB, také zakáže schopnost shromažďovat protokoly, které mohou být užitečné při řešení potíží. |
| Zabezpečení systému | Minimální úroveň opravy zabezpečení | Nenakonfigurováno | Zařízení s Androidem můžou přijímat měsíční opravy zabezpečení, ale tato verze závisí na výrobci OEM nebo nosiči. Organizace musí před implementací tohoto nastavení zajistit, aby nasazená zařízení s Androidem přijímala aktualizace zabezpečení. Nejnovější verze oprav najdete v [bulletinech zabezpečení pro Android](https://source.android.com/security/bulletin/). |
| Akce při nedodržení předpisů | Označit zařízení jako nevyhovující | Okamžitě | Ve výchozím nastavení je zásada nakonfigurovaná tak, aby zařízení označila jako nevyhovující. K dispozici jsou další akce. Další informace najdete v tématu [Konfigurace akcí pro zařízení nedodržující předpisy v Intune](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Omezení zařízení

| Sekce | Nastavení | Hodnota | Poznámky |
| ----- | ----- | ----- | ----- |
| Nastavení pracovního profilu | Kopírování a vkládání mezi pracovními a osobními profily | Blok ||
| Nastavení pracovního profilu | Sdílení dat mezi pracovními a osobními profily | Aplikace v pracovním profilu můžou zpracovat žádost o sdílení z osobního profilu ||
| Nastavení pracovního profilu | Oznámení z pracovního profilu, když je zařízení uzamčené | Nenakonfigurováno | Blokování tohoto nastavení zajistí, že citlivá data nebudou vystavena v oznámeních pracovních profilů, která mohou mít dopad na použitelnost. |
| Nastavení pracovního profilu | Výchozí oprávnění aplikace | Výchozí nastavení zařízení | Správci musí kontrolovat a upravovat oprávnění udělená aplikacemi, které nasazují. |
| Nastavení pracovního profilu | Přidat nebo odebrat účty | Blok ||
| Nastavení pracovního profilu | Sdílení kontaktů přes Bluetooth | Povolit | Ve výchozím nastavení není přístup k pracovním kontaktům k dispozici na jiných zařízeních, jako jsou Automobiles přes integraci Bluetooth. Povolením tohoto nastavení dojde k lepšímu používání bezplatného uživatelského prostředí. Zařízení Bluetooth ale může kontakty při prvním připojení Uložit do mezipaměti. Organizace by měly zvážit vyrovnávání scénářů použitelnosti s aspekty ochrany dat při implementaci tohoto nastavení. |
| Nastavení pracovního profilu | Snímek obrazovky | Blok ||
| Nastavení pracovního profilu | Zobrazit v osobním profilu ID volajícího pracovního kontaktu | Nenakonfigurováno ||
| Nastavení pracovního profilu | Hledat pracovní kontakty z osobního profilu | Nenakonfigurováno | Blokování přístupu uživatelů k pracovním kontaktům z osobního profilu může mít vliv na určité scénáře použitelnosti, jako je textové zasílání zpráv a prostředí vytáčení v rámci osobního profilu. Organizace by měly zvážit vyrovnávání scénářů použitelnosti s aspekty ochrany dat při implementaci tohoto nastavení. |
| Nastavení pracovního profilu | Camera | Nenakonfigurováno ||
| Nastavení pracovního profilu | Povoluje widgety z pracovních profilů aplikací. | Povolit ||
| Nastavení pracovního profilu | Vyžadovat heslo pracovního profilu | Vyžadovat ||
| Nastavení pracovního profilu | Minimální délka hesla | 6 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Nastavení pracovního profilu | Maximální počet minut nečinnosti, po kterém se zamkne pracovní profil| 5 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Nastavení pracovního profilu | Počet neúspěšných přihlášení před vymazáním pracovního profilu| 10 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Nastavení pracovního profilu | Omezená platnost hesla (ve dnech) | Nenakonfigurováno | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Nastavení pracovního profilu | Vyžadovaný typ hesla | Číselné komplexní ||
| Nastavení pracovního profilu | Zakázat opakované použití předchozích hesel | Nenakonfigurováno | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel.|
| Nastavení pracovního profilu | Odemknutí pomocí otisků prstů | Nenakonfigurováno ||
| Nastavení pracovního profilu | Smart Lock a jiní agenti pro určování důvěryhodnosti | Nenakonfigurováno |||
| Heslo zařízení | Minimální délka hesla | 6 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Heslo zařízení | Maximální počet minut nečinnosti, po které se zamkne obrazovka | 5 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Heslo zařízení | Počet neúspěšných přihlášení před vymazáním obsahu zařízení | 10 | Toto nastavení aktivuje vymazání pracovního profilu a nejedná se o vymazání zařízení. |
| Heslo zařízení | Omezená platnost hesla (ve dnech) | Nenakonfigurováno | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Heslo zařízení | Vyžadovaný typ hesla | Číselné komplexní ||
| Heslo zařízení | Zakázat opakované použití předchozích hesel | Nenakonfigurováno | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Heslo zařízení | Odemknutí pomocí otisků prstů | Nenakonfigurováno ||
| Heslo zařízení | Smart Lock a jiní agenti pro určování důvěryhodnosti | Nenakonfigurováno ||
| Zabezpečení systému | Kontrola ohrožení aplikací | Vyžadovat | Toto nastavení zajistí, aby byla pro zařízení koncových uživatelů zapnutá kontrola aplikací pro ověřování Google. V případě konfigurace bude koncový uživatel zablokován přístup, dokud nezapnete kontrolu aplikací Google na svém zařízení s Androidem. |
| Zabezpečení systému | Zabránit instalaci aplikací z neznámých zdrojů v osobním profilu | Blok ||

> [!Note]
> Když je povolený podnikový pracovní profil v Androidu, ve výchozím nastavení se nakonfiguruje "jeden zámek", aby bylo možné kombinovat hesla pro zařízení a pracovní profil. V případě potřeby může být v části Nastavení pracovního profilu v případě potřeby zakázaný jeden zámek pro samostatné pracovní profily a hesla zařízení.

## <a name="work-profile-high-security"></a>Vysoké zabezpečení pracovního profilu

Úroveň 3 je doporučená konfigurace pro zařízení používaná uživateli nebo skupinami, které mají jednoznačně vysoké riziko. Například uživatelé, kteří zpracovávají vysoce citlivá data v případě neoprávněného odhalení, způsobují značnou ztrátu materiálu. Organizace, na kterou je pravděpodobně cílena dobře financovaná a propracovaná nežádoucí osoby, by měla obsahovat další omezení popsaná níže. Tato konfigurace se rozšíří na konfiguraci na úrovni 1 o:
- implementace ochrany před mobilními hrozbami nebo ATP v programu Microsoft Defender.
- omezení scénářů dat pracovního profilu.
- vynutí se silnější zásady hesel.

Nastavení zásad vyžadované v úrovni 3 zahrnují všechna nastavení zásad doporučená pro úroveň 1. Níže uvedená nastavení však zahrnují pouze ty, které byly přidány nebo změněny. Tato nastavení mohou mít mírně vyšší dopad na uživatele nebo aplikace. Vynutily úroveň zabezpečení, která je lépe vhodná pro rizika směřující uživatelům s přístupem k citlivým informacím na mobilních zařízeních.

### <a name="device-compliance"></a>Dodržování předpisů zařízení

| Sekce | Nastavení | Hodnota | Poznámky |
| ----- | ----- | ----- | ----- |
| Ochrana ATP v programu Microsoft Defender | Vyžadovat, aby zařízení bylo na nebo pod hodnocením rizika počítače | Vymazat | Toto nastavení vyžaduje ATP programu Microsoft Defender. Další informace najdete v tématu vymáhání dodržování předpisů pro [Microsoft Defender ATP s podmíněným přístupem v Intune](../protect/advanced-threat-protection.md).<p>Zákazníci by měli zvážit implementaci řešení ochrany před mobilními hrozbami v programu Microsoft Defender. Není nutné nasazovat obojí. |
| Stav zařízení | Vyžadovat, aby zařízení bylo na úrovni hrozby pro zařízení nebo pod ní | Psán | Toto nastavení vyžaduje produkt ochrany před mobilními hrozbami. Další informace najdete v tématu Ochrana před [mobilními hrozbami u zaregistrovaných zařízení](../protect/mtd-device-compliance-policy-create.md).<p>Zákazníci by měli zvážit implementaci řešení ochrany před mobilními hrozbami v programu Microsoft Defender. Není nutné nasazovat obojí.|
| Vlastnosti zařízení | Minimální verze operačního systému | Formát: Hlavní_verze. podverze<br>Příklad: 8,0| Microsoft doporučuje nakonfigurovat minimální hlavní verzi Androidu tak, aby odpovídala podporovaným verzím Androidu pro aplikace Microsoftu. Výrobci OEM a zařízení, kteří dodržují doporučené požadavky na Android Enterprise, musí podporovat aktuální dodací verzi a jeden upgrade na jedno písmeno. V současné době Android doporučuje Android 8,0 a novější pro pracovníky znalostní báze. Nejnovější doporučení pro Android najdete v tématu Doporučené požadavky pro Android Enterprise |
| Zabezpečení systému | Počet dní do vypršení platnosti hesla | 365 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Zabezpečení systému | Počet předchozích hesel, která se zabrání použití | 5 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |


### <a name="device-restrictions"></a>Omezení zařízení

| Sekce | Nastavení | Hodnota | Poznámky |
| ----- | ----- | ----- | ----- |
| Nastavení pracovního profilu | Oznámení z pracovního profilu, když je zařízení uzamčené | Blok | Blokování tohoto nastavení zajistí, že citlivá data nebudou vystavena v oznámeních pracovních profilů, která mohou mít dopad na použitelnost. |
| Nastavení pracovního profilu | Sdílení kontaktů přes Bluetooth | Nenakonfigurováno | Ve výchozím nastavení není přístup k pracovním kontaktům k dispozici na jiných zařízeních, jako jsou Automobiles přes integraci Bluetooth. Povolením tohoto nastavení dojde k lepšímu používání bezplatného uživatelského prostředí. Zařízení Bluetooth ale může kontakty při prvním připojení Uložit do mezipaměti. Organizace by měly zvážit vyrovnávání scénářů použitelnosti s aspekty ochrany dat při implementaci tohoto nastavení. |
| Nastavení pracovního profilu | Hledat pracovní kontakty z osobního profilu | Blok | Blokování přístupu uživatelů k pracovním kontaktům z osobního profilu může mít vliv na určité scénáře použitelnosti, jako je textové zasílání zpráv a prostředí vytáčení v rámci osobního profilu. Organizace by měly zvážit vyrovnávání scénářů použitelnosti s aspekty ochrany dat při implementaci tohoto nastavení. |
| Nastavení pracovního profilu | Povoluje widgety z pracovních profilů aplikací. | Nenakonfigurováno ||
| Nastavení pracovního profilu | Počet neúspěšných přihlášení před vymazáním pracovního profilu | 5 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Nastavení pracovního profilu | Omezená platnost hesla (ve dnech) | 365 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Nastavení pracovního profilu | Zakázat opakované použití předchozích hesel | 5 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Nastavení pracovního profilu | Smart Lock a jiní agenti pro určování důvěryhodnosti | Blok ||
| Heslo zařízení | Počet neúspěšných přihlášení před vymazáním obsahu zařízení | 5 | Toto nastavení aktivuje vymazání pracovního profilu a nejedná se o vymazání zařízení. |
| Heslo zařízení | Omezená platnost hesla (ve dnech) | 365 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |
| Heslo zařízení | Zakázat opakované použití předchozích hesel | 5 | Organizace možná budou muset aktualizovat toto nastavení tak, aby odpovídalo zásadám hesel. |

## <a name="next-steps"></a>Další kroky

Správci můžou zahrnout výše uvedené úrovně konfigurace v rámci své metodiky nasazení do kroužku pro účely testování a produkčního použití importováním ukázkových [šablon JSON pro konfiguraci Android Enterprise Security Framework](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) pomocí [skriptů PowerShellu pro Intune](https://github.com/microsoftgraph/powershell-intune-samples).
