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
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="b709e-103">Débogage de votre application Java Service Fabric avec Eclipse</span><span class="sxs-lookup"><span data-stu-id="b709e-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b709e-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="b709e-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="b709e-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="b709e-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="b709e-106">Démarrer un cluster de développement local en suivant les étapes de hello dans [configuration de votre environnement de développement Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b709e-106">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="b709e-107">Mettre à jour entryPoint.sh du service de hello vous souhaitez toodebug, pour qu’il démarre le processus de java hello avec les paramètres de débogage à distance.</span><span class="sxs-lookup"><span data-stu-id="b709e-107">Update entryPoint.sh of hello service you wish toodebug, so that it starts hello java process with remote debug parameters.</span></span> <span data-ttu-id="b709e-108">Ce fichier se trouve à l’emplacement suivant de hello : ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="b709e-108">This file can be found at hello following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="b709e-109">Le port 8001 est défini pour le débogage dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="b709e-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="b709e-110">Mettre à jour hello manifeste d’Application en définissant le nombre d’instances hello ou hello nombre de réplicas pour le service de hello qui est en cours de débogage too1.</span><span class="sxs-lookup"><span data-stu-id="b709e-110">Update hello Application Manifest by setting hello instance count or hello replica count for hello service that is being debugged too1.</span></span> <span data-ttu-id="b709e-111">Ce paramètre évite les conflits de port hello qui est utilisé pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="b709e-111">This setting avoids conflicts for hello port that is used for debugging.</span></span> <span data-ttu-id="b709e-112">Par exemple, pour les services sans état, définissez ``InstanceCount="1"`` et pour les services avec état ensemble hello min et la cible d’ensemble de réplicas tailles too1 comme suit : `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="b709e-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set hello target and min replica set sizes too1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="b709e-113">Déployer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b709e-113">Deploy hello application.</span></span>

5. <span data-ttu-id="b709e-114">Bonjour IDE Eclipse, sélectionnez **exécuter -> Configurations de débogage -> Application Java distante et les propriétés de connexion d’entrée** et définissez les propriétés de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b709e-114">In hello Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set hello properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="b709e-115">Définir des points d’arrêt au niveau des points de votre choisis et déboguer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b709e-115">Set breakpoints at desired points and debug hello application.</span></span>

<span data-ttu-id="b709e-116">Si l’application hello est en panne, vous pouvez également tooenable coredumps.</span><span class="sxs-lookup"><span data-stu-id="b709e-116">If hello application is crashing, you may also want tooenable coredumps.</span></span> <span data-ttu-id="b709e-117">Exécutez ``ulimit -c`` dans un interpréteur de commandes et si elle renvoie la valeur 0, les vidages de la mémoire de travail ne sont pas activés.</span><span class="sxs-lookup"><span data-stu-id="b709e-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="b709e-118">tooenable coredumps illimités, exécutez hello de commande suivante : ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="b709e-118">tooenable unlimited coredumps, execute hello following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="b709e-119">Vous pouvez également vérifier le statut de hello à l’aide de la commande hello ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="b709e-119">You can also verify hello status using hello command ``ulimit -a``.</span></span>  <span data-ttu-id="b709e-120">Si vous souhaitez que le chemin d’accès de tooupdate hello coredump génération, exécutez ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="b709e-120">If you wanted tooupdate hello coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="b709e-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b709e-121">Next steps</span></span>

* <span data-ttu-id="b709e-122">[Collecter les journaux avec Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="b709e-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="b709e-123">[Surveiller et diagnostiquer les services localement](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b709e-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
