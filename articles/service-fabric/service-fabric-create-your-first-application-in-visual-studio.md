---
title: aaaCreate un service fiable Azure Service Fabric avec c#
description: "Créer, déployer et déboguer une application Reliable Service basée sur Azure Service Fabric avec Visual Studio."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="4cd33-103">Création de votre première application de services fiables avec état c# Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4cd33-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="4cd33-104">Découvrez comment toodeploy votre première application de Service Fabric pour .NET sur Windows dans quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4cd33-104">Learn how toodeploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="4cd33-105">Une fois l’opération terminée, vous obtenez un cluster local fonctionnant avec une application de service fiable.</span><span class="sxs-lookup"><span data-stu-id="4cd33-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4cd33-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4cd33-106">Prerequisites</span></span>

<span data-ttu-id="4cd33-107">Avant de commencer, assurez-vous que vous avez bien [configuré votre environnement de développement](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4cd33-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="4cd33-108">Cela inclut l’installation de type hello Service Fabric SDK et Visual Studio 2017 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="4cd33-108">This includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="4cd33-109">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="4cd33-109">Create hello application</span></span>

<span data-ttu-id="4cd33-110">Lancez Visual Studio en tant qu’**administrateur**.</span><span class="sxs-lookup"><span data-stu-id="4cd33-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="4cd33-111">Créer un projet avec `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="4cd33-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="4cd33-112">Bonjour **nouveau projet** boîte de dialogue, choisissez **Cloud > Application Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="4cd33-112">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="4cd33-113">Nommez l’application hello **MyApplication** et appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4cd33-113">Name hello application **MyApplication** and press **OK**.</span></span>

   
![Boîte de dialogue Nouveau projet dans Visual Studio][1]

<span data-ttu-id="4cd33-115">Vous pouvez créer n’importe quel type d’application de Service Fabric à partir de la boîte de dialogue suivante hello.</span><span class="sxs-lookup"><span data-stu-id="4cd33-115">You can create any type of Service Fabric application from hello next dialog.</span></span> <span data-ttu-id="4cd33-116">Pour ce démarrage rapide, choisissez **Service avec état**.</span><span class="sxs-lookup"><span data-stu-id="4cd33-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="4cd33-117">Nom de votre service de hello **MyStatefulService** et appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4cd33-117">Name hello service **MyStatefulService** and press **OK**.</span></span>

![Boîte de dialogue Nouveau service dans Visual Studio.][2]


<span data-ttu-id="4cd33-119">Visual Studio crée le projet d’application hello et de projet de service avec état hello et les affiche dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="4cd33-119">Visual Studio creates hello application project and hello stateful service project and displays them in Solution Explorer.</span></span>

![Explorateur de solutions après la création de l’application de service avec état][3]

<span data-ttu-id="4cd33-121">projet d’application Hello (**MyApplication**) ne contient pas de code directement.</span><span class="sxs-lookup"><span data-stu-id="4cd33-121">hello application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="4cd33-122">Au lieu de cela, il fait référence à un ensemble de projets de service.</span><span class="sxs-lookup"><span data-stu-id="4cd33-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="4cd33-123">En outre, il contient trois autres types de contenu :</span><span class="sxs-lookup"><span data-stu-id="4cd33-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="4cd33-124">**Profils de publication**</span><span class="sxs-lookup"><span data-stu-id="4cd33-124">**Publish profiles**</span></span>  
<span data-ttu-id="4cd33-125">Profils pour le déploiement d’environnements de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="4cd33-125">Profiles for deploying toodifferent environments.</span></span>

* <span data-ttu-id="4cd33-126">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="4cd33-126">**Scripts**</span></span>  
<span data-ttu-id="4cd33-127">Script PowerShell de déploiement/mise à niveau de votre application.</span><span class="sxs-lookup"><span data-stu-id="4cd33-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="4cd33-128">**Définition d’application**</span><span class="sxs-lookup"><span data-stu-id="4cd33-128">**Application definition**</span></span>  
<span data-ttu-id="4cd33-129">Inclut le fichier ApplicationManifest.xml hello *ApplicationPackageRoot* qui décrit la composition de votre application.</span><span class="sxs-lookup"><span data-stu-id="4cd33-129">Includes hello ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="4cd33-130">Fichiers de paramètres d’application associée sont sous *ApplicationParameters*, qui peut être utilisé toospecify paramètres spécifiques à l’environnement.</span><span class="sxs-lookup"><span data-stu-id="4cd33-130">Associated application parameter files are under *ApplicationParameters*, which can be used toospecify environment-specific parameters.</span></span> <span data-ttu-id="4cd33-131">Profil de publication Visual sélectionne Studio associé d’un fichier de paramètres d’application qui est spécifié dans hello au cours de l’environnement de déploiement tooa spécifique.</span><span class="sxs-lookup"><span data-stu-id="4cd33-131">Visual Studio selects an application parameter file that's specified in hello associated publish profile during deployment tooa specific environment.</span></span>
    
<span data-ttu-id="4cd33-132">Pour une vue d’ensemble du contenu hello hello du projet de service, consultez [prise en main des Services fiables](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="4cd33-132">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-hello-application"></a><span data-ttu-id="4cd33-133">Déployer et déboguer l’application hello</span><span class="sxs-lookup"><span data-stu-id="4cd33-133">Deploy and debug hello application</span></span>

<span data-ttu-id="4cd33-134">Maintenant que vous disposez d’une application, exécutez-la.</span><span class="sxs-lookup"><span data-stu-id="4cd33-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="4cd33-135">Dans Visual Studio, appuyez sur `F5` application hello de toodeploy pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="4cd33-135">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="4cd33-136">Hello la première fois que vous exécutez et déployez l’application hello localement, Visual Studio crée un cluster local pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="4cd33-136">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="4cd33-137">Cette opération peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="4cd33-137">This may take some time.</span></span> <span data-ttu-id="4cd33-138">état de la création de cluster Hello s’affiche dans la fenêtre de sortie de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="4cd33-138">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="4cd33-139">Lorsque le cluster de hello est prêt, vous recevez une notification d’une application hello cluster local système bac manager incluse avec le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="4cd33-139">When hello cluster is ready, you get a notification from hello local cluster system tray manager application included with hello SDK.</span></span>
   
![Notification de barre d’état système de cluster local][4]

<span data-ttu-id="4cd33-141">Une fois hello démarrage de l’application, Visual Studio appelle automatiquement hello **Observateur d’événements de diagnostic**, où vous pouvez consulter la sortie de trace à partir de vos services.</span><span class="sxs-lookup"><span data-stu-id="4cd33-141">Once hello application starts, Visual Studio automatically brings up hello **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Observateur d’événements de diagnostic][5]

<span data-ttu-id="4cd33-143">Hello modèle de service avec état nous utilisés affiche simplement une valeur de compteur incrémenté Bonjour `RunAsync` méthode **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="4cd33-143">hello stateful service template we used simply shows a counter value incrementing in hello `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="4cd33-144">Développez un des hello événements toosee de plus de détails, y compris le nœud hello où hello code est exécuté.</span><span class="sxs-lookup"><span data-stu-id="4cd33-144">Expand one of hello events toosee more details, including hello node where hello code is running.</span></span> <span data-ttu-id="4cd33-145">Dans ce cas, il s’agit du \_Node\_2, bien que cela puisse être différent sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4cd33-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Détails de l’Observateur d’événements de diagnostic][6]

<span data-ttu-id="4cd33-147">le cluster local Hello contient cinq nœuds hébergés sur un seul ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4cd33-147">hello local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="4cd33-148">Dans un environnement de production, chaque nœud est hébergé sur une machine virtuelle ou physique distincte.</span><span class="sxs-lookup"><span data-stu-id="4cd33-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="4cd33-149">débogueur de perte de hello toosimulate d’un ordinateur lors de l’exercice hello Visual Studio au hello même temps, nous allons prendre un des nœuds hello sur le cluster local de hello.</span><span class="sxs-lookup"><span data-stu-id="4cd33-149">toosimulate hello loss of a machine while exercising hello Visual Studio debugger at hello same time, let's take down one of hello nodes on hello local cluster.</span></span>

<span data-ttu-id="4cd33-150">Bonjour **l’Explorateur de solutions** fenêtre, ouvrez **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="4cd33-150">In hello **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="4cd33-151">Recherche hello `RunAsync` (méthode) et définissez un point d’arrêt sur la première ligne de hello de méthode hello.</span><span class="sxs-lookup"><span data-stu-id="4cd33-151">Find hello `RunAsync` method and set a breakpoint on hello first line of hello method.</span></span>

![Point d’arrêt dans la méthode RunAsync de service avec état][7]

<span data-ttu-id="4cd33-153">Lancez hello **Service Fabric Explorer** outil en cliquant sur hello **le Gestionnaire du Cluster Local** application de barre d’état système et choisissez **gérer un Cluster Local**.</span><span class="sxs-lookup"><span data-stu-id="4cd33-153">Launch hello **Service Fabric Explorer** tool by right-clicking on hello **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Lancer le Service Fabric Explorer à partir de hello Gestionnaire du Cluster Local][systray-launch-sfx]

<span data-ttu-id="4cd33-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offre une représentation visuelle d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="4cd33-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="4cd33-156">Elle inclut ensemble hello des applications déployées tooit et ensemble hello nœuds physiques qui le composent.</span><span class="sxs-lookup"><span data-stu-id="4cd33-156">It includes hello set of applications deployed tooit and hello set of physical nodes that make it up.</span></span>

<span data-ttu-id="4cd33-157">Dans le volet gauche de hello, développez **Cluster > nœuds** et nœud de hello rechercher où votre code est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4cd33-157">In hello left pane, expand **Cluster > Nodes** and find hello node where your code is running.</span></span>

<span data-ttu-id="4cd33-158">Cliquez sur **Actions > désactiver (Redémarrer)** toosimulate un redémarrage de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4cd33-158">Click **Actions > Deactivate (Restart)** toosimulate a machine restarting.</span></span>

![Arrêter un nœud Service Fabric Explorer][sfx-stop-node]

<span data-ttu-id="4cd33-160">Bientôt, vous devez voir votre point d’arrêt atteint dans Visual Studio que vous faisiez en toute transparence sur un nœud de calcul de hello bascule tooanother.</span><span class="sxs-lookup"><span data-stu-id="4cd33-160">Momentarily, you should see your breakpoint hit in Visual Studio as hello computation you were doing on one node seamlessly fails over tooanother.</span></span>


<span data-ttu-id="4cd33-161">Ensuite, retourner toohello Observateur d’événements de Diagnostic et observez les messages de type hello.</span><span class="sxs-lookup"><span data-stu-id="4cd33-161">Next, return toohello Diagnostic Events Viewer and observe hello messages.</span></span> <span data-ttu-id="4cd33-162">compteur de Hello a continué à incrémentation, même si les événements hello réellement provenant d’un autre nœud.</span><span class="sxs-lookup"><span data-stu-id="4cd33-162">hello counter has continued incrementing, even though hello events are actually coming from a different node.</span></span>

![Observateur d’événements de diagnostic après basculement][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a><span data-ttu-id="4cd33-164">Nettoyage de cluster local de hello (facultatif)</span><span class="sxs-lookup"><span data-stu-id="4cd33-164">Cleaning up hello local cluster (optional)</span></span>

<span data-ttu-id="4cd33-165">N’oubliez pas que ce cluster local est réel.</span><span class="sxs-lookup"><span data-stu-id="4cd33-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="4cd33-166">L’arrêt du débogueur de hello supprime l’instance d’application et annule l’inscription du type de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4cd33-166">Stopping hello debugger removes your application instance and unregisters hello application type.</span></span> <span data-ttu-id="4cd33-167">Toutefois, le cluster de hello continue toorun en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="4cd33-167">However, hello cluster continues toorun in hello background.</span></span> <span data-ttu-id="4cd33-168">Lorsque vous êtes le cluster local de prêt toostop hello, il existe deux options.</span><span class="sxs-lookup"><span data-stu-id="4cd33-168">When you're ready toostop hello local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="4cd33-169">Conserver les données d’application et de trace</span><span class="sxs-lookup"><span data-stu-id="4cd33-169">Keep application and trace data</span></span>

<span data-ttu-id="4cd33-170">Arrêter le cluster de hello en cliquant sur hello **le Gestionnaire du Cluster Local** application de barre d’état système, puis **arrêter le Cluster Local**.</span><span class="sxs-lookup"><span data-stu-id="4cd33-170">Shut down hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-hello-cluster-and-all-data"></a><span data-ttu-id="4cd33-171">Supprimer le cluster de hello et toutes les données</span><span class="sxs-lookup"><span data-stu-id="4cd33-171">Delete hello cluster and all data</span></span>

<span data-ttu-id="4cd33-172">Supprimer le cluster de hello en cliquant sur hello **le Gestionnaire du Cluster Local** application de barre d’état système, puis **supprimer le Cluster Local**.</span><span class="sxs-lookup"><span data-stu-id="4cd33-172">Remove hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="4cd33-173">Si vous choisissez cette option, Visual Studio redéployer hello de cluster hello prochaine fois que vous exécutez hello application.</span><span class="sxs-lookup"><span data-stu-id="4cd33-173">If you choose this option, Visual Studio will redeploy hello cluster hello next time your run hello application.</span></span> <span data-ttu-id="4cd33-174">Choisissez cette option si vous n’envisagez pas cluster local de hello toouse pendant un certain temps, ou si vous avez besoin des ressources de tooreclaim.</span><span class="sxs-lookup"><span data-stu-id="4cd33-174">Choose this option if you don't intend toouse hello local cluster for some time or if you need tooreclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cd33-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4cd33-175">Next steps</span></span>
<span data-ttu-id="4cd33-176">En savoir plus sur les [services fiables](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4cd33-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
