---
title: "aaaDeploy un tooAzure exécutable existant Service Fabric | Documents Microsoft"
description: "Procédure pas à pas sur comment toopackage une application existante en tant qu’invité exécutable, il peut être déployé cluster Service Fabric de tooa"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a><span data-ttu-id="17d68-103">Déployer une infrastructure de tooService exécutable invité</span><span class="sxs-lookup"><span data-stu-id="17d68-103">Deploy a guest executable tooService Fabric</span></span>
<span data-ttu-id="17d68-104">Vous pouvez exécuter n’importe quel type de code, comme Node.js, Java ou C++ dans Azure Service Fabric en tant que service.</span><span class="sxs-lookup"><span data-stu-id="17d68-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="17d68-105">Service Fabric fait référence à des types de toothese de services en tant qu’invité exécutables.</span><span class="sxs-lookup"><span data-stu-id="17d68-105">Service Fabric refers toothese types of services as guest executables.</span></span>

<span data-ttu-id="17d68-106">Les invités exécutables sont traités par le Service Fabric comme des services sans état.</span><span class="sxs-lookup"><span data-stu-id="17d68-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="17d68-107">En conséquence, ils sont placés dans des nœuds dans un cluster, sur la base de la disponibilité et d’autres mesures.</span><span class="sxs-lookup"><span data-stu-id="17d68-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="17d68-108">Cet article décrit comment toopackage et déployer un cluster Service Fabric de tooa exécutable invité, à l’aide de Visual Studio ou un utilitaire de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="17d68-108">This article describes how toopackage and deploy a guest executable tooa Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="17d68-109">Dans cet article, nous couvrir hello étapes toopackage exécutable invité et déployez-le tooService l’ensemble fibre optique.</span><span class="sxs-lookup"><span data-stu-id="17d68-109">In this article, we cover hello steps toopackage a guest executable and deploy it tooService Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="17d68-110">Avantages de l'exécution d'un exécutable invité dans Service Fabric</span><span class="sxs-lookup"><span data-stu-id="17d68-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="17d68-111">Il existe plusieurs avantages toorunning invité exécutable dans un cluster Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="17d68-111">There are several advantages toorunning a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="17d68-112">Haute disponibilité :</span><span class="sxs-lookup"><span data-stu-id="17d68-112">High availability.</span></span> <span data-ttu-id="17d68-113">Les applications qui sont exécutées dans Service Fabric sont hautement disponibles.</span><span class="sxs-lookup"><span data-stu-id="17d68-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="17d68-114">Service Fabric s’assure que les instances d’une application sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="17d68-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="17d68-115">Analyse du fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="17d68-115">Health monitoring.</span></span> <span data-ttu-id="17d68-116">La fonction d’analyse du fonctionnement de Service Fabric détecte si une application est en cours d’exécution et fournit des informations de diagnostic en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="17d68-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="17d68-117">Gestion du cycle de vie des applications.</span><span class="sxs-lookup"><span data-stu-id="17d68-117">Application lifecycle management.</span></span> <span data-ttu-id="17d68-118">Outre les mises à niveau sans interruption de service, Service Fabric fournit la version précédente de la restauration automatique toohello s’il existe un événement fonctionnent-elles signalé pendant une mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="17d68-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback toohello previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="17d68-119">Densité.</span><span class="sxs-lookup"><span data-stu-id="17d68-119">Density.</span></span> <span data-ttu-id="17d68-120">Vous pouvez exécuter plusieurs applications dans un cluster, ce qui évite de hello pour chaque toorun application sur son propre matériel.</span><span class="sxs-lookup"><span data-stu-id="17d68-120">You can run multiple applications in a cluster, which eliminates hello need for each application toorun on its own hardware.</span></span>
* <span data-ttu-id="17d68-121">Découverte : À l’aide de REST vous pouvez appeler hello Service Fabric Naming service toofind autres services dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-121">Discoverability: Using REST you can call hello Service Fabric Naming service toofind other services in hello cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="17d68-122">Exemples</span><span class="sxs-lookup"><span data-stu-id="17d68-122">Samples</span></span>
* [<span data-ttu-id="17d68-123">Exemple pour empaqueter et déployer un fichier exécutable invité</span><span class="sxs-lookup"><span data-stu-id="17d68-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="17d68-124">Exemple de l’invité deux exécutables (c# et nodejs) communique via le service d’affectation de noms de hello à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="17d68-124">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="17d68-125">Vue d’ensemble des fichiers du manifeste de service et d’application</span><span class="sxs-lookup"><span data-stu-id="17d68-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="17d68-126">Dans le cadre du déploiement d’un exécutable invité, il est modèle de déploiement et d’empaquetage de Service Fabric hello toounderstand utile comme décrit dans [modèle d’application](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="17d68-126">As part of deploying a guest executable, it is useful toounderstand hello Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="17d68-127">le modèle de packaging Hello Service Fabric s’appuie sur deux fichiers XML : hello manifestes d’application et des services.</span><span class="sxs-lookup"><span data-stu-id="17d68-127">hello Service Fabric packaging model relies on two XML files: hello application and service manifests.</span></span> <span data-ttu-id="17d68-128">Hello définition de schéma pour les fichiers ApplicationManifest.xml et ServiceManifest.xml hello est installé avec hello SDK de l’infrastructure de Service en *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="17d68-128">hello schema definition for hello ApplicationManifest.xml and ServiceManifest.xml files is installed with hello Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="17d68-129">**Manifeste d’application** manifeste de l’application hello est utilisé toodescribe hello application.</span><span class="sxs-lookup"><span data-stu-id="17d68-129">**Application manifest** hello application manifest is used toodescribe hello application.</span></span> <span data-ttu-id="17d68-130">Il répertorie les services hello qui le composent et autres paramètres qui sont utilisé toodefine comment un ou plusieurs services doivent être déployés, telles que nombre hello d’instances.</span><span class="sxs-lookup"><span data-stu-id="17d68-130">It lists hello services that compose it, and other parameters that are used toodefine how one or more services should be deployed, such as hello number of instances.</span></span>

  <span data-ttu-id="17d68-131">Dans Service Fabric, une application est une unité de déploiement et de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="17d68-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="17d68-132">Une application peut être mise à niveau en tant qu’unité simple, dans laquelle les défaillances (et restaurations) potentielles sont gérées.</span><span class="sxs-lookup"><span data-stu-id="17d68-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="17d68-133">L’infrastructure de service garantit que le processus de mise à niveau hello est soit réussi, sinon, si la mise à niveau hello échoue, ne laissez pas application hello dans un état inconnu ou instable.</span><span class="sxs-lookup"><span data-stu-id="17d68-133">Service Fabric guarantees that hello upgrade process is either successful, or, if hello upgrade fails, does not leave hello application in an unknown or unstable state.</span></span>
* <span data-ttu-id="17d68-134">**Manifeste de service** manifeste de service hello décrit les composants de hello d’un service.</span><span class="sxs-lookup"><span data-stu-id="17d68-134">**Service manifest** hello service manifest describes hello components of a service.</span></span> <span data-ttu-id="17d68-135">Il inclut des données, telles que le nom de hello et le type de service et son code et la configuration.</span><span class="sxs-lookup"><span data-stu-id="17d68-135">It includes data, such as hello name and type of service, and its code and configuration.</span></span> <span data-ttu-id="17d68-136">Hello manifeste de service inclut également des paramètres supplémentaires qui peuvent être utilisées de service de hello tooconfigure une fois qu’il est déployé.</span><span class="sxs-lookup"><span data-stu-id="17d68-136">hello service manifest also includes some additional parameters that can be used tooconfigure hello service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="17d68-137">Structure de fichier d'un package d'application</span><span class="sxs-lookup"><span data-stu-id="17d68-137">Application package file structure</span></span>
<span data-ttu-id="17d68-138">toodeploy un tooService d’application Fabric, l’application hello doit suivre une structure de répertoire prédéfini.</span><span class="sxs-lookup"><span data-stu-id="17d68-138">toodeploy an application tooService Fabric, hello application should follow a predefined directory structure.</span></span> <span data-ttu-id="17d68-139">Hello Voici un exemple de cette structure.</span><span class="sxs-lookup"><span data-stu-id="17d68-139">hello following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="17d68-140">Hello ApplicationPackageRoot contient le fichier ApplicationManifest.xml hello qui définit l’application hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-140">hello ApplicationPackageRoot contains hello ApplicationManifest.xml file that defines hello application.</span></span> <span data-ttu-id="17d68-141">Un sous-répertoire pour chaque service inclus dans l’application hello est utilisé toocontain tous hello artefacts hello service requiert.</span><span class="sxs-lookup"><span data-stu-id="17d68-141">A subdirectory for each service included in hello application is used toocontain all hello artifacts that hello service requires.</span></span> <span data-ttu-id="17d68-142">Ces sous-répertoires sont hello ServiceManifest.xml et, en règle générale, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="17d68-142">These subdirectories are hello ServiceManifest.xml and, typically, hello following:</span></span>

* <span data-ttu-id="17d68-143">*Code*.</span><span class="sxs-lookup"><span data-stu-id="17d68-143">*Code*.</span></span> <span data-ttu-id="17d68-144">Ce répertoire contient un code de service hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-144">This directory contains hello service code.</span></span>
* <span data-ttu-id="17d68-145">*Config*. Ce répertoire contient un fichier Settings.xml (et autres fichiers si nécessaire) que les service de hello peut accéder à des paramètres de configuration spécifiques tooretrieve runtime.</span><span class="sxs-lookup"><span data-stu-id="17d68-145">*Config*. This directory contains a Settings.xml file (and other files if necessary) that hello service can access at runtime tooretrieve specific configuration settings.</span></span>
* <span data-ttu-id="17d68-146">*Data*.</span><span class="sxs-lookup"><span data-stu-id="17d68-146">*Data*.</span></span> <span data-ttu-id="17d68-147">Il s’agit d’une annuaire supplémentaire toostore local des données supplémentaires qui hello service peut avoir besoin.</span><span class="sxs-lookup"><span data-stu-id="17d68-147">This is an additional directory toostore additional local data that hello service may need.</span></span> <span data-ttu-id="17d68-148">Données doivent être les données uniquement éphémère toostore utilisé.</span><span class="sxs-lookup"><span data-stu-id="17d68-148">Data should be used toostore only ephemeral data.</span></span> <span data-ttu-id="17d68-149">L’infrastructure de service effectue pas de copie ou de la réplication du répertoire de données modifications toohello si le service de hello doit toobe déplacée (par exemple, pendant le basculement).</span><span class="sxs-lookup"><span data-stu-id="17d68-149">Service Fabric does not copy or replicate changes toohello data directory if hello service needs toobe relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="17d68-150">Vous n’avez pas toocreate hello `config` et `data` si vous n’en avez pas besoin de répertoires.</span><span class="sxs-lookup"><span data-stu-id="17d68-150">You don't have toocreate hello `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="17d68-151">Empaqueter un exécutable existant</span><span class="sxs-lookup"><span data-stu-id="17d68-151">Package an existing executable</span></span>
<span data-ttu-id="17d68-152">Lors de l’empaquetage d’un exécutable invité, vous pouvez choisir soit toouse un modèle de projet Visual Studio ou trop[créer le package d’application hello manuellement](#manually).</span><span class="sxs-lookup"><span data-stu-id="17d68-152">When packaging a guest executable, you can choose either toouse a Visual Studio project template or too[create hello application package manually](#manually).</span></span> <span data-ttu-id="17d68-153">À l’aide de Visual Studio, hello structure de package d’application et les fichiers manifeste sont créés par le nouveau modèle de projet hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="17d68-153">Using Visual Studio, hello application package structure and manifest files are created by hello new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="17d68-154">toopackage de façon plus simple Hello un exécutable dans un service de Windows existant est toouse Visual Studio et sur Linux toouse Yeoman</span><span class="sxs-lookup"><span data-stu-id="17d68-154">hello easiest way toopackage an existing Windows executable into a service is toouse Visual Studio and on Linux toouse Yeoman</span></span>
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a><span data-ttu-id="17d68-155">Utilisez Visual Studio toopackage et déployer un fichier exécutable existant</span><span class="sxs-lookup"><span data-stu-id="17d68-155">Use Visual Studio toopackage and deploy an existing executable</span></span>
<span data-ttu-id="17d68-156">Visual Studio fournit une infrastructure de Service toohelp de modèle de service vous déployez un cluster Service Fabric de tooa exécutable invité.</span><span class="sxs-lookup"><span data-stu-id="17d68-156">Visual Studio provides a Service Fabric service template toohelp you deploy a guest executable tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="17d68-157">Sélectionnez **Fichier** > **Nouveau projet** pour créer une application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="17d68-157">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="17d68-158">Choisissez **exécutable invité** comme modèle de service hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-158">Choose **Guest Executable** as hello service template.</span></span>
3. <span data-ttu-id="17d68-159">Cliquez sur **Parcourir** dossier de hello tooselect avec votre fichier exécutable et le remplissage reste hello du service de hello paramètres toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-159">Click **Browse** tooselect hello folder with your executable and fill in hello rest of hello parameters toocreate hello service.</span></span>
   * <span data-ttu-id="17d68-160">*Comportement du package de code*.</span><span class="sxs-lookup"><span data-stu-id="17d68-160">*Code Package Behavior*.</span></span> <span data-ttu-id="17d68-161">Peut être ensemble toocopy tout le contenu de votre projet de Visual Studio, de toohello dossier hello qui est utile si hello exécutable ne change pas.</span><span class="sxs-lookup"><span data-stu-id="17d68-161">Can be set toocopy all hello content of your folder toohello Visual Studio Project, which is useful if hello executable does not change.</span></span> <span data-ttu-id="17d68-162">Si vous prévoyez toochange d’exécutable hello et que vous souhaitez toopick de capacité hello des nouvelles builds dynamiquement, vous pouvez choisir toolink toohello dossier à la place.</span><span class="sxs-lookup"><span data-stu-id="17d68-162">If you expect hello executable toochange and want hello ability toopick up new builds dynamically, you can choose toolink toohello folder instead.</span></span> <span data-ttu-id="17d68-163">Vous pouvez utiliser des dossiers liés lors de la création du projet d’application hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17d68-163">You can use linked folders when creating hello application project in Visual Studio.</span></span> <span data-ttu-id="17d68-164">Cette opération lie toohello source emplacement au sein du projet hello, donnant aux invités hello tooupdate exécutable dans la destination de la source.</span><span class="sxs-lookup"><span data-stu-id="17d68-164">This links toohello source location from within hello project, making it possible for you tooupdate hello guest executable in its source destination.</span></span> <span data-ttu-id="17d68-165">Ces mises à jour font partie du package d’application hello lors de la build.</span><span class="sxs-lookup"><span data-stu-id="17d68-165">Those updates become part of hello application package on build.</span></span>
   * <span data-ttu-id="17d68-166">*Programme* spécifie hello exécutable qui doit être exécutée de service de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="17d68-166">*Program* specifies hello executable that should be run toostart hello service.</span></span>
   * <span data-ttu-id="17d68-167">*Arguments* spécifie les arguments hello qui doivent être passés toohello exécutable.</span><span class="sxs-lookup"><span data-stu-id="17d68-167">*Arguments* specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="17d68-168">Il peut s’agir d’une liste de paramètres avec des arguments.</span><span class="sxs-lookup"><span data-stu-id="17d68-168">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="17d68-169">*WorkingFolder* Spécifie le répertoire de travail hello pour les processus hello qui sont en train de toobe a démarré.</span><span class="sxs-lookup"><span data-stu-id="17d68-169">*WorkingFolder* specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="17d68-170">Vous pouvez spécifier trois valeurs :</span><span class="sxs-lookup"><span data-stu-id="17d68-170">You can specify three values:</span></span>
     * <span data-ttu-id="17d68-171">`CodeBase`Spécifie le répertoire de travail que hello est en train de toobe définir le répertoire de code toohello dans le package d’application hello (`Code` répertoire Bonjour précédant la structure de fichiers).</span><span class="sxs-lookup"><span data-stu-id="17d68-171">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="17d68-172">`CodePackage`Spécifie le répertoire de travail que hello est en train de toobe définir racine toohello du package d’application hello (`GuestService1Pkg` illustré hello précédant la structure de fichiers).</span><span class="sxs-lookup"><span data-stu-id="17d68-172">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="17d68-173">`Work`Spécifie que les fichiers de hello sont placés dans un sous-répertoire appelé travail.</span><span class="sxs-lookup"><span data-stu-id="17d68-173">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="17d68-174">Donnez un nom à votre service et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="17d68-174">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="17d68-175">Si votre service a besoin d’un point de terminaison pour la communication, vous pouvez maintenant ajouter hello protocole, port et fichier de type toohello ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="17d68-175">If your service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="17d68-176">Par exemple : `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="17d68-176">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="17d68-177">Vous pouvez maintenant utiliser hello package et action de publication sur votre cluster local en déboguant solution hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17d68-177">You can now use hello package and publish action against your local cluster by debugging hello solution in Visual Studio.</span></span> <span data-ttu-id="17d68-178">Lorsque vous êtes prêt, vous pouvez publier le cluster de l’application hello tooa à distance ou archiver hello solution toosource contrôle.</span><span class="sxs-lookup"><span data-stu-id="17d68-178">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span>
7. <span data-ttu-id="17d68-179">Aller à la fin de toohello de toosee de cet article comment tooview votre service exécutable invité en cours d’exécution dans le Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="17d68-179">Go toohello end of this article toosee how tooview your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="17d68-180">Utilisez Yoeman toopackage et déployer un exécutable existant sur Linux</span><span class="sxs-lookup"><span data-stu-id="17d68-180">Use Yoeman toopackage and deploy an existing executable on Linux</span></span>

<span data-ttu-id="17d68-181">procédure de Hello pour créer et déployer un invité exécutable sur Linux est hello même que le déploiement d’une application csharp ou java.</span><span class="sxs-lookup"><span data-stu-id="17d68-181">hello procedure for creating and deploying a guest executable on Linux is hello same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="17d68-182">Saisissez `yo azuresfguest` dans un terminal.</span><span class="sxs-lookup"><span data-stu-id="17d68-182">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="17d68-183">Donnez un nom à votre application.</span><span class="sxs-lookup"><span data-stu-id="17d68-183">Name your application.</span></span>
3. <span data-ttu-id="17d68-184">Nom de votre service et fournissent des détails de hello, y compris le chemin d’accès du fichier exécutable de hello et elle doit être appelée avec des paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-184">Name your service, and provide hello details including path of hello executable and hello parameters it must be invoked with.</span></span>

<span data-ttu-id="17d68-185">Yeoman crée un package d’application avec l’application appropriée hello et les fichiers manifeste avec installer et désinstaller des scripts.</span><span class="sxs-lookup"><span data-stu-id="17d68-185">Yeoman creates an application package with hello appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="17d68-186">Empaqueter et déployer manuellement d’un exécutable existant</span><span class="sxs-lookup"><span data-stu-id="17d68-186">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="17d68-187">processus Hello de l’empaquetage d’un exécutable invité manuellement est basée sur hello général comme suit :</span><span class="sxs-lookup"><span data-stu-id="17d68-187">hello process of manually packaging a guest executable is based on hello following general steps:</span></span>

1. <span data-ttu-id="17d68-188">Créer la structure de répertoire du package hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-188">Create hello package directory structure.</span></span>
2. <span data-ttu-id="17d68-189">Ajouter des fichiers de code et la configuration de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-189">Add hello application's code and configuration files.</span></span>
3. <span data-ttu-id="17d68-190">Modifiez le fichier de manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-190">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="17d68-191">Modifier le fichier manifeste d’application hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-191">Edit hello application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a><span data-ttu-id="17d68-192">Créer la structure de répertoire du package hello</span><span class="sxs-lookup"><span data-stu-id="17d68-192">Create hello package directory structure</span></span>
<span data-ttu-id="17d68-193">Commencez par créer la structure de répertoire hello, comme décrit dans hello précédant la section, « Structure de fichier de package Application ».</span><span class="sxs-lookup"><span data-stu-id="17d68-193">You can start by creating hello directory structure, as described in hello preceding section, "Application package file structure."</span></span>

### <a name="add-hello-applications-code-and-configuration-files"></a><span data-ttu-id="17d68-194">Ajouter des fichiers de code et la configuration de l’application hello</span><span class="sxs-lookup"><span data-stu-id="17d68-194">Add hello application's code and configuration files</span></span>
<span data-ttu-id="17d68-195">Une fois que vous avez créé la structure de répertoire hello, vous pouvez ajouter des fichiers de code et la configuration de l’application hello sous les répertoires de code et de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-195">After you have created hello directory structure, you can add hello application's code and configuration files under hello code and config directories.</span></span> <span data-ttu-id="17d68-196">Vous pouvez également créer des répertoires supplémentaires ou des sous-répertoires dans les répertoires de code ou la configuration hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-196">You can also create additional directories or subdirectories under hello code or config directories.</span></span>

<span data-ttu-id="17d68-197">Service Fabric est un `xcopy` de contenu hello hello répertoire racine d’application, il n’existe aucun toouse structure prédéfinie autre que la création de deux répertoires supérieur, les codes et les paramètres.</span><span class="sxs-lookup"><span data-stu-id="17d68-197">Service Fabric does an `xcopy` of hello content of hello application root directory, so there is no predefined structure toouse other than creating two top directories, code and settings.</span></span> <span data-ttu-id="17d68-198">(Vous pouvez choisir des noms différents si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="17d68-198">(You can pick different names if you want.</span></span> <span data-ttu-id="17d68-199">Plus de détails sont dans la section suivante de hello.)</span><span class="sxs-lookup"><span data-stu-id="17d68-199">More details are in hello next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="17d68-200">Assurez-vous que vous incluez tous les fichiers de hello et les dépendances qui hello les besoins de l’application.</span><span class="sxs-lookup"><span data-stu-id="17d68-200">Make sure that you include all hello files and dependencies that hello application needs.</span></span> <span data-ttu-id="17d68-201">Service Fabric copie hello contenu du package d’application hello sur tous les nœuds de cluster hello où les services de l’application hello sont toobe continu déployé.</span><span class="sxs-lookup"><span data-stu-id="17d68-201">Service Fabric copies hello content of hello application package on all nodes in hello cluster where hello application's services are going toobe deployed.</span></span> <span data-ttu-id="17d68-202">package de Hello doit contenir tout code hello qu’application hello doit toorun.</span><span class="sxs-lookup"><span data-stu-id="17d68-202">hello package should contain all hello code that hello application needs toorun.</span></span> <span data-ttu-id="17d68-203">Ne supposez pas que les dépendances de hello sont déjà installés.</span><span class="sxs-lookup"><span data-stu-id="17d68-203">Do not assume that hello dependencies are already installed.</span></span>
>
>

### <a name="edit-hello-service-manifest-file"></a><span data-ttu-id="17d68-204">Modifier le fichier manifeste de service hello</span><span class="sxs-lookup"><span data-stu-id="17d68-204">Edit hello service manifest file</span></span>
<span data-ttu-id="17d68-205">étape suivante de Hello est hello tooedit hello service fichier manifeste tooinclude informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="17d68-205">hello next step is tooedit hello service manifest file tooinclude hello following information:</span></span>

* <span data-ttu-id="17d68-206">nom Hello hello du type de service.</span><span class="sxs-lookup"><span data-stu-id="17d68-206">hello name of hello service type.</span></span> <span data-ttu-id="17d68-207">Il s’agit d’un ID que le Service Fabric utilise tooidentify un service.</span><span class="sxs-lookup"><span data-stu-id="17d68-207">This is an ID that Service Fabric uses tooidentify a service.</span></span>
* <span data-ttu-id="17d68-208">commande toouse toolaunch hello application Hello (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="17d68-208">hello command toouse toolaunch hello application (ExeHost).</span></span>
* <span data-ttu-id="17d68-209">N’importe quel script qui doit tooset toobe exécuter l’application hello (SetupEntrypoint).</span><span class="sxs-lookup"><span data-stu-id="17d68-209">Any script that needs toobe run tooset up hello application (SetupEntrypoint).</span></span>

<span data-ttu-id="17d68-210">Hello Voici un exemple d’un `ServiceManifest.xml` fichier :</span><span class="sxs-lookup"><span data-stu-id="17d68-210">hello following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="17d68-211">Hello les sections suivantes accédez hello différentes parties du fichier hello que vous avez besoin de tooupdate.</span><span class="sxs-lookup"><span data-stu-id="17d68-211">hello following sections go over hello different parts of hello file that you need tooupdate.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="17d68-212">Mettre à jour ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="17d68-212">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="17d68-213">Vous pouvez choisir n’importe quel nom pour `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="17d68-213">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="17d68-214">valeur de Hello est utilisée dans hello `ApplicationManifest.xml` tooidentify hello service de fichiers.</span><span class="sxs-lookup"><span data-stu-id="17d68-214">hello value is used in hello `ApplicationManifest.xml` file tooidentify hello service.</span></span>
* <span data-ttu-id="17d68-215">Spécifiez `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="17d68-215">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="17d68-216">Cet attribut indique à Service Fabric que service de hello est basé sur une application autonome, par conséquent, tous les Service Fabric doit toodo est toolaunch sous la forme d’un processus et d’analyser son intégrité.</span><span class="sxs-lookup"><span data-stu-id="17d68-216">This attribute tells Service Fabric that hello service is based on a self-contained app, so all Service Fabric needs toodo is toolaunch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="17d68-217">Mettre à jour CodePackage</span><span class="sxs-lookup"><span data-stu-id="17d68-217">Update CodePackage</span></span>
<span data-ttu-id="17d68-218">Hello CodePackage élément indique les emplacement hello (version) de hello du code.</span><span class="sxs-lookup"><span data-stu-id="17d68-218">hello CodePackage element specifies hello location (and version) of hello service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="17d68-219">Hello `Name` élément désigne toospecify utilisé hello du répertoire hello dans le package d’application hello qui contient le code du service hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-219">hello `Name` element is used toospecify hello name of hello directory in hello application package that contains hello service's code.</span></span> <span data-ttu-id="17d68-220">`CodePackage`a également hello `version` attribut.</span><span class="sxs-lookup"><span data-stu-id="17d68-220">`CodePackage` also has hello `version` attribute.</span></span> <span data-ttu-id="17d68-221">Cela peut être utilisé toospecify hello version de hello code et peut également être utilisé tooupgrade hello du code à l’aide d’infrastructure de gestion du cycle de vie hello application Service fabric.</span><span class="sxs-lookup"><span data-stu-id="17d68-221">This can be used toospecify hello version of hello code, and can also potentially be used tooupgrade hello service's code by using hello application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="17d68-222">Facultatif : mettre à jour SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="17d68-222">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="17d68-223">élément de SetupEntryPoint Hello est toospecify utilisée n’importe quel fichier exécutable ou un lot qui doit être exécutée avant de lancer hello du code.</span><span class="sxs-lookup"><span data-stu-id="17d68-223">hello SetupEntryPoint element is used toospecify any executable or batch file that should be executed before hello service's code is launched.</span></span> <span data-ttu-id="17d68-224">Il est une étape facultative, donc il n’a pas besoin de toobe incluse si aucune initialisation n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="17d68-224">It is an optional step, so it does not need toobe included if there is no initialization required.</span></span> <span data-ttu-id="17d68-225">Hello SetupEntryPoint est exécutée chaque fois que le service de hello est redémarré.</span><span class="sxs-lookup"><span data-stu-id="17d68-225">hello SetupEntryPoint is executed every time hello service is restarted.</span></span>

<span data-ttu-id="17d68-226">Il est SetupEntryPoint qu’un seul, donc pas besoin de scripts d’installation toobe regroupé dans un fichier de commandes même si le programme d’installation de l’application hello requiert plusieurs scripts.</span><span class="sxs-lookup"><span data-stu-id="17d68-226">There is only one SetupEntryPoint, so setup scripts need toobe grouped in a single batch file if hello application's setup requires multiple scripts.</span></span> <span data-ttu-id="17d68-227">Hello SetupEntryPoint peut exécuter n’importe quel type de fichier : fichiers exécutables, les fichiers de commandes et les applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17d68-227">hello SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="17d68-228">Pour en savoir plus, consultez la rubrique relative à la [configuration de l’élément SetupEntryPoint](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="17d68-228">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="17d68-229">Bonjour précédent exemple, hello SetupEntryPoint exécute un fichier de commandes appelé `LaunchConfig.cmd` qui est situé dans hello `scripts` sous-répertoire du répertoire de code hello (en supposant que hello WorkingFolder a la valeur tooCodeBase).</span><span class="sxs-lookup"><span data-stu-id="17d68-229">In hello preceding example, hello SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in hello `scripts` subdirectory of hello code directory (assuming hello WorkingFolder element is set tooCodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="17d68-230">Mettre à jour EntryPoint</span><span class="sxs-lookup"><span data-stu-id="17d68-230">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="17d68-231">Hello `EntryPoint` élément dans le fichier manifeste de service hello est utilisé toospecify comment service hello de toolaunch.</span><span class="sxs-lookup"><span data-stu-id="17d68-231">hello `EntryPoint` element in hello service manifest file is used toospecify how toolaunch hello service.</span></span> <span data-ttu-id="17d68-232">Hello `ExeHost` élément spécifie hello exécutable (et arguments) qui doit être utilisé toolaunch hello service.</span><span class="sxs-lookup"><span data-stu-id="17d68-232">hello `ExeHost` element specifies hello executable (and arguments) that should be used toolaunch hello service.</span></span>

* <span data-ttu-id="17d68-233">`Program`Spécifie le nom hello du fichier exécutable hello qui doit démarrer hello service.</span><span class="sxs-lookup"><span data-stu-id="17d68-233">`Program` specifies hello name of hello executable that should start hello service.</span></span>
* <span data-ttu-id="17d68-234">`Arguments`Spécifie les arguments hello qui doivent être passés toohello exécutable.</span><span class="sxs-lookup"><span data-stu-id="17d68-234">`Arguments` specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="17d68-235">Il peut s’agir d’une liste de paramètres avec des arguments.</span><span class="sxs-lookup"><span data-stu-id="17d68-235">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="17d68-236">`WorkingFolder`Spécifie le répertoire de travail hello pour les processus hello qui sont en train de toobe a démarré.</span><span class="sxs-lookup"><span data-stu-id="17d68-236">`WorkingFolder` specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="17d68-237">Vous pouvez spécifier trois valeurs :</span><span class="sxs-lookup"><span data-stu-id="17d68-237">You can specify three values:</span></span>
  * <span data-ttu-id="17d68-238">`CodeBase`Spécifie le répertoire de travail que hello est en train de toobe définir le répertoire de code toohello dans le package d’application hello (`Code` répertoire hello précédant la structure de fichiers).</span><span class="sxs-lookup"><span data-stu-id="17d68-238">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory in hello preceding file structure).</span></span>
  * <span data-ttu-id="17d68-239">`CodePackage`Spécifie le répertoire de travail que hello est en train de toobe définir racine toohello du package d’application hello (`GuestService1Pkg` Bonjour précédant la structure de fichiers).</span><span class="sxs-lookup"><span data-stu-id="17d68-239">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` in hello preceding file structure).</span></span>
    * <span data-ttu-id="17d68-240">`Work`Spécifie que les fichiers de hello sont placés dans un sous-répertoire appelé travail.</span><span class="sxs-lookup"><span data-stu-id="17d68-240">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="17d68-241">Hello WorkingFolder est le répertoire de travail correct tooset utile hello afin que les chemins d’accès relatifs peuvent être utilisés par l’application ou l’initialisation des scripts hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-241">hello WorkingFolder is useful tooset hello correct working directory so that relative paths can be used by either hello application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="17d68-242">Mettre à jour des points de terminaison et les inscrire auprès du service d’affectation de noms à des fins de communication</span><span class="sxs-lookup"><span data-stu-id="17d68-242">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="17d68-243">Bonjour précédent exemple, hello `Endpoint` élément spécifie les points de terminaison hello application hello peut écouter.</span><span class="sxs-lookup"><span data-stu-id="17d68-243">In hello preceding example, hello `Endpoint` element specifies hello endpoints that hello application can listen on.</span></span> <span data-ttu-id="17d68-244">Dans cet exemple, hello application Node.js écoute http sur le port 3000.</span><span class="sxs-lookup"><span data-stu-id="17d68-244">In this example, hello Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="17d68-245">Vous pouvez en outre demander à Service Fabric toopublish cette toohello de point de terminaison d’affectation de noms Service pour d’autres services puissent détecter le service de toothis d’adresse de point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-245">Furthermore you can ask Service Fabric toopublish this endpoint toohello Naming Service so other services can discover hello endpoint address toothis service.</span></span> <span data-ttu-id="17d68-246">Cela vous permet de toocommunicate en mesure de toobe entre les services qui sont des exécutables de l’invité.</span><span class="sxs-lookup"><span data-stu-id="17d68-246">This enables you toobe able toocommunicate between services that are guest executables.</span></span>
<span data-ttu-id="17d68-247">Bonjour adresse de point de terminaison publié est sous forme de hello `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="17d68-247">hello published endpoint address is of hello form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="17d68-248">`UriScheme` et `PathSuffix` sont des attributs facultatifs.</span><span class="sxs-lookup"><span data-stu-id="17d68-248">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="17d68-249">`IPAddressOrFQDN`est hello adresse IP ou nom de domaine complet du nœud hello cet exécutable est placé sur, et elle est calculée pour vous.</span><span class="sxs-lookup"><span data-stu-id="17d68-249">`IPAddressOrFQDN` is hello IP address or fully qualified domain name of hello node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="17d68-250">Hello exemple suivant, une fois les services hello est déployé, dans l’Explorateur de l’infrastructure de Service vous voyez un point de terminaison similaire trop`http://10.1.4.92:3000/myapp/` publiée pour l’instance de service hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-250">In hello following example, once hello service is deployed, in Service Fabric Explorer you see an endpoint similar too`http://10.1.4.92:3000/myapp/` published for hello service instance.</span></span> <span data-ttu-id="17d68-251">S’il s’agit d’un ordinateur local, vous verrez`http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="17d68-251">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="17d68-252">Vous pouvez utiliser ces adresses avec [proxy inverse](service-fabric-reverseproxy.md) toocommunicate entre les services.</span><span class="sxs-lookup"><span data-stu-id="17d68-252">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) toocommunicate between services.</span></span>

### <a name="edit-hello-application-manifest-file"></a><span data-ttu-id="17d68-253">Modifier le fichier manifeste d’application hello</span><span class="sxs-lookup"><span data-stu-id="17d68-253">Edit hello application manifest file</span></span>
<span data-ttu-id="17d68-254">Une fois que vous avez configuré hello `Servicemanifest.xml` fichier, vous devez toomake toohello de certaines modifications `ApplicationManifest.xml` fichier tooensure hello correct de type de service et le nom sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="17d68-254">Once you have configured hello `Servicemanifest.xml` file, you need toomake some changes toohello `ApplicationManifest.xml` file tooensure that hello correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="17d68-255">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="17d68-255">ServiceManifestImport</span></span>
<span data-ttu-id="17d68-256">Bonjour `ServiceManifestImport` élément, vous pouvez spécifier un ou plusieurs services que vous souhaitez tooinclude dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-256">In hello `ServiceManifestImport` element, you can specify one or more services that you want tooinclude in hello app.</span></span> <span data-ttu-id="17d68-257">Les services sont référencés avec `ServiceManifestName`, qui spécifie le nom hello du répertoire de hello où hello `ServiceManifest.xml` fichier se trouve.</span><span class="sxs-lookup"><span data-stu-id="17d68-257">Services are referenced with `ServiceManifestName`, which specifies hello name of hello directory where hello `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="17d68-258">Configurez la journalisation</span><span class="sxs-lookup"><span data-stu-id="17d68-258">Set up logging</span></span>
<span data-ttu-id="17d68-259">Pour les exécutables de l’invité, il est utile toobe toosee en mesure de console journaux toofind out si les scripts de configuration et application hello affichent toutes les erreurs.</span><span class="sxs-lookup"><span data-stu-id="17d68-259">For guest executables, it is useful toobe able toosee console logs toofind out if hello application and configuration scripts show any errors.</span></span>
<span data-ttu-id="17d68-260">Redirection de la console peut être configuré dans hello `ServiceManifest.xml` fichier à l’aide de hello `ConsoleRedirection` élément.</span><span class="sxs-lookup"><span data-stu-id="17d68-260">Console redirection can be configured in hello `ServiceManifest.xml` file using hello `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="17d68-261">N’utilisez jamais de stratégie de redirection de console hello dans une application est déployée en production, car cela peut affecter le basculement d’application hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-261">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="17d68-262">N’utilisez cette stratégie *que* pour le développement local et à des fins de débogage.</span><span class="sxs-lookup"><span data-stu-id="17d68-262">*Only* use this for local development and debugging purposes.</span></span>  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="17d68-263">`ConsoleRedirection`répertoire de travail tooa tooredirect utilisé console sortie (stdout et stderr) est possible.</span><span class="sxs-lookup"><span data-stu-id="17d68-263">`ConsoleRedirection` can be used tooredirect console output (both stdout and stderr) tooa working directory.</span></span> <span data-ttu-id="17d68-264">Cela fournit hello capacité tooverify qu’il n’y a aucune erreur durant l’installation de hello ou de l’exécution de l’application hello dans le cluster Service Fabric de hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-264">This provides hello ability tooverify that there are no errors during hello setup or execution of hello application in hello Service Fabric cluster.</span></span>

<span data-ttu-id="17d68-265">`FileRetentionCount`Détermine le nombre de fichiers est enregistré dans le répertoire de travail hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-265">`FileRetentionCount` determines how many files are saved in hello working directory.</span></span> <span data-ttu-id="17d68-266">Une valeur de 5, par exemple, signifie que les fichiers de journaux hello pour les exécutions de cinq hello précédente sont stockés dans le répertoire de travail hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-266">A value of 5, for example, means that hello log files for hello previous five executions are stored in hello working directory.</span></span>

<span data-ttu-id="17d68-267">`FileMaxSizeInKb`Spécifie la taille maximale de hello des fichiers journaux de hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-267">`FileMaxSizeInKb` specifies hello maximum size of hello log files.</span></span>

<span data-ttu-id="17d68-268">Fichiers journaux sont enregistrés dans un des répertoires de travail du service hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-268">Log files are saved in one of hello service's working directories.</span></span> <span data-ttu-id="17d68-269">toodetermine où se trouvent les fichiers hello, utilisez Service Fabric Explorer toodetermine service hello nœud est en cours d’exécution et le répertoire de travail est utilisé.</span><span class="sxs-lookup"><span data-stu-id="17d68-269">toodetermine where hello files are located, use Service Fabric Explorer toodetermine which node hello service is running on, and which working directory is being used.</span></span> <span data-ttu-id="17d68-270">Cette procédure est décrite ultérieurement dans cet article.</span><span class="sxs-lookup"><span data-stu-id="17d68-270">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="17d68-271">Déploiement</span><span class="sxs-lookup"><span data-stu-id="17d68-271">Deployment</span></span>
<span data-ttu-id="17d68-272">dernière étape de Hello est trop[déployer votre application](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="17d68-272">hello last step is too[deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="17d68-273">Hello suivant montre de script PowerShell comment toodeploy votre cluster de développement local toohello application et démarrer un nouveau service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="17d68-273">hello following PowerShell script shows how toodeploy your application toohello local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="17d68-274">[Compresser le package de hello](service-fabric-package-apps.md#compress-a-package) avant de copier le magasin d’images toohello si le package de hello est trop grande ou a de nombreux fichiers.</span><span class="sxs-lookup"><span data-stu-id="17d68-274">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store if hello package is large or has many files.</span></span> <span data-ttu-id="17d68-275">En savoir plus [ici](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="17d68-275">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="17d68-276">Plusieurs configurations différentes peuvent être utilisées pour déployer un service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="17d68-276">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="17d68-277">Par exemple, il peut être déployé en tant qu’une ou plusieurs instances, ou il peut être déployé de manière à ce qu’il existe une instance du service hello sur chaque nœud du cluster Service Fabric de hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-277">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of hello service on each node of hello Service Fabric cluster.</span></span>

<span data-ttu-id="17d68-278">Hello `InstanceCount` paramètre Hello `New-ServiceFabricService` applet de commande est utilisée toospecify combien d’instances de service de hello doit être lancée dans le cluster Service Fabric de hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-278">hello `InstanceCount` parameter of hello `New-ServiceFabricService` cmdlet is used toospecify how many instances of hello service should be launched in hello Service Fabric cluster.</span></span> <span data-ttu-id="17d68-279">Vous pouvez définir hello `InstanceCount` valeur, en fonction de type hello d’application que vous déployez.</span><span class="sxs-lookup"><span data-stu-id="17d68-279">You can set hello `InstanceCount` value, depending on hello type of application that you are deploying.</span></span> <span data-ttu-id="17d68-280">les scénarios les plus courants Hello deux sont :</span><span class="sxs-lookup"><span data-stu-id="17d68-280">hello two most common scenarios are:</span></span>

* <span data-ttu-id="17d68-281">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="17d68-281">`InstanceCount = "1"`.</span></span> <span data-ttu-id="17d68-282">Dans ce cas, seule une instance de service de hello est déployée dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-282">In this case, only one instance of hello service is deployed in hello cluster.</span></span> <span data-ttu-id="17d68-283">Le planificateur du service Fabric détermine quel service hello de nœud est en train de toobe déployé sur.</span><span class="sxs-lookup"><span data-stu-id="17d68-283">Service Fabric's scheduler determines which node hello service is going toobe deployed on.</span></span>
* <span data-ttu-id="17d68-284">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="17d68-284">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="17d68-285">Dans ce cas, une instance du service de hello est déployée sur chaque nœud de cluster du Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-285">In this case, one instance of hello service is deployed on every node in hello Service Fabric cluster.</span></span> <span data-ttu-id="17d68-286">résultat de Hello a un seul (et unique) instance du service hello pour chaque nœud de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-286">hello result is having one (and only one) instance of hello service for each node in hello cluster.</span></span>

<span data-ttu-id="17d68-287">Il s’agit d’une configuration utile pour des applications frontales (par exemple, un point de terminaison REST), étant donné que les applications clientes doivent trop « se connecter » tooany de nœuds hello dans le point de terminaison hello cluster toouse hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-287">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need too"connect" tooany of hello nodes in hello cluster toouse hello endpoint.</span></span> <span data-ttu-id="17d68-288">Cette configuration peut également être utilisée lorsque, par exemple, tous les nœuds du cluster Service Fabric de hello sont équilibrage de charge tooa connecté.</span><span class="sxs-lookup"><span data-stu-id="17d68-288">This configuration can also be used when, for example, all nodes of hello Service Fabric cluster are connected tooa load balancer.</span></span> <span data-ttu-id="17d68-289">Le trafic des clients peut ensuite être distribué sur service hello qui s’exécute sur tous les nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="17d68-289">Client traffic can then be distributed across hello service that is running on all nodes in hello cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="17d68-290">Vérification de votre application en cours d'exécution</span><span class="sxs-lookup"><span data-stu-id="17d68-290">Check your running application</span></span>
<span data-ttu-id="17d68-291">Dans l’Explorateur de l’infrastructure de Service, identifiez le nœud hello où hello service s’exécute.</span><span class="sxs-lookup"><span data-stu-id="17d68-291">In Service Fabric Explorer, identify hello node where hello service is running.</span></span> <span data-ttu-id="17d68-292">Dans cet exemple, il s’exécute sur le nœud 1 :</span><span class="sxs-lookup"><span data-stu-id="17d68-292">In this example, it runs on Node1:</span></span>

![Nœud sur lequel le service est en cours d’exécution](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="17d68-294">Si vous accédez toohello nœud et parcourir toohello application, vous consultez informations de nœud essentielles hello, y compris son emplacement sur le disque.</span><span class="sxs-lookup"><span data-stu-id="17d68-294">If you navigate toohello node and browse toohello application, you see hello essential node information, including its location on disk.</span></span>

![Emplacement sur le disque](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="17d68-296">Si vous y accédez toohello active à l’aide de l’Explorateur de serveurs, vous trouverez répertoire de travail hello et le dossier du journal du service hello, comme indiqué dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="17d68-296">If you browse toohello directory by using Server Explorer, you can find hello working directory and hello service's log folder, as shown in hello following screenshot:</span></span> 

![Emplacement du journal](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="17d68-298">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="17d68-298">Next steps</span></span>
<span data-ttu-id="17d68-299">Dans cet article, vous avez appris comment toopackage un exécutable invité et déployez-le tooService l’ensemble fibre optique.</span><span class="sxs-lookup"><span data-stu-id="17d68-299">In this article, you have learned how toopackage a guest executable and deploy it tooService Fabric.</span></span> <span data-ttu-id="17d68-300">Consultez hello suivant des articles pour les tâches et les informations connexes.</span><span class="sxs-lookup"><span data-stu-id="17d68-300">See hello following articles for related information and tasks.</span></span>

* <span data-ttu-id="17d68-301">[Exemple pour empaqueter et déployer un exécutable invité](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), y compris une version préliminaire toohello de lien de l’outil d’empaquetage hello</span><span class="sxs-lookup"><span data-stu-id="17d68-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link toohello prerelease of hello packaging tool</span></span>
* [<span data-ttu-id="17d68-302">Exemple de l’invité deux exécutables (c# et nodejs) communique via le service d’affectation de noms de hello à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="17d68-302">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="17d68-303">Déploiement de plusieurs exécutables invités</span><span class="sxs-lookup"><span data-stu-id="17d68-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="17d68-304">Créez votre première application Service Fabric avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17d68-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
