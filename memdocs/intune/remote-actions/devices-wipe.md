---
title: Vyřazení nebo vymazání zařízení pomocí Microsoft Intune – Azure | Microsoft Docs
description: Vyřazení nebo vymazání zařízení v Androidu, pracovním profilu Androidu, iOS/iPadOS, macOS nebo zařízení s Windows pomocí Microsoft Intune. Můžete také odstranit zařízení z Azure Active Directory.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 2/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4fdb787e-084f-4507-9c63-c96b13bfcdf9
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2eae55477ef62c408ff886499f4668c81c799fc8
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326292"
---
# <a name="remove-devices-by-using-wipe-retire-or-manually-unenrolling-the-device"></a>Odebrání zařízení vymazáním, vyřazením nebo ručním zrušením registrace

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Zařízení, která už nepotřebujete, která využíváte k jinému účelu nebo která se ztratila, můžete z Intune odebrat prostřednictvím akce **Vyřazení** nebo **Vymazání**. Uživatelé taky můžou z Portál společnosti Intune vydat vzdálený příkaz do zařízení, která jsou zaregistrovaná v Intune.

> [!NOTE]
> Před odebráním uživatele z Azure Active Directory (Azure AD) použijte akce **Vymazání** nebo **Vyřazení** u všech zařízení přidružených k tomuto uživateli. Pokud z Azure AD odeberete uživatele se spravovanými zařízeními, nemůže už Intune tato zařízení vymazat ani vyřadit.

## <a name="wipe"></a>Vymazání

Akce **Vymazání** obnoví výchozí tovární nastavení zařízení. Data uživatele se zachovají, pokud zaškrtnete políčko **Zachovat stav registrace a uživatelský účet**. Jinak se odeberou všechna data, aplikace a nastavení.

|Akce vymazání|**Zachovat stav registrace a uživatelský účet**|Odebráno ze správy v Intune|Popis|
|:-------------:|:------------:|:------------:|------------|
|**Vymazání**| Není zaškrtnuto | Ano | Vymaže všechny uživatelské účty, data, zásady MDM a nastavení. Obnoví operační systém do výchozího stavu a nastavení.|
|**Vymazání**| Zaškrtnuto | Ne | Vymaže všechny zásady MDM. Zachová uživatelské účty a data. Obnoví nastavení uživatele zpět na výchozí nastavení. Obnoví operační systém do výchozího stavu a nastavení.|


> [!NOTE]
> Akce vymazání není k dispozici pro zařízení se systémem iOS/iPadOS zaregistrovaná při registraci uživatele.

Pro Windows 10 verze 1709 nebo novější máte také možnost **Zachovat stav registrace a uživatelský účet**.

Zásady MDM se znovu použijí při příštím připojení zařízení k Intune.

Vymazání je vhodné, když chcete zařízení resetovat, abyste ho mohli dát novému uživateli, nebo když došlo k jeho ztrátě nebo odcizení. Volbu **vymazání** používejte velmi opatrně. Data v zařízení není možné obnovit.

### <a name="wiping-a-device"></a>Vymazání zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Vyberte **Zařízení** > **Všechna zařízení**.
4. Zvolte název zařízení, které chcete vymazat.
5. V podokně s názvem zařízení vyberte **Vymazání**.
6. Pro Windows 10 verze 1709 nebo novější máte také **zařízení pro vymazání, ale možnost zachovat stav registrace a přidružený uživatelský účet** . 
    
    |Zachová se při vymazání |Nezachová se|
    | -------------|------------|
    |Uživatelské účty přidružené k zařízení|Soubory uživatele|
    |Stav počítače \(připojení k doméně, připojení k Azure AD)| Aplikace nainstalované uživatelem \(aplikace ze Storu a aplikace Win32)|
    |Registrace ve správě mobilních zařízení (MDM)|Nevýchozí nastavení zařízení|
    |Aplikace nainstalované výrobcem OEM \(aplikace ze Storu a aplikace Win32)||
    |Profil uživatele||
    |Uživatelská data mimo profil uživatele||
    |Automatické přihlášení uživatele|| 
    
7. **Vymaže zařízení a pokračuje v mazání i v případě, že zařízení ztratí napájení.** možnost zajistěte, aby se akce vymazání nemohla obejít vypnutím zařízení. Tato možnost bude pokračovat v pokusu o resetování zařízení, dokud neproběhne úspěšně. V některých konfiguracích může tato akce opustit zařízení, protože se [nemůže restartovat](troubleshoot-device-actions.md#wipe-action).        
8. Potvrďte vymazání volbou možnosti **Ano**.

Pokud je zařízení zapnuté a připojené, akce **Vymazání** se do všech typů zařízení rozšíří do 15 minut.

## <a name="retire"></a>Vyřadit

Akce **Vyřazení** odebere data případných spravovaných aplikací, nastavení a e-mailové profily, které byly přiřazeny přes Intune. Toto zařízení se odebere ze správy v Intune. K tomu dojde, když se zařízení příště přihlásí a přijme vzdálenou akci **Vyřazení**. Zařízení se pořád zobrazuje v Intune, dokud zařízení nekontroluje. Pokud chcete okamžitě odebrat zastaralá zařízení, použijte místo toho [akci odstranit](devices-wipe.md#delete-devices-from-the-intune-portal) .

Při této akci zůstanou v zařízení osobní data uživatele.  

Následující tabulky popisují, jaká data se odeberou a jaký vliv má akce **Vyřazení** na zbývající data v zařízení po odebrání firemních dat.

### <a name="ios"></a>iOS

|Datový typ|iOS|
|-------------|-------|
|Firemní aplikace a související data instalovaná službou Intune|**Aplikace nainstalované pomocí portál společnosti:** Pro aplikace, které jsou připnuté na profil správy, se odeberou všechna data aplikací a aplikace. Tyto aplikace zahrnují aplikace původně nainstalované z App Storu a později spravované jako firemní aplikace, pokud není aplikace nakonfigurovaná tak, aby se odinstalovala při odebírání zařízení. <br /><br /> **Aplikace Microsoftu, které používají správu mobilních aplikací a které se nainstalovaly z App Storu:** Pro aplikace, které nejsou spravované Portál společnosti, se odeberou data firemní aplikace chráněná šifrováním pomocí správy mobilních aplikací (MAM) v rámci aplikace v místním úložišti. Data chráněná šifrováním MAM mimo aplikaci zůstávají šifrovaná a nepoužitelná, ale neodstraňují se. Data osobní aplikace a aplikace se neodeberou.|
|Nastavení|Konfigurace nastavené zásadami Intune se už nevynucují. Uživatelé můžou nastavení změnit.|
|Nastavení profilu sítě Wi-Fi a VPN|Odebrány.|
|Nastavení profilu certifikátu|Certifikáty jsou odebrané a odvolané.|
|Agent pro správu|Odebere se profil pro správu.|
|E-mail|Odeberou se e-mailové profily, které jsou zřízené prostřednictvím Intune. Odstraní se e-maily v mezipaměti zařízení.|
|Zrušení připojení k Azure AD|Odebere se záznam Azure AD.|

### <a name="android"></a>Android

|Datový typ|Android|Android Samsung Knox Standard|
|-------------|-----------|------------------------|
|Webové odkazy|Odebrány.|Odebrány.|
|Nespravované aplikace Google Play|Aplikace a data zůstanou nainstalována. <br /> <br />Odeberou se data firemních aplikací chráněná šifrováním pomocí správy mobilních aplikací (MAM) v rámci aplikace v místním úložišti. Data chráněná šifrováním MAM mimo aplikaci zůstávají šifrovaná a nepoužitelná, ale neodstraňují se. |Aplikace a data zůstanou nainstalována. <br /> <br />Odeberou se data firemních aplikací chráněná šifrováním pomocí správy mobilních aplikací (MAM) v rámci aplikace v místním úložišti. Data chráněná šifrováním MAM mimo aplikaci zůstávají šifrovaná a nepoužitelná, ale neodstraňují se.|
|Nespravované obchodní aplikace|Aplikace a data zůstanou nainstalována.|Odinstalují se aplikace a odeberou se jejich místní data. Data mimo aplikaci (například na kartě SD) se neodeberou.|
|Spravované aplikace Google Play|Odeberou se data aplikací. Aplikace se neodebere. Data chráněná šifrováním správy mobilních zařízení (MAM) mimo aplikaci (třeba na kartě SD) zůstanou zašifrována, takže nepůjdou použít, ale neodeberou se.|Odeberou se data aplikací. Aplikace se neodebere. Data chráněná šifrováním MAM mimo aplikaci (třeba na kartě SD) zůstanou zašifrována, ale neodeberou se.|
|Spravované obchodní aplikace|Odeberou se data aplikací. Aplikace se neodebere. Data chráněná šifrováním MAM mimo aplikaci (třeba na kartě SD) zůstanou zašifrována, takže nepůjdou použít, ale neodeberou se.|Odeberou se data aplikací. Aplikace se neodebere. Data chráněná šifrováním MAM mimo aplikaci (třeba na kartě SD) zůstanou zašifrována, takže nepůjdou použít, ale neodeberou se.|
|Nastavení|Konfigurace nastavené zásadami Intune se už nevynucují. Uživatelé můžou nastavení změnit.|Konfigurace nastavené zásadami Intune se už nevynucují. Uživatelé můžou nastavení změnit.|
|Nastavení profilu sítě Wi-Fi a VPN|Odebrány.|Odebrány.|
|Nastavení profilu certifikátu|Certifikáty se zruší, ale neodeberou.|Certifikáty jsou odebrané a odvolané.|
|Agent pro správu|Zruší se oprávnění správce zařízení.|Zruší se oprávnění správce zařízení.|
|E-mail|Není k dispozici (zařízení s Androidem nepodporují e-mailové profily)|Odeberou se e-mailové profily, které jsou zřízené prostřednictvím Intune. Odstraní se e-maily v mezipaměti zařízení.|
|Zrušení připojení k Azure AD|Odebere se záznam Azure AD.|Odebere se záznam Azure AD.|

### <a name="android-work-profile"></a>Pracovní profil Androidu

Při odebrání firemních dat ze zařízení s pracovním profilem Androidu se odeberou všechna data, aplikace a nastavení v pracovním profilu na tomto zařízení. Zařízení se vyřadí ze správy pomocí Intune. Pracovní profily Androidu nepodporují vymazání.

### <a name="android-enterprise-kiosk-devices"></a>Zařízení s Androidem Enterprise v beznabídkovém režimu

Zařízení s Androidem v beznabídkovém režimu můžete jen vymazat. Vyřazení u nich není možné.


### <a name="macos"></a>macOS

|Datový typ|macOS|
|-------------|-------|
|Nastavení|Konfigurace nastavené zásadami Intune se už nevynucují. Uživatelé můžou nastavení změnit.|
|Nastavení profilu sítě Wi-Fi a VPN|Odebrány.|
|Nastavení profilu certifikátu|Certifikáty nasazené prostřednictvím správy mobilních zařízení se odeberou a odvolají.|
|Agent pro správu|Odebere se profil pro správu.|
|Outlook|Pokud je podmíněný přístup povolený, zařízení neobdrží novou poštu.|
|Zrušení připojení k Azure AD|Odebere se záznam Azure AD.|

### <a name="windows"></a>Windows

|Datový typ|Windows 8.1 (MDM) a Windows RT 8.1|Windows RT|Windows Phone 8.1 a Windows Phone 8|Windows 10|
|-------------|----------------------------------------------------------------|--------------|-----------------------------------------|--------|
|Firemní aplikace a související data instalovaná službou Intune|Odvolají se klíče pro soubory, které jsou chráněné systémem souborů EFS. Uživatel nemůže soubory otevřít.|Firemní aplikace se neodeberou.|Odinstalují se aplikace původně nainstalované prostřednictvím Portálu společnosti. Odeberou se data firemních aplikací.|Odinstalují se aplikace. Odeberou se klíče pro zkušební načtení.<br>Ve Windows 10 verze 1703 (Creators Update) a novějších verzích se neodeberou aplikace Office 365 ProPlus. Rozšíření pro správu Intune nainstalované aplikace Win32 se odinstalují na nezaregistrovaných zařízeních. Správci můžou využít vyloučení přiřazení, aby nenabízeli aplikacím Win32 možnost BYOD zařízení.|
|Nastavení|Konfigurace nastavené zásadami Intune se už nevynucují. Uživatelé můžou nastavení změnit.|Konfigurace nastavené zásadami Intune se už nevynucují. Uživatelé můžou nastavení změnit.|Konfigurace nastavené zásadami Intune se už nevynucují. Uživatelé můžou nastavení změnit.|Konfigurace nastavené zásadami Intune se už nevynucují. Uživatelé můžou nastavení změnit.|
|Nastavení profilu sítě Wi-Fi a VPN|Odebrány.|Odebrány.|Není podporováno.|Odebrány.|
|Nastavení profilu certifikátu|Certifikáty jsou odebrané a odvolané.|Certifikáty jsou odebrané a odvolané.|Není podporováno.|Certifikáty jsou odebrané a odvolané.|
|E-mail|Odeberou se e-maily s povoleným systémem souborů EFS. To zahrnuje e-maily a přílohy v aplikaci Pošta pro Windows.|Není podporováno.|Odeberou se e-mailové profily, které jsou zřízené prostřednictvím Intune. Odstraní se e-maily v mezipaměti zařízení.|Odeberou se e-maily s povoleným systémem souborů EFS. To zahrnuje e-maily a přílohy v aplikaci Pošta pro Windows. Odebere e-mailové účty, které byly zřízené Intune.|
|Zrušení připojení k Azure AD|Ne.|Ne.|Odebere se záznam Azure AD.|Odebere se záznam Azure AD.|

> [!NOTE]
> Pro zařízení s Windows 10, která se připojují k Azure AD při počátečním nastavení (OOBE), příkaz vyřadit ze zařízení odeberou všechny účty Azure AD. Postupujte podle kroků v části [spuštění počítače v bezpečném režimu](https://support.microsoft.com/en-us/help/12376/windows-10-start-your-pc-in-safe-mode) , abyste se mohli přihlásit jako místní správce a znovu získat přístup k místním datům uživatele. 

### <a name="retire"></a>Vyřadit

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. V podokně **Zařízení** zvolte **Všechna zařízení**.
3. Zvolte název zařízení, které chcete vyřadit.
4. V podokně s názvem zařízení vyberte **Vyřazení**. Potvrďte zvolením **Ano**.

Pokud je zařízení zapnuté a připojené, akce **Vyřazení** se do všech typů zařízení rozšíří do 15 minut.

## <a name="delete-devices-from-the-intune-portal"></a>Odstranění zařízení z portálu Intune

Pokud chcete odebrat zařízení z portálu Intune, můžete je odstranit z podokna konkrétního zařízení. Při příštím přihlášení zařízení se z něj odeberou všechna firemní data.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Zvolte **Zařízení** > **Všechna zařízení** > vyberte zařízení, která chcete odstranit > **Odstranit**.

### <a name="automatically-delete-devices-with-cleanup-rules"></a>Automatické odstranění zařízení pomocí pravidel čištění
Můžete nakonfigurovat Intune tak, aby automaticky odstraňoval zařízení, která jsou neaktivní, zastaralá nebo nereagující. Tato pravidla čištění průběžně monitorují váš inventář zařízení, aby záznamy vašich zařízení byly stále aktuální. Zařízení odstraněná tímto způsobem se odeberou ze správy Intune.
1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Zvolte **Zařízení** > **Pravidla čištění zařízení** > **Ano**.
3. V poli **Odstranit zařízení, která se pro tento počet dnů nevrátila** , zadejte číslo mezi 30 a 270.
4. Zvolte **Uložit**.



## <a name="delete-devices-from-the-azure-active-directory-portal"></a>Odstranění zařízení z portálu služby Azure Active Directory

Kvůli komunikačním problémům nebo ztraceným zařízením můžete potřebovat odstranit zařízení z Azure AD. Pomocí akce **Odstranit** můžete z portálu Azure Portal odebrat záznamy zařízení, o kterých víte, že jsou nedosažitelná a je nepravděpodobné, že by se službou Azure znovu komunikovala. Akce **Odstranit** neodebere zařízení ze správy.

1. Přihlaste se k [Azure Active Directory na portálu Azure Portal](https://aka.ms/accessaad) pomocí přihlašovacích údajů správce. Můžete se také přihlásit do centra pro [správu Microsoft 365](https://admin.microsoft.com). V nabídce vyberte **Centra pro správu** > **Azure AD**.
2. Pokud nemáte předplatné Azure, vytvořte ho. Pokud máte placený účet, neměli byste potřebovat platební kartu ani zadání platby (vyberte odkaz pro předplatné **Zdarma zaregistrovat službu Azure Active Directory** ).
3. Vyberte **Azure Active Directory** a pak vyberte svoji organizaci.
4. Vyberte kartu **Uživatelé** .
5. Vyberte uživatele spojeného se zařízením, které chcete odstranit.
6. Vyberte **Zařízení**.
7. Odeberte zařízení podle potřeby. Můžete třeba odebrat zařízení, která už se nepoužívají, nebo zařízení s nesprávnými definicemi.

## <a name="retire-an-apple-dep-device-from-intune"></a>Vyřazení zařízení Apple DEP z Intune

Pokud chcete zařízení Apple DEP zcela odebrat ze systému správy Intune, postupujte takto:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Zvolte **Zařízení** > **Všechna zařízení** > vyberte požadované zařízení > **Vyřazení**.
![Snímek obrazovky s akcí vyřazení](./media/devices-wipe/retire.png)
3. Navštivte [Business.Apple.com](http://business.apple.com) a vyhledejte zařízení podle jeho sériového čísla.
4. V nabídce **Přiřazeno** zvolte **Nepřiřazeno**.

5. Zvolte **Znovu přiřadit**.

    ![Snímek obrazovky opětovného přiřazení Apple](./media/devices-wipe/apple-reassign.png)

## <a name="device-states"></a>Stavy zařízení
Popis stavů zařízení najdete v [kolekci managementStates](../developer/intune-data-warehouse-collections.md#managementstates).

## <a name="fresh-start"></a>Nový Start

Platí pro zařízení s Windows 10. Přečtěte si další informace o [čerstvém startu](device-fresh-start.md).

## <a name="next-steps"></a>Další kroky

Pokud chcete znovu zaregistrovat odstraněné zařízení, najdete informace v tématu o [možnostech registrace](../enrollment/enrollment-options.md).

