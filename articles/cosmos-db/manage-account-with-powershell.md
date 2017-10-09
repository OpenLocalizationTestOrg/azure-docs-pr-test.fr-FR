---
title: "aaaAzure Cosmos Automation de base de données - gestion avec Powershell | Documents Microsoft"
description: "Utilisez Azure Powershell pour gérer vos comptes Azure Cosmos DB."
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 3239fb815918a0e47bff69fcd1ab6562519e429b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a>Créer un compte Azure Cosmos DB à l’aide de PowerShell

Hello guide suivant décrit la commandes tooautomate gestion de vos comptes de base de données de base de données Azure Cosmos à l’aide d’Azure Powershell. Il inclut également des clés de compte toomanage de commandes et les priorités de basculement dans [des comptes de base de données de plusieurs régions][scaling-globally]. Mise à jour de votre compte de base de données vous permet de stratégies de cohérence toomodify et ajouter/supprimer des régions. Pour la gestion de votre compte de base de données Azure Cosmos inter-plateformes, vous pouvez utiliser soit [CLI d’Azure](cli-samples.md), hello [API REST de fournisseur de ressources][rp-rest-api], ou hello [Azure portail](create-documentdb-dotnet.md#create-account).

## <a name="getting-started"></a>Mise en route

Suivez les instructions de hello dans [comment tooinstall et configurer Azure PowerShell] [ powershell-install-configure] tooinstall et vous connecter tooyour Azure Resource Manager compte dans Powershell.

### <a name="notes"></a>Remarques

* Si vous souhaitez que hello tooexecute suivant les commandes sans demander confirmation de l’utilisateur, ajouter hello `-Force` indicateur toohello commande.
* Tous les hello suivant les commandes sont synchrones.

## <a id="create-documentdb-account-powershell"></a> Créer un compte Azure Cosmos DB

Cette commande vous permet de toocreate un compte de base de données de base de données Azure Cosmos. Configurez votre nouveau compte de base de données pour une seule ou [plusieurs régions][scaling-globally] avec une [stratégie de cohérence](consistency-levels.md) déterminée.

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`nom de l’emplacement de hello Hello écrire la région du compte de base de données hello. Cet emplacement est requis toohave une valeur de priorité de basculement de 0. Il doit y avoir exactement une région d’écriture par compte de base de données.
* `<read-region-location>`nom de l’emplacement de hello Hello lire la région du compte de base de données hello. Cet emplacement est requis toohave une valeur de priorité de basculement supérieure à 0. Un compte de base de données peut présenter plusieurs régions de lecture.
* `<ip-range-filter>`Spécifie les ensemble de hello d’adresses IP ou des plages d’adresses IP dans toobe de forme CIDR inclus en tant que hello autorisée de la liste des adresses IP de client pour un compte de base de données spécifique. Les plages/adresses IP doivent être séparées par des virgules et ne doivent pas contenir d’espaces. Pour plus d’informations, consultez [Prise en charge du pare-feu dans Azure Cosmos DB](firewall-support.md).
* `<default-consistency-level>`niveau de cohérence Hello par défaut de hello compte de base de données Azure Cosmos. Pour plus d’informations, consultez [Niveaux de cohérence dans Azure Cosmos DB](consistency-levels.md).
* `<max-interval>`Lorsqu’il est utilisé avec une cohérence Bounded Staleness, cette valeur représente la quantité de temps hello de péremption (en secondes) au terme. Les valeurs acceptables sont comprises entre 1 et 100.
* `<max-staleness-prefix>`Lorsqu’il est utilisé avec une cohérence Bounded Staleness, cette valeur représente nombre hello de requêtes périmées tolérée. Les valeurs acceptables sont 1-2, 147, 483 et 647.
* `<resource-group-name>`nom Hello Hello [groupe de ressources Azure] [ azure-resource-groups] compte de base de données de base de données Azure Cosmos nouvelle toowhich hello appartient.
* `<resource-group-location>`emplacement Hello Hello compte de base de données nouvelle base de données Azure Cosmos de groupe de ressources Azure toowhich hello appartient.
* `<database-account-name>`nom de Hello de hello toobe du compte de base de données de base de données Azure Cosmos créé. Il peut uniquement utiliser des minuscules, nombres hello '-' caractère et doit être comprise entre 3 et 50 caractères.

Exemple : 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a>Remarques
* Hello exemple précédent crée un compte de base de données avec deux zones. Il est également possible de toocreate un compte de base de données avec une région (qui est désignée en tant que zone d’écriture hello et avoir une valeur de priorité de basculement de 0) ou plus de deux régions. Pour plus d’informations, consultez la section des [comptes de base de données multi-régions][scaling-globally].
* emplacements de Hello doivent être des régions dans lequel la base de données Azure Cosmos est généralement disponible. la liste actuelle des régions Hello est fournie sur hello [page des régions Azure](https://azure.microsoft.com/regions/#services).

## <a id="update-documentdb-account-powershell"></a> Mise à jour d’un compte de base de données DocumentDB

Cette commande vous permet de tooupdate vos propriétés de compte de base de données de base de données Azure Cosmos. Cela inclut la règle de cohérence hello et emplacements de hello quel compte de base de données hello existe dans.

> [!NOTE]
> Cette commande vous permet de régions tooadd et de suppression, mais ne vous autorise pas toomodify les priorités de basculement. toomodify les priorités de basculement, consultez [ci-dessous](#modify-failover-priority-powershell).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`nom de l’emplacement de hello Hello écrire la région du compte de base de données hello. Cet emplacement est requis toohave une valeur de priorité de basculement de 0. Il doit y avoir exactement une région d’écriture par compte de base de données.
* `<read-region-location>`nom de l’emplacement de hello Hello lire la région du compte de base de données hello. Cet emplacement est requis toohave une valeur de priorité de basculement supérieure à 0. Un compte de base de données peut présenter plusieurs régions de lecture.
* `<default-consistency-level>`niveau de cohérence Hello par défaut de hello compte de base de données Azure Cosmos. Pour plus d’informations, consultez [Niveaux de cohérence dans Azure Cosmos DB](consistency-levels.md).
* `<ip-range-filter>`Spécifie les ensemble de hello d’adresses IP ou des plages d’adresses IP dans toobe de forme CIDR inclus en tant que hello autorisée de la liste des adresses IP de client pour un compte de base de données spécifique. Les plages/adresses IP doivent être séparées par des virgules et ne doivent pas contenir d’espaces. Pour plus d’informations, consultez [Prise en charge du pare-feu dans Azure Cosmos DB](firewall-support.md).
* `<max-interval>`Lorsqu’il est utilisé avec une cohérence Bounded Staleness, cette valeur représente la quantité de temps hello de péremption (en secondes) au terme. Les valeurs acceptables sont comprises entre 1 et 100.
* `<max-staleness-prefix>`Lorsqu’il est utilisé avec une cohérence Bounded Staleness, cette valeur représente nombre hello de requêtes périmées tolérée. Les valeurs acceptables sont 1-2, 147, 483 et 647.
* `<resource-group-name>`nom Hello Hello [groupe de ressources Azure] [ azure-resource-groups] compte de base de données de base de données Azure Cosmos nouvelle toowhich hello appartient.
* `<resource-group-location>`emplacement Hello Hello compte de base de données nouvelle base de données Azure Cosmos de groupe de ressources Azure toowhich hello appartient.
* `<database-account-name>`nom de Hello de hello toobe du compte de base de données de base de données Azure Cosmos mis à jour.

Exemple : 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <a id="delete-documentdb-account-powershell"></a> Suppression d’un compte de base de données DocumentDB

Cette commande vous permet de toodelete un compte de base de données de base de données Azure Cosmos existant.

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* `<resource-group-name>`nom Hello Hello [groupe de ressources Azure] [ azure-resource-groups] compte de base de données de base de données Azure Cosmos nouvelle toowhich hello appartient.
* `<database-account-name>`nom de Hello de hello toobe du compte de base de données de base de données Azure Cosmos supprimé.

Exemple :

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a> Obtention des propriétés d’un compte de base de données DocumentDB

Cette commande vous permet de propriétés de hello tooget d’un compte de base de données de base de données Azure Cosmos existant.

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nom Hello Hello [groupe de ressources Azure] [ azure-resource-groups] compte de base de données de base de données Azure Cosmos nouvelle toowhich hello appartient.
* `<database-account-name>`nom Hello Hello compte de base de données de base de données Azure Cosmos.

Exemple :

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a> Mettre à jour les balises d’un compte de base de données Azure Cosmos DB

Hello exemple suivant décrit comment tooset [les balises de ressources Azure] [ azure-resource-tags] pour votre base de données Azure Cosmos compte base de données.

> [!NOTE]
> Cette commande peut être combinée avec hello créer ou mettre à jour des commandes en ajoutant hello `-Tags` indicateur avec le paramètre correspondant de hello.

Exemple :

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a> Liste des clés de comptes

Lorsque vous créez un compte de base de données Azure Cosmos, service de hello génère deux clés d’accès maître qui peuvent être utilisés pour l’authentification lors de l’accès hello compte de base de données Azure Cosmos. En fournissant deux clés d’accès, base de données Azure Cosmos vous permet de clés de hello tooregenerate avec aucune tooyour d’interruption du compte de base de données Azure Cosmos. Des clés en lecture seule pour l’authentification des opérations en lecture seule sont également disponibles. Il existe deux clés en lecture et écriture (primaire et secondaire) et deux clés en lecture seule (primaire et secondaire).

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nom Hello Hello [groupe de ressources Azure] [ azure-resource-groups] compte de base de données de base de données Azure Cosmos nouvelle toowhich hello appartient.
* `<database-account-name>`nom Hello Hello compte de base de données de base de données Azure Cosmos.

Exemple :

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a> Répertorier les chaînes de connexion

Pour les comptes de MongoDB, hello tooconnect de chaîne de connexion que votre compte de base de données MongoDB application toohello peut être récupérée à l’aide de hello commande suivante.

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nom Hello Hello [groupe de ressources Azure] [ azure-resource-groups] compte de base de données de base de données Azure Cosmos nouvelle toowhich hello appartient.
* `<database-account-name>`nom Hello Hello compte de base de données de base de données Azure Cosmos.

Exemple :

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a> Régénération de la clé de compte

Vous devez modifier le compte de base de données Azure Cosmos tooyour hello accès clés périodiquement toohelp renforcer vos connexions. Deux clés d’accès sont affectés tooenable connexions toomaintain vous toohello compte de base de données Azure Cosmos à l’aide d’une clé d’accès pendant la régénération de hello autre clé d’accès.

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* `<resource-group-name>`nom Hello Hello [groupe de ressources Azure] [ azure-resource-groups] compte de base de données de base de données Azure Cosmos nouvelle toowhich hello appartient.
* `<database-account-name>`nom Hello Hello compte de base de données de base de données Azure Cosmos.
* `<key-kind>`Un des types hello quatre de clés : [« Primaire » | » Secondaire « | » PrimaryReadonly « | » SecondaryReadonly »] que vous aimeriez tooregenerate.

Exemple :

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a> Modifier la priorité de basculement d’un compte de base de données Azure Cosmos DB

Pour les comptes de la base de données de plusieurs régions, vous pouvez modifier la priorité de basculement hello Hello différentes régions hello du compte de base de données de base de données Azure Cosmos existe dans. Pour plus d’informations sur le basculement dans votre compte de base de données Azure Cosmos DB, consultez la section [Azure Cosmos DB, un service de base de données mondialement distribué sur Azure][distribute-data-globally].

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* `<write-region-location>`nom de l’emplacement de hello Hello écrire la région du compte de base de données hello. Cet emplacement est requis toohave une valeur de priorité de basculement de 0. Il doit y avoir exactement une région d’écriture par compte de base de données.
* `<read-region-location>`nom de l’emplacement de hello Hello lire la région du compte de base de données hello. Cet emplacement est requis toohave une valeur de priorité de basculement supérieure à 0. Un compte de base de données peut présenter plusieurs régions de lecture.
* `<resource-group-name>`nom Hello Hello [groupe de ressources Azure] [ azure-resource-groups] compte de base de données de base de données Azure Cosmos nouvelle toowhich hello appartient.
* `<database-account-name>`nom Hello Hello compte de base de données de base de données Azure Cosmos.

Exemple :

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a>Étapes suivantes

* tooconnect à l’aide de .NET, consultez [se connecter et requête avec .NET](create-documentdb-dotnet.md).
* tooconnect à l’aide de .NET Core, consultez [se connecter et requête avec le .NET Core](create-documentdb-dotnet-core.md).
* tooconnect à l’aide de Node.js, consultez [se connecter et requête avec Node.js et une application MongoDB](create-mongodb-nodejs.md).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
