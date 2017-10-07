---
title: "aaaDeploy un tooa d’application Azure Service Fabric tiers Cluster | Documents Microsoft"
description: "Découvrez comment toodeploy un tooa application partie du Cluster."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a><span data-ttu-id="fa076-103">Déployer une application de tooa Cluster tiers dans Azure</span><span class="sxs-lookup"><span data-stu-id="fa076-103">Deploy an application tooa Party Cluster in Azure</span></span>
<span data-ttu-id="fa076-104">Ce didacticiel fait partie de deux d’une série et vous montre comment toodeploy un tooa d’application Azure Service Fabric Cluster tiers dans Azure.</span><span class="sxs-lookup"><span data-stu-id="fa076-104">This tutorial is part two of a series and shows you how toodeploy an Azure Service Fabric application tooa Party Cluster in Azure.</span></span>

<span data-ttu-id="fa076-105">Dans la deuxième partie de la série de didacticiels hello, vous apprenez comment :</span><span class="sxs-lookup"><span data-stu-id="fa076-105">In part two of hello tutorial series, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="fa076-106">Déployer un cluster à distance tooa d’application à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fa076-106">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="fa076-107">Supprimer une application d’un cluster à l’aide de Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="fa076-107">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="fa076-108">Cette série de didacticiels vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fa076-108">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="fa076-109">Créer une application .NET Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fa076-109">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * <span data-ttu-id="fa076-110">Déployer le cluster de l’application hello tooa à distance</span><span class="sxs-lookup"><span data-stu-id="fa076-110">Deploy hello application tooa remote cluster</span></span>
> * [<span data-ttu-id="fa076-111">Configurer l’intégration et le déploiement continus à l’aide de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="fa076-111">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="fa076-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fa076-112">Prerequisites</span></span>
<span data-ttu-id="fa076-113">Avant de commencer ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="fa076-113">Before you begin this tutorial:</span></span>
- <span data-ttu-id="fa076-114">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="fa076-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="fa076-115">[Installer Visual Studio 2017](https://www.visualstudio.com/) et installer hello **le développement Azure** et **développement web ASP.NET et** les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="fa076-115">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="fa076-116">Installer hello SDK de l’infrastructure de Service</span><span class="sxs-lookup"><span data-stu-id="fa076-116">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a><span data-ttu-id="fa076-117">Télécharger l’application d’exemple hello vote</span><span class="sxs-lookup"><span data-stu-id="fa076-117">Download hello Voting sample application</span></span>
<span data-ttu-id="fa076-118">Si vous n’avez pas généré application d’exemple hello vote [première partie de cette série de didacticiels](service-fabric-tutorial-create-dotnet-app.md), vous pouvez le télécharger.</span><span class="sxs-lookup"><span data-stu-id="fa076-118">If you did not build hello Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="fa076-119">Dans une fenêtre de commande, exécutez hello suivant commande tooclone hello exemple application référentiel tooyour ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="fa076-119">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a><span data-ttu-id="fa076-120">Configurer un cluster tiers</span><span class="sxs-lookup"><span data-stu-id="fa076-120">Set up a Party Cluster</span></span>
<span data-ttu-id="fa076-121">Clusters tiers sont des clusters Service Fabric gratuites et limitée dans le temps hébergé sur Azure et exécuté par l’équipe de Service Fabric hello où tout le monde peut déployer des applications et en savoir plus sur la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="fa076-121">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="fa076-122">gratuitement.</span><span class="sxs-lookup"><span data-stu-id="fa076-122">For free!</span></span>

<span data-ttu-id="fa076-123">tooget accès tooa tiers Cluster, parcourir toothis site : http://aka.ms/tryservicefabric et suivez hello instructions tooget tooa cluster d’accès.</span><span class="sxs-lookup"><span data-stu-id="fa076-123">tooget access tooa Party Cluster, browse toothis site: http://aka.ms/tryservicefabric and follow hello instructions tooget access tooa cluster.</span></span> <span data-ttu-id="fa076-124">Vous avez besoin d’un Facebook ou GitHub compte tooget accès tooa tiers Cluster.</span><span class="sxs-lookup"><span data-stu-id="fa076-124">You need a Facebook or GitHub account tooget access tooa Party Cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="fa076-125">Clusters de tiers ne sont pas sécurisés, vos applications et toutes les données que vous placez dans les peuvent être tooothers visible.</span><span class="sxs-lookup"><span data-stu-id="fa076-125">Party clusters are not secured, so your applications and any data you put in them may be visible tooothers.</span></span> <span data-ttu-id="fa076-126">Ne déploie pas tout ce que vous ne souhaitez pas que d’autres toosee.</span><span class="sxs-lookup"><span data-stu-id="fa076-126">Don't deploy anything you don't want others toosee.</span></span> <span data-ttu-id="fa076-127">Être tooread que sur les conditions d’utilisation pour tous les détails de hello.</span><span class="sxs-lookup"><span data-stu-id="fa076-127">Be sure tooread over our Terms of Use for all hello details.</span></span>

## <a name="configure-hello-listening-port"></a><span data-ttu-id="fa076-128">Configurer le port d’écoute hello</span><span class="sxs-lookup"><span data-stu-id="fa076-128">Configure hello listening port</span></span>
<span data-ttu-id="fa076-129">Lors de la création de hello VotingWeb le service frontal, Visual Studio sélectionne de manière aléatoire un port pour hello service toolisten sur.</span><span class="sxs-lookup"><span data-stu-id="fa076-129">When hello VotingWeb front-end service is created, Visual Studio randomly selects a port for hello service toolisten on.</span></span>  <span data-ttu-id="fa076-130">Hello VotingWeb service joue le rôle hello frontal pour cette application et qu’il accepte le trafic externe, nous allons donc lier ce tooa service fixée et bien en connaître le port.</span><span class="sxs-lookup"><span data-stu-id="fa076-130">hello VotingWeb service acts as hello front-end for this application and accepts external traffic, so let's bind that service tooa fixed and well-know port.</span></span> <span data-ttu-id="fa076-131">Dans l’Explorateur de solutions, ouvrez *VotingWeb/PackageRoot/ServiceManifest.xml*.</span><span class="sxs-lookup"><span data-stu-id="fa076-131">In Solution Explorer, open  *VotingWeb/PackageRoot/ServiceManifest.xml*.</span></span>  <span data-ttu-id="fa076-132">Recherche hello **point de terminaison** ressource Bonjour **ressources** section et modifier hello **Port** too80 de valeur.</span><span class="sxs-lookup"><span data-stu-id="fa076-132">Find hello **Endpoint** resource in hello **Resources** section and change hello **Port** value too80.</span></span>

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="fa076-133">Mettre à jour également valeur de la propriété URL de l’Application hello dans le projet de vote hello sorte un navigateur web s’ouvre toohello bon port lorsque vous déboguez à l’aide de « F5 ».</span><span class="sxs-lookup"><span data-stu-id="fa076-133">Also update hello Application URL property value in hello Voting project so a web browser opens toohello correct port when you debug using 'F5'.</span></span>  <span data-ttu-id="fa076-134">Dans l’Explorateur de solutions, sélectionnez hello **vote** mise à jour et projet hello **URL de l’Application** propriété.</span><span class="sxs-lookup"><span data-stu-id="fa076-134">In Solution Explorer, select hello **Voting** project and update hello **Application URL** property.</span></span>

![URL de l’application](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a><span data-ttu-id="fa076-136">Déployer hello application toohello Azure</span><span class="sxs-lookup"><span data-stu-id="fa076-136">Deploy hello app toohello Azure</span></span>
<span data-ttu-id="fa076-137">Maintenant que l’application hello est prête, vous pouvez la déployer toohello Cluster tiers directement à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa076-137">Now that hello application is ready, you can deploy it toohello Party Cluster direct from Visual Studio.</span></span>

1. <span data-ttu-id="fa076-138">Avec le bouton droit **vote** dans hello l’Explorateur de solutions et choisissez **publier**.</span><span class="sxs-lookup"><span data-stu-id="fa076-138">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span>

    ![Boîte de dialogue Publier](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. <span data-ttu-id="fa076-140">Type Bonjour point de terminaison de connexion de hello tiers Cluster Bonjour **connexion de point de terminaison** champ et cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="fa076-140">Type in hello Connection Endpoint of hello Party Cluster in hello **Connection Endpoint** field and click **Publish**.</span></span>

    <span data-ttu-id="fa076-141">Une fois la publication de hello a terminé, vous devez être en mesure de toosend une application de toohello demande via un navigateur.</span><span class="sxs-lookup"><span data-stu-id="fa076-141">Once hello publish has finished, you should be able toosend a request toohello application via a browser.</span></span>

3. <span data-ttu-id="fa076-142">Ouvrez préféré navigateur et tapez dans l’adresse du cluster hello (hello connexion point de terminaison sans informations de port hello - par exemple, win1kw5649s.westus.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fa076-142">Open you preferred browser and type in hello cluster address (hello connection endpoint without hello port information - for example, win1kw5649s.westus.cloudapp.azure.com).</span></span>

    <span data-ttu-id="fa076-143">Vous devez maintenant voir hello même résultat que vous avez vu lors de l’exécution application hello localement.</span><span class="sxs-lookup"><span data-stu-id="fa076-143">You should now see hello same result as you saw when running hello application locally.</span></span>

    ![Réponse de l’API à partir du cluster](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="fa076-145">Supprimer l’application hello à partir d’un cluster à l’aide du Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="fa076-145">Remove hello application from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="fa076-146">Service Fabric Explorer est un tooexplore d’interface utilisateur graphique et gérer des applications dans un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fa076-146">Service Fabric Explorer is a graphical user interface tooexplore and manage applications in a Service Fabric cluster.</span></span>

<span data-ttu-id="fa076-147">application hello tooremove hello tiers Cluster :</span><span class="sxs-lookup"><span data-stu-id="fa076-147">tooremove hello application from hello Party Cluster:</span></span>

1. <span data-ttu-id="fa076-148">Parcourir toohello Service Fabric Explorer, à l’aide du lien hello fournie par la page d’inscription de tiers Cluster hello.</span><span class="sxs-lookup"><span data-stu-id="fa076-148">Browse toohello Service Fabric Explorer, using hello link provided by hello Party Cluster sign-up page.</span></span> <span data-ttu-id="fa076-149">Par exemple, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="fa076-149">For example, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span></span>

2. <span data-ttu-id="fa076-150">Dans l’Explorateur de l’infrastructure de Service, accédez à toohello **fabric://Voting** nœud de treeview hello sur le côté gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="fa076-150">In Service Fabric Explorer, navigate toohello **fabric://Voting** node in hello treeview on hello left-hand side.</span></span>

3. <span data-ttu-id="fa076-151">Cliquez sur hello **Action** bouton Bonjour droite **Essentials** volet, choisissez **supprimer l’Application**.</span><span class="sxs-lookup"><span data-stu-id="fa076-151">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Delete Application**.</span></span> <span data-ttu-id="fa076-152">Confirmer la suppression hello instance de l’application, ce qui supprime l’instance de notre application s’exécutant dans un cluster de hello hello.</span><span class="sxs-lookup"><span data-stu-id="fa076-152">Confirm deleting hello application instance, which removes hello instance of our application running in hello cluster.</span></span>

![Supprimer l’application dans Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="fa076-154">Supprimer le type d’application hello à partir d’un cluster à l’aide du Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="fa076-154">Remove hello application type from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="fa076-155">Les applications sont déployées en tant que types d’applications dans un cluster Service Fabric, ce qui permet de vous toohave plusieurs instances et les versions de l’application hello en cours d’exécution dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="fa076-155">Applications are deployed as application types in a Service Fabric cluster, which enables you toohave multiple instances and versions of hello application running within hello cluster.</span></span> <span data-ttu-id="fa076-156">Après l’avoir supprimé hello qui exécute l’instance de notre application, nous pouvons également supprimer de type hello, nettoyage de hello toocomplete du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="fa076-156">After having removed hello running instance of our application, we can also remove hello type, toocomplete hello cleanup of hello deployment.</span></span>

<span data-ttu-id="fa076-157">Pour plus d’informations sur le modèle d’application hello dans l’infrastructure de Service, consultez [une application dans l’infrastructure de Service de modèle](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="fa076-157">For more information about hello application model in Service Fabric, see [Model an application in Service Fabric](service-fabric-application-model.md).</span></span>

1. <span data-ttu-id="fa076-158">Accédez toohello **VotingType** nœud hello treeview.</span><span class="sxs-lookup"><span data-stu-id="fa076-158">Navigate toohello **VotingType** node in hello treeview.</span></span>

2. <span data-ttu-id="fa076-159">Cliquez sur hello **Action** bouton Bonjour droite **Essentials** volet, choisissez **la mise hors service Type**.</span><span class="sxs-lookup"><span data-stu-id="fa076-159">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Unprovision Type**.</span></span> <span data-ttu-id="fa076-160">Vérifiez le type d’application hello annulation du déploiement.</span><span class="sxs-lookup"><span data-stu-id="fa076-160">Confirm unprovisioning hello application type.</span></span>

![Annuler la mise en service du type d’application dans Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

<span data-ttu-id="fa076-162">Ceci conclut le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="fa076-162">This concludes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa076-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fa076-163">Next steps</span></span>
<span data-ttu-id="fa076-164">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="fa076-164">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fa076-165">Déployer un cluster à distance tooa d’application à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fa076-165">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="fa076-166">Supprimer une application d’un cluster à l’aide de Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="fa076-166">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="fa076-167">Avance toohello étape suivante du didacticiel :</span><span class="sxs-lookup"><span data-stu-id="fa076-167">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fa076-168">Configurer l’intégration continue avec Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="fa076-168">Set up continuous integration using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)