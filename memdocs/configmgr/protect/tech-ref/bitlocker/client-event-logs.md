---
title: Protokoly klientských událostí
titleSuffix: Configuration Manager
description: Technické informace o možných záznamech klienta BitLocker (MBAM) v protokolu událostí systému Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4043af4aa30942a5e8e1f7d2a3d1017c1e72d89f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722057"
---
# <a name="client-event-logs"></a>Protokoly klientských událostí

*Platí pro: Configuration Manager (Current Branch)*

<!--3601034-->

V klientovi Configuration Manager, do kterého nasazujete zásadu správy BitLockeru, použijte Prohlížeč událostí Windows k zobrazení protokolů událostí klienta BitLockeru. Přejít na **protokoly aplikací a služeb**, **Microsoft**, **Windows**, **MBAM** pro protokoly událostí [správce](#admin) i [operační](#operational) systémy.

## <a name="admin"></a>Správce

### <a name="2-volumeenactmentfailed"></a>2: VolumeEnactmentFailed

Při použití zásad MBAM došlo k chybě.

#### <a name="error-code--2144272219"></a>Kód chyby:-2144272219

Podrobnosti: nástroj BitLocker Drive Encryption podporuje jenom využité místo šifrování jenom pro dynamicky zřízené úložiště.

K této chybě dochází, pokud se pokusíte použít BitLocker k šifrování virtuálního počítače se systémem Windows 10 verze 1803 nebo starším. Starší verze Windows 10 nepodporují šifrování celého disku. Zásady správy BitLockeru vynutily úplné šifrování disku.

#### <a name="error-code--2147024774"></a>Kód chyby:-2147024774

Podrobnosti: oblast dat předaná systémovému volání je příliš malá.

Chcete-li tento problém vyřešit, restartujte počítač.

### <a name="4-transferstatusdatafailed"></a>4: TransferStatusDataFailed

Při odesílání dat o stavu šifrování došlo k chybě.

### <a name="8-systemvolumenotfound"></a>8: SystemVolumeNotFound

Chybí systémový svazek. SystemVolume je potřeba k šifrování jednotky operačního systému.

### <a name="9-tpmnotfound"></a>9: TPMNotFound

Chybí hardware TPM. ČIP TPM je nutný k šifrování jednotky operačního systému s jakýmkoli ochranným modulem TPM.

### <a name="10-machinehwexempted"></a>10: MachineHWExempted

Počítač je vyloučený z šifrování. Stav hardwaru počítače: vyloučené

### <a name="11-machinehwunknown"></a>11: MachineHWUnknown

Počítač je vyloučený z šifrování. Stav hardwaru počítače: neznámý

### <a name="12-hwcheckfailed"></a>12: HWCheckFailed

Kontroly výjimky hardwaru se nezdařila.

### <a name="13-userisexempted"></a>13: UserIsExempted

Uživatel je od šifrování nešifrovaný.

### <a name="14-useriswaiting"></a>14: UserIsWaiting

Uživatel požadoval výjimku.

### <a name="15-userexemptioncheckfailed"></a>15: UserExemptionCheckFailed

Ověření výjimky uživatele se nezdařilo.

### <a name="16-userpostponed"></a>16: UserPostponed

Uživatel odložil proces šifrování.

### <a name="17-tpminitializationfailed"></a>17: TPMInitializationFailed

Inicializace čipu TPM se nezdařila. Uživatel odmítl změny v systému BIOS.

### <a name="18-coreservicedown"></a>18: CoreServiceDown

Nelze se připojit k MBAM Recovery a hardwarové službě.

#### <a name="error-code--2147024809"></a>Kód chyby:-2147024809

Podrobnosti: parametr je nesprávný.

K této chybě dochází, pokud web není HTTPS, nebo klient nemá certifikát PKI.

### <a name="20-policymismatch"></a>20: PolicyMismatch

Zásada správy BitLockeru je v konfliktu nebo je poškozená.

### <a name="21-conflictingosvolumepolicies"></a>21: ConflictingOSVolumePolicies

Byly zjištěny konflikty zásad šifrování svazku operačního systému. Zkontrolujte zásady BitLockeru související s ochranou jednotky operačního systému.

### <a name="22-conflictingfddvolumepolicies"></a>22: ConflictingFDDVolumePolicies

Byl zjištěn konflikt zásad šifrování svazku pevné datové jednotky. Zkontrolujte zásady BitLockeru související s pevnými ochranou jednotek datové jednotky.

### <a name="27-encryptionfailednodra"></a>27: EncryptionFailedNoDra

Při šifrování došlo k chybě. Ochrana agenta obnovování dat (DRA) se vyžaduje v režimu FIPS pro předWindows 8.1 počítače.

### <a name="34-tpmlockoutresetfailed"></a>34: TpmLockOutResetFailed

Nepovedlo se resetovat uzamčení čipu TPM.

### <a name="36-tpmownerauthretrievalfailed"></a>36: TpmOwnerAuthRetrievalFailed

Nepovedlo se načíst OwnerAuth TPM ze služeb MBAM.

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37: WmiProviderDllSearchPathUpdateFailed

Nepovedlo se aktualizovat cestu pro hledání knihovny DLL pro zprostředkovatele rozhraní WMI.

### <a name="38-timedoutwaitingforwmiprovider"></a>38: TimedOutWaitingForWmiProvider

Agent se zastavuje. Vypršel časový limit při čekání na instanci zprostředkovatele rozhraní WMI MBAM.

## <a name="operational"></a>Funkční

### <a name="1-volumeenactmentsuccessful"></a>1: VolumeEnactmentSuccessful

Zásady správy BitLockeru se úspěšně nastavily.

### <a name="3-transferstatusdatasuccessful"></a>3: TransferStatusDataSuccessful

Data o stavu šifrování se úspěšně odeslala.

### <a name="19-coreserviceup"></a>19: CoreServiceUp

Úspěšně připojeno k MBAM obnovení a hardwarové službě

### <a name="28-tpmownerauthescrowed"></a>28: TpmOwnerAuthEscrowed

ČIP TPM OwnerAuth byl uloží.

### <a name="29-recoverykeyescrowed"></a>29: RecoveryKeyEscrowed

Obnovovací klíč BitLockeru pro svazek byl uloží.

### <a name="30-recoverykeyreset"></a>30: RecoveryKeyReset

Obnovovací klíč BitLockeru pro svazek byl aktualizován.

### <a name="31-enforcepolicydateset"></a>31: EnforcePolicyDateSet

Vynutilo datum zásad... byl nastaven pro svazek

### <a name="32-enforcepolicydatecleared"></a>32: EnforcePolicyDateCleared

Vynutilo datum zásad... pro svazek byl vymazán.

### <a name="33-tpmlockoutresetsucceeded"></a>33: TpmLockOutResetSucceeded

Uzamčení čipu TPM se úspěšně obnovilo.

### <a name="35-tpmownerauthretrievalsucceeded"></a>35: TpmOwnerAuthRetrievalSucceeded

Úspěšně se načetl OwnerAuth TPM ze služeb MBAM.

### <a name="39-removabledrivemounted"></a>39: RemovableDriveMounted

Vyměnitelná jednotka byla připojena.

### <a name="40-removabledrivedismounted"></a>40: RemovableDriveDismounted

Vyměnitelná jednotka byla odpojena.

### <a name="41-failedtoenactendpointunreachable"></a>41: FailedToEnactEndpointUnreachable

Nepovedlo se připojit k MBAM obnovení a hardwarové službě se zabránilo úspěšnému uplatnění zásad správy BitLockeru na svazek.

### <a name="42-failedtoenactlockedvolume"></a>42: FailedToEnactLockedVolume

Stav zamčeného svazku zabránil úspěšnému použití zásad správy nástroje BitLocker pro daný svazek.

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43: TransferStatusDataFailedEndpointUnreachable

Nepovedlo se připojit ke službě MBAM dodržování předpisů a stavu, což zabránilo přenosu dat o stavu šifrování.

## <a name="see-also"></a>Viz také

Další informace o použití těchto protokolů najdete v tématu [protokoly událostí BitLockeru](about-event-logs.md).

Další informace o řešení potíží najdete v tématu [řešení potíží s nástrojem BitLocker](troubleshoot.md).
