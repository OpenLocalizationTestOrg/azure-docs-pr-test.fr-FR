---
title: "(obsolète) Publication du service web Machine Learning sur Azure Marketplace | Microsoft Docs"
description: "(obsolète) Publication du service web Machine Learning sur Azure Marketplace"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: TRUE
ms.openlocfilehash: 3e3420872f0c604e027d1f309a6de6f52a5a788c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a><span data-ttu-id="7b33d-103">(obsolète) Publication du service web Machine Learning sur Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="7b33d-103">(deprecated) Publish Azure Machine Learning Web Service to the Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="7b33d-104">DataMarket et Data Services vont être mis hors service et les abonnements existants seront annulés à compter du 31/03/2017.</span><span class="sxs-lookup"><span data-stu-id="7b33d-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="7b33d-105">Par conséquent, cet article deviendra obsolète.</span><span class="sxs-lookup"><span data-stu-id="7b33d-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="7b33d-106">Vous pouvez aussi publier vos expériences d’apprentissage Machine Learning dans la [galerie Cortana Intelligence](https://gallery.cortanaintelligence.com/) pour les partager avec la communauté spécialiste des données.</span><span class="sxs-lookup"><span data-stu-id="7b33d-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="7b33d-107">Pour plus d’informations, consultez [Partager et découvrir des solutions dans la galerie Cortana Intelligence](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="7b33d-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="7b33d-108">Azure Marketplace offre la possibilité de publier des services web Azure Machine Learning sous forme de services payants ou gratuits que des clients externes pourront consommer.</span><span class="sxs-lookup"><span data-stu-id="7b33d-108">The Azure Marketplace provides the ability to publish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="7b33d-109">Cet article propose une présentation du processus, avec des liens vers les consignes pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="7b33d-109">This article provides an overview of that process with links to guidelines to get you started.</span></span> <span data-ttu-id="7b33d-110">À l’aide de ce processus, vous pouvez mettre vos services Web à disposition d’autres développeurs, qui pourront les consommer dans leurs applications.</span><span class="sxs-lookup"><span data-stu-id="7b33d-110">By using this process, you can make your web services available for other developers to consume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a><span data-ttu-id="7b33d-111">Présentation du processus de publication</span><span class="sxs-lookup"><span data-stu-id="7b33d-111">Overview of the publishing process</span></span>
<span data-ttu-id="7b33d-112">Les étapes suivantes vous permettront de publier un service Web Azure Machine Learning sur Azure Marketplace :</span><span class="sxs-lookup"><span data-stu-id="7b33d-112">The following are the steps for publishing an Azure Machine Learning web service to Azure Marketplace:</span></span>

1. <span data-ttu-id="7b33d-113">Créez et publiez un service Request-Response (Request-Response Service, service de requête-réponse) Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7b33d-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="7b33d-114">Déployez le service en production et obtenez les informations du point de terminaison OData et de la clé d’API.</span><span class="sxs-lookup"><span data-stu-id="7b33d-114">Deploy the service to production, and obtain the API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="7b33d-115">Utilisez l’URL du service Web à publier sur [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="7b33d-115">Use the URL of the published web service to publish to [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="7b33d-116">Une fois soumise, votre offre est évaluée et doit être approuvée avant que vos clients puissent commencer à l'acheter.</span><span class="sxs-lookup"><span data-stu-id="7b33d-116">Once submitted, your offer is reviewed and needs to be approved before your customers can start purchasing it.</span></span> <span data-ttu-id="7b33d-117">Le processus de publication peut prendre quelques jours ouvrés.</span><span class="sxs-lookup"><span data-stu-id="7b33d-117">The publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="7b33d-118">Procédure</span><span class="sxs-lookup"><span data-stu-id="7b33d-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="7b33d-119">Étape 1 : créez et publiez un RRS (Request-Response Service, service de requête-réponse) Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7b33d-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="7b33d-120">Si vous ne l’avez pas encore fait, consultez ce [guide](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="7b33d-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a><span data-ttu-id="7b33d-121">Étape 2 : déployez le service en production et obtenez les informations de point de terminaison OData et de la clé d’API.</span><span class="sxs-lookup"><span data-stu-id="7b33d-121">Step 2: Deploy the service to production, and obtain the API Key and OData endpoint information</span></span>
1. <span data-ttu-id="7b33d-122">Depuis le [portail Azure Classic](http://manage.windowsazure.com), sélectionnez l’option **MACHINE LEARNING** dans la barre de navigation de gauche, puis sélectionnez votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="7b33d-122">From the [Azure Classic Portal](http://manage.windowsazure.com), select the **MACHINE LEARNING** option from the left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="7b33d-123">Cliquez sur l’onglet **WEB SERVICES** (services Web) et sélectionnez le service Web que vous souhaitez publier sur le marché.</span><span class="sxs-lookup"><span data-stu-id="7b33d-123">Click on the **WEB SERVICES** tab, and select the web service you would like to publish to the marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="7b33d-125">Sélectionnez le point de terminaison que vous souhaitez voir consommé par le marché.</span><span class="sxs-lookup"><span data-stu-id="7b33d-125">Select the endpoint you would like to have the marketplace consume.</span></span> <span data-ttu-id="7b33d-126">Si vous n’avez créé aucun point de terminaison supplémentaire, vous pouvez sélectionner le point de terminaison **Default** (par défaut).</span><span class="sxs-lookup"><span data-stu-id="7b33d-126">If you have not created any additional endpoints, you can select the **Default** endpoint.</span></span>
4. <span data-ttu-id="7b33d-127">Une fois que vous avez cliqué sur le point de terminaison, vous voyez la **API KEY** (clé API).</span><span class="sxs-lookup"><span data-stu-id="7b33d-127">Once you have clicked on the endpoint, you will be able to see the **API KEY**.</span></span> <span data-ttu-id="7b33d-128">Vous aurez besoin de cette information par la suite, lors de l’étape 3. Faites-en une copie.</span><span class="sxs-lookup"><span data-stu-id="7b33d-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="7b33d-130">Cliquez sur la méthode **REQUEST/RESPONSE** (requête/réponse). Pour l’instant, nous ne prenons pas en charge la publication de services d’exécution par lots sur le marketplace.</span><span class="sxs-lookup"><span data-stu-id="7b33d-130">Click on the **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services to the marketplace.</span></span> <span data-ttu-id="7b33d-131">Vous serez dirigé sur la page d’aide API pour la méthode Request/Response.</span><span class="sxs-lookup"><span data-stu-id="7b33d-131">That will take you to the API help page for the Request/Response method.</span></span>
6. <span data-ttu-id="7b33d-132">Copiez l’ **OData Endpoint Address**(l’adresse du point de terminaison OData), vous aurez besoin de ces informations ultérieurement, lors de l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="7b33d-132">Copy the **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="7b33d-134">déployez le service en production.</span><span class="sxs-lookup"><span data-stu-id="7b33d-134">deploy the service into production.</span></span>

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a><span data-ttu-id="7b33d-135">Étape 3 : utilisez l’URL du service Web à publier sur Azure Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="7b33d-135">Step 3: Use the URL of the published web service to publish to Azure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="7b33d-136">Accédez à [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="7b33d-136">Navigate to [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="7b33d-137">Cliquez sur le lien **Publish** (Publier) en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="7b33d-137">Click on the **Publish** link at the top of the page.</span></span> <span data-ttu-id="7b33d-138">Vous serez dirigé vers le [portail de publication Microsoft Azure](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="7b33d-138">This will take you to the [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="7b33d-139">Cliquez sur la section **publishers** (éditeurs) pour vous inscrire en tant qu’éditeur.</span><span class="sxs-lookup"><span data-stu-id="7b33d-139">Click on the **publishers** section to register as a publisher.</span></span>
4. <span data-ttu-id="7b33d-140">Durant la création d’une offre, sélectionnez **Services de données**, puis cliquez sur **Créer un nouveau service de données**.</span><span class="sxs-lookup"><span data-stu-id="7b33d-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="7b33d-142">Sous **Plans** , indiquez les informations relatives à votre offre, y compris un plan de tarification.</span><span class="sxs-lookup"><span data-stu-id="7b33d-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="7b33d-143">Vous pouvez choisir de proposer un service payant ou gratuit.</span><span class="sxs-lookup"><span data-stu-id="7b33d-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="7b33d-144">Pour être payé, vous devez indiquer des informations de paiement, notamment vos renseignements bancaires et fiscaux.</span><span class="sxs-lookup"><span data-stu-id="7b33d-144">To get paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="7b33d-145">Sous **Marketing** , vous devez fournir des informations relatives à votre offre, comme son titre et sa description.</span><span class="sxs-lookup"><span data-stu-id="7b33d-145">Under **Marketing** provide information about your offer, such as the title and description for your offer.</span></span>
7. <span data-ttu-id="7b33d-146">Sous **Tarification** , vous pouvez fixer le prix de vos plans pour des pays donnés, ou laisser le système décider lui-même du prix de votre offre.</span><span class="sxs-lookup"><span data-stu-id="7b33d-146">Under **Pricing** you can set the price for your plans for specific countries, or let the system "autoprice" your offer.</span></span>
8. <span data-ttu-id="7b33d-147">Sous l’onglet **Service de données**, cliquez sur **Service Web** pour la **Source de données**.</span><span class="sxs-lookup"><span data-stu-id="7b33d-147">On the **Data Service** tab, click **Web Service** as the **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="7b33d-149">Obtenez l’URL du service web et la clé API à partir du portail Azure Classic, tel qu’expliqué dans l’étape 2 ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7b33d-149">Get the web service URL and API key from the Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="7b33d-150">Dans la boîte de dialogue de configuration du service de données Marketplace, collez l’adresse du point de terminaison OData dans la zone de texte **URL du service** .</span><span class="sxs-lookup"><span data-stu-id="7b33d-150">In the Marketplace Data Service setup dialog box, paste the OData endpoint address into the **Service URL** text box.</span></span>
11. <span data-ttu-id="7b33d-151">Pour **l’authentification**, choisissez **En-tête** comme **Schéma d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7b33d-151">For **Authentication**, choose **Header** as the **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="7b33d-152">Saisissez « Autorisation » comme **nom d’en-tête**.</span><span class="sxs-lookup"><span data-stu-id="7b33d-152">Enter "Authorization" for the **Header Name**.</span></span>
    * <span data-ttu-id="7b33d-153">Pour la **valeur d’en-tête**, entrez « Titulaire » (sans les guillemets), appuyez sur la barre **d’espace** et collez la clé API.</span><span class="sxs-lookup"><span data-stu-id="7b33d-153">For the **Header Value**, enter "Bearer" (without the quotation marks), click the **Space** bar, and then paste the API key.</span></span>
    * <span data-ttu-id="7b33d-154">Cochez la case **Ce service est OData** .</span><span class="sxs-lookup"><span data-stu-id="7b33d-154">Select the **This Service is OData** check box.</span></span>
    * <span data-ttu-id="7b33d-155">Cliquez sur **Tester la connexion** pour tester la connexion.</span><span class="sxs-lookup"><span data-stu-id="7b33d-155">Click **Test Connection** to test the connection.</span></span>
12. <span data-ttu-id="7b33d-156">Sous **Catégories**, assurez-vous que l’option **Apprentissage automatique** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="7b33d-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="7b33d-157">Quand vous avez terminé la saisie de toutes les métadonnées concernant votre offre, cliquez sur **Publier**, puis **Push dans l’environnement intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="7b33d-157">When you are done entering all the metadata about your offer, click on **Publish**, and then **Push to Staging**.</span></span> <span data-ttu-id="7b33d-158">À ce stade, vous recevrez une notification pour chaque problème restant à corriger.</span><span class="sxs-lookup"><span data-stu-id="7b33d-158">At this point, you will be notified of any remaining issues that you need to fix.</span></span>
14. <span data-ttu-id="7b33d-159">Après avoir vérifié l’achèvement de tous les problèmes en suspens, cliquez sur **Demander l’approbation pour pousser vers la Production**.</span><span class="sxs-lookup"><span data-stu-id="7b33d-159">After you have ensured completion of all the outstanding issues, click on **Request approval to push to Production**.</span></span> <span data-ttu-id="7b33d-160">Le processus de publication peut prendre quelques jours ouvrés.</span><span class="sxs-lookup"><span data-stu-id="7b33d-160">The publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

