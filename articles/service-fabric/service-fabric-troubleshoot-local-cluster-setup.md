---
title: aaaTroubleshoot votre configuration du cluster Service Fabric locale | Documents Microsoft
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
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="ef875-103">Résoudre les problèmes d'installation de votre cluster de développement local</span><span class="sxs-lookup"><span data-stu-id="ef875-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="ef875-104">Si vous rencontrez un problème lors de l’interaction avec votre cluster de développement local Azure Service Fabric, passez en revue hello suivant des suggestions pour les solutions possibles.</span><span class="sxs-lookup"><span data-stu-id="ef875-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review hello following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="ef875-105">Échecs de configuration du cluster</span><span class="sxs-lookup"><span data-stu-id="ef875-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="ef875-106">Impossible de nettoyer les journaux de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ef875-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="ef875-107">Problème</span><span class="sxs-lookup"><span data-stu-id="ef875-107">Problem</span></span>
<span data-ttu-id="ef875-108">Lorsque vous exécutez le script de DevClusterSetup hello, vous voyez ce type d’erreur :</span><span class="sxs-lookup"><span data-stu-id="ef875-108">While running hello DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="ef875-109">Solution</span><span class="sxs-lookup"><span data-stu-id="ef875-109">Solution</span></span>
<span data-ttu-id="ef875-110">Fermez hello fenêtre actuelle de PowerShell et ouvrir une nouvelle fenêtre PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ef875-110">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="ef875-111">Vous devez maintenant être en mesure de toosuccessfully exécuter le script de hello.</span><span class="sxs-lookup"><span data-stu-id="ef875-111">You should now be able toosuccessfully run hello script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="ef875-112">Échecs de connexion au cluster</span><span class="sxs-lookup"><span data-stu-id="ef875-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="ef875-113">Applets de commande PowerShell de Service Fabric non reconnues dans Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef875-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="ef875-114">Problème</span><span class="sxs-lookup"><span data-stu-id="ef875-114">Problem</span></span>
<span data-ttu-id="ef875-115">Si vous essayez toorun des hello applets de commande PowerShell de l’infrastructure de Service, tel que `Connect-ServiceFabricCluster` dans une fenêtre Azure PowerShell, il échoue, indiquant que cette applet de commande hello n’est pas reconnu.</span><span class="sxs-lookup"><span data-stu-id="ef875-115">If you try toorun any of hello Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that hello cmdlet is not recognized.</span></span> <span data-ttu-id="ef875-116">Hello fait que Azure PowerShell utilise hello 32 bits de Windows PowerShell (même sur les versions de système d’exploitation 64 bits), alors que hello applets de commande Service Fabric fonctionnent uniquement dans les environnements 64 bits.</span><span class="sxs-lookup"><span data-stu-id="ef875-116">hello reason for this is that Azure PowerShell uses hello 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas hello Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="ef875-117">Solution</span><span class="sxs-lookup"><span data-stu-id="ef875-117">Solution</span></span>
<span data-ttu-id="ef875-118">Exécutez toujours les applets de commande Service Fabric directement à partir de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef875-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="ef875-119">version la plus récente d’Azure PowerShell Hello ne crée pas un raccourci spécial, donc cela ne devrait plus apparaître.</span><span class="sxs-lookup"><span data-stu-id="ef875-119">hello latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="ef875-120">Exception durant l’initialisation de type</span><span class="sxs-lookup"><span data-stu-id="ef875-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="ef875-121">Problème</span><span class="sxs-lookup"><span data-stu-id="ef875-121">Problem</span></span>
<span data-ttu-id="ef875-122">Lorsque vous vous connectez le cluster toohello dans PowerShell, vous voyez l’erreur hello TypeInitializationException pour System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="ef875-122">When you are connecting toohello cluster in PowerShell, you see hello error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="ef875-123">Solution</span><span class="sxs-lookup"><span data-stu-id="ef875-123">Solution</span></span>
<span data-ttu-id="ef875-124">Votre variable PATH n’a pas été correctement définie durant l’installation.</span><span class="sxs-lookup"><span data-stu-id="ef875-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="ef875-125">Déconnectez-vous de Windows, puis reconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="ef875-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="ef875-126">Le chemin d’accès est alors actualisé.</span><span class="sxs-lookup"><span data-stu-id="ef875-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="ef875-127">La connexion au cluster est mise en échec avec une indication de fermeture de l’objet</span><span class="sxs-lookup"><span data-stu-id="ef875-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="ef875-128">Problème</span><span class="sxs-lookup"><span data-stu-id="ef875-128">Problem</span></span>
<span data-ttu-id="ef875-129">Un appel tooConnect-ServiceFabricCluster échoue avec une erreur comme suit :</span><span class="sxs-lookup"><span data-stu-id="ef875-129">A call tooConnect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="ef875-130">Solution</span><span class="sxs-lookup"><span data-stu-id="ef875-130">Solution</span></span>
<span data-ttu-id="ef875-131">Fermez hello fenêtre actuelle de PowerShell et ouvrir une nouvelle fenêtre PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ef875-131">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="ef875-132">Vous devez maintenant être en mesure de se connecter de toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="ef875-132">You should now be able toosuccessfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="ef875-133">Exception Connexion Fabric refusée</span><span class="sxs-lookup"><span data-stu-id="ef875-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="ef875-134">Problème</span><span class="sxs-lookup"><span data-stu-id="ef875-134">Problem</span></span>
<span data-ttu-id="ef875-135">Pendant le débogage à partir de Visual Studio, vous obtenez une erreur FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="ef875-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="ef875-136">Solution</span><span class="sxs-lookup"><span data-stu-id="ef875-136">Solution</span></span>
<span data-ttu-id="ef875-137">Cette erreur se produit généralement lorsque vous essayez de toostart un processus hôte de service manuellement, au lieu de laisser toostart de runtime Service Fabric hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="ef875-137">This error usually occurs when you try toostart a service host process manually, rather than allowing hello Service Fabric runtime toostart it for you.</span></span>

<span data-ttu-id="ef875-138">Assurez-vous de ne pas disposer de projets de service définis en tant que projets de démarrage dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="ef875-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="ef875-139">Seuls les projets d’application Service Fabric doivent être définis en tant que projets de démarrage.</span><span class="sxs-lookup"><span data-stu-id="ef875-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="ef875-140">Si, après l’installation, votre cluster local commence toobehave anormalement, vous pouvez réinitialiser à l’aide d’application de barre d’état système hello cluster local manager.</span><span class="sxs-lookup"><span data-stu-id="ef875-140">If, following setup, your local cluster begins toobehave abnormally, you can reset it using hello local cluster manager system tray application.</span></span> <span data-ttu-id="ef875-141">Cette supprime hello cluster existant et configurer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="ef875-141">This removes hello existing cluster and set up a new one.</span></span> <span data-ttu-id="ef875-142">Notez que toutes les applications déployées et les données associées sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="ef875-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ef875-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef875-143">Next steps</span></span>
* [<span data-ttu-id="ef875-144">Comprendre votre cluster et résoudre les problèmes à l’aide des rapports d’intégrité système</span><span class="sxs-lookup"><span data-stu-id="ef875-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="ef875-145">Visualiser votre cluster à l’aide de l’outil Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="ef875-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

