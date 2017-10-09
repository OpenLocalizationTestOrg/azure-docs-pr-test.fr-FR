---
title: aaaDeploy une application .NET dans un conteneur de tooAzure Service Fabric | Documents Microsoft
description: "Vous apprend comment toopackage une application .NET dans Visual Studio dans un conteneur Docker. Cette nouvelle application « conteneur » est ensuite déployée cluster Service Fabric de tooa."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a><span data-ttu-id="88138-104">Déployer une application .NET dans un tooAzure de conteneur Windows Service Fabric</span><span class="sxs-lookup"><span data-stu-id="88138-104">Deploy a .NET application in a Windows container tooAzure Service Fabric</span></span>

<span data-ttu-id="88138-105">Ce didacticiel vous montre comment toodeploy une application ASP.NET existante dans un conteneur Windows sur Azure.</span><span class="sxs-lookup"><span data-stu-id="88138-105">This tutorial shows you how toodeploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="88138-106">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="88138-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88138-107">Créer un projet Docker dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88138-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="88138-108">Mettre en conteneur une application existante</span><span class="sxs-lookup"><span data-stu-id="88138-108">Containerize an existing application</span></span>
> * <span data-ttu-id="88138-109">Configurer l’intégration continue avec Visual Studio et VSTS</span><span class="sxs-lookup"><span data-stu-id="88138-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88138-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="88138-110">Prerequisites</span></span>

1. <span data-ttu-id="88138-111">Installez [Docker CE pour Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) afin que vous puissiez exécuter des conteneurs sur Windows 10.</span><span class="sxs-lookup"><span data-stu-id="88138-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="88138-112">Familiarisez-vous avec hello [démarrage rapide des conteneurs de Windows 10][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="88138-112">Familiarize yourself with hello [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="88138-113">Télécharger hello [Fabrikam Fiber CallCenter] [ link-fabrikam-github] exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="88138-113">Download hello [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="88138-114">Installez [Azure PowerShell][link-azure-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="88138-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="88138-115">Installer hello [extension des outils de livraison continue pour Visual Studio 2017][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="88138-115">Install hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="88138-116">Créez un [Abonnement Azure][link-azure-subscription] et un [Compte Visual Studio Team Services][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="88138-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="88138-117">Créez un cluster sur Azure</span><span class="sxs-lookup"><span data-stu-id="88138-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a><span data-ttu-id="88138-118">Mettez en conteneur application hello</span><span class="sxs-lookup"><span data-stu-id="88138-118">Containerize hello application</span></span>

<span data-ttu-id="88138-119">Maintenant que vous avez un [cluster Service Fabric s’exécute dans Azure](service-fabric-tutorial-create-cluster-azure-ps.md) vous êtes prêt toocreate et que vous déployez une application en conteneur.</span><span class="sxs-lookup"><span data-stu-id="88138-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready toocreate and deploy a containerized application.</span></span> <span data-ttu-id="88138-120">toostart notre application en cours d’exécution dans un conteneur, nous devons tooadd **prise en charge Docker** projet toohello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88138-120">toostart running our application in a container, we need tooadd **Docker Support** toohello project in Visual Studio.</span></span> <span data-ttu-id="88138-121">Lorsque vous ajoutez **prise en charge Docker** toohello application, deux événements se produisent.</span><span class="sxs-lookup"><span data-stu-id="88138-121">When you add **Docker support** toohello application, two things happen.</span></span> <span data-ttu-id="88138-122">Tout d’abord, un _Dockerfile_ est ajouté toohello projet.</span><span class="sxs-lookup"><span data-stu-id="88138-122">First, a _Dockerfile_ is added toohello project.</span></span> <span data-ttu-id="88138-123">Ce nouveau fichier décrit comment image de conteneur hello toobe généré.</span><span class="sxs-lookup"><span data-stu-id="88138-123">This new file describes how hello container image is toobe built.</span></span> <span data-ttu-id="88138-124">Puis la deuxième, un nouveau _docker-composer_ projet est ajouté à la solution de toohello.</span><span class="sxs-lookup"><span data-stu-id="88138-124">Then second, a new _docker-compose_ project is added toohello solution.</span></span> <span data-ttu-id="88138-125">nouveau projet Hello contient quelques docker-composer des fichiers.</span><span class="sxs-lookup"><span data-stu-id="88138-125">hello new project contains a few docker-compose files.</span></span> <span data-ttu-id="88138-126">Fichiers de composer de docker peuvent être utilisé toodescribe comment conteneur de hello est exécuté.</span><span class="sxs-lookup"><span data-stu-id="88138-126">Docker-compose files can be used toodescribe how hello container is run.</span></span>

<span data-ttu-id="88138-127">En savoir plus sur l’utilisation de [Visual Studio Container Tools][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="88138-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="88138-128">S’il est hello première fois que vous les images de conteneur Windows sont en cours d’exécution sur votre ordinateur, CE de Docker doit le chercher les images de base hello pour vos conteneurs.</span><span class="sxs-lookup"><span data-stu-id="88138-128">If it is hello first time you are running Windows container images on your computer, Docker CE must pull down hello base images for your containers.</span></span> <span data-ttu-id="88138-129">les images de Hello utilisés dans ce didacticiel sont 14 Go.</span><span class="sxs-lookup"><span data-stu-id="88138-129">hello images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="88138-130">Pour commencer, exécutez hello suivant des images de base hello toopull commande Terminal Server :</span><span class="sxs-lookup"><span data-stu-id="88138-130">Go ahead and run hello following terminal command toopull hello base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="88138-131">Ajouter la prise en charge Docker</span><span class="sxs-lookup"><span data-stu-id="88138-131">Add Docker support</span></span>

<span data-ttu-id="88138-132">Ouvrez hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] fichier dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88138-132">Open hello [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="88138-133">Avec le bouton hello **FabrikamFiber.Web** projet > **ajouter** > **prise en charge Docker**.</span><span class="sxs-lookup"><span data-stu-id="88138-133">Right-click hello **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="88138-134">Ajouter la prise en charge de SQL</span><span class="sxs-lookup"><span data-stu-id="88138-134">Add support for SQL</span></span>

<span data-ttu-id="88138-135">Cette application utilise SQL en tant que fournisseur de données hello, par conséquent, un serveur SQL server est requis toorun hello application.</span><span class="sxs-lookup"><span data-stu-id="88138-135">This application uses SQL as hello data provider, so a SQL server is required toorun hello application.</span></span> <span data-ttu-id="88138-136">Référencez une image de conteneur SQL Server dans notre fichier docker-compose.override.yml.</span><span class="sxs-lookup"><span data-stu-id="88138-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="88138-137">Dans Visual Studio, ouvrez **l’Explorateur de solutions**, trouver **composer de docker**et ouvrez hello **docker-compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="88138-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="88138-138">Accédez toohello `services:` nœud, ajoutez un nœud nommé `db:` qui définit l’entrée de SQL Server hello pour le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="88138-138">Navigate toohello `services:` node, add a node named `db:` that defines hello SQL Server entry for hello container.</span></span>

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
><span data-ttu-id="88138-139">Vous pouvez utiliser l’instance SQL Server de votre choix pour le débogage local, tant qu’elle est accessible à partir de votre hôte.</span><span class="sxs-lookup"><span data-stu-id="88138-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="88138-140">**localdb** ne prend cependant pas en charge la communication `container -> host`.</span><span class="sxs-lookup"><span data-stu-id="88138-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="88138-141">L’exécution de SQL Server dans un conteneur ne prend pas en charge les données persistantes.</span><span class="sxs-lookup"><span data-stu-id="88138-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="88138-142">Lorsque le conteneur de hello s’arrête, vos données sont effacées.</span><span class="sxs-lookup"><span data-stu-id="88138-142">When hello container stops, your data is erased.</span></span> <span data-ttu-id="88138-143">N’utilisez pas cette configuration pour la production.</span><span class="sxs-lookup"><span data-stu-id="88138-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="88138-144">Accédez toohello `fabrikamfiber.web:` nœud et ajouter un nœud enfant nommé `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="88138-144">Navigate toohello `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="88138-145">Cela garantit que hello `db` service (conteneur de SQL Server hello) démarre avant que notre application web (fabrikamfiber.web).</span><span class="sxs-lookup"><span data-stu-id="88138-145">This ensures that hello `db` service (hello SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a><span data-ttu-id="88138-146">Mettre à jour hello web config</span><span class="sxs-lookup"><span data-stu-id="88138-146">Update hello web config</span></span>

<span data-ttu-id="88138-147">Dans hello **FabrikamFiber.Web** projet, la chaîne de connexion de mise à jour hello Bonjour **web.config** toopoint toohello SQL Server dans le conteneur de hello, de fichiers.</span><span class="sxs-lookup"><span data-stu-id="88138-147">Back in hello **FabrikamFiber.Web** project, update hello connection string in hello **web.config** file, toopoint toohello SQL Server in hello container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="88138-148">Si vous voulez toouse un autre serveur SQL Server lors de la création d’une version de build de votre application web, ajoutez un autre fichier de web.release.config tooyour chaîne connexion.</span><span class="sxs-lookup"><span data-stu-id="88138-148">If you want toouse a different SQL Server when building a release build of your web application, add another connection string tooyour web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="88138-149">Tester votre conteneur</span><span class="sxs-lookup"><span data-stu-id="88138-149">Test your container</span></span>

<span data-ttu-id="88138-150">Appuyez sur **F5** toorun et déboguer l’application hello dans votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="88138-150">Press **F5** toorun and debug hello application in your container.</span></span>

<span data-ttu-id="88138-151">Bord ouvre la page de lancement défini de votre application à l’aide d’adresse IP de hello du conteneur de hello sur le réseau interne NAT (généralement 172.x.x.x) de hello.</span><span class="sxs-lookup"><span data-stu-id="88138-151">Edge opens your application's defined launch page using hello IP address of hello container on hello internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="88138-152">toolearn en savoir plus sur le débogage d’applications dans des conteneurs à l’aide de Visual Studio 2017, consultez [cet article][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="88138-152">toolearn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![exemple de fabrikam dans un conteneur][image-web-preview]

<span data-ttu-id="88138-154">Hello conteneur est maintenant prêt toobe généré et empaqueté dans une application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88138-154">hello container is now ready toobe built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="88138-155">Une fois que vous avez hello conteneur génération de l’image sur votre ordinateur, vous pouvez distribuer le Registre de conteneur tooany et par l’extraction vers le bas tooany hôte toorun.</span><span class="sxs-lookup"><span data-stu-id="88138-155">Once you have hello container image built on your machine, you can push it tooany container registry and pull it down tooany host toorun.</span></span>

## <a name="get-hello-application-ready-for-hello-cloud"></a><span data-ttu-id="88138-156">Préparer l’application hello pour le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="88138-156">Get hello application ready for hello cloud</span></span>

<span data-ttu-id="88138-157">l’application de hello tooget prête pour l’exécution dans l’infrastructure de Service dans Azure, nous devons toocomplete deux étapes :</span><span class="sxs-lookup"><span data-stu-id="88138-157">tooget hello application ready for running in Service Fabric in Azure, we need toocomplete two steps:</span></span>

1. <span data-ttu-id="88138-158">Exposer le port hello que nous voulons tooreach en mesure de toobe notre application web dans le cluster Service Fabric de hello.</span><span class="sxs-lookup"><span data-stu-id="88138-158">Expose hello port where we want toobe able tooreach our web application in hello Service Fabric cluster.</span></span>
2. <span data-ttu-id="88138-159">Fournir une base de données SQL prête pour notre application.</span><span class="sxs-lookup"><span data-stu-id="88138-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-hello-port-for-hello-app"></a><span data-ttu-id="88138-160">Exposer le port hello pour une application hello</span><span class="sxs-lookup"><span data-stu-id="88138-160">Expose hello port for hello app</span></span>
<span data-ttu-id="88138-161">cluster Service Fabric de Hello que nous avons configuré, a port *80* ouvert par défaut dans hello équilibrage de charge Azure, qui équilibre cluster de toohello le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="88138-161">hello Service Fabric cluster we have configured, has port *80* open by default in hello Azure Load Balancer, that balances incoming traffic toohello cluster.</span></span> <span data-ttu-id="88138-162">Nous pouvons exposer notre conteneur sur ce port par le biais de notre fichier docker-compose.yml.</span><span class="sxs-lookup"><span data-stu-id="88138-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="88138-163">Dans Visual Studio, ouvrez **l’Explorateur de solutions**, trouver **composer de docker**et ouvrez hello **docker-compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="88138-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="88138-164">Modifier hello `fabrikamfiber.web:` nœud, ajoutez un nœud enfant nommé `ports:`.</span><span class="sxs-lookup"><span data-stu-id="88138-164">Modify hello `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="88138-165">Ajoutez une entrée chaîne `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="88138-165">Add a string entry `- "80:80"`.</span></span>

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a><span data-ttu-id="88138-166">Utiliser une base de données SQL de production</span><span class="sxs-lookup"><span data-stu-id="88138-166">Use a production SQL database</span></span>
<span data-ttu-id="88138-167">Lors de l’exécution dans un environnement de production, nos données doivent être persistantes dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="88138-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="88138-168">Il n’existe actuellement aucune donnée persistante de façon tooguarantee dans un conteneur, par conséquent vous ne pouvez pas stocker les données de production dans SQL Server dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="88138-168">There is currently no way tooguarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="88138-169">Nous vous recommandons d’utiliser une base de données Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="88138-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="88138-170">tooset haut et exécuter un serveur SQL géré dans Azure, visitez hello [Démarrages rapides de base de données Azure SQL] [ link-azure-sql] l’article.</span><span class="sxs-lookup"><span data-stu-id="88138-170">tooset up and run a managed SQL Server in Azure, visit hello [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="88138-171">N’oubliez pas de serveur SQL toochange hello connexion chaînes toohello Bonjour **web.release.config** fichier Bonjour **FabrikamFiber.Web** projet.</span><span class="sxs-lookup"><span data-stu-id="88138-171">Remember toochange hello connection strings toohello SQL server in hello **web.release.config** file in hello **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="88138-172">Cette application échoue normalement si aucune base de données SQL n’est accessible.</span><span class="sxs-lookup"><span data-stu-id="88138-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="88138-173">Vous pouvez choisir toogo avance et déployer l’application hello avec aucun serveur SQL server.</span><span class="sxs-lookup"><span data-stu-id="88138-173">You can choose toogo ahead and deploy hello application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="88138-174">Déployer avec Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="88138-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="88138-175">tooset le déploiement à l’aide de Visual Studio Team Services, vous devez tooinstall hello [extension des outils de livraison continue pour Visual Studio 2017][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="88138-175">tooset up deployment using Visual Studio Team Services, you need tooinstall hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="88138-176">Cette extension rend facile toodeploy tooAzure par la configuration de Visual Studio Team Services et obtenir votre cluster Service Fabric de tooyour application déployée.</span><span class="sxs-lookup"><span data-stu-id="88138-176">This extension makes it easy toodeploy tooAzure by configuring Visual Studio Team Services and get your app deployed tooyour Service Fabric cluster.</span></span>

<span data-ttu-id="88138-177">tooget démarré, votre code doit être hébergé dans le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="88138-177">tooget started, your code must be hosted in source control.</span></span> <span data-ttu-id="88138-178">reste Hello de cette section suppose que **git** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="88138-178">hello rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="88138-179">Configurer un référentiel VSTS</span><span class="sxs-lookup"><span data-stu-id="88138-179">Set up a VSTS repo</span></span>
<span data-ttu-id="88138-180">En hello en bas à droite de Visual Studio, cliquez sur **ajouter tooSource contrôle** > **Git** (ou de l’option que vous préférez).</span><span class="sxs-lookup"><span data-stu-id="88138-180">At hello bottom-right corner of Visual Studio, click **Add tooSource Control** > **Git** (or whichever option you prefer).</span></span>

![Appuyez sur le bouton de contrôle de source de hello][image-source-control]

<span data-ttu-id="88138-182">Bonjour _Team Explorer_ volet, appuyez sur **publier le référentiel Git**.</span><span class="sxs-lookup"><span data-stu-id="88138-182">In hello _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="88138-183">Sélectionnez le nom de votre dépôt VSTS et appuyez sur **Dépôt**.</span><span class="sxs-lookup"><span data-stu-id="88138-183">Select your VSTS repository name and press **Repository**.</span></span>

![publier le référentiel tooVSTS][image-publish-repo]

<span data-ttu-id="88138-185">Maintenant que votre code est synchronisé avec un dépôt de code source VSTS, vous pouvez configurer l’intégration continue et la livraison continue.</span><span class="sxs-lookup"><span data-stu-id="88138-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="88138-186">Configurer une livraison continue</span><span class="sxs-lookup"><span data-stu-id="88138-186">Setup continuous delivery</span></span>

<span data-ttu-id="88138-187">Dans _l’Explorateur de solutions_, avec le bouton hello **solution** > **configurer la livraison continue**.</span><span class="sxs-lookup"><span data-stu-id="88138-187">In _Solution Explorer_, right-click hello **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="88138-188">Sélectionnez hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="88138-188">Select hello Azure Subscription.</span></span>

<span data-ttu-id="88138-189">Définissez **Type d’hôte** trop**Cluster Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="88138-189">Set **Host Type** too**Service Fabric Cluster**.</span></span>

<span data-ttu-id="88138-190">Définissez **hôte cible** toohello cluster service fabric vous avez créé dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="88138-190">Set **Target Host** toohello service fabric cluster you created in hello previous section.</span></span>

<span data-ttu-id="88138-191">Choisissez un **Registre de conteneur** toopublish à votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="88138-191">Choose a **Container Registry** toopublish your container to.</span></span>

>[!TIP]
><span data-ttu-id="88138-192">Hello d’utilisation **modifier** bouton toocreate un Registre de conteneur.</span><span class="sxs-lookup"><span data-stu-id="88138-192">Use hello **Edit** button toocreate a container registry.</span></span>

<span data-ttu-id="88138-193">Appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="88138-193">Press **OK**.</span></span>

![configurer l’intégration continue pour service fabric][image-setup-ci]
   
   <span data-ttu-id="88138-195">Une fois la configuration hello est terminée, votre conteneur est déployé tooService l’ensemble fibre optique.</span><span class="sxs-lookup"><span data-stu-id="88138-195">Once hello configuration is completed, your container is deployed tooService Fabric.</span></span> <span data-ttu-id="88138-196">Chaque fois que vous effectuez un push référentiel toohello de mises à jour une nouvelle build et la version est exécutée.</span><span class="sxs-lookup"><span data-stu-id="88138-196">Whenever you push updates toohello repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="88138-197">Images de conteneur de construction hello prennent environ 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="88138-197">Building hello container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="88138-198">Hello premier déploiement toohello Service Fabric cluster entraîne hello base Windows Server Core conteneur images toobe téléchargé.</span><span class="sxs-lookup"><span data-stu-id="88138-198">hello first deployment toohello Service Fabric cluster causes hello base Windows Server Core container images toobe downloaded.</span></span> <span data-ttu-id="88138-199">téléchargement de Hello prend plus de 5 à 10 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="88138-199">hello download takes additional 5-10 minutes toocomplete.</span></span>

<span data-ttu-id="88138-200">Parcourir l’application de centre d’appels Fabrikam toohello à l’aide des url hello de votre cluster : par exemple, *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="88138-200">Browse toohello Fabrikam Call Center application using hello url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="88138-201">Maintenant que vous avez placées dans des conteneurs et déployé la solution de centre d’appels Fabrikam hello, vous pouvez ouvrir hello [portail Azure] [ link-azure-portal] et voir l’application hello en cours d’exécution dans l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="88138-201">Now that you have containerized and deployed hello Fabrikam Call Center solution, you can open hello [Azure portal][link-azure-portal] and see hello application running in Service Fabric.</span></span> <span data-ttu-id="88138-202">application de hello tootry, ouvrez un navigateur web et accédez toohello des URL de votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88138-202">tootry hello application, open a web browser and go toohello URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88138-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="88138-203">Next steps</span></span>

<span data-ttu-id="88138-204">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="88138-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88138-205">Créer un projet Docker dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88138-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="88138-206">Mettre en conteneur une application existante</span><span class="sxs-lookup"><span data-stu-id="88138-206">Containerize an existing application</span></span>
> * <span data-ttu-id="88138-207">Configurer l’intégration continue avec Visual Studio et VSTS</span><span class="sxs-lookup"><span data-stu-id="88138-207">Setup continuous integration with Visual Studio and VSTS</span></span>

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
