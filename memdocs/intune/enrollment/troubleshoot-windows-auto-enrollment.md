---
title: Řešení potíží s automatickým zápisem pro Windows 10 v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si, jak řešit potíže s automatickým zápisem.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 8/3/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jchombe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 968aa9b2f7127e9b7f092f36a99b491a75f0b78c
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546862"
---
# <a name="troubleshoot-windows-10-group-policy-based-auto-enrollment-in-intune"></a>Řešení potíží s automatickým zápisem na základě zásad skupiny Windows 10 v Intune

Pomocí zásad skupiny můžete aktivovat automatickou registraci MDM pro zařízení připojená k doméně služby Active Directory (AD). Další informace o této funkci najdete v tématu [automatické registrace zařízení s Windows 10 pomocí Zásady skupiny](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy).

## <a name="verify-the-configuration"></a>Ověření konfigurace

Než začnete řešit potíže, je nejlepší ověřit, jestli je vše nakonfigurované správně. Pokud se problém během ověřování nedá opravit, můžete k dalšímu odstraňování potíží zkontrolovat některé důležité soubory protokolu.

- Ověřte, jestli se uživateli, který se pokouší zaregistrovat zařízení, přiřadí platná licence Intune.

   ![Ověřit licenci Intune](./media/troubleshoot-windows-auto-enrollment/intune-license.png)

- Ověřte, jestli je automatický zápis povolený pro všechny uživatele, kteří budou zařízení registrovat v Intune. Další informace najdete v tématu [Azure AD a Microsoft Intune: Automatická registrace MDM na novém portálu](https://docs.microsoft.com/windows/client-management/mdm/azure-ad-and-microsoft-intune-automatic-mdm-enrollment-in-the-new-portal).

   ![Ověřit automatickou registraci](./media/troubleshoot-windows-auto-enrollment/verify-auto-enrollment.png)

   - Ověřte, jestli je **obor uživatele MDM** nastavený na **vše** a umožní všem uživatelům zaregistrovat zařízení v Intune.
   - Ověřte, zda je **obor uživatele mam** nastaven na **hodnotu None**. V opačném případě bude mít toto nastavení přednost před rozsahem MDM a způsobovat problémy.
   - Ověřte, jestli je **Adresa URL zjišťování MDM** nastavená na **https://enrollment.manage.microsoft.com/enrollmentserver/discovery** .

- Ověřte, že na zařízení běží Windows 10 verze 1709 nebo novější.

- Ověřte, že jsou zařízení nastavená na **hybridní službu Azure AD**. Toto nastavení znamená, že jsou zařízení připojená k doméně i k Azure AD.

   Nastavení ověříte spuštěním **dsregcmd/status** na příkazovém řádku. Pak ověřte následující hodnoty stavu ve výstupu:

   - Stav zařízení
 
     ```asciidoc
     AzureAdJoined: YES
     DomainJoined: YES
     ```

   - Stav jednotného přihlašování

     ```asciidoc
     AzureAdPrt: YES
     ```

   Stejné informace najdete v seznamu zařízení připojených k Azure AD:

   ![Seznam zařízení připojených k Azure AD](./media/troubleshoot-windows-auto-enrollment/ad-joined-devices.png)

- **Microsoft Intune**   V okně Azure AD se můžou v části **mobilita (MDM a mam)** uvést jak **registrace** Microsoft Intune, tak Microsoft Intune   . Pokud jsou k dispozici obě, ujistěte se, že jste nakonfigurovali nastavení automatického zápisu v části **Microsoft Intune**.

- Ověřte, jestli se následující nastavení zásad Zásady skupiny úspěšně nasadilo do všech zařízení, která by se měla zaregistrovat v Intune:

   **Konfigurace počítače**  >  **Zásady**  >  **Šablony pro správu**  >  **Součásti**  >  systému Windows **MDM**  >  **Povolit automatickou registraci MDM pomocí výchozích přihlašovacích údajů Azure AD**

   Můžete se obrátit na správce domény a ověřit, jestli se nastavení zásad Zásady skupiny úspěšně nasadilo.

- Ujistěte se, že zařízení není zaregistrované v Intune pomocí klasického agenta pro počítače PC.
- Ověřte následující nastavení v Azure AD a Intune:

   **V nastavení zařízení Azure AD:**

   ![Nastavení zařízení Azure AD](./media/troubleshoot-windows-auto-enrollment/device-setting.png)

   - **Uživatelé můžou připojit zařízení k Azure AD** nastavení je nastavené na **vše**.
   - Počet zařízení, která uživatel ve službě Azure AD používá, nepřekračuje **maximální počet zařízení na** kvótu uživatele.
   
   **V rámci omezení registrace v Intune:**

   - Registrace zařízení s Windows je povolená.

     ![Povolená registrace zařízení s Windows](./media/troubleshoot-windows-auto-enrollment/restrictions.png)

## <a name="troubleshooting"></a>Poradce při potížích

Pokud se problém opakuje, Projděte si protokoly MDM na zařízení v následujícím umístění v Prohlížeč událostí:

Protokoly aplikací a **služeb**  >  **Microsoft**  >  **Systém Windows**  >  **DeviceManagement-Enterprise-Diagnostic-Provider**  >  **Správce**

Vyhledejte událost s ID 75 (zpráva události "Automatická registrace MDM: úspěšné"). Tato událost označuje, že automatický zápis byl úspěšný.

Událost s ID 75 není zaznamenána v následujících situacích:

- Registrace se nezdařila.

  Tuto chybu můžete ověřit tak, že vyhledáte událost ID 76 (zpráva o události: Automatická registrace MDM: selhala (Neznámý kód chyby Win32:0x8018002b)). Tato událost označuje neúspěšnou automatickou registraci.

  Řešení této chyby najdete [v tématu řešení potíží s registrací zařízení s Windows v Microsoft Intune](https://docs.microsoft.com/intune/troubleshoot-windows-enrollment-errors).

- Registrace neaktivovala vůbec.V tomto případě nejsou události s ID 75 a ID události 76 protokolovány.
  
  Proces automatické registrace se aktivuje pomocí možnosti**Plán vytvořený klientem registrace pro automatické zaregistrování do MDM z AAD**, které se nachází v systému **Microsoft**  >  **Windows**  >  **EnterpriseMgmt** v Plánovač úloh.

  ![Registrace se neaktivovala.](./media/troubleshoot-windows-auto-enrollment/trigger.png)

  Tato úloha se vytvoří, když se nastavení zásad Zásady skupiny **Povolit automatický zápis MDM pomocí výchozích přihlašovacích údajů služby Azure AD** úspěšně nasadí do cílového zařízení. Úloha je naplánována na spuštění každých 5 minut během 1 dne.

  Chcete-li ověřit, zda je úloha spuštěna, zkontrolujte protokoly událostí plánovače úloh v následujícím umístění v Prohlížeč událostí:

  **Protokoly aplikací a služeb > Microsoft > Windows > Plánovač úloh > provozní**

  Při spuštění úlohy v plánovači se zaprotokoluje událost s ID 107.

  Po dokončení úlohy se zaprotokoluje událost s ID 102. Událost je protokolována bez ohledu na to, zda je automatický zápis úspěšný.

  > [!NOTE]
  > Pomocí protokolu plánovače úloh můžete ověřit, jestli se spustil automatický zápis. Protokol ale nemůžete použít k určení, jestli se automatický zápis úspěšně zdařil.

  V následující situaci může dojít k selhání plánu vytvořeného klientem registrace pro automatické registraci do MDM z úlohy AAD, kterou nechcete spustit:

  - Zařízení je už zaregistrované v jiném řešení MDM. V tomto případě se protokol událostí s ID 7016 společně s kódem chyby 2149056522 protokoluje v protokolech **aplikací a služeb**  >  **Microsoft**  >  **Windows**  >  **Plánovač úloh**  >  protokolu událostí**operačního** systému.

    Pokud chcete tento problém vyřešit, odregistrujte zařízení v MDM.

  - Zásady skupiny existuje problém. V takovém případě vynuťte aktualizaci Zásady skupiny nastavením spuštěním následujícího příkazu:

    **gpupdate/force**

    Pokud se problém opakuje, proveďte další řešení potíží ve službě Active Directory.

## <a name="next-steps"></a>Další kroky
[Řešení potíží s registrací zařízení s Windows](troubleshoot-windows-enrollment-errors.md)