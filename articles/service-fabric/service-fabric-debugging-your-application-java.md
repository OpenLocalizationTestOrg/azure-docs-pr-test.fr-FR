---
title: "Débogage de votre application Azure Service Fabric dans Eclipse | Microsoft Docs"
description: "Améliorez la fiabilité et les performances de vos services en les développant et en procédant à leur débogage dans Eclipse sur un cluster de développement local."
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
ms.openlocfilehash: f3bcee3794de35005bd387ecfae7e6707f3cb5ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="269ac-103">Débogage de votre application Java Service Fabric avec Eclipse</span><span class="sxs-lookup"><span data-stu-id="269ac-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="269ac-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="269ac-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="269ac-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="269ac-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="269ac-106">Démarrez un cluster de développement local en suivant les étapes de la section [Configuration de votre environnement de développement Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="269ac-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="269ac-107">Mettez à jour entryPoint.sh du service que vous souhaitez déboguer, afin qu’il démarre le processus java avec les paramètres de débogage à distance.</span><span class="sxs-lookup"><span data-stu-id="269ac-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span></span> <span data-ttu-id="269ac-108">Ce fichier se trouve à l’emplacement suivant : ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="269ac-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="269ac-109">Le port 8001 est défini pour le débogage dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="269ac-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="269ac-110">Mettez à jour le manifeste de l’application en définissant le nombre d’instances ou le nombre de réplicas pour le service en cours de débogage sur 1.</span><span class="sxs-lookup"><span data-stu-id="269ac-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span></span> <span data-ttu-id="269ac-111">Ce paramètre évite les conflits pour le port utilisé pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="269ac-111">This setting avoids conflicts for the port that is used for debugging.</span></span> <span data-ttu-id="269ac-112">Par exemple, pour les services sans état, définissez ``InstanceCount="1"`` et pour les services avec état, définissez les tailles cible et de jeu de réplicas minimales sur 1 comme suit : `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="269ac-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="269ac-113">Déployez l’application.</span><span class="sxs-lookup"><span data-stu-id="269ac-113">Deploy the application.</span></span>

5. <span data-ttu-id="269ac-114">Dans l’IDE Eclipse, sélectionnez **Exécuter-> Déboguer des Configurations-> Application Java distante et entrez les propriétés de connexion**, puis définissez les propriétés comme suit :</span><span class="sxs-lookup"><span data-stu-id="269ac-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="269ac-115">Définissez des points d’arrêt sur les points de votre choix et déboguez l’application.</span><span class="sxs-lookup"><span data-stu-id="269ac-115">Set breakpoints at desired points and debug the application.</span></span>

<span data-ttu-id="269ac-116">Si l’application se bloque, vous pouvez également activer le vidage de la mémoire de travail.</span><span class="sxs-lookup"><span data-stu-id="269ac-116">If the application is crashing, you may also want to enable coredumps.</span></span> <span data-ttu-id="269ac-117">Exécutez ``ulimit -c`` dans un interpréteur de commandes et si elle renvoie la valeur 0, les vidages de la mémoire de travail ne sont pas activés.</span><span class="sxs-lookup"><span data-stu-id="269ac-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="269ac-118">Pour activer un nombre illimité de vidages de la mémoire de travail, exécutez la commande suivante : ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="269ac-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="269ac-119">Vous pouvez également vérifier l’état à l’aide de la commande ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="269ac-119">You can also verify the status using the command ``ulimit -a``.</span></span>  <span data-ttu-id="269ac-120">Si vous souhaitez mettre à jour le chemin d’accès de la génération des vidages de la mémoire de travail, exécutez ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="269ac-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="269ac-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="269ac-121">Next steps</span></span>

* <span data-ttu-id="269ac-122">[Collecter les journaux avec Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="269ac-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="269ac-123">[Surveiller et diagnostiquer les services localement](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="269ac-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
