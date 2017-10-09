---
title: "aaaDefinine et gérer l’état dans Azure microservices | Documents Microsoft"
description: "Comment toodefine et gérer l’état de service dans le Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a>État du service
**État de service** fait référence toohello en mémoire ou sur des données de disque qu’un service nécessite toofunction. Il contient, par exemple, les structures de données hello et les variables de membre que le service hello lit et écrit toodo travail. Selon l’architecture de service de hello, elle peut aussi inclure des fichiers ou autres ressources qui sont stockés sur le disque. Par exemple, hello fichiers à une base de données utiliserait toostore des journaux de transaction et de données.

Prenons l’exemple d’une calculatrice. Un service de calculatrice de base accepte deux nombres et retourne leur somme. Ce calcul n’implique aucune variable membre ni aucune autre information.

Examinons à présent hello calculatrice même, mais avec une méthode supplémentaire pour le stockage et de retourner la somme de dernière hello, elle est calculée. Il s’agit à présent d’un service avec état, Avec état signifie qu’il contient un certain état qu’il écrit toowhen il calcule une somme de nouveau et lit lorsque vous aurez besoin somme calculée de tooreturn hello dernière.

Dans Azure Service Fabric, le premier service de hello est appelée un service sans état. service de deuxième Hello est appelé un service avec état.

## <a name="storing-service-state"></a>Stockage de l’état du service
État permettre être externalisé ou colocalisé avec le code hello qui manipule les état hello. L’externalisation d’état est généralement effectuée à l’aide d’une base de données externe ou stocker d’autres données que s’exécute sur le réseau de hello ou en dehors du processus sur des ordinateurs différents hello le même ordinateur. Dans notre exemple de calculatrice, magasin de données hello peut être une base de données SQL ou d’une instance de magasin de tables Azure. Chaque somme de hello toocompute demande effectue une mise à jour sur ces données et demandes toohello service tooreturn hello valeur de résultat dans la valeur actuelle de hello lue à partir du magasin de hello. 

État peut également être colocalisé avec le code hello qui manipule hello état. Les services avec état de Service Fabric sont majoritairement générés suivant ce modèle. Service Fabric fournit hello infrastructure tooensure que cet état est hautement disponible, cohérent et durable, et que les services hello conçus de cette façon peuvent évoluer facilement.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les concepts de l’infrastructure de Service, consultez hello suivant des articles :

* [Disponibilité des services Service Fabric](service-fabric-availability-services.md)
* [Extensibilité des services Service Fabric](service-fabric-concepts-scalability.md)
* [Partitionnement des services Service Fabric](service-fabric-concepts-partitioning.md)
* [Modèle Reliable Services de Service Fabric](service-fabric-reliable-services-introduction.md)
