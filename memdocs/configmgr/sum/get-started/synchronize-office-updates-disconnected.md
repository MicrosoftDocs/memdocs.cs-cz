---
title: Synchronizace aktualizací Office 365 bez připojení k Internetu
titleSuffix: Configuration Manager
description: Synchronizuje aktualizace Office 365 v bodu aktualizace softwaru nejvyšší úrovně, který je odpojený od Internetu.
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a8fa7e7a-bf55-42de-b0c2-c56777dc1508
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 3627d2f7772b7b9e133d742b0ee4f94dba6e457a
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110351"
---
# <a name="synchronize-office-365-updates-from-a-disconnected-software-update-point"></a><a name="bkmk_O365"></a>Synchronizace aktualizací Office 365 z odpojeného bodu aktualizace softwaru

*Platí pro: Configuration Manager (Current Branch)*
<!--4065163-->
Configuration Manager počínaje verzí 2002 můžete pomocí nástroje importovat aktualizace Office 365 ze serveru WSUS připojeného k Internetu do odpojeného Configuration Manager prostředí. Dříve, když jste exportovali a importovali metadata pro software aktualizovaný v odpojených prostředích, nemůžete nasadit aktualizace Office 365. Aktualizace Office 365 vyžadují další metadata stažená z rozhraní Office API a CDN Office, což není u odpojených prostředí možné.

> [!Note]
> Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). V konzole Configuration Manager se pořád zobrazují odkazy na starý název a podpůrná dokumentace, zatímco se konzola aktualizuje.

## <a name="prerequisites"></a>Požadavky

- Server WSUS připojený k Internetu s minimálně Windows Serverem 2012.
- Server WSUS se musí připojit k těmto dvěma koncovým bodům Internetu:
   - `officecdn.microsoft.com`
   - `config.office.com`
- Zkopírujte nástroj OfflineUpdateExporter a jeho závislosti na server služby WSUS připojený k Internetu.
  - Nástroj a jeho závislosti jsou v adresáři ** &lt;ConfigMgrInstallDir>/Tools/offlineupdateexporter** .
- Uživatel, který nástroj spustil, musí být součástí skupiny **Správci služby WSUS** .
- Adresář vytvořený pro uložení metadat a obsahu aktualizace Office by měl mít odpovídající seznamy řízení přístupu (ACL) k zabezpečení souborů.
    - Tento adresář musí být také prázdný.
- Data přesunovaná z online serveru WSUS do odpojeného prostředí by se měla bezpečně přesunout.

> [!IMPORTANT]
> Obsah bude stažen pro všechny jazyky Office 365. Každá aktualizace může mít přibližně 10 GB obsahu.

## <a name="synchronize-then-decline-unneeded-office-365-updates"></a>Synchronizovat a odmítat nepotřebné aktualizace Office 365

1. Na serveru WSUS připojené k Internetu otevřete konzolu služby WSUS.
1. Vyberte **možnost možnosti** **a produkty a klasifikace**.
1. Na kartě **produkty** vyberte **klienta Office 365** a na kartě **klasifikace** vyberte **aktualizace** . [ ![produkty a klasifikace pro aktualizace sady Office 365 ve službě WSUS](./media/4065163-o365-updates-product-classification.png)](./media/4065163-o365-updates-product-classification.png#lightbox)
1. Pokud chcete aktualizace Office 365 stáhnout do WSUS, klikněte na **synchronizace** a vyberte **synchronizovat** .
1. Po dokončení synchronizace odmítněte všechny aktualizace Office 365, které nechcete nasadit, pomocí Configuration Manager. Nemusíte schvalovat aktualizace Office 365, aby je bylo možné stáhnout.  
   - Odmítnutí nechtěných aktualizací Office 365 ve službě WSUS neukončí jejich export během exportu WsusUtil. exe, ale zastaví nástroj OfflineUpdateExporter ze stahování obsahu pro ně.
   - Nástroj OfflineUpdateExporter provede stažení aktualizací Office 365. Pokud exportujete aktualizace pro tyto produkty, budete je muset i nadále schvalovat ke stažení.
    - Vytvořte [nové zobrazení aktualizace ve službě WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/viewing-and-managing-updates#to-create-a-new-update-view-on-wsus) , abyste mohli snadno zobrazit a odmítnout nepotřebné aktualizace Office 365 ve službě WSUS.
1. Pokud schvalujete jiné aktualizace produktů ke stažení a exportu, počkejte na dokončení stažení obsahu před spuštěním WsusUtil. exe export a zkopírování obsahu složky WSUSContent. Další informace najdete v tématu [synchronizace aktualizací softwaru z odpojeného bodu aktualizace softwaru](synchronize-software-updates-disconnected.md) .

## <a name="exporting-the-office-365-updates"></a>Exportují se aktualizace Office 365.

1. Zkopírujte složku OfflineUpdateExporter z Configuration Manager na server služby WSUS připojený k Internetu.
    - Nástroj a jeho závislosti jsou v adresáři ** &lt;ConfigMgrInstallDir>/Tools/offlineupdateexporter** .
1. Z příkazového řádku na serveru WSUS připojeném k Internetu spusťte nástroj s následujícím použitím: **OfflineUpdateExporter. exe-O-D &lt;cílová cesta>**

   |Parametr OfflineUpdateExporter|Popis|
   |---|---|
   |**– O**|  **– Office**. Určuje produkt pro export aktualizací je Office 365.|
   |**– D**|**– Cíl**. Cíl je povinný parametr a je nutná úplná cesta k cílové složce.|

   - Nástroj **OfflineUpdateExporter** provádí následující akce:
      - Připojí se ke službě WSUS.
      - Přečte metadata aktualizace Office 365 ve službě WSUS.
      - Stáhne obsah a veškerá další metadata potřebná pro aktualizaci Office 365 do cílové složky.

1. Na příkazovém řádku na serveru WSUS připojeném k Internetu přejděte do složky, která obsahuje WsusUtil. exe. Ve výchozím nastavení se nástroj nachází ve složce%*ProgramFiles*% \ Update Services\Tools. Třeba pokud se nástroj nachází ve výchozím umístění, zadejte příkaz **cd %ProgramFiles%\Update Services\Tools**.
   - Pokud používáte Windows Server 2012, ujistěte se, že je na serverech WSUS nainstalovaný [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) .
   - Uživatel, který spouští nástroj WsusUtil, musí být členem místní skupiny Administrators na serveru.

1. Pro export metadat aktualizací softwaru do souboru GZIP zadejte následující text:  

    **WsusUtil. exe Export souboru s příponou***packagename**logfile*      

    Příklad:  

    **WsusUtil. exe export export. XML. gz export. log**

1. Do serveru WSUS na nejvyšší úrovni v odpojené síti zkopírujte soubor **Export. XML. gz** .
1. Pokud jste schválili aktualizace pro jiné produkty, zkopírujte obsah složky WSUSContent do složky WSUSContent odpojeného serveru WSUS, který je na nejvyšší úrovni.
1. Zkopírujte cílovou složku, která se používá pro **OfflineUpdateExporter** , do serveru lokality nejvyšší úrovně Configuration Manager v odpojené síti.

## <a name="import-the-office-365-updates"></a>Import aktualizací Office 365

1. Na odpojeném serveru WSUS nejvyšší úrovně importujte metadata aktualizace z **souboru export. XML. gz** , který jste vygenerovali na serveru WSUS připojeném k Internetu.
   
    Příklad:  

    **WsusUtil. exe import export. XML. gz import. log**
    
    Ve výchozím nastavení se nástroj WsusUtil. exe nachází ve složce%*ProgramFiles*% \ Update Services\Tools.

1. Po dokončení importu budete muset nakonfigurovat vlastnost řízení lokality na odpojeném serveru Configuration Manager lokality nejvyšší úrovně. Tyto body změny konfigurace Configuration Manager k obsahu pro Office 365. Změna konfigurace vlastnosti:
   1. Zkopírujte [skript prostředí PowerShell O365OflBaseUrlConfigured](#bkmk_o365_script) na nejvyšší úroveň odpojeného serveru Configuration Manager lokality.
   1. Změňte `"D:\Office365updates\content"` na úplnou cestu ke zkopírovanému adresáři, který obsahuje obsah Office a metadata generovaná nástrojem OfflineUpdateExporter.
      > [!IMPORTANT]
      > Pouze místní cesty fungují pro vlastnost O365OflBaseUrlConfigured.
   1. Uložte skript jako`O365OflBaseUrlConfigured.ps1`
   1. Z okna PowerShellu se zvýšenými oprávněními na odpojené Configuration Manager serveru lokality na nejvyšší `.\O365OflBaseUrlConfigured.ps1`úrovni spusťte.
   1. Restartujte službu **SMS_Executive** na serveru lokality.
1. V konzole **Configuration Manager** přejděte na **Správa** > **Konfigurace** > lokality**lokality**.
1. Klikněte pravým tlačítkem myši na lokalitu nejvyšší úrovně a pak vyberte **Konfigurovat součásti** > lokality**bod aktualizace softwaru**.
1. Na kartě **klasifikace** vyberte *aktualizace*. Na kartě **produkty** vyberte *klienta Office 365*.
1. [Synchronizovat aktualizace softwaru](synchronize-software-updates.md#manually-start-software-updates-synchronization) pro Configuration Manager
1. Po dokončení synchronizace použijte běžný postup nasazení aktualizací Office 365.

## <a name="proxy-configuration"></a><a name="bkmk_O365_ki"></a>Konfigurace proxy serveru

- Konfigurace proxy serveru není do nástroje nativně integrovaná. Pokud je proxy server nastaven v možnostech internetu na serveru, na kterém je nástroj spuštěný, v teorie se použije a musí fungovat správně.
   - Na příkazovém řádku spusťte `netsh winhttp show proxy` příkaz, který zobrazí nakonfigurovaný proxy server.



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