---
title: "service web d’aaaTroubleshoot réapprentissage un Azure Machine Learning Classic | Documents Microsoft"
description: "Identifiez et corrigez rencontré de problèmes courants lorsque vous sont former le modèle de hello pour un Service Web de Azure Machine Learning."
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
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="a6665-103">Résolution des problèmes de hello recyclage d’un service Web classique de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a6665-103">Troubleshooting hello retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="a6665-104">Vue d’ensemble de la reformation</span><span class="sxs-lookup"><span data-stu-id="a6665-104">Retraining overview</span></span>
<span data-ttu-id="a6665-105">Lorsque vous déployez une expérience prédictive en tant que service web d’évaluation, il s’agit d’un modèle statique.</span><span class="sxs-lookup"><span data-stu-id="a6665-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="a6665-106">Comme les nouvelles données sont disponibles ou lorsque le consommateur hello Hello API a ses propres données, modèle de hello doit toobe reformé.</span><span class="sxs-lookup"><span data-stu-id="a6665-106">As new data becomes available or when hello consumer of hello API has their own data, hello model needs toobe retrained.</span></span> 

<span data-ttu-id="a6665-107">Pour obtenir une description complète de hello recyclage de processus d’un service Web classique, consultez [recycler Machine Learning modèles par programme](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="a6665-107">For a complete walkthrough of hello retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="a6665-108">Processus de reformation</span><span class="sxs-lookup"><span data-stu-id="a6665-108">Retraining process</span></span>
<span data-ttu-id="a6665-109">Lorsque vous devez tooretrain hello service Web, vous devez ajouter certains éléments supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="a6665-109">When you need tooretrain hello Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="a6665-110">Un service Web est déployé à partir de hello expérience d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="a6665-110">A Web service deployed from hello Training Experiment.</span></span> <span data-ttu-id="a6665-111">expérience de Hello doit avoir un **sortie du Service Web** module attaché sortie toohello Hello **Train Model** module.</span><span class="sxs-lookup"><span data-stu-id="a6665-111">hello experiment must have a **Web Service Output** module attached toohello output of hello **Train Model** module.</span></span>  
  
    ![Attacher le modèle de hello web service sortie toohello train.][image1]
* <span data-ttu-id="a6665-113">Un nouveau point de terminaison ajouté tooyour calcul du score du service Web.</span><span class="sxs-lookup"><span data-stu-id="a6665-113">A new endpoint added tooyour scoring Web service.</span></span>  <span data-ttu-id="a6665-114">Vous pouvez ajouter des point de terminaison hello par programmation à l’aide des exemples de code hello référencés Bonjour recycler l’apprentissage des modèles par programme rubrique ou via hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="a6665-114">You can add hello endpoint programmatically using hello sample code referenced in hello Retrain Machine Learning models programmatically topic or through hello Azure classic portal.</span></span>

<span data-ttu-id="a6665-115">Vous pouvez ensuite utiliser hello exemple c# code à partir API aide page tooretrain modèle du Service Web hello formation.</span><span class="sxs-lookup"><span data-stu-id="a6665-115">You can then use hello sample C# code from hello Training Web Service's API help page tooretrain model.</span></span> <span data-ttu-id="a6665-116">Une fois que vous avez évalué les résultats hello et soyez satisfaisants, vous mettez à jour formé hello calcul du score du service web à l’aide de hello nouveau point de terminaison que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="a6665-116">Once you have evaluated hello results and are satisfied with them, you update hello trained model scoring web service using hello new endpoint that you added.</span></span>

<span data-ttu-id="a6665-117">Avec tous les éléments de hello en place, les étapes majeures hello vous devez prendre le modèle de hello tooretrain sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="a6665-117">With all hello pieces in place, hello major steps you must take tooretrain hello model are as follows:</span></span>

1. <span data-ttu-id="a6665-118">Appelez hello Service Web de formation : appel de hello est toohello Service de l’exécution de lot (BES), ne Hello pas les demandes de Service de réponse (RR).</span><span class="sxs-lookup"><span data-stu-id="a6665-118">Call hello Training Web Service:  hello call is toohello Batch Execution Service (BES), not hello Request Response Service (RRS).</span></span> <span data-ttu-id="a6665-119">Vous pouvez utiliser le code c# exemple hello astreinte hello API aide page toomake hello.</span><span class="sxs-lookup"><span data-stu-id="a6665-119">You can use hello sample C# code on hello API help page toomake hello call.</span></span> 
2. <span data-ttu-id="a6665-120">Rechercher les valeurs hello hello *BaseLocation*, *RelativeLocation*, et *SasBlobToken*: ces valeurs sont retournées dans la sortie de hello à partir de votre toohello appel Web de formation Service.</span><span class="sxs-lookup"><span data-stu-id="a6665-120">Find hello values for hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in hello output from your call toohello Training Web Service.</span></span> 
   <span data-ttu-id="a6665-121">![affichage de sortie hello Hello réapprentissage exemple et hello BaseLocation, RelativeLocation et SasBlobToken des valeurs.][image6]</span><span class="sxs-lookup"><span data-stu-id="a6665-121">![showing hello output of hello retraining sample and hello BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="a6665-122">Mise à jour hello ajouté modèle entraîné de point de terminaison de hello score de nouveau service web avec hello : à l’aide des exemples de code hello fournies hello recycler l’apprentissage des modèles par programmation, mettre à jour nouveau point de terminaison hello, vous avez ajouté toohello score du modèle avec hello récemment modèle formé à partir de hello formation Web Service.</span><span class="sxs-lookup"><span data-stu-id="a6665-122">Update hello added endpoint from hello scoring web service with hello new trained model: Using hello sample code provided in hello Retrain Machine Learning models programmatically, update hello new endpoint you added toohello scoring model with hello newly trained model from hello Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="a6665-123">Obstacles courants</span><span class="sxs-lookup"><span data-stu-id="a6665-123">Common obstacles</span></span>
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a><span data-ttu-id="a6665-124">Vérifiez toosee si vous avez hello Corrigez-la de correctif logiciel</span><span class="sxs-lookup"><span data-stu-id="a6665-124">Check toosee if you have hello correct PATCH URL</span></span>
<span data-ttu-id="a6665-125">Hello URL de correctif logiciel que vous utilisez doit être hello associé hello nouveau calcul du score du point de terminaison que vous avez ajouté toohello calcul du score du service Web.</span><span class="sxs-lookup"><span data-stu-id="a6665-125">hello PATCH URL you are using must be hello one associated with hello new scoring endpoint you added toohello scoring Web service.</span></span> <span data-ttu-id="a6665-126">Il existe un certain nombre de façons tooobtain hello de correctif logiciel des URL :</span><span class="sxs-lookup"><span data-stu-id="a6665-126">There are a number of ways tooobtain hello PATCH URL:</span></span>

<span data-ttu-id="a6665-127">**Option 1 : par programme**</span><span class="sxs-lookup"><span data-stu-id="a6665-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="a6665-128">tooget hello Corrigez-la de correctif logiciel :</span><span class="sxs-lookup"><span data-stu-id="a6665-128">tooget hello correct PATCH URL:</span></span>

1. <span data-ttu-id="a6665-129">Exécutez hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) exemple de code.</span><span class="sxs-lookup"><span data-stu-id="a6665-129">Run hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="a6665-130">À partir de la sortie de hello de AddEndpoint, recherche hello *HelpLocation* valeur et copier l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="a6665-130">From hello output of AddEndpoint, find hello *HelpLocation* value and copy hello URL.</span></span>
   
   ![HelpLocation sortie hello addEndpoint exemple hello.][image2]
3. <span data-ttu-id="a6665-132">Collez hello URL dans une page du navigateur toonavigate tooa qui fournit des liens d’aide pour le service Web de hello.</span><span class="sxs-lookup"><span data-stu-id="a6665-132">Paste hello URL into a browser toonavigate tooa page that provides help links for hello Web service.</span></span>
4. <span data-ttu-id="a6665-133">Cliquez sur hello **mise à jour de ressource** page d’aide lien tooopen hello correctif.</span><span class="sxs-lookup"><span data-stu-id="a6665-133">Click hello **Update Resource** link tooopen hello patch help page.</span></span>

<span data-ttu-id="a6665-134">**Option 2 : Utiliser hello portail Azure classic**</span><span class="sxs-lookup"><span data-stu-id="a6665-134">**Option 2: Use hello Azure classic portal**</span></span>

1. <span data-ttu-id="a6665-135">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a6665-135">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a6665-136">Onglet d’apprentissage hello ouvert. ![Onglet Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="a6665-136">Open hello Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="a6665-137">Cliquez sur le nom de votre espace de travail, puis sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="a6665-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="a6665-138">Cliquez sur hello calcul du score du service Web que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="a6665-138">Click hello scoring Web service you are working with.</span></span> <span data-ttu-id="a6665-139">(Si vous n’avez pas modifié le nom par défaut de hello du service web de hello, il va se terminer dans [score Exp.].)</span><span class="sxs-lookup"><span data-stu-id="a6665-139">(If you did not modify hello default name of hello web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="a6665-140">Cliquez sur **Ajouter un point de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="a6665-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="a6665-141">Une fois le point de terminaison hello est ajouté, cliquez sur nom de point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="a6665-141">After hello endpoint is added, click hello endpoint name.</span></span> <span data-ttu-id="a6665-142">Puis cliquez sur **mise à jour de ressource** tooopen hello correction page d’aide.</span><span class="sxs-lookup"><span data-stu-id="a6665-142">Then click **Update Resource** tooopen hello patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="a6665-143">Si vous avez ajouté toohello de point de terminaison hello Service Web de formation au lieu de hello prédictive Service Web, vous recevrez l’erreur suivante lorsque vous cliquez sur hello de hello **mise à jour de ressource** lien : nous sommes désolés, mais cette fonctionnalité n’est pas prise en charge ou disponible dans ce contexte.</span><span class="sxs-lookup"><span data-stu-id="a6665-143">If you have added hello endpoint toohello Training Web Service instead of hello Predictive Web Service, you will receive hello following error when you click hello **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="a6665-144">Ce service web n’a aucune ressource actualisable.</span><span class="sxs-lookup"><span data-stu-id="a6665-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="a6665-145">Nous excuser pour tout désagrément de hello et que vous travaillez sur l’amélioration de ce flux de travail.</span><span class="sxs-lookup"><span data-stu-id="a6665-145">We apologize for hello inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Nouveau tableau de bord de point de terminaison.][image3]

<span data-ttu-id="a6665-147">page d’aide du correctif Hello contient hello correctif URL, vous devez utiliser et fournit des exemples de code que vous pouvez utiliser toocall il.</span><span class="sxs-lookup"><span data-stu-id="a6665-147">hello PATCH help page contains hello PATCH URL you must use and provides sample code you can use toocall it.</span></span>

![URL d’application de correctifs.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a><span data-ttu-id="a6665-149">Vérifiez que vous mettez à jour point de terminaison hello correct score de toosee</span><span class="sxs-lookup"><span data-stu-id="a6665-149">Check toosee that you are updating hello correct scoring endpoint</span></span>
* <span data-ttu-id="a6665-150">Pas de correctif logiciel hello Service Web de formation : opération de hello patch doit être effectuée sur hello calcul du score du service Web.</span><span class="sxs-lookup"><span data-stu-id="a6665-150">Do not patch hello Training Web Service: hello patch operation must be performed on hello scoring Web service.</span></span>
* <span data-ttu-id="a6665-151">Correctif pas de point de terminaison hello par défaut sur le service Web : opération de hello patch doit être effectuée sur hello nouveau calcul du score du point de terminaison Web service que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="a6665-151">Do not patch hello default endpoint on Web service: hello patch operation must be performed on hello new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="a6665-152">Vous pouvez vérifier quel point de terminaison Web service hello est sous tension en visite hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="a6665-152">You can verify which Web service hello endpoint is on by visiting hello Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="a6665-153">Assurez-vous que vous ajoutez toohello de point de terminaison hello prédictive Web Service, pas hello formation Web Service.</span><span class="sxs-lookup"><span data-stu-id="a6665-153">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="a6665-154">Si vous avez correctement déployé à la fois un service web prédictif et un service web de formation, vous devez voir deux services web distincts répertoriés.</span><span class="sxs-lookup"><span data-stu-id="a6665-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="a6665-155">Hello prédictive Service Web doit se terminer par « [exp prédictive.] ».</span><span class="sxs-lookup"><span data-stu-id="a6665-155">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="a6665-156">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a6665-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a6665-157">Onglet d’apprentissage hello ouvert. ![Interface utilisateur de l’espace de travail Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="a6665-157">Open hello Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="a6665-158">Sélectionnez votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="a6665-158">Select your workspace.</span></span>
4. <span data-ttu-id="a6665-159">Cliquez sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="a6665-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="a6665-160">Sélectionnez votre service web prédictif.</span><span class="sxs-lookup"><span data-stu-id="a6665-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="a6665-161">Vérifiez que votre nouveau point de terminaison a été ajouté de service Web de toohello.</span><span class="sxs-lookup"><span data-stu-id="a6665-161">Verify that your new endpoint was added toohello Web service.</span></span>

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a><span data-ttu-id="a6665-162">Vérifiez l’espace de travail hello que votre service web est en tooensure, qu'il se trouve dans la région correcte de hello</span><span class="sxs-lookup"><span data-stu-id="a6665-162">Check hello workspace that your web service is in tooensure it is in hello correct region</span></span>
1. <span data-ttu-id="a6665-163">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a6665-163">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a6665-164">Sélectionnez la Machine Learning à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="a6665-164">Select Machine Learning from hello menu.</span></span>
   <span data-ttu-id="a6665-165">![Interface utilisateur de la région Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="a6665-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="a6665-166">Vérifiez l’emplacement hello de votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="a6665-166">Verify hello location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
