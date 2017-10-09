---
title: aaaMove ressources Azure toonew abonnement ou groupe de ressources | Documents Microsoft
description: "Utilisez le Gestionnaire de ressources Azure toomove ressources tooa nouveau groupe de ressources ou d’un abonnement."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a>Déplacer le groupe de ressources toonew ressources ou d’un abonnement
Cette rubrique vous montre comment toomove ressources tooeither un nouvel abonnement ou une ressource de groupe Bonjour même abonnement. Vous pouvez utiliser le portail de hello, PowerShell, CLI d’Azure ou hello ressource de toomove API REST. les opérations de déplacement Hello dans cette rubrique sont disponible tooyou sans l’assistance du support technique Azure.

Lors du déplacement de ressources, les groupes de source de hello et hello cible sont verrouillés au cours de l’opération de hello. Écriture et suppression des opérations sont bloquées sur les groupes de ressources hello jusqu'à ce que le déplacement de hello se termine. Ce verrou signifie que vous ne peut pas ajouter, mettre à jour ou supprimer des ressources dans les groupes de ressources hello, mais cela ne signifie pas les ressources hello sont figées. Par exemple, si vous déplacez un serveur SQL Server et son groupe de ressources de base de données tooa, une application qui utilise la base de données hello ne rencontre aucune interruption de service. Il peut toujours lire et écrire des toohello de base de données.

Vous ne pouvez pas modifier l’emplacement hello de ressource de hello. Déplacement d’une ressource uniquement déplace tooa nouveau groupe de ressources. nouveau groupe de ressources Hello peut avoir un emplacement différent, mais qui ne modifie pas l’emplacement hello de ressource de hello.

> [!NOTE]
> Cet article décrit comment les ressources toomove dans Azure existant compte offres. Reportez-vous à votre compte Azure offre (par exemple, la mise à niveau à partir de paiement à l’utilisation de paie-toopre) tout en continuant toowork avec vos ressources existantes, si vous souhaitez réellement toochange [basculer votre offre de tooanother abonnement Azure](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Liste de contrôle avant le déplacement de ressources
Il existe certains tooperform étapes importantes avant de déplacer une ressource. Vérifiez ces conditions pour prévenir d'éventuelles erreurs.

1. Hello abonnements source et de destination doivent exister dans hello même [client Azure Active Directory](../active-directory/active-directory-howto-tenant.md). toocheck que les deux abonnements ont hello même ID de locataire, utilisez Azure PowerShell ou CLI d’Azure.

  Pour Azure PowerShell, utilisez :

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  Pour Azure CLI 2.0, utilisez :

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Si hello client ID pour les abonnements source et destination hello ne sont pas hello même, vous pouvez tenter de répertoire de hello toochange pour l’abonnement de hello. Toutefois, cette option est uniquement disponible tooService administrateurs qui se sont connectés avec un compte Microsoft (et non pas un compte d’organisation). tooattempt passage du répertoire hello, ouvrez une session toohello [portail classique](https://manage.windowsazure.com/), puis sélectionnez **paramètres**, puis sélectionnez l’abonnement de hello. Si hello **modifier l’annuaire** icône n’est disponible, sélectionnez-la toochange hello associé à Azure Active Directory.

  ![Modifier l’annuaire](./media/resource-group-move-resources/edit-directory.png)

  Si cette icône n’est pas disponible, vous devez contacter le support toomove hello ressources tooa nouveau client.

2. service de Hello doit activer les ressources de toomove de capacité hello. Cette rubrique répertorie les services permettant de déplacer des ressources et les services qui ne le permettent pas.
3. abonnement de destination Hello doit être inscrit pour le fournisseur de ressources hello de ressource hello en cours de déplacement. Si non, vous recevez un message d’erreur indiquant que hello **abonnement n’est pas inscrit pour un type de ressource**. Vous pouvez rencontrer ce problème lors du déplacement d’un abonnement tooa ressource, mais cet abonnement n’a jamais été utilisé avec ce type de ressource. toolearn toocheck hello l’état de l’inscription et inscrire des fournisseurs de ressources, voir [les types et les fournisseurs de ressources](resource-manager-supported-services.md).

## <a name="when-toocall-support"></a>Quand toocall prennent en charge
Vous pouvez déplacer la plupart des ressources via des opérations de libre-service hello présentées dans cette rubrique. Utilisez hello libre-service des opérations :

* Déplacer des ressources Resource Manager.
* Déplacer les ressources classiques selon toohello [limitations concernant le déploiement classique](#classic-deployment-limitations).

Appelez le support technique quand vous devez :

* Déplacez votre compte Azure tooa ressources (et le client Azure Active Directory).
* Déplacer les ressources classiques mais rencontrez des problèmes avec les limitations hello.

## <a name="services-that-enable-move"></a>Services permettant le déplacement
Pour l’instant, les services hello activez tooboth déplacer un groupe de ressources et l’abonnement sont :

* API Management
* Applications App Service (applications web) : consultez [Limitations d’App Service](#app-service-limitations)
* Application Insights
* Automatisation
* Batch
* Bing Maps
* CDN
* Cloud Services : consultez [Limitations relatives au déploiement Classic](#classic-deployment-limitations)
* Cognitive Services
* Content Moderator
* Data Catalog
* Data Factory
* Data Lake Analytics
* Data Lake Store
* DNS
* Azure Cosmos DB
* Event Hubs
* Clusters HDInsight - voir [Limitations de HDInsight](#hdinsight-limitations)
* IoT Hubs
* Key Vault
* Équilibreurs de charge
* Logic Apps
* Apprentissage automatique
* Media Services
* Mobile Engagement
* Notification Hubs
* Operational Insights
* Operations Management
* Power BI
* Cache Redis
* Scheduler
* Search
* Gestion de serveur
* Service Bus
* Service Fabric
* Storage
* Storage (classique) : consultez [Limitations relatives au déploiement classique](#classic-deployment-limitations)
* Stream Analytics - Les tâches Stream Analytics ne peuvent pas être déplacées lorsqu’elles sont en cours d’exécution.
* Serveur de base de données SQL - hello base de données et le serveur doivent résider dans hello même groupe de ressources. Lorsque vous déplacez un serveur SQL, toutes ses bases de données sont également déplacées.
* Traffic Manager
* Machines virtuelles
* Machines virtuelles avec un certificat stocké dans le coffre de clés - déplacer le groupe ressource toonew dans le même abonnement est activé, mais abonnement croisée déplacement n’est pas activé.
* Virtual Machines (classique) : consultez [Limitations relatives au déploiement classique](#classic-deployment-limitations)
* Jeux de mise à l’échelle de machine virtuelle
* Réseaux virtuels : actuellement, un réseau virtuel homologué ne peut pas être déplacé tant que l’homologation de réseau virtuel est activée. Une fois désactivée, hello réseau virtuel peut être déplacé correctement et d’homologation de réseau virtuel hello peut être activée. En outre, un réseau virtuel ne peut pas être déplacé tooa autre abonnement si hello réseau virtuel contient un sous-réseau avec des liens de navigation de ressources. Par exemple, un sous-réseau de réseau virtuel dispose d’un lien de navigation dans les ressources lorsqu’une ressource Microsoft.Cache redis est déployée dans ce sous-réseau.
* Passerelle VPN


## <a name="services-that-do-not-enable-move"></a>Services qui ne permettent pas le déplacement
services Hello actuellement n’activent pas le déplacement d’une ressource sont :

* Services de domaine AD
* Service de contrôle d’intégrité hybride Active Directory
* Application Gateway
* Groupes à haute disponibilité comprenant des machines virtuelles avec des disques gérés
* BizTalk Services
* Service de conteneur
* ExpressRoute
* DevTest Labs - déplacer le groupe ressource toonew dans le même abonnement est activé, mais la déplacer de l’abonnement n’est pas activé.
* Dynamics LCS
* Images créées à partir de disques gérés
* Managed Disks
* Applications gérées
* Coffre de Services de récupération - également pas déplacement hello calcul, réseau et stockage de ressources associés à font hello Services de récupération de coffre, consultez [limitations de Services de récupération](#recovery-services-limitations).
* Sécurité
* Instantanés créés à partir de disques gérés
* StorSimple Device Manager
* Machines virtuelles avec des disques managés
* Réseaux virtuels (classique) : consultez [Limitations relatives au déploiement classique](#classic-deployment-limitations)
* Les machines virtuelles créées à partir de ressources de la Place de marché ne peuvent pas être déplacées entre des abonnements. Besoins en ressources toobe a été annulé dans l’abonnement actif de hello et déployé à nouveau dans un nouvel abonnement hello

## <a name="app-service-limitations"></a>limitations d’App Service
Lorsque vous travaillez avec des applications App Service, vous ne pouvez pas déplacer uniquement un plan App Service. applications de Service d’applications toomove, les options disponibles sont :

* Déplacez hello plan App Service et toutes les autres ressources du Service d’applications dans cette ressource groupe tooa nouveau groupe de ressources qui ne possède pas les ressources du Service d’applications. Cette exigence signifie que vous devez déplacer même hello les ressources du Service d’applications qui ne sont pas associés avec hello plan App Service.
* Déplacer le groupe de ressources différent tooa hello applications, en conservant tous les plans de Service d’applications dans le groupe de ressources d’origine hello.

Hello du Service d’applications plan n’a pas besoin tooreside dans hello même groupe de ressources en tant qu’application hello pour hello application toofunction correctement.

Par exemple, si votre groupe de ressources contient :

* **web-a**, qui est associé à **plan-a**
* **web-b**, qui est associé à **plan-b**

Vos options sont :

* Déplacer **web-a**, **plan-a**, **web-b** et **plan-b**
* Déplacer **web-a** et **web-b**
* Déplacez **web-a**
* Déplacez **web-b**

Toutes les autres combinaisons impliquent l’abandon d’un type de ressource qui ne peut pas être abandonné lors du déplacement d’un plan App Service (n’importe quel type de ressource App Service).

Si votre application web réside dans un autre groupe de ressources que son plan de Service d’applications, mais que vous souhaitez toomove les deux tooa nouveau groupe de ressources, vous devez effectuer le déplacement de hello en deux étapes. Par exemple :

* **web-a** se trouve dans **web-group**
* **plan-a** se trouve dans **plan-group**
* Vous souhaitez **a web** et **un plan** tooreside dans **groupe combinés**

tooaccomplish ce déplacement, effectuer deux opérations distinctes de déplacement Bonjour suivant séquence :

1. Déplacer hello **a web** trop**groupe de plan**
2. Déplacer **a web** et **un plan** trop**groupe combinés**.

Vous pouvez déplacer un certificat de Service d’application tooa nouveau groupe de ressources ou d’un abonnement sans problème. Toutefois, si votre application web inclut un certificat SSL que vous acheté en externe et téléchargé toohello application, vous devez supprimer le certificat hello avant l’application web mobile hello. Par exemple, vous pouvez effectuer hello comme suit :

1. Supprimer hello téléchargé certificat hello web app
2. Déplacez l’application hello web
3. Télécharger l’application hello certificat toohello web

## <a name="recovery-services-limitations"></a>Limitations de Recovery Services
Déplacement n’est pas activé pour le stockage, réseau, ou les ressources de calcul utilisé tooset la récupération d’urgence avec Azure Site Recovery.

Par exemple, supposons que vous avez configuré la réplication de votre compte de stockage local machines tooa (Storage1) et souhaitez hello protégé machine toocome des après basculement tooAzure comme un ordinateur virtuel (VM1) attaché tooa de réseau virtuel (Network1). Vous ne pouvez pas déplacer ces ressources Azure - Storage1, VM1, et Network1 - ressources entre les groupes de hello même abonnement ou entre plusieurs abonnements.

## <a name="hdinsight-limitations"></a>Limitations de HDInsight

Vous pouvez déplacer HDInsight clusters tooa nouvel abonnement ou groupe de ressources. Toutefois, vous ne pouvez pas déplacer entre hello abonnements mise en réseau de cluster de HDInsight ressources toohello lié (par exemple, le réseau virtuel de hello, carte réseau ou d’équilibrage de charge). En outre, vous ne pouvez pas déplacer tooa nouveau groupe de ressources une carte réseau qui est la machine virtuelle jointe tooa cluster de hello.

Lorsque vous déplacez un HDInsight cluster tooa nouvel abonnement, commencez par déplacer autres ressources (telles que le compte de stockage hello). Déplacez ensuite le cluster HDInsight de hello par lui-même.

## <a name="classic-deployment-limitations"></a>Limitations relatives au déploiement Classic
Hello options de déplacement des ressources déployées via le modèle classique de hello diffèrent selon que vous déplacez des ressources hello au sein d’un abonnement ou tooa nouveau.

### <a name="same-subscription"></a>Même abonnement
Déplacement de ressources à partir d’un groupe tooanother groupe de ressources au sein de hello même abonnement, hello suivant des restrictions s’appliquent lorsque :

* Les réseaux virtuels (classiques) ne peuvent pas être déplacés.
* Machines virtuelles (classiques) doivent être déplacées avec le service cloud hello.
* Service de cloud computing peut uniquement être déplacé lorsque hello déplacement inclut tous ses ordinateurs virtuels.
* Un seul service cloud peut être déplacé à la fois.
* Un seul compte de stockage (classique) peut être déplacé à la fois.
* Compte de stockage (classiques) ne peut pas être déplacé dans hello même opération avec un ordinateur virtuel ou un service cloud.

toomove les ressources classiques tooa nouveau groupe de ressources dans hello même abonnement, utilisez des opérations de déplacement standard hello via hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [CLI d’Azure](#use-azure-cli), ou [API REST](#use-rest-api). Vous utilisez hello les mêmes opérations que vous utilisez pour le déplacement de ressources du Gestionnaire de ressources.

### <a name="new-subscription"></a>Nouvel abonnement
Lors du déplacement des ressources tooa un nouvel abonnement, hello suivant des restrictions s’appliquent :

* Toutes les ressources classiques dans l’abonnement de hello doivent être déplacées dans hello même opération.
* abonnement de Hello cible ne doit pas contenir d’autres ressources classiques.
* déplacement de Hello ne peut être demandée via une API REST distincts pour les déplacements classiques. commandes de déplacement de gestionnaire de ressources standard Hello ne fonctionnent pas lorsque vous déplacez les ressources classiques tooa un nouvel abonnement.

toomove les ressources classiques tooa nouvel abonnement, utilisez hello reste des opérations qui sont des ressources de tooclassic spécifique. toouse REST, effectuez hello comme suit :

1. Vérifiez si l’abonnement source hello peut participer à un abonnement de la déplacer. Utilisez hello l’opération suivante :

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     Dans le corps de la demande hello, sont les suivantes :

  ```json
  {
    "role": "source"
  }
  ```

     réponse Hello pour l’opération de validation hello est Bonjour suivant le format :

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Vérifiez si l’abonnement de destination hello peut participer à un abonnement de la déplacer. Utilisez hello l’opération suivante :

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     Dans le corps de la demande hello, sont les suivantes :

  ```json
  {
    "role": "target"
  }
  ```

     réponse de Hello est au même format que la validation d’abonnement source hello de hello.
3. Si les deux abonnements ont été validés, déplacez toutes les ressources classiques de l’abonnement de tooanother un abonnement avec hello l’opération suivante :

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    Dans le corps de la demande hello, sont les suivantes :

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

opération de Hello peut-être s’exécuter pendant plusieurs minutes.

## <a name="use-portal"></a>Utilisation du portail
ressources de toomove, sélectionnez le groupe de ressources hello contenant ces ressources, puis sélectionnez hello **déplacer** bouton.

![Déplacer des ressources](./media/resource-group-move-resources/select-move.png)

Indiquez si vous déplacez hello ressources tooa nouveau groupe de ressources ou d’un nouvel abonnement.

Sélectionnez hello ressources toomove et le groupe de ressources de destination hello. Confirmer que vous devez tooupdate scripts pour ces ressources sélectionnez **OK**. Si vous avez sélectionné l’icône d’abonnement hello modifier à l’étape précédente de hello, vous devez également sélectionner l’abonnement de destination hello.

![Sélectionner la destination](./media/resource-group-move-resources/select-destination.png)

Dans **Notifications**, vous voyez que hello déplacer l’opération est en cours d’exécution.

![afficher l’état du déplacement](./media/resource-group-move-resources/show-status.png)

Lorsqu’il a terminé, vous êtes averti du résultat de hello.

![afficher les résultats du déplacement](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>Utiliser PowerShell
toomove existant groupe de ressources tooanother ressources ou d’un abonnement, utilisez hello `Move-AzureRmResource` commande.

Hello le premier exemple montre comment toomove qu’une seule ressource tooa nouveau groupe de ressources.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

Hello deuxième exemple montre comment toomove plusieurs ressources tooa nouveau groupe de ressources.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

toomove tooa nouvel abonnement, incluez une valeur pour hello `DestinationSubscriptionId` paramètre.

Vous êtes invité tooconfirm que vous souhaitez toomove hello les ressources spécifiées.

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Utiliser Azure CLI 2.0
toomove existant groupe de ressources tooanother ressources ou d’un abonnement, utilisez hello `az resource move` commande. Fournir des ressources d’hello ID de hello ressources toomove. Vous pouvez obtenir l’ID de ressource par hello de commande suivante :

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

Bonjour à l’exemple suivant montre comment toomove un stockage compte tooa nouveau groupe de ressources. Bonjour `--ids` paramètre, fournir une liste séparée par des espaces de hello ressource ID toomove.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

toomove tooa nouvel abonnement, fournissez hello `--destination-subscription-id` paramètre.

## <a name="use-azure-cli-10"></a>Utiliser Azure CLI 1.0
toomove existant groupe de ressources tooanother ressources ou d’un abonnement, utilisez hello `azure resource move` commande. Fournir des ressources d’hello ID de hello ressources toomove. Vous pouvez obtenir l’ID de ressource par hello de commande suivante :

```azurecli
azure resource list -g sourceGroup --json
```

Qui renvoie hello suivant le format :

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

Bonjour à l’exemple suivant montre comment toomove un stockage compte tooa nouveau groupe de ressources. Bonjour `-i` paramètre, fournir une liste séparée par des virgules de hello ressource ID toomove.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

Vous êtes invité tooconfirm que vous souhaitez toomove hello de la ressource spécifiée.

## <a name="use-rest-api"></a>Avec l’API REST
groupe de ressources de tooanother ressources toomove existant ou d’un abonnement, exécutez :

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

Dans le corps de la demande hello, vous spécifiez le groupe de ressources cible hello et hello ressources toomove. Pour plus d’informations sur l’opération de déplacement de REST hello, consultez [déplacer des ressources](https://msdn.microsoft.com/library/azure/mt218710.aspx).

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur les applets de commande PowerShell pour gérer votre abonnement, consultez [à l’aide de Azure PowerShell avec le Gestionnaire de ressources](powershell-azure-resource-manager.md).
* toolearn sur les commandes CLI d’Azure pour gérer votre abonnement, consultez [Using hello CLI d’Azure avec le Gestionnaire de ressources](xplat-cli-azure-resource-manager.md).
* toolearn sur les fonctionnalités du portail de gestion de votre abonnement, consultez [à l’aide des ressources de toomanage portail Azure hello](resource-group-portal.md).
* toolearn sur l’application d’une ressource tooyour organisation logique, consultez [à l’aide des balises tooorganize vos ressources](resource-group-using-tags.md).
