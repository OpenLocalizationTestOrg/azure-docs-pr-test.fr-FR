---
title: Migrer vers Resource Manager avec PowerShell | Microsoft Docs
description: "Cet article décrit pas à pas la procédure de migration de ressources IaaS, comme les machines virtuelles (VM), les réseaux virtuels (VNET) et les comptes de stockage, prise en charge par la plateforme de l’environnement Classic vers Azure Resource Manager (ARM) à l’aide de commandes Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 489e6cc6bd3c5b36635f5f7e398d08fed681d2e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="ec315-103">Migration de ressources IaaS d’un environnement Classic vers Azure Resource Manager à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec315-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="ec315-104">Ces étapes vous montrent comment utiliser les commandes Azure PowerShell pour migrer des ressources d’infrastructure en tant que service (IaaS) à partir du modèle de déploiement Classic vers le modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec315-104">These steps show you how to use Azure PowerShell commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="ec315-105">Si vous le souhaitez, vous pouvez également migrer des ressources à l’aide de [l’Interface de ligne de commande Azure (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ec315-105">If you want, you can also migrate resources by using the [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="ec315-106">Pour plus d’informations sur les scénarios de migration pris en charge, consultez [Migration prise en charge par la plateforme de ressources IaaS Classic vers Azure Resource Manager](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ec315-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="ec315-107">Pour un guide détaillé et une procédure pas à pas pour la migration, consultez [Étude technique approfondie de la migration prise en charge par la plateforme de ressources Classic vers Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="ec315-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic to Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="ec315-108">Passer en revue les erreurs courantes de migration</span><span class="sxs-lookup"><span data-stu-id="ec315-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="ec315-109">Voici un diagramme de flux permettant d’identifier l’ordre dans lequel les étapes doivent être exécutées lors d’un processus de migration.</span><span class="sxs-lookup"><span data-stu-id="ec315-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Screenshot that shows the migration steps](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="ec315-111">Étape 1 : planifier la migration</span><span class="sxs-lookup"><span data-stu-id="ec315-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="ec315-112">Voici quelques bonnes pratiques recommandées lorsque vous évaluez la migration de ressources IaaS d’un environnement Classic vers Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec315-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="ec315-113">Lisez les [Fonctionnalités et configurations prises en charge et non prises en charge](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ec315-113">Read through the [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="ec315-114">Si vous avez des machines virtuelles qui utilisent des configurations ou fonctionnalités non prises en charge, nous vous conseillons d’attendre que leur prise en charge soit annoncée.</span><span class="sxs-lookup"><span data-stu-id="ec315-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the configuration/feature support to be announced.</span></span> <span data-ttu-id="ec315-115">Vous pouvez également supprimer cette fonctionnalité ou modifier cette configuration pour permettre la migration si cela répond à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="ec315-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration to enable migration.</span></span>
* <span data-ttu-id="ec315-116">Si vous avez déjà des scripts automatisés qui déploient votre infrastructure et vos applications, essayez de créer une configuration de test similaire à l’aide de ces scripts pour la migration.</span><span class="sxs-lookup"><span data-stu-id="ec315-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="ec315-117">Vous pouvez également configurer des environnements de test à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ec315-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec315-118">Les passerelles d’application ne sont actuellement pas prises en charge pour la migration de déploiement classique vers Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec315-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="ec315-119">Pour migrer un réseau virtuel classique avec une passerelle d’application, supprimez la passerelle avant d’exécuter une opération de préparation pour déplacer le réseau.</span><span class="sxs-lookup"><span data-stu-id="ec315-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="ec315-120">Après avoir effectué la migration, reconnectez la passerelle dans Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec315-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="ec315-121">Les passerelles ExpressRoute se connectant à des circuits ExpressRoute dans un autre abonnement ne peuvent pas être migrées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ec315-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="ec315-122">Dans ce cas, supprimez la passerelle ExpressRoute, migrez le réseau virtuel et recréez la passerelle.</span><span class="sxs-lookup"><span data-stu-id="ec315-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="ec315-123">Pour plus d’informations, cnsultez [Migrer des circuits ExpressRoute et les réseaux virtuels associés du modèle de déploiement classique au modèle de déploiement Resource Manager](../../expressroute/expressroute-migration-classic-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ec315-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="ec315-124">Étape 2 : installer la dernière version d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec315-124">Step 2: Install the latest version of Azure PowerShell</span></span>
<span data-ttu-id="ec315-125">Il existe deux options principales d’installation d’Azure PowerShell : [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) et [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="ec315-125">There are two main options to install Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="ec315-126">WebPI reçoit des mises à jour mensuelles.</span><span class="sxs-lookup"><span data-stu-id="ec315-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="ec315-127">PowerShell Gallery reçoit des mises à jour en continu.</span><span class="sxs-lookup"><span data-stu-id="ec315-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="ec315-128">Cet article est basé sur Azure PowerShell version 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="ec315-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="ec315-129">Pour connaître la procédure d’installation, consultez l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ec315-129">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-the-subscription-in-azure-portal"></a><span data-ttu-id="ec315-130">Étape 3 : vérifier que vous êtes administrateur de l’abonnement dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ec315-130">Step 3: Ensure that you are an administrator for the subscription in Azure portal</span></span>
<span data-ttu-id="ec315-131">Pour effectuer cette migration, vous devez être ajouté en tant que coadministrateur de l’abonnement dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ec315-131">To perform this migration, you must be added as a co-administrator for the subscription in the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="ec315-132">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ec315-132">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ec315-133">Dans le menu Hub, sélectionnez **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ec315-133">On the Hub menu, select **Subscription**.</span></span> <span data-ttu-id="ec315-134">Si vous ne le voyez pas, sélectionnez **Autres services**.</span><span class="sxs-lookup"><span data-stu-id="ec315-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="ec315-135">Recherchez l’entrée d’abonnement appropriée, puis examinez le champ **MON RÔLE**.</span><span class="sxs-lookup"><span data-stu-id="ec315-135">Find the appropriate subscription entry, then look at the **MY ROLE** field.</span></span> <span data-ttu-id="ec315-136">Pour un coadministrateur, la valeur doit être _Administrateur de compte_.</span><span class="sxs-lookup"><span data-stu-id="ec315-136">For a co-administrator, the value should be _Account admin_.</span></span>

<span data-ttu-id="ec315-137">Si vous n’êtes pas en mesure d’ajouter un coadministrateur, contactez un administrateur de service ou un coadministrateur de l’abonnement afin qu’il vous ajoute.</span><span class="sxs-lookup"><span data-stu-id="ec315-137">If you are not able to add a co-administrator, then contact a service administrator or co-administrator for the subscription to get yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="ec315-138">Étape 4 : définition de votre abonnement inscription pour la migration</span><span class="sxs-lookup"><span data-stu-id="ec315-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="ec315-139">Commencez par démarrer une invite de commandes PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ec315-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="ec315-140">Pour la migration, vous devez configurer votre environnement à la fois pour l’environnement Classic et pour Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec315-140">For migration, you need to set up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="ec315-141">Connectez-vous à votre compte pour le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec315-141">Sign in to your account for the Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="ec315-142">Obtenez tous les abonnements disponibles à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-142">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="ec315-143">Définissez votre abonnement Azure pour la session active.</span><span class="sxs-lookup"><span data-stu-id="ec315-143">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="ec315-144">Cet exemple définit le nom d’abonnement par défaut sur **My Azure Subscription**.</span><span class="sxs-lookup"><span data-stu-id="ec315-144">This example sets the default subscription name to **My Azure Subscription**.</span></span> <span data-ttu-id="ec315-145">Remplacez l’exemple de nom d’abonnement par le vôtre.</span><span class="sxs-lookup"><span data-stu-id="ec315-145">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="ec315-146">L’inscription constitue une étape unique, mais vous devez le faire une seule fois avant de tenter la migration.</span><span class="sxs-lookup"><span data-stu-id="ec315-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="ec315-147">Sans vous inscrire, vous verrez le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="ec315-147">Without registering, you see the following error message:</span></span>
>
> <span data-ttu-id="ec315-148">*Requête invalide : l’abonnement n’est pas inscrit pour la migration.*</span><span class="sxs-lookup"><span data-stu-id="ec315-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="ec315-149">Inscrivez-vous auprès du fournisseur de ressources de migration à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-149">Register with the migration resource provider by using the following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="ec315-150">Veuillez patienter cinq minutes le temps que l’inscription se termine.</span><span class="sxs-lookup"><span data-stu-id="ec315-150">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="ec315-151">Vous pouvez vérifier l’état de l’approbation à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-151">You can check the status of the approval by using the following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="ec315-152">Assurez-vous que RegistrationState est `Registered` avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="ec315-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="ec315-153">Connectez-vous à votre compte pour le modèle Classic.</span><span class="sxs-lookup"><span data-stu-id="ec315-153">Now sign in to your account for the classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="ec315-154">Obtenez tous les abonnements disponibles à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-154">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="ec315-155">Définissez votre abonnement Azure pour la session active.</span><span class="sxs-lookup"><span data-stu-id="ec315-155">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="ec315-156">Cet exemple définit l’abonnement par défaut sur **My Azure Subscription**.</span><span class="sxs-lookup"><span data-stu-id="ec315-156">This example sets the default subscription to **My Azure Subscription**.</span></span> <span data-ttu-id="ec315-157">Remplacez l’exemple de nom d’abonnement par le vôtre.</span><span class="sxs-lookup"><span data-stu-id="ec315-157">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="ec315-158">Étape 5 : vérification du nombre de cœurs de machines virtuelles Azure Resource Manager dans la région Azure de votre déploiement ou réseau virtuel actuel</span><span class="sxs-lookup"><span data-stu-id="ec315-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="ec315-159">Vous pouvez utiliser la commande PowerShell suivante pour vérifier la quantité de cœurs dont vous disposez actuellement dans Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec315-159">You can use the following PowerShell command to check the current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="ec315-160">Pour en savoir plus sur les quotas de cœurs, consultez [Limites et Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="ec315-160">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="ec315-161">Cet exemple vérifie la disponibilité dans la région **ouest des États-Unis**.</span><span class="sxs-lookup"><span data-stu-id="ec315-161">This example checks the availability in the **West US** region.</span></span> <span data-ttu-id="ec315-162">Remplacez l’exemple de nom de région par le vôtre.</span><span class="sxs-lookup"><span data-stu-id="ec315-162">Replace the example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-to-migrate-your-iaas-resources"></a><span data-ttu-id="ec315-163">Étape 6 : exécution de commandes pour effectuer la migration de vos ressources IaaS</span><span class="sxs-lookup"><span data-stu-id="ec315-163">Step 6: Run commands to migrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="ec315-164">Toutes les opérations décrites ici sont idempotentes.</span><span class="sxs-lookup"><span data-stu-id="ec315-164">All the operations described here are idempotent.</span></span> <span data-ttu-id="ec315-165">Si vous rencontrez un problème autre qu’une fonctionnalité non prise en charge ou qu’une erreur de configuration, nous vous recommandons de réexécuter la procédure de préparation, d’abandon ou de validation.</span><span class="sxs-lookup"><span data-stu-id="ec315-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="ec315-166">La plateforme réessaie alors d’exécuter l’action.</span><span class="sxs-lookup"><span data-stu-id="ec315-166">The platform then tries the action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="ec315-167">Étape 6.1 : Option 1 - migrer les machines virtuelles vers un service cloud (pas un réseau virtuel)</span><span class="sxs-lookup"><span data-stu-id="ec315-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="ec315-168">Obtenez la liste des services cloud à l’aide de la commande suivante, puis choisissez le service cloud que vous voulez migrer.</span><span class="sxs-lookup"><span data-stu-id="ec315-168">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="ec315-169">La commande renvoie un message d’erreur si les machines virtuelles du service cloud sont dans un réseau virtuel ou si elles ont des rôles web/de travail.</span><span class="sxs-lookup"><span data-stu-id="ec315-169">If the VMs in the cloud service are in a virtual network or if they have web or worker roles, the command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="ec315-170">Obtenez le nom du déploiement du service cloud.</span><span class="sxs-lookup"><span data-stu-id="ec315-170">Get the deployment name for the cloud service.</span></span> <span data-ttu-id="ec315-171">Dans cet exemple, le nom du service est **Mon service**.</span><span class="sxs-lookup"><span data-stu-id="ec315-171">In this example, the service name is **My Service**.</span></span> <span data-ttu-id="ec315-172">Remplacez l’exemple de nom de service avec votre propre nom de service.</span><span class="sxs-lookup"><span data-stu-id="ec315-172">Replace the example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="ec315-173">Préparez les machines virtuelles dans le service cloud pour la migration.</span><span class="sxs-lookup"><span data-stu-id="ec315-173">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="ec315-174">Vous disposez de deux options.</span><span class="sxs-lookup"><span data-stu-id="ec315-174">You have two options to choose from.</span></span>

* <span data-ttu-id="ec315-175">**Option 1. Migrer les machines virtuelles vers un réseau virtuel créé à partir d’une plateforme**</span><span class="sxs-lookup"><span data-stu-id="ec315-175">**Option 1. Migrate the VMs to a platform-created virtual network**</span></span>

    <span data-ttu-id="ec315-176">La première étape consiste à valider si vous pouvez migrer le service cloud à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ec315-176">First, validate if you can migrate the cloud service using the following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="ec315-177">La commande ci-dessus affiche les avertissements et erreurs qui bloquent la migration.</span><span class="sxs-lookup"><span data-stu-id="ec315-177">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="ec315-178">Si la validation se déroule correctement, passez à l’étape de **préparation** :</span><span class="sxs-lookup"><span data-stu-id="ec315-178">If validation is successful, then you can move on to the **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="ec315-179">**Option 2. Migrer vers un réseau virtuel existant dans le modèle de déploiement Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="ec315-179">**Option 2. Migrate to an existing virtual network in the Resource Manager deployment model**</span></span>

    <span data-ttu-id="ec315-180">Cet exemple définit le nom de groupe de ressources sur **myResourceGroup**, le nom de réseau virtuel sur **myVirtualNetwork** et le nom du sous-réseau sur **mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="ec315-180">This example sets the resource group name to **myResourceGroup**, the virtual network name to **myVirtualNetwork** and the subnet name to **mySubNet**.</span></span> <span data-ttu-id="ec315-181">Remplacez les noms dans l’exemple par les noms de vos propres ressources.</span><span class="sxs-lookup"><span data-stu-id="ec315-181">Replace the names in the example with the names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="ec315-182">Vérifiez d’abord que vous pouvez migrer le réseau virtuel à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-182">First, validate if you can migrate the virtual network using the following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="ec315-183">La commande ci-dessus affiche les avertissements et erreurs qui bloquent la migration.</span><span class="sxs-lookup"><span data-stu-id="ec315-183">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="ec315-184">Si la validation se déroule correctement, vous pouvez passer à l’étape de la préparation :</span><span class="sxs-lookup"><span data-stu-id="ec315-184">If validation is successful, then you can proceed with the following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="ec315-185">Une fois l’opération de préparation effectuée avec une des options précédentes, interrogez l’état de la migration des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="ec315-185">After the Prepare operation succeeds with either of the preceding options, query the migration state of the VMs.</span></span> <span data-ttu-id="ec315-186">Assurez-vous qu’elles ont l’état `Prepared` .</span><span class="sxs-lookup"><span data-stu-id="ec315-186">Ensure that they are in the `Prepared` state.</span></span>

<span data-ttu-id="ec315-187">Cet exemple définit le nom de la machine virtuelle sur **myVM**.</span><span class="sxs-lookup"><span data-stu-id="ec315-187">This example sets the VM name to **myVM**.</span></span> <span data-ttu-id="ec315-188">Remplacez l’exemple de nom avec votre propre nom de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ec315-188">Replace the example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="ec315-189">Vérifiez la configuration pour les ressources préparées à l’aide de PowerShell ou du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ec315-189">Check the configuration for the prepared resources by using either PowerShell or the Azure portal.</span></span> <span data-ttu-id="ec315-190">Si vous n’êtes pas prêt pour la migration et que vous souhaitez revenir à l’ancien état, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-190">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="ec315-191">Si la configuration préparée semble correcte, vous pouvez continuer et valider les ressources à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-191">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="ec315-192">Étape 6.1 : Option 2 - migrer les machines virtuelles vers un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="ec315-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="ec315-193">Pour migrer des machines virtuelles dans un service cloud, vous migrez le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="ec315-193">To migrate virtual machines in a virtual network, you migrate the virtual network.</span></span> <span data-ttu-id="ec315-194">Les machines virtuelles migrent automatiquement avec le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="ec315-194">The virtual machines automatically migrate with the virtual network.</span></span> <span data-ttu-id="ec315-195">Sélectionnez le réseau virtuel dont vous souhaitez effectuer la migration.</span><span class="sxs-lookup"><span data-stu-id="ec315-195">Pick the virtual network that you want to migrate.</span></span>
> [!NOTE]
> <span data-ttu-id="ec315-196">[Migrez une machine virtuelle classique unique](migrate-single-classic-to-resource-manager.md) en créant une nouvelle machine virtuelle Resource Manager avec des disques gérés en utilisant les fichiers de disque dur virtuel (système d’exploitation et données) de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ec315-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using the VHD (OS and data) files of the virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="ec315-197">Le nom du réseau virtuel peut différer de ce qui est affiché dans le nouveau portail.</span><span class="sxs-lookup"><span data-stu-id="ec315-197">The virtual network name might be different from what is shown in the new Portal.</span></span> <span data-ttu-id="ec315-198">Le nouveau portail Azure affiche le nom sous la forme `[vnet-name]`, mais le nom réel du réseau virtuel est du type `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="ec315-198">The new Azure Portal displays the name as `[vnet-name]` but the actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="ec315-199">Avant de migrer, recherchez le nom du réseau virtuel à l’aide de la commande `Get-AzureVnetSite | Select -Property Name`, ou affichez-le dans l’ancien portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ec315-199">Before migrating, lookup the actual virtual network name using the command `Get-AzureVnetSite | Select -Property Name` or view it in the old Azure Portal.</span></span> 

<span data-ttu-id="ec315-200">Cet exemple définit le nom de réseau virtuel sur **myVnet**.</span><span class="sxs-lookup"><span data-stu-id="ec315-200">This example sets the virtual network name to **myVnet**.</span></span> <span data-ttu-id="ec315-201">Remplacez l’exemple de nom de réseau virtuel par le vôtre.</span><span class="sxs-lookup"><span data-stu-id="ec315-201">Replace the example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="ec315-202">Vous obtenez un message d’erreur pour la validation si le réseau virtuel contient des rôles web/de travail ou des machines virtuelles avec des configurations non prises en charge.</span><span class="sxs-lookup"><span data-stu-id="ec315-202">If the virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="ec315-203">La première étape consiste à valider si vous pouvez migrer le réseau virtuel à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-203">First, validate if you can migrate the virtual network by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="ec315-204">La commande ci-dessus affiche les avertissements et erreurs qui bloquent la migration.</span><span class="sxs-lookup"><span data-stu-id="ec315-204">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="ec315-205">Si la validation se déroule correctement, vous pouvez passer à l’étape de la préparation :</span><span class="sxs-lookup"><span data-stu-id="ec315-205">If validation is successful, then you can proceed with the following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="ec315-206">Vérifiez la configuration pour les machines virtuelles préparées à l’aide d’Azure PowerShell ou du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ec315-206">Check the configuration for the prepared virtual machines by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="ec315-207">Si vous n’êtes pas prêt pour la migration et que vous souhaitez revenir à l’ancien état, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-207">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="ec315-208">Si la configuration préparée semble correcte, vous pouvez continuer et valider les ressources à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-208">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="ec315-209">Étape 6.2 : migrer un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="ec315-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="ec315-210">Une fois que vous avez terminé la migration des machines virtuelles, nous vous recommandons de migrer les comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec315-210">Once you're done migrating the virtual machines, we recommend you migrate the storage accounts.</span></span>

<span data-ttu-id="ec315-211">Avant de migrer le compte de stockage, effectuez les vérifications de conditions préalables suivantes :</span><span class="sxs-lookup"><span data-stu-id="ec315-211">Before you migrate the storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="ec315-212">**Migrer des machines virtuelles classiques dont les disques sont stockés dans le compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="ec315-212">**Migrate classic virtual machines whose disks are stored in the storage account**</span></span>

    <span data-ttu-id="ec315-213">La commande précédente renvoie les propriétés RoleName et DiskName de tous les disques de machine virtuelle classique dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec315-213">Preceding command returns RoleName and DiskName properties of all the classic VM disks in the storage account.</span></span> <span data-ttu-id="ec315-214">RoleName est le nom de la machine virtuelle à laquelle un disque est joint.</span><span class="sxs-lookup"><span data-stu-id="ec315-214">RoleName is the name of the virtual machine to which a disk is attached.</span></span> <span data-ttu-id="ec315-215">Si la commande précédente renvoie des disques, assurez-vous que les machines virtuelles sur lesquelles ces disques sont joints sont migrés avant de migrer le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec315-215">If preceding command returns disks then ensure that virtual machines to which these disks are attached are migrated before migrating the storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="ec315-216">**Supprimer les disques de machine virtuelle classique détachés stockés dans le compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="ec315-216">**Delete unattached classic VM disks stored in the storage account**</span></span>

    <span data-ttu-id="ec315-217">Recherchez les disques de machine virtuelle détachés dans le compte de stockage à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-217">Find unattached classic VM disks in the storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="ec315-218">Si la commande ci-dessus renvoie des disques, supprimez-les en utilisant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="ec315-219">**Supprimer les images de machine virtuelle stockées dans le compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="ec315-219">**Delete VM images stored in the storage account**</span></span>

    <span data-ttu-id="ec315-220">La commande précédente renvoie toutes les images de machine virtuelle avec un disque de système d’exploitation stocké dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec315-220">Preceding command returns all the VM images with OS disk stored in the storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="ec315-221">La commande précédente renvoie toutes les images de machine virtuelle avec les disques de données stockés dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec315-221">Preceding command returns all the VM images with data disks stored in the storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="ec315-222">Supprimez toutes les images de machine virtuelle renvoyées par les commandes précédentes à l’aide de la commande :</span><span class="sxs-lookup"><span data-stu-id="ec315-222">Delete all the VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="ec315-223">Validez chaque compte de stockage pour la migration à l’aide de la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="ec315-223">Validate each storage account for migration by using the following command.</span></span> <span data-ttu-id="ec315-224">Dans cet exemple, le nom de compte de stockage est **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="ec315-224">In this example, the storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="ec315-225">Remplacez le nom d’exemple par celui de votre propre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec315-225">Replace the example name with the name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="ec315-226">L’étape suivante consiste à préparer le compte de stockage pour la migration.</span><span class="sxs-lookup"><span data-stu-id="ec315-226">Next step is to Prepare the storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="ec315-227">Vérifiez la configuration pour le compte de stockage préparé à l’aide d’Azure PowerShell ou du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ec315-227">Check the configuration for the prepared storage account by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="ec315-228">Si vous n’êtes pas prêt pour la migration et que vous souhaitez revenir à l’ancien état, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-228">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="ec315-229">Si la configuration préparée semble correcte, vous pouvez continuer et valider les ressources à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec315-229">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="ec315-230">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec315-230">Next steps</span></span>
* [<span data-ttu-id="ec315-231">Vue d’ensemble de la migration prise en charge par la plateforme de ressources IaaS Classic vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ec315-231">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ec315-232">Étude technique approfondie de la migration prise en charge par la plateforme de ressources Classic vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ec315-232">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ec315-233">Planification de la migration des ressources IaaS d’Azure Classic vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ec315-233">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ec315-234">Faire migrer des ressources IaaS Classic vers Azure Resource Manager à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ec315-234">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ec315-235">Outils de la communauté pour aider à la migration de ressources IaaS de Classic vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ec315-235">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ec315-236">Passer en revue les erreurs courantes de migration</span><span class="sxs-lookup"><span data-stu-id="ec315-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ec315-237">Passez en revue les questions fréquemment posées sur la migration des ressources IaaS de Classic vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ec315-237">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
