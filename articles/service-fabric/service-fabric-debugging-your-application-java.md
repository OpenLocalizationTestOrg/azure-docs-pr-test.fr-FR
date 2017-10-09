---
title: aaaDebug votre Application Azure Service Fabric dans Eclipse | Documents Microsoft
description: "Améliorer la fiabilité de hello et les performances de vos services en développant et en leur débogage dans Eclipse sur un cluster de développement local."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a>Débogage de votre application Java Service Fabric avec Eclipse
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
> 

1. Démarrer un cluster de développement local en suivant les étapes de hello dans [configuration de votre environnement de développement Service Fabric](service-fabric-get-started-linux.md).

2. Mettre à jour entryPoint.sh du service de hello vous souhaitez toodebug, pour qu’il démarre le processus de java hello avec les paramètres de débogage à distance. Ce fichier se trouve à l’emplacement suivant de hello : ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``. Le port 8001 est défini pour le débogage dans cet exemple.

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. Mettre à jour hello manifeste d’Application en définissant le nombre d’instances hello ou hello nombre de réplicas pour le service de hello qui est en cours de débogage too1. Ce paramètre évite les conflits de port hello qui est utilisé pour le débogage. Par exemple, pour les services sans état, définissez ``InstanceCount="1"`` et pour les services avec état ensemble hello min et la cible d’ensemble de réplicas tailles too1 comme suit : `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.

4. Déployer l’application hello.

5. Bonjour IDE Eclipse, sélectionnez **exécuter -> Configurations de débogage -> Application Java distante et les propriétés de connexion d’entrée** et définissez les propriétés de hello comme suit :

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  Définir des points d’arrêt au niveau des points de votre choisis et déboguer l’application hello.

Si l’application hello est en panne, vous pouvez également tooenable coredumps. Exécutez ``ulimit -c`` dans un interpréteur de commandes et si elle renvoie la valeur 0, les vidages de la mémoire de travail ne sont pas activés. tooenable coredumps illimités, exécutez hello de commande suivante : ``ulimit -c unlimited``. Vous pouvez également vérifier le statut de hello à l’aide de la commande hello ``ulimit -a``.  Si vous souhaitez que le chemin d’accès de tooupdate hello coredump génération, exécutez ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``. 

### <a name="next-steps"></a>Étapes suivantes

* [Collecter les journaux avec Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).
* [Surveiller et diagnostiquer les services localement](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).
