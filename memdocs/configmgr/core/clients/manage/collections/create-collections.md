---
title: Vytváření kolekcí
titleSuffix: Configuration Manager
description: Vytváření kolekcí v Configuration Manager pro snazší správu skupin uživatelů a zařízení.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e3f178b41fbb305ef938063bd9b9743daa6b5c69
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714357"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Vytváření kolekcí v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Kolekce jsou skupiny uživatelů nebo zařízení. Použijte kolekce pro úlohy, jako je Správa aplikací, nasazení nastavení dodržování předpisů nebo instalace aktualizací softwaru. Kolekce můžete použít také ke správě skupin nastavení klienta nebo společně se správou založenou na rolích k určení prostředků, ke kterým má administrativní uživatel přístup. Configuration Manager obsahuje několik předdefinovaných kolekcí. Další informace najdete v tématu [Úvod do kolekcí](introduction-to-collections.md).  

> [!NOTE]  
> Kolekce může obsahovat uživatele nebo zařízení, ale ne obojí.  


Informace v tomto článku vám pomůžou vytvořit kolekce v Configuration Manager. Můžete také importovat kolekce, které byly vytvořeny v aktuální Configuration Manager lokalitě nebo v jiné. Další informace o exportu a importu kolekcí najdete v tématu [Správa kolekcí](manage-collections.md).  


## <a name="collection-rules"></a>Pravidla shromažďování

Existují různé typy pravidel, která můžete použít ke konfiguraci členů kolekce v Configuration Manager.  


### <a name="direct-rule"></a>Přímé pravidlo

Pomocí přímých pravidel můžete vybrat uživatele nebo počítače, které chcete přidat do kolekce. Členství se nezmění, dokud neodeberete prostředek z Configuration Manager. Než budete moci přidat prostředky do kolekce přímých pravidel, Configuration Manager je třeba zjistit nebo je musíte importovat. Kolekce přímých pravidel mají větší administrativní režii než kolekce pravidel dotazů, protože vyžadují ruční změny.


### <a name="query-rule"></a>Dotazové pravidlo

Dynamickou aktualizaci členství v kolekci na základě dotazu, který Configuration Manager spouští podle plánu. Můžete například vytvořit kolekci uživatelů, kteří jsou ve službě Active Directory Domain Services členy organizační jednotky lidských zdrojů. Tato kolekce se automaticky aktualizuje, když se do organizační jednotky lidských zdrojů přidají nebo odeberou noví uživatelé.

Příklady dotazů, které můžete použít k vytvoření kolekcí, najdete v tématu [Vytvoření dotazů](../../../servers/manage/create-queries.md).


### <a name="device-category-rule"></a>Pravidlo kategorie zařízení

Správu svých zařízení můžete usnadnit přidružením kategorií zařízení k kolekcím zařízení. 

Další informace najdete v tématu [Automatická kategorizace zařízení do kolekcí](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Pravidlo zahrnutí kolekce

Zahrnutí členů jiné kolekce do kolekce Configuration Manager. Pokud se zahrnutá kolekce změní, Configuration Manager aktualizuje členství v aktuální kolekci podle plánu.

V kolekci můžete použít víc pravidel zahrnutí jiné kolekce.


### <a name="exclude-collection-rule"></a>Pravidlo vyloučení kolekce

Pravidla vyloučení kolekce umožňují vyloučit členy jedné kolekce z jiné kolekce Configuration Manager. Pokud se vyloučená kolekce změní, Configuration Manager aktualizuje členství v aktuální kolekci podle plánu.

V kolekci můžete použít víc pravidel vyloučení jiné kolekce. Pokud kolekce zahrnuje pravidla zahrnutí i vyloučení a dojde ke konfliktu, má pravidlo pro vyloučení kolekce přednost.

#### <a name="example"></a>Příklad
Vytvoříte kolekci, která má jedno pravidlo zahrnutí kolekce a jedno pravidlo vyloučení kolekce. Pravidlo pro zahrnutí přidá všechny stolní počítače Dell. Kolekce vyloučení je určena pro kolekci počítačů, které mají méně než 4 GB paměti RAM. Nová kolekce obsahuje stolní počítače Dell, které mají alespoň 4 GB paměti RAM.



## <a name="create-a-collection"></a><a name="bkmk_create"></a>Vytvoření kolekce  

1. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** .  

    - Chcete-li vytvořit *kolekci zařízení*, vyberte uzel **kolekce zařízení** . Pak na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit kolekci zařízení**.  

    - Chcete-li vytvořit *kolekci uživatelů*, vyberte uzel **kolekce uživatelů** . Pak na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit uživatelskou kolekci**.  

2. Na stránce **Obecné** v průvodci zadejte **název** a **Komentář**. V části **omezení kolekce** vyberte **Procházet**a pak vyberte omezující kolekci. Kolekce, kterou vytváříte, bude obsahovat jenom členy z limitující kolekce.  

4. Na stránce **pravidla členství** vyberte v seznamu **Přidat pravidlo** typ pravidla členství, které chcete pro kolekci použít. Můžete nakonfigurovat víc pravidel pro každou kolekci. Konfigurace každého pravidla se liší. Další informace o konfiguraci jednotlivých pravidel najdete v následujících částech tohoto článku:  
    - [Přímé pravidlo](#bkmk-direct)
    - [Dotazové pravidlo](#bkmk-query)
    - [Pravidlo kategorie zařízení](#bkmk-category)
    - [Pravidlo zahrnutí kolekce](#bkmk-include)
    - [Pravidlo vyloučení kolekce](#bkmk-exclude)

5. Na stránce **pravidla členství** si taky Projděte následující nastavení.

    - **Pro tuto kolekci použijte přírůstkové aktualizace**: tuto možnost vyberte, pokud chcete pravidelně kontrolovat a aktualizovat jenom nové nebo změněné prostředky z předchozího vyhodnocení kolekce. Tento proces je nezávisle na úplném vyhodnocování kolekcí. Ve výchozím nastavení se přírůstkové aktualizace vyskytují v intervalu 5 minut.  

        > [!IMPORTANT]  
        >  Kolekce s pravidly dotazů, které používají následující třídy, přírůstkové aktualizace nepodporují:  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (jenom pro kolekce uživatelů)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (jenom pro kolekce uživatelů)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **Naplánujte úplnou aktualizaci této kolekce**: Naplánujte pravidelné úplné vyhodnocení členství kolekce.  

        Počínaje verzí 1810 tyto změny v chování při vyhodnocování kolekce můžou zlepšit výkon webu:<!--3607726-->  

        - Pokud jste dřív nakonfigurovali plán pro kolekci založenou na dotazech, bude lokalita i nadále vyhodnocovat dotaz bez ohledu na to, jestli jste povolili nastavení kolekce **naplánovat úplnou aktualizaci této kolekce**. K úplnému zakázání plánu jste museli změnit plán na **žádný**.

            Když teď toto nastavení zakážete, tento web zruší plán. Chcete-li zadat plán pro vyhodnocení kolekce, povolte možnost **naplánovat úplnou aktualizaci v této kolekci**.  

            Když aktualizujete lokalitu, pro všechny existující kolekce, na které jste určili plán, lokalita povolí možnost **naplánovat úplnou aktualizaci v této kolekci**. I když tato konfigurace nemusí být vaším záměrem, jednalo se o skutečné chování plánu před tím, než aktualizujete lokalitu. Chcete-li zastavit web vyhodnocování kolekce podle plánu, zakažte tuto možnost.  

        - Nemůžete zakázat vyhodnocení předdefinovaných kolekcí, jako jsou **všechny systémy**, ale teď můžete plán nakonfigurovat. Toto chování vám umožní přizpůsobit tuto akci v čase, který splňuje vaše požadavky. 

            > [!TIP]  
            > V předdefinovaných kolekcích změňte pouze **čas** vlastního plánu. Neměňte způsob **opakování**. Budoucí iterace můžou vyhovět konkrétnímu způsobu opakování.  

6. Dokončením průvodce vytvořte novou kolekci. Nová kolekce se zobrazí v uzlu **Kolekce zařízení** v pracovním prostoru **Prostředky a kompatibilita** .  

> [!NOTE]  
> Chcete-li zobrazit členy kolekce, je nutné aktualizovat nebo znovu načíst konzolu Configuration Manager. Nezobrazují se v kolekci až do první plánované aktualizace. Můžete také ručně vybrat možnost **aktualizovat členství** pro kolekci. Dokončení aktualizace kolekce může trvat několik minut.  

        
### <a name="configure-a-direct-rule"></a><a name="bkmk-direct"></a>Konfigurace přímého pravidla  

1. Na stránce **Hledat prostředky** v **Průvodci vytvořením pravidla přímého členství**zadejte následující informace.  

    - **Třída prostředku**: Vyberte typ prostředku, který chcete vyhledat a přidat do kolekce. Příklad:
        - **Systémový prostředek**: Vyhledejte data inventáře vrácená z klientských počítačů.
        - **Neznámý počítač**: vyberte z hodnot vrácených neznámými počítači.
        - **Prostředek uživatele**: vyhledejte informace o uživateli shromážděné pomocí Configuration Manager.
        - **Prostředek skupiny uživatelů**: vyhledejte informace o skupině uživatelů shromažďované nástrojem Configuration Manager.

    - **Název atributu**: vyberte atribut přidružený k vybrané třídě prostředků, kterou chcete vyhledat. Příklad:  

        - Pokud chcete vybrat počítače podle názvu NetBIOS, vyberte **systémový prostředek** v seznamu **Třída prostředků** a **název NetBIOS** v seznamu **název atributu** .  

        - Pokud chcete vybrat uživatele podle názvu jejich organizační jednotky (OU), vyberte **prostředek uživatele** v seznamu **Třída prostředků** a **název uživatelské organizační jednotky** v seznamu **název atributu** .  

    - **Vyloučit prostředky označené jako zastaralé**: Pokud je klientský počítač označený jako zastaralý, nezahrňte tuto hodnotu do výsledků hledání.  

    - **Vylučte prostředky, které nemají nainstalovaného klienta Configuration Manager**: tyto prostředky se ve výsledcích hledání nezobrazí.  

    - **Hodnota**: zadejte hodnotu pro vyhledání názvu vybraného atributu. Použít znak procenta (%) jako zástupný znak. Příklad:  
        - Pokud chcete vyhledat počítače, které mají název pro rozhraní NetBIOS začínající na M, zadejte do tohoto pole **M%** .  
        - Pokud chcete hledat uživatele v organizační jednotce společnosti Contoso, zadejte do tohoto pole **Contoso** .

2. Na stránce **vybrat prostředky** vyberte prostředky, které chcete přidat do kolekce v seznamu **prostředky** , a pak vyberte **Další**.  


### <a name="configure-a-query-rule"></a><a name="bkmk-query"></a>Konfigurace pravidla dotazu  

V dialogovém okně **Vlastnosti dotazového pravidla** zadejte následující informace.  

- **Název**: Zadejte jedinečný název pro dotaz.  

- **Import příkazu dotazu**: otevře dialogové okno **Procházet dotaz** . Vyberte [Configuration Manager dotaz](../../../servers/manage/create-queries.md) , který chcete použít jako pravidlo dotazu pro kolekci.   

- **Třída prostředku**: Vyberte typ prostředku, který chcete vyhledat a přidat do kolekce. Vyberte hodnotu ze **systémového prostředku** a vyhledejte data inventáře vrácená z klientských počítačů nebo z **neznámého počítače** , abyste mohli vybírat z hodnot vrácených neznámými počítači.  

- **Upravit příkaz dotazu**: otevře dialogové okno **vlastnosti příkazu dotazu** , kde můžete napsat dotaz, který chcete použít jako pravidlo pro kolekci. Další informace o dotazech najdete v tématu [Úvod do dotazů](../../../servers/manage/introduction-to-queries.md).  

        
        > [!TIP]  
        > On the General tab, selecting the checkbox to **Omit duplicate rows (select distinct)** may result in less rows returned and potentially quicker results. 

### <a name="device-category-rule"></a><a name="bkmk-category"></a>Pravidlo kategorie zařízení

V okně **vybrat kategorie zařízení** jsou k dispozici následující akce.

- **Vytvořit**: zadejte název pro vytvoření nové kategorie.
- **Přejmenovat**: Přejmenuje vybranou kategorii.
- **Odstranit**: vyberte jednu nebo více kategorií a pomocí této akce je odeberte ze seznamu.

Další informace najdete v tématu [Automatická kategorizace zařízení do kolekcí](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="configure-an-include-collection-rule"></a><a name="bkmk-include"></a>Konfigurace pravidla zahrnutí kolekce  

V dialogovém okně **Vybrat kolekce** vyberte kolekce, které chcete zahrnout do nové kolekce, a pak vyberte **OK**.  


### <a name="configure-an-exclude-collection-rule"></a><a name="bkmk-exclude"></a>Konfigurace pravidla vyloučení kolekce  

V dialogovém okně **Vybrat kolekce** vyberte kolekce, které chcete vyloučit z nové kolekce, a pak vyberte **OK**.  



## <a name="import-a-collection"></a><a name="bkmk_import"></a>Import kolekce  

Když exportujete kolekci z lokality, Configuration Manager ji uloží jako soubor formát MOF (Managed Object Format) (MOF). Tento postup použijte k importu tohoto souboru do databáze lokality. Chcete-li provést tento postup, potřebujete oprávnění **vytvořit** pro třídu Collections.

> [!IMPORTANT]  
> - Ujistěte se, že soubor obsahuje pouze data kolekce, pochází z důvěryhodného zdroje a nebyl zfalšován.  
> 
> - Zajistěte, aby byl soubor exportovaný z lokality, na které běží stejná verze Configuration Manager, kterou používáte.  

Další informace o exportu kolekcí najdete v tématu [Správa kolekcí](manage-collections.md).


1. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Vyberte buď **kolekce uživatelů** , nebo uzel **kolekce zařízení** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **importovat kolekce**.  

3. Na stránce **Obecné** v **Průvodci importem kolekcí**vyberte **Další**.  

4. Na stránce **název souboru MOF** vyberte **Procházet**. Vyhledejte soubor MOF, který obsahuje informace o kolekci, které chcete importovat.  

5. Dokončete průvodce pro import kolekce. Nové kolekce se zobrazí v uzlu **Kolekce uživatelů** nebo **Kolekce zařízení** v pracovním prostoru **Prostředky a kompatibilita** . Aktualizujte nebo znovu načtěte konzolu Configuration Manager pro zobrazení členů kolekce pro nově importovanou kolekci.  

## <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a><a name="bkmk_aadcollsync"></a>Synchronizace výsledků členství kolekce do skupin Azure Active Directory

<!--3607475-->
> [!Tip]  
> Tato funkce byla poprvé představena ve verzi 1906 jako [funkce předběžné verze](../../../servers/manage/pre-release-features.md). Od verze 2002 už není k dispozici funkce předběžného vydání.  

Synchronizaci členství v kolekci můžete povolit do skupiny Azure Active Directory (Azure AD). Tato synchronizace vám umožní využít stávající pravidla pro seskupení místních dat v cloudu vytvořením členství ve skupině Azure AD na základě výsledků členství v kolekci. Můžete synchronizovat kolekce zařízení. Ve skupině Azure AD se projeví pouze zařízení se záznamem Azure Active Directory. Podporovaná je i zařízení připojená k hybridní službě Azure AD i zařízením připojená k Azure Active Director.

Synchronizace služby Azure AD proběhne každých pět minut. Jedná se o jednosměrný proces, od Configuration Manager do Azure AD. Změny provedené v Azure AD se neprojeví v kolekcích Configuration Manager, ale Configuration Manager se nepřepíší. Pokud má například kolekce Configuration Manager dvě zařízení a skupina Azure AD má tři různá zařízení, po synchronizaci má skupina Azure AD pět zařízení.


### <a name="prerequisites"></a>Požadavky

- [Správa cloudu](../../../servers/deploy/configure/azure-services-wizard.md)
- [Azure Active Directory zjišťování uživatelů](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>Vytvoření skupiny a nastavení vlastníka ve službě Azure AD

1. Přejít na [https://portal.azure.com](https://portal.azure.com).
1. Přejděte na **Azure Active Directory** > **skupiny** > **všechny skupiny**.
1. Klikněte na **Nová skupina** a zadejte **název skupiny** a volitelně také **Popis skupiny**.
1. Ujistěte se, že je **přiřazen** **typ členství** .
1. Vyberte **vlastníci**a pak přidejte identitu, která vytvoří synchronizační vztah v Configuration Manager.
1. Kliknutím na **vytvořit** dokončete vytváření skupiny Azure AD.

### <a name="enable-collection-synchronization-for-the-azure-service"></a>Povolit synchronizaci kolekce pro službu Azure

1. V konzole Configuration Manager v části**Přehled** >  **správy** > **Cloud Services** > **služby Azure**.
1. Klikněte pravým tlačítkem na tenanta Azure AD, kde jste vytvořili skupinu, a vyberte **vlastnosti**.
1. Na kartě **synchronizace kolekce** zaškrtněte políčko **Povolit synchronizaci skupiny adresářů Azure**.
1. Kliknutím na tlačítko **OK** nastavení uložte.

### <a name="enable-the-collection-to-synchronize"></a>Povolit synchronizaci kolekce

1. V konzole Configuration Manager přejdete na **prostředky a kompatibilita** > **Přehled** > **kolekce zařízení**.
1. Klikněte pravým tlačítkem na kolekci, kterou chcete synchronizovat, a pak klikněte na **vlastnosti**. 
1. Na kartě **synchronizace skupiny AAD** klikněte na **Přidat**.
1. V rozevírací nabídce vyberte **tenanta** , ve kterém jste skupinu Azure AD vytvořili.
1. Do pole **název začíná** polem zadejte kritéria hledání a klikněte na **Hledat**.
  - Pokud se zobrazí výzva k přihlášení, použijte identitu, kterou jste zadali jako vlastníka pro skupinu Azure AD.
1. Vyberte cílovou skupinu a potom kliknutím na tlačítko **OK** skupinu přidejte a kliknutím na **OK** zavřete vlastnosti kolekce.
1. Než budete moct ověřit členství ve skupině Azure Portal, budete muset počkat 5 až 7 minut.
   - Pokud chcete zahájit úplnou synchronizaci, klikněte pravým tlačítkem na kolekci a pak vyberte **synchronizovat členství**.


### <a name="verify-the-azure-ad-group-membership"></a>Ověření členství ve skupině Azure AD

1. Přejít na [https://portal.azure.com](https://portal.azure.com).
1. Přejděte na **Azure Active Directory** > **skupiny** > **všechny skupiny**.
1. Najděte skupinu, kterou jste vytvořili, a vyberte **členy**. 
1. Potvrďte, že členové odrážejí ty, které jsou v kolekci Configuration Manager.
   - Ve skupině se zobrazí pouze zařízení s identitou Azure AD.


![Synchronizovat kolekce do Azure AD](media/3607475-sync-collection-to-azuread.png)

## <a name="using-powershell"></a><a name="bkmk_powershell"></a>Použití PowerShellu

K vytváření a importu kolekcí můžete použít PowerShell. Další informace naleznete v tématu:

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import – CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

## <a name="next-steps"></a>Další kroky

[Spravovat kolekce](manage-collections.md)
