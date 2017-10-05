---
title: "Tester votre offre de service de données pour Marketplace | Microsoft Docs"
description: "Découvrez comment tester votre offre de service de données pour Azure Marketplace."
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
ms.openlocfilehash: 56a8aad7484fed18b74200ffa7acf22363625a15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="61596-103">Tester votre offre de service de données dans l'emplacement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="61596-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="61596-104">**À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.**</span><span class="sxs-lookup"><span data-stu-id="61596-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="61596-105">Si vous avez une application SaaS professionnelle à publier sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="61596-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="61596-106">Si vous avez une application IaaS ou un service de développement à publier sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="61596-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="61596-107">Après avoir effectué les deux premières étapes ([Création de votre compte de développeur Microsoft](marketplace-publishing-accounts-creation-registration.md) et [Création de votre offre de service de données dans le portail de publication](marketplace-publishing-data-service-creation.md)), vous êtes prêt à proposer votre offre dans Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="61596-107">After completing the first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in the Azure Marketplace.</span></span> <span data-ttu-id="61596-108">Cette rubrique vous guidera dans la première étape appelée « préproduction »</span><span class="sxs-lookup"><span data-stu-id="61596-108">This topic will walk you through the first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="61596-109">Dans le cadre du déploiement dans un environnement intermédiaire, vous déployez votre offre dans un « bac à sable » (sandbox) privé dans lequel vous pouvez tester et vérifier ses fonctionnalités avant le lancement de sa production.</span><span class="sxs-lookup"><span data-stu-id="61596-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="61596-110">L'offre apparaît avec le statut Intermédiaire, comme pour un client qui l'aurait déployée.</span><span class="sxs-lookup"><span data-stu-id="61596-110">The offer will appear in staging just as it would to a customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-to-staging"></a><span data-ttu-id="61596-111">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="61596-111">Step 1.</span></span> <span data-ttu-id="61596-112">Déployer votre offre dans un environnement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="61596-112">Pushing your offer to staging</span></span>
<span data-ttu-id="61596-113">Le placement de votre offre dans l'environnement intermédiaire vous permet de tester cette offre avant de la proposer aux futurs abonnés.</span><span class="sxs-lookup"><span data-stu-id="61596-113">Pushing your offer to staging allows you to test the offer before it becomes available to future subscribers.</span></span>  <span data-ttu-id="61596-114">Vous pouvez ainsi voir comment votre offre apparaît et comment elle est utilisée par les abonnés à vos données.</span><span class="sxs-lookup"><span data-stu-id="61596-114">You can see how your offer will appear and function for those subscribing to your data.</span></span>  

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="61596-116">Connexion au [portail de publication](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="61596-116">Login into the [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="61596-117">Sélectionnez **DATA SERVICES** dans la fenêtre de navigation de gauche</span><span class="sxs-lookup"><span data-stu-id="61596-117">Select **Data Services** in the left navigation window</span></span>
3. <span data-ttu-id="61596-118">Sélectionnez l’offre que vous voulez placer dans l'environnement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="61596-118">Select your offer you want to push to staging.</span></span> <span data-ttu-id="61596-119">L'écran ci-dessus apparaît.</span><span class="sxs-lookup"><span data-stu-id="61596-119">You will see the above screen.</span></span>
4. <span data-ttu-id="61596-120">Cliquez sur le bouton **PUSH TO STAGING** .</span><span class="sxs-lookup"><span data-stu-id="61596-120">Click **Push To Staging** button.</span></span>  
5. <span data-ttu-id="61596-121">Si des problèmes liés à l'offre doivent être résolus avant que l’offre ne passe dans l'environnement intermédiaire, la liste de ces problèmes s’affichera.</span><span class="sxs-lookup"><span data-stu-id="61596-121">If there are issues with the offer that needed to be completed prior to pushing to staging, you will see a list displayed.</span></span>  <span data-ttu-id="61596-122">Corrigez-les en cliquant sur chaque élément de la liste.</span><span class="sxs-lookup"><span data-stu-id="61596-122">Correct these items by clicking on each item in the list.</span></span> <span data-ttu-id="61596-123">Une fois toutes les corrections effectuées, cliquez de nouveau sur le bouton **PUSH TO STAGING** .</span><span class="sxs-lookup"><span data-stu-id="61596-123">When all corrections made, click **Push to Staging** button again.</span></span>

<span data-ttu-id="61596-124">Si votre offre ne présente aucun problème, vous verrez la fenêtre contextuelle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="61596-124">If there are no issues with your offer you will see the popup window below.</span></span>  

<span data-ttu-id="61596-125">Si vous n’avez pas l’intention ou n’être pas habilité à publier votre offre dans le portail Azure (capacité limitée), fermez la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="61596-125">If you’re not planning/not approved to surface your offer in Azure Portal (currently has limited capacity), then just close the pop-up window.</span></span>

<span data-ttu-id="61596-126">Pour tester votre service de données dans le Portail Azure (en plus du portail DataMarket), vous devez utiliser un ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="61596-126">To test your Data Service in Azure Portal (in addition to the DataMarket portal), you will need an Azure Subscription ID to test with.</span></span>  <span data-ttu-id="61596-127">Cet ID d’abonnement identifiera le compte autorisé à tester votre offre.</span><span class="sxs-lookup"><span data-stu-id="61596-127">This Subscription ID will identify the account that will be allowed to test your offer.</span></span>  

<span data-ttu-id="61596-128">Coupez et collez votre ID d’abonnement, puis cliquez sur la coche pour continuer.</span><span class="sxs-lookup"><span data-stu-id="61596-128">Cut and paste your Subscription ID and click the checkmark to continue.</span></span>

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="61596-130">Ces ID d’abonnement Azure sont uniquement requis pour le test et la gestion intermédiaire dans le [Portail de gestion Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="61596-130">These Azure subscriptions IDs are only required for testing and staging in the [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="61596-131">Ils ne sont pas nécessaires pour le test dans Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="61596-131">They are not required to test in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="61596-132">L'écran suivant montre que la publication a lieu en affichant l'icône « En cours » en surbrillance jaune ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="61596-132">The next screen that appears shows that publishing is taking place by displaying the “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="61596-133">Le transfert de l’offre vers l’environnement intermédiaire prend entre 10 à 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="61596-133">Pushing to staging takes between 10 to 15 minutes.</span></span>  <span data-ttu-id="61596-134">Si l’opération prend plus de temps, actualisez d’abord votre navigateur (appuyez sur F5 dans Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="61596-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="61596-135">Dans les rares cas où votre offre est toujours en cours de transfert vers l'environnement intermédiaire après une heure, cliquez sur le lien de contact pour nous avertir du problème.</span><span class="sxs-lookup"><span data-stu-id="61596-135">In the rare cases where your offer is still pushing to staging after an hour, click the contact us link to let us know that there is an issue.</span></span>

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="61596-137">Une fois le passage vers l’environnement intermédiaire effectué, l'icône « En cours » s’immobilise et passe à l’état « Intermédiaire ».</span><span class="sxs-lookup"><span data-stu-id="61596-137">When the Push to Staging completes the “In progress” icon will stop moving and the status will be updated to “Staged”.</span></span>  <span data-ttu-id="61596-138">Vous êtes maintenant prêt à tester votre offre.</span><span class="sxs-lookup"><span data-stu-id="61596-138">You are now ready to test your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="61596-139">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="61596-139">Step 2.</span></span> <span data-ttu-id="61596-140">Tester votre offre intermédiaire dans DataMarket</span><span class="sxs-lookup"><span data-stu-id="61596-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="61596-141">Cliquez sur le lien après le texte **« See Your service offer at... »**</span><span class="sxs-lookup"><span data-stu-id="61596-141">Click the link following the text **“See Your service offer at…”**</span></span> <span data-ttu-id="61596-142">pour afficher l'écran que verra l'abonné lorsque votre offre est mise en production et visible dans DataMarket.</span><span class="sxs-lookup"><span data-stu-id="61596-142">to display the screen that the subscriber will see when your offer goes to production and will appear in DataMarket.</span></span>

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="61596-144">Testez ou vérifiez chacun des 12 éléments marqués ci-dessus pour vous assurer que tous les logos, prix/transactions, textes, images, documentation et liens sont corrects et fonctionnent.</span><span class="sxs-lookup"><span data-stu-id="61596-144">Test or verify each of the 12 items marked above to ensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="61596-145">Il s'agit d'un bon moment pour vérifier que toutes les valeurs de test que vous avez entrées lors de la création de votre offre ont bien été remplacées par les valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="61596-145">This is a good time to ensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="61596-146">Logo de l'offre</span><span class="sxs-lookup"><span data-stu-id="61596-146">Offer logo</span></span>
2. <span data-ttu-id="61596-147">Nom de l’offre</span><span class="sxs-lookup"><span data-stu-id="61596-147">Offer name</span></span>
3. <span data-ttu-id="61596-148">Nom de l’éditeur/lien vers le site web de votre entreprise</span><span class="sxs-lookup"><span data-stu-id="61596-148">Publisher name/link to your company's website</span></span>
4. <span data-ttu-id="61596-149">Parcourir les catégories de votre offre</span><span class="sxs-lookup"><span data-stu-id="61596-149">Search categories for your offer</span></span>
5. <span data-ttu-id="61596-150">Lien vers le support de votre offre pour aider les abonnés</span><span class="sxs-lookup"><span data-stu-id="61596-150">Your offer's support link to assist subscribers</span></span>
6. <span data-ttu-id="61596-151">Description contextuelle de votre offre</span><span class="sxs-lookup"><span data-stu-id="61596-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="61596-152">Plan de l’offre précisant les détails de la facturation</span><span class="sxs-lookup"><span data-stu-id="61596-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="61596-153">Lien vers le code d'implémentation</span><span class="sxs-lookup"><span data-stu-id="61596-153">Link to implementation code</span></span>
9. <span data-ttu-id="61596-154">Exemples d'images illustrant l’utilisation des données de l'offre</span><span class="sxs-lookup"><span data-stu-id="61596-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="61596-155">Métadonnées d'entrée/sortie pour chaque service au sein de l'offre</span><span class="sxs-lookup"><span data-stu-id="61596-155">Input/Output metadata for each service within the offer</span></span>
11. <span data-ttu-id="61596-156">Conditions d'utilisation de l’offre</span><span class="sxs-lookup"><span data-stu-id="61596-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="61596-157">Aperçu des données de l'offre</span><span class="sxs-lookup"><span data-stu-id="61596-157">Preview of the offer's data</span></span>

<span data-ttu-id="61596-158">Enfin, vérifiez que le service fonctionnera dans Datamarket en cliquant sur le lien « Explorer ce jeu de données ».</span><span class="sxs-lookup"><span data-stu-id="61596-158">Finally, check the service will work through the Datamarket by clicking the link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="61596-159">Une nouvelle fenêtre s'ouvrira dans l'outil que nous appelons « Explorateur de service », vous permettant de prévisualiser les résultats d'une requête sur votre service.</span><span class="sxs-lookup"><span data-stu-id="61596-159">A new window will open in the tool we call “Service Explorer” so you can preview the results of a query against your service.</span></span>  <span data-ttu-id="61596-160">Dans cette fenêtre, vous pouvez entrer les paramètres nécessaires et afficher les résultats d'une requête sur votre service.</span><span class="sxs-lookup"><span data-stu-id="61596-160">In this window, you can enter the parameters needed and see the results displayed from a query against your service.</span></span>   <span data-ttu-id="61596-161">Vous y verrez également l'URL de votre requête.</span><span class="sxs-lookup"><span data-stu-id="61596-161">Also, displayed is the URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="61596-162">Veillez à consulter la description textuelle du service affichée en haut.</span><span class="sxs-lookup"><span data-stu-id="61596-162">Be sure to review the textual description of the service displayed at the top.</span></span>  <span data-ttu-id="61596-163">Si votre offre se compose de plusieurs appels de services, cliquez sur les onglets en bas pour basculer vers le service suivant afin de le vérifier et de le tester.</span><span class="sxs-lookup"><span data-stu-id="61596-163">And if your offer consists of more than one service call, click the tabs at the bottom to switch to the next service to review and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="61596-164">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="61596-164">Next step</span></span>
<span data-ttu-id="61596-165">Si vous rencontrez des problèmes et avez besoin d'aide pour les résoudre, veuillez contacter l’ [assistance pour éditeurs Azure](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="61596-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="61596-166">Si vous êtes satisfait et prêt à publier votre offre, consultez la documentation [Request Approval to Push To Production](marketplace-publishing-push-to-production.md) (Demander une approbation pour lancer la production).</span><span class="sxs-lookup"><span data-stu-id="61596-166">If you are satisfied and ready to publish your offer please read the [Request Approval to Push To Production](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="61596-167">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="61596-167">See Also</span></span>
* [<span data-ttu-id="61596-168">Mise en route : publication d’une offre dans Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="61596-168">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

