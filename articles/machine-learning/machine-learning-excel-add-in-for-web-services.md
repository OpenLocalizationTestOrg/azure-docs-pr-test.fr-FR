---
title: "complément aaaExcel pour les services Web d’apprentissage Machine | Documents Microsoft"
description: "Comment toouse Azure Machine Learning Web services directement dans Excel sans écrire de code."
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
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="b26cc-103">Complément Excel de services web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b26cc-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="b26cc-104">Excel rend toocall facilement des services web directement sans hello besoin toowrite n’importe quel code.</span><span class="sxs-lookup"><span data-stu-id="b26cc-104">Excel makes it easy toocall web services directly without hello need toowrite any code.</span></span>

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a><span data-ttu-id="b26cc-105">Étapes tooUse un service web existant hello classeur</span><span class="sxs-lookup"><span data-stu-id="b26cc-105">Steps tooUse an Existing web service in hello Workbook</span></span>

1. <span data-ttu-id="b26cc-106">Ouvrez hello [exemple de fichier Excel](http://aka.ms/amlexcel-sample-2), qui contient du complément Excel hello et données concernant les passagers sur hello TITANE.</span><span class="sxs-lookup"><span data-stu-id="b26cc-106">Open hello [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains hello Excel add-in and data about passengers on hello Titanic.</span></span>
2. <span data-ttu-id="b26cc-107">Choisissez le service web de hello en cliquant dessus-« Titanic survivant PRÉDICTEUR (exemple de complément Excel) [Score] » dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="b26cc-107">Choose hello web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Sélectionner un service web][01]
3. <span data-ttu-id="b26cc-109">Vous accéderez toohello **Predict** section.</span><span class="sxs-lookup"><span data-stu-id="b26cc-109">This takes you toohello **Predict** section.</span></span>  <span data-ttu-id="b26cc-110">Ce classeur contient déjà des exemples de données mais, pour un classeur vide, vous pouvez également sélectionner une cellule dans Excel et cliquer sur **Utiliser les exemples de données**.</span><span class="sxs-lookup"><span data-stu-id="b26cc-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="b26cc-111">Sélectionnez les données hello avec les en-têtes, puis cliquez sur icône des tranches de données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="b26cc-111">Select hello data with headers and click hello input data range icon.</span></span>  <span data-ttu-id="b26cc-112">Vérifiez que hello « mes données comportent des en-têtes » est activée.</span><span class="sxs-lookup"><span data-stu-id="b26cc-112">Make sure hello "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="b26cc-113">Sous **sortie**, entrez le nombre de cellules hello hello toobe de sortie, par exemple « H1 » ici.</span><span class="sxs-lookup"><span data-stu-id="b26cc-113">Under **Output**, enter hello cell number where you want hello output toobe, for example "H1" here.</span></span>
6. <span data-ttu-id="b26cc-114">Cliquez sur **Prédire**.</span><span class="sxs-lookup"><span data-stu-id="b26cc-114">Click **Predict**.</span></span>
   
    ![Section Prédire][02]

<span data-ttu-id="b26cc-116">Déployez un service web ou utilisez un service web existant.</span><span class="sxs-lookup"><span data-stu-id="b26cc-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="b26cc-117">Pour plus d’informations sur le déploiement d’un service web, consultez [procédure pas à pas étape 5 : déployer le service d’Azure Machine Learning Web hello](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="b26cc-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="b26cc-118">Obtenir la clé d’API hello pour votre service web.</span><span class="sxs-lookup"><span data-stu-id="b26cc-118">Get hello API key for your web service.</span></span> <span data-ttu-id="b26cc-119">L’emplacement à partir duquel exécutez cette action diffère selon que vous avez publié un service web Machine Learning classique ou un nouveau service web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="b26cc-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="b26cc-120">**Utiliser un service web classique**</span><span class="sxs-lookup"><span data-stu-id="b26cc-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="b26cc-121">Dans Machine Learning Studio, cliquez sur hello **SERVICES WEB** section dans le volet gauche de hello, puis sélectionnez le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="b26cc-121">In Machine Learning Studio, click hello **WEB SERVICES** section in hello left pane, and then select hello web service.</span></span>
   
    ![Studio - Sélectionner un service web][04]
2. <span data-ttu-id="b26cc-123">Copiez la clé d’API hello pour le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="b26cc-123">Copy hello API key for hello web service.</span></span>
   
    ![Studio clé API][05]
3. <span data-ttu-id="b26cc-125">Sur hello **tableau de bord** pour le service web de hello, cliquez sur hello **demande/réponse** lien.</span><span class="sxs-lookup"><span data-stu-id="b26cc-125">On hello **DASHBOARD** tab for hello web service, click hello **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="b26cc-126">Recherchez hello **URI de requête** section.</span><span class="sxs-lookup"><span data-stu-id="b26cc-126">Look for hello **Request URI** section.</span></span>  <span data-ttu-id="b26cc-127">Copiez et enregistrez l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="b26cc-127">Copy and save hello URL.</span></span>

> [!NOTE]
> <span data-ttu-id="b26cc-128">Il est désormais possible toosign dans hello [Azure Machine Learning Web Services](https://services.azureml.net) clé de hello API tooobtain portail pour un service web d’apprentissage classique.</span><span class="sxs-lookup"><span data-stu-id="b26cc-128">It is now possible toosign into hello [Azure Machine Learning Web Services](https://services.azureml.net) portal tooobtain hello API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="b26cc-129">**Utiliser un nouveau service web**</span><span class="sxs-lookup"><span data-stu-id="b26cc-129">**Use a New web service**</span></span>

1. <span data-ttu-id="b26cc-130">Bonjour [Azure Machine Learning Web Services](https://services.azureml.net) portail, cliquez sur **Services Web**, puis sélectionnez votre service web.</span><span class="sxs-lookup"><span data-stu-id="b26cc-130">In hello [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="b26cc-131">Cliquez sur **Consommer**.</span><span class="sxs-lookup"><span data-stu-id="b26cc-131">Click **Consume**.</span></span>
3. <span data-ttu-id="b26cc-132">Recherchez hello **les informations de base de la consommation** section.</span><span class="sxs-lookup"><span data-stu-id="b26cc-132">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="b26cc-133">Copiez et enregistrez hello **clé primaire** et hello **demande-réponse** URL.</span><span class="sxs-lookup"><span data-stu-id="b26cc-133">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>

## <a name="steps-tooadd-a-new-web-service"></a><span data-ttu-id="b26cc-134">Étapes tooAdd un nouveau service web</span><span class="sxs-lookup"><span data-stu-id="b26cc-134">Steps tooAdd a New web service</span></span>

1. <span data-ttu-id="b26cc-135">Déployez un service web ou utilisez un service web existant.</span><span class="sxs-lookup"><span data-stu-id="b26cc-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="b26cc-136">Pour plus d’informations sur le déploiement d’un service web, consultez [procédure pas à pas étape 5 : déployer le service d’Azure Machine Learning Web hello](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="b26cc-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="b26cc-137">Cliquez sur **Consommer**.</span><span class="sxs-lookup"><span data-stu-id="b26cc-137">Click **Consume**.</span></span>
3. <span data-ttu-id="b26cc-138">Recherchez hello **les informations de base de la consommation** section.</span><span class="sxs-lookup"><span data-stu-id="b26cc-138">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="b26cc-139">Copiez et enregistrez hello **clé primaire** et hello **demande-réponse** URL.</span><span class="sxs-lookup"><span data-stu-id="b26cc-139">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>
4. <span data-ttu-id="b26cc-140">Dans Excel, accédez à toohello **Services Web** section (si vous êtes dans hello **Predict** , cliquez sur la liste de toohello toogo hello flèche précédent de services web).</span><span class="sxs-lookup"><span data-stu-id="b26cc-140">In Excel, go toohello **Web Services** section (if you are in hello **Predict** section, click hello back arrow toogo toohello list of web services).</span></span>
   
    ![Atteindre la sélection du service tooWeb][03]
5. <span data-ttu-id="b26cc-142">Cliquez sur **Ajouter un service web**.</span><span class="sxs-lookup"><span data-stu-id="b26cc-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="b26cc-143">Collez les URL hello hello Excel intitulé de la zone de texte du complément **URL**.</span><span class="sxs-lookup"><span data-stu-id="b26cc-143">Paste hello URL into hello Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="b26cc-144">Clé d’API/primaire de hello coller dans la zone de texte hello **clé API**.</span><span class="sxs-lookup"><span data-stu-id="b26cc-144">Paste hello API/Primary key into hello text box labeled **API key**.</span></span>
8. <span data-ttu-id="b26cc-145">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="b26cc-145">Click **Add**.</span></span>
   
    ![URL et clé API pour un service web classique.][06]
9. <span data-ttu-id="b26cc-147">service web de hello toouse, suivez hello précédant directions, « Étapes tooUse un Service de serveur web existant ».</span><span class="sxs-lookup"><span data-stu-id="b26cc-147">toouse hello web service, follow hello preceding directions, "Steps tooUse an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="b26cc-148">Partage de votre classeur</span><span class="sxs-lookup"><span data-stu-id="b26cc-148">Sharing Your Workbook</span></span>
<span data-ttu-id="b26cc-149">Si vous enregistrez votre classeur, puis clé d’API/primaire hello pour les services web hello que vous avez ajouté est également enregistré.</span><span class="sxs-lookup"><span data-stu-id="b26cc-149">If you save your workbook, then hello API/Primary key for hello web services you have added is also saved.</span></span> <span data-ttu-id="b26cc-150">Cela signifie que vous devez uniquement partager les classeur hello avec des personnes de que confiance.</span><span class="sxs-lookup"><span data-stu-id="b26cc-150">That means you should only share hello workbook with individuals you trust.</span></span>

<span data-ttu-id="b26cc-151">Poser des questions dans hello suivant la section commentaires ou sur notre [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="b26cc-151">Ask any questions in hello following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
