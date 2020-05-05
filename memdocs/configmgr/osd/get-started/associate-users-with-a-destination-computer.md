---
title: Přidružení uživatelů k počítači
titleSuffix: Configuration Manager
description: Nakonfigurujte Configuration Manager pro přidružení uživatelů k cílovým počítačům při nasazování operačních systémů.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3a77e06dd2502b9007244ff9a3c9c9922fea592
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724199"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Přidružte uživatele k cílovému počítači v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Když použijete Configuration Manager k nasazení operačních systémů, můžete přidružit uživatele k cílovému počítači. Tato možnost funguje bez ohledu na to, jestli je jeden uživatel nebo více uživatelů primárními uživateli cílového počítače.  

Spřažení uživatelských zařízení podporuje správu zaměřenou na uživatele při nasazování aplikací. Pokud přidružíte uživatele k cílovému počítači, do kterého chcete nainstalovat operační systém, můžete později nasadit aplikace pro tohoto uživatele a aplikace se automaticky nainstalují do cílového počítače. I když během nasazování operačního systému můžete nakonfigurovat podporu spřažení uživatelských zařízení, nemůžete použít spřažení uživatelských zařízení k nasazení operačního systému.  

Další informace o spřažení uživatelských zařízení najdete v tématu [propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Existuje několik způsobů, kterými můžete integrovat spřažení uživatelských zařízení do nasazení operačního systému. Spřažení uživatelských zařízení můžete integrovat do nasazení PXE, nasazení na spouštěcí a předzpracovaná média.  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>Vytvoření pořadí úkolů obsahujícího proměnnou **SMSTSAssignUsersMode**

Přidejte proměnnou **SMSTSAssignUsersMode** na začátek pořadí úkolů pomocí kroku [nastavit proměnnou pořadí úloh](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) . Tato proměnná určuje, jak pořadí úloh zpracovává informace o uživateli.

Další informace najdete v tématu [proměnné pořadí úkolů](../understand/task-sequence-variables.md#SMSTSAssignUsersMode).


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>Vytvoření předstartovního příkazu, který získává informace o uživateli

Předstartovní příkaz může být VBScript se vstupním polem. Může to být také aplikace HTML (HTA), která ověřuje zadaná uživatelská data. 

Tento Předstartovní příkaz musí nastavit proměnnou **SMSTSUdaUsers** , která se používá při spuštění pořadí úkolů. Tuto proměnnou lze nastavit v počítači, v kolekci nebo jako proměnnou pořadí úloh.

Další informace najdete v tématu [proměnné pořadí úkolů](../understand/task-sequence-variables.md#SMSTSUDAUsers).


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>Konfigurace způsobu, jakým distribuční body a média přiřazují uživatele k cílovému počítači

Distribuční bod nebo médium podporuje přiřazování uživatelů k cílovému počítači, kde je operační systém nasazen. Použijte jednu z následujících metod: 

- [Konfigurace distribučního bodu pro příjem požadavků na spouštění pomocí technologie PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)  
- [Vytvoření spouštěcího média](../deploy-use/create-bootable-media.md)  
- [Vytvoření předzpracovaného média](../deploy-use/create-prestaged-media.md)  


Konfigurace podpory spřažení uživatelských zařízení nemá předdefinovanou metodu pro ověření identity uživatele. Toto chování je důležité, když pracovník zřídí počítač a zadá informace jménem uživatele. Kromě nastavení způsobu, jakým pořadí úloh zpracovává informace o uživateli, konfiguruje tyto možnosti v distribučním bodě a na médiu možnost omezit nasazení, která se spouštějí při spuštění PXE nebo z konkrétního typu média.
