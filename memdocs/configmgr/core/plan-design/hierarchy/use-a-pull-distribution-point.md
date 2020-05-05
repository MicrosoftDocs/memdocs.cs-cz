---
title: Distribuční bod pro vyžádání obsahu
titleSuffix: Configuration Manager
description: Přečtěte si o konfiguracích a omezeních použití distribučního bodu pro vyžádání obsahu s Configuration Manager.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c243897a4c52eff04263325b998c4b23d6b3dde4
ms.sourcegitcommit: ad4b3e4874a797b755e774ff84429b5623f17c5c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/27/2020
ms.locfileid: "82166583"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>Použití distribučního bodu pro vyžádání obsahu s Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Když distribuujete obsah do standardního distribučního bodu v konzole Configuration Manager, server lokality bude obsah nabízet do distribučního bodu. Distribuční bod pro vyžádání obsahu získá obsah stažením ze zdrojového umístění, jako je klient.  

Když distribuujete obsah do mnoha distribučních bodů, umožňují distribuční body pro vyžádání obsahu snížit zatížení serveru lokality. Můžou také urychlit přenos obsahu na každý server. Komponenta správce distribuce na serveru lokality obvykle odesílá obsah do každého distribučního bodu. Místo toho lokalita přenáší proces přenosu obsahu do distribučních bodů pro vyžádání obsahu.  

Jednotlivé distribuční body můžete nakonfigurovat tak, aby byly distribuční body pro vyžádání obsahu. Pro každý distribuční bod pro vyžádání obsahu zadejte jeden nebo více zdrojových distribučních bodů, ze kterých může získat obsah. Distribuční bod pro vyžádání obsahu může stahovat pouze obsah z distribučního bodu, který zadáte jako zdrojový distribuční bod.

Když distribuujete obsah do distribučního bodu pro vyžádání obsahu v konzole nástroje, server lokality pošle oznámení. Distribuční bod pro vyžádání obsahu pak stáhne obsah ze zdrojového distribučního bodu. Distribuční bod pro vyžádání obsahu spravuje přenos obsahu stahováním z distribučního bodu, který již obsahuje kopii obsahu.  

Distribuční body pro vyžádání obsahu podporují stejné konfigurace a funkce jako obvyklé distribuční body. Například distribuční bod pro vyžádání obsahu podporuje:

- Konfigurace vícesměrového vysílání a PXE
- Ověření obsahu
- Distribuce obsahu na vyžádání
- Komunikace HTTP nebo HTTPS od klientů
- Stejné možnosti certifikátu jako jiné distribuční body
- Správa individuálně nebo jako člena skupiny distribučních bodů  

Nakonfigurujte distribuční bod pro vyžádání obsahu při instalaci distribučního bodu. Po vytvoření distribučního bodu ho nakonfigurujte jako distribuční bod pro vyžádání obsahu úpravou vlastností role. Další informace o tom, jak povolit distribuční bod jako distribuční bod pro vyžádání obsahu, najdete v tématu věnovaném [distribučnímu bodu pro vyžádání](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pull)obsahu.  

Odeberte konfiguraci, která bude distribuční bod pro vyžádání obsahu, úpravou vlastností distribučního bodu. Když konfiguraci odeberete jako distribuční bod pro vyžádání obsahu, vrátí se normální operace. Webový server spravuje budoucí přenosy obsahu do distribučního bodu.  

## <a name="distribution-process"></a>Proces distribuce

Při distribuci obsahu do distribučního bodu pro vyžádání obsahu dojde k následující posloupnosti událostí:

- Jakmile distribuujete obsah do distribučního bodu pro vyžádání obsahu v konzole nástroje, součást správce přenosu balíčků na serveru lokality zkontroluje databázi lokality a potvrdí, zda je obsah dostupný ve zdrojovém distribučním bodě. Pokud nemůže potvrdit, že se obsah nachází ve zdrojovém distribučním bodě pro distribuční bod pro vyžádání obsahu, zopakuje kontrolu každých 20 minut, dokud nebude obsah k dispozici.  

- Když správce přenosu balíčku potvrdí, že je obsah dostupný, upozorní distribuční bod pro vyžádání obsahu, aby si stáhl obsah. Pokud se toto oznámení nepovede, opakuje se na základě **Nastavení opakování** součásti distribuce softwaru pro distribuční body pro vyžádání obsahu. Když distribuční bod pro vyžádání obsahu obdrží toto oznámení, pokusí se stáhnout obsah ze svých zdrojových distribučních bodů.  

- I když distribuční bod pro vyžádání obsahu stáhne obsah, správce přenosu balíčků propojí stav na základě **Nastavení cyklického dotazování na stav** součásti distribuce softwaru pro distribuční body pro vyžádání obsahu.  Když distribuční bod pro vyžádání obsahu dokončí stahování obsahu, odešle tento stav do bodu správy.  

## <a name="configure-site-component-settings"></a>Konfigurovat nastavení součásti lokality

Když použijete distribuční bod pro vyžádání obsahu, zkontrolujte a nakonfigurujte následující nastavení součásti lokality:  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2. Vyberte lokalitu. Na pásu karet vyberte **Konfigurovat součásti webu**a vyberte **distribuce softwaru**.  

3. Přepněte na kartu **distribučního bodu pro vyžádání** obsahu.  

4. Ve skupině **Nastavení opakování** zkontrolujte následující hodnoty:  

    - **Počet opakovaných pokusů**: počet pokusů, které se správce přenosu balíčků pokusí odeslat distribučnímu bodu pro vyžádání obsahu, aby si stáhl obsah. Jakmile se tento počet pokusí, správce přenosu balíčků přenos zruší. Výchozí hodnota je 30.  

    - **Prodleva před opakováním (v minutách)**: počet minut, po které správce přenosu balíčku počká mezi pokusy. Ve výchozím nastavení je tato hodnota 20.  

5. Ve skupině **Nastavení cyklického dotazování na stav** zkontrolujte následující hodnoty:  

    - **Počet dotazů**: počet pokusů, kolikrát správce přenosu balíčků kontaktuje distribuční bod pro vyžádání obsahu, aby načetl stav úlohy. Pokud se tento počet několikrát pokusí dokončit, správce přenosu balíčků přenos zruší. Ve výchozím nastavení je tato hodnota 72.

    - **Prodleva před opakováním (v minutách)**: počet minut, po které správce přenosu balíčku počká mezi pokusy. Ve výchozím nastavení je tato hodnota 60.

    > [!NOTE]  
    >  Když správce přenosu balíčků úlohu zruší, protože překračuje počet opakovaných pokusů o cyklické dotazování, distribuční bod pro vyžádání obsahu nadále stahuje obsah. Po jeho dokončení pošle distribuční bod pro vyžádání obsahu příslušnou stavovou zprávu a konzola bude odpovídat novému stavu.  

## <a name="limitations"></a>Omezení

- Distribuční bod cloudu nelze konfigurovat jako distribuční bod pro vyžádání obsahu.  

- Roli distribučního bodu na serveru lokality nelze konfigurovat jako distribuční bod pro vyžádání obsahu.  

- Konfigurace připraveného obsahu potlačí konfiguraci distribučního bodu pro vyžádání obsahu. Pokud zapnete možnost **Povolit tento distribuční bod pro připravený obsah** v distribučním bodě pro vyžádání obsahu, počká na něj obsah. Neumožňuje vyžádat obsah ze zdrojového distribučního bodu. Podobně jako standardní distribuční bod povolený pro připravený obsah nepřijímá obsah ze serveru lokality. Další informace najdete v tématu [připravený obsah](manage-network-bandwidth.md#BKMK_PrestagingContent).  

- Distribuční bod pro vyžádání obsahu nepoužívá konfigurace plánu nebo omezení četnosti. Pokud nakonfigurujete dříve nainstalovaný distribuční bod jako distribuční bod pro vyžádání obsahu, budou konfigurace pro omezení četnosti a frekvence uloženy, ale nebudou použity. Pokud později odeberete konfiguraci distribučního bodu pro vyžádání obsahu, konfigurace plánu a četnosti jsou implementovány jako dříve nakonfigurované.  

    > [!NOTE]  
    >  Karty omezení **plánu** a **četnosti** nejsou viditelné ve vlastnostech distribučního bodu.  

- Distribuční body pro vyžádání obsahu nepoužívají nastavení na kartě **Obecné** ve **vlastnostech součásti distribuce softwaru** pro každou lokalitu. Mezi tato nastavení patří **Souběžná distribuce** a **opakování vícesměrového vysílání**.  

- Chcete-li přenést obsah ze zdrojového distribučního bodu ve vzdálené doménové struktuře, nainstalujte klienta Configuration Manager do distribučního bodu pro vyžádání obsahu. Také nakonfigurujte účet přístupu k síti, který má přístup ke zdrojovému distribučnímu bodu. Pokud povolíte možnost lokalita pro **použití Configuration Manager generovaných certifikátů pro systémy lokality http**, nepotřebujete účet pro přístup k síti.<!--1358228-->  

- Pokud je distribuční bod pro vyžádání obsahu zároveň klientem Configuration Manager, verze klienta musí být stejná jako Configuration Manager lokalita, která instaluje distribuční bod pro vyžádání obsahu. Distribuční bod pro vyžádání obsahu používá CCMFramework, který je společný pro distribuční bod pro vyžádání obsahu i pro klienta Configuration Manager.  

## <a name="about-source-distribution-points"></a>Zdrojové distribuční body  

Při konfiguraci distribučního bodu pro vyžádání obsahu zadejte jeden nebo více zdrojových distribučních bodů:  

- Průvodce zobrazí pouze distribuční body, které mají nárok na zdrojové distribuční body.  

- Distribuční bod pro vyžádání obsahu lze určit jako zdrojový distribuční bod pro další distribuční bod pro vyžádání obsahu.  

- Při použití konzoly Configuration Manager lze zadat pouze distribuční body, které podporují protokol HTTP jako zdrojové distribuční body.  

- Pomocí sady SDK Configuration Manager můžete určit zdrojový distribuční bod, který je nakonfigurován pro protokol HTTPS. Chcete-li použít zdrojový distribuční bod, který je nakonfigurován pro protokol HTTPS, nainstalujte klienta Configuration Manager do distribučního bodu pro vyžádání obsahu.  

- Pokud vaše vzdálené pobočky mají lepší připojení k Internetu nebo chcete snížit zatížení sítě WAN, použijte [distribuční bod cloudu](use-a-cloud-based-distribution-point.md) v Microsoft Azure jako zdroj. Distribuční bod pro vyžádání obsahu potřebuje přístup k Internetu, aby mohl komunikovat s Microsoft Azure. Obsah musí být distribuován do zdrojového cloudového distribučního bodu.<!--1321554-->  

    > [!Note]  
    > Tato funkce se za vaše předplatné Azure účtuje za ukládání dat a odchozí přenos z sítě. Další informace najdete v tématu [náklady na použití cloudového distribučního bodu](use-a-cloud-based-distribution-point.md#bkmk_cost).  

> [!Tip]  
> Pokud distribuční bod pro vyžádání obsahu stáhne obsah ze zdrojového distribučního bodu, bude tento distribuční bod pro vyžádání obsahu považovaný za klienta ve sloupci **Klientský přístup (jedinečný)** sestavy **Souhrn využívání distribučních bodů** .  

### <a name="source-priorities"></a>Zdrojové priority

- Přiřaďte každému zdrojovému distribučnímu bodu samostatnou prioritu nebo přiřaďte více zdrojových distribučních bodů stejné prioritě.  

- Priorita určuje, v jakém pořadí bude distribuční bod pro vyžádání obsahu požadovat obsah ze svých zdrojových distribučních bodů.  

- Distribuční body pro vyžádání obsahu nejprve kontaktují zdrojový distribuční bod s nejnižší hodnotou priority. Pokud existuje více zdrojových distribučních bodů se stejnou prioritou, distribuční bod pro vyžádání obsahu náhodně vybere jeden ze zdrojů s touto prioritou.  

- Pokud není obsah na vybraném zdroji dostupný, pokusí se distribuční bod pro vyžádání obsahu stáhnout obsah z jiného distribučního bodu se stejnou prioritou.  

- Pokud žádný z distribučních bodů s danou prioritou nemá obsah, pokusí se distribuční bod pro vyžádání obsahu stáhnout obsah ze zdrojového distribučního bodu s další úrovní priority. Pokračuje v hledání až do umístění obsahu.

- Pokud žádný z přiřazených zdrojových distribučních bodů nemá obsah, bude distribuční bod pro vyžádání obsahu čekat 30 minut a poté proces znovu spustí.  

## <a name="inside-the-pull-distribution-point"></a>V distribučním bodě pro vyžádání obsahu

- Pro správu přenosu obsahu používají distribuční body pro vyžádání obsahu komponentu **CCMFramework** . Klient Configuration Manager zahrnuje tuto součást.  

- Pokud povolíte distribuční bod pro vyžádání obsahu, lokalita nainstaluje **služby PullDP. msi**. Tento instalační program také přidá komponentu CCMFramework. Rozhraní nevyžaduje klienta Configuration Manager.  

- Po instalaci distribučního bodu pro vyžádání obsahu primárně používá službu **ccmexec** ke fungování.  

- Pokud distribuční bod pro vyžádání obsahu přenáší obsah, používá **Background Intelligent Transfer Service** (BITS) integrovaný do systému Windows. Distribuční bod pro vyžádání obsahu nevyžaduje instalaci rozšíření BITS pro server služby IIS.<!--sms.503672 -Clarified BITS use-->

- Provozní podrobnosti najdete v následujících protokolových souborech v distribučním bodu pro vyžádání obsahu:  

  - **DataTransferService.log**
  - **PullDP.log**

> [!TIP]
> Pokud se v souborech protokolu po přidání distribučního bodu pro vyžádání obsahu zobrazí chyby protokolu HTTP 403, proveďte následující změnu:
>
> 1. Ve zdrojovém distribučním bodě nastavte následující hodnotu registru:`HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL, ClientAuthTrustMode = 2 (REG_DWORD)`
> 1. Restartujte zdrojový server distribučního bodu.
>
> Distribuční bod pro vyžádání obsahu by měl začít stahovat obsah ze zdroje. Další informace o tomto klíči registru najdete v tématu [Přehled TLS-SSL (Schannel SSP)](https://docs.microsoft.com/windows-server/security/tls/what-s-new-in-tls-ssl-schannel-ssp-overview).<!-- SCCMDocs#1973 -->

## <a name="see-also"></a>Viz také  

[Základní koncepty správy obsahu](fundamental-concepts-for-content-management.md)
