---
title: Podmíněný přístup se spolusprávou
titleSuffix: Configuration Manager
description: Řízení přístupu uživatelů k prostředkům organizace na základě pravidel dodržování předpisů z Intune
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d35f36b6578359f62f21b4e2208a70ace22cf0d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711501"
---
# <a name="conditional-access-with-co-management"></a>Podmíněný přístup se spolusprávou

Podmíněný přístup zajistí, že přístup k prostředkům organizace na důvěryhodných zařízeních pomocí důvěryhodných aplikací má jenom důvěryhodní uživatelé. Je vytvořená od začátku v cloudu. Bez ohledu na to, jestli spravujete zařízení pomocí Intune nebo rozšíření nasazení Configuration Manager se spolusprávou, funguje stejným způsobem.

V následujícím videu, vedoucí program Justinu Glocke a marketingový manažer pro produkty, Ainley projednávat a ukázkový podmíněný přístup pomocí spolusprávy:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Díky spolusprávě Intune vyhodnocuje každé zařízení ve vaší síti, aby bylo možné určit, jak důvěřuje. Provede toto vyhodnocení následujícími dvěma způsoby:

1. Intune zajišťuje, aby bylo zařízení nebo aplikace spravované a bezpečně nakonfigurované. Tato kontrolu závisí na nastavení zásad dodržování předpisů ve vaší organizaci. Ujistěte se například, že všechna zařízení mají povolené šifrování a nejsou jailbreakem.  

    - Toto vyhodnocení je před porušením zabezpečení a na základě konfigurace.  

    - Pro spoluspravovaná zařízení Configuration Manager také vyhodnocení na základě konfigurace. Například požadované aktualizace nebo dodržování předpisů pro aplikace. Intune kombinuje Toto vyhodnocení společně s jeho vlastním posouzením.  

2. Intune detekuje aktivní incidenty zabezpečení na zařízení. Používá inteligentní zabezpečení programu [Microsoft Defender Advanced Threat Protection](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (dříve ATP v programu Windows Defender) a další [poskytovatele ochrany před mobilními hrozbami](https://www.lookout.com/about/partners/microsoft). Tito partneři spouštějí průběžnou analýzu chování na zařízeních. Tato analýza detekuje aktivní incidenty a pak předá tyto informace do Intune pro vyhodnocení dodržování předpisů v reálném čase.  

    - Toto vyhodnocení je porušení zabezpečení po podsystému a na základě incidentu.  

Společnost Microsoft z viceprezidenta Brad Anderson popisuje podmíněný přístup v hloubkě s živými ukázkami během Ignite 2018 vystoupení. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Podmíněný přístup taky poskytuje centralizované místo pro zobrazení stavu všech zařízení připojených k síti. Získáte výhody cloudového škálování, což je obzvláště důležité pro testování Configuration Manager produkčních instancí.


## <a name="benefits"></a>Výhody

Každý tým IT je Obsessed se zabezpečením sítě. Před přístupem k síti je nutné zajistit, aby všechna zařízení splňovala vaše požadavky na zabezpečení a podnikové požadavky. Pomocí podmíněného přístupu můžete určit následující faktory: 
- Pokud je každé zařízení zašifrované  
- Pokud je nainstalován malware  
- Pokud je jeho nastavení Aktualizováno  
- Pokud má jailbreak nebo root  

Podmíněný přístup kombinuje přesnější kontrolu nad daty organizace s uživatelským prostředím, které maximalizuje produktivitu pracovních procesů na jakémkoli zařízení z libovolného místa.

Následující video ukazuje, jak je [Rozšířená ochrana vláken](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) integrovaná do běžných scénářů, ke kterým dochází pravidelně:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Díky spolusprávě může Intune zahrnovat Configuration Manager odpovědnost za hodnocení dodržování standardů zabezpečení u požadovaných aktualizací nebo aplikací. Toto chování je důležité pro všechny IT organizace, které chtějí dál používat Configuration Manager pro komplexní správu aplikací a oprav.

Podmíněný přístup je také důležitou součástí vývoje vaší síťové architektury s [nulovou důvěryhodností](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) . V případě podmíněného přístupu se řízení přístupu k zařízením dodržuje v základních vrstvách nulové důvěryhodné sítě. Tato funkce je velkou součástí zabezpečení vaší organizace v budoucnu.

Další informace najdete v blogovém příspěvku o [vylepšení podmíněného přístupu s daty z důvodu ochrany počítačů pomocí rozšířené ochrany před internetovými útoky v programu Microsoft Defender](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Případové studie

Společnost Wipro v poradenském podniku používá podmíněný přístup k ochraně a správě zařízení používaných všemi zaměstnanci 91 000. V nedávném případové studii je viceprezident v programu Wipro uveden:

> *Dosažení podmíněného přístupu je velký soubor Win pro společnosti Wipro. Všichni naši zaměstnanci teď mají mobilní přístup k informacím na vyžádání.* 
>  *Vylepšili jsme naše stavy zabezpečení a produktivitu zaměstnanců. Zaměstnanci teď 91 000 využívají vysoce zabezpečený přístup k více než 100 aplikacím z libovolného zařízení a kdekoli.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Mezi další příklady patří: 

- Nestlé, kdo používá podmíněný přístup na základě aplikace pro více než 150 000 zaměstnanců  

- Společnost pro automatizaci softwaru tempo, která teď může zajistit, aby přístup k aplikacím Office 365, jako jsou týmy a intranetu společnosti, měla jenom spravovaná zařízení. Mohou také nabídnout pracovníkům "bezpečnější přístup k jiným cloudovým aplikacím, jako je například Workday a Salesforce." Další informace o zkušenostech s tempo s Intune najdete v článku [tempo zvyšuje tempo podnikání pomocí nástrojů pro mobilní spolupráci v Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

Intune se taky plně integruje s partnery, jako je Cisco ISE, Aruba Clear Pass a Citrix NetScaler. U těchto partnerů můžete spravovat řízení přístupu na základě registrace Intune a stavu dodržování předpisů zařízením napříč těmito platformami.

Další informace najdete v následujících videích:
- [Brad Anderson demo podrobně popisuje podmíněný přístup](https://youtu.be/8321obNofgM?t=547)  
- [Další podrobnosti ze zóny Endpoint 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Pozice hodnoty

S integrací podmíněného přístupu a ATP se zvyšuje základní součást každé organizace IT: zabezpečený cloudový přístup.

Ve více než 63% všech porušení dat získají útočníci přístup k síti organizace prostřednictvím slabých, výchozích nebo odcizených přihlašovacích údajů uživatele. Vzhledem k tomu, že se podmíněný přístup zaměřuje na zabezpečení identity uživatele, omezuje odcizení přihlašovacích údajů. Podmíněný přístup spravuje a chrání vaše identity, ať už privilegované, nebo Neprivilegovaný. Neexistuje lepší způsob, jak chránit zařízení a data v nich.

Vzhledem k tomu, že podmíněný přístup je základní součástí Enterprise Mobility + Security (EMS), není nutná žádná místní instalace nebo architektura. S Intune a Azure Active Directory (Azure AD) můžete rychle nakonfigurovat podmíněný přístup v cloudu. Pokud v tuto chvíli používáte Configuration Manager, můžete své prostředí snadno roztáhnout do cloudu pomocí spolusprávy a začít ho používat hned teď.

Další informace o integraci ATP najdete v tomto blogovém příspěvku [hodnocení rizik zařízení v programu Microsoft Defender. vystavuje nové cyberattack, řídí podmíněný přístup k ochraně sítí](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). Podrobná informace o tom, jak Pokročilá skupina hackerů používala ještě nikdy před zobrazením nástrojů. Cloud Microsoftu je zjistil a zastavil, protože cíloví uživatelé měli podmíněný přístup. Neoprávněný vniknutí aktivoval zásadu podmíněného přístupu na základě rizika zařízení. I když útočník již v síti navázal dostane, zneužité počítače automaticky omezily přístup k podnikovým službám a datům spravovaným službou Azure AD.



## <a name="configure"></a>Konfigurace

Podmíněný přístup se dá snadno použít, když [povolíte spolusprávu](how-to-enable.md). Vyžaduje přesun úlohy **zásad dodržování předpisů** do Intune. Další informace najdete v tématu [Postup přepnutí úloh Configuration Manager do Intune](how-to-switch-workloads.md). 

Další informace o použití podmíněného přístupu najdete v následujících článcích: 

- [Podmíněný přístup v Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Zásady dodržování předpisů zařízeními v Intune](https://docs.microsoft.com/intune/device-compliance)  

- [Podmíněný přístup na základě aplikace s využitím Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Funkce podmíněného přístupu budou k dispozici okamžitě pro zařízení připojená k hybridní službě Azure AD. Mezi tyto funkce patří Multi-Factor Authentication a hybridní řízení přístupu ke službě Azure AD. Důvodem je to, že jsou založené na vlastnostech Azure AD. Pokud chcete využít hodnocení na základě konfigurace z Intune a Configuration Manager, povolte spolusprávu. Tato konfigurace poskytuje přístup k řízení přístupu přímo z Intune pro vyhovující zařízení. Poskytuje taky funkci vyhodnocení zásad dodržování předpisů pro Intune.  

