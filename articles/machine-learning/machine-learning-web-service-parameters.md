---
title: "Utilisation des paramètres de service web Azure Machine Learning | Microsoft Docs"
description: "Comment utiliser les paramètres de service Web Azure Machine Learning pour modifier le comportement de votre modèle au moment d’accéder au service Web."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 482726c1dae5385964e08b720e529817d5907537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a><span data-ttu-id="0b8a8-103">Utilisation des paramètres de service Web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0b8a8-103">Use Azure Machine Learning Web Service Parameters</span></span>
<span data-ttu-id="0b8a8-104">Un service Web Azure Machine Learning est créé en publiant une expérience qui contient des modules avec des paramètres configurables.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span></span> <span data-ttu-id="0b8a8-105">Il se peut que, dans certains cas, vous souhaitiez modifier le comportement du module lorsque le service Web est en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-105">In some cases, you may want to change the module behavior while the web service is running.</span></span> <span data-ttu-id="0b8a8-106">Vous pouvez effectuer cette tâche grâce aux *paramètres de service Web*.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-106">*Web Service Parameters* allow you to do this task.</span></span> 

<span data-ttu-id="0b8a8-107">Un exemple courant consiste à configurer le module [Importer les données][reader], afin que l’utilisateur du service web publié puisse spécifier une autre source de données lors de l’accès au service web.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-107">A common example is setting up the [Import Data][reader] module so that the user of the published web service can specify a different data source when the web service is accessed.</span></span> <span data-ttu-id="0b8a8-108">Il est également possible de configurer le module [Exporter les données][writer] de façon à spécifier une destination différente.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-108">Or configuring the [Export Data][writer] module so that a different destination can be specified.</span></span> <span data-ttu-id="0b8a8-109">Vous pouvez aussi, par exemple, modifier le nombre de bits pour le module [Feature Hashing][feature-hashing] ou le nombre de fonctionnalités souhaitées pour le module de [Sélection de fonctionnalités basée sur le filtre][filter-based-feature-selection].</span><span class="sxs-lookup"><span data-stu-id="0b8a8-109">Some other examples include changing the number of bits for the [Feature Hashing][feature-hashing] module or the number of desired features for the [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> 

<span data-ttu-id="0b8a8-110">Vous pouvez définir des paramètres de service web et les associer à un ou plusieurs paramètres de module dans votre expérience, en spécifiant s’ils sont obligatoires ou facultatifs.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="0b8a8-111">L’utilisateur du service web peut ensuite fournir des valeurs pour ces paramètres quand il appelle le service web.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-111">The user of the web service can then provide values for these parameters when they call the web service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-to-set-and-use-web-service-parameters"></a><span data-ttu-id="0b8a8-112">Comment configurer et utiliser les paramètres de service Web</span><span class="sxs-lookup"><span data-stu-id="0b8a8-112">How to set and use Web Service Parameters</span></span>
<span data-ttu-id="0b8a8-113">Pour définir un paramètre de service Web, cliquez sur l'icône située à côté du paramètre pour module et sélectionnez « Définir en tant que paramètre du service Web ».</span><span class="sxs-lookup"><span data-stu-id="0b8a8-113">You define a Web Service Parameter by clicking the icon next to the parameter for a module and selecting "Set as web service parameter".</span></span> <span data-ttu-id="0b8a8-114">Cette opération crée un nouveau paramètre de service Web et le connecte à ce paramètre de module.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-114">This creates a new Web Service Parameter and connects it to that module parameter.</span></span> <span data-ttu-id="0b8a8-115">L'utilisateur peut ensuite, lorsqu’il accède au service Web, spécifier une valeur pour le paramètre de service Web. Celle-ci est appliquée au paramètre de module.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-115">Then, when the web service is accessed, the user can specify a value for the Web Service Parameter and it is applied to the module parameter.</span></span>

<span data-ttu-id="0b8a8-116">Une fois le paramètre de service Web défini, il est disponible pour n'importe quel autre paramètre de module faisant partie de l'expérience.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-116">Once you define a Web Service Parameter, it's available to any other module parameter in the experiment.</span></span> <span data-ttu-id="0b8a8-117">Si vous définissez un paramètre de service Web associé à un paramètre défini pour un module, vous pouvez utiliser ce même paramètre de service Web pour n’importe quel autre module, pourvu que la valeur attribuée au paramètre soit de même type.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as the parameter expects the same type of value.</span></span> <span data-ttu-id="0b8a8-118">Par exemple, si le paramètre de service Web est une valeur numérique, il peut uniquement être utilisé pour les paramètres de module qui gèrent des valeurs numériques.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-118">For example, if the Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span></span> <span data-ttu-id="0b8a8-119">Lorsque l'utilisateur définit une valeur pour le paramètre de service Web, elle est appliquée à tous les paramètres de modules associés.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-119">When the user sets a value for the Web Service Parameter, it will be applied to all associated module parameters.</span></span>

<span data-ttu-id="0b8a8-120">Vous pouvez décider de définir ou non une valeur par défaut pour le paramètre de service Web.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-120">You can decide whether to provide a default value for the Web Service Parameter.</span></span> <span data-ttu-id="0b8a8-121">Si vous en définissez une, le paramètre est facultatif pour l'utilisateur du service Web.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-121">If you do, then the parameter is optional for the user of the web service.</span></span> <span data-ttu-id="0b8a8-122">Si vous ne le faites pas, l'utilisateur doit entrer une valeur au moment d’accéder au service Web.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-122">If you don't provide a default value, then the user is required to enter a value when the web service is accessed.</span></span>

<span data-ttu-id="0b8a8-123">La documentation pour le service Web fournit à l'utilisateur du service Web des informations sur la façon de définir, en les programmant, les paramètres de service web au moment d'accéder au service web.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-123">The API documentation for the web service includes information for the web service user on how to specify the Web Service Parameter programmatically when accessing the web service.</span></span>

> [!NOTE]
> <span data-ttu-id="0b8a8-124">La documentation API pour un service web classique est fournie via le lien **Page d’aide de l’API** dans le service web **TABLEAU DE BORD** dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-124">The API documentation for a classic web service is provided through the **API help page** link in the web service **DASHBOARD** in Machine Learning Studio.</span></span> <span data-ttu-id="0b8a8-125">La documentation API pour un service web est fournie via le portail des [services web Azure Machine Learning](https://services.azureml.net/Quickstart) des pages **Utiliser** et **API Swagger** de votre service web.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-125">The API documentation for a new web service is provided through the [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on the **Consume** and **Swagger API** pages for your web service.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="0b8a8-126">Exemple</span><span class="sxs-lookup"><span data-stu-id="0b8a8-126">Example</span></span>
<span data-ttu-id="0b8a8-127">Par exemple, supposons que nous avons une expérience avec un module [Exporter les données][writer] qui envoie des informations vers le stockage blob Azure.
</span><span class="sxs-lookup"><span data-stu-id="0b8a8-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information to Azure blob storage.</span></span> <span data-ttu-id="0b8a8-128">Nous allons définir un paramètre de service Web nommé « Chemin d'accès d'objet blob » qui permet à l'utilisateur de service Web de modifier le chemin d'accès pour le stockage d'objets blob lors de l’accès au service.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-128">We'll define a Web Service Parameter named "Blob path" that allows the web service user to change the path to the blob storage when the service is accessed.</span></span>

1. <span data-ttu-id="0b8a8-129">Dans Machine Learning Studio, cliquez sur le module [Exporter les données][writer] pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-129">In Machine Learning Studio, click the [Export Data][writer] module to select it.</span></span> <span data-ttu-id="0b8a8-130">Ses propriétés sont affichées dans le volet Propriétés à droite du canevas de l'expérience.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-130">Its properties are shown in the Properties pane to the right of the experiment canvas.</span></span>
2. <span data-ttu-id="0b8a8-131">Spécification du type de stockage :</span><span class="sxs-lookup"><span data-stu-id="0b8a8-131">Specify the storage type:</span></span>
   
   * <span data-ttu-id="0b8a8-132">Sous le message **Veuillez spécifier la destination des données**, sélectionnez « Stockage d'objets blob Azure ».</span><span class="sxs-lookup"><span data-stu-id="0b8a8-132">Under **Please specify data destination**, select "Azure Blob Storage".</span></span>
   * <span data-ttu-id="0b8a8-133">Sous le message **Veuillez spécifier le type d'authentification**, sélectionnez « Compte ».</span><span class="sxs-lookup"><span data-stu-id="0b8a8-133">Under **Please specify authentication type**, select "Account".</span></span>
   * <span data-ttu-id="0b8a8-134">Entrez les informations de compte correspondant au stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-134">Enter the account information for the Azure blob storage.</span></span> 
     <p /><span data-ttu-id="0b8a8-135">
3. Cliquez sur l’icône à droite du **Chemin d’accès d’objet blob commençant par le paramètre du conteneur**.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-135">
3. Click the icon to the right of the **Path to blob beginning with container parameter**.</span></span> <span data-ttu-id="0b8a8-136">Voici à quoi cela ressemble :</span><span class="sxs-lookup"><span data-stu-id="0b8a8-136">It looks like this:</span></span>
   
   ![Icône de paramètre de service Web][icon]
   
   <span data-ttu-id="0b8a8-138">Sélectionnez « Définir en tant que paramètre du service Web ».</span><span class="sxs-lookup"><span data-stu-id="0b8a8-138">Select "Set as web service parameter".</span></span>
   
   <span data-ttu-id="0b8a8-139">Une entrée est ajoutée sous les **paramètres de service Web** en bas du volet Propriétés portant le nom de « Chemin d'accès d’objet blob commençant par le conteneur ».</span><span class="sxs-lookup"><span data-stu-id="0b8a8-139">An entry is added under **Web Service Parameters** at the bottom of the Properties pane with the name "Path to blob beginning with container".</span></span> <span data-ttu-id="0b8a8-140">C’est le paramètre de service web qui est désormais associé à ce paramètre de module [Exporter les données][writer].</span><span class="sxs-lookup"><span data-stu-id="0b8a8-140">This is the Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span></span>
4. <span data-ttu-id="0b8a8-141">Pour renommer le paramètre de service Web, cliquez sur son nom, entrez « Blob path », puis appuyez sur la touche **Entrée** .</span><span class="sxs-lookup"><span data-stu-id="0b8a8-141">To rename the Web Service Parameter, click the name, enter "Blob path", and press the **Enter** key.</span></span> 
5. <span data-ttu-id="0b8a8-142">Pour attribuer au paramètre de service Web une valeur par défaut, cliquez sur l'icône à droite du nom, sélectionnez « Fournir la valeur par défaut », entrez une valeur (par exemple, « container1/output1.csv »), puis appuyez sur la touche **Entrée** .</span><span class="sxs-lookup"><span data-stu-id="0b8a8-142">To provide a default value for the Web Service Parameter, click the icon to the right of the name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press the **Enter** key.</span></span>
   
   ![Paramètre de service Web][parameter]
6. <span data-ttu-id="0b8a8-144">Cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-144">Click **Run**.</span></span> 
7. <span data-ttu-id="0b8a8-145">Cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [standard]** ou **déployer le Service Web [nouveau]** pour déployer le service web.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** to deploy the web service.</span></span>

> [!NOTE] 
> <span data-ttu-id="0b8a8-146">Pour déployer un nouveau service web, vous devez disposer d’autorisations suffisantes dans l’abonnement dans lequel déployer le service web.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-146">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="0b8a8-147">Pour en savoir plus, consultez la rubrique [Gérer un service web à l’aide du portail des services web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="0b8a8-147">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="0b8a8-148">L’utilisateur du service web peut désormais indiquer une nouvelle destination pour le module [Exporter les données][writer] au moment d’accéder au service web.</span><span class="sxs-lookup"><span data-stu-id="0b8a8-148">The user of the web service can now specify a new destination for the [Export Data][writer] module when accessing the web service.</span></span>

## <a name="more-information"></a><span data-ttu-id="0b8a8-149">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="0b8a8-149">More information</span></span>
<span data-ttu-id="0b8a8-150">Vous trouverez un exemple plus détaillé en consultant l’entrée [Paramètres de service Web](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) du blog [Machine Learning ](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b8a8-150">For a more detailed example, see the [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in the [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span></span>

<span data-ttu-id="0b8a8-151">Pour plus d’informations sur l’accès à un service web Machine Learning, consultez [Utilisation d’un service web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="0b8a8-151">For more information on accessing a Machine Learning web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

