---
title: Řešení potíží s CMPivot
titleSuffix: Configuration Manager
description: Naučte se řešit potíže s CMPivot v Configuration Manager.
ms.date: 10/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 69178f9ac1c1acb1ee2a2931c88a55a0784435b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723506"
---
# <a name="troubleshoot-cmpivot"></a>Řešení potíží s CMPivot

CMPivot je nástroj, který poskytuje přístup ke stavu zařízení ve vašem prostředí v reálném čase. CMPivot spustí dotaz na všech aktuálně připojených zařízeních v cílové kolekci a vrátí výsledky.

V některých případech může být nutné vyřešit potíže s CMPivot. Pokud je například stavová zpráva z klienta na CMPivot poškozená, server lokality nemůže zprávu zpracovat. Tento článek vám pomůže pochopit tok informací pro CMPivot.

## <a name="troubleshoot-cmpivot-in-version-1902-and-later"></a><a name="bkmk_CMPivot-1902"></a>Řešení potíží s CMPivot ve verzi 1902 a novější

V Configuration Manager verzích 1902 a novějších můžete spustit CMPivot z lokality centrální správy (CAS) v hierarchii. Primární lokalita stále zpracovává komunikaci s klientem.

Když spouštíte CMPivot z CAS, používá se vysokorychlostní kanál pro odběr zpráv ke komunikaci s primární lokalitou. CMPivot nepoužívá standardní replikaci SQL mezi lokalitami. Pokud je vaše instance SQL Server nebo poskytovatel SQL vzdálená nebo pokud používáte SQL Server Always On, budete mít pro CMPivot scénář "dvojím směrováním". Informace o tom, jak definovat omezené delegování pro scénář dvojího směrování, najdete v tématu [CMPivot počínaje verzí 1902](cmpivot.md#bkmk_cmpivot1902).

>[!IMPORTANT]
> Při řešení potíží s CMPivot povolte podrobné protokolování v bodech správy (MPs) a na SMS_MESSAGE_PROCESSING_ENGINE serveru lokality a získejte další informace. Pokud je výstup klienta větší než 80 KB, povolte podrobné protokolování na MP a SMS_STATE_SYSTEM součásti serveru lokality. Informace o tom, jak povolit podrobné protokolování, najdete v tématu [Možnosti protokolování serveru lokality](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="get-information-from-the-site-server"></a>Získat informace ze serveru lokality

Ve výchozím nastavení jsou soubory protokolu webového serveru umístěny v `C:\Program Files\Microsoft Configuration Manager\logs`. Toto umístění může být odlišné, pokud jste zadali nevýchozí instalační adresář nebo převedené položky jako poskytovatel serveru SMS na jiný server. Pokud CMPivot spustíte z CAS, protokoly se nacházejí na primárním serveru lokality.

`smsprov.log` Vyhledejte tyto řádky:

- Configuration Manager verze 1906:
  <pre><code lang="Log">Auditing: User &ltusername> initiated client operation 145 to collection &ltCollectionId>. </code></pre>

- Configuration Manager verze 1902:
  <pre><code lang="Log">Type parameter is 135.
  Auditing: User &ltusername> ran script 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 with hash dc6c2ad05f1bfda88d880c54121c8b5cea6a394282425a88dd4d8714547dc4a2 on collection &ltCollectionId>. </code></pre>

 `7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14`je identifikátor GUID skriptu pro CMPivot. Tento identifikátor GUID můžete zobrazit také ve [zprávách o stavu auditů CMPivot](cmpivot.md#cmpivot-audit-status-messages).

V dalším kroku vyhledejte ID v okně CMPivot. Toto ID je `ClientOperationID`.

![Okno CMPivot se zvýrazněným ClientOperationID](media/cmpivot-client-operationid-1902.png)

Vyhledejte `TaskID` z tabulky ClientAction. `TaskID` Odpovídá `UniqueID` v tabulce ClientAction.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

V `BgbServer.log`nástroji vyhledejte `TaskID` shromážděné údaje z SQL a Všimněte si `PushID`. `TaskID` Je označen `TaskGUID`. Příklad:

<pre><code lang="Log">Starting to send push task (<b>PushID: 9</b> TaskID: 12 <b>TaskGUID: 9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b> TaskType: 15 TaskParam: PFNjcmlwdENvbnRlbnQgU2NyaXB0R3VpZD0nN0RDNkI2RjEtRTdGNi00M0MxL (truncated log entry)
Finished sending push task (<b>PushID: 9</b> TaskID: 12) to 2 clients
</code></pre>

### <a name="client-logs"></a>Protokoly klienta

Po zjištění informací ze serveru lokality ověřte protokoly klienta. Ve výchozím nastavení se protokoly klienta nacházejí v `C:\Windows\CCM\Logs`nástroji.

V `CcmNotificationAgent.log`nástroji vyhledejte položky protokolu, které vypadají jako následující řádky:  

<pre><code lang="Log">Receive task from server with <b>pushid=9</b>, taskid=12, <b>taskguid=9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b>, tasktype=15 and taskParam=PFNjcmlwdEhhc2ggU2NyaXB0SGF (truncated log entry)
Send Task response message &ltBgbResponseMessage TimeStamp="2019-09-13T17:29:09Z"><b>&ltPushID>5</b>&lt/PushID>&ltTaskID>4&lt/TaskID>&ltReturnCode>1&lt/ReturnCode>&lt/BgbResponseMessage> successfuly.
 </code></pre>

Podívejte `Scripts.log` se na `TaskID`. V následujícím příkladu vidíte `Task ID` `{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`:  

<pre><code lang="Log">Sending script state message (fast): <b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Result are sent for ScriptGuid: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 and <b>TaskID: {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
</code></pre>

> [!NOTE]
> Pokud v nástroji nevidíte "(Fast)" `Scripts.log`, data budou pravděpodobně vyšší než 80 kB. V takovém případě se informace odesílají na server lokality jako stavová zpráva. Použijte klienta `StateMessage.log` a server lokality `Statesys.log`.

### <a name="review-messages-on-the-site-server"></a>Zkontrolovat zprávy na serveru lokality

Pokud je v bodu správy povoleno [podrobné protokolování](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client) , můžete zjistit, jak jsou zpracovávány příchozí zprávy klienta. V `MP_RelayMsgMgr.log`nástroji vyhledejte `TaskID`.

V tomto `MP_RelayMsgMgr.log` příkladu vidíte ID `(GUID:83F67728-2E6D-4E4F-8075-ED035C31B783)` klienta a `Task ID {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`. ID zprávy se před odesláním do modulu zpracování zprávy přiřadí k odpovědi klienta:

<pre><code lang="Log">MessageKey: GUID:83F67728-2E6D-4E4F-8075-ED035C31B783<b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Create message succeeded for <b>message id 22f00adf-181e-4bad-b35e-d18912f39f89</b>
Add message payload succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
Put message succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
CRelayMsgMgrHandler::HandleMessage(): ExecuteTask() succeeded
</code></pre>

Pokud je v `SMS_MESSAGE_PROCESSING_ENGINE.log`nástroji povoleno [podrobné protokolování](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) , jsou zpracovány výsledky klienta. Použijte ID zprávy, které jste našli z `MP_RelayMsgMgr.log`. Položky protokolu zpracování jsou podobné jako v následujícím příkladu:

<pre><code lang="Log">Processing 2 messages with type Instant and IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]...
Processed 2 messages with type Instant. Failed to process 0 messages. All message IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]
</code></pre>

> [!TIP]
> Pokud během zpracování dojde k výjimce, můžete ji zkontrolovat spuštěním následujícího dotazu SQL a vyhledáním ve sloupci výjimka. Po zpracování zprávy již nebude v `MPE_RequestMessages_Instant` tabulce.
>
> ```SQL
> select * from MPE_RequestMessages_Instant where MessageID=<ID from SMS_MESSAGE_PROCESSING_ENGINE.log>
> ```

V `BgbServer.log`nástroji vyhledejte `PushID` a zobrazte počet klientů, kteří se nahlásili nebo nezdařili.

<pre><code lang="Log">Generated BGB task status report c:\ConfigMgr\inboxes\bgb.box\Bgb5c1db.BTS at 09/16/2019 16:46:39. (<b>PushID: 9</b> ReportedClients: 2 FailedClients: 0)
</code></pre>

Zkontrolujte zobrazení monitorování pro CMPivot z SQL pomocí `TaskID`.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}'
```

[![CMPIVOT dotazy SQL pro řešení potíží ve verzi 1902](media/cmpivot-sql-queries-1902.png)](media/cmpivot-sql-queries-1902.png#lightbox)

## <a name="troubleshoot-cmpivot-in-1810-and-earlier"></a><a name="bkmk_CMPivot-1810"></a>Řešení potíží s CMPivot v 1810 a dřívějších verzích

V Configuration Manager verze 1810 a starší Server vaše lokalita zpracovává komunikaci s klientem.

### <a name="get-information-from-the-site-server"></a>Získat informace ze serveru lokality

Ve výchozím nastavení jsou soubory protokolu webového serveru umístěny v `C:\Program Files\Microsoft Configuration Manager\logs`. Toto umístění může být odlišné, pokud jste zadali nevýchozí instalační adresář nebo převedené položky jako poskytovatel serveru SMS na jiný server.

`smsprov.log` Vyhledejte tento řádek:

<pre><code lang="Log">Auditing: User <username> initiated client operation 135 to collection &ltCollectionId>.
</code></pre>

Vyhledejte ID v okně CMPivot. Toto ID je `ClientOperationID`.

![Okno CMPivot se zvýrazněným ClientOperationID](media/cmpivot-clientoperationid.png)

Vyhledejte `TaskID` z tabulky ClientAction. `TaskID` Odpovídá `UniqueID` v tabulce ClientAction.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

V `BgbServer.log`nástroji vyhledejte `TaskID` shromážděné údaje z SQL. Je označený `TaskGUID`. Příklad:

<pre><code lang="Log">Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: <b>F8C7C37F-B42B-4C0A-B050-2BB44DF1098A</b> TaskType: 15
TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGF...truncated...to 5 clients with throttling (strategy: 1 param: 42)
Finished sending push task (PushID: 260 TaskID: 258) to 5 clients
</code></pre>

### <a name="client-logs"></a>Protokoly klienta

Po zjištění informací ze serveru lokality ověřte protokoly klienta. Ve výchozím nastavení se protokoly klienta nacházejí v `C:\Windows\CCM\Logs`nástroji.

V `CcmNotificationAgent.log`nástroji vyhledejte protokoly, které jsou podobné následujícímu záznamu:  

<pre><code lang="Log"><b>Error! Bookmark not defined.</b>+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp (truncated log entry)
</code></pre>

`Scripts.log` Podívejte se `TaskID`na. V následujícím příkladu vidíte `Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}`:

<pre><code lang="Log">Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14
State message: Task Id <b>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</b>
</code></pre>

Oblast hledání `StateMessage.log`. V následujícím příkladu vidíte, že `TaskID` se nachází poblíž dolního okraje zprávy vedle: `<Param>`

``` XML
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>

Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

### <a name="review-messages-on-the-site-server"></a>Zkontrolovat zprávy na serveru lokality

Otevřete `statesys.log` a zjistěte, zda je zpráva přijata a zpracována. V následujícím příkladu vidíte `TaskID` poblíž dolní části zprávy vedle. `<Param>` Pokud chcete zobrazit tyto položky protokolu, povolte [podrobné protokolování](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) na komponentě SMS_STATE_SYSTEM.

``` XML
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

Pokud zpráva nebyla zpracována, podívejte se do složky Doručená pošta zpráv o stavu. Výchozí umístění doručené pošty `C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\`je. Vyhledejte soubory v těchto umístěních:

- Příchozí
- Škod
- Proces

Podívejte se do zobrazení monitorování pro CMPivot z SQL pomocí `TaskID`.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

>[!NOTE]
>Pro klienty, kteří používají verzi 1810 nebo vyšší, se zasílání zpráv o stavu nepoužívá, pokud je výstup větší než 80 KB. Při řešení potíží s CMPivot v těchto případech můžete získat další informace, když povolíte podrobné protokolování v rámci sady MPs a SMS_MESSAGE_PROCESSING_ENGINE serveru lokality. Informace o tom, jak povolit podrobné protokolování, najdete v tématu [Možnosti protokolování serveru lokality](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).
>
> Informace o řešení potíží najdete v následujících protokolech:
>
> - `MP_Relay.log`
> - `SMS_MESSAGE_PROCESSING_ENGINE.log`

## <a name="next-steps"></a>Další kroky

- [Použití CMPivot](cmpivot.md)
- [Vytváření a spouštění powershellových skriptů](../../../apps/deploy-use/create-deploy-scripts.md)
