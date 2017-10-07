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
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a>Déplacer des circuits ExpressRoute à partir du modèle de déploiement de gestionnaire de ressources hello toohello classique à l’aide de PowerShell

toouse un circuit ExpressRoute pour hello classique et les modèles de déploiement de gestionnaire de ressources, vous devez déplacer le modèle de déploiement hello circuit toohello Gestionnaire de ressources. Hello sections suivantes vous aider à déplacer votre circuit à l’aide de PowerShell.

## <a name="before-you-begin"></a>Avant de commencer

* Vérifiez que vous disposez de version la plus récente des modules d’Azure PowerShell hello hello (au moins la version 1.0). Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
* Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflows](expressroute-workflows.md) avant de commencer la configuration.
* Passez en revue les informations hello qui sont fournies sous [déplacement d’un circuit ExpressRoute de tooResource classique Manager](expressroute-move.md). Assurez-vous de bien comprendre les limites de hello et limitations.
* Vérifiez que le circuit de hello est complètement opérationnel dans le modèle de déploiement classique hello.
* Assurez-vous que vous disposez d’un groupe de ressources qui a été créé dans le modèle de déploiement du Gestionnaire de ressources hello.

## <a name="move-an-expressroute-circuit"></a>Déplacer un circuit ExpressRoute

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a>Étape 1 : Collecter les détails du circuit de modèle de déploiement classique de hello

Connectez-vous à toohello environnement classique Azure et recueillir la clé du service hello.

1. Se connecter tooyour compte Azure.

  ```powershell
  Add-AzureAccount
  ```

2. Sélectionnez un abonnement Azure approprié de hello.

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. Importez les modules PowerShell hello pour Azure et ExpressRoute.

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. Utiliser l’applet de commande hello ci-dessous clés du service tooget hello pour toutes votre circuits ExpressRoute. Après la récupération des clés de hello, copiez hello **clé service** du circuit hello que vous souhaitez le modèle de déploiement du Gestionnaire de ressources toomove toohello.

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a>Étape 2 : connexion et création d’un groupe de ressources

Se connecter dans l’environnement du Gestionnaire de ressources toohello et créer un nouveau groupe de ressources.

1. Environnement de Azure Resource Manager tooyour vous connecter.

  ```powershell
  Login-AzureRmAccount
  ```

2. Sélectionnez un abonnement Azure approprié de hello.

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. Modifier l’extrait de code hello ci-dessous toocreate un groupe de ressources si vous n’avez pas déjà un groupe de ressources.

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a>Étape 3 : Déplacer le modèle de déploiement du circuit toohello Gestionnaire de ressources hello ExpressRoute

Vous est désormais prêt toomove votre circuit ExpressRoute à partir du modèle de déploiement du modèle toohello Gestionnaire de ressources hello déploiement classique. Avant de continuer, examinez les informations de hello fournies dans [déplacement d’un circuit ExpressRoute à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](expressroute-move.md).

toomove votre circuit, modifiez et exécutez hello suivant extrait de code :

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> Une fois hello déplacement terminée, hello nouveau nom qui est répertorié dans l’applet de commande précédente hello sera utilisé tooaddress hello ressource. circuit de Hello essentiellement sera renommé.
> 

## <a name="modify-circuit-access"></a>Modifier l’accès d’un circuit

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a>tooenable accès de circuit ExpressRoute pour les deux modèles de déploiement

Après le déplacement de votre modèle de déploiement Resource Manager classique ExpressRoute circuit toohello, vous pouvez activer l’accès au modèle de déploiement tooboth. Exécutez hello suivant d’applets de commande tooenable accéder aux modèles de déploiement tooboth :

1. Obtenir les détails du circuit hello.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Définissez « Autoriser les opérations classiques » tooTRUE.

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. Mettre à jour de circuit de hello. Une fois cette opération terminée avec succès, vous serez tooview en mesure de circuit de hello dans le modèle de déploiement classique hello.

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. Exécutez hello suivant applet de commande tooget hello détaille Hello circuit ExpressRoute. Vous devez être toosee en mesure de clé de service hello répertorié.

  ```powershell
  get-azurededicatedcircuit
  ```

5. Vous pouvez désormais gérer le circuit ExpressRoute de liens toohello à l’aide des commandes de modèle de déploiement classique de hello pour les réseaux virtuels classiques et les commandes de gestionnaire de ressources hello pour le Gestionnaire de ressources VNets. Hello articles suivants vous aider à gérer des liens toohello circuit ExpressRoute :

    * [Lier votre réseau virtuel de tooyour circuit ExpressRoute dans le modèle de déploiement du Gestionnaire de ressources hello](expressroute-howto-linkvnet-arm.md)
    * [Lier votre réseau virtuel de tooyour circuit ExpressRoute dans le modèle de déploiement classique de hello](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a>modèle de déploiement classique du circuit accès toohello toodisable ExpressRoute

Exécutez hello suivant le modèle de déploiement classique d’applets de commande toodisable accès toohello.

1. Obtenir les détails de hello circuit ExpressRoute.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Définissez « Autoriser les opérations classiques » tooFALSE.

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. Mettre à jour de circuit de hello. Une fois cette opération terminée avec succès, vous ne serez pas tooview en mesure de circuit de hello dans le modèle de déploiement classique hello.

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a>Étapes suivantes

* [Créer et modifier le routage le routage pour votre circuit ExpressRoute](expressroute-howto-routing-arm.md)
* [Lier votre réseau virtuel de tooyour circuit ExpressRoute](expressroute-howto-linkvnet-arm.md)
