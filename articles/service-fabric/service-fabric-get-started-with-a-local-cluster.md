---
title: "aaaDeploy et mettre à niveau microservices Azure localement | Documents Microsoft"
description: "Découvrez comment tooset configuration d’un cluster Service Fabric local, déployez un tooit d’application existant et puis mise à niveau de cette application."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="1d3d4-103">Prise en main avec le déploiement et la mise à niveau d’applications sur votre cluster local</span><span class="sxs-lookup"><span data-stu-id="1d3d4-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="1d3d4-104">Bonjour Azure Service Fabric SDK inclut un environnement de développement local complet que vous pouvez utiliser tooquickly prise en main déploiement et gestion des applications sur un cluster local.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-104">hello Azure Service Fabric SDK includes a full local development environment that you can use tooquickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="1d3d4-105">Dans cet article, vous créez un cluster local, déployez une tooit d’application existant et puis mettre à niveau cette version de nouvelle application tooa, à partir de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-105">In this article, you create a local cluster, deploy an existing application tooit, and then upgrade that application tooa new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="1d3d4-106">Cet article suppose que vous avez déjà [configuré votre environnement de développement](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1d3d4-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="1d3d4-107">Créer un cluster local</span><span class="sxs-lookup"><span data-stu-id="1d3d4-107">Create a local cluster</span></span>
<span data-ttu-id="1d3d4-108">Un cluster Service Fabric représente un ensemble de ressources matérielles sur lequel vous pouvez déployer des applications.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="1d3d4-109">En règle générale, un cluster est constitué de n’importe où à partir de cinq réduire des milliers d’ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-109">Typically, a cluster is made up of anywhere from five toomany thousands of machines.</span></span> <span data-ttu-id="1d3d4-110">Toutefois, hello Service Fabric SDK inclut une configuration de cluster pouvant s’exécuter sur un seul ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-110">However, hello Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="1d3d4-111">Il est important de toounderstand qui hello cluster local Service Fabric n’est pas un émulateur ou un simulateur.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-111">It is important toounderstand that hello Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="1d3d4-112">Il s’exécute hello même code de plate-forme qui se trouve sur des clusters comportant plusieurs ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-112">It runs hello same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="1d3d4-113">Hello seule différence est qu’elle s’exécute le processus de plateforme hello qui sont normalement réparties sur cinq ordinateurs sur un ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-113">hello only difference is that it runs hello platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="1d3d4-114">Hello SDK fournit deux façons tooset, configuration d’un cluster local : une Windows PowerShell script et hello Gestionnaire du Cluster Local système barre d’état d’application.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-114">hello SDK provides two ways tooset up a local cluster: a Windows PowerShell script and hello Local Cluster Manager system tray app.</span></span> <span data-ttu-id="1d3d4-115">Dans ce didacticiel, nous utilisons de script PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-115">In this tutorial, we use hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="1d3d4-116">Si vous avez déjà créé un cluster local en déployant une application depuis Visual Studio, vous pouvez ignorer cette section.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="1d3d4-117">Lancez une nouvelle fenêtre PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="1d3d4-118">Exécutez le script d’installation de cluster hello à partir du dossier du Kit de développement logiciel hello :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-118">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="1d3d4-119">L’installation du cluster prend quelques instants.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="1d3d4-120">Une fois l’installation terminée, vous devriez obtenir un résultat similaire à ceci :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Résultat de configuration du cluster][cluster-setup-success]
   
    <span data-ttu-id="1d3d4-122">Vous êtes maintenant prêt tootry déploiement d’un cluster de tooyour d’application.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-122">You are now ready tootry deploying an application tooyour cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="1d3d4-123">Déployer une application</span><span class="sxs-lookup"><span data-stu-id="1d3d4-123">Deploy an application</span></span>
<span data-ttu-id="1d3d4-124">Hello Service Fabric SDK comprend un ensemble complet des infrastructures et outils pour créer des applications de développeur.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-124">hello Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="1d3d4-125">Si vous souhaitez en savoir comment les applications toocreate dans Visual Studio, consultez [créer votre première application de Service Fabric dans Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="1d3d4-125">If you are interested in learning how toocreate applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="1d3d4-126">Dans ce didacticiel, vous utilisez un exemple d’application existant (appelé WordCount) afin de pouvoir vous concentrer sur les aspects de gestion hello de plateforme de hello : déploiement, la surveillance et la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on hello management aspects of hello platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="1d3d4-127">Lancez une nouvelle fenêtre PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="1d3d4-128">Importez le module de Service Fabric SDK PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-128">Import hello Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="1d3d4-129">Créez une application hello de toostore de répertoire que vous téléchargez et déployez, tels que C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-129">Create a directory toostore hello application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="1d3d4-130">[Télécharger l’application WordCount de hello](http://aka.ms/servicefabric-wordcountapp) emplacement toohello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-130">[Download hello WordCount application](http://aka.ms/servicefabric-wordcountapp) toohello location you created.</span></span>  <span data-ttu-id="1d3d4-131">Remarque : le navigateur Microsoft Edge de hello enregistre fichier hello avec un *.zip* extension.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-131">Note: hello Microsoft Edge browser saves hello file with a *.zip* extension.</span></span>  <span data-ttu-id="1d3d4-132">Changent d’extension de fichier hello*.sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-132">Change hello file extension too*.sfpkg*.</span></span>
5. <span data-ttu-id="1d3d4-133">Connecter le cluster local de toohello :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-133">Connect toohello local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="1d3d4-134">Créez une application à l’aide de la commande de déploiement du Kit de développement hello avec un nom et un package d’application toohello chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-134">Create a new application using hello SDK's deployment command with a name and a path toohello application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="1d3d4-135">Si tout se passe bien, vous devez voir hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-135">If all goes well, you should see hello following output:</span></span>
   
    ![Déployer un cluster local toohello d’application][deploy-app-to-local-cluster]
7. <span data-ttu-id="1d3d4-137">application de hello toosee en action, lancer hello navigateur et accédez trop[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="1d3d4-137">toosee hello application in action, launch hello browser and navigate too[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="1d3d4-138">Ce qui suit doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-138">You should see:</span></span>
   
    ![Interface utilisateur des applications déployées.][deployed-app-ui]
   
    <span data-ttu-id="1d3d4-140">Hello WordCount application est simple.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-140">hello WordCount application is simple.</span></span> <span data-ttu-id="1d3d4-141">Il inclut côté client JavaScript toogenerate aléatoire cinq caractères « mots », qui sont ensuite relayés application toohello via l’API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-141">It includes client-side JavaScript code toogenerate random five-character "words", which are then relayed toohello application via ASP.NET Web API.</span></span> <span data-ttu-id="1d3d4-142">Un service avec état effectue le suivi de nombre hello de mots comptabilisées.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-142">A stateful service tracks hello number of words counted.</span></span> <span data-ttu-id="1d3d4-143">Ils sont partitionnées selon hello premier caractère de mot de hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-143">They are partitioned based on hello first character of hello word.</span></span> <span data-ttu-id="1d3d4-144">Vous pouvez trouver le code source de hello pour application WordCount hello hello [classique route exemples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="1d3d4-144">You can find hello source code for hello WordCount app in hello [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="1d3d4-145">application Hello que nous avons déployé contient quatre partitions.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-145">hello application that we deployed contains four partitions.</span></span> <span data-ttu-id="1d3d4-146">Pour les mots qui commencent par A à G sont stockés dans la première partition de hello, mots qui commencent par H et N sont stockés dans hello deuxième partition et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-146">So words beginning with A through G are stored in hello first partition, words beginning with H through N are stored in hello second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="1d3d4-147">Afficher les détails et l’état de l’application</span><span class="sxs-lookup"><span data-stu-id="1d3d4-147">View application details and status</span></span>
<span data-ttu-id="1d3d4-148">Maintenant que nous avons déployé l’application hello, examinons certains détails de l’application hello dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-148">Now that we have deployed hello application, let's look at some of hello app details in PowerShell.</span></span>

1. <span data-ttu-id="1d3d4-149">Interroger toutes les applications déployées sur le cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-149">Query all deployed applications on hello cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="1d3d4-150">En supposant que vous avez uniquement hello WordCount application déployée, vous voyez quelque chose de similaire à :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-150">Assuming that you have only deployed hello WordCount app, you see something similar to:</span></span>
   
    ![Interroger toutes les applications déployées sur PowerShell :][ps-getsfapp]
2. <span data-ttu-id="1d3d4-152">Atteindre le niveau suivant de toohello en interrogeant l’ensemble de hello de services qui sont inclus dans l’application WordCount de hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-152">Go toohello next level by querying hello set of services that are included in hello WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Liste des services d’application hello dans PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="1d3d4-154">application Hello est constituée de deux services, hello serveur web frontal et le service avec état hello qui gère les mots hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-154">hello application is made up of two services, hello web front end, and hello stateful service that manages hello words.</span></span>
3. <span data-ttu-id="1d3d4-155">Enfin, recherchez liste hello de partitions WordCountService :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-155">Finally, look at hello list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Afficher les partitions de service hello dans PowerShell][ps-getsfpartitions]
   
    <span data-ttu-id="1d3d4-157">Hello ensemble de commandes que vous avez utilisé, comme toutes les commandes PowerShell de l’infrastructure de Service, sont disponibles pour n’importe quel cluster que vous pouvez vous connecter, local ou distant.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-157">hello set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="1d3d4-158">Pour un toointeract de manière plus visuelle avec cluster de hello, vous pouvez utiliser les outils Service Fabric Explorer hello web en naviguant trop[http://localhost:19080/Explorer](http://localhost:19080/Explorer) dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-158">For a more visual way toointeract with hello cluster, you can use hello web-based Service Fabric Explorer tool by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer) in hello browser.</span></span>
   
    ![Afficher les détails de l’application dans Fabric Service Explorer][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="1d3d4-160">toolearn en savoir plus sur le Service Fabric Explorer, consultez [visualiser votre cluster avec Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1d3d4-160">toolearn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="1d3d4-161">Mettre à niveau une application</span><span class="sxs-lookup"><span data-stu-id="1d3d4-161">Upgrade an application</span></span>
<span data-ttu-id="1d3d4-162">L’infrastructure de service fournit des mises à niveau sans temps mort en surveillant la santé de l’application hello hello comme il déploie sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-162">Service Fabric provides no-downtime upgrades by monitoring hello health of hello application as it rolls out across hello cluster.</span></span> <span data-ttu-id="1d3d4-163">Effectuer une mise à niveau de hello WordCount application.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-163">Perform an upgrade of hello WordCount application.</span></span>

<span data-ttu-id="1d3d4-164">Hello nouvelle version d’application hello maintenant compte uniquement les mots qui commencent par une voyelle.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-164">hello new version of hello application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="1d3d4-165">Comme la mise à niveau hello déploie des, nous voyons deux modifications de comportement de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-165">As hello upgrade rolls out, we see two changes in hello application's behavior.</span></span> <span data-ttu-id="1d3d4-166">Taux hello auquel augmente le nombre de hello doit tout d’abord, lent, étant donné que moins de mots sont comptabilisées.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-166">First, hello rate at which hello count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="1d3d4-167">En second lieu, étant donné que la première partition de hello possède deux voyelles (A et E), et toutes les autres partitions contient un seul chaque, son nombre doit finalement démarrer toooutpace hello d’autres.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-167">Second, since hello first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start toooutpace hello others.</span></span>

1. <span data-ttu-id="1d3d4-168">[Télécharger le package de version 2 WordCount hello](http://aka.ms/servicefabric-wordcountappv2) toohello même emplacement où vous avez téléchargé le package de version 1 hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-168">[Download hello WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) toohello same location where you downloaded hello version 1 package.</span></span>
2. <span data-ttu-id="1d3d4-169">Retourne la fenêtre de PowerShell tooyour et utilisez la commande de mise à niveau du Kit de développement hello tooregister hello la nouvelle version dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-169">Return tooyour PowerShell window and use hello SDK's upgrade command tooregister hello new version in hello cluster.</span></span> <span data-ttu-id="1d3d4-170">Commencez la mise à niveau de l’ensemble fibre optique hello : / WordCount application.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-170">Then begin upgrading hello fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="1d3d4-171">Vous devez voir hello sortie suivante dans PowerShell comme hello mise à niveau commence.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-171">You should see hello following output in PowerShell as hello upgrade begins.</span></span>
   
    ![Progression de la mise à niveau dans PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="1d3d4-173">Lors de la mise à niveau hello est continuer, il peut s’avérer plus facile toomonitor son état de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-173">While hello upgrade is proceeding, you may find it easier toomonitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="1d3d4-174">Lancez une fenêtre de navigateur et accédez trop[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="1d3d4-174">Launch a browser window and navigate too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="1d3d4-175">Développez **Applications** dans l’arborescence hello hello gauche, puis choisissez **WordCount**et enfin **fabric : / WordCount**.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-175">Expand **Applications** in hello tree on hello left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="1d3d4-176">Dans l’onglet d’essentials hello, vous voyez état hello de mise à niveau hello elle parcoure les domaines de mise à niveau du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-176">In hello essentials tab, you see hello status of hello upgrade as it proceeds through hello cluster's upgrade domains.</span></span>
   
    ![Progression de la mise à niveau dans Service Fabric Explorer][sfx-upgradeprogress]
   
    <span data-ttu-id="1d3d4-178">Comme la mise à niveau hello se poursuit dans chaque domaine, contrôles d’intégrité sont effectuée tooensure qui application hello se comporte correctement.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-178">As hello upgrade proceeds through each domain, health checks are performed tooensure that hello application is behaving properly.</span></span>
4. <span data-ttu-id="1d3d4-179">Si vous réexécutez hello précédemment de requête d’ensemble de hello de services dans l’ensemble fibre optique hello : / WordCount application, notez que hello version WordCountService modifiée mais hello WordCountWebService version n’a pas :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-179">If you rerun hello earlier query for hello set of services in hello fabric:/WordCount application, notice that hello WordCountService version changed but hello WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Services d’application de requête après mise à niveau][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="1d3d4-181">Cet exemple met en évidence la façon dont Service Fabric gère les mises à niveau d’application.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="1d3d4-182">Il touche uniquement hello ensemble de services (ou des packages de code/de configuration au sein de ces services) qui ont été modifiés, ce qui rend le processus de mise à niveau plus rapide et plus fiable de hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-182">It touches only hello set of services (or code/configuration packages within those services) that have changed, which makes hello process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="1d3d4-183">Enfin, retourner le comportement de hello toohello navigateur tooobserve version nouvelle de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-183">Finally, return toohello browser tooobserve hello behavior of hello new application version.</span></span> <span data-ttu-id="1d3d4-184">Comme prévu, hello nombre progresse plus lentement et partition de première hello se termine par légèrement plus du volume de hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-184">As expected, hello count progresses more slowly, and hello first partition ends up with slightly more of hello volume.</span></span>
   
    ![Vue hello nouvelle version de l’application hello dans le navigateur de hello][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="1d3d4-186">Nettoyage</span><span class="sxs-lookup"><span data-stu-id="1d3d4-186">Cleaning up</span></span>
<span data-ttu-id="1d3d4-187">Avant de conclure, il est important de tooremember qui hello cluster local est de type real.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-187">Before wrapping up, it's important tooremember that hello local cluster is real.</span></span> <span data-ttu-id="1d3d4-188">Applications continuent toorun en arrière-plan de hello jusqu'à ce que vous les supprimez.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-188">Applications continue toorun in hello background until you remove them.</span></span>  <span data-ttu-id="1d3d4-189">Selon la nature hello de vos applications, une application en cours d’exécution peut prendre des ressources importantes sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-189">Depending on hello nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="1d3d4-190">Vous avez plusieurs applications de toomanage options et cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-190">You have several options toomanage applications and hello cluster:</span></span>

1. <span data-ttu-id="1d3d4-191">tooremove une application individuelle et toutes ses données, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-191">tooremove an individual application and all it's data, run hello following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="1d3d4-192">Ou bien, supprimez l’application hello de hello Service Fabric Explorer **ACTIONS** un menu ou hello dans la vue de liste de gauche application hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-192">Or, delete hello application from hello Service Fabric Explorer **ACTIONS** menu or hello context menu in hello left-hand application list view.</span></span>
   
    ![Supprimer une application dans Service Fabric Explorer][sfe-delete-application]
2. <span data-ttu-id="1d3d4-194">Après avoir supprimé l’application hello du cluster de hello, annulez l’enregistrement de versions 1.0.0 et 2.0.0 Hello WordCount type d’application.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-194">After deleting hello application from hello cluster, unregister versions 1.0.0 and 2.0.0 of hello WordCount application type.</span></span> <span data-ttu-id="1d3d4-195">Suppression supprime les packages d’application hello, y compris le code de hello et la configuration, à partir du magasin d’images du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-195">Deletion removes hello application packages, including hello code and configuration, from hello cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="1d3d4-196">Ou, dans l’Explorateur de l’infrastructure de Service, choisissez **la mise hors service Type** pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for hello application.</span></span>
3. <span data-ttu-id="1d3d4-197">tooshut cluster de hello mais conserver les données application hello et traces, cliquez sur **arrêter le Cluster Local** dans l’application de barre d’état système hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-197">tooshut down hello cluster but keep hello application data and traces, click **Stop Local Cluster** in hello system tray app.</span></span>
4. <span data-ttu-id="1d3d4-198">est entièrement, cliquez sur cluster de hello toodelete **supprimer le Cluster Local** dans l’application de barre d’état système hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-198">toodelete hello cluster entirely, click **Remove Local Cluster** in hello system tray app.</span></span> <span data-ttu-id="1d3d4-199">Cette option entraîne une autre hello de déploiement lente prochaine fois que vous appuyez sur F5 dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-199">This option will result in another slow deployment hello next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="1d3d4-200">Supprimer cluster local de hello uniquement si vous n’envisagez pas toouse pendant un certain temps, ou si vous avez besoin des ressources de tooreclaim.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-200">Remove hello local cluster only if you don't intend toouse it for some time or if you need tooreclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="1d3d4-201">Modes de cluster un nœud et cinq nœuds</span><span class="sxs-lookup"><span data-stu-id="1d3d4-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="1d3d4-202">Lorsque vous développez des applications, vous êtes souvent amené à effectuer des itérations rapides d’écriture de code, de débogage, de modification de code et de débogage.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="1d3d4-203">toohelp optimiser ce processus, le cluster local de hello peut exécuter dans deux modes : un nœud ou cinq nœuds.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-203">toohelp optimize this process, hello local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="1d3d4-204">Ces deux modes de cluster présentent chacun des avantages.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="1d3d4-205">Cinq nœuds permet de toowork avec un cluster réel.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-205">Five-node cluster mode enables you toowork with a real cluster.</span></span> <span data-ttu-id="1d3d4-206">Vous pouvez tester des scénarios de basculement, et travailler avec un plus grand nombre d’instances et de réplicas de vos services.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="1d3d4-207">Un nœud est un déploiement rapide toodo optimisé et l’inscription des services, toohelp vous validez rapidement le code à l’aide du runtime de Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-207">One-node cluster mode is optimized toodo quick deployment and registration of services, toohelp you quickly validate code using hello Service Fabric runtime.</span></span>

<span data-ttu-id="1d3d4-208">Ni le mode de cluster un nœud, ni le mode de cluster cinq nœuds ne constituent un émulateur ou un simulateur.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="1d3d4-209">cluster de développement local Hello exécute hello même code de plate-forme qui se trouve sur des clusters comportant plusieurs ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-209">hello local development cluster runs hello same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="1d3d4-210">Lorsque vous modifiez le mode de cluster hello, le cluster actuel hello est supprimé de votre système et un nouveau cluster est créé.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-210">When you change hello cluster mode, hello current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="1d3d4-211">données Hello stockées dans un cluster de hello sont supprimées lorsque vous modifiez le mode de cluster.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-211">hello data stored in hello cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="1d3d4-212">toochange hello mode tooone cluster à nœud, sélectionnez **le Mode Cluster** Bonjour Gestionnaire du Cluster Service Fabric Local.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-212">toochange hello mode tooone-node cluster, select **Switch Cluster Mode** in hello Service Fabric Local Cluster Manager.</span></span>

![Changer de mode de cluster][switch-cluster-mode]

<span data-ttu-id="1d3d4-214">Ou bien, modifier le mode de cluster hello à l’aide de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-214">Or, change hello cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="1d3d4-215">Lancez une nouvelle fenêtre PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="1d3d4-216">Exécutez le script d’installation de cluster hello à partir du dossier du Kit de développement logiciel hello :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-216">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="1d3d4-217">L’installation du cluster prend quelques instants.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="1d3d4-218">Une fois l’installation terminée, vous devriez obtenir un résultat similaire à ceci :</span><span class="sxs-lookup"><span data-stu-id="1d3d4-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Résultat de configuration du cluster][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="1d3d4-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1d3d4-220">Next steps</span></span>
* <span data-ttu-id="1d3d4-221">Maintenant que vous avez déployé et mis à niveau certaines des applications pré intégrées, vous pouvez [Réessayer de générer les vôtres dans Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="1d3d4-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="1d3d4-222">Toutes les actions de hello effectuées sur le cluster local de hello dans cet article peuvent être effectuées sur un [cluster Azure](service-fabric-cluster-creation-via-portal.md) également.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-222">All hello actions performed on hello local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="1d3d4-223">mise à niveau de Hello que nous avons effectué dans cet article a été base.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-223">hello upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="1d3d4-224">Consultez hello [mise à niveau de la documentation](service-fabric-application-upgrade.md) toolearn plus d’informations sur la puissance de hello et la flexibilité de mises à niveau de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1d3d4-224">See hello [upgrade documentation](service-fabric-application-upgrade.md) toolearn more about hello power and flexibility of Service Fabric upgrades.</span></span>

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
