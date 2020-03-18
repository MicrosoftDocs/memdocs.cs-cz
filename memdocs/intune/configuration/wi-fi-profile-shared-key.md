---
title: Vytvoření profilu Wi-Fi s předsdíleným klíčem v Microsoft Intune – Azure | Microsoft Docs
description: Pokud chcete v Microsoft Intune vytvořit profil Wi-Fi s předsdíleným klíčem, použijte vlastní profil a získáte ukázkový kód XML pro profily Wi-Fi založené na Androidu, Windows a protokolu EAP.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c6fd72a6-7dc8-48fc-9df1-db5627a51597
ms.reviewer: karanda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 105a25e33e0f8f0a76934199d24060328d50c05f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331871"
---
# <a name="use-a-custom-device-profile-to-create-a-wifi-profile-with-a-pre-shared-key-in-intune"></a>Vytvoření profilu Wi-Fi s předsdíleným klíčem pomocí vlastního profilu zařízení v Intune

Předsdílený klíč (PSK) se obvykle používá k ověřování uživatelů v sítích Wi-Fi nebo bezdrátových sítích LAN. V Intune můžete vytvořit profil Wi-Fi s využitím předsdíleného klíče. Pokud chcete vytvořit profil, použijte funkci **vlastních profilů zařízení** v Intune. Tento článek také obsahuje několik příkladů vytvoření profilu Wi-Fi založeného na protokolu EAP.

Tato funkce podporuje:

- Správce zařízení s Androidem
- Pracovní profil Android Enterprise
- Windows
- Wi-Fi založený na protokolu EAP

> [!IMPORTANT]
> - Použití předsdíleného klíče se systémem Windows 10 způsobuje chybu opravy v Intune. Když k ní dojde, profil Wi-Fi se správně přiřadí k zařízení a profil bude fungovat podle očekávání.
> - Pokud exportujete profil Wi-Fi s předsdíleným klíčem, ověřte si, že je soubor chráněný. Klíč má formát prostého textu, takže jeho ochranu zajišťujete vy.

## <a name="before-you-begin"></a>Před zahájením

- Může být pro vás snadnější zkopírovat kód z počítače připojeného k síti, jak je popsáno dále v tomto článku.
- Přidáním dalších nastavení OMA-URI můžete přidat více sítí a klíčů.
- Pro iOS/iPadOS použijte pro nastavení profilu Apple Configuratoru na stanici Mac.
- PSK vyžaduje řetězec 64 číslic v šestnáctkovém formátu nebo heslo o délce 8 až 63 tisknutelných znaků ASCII. Některé znaky, například hvězdička (*), nejsou podporovány.

## <a name="create-a-custom-profile"></a>Vytvoření vlastního profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **vlastní nastavení profilu Wi-Fi OMA-URI pro zařízení s Androidem**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: Vyberte svou platformu.
    - **Typ profilu**: vyberte **vlastní**.

4. V **Nastavení**vyberte **Přidat**. Zadejte nové nastavení OMA-URI s následujícími vlastnostmi:

    1. **Název**: zadejte název nastavení OMA-URI.
    2. **Popis**: zadejte popis nastavení OMA-URI. Toto nastavení není povinné, ale doporučujeme ho zadat.
    3. **OMA-URI**: zadejte jednu z následujících možností:

        - **Pro Android**: `./Vendor/MSFT/WiFi/Profile/SSID/Settings`
        - **Pro Windows**: `./Vendor/MSFT/WiFi/Profile/SSID/WlanXml`

        > [!NOTE]
        > Nezapomeňte použít tečku na začátku.

        SSID je identifikátor SSID, pro který vytváříte zásady. Pokud se například síť Wi-Fi jmenuje `Hotspot-1`, zadejte `./Vendor/MSFT/WiFi/Profile/Hotspot-1/Settings`.

    4. **Datový typ**: vyberte **řetězec**.

    5. **Hodnota**: vložte kód XML. Podívejte se na [Příklady](#android-or-windows-wi-fi-profile-example) v tomto článku. Aktualizujte jednotlivé hodnoty tak, aby odpovídaly nastavení vaší sítě. Nějaké pokyny najdete v sekci komentáře ke kódu.

5. Až to budete mít, vyberte **OK** > **Vytvořit** a změny uložte.

Váš profil se zobrazí v seznamu profily. V dalším kroku [přiřaďte tento profil](device-profile-assign.md) ke skupinám uživatelů. Tuto zásadu je možné přiřadit pouze skupinám uživatelů.

Pro každé zařízení, které se příště vrátí se změnami, se použijí zásady a vytvoří se pro ně profil Wi-Fi. Zařízení se potom připojí k síti automaticky.

## <a name="android-or-windows-wi-fi-profile-example"></a>Příklad profilu Wi-Fi pro Android nebo Windows

Následující příklad zahrnuje kód XML pro profil Wi-Fi pro Android nebo Windows: Příklad uvádíme proto, abychom ukázali správný formát a poskytli více podrobností. Je to jenom příklad a není myšlen jako doporučená konfigurace pro vaše prostředí.

### <a name="what-you-need-to-know"></a>Co je potřeba vědět

- `<protected>false</protected>` je třeba nastavit na hodnotu **nepravda**. Nastavení hodnoty **pravda** by mohlo způsobit, že zařízení by očekávalo šifrované heslo, následně by se ho pokoušelo dešifrovat a to by vedlo k selhání připojení.

- `<hex>53534944</hex>`má být nastaveno na šestnáctkovou hodnotu `<name><SSID of wifi profile></name>`. Zařízení s Windows 10 můžou vracet falešnou chybu `x87D1FDE8 Remediation failed`, ale zařízení pořád obsahuje profil.

- XML má speciální znaky, například `&` (ampersand). Použití speciálních znaků může zabránit tomu, aby XML fungovalo podle očekávání. 

### <a name="example"></a>Příklad

``` xml
<!--
<hex>53534944</hex> = The hexadecimal value of <name><SSID of wifi profile></name>
<Name of wifi profile> = Name of profile shown to users. It could be <name>Your Company's Network</name>.
<SSID of wifi profile> = Plain text of SSID. Does not need to be escaped. It could be <name>Your Company's Network</name>.
<nonBroadcast><true/false></nonBroadcast>
<Type of authentication> = Type of authentication used by the network, such as WPA2PSK.
<Type of encryption> = Type of encryption used by the network, such as AES.
<protected>false</protected> do not change this value, as true could cause device to expect an encrypted password and then try to decrypt it, which may result in a failed connection.
<password> = Plain text of the password to connect to the network
-->

<WLANProfile
xmlns="http://www.microsoft.com/networking/WLAN/profile/v1">
  <name><Name of wifi profile></name>
  <SSIDConfig>
    <SSID>
      <hex>53534944</hex>
 <name><SSID of wifi profile></name>
    </SSID>
    <nonBroadcast>false</nonBroadcast>
  </SSIDConfig>
  <connectionType>ESS</connectionType>
  <connectionMode>auto</connectionMode>
  <autoSwitch>false</autoSwitch>
  <MSM>
    <security>
      <authEncryption>
        <authentication><Type of authentication></authentication>
        <encryption><Type of encryption></encryption>
        <useOneX>false</useOneX>
      </authEncryption>
      <sharedKey>
        <keyType>passPhrase</keyType>
        <protected>false</protected>
        <keyMaterial>password</keyMaterial>
      </sharedKey>
      <keyIndex>0</keyIndex>
    </security>
  </MSM>
</WLANProfile>
```

### <a name="eap-based-wi-fi-profile-example"></a>Příklad profilu Wi-Fi založeného na protokolu EAP
Následující příklad obsahuje kód XML pro profil Wi-Fi založený na protokolu EAP: Příklad uvádíme proto, abychom ukázali správný formát a poskytli více podrobností. Je to jenom příklad a není myšlen jako doporučená konfigurace pro vaše prostředí.


```xml
    <WLANProfile xmlns="http://www.microsoft.com/networking/WLAN/profile/v1">
      <name>testcert</name>
      <SSIDConfig>
        <SSID>
          <hex>7465737463657274</hex>
          <name>testcert</name>
        </SSID>
        <nonBroadcast>true</nonBroadcast>
      </SSIDConfig>
      <connectionType>ESS</connectionType>
      <connectionMode>auto</connectionMode>
      <autoSwitch>false</autoSwitch>
      <MSM>
        <security>
          <authEncryption>
            <authentication>WPA2</authentication>
            <encryption>AES</encryption>
            <useOneX>true</useOneX>
            <FIPSMode     xmlns="http://www.microsoft.com/networking/WLAN/profile/v2">false</FIPSMode>
          </authEncryption>
          <PMKCacheMode>disabled</PMKCacheMode>
          <OneX xmlns="http://www.microsoft.com/networking/OneX/v1">
            <cacheUserData>false</cacheUserData>
            <authMode>user</authMode>
            <EAPConfig>
              <EapHostConfig     xmlns="http://www.microsoft.com/provisioning/EapHostConfig">
                <EapMethod>
                  <Type xmlns="http://www.microsoft.com/provisioning/EapCommon">13</Type>
                  <VendorId xmlns="http://www.microsoft.com/provisioning/EapCommon">0</VendorId>
                  <VendorType xmlns="http://www.microsoft.com/provisioning/EapCommon">0</VendorType>
                  <AuthorId xmlns="http://www.microsoft.com/provisioning/EapCommon">0</AuthorId>
                </EapMethod>
                <Config xmlns="http://www.microsoft.com/provisioning/EapHostConfig">
                  <Eap xmlns="http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1">
                    <Type>13</Type>
                    <EapType xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1">
                      <CredentialsSource>
                        <CertificateStore>
                          <SimpleCertSelection>true</SimpleCertSelection>
                        </CertificateStore>
                      </CredentialsSource>
                      <ServerValidation>
                        <DisableUserPromptForServerValidation>false</DisableUserPromptForServerValidation>
                        <ServerNames></ServerNames>
                      </ServerValidation>
                      <DifferentUsername>false</DifferentUsername>
                      <PerformServerValidation xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">false</PerformServerValidation>
                      <AcceptServerName xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">false</AcceptServerName>
                      <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">
                        <FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3">
                          <AllPurposeEnabled>true</AllPurposeEnabled>
                          <CAHashList Enabled="true">
                            <IssuerHash>75 f5 06 9c a4 12 0e 9b db bc a1 d9 9d d0 f0 75 fa 3b b8 78 </IssuerHash>
                          </CAHashList>
                          <EKUMapping>
                            <EKUMap>
                              <EKUName>Client Authentication</EKUName>
                              <EKUOID>1.3.6.1.5.5.7.3.2</EKUOID>
                            </EKUMap>
                          </EKUMapping>
                          <ClientAuthEKUList Enabled="true"/>
                          <AnyPurposeEKUList Enabled="false">
                            <EKUMapInList>
                              <EKUName>Client Authentication</EKUName>
                            </EKUMapInList>
                          </AnyPurposeEKUList>
                        </FilteringInfo>
                      </TLSExtensions>
                    </EapType>
                  </Eap>
                </Config>
              </EapHostConfig>
            </EAPConfig>
          </OneX>
        </security>
      </MSM>
    </WLANProfile>
```

## <a name="create-the-xml-file-from-an-existing-wi-fi-connection"></a>Vytvoření souboru XML z existujícího připojení Wi-Fi

Můžete také vytvořit soubor XML z existujícího připojení Wi-Fi. V počítači se systémem Windows použijte následující postup:

1. Vytvořte místní složku pro exportované profily W-Fi, například c:\WiFi.
2. Otevřete příkazový řádek jako správce (klikněte pravým tlačítkem na `cmd` > **Spustit jako správce**).
3. Spusťte `netsh wlan show profiles`. Zobrazí se názvy všech profilů.
4. Spusťte `netsh wlan export profile name="YourProfileName" folder=c:\Wifi`. Tento příkaz vytvoří soubor s názvem `Wi-Fi-YourProfileName.xml` v c:\Wifi.

    - Pokud exportujete profil Wi-Fi, který obsahuje předsdílený klíč, přidejte `key=clear` k příkazu:
  
        `netsh wlan export profile name="YourProfileName" key=clear folder=c:\Wifi`

        `key=clear` exportuje klíč do prostého textu, který je nutný k úspěšnému použití profilu.

Až budete mít soubor XML, zkopírujte a vložte syntax XML do nastavení OMA-URI > **datový typ**. [Vytvoření vlastního profilu](#create-a-custom-profile) (v tomto článku) obsahuje seznam kroků.

> [!TIP]
> `\ProgramData\Microsoft\Wlansvc\Profiles\Interfaces\{guid}` také zahrnuje všechny profily ve formátu XML.

## <a name="best-practices"></a>Osvědčené postupy

- Než profil Wi-Fi s předsdíleným klíčem nasadíte, ověřte, jestli se zařízení může přímo připojit ke koncovému bodu.

- Při střídání klíčů (hesla nebo hesla) očekává prostoje a naplánujte nasazení. Zvažte zavedení nových profilů Wi-Fi mimo pracovní dobu. Také upozorněte uživatele, že může být ovlivněno připojení.

- Pokud chcete zajistit hladký přechod, ujistěte se, že je zařízení koncového uživatele alternativním připojením k Internetu. Koncový uživatel například může přejít zpátky na Host WiFi (nebo na jinou síť Wi-Fi) nebo mít mobilní připojení ke komunikaci s Intune. Toto připojení navíc mu umožní i nadále přijímat aktualizace zásad, když dojde k aktualizaci firemního profilu Wi-Fi na zařízení.

## <a name="next-steps"></a>Další kroky

Nezapomeňte [profil přiřadit](device-profile-assign.md)a [monitorovat](device-profile-monitor.md) jeho stav.
