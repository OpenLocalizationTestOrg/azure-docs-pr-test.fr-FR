---
title: "Sécurité d’un cluster Service Fabric : rôles clients | Microsoft Docs"
description: "Cet article décrit les deux rôles de client hello et autorisations hello fournies toohello rôles."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4a4a9f93e91ea816005b730bebbcb317f8bab255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a>Contrôle d’accès en fonction du rôle pour les clients de Service Fabric
Azure Service Fabric prend en charge deux types de contrôle d’accès différents pour les clients qui sont connectés tooa Service Fabric clusters : administrateur et utilisateur. Contrôle d’accès permet de cluster administrateur toolimit toocertain cluster opérations d’accès pour différents groupes d’utilisateurs, la sécurisation de cluster de hello hello.  

**Les administrateurs** ont un accès complet des fonctionnalités toomanagement (y compris les fonctionnalités en lecture/écriture). Par défaut, **utilisateurs** uniquement avoir un accès en lecture toomanagement fonctionnalités (par exemple, les fonctions de requête) et des applications de tooresolve hello capacité et des services.

Vous spécifiez les rôles de client hello deux (administrateur et client) lors de la création du cluster hello en fournissant des certificats pour chacun. Pour plus d’informations sur la configuration d’un cluster Service Fabric sécurisé, consultez [Sécurité d’un cluster Service Fabric](service-fabric-cluster-security.md) .

## <a name="default-access-control-settings"></a>Paramètres de contrôle d'accès par défaut
type de contrôle d’accès administrateur Hello a hello de tooall d’un accès complet FabricClient APIs. Il peut effectuer toutes les lectures et les écritures sur le cluster Service Fabric de hello, y compris hello opérations suivantes :

### <a name="application-and-service-operations"></a>Opérations de service et d'application
* **CreateService**: création du service                             
* **CreateServiceFromTemplate**: création du service à partir d’un modèle                             
* **UpdateService**: mises à jour du service                             
* **DeleteService**: suppression du service                             
* **ProvisionApplicationType**: approvisionnement du type d’application                             
* **CreateApplication**: création d’application                               
* **DeleteApplication**: suppression d’application                             
* **UpgradeApplication**: démarrage ou interruption des mises à niveau de l’application                             
* **UnprovisionApplicationType**: désapprovisionnement du type d’application                             
* **MoveNextUpgradeDomain**: reprise des mises à niveau de l’application avec un domaine de mise à jour explicite                             
* **ReportUpgradeHealth**: la reprise des mises à niveau de l’application avec la progression de mise à niveau en cours hello                             
* **ReportHealth**: création de rapports d'intégrité                             
* **PredeployPackageToNode**: API de prédéploiement                            
* **CodePackageControl**: redémarrage des packages de code                             
* **RecoverPartition**: récupération d’une partition                             
* **RecoverPartitions**: récupération de partitions                             
* **RecoverServicePartitions**: récupération des partitions d’un service                             
* **RecoverSystemPartitions**: récupération des partitions d’un service système                             

### <a name="cluster-operations"></a>Opérations de cluster
* **ProvisionFabric**: approvisionnement du manifeste de cluster et/ou MSI                             
* **UpgradeFabric**: démarrage des mises à niveau du cluster                             
* **UnprovisionFabric**: désapprovisionnement du manifeste de cluster et/ou MSI                         
* **MoveNextFabricUpgradeDomain**: reprise des mises à niveau du cluster avec un domaine de mise à jour explicite                             
* **ReportFabricUpgradeHealth**: la reprise des mises à niveau de cluster avec hello actuelle mise à niveau de progression                             
* **StartInfrastructureTask**: démarrage des tâches d’infrastructure                             
* **FinishInfrastructureTask**: fin des tâches d’infrastructure                             
* **InvokeInfrastructureCommand**: commandes de gestion des tâches d’infrastructure                              
* **ActivateNode**: activation d’un nœud                             
* **DeactivateNode**: désactivation d’un nœud                             
* **DeactivateNodesBatch**: désactivation de plusieurs nœuds                             
* **RemoveNodeDeactivations**: annulation de la désactivation de plusieurs nœuds                             
* **GetNodeDeactivationStatus**: vérification de l’état de désactivation                             
* **NodeStateRemoved**: suppression du rapport d’état du nœud                             
* **ReportFault**: erreur de création de rapport                             
* **FileContent**: transfert de fichiers client magasin (toocluster externe) de l’image                             
* **FileDownload**: image store client fichier téléchargement initiation (toocluster externe)                             
* **InternalList**: opération de liste de fichier client de magasin d’image (interne)                             
* **Delete**: opération de suppression de client de magasin d’image                              
* **Upload**: opération de téléchargement de client de magasin d’image                             
* **NodeControl**: démarrage, arrêt et redémarrage des nœuds                             
* **MoveReplicaControl**: déplacement des réplicas à partir d’un nœud tooanother                             

### <a name="miscellaneous-operations"></a>Opérations diverses
* **Ping**: commandes ping client                             
* **Query**: toutes les requêtes autorisées
* **NameExists**: contrôles de présence de l’URI de dénomination                             

par défaut, Hello type de contrôle d’accès utilisateur est limitée toohello opérations suivantes : 

* **EnumerateSubnames**: énumération de l’URI de dénomination                             
* **EnumerateProperties**: énumération des propriétés de dénomination                             
* **PropertyReadBatch**: opérations de lecture des propriétés de dénomination                             
* **GetServiceDescription**: lecture des descriptions de service et notifications de sondage de longue durée                             
* **ResolveService**: résolution de service basée sur plainte                             
* **ResolveNameOwner**: résolution du propriétaire de l’URI de dénomination                             
* **ResolvePartition**: résolution des services système                             
* **ServiceNotifications**: notifications de service basées sur des événements                             
* **GetUpgradeStatus**: interrogation de l’état de mise à niveau de l’application                             
* **GetFabricUpgradeStatus**: interrogation de l’état de mise à niveau du cluster                             
* **InvokeInfrastructureQuery**: interrogation des tâches d’infrastructure                             
* **List**: opération de liste de fichier client de magasin d’image                             
* **ResetPartitionLoad**: réinitialisation de chargement pour une unité de basculement                             
* **ToggleVerboseServicePlacementHealthReporting**: basculement des rapports d’intégrité sur le placement de service détaillé                             

contrôle d’accès administrateur Hello a également toohello accès les opérations précédentes.

## <a name="changing-default-settings-for-client-roles"></a>Modification des paramètres par défaut des rôles clients
Dans le fichier de manifeste du cluster de hello, vous pouvez fournir client d’administration fonctionnalités toohello si nécessaire. Vous pouvez modifier les valeurs par défaut hello en va de toohello **les paramètres de l’ensemble fibre optique** option pendant [création d’un cluster](service-fabric-cluster-creation-via-portal.md)et en fournissant hello précédents paramètres Bonjour **nom**, **admin**, **utilisateur**, et **valeur** champs.

## <a name="next-steps"></a>Étapes suivantes
[Sécurité d’un cluster Service Fabric](service-fabric-cluster-security.md)

[Création d’un cluster Service Fabric](service-fabric-cluster-creation-via-portal.md)

