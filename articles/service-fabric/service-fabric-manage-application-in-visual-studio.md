---
title: Gestion de vos applications dans Visual Studio | Microsoft Docs
description: "Utilisez Visual Studio pour créer, développer, packager, déployer et déboguer vos applications et services Service Fabric."
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
ms.openlocfilehash: 3f6a47a15b74a7ceb6504b2834be62e76ab70bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-visual-studio-to-simplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="ecb6f-103">Utilisation de Visual Studio pour simplifier l'écriture et la gestion des applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ecb6f-103">Use Visual Studio to simplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="ecb6f-104">Vous pouvez gérer vos applications et services Azure Service Fabric via Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="ecb6f-105">Après avoir [configuré votre environnement de développement](service-fabric-get-started.md), vous pouvez utiliser Visual Studio pour créer des applications Service Fabric, ajouter des services ou empaqueter, enregistrer et déployer des applications dans votre cluster de développement local.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio to create Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="ecb6f-106">Déploiement de votre application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ecb6f-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="ecb6f-107">Par défaut, le déploiement d’une application regroupe les étapes suivantes en une simple opération :</span><span class="sxs-lookup"><span data-stu-id="ecb6f-107">By default, deploying an application combines the following steps into one simple operation:</span></span>

1. <span data-ttu-id="ecb6f-108">Création du package d'application</span><span class="sxs-lookup"><span data-stu-id="ecb6f-108">Creating the application package</span></span>
2. <span data-ttu-id="ecb6f-109">Téléchargement du package d'application dans le magasin d'images</span><span class="sxs-lookup"><span data-stu-id="ecb6f-109">Uploading the application package to the image store</span></span>
3. <span data-ttu-id="ecb6f-110">Enregistrement du type d'application</span><span class="sxs-lookup"><span data-stu-id="ecb6f-110">Registering the application type</span></span>
4. <span data-ttu-id="ecb6f-111">Suppression des instances d'application en cours d'exécution</span><span class="sxs-lookup"><span data-stu-id="ecb6f-111">Removing any running application instances</span></span>
5. <span data-ttu-id="ecb6f-112">Création d’une instance d’application</span><span class="sxs-lookup"><span data-stu-id="ecb6f-112">Creating an application instance</span></span>

<span data-ttu-id="ecb6f-113">Dans Visual Studio, appuyer sur **F5** permet de déployer votre application et d’attacher le débogueur à toutes les instances de l’application.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-113">In Visual Studio, pressing **F5** deploys your application and attach the debugger to all application instances.</span></span> <span data-ttu-id="ecb6f-114">Vous pouvez utiliser **Ctrl + F5** pour déployer une application sans débogage ou la publier sur un cluster local ou distant à l’aide du profil de publication.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-114">You can use **Ctrl+F5** to deploy an application without debugging, or you can publish to a local or remote cluster by using the publish profile.</span></span> <span data-ttu-id="ecb6f-115">Pour plus d’informations, reportez-vous à la section [Publication d’une application dans un cluster à distance avec Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ecb6f-115">For more information, see [Publish an application to a remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="ecb6f-116">Mode de débogage d’application</span><span class="sxs-lookup"><span data-stu-id="ecb6f-116">Application Debug Mode</span></span>
<span data-ttu-id="ecb6f-117">Visual Studio fournit une propriété appelée **Mode de débogage de l’application**, qui contrôle la façon dont vous souhaitez que Visual Studio gère le déploiement de l’application dans le cadre du débogage.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios to handle Application deployment as part of debugging.</span></span>

#### <a name="to-set-the-application-debug-mode-property"></a><span data-ttu-id="ecb6f-118">Pour définir la propriété Mode de débogage d’application</span><span class="sxs-lookup"><span data-stu-id="ecb6f-118">To set the Application Debug Mode property</span></span>
1. <span data-ttu-id="ecb6f-119">Dans le menu contextuel du projet d’application Service Fabric (*.sfproj), cliquez sur **Propriétés** (ou appuyez sur la touche **F4**).</span><span class="sxs-lookup"><span data-stu-id="ecb6f-119">On the Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press the **F4** key).</span></span>
2. <span data-ttu-id="ecb6f-120">Dans la fenêtre **Propriétés**, définissez la propriété **Mode de débogage d’application**.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-120">In the **Properties** window, set the **Application Debug Mode** property.</span></span>

![Définir la propriété Mode de débogage d’application][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="ecb6f-122">Modes de débogage de l’application</span><span class="sxs-lookup"><span data-stu-id="ecb6f-122">Application Debug Modes</span></span>

1. <span data-ttu-id="ecb6f-123">**Actualiser l’application** Ce mode vous permet de modifier et de déboguer rapidement votre code, et prend en charge la modification des fichiers web statiques pendant le débogage.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-123">**Refresh Application** This mode enables you to quickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="ecb6f-124">Ce mode fonctionne uniquement si votre cluster de développement local est en [mode 1 nœud](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="ecb6f-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="ecb6f-125">**Supprimer l’application** entraîne la suppression de l’application lorsque la session de débogage se termine.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-125">**Remove Application** causes the application to be removed when the debug session ends.</span></span>
3. <span data-ttu-id="ecb6f-126">**Mise à niveau automatique** L’application continue à s’exécuter lorsque la session de débogage se termine.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-126">**Auto Upgrade** The application continues to run when the debug session ends.</span></span> <span data-ttu-id="ecb6f-127">La session de débogage suivante traitera le déploiement comme une mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-127">The next debug session will treat the deployment as an upgrade.</span></span> <span data-ttu-id="ecb6f-128">Le processus de mise à niveau conserve les données que vous avez saisies au cours de la précédente session de débogage.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-128">The upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="ecb6f-129">**Conserver l’application** L’application continue à s’exécuter dans le cluster lorsque la session de débogage se termine.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-129">**Keep Application** The application keeps running in the cluster when the debug session ends.</span></span> <span data-ttu-id="ecb6f-130">Au début de la prochaine session de débogage, l’application sera supprimée.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-130">At the beginning of the next debug session, the application will be removed.</span></span>

<span data-ttu-id="ecb6f-131">Avec l’option **Mise à niveau automatique**, les données sont conservées en appliquant les fonctionnalités de mise à niveau d’application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-131">For **Auto Upgrade** data is preserved by applying the application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="ecb6f-132">Pour plus d’informations sur la mise à niveau des applications et sur la façon d’effectuer une mise à niveau dans un environnement réel, consultez [Mise à niveau d’application Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="ecb6f-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-to-your-service-fabric-application"></a><span data-ttu-id="ecb6f-133">Ajouter un service à votre application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ecb6f-133">Add a service to your Service Fabric application</span></span>
<span data-ttu-id="ecb6f-134">Vous pouvez ajouter de nouveaux services à votre application pour étendre ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-134">You can add new services to your application to extend its functionality.</span></span>  <span data-ttu-id="ecb6f-135">Pour garantir que le service est inclus dans votre package d’application, ajoutez-le via l’élément de menu **Nouveau service Service Fabric…** .</span><span class="sxs-lookup"><span data-stu-id="ecb6f-135">To ensure that the service is included in your application package, add the service through the **New Fabric Service...** menu item.</span></span>

![Ajouter un service Service Fabric][newservice]

<span data-ttu-id="ecb6f-137">Sélectionnez un type de projet Service Fabric à ajouter à votre application et spécifiez un nom pour le service.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-137">Select a Service Fabric project type to add to your application, and specify a name for the service.</span></span>  <span data-ttu-id="ecb6f-138">Consultez [Choix d’une infrastructure pour votre service](service-fabric-choose-framework.md) pour vous aider à choisir le type de service à utiliser.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) to help you decide which service type to use.</span></span>

![Sélectionner un type de projet de service Service Fabric à ajouter à votre application][addserviceproject]

<span data-ttu-id="ecb6f-140">Le nouveau service est ajouté à votre solution et au package d’application existant.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-140">The new service is added to your solution and existing application package.</span></span> <span data-ttu-id="ecb6f-141">Les références de service et une instance de service par défaut seront ajoutées au manifeste de l’application, provoquant la création et le démarrage du service la prochaine fois que vous déployez l’application.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-141">The service references and a default service instance will be added to the application manifest, causing the service to be created and started the next time you deploy the application.</span></span>

![Le nouveau service est ajouté à votre manifeste de l’application][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="ecb6f-143">Empaquetage de votre application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ecb6f-143">Package your Service Fabric application</span></span>
<span data-ttu-id="ecb6f-144">Pour déployer l’application et ses services dans un cluster, vous devez créer un package d’application.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-144">To deploy the application and its services to a cluster, you need to create an application package.</span></span>  <span data-ttu-id="ecb6f-145">Le package organise le manifeste de l’application, les manifestes de service et les autres fichiers nécessaires dans une disposition spécifique.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-145">The package organizes the application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="ecb6f-146">Visual Studio configure et gère le package dans le dossier du projet d'application, dans le répertoire « pkg ».</span><span class="sxs-lookup"><span data-stu-id="ecb6f-146">Visual Studio sets up and manages the package in the application project's folder, in the 'pkg' directory.</span></span>  <span data-ttu-id="ecb6f-147">Cliquez sur **Package** dans le menu contextuel **Application** pour créer ou mettre à jour le package d’application.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-147">Clicking **Package** from the **Application** context menu creates or updates the application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="ecb6f-148">Supprimer des applications et des types d’applications à l’aide de Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="ecb6f-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="ecb6f-149">Vous pouvez effectuer des opérations de gestion de cluster de base à partir de Visual Studio à l’aide de Cloud Explorer, que vous pouvez lancer à partir du menu **Affichage** .</span><span class="sxs-lookup"><span data-stu-id="ecb6f-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from the **View** menu.</span></span> <span data-ttu-id="ecb6f-150">Par exemple, vous pouvez supprimer des applications et annuler la mise en service de types d’applications sur des clusters locaux ou distants.</span><span class="sxs-lookup"><span data-stu-id="ecb6f-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Supprimer une application][removeapplication]

> [!TIP]
> <span data-ttu-id="ecb6f-152">Pour obtenir des fonctionnalités de gestion de clusters enrichies, consultez [Visualisation de votre cluster à l’aide de l’outil Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ecb6f-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="ecb6f-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ecb6f-153">Next steps</span></span>
* [<span data-ttu-id="ecb6f-154">Modèle d'application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ecb6f-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="ecb6f-155">Déploiement d'applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ecb6f-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="ecb6f-156">Gestion des paramètres d’application pour plusieurs environnements</span><span class="sxs-lookup"><span data-stu-id="ecb6f-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="ecb6f-157">Débogage de votre application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ecb6f-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="ecb6f-158">Visualisation de votre cluster à l’aide de l’explorateur Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ecb6f-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png