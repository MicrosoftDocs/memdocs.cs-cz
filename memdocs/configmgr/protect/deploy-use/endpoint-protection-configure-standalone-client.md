---
title: Konfigurace Endpoint Protection na samostatném klientovi
titleSuffix: Configuration Manager
description: Přečtěte si, jak nakonfigurovat Endpoint Protection na samostatném klientovi.
ms.date: 07/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f8d116879b0a85f3276d848b01c69d575b8b69fd
ms.sourcegitcommit: 41b2b50d5870dc127a8848a6657d56112f92515a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/04/2020
ms.locfileid: "87758308"
---
# <a name="configure-endpoint-protection-on-a-standalone-client"></a>Konfigurace Endpoint Protection na samostatném klientovi

*Platí pro: Configuration Manager (Current Branch)*

Vaše organizace může mít řadu samostatných klientů, které nemůžete spravovat ani chránit pomocí služby Microsoft Endpoint Configuration Manager. Bez ochrany koncových bodů je tato samostatná klienti zranitelná vůči potenciálním útokům na malware. Chcete-li tyto samostatné klienty chránit, můžete je ručně nakonfigurovat pomocí Endpoint Protection, jak je popsáno v tomto tématu.

Ruční konfigurace Endpoint Protection na samostatném klientovi:

- [Vytvoření antimalwarové zásady pro samostatného klienta](#create-an-antimalware-policy-for-the-standalone-client)
- [Přenos instalačního balíčku klienta Endpoint Protection do samostatného klienta](#transfer-endpoint-protection-client-installation-package-to-the-standalone-client)
- [Instalace Endpoint Protection na samostatném klientovi](#install-endpoint-protection-on-the-standalone-client)

## <a name="prerequisites"></a>Předpoklady

Níže jsou uvedené předpoklady pro konfiguraci Endpoint Protection na samostatném klientovi:

- Musíte mít přístup k instalačnímu balíčku klienta Endpoint Protection **scepinstall.exe**. Tento balíček najdete ve složce **C:\Program Files\Microsoft Configuration Manager\Client** . 
- Ujistěte se, že je nainstalovaná [aktualizace antimalwarové platformy od ledna 2017 pro klienty Endpoint Protection](https://support.microsoft.com/help/3209361/january-2017-anti-malware-platform-update-for-endpoint-protection-clie) . 

## <a name="create-an-antimalware-policy-for-the-standalone-client"></a>Vytvoření antimalwarové zásady pro samostatného klienta

V tomto kroku vytvoříte vlastní antimalwarové zásady v konzole Configuration Manager a pak ji přenesete do samostatného klienta.

Při vytváření antimalwarových zásad je nutné nakonfigurovat zdroj aktualizace definice tak, aby byly definice zásad aktuální na samostatném klientovi. Pokud je samostatný klient připojen k Internetu, můžete nakonfigurovat zdroj aktualizace definic jako [Microsoft Update](endpoint-definitions-microsoft-updates.md) a [Microsoft Malware Protection Center](endpoint-definitions-protection-center.md). Případně můžete vybrat možnost [Síťová sdílená položka](endpoint-definitions-network.md) jako zdroj distribuce definice a pravidelně ji aktualizovat pomocí nejnovějšího balíčku aktualizace definice. 

Postup vytvoření antimalwarových zásad pro samostatného klienta:

1. V konzole **Configuration Manager** klikněte na **prostředky a kompatibilita**.
2. V pracovním prostoru **Prostředky a kompatibilita** rozbalte položku **Endpoint Protection**a potom klikněte na **Antimalwarové zásady**.
3. Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit antimalwarové zásady**.
4. V části **Obecné** v dialogovém okně **Vytvořit antimalwarové zásady** zadejte název a popis zásad.
5. V dialogovém okně **Vytvořit antimalwarové zásady** nakonfigurujte nastavení, které mají tyto antimalwarové zásady mít, a poté klikněte na **OK**. Seznam nastavení, která můžete konfigurovat, najdete v tématu [seznam nastavení antimalwarových zásad](endpoint-antimalware-policies.md#list-of-antimalware-policy-settings).
    > [!NOTE]
    > V případě nastavení **aktualizace definic** vyberte **aktualizace distribuované z Microsoft Update** a **Aktualizace distribuované z centra společnosti Microsoft pro ochranu před škodlivým softwarem** , pokud je váš samostatný klient připojený k Internetu.  
    > Případně můžete vybrat **aktualizace ze sdílených složek souboru UNC** a distribuovat definice zásad pomocí síťové sdílené složky. Pak přidejte jednu nebo více cest UNC k umístění souborů aktualizací definic ve sdílené síťové složce.

6. Exportujte nově vytvořenou zásadu jako XML:
    1. V seznamu **antimalwarové zásady** klikněte pravým tlačítkem na zásadu.
    1. Vyberte **Exportovat**.
    1. Uložte zásadu jako XML, například **standalone.xml**.
7. Přeneste nový kód XML antimalwarové zásady do cílového samostatného klienta, na kterém chcete Endpoint Protection nakonfigurovat.

## <a name="transfer-endpoint-protection-client-installation-package-to-the-standalone-client"></a>Přenos instalačního balíčku klienta Endpoint Protection do samostatného klienta

V tomto kroku zkopírujete Endpoint Protection instalační balíček klienta (**scepinstall.exe**) z Configuration Manager serveru a přesunete ho do samostatného klienta.

1. Přihlaste se k serveru Configuration Manager.
2. Přejděte do složky **Client** složky Configuration Manager instalační složka (**C:\Program Files\Microsoft Configuration Manager\Client**).
3. Zkopírujte **scepinstall.exe**.
4. Přeneste **scepinstall.exe** do cílového samostatného klienta, na kterém chcete nainstalovat Endpoint Protection klientský software.

## <a name="install-endpoint-protection-on-the-standalone-client"></a>Instalace Endpoint Protection na samostatném klientovi
V tomto kroku spustíte instalační balíček (**scepinstall.exe**) a antimalwarové zásady (dříve přenesené ze Configuration Manager serveru) z příkazového řádku na samostatném klientovi.

Instalace Endpoint Protection na samostatném klientovi:

1. V samostatném klientovi otevřete příkazový řádek jako správce.
2. Změňte adresář na složku, do které jste uložili instalační soubor **scepinstall.exe** .
3. Zadejte následující příkaz, který spustí **scepinstall.exe** s antimalwarovou zásadou:

    ```cmd
    scepinstall.exe /policy <full path>\<policy file>
    ```

    Nahraďte `full path` cestou, kam jste uložili soubor XML antimalwarové zásady a `policy file` název souboru antimalwarové zásady.
 
    Instalační program se extrahuje a spustí se Průvodce instalací nástroje.

4. Dokončete instalaci klienta podle pokynů na obrazovce.

    Na poslední obrazovce Průvodce instalací se ve výchozím nastavení vybere možnost Prohledat v počítači potenciální hrozby po získání nejnovějších aktualizací. Zaškrtnutím políčka můžete přeskočit kontrolu.

## <a name="change-antimalware-policy-settings-on-a-standalone-endpoint-protection-client"></a>Změnit nastavení antimalwarových zásad u samostatného klienta Endpoint Protection

Postup změny nebo aktualizace antimalwarových zásad u samostatného klienta Endpoint Protection: 

1. [Vytvořte antimalwarové zásady pro samostatného klienta](#create-an-antimalware-policy-for-the-standalone-client).
2. Na samostatném klientovi spusťte následující příkaz:

```cmd
C:\Program Files\Microsoft Security Client\ConfigSecurityPolicy.exe <full path>\<policy file>
```

Nahraďte `full path` cestou, kam jste uložili nový soubor XML antimalwarové zásady a `policy file` názvem souboru antimalwarové zásady.

## <a name="next-steps"></a>Další kroky

Informace o tom, jak pomocí Endpoint Protection spravovat zabezpečení a malware v Configuration Manager klientských počítačích, najdete v tématu [konfigurace Endpoint Protection](endpoint-protection-configure.md).