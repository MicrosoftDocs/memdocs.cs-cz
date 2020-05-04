---
title: 'Synchronizovat aktualizace bez připojení k Internetu '
titleSuffix: Configuration Manager
description: Spustí synchronizaci aktualizací softwaru v bodu aktualizace softwaru nejvyšší úrovně, který je odpojený od Internetu.
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: c2fd85ea9d72e0986f56e24c7ccb66826829079b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710374"
---
# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>Synchronizace aktualizací softwaru z odpojeného bodu aktualizace softwaru  

*Platí pro: Configuration Manager (Current Branch)*

 Pokud dojde k odpojení bodu aktualizace softwaru lokality nejvyššího bodu od internetu, je nutné k synchronizaci metadat aktualizací softwaru použít funkce exportu a importu nástroje WSUSUtil. Jako zdroj synchronizace můžete zvolit existující server WSUS, který není ve vaší Configuration Manager hierarchii. Tento článek poskytuje informace o tom, jak používat funkce exportu a importu nástroje WSUSUtil.  

 Chcete-li metadata aktualizací softwaru exportovat a importovat, je nutné metadata aktualizací softwaru exportovat z databáze WSUS na určitém serveru pro export, poté zkopírovat místně uložené soubory licence do odpojeného bodu aktualizace softwaru a nakonec naimportovat metadata aktualizací softwaru do databáze WSUS na odpojeném bodě aktualizace softwaru.  

 Pomocí následující tabulky identifikujte server pro export, na který chcete metadata aktualizací softwaru vyexportovat.  

|Bod aktualizace softwaru|Nadřazený zdroj aktualizace pro připojené body aktualizace softwaru|Server pro export pro odpojený bod aktualizace softwaru|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Lokalita centrální správy|Microsoft Update (Internet)<br /><br /> Stávající server WSUS|Vyberte server WSUS, který je synchronizovaný s Microsoft Update pomocí klasifikace aktualizací softwaru, produktů a jazyků, které potřebujete ve svém Configuration Manager prostředí.|  
|Samostatná primární lokalita|Microsoft Update (Internet)<br /><br /> Stávající server WSUS|Vyberte server WSUS, který je synchronizovaný s Microsoft Update pomocí klasifikace aktualizací softwaru, produktů a jazyků, které potřebujete ve svém Configuration Manager prostředí.|  

 Než začnete s procesem exportu, ověřte, zda je synchronizace aktualizací softwaru na vybraném serveru pro export dokončena, aby bylo možné zajistit, že byla synchronizována poslední metadata aktualizací softwaru. Chcete-li ověřit, zda byla synchronizace aktualizací softwaru úspěšně dokončena, proveďte následující postup.  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>Ověření úspěšného dokončení synchronizace aktualizací softwaru na serveru pro export  

1.  Otevřete konzolu pro správu serveru WSUS a připojte se k databázi WSUS na serveru pro export.  

2.  V konzole pro správu služby WSUS klikněte na **Synchronizace**. V podokně výsledků se zobrazí seznam pokusů o synchronizaci aktualizací softwaru.  

3.  V podokně výsledků vyhledejte poslední pokus o synchronizaci aktualizací softwaru a ověřte, zda byla úspěšně dokončena.  

> [!IMPORTANT]  
> - Nástroj WSUSUtil musí být spuštěn místně na serveru pro export, aby bylo možné metadata aktualizací softwaru exportovat, a musí být spuštěn také na serveru odpojeného bodu aktualizací softwaru, aby bylo možné aktualizace softwaru importovat. Kromě toho uživatel, který nástroj WSUSUtil spustí, musí být členem místní skupiny správců na jednotlivých serverech.  
> - Pokud používáte Windows Server 2012, ujistěte se, že je na serverech WSUS nainstalovaný [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) .

## <a name="export-process-for-software-updates"></a>Proces exportu aktualizací softwaru  
 Export aktualizací softwaru zahrnuje dva hlavní kroky: kopírování místně uložených souborů licence do odpojeného bodu aktualizací softwaru a export metadat aktualizací softwaru z databáze WSUS na serveru pro export.  

 Pomocí následujícího postupu zkopírujte místní metadata licence do odpojeného bodu aktualizace softwaru.  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>Kopírování místních souborů ze serveru pro export na server odpojeného bodu aktualizace softwaru  

1. Na serveru pro export vyhledejte složku, ve které jsou uloženy aktualizace softwaru a jejich licenční podmínky. Ve výchozím nastavení se soubory serveru WSUS ukládají do složky <*instalační_jednotka_WSUS*>\WSUS\WSUSContent\\, kde *instalační_jednotka_WSUS* je jednotka, na které je server WSUS nainstalovaný.  

2. Zkopírujte všechny soubory a složky z tohoto umístění do složky WSUSContent na serveru odpojeného bodu aktualizace softwaru.  

   Pomocí následujícího postupu vyexportujte metadata aktualizací softwaru z databáze WSUS na server pro export.  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>Export metadat aktualizací software z databáze WSUS na server pro export  

1.  Na výzvu příkazového řádku na serveru pro export přejděte do složky, která obsahuje soubor WSUSutil.exe. Ve výchozím nastavení se nástroj nachází ve složce %*ProgramFiles*%\Update Services\Tools. Třeba pokud se nástroj nachází ve výchozím umístění, zadejte příkaz **cd %ProgramFiles%\Update Services\Tools**.  

2.  Zadejte následující příkaz pro export metadat aktualizací softwaru do souboru balíčku:  

     **wsusutil.exe export**  *název_balíčku*  *soubor_protokolu*  
 
     Příklad:  

     **WSUSutil. exe export export. XML. gz export. log**  

     Formát lze shrnout takto: WSUSutil. exe je následován možností exportu, název souboru export. XML. gz, který se vytvoří během operace exportu, a název souboru protokolu. Soubor WSUSutil.exe vyexportuje metadata ze serveru pro export a vytvoří soubor protokolu z činnosti.  

    > [!NOTE]  
    >  Balíček (soubor. XML. gz) a název souboru protokolu musí být v aktuální složce jedinečné.  

3.  Přesuňte balíček pro export do složky, která obsahuje soubor WSUSutil.exe, na serveru WSUS pro import.  

    > [!NOTE]  
    >  Pokud balíček do této složky přesunete, bude import jednodušší. Balíček lze přesunout do libovolného umístění, které je na serveru pro import dostupné. Poté zadejte umístění při spuštění souboru WSUSutil.exe.  

## <a name="import-software-updates-metadata"></a>Import metadat aktualizací softwaru  
 Pomocí následujícího postupu naimportujte metadata aktualizací softwaru ze serveru pro export do odpojeného bodu aktualizace softwaru.  

> [!IMPORTANT]  
>  Nikdy neimportujte žádná exportovaná data ze zdroje, kterému nedůvěřujete. Pokud naimportujete obsah ze zdroje, kterému nedůvěřujete, může dojít k ohrožení zabezpečení serveru WSUS.  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>Import metadat do databáze serveru pro import  

1.  Na výzvu příkazového řádku na serveru WSUS pro import přejděte do složky, která obsahuje soubor WSUSutil.exe. Ve výchozím nastavení se nástroj nachází ve složce %*ProgramFiles*%\Update Services\Tools.  

2.  Zadejte:  

     **wsusutil.exe import**  *název_balíčku*  *soubor_protokolu*  

     Příklad:  

     **WSUSutil. exe import export. XML. gz import. log**  

     Formát může být shrnut takto: WSUSutil. exe je následován příkazem import, název souboru balíčku (. XML. gz), který se vytvoří během operace exportu, cesta k souboru balíčku, pokud se nachází v jiné složce a název souboru protokolu. Soubor WSUSutil.exe naimportuje metadata ze serveru pro export a vytvoří soubor protokolu z činnosti.  

## <a name="next-steps"></a>Další kroky
Po první synchronizaci aktualizací softwaru nebo po dostupných nových klasifikací nebo dostupných produktech musíte [nakonfigurovat nové klasifikace a produkty](configure-classifications-and-products.md) pro synchronizaci aktualizací softwaru s novými kritérii.

Po synchronizaci aktualizací softwaru s požadovanými kritérii [Spravujte nastavení pro aktualizace softwaru](manage-settings-for-software-updates.md).   
