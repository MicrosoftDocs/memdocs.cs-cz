---
title: Bokem aplikací pro Windows a Windows Phone
titleSuffix: Microsoft Intune
description: Tady je postup, jak zaregistrovat obchodní aplikace, aby je bylo možné nasadit pomocí Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e44f1756-52e1-4ed5-bf7d-0e80363a8674
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: fc1a06f596ee5d700d30430e4fb2693138fe1e39
ms.sourcegitcommit: 441d0958721b6f9b6694dfffbec77c9a49929dd3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/08/2020
ms.locfileid: "80863141"
---
# <a name="sign-line-of-business-apps-so-they-can-be-deployed-to-windows-devices-with-intune"></a>Registrace obchodních aplikací, aby je bylo možné nasadit na zařízení s Windows pomocí Intune

Jako správce Intune můžete nasazovat obchodní aplikace (LOB) do Windows 8.1 plochy nebo Windows 10 Desktop & mobilní zařízení, včetně aplikace Portál společnosti. Pokud chcete nasadit aplikace *. appx* pro Windows 8.1 Desktop nebo Windows 10 Desktop & mobilní zařízení, můžete použít certifikát pro podepisování kódu od veřejné certifikační autority, která už je pro vaše zařízení s Windows důvěryhodná, nebo můžete použít vlastní certifikační autoritu.

 > [!NOTE]
 > Windows 8.1 Desktop vyžaduje pro povolení zkušebního načtení nebo použití klíčů pro zkušební načtení (automaticky povolených pro zařízení připojená k doméně) buď zásadu Enterprise. Další informace najdete v tématu [zkušební načtení systému Windows 8](https://blogs.technet.microsoft.com/scd-odtsp/2012/09/27/windows-8-sideloading-requirements-from-technet/).

## <a name="windows-10-sideloading"></a>Zkušební načtení Windows 10

Ve Windows 10 se zkušební verze liší od verze v dřívějších verzích Windows:

- Zařízení můžete odemknout pro zkušební načtení pomocí podnikových zásad. Intune poskytuje zásady konfigurace zařízení s názvem "instalace důvěryhodné aplikace". Tato možnost <allow> je potřebná pro zařízení, která už důvěřují certifikátu používanému k podepsání aplikace appx.

- Certifikáty Symantec Phone a licenční klíče pro zkušební načtení se nevyžadují. Pokud však není k dispozici místní certifikační autorita, může být nutné získat certifikát pro podpis kódu od veřejné certifikační autority. Další informace najdete v tématu [Úvod do podepisování kódu](https://docs.microsoft.com/windows/desktop/SecCrypto/cryptography-tools#introduction-to-code-signing).

### <a name="code-sign-your-app"></a>Podpis kódu vaší aplikace

Prvním krokem je podepsání vašeho balíčku appx vaším kódem. Podrobnosti najdete v tématu [podepsání balíčku aplikace pomocí nástroje SignTool](https://docs.microsoft.com/windows/uwp/packaging/sign-app-package-using-signtool).

### <a name="upload-your-app"></a>Nahrání aplikace

Dále je nutné nahrát podepsaný soubor appx. Podrobnosti najdete v tématu [Přidání obchodní aplikace pro Windows do Microsoft Intune](lob-apps-windows.md).

Pokud aplikaci nasadíte podle potřeby pro uživatele nebo zařízení, nepotřebujete aplikaci Inutne Portál společnosti. Pokud ale aplikaci nasadíte jako dostupnou pro uživatele, pak ji mohou použít Portál společnosti z veřejného Microsoft Store, použít aplikaci Portál společnosti z privátního Microsoft Store pro firmy nebo budete muset podepsat a ručně nasadit společnost Intune. Aplikace portálu

### <a name="upload-the-code-signing-certificate"></a>Nahrajte certifikát pro podpis kódu.

Pokud vaše zařízení s Windows 10 ještě nedůvěřuje certifikační autoritě, pak po podepsání balíčku appx a jeho nahrání do služby Intune je potřeba nahrát certifikát pro podepisování kódu na portál Intune:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Klikněte na **Správa tenanta** > **konektory a tokeny** > **Windows Enterprise certifcates**.
3. Vyberte soubor v **souboru certifikátu pro podpis kódu**.
4. Vyberte soubor *. cer* a klikněte na **otevřít**.
5. Kliknutím na **nahrát** přidejte soubor certifikátu do Intune.

Nyní jakékoli & mobilní zařízení s Windows 10 Desktop s nasazením appx službou Intune automaticky stáhne odpovídající podnikový certifikát a aplikace se bude moct spustit po instalaci.

Intune nasadí nejnovější soubor. CER, který se nahrál. Pokud máte více souborů appx vytvořených různými vývojáři, kteří nejsou přidruženi k vaší organizaci, budete je muset buď poskytnout nepodepsané soubory appx pro podepsání certifikátu, nebo jim poskytnout podpisový certifikát kódu, který používá. vaše organizace.

## <a name="how-to-renew-the-symantec-enterprise-code-signing-certificate"></a>Jak obnovit certifikát Symantec Enterprise pro podpis kódu

Certifikát použitý k nasazení mobilních aplikací Windows Phone 8,1 byl ukončený 28 2019 a již není k dispozici pro obnovení z Symantec. Pokud nasazujete na WIndows 10 Mobile, můžete dál používat certifikáty pro podepisování kódu Symantec Desktop Enterprise, a to podle pokynů pro [zkušební načtení Windows 10](app-sideload-windows.md#windows-10-sideloading) .

## <a name="how-to-install-the-updated-certificate-for-line-of-business-lob-apps"></a>Jak nainstalovat aktualizovaný certifikát pro obchodní aplikace

Windows Phone 8.1

Služba Intune už nemůže nasazovat obchodní aplikace pro tuto platformu, jakmile vyprší platnost existujícího certifikátu pro podpis kódu Symantec Mobile Enterprise. Pořád bude možné bokem nepodepsané soubory XAP/APPX pomocí karty SD nebo stažením souboru do zařízení. Další informace najdete v tématu [instalace souborů XAP na Windows Phone](https://answers.microsoft.com/en-us/mobiledevices/forum/mdlumia-mdapps/how-to-install-xap-file-in-windows-phone-8/da09ee72-51ae-407c-9b85-bc148df89280).

Windows 8.1 Desktop/Windows 10 Desktop & Mobile

Pokud vypršela doba platnosti certifikátu, může se stát, že se spustí spuštění souborů appx. Měli byste získat nový soubor. cer a postupovat podle pokynů pro podepsání kódu každého nasazeného souboru appx a znovu nahrát všechny soubory appx a aktualizovaný soubor. cer do oddílu Windows Enterprise Certificates na portálu Intune.

## <a name="manually-deploy-windows-10-company-portal-app"></a>Ruční nasazení aplikace Portál společnosti pro Windows 10

Pokud nechcete poskytnout přístup k Microsoft Store, můžete ručně nasadit aplikaci pro Windows 10 Portál společnosti přímo z Intune, i když službu Intune nemáte integrovanou s Microsoft Store for Business (MSFB). Případně, pokud máte integraci, můžete nasadit aplikaci Portál společnosti pomocí [nasazení aplikací pomocí nástroje MSFB](store-apps-windows.md).

 > [!NOTE]
 > Tato možnost vyžaduje, abyste ručně nasazovali aktualizace pokaždé, když je vydaná aktualizace aplikace.

1. Přihlaste se ke svému účtu v [Microsoft Store pro firmy](https://www.microsoft.com/business-store) a získejte verzi portál společnosti aplikace pro **offline licenci** .  
2. Jakmile aplikaci získáte, vyberte ji na stránce **Inventář**.  
3. Vyberte **Windows 10 – všechna zařízení** jako **platformu**, potom vyberte příslušnou **architekturu** a stahujte. Pro tuto aplikaci není nutné mít soubor s licencí aplikace.
   ![obrázek podrobností balíčku Windows 10 x86 pro stažení](./media/app-sideload-windows/Win10CP-all-devices.png)
4. Stáhněte všechny balíčky v části Požadované platformy. To je nutné provést pro architektury x86, x64, ARM a ARM64 – výsledkem je celkem 9 balíčků, jak je znázorněno níže.

   ![Obrázek souborů závislostí ke stažení ](./media/app-sideload-windows/Win10CP-dependent-files.png)
5. Než nahrajete aplikaci Portál společnosti do Intune, vytvořte složku (například C:&#92;Portál společnosti) s balíčky strukturovanými následovně:
   1. Umístěte balíček Portálu společnosti do složky C:\Portál společnosti. V tomto umístění vytvořte také podsložku Závislosti.  
      ![Obrázek složky Závislosti uložené se souborem APPXBUN](./media/app-sideload-windows/Win10CP-Dependencies-save.png)
   2. Umístěte devět balíčků závislostí do složky Závislosti.  
      Pokud nebudou závislosti umístěné v tomto formátu, Intune je při nahrávání balíčku nerozpozná a nenahraje a nahrávání se nezdaří s následující chybou.  
      <img alt="Error message - The Windows app dependency must be provided." src="./media/app-sideload-windows/Win10CP-error-message.png" width="200">
6. Vraťte se do Intune a nahrajte aplikaci Portál společnosti jako novou aplikaci. Nasaďte ji jako požadovanou aplikaci pro vybranou skupinu cílových uživatelů.  

Další informace o tom, jak Intune nakládá se závislostmi pro univerzální aplikace, najdete v článku [Deploying an appxbundle with dependencies via Microsoft Intune MDM](https://blogs.technet.microsoft.com/configmgrdogs/2016/11/30/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm/) (Nasazení souboru appxbundle se závislostmi prostřednictvím Microsoft Intune MDM).  

### <a name="how-do-i-update-the-company-portal-on-my-users-devices-if-they-have-already-installed-the-older-apps-from-the-store"></a>Jak mám aktualizovat Portál společnosti na zařízeních uživatelů, pokud si už nainstalovali starší aplikace ze Storu?

Pokud si uživatelé nainstalovali aplikace Portál společnosti pro Windows 8.1 nebo Windows Phone 8.1 ze Storu, měly by se tyto aplikace automaticky aktualizovat na novou verzi. Není tedy třeba provádět žádnou akci. Pokud k aktualizaci nedojde, požádejte uživatele, aby zkontrolovali, jestli mají na svých zařízeních povolené automatické aktualizace pro aplikace ze Storu.

### <a name="how-do-i-upgrade-my-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>Jak mám upgradovat aplikaci Portál společnosti pro Windows 8.1 nainstalovanou bokem na aplikaci Portál společnosti pro Windows 10?

Doporučujeme následující způsob migrace – odstraňte nasazení pro aplikaci Portál společnosti pro Windows 8.1 nastavením akce nasazení na možnost Odinstalovat. Až to provedete, můžete aplikaci Portál společnosti pro Windows 10 nasadit některým z výše uvedených způsobů.  

Pokud potřebujete aplikaci nainstalovat bokem a nasadili jste Portál společnosti pro Windows 8.1 bez podepisování certifikátem Symantec, postupujte podle pokynů ve výše uvedené části věnované přímému nasazení prostřednictvím Intune a proveďte upgrade.

Pokud potřebujete aplikaci nainstalovat bokem a Portál společnosti pro Windows 8.1 jste podepsali a nasadili prostřednictvím certifikátu Symantec pro podepisování kódu, postupujte podle pokynů v níže uvedené části.  

### <a name="how-do-i-upgrade-my-signed-and-sideloaded-windows-phone-81-company-portal-app-or-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>Jak mám upgradovat podepsanou a bokem nainstalovanou aplikaci Portál společnosti pro Windows Phone 8.1 nebo aplikaci Portál společnosti pro Windows 8.1 na aplikaci Portál společnosti pro Windows 10?

Doporučujeme následující způsob migrace – odstraňte existující nasazení pro aplikaci Portál společnosti pro Windows Phone 8.1 nebo aplikaci Portál společnosti pro Windows 8.1 nastavením akce nasazení na možnost Odinstalovat. Až to provedete, můžete aplikaci Portál společnosti pro Windows 10 nasadit normálním způsobem.  

Jinak musí být aplikace Portál společnosti pro Windows 10 náležitě aktualizovaná a podepsaná, abyste dodrželi patřičný způsob upgradu.  

Pokud je aplikace Portál společnosti pro Windows 10 podepsaná a nasazená tímto způsobem, budete muset tento proces opakovat pro každou novou aktualizaci aplikace, až bude ve Storu k dispozici. Aplikace se při aktualizaci Storu automaticky neaktualizuje.  

Aplikaci můžete tímto způsobem podepsat a nasadit takto:

1. Z webu [https://aka.ms/win10cpscript](https://aka.ms/win10cpscript) si stáhněte podepisovací skript Microsoft Intune pro aplikaci Portál společnosti pro Windows 10.  Tento skript vyžaduje, aby na hostitelském počítači byla nainstalovaná sada Windows SDK pro Windows 10. Sadu Windows SDK pro Windows 10 si můžete stáhnout z webu [https://go.microsoft.com/fwlink/?LinkId=619296](https://go.microsoft.com/fwlink/?LinkId=619296).
2. Stáhněte si aplikaci Portál společnosti pro Windows 10 z Microsoft Storu pro firmy (podrobnosti jsou uvedené výše).  
3. Spusťte skript se vstupními parametry popsanými v hlavičce skriptu, abyste podepsali aplikaci Portál společnosti pro Windows 10 (extrahovanou níže). Závislosti není nutné do skriptu předávat. Jsou vyžadované jenom v případě, když aplikaci nahráváte do konzoly pro správu Intune.

|       Parametr       |                                                                    Popis                                                                    |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| InputWin10AppxBundle  |                                             Cesta k umístění zdrojového souboru appxbundle                                              |
| OutputWin10AppxBundle |                                                  Výstupní cesta pro podepsaný soubor appxbundle                                                  |
|       Win81Appx       |                          Cesta k umístění souboru Portálu společnosti pro Windows 8.1 nebo Windows Phone 8.1 (.APPX)                           |
|      PfxFilePath      |                                   Cesta k souboru certifikátu Symantec Enterprise Mobile Code Signing Certificate (.PFX)                                    |
|      PfxPassword      |                                     Heslo certifikátu Symantec Enterprise Mobile Code Signing Certificate                                      |
|      PublisherId      |      ID vydavatele dané organizace. Pokud chybí, použije se pole Subject certifikátu Symantec Enterprise Mobile Code Signing Certificate.       |
|        SdkPath        | Cesta ke kořenové složce sady Windows SDK pro Windows 10. Tento argument je volitelný a jeho výchozí hodnota je ${env:ProgramFiles(x86)}\Windows Kits\10. |

Po ukončení běhu tohoto skriptu bude jeho výstupem podepsaná verze aplikace Portál společnosti pro Windows 10. Potom můžete podepsanou verzi aplikace nasadit jako obchodní aplikaci prostřednictvím Intune. Tím se aktuálně nasazené verze upgradují na tuto novou aplikaci.  
