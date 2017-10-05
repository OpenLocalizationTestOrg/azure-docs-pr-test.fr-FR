---
title: "Outil de diagnostic pour la résolution des problèmes de l’appareil StorSimple 8000 | Microsoft Docs"
description: "Décrit les modes de l’appareil StorSimple et explique comment utiliser Windows PowerShell for StorSimple pour changer le mode de l’appareil."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 8fae7bb357f8e5e8eff249edfe3a2aaafe04283c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-diagnostics-tool-to-troubleshoot-8000-series-device-issues"></a><span data-ttu-id="68449-103">Utiliser l’outil de diagnostic StorSimple pour résoudre les problèmes des appareils de la gamme 8000</span><span class="sxs-lookup"><span data-stu-id="68449-103">Use the StorSimple Diagnostics Tool to troubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="68449-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="68449-104">Overview</span></span>

<span data-ttu-id="68449-105">L’outil de diagnostic StorSimple permet de détecter les problèmes liés au système, aux performances, au réseau et à l’intégrité des composants matériels sur un appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68449-105">The StorSimple Diagnostics tool diagnoses issues related to system, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="68449-106">L’outil de diagnostic peut être utilisé dans différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="68449-106">The diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="68449-107">Ces scénarios incluent la planification de la charge de travail, le déploiement d’un appareil StorSimple, l’évaluation de l’environnement réseau et la détermination des performances d’un appareil opérationnel.</span><span class="sxs-lookup"><span data-stu-id="68449-107">These scenarios include workload planning, deploying a StorSimple device, assessing the network environment, and determining the performance of an operational device.</span></span> <span data-ttu-id="68449-108">Cet article offre une vue d’ensemble de l’outil de diagnostic et explique comment utiliser cet outil avec un appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68449-108">This article provides an overview of the diagnostics tool and describes how the tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="68449-109">L’outil de diagnostic est destiné principalement aux appareils locaux de la gamme StorSimple 8000 (8100 et 8600).</span><span class="sxs-lookup"><span data-stu-id="68449-109">The diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="68449-110">Exécuter l’outil de diagnostic</span><span class="sxs-lookup"><span data-stu-id="68449-110">Run diagnostics tool</span></span>

<span data-ttu-id="68449-111">Cet outil peut être exécuté à partir de l’interface Windows PowerShell de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68449-111">This tool can be run via the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="68449-112">Pour accéder à l’interface locale de votre appareil, deux options s’offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="68449-112">There are two ways to access the local interface of your device:</span></span>

* <span data-ttu-id="68449-113">[Utiliser PuTTY pour vous connecter à la console série de l’appareil](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="68449-113">[Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="68449-114">[Accéder à l’outil à distance via Windows PowerShell pour StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="68449-114">[Remotely access the tool via the Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="68449-115">Dans cet article, nous partons du principe que vous vous êtes connecté à la console série de l’appareil via PuTTY.</span><span class="sxs-lookup"><span data-stu-id="68449-115">In this article, we assume that you have connected to the device serial console via PuTTY.</span></span>

#### <a name="to-run-the-diagnostics-tool"></a><span data-ttu-id="68449-116">Pour exécuter l’outil de diagnostic</span><span class="sxs-lookup"><span data-stu-id="68449-116">To run the diagnostics tool</span></span>

<span data-ttu-id="68449-117">Une fois que vous êtes connecté à l’interface Windows PowerShell de l’appareil, procédez comme suit pour exécuter l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="68449-117">Once you have connected to the Windows PowerShell interface of the device, perform the following steps to run the cmdlet.</span></span>
1. <span data-ttu-id="68449-118">Ouvrez une session sur la console série de l'appareil en suivant les étapes dans [Utilisation de PuTTY pour se connecter à la console série de l'appareil](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="68449-118">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="68449-119">Tapez la commande suivante : </span><span class="sxs-lookup"><span data-stu-id="68449-119">Type the following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="68449-120">Si le paramètre d’étendue (Scope) n’est pas spécifié, l’applet de commande exécute tous les tests de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="68449-120">If the scope parameter is not specified, the cmdlet executes all the diagnostic tests.</span></span> <span data-ttu-id="68449-121">Ceux-ci incluent des tests du système, de l’intégrité des composants matériels, du réseau et des performances.</span><span class="sxs-lookup"><span data-stu-id="68449-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="68449-122">Pour exécuter un test spécifique, spécifiez le paramètre Scope.</span><span class="sxs-lookup"><span data-stu-id="68449-122">To run only a specific test, specify the scope parameter.</span></span> <span data-ttu-id="68449-123">Par exemple, pour exécuter uniquement le test du réseau, tapez :</span><span class="sxs-lookup"><span data-stu-id="68449-123">For instance, to run only the network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="68449-124">Sélectionnez et copiez la sortie de la fenêtre PuTTY dans un fichier texte pour approfondir l’analyse.</span><span class="sxs-lookup"><span data-stu-id="68449-124">Select and copy the output from the PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-to-use-the-diagnostics-tool"></a><span data-ttu-id="68449-125">Scénarios d’utilisation de l’outil de diagnostic</span><span class="sxs-lookup"><span data-stu-id="68449-125">Scenarios to use the diagnostics tool</span></span>

<span data-ttu-id="68449-126">L’outil de diagnostic permet de résoudre les problèmes de réseau, de performances, de système et d’intégrité matérielle de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-126">Use the diagnostics tool to troubleshoot the network, performance, system, and hardware health of the system.</span></span> <span data-ttu-id="68449-127">Voici quelques scénarios possibles :</span><span class="sxs-lookup"><span data-stu-id="68449-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="68449-128">**Appareil hors connexion** : votre appareil de la gamme StorSimple 8000 est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="68449-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="68449-129">Toutefois, dans l’interface Windows PowerShell, les deux contrôleurs semblent être opérationnels.</span><span class="sxs-lookup"><span data-stu-id="68449-129">However, from the Windows PowerShell interface, it seems that both the controllers are up and running.</span></span>
    * <span data-ttu-id="68449-130">Vous pouvez utiliser cet outil pour déterminer l’état du réseau.</span><span class="sxs-lookup"><span data-stu-id="68449-130">You can use this tool to then determine the network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="68449-131">N’utilisez pas cet outil pour évaluer les performances et les paramètres réseau sur un appareil avant son inscription (ou sa configuration via l’Assistant d’installation).</span><span class="sxs-lookup"><span data-stu-id="68449-131">Do not use this tool to assess performance and network settings on a device before the registration (or configuring via setup wizard).</span></span> <span data-ttu-id="68449-132">Une adresse IP valide est affectée à l’appareil lors de sa configuration via l’Assistant installation et de son inscription.</span><span class="sxs-lookup"><span data-stu-id="68449-132">A valid IP is assigned to the device during setup wizard and registration.</span></span> <span data-ttu-id="68449-133">Vous pouvez exécuter cette applet de commande sur un appareil qui n’est pas inscrit pour évaluer l’intégrité matérielle et le système.</span><span class="sxs-lookup"><span data-stu-id="68449-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="68449-134">Utilisez le paramètre Scope, par exemple :</span><span class="sxs-lookup"><span data-stu-id="68449-134">Use the scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="68449-135">**Problèmes d’appareil persistants** : vous rencontrez des problèmes d’appareil qui semblent persister.</span><span class="sxs-lookup"><span data-stu-id="68449-135">**Persistent device issues** - You are experiencing device issues that seem to persist.</span></span> <span data-ttu-id="68449-136">Par exemple, son inscription échoue.</span><span class="sxs-lookup"><span data-stu-id="68449-136">For instance, registration is failing.</span></span> <span data-ttu-id="68449-137">Vous pouvez également rencontrer des problèmes alors que l’appareil a été inscrit avec succès et que vous l’utilisez depuis un certain temps.</span><span class="sxs-lookup"><span data-stu-id="68449-137">You could also be experiencing device issues after the device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="68449-138">Dans ce cas, utilisez cet outil pour procéder à un dépannage préliminaire avant d’enregistrer une demande de service auprès du Support Microsoft.</span><span class="sxs-lookup"><span data-stu-id="68449-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="68449-139">Nous vous recommandons d’exécuter cet outil et de consigner sa sortie.</span><span class="sxs-lookup"><span data-stu-id="68449-139">We recommend that you run this tool and capture the output of this tool.</span></span> <span data-ttu-id="68449-140">Vous pouvez ensuite fournir cette sortie à la prise en charge afin d’accélérer la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="68449-140">You can then provide this output to Support to expedite troubleshooting.</span></span>
    * <span data-ttu-id="68449-141">En cas de défaillances de composants matériels ou de clusters, vous devez enregistrer une demande de Support.</span><span class="sxs-lookup"><span data-stu-id="68449-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="68449-142">**Faibles performances de l’appareil** : votre appareil StorSimple est lent.</span><span class="sxs-lookup"><span data-stu-id="68449-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="68449-143">Dans ce cas, exécutez cette applet de commande avec le paramètre Scope défini sur Performance.</span><span class="sxs-lookup"><span data-stu-id="68449-143">In this case, run this cmdlet with scope parameter set to performance.</span></span> <span data-ttu-id="68449-144">Analysez la sortie.</span><span class="sxs-lookup"><span data-stu-id="68449-144">Analyze the output.</span></span> <span data-ttu-id="68449-145">Vous obtenez les latences de lecture-écriture dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="68449-145">You get the cloud read-write latencies.</span></span> <span data-ttu-id="68449-146">Utilisez les latences signalées en tant que cible maximale possible, prenez en compte une certaine surcharge pour le traitement interne des données, puis déployez les charges de travail sur le système.</span><span class="sxs-lookup"><span data-stu-id="68449-146">Use the reported latencies as maximum achievable target, factor in some overhead for the internal data processing, and then deploy the workloads on the system.</span></span> <span data-ttu-id="68449-147">Pour obtenir des informations sur l’utilisation du test du réseau pour résoudre les problèmes de performances de l’appareil, consultez la section [Test du réseau](#network-test).</span><span class="sxs-lookup"><span data-stu-id="68449-147">For more information, go to [Use the network test to troubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="68449-148">Tests de diagnostic et exemples de sorties</span><span class="sxs-lookup"><span data-stu-id="68449-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="68449-149">Test du matériel</span><span class="sxs-lookup"><span data-stu-id="68449-149">Hardware test</span></span>

<span data-ttu-id="68449-150">Ce test permet de déterminer l’état des composants matériels, du microprogramme USM et du microprogramme de disque de votre système.</span><span class="sxs-lookup"><span data-stu-id="68449-150">This test determines the status of the hardware components, the USM firmware, and the disk firmware running on your system.</span></span>

* <span data-ttu-id="68449-151">Les composants matériels signalés sont ceux pour lesquels le test a échoué ou qui ne sont pas présents dans le système.</span><span class="sxs-lookup"><span data-stu-id="68449-151">The hardware components reported are those components that failed the test or are not present in the system.</span></span>
* <span data-ttu-id="68449-152">Les versions du microprogramme USM et du microprogramme de disque sont indiquées pour le contrôleur 0, le contrôleur 1 et les composants partagés de votre système.</span><span class="sxs-lookup"><span data-stu-id="68449-152">The USM firmware and disk firmware versions are reported for the Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="68449-153">Pour obtenir une liste complète des composants matériels, consultez :</span><span class="sxs-lookup"><span data-stu-id="68449-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="68449-154">Composants du boîtier principal</span><span class="sxs-lookup"><span data-stu-id="68449-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="68449-155">Composants du boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="68449-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="68449-156">Si le test du matériel signale des composants défectueux, [enregistrez une demande de service auprès du Support Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="68449-156">If the hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="68449-157">Exemple de sortie du test du matériel sur un appareil 8100</span><span class="sxs-lookup"><span data-stu-id="68449-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="68449-158">Voici un exemple de sortie pour un appareil StorSimple 8100.</span><span class="sxs-lookup"><span data-stu-id="68449-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="68449-159">Le modèle 8100 ne présente pas de boîtier EBOD.</span><span class="sxs-lookup"><span data-stu-id="68449-159">In the 8100 model device, the EBOD enclosure is not present.</span></span> <span data-ttu-id="68449-160">Par conséquent, les composants du contrôleur du boîtier EBOD ne sont pas signalés.</span><span class="sxs-lookup"><span data-stu-id="68449-160">Hence, the EBOD controller components are not reported.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a><span data-ttu-id="68449-161">Test du système</span><span class="sxs-lookup"><span data-stu-id="68449-161">System test</span></span>

<span data-ttu-id="68449-162">Ce test fait état des informations système, des mises à jour disponibles, des informations sur les clusters et des informations sur les services pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-162">This test reports the system information, the updates available, the cluster information, and the service information for your device.</span></span>

* <span data-ttu-id="68449-163">Les informations système incluent le modèle, le numéro de série de l’appareil, le fuseau horaire, l’état du contrôleur et le détail de la version du logiciel exécuté sur le système.</span><span class="sxs-lookup"><span data-stu-id="68449-163">The system information includes the model, device serial number, time zone, controller status, and the detailed software version running on the system.</span></span> <span data-ttu-id="68449-164">Pour comprendre les différents paramètres du système signalés dans la sortie, consultez [Interprétation des informations système](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="68449-164">To understand the various system parameters reported as the output, go to [Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="68449-165">Les informations sur la disponibilité de mises à jour indiquent si des mises à jour sont disponibles pour les modes normal et maintenance et, le cas échéant, le nom des packages associés.</span><span class="sxs-lookup"><span data-stu-id="68449-165">The update availability reports whether the regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="68449-166">Si `RegularUpdates` et `MaintenanceModeUpdates` présentent la valeur `false`, cela indique qu’aucune mise à jour n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="68449-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that the updates are not available.</span></span> <span data-ttu-id="68449-167">Votre appareil est à jour.</span><span class="sxs-lookup"><span data-stu-id="68449-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="68449-168">Les informations sur les clusters incluent des informations sur les différents composants logiques de l’ensemble des groupes de clusters HCS et sur leur état respectif.</span><span class="sxs-lookup"><span data-stu-id="68449-168">The cluster information contains the information on various logical components of all the HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="68449-169">Si un groupe de clusters hors connexion apparaît dans cette section du rapport, [contactez le Support Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="68449-169">If you see an offline cluster group in this section of the report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="68449-170">Les informations sur les services incluent le nom et l’état de tous les services HCS et CiS exécutés sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-170">The service information includes the names and statuses of all the HCS and CiS services running on your device.</span></span> <span data-ttu-id="68449-171">Ces informations aident le Support Microsoft à résoudre les problèmes d’appareil associés.</span><span class="sxs-lookup"><span data-stu-id="68449-171">This information is helpful for the Microsoft Support in troubleshooting the device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="68449-172">Exemple de sortie du test du système sur un appareil 8100</span><span class="sxs-lookup"><span data-stu-id="68449-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="68449-173">Voici un exemple de sortie du test du système sur un appareil 8100.</span><span class="sxs-lookup"><span data-stu-id="68449-173">Here is a sample output of the system test run on an 8100 device.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a><span data-ttu-id="68449-174">Test du réseau</span><span class="sxs-lookup"><span data-stu-id="68449-174">Network test</span></span>

<span data-ttu-id="68449-175">Ce test vérifie l’état des interfaces réseau, des ports, de la connectivité des serveurs DNS et NTP, du certificat SSL, des informations d’identification de compte de stockage, de la connectivité aux serveurs de mise à jour et de la connectivité du proxy web sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68449-175">This test validates the status of the network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity to the Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="68449-176">Exemple de sortie du test du réseau lorsque seule l’interface DATA0 est activée</span><span class="sxs-lookup"><span data-stu-id="68449-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="68449-177">Voici un exemple de sortie pour l’appareil 8100.</span><span class="sxs-lookup"><span data-stu-id="68449-177">Here is a sample output of the 8100 device.</span></span> <span data-ttu-id="68449-178">Vous pouvez observer dans la sortie que :</span><span class="sxs-lookup"><span data-stu-id="68449-178">You can see in the output that:</span></span>
* <span data-ttu-id="68449-179">Seules les interfaces réseau DATA0 et DATA1 sont activées et configurées.</span><span class="sxs-lookup"><span data-stu-id="68449-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="68449-180">Les interfaces DATA2 à DATA5 ne sont pas activées dans le portail.</span><span class="sxs-lookup"><span data-stu-id="68449-180">DATA 2 - 5 are not enabled in the portal.</span></span>
* <span data-ttu-id="68449-181">La configuration du serveur DNS est valide et l’appareil peut se connecter via le serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="68449-181">The DNS server configuration is valid and the device can connect via the DNS server.</span></span>
* <span data-ttu-id="68449-182">La connectivité du serveur NTP est également correcte.</span><span class="sxs-lookup"><span data-stu-id="68449-182">The NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="68449-183">Les ports 80 et 443 sont ouverts.</span><span class="sxs-lookup"><span data-stu-id="68449-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="68449-184">Toutefois, le port 9354 est bloqué.</span><span class="sxs-lookup"><span data-stu-id="68449-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="68449-185">Conformément à la [configuration réseau requise pour le système](storsimple-system-requirements.md), vous devez ouvrir ce port pour la communication avec Service Bus.</span><span class="sxs-lookup"><span data-stu-id="68449-185">Based on the [system network requirements](storsimple-system-requirements.md), you need to open this port for the service bus communication.</span></span>
* <span data-ttu-id="68449-186">Le certificat SSL est valide.</span><span class="sxs-lookup"><span data-stu-id="68449-186">The SSL certification is valid.</span></span>
* <span data-ttu-id="68449-187">L’appareil peut se connecter au compte de stockage _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="68449-187">The device can connect to the storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="68449-188">La connectivité aux serveurs de mise à jour est valide.</span><span class="sxs-lookup"><span data-stu-id="68449-188">The connectivity to Update servers is valid.</span></span>
* <span data-ttu-id="68449-189">Le proxy web n’est pas configuré sur cet appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-189">The web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="68449-190">Exemple de sortie du test du réseau lorsque les interfaces DATA0 et DATA1 sont activées</span><span class="sxs-lookup"><span data-stu-id="68449-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a><span data-ttu-id="68449-191">Test de performance</span><span class="sxs-lookup"><span data-stu-id="68449-191">Performance test</span></span>

<span data-ttu-id="68449-192">Ce test fait état des performances cloud via les latences de lecture-écriture dans le cloud pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-192">This test reports the cloud performance via the cloud read-write latencies for your device.</span></span> <span data-ttu-id="68449-193">Cet outil peut être utilisé afin de déterminer les performances cloud potentielles de l’appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68449-193">This tool can be used to establish a baseline of the cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="68449-194">L’outil signale les performances maximales (scénario optimal pour les latences de lecture-écriture) que vous pouvez obtenir pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="68449-194">The tool reports the maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="68449-195">Comme l’outil signale les performances maximales possibles, nous pouvons utiliser les latences de lecture-écriture signalées en tant que cibles lors du déploiement des charges de travail.</span><span class="sxs-lookup"><span data-stu-id="68449-195">As the tool reports the maximum achievable performance, we can use the reported read-write latencies as targets when deploying the workloads.</span></span>

<span data-ttu-id="68449-196">Le test simule les tailles d’objet blob associées aux types différents de volumes sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-196">The test simulates the blob sizes associated with the different volume types on the device.</span></span> <span data-ttu-id="68449-197">Les volumes hiérarchisés standard et les sauvegardes des volumes épinglés localement utilisent une taille d’objet blob de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="68449-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="68449-198">Les volumes hiérarchisés avec option d’archivage activée utilisent une taille d’objet blob de 512 Ko.</span><span class="sxs-lookup"><span data-stu-id="68449-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="68449-199">Si des volumes hiérarchisés et épinglés localement sont configurés pour votre appareil, seul le test correspondant à la taille d’objet blob de 64 Ko est exécuté.</span><span class="sxs-lookup"><span data-stu-id="68449-199">If your device has tiered and locally pinned volumes configured, only the test corresponding to 64 KB blob data size is run.</span></span>

<span data-ttu-id="68449-200">Pour utiliser cet outil, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="68449-200">To use this tool, perform the following steps:</span></span>

1.  <span data-ttu-id="68449-201">Tout d’abord, créez un ensemble de volumes hiérarchisés et de volumes hiérarchisés avec option d’archivage activée.</span><span class="sxs-lookup"><span data-stu-id="68449-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="68449-202">L’outil exécutera ainsi les tests pour les tailles d’objet blob de 64 Ko et 512 Ko.</span><span class="sxs-lookup"><span data-stu-id="68449-202">This action ensures that the tool runs the tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="68449-203">Une fois que vous avez créé et configuré les volumes, exécutez l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="68449-203">Run the cmdlet after you have created and configured the volumes.</span></span> <span data-ttu-id="68449-204">Tapez :</span><span class="sxs-lookup"><span data-stu-id="68449-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="68449-205">Notez les latences de lecture-écriture signalées par l’outil.</span><span class="sxs-lookup"><span data-stu-id="68449-205">Make a note of the read-write latencies reported by the tool.</span></span> <span data-ttu-id="68449-206">L’affichage des résultats du test peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="68449-206">This test can take several minutes to run before it reports the results.</span></span>

4. <span data-ttu-id="68449-207">Si les latences de connexion sont toutes inférieures à la plage attendue, les latences signalées par l’outil peuvent être utilisées en tant que cible maximale possible lors du déploiement des charges de travail.</span><span class="sxs-lookup"><span data-stu-id="68449-207">If the connection latencies are all under the expected range, then the latencies reported by the tool can be used as maximum achievable target when deploying the workloads.</span></span> <span data-ttu-id="68449-208">Prenez en compte une certaine surcharge pour le traitement interne des données.</span><span class="sxs-lookup"><span data-stu-id="68449-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="68449-209">Si les latences de lecture-écriture signalées par l’outil de diagnostic sont élevées :</span><span class="sxs-lookup"><span data-stu-id="68449-209">If the read-write latencies reported by the diagnostics tool are high:</span></span>

    1. <span data-ttu-id="68449-210">Configurez Storage Analytics pour les services BLOB et analysez la sortie pour déterminer les latences du compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="68449-210">Configure Storage Analytics for blob services and analyze the output to understand the latencies for the Azure storage account.</span></span> <span data-ttu-id="68449-211">Pour obtenir des instructions détaillées sur l’activation et la configuration de Storage Analytics, consultez [cet article](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="68449-211">For detailed instructions, go to [enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="68449-212">Si ces latences sont également élevées et comparables aux valeurs fournies par l’outil de diagnostic StorSimple, vous devez enregistrer une demande de service auprès de Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="68449-212">If those latencies are also high and comparable to the numbers you received from the StorSimple Diagnostics tool, then you need to log a service request with Azure storage.</span></span>

    2. <span data-ttu-id="68449-213">Si les latences du compte de stockage sont faibles, contactez votre administrateur réseau pour qu’il recherche les éventuels problèmes de latence du réseau.</span><span class="sxs-lookup"><span data-stu-id="68449-213">If the storage account latencies are low, contact your network administrator to investigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="68449-214">Exemple de sortie du test des performances sur un appareil 8100</span><span class="sxs-lookup"><span data-stu-id="68449-214">Sample output of performance test run on an 8100 device</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="68449-215">Annexe : Interprétation des informations système</span><span class="sxs-lookup"><span data-stu-id="68449-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="68449-216">Le tableau ci-dessous décrit les différents paramètres Windows PowerShell dans les informations système.</span><span class="sxs-lookup"><span data-stu-id="68449-216">Here is a table describing what the various Windows PowerShell parameters in the system information map to.</span></span> 

| <span data-ttu-id="68449-217">Paramètre PowerShell</span><span class="sxs-lookup"><span data-stu-id="68449-217">PowerShell Parameter</span></span>    | <span data-ttu-id="68449-218">Description</span><span class="sxs-lookup"><span data-stu-id="68449-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="68449-219">ID de l’instance</span><span class="sxs-lookup"><span data-stu-id="68449-219">Instance ID</span></span>             | <span data-ttu-id="68449-220">Un identificateur unique ou un GUID est associé à chaque contrôleur.</span><span class="sxs-lookup"><span data-stu-id="68449-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="68449-221">Nom</span><span class="sxs-lookup"><span data-stu-id="68449-221">Name</span></span>                    | <span data-ttu-id="68449-222">Nom convivial configuré pour l’appareil via le portail Azure lors du déploiement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-222">The friendly name of the device as configured through the Azure portal during device deployment.</span></span> <span data-ttu-id="68449-223">Le nom convivial par défaut est le numéro de série de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-223">The default friendly name is the device serial number.</span></span> |
| <span data-ttu-id="68449-224">Modèle</span><span class="sxs-lookup"><span data-stu-id="68449-224">Model</span></span>                   | <span data-ttu-id="68449-225">Modèle de votre appareil de la gamme StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="68449-225">The model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="68449-226">Il peut s’agir du modèle 8100 ou 8600.</span><span class="sxs-lookup"><span data-stu-id="68449-226">The model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="68449-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="68449-227">SerialNumber</span></span>            | <span data-ttu-id="68449-228">Le numéro de série de l’appareil est attribué en usine et comprend 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="68449-228">The device serial number is assigned at the factory and is 15 characters long.</span></span> <span data-ttu-id="68449-229">Par exemple, 8600-SHX0991003G44HT indique :</span><span class="sxs-lookup"><span data-stu-id="68449-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="68449-230">8600 : modèle de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-230">8600 – Is the device model.</span></span><br><span data-ttu-id="68449-231">SHX : site de fabrication.</span><span class="sxs-lookup"><span data-stu-id="68449-231">SHX – Is the manufacturing site.</span></span><br> <span data-ttu-id="68449-232">0991003 : produit spécifique.</span><span class="sxs-lookup"><span data-stu-id="68449-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="68449-233">G44HT : les 5 derniers chiffres sont incrémentés pour créer des numéros de série uniques.</span><span class="sxs-lookup"><span data-stu-id="68449-233">G44HT- the last 5 digits are incremented to create unique serial numbers.</span></span> <span data-ttu-id="68449-234">Il ne s’agit pas nécessairement d’une suite.</span><span class="sxs-lookup"><span data-stu-id="68449-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="68449-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="68449-235">TimeZone</span></span>                | <span data-ttu-id="68449-236">Fuseau horaire configuré pour l’appareil dans le portail Azure lors du déploiement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-236">The device time zone as configured in the Azure portal during device deployment.</span></span>|
| <span data-ttu-id="68449-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="68449-237">CurrentController</span></span>       | <span data-ttu-id="68449-238">Contrôleur auquel vous êtes connecté via l’interface Windows PowerShell de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68449-238">The controller that you are connected to through the Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="68449-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="68449-239">ActiveController</span></span>        | <span data-ttu-id="68449-240">Contrôleur qui est actif sur votre appareil et contrôle toutes les opérations de réseau et de disque.</span><span class="sxs-lookup"><span data-stu-id="68449-240">The controller that is active on your device and is controlling all the network and disk operations.</span></span> <span data-ttu-id="68449-241">Il peut s’agir du contrôleur 0 ou du contrôleur 1.</span><span class="sxs-lookup"><span data-stu-id="68449-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="68449-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="68449-242">Controller0Status</span></span>       | <span data-ttu-id="68449-243">État du contrôleur 0 sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-243">The status of Controller 0 on your device.</span></span> <span data-ttu-id="68449-244">L’état du contrôleur peut être Normal, Recovery (Récupération) ou Unreachable (Inaccessible).</span><span class="sxs-lookup"><span data-stu-id="68449-244">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="68449-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="68449-245">Controller1Status</span></span>       | <span data-ttu-id="68449-246">État du contrôleur 1 sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-246">The status of Controller 1 on your device.</span></span>  <span data-ttu-id="68449-247">L’état du contrôleur peut être Normal, Recovery (Récupération) ou Unreachable (Inaccessible).</span><span class="sxs-lookup"><span data-stu-id="68449-247">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="68449-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="68449-248">SystemMode</span></span>              | <span data-ttu-id="68449-249">État général de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68449-249">The overall status of your StorSimple device.</span></span> <span data-ttu-id="68449-250">L’état de l’appareil peut être Normal, Maintenance ou Decommissioned (Retiré) (correspond à Désactivé dans le portail Azure).</span><span class="sxs-lookup"><span data-stu-id="68449-250">The device status can be normal, maintenance, or decommissioned (corresponds to deactivated in the Azure portal).</span></span>|
| <span data-ttu-id="68449-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="68449-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="68449-252">Chaîne conviviale qui correspond à la version du logiciel de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-252">The friendly string that corresponds to the device software version.</span></span> <span data-ttu-id="68449-253">Pour un système exécutant Update 4, la version conviviale du logiciel serait StorSimple 8000 Series Update 4.0.</span><span class="sxs-lookup"><span data-stu-id="68449-253">For a system running Update 4, the friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="68449-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="68449-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="68449-255">Version du logiciel HCS exécutée sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-255">The HCS software version running on your device.</span></span> <span data-ttu-id="68449-256">Par exemple, la version du logiciel HCS correspondant à StorSimple 8000 Series Update 4.0 est 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="68449-256">For instance, the HCS software version corresponding to StorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="68449-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="68449-257">ApiVersion</span></span>              | <span data-ttu-id="68449-258">Version du logiciel de l’API Windows PowerShell de l’appareil HCS.</span><span class="sxs-lookup"><span data-stu-id="68449-258">The software version of the Windows PowerShell API of the HCS device.</span></span>|
| <span data-ttu-id="68449-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="68449-259">VhdVersion</span></span>              | <span data-ttu-id="68449-260">Version du logiciel de l’image d’usine fournie avec l’appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-260">The software version of the factory image that the device was shipped with.</span></span> <span data-ttu-id="68449-261">Si vous avez rétabli les paramètres d’usine de votre appareil, ce dernier exécute cette version du logiciel.</span><span class="sxs-lookup"><span data-stu-id="68449-261">If you reset your device to factory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="68449-262">OSVersion:</span><span class="sxs-lookup"><span data-stu-id="68449-262">OSVersion</span></span>               | <span data-ttu-id="68449-263">Version du logiciel du système d’exploitation Windows Server exécuté sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-263">The software version of the Windows Server operating system running on the device.</span></span> <span data-ttu-id="68449-264">L’appareil StorSimple est basé sur Windows Server 2012 R2, qui correspond à la version 6.3.9600.</span><span class="sxs-lookup"><span data-stu-id="68449-264">The StorSimple device is based off the Windows Server 2012 R2 that corresponds to 6.3.9600.</span></span>|
| <span data-ttu-id="68449-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="68449-265">CisAgentVersion</span></span>         | <span data-ttu-id="68449-266">Version de l’agent Cis exécuté sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68449-266">The version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="68449-267">Cet agent permet de communiquer avec le service StorSimple Manager exécuté dans Azure.</span><span class="sxs-lookup"><span data-stu-id="68449-267">This agent helps communicate with the StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="68449-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="68449-268">MdsAgentVersion</span></span>         | <span data-ttu-id="68449-269">Version correspondant à l’agent Mds exécuté sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68449-269">The version corresponding to the Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="68449-270">Cet agent transfère des données au service de surveillance et de diagnostics (Monitoring and Diagnostics Service, ou MDS).</span><span class="sxs-lookup"><span data-stu-id="68449-270">This agent moves data to the Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="68449-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="68449-271">Lsisas2Version</span></span>          | <span data-ttu-id="68449-272">Version correspondant aux pilotes LSI exécutés sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68449-272">The version corresponding to the LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="68449-273">Capacité</span><span class="sxs-lookup"><span data-stu-id="68449-273">Capacity</span></span>                | <span data-ttu-id="68449-274">Capacité totale de l’appareil en octets.</span><span class="sxs-lookup"><span data-stu-id="68449-274">The total capacity of the device in bytes.</span></span>|
| <span data-ttu-id="68449-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="68449-275">RemoteManagementMode</span></span>    | <span data-ttu-id="68449-276">Indique si l’appareil peut être géré à distance via son interface Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68449-276">Indicates whether the device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="68449-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="68449-277">FipsMode</span></span>                | <span data-ttu-id="68449-278">Indique si le mode FIPS (Federal Information Processing Standard) est activé sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="68449-278">Indicates whether the United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="68449-279">La norme FIPS 140 définit les algorithmes de chiffrement qui sont approuvés pour une utilisation sur les systèmes informatiques du gouvernement fédéral américain dans le but de protéger les données sensibles.</span><span class="sxs-lookup"><span data-stu-id="68449-279">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span> <span data-ttu-id="68449-280">Pour les appareils exécutant Update 4 ou version ultérieure, le mode FIPS est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="68449-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="68449-281">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="68449-281">Next steps</span></span>

* <span data-ttu-id="68449-282">Découvrez la [syntaxe de l’applet de commande Invoke-HcsDiagnostics](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="68449-282">Learn the [syntax of the Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="68449-283">Découvrez plus en détail comment [résoudre les problèmes de déploiement](storsimple-troubleshoot-deployment.md) sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="68449-283">Learn more about how to [troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
