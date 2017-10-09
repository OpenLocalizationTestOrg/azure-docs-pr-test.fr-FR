---
title: aaaManage vos applications dans Visual Studio | Documents Microsoft
description: "Utiliser Visual Studio toocreate, package, développer, déployer et déboguer vos applications de Service Fabric et services."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="eb926-103">Utiliser l’écriture de toosimplify Visual Studio et la gestion de vos applications de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb926-103">Use Visual Studio toosimplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="eb926-104">Vous pouvez gérer vos applications et services Azure Service Fabric via Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb926-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="eb926-105">Une fois que vous avez [configurer votre environnement de développement](service-fabric-get-started.md), vous pouvez utiliser les applications de Service Fabric toocreate Visual Studio, ajouter le Registre des services ou un package et déployer des applications dans votre cluster de développement local.</span><span class="sxs-lookup"><span data-stu-id="eb926-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio toocreate Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="eb926-106">Déploiement de votre application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb926-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="eb926-107">Par défaut, le déploiement d’une application combine hello dans une simple opération comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb926-107">By default, deploying an application combines hello following steps into one simple operation:</span></span>

1. <span data-ttu-id="eb926-108">Création de package d’application hello</span><span class="sxs-lookup"><span data-stu-id="eb926-108">Creating hello application package</span></span>
2. <span data-ttu-id="eb926-109">Magasin d’images toohello hello application package de téléchargement</span><span class="sxs-lookup"><span data-stu-id="eb926-109">Uploading hello application package toohello image store</span></span>
3. <span data-ttu-id="eb926-110">L’enregistrement du type d’application hello</span><span class="sxs-lookup"><span data-stu-id="eb926-110">Registering hello application type</span></span>
4. <span data-ttu-id="eb926-111">Suppression des instances d'application en cours d'exécution</span><span class="sxs-lookup"><span data-stu-id="eb926-111">Removing any running application instances</span></span>
5. <span data-ttu-id="eb926-112">Création d’une instance d’application</span><span class="sxs-lookup"><span data-stu-id="eb926-112">Creating an application instance</span></span>

<span data-ttu-id="eb926-113">Dans Visual Studio, en appuyant sur **F5** déploie votre application et de joindre des instances de l’application hello débogueur tooall.</span><span class="sxs-lookup"><span data-stu-id="eb926-113">In Visual Studio, pressing **F5** deploys your application and attach hello debugger tooall application instances.</span></span> <span data-ttu-id="eb926-114">Vous pouvez utiliser **Ctrl + F5** toodeploy une application sans débogage, ou vous pouvez publier tooa local ou un cluster distant à l’aide de hello le profil de publication.</span><span class="sxs-lookup"><span data-stu-id="eb926-114">You can use **Ctrl+F5** toodeploy an application without debugging, or you can publish tooa local or remote cluster by using hello publish profile.</span></span> <span data-ttu-id="eb926-115">Pour plus d’informations, consultez [publier un cluster à distance tooa d’application à l’aide de Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="eb926-115">For more information, see [Publish an application tooa remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="eb926-116">Mode de débogage d’application</span><span class="sxs-lookup"><span data-stu-id="eb926-116">Application Debug Mode</span></span>
<span data-ttu-id="eb926-117">Visual Studio fournit une propriété appelée **Mode de débogage d’Application**, qui contrôle comment vous souhaitez que le déploiement d’applications Visual Studio toohandle dans le cadre du débogage.</span><span class="sxs-lookup"><span data-stu-id="eb926-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios toohandle Application deployment as part of debugging.</span></span>

#### <a name="tooset-hello-application-debug-mode-property"></a><span data-ttu-id="eb926-118">tooset hello propriété Mode de débogage d’Application</span><span class="sxs-lookup"><span data-stu-id="eb926-118">tooset hello Application Debug Mode property</span></span>
1. <span data-ttu-id="eb926-119">Sur hello Service Fabric du projet d’application (*.sfproj) menu contextuel, choisissez **propriétés** (ou appuyez sur hello **F4** clé).</span><span class="sxs-lookup"><span data-stu-id="eb926-119">On hello Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press hello **F4** key).</span></span>
2. <span data-ttu-id="eb926-120">Bonjour **propriétés** fenêtre, jeu hello **Mode de débogage d’Application** propriété.</span><span class="sxs-lookup"><span data-stu-id="eb926-120">In hello **Properties** window, set hello **Application Debug Mode** property.</span></span>

![Définir la propriété Mode de débogage d’application][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="eb926-122">Modes de débogage de l’application</span><span class="sxs-lookup"><span data-stu-id="eb926-122">Application Debug Modes</span></span>

1. <span data-ttu-id="eb926-123">**Actualiser l’Application** ce mode vous permet de tooquickly modifier et déboguer votre code et les prend en charge la modification des fichiers web statiques pendant le débogage.</span><span class="sxs-lookup"><span data-stu-id="eb926-123">**Refresh Application** This mode enables you tooquickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="eb926-124">Ce mode fonctionne uniquement si votre cluster de développement local est en [mode 1 nœud](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="eb926-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="eb926-125">**Supprimer Application** causes hello toobe application supprimée lors de la session de débogage hello se termine.</span><span class="sxs-lookup"><span data-stu-id="eb926-125">**Remove Application** causes hello application toobe removed when hello debug session ends.</span></span>
3. <span data-ttu-id="eb926-126">**Mis à niveau automatiquement** application hello continue toorun lors de la session de débogage hello se termine.</span><span class="sxs-lookup"><span data-stu-id="eb926-126">**Auto Upgrade** hello application continues toorun when hello debug session ends.</span></span> <span data-ttu-id="eb926-127">Hello session de débogage suivante traite le déploiement de hello comme une mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="eb926-127">hello next debug session will treat hello deployment as an upgrade.</span></span> <span data-ttu-id="eb926-128">processus de mise à niveau de Hello conserve toutes les données que vous avez entré dans une session de débogage précédente.</span><span class="sxs-lookup"><span data-stu-id="eb926-128">hello upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="eb926-129">**Conserver l’Application** hello maintient les applications en cours d’exécution dans le cluster hello lorsque hello fin de la session de débogage.</span><span class="sxs-lookup"><span data-stu-id="eb926-129">**Keep Application** hello application keeps running in hello cluster when hello debug session ends.</span></span> <span data-ttu-id="eb926-130">Hello début Hello prochaine session de débogage, application hello sera supprimée.</span><span class="sxs-lookup"><span data-stu-id="eb926-130">At hello beginning of hello next debug session, hello application will be removed.</span></span>

<span data-ttu-id="eb926-131">Pour **mise à niveau automatique** données sont conservées par l’application hello mise à niveau des fonctionnalités des applications de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eb926-131">For **Auto Upgrade** data is preserved by applying hello application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="eb926-132">Pour plus d’informations sur la mise à niveau des applications et sur la façon d’effectuer une mise à niveau dans un environnement réel, consultez [Mise à niveau d’application Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="eb926-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-tooyour-service-fabric-application"></a><span data-ttu-id="eb926-133">Ajouter un tooyour service application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb926-133">Add a service tooyour Service Fabric application</span></span>
<span data-ttu-id="eb926-134">Vous pouvez ajouter les nouveaux services tooyour application tooextend ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="eb926-134">You can add new services tooyour application tooextend its functionality.</span></span>  <span data-ttu-id="eb926-135">tooensure que le service de hello est inclus dans votre package d’application, ajoutez service hello via hello **nouveau Service Fabric...**  élément de menu.</span><span class="sxs-lookup"><span data-stu-id="eb926-135">tooensure that hello service is included in your application package, add hello service through hello **New Fabric Service...** menu item.</span></span>

![Ajouter un service Service Fabric][newservice]

<span data-ttu-id="eb926-137">Sélectionnez une application de Service Fabric projet type tooadd tooyour et spécifiez un nom pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="eb926-137">Select a Service Fabric project type tooadd tooyour application, and specify a name for hello service.</span></span>  <span data-ttu-id="eb926-138">Consultez [choix d’une infrastructure pour votre service](service-fabric-choose-framework.md) toohelp vous décidez quel service de type toouse.</span><span class="sxs-lookup"><span data-stu-id="eb926-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) toohelp you decide which service type toouse.</span></span>

![Sélectionnez une application de Service Fabric service projet type tooadd tooyour][addserviceproject]

<span data-ttu-id="eb926-140">Hello nouveau service est ajouté tooyour solution et le package d’application existant.</span><span class="sxs-lookup"><span data-stu-id="eb926-140">hello new service is added tooyour solution and existing application package.</span></span> <span data-ttu-id="eb926-141">références de service Hello et une instance de service par défaut sera ajouté toohello manifeste d’application, toobe de service à l’origine hello créé et démarré hello prochaine fois que vous déployez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="eb926-141">hello service references and a default service instance will be added toohello application manifest, causing hello service toobe created and started hello next time you deploy hello application.</span></span>

![nouveau service de Hello est ajouté le manifeste d’application tooyour][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="eb926-143">Empaquetage de votre application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb926-143">Package your Service Fabric application</span></span>
<span data-ttu-id="eb926-144">application de hello toodeploy et son cluster tooa de services, vous devez toocreate un package d’application.</span><span class="sxs-lookup"><span data-stu-id="eb926-144">toodeploy hello application and its services tooa cluster, you need toocreate an application package.</span></span>  <span data-ttu-id="eb926-145">package de Hello organise le manifeste de l’application hello, les manifestes de service et les autres fichiers nécessaires dans une disposition spécifique.</span><span class="sxs-lookup"><span data-stu-id="eb926-145">hello package organizes hello application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="eb926-146">Visual Studio configure et gère le package hello dans le dossier du projet d’application hello, dans le répertoire de « pkg » hello.</span><span class="sxs-lookup"><span data-stu-id="eb926-146">Visual Studio sets up and manages hello package in hello application project's folder, in hello 'pkg' directory.</span></span>  <span data-ttu-id="eb926-147">En cliquant sur **Package** de hello **Application** crée du menu contextuel ou les mises à jour hello package d’application.</span><span class="sxs-lookup"><span data-stu-id="eb926-147">Clicking **Package** from hello **Application** context menu creates or updates hello application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="eb926-148">Supprimer des applications et des types d’applications à l’aide de Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="eb926-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="eb926-149">Vous pouvez effectuer les opérations de gestion de cluster de base à partir de Visual Studio à l’aide de Cloud Explorer, que vous pouvez lancer à partir de hello **vue** menu.</span><span class="sxs-lookup"><span data-stu-id="eb926-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from hello **View** menu.</span></span> <span data-ttu-id="eb926-150">Par exemple, vous pouvez supprimer des applications et annuler la mise en service de types d’applications sur des clusters locaux ou distants.</span><span class="sxs-lookup"><span data-stu-id="eb926-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Supprimer une application][removeapplication]

> [!TIP]
> <span data-ttu-id="eb926-152">Pour obtenir des fonctionnalités de gestion de clusters enrichies, consultez [Visualisation de votre cluster à l’aide de l’outil Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="eb926-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="eb926-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eb926-153">Next steps</span></span>
* [<span data-ttu-id="eb926-154">Modèle d'application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb926-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="eb926-155">Déploiement d'applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb926-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="eb926-156">Gestion des paramètres d’application pour plusieurs environnements</span><span class="sxs-lookup"><span data-stu-id="eb926-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="eb926-157">Débogage de votre application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb926-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="eb926-158">Visualisation de votre cluster à l’aide de l’explorateur Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb926-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png