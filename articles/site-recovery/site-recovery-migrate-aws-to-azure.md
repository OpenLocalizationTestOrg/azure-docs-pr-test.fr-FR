---
title: "Migrer des machines virtuelles d’AWS vers Azure | Microsoft Docs"
description: "Cet article décrit comment migrer des machines virtuelles exécutées dans Amazon Web Services (AWS) vers Azure à l’aide d’Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: b3c0727a279649f4f7dae30d41027129ce5b04ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-to-azure-with-azure-site-recovery"></a><span data-ttu-id="cbaea-103">Migrer des machines virtuelles Windows dans Amazon Web Services (AWS) vers Azure avec Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="cbaea-103">Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery</span></span>

<span data-ttu-id="cbaea-104">Cet article décrit la procédure de migration d’instances Windows AWS vers des machines virtuelles Azure avec le service [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cbaea-104">This article describes how to migrate AWS Windows instances to Azure virtual machines with the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="cbaea-105">La migration est en fait un basculement d’AWS vers Azure.</span><span class="sxs-lookup"><span data-stu-id="cbaea-105">Migration is effectively a failover from AWS to Azure.</span></span> <span data-ttu-id="cbaea-106">Vous ne pouvez pas restaurer automatiquement les machines et il n’y a pas de réplication continue.</span><span class="sxs-lookup"><span data-stu-id="cbaea-106">You can't failback machines to AWS, and there's no ongoing replication.</span></span> <span data-ttu-id="cbaea-107">Cet article décrit les étapes de migration dans le Portail Azure, qui se basent sur les instructions de [réplication d’une machine physique vers Azure](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cbaea-107">This article describes the steps for migration in the Azure portal, and are based on the instructions for [replicating a physical machine to Azure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="cbaea-108">Publiez des commentaires ou des questions au bas de cet article ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="cbaea-108">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="cbaea-109">Systèmes d’exploitation pris en charge</span><span class="sxs-lookup"><span data-stu-id="cbaea-109">Supported operating systems</span></span>

<span data-ttu-id="cbaea-110">Site Recovery permet de migrer des instances EC2 qui fonctionnent sous l’un des systèmes d’exploitation suivants :</span><span class="sxs-lookup"><span data-stu-id="cbaea-110">Site Recovery can be used to migrate EC2 instances running any of the following operating systems:</span></span>

- <span data-ttu-id="cbaea-111">Windows (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="cbaea-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="cbaea-112">Windows Server 2008 R2 SP1+ (pilotes PV Citrix AWS uniquement.</span><span class="sxs-lookup"><span data-stu-id="cbaea-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="cbaea-113">**Les instances qui exécutent des pilotes PV RedHat ne sont pas pris en charge**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cbaea-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="cbaea-114">Linux (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="cbaea-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="cbaea-115">Red Hat Enterprise Linux 6.7 (instances virtualisées HVM uniquement)</span><span class="sxs-lookup"><span data-stu-id="cbaea-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbaea-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cbaea-116">Prerequisites</span></span>

<span data-ttu-id="cbaea-117">Voici ce dont vous avez besoin pour ce déploiement :</span><span class="sxs-lookup"><span data-stu-id="cbaea-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="cbaea-118">**Serveur de configuration** : une machine virtuelle Amazon EC2 sous Windows Server 2012 R2 est déployée en tant que serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="cbaea-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as the configuration server.</span></span> <span data-ttu-id="cbaea-119">Par défaut, les autres composants Azure Site Recovery (serveur de traitement et serveur cible maître) sont installés pendant le déploiement du serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="cbaea-119">By default, the other Azure Site Recovery components (process server and master target server) are installed when you deploy the configuration server.</span></span> <span data-ttu-id="cbaea-120">Cet article décrit les étapes de migration dans le portail Azure. Celles-ci s’appuient sur les instructions de la section [En savoir plus](site-recovery-components.md).</span><span class="sxs-lookup"><span data-stu-id="cbaea-120">This article describes the steps for migration in the Azure portal, and are based on the instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="cbaea-121">**Instances EC2** : les instances de machines virtuelles Amazon EC2 que vous souhaitez migrer.</span><span class="sxs-lookup"><span data-stu-id="cbaea-121">**EC2 instances**: The Amazon EC2 virtual machines instances that you want to migrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="cbaea-122">Étapes du déploiement</span><span class="sxs-lookup"><span data-stu-id="cbaea-122">Deployment steps</span></span>

1. <span data-ttu-id="cbaea-123">Créez un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="cbaea-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="cbaea-124">Le groupe de sécurité de vos instances EC2 doit avoir des règles configurées pour permettre la communication entre l’instance EC2 que vous souhaitez migrer et l’instance sur laquelle vous envisagez de déployer le Serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="cbaea-124">The Security Group of your EC2 instances should have rules configured to allow communication between the EC2 instance that you want to migrate, and the instance on which you plan to deploy the Configuration Server.</span></span>

3. <span data-ttu-id="cbaea-125">Sur le même cloud privé virtuel Amazon que vos instances EC2, déployez un serveur de configuration ASR.</span><span class="sxs-lookup"><span data-stu-id="cbaea-125">On the same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="cbaea-126">Consultez les conditions préalables pour un déploiement de machines virtuelles VMware et de serveurs physiques sur Azure et ainsi connaître les composants nécessaires à la configuration d’un déploiement serveur.</span><span class="sxs-lookup"><span data-stu-id="cbaea-126">Refer the VMware / Physical to Azure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="cbaea-128">Une fois votre serveur de configuration déployé dans AWS et inscrit avec votre coffre Recovery Services, vous devriez voir le serveur de configuration et le serveur de traitement dans l’infrastructure Site Recovery comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="cbaea-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see the configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="cbaea-130">Après avoir déployé le serveur de configuration (son affichage peut prendre jusqu’à 15 minutes), vérifiez qu’il peut communiquer avec les machines virtuelles que vous souhaitez migrer.</span><span class="sxs-lookup"><span data-stu-id="cbaea-130">After you've deployed the configuration server (it might take up to 15 minustes for it to appear), validate that it can communicate with the VMs that you want to migrate.</span></span>

6. <span data-ttu-id="cbaea-131">[Configurer les paramètres de réplication](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="cbaea-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="cbaea-132">Activer la réplication : activez la réplication pour les machines virtuelles que vous souhaitez migrer.</span><span class="sxs-lookup"><span data-stu-id="cbaea-132">Enable replication: Enable replication for the VMs you want to migrate.</span></span> <span data-ttu-id="cbaea-133">Vous pouvez découvrir les instances EC2 à l’aide de l’adresse IP privée, que vous pouvez obtenir à partir de la console EC2.</span><span class="sxs-lookup"><span data-stu-id="cbaea-133">You can discover the EC2 instances using the private IP addresses, which you can get from the EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="cbaea-135">Une fois que les instances EC2 ont été protégées et que la réplication vers Azure est terminée, [exécutez un test de basculement](site-recovery-test-failover-to-azure.md) pour valider les performances de votre application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cbaea-135">Once the EC2 instances have been protected and the replication to Azure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) to validate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="cbaea-137">Effectuer un basculement de AWS vers Azure pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cbaea-137">Run a Failover from AWS to Azure for each VM.</span></span> <span data-ttu-id="cbaea-138">Si vous le souhaitez, vous pouvez créer un plan de récupération et exécuter un basculement pour migrer des machines virtuelles d’AWS vers Azure.</span><span class="sxs-lookup"><span data-stu-id="cbaea-138">Optionally, you can create a recovery plan and run a Failover, to migrate multiple virtual machines from AWS to Azure.</span></span> <span data-ttu-id="cbaea-139">[Découvrez d’autres informations](site-recovery-create-recovery-plans.md) sur les plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="cbaea-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="cbaea-140">Pour la migration, vous n’avez pas besoin de valider de basculement.</span><span class="sxs-lookup"><span data-stu-id="cbaea-140">For migration, you don't need to commit a failover.</span></span> <span data-ttu-id="cbaea-141">Au lieu de cela, sélectionnez l’option Terminer la migration pour chacune des machines que vous souhaitez migrer.</span><span class="sxs-lookup"><span data-stu-id="cbaea-141">Instead, you select the Complete Migration option for each machine you want to migrate.</span></span> <span data-ttu-id="cbaea-142">L’action Terminer la migration met un terme au processus de migration, supprime la réplication de la machine, puis arrête la facturation de Site Recovery pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="cbaea-142">The Complete Migration action finishes up the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

    ![Migrer](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="cbaea-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cbaea-144">Next steps</span></span>

- <span data-ttu-id="cbaea-145">[Replicate Azure VMs to another region after migration to Azure using Azure Site Recovery](site-recovery-azure-to-azure-after-migration.md) (Répliquer des machines virtuelles Azure vers une autre région après la migration vers Azure à l’aide d’Azure Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="cbaea-145">[Prepare migrated machines to enable replication](site-recovery-azure-to-azure-after-migration.md) to another region for disaster recovery needs.</span></span>
- <span data-ttu-id="cbaea-146">Commencez à protéger vos charges de travail en [répliquant des machines virtuelles Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="cbaea-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
