---
title: aaaMigrate tooResource Manager avec PowerShell | Documents Microsoft
description: "Cet article assiste hello plateforme prise en charge la migration de ressources IaaS telles que les machines virtuelles (VM), les réseaux virtuels (réseaux virtuels) et les comptes de stockage à partir de tooAzure classique Resource Manager (ARM) à l’aide de commandes Azure PowerShell"
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
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="c6795-103">Migrer les ressources de IaaS de classique tooAzure Gestionnaire de ressources à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6795-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="c6795-104">Ces étapes vous montrent comment toouse Azure PowerShell commandes toomigrate infrastructure en tant qu’une ressource de service (IaaS) à partir du modèle de déploiement du modèle toohello Azure Resource Manager hello déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="c6795-104">These steps show you how toouse Azure PowerShell commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="c6795-105">Si vous le souhaitez, vous pouvez également migrer des ressources à l’aide de hello [Azure Interface de ligne de commande (CLI d’Azure)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c6795-105">If you want, you can also migrate resources by using hello [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="c6795-106">Pour plus d’informations sur les scénarios de migration pris en charge, consultez [plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6795-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic tooAzure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="c6795-107">Pour obtenir des instructions détaillées et une procédure pas à pas la migration, consultez [techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="c6795-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="c6795-108">Passer en revue les erreurs courantes de migration</span><span class="sxs-lookup"><span data-stu-id="c6795-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="c6795-109">Voici un ordre de hello tooidentify organigramme dans lequel les étapes doivent toobe exécutée pendant un processus de migration</span><span class="sxs-lookup"><span data-stu-id="c6795-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Capture d’écran qui illustre les étapes de migration hello](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="c6795-111">Étape 1 : planifier la migration</span><span class="sxs-lookup"><span data-stu-id="c6795-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="c6795-112">Voici quelques meilleures pratiques que nous recommandons lors de l’évaluation de la migration des ressources IaaS de classique tooResource Manager :</span><span class="sxs-lookup"><span data-stu-id="c6795-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="c6795-113">Lisez hello [pris en charge et non pris en charge des fonctionnalités et configurations](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6795-113">Read through hello [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="c6795-114">Si vous avez des ordinateurs virtuels qui utilisent des configurations non prises en charge et fonctionnalités, nous vous recommandons d’attendre hello configuration ou une fonctionnalité prise en charge toobe a annoncé.</span><span class="sxs-lookup"><span data-stu-id="c6795-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello configuration/feature support toobe announced.</span></span> <span data-ttu-id="c6795-115">Si elle répond à vos besoins, supprimer cette fonctionnalité ou sortir de cette migration tooenable de configuration.</span><span class="sxs-lookup"><span data-stu-id="c6795-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration tooenable migration.</span></span>
* <span data-ttu-id="c6795-116">Si vous avez automatisé scripts aujourd'hui à déployer votre infrastructure et vos applications, essayez de toocreate une configuration de test similaire à l’aide de ces scripts pour la migration.</span><span class="sxs-lookup"><span data-stu-id="c6795-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="c6795-117">Ou bien, vous pouvez définir des environnements d’exemple à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c6795-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6795-118">Passerelles d’application ne sont pas actuellement pris en charge pour la migration de classique tooResource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6795-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="c6795-119">toomigrate un réseau virtuel classique avec une passerelle d’Application, supprimer la passerelle de hello avant l’exécution d’un réseau de Préparer opération toomove hello.</span><span class="sxs-lookup"><span data-stu-id="c6795-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="c6795-120">Après avoir effectué la migration de hello, reconnectez le passerelle hello dans Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6795-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="c6795-121">Les passerelles ExpressRoute connexion circuits tooExpressRoute dans un autre abonnement ne peut pas être migrés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="c6795-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="c6795-122">Dans ce cas, supprimez la passerelle ExpressRoute de hello, migrer un réseau virtuel hello et recréez hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="c6795-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="c6795-123">Consultez [ExpressRoute de migrer des circuits et associé des réseaux virtuels à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](../../expressroute/expressroute-migration-classic-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="c6795-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="c6795-124">Étape 2 : Installer la version la plus récente d’Azure PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="c6795-124">Step 2: Install hello latest version of Azure PowerShell</span></span>
<span data-ttu-id="c6795-125">Il existe deux options principales tooinstall Azure PowerShell : [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) ou [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="c6795-125">There are two main options tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="c6795-126">WebPI reçoit des mises à jour mensuelles.</span><span class="sxs-lookup"><span data-stu-id="c6795-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="c6795-127">PowerShell Gallery reçoit des mises à jour en continu.</span><span class="sxs-lookup"><span data-stu-id="c6795-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="c6795-128">Cet article est basé sur Azure PowerShell version 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="c6795-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="c6795-129">Pour obtenir des instructions d’installation, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c6795-129">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a><span data-ttu-id="c6795-130">Étape 3 : Vérifiez que vous êtes un administrateur pour l’abonnement de hello dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c6795-130">Step 3: Ensure that you are an administrator for hello subscription in Azure portal</span></span>
<span data-ttu-id="c6795-131">tooperform cette migration, vous devez être ajouté en tant que coadministrateur pour l’abonnement hello Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6795-131">tooperform this migration, you must be added as a co-administrator for hello subscription in hello [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="c6795-132">L’authentification à hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6795-132">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c6795-133">Dans le menu du Hub hello, sélectionnez **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="c6795-133">On hello Hub menu, select **Subscription**.</span></span> <span data-ttu-id="c6795-134">Si vous ne le voyez pas, sélectionnez **Autres services**.</span><span class="sxs-lookup"><span data-stu-id="c6795-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="c6795-135">Trouver l’entrée d’abonnement approprié hello, puis examinez hello **mon rôle** champ.</span><span class="sxs-lookup"><span data-stu-id="c6795-135">Find hello appropriate subscription entry, then look at hello **MY ROLE** field.</span></span> <span data-ttu-id="c6795-136">Pour un coadministrateur, valeur de hello doit être _admin. compte_.</span><span class="sxs-lookup"><span data-stu-id="c6795-136">For a co-administrator, hello value should be _Account admin_.</span></span>

<span data-ttu-id="c6795-137">Si vous n’êtes pas en mesure de tooadd un coadministrateur, puis contactez un administrateur de service ou un coadministrateur pour tooget d’abonnement hello vous-même ajouté.</span><span class="sxs-lookup"><span data-stu-id="c6795-137">If you are not able tooadd a co-administrator, then contact a service administrator or co-administrator for hello subscription tooget yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="c6795-138">Étape 4 : définition de votre abonnement inscription pour la migration</span><span class="sxs-lookup"><span data-stu-id="c6795-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="c6795-139">Commencez par démarrer une invite de commandes PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6795-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="c6795-140">Pour la migration, vous devez tooset de votre environnement pour les deux classique et Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="c6795-140">For migration, you need tooset up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="c6795-141">Compte tooyour pour le modèle de gestionnaire de ressources hello de connexion.</span><span class="sxs-lookup"><span data-stu-id="c6795-141">Sign in tooyour account for hello Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="c6795-142">Obtenir les abonnements disponibles hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-142">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="c6795-143">Définissez votre abonnement Azure pour hello la session active.</span><span class="sxs-lookup"><span data-stu-id="c6795-143">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="c6795-144">Cet exemple définit hello le nom de l’abonnement par défaut trop**mon abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="c6795-144">This example sets hello default subscription name too**My Azure Subscription**.</span></span> <span data-ttu-id="c6795-145">Remplacez le nom de l’abonnement exemple hello avec vos propres.</span><span class="sxs-lookup"><span data-stu-id="c6795-145">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="c6795-146">L’inscription constitue une étape unique, mais vous devez le faire une seule fois avant de tenter la migration.</span><span class="sxs-lookup"><span data-stu-id="c6795-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="c6795-147">Sans l’enregistrer, vous voyez hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="c6795-147">Without registering, you see hello following error message:</span></span>
>
> <span data-ttu-id="c6795-148">*Requête invalide : l’abonnement n’est pas inscrit pour la migration.*</span><span class="sxs-lookup"><span data-stu-id="c6795-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="c6795-149">Enregistrer avec le fournisseur de ressources hello migration à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-149">Register with hello migration resource provider by using hello following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="c6795-150">Attendez cinq minutes pour hello inscription toofinish.</span><span class="sxs-lookup"><span data-stu-id="c6795-150">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="c6795-151">Vous pouvez vérifier l’état hello d’approbation de hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-151">You can check hello status of hello approval by using hello following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="c6795-152">Assurez-vous que RegistrationState est `Registered` avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="c6795-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="c6795-153">Connectez-vous maintenant compte tooyour pour le modèle classique de hello.</span><span class="sxs-lookup"><span data-stu-id="c6795-153">Now sign in tooyour account for hello classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="c6795-154">Obtenir les abonnements disponibles hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-154">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="c6795-155">Définissez votre abonnement Azure pour hello la session active.</span><span class="sxs-lookup"><span data-stu-id="c6795-155">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="c6795-156">Cet exemple définit abonnement par défaut de hello trop**mon abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="c6795-156">This example sets hello default subscription too**My Azure Subscription**.</span></span> <span data-ttu-id="c6795-157">Remplacez le nom de l’abonnement exemple hello avec vos propres.</span><span class="sxs-lookup"><span data-stu-id="c6795-157">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="c6795-158">Étape 5 : Vérifiez que vous disposez assez de cœurs Machine virtuelle de Azure Resource Manager Bonjour région Azure de votre déploiement en cours ou de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="c6795-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="c6795-159">Vous pouvez utiliser hello suivant PowerShell commande toocheck hello nombre actuel de cœurs que dans le Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="c6795-159">You can use hello following PowerShell command toocheck hello current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="c6795-160">toolearn en savoir plus sur les quotas de base, consultez [hello Azure Resource Manager et les limites](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="c6795-160">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="c6795-161">Cet exemple vérifie la disponibilité de hello Bonjour **ouest des États-Unis** région.</span><span class="sxs-lookup"><span data-stu-id="c6795-161">This example checks hello availability in hello **West US** region.</span></span> <span data-ttu-id="c6795-162">Remplacez le nom de la région exemple hello par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="c6795-162">Replace hello example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a><span data-ttu-id="c6795-163">Étape 6 : Exécuter des commandes toomigrate vos ressources IaaS</span><span class="sxs-lookup"><span data-stu-id="c6795-163">Step 6: Run commands toomigrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="c6795-164">Toutes les opérations de hello décrites ici sont idempotent.</span><span class="sxs-lookup"><span data-stu-id="c6795-164">All hello operations described here are idempotent.</span></span> <span data-ttu-id="c6795-165">Si vous avez un problème autre qu’une fonctionnalité non prise en charge ou une erreur de configuration, nous vous recommandons de relancer hello préparer, abandonner ou valider l’opération.</span><span class="sxs-lookup"><span data-stu-id="c6795-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="c6795-166">plateforme de Hello tente ensuite action hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="c6795-166">hello platform then tries hello action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="c6795-167">Étape 6.1 : Option 1 - migrer les machines virtuelles vers un service cloud (pas un réseau virtuel)</span><span class="sxs-lookup"><span data-stu-id="c6795-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="c6795-168">Obtenez la liste de services de cloud computing à l’aide de hello commande suivante, puis sur service de cloud hello choix que vous souhaitez toomigrate hello.</span><span class="sxs-lookup"><span data-stu-id="c6795-168">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="c6795-169">Si hello machines virtuelles dans le service cloud hello se trouvent dans un réseau virtuel, ou si elles ont des rôles web ou de travail, la commande hello renvoie un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="c6795-169">If hello VMs in hello cloud service are in a virtual network or if they have web or worker roles, hello command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="c6795-170">Obtenir le nom du déploiement pour le service cloud hello hello.</span><span class="sxs-lookup"><span data-stu-id="c6795-170">Get hello deployment name for hello cloud service.</span></span> <span data-ttu-id="c6795-171">Dans cet exemple, le nom du service hello est **mon Service**.</span><span class="sxs-lookup"><span data-stu-id="c6795-171">In this example, hello service name is **My Service**.</span></span> <span data-ttu-id="c6795-172">Remplacez le nom du service exemple hello avec votre propre nom de service.</span><span class="sxs-lookup"><span data-stu-id="c6795-172">Replace hello example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="c6795-173">Préparer les ordinateurs virtuels de hello dans le service cloud hello pour la migration.</span><span class="sxs-lookup"><span data-stu-id="c6795-173">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="c6795-174">Vous avez deux options toochoose, à partir de.</span><span class="sxs-lookup"><span data-stu-id="c6795-174">You have two options toochoose from.</span></span>

* <span data-ttu-id="c6795-175">**Option 1. Migrer hello machines virtuelles tooa créé de plateforme réseau virtuel**</span><span class="sxs-lookup"><span data-stu-id="c6795-175">**Option 1. Migrate hello VMs tooa platform-created virtual network**</span></span>

    <span data-ttu-id="c6795-176">Tout d’abord, vérifiez si vous pouvez migrer le service de cloud computing hello hello suivant les commandes à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="c6795-176">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="c6795-177">Hello commande précédente affiche les avertissements et erreurs qui bloquent la migration.</span><span class="sxs-lookup"><span data-stu-id="c6795-177">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="c6795-178">Si la validation est réussie, vous pouvez déplacer sur toohello **préparation** étape :</span><span class="sxs-lookup"><span data-stu-id="c6795-178">If validation is successful, then you can move on toohello **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="c6795-179">**Option 2. Migrer tooan un réseau virtuel existant dans le modèle de déploiement du Gestionnaire de ressources hello**</span><span class="sxs-lookup"><span data-stu-id="c6795-179">**Option 2. Migrate tooan existing virtual network in hello Resource Manager deployment model**</span></span>

    <span data-ttu-id="c6795-180">Cet exemple définit hello nom groupe de ressources trop**myResourceGroup**, hello trop de nom de réseau virtuel**myVirtualNetwork** et hello nom du sous-réseau trop**mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="c6795-180">This example sets hello resource group name too**myResourceGroup**, hello virtual network name too**myVirtualNetwork** and hello subnet name too**mySubNet**.</span></span> <span data-ttu-id="c6795-181">Remplacez les noms de hello dans hello exemple avec des noms de vos propres ressources hello.</span><span class="sxs-lookup"><span data-stu-id="c6795-181">Replace hello names in hello example with hello names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="c6795-182">Tout d’abord, vérifiez si vous pouvez migrer hello virtual network utilisant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-182">First, validate if you can migrate hello virtual network using hello following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="c6795-183">Hello commande précédente affiche les avertissements et erreurs qui bloquent la migration.</span><span class="sxs-lookup"><span data-stu-id="c6795-183">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="c6795-184">Si la validation est réussie, vous pouvez poursuivre hello suivant l’étape de préparation :</span><span class="sxs-lookup"><span data-stu-id="c6795-184">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="c6795-185">Une fois hello opération de préparation réussie avec l’option de hello précédant options, interroger l’état de migration de hello Hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c6795-185">After hello Prepare operation succeeds with either of hello preceding options, query hello migration state of hello VMs.</span></span> <span data-ttu-id="c6795-186">Vérifier qu’ils sont Bonjour `Prepared` état.</span><span class="sxs-lookup"><span data-stu-id="c6795-186">Ensure that they are in hello `Prepared` state.</span></span>

<span data-ttu-id="c6795-187">Cet exemple définit hello nom d’ordinateur virtuel trop**myVM**.</span><span class="sxs-lookup"><span data-stu-id="c6795-187">This example sets hello VM name too**myVM**.</span></span> <span data-ttu-id="c6795-188">Remplacez le nom de l’exemple hello avec votre propre nom d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="c6795-188">Replace hello example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="c6795-189">Vérifiez la configuration de hello pour hello préparé des ressources à l’aide de PowerShell ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c6795-189">Check hello configuration for hello prepared resources by using either PowerShell or hello Azure portal.</span></span> <span data-ttu-id="c6795-190">Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-190">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="c6795-191">Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-191">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="c6795-192">Étape 6.1 : Option 2 - migrer les machines virtuelles vers un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="c6795-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="c6795-193">machines virtuelles de toomigrate dans un réseau virtuel, vous migrez le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c6795-193">toomigrate virtual machines in a virtual network, you migrate hello virtual network.</span></span> <span data-ttu-id="c6795-194">machines virtuelles de Hello faire migrer automatiquement avec un réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="c6795-194">hello virtual machines automatically migrate with hello virtual network.</span></span> <span data-ttu-id="c6795-195">Réseau virtuel de prélèvement hello que vous souhaitez toomigrate.</span><span class="sxs-lookup"><span data-stu-id="c6795-195">Pick hello virtual network that you want toomigrate.</span></span>
> [!NOTE]
> <span data-ttu-id="c6795-196">[Migration classique de machine virtuelle unique](migrate-single-classic-to-resource-manager.md) en créant un nouvel ordinateur virtuel de gestionnaire de ressources avec des disques gérés à l’aide de fichiers de (système d’exploitation et données) de disque dur virtuel de la machine virtuelle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="c6795-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using hello VHD (OS and data) files of hello virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="c6795-197">nom de réseau virtuel Hello peut différer de ce qui est affiché dans hello nouveau portail.</span><span class="sxs-lookup"><span data-stu-id="c6795-197">hello virtual network name might be different from what is shown in hello new Portal.</span></span> <span data-ttu-id="c6795-198">nouveau portail Azure Hello affiche nom hello en tant que `[vnet-name]` , mais le nom de réseau virtuel réelle hello est de type `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="c6795-198">hello new Azure Portal displays hello name as `[vnet-name]` but hello actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="c6795-199">Avant de migrer, nom de réseau virtuel réelle hello de recherche à l’aide de la commande hello `Get-AzureVnetSite | Select -Property Name` ni l’afficher dans hello ancien portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c6795-199">Before migrating, lookup hello actual virtual network name using hello command `Get-AzureVnetSite | Select -Property Name` or view it in hello old Azure Portal.</span></span> 

<span data-ttu-id="c6795-200">Cet exemple définit hello nom de réseau virtuel trop**myVnet**.</span><span class="sxs-lookup"><span data-stu-id="c6795-200">This example sets hello virtual network name too**myVnet**.</span></span> <span data-ttu-id="c6795-201">Remplacez le nom de réseau virtuel exemple hello avec vos propres.</span><span class="sxs-lookup"><span data-stu-id="c6795-201">Replace hello example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="c6795-202">Si les réseaux virtuels hello contient web ou des rôles de travail ou des machines virtuelles avec des configurations non prises en charge, vous obtenez un message d’erreur de validation.</span><span class="sxs-lookup"><span data-stu-id="c6795-202">If hello virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="c6795-203">Tout d’abord, vérifiez si vous pouvez migrer le réseau virtuel de hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-203">First, validate if you can migrate hello virtual network by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="c6795-204">Hello commande précédente affiche les avertissements et erreurs qui bloquent la migration.</span><span class="sxs-lookup"><span data-stu-id="c6795-204">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="c6795-205">Si la validation est réussie, vous pouvez poursuivre hello suivant l’étape de préparation :</span><span class="sxs-lookup"><span data-stu-id="c6795-205">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="c6795-206">Vérifiez la configuration de hello pour hello préparé les ordinateurs virtuels à l’aide d’Azure PowerShell ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c6795-206">Check hello configuration for hello prepared virtual machines by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="c6795-207">Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-207">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="c6795-208">Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-208">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="c6795-209">Étape 6.2 : migrer un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="c6795-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="c6795-210">Une fois que vous avez terminé la migration d’ordinateurs virtuels hello, nous vous recommandons de que migrer les comptes de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="c6795-210">Once you're done migrating hello virtual machines, we recommend you migrate hello storage accounts.</span></span>

<span data-ttu-id="c6795-211">Avant de migrer de compte de stockage hello, effectuez précédant les vérifications des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="c6795-211">Before you migrate hello storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="c6795-212">**Migrer des machines virtuelles classiques, dont les disques sont stockés dans le compte de stockage hello**</span><span class="sxs-lookup"><span data-stu-id="c6795-212">**Migrate classic virtual machines whose disks are stored in hello storage account**</span></span>

    <span data-ttu-id="c6795-213">Précédant la commande retourne les propriétés RoleName et DiskName de tous les disques de machine virtuelle classiques hello hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c6795-213">Preceding command returns RoleName and DiskName properties of all hello classic VM disks in hello storage account.</span></span> <span data-ttu-id="c6795-214">RoleName désigne hello hello toowhich de machine virtuelle qu'un disque est attaché.</span><span class="sxs-lookup"><span data-stu-id="c6795-214">RoleName is hello name of hello virtual machine toowhich a disk is attached.</span></span> <span data-ttu-id="c6795-215">Si précédant la commande retourne les disques, puis vérifiez que toowhich de machines virtuelles ces disques sont attachés sont migrés avant la migration hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c6795-215">If preceding command returns disks then ensure that virtual machines toowhich these disks are attached are migrated before migrating hello storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="c6795-216">**Supprimer des disques de machine virtuelle classiques détachés stockées dans le compte de stockage hello**</span><span class="sxs-lookup"><span data-stu-id="c6795-216">**Delete unattached classic VM disks stored in hello storage account**</span></span>

    <span data-ttu-id="c6795-217">Trouver détachés classiques disques de machine virtuelle dans le stockage hello compte à l’aide commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-217">Find unattached classic VM disks in hello storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="c6795-218">Si la commande ci-dessus renvoie des disques, supprimez-les en utilisant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="c6795-219">**Supprimer les images de machine virtuelle stockés dans le compte de stockage hello**</span><span class="sxs-lookup"><span data-stu-id="c6795-219">**Delete VM images stored in hello storage account**</span></span>

    <span data-ttu-id="c6795-220">Disque de système d’exploitation stockée dans le compte de stockage hello précédant la commande retourne toutes les images de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="c6795-220">Preceding command returns all hello VM images with OS disk stored in hello storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="c6795-221">Disques de données stockées dans le compte de stockage hello précédant la commande retourne toutes les images de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="c6795-221">Preceding command returns all hello VM images with data disks stored in hello storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="c6795-222">Supprimer toutes les images de machine virtuelle hello retournés par au-dessus de commandes à l’aide de la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="c6795-222">Delete all hello VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="c6795-223">Valider chaque compte de stockage pour la migration à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="c6795-223">Validate each storage account for migration by using hello following command.</span></span> <span data-ttu-id="c6795-224">Dans cet exemple, le nom de compte de stockage hello est **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="c6795-224">In this example, hello storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="c6795-225">Remplacer le nom de l’exemple hello avec nom hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c6795-225">Replace hello example name with hello name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="c6795-226">Étape suivante est le compte de stockage tooPrepare hello pour la migration</span><span class="sxs-lookup"><span data-stu-id="c6795-226">Next step is tooPrepare hello storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="c6795-227">Vérifiez la configuration de hello pour hello préparé le compte de stockage à l’aide d’Azure PowerShell ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c6795-227">Check hello configuration for hello prepared storage account by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="c6795-228">Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-228">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="c6795-229">Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6795-229">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="c6795-230">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c6795-230">Next steps</span></span>
* [<span data-ttu-id="c6795-231">Vue d’ensemble de la plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="c6795-231">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="c6795-232">Techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="c6795-232">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="c6795-233">Planification de la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="c6795-233">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="c6795-234">Utiliser les ressources IaaS CLI toomigrate classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="c6795-234">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="c6795-235">Outils de communauté qui contribuent à la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="c6795-235">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="c6795-236">Passer en revue les erreurs courantes de migration</span><span class="sxs-lookup"><span data-stu-id="c6795-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="c6795-237">Hello de révision plus Forum aux questions sur la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="c6795-237">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
