---
title: Appareil de tootroubleshoot StorSimple 8000 outil aaaDiagnostics | Documents Microsoft
description: "Décrit les modes du périphérique StorSimple hello et explique comment toouse Windows PowerShell pour StorSimple toochange hello mode de l’appareil."
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
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a><span data-ttu-id="d4a17-103">Utilisez les problèmes de périphériques série 8000 hello outil de diagnostic StorSimple tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="d4a17-103">Use hello StorSimple Diagnostics Tool tootroubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="d4a17-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d4a17-104">Overview</span></span>

<span data-ttu-id="d4a17-105">Hello, outil de diagnostic de StorSimple diagnostique toosystem connexes de problèmes, les performances, réseau et l’intégrité du composant matériel pour un appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4a17-105">hello StorSimple Diagnostics tool diagnoses issues related toosystem, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="d4a17-106">outil de diagnostic Hello peut être utilisé dans divers scénarios.</span><span class="sxs-lookup"><span data-stu-id="d4a17-106">hello diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="d4a17-107">Ces scénarios incluent la planification de la charge de travail, déploiement d’un appareil StorSimple, évaluer l’environnement de réseau hello et déterminer les performances d’une unité opérationnelle hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-107">These scenarios include workload planning, deploying a StorSimple device, assessing hello network environment, and determining hello performance of an operational device.</span></span> <span data-ttu-id="d4a17-108">Cet article fournit une vue d’ensemble de l’outil de diagnostic hello et décrit comment les outil hello peuvent être utilisé avec un appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4a17-108">This article provides an overview of hello diagnostics tool and describes how hello tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="d4a17-109">outil de diagnostic Hello est principalement utilisée pour les appareils StorSimple 8000 series local (8100 et 8600).</span><span class="sxs-lookup"><span data-stu-id="d4a17-109">hello diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="d4a17-110">Exécuter l’outil de diagnostic</span><span class="sxs-lookup"><span data-stu-id="d4a17-110">Run diagnostics tool</span></span>

<span data-ttu-id="d4a17-111">Cet outil peut être exécuté via l’interface Windows PowerShell de hello de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4a17-111">This tool can be run via hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="d4a17-112">Il existe deux façons tooaccess hello interface locale de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="d4a17-112">There are two ways tooaccess hello local interface of your device:</span></span>

* <span data-ttu-id="d4a17-113">[Console série du périphérique toohello tooconnect PuTTY utilisation](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d4a17-113">[Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="d4a17-114">[Accéder à distance à outil hello via hello Windows PowerShell pour StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d4a17-114">[Remotely access hello tool via hello Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="d4a17-115">Dans cet article, nous supposons que vous avez connecté la console série du périphérique toohello via PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d4a17-115">In this article, we assume that you have connected toohello device serial console via PuTTY.</span></span>

#### <a name="toorun-hello-diagnostics-tool"></a><span data-ttu-id="d4a17-116">outil de diagnostic hello toorun</span><span class="sxs-lookup"><span data-stu-id="d4a17-116">toorun hello diagnostics tool</span></span>

<span data-ttu-id="d4a17-117">Une fois que vous avez connecté l’interface Windows PowerShell de toohello du périphérique de hello, effectuer hello suivant les étapes toorun hello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d4a17-117">Once you have connected toohello Windows PowerShell interface of hello device, perform hello following steps toorun hello cmdlet.</span></span>
1. <span data-ttu-id="d4a17-118">Ouvrez une session sur la console série du périphérique toohello en suivant les étapes de hello dans [console série du périphérique toohello tooconnect utilisez PuTTY](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d4a17-118">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="d4a17-119">Tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d4a17-119">Type hello following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="d4a17-120">Si le paramètre d’étendue hello n’est pas spécifié, hello applet de commande exécute tous les tests de diagnostic hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-120">If hello scope parameter is not specified, hello cmdlet executes all hello diagnostic tests.</span></span> <span data-ttu-id="d4a17-121">Ceux-ci incluent des tests du système, de l’intégrité des composants matériels, du réseau et des performances.</span><span class="sxs-lookup"><span data-stu-id="d4a17-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="d4a17-122">toorun un test spécifique, spécifier un paramètre d’étendue hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-122">toorun only a specific test, specify hello scope parameter.</span></span> <span data-ttu-id="d4a17-123">Par exemple, toorun uniquement hello réseau test, type</span><span class="sxs-lookup"><span data-stu-id="d4a17-123">For instance, toorun only hello network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="d4a17-124">Sélectionner et copier la sortie de hello hello PuTTY fenêtre dans un fichier texte pour une analyse plus approfondie.</span><span class="sxs-lookup"><span data-stu-id="d4a17-124">Select and copy hello output from hello PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-toouse-hello-diagnostics-tool"></a><span data-ttu-id="d4a17-125">Outil de diagnostic de scénarios toouse hello</span><span class="sxs-lookup"><span data-stu-id="d4a17-125">Scenarios toouse hello diagnostics tool</span></span>

<span data-ttu-id="d4a17-126">Utilisez hello diagnostics outil tootroubleshoot hello réseau, les performances, système et matériel d’intégrité du système de hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-126">Use hello diagnostics tool tootroubleshoot hello network, performance, system, and hardware health of hello system.</span></span> <span data-ttu-id="d4a17-127">Voici quelques scénarios possibles :</span><span class="sxs-lookup"><span data-stu-id="d4a17-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="d4a17-128">**Appareil hors connexion** : votre appareil de la gamme StorSimple 8000 est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="d4a17-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="d4a17-129">Toutefois, à partir de l’interface Windows PowerShell de hello, il semble que les deux contrôleurs hello sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d4a17-129">However, from hello Windows PowerShell interface, it seems that both hello controllers are up and running.</span></span>
    * <span data-ttu-id="d4a17-130">Vous pouvez utiliser cet outil toothen déterminer l’état du réseau hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-130">You can use this tool toothen determine hello network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="d4a17-131">N’utilisez pas cette tooassess performances et les paramètres réseau sur un appareil avant l’inscription de hello (ou de configurer via l’Assistant d’installation).</span><span class="sxs-lookup"><span data-stu-id="d4a17-131">Do not use this tool tooassess performance and network settings on a device before hello registration (or configuring via setup wizard).</span></span> <span data-ttu-id="d4a17-132">Une adresse IP valide est attribuée toohello périphérique lors de l’inscription et l’Assistant installation.</span><span class="sxs-lookup"><span data-stu-id="d4a17-132">A valid IP is assigned toohello device during setup wizard and registration.</span></span> <span data-ttu-id="d4a17-133">Vous pouvez exécuter cette applet de commande sur un appareil qui n’est pas inscrit pour évaluer l’intégrité matérielle et le système.</span><span class="sxs-lookup"><span data-stu-id="d4a17-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="d4a17-134">Utilisez le paramètre d’étendue hello, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d4a17-134">Use hello scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="d4a17-135">**Problèmes de l’appareil persistant** -vous rencontrez des problèmes de l’appareil qui semblent toopersist.</span><span class="sxs-lookup"><span data-stu-id="d4a17-135">**Persistent device issues** - You are experiencing device issues that seem toopersist.</span></span> <span data-ttu-id="d4a17-136">Par exemple, son inscription échoue.</span><span class="sxs-lookup"><span data-stu-id="d4a17-136">For instance, registration is failing.</span></span> <span data-ttu-id="d4a17-137">Vous pouvez également rencontrer des problèmes de périphérique une fois hello appareil correctement inscrit et opérationnel pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="d4a17-137">You could also be experiencing device issues after hello device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="d4a17-138">Dans ce cas, utilisez cet outil pour procéder à un dépannage préliminaire avant d’enregistrer une demande de service auprès du Support Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d4a17-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="d4a17-139">Nous vous conseillons d’exécuter cette sortie hello outil et de capture de cet outil.</span><span class="sxs-lookup"><span data-stu-id="d4a17-139">We recommend that you run this tool and capture hello output of this tool.</span></span> <span data-ttu-id="d4a17-140">Vous pouvez ensuite fournir cette sortie tooSupport tooexpedite procédure de dépannage.</span><span class="sxs-lookup"><span data-stu-id="d4a17-140">You can then provide this output tooSupport tooexpedite troubleshooting.</span></span>
    * <span data-ttu-id="d4a17-141">En cas de défaillances de composants matériels ou de clusters, vous devez enregistrer une demande de Support.</span><span class="sxs-lookup"><span data-stu-id="d4a17-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="d4a17-142">**Faibles performances de l’appareil** : votre appareil StorSimple est lent.</span><span class="sxs-lookup"><span data-stu-id="d4a17-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="d4a17-143">Dans ce cas, exécutez cette applet de commande avec tooperformance de jeu de paramètres de portée.</span><span class="sxs-lookup"><span data-stu-id="d4a17-143">In this case, run this cmdlet with scope parameter set tooperformance.</span></span> <span data-ttu-id="d4a17-144">Analyser la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-144">Analyze hello output.</span></span> <span data-ttu-id="d4a17-145">Vous obtenez le cloud de hello latences de lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="d4a17-145">You get hello cloud read-write latencies.</span></span> <span data-ttu-id="d4a17-146">Hello d’utilisation signalées facteur dans une surcharge pour le traitement des données internes hello et latences en tant que cible réalisable maximale, puis déployer les charges de travail hello sur le système de hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-146">Use hello reported latencies as maximum achievable target, factor in some overhead for hello internal data processing, and then deploy hello workloads on hello system.</span></span> <span data-ttu-id="d4a17-147">Pour plus d’informations, consultez trop[utiliser les performances de l’appareil hello réseau test tootroubleshoot](#network-test).</span><span class="sxs-lookup"><span data-stu-id="d4a17-147">For more information, go too[Use hello network test tootroubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="d4a17-148">Tests de diagnostic et exemples de sorties</span><span class="sxs-lookup"><span data-stu-id="d4a17-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="d4a17-149">Test du matériel</span><span class="sxs-lookup"><span data-stu-id="d4a17-149">Hardware test</span></span>

<span data-ttu-id="d4a17-150">Ce test détermine hello état des composants matériels de hello, le microprogramme USM hello et du microprogramme du disque hello en cours d’exécution sur votre système.</span><span class="sxs-lookup"><span data-stu-id="d4a17-150">This test determines hello status of hello hardware components, hello USM firmware, and hello disk firmware running on your system.</span></span>

* <span data-ttu-id="d4a17-151">les composants de matériels Hello signalés sont ces composants ce test hello ayant échoué ou ne sont pas présentes dans le système de hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-151">hello hardware components reported are those components that failed hello test or are not present in hello system.</span></span>
* <span data-ttu-id="d4a17-152">versions du microprogramme Hello USM microprogramme et de disque sont signalées pour hello contrôleur 0, le contrôleur 1 et des composants partagés de votre système.</span><span class="sxs-lookup"><span data-stu-id="d4a17-152">hello USM firmware and disk firmware versions are reported for hello Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="d4a17-153">Pour obtenir une liste complète des composants matériels, consultez :</span><span class="sxs-lookup"><span data-stu-id="d4a17-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="d4a17-154">Composants du boîtier principal</span><span class="sxs-lookup"><span data-stu-id="d4a17-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="d4a17-155">Composants du boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="d4a17-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="d4a17-156">Si les composants en échec, des rapports de test sur du matériel hello [connectez-vous à une demande de service avec le Support technique de Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="d4a17-156">If hello hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="d4a17-157">Exemple de sortie du test du matériel sur un appareil 8100</span><span class="sxs-lookup"><span data-stu-id="d4a17-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="d4a17-158">Voici un exemple de sortie pour un appareil StorSimple 8100.</span><span class="sxs-lookup"><span data-stu-id="d4a17-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="d4a17-159">Dans l’appareil de modèle 8100 hello, hello boîtiers n’est pas présente.</span><span class="sxs-lookup"><span data-stu-id="d4a17-159">In hello 8100 model device, hello EBOD enclosure is not present.</span></span> <span data-ttu-id="d4a17-160">Par conséquent, les composants du contrôleur EBOD hello ne sont pas signalées.</span><span class="sxs-lookup"><span data-stu-id="d4a17-160">Hence, hello EBOD controller components are not reported.</span></span>

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

### <a name="system-test"></a><span data-ttu-id="d4a17-161">Test du système</span><span class="sxs-lookup"><span data-stu-id="d4a17-161">System test</span></span>

<span data-ttu-id="d4a17-162">Ce test signale des informations de système de hello, hello mises à jour disponibles, les informations de cluster hello et informations du service hello pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d4a17-162">This test reports hello system information, hello updates available, hello cluster information, and hello service information for your device.</span></span>

* <span data-ttu-id="d4a17-163">informations de système de Hello incluent hello modèle, numéro de série de périphérique, fuseau horaire, l’état du contrôleur et en cours d’exécution sur le système de hello de la version du logiciel détaillées hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-163">hello system information includes hello model, device serial number, time zone, controller status, and hello detailed software version running on hello system.</span></span> <span data-ttu-id="d4a17-164">hello toounderstand divers paramètres système signalés en tant que sortie de hello, accédez trop[interprétation des informations système](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="d4a17-164">toounderstand hello various system parameters reported as hello output, go too[Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="d4a17-165">rapports de disponibilité de mises à jour de Hello si les modes standard et la maintenance hello sont disponibles et leurs noms de package associé.</span><span class="sxs-lookup"><span data-stu-id="d4a17-165">hello update availability reports whether hello regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="d4a17-166">Si `RegularUpdates` et `MaintenanceModeUpdates` sont `false`, cela indique que les mises à jour hello ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="d4a17-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that hello updates are not available.</span></span> <span data-ttu-id="d4a17-167">Votre appareil est à jour.</span><span class="sxs-lookup"><span data-stu-id="d4a17-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="d4a17-168">cluster Hello contient hello des informations sur les différents composants de logiques de tous les groupes de cluster HCS hello et leurs États respectifs.</span><span class="sxs-lookup"><span data-stu-id="d4a17-168">hello cluster information contains hello information on various logical components of all hello HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="d4a17-169">Si vous voyez un groupe de clusters en mode hors connexion dans cette section du rapport de hello, [contactez le Support Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="d4a17-169">If you see an offline cluster group in this section of hello report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="d4a17-170">informations sur le service Hello incluent les noms de hello et états de tous les hello HCS et services des éléments de configuration en cours d’exécution sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d4a17-170">hello service information includes hello names and statuses of all hello HCS and CiS services running on your device.</span></span> <span data-ttu-id="d4a17-171">Ces informations sont utiles pour hello Support Microsoft à résoudre les problème de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-171">This information is helpful for hello Microsoft Support in troubleshooting hello device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="d4a17-172">Exemple de sortie du test du système sur un appareil 8100</span><span class="sxs-lookup"><span data-stu-id="d4a17-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="d4a17-173">Voici un exemple de sortie hello système de série de tests sur un appareil 8100.</span><span class="sxs-lookup"><span data-stu-id="d4a17-173">Here is a sample output of hello system test run on an 8100 device.</span></span>

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

### <a name="network-test"></a><span data-ttu-id="d4a17-174">Test du réseau</span><span class="sxs-lookup"><span data-stu-id="d4a17-174">Network test</span></span>

<span data-ttu-id="d4a17-175">Ce test vérifie l’état de hello des interfaces réseau de hello, ports, DNS et NTP connectivité du serveur, SSL certificat, informations d’identification du compte de stockage, serveurs de mise à jour toohello de connectivité et connectivité de proxy web sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4a17-175">This test validates hello status of hello network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity toohello Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="d4a17-176">Exemple de sortie du test du réseau lorsque seule l’interface DATA0 est activée</span><span class="sxs-lookup"><span data-stu-id="d4a17-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="d4a17-177">Voici un exemple de sortie de l’appareil de 8100 hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-177">Here is a sample output of hello 8100 device.</span></span> <span data-ttu-id="d4a17-178">Vous pouvez voir dans la sortie de hello qui :</span><span class="sxs-lookup"><span data-stu-id="d4a17-178">You can see in hello output that:</span></span>
* <span data-ttu-id="d4a17-179">Seules les interfaces réseau DATA0 et DATA1 sont activées et configurées.</span><span class="sxs-lookup"><span data-stu-id="d4a17-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="d4a17-180">2 à 5 de données ne sont pas activées dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-180">DATA 2 - 5 are not enabled in hello portal.</span></span>
* <span data-ttu-id="d4a17-181">configuration du serveur DNS Hello est valide et appareils de hello de se connecter via des serveurs DNS hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-181">hello DNS server configuration is valid and hello device can connect via hello DNS server.</span></span>
* <span data-ttu-id="d4a17-182">Hello connectivité du serveur NTP fonctionne également bien.</span><span class="sxs-lookup"><span data-stu-id="d4a17-182">hello NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="d4a17-183">Les ports 80 et 443 sont ouverts.</span><span class="sxs-lookup"><span data-stu-id="d4a17-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="d4a17-184">Toutefois, le port 9354 est bloqué.</span><span class="sxs-lookup"><span data-stu-id="d4a17-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="d4a17-185">En fonction de hello [configuration système requise du réseau](storsimple-system-requirements.md), vous devez tooopen ce port pour la communication de bus de service hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-185">Based on hello [system network requirements](storsimple-system-requirements.md), you need tooopen this port for hello service bus communication.</span></span>
* <span data-ttu-id="d4a17-186">la certification SSL de Hello est valide.</span><span class="sxs-lookup"><span data-stu-id="d4a17-186">hello SSL certification is valid.</span></span>
* <span data-ttu-id="d4a17-187">Hello appareils de se connecter compte de stockage toohello : _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="d4a17-187">hello device can connect toohello storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="d4a17-188">serveurs de tooUpdate Hello connectivité n’est valide.</span><span class="sxs-lookup"><span data-stu-id="d4a17-188">hello connectivity tooUpdate servers is valid.</span></span>
* <span data-ttu-id="d4a17-189">le proxy web Hello n’est pas configuré sur ce périphérique.</span><span class="sxs-lookup"><span data-stu-id="d4a17-189">hello web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="d4a17-190">Exemple de sortie du test du réseau lorsque les interfaces DATA0 et DATA1 sont activées</span><span class="sxs-lookup"><span data-stu-id="d4a17-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

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

### <a name="performance-test"></a><span data-ttu-id="d4a17-191">Test de performance</span><span class="sxs-lookup"><span data-stu-id="d4a17-191">Performance test</span></span>

<span data-ttu-id="d4a17-192">Ce test signale les performances du cloud hello via des latences de lecture-écriture hello cloud pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d4a17-192">This test reports hello cloud performance via hello cloud read-write latencies for your device.</span></span> <span data-ttu-id="d4a17-193">Cet outil peut être utilisé tooestablish une ligne de base des performances de cloud hello que vous pouvez obtenir avec StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4a17-193">This tool can be used tooestablish a baseline of hello cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="d4a17-194">Hello outil rapports hello performances maximales (scénario meilleur des cas de latence de lecture-écriture) que vous pouvez obtenir pour votre connexion.</span><span class="sxs-lookup"><span data-stu-id="d4a17-194">hello tool reports hello maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="d4a17-195">Outil de hello rapports des performances maximales réalisable hello, nous pouvons utiliser hello déclarée en lecture-écriture latences cibles lors du déploiement hello les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="d4a17-195">As hello tool reports hello maximum achievable performance, we can use hello reported read-write latencies as targets when deploying hello workloads.</span></span>

<span data-ttu-id="d4a17-196">test de Hello simule les tailles de blob hello associées aux types de volume différent hello sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-196">hello test simulates hello blob sizes associated with hello different volume types on hello device.</span></span> <span data-ttu-id="d4a17-197">Les volumes hiérarchisés standard et les sauvegardes des volumes épinglés localement utilisent une taille d’objet blob de 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="d4a17-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="d4a17-198">Les volumes hiérarchisés avec option d’archivage activée utilisent une taille d’objet blob de 512 Ko.</span><span class="sxs-lookup"><span data-stu-id="d4a17-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="d4a17-199">Si votre appareil a volumes attachés localement et hiérarchisés configuré, seuls hello test too64 Ko objet blob correspondant taille des données est exécutée.</span><span class="sxs-lookup"><span data-stu-id="d4a17-199">If your device has tiered and locally pinned volumes configured, only hello test corresponding too64 KB blob data size is run.</span></span>

<span data-ttu-id="d4a17-200">toouse cette outil, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d4a17-200">toouse this tool, perform hello following steps:</span></span>

1.  <span data-ttu-id="d4a17-201">Tout d’abord, créez un ensemble de volumes hiérarchisés et de volumes hiérarchisés avec option d’archivage activée.</span><span class="sxs-lookup"><span data-stu-id="d4a17-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="d4a17-202">Cette action garantit que cet outil hello exécute les tests de hello 64 Ko et 512 Ko pour les tailles des objets blob.</span><span class="sxs-lookup"><span data-stu-id="d4a17-202">This action ensures that hello tool runs hello tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="d4a17-203">Exécuter l’applet de commande hello après avoir créé et configuré les volumes hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-203">Run hello cmdlet after you have created and configured hello volumes.</span></span> <span data-ttu-id="d4a17-204">Entrez :</span><span class="sxs-lookup"><span data-stu-id="d4a17-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="d4a17-205">Prenez note des latences de lecture-écriture hello signalés par l’outil de hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-205">Make a note of hello read-write latencies reported by hello tool.</span></span> <span data-ttu-id="d4a17-206">Ce test peut prendre plusieurs minutes toorun avant de signaler les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-206">This test can take several minutes toorun before it reports hello results.</span></span>

4. <span data-ttu-id="d4a17-207">Si le temps de latence de connexion hello sont tous sous hello plages attendues, puis hello latences signalés par l’outil de hello est utilisable comme cible réalisable maximale lors du déploiement de charges de travail hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-207">If hello connection latencies are all under hello expected range, then hello latencies reported by hello tool can be used as maximum achievable target when deploying hello workloads.</span></span> <span data-ttu-id="d4a17-208">Prenez en compte une certaine surcharge pour le traitement interne des données.</span><span class="sxs-lookup"><span data-stu-id="d4a17-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="d4a17-209">Si la latence de lecture-écriture hello signalés par outil de diagnostic hello sont élevées :</span><span class="sxs-lookup"><span data-stu-id="d4a17-209">If hello read-write latencies reported by hello diagnostics tool are high:</span></span>

    1. <span data-ttu-id="d4a17-210">Configurer le stockage Analytique pour les services blob et analysez les hello sortie toounderstand hello latences pour hello compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a17-210">Configure Storage Analytics for blob services and analyze hello output toounderstand hello latencies for hello Azure storage account.</span></span> <span data-ttu-id="d4a17-211">Pour obtenir des instructions détaillées, consultez trop[activer et configurer le stockage Analytique](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d4a17-211">For detailed instructions, go too[enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="d4a17-212">Si ces temps de latence sont également numéros élevée et comparables toohello que vous avez reçu de hello outil de diagnostic de StorSimple, vous devez toolog une demande de service avec le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a17-212">If those latencies are also high and comparable toohello numbers you received from hello StorSimple Diagnostics tool, then you need toolog a service request with Azure storage.</span></span>

    2. <span data-ttu-id="d4a17-213">Si les latences de compte de stockage hello sont insuffisantes, contactez votre tooinvestigate d’administrateur réseau aucun temps d’attente de problèmes dans votre réseau.</span><span class="sxs-lookup"><span data-stu-id="d4a17-213">If hello storage account latencies are low, contact your network administrator tooinvestigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="d4a17-214">Exemple de sortie du test des performances sur un appareil 8100</span><span class="sxs-lookup"><span data-stu-id="d4a17-214">Sample output of performance test run on an 8100 device</span></span>

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

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="d4a17-215">Annexe : Interprétation des informations système</span><span class="sxs-lookup"><span data-stu-id="d4a17-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="d4a17-216">Voici un tableau décrivant le hello différents paramètres de Windows PowerShell dans les informations de système de hello mappent à.</span><span class="sxs-lookup"><span data-stu-id="d4a17-216">Here is a table describing what hello various Windows PowerShell parameters in hello system information map to.</span></span> 

| <span data-ttu-id="d4a17-217">Paramètre PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4a17-217">PowerShell Parameter</span></span>    | <span data-ttu-id="d4a17-218">Description</span><span class="sxs-lookup"><span data-stu-id="d4a17-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="d4a17-219">ID de l’instance</span><span class="sxs-lookup"><span data-stu-id="d4a17-219">Instance ID</span></span>             | <span data-ttu-id="d4a17-220">Un identificateur unique ou un GUID est associé à chaque contrôleur.</span><span class="sxs-lookup"><span data-stu-id="d4a17-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="d4a17-221">Nom</span><span class="sxs-lookup"><span data-stu-id="d4a17-221">Name</span></span>                    | <span data-ttu-id="d4a17-222">nom convivial de Hello du périphérique hello configuré via hello portail Azure pendant le déploiement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="d4a17-222">hello friendly name of hello device as configured through hello Azure portal during device deployment.</span></span> <span data-ttu-id="d4a17-223">nom convivial de Hello par défaut est le numéro de série du périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-223">hello default friendly name is hello device serial number.</span></span> |
| <span data-ttu-id="d4a17-224">Modèle</span><span class="sxs-lookup"><span data-stu-id="d4a17-224">Model</span></span>                   | <span data-ttu-id="d4a17-225">modèle Hello de votre appareil de série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="d4a17-225">hello model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="d4a17-226">modèle de Hello peut être 8100 ou 8600.</span><span class="sxs-lookup"><span data-stu-id="d4a17-226">hello model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="d4a17-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="d4a17-227">SerialNumber</span></span>            | <span data-ttu-id="d4a17-228">numéro de série du périphérique Hello est attribué à la fabrique de hello et 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="d4a17-228">hello device serial number is assigned at hello factory and is 15 characters long.</span></span> <span data-ttu-id="d4a17-229">Par exemple, 8600-SHX0991003G44HT indique :</span><span class="sxs-lookup"><span data-stu-id="d4a17-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="d4a17-230">8600 – est le modèle d’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-230">8600 – Is hello device model.</span></span><br><span data-ttu-id="d4a17-231">SHX – hello fabrication site.</span><span class="sxs-lookup"><span data-stu-id="d4a17-231">SHX – Is hello manufacturing site.</span></span><br> <span data-ttu-id="d4a17-232">0991003 : produit spécifique.</span><span class="sxs-lookup"><span data-stu-id="d4a17-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="d4a17-233">G44HT-hello 5 derniers chiffres sont incrémentés toocreate les numéros de série uniques.</span><span class="sxs-lookup"><span data-stu-id="d4a17-233">G44HT- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="d4a17-234">Il ne s’agit pas nécessairement d’une suite.</span><span class="sxs-lookup"><span data-stu-id="d4a17-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="d4a17-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="d4a17-235">TimeZone</span></span>                | <span data-ttu-id="d4a17-236">Hello fuseau horaire configuré Bonjour Azure portal durant le déploiement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="d4a17-236">hello device time zone as configured in hello Azure portal during device deployment.</span></span>|
| <span data-ttu-id="d4a17-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="d4a17-237">CurrentController</span></span>       | <span data-ttu-id="d4a17-238">contrôleur Hello que vous êtes connecté toothrough interface de Windows PowerShell hello de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4a17-238">hello controller that you are connected toothrough hello Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="d4a17-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="d4a17-239">ActiveController</span></span>        | <span data-ttu-id="d4a17-240">contrôleur Hello qui est active sur votre appareil et contrôle toutes les opérations de réseau et disque hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-240">hello controller that is active on your device and is controlling all hello network and disk operations.</span></span> <span data-ttu-id="d4a17-241">Il peut s’agir du contrôleur 0 ou du contrôleur 1.</span><span class="sxs-lookup"><span data-stu-id="d4a17-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="d4a17-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="d4a17-242">Controller0Status</span></span>       | <span data-ttu-id="d4a17-243">état de Hello du contrôleur 0 sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d4a17-243">hello status of Controller 0 on your device.</span></span> <span data-ttu-id="d4a17-244">état du contrôleur Hello peut être normal, en mode de récupération ou inaccessible.</span><span class="sxs-lookup"><span data-stu-id="d4a17-244">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="d4a17-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="d4a17-245">Controller1Status</span></span>       | <span data-ttu-id="d4a17-246">état de Hello du contrôleur 1 sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d4a17-246">hello status of Controller 1 on your device.</span></span>  <span data-ttu-id="d4a17-247">état du contrôleur Hello peut être normal, en mode de récupération ou inaccessible.</span><span class="sxs-lookup"><span data-stu-id="d4a17-247">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="d4a17-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="d4a17-248">SystemMode</span></span>              | <span data-ttu-id="d4a17-249">Bonjour à l’état global de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4a17-249">hello overall status of your StorSimple device.</span></span> <span data-ttu-id="d4a17-250">état du périphérique Hello peut être normal, maintenance, ou mis hors service (correspond toodeactivated Bonjour portail Azure).</span><span class="sxs-lookup"><span data-stu-id="d4a17-250">hello device status can be normal, maintenance, or decommissioned (corresponds toodeactivated in hello Azure portal).</span></span>|
| <span data-ttu-id="d4a17-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="d4a17-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="d4a17-252">chaîne conviviale Hello correspondant toohello version du logiciel.</span><span class="sxs-lookup"><span data-stu-id="d4a17-252">hello friendly string that corresponds toohello device software version.</span></span> <span data-ttu-id="d4a17-253">Pour un système exécutant la mise à jour 4, version du logiciel convivial hello serait StorSimple 8000 Series Update 4.0.</span><span class="sxs-lookup"><span data-stu-id="d4a17-253">For a system running Update 4, hello friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="d4a17-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="d4a17-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="d4a17-255">version du logiciel HCS Hello en cours d’exécution sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d4a17-255">hello HCS software version running on your device.</span></span> <span data-ttu-id="d4a17-256">Par exemple, hello tooStorSimple correspondante de la version logicielle HCS 8000 Series Update 4.0 est 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="d4a17-256">For instance, hello HCS software version corresponding tooStorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="d4a17-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="d4a17-257">ApiVersion</span></span>              | <span data-ttu-id="d4a17-258">version du logiciel Hello Hello API PowerShell de Windows du périphérique HCS de hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-258">hello software version of hello Windows PowerShell API of hello HCS device.</span></span>|
| <span data-ttu-id="d4a17-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="d4a17-259">VhdVersion</span></span>              | <span data-ttu-id="d4a17-260">version du logiciel Hello d’image de fabrique hello hello périphérique a été livré avec.</span><span class="sxs-lookup"><span data-stu-id="d4a17-260">hello software version of hello factory image that hello device was shipped with.</span></span> <span data-ttu-id="d4a17-261">Si vous réinitialisez votre toofactory de périphérique par défaut, puis il exécute cette version du logiciel.</span><span class="sxs-lookup"><span data-stu-id="d4a17-261">If you reset your device toofactory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="d4a17-262">OSVersion:</span><span class="sxs-lookup"><span data-stu-id="d4a17-262">OSVersion</span></span>               | <span data-ttu-id="d4a17-263">version du logiciel Hello de hello système d’exploitation Windows en cours d’exécution sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-263">hello software version of hello Windows Server operating system running on hello device.</span></span> <span data-ttu-id="d4a17-264">hello Windows Server 2012 R2 correspondant too6.3.9600 est basée sur l’appareil StorSimple Hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-264">hello StorSimple device is based off hello Windows Server 2012 R2 that corresponds too6.3.9600.</span></span>|
| <span data-ttu-id="d4a17-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="d4a17-265">CisAgentVersion</span></span>         | <span data-ttu-id="d4a17-266">version Hello pour votre agent d’éléments de configuration en cours d’exécution sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4a17-266">hello version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="d4a17-267">Cet agent permet de communiquer avec le service StorSimple Manager hello s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a17-267">This agent helps communicate with hello StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="d4a17-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="d4a17-268">MdsAgentVersion</span></span>         | <span data-ttu-id="d4a17-269">Hello version toohello Mds agent correspondant en cours d’exécution sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4a17-269">hello version corresponding toohello Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="d4a17-270">Cet agent déplace les données toohello analyse et Diagnostics de Service (MDS).</span><span class="sxs-lookup"><span data-stu-id="d4a17-270">This agent moves data toohello Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="d4a17-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="d4a17-271">Lsisas2Version</span></span>          | <span data-ttu-id="d4a17-272">Bonjour version des pilotes toohello LSI correspondants sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4a17-272">hello version corresponding toohello LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="d4a17-273">Capacity</span><span class="sxs-lookup"><span data-stu-id="d4a17-273">Capacity</span></span>                | <span data-ttu-id="d4a17-274">capacité totale de Hello du périphérique hello en octets.</span><span class="sxs-lookup"><span data-stu-id="d4a17-274">hello total capacity of hello device in bytes.</span></span>|
| <span data-ttu-id="d4a17-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="d4a17-275">RemoteManagementMode</span></span>    | <span data-ttu-id="d4a17-276">Indique si les appareils hello peuvent être gérés à distance via son interface Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4a17-276">Indicates whether hello device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="d4a17-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="d4a17-277">FipsMode</span></span>                | <span data-ttu-id="d4a17-278">Indique si le mode hello United States traitement Standard FIPS (Federal Information) est activé sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d4a17-278">Indicates whether hello United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="d4a17-279">norme de Hello FIPS 140 définit les algorithmes de chiffrement approuvés pour une utilisation par les systèmes d’ordinateur gouvernement fédéral nous pour une protection des données sensibles hello.</span><span class="sxs-lookup"><span data-stu-id="d4a17-279">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span> <span data-ttu-id="d4a17-280">Pour les appareils exécutant Update 4 ou version ultérieure, le mode FIPS est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="d4a17-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d4a17-281">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4a17-281">Next steps</span></span>

* <span data-ttu-id="d4a17-282">En savoir plus hello [syntaxe de l’applet de commande Invoke-HcsDiagnostics de hello](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4a17-282">Learn hello [syntax of hello Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="d4a17-283">En savoir plus sur la façon trop[résoudre les problèmes de déploiement](storsimple-troubleshoot-deployment.md) sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d4a17-283">Learn more about how too[troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
