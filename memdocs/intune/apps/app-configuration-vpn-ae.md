---
title: Konfigurace sítě VPN pro zařízení s Androidem Enterprise
titleSuffix: Microsoft Intune
description: Použijte zásadu ochrany aplikací v obsahu konfigurace sítě VPN pro zařízení s Androidem Enterprise.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/01/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcb7bd506d92befa3c73faf7270de28765f5b192
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347348"
---
# <a name="configure-a-vpn-for-android-enterprise-devices"></a>Konfigurace sítě VPN pro zařízení s Androidem Enterprise

Toto téma popisuje, jak vytvořit zásady konfigurace aplikace, které se dají nasadit ve spojení s klientem VPN na zařízeních s Androidem Enterprise. Tato konfigurace umožní síťovému provozu pro vybrané aplikace přistupovat k podnikovým prostředkům.

> [!NOTE]
> Platforma Android momentálně nepodporuje automatické spouštění připojení klienta VPN, když je otevřená jedna z vybraných aplikací. Připojení VPN se musí nejdřív iniciovat ručně, nebo můžete použít [vždycky zapnutou síť VPN](../configuration/vpn-settings-android-enterprise.md).

Požadavky na vytvoření zásady konfigurace pro dosažení úspěšného přístupu k síti VPN zahrnují možnosti zvoleného klienta VPN pro podporu konfiguračních profilů spravované aplikace. Klienti VPN, kteří podporují zásady konfigurace aplikací Intune v současné době, zahrnují:
- Cisco AnyConnect
- Citrix SSO
- F5 Access
- Globální připojení Palo Alto
- Pulse Secure
- SonicWall Mobile Connect

Pokud metoda pro přístup k tomuto koncovému bodu VPN vyžaduje použití klientských certifikátů, pak je potřeba profily certifikátů vytvořit předem, abyste mohli naplnit požadované hodnoty pro zásady konfigurace aplikace.

> [!NOTE]
> I když scénáře podnikového pracovního profilu Androidu podporují certifikáty SCEP a PKCS, v současné době podporují jenom certifikáty SCEP. 

Základní postup pro vytváření a testování profilu sítě VPN pro jednotlivé aplikace je následující:
1.  Vyberte odpovídající aplikaci klienta VPN pro vaši infrastrukturu.
2.  Identifikujte ID balíčků aplikací pro kancelářské aplikace, které chcete používat s připojením VPN.
3.  Nasaďte všechny profily certifikátů, které jsou potřebné pro splnění požadavků na ověření připojení VPN. Ujistěte se, že jste ověřili úspěšné nasazení.
4.  Nasaďte klientskou aplikaci VPN.
5.  Připravte profil VPN založený na konfiguraci aplikace s využitím informací shromážděných během předchozích kroků.
6.  Nasaďte nově vytvořený profil sítě VPN.
7.  Ověřte, že se klientská aplikace VPN úspěšně připojí k infrastruktuře serveru VPN.
8.  Ověřte, že provoz z vybraných kancelářských aplikací úspěšně provedl přenos sítě VPN, když je aktivní.

## <a name="get-the-app-package-id"></a>Získat ID balíčku aplikace

Identifikujte ID balíčku pro každou aplikaci, ke které chcete udělit přístup k síti VPN. Pro veřejně dostupné aplikace zvažte získání ID balíčku pro každou aplikaci v Google Play Storu. Zobrazovaná adresa URL pro každou aplikaci zahrnuje ID balíčku. Například ID balíčku pro verzi Android prohlížeče Microsoft Edge je `com.microsoft.emmx` . ID balíčku je součástí adresy URL.

![Příklad hledání ID balíčku aplikace](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png)

U obchodních aplikací požádejte svého dodavatele nebo vývojový tým aplikace, aby poskytoval příslušné ID balíčku.

## <a name="certificates"></a>Certifikáty

V tomto tématu předpokládáme, že připojení VPN bude používat ověřování založené na certifikátech a že jste úspěšně nasadili všechny certifikáty v řetězu, které jsou potřeba k úspěšnému ověření klienta. Obvykle to bude klientský certifikát, všechny zprostředkující certifikáty i kořenový certifikát.
Chcete-li získat další informace o nasazení certifikátů pro Android Enterprise, začněte tím, že si projděte téma [použití certifikátů k ověřování v Microsoft Intune](../protect/certificates-configure.md).

Po nasazení profilu certifikátu pro ověřování klientů potřebujete nějaké podrobnosti o tomto profilu, abyste mohli vytvořit zásady konfigurace aplikace VPN.
Pokud nejste obeznámeni s vytvářením konfiguračních profilů aplikací, přečtěte si téma [Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem Enterprise](../apps/app-configuration-policies-use-android.md).
 

## <a name="build-the-vpn-profile"></a>Sestavení profilu sítě VPN

Existují dva způsoby, jak vytvořit zásady konfigurace aplikací pro aplikaci VPN. Můžete použít **Návrhář konfigurace** nebo **datovou položku JSON** . Pokud nejsou v metodě **Návrháře konfigurace** dostupná všechna požadovaná nastavení sítě VPN, je potřeba možnost **data JSON** . Pokud určíte, že je pro podporu nutná možnost JSON, obraťte se na dodavatele sítě VPN. V tomto tématu zobrazíme příklady obou metod. V metodách **JSON data** a **Configuration Designer** můžete úspěšně začlenit ověřování na základě certifikátů. Při použití metody **dat JSON** můžete začít pomocí **Návrháře konfigurace** extrahovat potřebné hodnoty profilu.

> [!NOTE]
> Přestože je mnoho parametrů konfigurace klienta VPN podobné, každá aplikace má jedinečné klíče a možnosti. Pokud vznikne otázky, obraťte se na dodavatele sítě VPN. 

## <a name="use-the-configuration-designer-flow"></a>Použití toku návrháře konfigurace

1.  Začněte přidáním nové zásady konfigurace aplikací pro **spravovaná zařízení**.
2.  Zadejte vhodný název.
3.  Jako platformu vyberte **Android Enterprise** .
4.  Pokud je vyžadováno ověřování založené na certifikátech, vyberte buď možnost **pracovní profil** , nebo pouze **vlastník zařízení** jako typ profilu. **Profil pracovní vlastník a vlastník zařízení** není kompatibilní s ověřováním pomocí certifikátu.
5.  U cílové aplikace vyberte klienta VPN, který jste nasadili. v tomto příkladu používáme dříve nasazeného klienta Cisco AnyConnect VPN.

  ![Příklad vytvoření základních zásad konfigurace aplikace](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png)

6. Na další stránce použijte rozevírací seznam nastavení konfigurace a vyberte možnost **použít návrháře konfigurace** .

  ![Příklad použití nastavení Flow návrháře konfigurace.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png)

7. Kliknutím na tlačítko **Přidat** zobrazte seznam konfiguračních klíčů.
8.  Vyberte všechny konfigurační klíče, které požadujete pro zvolenou konfiguraci. V tomto příkladu používáme minimální seznam pro nastavení AnyConnect VPN, včetně ověřování založeného na certifikátech a sítě VPN pro aplikaci.
  
  <img alt="Example of using the Configuration Designer Flow - Configuration keys." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" width="350">

9. Zadejte odpovídající hodnoty pro **název připojení**, **hostitele**a klíče **protokolu** .

  ![Příklad použití výběru konfiguračního klíče toku návrháře konfigurace.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png)  

  > [!NOTE]
  > Názvy těchto klíčů se můžou lišit v závislosti na tom, která klientská aplikace VPN zásadu vytváří.

10. Zadejte ID balíčků aplikací, které jste shromáždili dříve v klíči **povolených aplikací VPN pro aplikaci VPN** .

  ![Příklad použití ID balíčku aplikace Flow návrháře konfigurace.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png)  

11. V klíčovém **aliasu certifikátu řetězce klíčů** (volitelné) přepněte **typ hodnoty** z **řetězce** na **certifikát**, což vám umožní vybrat správný profil klientského certifikátu, který se má používat s ověřováním VPN.

  ![Příklad použití toku návrháře konfigurace – aktualizace aliasu certifikátu řetězce klíčů](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png)  

12. Na další stránce vyberte všechny příslušné značky oboru.
13. Na další stránce zadejte příslušné skupiny, do kterých chcete nasadit zásady konfigurace aplikace.
14. Výběrem **vytvořit** dokončete vytvoření a nasazení zásady.

  ![Příklad použití návrháře konfigurace tok – přezkoumání.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png)  

## <a name="use-the-json-flow"></a>Použití toku JSON

Vytvořte dočasný profil:
1.  Začněte přidáním nové zásady konfigurace aplikací pro **spravovaná zařízení**.
2.  Zadejte vhodný název (použití tohoto profilu je dočasné, protože ho nebude možné uložit).
3.  Jako platformu vyberte **Android Enterprise** .
4.  U cílové aplikace vyberte klienta VPN, který jste nasadili.
5.  Pokud je vyžadováno ověřování založené na certifikátech, vyberte buď možnost **pracovní profil** , nebo pouze **vlastník zařízení** jako typ profilu. **Profil pracovní vlastník a vlastník zařízení** není kompatibilní s ověřováním pomocí certifikátu.

  ![Příklad použití základních informací o toku JSON.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-09.png)  

6.  Na další stránce použijte rozevírací seznam **nastavení konfigurace** a vyberte možnost **použít návrháře konfigurace**.

  ![Příklad použití formátu nastavení konfigurace toku JSON.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-10.png)  

7.  Kliknutím na tlačítko **Přidat** zobrazte seznam konfiguračních klíčů.
8.  Vyberte jeden z klíčů s **typem hodnoty** **řetězec**a klikněte na **OK**.

  <img alt="Example of using the JSON Flow - Select a key." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" width="350">

9.  Nyní změňte **typ hodnoty** z **řetězce** na **certifikát**. To vám umožní vybrat správný profil klientského certifikátu, který se má používat s ověřováním VPN.

  ![Příklad použití názvu datového připojení toku JSON.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png)  

10. Okamžitě změňte **typ hodnoty** zpět na **řetězec**. Všimněte si, že **hodnota konfigurace** se změní na token formátu `{{cert:GUID}}` .
11. Vyberte a zkopírujte reprezentace certifikátu tokenu do alternativního umístění, jako je textový editor.

  ![Příklad použití hodnoty konfigurace toku JSON.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png)  

12. Vyřaďte vytvořený profil – jediným účelem předchozích kroků bylo určit token certifikátu.

### <a name="create-the-vpn-profile"></a>Vytvoření profilu sítě VPN

1.  Začněte přidáním nového profilu konfigurace aplikace pro **spravovaná zařízení**.
2.  Zadejte vhodný název.
3.  Jako platformu vyberte **Android Enterprise** .
4.  U cílové aplikace vyberte klienta VPN, který jste nasadili.
5.  Pokud je vyžadováno ověřování založené na certifikátech, vyberte buď možnost **pracovní profil** , nebo pouze **vlastník zařízení** jako typ profilu. **Profil pracovní vlastník a vlastník zařízení** není kompatibilní s ověřováním pomocí certifikátu.
6.  Použijte rozevírací seznam **nastavení konfigurace** a vyberte možnost **zadat data JSON**.
7.  JSON můžete přímo nebo pokud dáváte přednost, pomocí tlačítka **Stáhnout šablonu JSON** Stáhněte a pak upravte šablonu v externím editoru podle vašeho výběru. Buďte opatrní s textovými editory, které mají možnost používat **inteligentní uvozovky**, protože jejich zahrnutí by vygenerovalo neplatný kód JSON.

  ![Příklad použití formátu JSON pro úpravu toku JSON.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png)  

8.  Bez ohledu na to, kterou metodu použijete, se po naplnění hodnot požadovaných pro požadovanou konfiguraci všechna zbývající nastavení s hodnotou STRING_VALUE nebo STRING_VALUE v celém formátu JSON musí odebrat.

#### <a name="example-json-for-f5-access-vpn"></a>Příklad JSON pro přístup k síti VPN pro F5

Následuje příklad dat JSON pro přístup k síti VPN nástroje F5.

``` JSON
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "app:com.f5.edge.client_ics",
    "managedProperty": [
        {
            "key": "disallowUserConfig",
            "valueBool": false
        },
        {
            "key": "vpnConfigurations",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "name",
                            "valueString": "MyCorpVPN"
                        },
                        {
                            "key": "server",
                            "valueString": "vpn.contoso.com"
                        },
                        {
                            "key": "weblogonMode",
                            "valueBool": false
                        },
                        {
                            "key": "fipsMode",
                            "valueBool": false
                        },
                        {
                            "key": "clientCertKeychainAlias",
                            "valueString": "{{cert:77333880-14e9-0aa0-9b2c-a1bc6b913829}}"
                        },
                        {
                            "key": "allowedApps",
                            "valueString": "com.microsoft.emmx"
                        },
                        {
                            "key": "mdmAssignedId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmInstanceId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceUniqueId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceWifiMacAddress",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceSerialNumber",
                            "valueString": ""
                        },
                        {
                            "key": "allowBypass",
                            "valueBool": false
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="summary"></a>Souhrn

Použití zásad konfigurace aplikací pro zaregistrovaná zařízení s Androidem Enterprise umožňuje využívat chování sítě VPN pro jednotlivé aplikace bez ohledu na to, že v této platformě není přímá podpora. 

## <a name="additional-information"></a>Další informace

Související informace najdete v následujících tématech:
- [Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem Enterprise](../apps/app-configuration-policies-use-android.md)
- [Nastavení zařízení s Androidem Enterprise pro konfiguraci sítě VPN v Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Další kroky

- [Vytvoření profilů sítě VPN pro připojení k serverům VPN v Intune](../configuration/vpn-settings-configure.md)
