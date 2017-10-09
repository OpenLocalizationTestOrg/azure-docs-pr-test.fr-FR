---
title: "aaaTesting votre Service de données de la plateforme pour hello Marketplace | Documents Microsoft"
description: "Comprendre comment tootest votre Service de données de la plateforme pour hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="8b75e-103">Tester votre offre de service de données dans l'emplacement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="8b75e-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8b75e-104">**À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.**</span><span class="sxs-lookup"><span data-stu-id="8b75e-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="8b75e-105">Si vous avez une application SaaS vous aimeriez toopublish sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="8b75e-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="8b75e-106">Si vous avez des applications IaaS ou développeur de service vous serait comme toopublish sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="8b75e-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="8b75e-107">Après avoir effectué les deux premières étapes de hello de [création de votre compte Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) et [création de votre offre de Service de données dans le portail de publication](marketplace-publishing-data-service-creation.md) vous êtes prêt pour la disposition de votre offre Bonjour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8b75e-107">After completing hello first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in hello Azure Marketplace.</span></span> <span data-ttu-id="8b75e-108">Cette rubrique vous guident tout hello tout d’abord, intermédiaires, étape appelée « étape intermédiaire »</span><span class="sxs-lookup"><span data-stu-id="8b75e-108">This topic will walk you through hello first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="8b75e-109">Désigne un déploiement de votre offre un « bac à sable » où vous pouvez tester et vérifier son fonctionnement avant d’en exécutant un push tooproduction privé de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="8b75e-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="8b75e-110">offre de Hello s’affiche dans la mise en lots comme il le ferait client tooa qui a déployé.</span><span class="sxs-lookup"><span data-stu-id="8b75e-110">hello offer will appear in staging just as it would tooa customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-toostaging"></a><span data-ttu-id="8b75e-111">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="8b75e-111">Step 1.</span></span> <span data-ttu-id="8b75e-112">En exécutant un push de votre offre toostaging</span><span class="sxs-lookup"><span data-stu-id="8b75e-112">Pushing your offer toostaging</span></span>
<span data-ttu-id="8b75e-113">En exécutant un push de votre toostaging offre vous permet d’offre de hello tootest avant de devenir disponible toofuture abonnés.</span><span class="sxs-lookup"><span data-stu-id="8b75e-113">Pushing your offer toostaging allows you tootest hello offer before it becomes available toofuture subscribers.</span></span>  <span data-ttu-id="8b75e-114">Vous pouvez voir comment votre offre apparaît et la fonction pour ceux qui s’abonnent tooyour données.</span><span class="sxs-lookup"><span data-stu-id="8b75e-114">You can see how your offer will appear and function for those subscribing tooyour data.</span></span>  

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="8b75e-116">La connexion en hello [portail de publication](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="8b75e-116">Login into hello [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="8b75e-117">Sélectionnez **Data Services** dans la fenêtre de navigation gauche hello</span><span class="sxs-lookup"><span data-stu-id="8b75e-117">Select **Data Services** in hello left navigation window</span></span>
3. <span data-ttu-id="8b75e-118">Sélectionnez votre offre que vous souhaitez toopush toostaging.</span><span class="sxs-lookup"><span data-stu-id="8b75e-118">Select your offer you want toopush toostaging.</span></span> <span data-ttu-id="8b75e-119">Vous verrez hello au-dessus d’écran.</span><span class="sxs-lookup"><span data-stu-id="8b75e-119">You will see hello above screen.</span></span>
4. <span data-ttu-id="8b75e-120">Cliquez sur **Push tooStaging** bouton.</span><span class="sxs-lookup"><span data-stu-id="8b75e-120">Click **Push tooStaging** button.</span></span>  
5. <span data-ttu-id="8b75e-121">Si des problèmes avec hello offre qui nécessaire toobe terminée préalable toopushing toostaging, vous verrez la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="8b75e-121">If there are issues with hello offer that needed toobe completed prior toopushing toostaging, you will see a list displayed.</span></span>  <span data-ttu-id="8b75e-122">Corriger ces éléments en cliquant sur chaque élément de liste de hello.</span><span class="sxs-lookup"><span data-stu-id="8b75e-122">Correct these items by clicking on each item in hello list.</span></span> <span data-ttu-id="8b75e-123">Lorsque toutes les corrections effectuées, cliquez sur **Push tooStaging** bouton Nouveau.</span><span class="sxs-lookup"><span data-stu-id="8b75e-123">When all corrections made, click **Push tooStaging** button again.</span></span>

<span data-ttu-id="8b75e-124">S’il n’y a aucun problème avec votre offre, vous verrez fenêtre hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8b75e-124">If there are no issues with your offer you will see hello popup window below.</span></span>  

<span data-ttu-id="8b75e-125">Si vous n’êtes pas planification/non approuvées toosurface votre offre dans le portail Azure (actuellement a une capacité limitée), puis la fenêtre contextuelle de hello simplement fermer.</span><span class="sxs-lookup"><span data-stu-id="8b75e-125">If you’re not planning/not approved toosurface your offer in Azure Portal (currently has limited capacity), then just close hello pop-up window.</span></span>

<span data-ttu-id="8b75e-126">tootest vos données de Service dans le portail Azure (dans le portail de DataMarket toohello ajout), vous aurez besoin d’un tootest ID d’abonnement Azure avec.</span><span class="sxs-lookup"><span data-stu-id="8b75e-126">tootest your Data Service in Azure Portal (in addition toohello DataMarket portal), you will need an Azure Subscription ID tootest with.</span></span>  <span data-ttu-id="8b75e-127">Cet ID d’abonnement identifiera compte hello qui sera autorisée tootest votre offre.</span><span class="sxs-lookup"><span data-stu-id="8b75e-127">This Subscription ID will identify hello account that will be allowed tootest your offer.</span></span>  

<span data-ttu-id="8b75e-128">Coupez et collez votre ID d’abonnement et cliquez sur hello coche toocontinue.</span><span class="sxs-lookup"><span data-stu-id="8b75e-128">Cut and paste your Subscription ID and click hello checkmark toocontinue.</span></span>

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="8b75e-130">Ces ID abonnements Azure est uniquement requises pour le test et de mise en lots Bonjour [portail de gestion Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8b75e-130">These Azure subscriptions IDs are only required for testing and staging in hello [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="8b75e-131">Ils ne sont pas requis tootest dans Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8b75e-131">They are not required tootest in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="8b75e-132">Hello écran suivant montre que la publication se déroule en affichant hello « en cours » icône mise en surbrillance jaune ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8b75e-132">hello next screen that appears shows that publishing is taking place by displaying hello “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="8b75e-133">En exécutant un push toostaging prend 10 minutes de too15.</span><span class="sxs-lookup"><span data-stu-id="8b75e-133">Pushing toostaging takes between 10 too15 minutes.</span></span>  <span data-ttu-id="8b75e-134">Si l’opération prend plus de temps, actualisez d’abord votre navigateur (appuyez sur F5 dans Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="8b75e-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="8b75e-135">Bonjour rares cas où votre offre est toujours en exécutant un push toostaging après une heure, cliquez sur lien toolet nous savoir qu’il existe un problème de contact hello.</span><span class="sxs-lookup"><span data-stu-id="8b75e-135">In hello rare cases where your offer is still pushing toostaging after an hour, click hello contact us link toolet us know that there is an issue.</span></span>

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="8b75e-137">Hello Push tooStaging issue hello « en cours » icône cesse de déplacement et l’état de hello sera mise à jour trop « intermédiaire ».</span><span class="sxs-lookup"><span data-stu-id="8b75e-137">When hello Push tooStaging completes hello “In progress” icon will stop moving and hello status will be updated too“Staged”.</span></span>  <span data-ttu-id="8b75e-138">Vous est désormais prêt tootest votre offre.</span><span class="sxs-lookup"><span data-stu-id="8b75e-138">You are now ready tootest your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="8b75e-139">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="8b75e-139">Step 2.</span></span> <span data-ttu-id="8b75e-140">Tester votre offre intermédiaire dans DataMarket</span><span class="sxs-lookup"><span data-stu-id="8b75e-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="8b75e-141">Cliquez sur le lien hello suivant texte hello **« consultez votre service proposer à... »**</span><span class="sxs-lookup"><span data-stu-id="8b75e-141">Click hello link following hello text **“See Your service offer at…”**</span></span> <span data-ttu-id="8b75e-142">écran hello toodisplay hello abonné s’affiche lorsque votre offre est tooproduction et apparaîtra dans DataMarket.</span><span class="sxs-lookup"><span data-stu-id="8b75e-142">toodisplay hello screen that hello subscriber will see when your offer goes tooproduction and will appear in DataMarket.</span></span>

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="8b75e-144">Tester ou vérifiez chacun des éléments de 12 hello marqué ci-dessus tooensure tous les logos, prix/transactions, texte, images, documentation et les liens sont corrects et fonctionnent correctement.</span><span class="sxs-lookup"><span data-stu-id="8b75e-144">Test or verify each of hello 12 items marked above tooensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="8b75e-145">Il s’agit d’un tooensure temps toutes les valeurs de test que vous avez entré lors de la création de votre offre ont été remplacés par des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="8b75e-145">This is a good time tooensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="8b75e-146">Logo de l'offre</span><span class="sxs-lookup"><span data-stu-id="8b75e-146">Offer logo</span></span>
2. <span data-ttu-id="8b75e-147">Nom de l’offre</span><span class="sxs-lookup"><span data-stu-id="8b75e-147">Offer name</span></span>
3. <span data-ttu-id="8b75e-148">Site Web de la société de tooyour/lien du nom du serveur de publication</span><span class="sxs-lookup"><span data-stu-id="8b75e-148">Publisher name/link tooyour company's website</span></span>
4. <span data-ttu-id="8b75e-149">Parcourir les catégories de votre offre</span><span class="sxs-lookup"><span data-stu-id="8b75e-149">Search categories for your offer</span></span>
5. <span data-ttu-id="8b75e-150">Abonnés tooassist du lien de prise en charge de votre offre</span><span class="sxs-lookup"><span data-stu-id="8b75e-150">Your offer's support link tooassist subscribers</span></span>
6. <span data-ttu-id="8b75e-151">Description contextuelle de votre offre</span><span class="sxs-lookup"><span data-stu-id="8b75e-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="8b75e-152">Plan de l’offre précisant les détails de la facturation</span><span class="sxs-lookup"><span data-stu-id="8b75e-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="8b75e-153">Code de tooimplementation de lien</span><span class="sxs-lookup"><span data-stu-id="8b75e-153">Link tooimplementation code</span></span>
9. <span data-ttu-id="8b75e-154">Exemples d'images illustrant l’utilisation des données de l'offre</span><span class="sxs-lookup"><span data-stu-id="8b75e-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="8b75e-155">Métadonnées d’entrée/sortie pour chaque service au sein de l’offre de hello</span><span class="sxs-lookup"><span data-stu-id="8b75e-155">Input/Output metadata for each service within hello offer</span></span>
11. <span data-ttu-id="8b75e-156">Conditions d'utilisation de l’offre</span><span class="sxs-lookup"><span data-stu-id="8b75e-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="8b75e-157">Aperçu des données de l’offre de hello</span><span class="sxs-lookup"><span data-stu-id="8b75e-157">Preview of hello offer's data</span></span>

<span data-ttu-id="8b75e-158">Enfin, recherchez le service de hello fonctionnera via hello Datamarket en cliquant sur le lien hello « Explorer ce jeu de données ».</span><span class="sxs-lookup"><span data-stu-id="8b75e-158">Finally, check hello service will work through hello Datamarket by clicking hello link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="8b75e-159">Une nouvelle fenêtre s’ouvre dans l’outil de hello, nous appelons « Explorateur de Service » afin de vous pouvez afficher un aperçu des résultats hello d’une requête par rapport à votre service.</span><span class="sxs-lookup"><span data-stu-id="8b75e-159">A new window will open in hello tool we call “Service Explorer” so you can preview hello results of a query against your service.</span></span>  <span data-ttu-id="8b75e-160">Dans cette fenêtre, vous pouvez entrer hello paramètres nécessitent et afficher les résultats de hello affichés à partir d’une requête sur votre service.</span><span class="sxs-lookup"><span data-stu-id="8b75e-160">In this window, you can enter hello parameters needed and see hello results displayed from a query against your service.</span></span>   <span data-ttu-id="8b75e-161">En outre, sont affichées hello URL pour votre requête.</span><span class="sxs-lookup"><span data-stu-id="8b75e-161">Also, displayed is hello URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="8b75e-162">Être vraiment tooreview hello description textuelle du service hello affiché en haut de hello.</span><span class="sxs-lookup"><span data-stu-id="8b75e-162">Be sure tooreview hello textual description of hello service displayed at hello top.</span></span>  <span data-ttu-id="8b75e-163">Et si votre offre se compose de plusieurs services appelant et cliquez sur les onglets de hello en hello bas tooswitch toohello suivant service tooreview de test.</span><span class="sxs-lookup"><span data-stu-id="8b75e-163">And if your offer consists of more than one service call, click hello tabs at hello bottom tooswitch toohello next service tooreview and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="8b75e-164">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="8b75e-164">Next step</span></span>
<span data-ttu-id="8b75e-165">Si vous rencontrez des problèmes et avez besoin d'aide pour les résoudre, veuillez contacter l’ [assistance pour éditeurs Azure](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="8b75e-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="8b75e-166">Si vous êtes satisfait et prêt toopublish votre offre Lisez hello [tooProduction tooPush de demander une approbation](marketplace-publishing-push-to-production.md) documentation.</span><span class="sxs-lookup"><span data-stu-id="8b75e-166">If you are satisfied and ready toopublish your offer please read hello [Request Approval tooPush tooProduction](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="8b75e-167">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8b75e-167">See Also</span></span>
* [<span data-ttu-id="8b75e-168">Mise en route : Comment toopublish une toohello offre Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="8b75e-168">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

