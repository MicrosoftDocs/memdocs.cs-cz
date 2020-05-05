---
title: Konfigurace správy na základě rolí
titleSuffix: Configuration Manager
ms.date: 11/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 14258c3e7e2cfe5423b97064a26fdf5616d6b0a4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078613"
---
# <a name="configure-role-based-administration-for-configuration-manager"></a>Konfigurace správy na základě rolí pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V Configuration Manager Správa na základě rolí kombinuje role zabezpečení, obory zabezpečení a přidělené kolekce k definování rozsahu správy pro jednotlivé správce. Obor správy zahrnuje objekty, které může administrativní uživatel zobrazit v konzole Configuration Manager a úlohy související s těmito objekty, ke kterým má administrativní uživatel oprávnění. Konfigurace správy na základě rolí platí pro všechny lokality v hierarchii.  

 Pokud ještě nejste obeznámeni s koncepty správy na základě rolí, přečtěte si téma [základy správy na základě rolí](../../../understand/fundamentals-of-role-based-administration.md).  

 Informace v následujících postupech vám pomůžou vytvořit a nakonfigurovat správu na základě rolí a související nastavení zabezpečení:  

- [Vytváření vlastních rolí zabezpečení](#BKMK_CreateSecRole)  
- [Konfigurování rolí zabezpečení](#BKMK_ConfigSecRole)  
- [Konfigurace oborů zabezpečení pro objekt](#BKMK_ConfigSecScope)  
- [Konfigurace kolekcí pro správu zabezpečení](#BKMK_ConfigColl)  
- [Vytvořit nového administrativního uživatele](#BKMK_Create_AdminUser)  
- [Úprava oboru správy správce](#BKMK_ModAdminUser)  

## <a name="create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a> Vytvoření vlastních rolí zabezpečení

 Configuration Manager poskytuje několik integrovaných rolí zabezpečení. Pokud požadujete další role zabezpečení, můžete vytvořit vlastní roli zabezpečení vytvořením kopie stávající role zabezpečení a pak můžete tuto kopii upravit. Můžete vytvořit vlastní roli zabezpečení, která uživatelům s právy pro správu uděluje dodatečná oprávnění zabezpečení, která vyžaduje, aby neobsahovala aktuálně přiřazenou roli zabezpečení. Pomocí vlastní role zabezpečení jim můžete udělit pouze oprávnění, která požadují, a zabránit přidělení role zabezpečení, která uděluje více oprávnění, než požadují.  

 Následující postup použijte k vytvoření nové role zabezpečení pomocí existující role zabezpečení jako šablony.  

### <a name="to-create-custom-security-roles"></a>Vytváření vlastních rolí zabezpečení

1. V konzole Configuration Manager klikněte na **Správa**.  

2. V pracovním prostoru **Správa** rozbalte položku **zabezpečení**a pak zvolte **role zabezpečení**.  

   Pro vytvoření nové role zabezpečení použijte jeden z následujících postupů:  

    - Pro vytvoření nové vlastní role zabezpečení proveďte následující akce:  

      1. Vyberte existující roli zabezpečení, kterou použijete jak zdroj pro novou roli zabezpečení.
      2. Na kartě **Domů** ve skupině **role zabezpečení** vyberte možnost **Kopírovat**. Tato akce vytvoří kopii zdrojové role zabezpečení.  
      3. V průvodci Kopírovat roli zabezpečení zadejte **Název** pro novou vlastní roli zabezpečení.  
      4. V okně **Přiřazení operací zabezpečení**rozbalením každého uzlu **Operace zabezpečení** zobrazte dostupné akce.  
      5. Chcete-li změnit nastavení operace zabezpečení, klikněte na šipku dolů ve sloupci **hodnota** a vyberte možnost **Ano** nebo **ne**.

            > [!CAUTION]  
            > Když konfigurujete vlastní roli zabezpečení, ujistěte se, že neudělíte oprávnění, která nejsou vyžadována administrativními uživateli, kteří jsou přidruženi k nové roli zabezpečení. Například hodnota **Upravit** pro operaci zabezpečení **role zabezpečení** uděluje správcům oprávnění k úpravě jakékoli přístupné role zabezpečení, a to i v případě, že nejsou k této roli zabezpečení přidruženi.  

      6. Po konfiguraci oprávnění kliknutím na **tlačítko OK** uložte novou roli zabezpečení.  

    - Chcete-li importovat roli zabezpečení, která byla exportována z jiné hierarchie Configuration Manager, proveďte následující akce:  

        1. Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **importovat roli zabezpečení**.  
        2. Zadejte soubor. XML, který obsahuje konfiguraci role zabezpečení, kterou chcete importovat. Kliknutím na tlačítko **otevřít** dokončete postup a uložte roli zabezpečení.  

            > [!NOTE]  
            > Po importu role zabezpečení můžete úpravou vlastností role zabezpečení změnit oprávnění objektu, která jsou přidružena k roli zabezpečení.  

## <a name="configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a>Konfigurace rolí zabezpečení

 Skupiny oprávnění zabezpečení, které jsou definovány pro roli zabezpečení, se nazývají přiřazení operací zabezpečení. Přiřazení operací zabezpečení představují kombinaci typů objektů a akcí, které jsou dostupné pro jednotlivé typy objektů. Můžete upravit, které operace zabezpečení jsou dostupné pro jakoukoli vlastní roli zabezpečení, ale nemůžete upravit předdefinované role zabezpečení, které Configuration Manager poskytovat.  

 K úpravě operací zabezpečení pro roli zabezpečení použijte následující postup.  

### <a name="to-modify-security-roles"></a>Úprava rolí zabezpečení

1. V konzole Configuration Manager vyberte možnost **Správa**.  
2. V pracovním prostoru **Správa** rozbalte položku **zabezpečení**a pak zvolte **role zabezpečení**.  
3. Vyberte vlastní roli zabezpečení, kterou chcete upravit.  
4. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  
5. Klikněte na kartu **oprávnění** .  
6. V okně **Přiřazení operací zabezpečení**rozbalením každého uzlu **Operace zabezpečení** zobrazte dostupné akce.  
7. Chcete-li změnit nastavení pro operaci zabezpečení, zvolte šipku dolů ve sloupci **hodnota** a zvolte možnost **Ano** nebo **ne**.  

    > [!CAUTION]  
    > Když konfigurujete vlastní roli zabezpečení, ujistěte se, že neudělíte oprávnění, která nejsou vyžadována administrativními uživateli, kteří jsou přidruženi k nové roli zabezpečení. Například hodnota **Upravit** pro operaci zabezpečení **role zabezpečení** uděluje správcům oprávnění k úpravě jakékoli přístupné role zabezpečení, a to i v případě, že nejsou k této roli zabezpečení přidruženi.  

8. Po dokončení konfigurace přiřazení operací zabezpečení klikněte na **tlačítko OK** a uložte novou roli zabezpečení.  

##  <a name="configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a> Konfigurování oborů zabezpečení pro objekt
 Můžete spravovat přidružení rozsahu zabezpečení pro objekt z objektu – nikoli z oboru zabezpečení. Jedinými přímými konfiguracemi, které rozsahy zabezpečení podporují, jsou změny jeho názvu a popisu. K provedení změny názvu a popisu rozsahu zabezpečení, když máte zobrazeny vlastnosti rozsahu zabezpečení, musíte mít oprávnění **Upravit** pro zabezpečitelný objekt **Rozsahy zabezpečení** .  

 Když vytvoříte nový objekt v Configuration Manager, je přidružený ke každému oboru zabezpečení, který je přidružený k rolím zabezpečení účtu, který se používá k vytvoření objektu. K tomuto chování dochází, když tyto role zabezpečení poskytují oprávnění **vytvořit** nebo **nastavit rozsah zabezpečení** . Rozsahy zabezpečení objektu můžete po jeho vytvoření změnit.  

 Například máte přiřazenou roli zabezpečení, která vám uděluje oprávnění k vytvoření nové skupiny hranic. Když vytvoříte novou skupinu hranic, nemáte žádnou možnost, ke které můžete přiřadit konkrétní rozsahy zabezpečení. Místo toho se automaticky přiřazují rozsahy zabezpečení, které jsou dostupné z rolí zabezpečení, ke kterým jste přidruženi, do nové skupiny hranic. Po uložení nové skupiny hranic můžete upravit obory zabezpečení, které jsou přidruženy k nové skupině hranic.  

 Pomocí následujícího postupu můžete nakonfigurovat obory zabezpečení, které jsou přiřazeny objektu.  

### <a name="to-configure-security-scopes-for-an-object"></a><a name="bkmk_config-sec-scope"></a>Konfigurace oborů zabezpečení pro objekt  

1. V konzole Configuration Manager vyberte objekt, který podporuje přiřazení k oboru zabezpečení.  
2. Na kartě **Domů** ve skupině **klasifikovat** klikněte na možnost **nastavit rozsahy zabezpečení**.
3. V dialogovém okně **Nastavit rozsahy zabezpečení** vyberte nebo zrušte rozsahy, ke kterým je tento objekt přidružen. Každý objekt, který podporuje rozsahy zabezpečení, musí být přiřazen minimálně jednomu rozsahu zabezpečení.  
4. Kliknutím na **tlačítko OK** uložte přiřazené obory zabezpečení.  

    > [!NOTE]  
    > Když vytvoříte nový objekt, můžete objekt přiřadit více rozsahům zabezpečení. Chcete-li upravit počet rozsahů zabezpečení, které jsou přidruženy k objektu, je nutné toto přiřazení změnit po vytvoření objektu.

### <a name="to-configure-security-scopes-for-a-folder-starting-in-version-1906"></a><a name="bkmk_config-folder"></a>Konfigurace oborů zabezpečení pro složku (počínaje verzí 1906)
<!--3600867-->

1. V konzole Configuration Manager vyberte složku.  
1. Na kartě **Složka** na pásu karet vyberte možnost **nastavit rozsahy zabezpečení**.
   - Můžete také kliknout pravým tlačítkem na složku a vybrat **složku** > **nastavit rozsahy zabezpečení**.
1. V dialogovém okně **nastavit rozsahy zabezpečení** vyberte nebo zrušte rozsahy zabezpečení pro složku. Každá složka musí být přiřazena alespoň k jednomu oboru zabezpečení. Všem složkám se přiřadí **výchozí** obor zabezpečení, dokud je nebudete měnit.
1. Kliknutím na **tlačítko OK** uložte přiřazené obory zabezpečení.  

    > [!IMPORTANT]  
    > - Existující role zabezpečení automaticky získá oprávnění **třídy složky** při instalaci Configuration Manager verze 1906. Pro všechny nové role zabezpečení budete muset přidat oprávnění **třídy složka** a ověřit, jestli mají stávající role potřebná oprávnění pro vaše prostředí.
    > 
    > - Položka je prohledávatelné mimo obor zabezpečení uživatele, pokud tento uživatel sdílí obor zabezpečení s osobou, která objekt vytvořila. <!--5602690-->

## <a name="configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a> Konfigurování kolekcí pro správu zabezpečení

 Pro konfigurování kolekcí pro správu na základě rolí neexistují žádné postupy. Kolekce nemají konfiguraci správy na základě rolí. Místo toho přiřadíte kolekce k administrativnímu uživateli, když nakonfigurujete administrativního uživatele. Operace zabezpečení kolekce, které jsou povoleny v rolích zabezpečení přiřazených uživateli, určují oprávnění, která má administrativní uživatel pro kolekce a prostředky kolekce (Členové kolekce).  

 Když má správce oprávnění ke kolekci, má také oprávnění ke kolekcím, které jsou omezeny na tuto kolekci. Vaše organizace například používá kolekci s názvem všechny plochy. Existuje také kolekce s názvem všechny Severní Amerika plochy, která je omezena na kolekci všechny pracovní plochy. Pokud správce má oprávnění ke kolekci Všechny pracovní plochy, tyto mají také stejná oprávnění ke kolekci Všechny pracovní plochy pro Severní Ameriku.

 Uživatel s právy pro správu navíc nemůže použít oprávnění **Odstranit** nebo **Upravit** na kolekci, která je jim přímo přiřazena. Ale můžou tato oprávnění použít pro kolekce, které jsou omezené na tuto kolekci. V předchozím příkladu může správce odstranit nebo upravit kolekci všechny Severní Amerika plochy, ale nemůže odstranit nebo upravit kolekci všechny pracovní plochy.  

## <a name="create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a> Vytvoření nového správce

 Chcete-li jednotlivcům nebo členům skupiny zabezpečení udělit přístup ke správě Configuration Manager, vytvořte správce v Configuration Manager a zadejte účet systému Windows uživatele nebo skupiny uživatelů. Každému administrativnímu uživateli v Configuration Manager musí být přiřazena nejméně jedna role zabezpečení a jeden obor zabezpečení. Rovněž je možné přiřadit kolekce a tím omezit obor zabezpečení správce.  

 Nové správce můžete vytvořit pomocí následujících postupů.  

### <a name="to-create-a-new-administrative-user"></a>Postup při vytvoření nového správce  

1. V konzole Configuration Manager vyberte možnost **Správa**.  
2. V pracovním prostoru **Správa** rozbalte položku **zabezpečení**a pak zvolte možnost **Administrativní uživatelé**.  
3. Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **Přidat uživatele nebo skupinu**.  
4. Zvolte **Procházet**a pak vyberte uživatelský účet nebo skupinu, které chcete použít pro tohoto nového administrativního uživatele.  

    > [!NOTE]  
    > U konzolové správy lze jako správce určit pouze uživatele domény nebo skupiny zabezpečení.

5. U **přidružených rolí zabezpečení**zvolte **Přidat** a otevřete seznam dostupných rolí zabezpečení, zaškrtněte políčko u jedné nebo více rolí zabezpečení a pak zvolte **OK**.  

6. Výběrem jedné z následujících dvou možností definujte chování zabezpečitelné objektu pro nového uživatele:  

    - **Všechny instance objektů, které souvisí s přiřazenými rolemi zabezpečení**: Tato volba přidružuje správce k oboru zabezpečení **vše** a kolekcím **všechny systémy** a **Všichni uživatelé a skupiny uživatelů** . Role zabezpečení přiřazené ke správci definují přístup k objektům. Nové objekty, které tento správce vytvoří, budou přiřazeny k oboru zabezpečení **Výchozí** .  

    - **Pouze instance objektů přiřazené k zadaným oborům zabezpečení a kolekcím**: ve výchozím nastavení tato volba přidružuje správce k oboru zabezpečení **výchozí** a kolekcím **všechny systémy** a **Všichni uživatelé a skupiny uživatelů** . Nicméně skutečné obory zabezpečení a kolekce jsou omezeny jen na ty, které jsou přidruženy k účtu, pomocí něhož byl vytvořen správce. Tato volba podporuje přidání nebo odebrání oborů zabezpečení a kolekcí, aby bylo možné přizpůsobit obor správy správce.  

    > [!IMPORTANT]  
    > Předchozí možnosti spojují jednotlivé přiřazené obory zabezpečení a kolekce ke všem rolím zabezpečení, které jsou přiřazeny administrativnímu uživateli. Můžete použít třetí možnost, **přidružit přiřazené role zabezpečení k určitým oborům zabezpečení a kolekcím**, aby bylo možné přidružit jednotlivé role zabezpečení k určitým oborům zabezpečení a kolekcím. Tato třetí možnost je dostupná po vytvoření nového správce při úpravě tohoto správce.  

7. V závislosti na výběru provedeném v kroku 6 postupujte následovně:  

    - Pokud jste vybrali **všechny instance objektů, které souvisí s přiřazenými rolemi zabezpečení**, klikněte na **tlačítko OK** a dokončete tento postup.  

    - Pokud jste vybrali **jenom instance objektů, které jsou přiřazené k zadaným oborům zabezpečení a kolekcím**, můžete zvolit **Přidat** a vybrat další kolekce a obory zabezpečení. Nebo vyberte jeden nebo více objektů v seznamu a kliknutím na tlačítko **Odebrat** je odeberte. Kliknutím na **tlačítko OK** dokončete tento postup.  

## <a name="modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a>Úprava oboru správy administrativního uživatele

 Obor správy správce lze upravit přidáním nebo odebráním rolí zabezpečení, oborů zabezpečení a kolekcí, které jsou přidruženy ke správci. Ke každému správci musí být přidružena nejméně jedna role zabezpečení a jeden obor zabezpečení. K oboru správy správce může být nutné přidružit jednu či více kolekcí. Většina rolí zabezpečení komunikuje s kolekcemi a bez přiřazené kolekce nefunguje správně.  

 Při úpravě správce lze změnit chování pro způsob přidružení zabezpečitelných objektů k přiřazeným rolím zabezpečení. Je možné zvolit jedno z následujících tří chování:  

- **Všechny instance objektů, které souvisí s přiřazenými rolemi zabezpečení**: Tato volba přidružuje správce k oboru **vše** a kolekce **všechny systémy** a **Všichni uživatelé a skupiny uživatelů** . Role zabezpečení přiřazené ke správci definují přístup k objektům.  

- **Pouze instance objektů přiřazené k zadaným oborům zabezpečení a kolekcím**: Tato volba přidružuje správce ke stejným oborům zabezpečení a kolekcím, které jsou přidruženy k účtu, který používáte ke konfiguraci správce. Tato volba podporuje přidání nebo odebrání rolí zabezpečení a kolekcí, aby bylo možné přizpůsobit obor správy správce.  

- **Přidružte přiřazené role zabezpečení ke konkrétním oborům a kolekcím zabezpečení**: pomocí této možnosti můžete pro uživatele vytvořit konkrétní přidružení mezi jednotlivými rolemi zabezpečení a určitými obory zabezpečení a kolekcemi.  

    > [!NOTE]  
    > Tato volba je k dispozici pouze při úpravě vlastností správce.  

Aktuální konfigurace chování zabezpečitelných objektů změní proces, který použijete k přiřazení dalších rolí zabezpečení. Následující postupy založené na různých volbách pro zabezpečitelné objekty vám pomohou při správě správce.  

Pomocí následujícího postupu můžete zobrazit a spravovat konfiguraci pro zabezpečitelné objekty pro uživatele s právy pro správu.  

### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Zobrazení a správa chování zabezpečitelných objektů u správce  

1. V konzole Configuration Manager vyberte možnost **Správa**.  
2. V pracovním prostoru **Správa** rozbalte položku **zabezpečení**a pak zvolte možnost **Administrativní uživatelé**.  
3. Zvolte správce, které chcete upravit.  
4. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  
5. Kliknutím na kartu **obory zabezpečení** zobrazíte aktuální konfiguraci pro zabezpečitelné objekty pro tohoto administrativního uživatele.  
6. Chcete-li upravit chování zabezpečitelných objektů, vyberte novou volbu chování zabezpečitelných objektů. Po provedení změny této konfigurace si přečtěte příslušný postup, kde najdete další pokyny ke konfiguraci oborů zabezpečení a kolekcí a rolí zabezpečení pro tohoto administrativního uživatele.  
7. Kliknutím na **tlačítko OK** dokončete postup.  

Následující postup slouží k úpravě administrativního uživatele, který má chování zabezpečitelné objekty nastaveno na **všechny instance objektů, které se vztahují k přiřazeným rolím zabezpečení**.  

### <a name="for-option-all-instances-of-the-objects-that-are-related-to-the-assigned-security-roles"></a>Pro možnost: všechny instance objektů, které se vztahují k přiřazeným rolím zabezpečení  

1. V konzole Configuration Manager vyberte možnost **Správa**.  
2. V pracovním prostoru **Správa** rozbalte položku **zabezpečení**a pak zvolte možnost **Administrativní uživatelé**.  
3. Zvolte správce, které chcete upravit.  
4. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  
5. Vyberte kartu **obory zabezpečení** a ověřte, že je administrativní uživatel nakonfigurován pro **všechny instance objektů, které souvisí s přiřazenými rolemi zabezpečení**.  
6. Chcete-li změnit přiřazené role zabezpečení, klikněte na kartu **role zabezpečení** .  

    - Chcete-li tomuto správci přiřadit další role zabezpečení, zvolte možnost **Přidat**, zaškrtněte políčko u každé další role zabezpečení, kterou chcete přiřadit, a pak zvolte možnost **OK**.  
    - Chcete-li odebrat role zabezpečení, vyberte jednu nebo více rolí zabezpečení ze seznamu a pak zvolte možnost **Odebrat**.

7. Chcete-li upravit chování zabezpečitelné objektu, klikněte na kartu **obory zabezpečení** a vyberte novou možnost pro chování zabezpečit objekty. Po provedení změny této konfigurace si přečtěte příslušný postup, kde najdete další pokyny ke konfiguraci oborů zabezpečení a kolekcí a rolí zabezpečení pro tohoto administrativního uživatele.  

    > [!NOTE]  
    > Když je chování zabezpečitelné objektu nastaveno na **všechny instance objektů, které se vztahují k přiřazeným rolím zabezpečení**, nemůžete přidat ani odebrat konkrétní obory zabezpečení a kolekce.  

8. Kliknutím na **tlačítko OK** dokončete tento postup.  

Následující postup slouží k úpravě administrativního uživatele, který má chování zabezpečitelné objektu nastaveno **pouze na instance objektů přiřazené k zadaným oborům zabezpečení a kolekcím**.  

### <a name="for-option-only-the-instances-of-objects-that-are-assigned-to-the-specified-security-scopes-and-collections"></a>Pro možnost: jenom instance objektů, které jsou přiřazené k zadaným oborům zabezpečení a kolekcím.  

1. V konzole Configuration Manager vyberte možnost **Správa**.  
2. V pracovním prostoru **Správa** rozbalte položku **zabezpečení**a pak zvolte možnost **Administrativní uživatelé**.  
3. Zvolte správce, které chcete upravit.  
4. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  
5. Klikněte na kartu **obory zabezpečení** a ověřte, že je uživatel nakonfigurován **pouze pro instance objektů přiřazené k zadaným oborům zabezpečení a kolekcím**.  
6. Chcete-li změnit přiřazené role zabezpečení, klikněte na kartu **role zabezpečení** .  

    - Chcete-li tomuto uživateli přiřadit další role zabezpečení, zvolte možnost **Přidat**, zaškrtněte políčko u každé další role zabezpečení, kterou chcete přiřadit, a poté klikněte na **tlačítko OK**.  
    - Chcete-li odebrat role zabezpečení, vyberte jednu nebo více rolí zabezpečení ze seznamu a pak zvolte možnost **Odebrat**.  
7. Chcete-li upravit obory zabezpečení a kolekce, které jsou přidruženy k rolím zabezpečení, klikněte na kartu **obory zabezpečení** .  

    - Chcete-li přidružit nové obory zabezpečení nebo kolekce ke všem rolím zabezpečení, které jsou přiřazeny tomuto administrativnímu uživateli, zvolte možnost **Přidat** a vyberte jednu ze čtyř možností. Pokud vyberete možnost **obor zabezpečení** nebo **kolekce**, zaškrtněte políčko u jednoho nebo více objektů pro dokončení tohoto výběru a pak zvolte možnost **OK**.  
    - Chcete-li odebrat obor zabezpečení nebo kolekci, vyberte objekt a zvolte možnost **Odebrat**.

8. Kliknutím na **tlačítko OK** dokončete tento postup.  

Následující postup slouží k úpravě správce, který má chování zabezpečitelné objektu nastaveno na **přidružení přiřazených rolí zabezpečení k určitým oborům zabezpečení a kolekcím**.  

### <a name="for-option-associate-assigned-security-roles-with-specific-security-scopes-and-collections"></a>Pro možnost: přidružte přiřazené role zabezpečení ke konkrétním oborům zabezpečení a kolekcím.  

1. V konzole Configuration Manager vyberte možnost **Správa**.  
2. V pracovním prostoru **Správa** rozbalte položku **zabezpečení**a pak zvolte možnost **Administrativní uživatelé**.  
3. Zvolte správce, které chcete upravit.  
4. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  
5. Klikněte na kartu **obory zabezpečení** a ověřte, že je administrativní uživatel nakonfigurovaný pro **přidružení přiřazených rolí zabezpečení k určitým oborům zabezpečení a kolekcím**.  
6. Chcete-li změnit přiřazené role zabezpečení, klikněte na kartu **role zabezpečení** .  

    - Pokud chcete tomuto správci přiřadit další role zabezpečení, klikněte na tlačítko **Přidat**. V dialogovém okně **Přidat roli zabezpečení** vyberte jednu nebo více dostupných rolí zabezpečení, zvolte možnost **Přidat**a vyberte typ objektu, který chcete přidružit k vybraným rolím zabezpečení. Pokud vyberete možnost **obor zabezpečení** nebo **kolekce**, zaškrtněte políčko u jednoho nebo více objektů pro dokončení tohoto výběru a pak zvolte možnost **OK**.  

        > [!NOTE]  
        > Než bude možné přidružit vybrané role zabezpečení ke správci, je nutné nakonfigurovat alespoň jeden obor zabezpečení. Když vyberete více rolí zabezpečení, bude každý obor zabezpečení a každá kolekce, kterou nakonfigurujete, přidružena ke každé vybrané roli zabezpečení.  

    - Chcete-li odebrat role zabezpečení, vyberte jednu nebo více rolí zabezpečení ze seznamu a pak zvolte možnost **Odebrat**.  

7. Chcete-li upravit obory zabezpečení a kolekce, které jsou přidruženy k určité roli zabezpečení, klikněte na kartu **obory zabezpečení** , vyberte roli zabezpečení a pak zvolte možnost **Upravit**.  

    - Chcete-li k této roli zabezpečení přidružit nové objekty, zvolte možnost **Přidat**a vyberte typ objektu, který chcete přidružit k vybraným rolím zabezpečení. Pokud vyberete možnost **obor zabezpečení** nebo **kolekce**, zaškrtněte políčko u jednoho nebo více objektů pro dokončení tohoto výběru a pak zvolte možnost **OK**.  

        > [!NOTE]  
        > Je nutné nakonfigurovat alespoň jeden obor zabezpečení.  

    - Chcete-li odebrat obor zabezpečení nebo kolekci, která je přidružena k této roli zabezpečení, vyberte objekt a zvolte možnost **Odebrat**.  

    - Po dokončení úprav přidružených objektů klikněte na **tlačítko OK**.  

8. Kliknutím na **tlačítko OK** dokončete tento postup.  

    > [!CAUTION]  
    > Když role zabezpečení uděluje správcům oprávnění k nasazení kolekcí, mohou tito správci distribuovat objekty z kteréhokoliv oboru zabezpečení, k němuž mají oprávnění typu **číst** , a to i v případě, že je tento obor zabezpečení přidružen k jiné roli zabezpečení.  

## <a name="next-steps"></a>Další kroky

[Účty používané v Configuration Manager](../../../plan-design/hierarchy/accounts.md)
