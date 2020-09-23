---
title: Referenční dokumentace k souborům a příkazům pro Microsoft Tunnel Gateway, řešení sítě VPN pro Microsoft Intune – Azure | Microsoft Docs
description: Vyhledá odkazy na soubory a příkazový řádek pro nástroje, které používáte k instalaci nebo správě služby Microsoft Tunnel Gateway, serveru VPN, který běží na systému Linux.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/23/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 950e1d20ab975bd3c6b3dfa37a83a69a4ae88a62
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "91017708"
---
# <a name="reference-for-microsoft-tunnel-gateway"></a>Referenční informace pro bránu Microsoft Tunnel Gateway

Informace v tomto odkazu pro bránu Microsoft Tunnel Gateway jsou k dispozici pro podporu instalace a údržby instalace tunelu ve vašem prostředí.

## <a name="mst-cli-command-line-tool-for-microsoft-tunnel-gateway"></a>Nástroj příkazového řádku MST-CLI pro bránu Microsoft Tunnel Gateway

**MST-CLI** je nástroj příkazového řádku pro použití s bránou Microsoft Tunnel Gateway. Tento nástroj je k dispozici na serveru Linux po dokončení instalace tunelu a nachází se na adrese **/usr/sbin/MST-CLI**. Mezi úlohy, které můžete použít k dokončení tohoto nástroje, patří:

- Získejte informace o serveru tunelového propojení.
- Nastaví nebo aktualizuje konfiguraci serveru tunelového propojení.
- Restartujte server tunelu.
- Odinstalujte Server tunelu.
Níže jsou uvedeny běžné použití tohoto nástroje na příkazovém řádku.

**Rozhraní příkazového řádku**:  

- `mst-cli –help` -Usage: **MST-CLI [příkaz]**

  Příkaz  
  - `agent` – Funguje na komponentě agenta.
  - `server` – Funguje na součásti serveru.
  - `uninstall` – Odinstalujte tunel od Microsoftu.
  - `eula` -Zobrazit smlouvu EULA.
  - `import_cert` – Importujte certifikát TLS.

- `mst-cli agent –help` -Usage: **MST-CLI agent [příkaz]**

  Příkaz  
  - `logs` -Zobrazit protokoly agenta (-h pro další informace).
  - `status` -Zobrazit stav agenta.
  - `start` -Spusťte službu agenta.
  - `stop` -Zastavit službu agenta.
  - `restart` -Restartujte službu agenta.

- `mst-cli agent logs   help` -Usage: **protokoly agentů MST-CLI [příznaky]**

  Flag
  - `-f, --follow` – Sledujte výstup protokolu. Výchozí hodnotou je hodnota false.
  - `--since string` -Zobrazit protokoly od časového RAZÍTKa.
  - `--tail uint` – Provede výstup zadaného počtu řádků na konci protokolů.  Výchozí hodnota je nula (0), která vytiskne všechny řádky.
  - `-t, --timestamps` – Výstup časových razítek v protokolu

- `mst-cli agent status` -Následující výsledky jsou příklady výsledků, které mohou být zobrazeny:  
  - Stav: spuštěno  
  - Stav: v pořádku

- `mst-cli agent start` -Spustí agenta, pokud je zastavený.

- `mst-cli agent stop` – Zastaví agenta.  Je nutné spustit ručně po zastavení.

- `mst-cli agent restart` -Restartuje agenta.

- `mst-cli server --help` -Usage: **MST-CLI Server [příkaz]**

  Příkaz
  - `logs` -Zobrazit protokoly serveru. Pro další informace použijte **-h** .
  - `status` -Zobrazit stav serveru.
  - `start` -Spusťte službu serveru.
  - `stop` – Zastavte službu serveru.
  - `restart` -Restartujte službu serveru.
  - `show` -Zobrazit různé statistiky serveru. Pro další informace použijte **-h** .

- `mst-cli server logs –help` -Usage: **protokoly serveru MST-CLI [příznaky]**

  Flag
  - `-f, --follow` – Sledujte výstup protokolu. Výchozí hodnotou je hodnota false.
  - `--since string` -Zobrazit protokoly od časového RAZÍTKa
  - `--tail uint` – Provede výstup zadaného počtu řádků na konci protokolů.  Výchozí hodnota je nula (0), která vytiskne všechny řádky.
  - `-t, --timestamps` – Výstup časových razítek v protokolu

- `mst-cli server status` -Následující výsledky jsou příklady výsledků, které mohou být zobrazeny:

  - Stav: spuštěno
  - Stav: v pořádku

- `mst-cli server start` – Spustí server, pokud je zastavený.

- `mst-cli server stop` – Zastaví Server.  Je nutné spustit ručně po zastavení.

- `mst-cli server restart` -Restartuje server.

- `mst-cli server show`
  - `show status` – Vytiskne stav a statistiku serveru.
  - `show users` -Vytiskne připojené uživatele.
  - `show ip bans` -Vytiskne zakázané IP adresy.
  - `show ip ban points` -Vytiskne všechny známé IP adresy, které mají body.
  - `show iroutes` – Vytiskne trasy poskytované uživateli serveru.
  - `show sessions all` -Vytiskne všechna ID relací.
  - `show sessions valid` -Vytiskne všechny relace platné pro opětovné připojení.
  - `show session [SID]` -Vytiskne informace o zadané relaci.
  - `show user [NAME]` -Zobrazí informace o zadaném uživateli.
  - `show id [ID]` -Vytiskne informace o zadaném ID.
  - `show events` – Poskytuje informace o připojení uživatelů.
  - `show cookies all` -Alias pro zobrazení relací ALL.
  - `show cookies valid` -Alias pro zobrazení platných relací.

## <a name="environment-variables"></a>Proměnné prostředí

Následují proměnné prostředí, které můžete chtít nakonfigurovat při instalaci softwaru Microsoft Tunnel Gateway na server Linux. Tyto proměnné se nacházejí v souboru prostředí **/etc/mstunnel/env.sh**:

- **http_proxy**= [adresa] – adresa http pro proxy server.
- **https_proxy**= [adresa] – Adresa HTTPS pro vaši proxy server. 

## <a name="data-paths"></a>Cesty k datům  

| Cesta/soubor                       | Description             | Oprávnění |
|---------------------------------|-------------------------|------------|
| /.../mstunnel                     | Kořenový adresář pro všechny konfigurace.   | Kořen vlastníka, skupina mstunnel |
| /.../mstunnel/admin-settings.js | Obsahuje nastavení pro instalaci serveru.   *Tento soubor spravuje Intune a neměli byste ho upravovat ručně*. | |
| /.../mstunnel/certs               | Adresář, ve kterém je uložený certifikát TLS.  | Kořen vlastníka, skupina mstunnel |
| /.../mstunnel/private             |Adresář, ve kterém jsou uložené certifikáty agenta Intune a privátního klíče TLS. | Kořen vlastníka, skupina mstunnel |

## <a name="files-add-during-server-installation"></a>Soubory přidané při instalaci serveru

**/etc/mstunnel**:

- **admin-settings.js**:
  - Obsahuje konfiguraci serializovaného *serveru* z Intune.
  - Vytvoří se po zaregistrování serveru.

- **agent-info.js**:
  - Vytvoří se po dokončení zápisu.
  - ID agenta, IntuneTenantId, AADTenantId a certifikát agenta RenewalDate.
  - Aktualizováno při obnovení certifikátu agenta.

- **privátní/agent. p12**:
  - Certifikát PFX, který se používá k ověření agenta pro Intune.
  - Automaticky obnoveno.

- **version-info.js**:
  - Obsahuje informace o verzi pro různé součásti.
  - ConfigVersion, DockerVersion, AgentImageHash, AgentCreateDate, ServerImageHash, ServerCreateDate.

- **ocserv. conf**:
  - Konfigurace serveru

- **Images_configured**

**Image Docker použité k vytvoření kontejnerů**:

- agentImageDigest
- serverImageDigest

### <a name="example-of-admin-settingsjson"></a>Příklad admin-settings.js

``` JSON
{
"PolicyName": "Auto Generated Policy for rh7vm",
   "DisplayName": "rh7vm Policy",
   "Description": "This policy was auto generated for rh7vm",  
   "Network": "169.100.0.0/16",
   "DNSServers": ["168.63.129.16"],
   "DefaultDomainSuffix": "nmqjwlanybmubp4imht0k2b4qd.xx.internal.cloudapp.net",
   "RoutesInclude": ["default"],
   "RoutesExclude": [],
   "ListenPort": 443
}
```

| Nastavení správce     | Description                           |
|-------------------|---------------------------------------|
| PolicyName          |Název zásady nastavení. Můžete zvolit název.       |
| DisplayName         |  Krátký zobrazovaný název. Můžete zvolit název.              |
| Description        | Popis zásady Můžete zvolit popis. |
| Síť             | Síť s maskou, která bude použita k přiřazení virtuálních adres klientů. To se nemusí měnit, pokud nemáte konflikt. Toto nastavení bude podporovat 64 000 klientů. |
| DNSServers          | Seznam serverů DNS, které by měl klient používat.  Tyto servery můžou přeložit adresy interních prostředků. |
| DefaultDomainSuffix | Přípona domény, kterou klient připojí k názvu hostitele při pokusu o překlad prostředků. |
| RoutesInclude       | Seznam tras, které budou směrovány prostřednictvím sítě VPN.  Výchozí hodnota je všechny trasy. |
| RoutesExclude       | Seznam tras, které by měly obejít síť VPN.                 |
| ListenPort          | Port, na kterém bude server VPN přijímat provoz.          |

## <a name="docker-commands"></a>Příkazy Docker

Níže jsou uvedené běžné příkazy pro Docker, které mohou být použity v případě, že je nutné prozkoumat problémy na serveru tunelového propojení.

Rozhraní příkazového řádku:

- `docker ps –a` – Zobrazit všechny kontejnery.
  - *mstunnel-Server* – tento kontejner spouští součásti serveru **ocserv** a používá příchozí port 443 *(výchozí)* nebo vlastní konfiguraci portů.
  - *mstunnel-agent* – tento kontejner spouští konektor Intune a používá odchozí port 443.

- **Restartování Docker**:  
  - `systemctl restart docker`

- **Chcete-li spustit něco v kontejneru**:
  - `docker exec –it mstunnel-server bash`
  - `docker exec –it mstunnel-agent bash`

## <a name="linux-commands"></a>Příkazy pro Linux

Níže jsou uvedené běžné příkazy pro Linux, které můžete používat se serverem tunelového propojení.

- `sudo su` – Nastaví kořen na box.  Tento příkaz použijte před spuštěním následujících příkazů a před spuštěním mstunnel-Setup.

- `ls` – Vypíše obsah adresáře.

- `ls – l` – Vypíše obsah adresáře včetně časových razítek.

- `cd` – změňte na jiný adresář. Například změny, které jste provedli v `cd /etc/test/stuff` *kořenovém* adresáři, do podsložky *etc* > do podsložky *test* > a potom do složky *s* přípravou.

- `cp <source> <destination>` – Užitečné pro kopírování certifikátů do správného umístění.

- `ln –s <source> <target>` – Vytvoření Softlink.

- `curl <URL>` – Kontroluje přístup k webu. Příklad: `curl https://microsoft.com`

- `./<filename>` – Spusťte skript.
