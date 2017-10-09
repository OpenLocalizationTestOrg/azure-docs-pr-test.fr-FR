---
title: "aaaVisualizing votre cluster à l’aide du Service Fabric Explorer | Documents Microsoft"
description: "Service Fabric Explorer est un outil web dédié à l’inspection et à la gestion des applications cloud et des nœuds dans un cluster Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a>Visualiser votre cluster à l’aide de l’outil Service Fabric Explorer
Service Fabric Explorer est un outil web dédié à l’inspection et à la gestion d’applications et de nœuds dans un cluster Azure Service Fabric. Service Fabric Explorer est hébergé directement dans le cluster de hello, elle est toujours disponible, quel que soit l’où votre cluster est en cours d’exécution.

## <a name="video-tutorial"></a>Didacticiel vidéo

toolearn comment toouse Service Fabric Explorer, regardez hello suivant vidéo de Microsoft Virtual Academy :

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a>Se connecter tooService Fabric Explorer
Si vous avez suivi les instructions hello trop[préparer votre environnement de développement](service-fabric-get-started.md), vous pouvez lancer le Service Fabric Explorer votre cluster local en naviguant toohttp://localhost:19080 / Explorer.

## <a name="understand-hello-service-fabric-explorer-layout"></a>Comprendre la mise en page du Service Fabric Explorer hello
Vous pouvez naviguer dans le Service Fabric Explorer à l’aide d’arborescence de hello sur hello gauche. À la racine de hello d’arborescence de hello, tableau de bord hello cluster fournit une vue d’ensemble de votre cluster, y compris un résumé de l’application et d’intégrité de nœud.

![Tableau de bord de cluster de Service Fabric Explorer][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a>Afficher la mise en page du cluster hello
Les nœuds dans un cluster Service Fabric sont répartis dans une grille à deux dimensions composée de domaines d’erreur et de domaines de mise à niveau. Ce positionnement garantit que vos applications restent disponibles en présence de hello de mises à niveau de l’application et des défaillances matérielles. Vous pouvez afficher la façon dont le cluster actuel hello est disposé à l’aide de carte de cluster hello.

![Mappage de cluster de Service Fabric Explorer][sfx-cluster-map]

### <a name="view-applications-and-services"></a>Afficher les applications et les services
cluster de Hello contient deux sous-arborescences : une pour les applications et un autre pour les nœuds.

Vous pouvez utiliser hello application vue toonavigate via la hiérarchie logique de l’architecture de Service : applications, services, partitions et réplicas.

Dans l’exemple hello ci-dessous, hello application **MyApp** se compose de deux services, **MyStatefulService** et **WebService**. Étant donné que **MyStatefulService** est une application avec état, elle inclut une partition avec un réplica principal et deux réplicas secondaires. En revanche, WebSvcService est une application sans état qui ne contient qu’une seule instance.

![Affichage des applications de Service Fabric Explorer][sfx-application-tree]

À chaque niveau de l’arborescence de hello, volet principal de hello affiche des informations pertinentes sur l’élément de hello. Par exemple, vous pouvez voir l’état d’intégrité hello et version pour un service particulier.

![Volet des éléments essentiels de Service Fabric Explorer][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a>Afficher les nœuds du cluster hello
affichage du nœud Hello montre la disposition physique de hello du cluster de hello. Vous pouvez identifier les applications ayant déployé du code sur un nœud donné. Plus particulièrement, vous pouvez voir les réplicas en cours d’exécution sur ce nœud.

## <a name="actions"></a>Actions
Service Fabric Explorer offre un moyen rapide de tooinvoke actions sur les nœuds, les applications et services au sein de votre cluster.

Par exemple, toodelete une instance d’application, choisissez application hello à partir de l’arborescence hello sur hello gauche, puis **Actions** > **supprimer l’Application**.

![Suppression d’une application dans Service Fabric Explorer][sfx-delete-application]

> [!TIP]
> Vous pouvez effectuer hello les mêmes actions en cliquant sur élément tooeach suivant de hello points de suspension.
>
>

Hello tableau suivant répertorie les actions de hello disponibles pour chaque entité :

| **Entité** | **Action** | **Description** |
| --- | --- | --- |
| Type d’application |Type de mise hors service |Supprime le package d’application hello à partir du magasin d’images du cluster hello. Nécessite toutes les applications de ce toobe type supprimé en premier. |
| Application |Supprimer l’application |Supprimer l’application hello, y compris tous ses services et leur état (le cas échéant). |
| Service |Supprimer le service |Supprimer le service de hello et son état (le cas échéant). |
| Nœud |Activer |Activer le nœud de hello. |
| Nœud | Désactiver (pause) | Suspendre le nœud hello dans son état actuel. Services continuent toorun mais Service Fabric ne déplace pas les proactive quoi que ce soit sur ou déconnecter, sauf si elle est requise tooprevent une panne ou une incohérence des données. Cette action est généralement utilisé tooenable tooensure un nœud spécifique qui elles ne déplacent pas lors de l’inspection, les services de débogage. | |
| Nœud | Désactiver (redémarrage) | Déplace en toute sécurité tous les services en mémoire d’un nœud et ferme les services persistants. Généralement utilisé lorsque le processus hôte de hello ou ordinateur besoin toobe redémarré. | |
| Nœud | Désactiver (suppression de données) | En toute sécurité, fermez tous les services en cours d’exécution sur le nœud de hello après la génération de réplicas de rechange suffisantes. Généralement utilisé quand un nœud (ou au moins son stockage) est définitivement mis hors service. | |
| Nœud | Supprimer l’état du nœud | Supprimer les connaissances de réplicas d’un nœud du cluster de hello. Généralement utilisé quand un nœud déjà défaillant est considéré comme irrécupérable. | |
| Nœud | Redémarrer | Simuler un échec de nœud en redémarrant le nœud de hello. Plus d’informations [ici](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps) | |

Étant donné que de nombreuses actions sont destructeurs, vous pouvez être invité tooconfirm votre intention avant hello action est terminée.

> [!TIP]
> Toutes les actions qui peuvent être effectuées via l’Explorateur de l’infrastructure de Service peuvent également être effectuée via PowerShell ou une API REST, tooenable automation.
>
>

Vous pouvez également utiliser des instances de l’application Service Fabric Explorer toocreate pour un type d’application donné et une version. Choisissez le type d’application hello dans l’arborescence de hello, puis cliquez sur hello **créer une instance application** version toohello suivante de liaison souhaité dans le volet de droite hello.

![Création d’une instance application dans Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> Les instances d’application créées via le Service Fabric Explorer ne peuvent actuellement pas être paramétrées. Elles sont créées à l’aide des valeurs de paramètre par défaut.
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a>Se connecter à distance des clusters Service Fabric tooa
Si vous connaissez le point de terminaison du cluster hello et que vous disposez des autorisations suffisantes, vous pouvez accéder Service Fabric Explorer à partir de n’importe quel navigateur. Il s’agit, car le Service Fabric Explorer est simplement un autre service qui s’exécute dans un cluster de hello.

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a>Découvrir le point de terminaison de Service Fabric Explorer hello pour un cluster à distance
tooreach Service Fabric Explorer pour un cluster donné, pointez votre navigateur sur :

http://&lt;point-de-terminaison-de-votre-cluster&gt;:19080/Explorer

Pour les clusters Azure, une URL complète hello est également disponible dans hello cluster essentials volet Hello portail Azure.

### <a name="connect-tooa-secure-cluster"></a>Connecter le cluster sécurisée de tooa
Vous pouvez contrôler le cluster Service Fabric tooyour client d’accès avec des certificats ou à l’aide d’Azure Active Directory (AAD).

Si vous essayez de tooconnect tooService Fabric Explorer sur un cluster sécurisé, puis en fonction de la configuration du cluster hello vous envisagez toopresent requis un certificat client ou connectez-vous à l’aide d’AAD.

## <a name="next-steps"></a>Étapes suivantes
* [Vue d’ensemble de la testabilité](service-fabric-testability-overview.md)
* [Gestion de vos applications Service Fabric dans Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Déploiement d’application Service Fabrix à l’aide de PowerShell](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
