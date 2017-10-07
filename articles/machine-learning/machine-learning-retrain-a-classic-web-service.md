---
title: aaaRetrain un service web de classique | Documents Microsoft
description: "Découvrez comment tooprogrammatically recycler un modèle et mise à jour hello web service toouse hello qui vient d’être formé dans Azure Machine Learning."
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
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="817fe-103">Reformer un service web Classic</span><span class="sxs-lookup"><span data-stu-id="817fe-103">Retrain a Classic web service</span></span>
<span data-ttu-id="817fe-104">Hello prédictive vous déployé le Service Web est par défaut de hello calcul du score du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="817fe-104">hello Predictive Web Service you deployed is hello default scoring endpoint.</span></span> <span data-ttu-id="817fe-105">Points de terminaison par défaut sont synchronisés avec hello d’origine de jeux d’apprentissage et le score des expériences, et par conséquent hello formé pour le point de terminaison par défaut hello ne peut pas être remplacé.</span><span class="sxs-lookup"><span data-stu-id="817fe-105">Default endpoints are kept in sync with hello original training and scoring experiments, and therefore hello trained model for hello default endpoint cannot be replaced.</span></span> <span data-ttu-id="817fe-106">service web de hello tooretrain, vous devez ajouter un nouveau service web de toohello point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="817fe-106">tooretrain hello web service, you must add a new endpoint toohello web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="817fe-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="817fe-107">Prerequisites</span></span>
<span data-ttu-id="817fe-108">Vous devez avoir configuré une expérience de formation et une expérimentation prédictive comme indiqué dans [Reformer des modèles Machine Learning par programme](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="817fe-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="817fe-109">expérience de prédictive Hello doit être déployé comme un service web d’apprentissage classique.</span><span class="sxs-lookup"><span data-stu-id="817fe-109">hello predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="817fe-110">Pour plus d’informations sur le déploiement de services web, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="817fe-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="817fe-111">Ajouter un nouveau point de terminaison</span><span class="sxs-lookup"><span data-stu-id="817fe-111">Add a new Endpoint</span></span>
<span data-ttu-id="817fe-112">Hello prédictive Service Web que vous avez déployé contient le point de terminaison qui est synchronisé avec l’apprentissage d’origine de hello et calcul de score formé d’expériences de calcul de score par défaut.</span><span class="sxs-lookup"><span data-stu-id="817fe-112">hello Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with hello original training and scoring experiments trained model.</span></span> <span data-ttu-id="817fe-113">tooupdate votre toowith de service web un nouveau modèle formé, vous devez créer un nouveau point de terminaison de score.</span><span class="sxs-lookup"><span data-stu-id="817fe-113">tooupdate your web service toowith a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="817fe-114">toocreate un nouveau calcul de score point de terminaison sur hello prédictive Service Web pouvant être mis à jour avec le modèle formé de hello :</span><span class="sxs-lookup"><span data-stu-id="817fe-114">toocreate a new scoring endpoint, on hello Predictive Web Service that can be updated with hello trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="817fe-115">Assurez-vous que vous ajoutez toohello de point de terminaison hello prédictive Web Service, pas hello formation Web Service.</span><span class="sxs-lookup"><span data-stu-id="817fe-115">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="817fe-116">Si vous avez correctement déployé à la fois un service web prédictif et un service web d’apprentissage, vous devez voir deux services web distincts répertoriés.</span><span class="sxs-lookup"><span data-stu-id="817fe-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="817fe-117">Hello prédictive Service Web doit se terminer par « [exp prédictive.] ».</span><span class="sxs-lookup"><span data-stu-id="817fe-117">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="817fe-118">Il existe trois façons dans laquelle vous pouvez ajouter un nouveau service web de tooa point de terminaison :</span><span class="sxs-lookup"><span data-stu-id="817fe-118">There are three ways in which you can add a new end point tooa web service:</span></span>

1. <span data-ttu-id="817fe-119">Par programmation</span><span class="sxs-lookup"><span data-stu-id="817fe-119">Programmatically</span></span>
2. <span data-ttu-id="817fe-120">Utiliser le portail de Services Web de Microsoft Azure hello</span><span class="sxs-lookup"><span data-stu-id="817fe-120">Use hello Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="817fe-121">Utilisez hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="817fe-121">Use hello Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="817fe-122">Ajouter un point de terminaison par programmation</span><span class="sxs-lookup"><span data-stu-id="817fe-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="817fe-123">Vous pouvez ajouter des points de terminaison de score à l’aide de code hello fourni dans cette [référentiel github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="817fe-123">You can add scoring endpoints using hello sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a><span data-ttu-id="817fe-124">Utilisez tooadd portail de Services Web de Microsoft Azure hello un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="817fe-124">Use hello Microsoft Azure Web Services portal tooadd an endpoint</span></span>
1. <span data-ttu-id="817fe-125">Dans Machine Learning Studio, sur la colonne du volet de navigation gauche hello, cliquez sur les Services Web.</span><span class="sxs-lookup"><span data-stu-id="817fe-125">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="817fe-126">Au bas de hello du tableau de bord de service web hello, cliquez sur **aperçu des points de terminaison de gestion**.</span><span class="sxs-lookup"><span data-stu-id="817fe-126">At hello bottom of hello web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="817fe-127">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="817fe-127">Click **Add**.</span></span>
4. <span data-ttu-id="817fe-128">Tapez un nom et une description pour le nouveau point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="817fe-128">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="817fe-129">Sélectionnez le niveau de journalisation hello et indique si les exemples de données sont activées.</span><span class="sxs-lookup"><span data-stu-id="817fe-129">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="817fe-130">Pour plus d’informations sur la journalisation, consultez [Activation de la journalisation pour les services web de Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="817fe-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a><span data-ttu-id="817fe-131">Utilisez hello tooadd portail classique Azure un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="817fe-131">Use hello Azure classic portal tooadd an endpoint</span></span>
1. <span data-ttu-id="817fe-132">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="817fe-132">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="817fe-133">Dans le menu de gauche hello, cliquez sur **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="817fe-133">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="817fe-134">Sous Nom, cliquez sur votre espace de travail, puis sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="817fe-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="817fe-135">Sous Nom, cliquez sur **Modèle de recensement [exp. prédictive]**.</span><span class="sxs-lookup"><span data-stu-id="817fe-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="817fe-136">Au bas de hello de page de hello, cliquez sur **ajouter le point de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="817fe-136">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="817fe-137">Pour plus d’informations sur l’ajout de points de terminaison, consultez [Création de points de terminaison](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="817fe-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-hello-added-endpoints-trained-model"></a><span data-ttu-id="817fe-138">Hello de mise à jour ajoutée formé du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="817fe-138">Update hello added endpoint’s Trained Model</span></span>
<span data-ttu-id="817fe-139">processus de reconversion hello toocomplete, vous devez mettre à jour modèle formé de hello de hello nouveau point de terminaison que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="817fe-139">toocomplete hello retraining process, you must update hello trained model of hello new endpoint that you added.</span></span>

* <span data-ttu-id="817fe-140">Si vous avez ajouté le nouveau point de terminaison hello à l’aide du portail Azure classic de hello, vous pouvez cliquez sur nom hello nouveau du point de terminaison dans le portail de hello, puis hello **UpdateResource** lien URL de hello tooget vous avez besoin de modèle de tooupdate hello du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="817fe-140">If you added hello new endpoint using hello classic Azure portal, you can click hello new endpoint's name in hello portal, then hello **UpdateResource** link tooget hello URL you would need tooupdate hello endpoint's model.</span></span>
* <span data-ttu-id="817fe-141">Si vous avez ajouté le point de terminaison hello à l’aide des exemples de code hello, cela inclut l’emplacement de l’URL d’aide hello identifié par hello *HelpLocationURL* valeur dans la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="817fe-141">If you added hello endpoint using hello sample code, this includes location of hello help URL identified by hello *HelpLocationURL* value in hello output.</span></span>

<span data-ttu-id="817fe-142">URL du chemin d’accès tooretrieve hello :</span><span class="sxs-lookup"><span data-stu-id="817fe-142">tooretrieve hello path URL:</span></span>

1. <span data-ttu-id="817fe-143">Copiez et collez l’URL de hello dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="817fe-143">Copy and paste hello URL into your browser.</span></span>
2. <span data-ttu-id="817fe-144">Cliquez sur le lien de ressource de la mise à jour de hello.</span><span class="sxs-lookup"><span data-stu-id="817fe-144">Click hello Update Resource link.</span></span>
3. <span data-ttu-id="817fe-145">Copiez hello poster une URL de demande de correctif hello.</span><span class="sxs-lookup"><span data-stu-id="817fe-145">Copy hello POST URL of hello PATCH request.</span></span> <span data-ttu-id="817fe-146">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="817fe-146">For example:</span></span>
   
     <span data-ttu-id="817fe-147">URL DU CORRECTIF : https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="817fe-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="817fe-148">Vous pouvez maintenant utiliser hello de tooupdate hello formé calcul du score du point de terminaison que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="817fe-148">You can now use hello trained model tooupdate hello scoring endpoint that you created previously.</span></span>

<span data-ttu-id="817fe-149">Hello suivant l’exemple de code montre comment toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*et de correctif logiciel tooupdate hello point de terminaison URL.</span><span class="sxs-lookup"><span data-stu-id="817fe-149">hello following sample code shows you how toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL tooupdate hello endpoint.</span></span>

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
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
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

<span data-ttu-id="817fe-150">Hello *apiKey* et hello *endpointUrl* pour l’appel de hello peut être obtenu à partir du tableau de bord de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="817fe-150">hello *apiKey* and hello *endpointUrl* for hello call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="817fe-151">Hello valeur Hello *nom* paramètre dans *ressources* doit hello de correspondance de nom de ressource de hello enregistré formé dans expérience prédictive de hello.</span><span class="sxs-lookup"><span data-stu-id="817fe-151">hello value of hello *Name* parameter in *Resources* should match hello Resource Name of hello saved Trained Model in hello predictive experiment.</span></span> <span data-ttu-id="817fe-152">hello tooget nom de la ressource :</span><span class="sxs-lookup"><span data-stu-id="817fe-152">tooget hello Resource Name:</span></span>

1. <span data-ttu-id="817fe-153">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="817fe-153">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="817fe-154">Dans le menu de gauche hello, cliquez sur **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="817fe-154">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="817fe-155">Sous Nom, cliquez sur votre espace de travail, puis sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="817fe-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="817fe-156">Sous Nom, cliquez sur **Modèle de recensement [exp. prédictive]**.</span><span class="sxs-lookup"><span data-stu-id="817fe-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="817fe-157">Cliquez sur le nouveau point de terminaison hello que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="817fe-157">Click hello new endpoint you added.</span></span>
6. <span data-ttu-id="817fe-158">Dans le tableau de bord du point de terminaison hello, cliquez sur **mise à jour de ressource**.</span><span class="sxs-lookup"><span data-stu-id="817fe-158">On hello endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="817fe-159">Sur la page de mise à jour de documentation sur les API de ressources hello pour le service web de hello, vous pouvez trouver hello **nom de la ressource** sous **être mise à jour des ressources**.</span><span class="sxs-lookup"><span data-stu-id="817fe-159">On hello Update Resource API Documentation page for hello web service, you can find hello **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="817fe-160">Si votre jeton SAS expire avant la fin de la mise à jour du point de terminaison hello, vous devez effectuer une opération GET avec l’Id de tâche de hello tooobtain un nouveau jeton.</span><span class="sxs-lookup"><span data-stu-id="817fe-160">If your SAS token expires before you finish updating hello endpoint, you must perform a GET with hello Job Id tooobtain a fresh token.</span></span>

<span data-ttu-id="817fe-161">Lorsque le code de hello correctement exécutée, nouveau point de terminaison hello doit démarrer à l’aide de modèle de hello reformé dans environ 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="817fe-161">When hello code has successfully run, hello new endpoint should start using hello retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="817fe-162">Résumé</span><span class="sxs-lookup"><span data-stu-id="817fe-162">Summary</span></span>
<span data-ttu-id="817fe-163">À l’aide de hello réapprentissage des API, vous pouvez mettre à jour modèle formé de hello d’un Service Web prédictif, permettant ainsi des scénarios tels que :</span><span class="sxs-lookup"><span data-stu-id="817fe-163">Using hello Retraining APIs, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="817fe-164">Nouvel apprentissage périodique d’un modèle avec de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="817fe-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="817fe-165">Distribution d’un modèle de toocustomers avec comme objectif hello leur permettant de former le modèle de hello à l’aide de leurs propres données.</span><span class="sxs-lookup"><span data-stu-id="817fe-165">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="817fe-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="817fe-166">Next steps</span></span>
[<span data-ttu-id="817fe-167">Résolution des problèmes de hello recyclage d’un service web classique de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="817fe-167">Troubleshooting hello retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

