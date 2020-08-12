---
title: Synchronizace aktualizací Microsoft 365 aplikací bez připojení k Internetu
titleSuffix: Configuration Manager
description: Synchronizuje aktualizace Microsoft 365 aplikací v bodu aktualizace softwaru nejvyšší úrovně, který je odpojený od Internetu.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a8fa7e7a-bf55-42de-b0c2-c56777dc1508
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 4739703436d7feec7c4c899e60b33d38ce28babf
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125725"
---
# <a name="synchronize-microsoft-365-apps-updates-from-a-disconnected-software-update-point"></a><a name="bkmk_O365"></a>Synchronizace aktualizací Microsoft 365ch aplikací z odpojeného bodu aktualizace softwaru

*Platí pro: Configuration Manager (Current Branch)*
<!--4065163-->
Configuration Manager počínaje verzí 2002 můžete pomocí nástroje importovat aktualizace Microsoft 365 aplikací ze serveru WSUS připojeného k Internetu do odpojeného Configuration Manager prostředí. Předtím, když jste exportovali a importovali metadata pro software aktualizovaný v odpojených prostředích, nemůžete nasadit aktualizace aplikací Microsoft 365. Aktualizace Microsoft 365 aplikací vyžadují další metadata stažená z rozhraní Office API a CDN, které není pro odpojená prostředí možné.

> [!Note]
> Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). V konzole Configuration Manager se pořád zobrazují odkazy na starý název a podpůrná dokumentace, zatímco se konzola aktualizuje.

## <a name="prerequisites"></a>Požadavky

- Server WSUS připojený k Internetu s minimálně Windows Serverem 2012.
- Server WSUS se musí připojit k těmto dvěma koncovým bodům Internetu:
   - `officecdn.microsoft.com`
   - `config.office.com`
- Zkopírujte nástroj OfflineUpdateExporter a jeho závislosti na server služby WSUS připojený k Internetu.
  - Nástroj a jeho závislosti jsou v adresáři ** &lt; ConfigMgrInstallDir>/Tools/offlineupdateexporter** .
- Uživatel, který nástroj spustil, musí být součástí skupiny **Správci služby WSUS** .
- Adresář vytvořený pro uložení Microsoft 365ch aktualizací metadat a obsah by měl mít vhodné seznamy řízení přístupu (ACL) k zabezpečení souborů.
    - Tento adresář musí být také prázdný.
- Data přesunovaná z online serveru WSUS do odpojeného prostředí by se měla bezpečně přesunout.

> [!IMPORTANT]
> Obsah bude stažen pro všechny jazyky Microsoft 365 aplikací. Každá aktualizace může mít přibližně 10 GB obsahu.

## <a name="synchronize-then-decline-unneeded-microsoft-365-apps-updates"></a>Synchronizovat a odmítat nepotřebné aktualizace Microsoft 365 aplikací

1. Na serveru WSUS připojené k Internetu otevřete konzolu služby WSUS.
1. Vyberte **možnost možnosti** **a produkty a klasifikace**.
1. Na kartě **produkty** vyberte **klienta Office 365** a na kartě **klasifikace** vyberte **aktualizace** . [ ![ produkty a klasifikace pro Microsoft 365 aktualizace aplikací ve službě WSUS](./media/4065163-o365-updates-product-classification.png)](./media/4065163-o365-updates-product-classification.png#lightbox)
1. Když přejdete na **synchronizace** a vyberete **synchronizovat** , získáte aktualizace Microsoft 365ch aplikací do WSUS.
1. Po dokončení synchronizace odmítněte všechny aktualizace Microsoft 365 aplikací, které nechcete nasadit pomocí Configuration Manager. Nemusíte schvalovat aktualizace aplikací Microsoft 365, aby je bylo možné stáhnout.  
   - Odmítání aktualizací nežádoucích Microsoft 365 aplikací ve službě WSUS nebrání jejich exportu během WsusUtil.exe exportu, ale nástroj OfflineUpdateExporter zastaví stahování obsahu pro tyto aplikace.
   - Nástroj OfflineUpdateExporter stahuje aktualizace aplikací Microsoft 365 za vás. Pokud exportujete aktualizace pro tyto produkty, budete je muset i nadále schvalovat ke stažení.
    - Vytvořte [nové zobrazení aktualizace ve službě WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/viewing-and-managing-updates#to-create-a-new-update-view-on-wsus) , abyste mohli snadno zobrazit a odmítnout nepotřebné aktualizace Microsoft 365 aplikací ve službě WSUS.
1. Pokud schvalujete jiné aktualizace produktů ke stažení a exportu, počkejte na dokončení stažení obsahu, než spustíte WsusUtil.exe export a zkopírování obsahu složky WSUSContent. Další informace najdete v tématu [synchronizace aktualizací softwaru z odpojeného bodu aktualizace softwaru](synchronize-software-updates-disconnected.md) .

## <a name="exporting-the-microsoft-365-apps-updates"></a>Export aktualizací Microsoft 365 Apps

1. Zkopírujte složku OfflineUpdateExporter z Configuration Manager na server služby WSUS připojený k Internetu.
    - Nástroj a jeho závislosti jsou v adresáři ** &lt; ConfigMgrInstallDir>/Tools/offlineupdateexporter** .
1. Z příkazového řádku na serveru WSUS připojeném k Internetu spusťte nástroj s následujícím použitím: **OfflineUpdateExporter.exe-O-D &lt; cílová cesta>**

   |Parametr OfflineUpdateExporter|Popis|
   |---|---|
   |**– O**|  **– Office**. Určuje produkt pro export aktualizací je Office 365 nebo aplikace Microsoft 365.|
   |**– D**|**– Cíl**. Cíl je povinný parametr a je nutná úplná cesta k cílové složce.|

   - Nástroj **OfflineUpdateExporter** provádí následující akce:
      - Připojí se ke službě WSUS.
      - Přečte metadata aktualizace Microsoft 365 Apps ve službě WSUS.
      - Stáhne obsah a veškerá další metadata potřebná pro Microsoft 365 aplikace se aktualizují do cílové složky.

1. Na příkazovém řádku na serveru WSUS připojeném k Internetu přejděte do složky, která obsahuje WsusUtil.exe. Ve výchozím nastavení se nástroj nachází ve složce%*ProgramFiles*% \ Update Services\Tools. Třeba pokud se nástroj nachází ve výchozím umístění, zadejte příkaz **cd %ProgramFiles%\Update Services\Tools**.
   - Pokud používáte Windows Server 2012, ujistěte se, že je na serverech WSUS nainstalovaný [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) .
   - Uživatel, který spouští nástroj WsusUtil, musí být členem místní skupiny Administrators na serveru.

1. Pro export metadat aktualizací softwaru do souboru GZIP zadejte následující text:  

    **WsusUtil.exe exportovat***soubor* s*balíčkem*      

    Například:  

    **WsusUtil.exe export export.xml. gz export. log**

1. Zkopírujte soubor **export.xml. gz** na server WSUS na nejvyšší úrovni v odpojené síti.
1. Pokud jste schválili aktualizace pro jiné produkty, zkopírujte obsah složky WSUSContent do složky WSUSContent odpojeného serveru WSUS, který je na nejvyšší úrovni.
1. Zkopírujte cílovou složku, která se používá pro **OfflineUpdateExporter** , do serveru lokality nejvyšší úrovně Configuration Manager v odpojené síti.

## <a name="import-the-microsoft-365-apps-updates"></a>Import aktualizací Microsoft 365 Apps

1. Na odpojeném serveru WSUS nejvyšší úrovně importujte metadata aktualizace z **export.xml. gz** , kterou jste vygenerovali na serveru WSUS připojeném k Internetu.
   
    Například:  

    **WsusUtil.exe import export.xml. gz importu. log**
    
    Ve výchozím nastavení se nástroj WsusUtil.exe nachází ve složce%*ProgramFiles*% \ Update Services\Tools.

1. Po dokončení importu budete muset nakonfigurovat vlastnost řízení lokality na odpojeném serveru Configuration Manager lokality nejvyšší úrovně. Tyto body změny konfigurace Configuration Manager k obsahu pro Microsoft 365 aplikace. Změna konfigurace vlastnosti:
   1. Zkopírujte [skript prostředí PowerShell O365OflBaseUrlConfigured](#bkmk_o365_script) na nejvyšší úroveň odpojeného serveru Configuration Manager lokality.
   1. Přejděte `"D:\Office365updates\content"` na úplnou cestu ke zkopírovanému adresáři, který obsahuje obsah aplikace Microsoft 365 Apps a metadata generovaná nástrojem OfflineUpdateExporter.
      > [!IMPORTANT]
      > Pouze místní cesty fungují pro vlastnost O365OflBaseUrlConfigured.
   1. Uložte skript jako`O365OflBaseUrlConfigured.ps1`
   1. Z okna PowerShellu se zvýšenými oprávněními na odpojené Configuration Manager serveru lokality na nejvyšší úrovni spusťte `.\O365OflBaseUrlConfigured.ps1` .
   1. Restartujte službu **SMS_Executive** na serveru lokality.
1. V konzole **Configuration Manager** přejděte na **Správa**  >  **Konfigurace lokality**  >  **lokality**.
1. Klikněte pravým tlačítkem myši na lokalitu nejvyšší úrovně a pak vyberte **Konfigurovat součásti lokality**  >  **bod aktualizace softwaru**.
1. Na kartě **klasifikace** vyberte *aktualizace*. Na kartě **produkty** vyberte *klienta Office 365*.
1. [Synchronizovat aktualizace softwaru](synchronize-software-updates.md#manually-start-software-updates-synchronization) pro Configuration Manager
1. Po dokončení synchronizace použijte běžný proces nasazení aktualizací aplikace Microsoft 365.

## <a name="proxy-configuration"></a><a name="bkmk_O365_ki"></a>Konfigurace proxy serveru

- Konfigurace proxy serveru není do nástroje nativně integrovaná. Pokud je proxy server nastaven v možnostech internetu na serveru, na kterém je nástroj spuštěný, v teorie se použije a musí fungovat správně.
   - Na příkazovém řádku spusťte příkaz, který `netsh winhttp show proxy` zobrazí nakonfigurovaný proxy server.



## <a name="modify-o365oflbaseurlconfigured-property"></a><a name="bkmk_o365_script"></a>Úprava vlastnosti O365OflBaseUrlConfigured

```powershell
# Name: O365OflBaseUrlConfigured.ps1
#
# Description: This sample sets the O365OflBaseUrlConfigured property for the SMS_WSUS_CONFIGURATION_MANAGER component on the top-level site.
# This script must be run on the disconnected top-level Configuration Manager site server
#
# Replace "D:\Office365updates\content" with the full path to the copied directory containing all the Office metadata and content generated by the OfflineUpdateExporter tool.
# Only local paths work for the O365OflBaseUrlConfigured property.

$PropertyValue = "D:\Office365updates\content"

# Don't change any of the lines below
$PropertyName = "O365OflBaseUrlConfigured"

# Get provider instance
$providerMachine = Get-WmiObject -namespace "root\sms" -class "SMS_ProviderLocation"

if($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = gwmi -ComputerName $providerMachine.Machine -namespace root\sms\site_$SiteCode -query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_WSUS_CONFIGURATION_MANAGER"'
$properties = $component.props

Write-host "Updating $PropertyName property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -eq $PropertyName) 
  {
    Write-host "Current value for $PropertyName is $($property.value2)"
    $property.value2 = $PropertyValue
    Write-host "Updating value for $PropertyName to $($property.value2)"
    break
  }
}

$component.props = $properties
$component.put()
```

## <a name="next-steps"></a>Další kroky

[Přidání aktualizací softwaru do skupiny aktualizací](../deploy-use/add-software-updates-to-an-update-group.md)