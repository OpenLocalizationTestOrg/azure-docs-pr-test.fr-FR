---
title: "Créer un service fiable Azure Service Fabric avec C#"
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
ms.openlocfilehash: f93298e6483fd8c9dfda835964aeebd1a430af69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="dbd22-103">Création de votre première application de services fiables avec état c# Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dbd22-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="dbd22-104">Découvrez comment déployer votre première application Service Fabric pour .NET sur Windows en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="dbd22-104">Learn how to deploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="dbd22-105">Une fois l’opération terminée, vous obtenez un cluster local fonctionnant avec une application de service fiable.</span><span class="sxs-lookup"><span data-stu-id="dbd22-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbd22-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dbd22-106">Prerequisites</span></span>

<span data-ttu-id="dbd22-107">Avant de commencer, assurez-vous que vous avez bien [configuré votre environnement de développement](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dbd22-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="dbd22-108">Cela inclut l’installation du SDK de Service Fabric et de Visual Studio 2017 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="dbd22-108">This includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="dbd22-109">Création de l'application</span><span class="sxs-lookup"><span data-stu-id="dbd22-109">Create the application</span></span>

<span data-ttu-id="dbd22-110">Lancez Visual Studio en tant qu’**administrateur**.</span><span class="sxs-lookup"><span data-stu-id="dbd22-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="dbd22-111">Créer un projet avec `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="dbd22-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="dbd22-112">Dans la boîte de dialogue **Nouveau projet**, sélectionnez **Cloud > Application Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="dbd22-112">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="dbd22-113">Appelez l’application **MonApplication**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dbd22-113">Name the application **MyApplication** and press **OK**.</span></span>

   
![Boîte de dialogue Nouveau projet dans Visual Studio][1]

<span data-ttu-id="dbd22-115">Vous pouvez créer n’importe quel type d’application Service Fabric à partir de la boîte de dialogue suivante.</span><span class="sxs-lookup"><span data-stu-id="dbd22-115">You can create any type of Service Fabric application from the next dialog.</span></span> <span data-ttu-id="dbd22-116">Pour ce démarrage rapide, choisissez **Service avec état**.</span><span class="sxs-lookup"><span data-stu-id="dbd22-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="dbd22-117">Appelez le service **MyStatefulService**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dbd22-117">Name the service **MyStatefulService** and press **OK**.</span></span>

![Boîte de dialogue Nouveau service dans Visual Studio.][2]


<span data-ttu-id="dbd22-119">Visual Studio crée le projet d’application et le projet de service avec état et les affiche dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="dbd22-119">Visual Studio creates the application project and the stateful service project and displays them in Solution Explorer.</span></span>

![Explorateur de solutions après la création de l’application de service avec état][3]

<span data-ttu-id="dbd22-121">Le projet d’application (**MyApplication**) ne contient pas de code directement.</span><span class="sxs-lookup"><span data-stu-id="dbd22-121">The application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="dbd22-122">Au lieu de cela, il fait référence à un ensemble de projets de service.</span><span class="sxs-lookup"><span data-stu-id="dbd22-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="dbd22-123">En outre, il contient trois autres types de contenu :</span><span class="sxs-lookup"><span data-stu-id="dbd22-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="dbd22-124">**Profils de publication**</span><span class="sxs-lookup"><span data-stu-id="dbd22-124">**Publish profiles**</span></span>  
<span data-ttu-id="dbd22-125">Profils pour le déploiement sur différents environnements.</span><span class="sxs-lookup"><span data-stu-id="dbd22-125">Profiles for deploying to different environments.</span></span>

* <span data-ttu-id="dbd22-126">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="dbd22-126">**Scripts**</span></span>  
<span data-ttu-id="dbd22-127">Script PowerShell de déploiement/mise à niveau de votre application.</span><span class="sxs-lookup"><span data-stu-id="dbd22-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="dbd22-128">**Définition d’application**</span><span class="sxs-lookup"><span data-stu-id="dbd22-128">**Application definition**</span></span>  
<span data-ttu-id="dbd22-129">Inclut le fichier ApplicationManifest.xml sous *ApplicationPackageRoot* qui décrit la composition de votre application.</span><span class="sxs-lookup"><span data-stu-id="dbd22-129">Includes the ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="dbd22-130">Les fichiers de paramètres d’application associés se trouvent sous le dossier *ApplicationParameters*, qui peut être utilisé pour spécifier des paramètres spécifiques à l’environnement.</span><span class="sxs-lookup"><span data-stu-id="dbd22-130">Associated application parameter files are under *ApplicationParameters*, which can be used to specify environment-specific parameters.</span></span> <span data-ttu-id="dbd22-131">Visual Studio sélectionne un fichier de paramètres d’application qui est spécifié dans le profil de publication associé au cours du déploiement dans un environnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="dbd22-131">Visual Studio selects an application parameter file that's specified in the associated publish profile during deployment to a specific environment.</span></span>
    
<span data-ttu-id="dbd22-132">Pour avoir une vue d’ensemble du contenu du projet de service, consultez l’article [Prise en main de Reliable Services](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="dbd22-132">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-the-application"></a><span data-ttu-id="dbd22-133">Déployer et déboguer l’application.</span><span class="sxs-lookup"><span data-stu-id="dbd22-133">Deploy and debug the application</span></span>

<span data-ttu-id="dbd22-134">Maintenant que vous disposez d’une application, exécutez-la.</span><span class="sxs-lookup"><span data-stu-id="dbd22-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="dbd22-135">Appuyez sur `F5` dans Visual Studio pour déployer l’application en vue d’un débogage.</span><span class="sxs-lookup"><span data-stu-id="dbd22-135">In Visual Studio, press `F5` to deploy the application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="dbd22-136">La première fois que vous exécutez et déployez l’application localement, Visual Studio crée un cluster local pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="dbd22-136">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="dbd22-137">Cette opération peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="dbd22-137">This may take some time.</span></span> <span data-ttu-id="dbd22-138">L’état de la création du cluster est affiché dans la fenêtre Sortie de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbd22-138">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="dbd22-139">Une fois le cluster prêt, vous obtenez une notification de la part de l’application de gestionnaire de la barre d’état système de cluster local incluse avec le kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="dbd22-139">When the cluster is ready, you get a notification from the local cluster system tray manager application included with the SDK.</span></span>
   
![Notification de barre d’état système de cluster local][4]

<span data-ttu-id="dbd22-141">Une fois que l’application a démarré, Visual Studio affiche automatiquement **l’Observateur d’événements de diagnostic**, où vous pouvez voir la sortie de suivi depuis vos services.</span><span class="sxs-lookup"><span data-stu-id="dbd22-141">Once the application starts, Visual Studio automatically brings up the **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Observateur d’événements de diagnostic][5]

<span data-ttu-id="dbd22-143">Le modèle de service avec état que nous avons utilisé indique simplement une valeur du compteur incrémentée dans la méthode `RunAsync` de **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="dbd22-143">The stateful service template we used simply shows a counter value incrementing in the `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="dbd22-144">Pour plus d’informations, développez un des événements, et notamment le nœud sur lequel le code s’exécute.</span><span class="sxs-lookup"><span data-stu-id="dbd22-144">Expand one of the events to see more details, including the node where the code is running.</span></span> <span data-ttu-id="dbd22-145">Dans ce cas, il s’agit du \_Node\_2, bien que cela puisse être différent sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dbd22-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Détails de l’Observateur d’événements de diagnostic][6]

<span data-ttu-id="dbd22-147">Le cluster local contient cinq nœuds hébergés sur un seul ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dbd22-147">The local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="dbd22-148">Dans un environnement de production, chaque nœud est hébergé sur une machine virtuelle ou physique distincte.</span><span class="sxs-lookup"><span data-stu-id="dbd22-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="dbd22-149">Pour simuler la perte d’une machine tout en testant le débogueur Visual Studio, examinons l’un des nœuds du cluster local.</span><span class="sxs-lookup"><span data-stu-id="dbd22-149">To simulate the loss of a machine while exercising the Visual Studio debugger at the same time, let's take down one of the nodes on the local cluster.</span></span>

<span data-ttu-id="dbd22-150">Dans la fenêtre de **l’Explorateur de solutions**, ouvrez **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="dbd22-150">In the **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="dbd22-151">Recherchez la méthode `RunAsync` et définissez un point d’arrêt sur la première ligne de la méthode.</span><span class="sxs-lookup"><span data-stu-id="dbd22-151">Find the `RunAsync` method and set a breakpoint on the first line of the method.</span></span>

![Point d’arrêt dans la méthode RunAsync de service avec état][7]

<span data-ttu-id="dbd22-153">Lancez l’outil **Service Fabric Explorer** en faisant un clic droit sur l’application du **gestionnaire du cluster local** dans la zone de notification, puis choisissez **Gérer le cluster local**.</span><span class="sxs-lookup"><span data-stu-id="dbd22-153">Launch the **Service Fabric Explorer** tool by right-clicking on the **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Lancer l’Explorateur de Fabric Service à partir du Gestionnaire de cluster Local.][systray-launch-sfx]

<span data-ttu-id="dbd22-155">[**Service Fabric Explorer** ](service-fabric-visualizing-your-cluster.md) offre une représentation visuelle d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd22-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="dbd22-156">Il inclut l’ensemble des applications qui y sont déployées, ainsi que le jeu de nœuds physiques qui le composent.</span><span class="sxs-lookup"><span data-stu-id="dbd22-156">It includes the set of applications deployed to it and the set of physical nodes that make it up.</span></span>

<span data-ttu-id="dbd22-157">Dans le volet de gauche, développez **Cluster > Nœuds** et recherchez le nœud sur lequel votre code s’exécute.</span><span class="sxs-lookup"><span data-stu-id="dbd22-157">In the left pane, expand **Cluster > Nodes** and find the node where your code is running.</span></span>

<span data-ttu-id="dbd22-158">Cliquez sur **Actions > Désactiver (Redémarrer)** pour simuler le redémarrage de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dbd22-158">Click **Actions > Deactivate (Restart)** to simulate a machine restarting.</span></span>

![Arrêter un nœud Service Fabric Explorer][sfx-stop-node]

<span data-ttu-id="dbd22-160">Vous devez voir momentanément le point d’arrêt atteint dans Visual Studio, car le calcul vous faisiez sur un nœud bascule en toute transparence vers un autre.</span><span class="sxs-lookup"><span data-stu-id="dbd22-160">Momentarily, you should see your breakpoint hit in Visual Studio as the computation you were doing on one node seamlessly fails over to another.</span></span>


<span data-ttu-id="dbd22-161">Revenez ensuite à l’Observateur d’événements de diagnostic et prenez connaissance des messages.</span><span class="sxs-lookup"><span data-stu-id="dbd22-161">Next, return to the Diagnostic Events Viewer and observe the messages.</span></span> <span data-ttu-id="dbd22-162">Le compteur a continué de s’incrémenter, même si les événements proviennent en fait d’un autre nœud.</span><span class="sxs-lookup"><span data-stu-id="dbd22-162">The counter has continued incrementing, even though the events are actually coming from a different node.</span></span>

![Observateur d’événements de diagnostic après basculement][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-the-local-cluster-optional"></a><span data-ttu-id="dbd22-164">Nettoyage du cluster local (facultatif)</span><span class="sxs-lookup"><span data-stu-id="dbd22-164">Cleaning up the local cluster (optional)</span></span>

<span data-ttu-id="dbd22-165">N’oubliez pas que ce cluster local est réel.</span><span class="sxs-lookup"><span data-stu-id="dbd22-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="dbd22-166">L’arrêt du débogueur supprime votre instance d’application et annule l’inscription du type d’application.</span><span class="sxs-lookup"><span data-stu-id="dbd22-166">Stopping the debugger removes your application instance and unregisters the application type.</span></span> <span data-ttu-id="dbd22-167">Le cluster continue toutefois de s’exécuter en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="dbd22-167">However, the cluster continues to run in the background.</span></span> <span data-ttu-id="dbd22-168">Lorsque vous êtes prêt à arrêter le cluster local, vous avez le choix entre deux options.</span><span class="sxs-lookup"><span data-stu-id="dbd22-168">When you're ready to stop the local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="dbd22-169">Conserver les données d’application et de trace</span><span class="sxs-lookup"><span data-stu-id="dbd22-169">Keep application and trace data</span></span>

<span data-ttu-id="dbd22-170">Fermez le cluster en effectuant un clic droit sur l’application de **gestionnaire du cluster local** dans la barre système, puis sélectionnez **Arrêter le cluster local**.</span><span class="sxs-lookup"><span data-stu-id="dbd22-170">Shut down the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-the-cluster-and-all-data"></a><span data-ttu-id="dbd22-171">Supprimer le cluster et toutes les données</span><span class="sxs-lookup"><span data-stu-id="dbd22-171">Delete the cluster and all data</span></span>

<span data-ttu-id="dbd22-172">Supprimez le cluster en effectuant un clic droit sur l’application de **gestionnaire du cluster local** dans la barre système, puis sélectionnez **Supprimer le cluster local**.</span><span class="sxs-lookup"><span data-stu-id="dbd22-172">Remove the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="dbd22-173">Si vous choisissez cette option, Visual Studio redéploiera le cluster la prochaine fois que vous exécuterez l’application.</span><span class="sxs-lookup"><span data-stu-id="dbd22-173">If you choose this option, Visual Studio will redeploy the cluster the next time your run the application.</span></span> <span data-ttu-id="dbd22-174">Optez pour cette option si vous n’envisagez pas d’utiliser le cluster local pendant un certain temps ou si vous avez besoin de libérer des ressources.</span><span class="sxs-lookup"><span data-stu-id="dbd22-174">Choose this option if you don't intend to use the local cluster for some time or if you need to reclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbd22-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dbd22-175">Next steps</span></span>
<span data-ttu-id="dbd22-176">En savoir plus sur les [services fiables](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dbd22-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
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
