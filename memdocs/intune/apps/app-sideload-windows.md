---
title: Instalace aplikací pro Windows bokem
titleSuffix: Microsoft Intune
description: Tady je postup, jak zaregistrovat obchodní aplikace, aby je bylo možné nasadit pomocí Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e44f1756-52e1-4ed5-bf7d-0e80363a8674
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: da43cab373021107a940ce0bd71c0f4986d5e907
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179617"
---
# <a name="sign-line-of-business-apps-so-they-can-be-deployed-to-windows-devices-with-intune"></a>Registrace obchodních aplikací, aby je bylo možné nasadit na zařízení s Windows pomocí Intune

Jako správce Intune můžete nasazovat obchodní aplikace (LOB) do Windows 8.1 plochy nebo Windows 10 Desktop & mobilní zařízení, včetně aplikace Portál společnosti. Pokud chcete nasadit aplikace *. appx* pro Windows 8.1 Desktop nebo Windows 10 Desktop & mobilní zařízení, můžete použít certifikát pro podepisování kódu od veřejné certifikační autority, která už je pro vaše zařízení s Windows důvěryhodná, nebo můžete použít vlastní certifikační autoritu.

 > [!NOTE]
 > Windows 8.1 Desktop vyžaduje pro povolení zkušebního načtení nebo použití klíčů pro zkušební načtení (automaticky povolených pro zařízení připojená k doméně) buď zásadu Enterprise. Další informace najdete v tématu [zkušební načtení systému Windows 8](https://blogs.technet.microsoft.com/scd-odtsp/2012/09/27/windows-8-sideloading-requirements-from-technet/).

## <a name="windows-10-sideloading"></a>Zkušební načtení Windows 10

Ve Windows 10 se zkušební verze liší od verze v dřívějších verzích Windows:

- Zařízení můžete odemknout pro zkušební načtení pomocí podnikových zásad. Intune poskytuje zásady konfigurace zařízení s názvem "instalace důvěryhodné aplikace". Tato možnost <allow> je nutná pro zařízení, která již důvěřují certifikátu používanému k podepsání aplikace appx.

- Certifikáty Symantec Phone a licenční klíče pro zkušební načtení se nevyžadují. Pokud však není k dispozici místní certifikační autorita, může být nutné získat certifikát pro podpis kódu od veřejné certifikační autority. Další informace najdete v tématu [Úvod do podepisování kódu](https://docs.microsoft.com/windows/desktop/SecCrypto/cryptography-tools#introduction-to-code-signing).

### <a name="code-sign-your-app"></a>Podpis kódu vaší aplikace

Prvním krokem je podepsání vašeho balíčku appx vaším kódem. Podrobnosti najdete v tématu [podepsání balíčku aplikace pomocí nástroje SignTool](https://docs.microsoft.com/windows/uwp/packaging/sign-app-package-using-signtool).

### <a name="upload-your-app"></a>Nahrání aplikace

Dále je nutné nahrát podepsaný soubor appx. Podrobnosti najdete v tématu [Přidání obchodní aplikace pro Windows do Microsoft Intune](lob-apps-windows.md).

Pokud aplikaci nasadíte podle potřeby pro uživatele nebo zařízení, nepotřebujete aplikaci Inutne Portál společnosti. Pokud ale aplikaci nasadíte jako dostupnou pro uživatele, pak ji mohou použít Portál společnosti z veřejného Microsoft Store, použít aplikaci Portál společnosti z privátního Microsoft Store pro firmy nebo budete muset aplikaci Portál společnosti Intune podepsat a ručně nasadit.

### <a name="upload-the-code-signing-certificate"></a>Nahrajte certifikát pro podpis kódu.

Pokud vaše zařízení s Windows 10 ještě nedůvěřuje certifikační autoritě, pak po podepsání balíčku appx a jeho nahrání do služby Intune je potřeba nahrát certifikát pro podepisování kódu na portál Intune:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Klikněte na možnost konektory **pro správu tenanta**  >  **a tokeny**pro  >  **certifikáty systému Windows Enterprise**.
3. Vyberte soubor v **souboru certifikátu pro podpis kódu**.
4. Vyberte soubor *. cer* a klikněte na **otevřít**.
5. Kliknutím na **nahrát** přidejte soubor certifikátu do Intune.

Nyní jakékoli & mobilní zařízení s Windows 10 Desktop s nasazením appx službou Intune automaticky stáhne odpovídající podnikový certifikát a aplikace se bude moct spustit po instalaci.

Intune nasadí nejnovější soubor. CER, který se nahrál. Pokud máte více souborů appx vytvořených různými vývojáři, kteří nejsou přidruženi k vaší organizaci, budete je muset buď poskytnout nepodepsané soubory appx pro podepsání certifikátu, nebo jim poskytnout podpisový certifikát kódu, který používá vaše organizace.

## <a name="how-to-renew-the-symantec-enterprise-code-signing-certificate"></a>Jak obnovit certifikát Symantec Enterprise pro podpis kódu

Certifikát použitý k nasazení mobilních aplikací Windows Phone 8,1 byl ukončený 28 2019 a již není k dispozici pro obnovení z Symantec. Intune také ukončil podporu pro Windows 10 Mobile od 10. srpna 2020.

## <a name="how-to-install-the-updated-certificate-for-line-of-business-lob-apps"></a>Jak nainstalovat aktualizovaný certifikát pro obchodní aplikace

Windows Phone 8.1

Služba Intune už nemůže nasazovat obchodní aplikace pro tuto platformu, jakmile vyprší platnost existujícího certifikátu pro podpis kódu Symantec Mobile Enterprise.

Windows 8.1 Desktop/Windows 10 Desktop & Mobile

Pokud vypršela doba platnosti certifikátu, může se stát, že se spustí spuštění souborů appx. Měli byste získat nový soubor. cer a postupovat podle pokynů pro podepsání kódu každého nasazeného souboru appx a znovu nahrát všechny soubory appx a aktualizovaný soubor. cer do oddílu Windows Enterprise Certificates na portálu Intune.

## <a name="manually-deploy-windows-10-company-portal-app"></a>Ruční nasazení aplikace Portál společnosti pro Windows 10

Pokud nechcete poskytnout přístup k Microsoft Store, můžete ručně nasadit aplikaci pro Windows 10 Portál společnosti přímo z Intune, i když službu Intune nemáte integrovanou s Microsoft Store for Business (MSFB). Případně, pokud máte integraci, můžete nasadit aplikaci Portál společnosti pomocí [nasazení aplikací pomocí nástroje MSFB](store-apps-windows.md).

 > [!NOTE]
 > Tato možnost vyžaduje, abyste ručně nasazovali aktualizace pokaždé, když je vydaná aktualizace aplikace.

1. Přihlaste se ke svému účtu v [Microsoft Store pro firmy](https://www.microsoft.com/business-store) a získejte verzi portál společnosti aplikace pro **offline licenci** .  
2. Jakmile aplikaci získáte, vyberte ji na stránce **Inventář**.  
3. Vyberte **Windows 10 – všechna zařízení** jako **platformu**, potom vyberte příslušnou **architekturu** a stahujte. Pro tuto aplikaci není nutné mít soubor s licencí aplikace.
   ![Obrázek podrobností balíčku Windows 10 x86 ke stažení](./media/app-sideload-windows/Win10CP-all-devices.png)
4. Stáhněte si všechny balíčky v části "požadované architektury". To je nutné provést pro architektury x86, x64, ARM a ARM64 – výsledkem je celkem 9 balíčků, jak je znázorněno níže.

   ![Obrázek souborů závislostí ke stažení ](./media/app-sideload-windows/Win10CP-dependent-files.png)
5. Než nahrajete aplikaci Portál společnosti do Intune, vytvořte složku (například C:&#92;Portál společnosti) s balíčky strukturovanými následovně:
   1. Umístěte balíček Portálu společnosti do složky C:\Portál společnosti. V tomto umístění vytvořte také podsložku Závislosti.  
      ![Obrázek složky Závislosti uložené se souborem APPXBUN](./media/app-sideload-windows/Win10CP-Dependencies-save.png)
   2. Umístěte devět balíčků závislostí do složky Závislosti.  
      Pokud nebudou závislosti umístěné v tomto formátu, Intune je při nahrávání balíčku nerozpozná a nenahraje a nahrávání se nezdaří s následující chybou.  
      <img alt="Error message - The Windows app dependency must be provided." src="./media/app-sideload-windows/Win10CP-error-message.png" width="200">
6. Vraťte se do Intune a nahrajte aplikaci Portál společnosti jako novou aplikaci. Nasaďte ji jako požadovanou aplikaci pro vybranou skupinu cílových uživatelů.  

Další informace o tom, jak Intune nakládá se závislostmi pro univerzální aplikace, najdete v článku [Deploying an appxbundle with dependencies via Microsoft Intune MDM](https://blogs.technet.microsoft.com/configmgrdogs/2016/11/30/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm/) (Nasazení souboru appxbundle se závislostmi prostřednictvím Microsoft Intune MDM).  

### <a name="how-do-i-update-the-company-portal-on-my-users-devices-if-they-have-already-installed-the-older-apps-from-the-store"></a>Návody aktualizovat Portál společnosti na zařízeních uživatelů, pokud už nainstalovaly starší aplikace z obchodu?

Pokud už vaši uživatelé nainstalovali Windows 8.1 Portál společnosti aplikace ze Storu, pak by se měly automaticky aktualizovat na novou verzi bez nutnosti zásahu uživatele nebo vašeho uživatele. Pokud k aktualizaci nedojde, požádejte uživatele, aby zkontrolovali, jestli mají na svých zařízeních povolené automatické aktualizace pro aplikace ze Storu.

### <a name="how-do-i-upgrade-my-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>Jak mám upgradovat aplikaci Portál společnosti pro Windows 8.1 nainstalovanou bokem na aplikaci Portál společnosti pro Windows 10?

Náš doporučený postup migrace je odstranění nasazení pro aplikaci Windows 8.1 Portál společnosti nastavením akce nasazení na možnost odinstalovat. Až to provedete, můžete aplikaci Portál společnosti pro Windows 10 nasadit některým z výše uvedených způsobů.  

Pokud potřebujete aplikaci nainstalovat bokem a nasadili jste Portál společnosti pro Windows 8.1 bez podepisování certifikátem Symantec, postupujte podle pokynů ve výše uvedené části věnované přímému nasazení prostřednictvím Intune a proveďte upgrade.

Pokud potřebujete aplikaci nainstalovat bokem a Portál společnosti pro Windows 8.1 jste podepsali a nasadili prostřednictvím certifikátu Symantec pro podepisování kódu, postupujte podle pokynů v níže uvedené části.  

### <a name="how-do-i-upgrade-my-signed-and-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>Návody Windows 8.1 Portál společnosti aplikaci upgradovat na Portál společnosti aplikaci pro Windows 10?

Náš doporučený postup migrace je odstranit existující nasazení pro aplikaci Windows 8.1 Portál společnosti nastavením akce nasazení na možnost odinstalovat. Až to provedete, můžete aplikaci Portál společnosti pro Windows 10 nasadit normálním způsobem.  

Jinak musí být aplikace Portál společnosti pro Windows 10 náležitě aktualizovaná a podepsaná, abyste dodrželi patřičný způsob upgradu.  

Pokud je aplikace Portál společnosti pro Windows 10 podepsaná a nasazená tímto způsobem, budete muset tento proces opakovat pro každou novou aktualizaci aplikace, až bude ve Storu k dispozici. Aplikace se při aktualizaci Storu automaticky neaktualizuje.  

Tímto způsobem můžete aplikaci podepsat a nasadit takto:

1. Stáhněte si Portál společnosti podpisový skript aplikace Microsoft Intune Windows 10 [https://aka.ms/win10cpscript](https://aka.ms/win10cpscript) .  Tento skript vyžaduje, aby na hostitelském počítači byla nainstalovaná sada Windows SDK pro Windows 10. Pokud si chcete stáhnout Windows SDK pro Windows 10, přejděte na [https://go.microsoft.com/fwlink/?LinkId=619296](https://go.microsoft.com/fwlink/?LinkId=619296) .
2. Stáhněte si aplikaci Portál společnosti pro Windows 10 z Microsoft Storu pro firmy (podrobnosti jsou uvedené výše).  
3. Spusťte skript se vstupními parametry popsanými v hlavičce skriptu, abyste podepsali aplikaci Portál společnosti pro Windows 10 (extrahovanou níže). Závislosti není nutné do skriptu předávat. Jsou vyžadované jenom v případě, když aplikaci nahráváte do konzoly pro správu Intune.

|       Parametr       |                                                                    Popis                                                                    |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| InputWin10AppxBundle  |                                             Cesta k umístění zdrojového souboru appxbundle                                              |
| OutputWin10AppxBundle |                                                  Výstupní cesta pro podepsaný soubor appxbundle                                                  |
|       Win81Appx       |                          Cesta k umístění Windows 8.1 Portál společnosti (. APPX) se nachází.                           |
|      PfxFilePath      |                                   Cesta k souboru certifikátu Symantec Enterprise Mobile Code Signing Certificate (.PFX)                                    |
|      PfxPassword      |                                     Heslo certifikátu Symantec Enterprise Mobile Code Signing Certificate                                      |
|      PublisherId      |      ID vydavatele dané organizace. Pokud chybí, použije se pole Subject certifikátu Symantec Enterprise Mobile Code Signing Certificate.       |
|        SdkPath        | Cesta ke kořenové složce sady Windows SDK pro Windows 10. Tento argument je volitelný a jeho výchozí hodnota je ${env:ProgramFiles(x86)}\Windows Kits\10. |

Po ukončení běhu tohoto skriptu bude jeho výstupem podepsaná verze aplikace Portál společnosti pro Windows 10. Potom můžete podepsanou verzi aplikace nasadit jako obchodní aplikaci prostřednictvím Intune. Tím se aktuálně nasazené verze upgradují na tuto novou aplikaci.  
