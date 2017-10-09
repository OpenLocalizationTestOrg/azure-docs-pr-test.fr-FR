---
title: "aaaAzure chaîne de connexion de Service Fabric image store | Documents Microsoft"
description: "Comprendre la chaîne de connexion de magasin hello image"
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: 
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: alexwun
ms.openlocfilehash: 83f5ad75b5df07726997da3173722028255b8cae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-imagestoreconnectionstring-setting"></a>Comprendre le paramètre de ImageStoreConnectionString hello

Dans certains notre documentation, nous mentionner existence hello d’un paramètre « ImageStoreConnectionString » sans décrivant ce que cela signifie réellement. Et après avoir effectué un article comme [déployer et supprimer des applications à l’aide de PowerShell][10], il semble que tout ce que vous faire est de copier/coller hello valeur tel qu’il apparaît dans le manifeste du cluster hello de cible de hello cluster. Paramètre de hello doivent donc être configurable par cluster, mais lorsque vous créez un cluster via hello [portail Azure][11], il n’existe aucune option de tooconfigure ce paramètre et ses toujours « fabric : images ». À quoi sert hello de ce paramètre ?

![Manifeste de cluster][img_cm]

Service Fabric commencé en tant que plateforme de consommation internes de Microsoft en de nombreuses équipes divers, pour certains aspects de celui-ci sont hautement personnalisables : hello « Image Store » est un aspect de ce type. Essentiellement, hello Image Store est un référentiel enfichable pour stocker les packages d’application. Lorsque votre application est un nœud tooa déployé dans un cluster de hello, ce nœud télécharge contenu hello de votre package d’application à partir de hello magasin d’images. Hello ImageStoreConnectionString est un paramètre qui inclut toutes les informations nécessaires hello pour les clients et les nœuds toofind hello correct magasin d’images pour un cluster donné.

Il existe actuellement trois genres possibles de fournisseurs de magasins d’images ; les chaînes de connexion correspondantes sont les suivantes :

1. Service de magasin d’images : « fabric:ImageStore »

2. Système de fichiers : « file:[chemin d’accès du système de fichiers] »

3. Stockage Azure : « xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...] »

type de fournisseur Hello utilisé en production est hello Service Banque d’Image, qui est un service système persistants avec état que vous pouvez voir à partir de Service Fabric Explorer. 

![Service de magasin d’images][img_is]

Hébergement hello magasin d’images dans un service système cluster hello lui-même élimine les dépendances externes pour le référentiel de packages hello et nous permet de mieux contrôler la localité hello de stockage. Futures améliorations autour hello magasin d’images sont tout d’abord, fournisseur de magasin d’images hello tootarget probable si ce n’est pas exclusivement. chaîne de connexion Hello pour le fournisseur de Service de magasin d’images hello ne contient aucune information unique, car le client de hello est déjà connecté toohello cible cluster. client de Hello doit uniquement tooknow que les protocoles ciblant le service système hello doivent être utilisés.

fournisseur de système de fichiers Hello est utilisée au lieu de hello Service Banque d’Image pour local une case clusters durant cluster de développement toobootstrap hello légèrement plus rapide. différence de Hello est généralement faible, mais il s’agit d’une optimisation utile pour la plupart des gens pendant le développement. Son possible toodeploy une zone locale un cluster avec hello d’autres types de fournisseurs de stockage ainsi, mais il est généralement inutile toodo par conséquent, étant donné que le reste du flux de travail de développement/test hello hello même quel que soit le fournisseur. Que cette utilisation, des fournisseurs de système de fichiers et de stockage Azure hello existent uniquement pour la prise en charge héritée.

Par conséquent, tandis que hello ImageStoreConnectionString est configurable, vous en général simplement utilisez hello paramètre par défaut. Lors de la publication tooAzure via [Visual Studio][12], hello est automatiquement affectée pour vous en conséquence. Pour un déploiement par programmation les tooclusters hébergés dans Azure, chaîne de connexion hello est toujours « fabric : images ». Bien que, en cas de doute, sa valeur peut toujours être vérifiée par la récupération du manifeste du cluster hello par [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), ou [reste](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest). De test à la fois localement et clusters de production doivent toujours être fournisseur de Service de magasin d’images hello toouse configuré ainsi.

### <a name="next-steps"></a>Étapes suivantes
[Déployer et supprimer des applications avec PowerShell][10]

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
