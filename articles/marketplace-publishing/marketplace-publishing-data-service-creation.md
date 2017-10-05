---
title: "Guide de création d’un service de données pour le Marketplace | Microsoft Docs"
description: "Instructions détaillées pour créer, certifier et déployer un service de données que d’autres peuvent acheter sur Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: c0c9362f1c2e15c947aaaf7187f3383ad243140f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="data-service-publishing-guide-for-the-azure-marketplace"></a><span data-ttu-id="4302b-103">Guide de publication d’un service de données pour Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4302b-103">Data Service Publishing Guide for the Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4302b-104">**À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.**</span><span class="sxs-lookup"><span data-stu-id="4302b-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="4302b-105">Si vous avez une application SaaS professionnelle à publier sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="4302b-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="4302b-106">Si vous avez une application IaaS ou un service de développement à publier sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="4302b-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="4302b-107">Après avoir effectué l’étape 1, [Création de compte et enregistrement](marketplace-publishing-accounts-creation-registration.md), nous vous avons guidé dans les [exigences générales non techniques](marketplace-publishing-pre-requisites.md) et les [exigences techniques](marketplace-publishing-data-service-creation-prerequisites.md) d’une offre de service de données sur Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4302b-107">After completing the step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through the [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="4302b-108">À présent, nous allons vous guider dans la procédure de création d’une offre de service de données sur le [portail de publication][link-pubportal] pour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4302b-108">Now we will walk you through the steps for creating a Data Service offer on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="1----login-to-the-publishing-portal"></a><span data-ttu-id="4302b-109">1.    Connectez-vous au portail de publication.</span><span class="sxs-lookup"><span data-stu-id="4302b-109">1.    Login to the Publishing Portal.</span></span>
<span data-ttu-id="4302b-110">Accédez à [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="4302b-110">Go to [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="4302b-111">**Pour votre première connexion au portail de publication, utilisez le même compte que celui avec lequel le profil de vendeur de votre entreprise a été inscrit dans le Centre de développement.**</span><span class="sxs-lookup"><span data-stu-id="4302b-111">**For first time login to Publishing Portal, use the same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="4302b-112">(Plus tard, vous pourrez ajouter des employés de votre entreprise comme coadministrateurs dans le portail de publication.)</span><span class="sxs-lookup"><span data-stu-id="4302b-112">(Later you can add any employee of your company as a co-admin in the Publishing Portal).</span></span>

<span data-ttu-id="4302b-113">Cliquez sur la mosaïque **Publier un service de données** s’il s’agit de votre première connexion au portail de publication.</span><span class="sxs-lookup"><span data-stu-id="4302b-113">Click on the **Publish a Data Services** tile if this is the first login into the publishing portal.</span></span>

## <a name="2----choose-data-services-in-the-navigation-menu-on-the-left-side"></a><span data-ttu-id="4302b-114">2.    Choisissez **Services de données** dans le menu de navigation situé à gauche.</span><span class="sxs-lookup"><span data-stu-id="4302b-114">2.    Choose **Data Services** in the navigation menu on the left side.</span></span>
  ![dessin](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="4302b-116">3.    Créez un service de données.</span><span class="sxs-lookup"><span data-stu-id="4302b-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="4302b-117">Remplissez le titre de votre nouvelle offre de service de données, puis cliquez sur le signe « + » affiché à droite.</span><span class="sxs-lookup"><span data-stu-id="4302b-117">Fill in the title for your new Data Service Offer and click on “+” on the right.</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-the-sub-menu-under-the-newly-created-data-service-in-the-navigation-menu"></a><span data-ttu-id="4302b-119">4.    Consultez le sous-menu sous le service de données nouvellement créé dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="4302b-119">4.    Review the sub-menu under the newly created Data Service in the navigation menu.</span></span>
<span data-ttu-id="4302b-120">Cliquez sur l’onglet **Procédure pas à pas** et passez en revue toutes les étapes nécessaires pour publier correctement le service de données sur Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4302b-120">Click on the **Walkthrough** tab and review all necessary steps needed to publish properly the Data Service on the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="4302b-121">Vous pouvez toujours cliquer sur les liens affichés dans la page « Procédure pas à pas » ou utiliser les onglets du sous-menu de l’offre de service de données situé à gauche.</span><span class="sxs-lookup"><span data-stu-id="4302b-121">You always can click on the links in the “Walkthrough” page or use tabs on the Data Service offer’s sub-menu on the left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="4302b-122">5.    Créez un plan.</span><span class="sxs-lookup"><span data-stu-id="4302b-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="4302b-123">Offres, plans, transactions.</span><span class="sxs-lookup"><span data-stu-id="4302b-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="4302b-124">Chaque offre peut avoir plusieurs plans, mais doit en avoir au moins un (1).</span><span class="sxs-lookup"><span data-stu-id="4302b-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="4302b-125">Lorsque les utilisateurs finaux s’abonnent à votre offre, ils s’abonnent à l’un des plans de l’offre.</span><span class="sxs-lookup"><span data-stu-id="4302b-125">When end-users subscribe to your offer they subscribe for one of the offer’s Plan.</span></span> <span data-ttu-id="4302b-126">Chaque plan définit la façon dont les utilisateurs finaux pourront utiliser votre service.</span><span class="sxs-lookup"><span data-stu-id="4302b-126">Each plan defines how end-users will be able to use your service.</span></span>

<span data-ttu-id="4302b-127">Actuellement, Azure Marketplace prend uniquement en charge le modèle d’abonnement mensuel basé les transactions pour Data Services. Autrement dit, les utilisateurs finaux payeront des frais mensuels en fonction du prix du plan spécifique auquel ils sont abonnés et pourront consommer chaque mois le nombre de transactions défini par le plan.</span><span class="sxs-lookup"><span data-stu-id="4302b-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according to the price of the specific plan they subscribed to and will be able to consume each month number of transaction defined by the plan.</span></span>

<span data-ttu-id="4302b-128">Chaque transaction est généralement définie sous la forme d’un nombre d’enregistrements que votre service de données renverra en fonction de la requête envoyée au service.</span><span class="sxs-lookup"><span data-stu-id="4302b-128">Each Transaction usually defined as number of records your Data Service will return based on the query sent to the Service.</span></span> <span data-ttu-id="4302b-129">La valeur par défaut est 100.</span><span class="sxs-lookup"><span data-stu-id="4302b-129">The default is 100.</span></span> <span data-ttu-id="4302b-130">Le nombre de transactions renvoyées à chaque requête correspond au nombre d’enregistrements divisé par 100 et arrondi à l’entier le plus proche.</span><span class="sxs-lookup"><span data-stu-id="4302b-130">Number of transactions returned to each query will be number of records divided by 100 and rounded up to the closest integer.</span></span>

<span data-ttu-id="4302b-131">Il incombe à la couche de service d’Azure Marketplace pour surveiller (compter) le nombre de transactions utilisées par chaque requête.</span><span class="sxs-lookup"><span data-stu-id="4302b-131">It’s Azure Marketplace Service layer responsibility to monitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4302b-132">Les utilisateurs finaux ayant atteint la limite de transactions au cours du mois ne peuvent pas continuer à utiliser le service jusqu’à la fin de leur cycle d’abonnement mensuel.</span><span class="sxs-lookup"><span data-stu-id="4302b-132">End-Users which reached the transaction limit during the month will be blocked from continuing to use the service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="4302b-133">Le plan ou l’un des plans peut (mais ne doit pas nécessairement) inclure un nombre illimité de transactions.</span><span class="sxs-lookup"><span data-stu-id="4302b-133">The plan or one of the plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="4302b-134">Créez un plan.</span><span class="sxs-lookup"><span data-stu-id="4302b-134">Create a plan.</span></span>
1. <span data-ttu-id="4302b-135">Cliquez sur le signe **« + »** en regard de « Ajouter un nouveau plan ».</span><span class="sxs-lookup"><span data-stu-id="4302b-135">Click on **“+”** next to the “Add a new plan”.</span></span>
2. <span data-ttu-id="4302b-136">Choisissez l’une des options suivantes : utilisation **Illimitée** ou **Limitée** pour ce plan.</span><span class="sxs-lookup"><span data-stu-id="4302b-136">Choose one of the options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="4302b-137">Si vous choisissez Limitée, indiquez le nombre de transactions que le plan autorise à utiliser en un mois.</span><span class="sxs-lookup"><span data-stu-id="4302b-137">If Limited then provide the number of transaction the plan will allow to consume in a month.</span></span>
   
    ![dessin](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="4302b-139">Le portail de publication suggère également un « identificateur de plan ». Cet identificateur sera utilisé pour communiquer aux utilisateurs finaux le nom du plan dans l’interface utilisateur. Il sera également utilisé par le service Marketplace pour identifier le plan.</span><span class="sxs-lookup"><span data-stu-id="4302b-139">Publishing Portal will also suggest “Plan Identifier”, which will be used to communicate to the end-users the name of the plan in the UI and also used by the Market Place Service to identify the Plan.</span></span> <span data-ttu-id="4302b-140">Vous pouvez modifier l’« identificateur de plan », si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="4302b-140">You can change the “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4302b-141">L’« identificateur de plan » doit être unique dans l’étendue de chaque offre.</span><span class="sxs-lookup"><span data-stu-id="4302b-141">The “Plan Identifier” must be unique within the scope of each offer.</span></span> <span data-ttu-id="4302b-142">Comme de nombreux autres identificateurs utilisés dans l’identificateur de plan du portail de publication seront verrouillés après la première publication en production, vous ne pourrez pas modifier cet identificateur.</span><span class="sxs-lookup"><span data-stu-id="4302b-142">As many other Identifiers used in the Publishing Portal Plan identifier will be locked after the first publishing to production and you will not be able to change this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="4302b-143">Cliquez pour valider votre choix.</span><span class="sxs-lookup"><span data-stu-id="4302b-143">Click to accept your choice.</span></span>
4. <span data-ttu-id="4302b-144">Vous êtes ensuite invité à répondre à quelques questions supplémentaires concernant votre plan nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="4302b-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![dessin](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="4302b-146">Question</span><span class="sxs-lookup"><span data-stu-id="4302b-146">Question</span></span> | <span data-ttu-id="4302b-147">Signification</span><span class="sxs-lookup"><span data-stu-id="4302b-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="4302b-148">**Ce plan est gratuit et disponible dans le monde entier**</span><span class="sxs-lookup"><span data-stu-id="4302b-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="4302b-149">Vous pouvez créer un plan entièrement gratuit.</span><span class="sxs-lookup"><span data-stu-id="4302b-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="4302b-150">Si c’est le seul plan de cette offre, cela signifie que vous publiez une « Offre gratuite » dans Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4302b-150">If it’s the only plan for this offer – it means that you are publishing “Free Offer” in the Marketplace.</span></span> <span data-ttu-id="4302b-151">Si c’est applicable à un seul plan (parmi plusieurs), cela vous permet de proposer aux utilisateurs finaux d’en savoir plus sur votre service avec un nombre assez restreint de transactions par mois.</span><span class="sxs-lookup"><span data-stu-id="4302b-151">If it’s only for one (of few) Plan, the it gives you an option to offer end-users to learn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="4302b-152">Si la réponse est « Oui », vous n’aurez à répondre à aucune autre question.</span><span class="sxs-lookup"><span data-stu-id="4302b-152">If the answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="4302b-153">Les utilisateurs finaux peuvent toujours effectuer une mise à niveau vers les plans payants.</span><span class="sxs-lookup"><span data-stu-id="4302b-153">End users can always upgrade to the paid plans.</span></span>
> 
> 

| <span data-ttu-id="4302b-154">Question</span><span class="sxs-lookup"><span data-stu-id="4302b-154">Question</span></span> | <span data-ttu-id="4302b-155">Signification</span><span class="sxs-lookup"><span data-stu-id="4302b-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="4302b-156">**Existe-t-il un essai gratuit ?**</span><span class="sxs-lookup"><span data-stu-id="4302b-156">**Is free trial available?**</span></span> |<span data-ttu-id="4302b-157">Vous pouvez choisir entre absolument « Aucune version d’évaluation » ou proposer une option pour utiliser votre plan pendant « Un mois ».</span><span class="sxs-lookup"><span data-stu-id="4302b-157">You can choose between “No Trial” at all or give an option to use your Plan for “One Month”.</span></span> <span data-ttu-id="4302b-158">Les éditeurs aiment utiliser cette option pour permettre aux utilisateurs finaux de comprendre gratuitement les avantages de l’offre gratuite pendant un mois.</span><span class="sxs-lookup"><span data-stu-id="4302b-158">Publishers like to use this option to provide end-users the possibility to understand the benefits of the offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="4302b-159">Les utilisateurs finaux ne pourront acheter un essai gratuit que s’ils disposent d’un moyen de paiement reconnus, tel qu’une carte de crédit ou un contrat d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="4302b-159">End-users will only be able to purchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="4302b-160">Après un mois d’essai gratuit, Azure Marketplace commence à faire payer le prix aux clients à compter de la date de l’abonnement, sauf si le client a entamé l’annulation de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="4302b-160">After one month of the free trial, Azure Marketplace will start charging customers the price as of the date of the subscription, unless the customer initiated the subscription cancellation.</span></span> <span data-ttu-id="4302b-161">Aucune notification spéciale n’est fournie aux utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="4302b-161">No special notification will be provided to the end-users.</span></span>
> 
> 

| <span data-ttu-id="4302b-162">Question</span><span class="sxs-lookup"><span data-stu-id="4302b-162">Question</span></span> | <span data-ttu-id="4302b-163">Signification</span><span class="sxs-lookup"><span data-stu-id="4302b-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="4302b-164">**L’achat de ce plan nécessite un code de promotion**</span><span class="sxs-lookup"><span data-stu-id="4302b-164">**This plan requires a promotion code to purchase?**</span></span> |<span data-ttu-id="4302b-165">Les éditeurs ont la possibilité de limiter l’accès à leurs plans de service en fournissant un code spécial, appelé « Code promo » pour des clients spécifiques.</span><span class="sxs-lookup"><span data-stu-id="4302b-165">Publishers have an option to limit access to their Service Plans by providing a special code, called “A Promocode” to specific customers.</span></span> <span data-ttu-id="4302b-166">Seuls les utilisateurs finaux disposant de ce Code promo peuvent s’abonner au plan.</span><span class="sxs-lookup"><span data-stu-id="4302b-166">Only end-users which will have this Promocode will be able to subscribe to the Plan.</span></span> <span data-ttu-id="4302b-167">Si vous choisissez « Non », vous reconnaissez que toutes les personnes de la région où l’offre est disponible (pour plus de détails, consultez le [Guide du contenu marketing d’Azure Marketplace](marketplace-publishing-push-to-staging.md) ) pourront s’abonner à ce plan.</span><span class="sxs-lookup"><span data-stu-id="4302b-167">If you choose “No”, then you agree that everyone from the region where the offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able to subscribe to this plan.</span></span> <span data-ttu-id="4302b-168">Vous n’aurez à répondre à aucune autre question.</span><span class="sxs-lookup"><span data-stu-id="4302b-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="4302b-169">**Également masquer ce plan pour toute personne ne disposant pas d’un code promotionnel valide ?**</span><span class="sxs-lookup"><span data-stu-id="4302b-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="4302b-170">Si la réponse à la question précédente est « Oui », l’éditeur a la possibilité de supprimer complètement l’affichage de ce plan dans l’interface utilisateur de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4302b-170">If the answer to the previous question is “Yes” the Publisher has an option to completely remove this plan from appearing in the UI of the Marketplace.</span></span> <span data-ttu-id="4302b-171">Cela signifie que les clients ne verront pas ce plan dans la page des détails de l’offre.</span><span class="sxs-lookup"><span data-stu-id="4302b-171">It means, customers will not see this plan in the Offer’s details page.</span></span> <span data-ttu-id="4302b-172">Les utilisateurs finaux qui recevront un code promotionnel pour l’achat pourront l’utiliser pour s’y abonner.</span><span class="sxs-lookup"><span data-stu-id="4302b-172">End-users which will receive a promocode to purchase it, will be able to subscribe to it using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="4302b-173">6.    Créez votre contenu marketing pour Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4302b-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="4302b-174">Pour savoir comment fournir les informations nécessaires les onglets **Marketing, Tarification, Support et Catégories** , consultez le [Guide du contenu marketing d’Azure Marketplace](marketplace-publishing-push-to-staging.md) qui est commun à tous les artefacts publiées dans Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4302b-174">For How to provide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common to all artifacts published in the Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-to-your-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="4302b-175">7.    Connectez votre offre à votre service (basé sur SQL Azure ou sur un service web).</span><span class="sxs-lookup"><span data-stu-id="4302b-175">7.    Connect your offer to your Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="4302b-176">Cliquez sur le sous-menu **Data Services** .</span><span class="sxs-lookup"><span data-stu-id="4302b-176">Click on the **Data Services** sub-menu.</span></span>

<span data-ttu-id="4302b-177">Dans la partie supérieure de la page, vous devez fournir l’ **espace de noms**de l’offre.</span><span class="sxs-lookup"><span data-stu-id="4302b-177">On the upper half of the page you’ll be asked to provide the offer’s **Namespace**.</span></span>  

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="4302b-179">La question ci-dessous définit la façon dont l’éditeur va exposer l’offre nouvellement créée dans Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4302b-179">The below question will define how the Publisher is going to expose newly created offer to Azure Marketplace.</span></span> <span data-ttu-id="4302b-180">(Pour plus d’informations, consultez le [guide des conditions techniques préalables de Data Services](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="4302b-180">(For more details see the [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="4302b-182">**Publication du service basée sur une base de données**</span><span class="sxs-lookup"><span data-stu-id="4302b-182">**Publishing the Database based service**</span></span>

<span data-ttu-id="4302b-183">Cliquez sur **Base de données**.</span><span class="sxs-lookup"><span data-stu-id="4302b-183">Click on **Database**.</span></span> <span data-ttu-id="4302b-184">La page suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="4302b-184">The following page will appear:</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="4302b-186">Pour créer un mappage CSDL pour le jeu de données basé sur la base de données SQL Azure :</span><span class="sxs-lookup"><span data-stu-id="4302b-186">To create a CSDL mapping for the Dataset based on the SQL Azure DB:</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="4302b-188">Puis pour chaque table</span><span class="sxs-lookup"><span data-stu-id="4302b-188">And then for each table</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="4302b-191">Dans le cas d’un service web</span><span class="sxs-lookup"><span data-stu-id="4302b-191">If Web Service</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="4302b-193">Pour obtenir des instructions détaillées et des exemples sur la création d’un service web CSDL, lisez [Mappage d’un service web existant à OData via le langage CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) .</span><span class="sxs-lookup"><span data-stu-id="4302b-193">Read [Mapping an existing web service to OData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4302b-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4302b-194">Next Steps</span></span>
<span data-ttu-id="4302b-195">Maintenant que vous avez créé votre offre de service de données, assurez-vous de suivre les instructions du [Guide de contenu marketing Azure Marketplace](marketplace-publishing-push-to-staging.md) avant de passer au [test de votre service de données dans un environnement intermédiaire](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="4302b-195">Now that you've created your Data Service offer, please ensure that you complete the instructions in the [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward to [Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4302b-196">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4302b-196">See Also</span></span>
* [<span data-ttu-id="4302b-197">Mise en route : publication d’une offre dans Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4302b-197">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="4302b-198">Si vous souhaitez comprendre le processus de mappage OData global et son rôle, lisez l’article [Mappage du service de données OData](marketplace-publishing-data-service-creation-odata-mapping.md) pour passer en revue des définitions, des structures et des instructions.</span><span class="sxs-lookup"><span data-stu-id="4302b-198">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="4302b-199">Si vous souhaitez découvrir et comprendre les nœuds spécifiques et leurs paramètres, lisez l’article [Nœuds de mappage du service de données OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) pour obtenir des définitions et des explications, des exemples, ainsi qu’un contexte de cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="4302b-199">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="4302b-200">Si vous souhaitez passer en revue des exemples, lisez l’article [Exemples de mappage du service de données OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) pour consulter des exemples de code, ainsi que pour comprendre la syntaxe et le contexte du code.</span><span class="sxs-lookup"><span data-stu-id="4302b-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
