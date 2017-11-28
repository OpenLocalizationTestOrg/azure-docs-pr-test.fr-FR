---
title: "Résoudre les problèmes de reformation d’un service web Azure Machine Learning Classic | Microsoft Docs"
description: "Identifiez et corrigez les problèmes courants rencontrés lorsque vous reformez le modèle d’un service web Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: fc36499ebff88c86635228ff899c85e9166aabed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-the-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="48b3d-103">Résolution des problèmes de reformation d’un service web Azure Machine Learning classique</span><span class="sxs-lookup"><span data-stu-id="48b3d-103">Troubleshooting the retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="48b3d-104">Vue d’ensemble de la reformation</span><span class="sxs-lookup"><span data-stu-id="48b3d-104">Retraining overview</span></span>
<span data-ttu-id="48b3d-105">Lorsque vous déployez une expérience prédictive en tant que service web d’évaluation, il s’agit d’un modèle statique.</span><span class="sxs-lookup"><span data-stu-id="48b3d-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="48b3d-106">Lorsque de nouvelles données sont disponibles ou lorsque le consommateur de l’API a ses propres données, le modèle doit être reformé.</span><span class="sxs-lookup"><span data-stu-id="48b3d-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span></span> 

<span data-ttu-id="48b3d-107">Pour une procédure pas à pas complète du processus de reformation d’un service web classique, voir [Reformation des modèles Machine Learning par programme](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="48b3d-107">For a complete walkthrough of the retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="48b3d-108">Processus de reformation</span><span class="sxs-lookup"><span data-stu-id="48b3d-108">Retraining process</span></span>
<span data-ttu-id="48b3d-109">Lorsque vous devez reformer le service web, vous devez ajouter quelques éléments supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="48b3d-109">When you need to retrain the Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="48b3d-110">Un service web déployé à partir de l’expérience de formation.</span><span class="sxs-lookup"><span data-stu-id="48b3d-110">A Web service deployed from the Training Experiment.</span></span> <span data-ttu-id="48b3d-111">L’expérience doit avoir un module de **sortie de service web** attaché à la sortie du module **Modèle de formation**.</span><span class="sxs-lookup"><span data-stu-id="48b3d-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span></span>  
  
    ![Attachez la sortie de service web au modèle de formation.][image1]
* <span data-ttu-id="48b3d-113">Un nouveau point de terminaison ajouté à votre service web de notation.</span><span class="sxs-lookup"><span data-stu-id="48b3d-113">A new endpoint added to your scoring Web service.</span></span>  <span data-ttu-id="48b3d-114">Vous pouvez ajouter le point de terminaison par programme à l’aide de l’exemple de code référencé dans la rubrique Reformation des modèles Machine Learning par programme ou via le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="48b3d-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure classic portal.</span></span>

<span data-ttu-id="48b3d-115">Vous pouvez utiliser l’exemple de code C# de la page d’aide API du service web de formation pour reformer le modèle.</span><span class="sxs-lookup"><span data-stu-id="48b3d-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span></span> <span data-ttu-id="48b3d-116">Après avoir évalué les résultats et que vous en êtes satisfait, vous mettez à jour le service web d’évaluation du modèle formé à l’aide du nouveau point de terminaison que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="48b3d-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span></span>

<span data-ttu-id="48b3d-117">Une fois tous les éléments en place, les principales étapes à suivre pour reformer le modèle sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="48b3d-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span></span>

1. <span data-ttu-id="48b3d-118">Appelez le service web de formation : l’appel est destiné au service d’exécution de lots (BES, Batch Execution Service), et non au service de requête-réponse (RRS, Request-Response Service).</span><span class="sxs-lookup"><span data-stu-id="48b3d-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span></span> <span data-ttu-id="48b3d-119">Vous pouvez utiliser l’exemple de code C# sur la page d’aide API pour effectuer l’appel.</span><span class="sxs-lookup"><span data-stu-id="48b3d-119">You can use the sample C# code on the API help page to make the call.</span></span> 
2. <span data-ttu-id="48b3d-120">Recherchez les valeurs pour *BaseLocation*, *RelativeLocation* et *SasBlobToken* : ces valeurs sont retournées dans la sortie à partir de votre appel au service web de formation.</span><span class="sxs-lookup"><span data-stu-id="48b3d-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span></span> 
   <span data-ttu-id="48b3d-121">![Affichage de la sortie de l’exemple de reformation et des valeurs BaseLocation, RelativeLocation et SasBlobToken.][image6]</span><span class="sxs-lookup"><span data-stu-id="48b3d-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="48b3d-122">Mettez à jour le point de terminaison ajouté à partir du service web d’évaluation avec le nouveau modèle formé : à l’aide de l’exemple de code fourni dans la rubrique Reformation des modèles Machine Learning par programme, mettez à jour le nouveau point de terminaison que vous avez ajouté au modèle d’évaluation avec le modèle nouvellement formé à partir du service web de formation.</span><span class="sxs-lookup"><span data-stu-id="48b3d-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="48b3d-123">Obstacles courants</span><span class="sxs-lookup"><span data-stu-id="48b3d-123">Common obstacles</span></span>
### <a name="check-to-see-if-you-have-the-correct-patch-url"></a><span data-ttu-id="48b3d-124">Vérifiez que vous disposez de l’URL d’application de correctifs appropriée</span><span class="sxs-lookup"><span data-stu-id="48b3d-124">Check to see if you have the correct PATCH URL</span></span>
<span data-ttu-id="48b3d-125">L’URL d’application de correctifs que vous utilisez doit être celle associée au nouveau point de terminaison d’évaluation que vous avez ajouté au service web d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="48b3d-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring Web service.</span></span> <span data-ttu-id="48b3d-126">Il existe plusieurs façons d’obtenir l’URL des CORRECTIFS :</span><span class="sxs-lookup"><span data-stu-id="48b3d-126">There are a number of ways to obtain the PATCH URL:</span></span>

<span data-ttu-id="48b3d-127">**Option 1 : par programme**</span><span class="sxs-lookup"><span data-stu-id="48b3d-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="48b3d-128">Pour obtenir l’URL d’application de correctifs appropriée :</span><span class="sxs-lookup"><span data-stu-id="48b3d-128">To get the correct PATCH URL:</span></span>

1. <span data-ttu-id="48b3d-129">Exécutez l’exemple de code [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) .</span><span class="sxs-lookup"><span data-stu-id="48b3d-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="48b3d-130">À partir de la sortie d’AddEndpoint, recherchez la valeur *HelpLocation* et copiez l’URL.</span><span class="sxs-lookup"><span data-stu-id="48b3d-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span></span>
   
   ![HelpLocation dans la sortie de l’exemple addEndpoint.][image2]
3. <span data-ttu-id="48b3d-132">Collez l’URL dans un navigateur pour accéder à une page qui fournit des liens d’aide pour le service web.</span><span class="sxs-lookup"><span data-stu-id="48b3d-132">Paste the URL into a browser to navigate to a page that provides help links for the Web service.</span></span>
4. <span data-ttu-id="48b3d-133">Cliquez sur le lien de **Mettre à jour la ressource** pour ouvrir la page d’aide sur le correctif.</span><span class="sxs-lookup"><span data-stu-id="48b3d-133">Click the **Update Resource** link to open the patch help page.</span></span>

<span data-ttu-id="48b3d-134">**Option 2 : utiliser le portail Azure Classic**</span><span class="sxs-lookup"><span data-stu-id="48b3d-134">**Option 2: Use the Azure classic portal**</span></span>

1. <span data-ttu-id="48b3d-135">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="48b3d-135">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="48b3d-136">Ouvrez l’onglet Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="48b3d-136">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="48b3d-137">![Onglet Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="48b3d-137">![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="48b3d-138">Cliquez sur le nom de votre espace de travail, puis sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="48b3d-138">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="48b3d-139">Cliquez sur le service web d’évaluation avec lequel vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="48b3d-139">Click the scoring Web service you are working with.</span></span> <span data-ttu-id="48b3d-140">(Si vous n’avez pas modifié le nom par défaut du service web, il se terminera par [Exp. de notation].)</span><span class="sxs-lookup"><span data-stu-id="48b3d-140">(If you did not modify the default name of the web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="48b3d-141">Cliquez sur **Ajouter un point de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="48b3d-141">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="48b3d-142">Après l’ajout du point de terminaison, cliquez sur le nom du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="48b3d-142">After the endpoint is added, click the endpoint name.</span></span> <span data-ttu-id="48b3d-143">Cliquez ensuite sur **Mettre à jour la ressource** pour ouvrir la page d’aide d’application de correctifs.</span><span class="sxs-lookup"><span data-stu-id="48b3d-143">Then click **Update Resource** to open the patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="48b3d-144">Si vous avez ajouté le point de terminaison au service web d’apprentissage plutôt qu’au service web prédictif, lorsque vous cliquez sur le lien **Mettre à jour la ressource**, vous recevrez un message d’erreur signalant que cette fonctionnalité n’est pas prise en charge ou disponible dans ce contexte.</span><span class="sxs-lookup"><span data-stu-id="48b3d-144">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="48b3d-145">Ce service web n’a aucune ressource actualisable.</span><span class="sxs-lookup"><span data-stu-id="48b3d-145">This Web Service has no updatable resources.</span></span> <span data-ttu-id="48b3d-146">Veuillez nous excuser pour ce désagrément. Nous travaillons actuellement à l’amélioration de ce flux de travail.</span><span class="sxs-lookup"><span data-stu-id="48b3d-146">We apologize for the inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Nouveau tableau de bord de point de terminaison.][image3]

<span data-ttu-id="48b3d-148">La page d’aide d’application de correctifs contient l’URL d’application de correctifs que vous devez utiliser et fournit un exemple de code que vous pouvez utiliser pour l’appeler.</span><span class="sxs-lookup"><span data-stu-id="48b3d-148">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span></span>

![URL d’application de correctifs.][image5]

### <a name="check-to-see-that-you-are-updating-the-correct-scoring-endpoint"></a><span data-ttu-id="48b3d-150">Vérifiez que vous mettez à jour le point de terminaison d’évaluation approprié</span><span class="sxs-lookup"><span data-stu-id="48b3d-150">Check to see that you are updating the correct scoring endpoint</span></span>
* <span data-ttu-id="48b3d-151">N’appliquez pas de correctifs au service web de formation : l’opération d’application de correctifs doit être effectuée sur le service web d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="48b3d-151">Do not patch the Training Web Service: The patch operation must be performed on the scoring Web service.</span></span>
* <span data-ttu-id="48b3d-152">N’appliquez pas de correctifs au point de terminaison par défaut du service web : l’opération d’application de correctifs doit être effectuée sur le nouveau point de terminaison du service web d’évaluation que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="48b3d-152">Do not patch the default endpoint on Web service: The patch operation must be performed on the new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="48b3d-153">Vous pouvez vérifier sur quel service web se trouve le point de terminaison en visitant le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="48b3d-153">You can verify which Web service the endpoint is on by visiting the Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="48b3d-154">Veillez à ajouter le point de terminaison au service web prédictif et non au service web d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="48b3d-154">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="48b3d-155">Si vous avez correctement déployé à la fois un service web prédictif et un service web de formation, vous devez voir deux services web distincts répertoriés.</span><span class="sxs-lookup"><span data-stu-id="48b3d-155">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="48b3d-156">Le service web prédictif doit se terminer par « [exp. prédictive] ».</span><span class="sxs-lookup"><span data-stu-id="48b3d-156">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="48b3d-157">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="48b3d-157">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="48b3d-158">Ouvrez l’onglet Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="48b3d-158">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="48b3d-159">![Interface utilisateur de l’espace de travail Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="48b3d-159">![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="48b3d-160">Sélectionnez votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="48b3d-160">Select your workspace.</span></span>
4. <span data-ttu-id="48b3d-161">Cliquez sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="48b3d-161">Click **Web Services**.</span></span>
5. <span data-ttu-id="48b3d-162">Sélectionnez votre service web prédictif.</span><span class="sxs-lookup"><span data-stu-id="48b3d-162">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="48b3d-163">Vérifiez que votre nouveau point de terminaison a été ajouté au service web.</span><span class="sxs-lookup"><span data-stu-id="48b3d-163">Verify that your new endpoint was added to the Web service.</span></span>

### <a name="check-the-workspace-that-your-web-service-is-in-to-ensure-it-is-in-the-correct-region"></a><span data-ttu-id="48b3d-164">Vérifiez l’espace de travail dans lequel votre service web se trouve afin de vous assurer qu’il est dans la région appropriée.</span><span class="sxs-lookup"><span data-stu-id="48b3d-164">Check the workspace that your web service is in to ensure it is in the correct region</span></span>
1. <span data-ttu-id="48b3d-165">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="48b3d-165">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="48b3d-166">Sélectionnez Machine Learning dans le menu.</span><span class="sxs-lookup"><span data-stu-id="48b3d-166">Select Machine Learning from the menu.</span></span>
   <span data-ttu-id="48b3d-167">![Interface utilisateur de la région Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="48b3d-167">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="48b3d-168">Vérifiez l’emplacement de votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="48b3d-168">Verify the location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
