---
title: "Déplacer des circuits ExpressRoute de tooResource classique Manager : PowerShell : Azure | Documents Microsoft"
description: "Cette page décrit comment toomove un toohello circuit classic déploiement du Gestionnaire de ressources du modèle à l’aide de PowerShell."
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
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="c0cce-103">Déplacer des circuits ExpressRoute à partir du modèle de déploiement de gestionnaire de ressources hello toohello classique à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0cce-103">Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="c0cce-104">toouse un circuit ExpressRoute pour hello classique et les modèles de déploiement de gestionnaire de ressources, vous devez déplacer le modèle de déploiement hello circuit toohello Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="c0cce-104">toouse an ExpressRoute circuit for both hello classic and Resource Manager deployment models, you must move hello circuit toohello Resource Manager deployment model.</span></span> <span data-ttu-id="c0cce-105">Hello sections suivantes vous aider à déplacer votre circuit à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c0cce-105">hello following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c0cce-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c0cce-106">Before you begin</span></span>

* <span data-ttu-id="c0cce-107">Vérifiez que vous disposez de version la plus récente des modules d’Azure PowerShell hello hello (au moins la version 1.0).</span><span class="sxs-lookup"><span data-stu-id="c0cce-107">Verify that you have hello latest version of hello Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="c0cce-108">Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c0cce-108">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="c0cce-109">Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="c0cce-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="c0cce-110">Passez en revue les informations hello qui sont fournies sous [déplacement d’un circuit ExpressRoute de tooResource classique Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="c0cce-110">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="c0cce-111">Assurez-vous de bien comprendre les limites de hello et limitations.</span><span class="sxs-lookup"><span data-stu-id="c0cce-111">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="c0cce-112">Vérifiez que le circuit de hello est complètement opérationnel dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-112">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="c0cce-113">Assurez-vous que vous disposez d’un groupe de ressources qui a été créé dans le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-113">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="c0cce-114">Déplacer un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c0cce-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a><span data-ttu-id="c0cce-115">Étape 1 : Collecter les détails du circuit de modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="c0cce-115">Step 1: Gather circuit details from hello classic deployment model</span></span>

<span data-ttu-id="c0cce-116">Connectez-vous à toohello environnement classique Azure et recueillir la clé du service hello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-116">Sign in toohello Azure classic environment and gather hello service key.</span></span>

1. <span data-ttu-id="c0cce-117">Se connecter tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="c0cce-117">Sign in tooyour Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="c0cce-118">Sélectionnez un abonnement Azure approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-118">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="c0cce-119">Importez les modules PowerShell hello pour Azure et ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c0cce-119">Import hello PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="c0cce-120">Utiliser l’applet de commande hello ci-dessous clés du service tooget hello pour toutes votre circuits ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c0cce-120">Use hello cmdlet below tooget hello service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="c0cce-121">Après la récupération des clés de hello, copiez hello **clé service** du circuit hello que vous souhaitez le modèle de déploiement du Gestionnaire de ressources toomove toohello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-121">After retrieving hello keys, copy hello **service key** of hello circuit that you want toomove toohello Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="c0cce-122">Étape 2 : connexion et création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="c0cce-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="c0cce-123">Se connecter dans l’environnement du Gestionnaire de ressources toohello et créer un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c0cce-123">Sign in toohello Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="c0cce-124">Environnement de Azure Resource Manager tooyour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="c0cce-124">Sign in tooyour Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="c0cce-125">Sélectionnez un abonnement Azure approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-125">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="c0cce-126">Modifier l’extrait de code hello ci-dessous toocreate un groupe de ressources si vous n’avez pas déjà un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c0cce-126">Modify hello snippet below toocreate a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a><span data-ttu-id="c0cce-127">Étape 3 : Déplacer le modèle de déploiement du circuit toohello Gestionnaire de ressources hello ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c0cce-127">Step 3: Move hello ExpressRoute circuit toohello Resource Manager deployment model</span></span>

<span data-ttu-id="c0cce-128">Vous est désormais prêt toomove votre circuit ExpressRoute à partir du modèle de déploiement du modèle toohello Gestionnaire de ressources hello déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="c0cce-128">You are now ready toomove your ExpressRoute circuit from hello classic deployment model toohello Resource Manager deployment model.</span></span> <span data-ttu-id="c0cce-129">Avant de continuer, examinez les informations de hello fournies dans [déplacement d’un circuit ExpressRoute à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="c0cce-129">Before proceeding, review hello information provided in [Moving an ExpressRoute circuit from hello classic toohello Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="c0cce-130">toomove votre circuit, modifiez et exécutez hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="c0cce-130">toomove your circuit, modify and run hello following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="c0cce-131">Une fois hello déplacement terminée, hello nouveau nom qui est répertorié dans l’applet de commande précédente hello sera utilisé tooaddress hello ressource.</span><span class="sxs-lookup"><span data-stu-id="c0cce-131">After hello move has finished, hello new name that is listed in hello previous cmdlet will be used tooaddress hello resource.</span></span> <span data-ttu-id="c0cce-132">circuit de Hello essentiellement sera renommé.</span><span class="sxs-lookup"><span data-stu-id="c0cce-132">hello circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="c0cce-133">Modifier l’accès d’un circuit</span><span class="sxs-lookup"><span data-stu-id="c0cce-133">Modify circuit access</span></span>

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="c0cce-134">tooenable accès de circuit ExpressRoute pour les deux modèles de déploiement</span><span class="sxs-lookup"><span data-stu-id="c0cce-134">tooenable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="c0cce-135">Après le déplacement de votre modèle de déploiement Resource Manager classique ExpressRoute circuit toohello, vous pouvez activer l’accès au modèle de déploiement tooboth.</span><span class="sxs-lookup"><span data-stu-id="c0cce-135">After moving your classic ExpressRoute circuit toohello Resource Manager deployment model, you can enable access tooboth deployment models.</span></span> <span data-ttu-id="c0cce-136">Exécutez hello suivant d’applets de commande tooenable accéder aux modèles de déploiement tooboth :</span><span class="sxs-lookup"><span data-stu-id="c0cce-136">Run hello following cmdlets tooenable access tooboth deployment models:</span></span>

1. <span data-ttu-id="c0cce-137">Obtenir les détails du circuit hello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-137">Get hello circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="c0cce-138">Définissez « Autoriser les opérations classiques » tooTRUE.</span><span class="sxs-lookup"><span data-stu-id="c0cce-138">Set "Allow Classic Operations" tooTRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="c0cce-139">Mettre à jour de circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-139">Update hello circuit.</span></span> <span data-ttu-id="c0cce-140">Une fois cette opération terminée avec succès, vous serez tooview en mesure de circuit de hello dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-140">After this operation has finished successfully, you will be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="c0cce-141">Exécutez hello suivant applet de commande tooget hello détaille Hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c0cce-141">Run hello following cmdlet tooget hello details of hello ExpressRoute circuit.</span></span> <span data-ttu-id="c0cce-142">Vous devez être toosee en mesure de clé de service hello répertorié.</span><span class="sxs-lookup"><span data-stu-id="c0cce-142">You must be able toosee hello service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="c0cce-143">Vous pouvez désormais gérer le circuit ExpressRoute de liens toohello à l’aide des commandes de modèle de déploiement classique de hello pour les réseaux virtuels classiques et les commandes de gestionnaire de ressources hello pour le Gestionnaire de ressources VNets.</span><span class="sxs-lookup"><span data-stu-id="c0cce-143">You can now manage links toohello ExpressRoute circuit using hello classic deployment model commands for classic VNets, and hello Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="c0cce-144">Hello articles suivants vous aider à gérer des liens toohello circuit ExpressRoute :</span><span class="sxs-lookup"><span data-stu-id="c0cce-144">hello following articles help you manage links toohello ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="c0cce-145">Lier votre réseau virtuel de tooyour circuit ExpressRoute dans le modèle de déploiement du Gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="c0cce-145">Link your virtual network tooyour ExpressRoute circuit in hello Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="c0cce-146">Lier votre réseau virtuel de tooyour circuit ExpressRoute dans le modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="c0cce-146">Link your virtual network tooyour ExpressRoute circuit in hello classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a><span data-ttu-id="c0cce-147">modèle de déploiement classique du circuit accès toohello toodisable ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c0cce-147">toodisable ExpressRoute circuit access toohello classic deployment model</span></span>

<span data-ttu-id="c0cce-148">Exécutez hello suivant le modèle de déploiement classique d’applets de commande toodisable accès toohello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-148">Run hello following cmdlets toodisable access toohello classic deployment model.</span></span>

1. <span data-ttu-id="c0cce-149">Obtenir les détails de hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c0cce-149">Get details of hello ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="c0cce-150">Définissez « Autoriser les opérations classiques » tooFALSE.</span><span class="sxs-lookup"><span data-stu-id="c0cce-150">Set "Allow Classic Operations" tooFALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="c0cce-151">Mettre à jour de circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-151">Update hello circuit.</span></span> <span data-ttu-id="c0cce-152">Une fois cette opération terminée avec succès, vous ne serez pas tooview en mesure de circuit de hello dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="c0cce-152">After this operation has finished successfully, you will not be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="c0cce-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0cce-153">Next steps</span></span>

* [<span data-ttu-id="c0cce-154">Créer et modifier le routage le routage pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c0cce-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="c0cce-155">Lier votre réseau virtuel de tooyour circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c0cce-155">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
