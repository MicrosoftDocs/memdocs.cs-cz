---
title: Ruční přidání aplikace Portál společnosti pro Windows 10
titleSuffix: Microsoft Intune
description: Přečtěte si, jak vaše zaměstnanci můžou ručně přidat Portál společnosti aplikaci pro Windows 10 do svého počítače z Microsoft Store.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: bfe1a2d3-f611-4dbb-adef-c0dff4d7b810
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c658176046fca5dfc8cda1a3c655e32150a7d9c7
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326787"
---
# <a name="add-the-windows-10-company-portal-app-by-using-microsoft-intune"></a>Přidání aplikace Portál společnosti s Windows 10 pomocí Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Vaši uživatelé si mohou nainstalovat aplikaci Portál společnosti sami z Microsoft Storu, aby mohli spravovat zařízení a instalovat aplikace. Pokud vaše obchodní potřeby vyžadují, abyste jim přidělili Portál společnosti aplikaci, můžete aplikaci Portál společnosti pro Windows 10 přiřadit přímo z Intune. Můžete to udělat i v případě, že se Intune Neintegruje s Microsoft Store pro firmy.

 > [!IMPORTANT]
 > Pokud si stáhnete aplikaci Portál společnosti, možnost popsanou v tomto článku vyžaduje, abyste při každém vydání aktualizace aplikace přiřadili ruční aktualizace. Postup nasazení Portál společnosti aplikace pro zařízení s autopilotem s Windows 10, která se zřídí, najdete v tématu [Přidání zařízení s Windows 10 portál společnosti autopilotování aplikací](store-apps-company-portal-autopilot.md).

## <a name="configure-settings-to-show-offline-apps"></a>Konfigurace nastavení k zobrazení offline aplikací
1. Přihlaste se k [Microsoft Storu pro firmy](https://www.microsoft.com/business-store) pomocí svého účtu správce.
2. Vyberte kartu **Spravovat** v horní části okna.
3. V levém podokně vyberte **Nastavení**.
4. V části **Prostředí nakupování** nastavte **Zobrazovat offline aplikace** na **Zapnuto**.  
    Zobrazí se aplikace licencované offline.

## <a name="download-the-offline-company-portal-app"></a>Stažení offline aplikace Portál společnosti
1. Vyhledejte a vyberte aplikaci **Portál společnosti**.
2. Nastavte **Typ licence** na **Offline**.
3. Výběrem možnosti **Získat aplikaci** offline aplikaci Portál společnosti získejte a přidejte do svého inventáře.
4. Na stránce aplikace **Portál společnosti** vyberte **Spravovat**.
5. Jako **Platformu** vyberte **Windows 10 – všechna zařízení**, potom vyberte příslušné hodnoty **Minimální verze**, **Architektury** a **Stáhnout metadata aplikace**. 
6. V části **Podrobnosti balíčku** vyberte **Stáhnout** a uložte soubor do místního počítače.

    ![Je vybraná možnost zařízení s Windows 10, kde se používá architektura x86.](./media/app-sideload-windows/Win10CP-all-devices.png)

7. Stáhněte si všechny balíčky v části "požadované architektury" výběrem možnosti **Stáhnout**.  

    Tuto akci je nutné provést pro architektury x86, x64 a ARM:<br> 
    *V případě, že při výběru 1607 použijete 1507 jako minimální verzi operačního systému, 12 balíčků při výběru 1511 a 15 balíčků, jsou k dispozici 9 požadovaných balíčků rozhraní.*

8. V Microsoft Intune na portálu Azure Portal nahrajte aplikaci Portál společnosti jako novou aplikaci. Aplikaci přidáte tak, že jako **Typ aplikace** v podokně **Vybrat typ aplikace** vyberete obchodní aplikace. Pak vyberte soubor balíčku aplikace (přípona. AppxBundle).

9. V části **Vybrat soubory aplikací závislosti** vyberte všechny závislosti, které jste stáhli v kroku 7, kliknutím na tlačítko Shift a ověřte, zda se v **přidaném** sloupci zobrazí **Ano** pro architektury, které potřebujete.

     > [!NOTE]
     > Pokud se závislosti nepřidaly, nemusí se aplikace nainstalovat na zadané typy zařízení.

10. Klikněte na **OK**, zadejte požadované **informace o aplikaci**a klikněte na **Přidat**.

11. Přiřaďte aplikaci Portál společnosti jako požadovanou aplikaci pro vybranou skupinu uživatelů nebo zařízení.  

Další informace o tom, jak Intune nakládá se závislostmi pro univerzální aplikace, najdete v článku [Deploying an appxbundle with dependencies via Microsoft Intune MDM](https://blogs.technet.microsoft.com/configmgrdogs/2016/11/30/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm/) (Nasazení souboru appxbundle se závislostmi prostřednictvím Microsoft Intune MDM).  

## <a name="frequently-asked-questions"></a>Nejčastější dotazy 
### <a name="how-do-i-update-the-company-portal-app-on-my-users-devices-if-they-have-already-installed-the-older-apps-from-the-store"></a>Návody aktualizovat aplikaci Portál společnosti na zařízeních uživatelů, pokud už nainstalovala starší aplikace ze Storu?
Pokud si uživatelé nainstalovali aplikace Portál společnosti pro Windows 8.1 nebo Windows Phone 8.1 z Microsoft Storu, měly by se tyto aplikace automaticky aktualizovat na nejnovější verzi. Není tedy třeba provádět žádnou akci. Pokud k aktualizaci nedojde, požádejte uživatele, aby zkontrolovali, jestli mají na svých zařízeních povolené automatické aktualizace pro aplikace ze Storu.   

### <a name="how-do-i-upgrade-my-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>Jak mám upgradovat aplikaci Portál společnosti pro Windows 8.1 nainstalovanou bokem na aplikaci Portál společnosti pro Windows 10?
Doporučujeme následující způsob migrace – odstraňte přiřazení aplikace Portál společnosti pro Windows 8.1 nastavením akce přiřazení na možnost **Odinstalovat**. Po výběru tohoto nastavení můžete přiřadit aplikaci Portál společnosti pro Windows 10 prostřednictvím některé ze zmíněných možností.  

Pokud potřebujete aplikaci nainstalovat bokem a Portál společnosti pro Windows 8.1 jste přiřadili bez podepsání certifikátem Symantec, dokončete upgrade podle pokynů v předchozích částech tohoto článku.

Pokud potřebujete aplikaci nainstalovat bokem a aplikaci Portál společnosti pro Windows 8.1 jste podepsali a přiřadili prostřednictvím certifikátu Symantec pro podepisování kódu, postupujte podle pokynů v následující části.

### <a name="how-do-i-upgrade-my-signed-and-sideloaded-windows-phone-81-company-portal-app-or-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>Jak mám upgradovat podepsanou a bokem nainstalovanou aplikaci Portál společnosti pro Windows Phone 8.1 nebo aplikaci Portál společnosti pro Windows 8.1 na aplikaci Portál společnosti pro Windows 10?
Doporučujeme následující způsob migrace – odstraňte existující přiřazení aplikace Portál společnosti pro Windows Phone 8.1 nebo aplikace Portál společnosti pro Windows 8.1 nastavením akce přiřazení na možnost **Odinstalovat**. Po výběru tohoto nastavení můžete aplikaci Portál společnosti pro Windows 10 přiřadit běžným způsobem.  

Jinak musí být aplikace Portál společnosti pro Windows 10 náležitě aktualizovaná a podepsaná, abyste dodrželi patřičný způsob upgradu.  

Pokud aplikaci Portál společnosti pro Windows 10 podepíšete a přiřadíte tímto způsobem, budete muset tento proces opakovat pro každou novou aktualizaci aplikace, až bude ve Storu k dispozici. Aplikace se při aktualizaci Storu automaticky neaktualizuje.  

Tímto způsobem podepisujete a přiřadíte aplikaci:

1. Stáhněte si [podepisovací skript Microsoft Intune pro aplikaci Portál společnosti pro Windows 10](https://aka.ms/win10cpscript).  
    Tento skript vyžaduje, aby na hostitelském počítači byla nainstalovaná sada Windows SDK pro Windows 10. [Stáhněte si sadu Windows SDK pro Windows 10](https://go.microsoft.com/fwlink/?LinkId=619296).
2. Stáhněte si aplikaci Portál společnosti pro Windows 10 z Microsoft Storu pro firmy, jak je popsáno v předchozích částech.  
3. Pokud chcete podepsat aplikaci Portál společnosti pro Windows 10, spusťte skript se vstupními parametry popsanými v hlavičce skriptu, jak je uvedeno v následující tabulce.  
    Závislosti není nutné do skriptu předávat. Jsou vyžadované jenom v případě, že aplikaci nahráváte do konzoly pro správu Intune.

| Parametr |  Popis  |
|---|---|
| InputWin10AppxBundle  |  Cesta ke zdrojovému souboru appxbundle |
| OutputWin10AppxBundle | Výstupní cesta pro podepsaný soubor appxbundle 
| Win81Appx  | Cesta k souboru Portálu společnosti pro Windows 8.1 nebo Windows Phone 8.1 (.APPX) |
| PfxFilePath  |  Cesta k souboru certifikátu Symantec Enterprise Mobile Code Signing Certificate (.PFX)  |
| PfxPassword  | Heslo certifikátu Symantec Enterprise Mobile Code Signing Certificate |
| PublisherId | ID vydavatele dané organizace. Pokud chybí, použije se pole Subject certifikátu Symantec Enterprise Mobile Code Signing Certificate. |
| SdkPath | Cesta ke kořenové složce sady Windows SDK pro Windows 10. Tento argument je volitelný a jeho výchozí hodnota je ${env:ProgramFiles(x86)}\Windows Kits\10.  |

Po dokončení běhu tohoto skriptu bude jeho výstupem podepsaná verze aplikace Portál společnosti pro Windows 10. Potom můžete podepsanou verzi aplikace přiřadit jako obchodní aplikaci přes Intune. Tím se aktuálně přiřazené verze upgradují na tuto novou aplikaci.  

## <a name="next-steps"></a>Další kroky

- [Přiřazení aplikací skupinám](apps-deploy.md)

