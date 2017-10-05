---
title: "Déplacer des circuits ExpressRoute du modèle de déploiement classique vers le modèle de déploiement Resource Manager : PowerShell : Azure | Microsoft Docs"
description: "Cette page décrit comment déplacer un circuit classique vers le modèle de déploiement Resource Manager à l’aide de PowerShell."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: c407e01e6d881cb8adcfe55faa246468669be883
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="1a880-103">Déplacer des circuits ExpressRoute du modèle de déploiement classique vers le modèle de déploiement Resource Manager à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a880-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="1a880-104">Pour utiliser un circuit ExpressRoute pour les modèles de déploiement classique et Resource Manager, vous devez déplacer ce circuit vers le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1a880-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span></span> <span data-ttu-id="1a880-105">Les sections suivantes vous aident à déplacer votre circuit à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a880-105">The following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1a880-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="1a880-106">Before you begin</span></span>

* <span data-ttu-id="1a880-107">Vérifiez que vous disposez de la dernière version des modules Azure PowerShell (au moins la version 1.0).</span><span class="sxs-lookup"><span data-stu-id="1a880-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="1a880-108">Pour plus d’informations, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a880-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="1a880-109">Veillez à consulter les [conditions préalables](expressroute-prerequisites.md), la [configuration requise pour le routage](expressroute-routing.md) et les [flux de travail](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="1a880-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="1a880-110">Examinez les informations fournies sous [Transfert des circuits ExpressRoute du modèle de déploiement classique vers le modèle de déploiement Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="1a880-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="1a880-111">Vous devez avoir bien compris les limites et les limitations.</span><span class="sxs-lookup"><span data-stu-id="1a880-111">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="1a880-112">Vérifiez que le circuit est totalement opérationnel dans le modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="1a880-112">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="1a880-113">Assurez-vous que vous disposez d’un groupe de ressources créé dans le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1a880-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="1a880-114">Déplacer un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1a880-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a><span data-ttu-id="1a880-115">Étape 1 : Collecter des informations sur le circuit à partir du modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="1a880-115">Step 1: Gather circuit details from the classic deployment model</span></span>

<span data-ttu-id="1a880-116">Connectez-vous à l’environnement classique Azure et collectez la clé de service.</span><span class="sxs-lookup"><span data-stu-id="1a880-116">Sign in to the Azure classic environment and gather the service key.</span></span>

1. <span data-ttu-id="1a880-117">Connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1a880-117">Sign in to your Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="1a880-118">Sélectionnez l’abonnement Azure approprié.</span><span class="sxs-lookup"><span data-stu-id="1a880-118">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="1a880-119">Importez les modules PowerShell pour Azure et ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1a880-119">Import the PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="1a880-120">Utilisez l’applet de commande ci-dessous pour obtenir les clés de service pour tous les circuits imprimés ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1a880-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="1a880-121">Après avoir récupéré les clés, copiez la **clé de service** du circuit que vous souhaitez déplacer vers le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1a880-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="1a880-122">Étape 2 : connexion et création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="1a880-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="1a880-123">Connectez-vous à l’environnement Resource Manager et créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1a880-123">Sign in to the Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="1a880-124">Connectez-vous à votre environnement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1a880-124">Sign in to your Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="1a880-125">Sélectionnez l’abonnement Azure approprié.</span><span class="sxs-lookup"><span data-stu-id="1a880-125">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="1a880-126">Modifiez l’extrait de code ci-dessous pour créer un groupe de ressources si vous n’en avez pas déjà un.</span><span class="sxs-lookup"><span data-stu-id="1a880-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a><span data-ttu-id="1a880-127">Étape 3 : Transférer le circuit ExpressRoute vers le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1a880-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span></span>

<span data-ttu-id="1a880-128">Vous êtes maintenant prêt à déplacer votre circuit ExpressRoute du modèle de déploiement classique vers le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1a880-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span></span> <span data-ttu-id="1a880-129">Avant de continuer, passez en revue les informations fournies sous [Transférer des circuits ExpressRoute du modèle de déploiement classique vers le modèle de déploiement Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="1a880-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="1a880-130">Pour déplacer votre circuit, modifiez et exécutez l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="1a880-130">To move your circuit, modify and run the following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="1a880-131">Une fois le déplacement terminé, le nouveau nom répertorié dans l’applet de commande précédente sera utilisé pour traiter la ressource.</span><span class="sxs-lookup"><span data-stu-id="1a880-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span></span> <span data-ttu-id="1a880-132">Le circuit sera essentiellement renommé.</span><span class="sxs-lookup"><span data-stu-id="1a880-132">The circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="1a880-133">Modifier l’accès d’un circuit</span><span class="sxs-lookup"><span data-stu-id="1a880-133">Modify circuit access</span></span>

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="1a880-134">Pour activer l’accès du circuit ExpressRoute pour les deux modèles de déploiement</span><span class="sxs-lookup"><span data-stu-id="1a880-134">To enable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="1a880-135">Après avoir déplacé votre circuit ExpressRoute classique vers le modèle de déploiement Resource Manager, vous pouvez activer l’accès aux deux modèles de déploiement.</span><span class="sxs-lookup"><span data-stu-id="1a880-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span></span> <span data-ttu-id="1a880-136">Exécutez les applets de commande suivantes pour activer l’accès aux deux modèles de déploiement :</span><span class="sxs-lookup"><span data-stu-id="1a880-136">Run the following cmdlets to enable access to both deployment models:</span></span>

1. <span data-ttu-id="1a880-137">Obtenez les informations sur le circuit.</span><span class="sxs-lookup"><span data-stu-id="1a880-137">Get the circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="1a880-138">Définissez « Autoriser les opérations classiques » sur TRUE.</span><span class="sxs-lookup"><span data-stu-id="1a880-138">Set "Allow Classic Operations" to TRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="1a880-139">Mettez à jour le circuit.</span><span class="sxs-lookup"><span data-stu-id="1a880-139">Update the circuit.</span></span> <span data-ttu-id="1a880-140">Une fois cette opération terminée avec succès, vous serez en mesure d’afficher le circuit dans le modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="1a880-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="1a880-141">Exécutez l’applet de commande suivante pour obtenir les informations concernant le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1a880-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span></span> <span data-ttu-id="1a880-142">Vous devez être en mesure de voir la clé de service répertoriée.</span><span class="sxs-lookup"><span data-stu-id="1a880-142">You must be able to see the service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="1a880-143">Vous pouvez maintenant gérer les liens au circuit ExpressRoute à l’aide des commandes du modèle de déploiement classique pour les réseaux virtuels classiques, et des commandes Resource Manager pour les réseaux virtuels Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1a880-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="1a880-144">Les articles suivants vous aident à gérer les liens vers le circuit ExpressRoute :</span><span class="sxs-lookup"><span data-stu-id="1a880-144">The following articles help you manage links to the ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="1a880-145">Liaison de réseaux virtuels à des circuits ExpressRoute dans le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1a880-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="1a880-146">Liaison de réseaux virtuels à des circuits ExpressRoute dans le modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="1a880-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a><span data-ttu-id="1a880-147">Pour désactiver l’accès du circuit ExpressRoute au modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="1a880-147">To disable ExpressRoute circuit access to the classic deployment model</span></span>

<span data-ttu-id="1a880-148">Exécutez les applets de commande suivantes pour désactiver l’accès au modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="1a880-148">Run the following cmdlets to disable access to the classic deployment model.</span></span>

1. <span data-ttu-id="1a880-149">Obtenez les informations concernant le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1a880-149">Get details of the ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="1a880-150">Définissez « Autoriser les opérations classiques » sur FALSE.</span><span class="sxs-lookup"><span data-stu-id="1a880-150">Set "Allow Classic Operations" to FALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="1a880-151">Mettez à jour le circuit.</span><span class="sxs-lookup"><span data-stu-id="1a880-151">Update the circuit.</span></span> <span data-ttu-id="1a880-152">Une fois cette opération terminée avec succès, vous ne serez pas en mesure d’afficher le circuit dans le modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="1a880-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="1a880-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a880-153">Next steps</span></span>

* [<span data-ttu-id="1a880-154">Créer et modifier le routage le routage pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1a880-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="1a880-155">Lier votre réseau virtuel à votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1a880-155">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)