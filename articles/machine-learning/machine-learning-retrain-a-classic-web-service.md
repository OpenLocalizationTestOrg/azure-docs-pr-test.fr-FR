---
title: Reformer un service web classique | Microsoft Docs
description: "Apprenez à reformer un modèle par programme et à mettre à jour le service Web pour utiliser le modèle reformé dans Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3f9f4cd5ed36262845f7a3139073ccd4e49f472a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="9201a-103">Reformer un service web Classic</span><span class="sxs-lookup"><span data-stu-id="9201a-103">Retrain a Classic web service</span></span>
<span data-ttu-id="9201a-104">Le service web prédictif que vous avez déployé est le point de terminaison de notation par défaut.</span><span class="sxs-lookup"><span data-stu-id="9201a-104">The Predictive Web Service you deployed is the default scoring endpoint.</span></span> <span data-ttu-id="9201a-105">Les points de terminaison par défaut sont toujours synchronisés avec l’expérience originale d’apprentissage et de notation. Par conséquent, le modèle entraîné du point de terminaison par défaut ne peut pas être remplacé.</span><span class="sxs-lookup"><span data-stu-id="9201a-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span></span> <span data-ttu-id="9201a-106">Pour reformer le service web, vous devez ajouter un nouveau point de terminaison au service web.</span><span class="sxs-lookup"><span data-stu-id="9201a-106">To retrain the web service, you must add a new endpoint to the web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9201a-107">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="9201a-107">Prerequisites</span></span>
<span data-ttu-id="9201a-108">Vous devez avoir configuré une expérience de formation et une expérimentation prédictive comme indiqué dans [Reformer des modèles Machine Learning par programme](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="9201a-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9201a-109">L’expérience prédictive doit être déployée comme un service web Machine Learning classique.</span><span class="sxs-lookup"><span data-stu-id="9201a-109">The predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="9201a-110">Pour plus d’informations sur le déploiement de services web, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9201a-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="9201a-111">Ajouter un nouveau point de terminaison</span><span class="sxs-lookup"><span data-stu-id="9201a-111">Add a new Endpoint</span></span>
<span data-ttu-id="9201a-112">Le service web prédictif que vous avez déployé contient un point de terminaison de notation par défaut qui est synchronisé avec le modèle formé pour les expériences de formation et de notation d’origine.</span><span class="sxs-lookup"><span data-stu-id="9201a-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span></span> <span data-ttu-id="9201a-113">Pour mettre à jour votre service web avec un nouveau modèle formé, vous devez créer un point de terminaison de notation.</span><span class="sxs-lookup"><span data-stu-id="9201a-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="9201a-114">Pour créer un nouveau point de terminaison de notation, sur le service web prédictif pouvant être mis à jour avec le modèle entraîné :</span><span class="sxs-lookup"><span data-stu-id="9201a-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="9201a-115">Veillez à ajouter le point de terminaison au service web prédictif et non au service web d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="9201a-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="9201a-116">Si vous avez correctement déployé à la fois un service web prédictif et un service web d’apprentissage, vous devez voir deux services web distincts répertoriés.</span><span class="sxs-lookup"><span data-stu-id="9201a-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="9201a-117">Le service web prédictif doit se terminer par « [exp. prédictive] ».</span><span class="sxs-lookup"><span data-stu-id="9201a-117">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="9201a-118">Pour ajouter un nouveau point de terminaison à un service web, trois options s’offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="9201a-118">There are three ways in which you can add a new end point to a web service:</span></span>

1. <span data-ttu-id="9201a-119">Par programmation</span><span class="sxs-lookup"><span data-stu-id="9201a-119">Programmatically</span></span>
2. <span data-ttu-id="9201a-120">Utilisation du portail de services web Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9201a-120">Use the Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="9201a-121">Utilisation du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="9201a-121">Use the Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="9201a-122">Ajouter un point de terminaison par programmation</span><span class="sxs-lookup"><span data-stu-id="9201a-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="9201a-123">Vous pouvez ajouter des points de terminaison de notation à l’aide de l’exemple de code fourni dans ce [référentiel GitHub](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="9201a-123">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-the-microsoft-azure-web-services-portal-to-add-an-endpoint"></a><span data-ttu-id="9201a-124">Utiliser le portail de services web Microsoft Azure pour ajouter un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="9201a-124">Use the Microsoft Azure Web Services portal to add an endpoint</span></span>
1. <span data-ttu-id="9201a-125">Dans Machine Learning Studio, dans la colonne de navigation de gauche, cliquez sur Services web.</span><span class="sxs-lookup"><span data-stu-id="9201a-125">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="9201a-126">En bas du tableau de bord de services web, cliquez sur **Gérer les points de terminaison (préversion)**.</span><span class="sxs-lookup"><span data-stu-id="9201a-126">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="9201a-127">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="9201a-127">Click **Add**.</span></span>
4. <span data-ttu-id="9201a-128">Tapez un nom et une description pour le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="9201a-128">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="9201a-129">Sélectionnez le niveau de journalisation et activez les exemples de données si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9201a-129">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="9201a-130">Pour plus d’informations sur la journalisation, consultez [Activation de la journalisation pour les services web de Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="9201a-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-the-azure-classic-portal-to-add-an-endpoint"></a><span data-ttu-id="9201a-131">Utiliser le portail Azure Classic pour ajouter un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="9201a-131">Use the Azure classic portal to add an endpoint</span></span>
1. <span data-ttu-id="9201a-132">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9201a-132">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9201a-133">Dans le menu de gauche, cliquez sur **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="9201a-133">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="9201a-134">Sous Nom, cliquez sur votre espace de travail, puis sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="9201a-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="9201a-135">Sous Nom, cliquez sur **Modèle de recensement [exp. prédictive]**.</span><span class="sxs-lookup"><span data-stu-id="9201a-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="9201a-136">En bas de la page, cliquez sur **Ajouter un point de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="9201a-136">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="9201a-137">Pour plus d’informations sur l’ajout de points de terminaison, consultez [Création de points de terminaison](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="9201a-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-the-added-endpoints-trained-model"></a><span data-ttu-id="9201a-138">Mettre à jour le modèle entraîné du point de terminaison ajouté</span><span class="sxs-lookup"><span data-stu-id="9201a-138">Update the added endpoint’s Trained Model</span></span>
<span data-ttu-id="9201a-139">Pour terminer le processus de nouvel entraînement, vous devez mettre à jour le modèle entraîné du nouveau point de terminaison que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="9201a-139">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span></span>

* <span data-ttu-id="9201a-140">Si vous avez ajouté le nouveau point de terminaison à l’aide du portail Azure Classic, vous pouvez cliquer sur le nom du nouveau point de terminaison dans le portail, puis sur le lien **UpdateResource** pour obtenir l’URL dont vous avez besoin pour mettre à jour le modèle du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="9201a-140">If you added the new endpoint using the classic Azure portal, you can click the new endpoint's name in the portal, then the **UpdateResource** link to get the URL you would need to update the endpoint's model.</span></span>
* <span data-ttu-id="9201a-141">Si vous avez ajouté le point de terminaison à l’aide de l’exemple de code, cela inclut l’emplacement de l’URL d’aide identifiée par la valeur *HelpLocationURL* dans la sortie.</span><span class="sxs-lookup"><span data-stu-id="9201a-141">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span></span>

<span data-ttu-id="9201a-142">Pour récupérer l’URL du chemin d’accès :</span><span class="sxs-lookup"><span data-stu-id="9201a-142">To retrieve the path URL:</span></span>

1. <span data-ttu-id="9201a-143">Copiez et collez l’URL dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="9201a-143">Copy and paste the URL into your browser.</span></span>
2. <span data-ttu-id="9201a-144">Cliquez sur le lien Mettre à jour les ressources.</span><span class="sxs-lookup"><span data-stu-id="9201a-144">Click the Update Resource link.</span></span>
3. <span data-ttu-id="9201a-145">Copiez l’URL de la publication de la requête PATCH.</span><span class="sxs-lookup"><span data-stu-id="9201a-145">Copy the POST URL of the PATCH request.</span></span> <span data-ttu-id="9201a-146">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9201a-146">For example:</span></span>
   
     <span data-ttu-id="9201a-147">URL DU CORRECTIF : https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="9201a-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="9201a-148">Vous pouvez maintenant utiliser le modèle entraîné pour mettre à jour le point de terminaison de notation que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="9201a-148">You can now use the trained model to update the scoring endpoint that you created previously.</span></span>

<span data-ttu-id="9201a-149">L’exemple de code suivant montre comment utiliser les éléments *BaseLocation*, *RelativeLocation*, *SasBlobToken* et l’URL d’application de correctifs pour mettre à jour le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="9201a-149">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span></span>

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from the output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from the output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

<span data-ttu-id="9201a-150">L’*apiKey* et l’*endpointUrl* pour l’appel sont figurent sur le tableau de bord du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="9201a-150">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="9201a-151">La valeur du paramètre *Name* dans *Ressources* doit correspondre au nom de ressource du modèle formé enregistré dans l’expérience prédictive.</span><span class="sxs-lookup"><span data-stu-id="9201a-151">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span></span> <span data-ttu-id="9201a-152">Pour obtenir le nom de la ressource :</span><span class="sxs-lookup"><span data-stu-id="9201a-152">To get the Resource Name:</span></span>

1. <span data-ttu-id="9201a-153">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9201a-153">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9201a-154">Dans le menu de gauche, cliquez sur **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="9201a-154">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="9201a-155">Sous Nom, cliquez sur votre espace de travail, puis sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="9201a-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="9201a-156">Sous Nom, cliquez sur **Modèle de recensement [exp. prédictive]**.</span><span class="sxs-lookup"><span data-stu-id="9201a-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="9201a-157">Cliquez sur le nouveau point de terminaison que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="9201a-157">Click the new endpoint you added.</span></span>
6. <span data-ttu-id="9201a-158">Dans le tableau de bord du point de terminaison, cliquez sur **Mettre à jour les ressources**.</span><span class="sxs-lookup"><span data-stu-id="9201a-158">On the endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="9201a-159">Dans la page Documentation de l’API Mettre à jour la ressource du service web, vous trouverez le **Nom de la ressource** sous **Ressources actualisables**.</span><span class="sxs-lookup"><span data-stu-id="9201a-159">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="9201a-160">Si votre jeton SAP expire avant la fin de la mise à jour du point de terminaison, vous devez effectuer une opération GET avec l’ID du travail pour obtenir un nouveau jeton.</span><span class="sxs-lookup"><span data-stu-id="9201a-160">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span></span>

<span data-ttu-id="9201a-161">Lorsque le code a été exécuté avec succès, le nouveau point de terminaison doit commencer à utiliser le modèle de nouveau entraîné après environ 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="9201a-161">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="9201a-162">Résumé</span><span class="sxs-lookup"><span data-stu-id="9201a-162">Summary</span></span>
<span data-ttu-id="9201a-163">À l’aide des API Retraining, vous pouvez mettre à jour le modèle entraîné d’un service web prédictif pour prendre en charge des scénarios tels que :</span><span class="sxs-lookup"><span data-stu-id="9201a-163">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="9201a-164">Nouvel apprentissage périodique d’un modèle avec de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="9201a-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="9201a-165">Distribution d’un modèle auprès des clients dans le but de leur permettre d’effectuer à nouveau l’apprentissage du modèle avec leurs propres données.</span><span class="sxs-lookup"><span data-stu-id="9201a-165">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9201a-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9201a-166">Next steps</span></span>
[<span data-ttu-id="9201a-167">Résolution des problèmes de reformation d’un service web Azure Machine Learning classique</span><span class="sxs-lookup"><span data-stu-id="9201a-167">Troubleshooting the retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

