---
title: "Complément Excel pour les services web Machine Learning | Microsoft Docs"
description: "Comment utiliser les services web Azure Machine Learning directement dans Excel sans écrire de code."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: 0d60dd87bbdd4d3eafac0f8876cc9e41412a53ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="72733-103">Complément Excel de services web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="72733-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="72733-104">Excel permet d'appeler facilement des services web directement sans qu'il soit nécessaire d'écrire du code.</span><span class="sxs-lookup"><span data-stu-id="72733-104">Excel makes it easy to call web services directly without the need to write any code.</span></span>

## <a name="steps-to-use-an-existing-web-service-in-the-workbook"></a><span data-ttu-id="72733-105">Procédure d’utilisation d’un service web existant dans le classeur</span><span class="sxs-lookup"><span data-stu-id="72733-105">Steps to Use an Existing web service in the Workbook</span></span>

1. <span data-ttu-id="72733-106">Ouvrez l’ [exemple de fichier Excel](http://aka.ms/amlexcel-sample-2), qui contient le complément Excel et les données concernant les passagers sur le Titanic.</span><span class="sxs-lookup"><span data-stu-id="72733-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span></span>
2. <span data-ttu-id="72733-107">Choisissez le service web en cliquant dessus : « Titanic Survivor Predictor (exemple de complément Excel) [Score] » dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="72733-107">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Sélectionner un service web][01]
3. <span data-ttu-id="72733-109">Vous accédez alors à la section **Prédire**.</span><span class="sxs-lookup"><span data-stu-id="72733-109">This takes you to the **Predict** section.</span></span>  <span data-ttu-id="72733-110">Ce classeur contient déjà des exemples de données mais, pour un classeur vide, vous pouvez également sélectionner une cellule dans Excel et cliquer sur **Utiliser les exemples de données**.</span><span class="sxs-lookup"><span data-stu-id="72733-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="72733-111">Sélectionnez les données avec les en-têtes et cliquez sur l'icône de plage de données d'entrée.</span><span class="sxs-lookup"><span data-stu-id="72733-111">Select the data with headers and click the input data range icon.</span></span>  <span data-ttu-id="72733-112">Assurez-vous que la case « Mes données ont des en-têtes » est activée.</span><span class="sxs-lookup"><span data-stu-id="72733-112">Make sure the "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="72733-113">Sous **Sortie**, entrez le numéro de la cellule dans laquelle vous souhaitez insérer le résultat, en l’occurrence, « H1 ».</span><span class="sxs-lookup"><span data-stu-id="72733-113">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span></span>
6. <span data-ttu-id="72733-114">Cliquez sur **Prédire**.</span><span class="sxs-lookup"><span data-stu-id="72733-114">Click **Predict**.</span></span>
   
    ![Section Prédire][02]

<span data-ttu-id="72733-116">Déployez un service web ou utilisez un service web existant.</span><span class="sxs-lookup"><span data-stu-id="72733-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="72733-117">Pour plus d’informations sur le déploiement d’un service web, consultez la rubrique [Étape 5 du didacticiel pas à pas : Déploiement du service web Azure Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="72733-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="72733-118">Obtenez la clé API de votre service web.</span><span class="sxs-lookup"><span data-stu-id="72733-118">Get the API key for your web service.</span></span> <span data-ttu-id="72733-119">L’emplacement à partir duquel exécutez cette action diffère selon que vous avez publié un service web Machine Learning classique ou un nouveau service web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="72733-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="72733-120">**Utiliser un service web classique**</span><span class="sxs-lookup"><span data-stu-id="72733-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="72733-121">Dans Machine Learning Studio, cliquez sur la section **WEB SERVICES** située sur le volet de gauche, puis sélectionnez le service web.</span><span class="sxs-lookup"><span data-stu-id="72733-121">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span></span>
   
    ![Studio - Sélectionner un service web][04]
2. <span data-ttu-id="72733-123">Copiez la clé API du service web.</span><span class="sxs-lookup"><span data-stu-id="72733-123">Copy the API key for the web service.</span></span>
   
    ![Studio clé API][05]
3. <span data-ttu-id="72733-125">Sous l’onglet **TABLEAU DE BORD** pour le service web, cliquez sur le lien **REQUÊTE/RÉPONSE**.</span><span class="sxs-lookup"><span data-stu-id="72733-125">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="72733-126">Recherchez la section **URI de requête** .</span><span class="sxs-lookup"><span data-stu-id="72733-126">Look for the **Request URI** section.</span></span>  <span data-ttu-id="72733-127">Copiez et enregistrez l’URL.</span><span class="sxs-lookup"><span data-stu-id="72733-127">Copy and save the URL.</span></span>

> [!NOTE]
> <span data-ttu-id="72733-128">Il est désormais possible de se connecter au portail [Azure Machine Learning Web Services](https://services.azureml.net) pour obtenir la clé API d’un service web Machine Learning classique.</span><span class="sxs-lookup"><span data-stu-id="72733-128">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="72733-129">**Utiliser un nouveau service web**</span><span class="sxs-lookup"><span data-stu-id="72733-129">**Use a New web service**</span></span>

1. <span data-ttu-id="72733-130">Dans le portail [Services web Azure Machine Learning](https://services.azureml.net), cliquez sur **Services web**, puis sélectionnez votre service web.</span><span class="sxs-lookup"><span data-stu-id="72733-130">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="72733-131">Cliquez sur **Consommer**.</span><span class="sxs-lookup"><span data-stu-id="72733-131">Click **Consume**.</span></span>
3. <span data-ttu-id="72733-132">Recherchez la section **des informations de base sur la consommation** .</span><span class="sxs-lookup"><span data-stu-id="72733-132">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="72733-133">Copiez et enregistrez la **Clé primaire** et l’URL de **Demande-réponse**.</span><span class="sxs-lookup"><span data-stu-id="72733-133">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>

## <a name="steps-to-add-a-new-web-service"></a><span data-ttu-id="72733-134">Procédure d’ajout d’un nouveau service web</span><span class="sxs-lookup"><span data-stu-id="72733-134">Steps to Add a New web service</span></span>

1. <span data-ttu-id="72733-135">Déployez un service web ou utilisez un service web existant.</span><span class="sxs-lookup"><span data-stu-id="72733-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="72733-136">Pour plus d’informations sur le déploiement d’un service web, consultez la rubrique [Étape 5 du didacticiel pas à pas : Déploiement du service web Azure Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="72733-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="72733-137">Cliquez sur **Consommer**.</span><span class="sxs-lookup"><span data-stu-id="72733-137">Click **Consume**.</span></span>
3. <span data-ttu-id="72733-138">Recherchez la section **des informations de base sur la consommation** .</span><span class="sxs-lookup"><span data-stu-id="72733-138">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="72733-139">Copiez et enregistrez la **Clé primaire** et l’URL de **Demande-réponse**.</span><span class="sxs-lookup"><span data-stu-id="72733-139">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>
4. <span data-ttu-id="72733-140">Dans Excel, accédez à la section **Services web** (si vous vous trouvez dans la section **Prédire**, cliquez sur la flèche de retour pour accéder à la liste des services web).</span><span class="sxs-lookup"><span data-stu-id="72733-140">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span></span>
   
    ![Accéder à la sélection du service web][03]
5. <span data-ttu-id="72733-142">Cliquez sur **Ajouter un service web**.</span><span class="sxs-lookup"><span data-stu-id="72733-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="72733-143">Collez l’URL dans la zone de texte du complément Excel intitulée **URL**.</span><span class="sxs-lookup"><span data-stu-id="72733-143">Paste the URL into the Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="72733-144">Collez l’API/Clé primaire dans la zone de texte intitulée **Clé API**.</span><span class="sxs-lookup"><span data-stu-id="72733-144">Paste the API/Primary key into the text box labeled **API key**.</span></span>
8. <span data-ttu-id="72733-145">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="72733-145">Click **Add**.</span></span>
   
    ![URL et clé API pour un service web classique.][06]
9. <span data-ttu-id="72733-147">Pour utiliser le service web, suivez les instructions de la section « Procédure d’utilisation d’un service web existant » ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="72733-147">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="72733-148">Partage de votre classeur</span><span class="sxs-lookup"><span data-stu-id="72733-148">Sharing Your Workbook</span></span>
<span data-ttu-id="72733-149">Si vous enregistrez votre classeur, l'API/la clé primaire pour les services web que vous avez ajoutés seront également enregistrés.</span><span class="sxs-lookup"><span data-stu-id="72733-149">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span></span> <span data-ttu-id="72733-150">Cela signifie que vous devez uniquement partager le classeur avec des personnes de confiance.</span><span class="sxs-lookup"><span data-stu-id="72733-150">That means you should only share the workbook with individuals you trust.</span></span>

<span data-ttu-id="72733-151">Posez les questions que vous voulez dans la section de commentaire suivante ou dans notre [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="72733-151">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
