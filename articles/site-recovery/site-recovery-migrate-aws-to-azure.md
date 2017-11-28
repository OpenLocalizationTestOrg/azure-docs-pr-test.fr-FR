---
title: "aaaMigrate machines virtuelles à partir de AWS tooAzure | Documents Microsoft"
description: "Cet article décrit comment toomigrate virtual machines en cours d’exécution dans tooAzure Amazon Web Services (AWS) à l’aide d’Azure Site Recovery."
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
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a><span data-ttu-id="bc96e-103">Migrer des ordinateurs virtuels dans tooAzure Amazon Web Services (AWS) avec Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="bc96e-103">Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery</span></span>

<span data-ttu-id="bc96e-104">Cet article décrit le fonctionnement des instances toomigrate AWS Windows virtuels tooAzure avec hello [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="bc96e-104">This article describes how toomigrate AWS Windows instances tooAzure virtual machines with hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="bc96e-105">La migration est en réalité un basculement à partir de AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bc96e-105">Migration is effectively a failover from AWS tooAzure.</span></span> <span data-ttu-id="bc96e-106">Vous ne pouvez pas la restauration automatique machines tooAWS, et il n’est pas en cours de réplication.</span><span class="sxs-lookup"><span data-stu-id="bc96e-106">You can't failback machines tooAWS, and there's no ongoing replication.</span></span> <span data-ttu-id="bc96e-107">Cet article décrit les étapes de hello pour la migration dans hello portail Azure et sont basées sur les instructions hello pour [répliquer un ordinateur physique de tooAzure](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="bc96e-107">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for [replicating a physical machine tooAzure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="bc96e-108">Valider des commentaires ou des questions au bas de hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="bc96e-108">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="bc96e-109">Systèmes d’exploitation pris en charge</span><span class="sxs-lookup"><span data-stu-id="bc96e-109">Supported operating systems</span></span>

<span data-ttu-id="bc96e-110">Récupération de site peut être utilisé toomigrate EC2 les instances des hello suivant des systèmes d’exploitation en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="bc96e-110">Site Recovery can be used toomigrate EC2 instances running any of hello following operating systems:</span></span>

- <span data-ttu-id="bc96e-111">Windows (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="bc96e-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="bc96e-112">Windows Server 2008 R2 SP1+ (pilotes PV Citrix AWS uniquement.</span><span class="sxs-lookup"><span data-stu-id="bc96e-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="bc96e-113">**Les instances qui exécutent des pilotes PV RedHat ne sont pas pris en charge**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="bc96e-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="bc96e-114">Linux (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="bc96e-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="bc96e-115">Red Hat Enterprise Linux 6.7 (instances virtualisées HVM uniquement)</span><span class="sxs-lookup"><span data-stu-id="bc96e-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc96e-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bc96e-116">Prerequisites</span></span>

<span data-ttu-id="bc96e-117">Voici ce dont vous avez besoin pour ce déploiement :</span><span class="sxs-lookup"><span data-stu-id="bc96e-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="bc96e-118">**Serveur de configuration**: un Amazon EC2 exécution des machines virtuelles Windows Server 2012 R2 est déployé comme serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="bc96e-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as hello configuration server.</span></span> <span data-ttu-id="bc96e-119">Par défaut, hello autres composants Azure Site Recovery (serveur de processus et un serveur cible maître) sont installés lorsque vous déployez le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="bc96e-119">By default, hello other Azure Site Recovery components (process server and master target server) are installed when you deploy hello configuration server.</span></span> <span data-ttu-id="bc96e-120">Cet article décrit les étapes de hello pour la migration dans hello portail Azure et sont basées sur les instructions hello pour [en savoir plus](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="bc96e-120">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="bc96e-121">**Les instances EC2**: hello Amazon EC2 instances de machines virtuelles que vous souhaitez toomigrate.</span><span class="sxs-lookup"><span data-stu-id="bc96e-121">**EC2 instances**: hello Amazon EC2 virtual machines instances that you want toomigrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="bc96e-122">Étapes du déploiement</span><span class="sxs-lookup"><span data-stu-id="bc96e-122">Deployment steps</span></span>

1. <span data-ttu-id="bc96e-123">Créez un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="bc96e-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="bc96e-124">Hello groupe de sécurité de vos instances EC2 doit avoir des règles configurées tooallow communiquer instance EC2 de hello que vous voulez toomigrate et instance hello sur lequel vous comptez toodeploy hello serveur de Configuration.</span><span class="sxs-lookup"><span data-stu-id="bc96e-124">hello Security Group of your EC2 instances should have rules configured tooallow communication between hello EC2 instance that you want toomigrate, and hello instance on which you plan toodeploy hello Configuration Server.</span></span>

3. <span data-ttu-id="bc96e-125">Sur hello même Cloud privé virtuel Amazon en tant que vos instances EC2, déployez un serveur de configuration du système.</span><span class="sxs-lookup"><span data-stu-id="bc96e-125">On hello same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="bc96e-126">Consultez hello VMware / physiques tooAzure les conditions préalables requises pour les spécifications de déploiement de serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="bc96e-126">Refer hello VMware / Physical tooAzure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="bc96e-128">Une fois que votre serveur de configuration est déployée dans AWS et inscrit avec votre coffre Recovery Services, vous devez voir serveur de configuration hello et serveur de processus sous l’infrastructure de la récupération de Site comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="bc96e-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see hello configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="bc96e-130">Une fois que vous avez déployé le serveur de configuration hello (elle peut prendre too15 minustes pour qu’il tooappear), valider qu’il peut communiquer avec des machines virtuelles de hello que vous souhaitez toomigrate.</span><span class="sxs-lookup"><span data-stu-id="bc96e-130">After you've deployed hello configuration server (it might take up too15 minustes for it tooappear), validate that it can communicate with hello VMs that you want toomigrate.</span></span>

6. <span data-ttu-id="bc96e-131">[Configurer les paramètres de réplication](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="bc96e-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="bc96e-132">Activer la réplication : activer la réplication pour hello machines virtuelles que vous souhaitez toomigrate.</span><span class="sxs-lookup"><span data-stu-id="bc96e-132">Enable replication: Enable replication for hello VMs you want toomigrate.</span></span> <span data-ttu-id="bc96e-133">Vous pouvez détecter les instances de EC2 hello à l’aide d’adresses IP privées hello, que vous pouvez obtenir à partir de la console de EC2 hello.</span><span class="sxs-lookup"><span data-stu-id="bc96e-133">You can discover hello EC2 instances using hello private IP addresses, which you can get from hello EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="bc96e-135">Une fois que les instances de hello EC2 ont été protégés et hello réplication tooAzure est terminée, [exécuter un Test de basculement](site-recovery-test-failover-to-azure.md) toovalidate les performances de votre application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bc96e-135">Once hello EC2 instances have been protected and hello replication tooAzure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) toovalidate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="bc96e-137">Exécuter un basculement à partir de AWS tooAzure pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bc96e-137">Run a Failover from AWS tooAzure for each VM.</span></span> <span data-ttu-id="bc96e-138">Si vous le souhaitez, vous pouvez créer un plan de récupération et exécuter un basculement, toomigrate plusieurs ordinateurs virtuels à partir de AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bc96e-138">Optionally, you can create a recovery plan and run a Failover, toomigrate multiple virtual machines from AWS tooAzure.</span></span> <span data-ttu-id="bc96e-139">[Découvrez d’autres informations](site-recovery-create-recovery-plans.md) sur les plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="bc96e-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="bc96e-140">Pour la migration, vous n’avez pas besoin toocommit un basculement.</span><span class="sxs-lookup"><span data-stu-id="bc96e-140">For migration, you don't need toocommit a failover.</span></span> <span data-ttu-id="bc96e-141">Au lieu de cela, vous sélectionnez l’option d’effectuer la Migration de hello pour chaque ordinateur, vous souhaitez toomigrate.</span><span class="sxs-lookup"><span data-stu-id="bc96e-141">Instead, you select hello Complete Migration option for each machine you want toomigrate.</span></span> <span data-ttu-id="bc96e-142">Hello action d’effectuer la Migration se termine les processus de migration hello, supprime la réplication pour l’ordinateur de hello et arrête la récupération de Site de facturation pour l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="bc96e-142">hello Complete Migration action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

    ![Migrer](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="bc96e-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bc96e-144">Next steps</span></span>

- <span data-ttu-id="bc96e-145">[Préparer les ordinateurs migrés tooenable réplication](site-recovery-azure-to-azure-after-migration.md) région tooanother pour les besoins de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="bc96e-145">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="bc96e-146">Commencez à protéger vos charges de travail en [répliquant des machines virtuelles Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="bc96e-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
