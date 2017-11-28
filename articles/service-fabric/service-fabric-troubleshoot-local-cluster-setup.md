---
title: "Dépanner votre configuration de cluster Service Fabric locale | Microsoft Docs"
description: "Cet article aborde un ensemble de suggestions relatives à la résolution des problèmes de votre cluster de développement local"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: aa393f884b564cee81fcf75cc2eff895efea9471
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="f6820-103">Résoudre les problèmes d'installation de votre cluster de développement local</span><span class="sxs-lookup"><span data-stu-id="f6820-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="f6820-104">Si vous rencontrez un problème en interagissant avec votre cluster de développement Azure Service Fabric local, examinez les suggestions suivantes de résolution.</span><span class="sxs-lookup"><span data-stu-id="f6820-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="f6820-105">Échecs de configuration du cluster</span><span class="sxs-lookup"><span data-stu-id="f6820-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="f6820-106">Impossible de nettoyer les journaux de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f6820-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="f6820-107">Problème</span><span class="sxs-lookup"><span data-stu-id="f6820-107">Problem</span></span>
<span data-ttu-id="f6820-108">Lors de l’exécution du script DevClusterSetup, une erreur de ce type peut s’afficher :</span><span class="sxs-lookup"><span data-stu-id="f6820-108">While running the DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="f6820-109">Solution</span><span class="sxs-lookup"><span data-stu-id="f6820-109">Solution</span></span>
<span data-ttu-id="f6820-110">Fermez la fenêtre PowerShell active et ouvrez une nouvelle fenêtre PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f6820-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="f6820-111">Vous devriez pouvoir exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="f6820-111">You should now be able to successfully run the script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="f6820-112">Échecs de connexion au cluster</span><span class="sxs-lookup"><span data-stu-id="f6820-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="f6820-113">Applets de commande PowerShell de Service Fabric non reconnues dans Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6820-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="f6820-114">Problème</span><span class="sxs-lookup"><span data-stu-id="f6820-114">Problem</span></span>
<span data-ttu-id="f6820-115">Si vous essayez d’exécuter l’une des applets de commande PowerShell de Service Fabric, par exemple `Connect-ServiceFabricCluster` , dans une fenêtre Azure PowerShell, l’applet de commande échoue avec un message indiquant qu’elle n’est pas reconnue.</span><span class="sxs-lookup"><span data-stu-id="f6820-115">If you try to run any of the Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that the cmdlet is not recognized.</span></span> <span data-ttu-id="f6820-116">Cela est dû au fait qu’Azure PowerShell utilise la version 32 bits de Windows PowerShell (même sur les versions 64 bits du système d’exploitation), tandis que les applets de commande Service Fabric fonctionnent uniquement dans des environnements 64 bits.</span><span class="sxs-lookup"><span data-stu-id="f6820-116">The reason for this is that Azure PowerShell uses the 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas the Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="f6820-117">Solution</span><span class="sxs-lookup"><span data-stu-id="f6820-117">Solution</span></span>
<span data-ttu-id="f6820-118">Exécutez toujours les applets de commande Service Fabric directement à partir de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6820-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="f6820-119">La dernière version d'Azure PowerShell ne crée aucun raccourci spécial, et cela ne devrait donc plus se reproduire.</span><span class="sxs-lookup"><span data-stu-id="f6820-119">The latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="f6820-120">Exception durant l’initialisation de type</span><span class="sxs-lookup"><span data-stu-id="f6820-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="f6820-121">Problème</span><span class="sxs-lookup"><span data-stu-id="f6820-121">Problem</span></span>
<span data-ttu-id="f6820-122">Quand vous êtes connecté au cluster dans PowerShell, l’erreur TypeInitializationException apparaît pour System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="f6820-122">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="f6820-123">Solution</span><span class="sxs-lookup"><span data-stu-id="f6820-123">Solution</span></span>
<span data-ttu-id="f6820-124">Votre variable PATH n’a pas été correctement définie durant l’installation.</span><span class="sxs-lookup"><span data-stu-id="f6820-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="f6820-125">Déconnectez-vous de Windows, puis reconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="f6820-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="f6820-126">Le chemin d’accès est alors actualisé.</span><span class="sxs-lookup"><span data-stu-id="f6820-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="f6820-127">La connexion au cluster est mise en échec avec une indication de fermeture de l’objet</span><span class="sxs-lookup"><span data-stu-id="f6820-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="f6820-128">Problème</span><span class="sxs-lookup"><span data-stu-id="f6820-128">Problem</span></span>
<span data-ttu-id="f6820-129">Un appel à Connect-ServiceFabricCluster est mis en échec avec une erreur de ce type :</span><span class="sxs-lookup"><span data-stu-id="f6820-129">A call to Connect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="f6820-130">Solution</span><span class="sxs-lookup"><span data-stu-id="f6820-130">Solution</span></span>
<span data-ttu-id="f6820-131">Fermez la fenêtre PowerShell active et ouvrez une nouvelle fenêtre PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f6820-131">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="f6820-132">Vous devez être maintenant en mesure de vous connecter.</span><span class="sxs-lookup"><span data-stu-id="f6820-132">You should now be able to successfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="f6820-133">Exception Connexion Fabric refusée</span><span class="sxs-lookup"><span data-stu-id="f6820-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="f6820-134">Problème</span><span class="sxs-lookup"><span data-stu-id="f6820-134">Problem</span></span>
<span data-ttu-id="f6820-135">Pendant le débogage à partir de Visual Studio, vous obtenez une erreur FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="f6820-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="f6820-136">Solution</span><span class="sxs-lookup"><span data-stu-id="f6820-136">Solution</span></span>
<span data-ttu-id="f6820-137">Cette erreur se produit généralement lorsque vous démarrez manuellement un processus hôte de service, sans recourir au runtime de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f6820-137">This error usually occurs when you try to start a service host process manually, rather than allowing the Service Fabric runtime to start it for you.</span></span>

<span data-ttu-id="f6820-138">Assurez-vous de ne pas disposer de projets de service définis en tant que projets de démarrage dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="f6820-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="f6820-139">Seuls les projets d’application Service Fabric doivent être définis en tant que projets de démarrage.</span><span class="sxs-lookup"><span data-stu-id="f6820-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="f6820-140">Si, après l’installation, votre cluster local commence à se comporter de manière anormale, vous pouvez le réinitialiser à l’aide de l’application de barre d’état système de gestionnaire de cluster local.</span><span class="sxs-lookup"><span data-stu-id="f6820-140">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span></span> <span data-ttu-id="f6820-141">Cela supprime le cluster existant et en installe un nouveau.</span><span class="sxs-lookup"><span data-stu-id="f6820-141">This removes the existing cluster and set up a new one.</span></span> <span data-ttu-id="f6820-142">Notez que toutes les applications déployées et les données associées sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="f6820-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f6820-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6820-143">Next steps</span></span>
* [<span data-ttu-id="f6820-144">Comprendre votre cluster et résoudre les problèmes à l’aide des rapports d’intégrité système</span><span class="sxs-lookup"><span data-stu-id="f6820-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="f6820-145">Visualiser votre cluster à l’aide de l’outil Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="f6820-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

