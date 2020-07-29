---
title: Konfigurace sítě VPN nebo sítě VPN vázané na aplikaci pro zařízení s Androidem Enterprise v Microsoft Intune | Microsoft Docs
titleSuffix: Microsoft Intune
description: Pomocí zásad konfigurace aplikací přidejte nebo vytvořte profil sítě VPN pro jednotlivé aplikace pro zařízení s Androidem Enterprise v Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/23/2020
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
ms.openlocfilehash: 7e869ad933e86d9330dbb8d6a26b1886a71cee07
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262893"
---
# <a name="use-a-vpn-and-per-app-vpn-policy-on-android-enterprise-devices-in-microsoft-intune"></a>Použití zásad sítě VPN a VPN pro aplikaci na zařízeních s Androidem Enterprise v Microsoft Intune

Virtuální privátní sítě (VPN) umožňují uživatelům přístup k prostředkům organizace vzdáleně, včetně domácích, hotelů, kavárnách a dalších. V Microsoft Intune můžete nakonfigurovat klientské aplikace VPN na zařízeních s Androidem Enterprise pomocí zásad konfigurace aplikace. Pak tyto zásady nasaďte s konfigurací sítě VPN do zařízení ve vaší organizaci.

Můžete také vytvořit zásady sítě VPN, které používají konkrétní aplikace. Tato funkce se označuje jako síť VPN pro jednotlivé aplikace. Když je aplikace aktivní, může se připojit k síti VPN a přistupovat k prostředkům prostřednictvím sítě VPN. Pokud aplikace není aktivní, síť VPN se nepoužije.

Tato funkce platí pro:

- Android Enterprise

Existují dva způsoby, jak vytvořit zásady konfigurace aplikace pro klientská aplikace VPN:

- Návrhář konfigurace
- Data JSON

V tomto článku se dozvíte, jak vytvořit zásadu konfigurace aplikace VPN pro jednotlivé aplikace a síť VPN pomocí obou možností.

> [!NOTE]
> Mnoho parametrů konfigurace klienta VPN je podobné. Každá aplikace ale má jedinečné klíče a možnosti. Pokud máte nějaké dotazy, obraťte se na dodavatele sítě VPN.

## <a name="before-you-begin"></a>Než začnete

- Android při otevření aplikace automaticky neaktivuje připojení klienta VPN. Připojení VPN musí být spuštěno ručně. Nebo můžete k zahájení připojení použít [vždycky zapnutou síť VPN](../configuration/vpn-settings-android-enterprise.md) .

- Následující klienti VPN podporují zásady konfigurace aplikací Intune:

  - Cisco AnyConnect
  - Citrix SSO
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - SonicWall Mobile Connect

- Při vytváření zásad sítě VPN v Intune vyberete jiné klíče ke konfiguraci. Tyto názvy klíčů se liší u různých klientských aplikací VPN. Názvy klíčů ve vašem prostředí se tak můžou lišit od příkladů v tomto článku.

- Návrhář konfigurace a data JSON můžou úspěšně používat ověřování pomocí certifikátů. Pokud ověřování pomocí sítě VPN vyžaduje klientské certifikáty, vytvořte profily certifikátů ještě před vytvořením zásad sítě VPN. Zásady konfigurace aplikace VPN používají hodnoty z profilů certifikátů.

  Zařízení se systémem Android Enterprise Work Profiles podporují certifikáty SCEP a PKCS. Zařízení s pracovními profily v Androidu Enterprise plně spravovaná, vyhrazená a podnikově vlastně podporují jenom certifikáty SCEP. Další informace najdete v tématu [použití certifikátů pro ověřování v Microsoft Intune](../protect/certificates-configure.md).

## <a name="per-app-vpn-overview"></a>Přehled sítě VPN pro jednotlivé aplikace

Při vytváření a testování sítě VPN pro jednotlivé aplikace zahrnuje základní tok následující kroky:

1. Vyberte aplikaci klienta VPN. [Než začnete](#before-you-begin) (v tomto článku), zobrazí seznam podporovaných aplikací.
2. Získejte ID balíčků aplikací pro aplikace, které budou používat připojení VPN. Postup [získání ID balíčku aplikace](#get-the-app-package-id) (v tomto článku) ukazuje, jak.
3. Pokud používáte certifikáty k ověření připojení VPN, pak vytvořte a nasaďte profily certifikátů ještě před nasazením zásad sítě VPN. Ujistěte se, že se profily certifikátů úspěšně nasazují. Další informace najdete v tématu [použití certifikátů pro ověřování v Microsoft Intune](../protect/certificates-configure.md).
4. Přidejte [aplikaci klienta VPN](apps-add-android-for-work.md) do Intune a nasaďte aplikaci pro vaše uživatele a zařízení.
5. Vytvořte zásady konfigurace aplikace VPN. Použijte v zásadách ID balíčku aplikace a informace o certifikátu.
6. Nasaďte nové zásady sítě VPN.
7. Potvrďte, že se aplikace klienta VPN úspěšně připojí k vašemu serveru VPN.
8. Když je aplikace aktivní, potvrďte, že provoz z vaší aplikace úspěšně prochází přes síť VPN.

## <a name="get-the-app-package-id"></a>Získat ID balíčku aplikace

Získejte ID balíčku pro každou aplikaci, která bude používat síť VPN. Pro veřejně dostupné aplikace můžete získat ID balíčku aplikace v Google Play Storu. Zobrazovaná adresa URL pro každou aplikaci zahrnuje ID balíčku.

V následujícím příkladu je ID balíčku aplikace Microsoft Edge Browser `com.microsoft.emmx` . ID balíčku je součástí adresy URL:

:::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png" alt-text="Získejte ID balíčku aplikace v adrese URL v Google Play Storu.":::

Pro obchodní aplikace (LOB) Získejte ID balíčku od vývojáře dodavatele nebo aplikace.

## <a name="certificates"></a>Certifikáty

Tento článek předpokládá, že připojení VPN používá ověřování založené na certifikátech. Také předpokládá, že jste úspěšně nasadili všechny certifikáty v řetězu, které jsou potřeba pro úspěšné ověření klientů. Tento řetěz certifikátů obvykle zahrnuje certifikát klienta, všechny zprostředkující certifikáty a kořenový certifikát.

Další informace o certifikátech najdete v tématu [použití certifikátů pro ověřování v Microsoft Intune](../protect/certificates-configure.md).

Po nasazení profilu certifikátu pro ověřování klienta se v profilu certifikátu vytvoří token certifikátu. Tento token se používá k vytvoření zásady konfigurace aplikace VPN.

Pokud nejste obeznámeni s vytvářením zásad konfigurace aplikací, přečtěte si téma [Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem Enterprise](app-configuration-policies-use-android.md).

## <a name="use-the-configuration-designer"></a>Použití návrháře konfigurace

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **zásady konfigurace aplikace**  >  **Přidat**  >  **spravovaná zařízení**.
3. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **Zásada Konfigurace aplikace: zásady sítě VPN Cisco AnyConnect pro zařízení s Androidem Enterprise Work Profile**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Android Enterprise**.
    - **Typ profilu**: vaše možnosti:
      - **Všechny typy profilů**: Tato možnost podporuje ověřování uživatelského jména a hesla. Pokud používáte ověřování založené na certifikátech, tuto možnost nepoužívejte.
      - **Jenom plně spravovaný, vyhrazený a podnikový pracovní profil**: Tato možnost podporuje ověřování na základě certifikátů a uživatelské jméno a heslo.
      - **Pouze pracovní profil**: Tato možnost podporuje ověřování na základě certifikátů a uživatelské jméno a ověřování hesla.
    - **Cílová aplikace**: vyberte aplikaci klienta VPN, kterou jste předtím přidali. V následujícím příkladu se používá klientská aplikace VPN Cisco AnyConnect:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png" alt-text="Vytvoření zásady konfigurace aplikace pro konfiguraci sítě VPN nebo sítě VPN pro jednotlivé aplikace v Microsoft Intune":::

4. Vyberte **Další**.
5. Do pole **Nastavení**zadejte následující vlastnosti:

    - **Formát nastavení konfigurace**: vyberte **použít návrháře konfigurace**:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png" alt-text="Vytvořte zásadu sítě VPN konfigurace aplikace v Microsoft Intune pomocí návrháře konfigurace – příklad.":::

    - **Přidat**: zobrazí seznam konfiguračních klíčů. Vyberte všechny konfigurační klíče potřebné pro vaši konfiguraci > **OK**.

      V následujícím příkladu jsme vybrali minimální seznam pro AnyConnect VPN, včetně ověřování založeného na certifikátech a sítě VPN pro jednotlivé aplikace:
  
      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" alt-text="Přidejte konfigurační klíče do zásad konfigurace aplikace VPN v Microsoft Intune pomocí návrháře konfigurace – příklad.":::

    - **Hodnota konfigurace**: zadejte hodnoty pro konfigurační klíče, které jste vybrali. Mějte na paměti, že se názvy klíčů liší v závislosti na aplikaci klienta VPN, kterou používáte. V části klíče vybrané v našem příkladu:

      - **Povolené aplikace sítě VPN pro jednotlivé aplikace**: Zadejte ID balíčků aplikací, které jste shromáždili dříve. Například:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png" alt-text="V Microsoft Intune pomocí návrháře konfigurace zadejte povolené identifikátory balíčku aplikace do zásad konfigurace aplikace VPN.":::

      - **Alias certifikátu řetězce klíčů** (volitelné): změňte **typ hodnoty** z **řetězce** na **certifikát**. Vyberte profil certifikátu klienta, který se má používat s ověřováním VPN. Například:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png" alt-text="Změňte alias certifikátu klienta řetězce klíčů v zásadách konfigurace aplikace VPN v Microsoft Intune pomocí návrháře konfigurace – příklad.":::

      - **Protokol**: Vyberte protokol **SSL** nebo protokol **IPSec** tunelu sítě VPN.
      - **Název připojení**: zadejte uživatelsky přívětivý název pro připojení VPN. Uživatelé uvidí tento název připojení na svých zařízeních. Zadejte například `ContosoVPN`.
      - **Hostitel**: zadejte adresu URL názvu hostitele k headend směrovači. Zadejte například `vpn.contoso.com`.

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png" alt-text="Příklady protokolů, názvu připojení a názvů hostitelů v zásadách konfigurace aplikace VPN v Microsoft Intune pomocí návrháře konfigurace":::

6. Vyberte **Další**.
7. V části **přiřazení**vyberte skupiny, kterým chcete přiřadit zásadu konfigurace aplikace VPN.

    Vyberte **Další**.

8. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a zásady se nasadí do vašich skupin. Tato zásada se taky zobrazuje v seznamu zásady konfigurace aplikací.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png" alt-text="V Microsoft Intune příkladu Zkontrolujte zásady konfigurace aplikací pomocí toku návrháře konfigurace.":::

## <a name="use-json"></a>Použít JSON

Tuto možnost použijte, pokud nemáte, nebo neznáte všechna požadovaná nastavení sítě VPN použitá v **Návrháři konfigurace**. Pokud potřebujete nápovědu, obraťte se na dodavatele sítě VPN.

### <a name="get-the-certificate-token"></a>Získání tokenu certifikátu

V tomto postupu vytvořte dočasnou zásadu. Zásada se neuloží. Záměrem je zkopírovat token certifikátu. Tento token použijete při vytváření zásad VPN pomocí JSON (další oddíl).

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace**  >  **zásady konfigurace aplikace**  >  **Přidat**  >  **spravovaná zařízení**.
2. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte libovolný název. Tato zásada je dočasná a nebude uložena.
    - **Platforma**: vyberte **Android Enterprise**.
    - **Typ profilu**: vyberte **pouze pracovní profil**.
    - **Cílová aplikace**: vyberte aplikaci klienta VPN, kterou jste předtím přidali.

3. Vyberte **Další**.
4. Do pole **Nastavení**zadejte následující vlastnosti:

    - **Formát nastavení konfigurace**: vyberte **použít návrháře konfigurace**.
    - **Přidat**: zobrazí seznam konfiguračních klíčů. Vyberte libovolný klíč s **typem hodnoty** **String**. Vyberte **OK**.

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" alt-text="V Návrháři konfigurace vyberte libovolný klíč s řetězcovou hodnotou v Microsoft Intune zásady konfigurace aplikace VPN.":::

5. Změňte **typ hodnoty** z **řetězce** na **certifikát**. Tento krok vám umožní vybrat správný profil klientského certifikátu, který ověřuje síť VPN:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png" alt-text="V Microsoft Intune příkladu změňte název připojení v zásadách konfigurace aplikace VPN.":::

6. Okamžitě změňte **typ hodnoty** zpět na **řetězec**. **Hodnota konfigurace** se změní na token `{{cert:GUID}}` :

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png" alt-text="Hodnota konfigurace zobrazuje token certifikátu v zásadách konfigurace aplikace VPN v Microsoft Intune":::

7. Zkopírujte tento token certifikátu a vložte ho do jiného souboru, jako je textový editor.

8. Zahodí tuto zásadu. Neukládejte ho. Jediným účelem je zkopírovat a vložit token certifikátu.

### <a name="create-the-vpn-policy-using-json"></a>Vytvoření zásady VPN pomocí formátu JSON

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **aplikace**  >  **zásady konfigurace aplikace**  >  **Přidat**  >  **spravovaná zařízení**.

2. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrý název zásady je třeba **Zásada Konfigurace aplikace: zásady sítě VPN pro zařízení s Androidem Enterprise Work Profile v celé společnosti**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Android Enterprise**.
    - **Typ profilu**: vaše možnosti:
      - **Všechny typy profilů**: Tato možnost podporuje ověřování uživatelského jména a hesla. Pokud používáte ověřování založené na certifikátech, tuto možnost nepoužívejte.
      - **Jenom plně spravovaný, vyhrazený a podnikový pracovní profil**: Tato možnost podporuje ověřování na základě certifikátů a uživatelské jméno a heslo.
      - **Pouze pracovní profil**: Tato možnost podporuje ověřování na základě certifikátů a uživatelské jméno a ověřování hesla.
    - **Cílová aplikace**: vyberte aplikaci klienta VPN, kterou jste předtím přidali. 

3. Vyberte **Další**.
4. Do pole **Nastavení**zadejte následující vlastnosti:

    - **Formát nastavení konfigurace**: vyberte **zadat data JSON**. JSON můžete přímo upravit.
    - **Stáhnout šablonu JSON**: tuto možnost použijte, pokud chcete stáhnout a aktualizovat šablonu v jakémkoli externím editoru. Buďte opatrní s textovými editory, které používají **inteligentní uvozovky**, protože můžou vytvořit neplatný kód JSON.

    Po zadání hodnot potřebných pro vaši konfiguraci odeberte všechna nastavení, která mají `"STRING_VALUE"` nebo `STRING_VALUE` .

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png" alt-text="Příklad použití formátu JSON pro úpravu toku JSON.":::

5. Vyberte **Další**.
6. V části **přiřazení**vyberte skupiny, kterým chcete přiřadit zásadu konfigurace aplikace VPN.

    Vyberte **Další**.

7. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a zásady se nasadí do vašich skupin. Tato zásada se taky zobrazuje v seznamu zásady konfigurace aplikací.

#### <a name="json-example-for-f5-access-vpn"></a>Příklad JSON pro přístup k síti VPN pro F5

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

## <a name="additional-information"></a>Další informace

- [Přidání zásad konfigurace aplikací pro spravovaná zařízení s Androidem Enterprise](app-configuration-policies-use-android.md)
- [Nastavení zařízení s Androidem Enterprise pro konfiguraci sítě VPN v Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Další kroky

- [Vytvoření profilů sítě VPN pro připojení k serverům VPN v Intune](../configuration/vpn-settings-configure.md)
