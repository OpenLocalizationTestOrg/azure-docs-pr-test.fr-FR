---
title: web service tooAzure Marketplace apprentissage publication automatique AAA(deprecated) | Documents Microsoft
description: "(déconseillée) Comment toopublish votre toohello de Service Web de Azure Machine Learning Azure Marketplace"
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
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a><span data-ttu-id="2dcd8-103">(déconseillée) Publier le Service Web de Azure Machine Learning toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="2dcd8-103">(deprecated) Publish Azure Machine Learning Web Service toohello Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="2dcd8-104">DataMarket et Data Services vont être mis hors service et les abonnements existants seront annulés à compter du 31/03/2017.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="2dcd8-105">Par conséquent, cet article deviendra obsolète.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="2dcd8-106">En guise d’alternative, vous pouvez publier votre toohello d’expériences d’apprentissage [Cortana Intelligence galerie](https://gallery.cortanaintelligence.com/) pour avantage hello de communauté de science des données hello.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-106">As an alternative, you can publish your Machine Learning experiments toohello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for hello benefit of hello data science community.</span></span> <span data-ttu-id="2dcd8-107">Pour plus d’informations, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="2dcd8-107">For more information, see [Share and discover resources in hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="2dcd8-108">Bonjour Azure Marketplace permet hello les services web Azure Machine Learning toopublish payée ou libérez de services pour la consommation par les clients externes.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-108">hello Azure Marketplace provides hello ability toopublish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="2dcd8-109">Cet article fournit une vue d’ensemble du processus avec des liens tooget de tooguidelines que vous avez démarré.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-109">This article provides an overview of that process with links tooguidelines tooget you started.</span></span> <span data-ttu-id="2dcd8-110">À l’aide de ce processus, vous proposer vos services web pour les autres tooconsume les développeurs dans leurs applications.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-110">By using this process, you can make your web services available for other developers tooconsume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a><span data-ttu-id="2dcd8-111">Vue d’ensemble du processus de publication de hello</span><span class="sxs-lookup"><span data-stu-id="2dcd8-111">Overview of hello publishing process</span></span>
<span data-ttu-id="2dcd8-112">Hello Voici les étapes de hello pour la publication d’un tooAzure de service web Azure Machine Learning Marketplace :</span><span class="sxs-lookup"><span data-stu-id="2dcd8-112">hello following are hello steps for publishing an Azure Machine Learning web service tooAzure Marketplace:</span></span>

1. <span data-ttu-id="2dcd8-113">Créez et publiez un service Request-Response (Request-Response Service, service de requête-réponse) Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2dcd8-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="2dcd8-114">Déployez hello service tooproduction et obtenir hello les informations de point de terminaison OData et de la clé d’API.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-114">Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="2dcd8-115">Utilisez les URL de hello Hello publié toopublish de service web trop[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="2dcd8-115">Use hello URL of hello published web service toopublish too[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="2dcd8-116">Une fois envoyé, votre offre est examinée et doit toobe approuvée avant son vos clients pouvez commencer à acheter.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-116">Once submitted, your offer is reviewed and needs toobe approved before your customers can start purchasing it.</span></span> <span data-ttu-id="2dcd8-117">processus de publication Hello peut prendre de quelques jours ouvrables.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-117">hello publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="2dcd8-118">Procédure</span><span class="sxs-lookup"><span data-stu-id="2dcd8-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="2dcd8-119">Étape 1 : créez et publiez un RRS (Request-Response Service, service de requête-réponse) Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2dcd8-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="2dcd8-120">Si vous ne l’avez pas encore fait, consultez ce [guide](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="2dcd8-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a><span data-ttu-id="2dcd8-121">Étape 2 : Déployer hello service tooproduction et obtenir hello les informations de point de terminaison OData et de la clé d’API</span><span class="sxs-lookup"><span data-stu-id="2dcd8-121">Step 2: Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information</span></span>
1. <span data-ttu-id="2dcd8-122">À partir de hello [portail classique Azure](http://manage.windowsazure.com), sélectionnez hello **MACHINE LEARNING** option à partir de la barre de navigation gauche hello et sélectionnez votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-122">From hello [Azure Classic Portal](http://manage.windowsazure.com), select hello **MACHINE LEARNING** option from hello left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="2dcd8-123">Cliquez sur hello **SERVICES WEB** onglet et sélectionnez hello web vous aimeriez toopublish toohello marketplace.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-123">Click on hello **WEB SERVICES** tab, and select hello web service you would like toopublish toohello marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="2dcd8-125">Sélectionnez le point de terminaison hello vous comme toohave hello marketplace consomme.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-125">Select hello endpoint you would like toohave hello marketplace consume.</span></span> <span data-ttu-id="2dcd8-126">Si vous n’avez pas créé de points de terminaison supplémentaires, vous pouvez sélectionner hello **par défaut** point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-126">If you have not created any additional endpoints, you can select hello **Default** endpoint.</span></span>
4. <span data-ttu-id="2dcd8-127">Une fois que vous avez cliqué sur le point de terminaison hello, vous serez en mesure de toosee hello **clé API**.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-127">Once you have clicked on hello endpoint, you will be able toosee hello **API KEY**.</span></span> <span data-ttu-id="2dcd8-128">Vous aurez besoin de cette information par la suite, lors de l’étape 3. Faites-en une copie.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="2dcd8-130">Cliquez sur hello **demande/réponse** toohello marketplace de services de méthode, à ce stade, nous ne prennent pas en charge la publication de l’exécution par lots.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-130">Click on hello **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services toohello marketplace.</span></span> <span data-ttu-id="2dcd8-131">Que vous obtiendrez la page d’aide toohello API hello méthode de demande/réponse.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-131">That will take you toohello API help page for hello Request/Response method.</span></span>
6. <span data-ttu-id="2dcd8-132">Hello de copie **adresse de point de terminaison OData**, vous devez ces informations ultérieurement à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-132">Copy hello **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="2dcd8-134">déployer un service de hello en production.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-134">deploy hello service into production.</span></span>

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a><span data-ttu-id="2dcd8-135">Étape 3 : Utilisation des URL de hello Hello publié web service toopublish tooAzure Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="2dcd8-135">Step 3: Use hello URL of hello published web service toopublish tooAzure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="2dcd8-136">Accédez trop[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="2dcd8-136">Navigate too[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="2dcd8-137">Cliquez sur hello **publier** lien en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-137">Click on hello **Publish** link at hello top of hello page.</span></span> <span data-ttu-id="2dcd8-138">Cette opération prendra toohello [portail de publication Microsoft Azure](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="2dcd8-138">This will take you toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="2dcd8-139">Cliquez sur hello **éditeurs** tooregister section comme serveur de publication.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-139">Click on hello **publishers** section tooregister as a publisher.</span></span>
4. <span data-ttu-id="2dcd8-140">Durant la création d’une offre, sélectionnez **Services de données**, puis cliquez sur **Créer un nouveau service de données**.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="2dcd8-142">Sous **Plans** , indiquez les informations relatives à votre offre, y compris un plan de tarification.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="2dcd8-143">Vous pouvez choisir de proposer un service payant ou gratuit.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="2dcd8-144">tooget payé, fournissent des informations de paiement telles que vos informations bancaires et les taxes.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-144">tooget paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="2dcd8-145">Sous **Marketing** fournissent des informations sur votre offre, telles que le titre de hello et une description pour votre offre.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-145">Under **Marketing** provide information about your offer, such as hello title and description for your offer.</span></span>
7. <span data-ttu-id="2dcd8-146">Sous **tarification** vous pouvez définir les prix hello pour vos plans pour pays spécifiques, ou laissez le système hello « autoprice » dans votre offre.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-146">Under **Pricing** you can set hello price for your plans for specific countries, or let hello system "autoprice" your offer.</span></span>
8. <span data-ttu-id="2dcd8-147">Sur hello **Service de données** , cliquez sur **Service Web** comme hello **Source de données**.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-147">On hello **Data Service** tab, click **Web Service** as hello **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="2dcd8-149">Obtenir hello web service URL et la clé API hello portail Azure Classic, comme expliqué à l’étape 2 ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-149">Get hello web service URL and API key from hello Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="2dcd8-150">Dans la boîte de dialogue de configuration de Service de données Marketplace de hello, collez adresse de point de terminaison OData hello hello **URL du Service** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-150">In hello Marketplace Data Service setup dialog box, paste hello OData endpoint address into hello **Service URL** text box.</span></span>
11. <span data-ttu-id="2dcd8-151">Pour **authentification**, choisissez **en-tête** comme hello **schéma d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-151">For **Authentication**, choose **Header** as hello **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="2dcd8-152">Entrez « Authorization » pour hello **nom d’en-tête**.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-152">Enter "Authorization" for hello **Header Name**.</span></span>
    * <span data-ttu-id="2dcd8-153">Pourquoi **valeur d’en-tête**, entrez « Support » (sans les guillemets hello), cliquez sur hello **espace** barre, puis collez la clé d’API de hello.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-153">For hello **Header Value**, enter "Bearer" (without hello quotation marks), click hello **Space** bar, and then paste hello API key.</span></span>
    * <span data-ttu-id="2dcd8-154">Sélectionnez hello **ce Service est OData** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-154">Select hello **This Service is OData** check box.</span></span>
    * <span data-ttu-id="2dcd8-155">Cliquez sur **tester la connexion** connexion de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-155">Click **Test Connection** tootest hello connection.</span></span>
12. <span data-ttu-id="2dcd8-156">Sous **Catégories**, assurez-vous que l’option **Apprentissage automatique** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="2dcd8-157">Lorsque vous avez terminé de saisir toutes hello métadonnées sur votre offre, cliquez sur **publier**, puis **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-157">When you are done entering all hello metadata about your offer, click on **Publish**, and then **Push tooStaging**.</span></span> <span data-ttu-id="2dcd8-158">À ce stade, vous soient prévenus de tous les problèmes restants que vous avez besoin de toofix.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-158">At this point, you will be notified of any remaining issues that you need toofix.</span></span>
14. <span data-ttu-id="2dcd8-159">Une fois que vous avez vérifié que l’achèvement de tous les problèmes en suspens hello, cliquez sur **demander l’approbation toopush tooProduction**.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-159">After you have ensured completion of all hello outstanding issues, click on **Request approval toopush tooProduction**.</span></span> <span data-ttu-id="2dcd8-160">processus de publication Hello peut prendre de quelques jours ouvrables.</span><span class="sxs-lookup"><span data-stu-id="2dcd8-160">hello publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

