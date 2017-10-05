---
title: "Planifier la capacité et la mise à l’échelle de la réplication des machines virtuelles Hyper-V (sans VMM) vers Azure avec Azure Site Recovery | Microsoft Docs"
description: "Utilisez cet article pour planifier la capacité et la mise à l’échelle lors de la réplication des machines virtuelles Hyper-V vers Azure avec Azure Site Recovery"
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
ms.openlocfilehash: c7891c188c2cecbbf056fa79672a13bb16fa7fcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-to-azure-replication"></a><span data-ttu-id="235c7-103">Étape 3 : Planifier la capacité et la mise à l’échelle pour la réplication d’Hyper-V vers Azure</span><span class="sxs-lookup"><span data-stu-id="235c7-103">Step 3: Plan capacity and scaling for Hyper-V to Azure replication</span></span>

<span data-ttu-id="235c7-104">Utilisez cet article pour déterminer la planification de la capacité et de la mise à l’échelle pendant la réplication de machines virtuelles Hyper-V locales (sans System Center VMM) vers Azure avec [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="235c7-104">Use this article to figure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs (without System Center VMM) to Azure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="235c7-105">Après avoir lu cet article, envoyez vos commentaires en bas ou posez vos questions techniques sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="235c7-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="235c7-106">Comment dois-je commencer la planification de la capacité ?</span><span class="sxs-lookup"><span data-stu-id="235c7-106">How do I start capacity planning?</span></span>


<span data-ttu-id="235c7-107">Collectez des informations sur l’environnement de réplication, puis planifiez la capacité en tenant compte de ces informations et de celles présentes dans l’article.</span><span class="sxs-lookup"><span data-stu-id="235c7-107">You gather information about your replication environment, and then plan capacity using this information, together with the considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="235c7-108">Collecter des informations</span><span class="sxs-lookup"><span data-stu-id="235c7-108">Gather information</span></span>

1. <span data-ttu-id="235c7-109">collecter les informations relatives à votre environnement de réplication, notamment les machines virtuelles, le nombre de disques par machine virtuelle et le stockage par disque ;</span><span class="sxs-lookup"><span data-stu-id="235c7-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="235c7-110">Déterminer le taux de modification (l’évolution) quotidienne des données répliquées.</span><span class="sxs-lookup"><span data-stu-id="235c7-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="235c7-111">Téléchargez l’[outil de planification de la capacité Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) pour obtenir le taux de modifications.</span><span class="sxs-lookup"><span data-stu-id="235c7-111">Download the [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) to get the change rate.</span></span> <span data-ttu-id="235c7-112">Nous vous recommandons d’exécuter cet outil sur une semaine pour enregistrer les moyennes.</span><span class="sxs-lookup"><span data-stu-id="235c7-112">We recommend you run this tool over a week to capture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="235c7-113">Déterminer la capacité</span><span class="sxs-lookup"><span data-stu-id="235c7-113">Figure out capacity</span></span>

<span data-ttu-id="235c7-114">En fonction des informations que vous avez collectées, exécutez l’outil [Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) pour analyser votre environnement source et vos charges de travail, déterminer vos besoins en bande passante et en ressources serveur à l’emplacement source, ainsi que les ressources (machines virtuelles et stockage, etc.) dont vous avez besoin à l’emplacement cible.</span><span class="sxs-lookup"><span data-stu-id="235c7-114">Based on the information you've gather, you run the [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) to analyze your source environment and workloads, estimate bandwidth needs and server resources for the source location, and the resources (virtual machines and storage etc), that you need in the target location.</span></span> <span data-ttu-id="235c7-115">Vous pouvez exécuter l’outil de deux manières :</span><span class="sxs-lookup"><span data-stu-id="235c7-115">You can run the tool in a couple of modes:</span></span>

- <span data-ttu-id="235c7-116">Planification rapide : exécutez l’outil dans ce mode pour obtenir des projections réseau et serveur sur la base de la quantité moyenne de machines virtuelles, de disques et de stockage, et sur le taux de modifications moyen.</span><span class="sxs-lookup"><span data-stu-id="235c7-116">Quick planning: Run the tool in this mode to get network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="235c7-117">Planification détaillée : exécutez l’outil dans ce mode et fournissez les détails de chaque charge de travail au niveau de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="235c7-117">Detailed planning: Run the tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="235c7-118">Analysez la compatibilité de machine virtuelle et obtenez des projections réseau et serveur.</span><span class="sxs-lookup"><span data-stu-id="235c7-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="235c7-119">Exécuter l’outil :</span><span class="sxs-lookup"><span data-stu-id="235c7-119">Now run the tool:</span></span>

1. <span data-ttu-id="235c7-120">Téléchargez l’[outil](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="235c7-120">Download the [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="235c7-121">Pour exécuter la planification rapide, suivez [ces instructions](site-recovery-capacity-planner.md#run-the-quick-planner) et sélectionnez le scénario **Hyper-V vers Azure**.</span><span class="sxs-lookup"><span data-stu-id="235c7-121">To run the quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select the scenario **Hyper-V to Azure**.</span></span>
3. <span data-ttu-id="235c7-122">Pour exécuter la planification détaillée, suivez [ces instructions](site-recovery-capacity-planner.md#run-the-detailed-planner) et sélectionnez le scénario **Hyper-V vers Azure**.</span><span class="sxs-lookup"><span data-stu-id="235c7-122">To run the detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select the scenario **Hyper-V to Azure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="235c7-123">Contrôler la bande passante réseau</span><span class="sxs-lookup"><span data-stu-id="235c7-123">Control network bandwidth</span></span>

<span data-ttu-id="235c7-124">Une fois que vous avez calculé la bande passante dont vous avez besoin, vous avez deux options pour contrôler la quantité de bande passante utilisée pour la réplication :</span><span class="sxs-lookup"><span data-stu-id="235c7-124">After you've calculated the bandwidth you need, you have a couple of options for controlling the amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="235c7-125">**Limite de bande passante**: le trafic Hyper-V qui est répliqué vers Azure passe par un hôte Hyper-V spécifique.</span><span class="sxs-lookup"><span data-stu-id="235c7-125">**Throttle bandwidth**: Hyper-V traffic that replicates to Azure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="235c7-126">Vous pouvez limiter la bande passante sur le serveur hôte.</span><span class="sxs-lookup"><span data-stu-id="235c7-126">You can throttle bandwidth on the host server.</span></span>
* <span data-ttu-id="235c7-127">**Influer sur la bande passante** : vous pouvez influer sur la bande passante utilisée pour la réplication à l’aide de quelques clés de Registre.</span><span class="sxs-lookup"><span data-stu-id="235c7-127">**Influence bandwidth**: You can influence the bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="235c7-128">Limiter la bande passante</span><span class="sxs-lookup"><span data-stu-id="235c7-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="235c7-129">Ouvrez le composant logiciel enfichable MMC de Microsoft Azure Backup sur le serveur hôte Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="235c7-129">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host server.</span></span> <span data-ttu-id="235c7-130">Par défaut, un raccourci vers Microsoft Azure Backup est créé sur le Bureau. Vous pouvez également le trouver ici : C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="235c7-130">By default a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="235c7-131">Dans le composant logiciel enfichable, cliquez sur **Modifier les propriétés**.</span><span class="sxs-lookup"><span data-stu-id="235c7-131">In the snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="235c7-132">Dans l’onglet **Limitation**, sélectionnez **Activer la limitation de la bande passante sur Internet pour les opérations de sauvegarde** et définissez les limites relatives aux heures de travail et aux heures non travaillées.</span><span class="sxs-lookup"><span data-stu-id="235c7-132">On the **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set the limits for work and non-work hours.</span></span> <span data-ttu-id="235c7-133">Les plages valides vont de 512 Kbits/s à 102 Mbits/s par seconde.</span><span class="sxs-lookup"><span data-stu-id="235c7-133">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![Limiter la bande passante](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

<span data-ttu-id="235c7-135">Vous pouvez également utiliser l’applet de commande [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) pour définir la limitation.</span><span class="sxs-lookup"><span data-stu-id="235c7-135">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="235c7-136">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="235c7-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="235c7-137">**Set-OBMachineSetting -NoThrottle** indique qu’aucune limitation n’est requise.</span><span class="sxs-lookup"><span data-stu-id="235c7-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="235c7-138">Influer sur la bande passante réseau</span><span class="sxs-lookup"><span data-stu-id="235c7-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="235c7-139">Dans le registre, accédez à **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="235c7-139">In the registry navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="235c7-140">Pour influer sur le trafic de la bande passante sur un disque de réplication, modifiez la valeur du paramètre **UploadThreadsPerVM**, ou créez la clé si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="235c7-140">To influence the bandwidth traffic on a replicating disk, modify the value the **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="235c7-141">Pour influer sur la bande passante utilisée pour le trafic lié à la restauration automatique à partir d’Azure, modifiez la valeur du paramètre **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="235c7-141">To influence the bandwidth for failback traffic from Azure, modify the value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="235c7-142">La valeur par défaut est 4.</span><span class="sxs-lookup"><span data-stu-id="235c7-142">The default value is 4.</span></span> <span data-ttu-id="235c7-143">Dans un réseau « surutilisé », ces clés de Registre doivent être modifiées par rapport aux valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="235c7-143">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="235c7-144">La valeur maximale est de 32.</span><span class="sxs-lookup"><span data-stu-id="235c7-144">The maximum is 32.</span></span> <span data-ttu-id="235c7-145">Surveillez le trafic pour optimiser la valeur.</span><span class="sxs-lookup"><span data-stu-id="235c7-145">Monitor traffic to optimize the value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="235c7-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="235c7-146">Next steps</span></span>

<span data-ttu-id="235c7-147">Aller à l’[Étape 4 : Planifier la mise en réseau](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="235c7-147">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
