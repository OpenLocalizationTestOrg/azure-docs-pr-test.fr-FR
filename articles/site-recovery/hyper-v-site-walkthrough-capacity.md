---
title: "aaaPlan la capacité et de mise à l’échelle pour tooAzure de réplication (sans VMM) d’un ordinateur virtuel Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Utilisez cette capacité tooplan de l’article et la mise à l’échelle lors de la réplication tooAzure d’ordinateurs virtuels Hyper-V avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f5b029f273e51c01c7d918d176832f6d1735b5f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-tooazure-replication"></a><span data-ttu-id="8b6a3-103">Étape 3 : Planifier la capacité et la mise à l’échelle pour la réplication Hyper-V tooAzure</span><span class="sxs-lookup"><span data-stu-id="8b6a3-103">Step 3: Plan capacity and scaling for Hyper-V tooAzure replication</span></span>

<span data-ttu-id="8b6a3-104">Utilisez cette toofigure article planification de la capacité et la mise à l’échelle lors de la réplication tooAzure de machines virtuelles de Hyper-V (sans System Center VMM) localement avec [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8b6a3-104">Use this article toofigure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs (without System Center VMM) tooAzure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="8b6a3-105">Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8b6a3-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="8b6a3-106">Comment dois-je commencer la planification de la capacité ?</span><span class="sxs-lookup"><span data-stu-id="8b6a3-106">How do I start capacity planning?</span></span>


<span data-ttu-id="8b6a3-107">Votre recueillir des informations sur votre environnement de réplication, puis planifier la capacité à l’aide de ces informations, ainsi que des considérations hello mis en surbrillance dans cet article.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-107">You gather information about your replication environment, and then plan capacity using this information, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="8b6a3-108">Collecter des informations</span><span class="sxs-lookup"><span data-stu-id="8b6a3-108">Gather information</span></span>

1. <span data-ttu-id="8b6a3-109">collecter les informations relatives à votre environnement de réplication, notamment les machines virtuelles, le nombre de disques par machine virtuelle et le stockage par disque ;</span><span class="sxs-lookup"><span data-stu-id="8b6a3-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="8b6a3-110">Déterminer le taux de modification (l’évolution) quotidienne des données répliquées.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="8b6a3-111">Télécharger hello [outil de planification des capacités de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) taux de modification tooget hello.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-111">Download hello [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello change rate.</span></span> <span data-ttu-id="8b6a3-112">Nous vous recommandons de qu'exécuter cet outil sur un toocapture semaine moyennes.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-112">We recommend you run this tool over a week toocapture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="8b6a3-113">Déterminer la capacité</span><span class="sxs-lookup"><span data-stu-id="8b6a3-113">Figure out capacity</span></span>

<span data-ttu-id="8b6a3-114">Selon que vous avez collecte d’informations hello, vous exécutez hello [Site Recovery outil Capacity Planner](http://aka.ms/asr-capacity-planner-excel) tooanalyze votre environnement source et les charges de travail, estimer les besoins en bande passante et ressources du serveur pour l’emplacement de source de hello et hello ressources (machines virtuelles et stockage, etc.) dont vous avez besoin dans l’emplacement cible de hello.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-114">Based on hello information you've gather, you run hello [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) tooanalyze your source environment and workloads, estimate bandwidth needs and server resources for hello source location, and hello resources (virtual machines and storage etc), that you need in hello target location.</span></span> <span data-ttu-id="8b6a3-115">Vous pouvez exécuter l’outil de hello dans deux modes :</span><span class="sxs-lookup"><span data-stu-id="8b6a3-115">You can run hello tool in a couple of modes:</span></span>

- <span data-ttu-id="8b6a3-116">Planification rapide : exécuter les outil hello dans ce mode tooget réseau et serveur les projections basées sur un nombre moyen de machines virtuelles, de disques, de stockage et de taux de modification.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-116">Quick planning: Run hello tool in this mode tooget network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="8b6a3-117">Planification détaillée : exécutez l’outil de hello dans ce mode et fournissent des détails de chaque charge de travail au niveau de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-117">Detailed planning: Run hello tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="8b6a3-118">Analysez la compatibilité de machine virtuelle et obtenez des projections réseau et serveur.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="8b6a3-119">Maintenant, exécutez les outil hello :</span><span class="sxs-lookup"><span data-stu-id="8b6a3-119">Now run hello tool:</span></span>

1. <span data-ttu-id="8b6a3-120">Télécharger hello [outil](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="8b6a3-120">Download hello [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="8b6a3-121">module rapide de toorun hello, procédez comme [ces instructions](site-recovery-capacity-planner.md#run-the-quick-planner)et sélectionnez hello scénario **Hyper-V tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-121">toorun hello quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>
3. <span data-ttu-id="8b6a3-122">toorun hello de planification détaillée, suivez [ces instructions](site-recovery-capacity-planner.md#run-the-detailed-planner)et sélectionnez hello scénario **Hyper-V tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-122">toorun hello detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="8b6a3-123">Contrôler la bande passante réseau</span><span class="sxs-lookup"><span data-stu-id="8b6a3-123">Control network bandwidth</span></span>

<span data-ttu-id="8b6a3-124">Une fois que vous êtes la bande passante calculée hello que vous avez besoin, vous avez deux options pour la quantité de hello contrôle de bande passante utilisée pour la réplication :</span><span class="sxs-lookup"><span data-stu-id="8b6a3-124">After you've calculated hello bandwidth you need, you have a couple of options for controlling hello amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="8b6a3-125">**Limiter la bande passante**: le trafic de Hyper-V qui réplique tooAzure passe par un hôte Hyper-V spécifique.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-125">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="8b6a3-126">Vous pouvez limiter la bande passante sur le serveur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-126">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="8b6a3-127">**Influencer la bande passante**: vous pouvez influer sur la bande passante hello utilisée pour la réplication à l’aide de deux clés de Registre.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-127">**Influence bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="8b6a3-128">Limiter la bande passante</span><span class="sxs-lookup"><span data-stu-id="8b6a3-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="8b6a3-129">Ouvrez le composant logiciel enfichable MMC Microsoft Azure Backup hello sur le serveur hôte de Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-129">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="8b6a3-130">Par défaut, un raccourci pour Microsoft Azure Backup est disponible sur le bureau de hello ou dans C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-130">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="8b6a3-131">Dans le composant logiciel enfichable hello, cliquez sur **modifier les propriétés**.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-131">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="8b6a3-132">Sur hello **limitation** onglet sélectionnez **activer l’utilisation de la bande passante internet pour les opérations de sauvegarde de limitation**et définir des limites de hello pour le travail et non liés au travail heures.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-132">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="8b6a3-133">Les plages valides sont de Mbits/s des too102 de 512 Kbits/s par seconde.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-133">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![Limiter la bande passante](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

<span data-ttu-id="8b6a3-135">Vous pouvez également utiliser hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) de limitation tooset applet de commande.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-135">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="8b6a3-136">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="8b6a3-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="8b6a3-137">**Set-OBMachineSetting -NoThrottle** indique qu’aucune limitation n’est requise.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="8b6a3-138">Influer sur la bande passante réseau</span><span class="sxs-lookup"><span data-stu-id="8b6a3-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="8b6a3-139">Dans le Registre de hello accédez trop**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-139">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="8b6a3-140">le trafic de la bande passante de hello tooinfluence sur un disque de réplication, modifiez hello de valeur hello **UploadThreadsPerVM**, ou créez la clé de hello si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-140">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="8b6a3-141">la bande passante de hello tooinfluence pour le trafic de la restauration automatique d’Azure, modifier la valeur de hello **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-141">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="8b6a3-142">Hello par défaut est 4.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-142">hello default value is 4.</span></span> <span data-ttu-id="8b6a3-143">Dans un réseau « surapprovisionnée », ces clés de Registre doivent être modifiées à partir des valeurs par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-143">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="8b6a3-144">Hello maximal est 32.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-144">hello maximum is 32.</span></span> <span data-ttu-id="8b6a3-145">Surveiller le trafic toooptimize hello valeur.</span><span class="sxs-lookup"><span data-stu-id="8b6a3-145">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b6a3-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8b6a3-146">Next steps</span></span>

<span data-ttu-id="8b6a3-147">Accédez trop[étape 4 : planifier la mise en réseau](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="8b6a3-147">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
