---
title: Úlohy spolusprávy
titleSuffix: Configuration Manager
description: Přečtěte si o úlohách, které můžete přepnout z Configuration Manager na Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: 8c91ba1c2b4b5ef7072c030eddd9b97dd69933e5
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075706"
---
# <a name="co-management-workloads"></a>Úlohy spolusprávy

Nemusíte přepínat úlohy, nebo je můžete provést jednotlivě, až budete připraveni. Configuration Manager nadále spravuje všechny ostatní úlohy, včetně úloh, které nepřepnete do Intune, a všech ostatních funkcí Configuration Manager, které spoluspráva nepodporuje.

Pokud úlohu přepnete do Intune, ale později ji změníte, můžete ji přepnout zpátky na Configuration Manager.

Spoluspráva podporuje následující úlohy:

- [Zásady dodržování předpisů](#compliance-policies)  

- [Zásady web Windows Update](#windows-update-policies)  

- [Zásady přístupu k prostředkům](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Konfigurace zařízení](#device-configuration)  

- [Aplikace pro Office Klikni a spusť](#office-click-to-run-apps)  

- [Klientské aplikace](#client-apps)  

## <a name="compliance-policies"></a>Compliance zásady

Zásady dodržování předpisů definují pravidla a nastavení, která musí zařízení dodržovat, aby se dalo považovat za zařízení, které dodržuje zásady podmíněného přístupu. Pomocí zásad dodržování předpisů můžete také monitorovat a opravovat problémy s kompatibilitou zařízení nezávisle na podmíněném přístupu. Od verze Configuration Manager 1910 můžete přidat hodnocení vlastních standardních hodnot konfigurace jako pravidla pro vyhodnocení zásad dodržování předpisů. Další informace najdete v tématu [Zahrnutí vlastních standardních hodnot konfigurace jako součásti posouzení zásad dodržování předpisů](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

Další informace o funkci Intune najdete v tématu [zásady dodržování předpisů pro zařízení](https://docs.microsoft.com/intune/device-compliance-get-started).  

## <a name="windows-update-policies"></a>Zásady web Windows Update

Zásady web Windows Update pro firmy umožňují nakonfigurovat zásady odložení pro aktualizace funkcí Windows 10 nebo aktualizace kvality pro zařízení s Windows 10 spravovaná přímo pomocí web Windows Update pro firmy.

Další informace o funkci Intune najdete v tématu [Konfigurace zásad odložení web Windows Update pro firmy](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

## <a name="resource-access-policies"></a>Zásady přístupu k prostředkům

Zásady přístupu k prostředkům konfigurují nastavení VPN, Wi-Fi, e-mailu a certifikátů na zařízeních.

Další informace o funkci Intune najdete v tématu [nasazení profilů přístupu k prostředkům](https://docs.microsoft.com/intune/device-profiles).

> [!Note]  
> Úlohy přístupu k prostředkům jsou také součástí konfigurace zařízení. Tyto zásady spravuje Intune při přepínání úlohy [Konfigurace zařízení](#device-configuration) .

## <a name="endpoint-protection"></a>Funkce Endpoint Protection

<!--1357365-->

Úloha Endpoint Protection obsahuje sadu funkcí ochrany proti malwaru v programu Windows Defender:

- Antimalwarová ochrana v programu Windows Defender
- Ochrana Application Guard v programu Windows Defender  
- Firewall v programu Windows Defender  
- Filtr SmartScreen v programu Windows Defender  
- Šifrování Windows
- Ochrana Exploit Guard v programu Windows Defender  
- Řízení aplikací programu Windows Defender  
- Centrum zabezpečení v programu Windows Defender  
- Rozšířená ochrana před internetovými útoky v programu Windows Defender (nyní označovaná jako Microsoft Defender Threat Protection)
- Windows Information Protection  

Další informace o funkci Intune najdete v tématu [Endpoint Protection Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

> [!Note]  
> Když přepnete tuto úlohu, zásady Configuration Manager zůstanou na zařízení, dokud je zásady Intune nepřepíší. Tím se zajistí, že zařízení má při přechodu stále zásady ochrany.
>
> Úlohy Endpoint Protection jsou také součástí konfigurace zařízení. Stejné chování platí při přepínání úlohy [Konfigurace zařízení](#device-configuration) .<!-- SCCMDocs.nl-nl issue #4 -->
>
> Nastavení ochrany antivirovým programem Microsoft Defender, která jsou součástí typu profilu omezení zařízení pro konfiguraci zařízení Intune, nejsou zahrnutá do rozsahu posuvníku Endpoint Protection. Pokud chcete spravovat antivirovou ochranu v programu Microsoft Defender pro spoluspravovaná zařízení s povoleným posuvníkem Endpoint Protection, použijte nové zásady antivirové ochrany v centru > pro **správu Microsoft Endpoint Manageru**v části**Endpoint Security** > **Antivirus**. Nový typ zásad má k dispozici nové a vylepšené možnosti a podporuje všechna stejná nastavení, která jsou dostupná v profilu omezení zařízení. <!--6609171-->
>
> Funkce šifrování systému Windows zahrnuje správu BitLockeru. Další informace o chování této funkce společně se správou najdete v tématu [nasazení správy nástroje BitLocker](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune).<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>Konfigurace zařízení

<!--1357903-->

Úloha konfigurace zařízení zahrnuje nastavení, která spravujete pro zařízení ve vaší organizaci. Přepnutí této úlohy také přesune úlohy **přístupu k prostředkům** a **Endpoint Protection** .

Nastavení můžete i nadále nasazovat z Configuration Manager do spoluspravovaných zařízení, i když je Intune autorita pro konfiguraci zařízení. Tato výjimka se dá použít ke konfiguraci nastavení, které vaše organizace vyžaduje, ale ještě není v Intune dostupná. Zadejte tuto výjimku pro [standardní hodnoty konfigurace Configuration Manager](../compliance/deploy-use/create-configuration-baselines.md). Tuto možnost povolte, pokud chcete při vytváření standardních hodnot **vždycky použít tyto standardní hodnoty i pro spoluspravované klienty** . Později ji můžete změnit na kartě **Obecné** ve vlastnostech existujícího směrného plánu.  

Další informace o funkci Intune najdete v tématu [Vytvoření profilu zařízení v Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  

## <a name="office-click-to-run-apps"></a>Aplikace pro Office Klikni a spusť

<!--1357841-->

Toto zatížení spravuje aplikace Office 365 na spoluspravovaných zařízeních.

- Po přesunutí úlohy se aplikace zobrazí v **portál společnosti** na zařízení.  

- Aktualizace Office může trvat přibližně 24 hodin, než se v klientovi zobrazí, pokud se zařízení nerestartují.  

- Je k dispozici nová globální podmínka, **jedná se o aplikace Office 365 spravované přes Intune na zařízení**. Tato podmínka se ve výchozím nastavení přidá jako požadavek pro nové aplikace Office 365. Při přechodu na tuto úlohu nesplňuje spoluspravovaná klienti požadavek na aplikaci. Pak neinstalují Office 365 nasazené prostřednictvím Configuration Manager.  

Další informace o funkci Intune najdete v článku [přiřazení aplikací Office 365 k zařízením s Windows 10 pomocí Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365).

## <a name="client-apps"></a>Klientské aplikace

<!--1357892-->

Pomocí Intune můžete spravovat klientské aplikace a skripty PowerShellu na spoluspravovaných zařízeních s Windows 10. Po přechodu na tuto úlohu jsou všechny dostupné aplikace nasazené z Intune dostupné v Portál společnosti. Aplikace, které nasazujete z Configuration Manager, jsou k dispozici v centru softwaru.

Další informace o funkci Intune najdete v tématu [co je Správa aplikací Microsoft Intune?](https://docs.microsoft.com/intune/app-management).

> [!Tip]  
> Tato funkce byla poprvé představena ve verzi 1806 jako [funkce předběžné verze](../core/servers/manage/pre-release-features.md). Od verze 2002 už není k dispozici funkce předběžného vydání.  
>
> Tato funkce se může zobrazit v seznamu funkcí jako **mobilní aplikace pro spoluspravovaná zařízení**.<!-- 5849669 -->

Pokud ve verzi 1910 povolíte v Configuration Manager distribučních bodech Microsoft připojenou mezipaměť, můžou teď Microsoft Intune aplikace Win32 sloužit spoluspravovaným klientům. Další informace najdete v tématu věnovaném [mezipaměti připojené k Microsoftu v Configuration Manager](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune).

## <a name="diagram-for-app-workloads"></a>Diagram pro úlohy aplikací

![Diagram úloh aplikací spolusprávy](media/co-management-apps.svg)

[Zobrazit diagram v plné velikosti](media/co-management-apps.svg)

## <a name="known-issues"></a>Známé problémy

Po přesunutí úlohy Endpoint Protection do Intune může klient nadále dodržovat zásady nastavené pomocí Configuration Manager a programu Microsoft Defender. <!--5024559-->

Pokud chcete tento problém obejít, použijte CleanUpPolicy. XML, až po přijetí zásad Intune z klienta použijte následující postup:

1. Zkopírujte a uložte níže uvedený text `CleanUpPolicy.xml`.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```
1. Otevřete příkazový řádek se zvýšenými `ConfigSecurityPolicy.exe`oprávněními na. Obvykle je tento spustitelný soubor v jednom z následujících adresářů:
   - C:\Program Files\Windows Defender
   - C:\Program Files\Microsoft – klient zabezpečení
1. Z příkazového řádku předejte soubor XML, aby se zásady vyčistily. Například, `ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`.  

## <a name="next-steps"></a>Další kroky

[Jak přepínat úlohy](how-to-switch-workloads.md)  
