---
title: "machines virtuelles d’aaaMigrate tooResource Manager à l’aide de CLI d’Azure | Documents Microsoft"
description: "Cet article assiste hello plateforme prise en charge la migration de ressources à partir de tooAzure classique Gestionnaire de ressources à l’aide de CLI d’Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="f5ecf-103">Migrer les ressources IaaS de classique tooAzure Gestionnaire de ressources à l’aide de CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="f5ecf-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="f5ecf-104">Ces étapes vous montrent comment toouse Azure interface de ligne de commande (CLI) commandes toomigrate infrastructure en tant qu’une ressource de service (IaaS) à partir du modèle de déploiement du modèle toohello Azure Resource Manager hello déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-104">These steps show you how toouse Azure command-line interface (CLI) commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="f5ecf-105">article de Hello requiert hello [CLI d’Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f5ecf-105">hello article requires hello [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f5ecf-106">Toutes les opérations de hello décrites ici sont idempotent.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-106">All hello operations described here are idempotent.</span></span> <span data-ttu-id="f5ecf-107">Si vous avez un problème autre qu’une fonctionnalité non prise en charge ou une erreur de configuration, nous vous recommandons de relancer hello préparer, abandonner ou valider l’opération.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="f5ecf-108">plateforme de Hello essaiera alors action hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-108">hello platform will then try hello action again.</span></span>
> 
> 

<br>
<span data-ttu-id="f5ecf-109">Voici un ordre de hello tooidentify organigramme dans lequel les étapes doivent toobe exécutée pendant un processus de migration</span><span class="sxs-lookup"><span data-stu-id="f5ecf-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Capture d’écran qui illustre les étapes de migration hello](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="f5ecf-111">Étape 1 : préparation de la migration</span><span class="sxs-lookup"><span data-stu-id="f5ecf-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="f5ecf-112">Voici quelques meilleures pratiques que nous recommandons lors de l’évaluation de la migration des ressources IaaS de classique tooResource Manager :</span><span class="sxs-lookup"><span data-stu-id="f5ecf-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="f5ecf-113">Lisez hello [la liste des configurations non prises en charge et fonctionnalités](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f5ecf-113">Read through hello [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="f5ecf-114">Si vous avez des ordinateurs virtuels qui utilisent des configurations non prises en charge et fonctionnalités, nous vous recommandons d’attendre toobe de prise en charge de configuration de la fonction hello annoncé.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello feature/configuration support toobe announced.</span></span> <span data-ttu-id="f5ecf-115">Vous pouvez également supprimer cette fonctionnalité ou sortir de cette migration tooenable de configuration si elle répond à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-115">Alternatively, you can remove that feature or move out of that configuration tooenable migration if it suits your needs.</span></span>
* <span data-ttu-id="f5ecf-116">Si vous avez automatisé scripts aujourd'hui à déployer votre infrastructure et vos applications, essayez de toocreate une configuration de test similaire à l’aide de ces scripts pour la migration.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="f5ecf-117">Ou bien, vous pouvez définir des environnements d’exemple à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5ecf-118">Passerelles d’application ne sont pas actuellement pris en charge pour la migration de classique tooResource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="f5ecf-119">toomigrate un réseau virtuel classique avec une passerelle d’Application, supprimer la passerelle de hello avant l’exécution d’un réseau de Préparer opération toomove hello.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="f5ecf-120">Après avoir effectué la migration de hello, reconnectez le passerelle hello dans Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="f5ecf-121">Les passerelles ExpressRoute connexion circuits tooExpressRoute dans un autre abonnement ne peut pas être migrés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="f5ecf-122">Dans ce cas, supprimez la passerelle ExpressRoute de hello, migrer un réseau virtuel hello et recréez hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="f5ecf-123">Consultez [ExpressRoute de migrer des circuits et associé des réseaux virtuels à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](../../expressroute/expressroute-migration-classic-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a><span data-ttu-id="f5ecf-124">Étape 2 : Définir votre abonnement et inscrire le fournisseur de hello</span><span class="sxs-lookup"><span data-stu-id="f5ecf-124">Step 2: Set your subscription and register hello provider</span></span>
<span data-ttu-id="f5ecf-125">Pour les scénarios de migration, vous devez tooset de votre environnement pour les deux classique et Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-125">For migration scenarios, you need tooset up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="f5ecf-126">[Installez l’interface de ligne de commande Azure](../../cli-install-nodejs.md) et [sélectionnez votre abonnement](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f5ecf-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="f5ecf-127">Compte de connexion tooyour.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-127">Sign-in tooyour account.</span></span>

    azure login

<span data-ttu-id="f5ecf-128">Sélectionnez hello abonnement Azure à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-128">Select hello Azure subscription by using hello following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="f5ecf-129">L’inscription est défini une fois l’étape, mais il a besoin toobe fait qu’une seule fois avant de tenter la migration.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-129">Registration is a one time step but it needs toobe done once before attempting migration.</span></span> <span data-ttu-id="f5ecf-130">Sans inscription hello message d’erreur suivant s’affiche</span><span class="sxs-lookup"><span data-stu-id="f5ecf-130">Without registering you'll see hello following error message</span></span> 
> 
> <span data-ttu-id="f5ecf-131">*Requête invalide : l’abonnement n’est pas inscrit pour la migration.*</span><span class="sxs-lookup"><span data-stu-id="f5ecf-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="f5ecf-132">Enregistrer avec le fournisseur de ressources hello migration à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-132">Register with hello migration resource provider by using hello following command.</span></span> <span data-ttu-id="f5ecf-133">Notez que cette commande expire dans certains cas. Toutefois, l’inscription hello sera réussie.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-133">Note that in some cases, this command times out. However, hello registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="f5ecf-134">Attendez cinq minutes pour hello inscription toofinish.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-134">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="f5ecf-135">Vous pouvez vérifier l’état hello d’approbation de hello à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-135">You can check hello status of hello approval by using hello following command.</span></span> <span data-ttu-id="f5ecf-136">Assurez-vous que RegistrationState est `Registered` avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-136">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="f5ecf-137">Passez maintenant CLI toohello `asm` mode.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-137">Now switch CLI toohello `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="f5ecf-138">Étape 3 : Vérifiez que vous disposez assez de cœurs Machine virtuelle de Azure Resource Manager Bonjour région Azure de votre déploiement en cours ou de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f5ecf-138">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="f5ecf-139">Pour cette étape vous devez tooswitch trop`arm` mode.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-139">For this step you'll need tooswitch too`arm` mode.</span></span> <span data-ttu-id="f5ecf-140">Cela hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-140">Do this with hello following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="f5ecf-141">Vous pouvez utiliser hello suivant CLI commande toocheck hello quantité actuelle de cœurs que dans le Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-141">You can use hello following CLI command toocheck hello current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="f5ecf-142">toolearn en savoir plus sur les quotas de base, consultez [limites et hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="f5ecf-142">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="f5ecf-143">Une fois que vous avez terminé à la vérification de cette étape, vous pouvez revenir trop`asm` mode.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-143">Once you're done verifying this step, you can switch back too`asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="f5ecf-144">Étape 4 : Option 1 - Migration de machines virtuelles dans un service cloud</span><span class="sxs-lookup"><span data-stu-id="f5ecf-144">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="f5ecf-145">Obtenez la liste de services de cloud computing à l’aide de hello commande suivante, puis sur service de cloud hello choix que vous souhaitez toomigrate hello.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-145">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="f5ecf-146">Notez que si hello machines virtuelles dans le service cloud hello se trouvent dans un réseau virtuel, ou si elles ont des rôles web/de travail, vous obtenez un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-146">Note that if hello VMs in hello cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="f5ecf-147">Exécutez hello suivant le nom du déploiement commande tooget hello pour le service cloud hello à partir de la sortie des commentaires hello.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-147">Run hello following command tooget hello deployment name for hello cloud service from hello verbose output.</span></span> <span data-ttu-id="f5ecf-148">Dans la plupart des cas, le nom du déploiement hello est hello identique au nom du service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-148">In most cases, hello deployment name is hello same as hello cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="f5ecf-149">Tout d’abord, vérifiez si vous pouvez migrer le service de cloud computing hello hello suivant les commandes à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="f5ecf-149">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="f5ecf-150">Préparer les ordinateurs virtuels de hello dans le service cloud hello pour la migration.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-150">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="f5ecf-151">Vous avez deux options toochoose, à partir de.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-151">You have two options toochoose from.</span></span>

<span data-ttu-id="f5ecf-152">Si vous souhaitez toomigrate hello machines virtuelles tooa plate-forme réseau virtuel créé, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-152">If you want toomigrate hello VMs tooa platform-created virtual network, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="f5ecf-153">Si vous souhaitez tooan toomigrate réseau virtuel dans le modèle de déploiement du Gestionnaire de ressources hello existant, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-153">If you want toomigrate tooan existing virtual network in hello Resource Manager deployment model, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="f5ecf-154">Une fois hello Préparer opération a réussi, vous pouvez examiner hello documenté tooget hello état de la migration de machines virtuelles de hello et vérifier qu’ils sont Bonjour `Prepared` état.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-154">After hello prepare operation is successful, you can look through hello verbose output tooget hello migration state of hello VMs and ensure that they are in hello `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="f5ecf-155">Vérifiez la configuration de hello pour hello préparé des ressources à l’aide de l’interface CLI ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-155">Check hello configuration for hello prepared resources by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="f5ecf-156">Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-156">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="f5ecf-157">Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-157">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="f5ecf-158">Étape 4 : Option 2 - Migration de machines virtuelles dans un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f5ecf-158">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="f5ecf-159">Réseau virtuel de prélèvement hello que vous souhaitez toomigrate.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-159">Pick hello virtual network that you want toomigrate.</span></span> <span data-ttu-id="f5ecf-160">Notez que si le réseau virtuel de hello contient les rôles web/de travail ou des machines virtuelles avec des configurations non prises en charge, vous obtenez un message d’erreur de validation.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-160">Note that if hello virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="f5ecf-161">Obtient tous les réseaux virtuels hello dans l’abonnement hello à l’aide de hello après la commande.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-161">Get all hello virtual networks in hello subscription by using hello following command.</span></span>

    azure network vnet list

<span data-ttu-id="f5ecf-162">Hello sortie ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="f5ecf-162">hello output will look something like this:</span></span>

![Capture d’écran de ligne de commande hello avec le nom de réseau virtuel entier hello mis en surbrillance.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="f5ecf-164">Bonjour exemple ci-dessus, hello **%virtualnetworkname** est le nom complet de hello **« Classicubuntu16 classicubuntu16 de groupe »**.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-164">In hello above example, hello **virtualNetworkName** is hello entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="f5ecf-165">Tout d’abord, vérifiez si vous pouvez migrer hello virtual network utilisant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f5ecf-165">First, validate if you can migrate hello virtual network using hello following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="f5ecf-166">Préparer les réseaux de hello de votre choix pour la migration à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-166">Prepare hello virtual network of your choice for migration by using hello following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="f5ecf-167">Vérifiez la configuration de hello pour hello préparé des machines virtuelles à l’aide de l’interface CLI ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-167">Check hello configuration for hello prepared virtual machines by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="f5ecf-168">Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-168">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="f5ecf-169">Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-169">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="f5ecf-170">Étape 5 : migration d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="f5ecf-170">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="f5ecf-171">Une fois que vous avez terminé la migration d’ordinateurs virtuels hello, nous vous recommandons de que migrer de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-171">Once you're done migrating hello virtual machines, we recommend you migrate hello storage account.</span></span>

<span data-ttu-id="f5ecf-172">Préparer la migration à l’aide de hello commande suivante compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="f5ecf-172">Prepare hello storage account for migration by using hello following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="f5ecf-173">Vérifiez la configuration de hello pour hello préparé le compte de stockage à l’aide de l’interface CLI ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-173">Check hello configuration for hello prepared storage account by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="f5ecf-174">Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-174">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="f5ecf-175">Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="f5ecf-175">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="f5ecf-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f5ecf-176">Next steps</span></span>

* [<span data-ttu-id="f5ecf-177">Vue d’ensemble de la plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="f5ecf-177">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f5ecf-178">Techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="f5ecf-178">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f5ecf-179">Planification de la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="f5ecf-179">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f5ecf-180">Utiliser les ressources IaaS PowerShell toomigrate classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="f5ecf-180">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="f5ecf-181">Outils de communauté qui contribuent à la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="f5ecf-181">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="f5ecf-182">Passer en revue les erreurs courantes de migration</span><span class="sxs-lookup"><span data-stu-id="f5ecf-182">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f5ecf-183">Hello de révision plus Forum aux questions sur la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="f5ecf-183">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
