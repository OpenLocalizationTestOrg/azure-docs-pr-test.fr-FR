---
title: "aaaUpgrade un coffre de Services de récupération Azure Site Recovery coffre tooan"
description: "Découvrez comment tooupgrade un coffre Azure Site Recovery Services de récupération tooa coffre"
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="9898d-103">Mise à niveau d’un coffre de Services de récupération basée sur le Gestionnaire de ressources Azure Site Recovery coffre tooan</span><span class="sxs-lookup"><span data-stu-id="9898d-103">Upgrade a Site Recovery vault tooan Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="9898d-104">Cet article décrit comment les coffres de coffres de Service de récupération basée sur le Gestionnaire de ressources tooAzure sans aucun impact sur la réplication en cours tooupgrade Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9898d-104">This article describes how tooupgrade Azure Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="9898d-105">Pour plus d’informations sur les fonctionnalités et les avantages d’Azure Resource Manager, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9898d-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="9898d-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="9898d-106">Introduction</span></span>
<span data-ttu-id="9898d-107">Un coffre Recovery Services est une ressource Azure Resource Manager pour la gestion de sauvegarde et récupération d’urgence en mode natif dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in hello cloud.</span></span> <span data-ttu-id="9898d-108">Il est un coffre unifié que vous pouvez utiliser dans le nouveau portail Azure hello et il remplace les sauvegarde classique hello et les coffres de récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="9898d-108">It is a unified vault that you can use in hello new Azure portal, and it replaces hello classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="9898d-109">Les coffres Recovery Services offrent tout un ensemble de fonctionnalités, notamment :</span><span class="sxs-lookup"><span data-stu-id="9898d-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="9898d-110">Prise en charge d’Azure Resource Manager : vous pouvez protéger et basculer vos machines virtuelles et ordinateurs physiques dans une pile Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9898d-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="9898d-111">Exclure le disque : Si vous avez des fichiers temporaires ou des données d’évolution élevé que vous ne souhaitez pas toouse votre bande passante pour, vous pouvez exclure des volumes de réplication.</span><span class="sxs-lookup"><span data-stu-id="9898d-111">Exclude disk: If you have temp files or high churn data that you don’t want toouse all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="9898d-112">Cette fonctionnalité a été activée actuellement en *VMware tooAzure* et *Hyper-V tooAzure* et est étendues scénarios tooother également.</span><span class="sxs-lookup"><span data-stu-id="9898d-112">This capability has been enabled currently in *VMware tooAzure* and *Hyper-V tooAzure* and is extended tooother scenarios as well.</span></span>

* <span data-ttu-id="9898d-113">Prise en charge pour le stockage localement redondant et premium : vous pouvez désormais protéger des serveurs dans un stockage premium comptes qui permettent aux clients tooprotect des applications avec une version ultérieure d’entrée/sortient d’opérations par seconde (IOPS).</span><span class="sxs-lookup"><span data-stu-id="9898d-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers tooprotect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="9898d-114">Cette fonctionnalité est actuellement activée dans *VMware tooAzure*.</span><span class="sxs-lookup"><span data-stu-id="9898d-114">This capability is currently enabled in *VMware tooAzure*.</span></span>

* <span data-ttu-id="9898d-115">Rationalisé expérience de mise en route : expérience de mise en route de hello améliorée a été conçu configuration de la récupération d’urgence toomake facile.</span><span class="sxs-lookup"><span data-stu-id="9898d-115">Streamlined getting-started experience: hello enhanced getting-started experience has been designed toomake disaster-recovery setup easy.</span></span>

* <span data-ttu-id="9898d-116">Sauvegarde et gestion de récupération de Site à partir de hello même coffre : vous pouvez désormais protéger les serveurs de récupération d’urgence ou effectuer la sauvegarde à partir de hello même coffre, ce qui peut réduire votre charge considérablement.</span><span class="sxs-lookup"><span data-stu-id="9898d-116">Backup and Site Recovery management from hello same vault: You can now protect servers for disaster recovery or perform backup from hello same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="9898d-117">Pour plus d’informations sur l’expérience de hello mis à niveau et de fonctionnalités, consultez hello [blog de stockage, la sauvegarde et récupération](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span><span class="sxs-lookup"><span data-stu-id="9898d-117">For more information about hello upgraded experience and features, see hello [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="9898d-118">Principales fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="9898d-118">Salient features</span></span>

* <span data-ttu-id="9898d-119">Aucun impact sur la réplication en cours : les réplications en cours se poursuivent sans interruption pendant et après la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="9898d-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="9898d-120">Aucun coût supplémentaire : à disposition, un ensemble complet de fonctionnalités mises à jour sans coût supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="9898d-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="9898d-121">Aucune perte de données : étant donné que ce processus est une mise à niveau et pas une migration, les paramètres et les points de récupération de réplication existants restent intacts pendant et après la mise à niveau hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after hello upgrade.</span></span>


## <a name="what-happens-during-hello-vault-upgrade"></a><span data-ttu-id="9898d-122">Que se passe-t-il au cours de la mise à niveau du coffre hello ?</span><span class="sxs-lookup"><span data-stu-id="9898d-122">What happens during hello vault upgrade?</span></span>

<span data-ttu-id="9898d-123">Au cours de la mise à niveau de hello, Impossible d’effectuer les opérations telles que l’inscription d’un nouveau serveur ou l’activation de la réplication pour un ordinateur virtuel (VM).</span><span class="sxs-lookup"><span data-stu-id="9898d-123">During hello upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="9898d-124">Les opérations qui impliquent la lecture des données à partir d’ou de l’écriture de données toohello coffre, telles que la réplication en cours de l’archivage de toohello les éléments protégés, continuent sans interruption.</span><span class="sxs-lookup"><span data-stu-id="9898d-124">Operations that involve reading data from or writing data toohello vault, such as ongoing replication of protected items toohello vault, continue uninterrupted.</span></span>

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a><span data-ttu-id="9898d-125">Modifications tooautomation et outils après la mise à niveau hello</span><span class="sxs-lookup"><span data-stu-id="9898d-125">Changes tooautomation and tooling after hello upgrade</span></span>
<span data-ttu-id="9898d-126">Comme le type d’archivage hello mise à niveau à partir du modèle de déploiement du modèle toohello Gestionnaire de ressources hello déploiement classique, mettre à jour automation existante de hello ou tooensure outils qu’il remplisse toujours toowork après mise à niveau hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-126">As you upgrade hello vault type from hello classic deployment model toohello Resource Manager deployment model, update hello existing automation or tooling tooensure that it continues toowork after hello upgrade.</span></span>

### <a name="prepare-your-environment-for-hello-upgrade"></a><span data-ttu-id="9898d-127">Préparer votre environnement pour la mise à niveau hello</span><span class="sxs-lookup"><span data-stu-id="9898d-127">Prepare your environment for hello upgrade</span></span>

* [<span data-ttu-id="9898d-128">Installer PowerShell ou de mettre à niveau tooversion 5 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="9898d-128">Install PowerShell or upgrade it tooversion 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="9898d-129">Installer la version la plus récente d’Azure PowerShell MSI hello</span><span class="sxs-lookup"><span data-stu-id="9898d-129">Install hello latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="9898d-130">Télécharger le script mis à niveau du coffre Recovery Services hello</span><span class="sxs-lookup"><span data-stu-id="9898d-130">Download hello Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="9898d-131">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9898d-131">Prerequisites</span></span>
<span data-ttu-id="9898d-132">tooAzure basée sur le Gestionnaire de ressources de Service de récupération coffres les coffres de tooupgrade à partir de la récupération de Site, vous devez disposer des hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="9898d-132">tooupgrade from Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults, you must meet hello following requirements:</span></span>

* <span data-ttu-id="9898d-133">Version minimale de l’agent : hello la version du fournisseur Azure Site Recovery installé sur votre serveur doit être 5.1.1700.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9898d-133">Minimum agent version: hello version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="9898d-134">Configuration prise en charge : vous ne pouvez pas configurer votre coffre avec le réseau de zone de stockage (SAN) ou des groupes de disponibilité AlwaysOn SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9898d-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="9898d-135">Toutes les autres configurations sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="9898d-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="9898d-136">Après la mise à niveau de hello, vous pouvez gérer le mappage de stockage uniquement via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9898d-136">After hello upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="9898d-137">Scénario de déploiement pris en charge : votre coffre ne doivent pas être hello *VMware tooAzure* modèle de déploiement hérité.</span><span class="sxs-lookup"><span data-stu-id="9898d-137">Supported deployment scenario: Your vault shouldn’t be hello *VMware tooAzure* legacy deployment model.</span></span> <span data-ttu-id="9898d-138">Avant de continuer, commencez par déplacer modèle améliorée du déploiement de toohello.</span><span class="sxs-lookup"><span data-stu-id="9898d-138">Before you proceed, first move toohello enhanced deployment model.</span></span>

* <span data-ttu-id="9898d-139">Aucune tâche active initiée par l’utilisateur qui impliquent management ne plan operations :, car le plan de gestion des accès toohello est limitée au cours de la mise à niveau, effectuez toutes les actions votre plan de gestion avant de déclencher la mise à niveau de hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-139">No active user-initiated jobs that involve management plane operations: Because access toohello management plane is restricted during upgrade, complete all your management plane actions before you trigger hello upgrade.</span></span> <span data-ttu-id="9898d-140">Ce processus n’inclut pas la réplication en cours.</span><span class="sxs-lookup"><span data-stu-id="9898d-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="9898d-141">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="9898d-141">Frequently asked questions</span></span>

<span data-ttu-id="9898d-142">**Cette mise à niveau affecte-t-elle la réplication en cours ?**</span><span class="sxs-lookup"><span data-stu-id="9898d-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="9898d-143">Non.</span><span class="sxs-lookup"><span data-stu-id="9898d-143">No.</span></span> <span data-ttu-id="9898d-144">La réplication en cours se poursuit sans interruption pendant et après la mise à niveau hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-144">Your ongoing replication continues uninterrupted during and after hello upgrade.</span></span>

<span data-ttu-id="9898d-145">**Que passe-t-il toonetwork des paramètres tels que les paramètres IP et VPN de site à site ?**</span><span class="sxs-lookup"><span data-stu-id="9898d-145">**What happens toonetwork settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="9898d-146">mise à niveau Hello n’affecte pas les paramètres de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-146">hello upgrade doesn't affect hello network settings.</span></span> <span data-ttu-id="9898d-147">Toutes les connexions depuis Azure vers un emplacement local demeurent intactes.</span><span class="sxs-lookup"><span data-stu-id="9898d-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="9898d-148">**Que passe-t-il toomy coffres si vous ne prévoyez pas tooupgrade Bonjour futur proche ?**</span><span class="sxs-lookup"><span data-stu-id="9898d-148">**What happens toomy vaults if I don’t plan tooupgrade in hello near future?**</span></span>

<span data-ttu-id="9898d-149">Prise en charge pour le coffre Site Recovery dans l’ancien portail de Azure hello sera déconseillée à partir de septembre 2017.</span><span class="sxs-lookup"><span data-stu-id="9898d-149">Support for Site Recovery vault in hello old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="9898d-150">Nous vous recommandons vivement que vous utilisez des hello mise à niveau de fonctionnalité toomove toohello nouveau portail.</span><span class="sxs-lookup"><span data-stu-id="9898d-150">We strongly recommend that you use hello upgrade feature toomove toohello new portal.</span></span>

<span data-ttu-id="9898d-151">**Quelles sont les implications de ce plan de migration pour mes outils existants ?**</span><span class="sxs-lookup"><span data-stu-id="9898d-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="9898d-152">Mise à jour de votre modèle de déploiement du Gestionnaire de ressources de toohello outils est une des modifications les plus importantes hello que vous devez prendre en compte pour dans vos plans de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="9898d-152">Updating your tooling toohello Resource Manager deployment model is one of hello most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="9898d-153">archivages de Recovery Services Hello sont basés sur le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-153">hello Recovery Services vaults are based on hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="9898d-154">**La durée pendant laquelle dernière hello temps mort du plan de gestion ?**</span><span class="sxs-lookup"><span data-stu-id="9898d-154">**How long does hello management-plane downtime last?**</span></span>

<span data-ttu-id="9898d-155">mise à niveau Hello prend généralement environ 15 minutes de too30, et il peut s’écouler jusqu'à tooa maximale d’une heure.</span><span class="sxs-lookup"><span data-stu-id="9898d-155">hello upgrade ordinarily takes about 15 too30 minutes, and it could take up tooa maximum of one hour.</span></span>

<span data-ttu-id="9898d-156">**Puis-je restaurer après la mise à niveau ?**</span><span class="sxs-lookup"><span data-stu-id="9898d-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="9898d-157">Non.</span><span class="sxs-lookup"><span data-stu-id="9898d-157">No.</span></span> <span data-ttu-id="9898d-158">La restauration n’est pas prise en charge une fois que les ressources hello ont été mis à niveau avec succès.</span><span class="sxs-lookup"><span data-stu-id="9898d-158">Rollback is not supported after hello resources have been successfully upgraded.</span></span>

<span data-ttu-id="9898d-159">**Puis-je valider des mon abonnement ou les ressources toosee si elles peuvent être mis à niveau ?**</span><span class="sxs-lookup"><span data-stu-id="9898d-159">**Can I validate my subscription or resources toosee whether they can be upgraded?**</span></span>

<span data-ttu-id="9898d-160">Oui.</span><span class="sxs-lookup"><span data-stu-id="9898d-160">Yes.</span></span> <span data-ttu-id="9898d-161">Dans hello plateforme prise en charge option mise à niveau, hello première étape de mise à niveau hello est toovalidate que les ressources hello compatibles avec une mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="9898d-161">In hello platform-supported upgrade option, hello first step in hello upgrade is toovalidate that hello resources are capable of an upgrade.</span></span> <span data-ttu-id="9898d-162">Si hello validation échoue, vous recevez des messages d’erreur appropriés ou des avertissements.</span><span class="sxs-lookup"><span data-stu-id="9898d-162">If hello validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="9898d-163">**Comment signaler un problème avec la mise à niveau hello ?**</span><span class="sxs-lookup"><span data-stu-id="9898d-163">**How do I report an issue with hello upgrade?**</span></span>

<span data-ttu-id="9898d-164">Si vous rencontrez les échecs au cours de la mise à niveau hello, notez les ID d’opération hello est répertorié dans l’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-164">If you experience any failures during hello upgrade, note hello operation ID that's listed in hello error.</span></span> <span data-ttu-id="9898d-165">Support technique de Microsoft proactive fonctionne sur la résolution de problème de hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-165">Microsoft Support will proactively work on resolving hello issue.</span></span> <span data-ttu-id="9898d-166">Vous pouvez également contacter l’équipe de Support hello avec votre ID d’abonnement, le nom de l’archivage et l’ID d’opération.</span><span class="sxs-lookup"><span data-stu-id="9898d-166">You can also contact hello Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="9898d-167">Prise en charge fonctionnera problème de hello tooresolve aussi rapidement que possible.</span><span class="sxs-lookup"><span data-stu-id="9898d-167">Support will work tooresolve hello issue as quickly as possible.</span></span> <span data-ttu-id="9898d-168">Ne pas réessayer les opération hello sauf si vous êtes toodo explicitement demandé c’est le cas par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9898d-168">Do not retry hello operation unless you are explicitly instructed toodo so by Microsoft.</span></span>

## <a name="run-hello-script"></a><span data-ttu-id="9898d-169">Exécutez le script de hello</span><span class="sxs-lookup"><span data-stu-id="9898d-169">Run hello script</span></span>

<span data-ttu-id="9898d-170">Dans PowerShell, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9898d-170">In PowerShell, run hello following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="9898d-171">SubscriptionID : ID d’abonnement hello qui est associé à l’archivage hello que vous mettez à niveau.</span><span class="sxs-lookup"><span data-stu-id="9898d-171">SubscriptionID: hello subscription ID that's associated with hello vault that you're upgrading.</span></span>

* <span data-ttu-id="9898d-172">Nom du coffre : nom de hello de coffre hello que vous mettez à niveau.</span><span class="sxs-lookup"><span data-stu-id="9898d-172">VaultName: hello name of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="9898d-173">Emplacement : emplacement de hello de coffre hello que vous mettez à niveau.</span><span class="sxs-lookup"><span data-stu-id="9898d-173">Location: hello location of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="9898d-174">ResourceType : HyperVRecoveryManagerVault pour les coffres Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9898d-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="9898d-175">TargetResourceGroupName : mise à niveau de groupe de ressources hello dans lequel vous souhaitez hello toobe coffre placé.</span><span class="sxs-lookup"><span data-stu-id="9898d-175">TargetResourceGroupName: hello resource group into which you want hello upgraded vault toobe placed.</span></span> <span data-ttu-id="9898d-176">TargetResourceGroupName peut être un groupe de ressources existant dans Azure Resource Manager ou un nouveau groupe.</span><span class="sxs-lookup"><span data-stu-id="9898d-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="9898d-177">Si hello TargetResourceGroupName fourni n’existe pas, il est créé dans le cadre de la mise à niveau hello Bonjour même emplacement que le coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-177">If hello TargetResourceGroupName that's supplied does not exist, it is created as part of hello upgrade in hello same location as hello vault.</span></span> <span data-ttu-id="9898d-178">Pour plus d’informations, voir section « Groupes de ressources » hello [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="9898d-178">For more information, see hello "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="9898d-179">Nom de groupe de ressources est contraintes toocertain de sujet.</span><span class="sxs-lookup"><span data-stu-id="9898d-179">Resource group naming is subject toocertain constraints.</span></span> <span data-ttu-id="9898d-180">tooprevent coffre mise à niveau de défaillance, être vraiment tooobserve hello convention d’affectation de noms avec soin.</span><span class="sxs-lookup"><span data-stu-id="9898d-180">tooprevent vault upgrade failure, be sure tooobserve hello naming convention carefully.</span></span>
    >
    ><span data-ttu-id="9898d-181">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9898d-181">For example:</span></span>
    >
    ><span data-ttu-id="9898d-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="9898d-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="9898d-183">Vous pouvez également exécuter hello script suivant.</span><span class="sxs-lookup"><span data-stu-id="9898d-183">Alternatively, you can run hello following script.</span></span> <span data-ttu-id="9898d-184">Entrez les valeurs de hello pour les paramètres hello requis.</span><span class="sxs-lookup"><span data-stu-id="9898d-184">Enter hello values for hello required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="9898d-185">Hello script PowerShell vous invite à entrer vous tooenter vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="9898d-185">hello PowerShell script prompts you tooenter your credentials.</span></span> <span data-ttu-id="9898d-186">Entrez-les à deux reprises, une fois pour le compte de modèle de déploiement classique de hello et une fois pour hello compte de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9898d-186">Enter them twice, once for hello classic deployment model account and once for hello Azure Resource Manager account.</span></span>

2. <span data-ttu-id="9898d-187">Une fois que vous avez entré vos informations d’identification, script de hello exécute un toodetermine à cocher si votre hello répond à du programme d’installation infrastructure mentionné précédemment configuration requise.</span><span class="sxs-lookup"><span data-stu-id="9898d-187">After you've entered your credentials, hello script runs a check toodetermine whether your infrastructure setup meets hello previously mentioned requirements.</span></span>

3. <span data-ttu-id="9898d-188">Une fois les conditions préalables de hello ont été vérifiés et confirmés, vous êtes tooproceed demandée avec mise à niveau du coffre hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-188">After hello prerequisites have been checked and confirmed, you are prompted tooproceed with hello vault upgrade.</span></span> <span data-ttu-id="9898d-189">processus de mise à niveau Hello démarre la mise à niveau votre archivage.</span><span class="sxs-lookup"><span data-stu-id="9898d-189">hello upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="9898d-190">mise à niveau entière de Hello peut prendre 15 toocomplete de minutes too30.</span><span class="sxs-lookup"><span data-stu-id="9898d-190">hello entire upgrade can take 15 too30 minutes toocomplete.</span></span>

4. <span data-ttu-id="9898d-191">Une fois la mise à niveau hello est terminée avec succès, vous pouvez accéder à hello de coffre mis à niveau dans le nouveau portail de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-191">After hello upgrade has been completed successfully, you can access hello upgraded vault in hello new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="9898d-192">Gestion du coffre après la mise à niveau</span><span class="sxs-lookup"><span data-stu-id="9898d-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a><span data-ttu-id="9898d-193">Répliquer à l’aide d’Azure Site Recovery Bonjour de coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="9898d-193">Replicate by using Azure Site Recovery in hello Recovery Services vault</span></span>

* <span data-ttu-id="9898d-194">Vous pouvez désormais protéger vos machines virtuelles Azure à partir d’une région tooanother.</span><span class="sxs-lookup"><span data-stu-id="9898d-194">You can now protect your Azure VMs from one region tooanother.</span></span> <span data-ttu-id="9898d-195">Pour plus d’informations, consultez [Répliquer des machines virtuelles Azure entre des régions avec Azure Site Recovery](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="9898d-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="9898d-196">Pour plus d’informations sur la réplication des ordinateurs virtuels VMware tooAzure, consultez [tooAzure de répliquer des machines virtuelles VMware avec Site Recovery](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9898d-196">For more information about replicating VMware VMs tooAzure, see [Replicate VMware VMs tooAzure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="9898d-197">Pour plus d’informations sur la réplication des ordinateurs virtuels Hyper-V (sans VMM) tooAzure, consultez [Hyper-V répliquer les machines virtuelles (sans VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9898d-197">For more information about replicating Hyper-V VMs (without VMM) tooAzure, see [Replicate Hyper-V virtual machines (without VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="9898d-198">Pour plus d’informations sur la réplication des ordinateurs virtuels Hyper-V (avec VMM) tooAzure, consultez [machines virtuelles de réplication Hyper-V dans VMM tooAzure de nuages à l’aide de la récupération de Site dans hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9898d-198">For more information about replicating Hyper-V VMs (with VMM) tooAzure, see [Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="9898d-199">Pour plus d’informations sur la réplication de site secondaire de tooa Hyper-VMs (avec VMM), consultez [machines virtuelles de réplication Hyper-V dans VMM clouds tooa secondaire VMM site à l’aide de hello Azure portal](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="9898d-199">For more information about replicating Hyper-VMs (with VMM) tooa secondary site, see [Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using hello Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="9898d-200">Pour plus d’informations sur la réplication de site secondaire de tooa les ordinateurs virtuels VMware, consultez [Replicate locaux des ordinateurs virtuels VMware ou serveurs physiques tooa secondaire dans le portail Azure classic de hello](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="9898d-200">For more information about replicating VMware VMs tooa secondary site, see [Replicate on-premises VMware virtual machines or physical servers tooa secondary site in hello classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="9898d-201">Afficher vos éléments répliqués</span><span class="sxs-lookup"><span data-stu-id="9898d-201">View your replicated items</span></span>

<span data-ttu-id="9898d-202">Hello image suivante montre hello Recovery Services page coffre du tableau de bord qui affiche les entités clés pour le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="9898d-202">hello following image shows hello Recovery Services vault dashboard page that displays key entities for hello vault.</span></span> <span data-ttu-id="9898d-203">tooview une liste des entités protégées dans le coffre de hello, sélectionnez **Site Recovery** > **éléments répliqués**.</span><span class="sxs-lookup"><span data-stu-id="9898d-203">tooview a list of protected entities in hello vault, select **Site Recovery** > **Replicated items**.</span></span>


![Éléments répliqués](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="9898d-205">Hello image suivante présente hello de flux de travail pour afficher les éléments répliqués hello **basculement** commande pour initialiser un basculement.</span><span class="sxs-lookup"><span data-stu-id="9898d-205">hello following image shows hello workflow for viewing your replicated items and hello **Failover** command for initiating a failover.</span></span>

![Éléments répliqués](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="9898d-207">Afficher vos paramètres de réplication</span><span class="sxs-lookup"><span data-stu-id="9898d-207">View your replication settings</span></span>

<span data-ttu-id="9898d-208">Dans le coffre Site Recovery hello, chaque groupe de protection est configuré avec une fréquence de copie, délai de rétention de point de récupération, fréquence des instantanés cohérents d’application et autres paramètres de réplication.</span><span class="sxs-lookup"><span data-stu-id="9898d-208">In hello Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="9898d-209">Dans le coffre Recovery Services hello, ces paramètres sont configurés en tant qu’une stratégie de réplication.</span><span class="sxs-lookup"><span data-stu-id="9898d-209">In hello Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="9898d-210">nom Hello de stratégie de hello est nom hello du groupe de protection hello ou hello *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="9898d-210">hello name of hello policy is hello name of hello protection group or hello *primarycloud_Policy*.</span></span>

<span data-ttu-id="9898d-211">Pour plus d’informations sur la stratégie de réplication, consultez [gérer la stratégie de réplication pour VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="9898d-211">For more information about replication policy, see [Manage replication policy for VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span></span>
