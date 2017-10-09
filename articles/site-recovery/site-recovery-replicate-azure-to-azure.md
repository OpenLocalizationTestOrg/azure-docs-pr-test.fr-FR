---
title: les applications aaaReplicate (tooAzure Azure) | Documents Microsoft
description: "Cet article décrit comment tooset la réplication de virtual machines en cours d’exécution dans une région Azure trop d’une autre région dans Azure."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a><span data-ttu-id="d7761-103">Répliquer les machines virtuelles tooanother région Azure</span><span class="sxs-lookup"><span data-stu-id="d7761-103">Replicate Azure virtual machines tooanother Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="d7761-104">La réplication Site Recovery pour les machines virtuelles Azure est actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="d7761-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="d7761-105">Cet article décrit comment tooset la réplication de virtual machines en cours d’exécution dans une région Azure tooanother région Azure.</span><span class="sxs-lookup"><span data-stu-id="d7761-105">This article describes how tooset up replication of virtual machines running in one Azure region tooanother Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7761-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d7761-106">Prerequisites</span></span>

* <span data-ttu-id="d7761-107">article de Hello part du principe que vous connaissez déjà sur la récupération de Site et de coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="d7761-107">hello article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="d7761-108">Vous devez toohave une pre 'Coffre Recovery services' créé.</span><span class="sxs-lookup"><span data-stu-id="d7761-108">You need toohave a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="d7761-109">Il est recommandé que vous créez hello 'Coffre Recovery services' dans hello emplacement où votre tooreplicate de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d7761-109">It is recommended that you create hello 'Recovery services vault' in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="d7761-110">Par exemple, si votre emplacement cible est la région « États-Unis du Centre », créez le coffre dans « États-Unis du Centre ».</span><span class="sxs-lookup"><span data-stu-id="d7761-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="d7761-111">Si vous utilisez des règles de groupes de sécurité réseau (NSG) ou de la connectivité internet de pare-feu proxy toocontrol accès toooutbound sur hello machines virtuelles Azure, vérifiez que hello liste blanche vous requis URL ou les adresses IP.</span><span class="sxs-lookup"><span data-stu-id="d7761-111">If you are using Network Security Groups (NSG) rules or firewall proxy toocontrol access toooutbound internet connectivity on hello Azure VMs, ensure that you whitelist hello required URLs or IPs.</span></span> <span data-ttu-id="d7761-112">Consultez trop[document du Guide de mise en réseau](./site-recovery-azure-to-azure-networking-guidance.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d7761-112">Refer too[Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="d7761-113">Si vous avez un ExpressRoute ou une connexion VPN entre locaux et hello source d’emplacement dans Azure, suivez [considérations de récupération de Site pour local tooon Azure ExpressRoute / configuration VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span><span class="sxs-lookup"><span data-stu-id="d7761-113">If you have an ExpressRoute or a VPN connection between on-premises and hello source location in Azure, follow [Site Recovery Considerations for Azure tooon-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="d7761-114">Votre compte d’utilisateur Azure doit toohave certaines [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="d7761-114">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="d7761-115">Votre abonnement Azure doit être activé toocreate VM dans l’emplacement cible de hello souhaité toouse comme région de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="d7761-115">Your Azure subscription should be enabled toocreate VMs in hello target location you want toouse as DR region.</span></span> <span data-ttu-id="d7761-116">Vous pouvez contacter le support tooenable hello requis quota.</span><span class="sxs-lookup"><span data-stu-id="d7761-116">You can contact support tooenable hello required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="d7761-117">Activer la réplication à partir du coffre Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="d7761-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="d7761-118">Dans cette illustration, nous va répliquer les machines virtuelles en cours d’exécution dans hello 'Asie orientale' emplacement Azure toohello ' Asie du Sud-est ' emplacement.</span><span class="sxs-lookup"><span data-stu-id="d7761-118">For this illustration, we will replicate VMs running  in hello ‘East Asia’ Azure location toohello ‘South East Asia’ location.</span></span> <span data-ttu-id="d7761-119">étapes de Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7761-119">hello steps are as follows:</span></span>

 <span data-ttu-id="d7761-120">Cliquez sur **+ répliquer** dans la réplication de tooenable coffre hello pour les ordinateurs virtuels de hello.</span><span class="sxs-lookup"><span data-stu-id="d7761-120">Click **+Replicate** in hello vault tooenable replication for hello virtual machines.</span></span>

1. <span data-ttu-id="d7761-121">**Source :** il fait référence à toohello point d’origine de machines de hello qui dans ce cas est **Azure**.</span><span class="sxs-lookup"><span data-stu-id="d7761-121">**Source:** It refers toohello point of origin of hello machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="d7761-122">**Emplacement source :** il est hello région Azure où vous souhaitez tooprotect vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d7761-122">**Source location:** It is hello Azure region from where you want tooprotect your virtual machines.</span></span> <span data-ttu-id="d7761-123">Dans cette illustration, emplacement de source de hello sera « East Asia »</span><span class="sxs-lookup"><span data-stu-id="d7761-123">For this illustration, hello source location will be 'East Asia'</span></span>

3. <span data-ttu-id="d7761-124">**Modèle de déploiement :** il fait référence le modèle de déploiement Azure toohello de machines de sources hello.</span><span class="sxs-lookup"><span data-stu-id="d7761-124">**Deployment model:** It refers toohello Azure deployment model of hello source machines.</span></span> <span data-ttu-id="d7761-125">Vous pouvez sélectionner soit classique ou le Gestionnaire de ressources et les machines appartenant toohello particuliers du modèle sont répertoriés pour la protection à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d7761-125">You can select either classic or resource manager and machines belonging toohello specific model will be listed for protection in hello next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="d7761-126">Vous pouvez uniquement répliquer une machine virtuelle classique et la récupérer en tant que machine virtuelle classique.</span><span class="sxs-lookup"><span data-stu-id="d7761-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="d7761-127">Vous ne pouvez pas la récupérer en tant que machine virtuelle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7761-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="d7761-128">**Groupe de ressources :** de toowhich de groupe de ressources hello vos machines virtuelles source appartient.</span><span class="sxs-lookup"><span data-stu-id="d7761-128">**Resource Group:** It’s hello resource group toowhich your source virtual machines belong.</span></span> <span data-ttu-id="d7761-129">Hello tous les ordinateurs virtuels sous le groupe de ressources sélectionné hello apparaît pour la protection à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d7761-129">All hello VMs under hello selected resource group will be listed for protection in hello next step.</span></span>

    ![Activer la réplication](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="d7761-131">Dans **virtuels > Sélectionner les machines virtuelles**, cliquez sur et sélectionnez chaque ordinateur que vous souhaitez tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="d7761-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="d7761-132">Vous pouvez uniquement sélectionner les machines pour lesquelles la réplication peut être activée.</span><span class="sxs-lookup"><span data-stu-id="d7761-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="d7761-133">Puis cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="d7761-133">Then click OK.</span></span>
    <span data-ttu-id="d7761-134">![Activer la réplication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="d7761-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="d7761-135">Dans la section Paramètres, vous pouvez configurer les propriétés du site cible.</span><span class="sxs-lookup"><span data-stu-id="d7761-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="d7761-136">**Emplacement cible :** emplacement hello où vos données d’ordinateur virtuel source seront répliquées.</span><span class="sxs-lookup"><span data-stu-id="d7761-136">**Target Location:**  This is hello location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="d7761-137">En fonction de votre emplacement d’ordinateurs sélectionnés, Site Recovery fournira que Hello de la liste des régions de la cible appropriée.</span><span class="sxs-lookup"><span data-stu-id="d7761-137">Depending upon your selected machines location, Site Recovery will provide you hello list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="d7761-138">Il est recommandé d’emplacement cible de tookeep même à compter de la récupération du coffre de services.</span><span class="sxs-lookup"><span data-stu-id="d7761-138">It is recommended tookeep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="d7761-139">**Groupe de ressources cible :** il est toowhich de groupe de ressources hello toutes vos machines virtuelles répliquées appartiendra. Par défaut ASR créera un nouveau groupe de ressources dans la région de hello cible avec le nom de suffixe de « asr ».</span><span class="sxs-lookup"><span data-stu-id="d7761-139">**Target resource group :** It is hello resource group toowhich all your replicated virtual machines will belong.By default ASR will create a new resource group in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="d7761-140">En cas de groupe de ressources créé par la fonctionnalité déjà existe, elle est réutilisée. Vous pouvez également choisir toocustomize comme indiqué dans la section hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d7761-140">In case resource group created by ASR already exist, it will be reused.You can also choose toocustomize it as shown in hello section below.</span></span>    
3. <span data-ttu-id="d7761-141">**Réseau virtuel de cible :** par défaut, la fonctionnalité créera un nouveau réseau virtuel dans la région de hello cible avec le nom de suffixe de « asr ».</span><span class="sxs-lookup"><span data-stu-id="d7761-141">**Target Virtual Network:** By default, ASR will create a new virtual network in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="d7761-142">Cela sera mappé tooyour source réseau et sera utilisé pour toute protection futures.</span><span class="sxs-lookup"><span data-stu-id="d7761-142">This will be mapped tooyour source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d7761-143">[Consultez les détails de mise en réseau](site-recovery-network-mapping-azure-to-azure.md) tooknow plus sur le mappage réseau.</span><span class="sxs-lookup"><span data-stu-id="d7761-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) tooknow more about network mapping.</span></span>

4. <span data-ttu-id="d7761-144">**Cibler des comptes de stockage :** par défaut, la fonctionnalité créera hello nouveau compte de stockage cible avec votre configuration de stockage d’ordinateur virtuel source.</span><span class="sxs-lookup"><span data-stu-id="d7761-144">**Target Storage accounts:** By default, ASR will create hello new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="d7761-145">Dans le cas où le compte de stockage créé par ASR existe déjà, il est réutilisé.</span><span class="sxs-lookup"><span data-stu-id="d7761-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="d7761-146">**Comptes de stockage de cache :** ASR a besoin de compte de stockage supplémentaire appelée stockage du cache dans la région de la source hello.</span><span class="sxs-lookup"><span data-stu-id="d7761-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in hello source region.</span></span> <span data-ttu-id="d7761-147">Tous les hello les modifications effectuées sur hello machines virtuelles source sont suivies et envoyés le compte de stockage toocache avant de répliquer ces emplacement cible de toohello.</span><span class="sxs-lookup"><span data-stu-id="d7761-147">All hello changes happening on hello source VMs are tracked and sent toocache storage account before replicating those toohello target location.</span></span>

6. <span data-ttu-id="d7761-148">**Haute disponibilité :** par défaut, la fonctionnalité créera un nouveau groupe à haute disponibilité dans la région de hello cible avec le nom de suffixe de « asr ».</span><span class="sxs-lookup"><span data-stu-id="d7761-148">**Availability set :** By default, ASR will create a new availability set in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="d7761-149">Dans le cas où le groupe à haute disponibilité créé par ASR existe déjà, il est réutilisé.</span><span class="sxs-lookup"><span data-stu-id="d7761-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="d7761-150">**La stratégie de réplication :** il définit des paramètres pour la récupération point rétention l’historique et application instantané cohérent fréquence hello.</span><span class="sxs-lookup"><span data-stu-id="d7761-150">**Replication Policy:** It defines hello settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="d7761-151">Par défaut, ASR crée une stratégie de réplication avec des paramètres par défaut de « 24 heures » pour la rétention des points de récupération et « 60 minutes » pour la fréquence des captures instantanées de cohérence des applications.</span><span class="sxs-lookup"><span data-stu-id="d7761-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Activer la réplication](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="d7761-153">Personnaliser les ressources cibles</span><span class="sxs-lookup"><span data-stu-id="d7761-153">Customize target resources</span></span>

<span data-ttu-id="d7761-154">Au cas où vous souhaiteriez toochange hello valeurs par défaut utilisées par la récupération automatique du système, vous pouvez modifier les paramètres de hello selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="d7761-154">In case you want toochange hello defaults used by ASR, you can change hello settings based on your needs.</span></span>

1. <span data-ttu-id="d7761-155">**Personnaliser :** dessus toochange hello par défaut utilisées par la récupération automatique du système.</span><span class="sxs-lookup"><span data-stu-id="d7761-155">**Customize:** Click it toochange hello defaults used by ASR.</span></span>

2. <span data-ttu-id="d7761-156">**Groupe de ressources cible :** vous pouvez sélectionner le groupe de ressources hello dans liste hello de tous les groupes de ressources hello existant dans l’emplacement cible de hello au sein de l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="d7761-156">**Target resource group :**  You can select hello resource group from hello list of all hello resource groups existing in hello target location within hello subscription.</span></span>

3. <span data-ttu-id="d7761-157">**Réseau virtuel de cible :** vous trouverez la liste hello de tous les réseaux hello dans l’emplacement cible de hello.</span><span class="sxs-lookup"><span data-stu-id="d7761-157">**Target Virtual Network:** You can find hello list of all hello virtual network in hello target location.</span></span>

4. <span data-ttu-id="d7761-158">**Haute disponibilité :** vous pouvez uniquement ajouter disponibilité jeux de paramètres toohello machines virtuelles qui font partie de la disponibilité dans la zone source.</span><span class="sxs-lookup"><span data-stu-id="d7761-158">**Availability set :** You can only add availability sets settings toohello virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="d7761-159">**Comptes de stockage cibles :**</span><span class="sxs-lookup"><span data-stu-id="d7761-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="d7761-160">![Activer la réplication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Cliquez sur **Créer la ressource cible** et Activer la réplication.</span><span class="sxs-lookup"><span data-stu-id="d7761-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="d7761-161">Une fois que les ordinateurs virtuels sont protégés, vous pouvez vérifier état hello d’intégrité des machines virtuelles sous **éléments répliqués**</span><span class="sxs-lookup"><span data-stu-id="d7761-161">Once virtual machines are protected you can check hello status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="d7761-162">Au cours de hello moment de la réplication initiale il pourrait possible qu’état prend toorefresh de temps et que vous ne voyez pas progression pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="d7761-162">During hello time of initial replication there could a possibility that status takes time toorefresh and you don't see progress for some time.</span></span> <span data-ttu-id="d7761-163">Vous pouvez cliquer le bouton d’actualisation hello haut hello d’état le plus récent hello panneau tooget hello.</span><span class="sxs-lookup"><span data-stu-id="d7761-163">You can click hello Refresh button on hello top of hello blade tooget hello latest status.</span></span>
>

![Activer la réplication](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="d7761-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7761-165">Next steps</span></span>
- <span data-ttu-id="d7761-166">[En savoir plus](site-recovery-test-failover-to-azure.md) sur l’exécution d’un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="d7761-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="d7761-167">[En savoir plus](site-recovery-failover.md) sur différents types de basculement et comment toorun les.</span><span class="sxs-lookup"><span data-stu-id="d7761-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="d7761-168">En savoir plus sur [à l’aide de plans de récupération](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="d7761-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
- <span data-ttu-id="d7761-169">En savoir plus sur la [reprotection des machines virtuelles Azure](site-recovery-how-to-reprotect.md) après le basculement.</span><span class="sxs-lookup"><span data-stu-id="d7761-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
