---
title: "aaaGuide toocreating un Service de données pour hello Marketplace | Documents Microsoft"
description: "Comment toocreate, certifier et déployer un Service de données pour obtenir des instructions détaillées d’achat sur hello Azure Marketplace."
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
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a><span data-ttu-id="d2258-103">Guide de publication du Service de données pour hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="d2258-103">Data Service Publishing Guide for hello Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d2258-104">**À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.**</span><span class="sxs-lookup"><span data-stu-id="d2258-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="d2258-105">Si vous avez une application SaaS vous aimeriez toopublish sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="d2258-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="d2258-106">Si vous avez des applications IaaS ou développeur de service vous serait comme toopublish sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="d2258-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="d2258-107">Après avoir effectué l’étape hello 1, [la création du compte et l’inscription](marketplace-publishing-accounts-creation-registration.md), nous vous découvrirez hello [général non technique](marketplace-publishing-pre-requisites.md) et [spécifications techniques](marketplace-publishing-data-service-creation-prerequisites.md) d’un Service de données offrent sur Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d2258-107">After completing hello step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through hello [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="d2258-108">Maintenant nous vous guidera à travers les étapes de hello pour la création d’une offre de Service de données sur hello [portail de publication] [ link-pubportal] pour hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d2258-108">Now we will walk you through hello steps for creating a Data Service offer on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="1----login-toohello-publishing-portal"></a><span data-ttu-id="d2258-109">1.    Connexion toohello portail de publication.</span><span class="sxs-lookup"><span data-stu-id="d2258-109">1.    Login toohello Publishing Portal.</span></span>
<span data-ttu-id="d2258-110">Accédez trop[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="d2258-110">Go too[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="d2258-111">**Pour la première heure connexion tooPublishing Portal, utilisez hello même compte avec lequel vendeur de votre société de profil a été inscrite dans le centre de développement.**</span><span class="sxs-lookup"><span data-stu-id="d2258-111">**For first time login tooPublishing Portal, use hello same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="d2258-112">(Vous pouvez ultérieurement ajouter tous les employés de votre société comme un co-admin Bonjour portail de publication).</span><span class="sxs-lookup"><span data-stu-id="d2258-112">(Later you can add any employee of your company as a co-admin in hello Publishing Portal).</span></span>

<span data-ttu-id="d2258-113">Cliquez sur hello **publier des Services de données** en mosaïque si c’est la première connexion de hello dans le portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="d2258-113">Click on hello **Publish a Data Services** tile if this is hello first login into hello publishing portal.</span></span>

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a><span data-ttu-id="d2258-114">2.    Choisissez **Data Services** dans le menu de navigation hello hello côté gauche.</span><span class="sxs-lookup"><span data-stu-id="d2258-114">2.    Choose **Data Services** in hello navigation menu on hello left side.</span></span>
  ![dessin](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="d2258-116">3.    Créez un service de données.</span><span class="sxs-lookup"><span data-stu-id="d2258-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="d2258-117">Renseignez les titre hello pour votre nouvelle offre de Service de données et cliquez sur « + » sur hello droite.</span><span class="sxs-lookup"><span data-stu-id="d2258-117">Fill in hello title for your new Data Service Offer and click on “+” on hello right.</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a><span data-ttu-id="d2258-119">4.    Révision hello sous-menu sous hello créée récemment Service de données dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d2258-119">4.    Review hello sub-menu under hello newly created Data Service in hello navigation menu.</span></span>
<span data-ttu-id="d2258-120">Cliquez sur hello **procédure pas à pas** onglet et examinez toutes les étapes nécessaires requises toopublish correctement hello Service de données sur hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d2258-120">Click on hello **Walkthrough** tab and review all necessary steps needed toopublish properly hello Data Service on hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="d2258-121">Vous pouvez toujours cliquer sur les liens hello dans la page de « Procédure pas à pas » hello ou utiliser les onglets dans l’offre de Service de données hello sous-menu sur le côté gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="d2258-121">You always can click on hello links in hello “Walkthrough” page or use tabs on hello Data Service offer’s sub-menu on hello left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="d2258-122">5.    Créez un plan.</span><span class="sxs-lookup"><span data-stu-id="d2258-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="d2258-123">Offres, plans, transactions.</span><span class="sxs-lookup"><span data-stu-id="d2258-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="d2258-124">Chaque offre peut avoir plusieurs plans, mais doit en avoir au moins un (1).</span><span class="sxs-lookup"><span data-stu-id="d2258-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="d2258-125">Lorsque les utilisateurs finaux s’abonner tooyour offre qu’ils s’abonner pour l’une de Plan l’offre de hello.</span><span class="sxs-lookup"><span data-stu-id="d2258-125">When end-users subscribe tooyour offer they subscribe for one of hello offer’s Plan.</span></span> <span data-ttu-id="d2258-126">Chaque plan définit la façon dont les utilisateurs finaux seront être toouse en mesure de votre service.</span><span class="sxs-lookup"><span data-stu-id="d2258-126">Each plan defines how end-users will be able toouse your service.</span></span>

<span data-ttu-id="d2258-127">Actuellement Azure Marketplace prennent en charge le modèle d’un niveau de Transaction d’abonnement mensuel basé uniquement pour les Services de données, autrement dit, les utilisateurs finaux payer des frais mensuels selon le prix toohello de plan spécifique de hello ils abonnés tooand sera en mesure de tooconsume chaque nombre de mois de transaction définie par le plan de hello.</span><span class="sxs-lookup"><span data-stu-id="d2258-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according toohello price of hello specific plan they subscribed tooand will be able tooconsume each month number of transaction defined by hello plan.</span></span>

<span data-ttu-id="d2258-128">Chaque Transaction généralement définie comme le nombre d’enregistrements renvoyés par votre Service de données basé sur la requête hello envoyé toohello Service.</span><span class="sxs-lookup"><span data-stu-id="d2258-128">Each Transaction usually defined as number of records your Data Service will return based on hello query sent toohello Service.</span></span> <span data-ttu-id="d2258-129">valeur par défaut Hello est 100.</span><span class="sxs-lookup"><span data-stu-id="d2258-129">hello default is 100.</span></span> <span data-ttu-id="d2258-130">Nombre de transactions retournés tooeach requête sera nombre d’enregistrements divisé par 100 et arrondi au nombre entier le plus proche de toohello.</span><span class="sxs-lookup"><span data-stu-id="d2258-130">Number of transactions returned tooeach query will be number of records divided by 100 and rounded up toohello closest integer.</span></span>

<span data-ttu-id="d2258-131">C’est le Service Azure Marketplace couche responsabilité toomonitor (compteur) nombre de transactions consommée par chaque requête.</span><span class="sxs-lookup"><span data-stu-id="d2258-131">It’s Azure Marketplace Service layer responsibility toomonitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2258-132">Les utilisateurs finaux qui atteint la limite de transaction hello mois hello seront bloqués de continuer le service de hello toouse jusqu'à la fin de leur cycle d’abonnement mensuel.</span><span class="sxs-lookup"><span data-stu-id="d2258-132">End-Users which reached hello transaction limit during hello month will be blocked from continuing toouse hello service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="d2258-133">Hello plan ou un des plans de hello permettre (mais ne doit pas) inclut un nombre illimité de transactions.</span><span class="sxs-lookup"><span data-stu-id="d2258-133">hello plan or one of hello plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="d2258-134">Créez un plan.</span><span class="sxs-lookup"><span data-stu-id="d2258-134">Create a plan.</span></span>
1. <span data-ttu-id="d2258-135">Cliquez sur **« + »** toohello suivant « ajouter un nouveau plan ».</span><span class="sxs-lookup"><span data-stu-id="d2258-135">Click on **“+”** next toohello “Add a new plan”.</span></span>
2. <span data-ttu-id="d2258-136">Choisissez une des options de hello : **illimité** ou **limité** l’utilisation de ce plan.</span><span class="sxs-lookup"><span data-stu-id="d2258-136">Choose one of hello options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="d2258-137">Si nombre hello du plan de hello transaction fournis Limited autorisera tooconsume dans un mois.</span><span class="sxs-lookup"><span data-stu-id="d2258-137">If Limited then provide hello number of transaction hello plan will allow tooconsume in a month.</span></span>
   
    ![dessin](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="d2258-139">Portail de publication également suggère « Identificateur de Plan », qui sera utilisé toocommunicate toohello les utilisateurs finaux hello nom du plan hello dans l’interface utilisateur de hello et utilisée également par hello tooidentify de marché Service hello Plan.</span><span class="sxs-lookup"><span data-stu-id="d2258-139">Publishing Portal will also suggest “Plan Identifier”, which will be used toocommunicate toohello end-users hello name of hello plan in hello UI and also used by hello Market Place Service tooidentify hello Plan.</span></span> <span data-ttu-id="d2258-140">Vous pouvez modifier hello « Identificateur de Plan » si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d2258-140">You can change hello “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d2258-141">Hello « Identificateur de Plan » doit être unique dans l’étendue de hello de chaque offre.</span><span class="sxs-lookup"><span data-stu-id="d2258-141">hello “Plan Identifier” must be unique within hello scope of each offer.</span></span> <span data-ttu-id="d2258-142">Comme de nombreux autres identificateurs utilisés dans hello planifier de portail de publication identificateur sera verrouillé une fois hello premier tooproduction de publication et que vous ne sera pas en mesure de toochange cet identificateur.</span><span class="sxs-lookup"><span data-stu-id="d2258-142">As many other Identifiers used in hello Publishing Portal Plan identifier will be locked after hello first publishing tooproduction and you will not be able toochange this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="d2258-143">Cliquez sur tooaccept de votre choix.</span><span class="sxs-lookup"><span data-stu-id="d2258-143">Click tooaccept your choice.</span></span>
4. <span data-ttu-id="d2258-144">Vous êtes ensuite invité à répondre à quelques questions supplémentaires concernant votre plan nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="d2258-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![dessin](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="d2258-146">Question</span><span class="sxs-lookup"><span data-stu-id="d2258-146">Question</span></span> | <span data-ttu-id="d2258-147">Signification</span><span class="sxs-lookup"><span data-stu-id="d2258-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="d2258-148">**Ce plan est gratuit et disponible dans le monde entier**</span><span class="sxs-lookup"><span data-stu-id="d2258-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="d2258-149">Vous pouvez créer un plan entièrement gratuit.</span><span class="sxs-lookup"><span data-stu-id="d2258-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="d2258-150">Si son hello envisagez uniquement pour cette offre, cela signifie que vous publiez « Offre gratuite » Bonjour Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d2258-150">If it’s hello only plan for this offer – it means that you are publishing “Free Offer” in hello Marketplace.</span></span> <span data-ttu-id="d2258-151">S’il s’agit uniquement pour des (peu) Plan, hello vous donne une option toooffer les utilisateurs finaux toolearn plus d’informations sur votre service avec un petit nombre de transactions par mois.</span><span class="sxs-lookup"><span data-stu-id="d2258-151">If it’s only for one (of few) Plan, hello it gives you an option toooffer end-users toolearn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="d2258-152">Si les réponses hello sont « Oui », vous n’êtes invitée aucun autre question.</span><span class="sxs-lookup"><span data-stu-id="d2258-152">If hello answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="d2258-153">Les utilisateurs finaux peuvent toujours mettre à niveau toohello payé plans.</span><span class="sxs-lookup"><span data-stu-id="d2258-153">End users can always upgrade toohello paid plans.</span></span>
> 
> 

| <span data-ttu-id="d2258-154">Question</span><span class="sxs-lookup"><span data-stu-id="d2258-154">Question</span></span> | <span data-ttu-id="d2258-155">Signification</span><span class="sxs-lookup"><span data-stu-id="d2258-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="d2258-156">**Existe-t-il un essai gratuit ?**</span><span class="sxs-lookup"><span data-stu-id="d2258-156">**Is free trial available?**</span></span> |<span data-ttu-id="d2258-157">Vous pouvez choisir entre « Aucune évaluation » tout ou donner un toouse option votre Plan pour « Mois ».</span><span class="sxs-lookup"><span data-stu-id="d2258-157">You can choose between “No Trial” at all or give an option toouse your Plan for “One Month”.</span></span> <span data-ttu-id="d2258-158">Éditeurs, tels que toouse cette tooprovide les utilisateurs finaux hello possibilité toounderstand hello avantages liés aux options de hello offrent gratuitement pendant un mois.</span><span class="sxs-lookup"><span data-stu-id="d2258-158">Publishers like toouse this option tooprovide end-users hello possibility toounderstand hello benefits of hello offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d2258-159">Les utilisateurs finaux seront en mesure de toopurchase une évaluation gratuite si elles ont établi paiement carte de crédit, par exemple, accord entreprise.</span><span class="sxs-lookup"><span data-stu-id="d2258-159">End-users will only be able toopurchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="d2258-160">Après un mois de la version d’évaluation gratuite de hello, Azure Marketplace démarrera charge clients prix hello date hello d’abonnement de hello, sauf si le client de hello initiée par l’annulation d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="d2258-160">After one month of hello free trial, Azure Marketplace will start charging customers hello price as of hello date of hello subscription, unless hello customer initiated hello subscription cancellation.</span></span> <span data-ttu-id="d2258-161">Aucune notification spéciale ne sera fournie aux utilisateurs finaux toohello.</span><span class="sxs-lookup"><span data-stu-id="d2258-161">No special notification will be provided toohello end-users.</span></span>
> 
> 

| <span data-ttu-id="d2258-162">Question</span><span class="sxs-lookup"><span data-stu-id="d2258-162">Question</span></span> | <span data-ttu-id="d2258-163">Signification</span><span class="sxs-lookup"><span data-stu-id="d2258-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="d2258-164">**Ce plan requiert un toopurchase de code de promotion ?**</span><span class="sxs-lookup"><span data-stu-id="d2258-164">**This plan requires a promotion code toopurchase?**</span></span> |<span data-ttu-id="d2258-165">Serveurs de publication ont une tootheir d’accès toolimit option Plans de Service en fournissant un code spécial, appelé « A du Promocode » toospecific clients.</span><span class="sxs-lookup"><span data-stu-id="d2258-165">Publishers have an option toolimit access tootheir Service Plans by providing a special code, called “A Promocode” toospecific customers.</span></span> <span data-ttu-id="d2258-166">Uniquement les utilisateurs finaux qui disposera de cet Promocode seront en mesure de toosubscribe toohello Plan.</span><span class="sxs-lookup"><span data-stu-id="d2258-166">Only end-users which will have this Promocode will be able toosubscribe toohello Plan.</span></span> <span data-ttu-id="d2258-167">Si vous choisissez « Non », vous acceptez que tout le monde à partir de la région de hello où hello offrent est disponible (voir [Guide de contenu Marketing Marketplace](marketplace-publishing-push-to-staging.md) pour plus de détails) seront en mesure de toosubscribe toothis plan.</span><span class="sxs-lookup"><span data-stu-id="d2258-167">If you choose “No”, then you agree that everyone from hello region where hello offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able toosubscribe toothis plan.</span></span> <span data-ttu-id="d2258-168">Vous n’aurez à répondre à aucune autre question.</span><span class="sxs-lookup"><span data-stu-id="d2258-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="d2258-169">**Également masquer ce plan pour toute personne ne disposant pas d’un code promotionnel valide ?**</span><span class="sxs-lookup"><span data-stu-id="d2258-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="d2258-170">Si hello répondre toohello précédent à la question est « Oui » hello serveur de publication a un toocompletely option apparaissant dans hello l’interface utilisateur de hello Marketplace pour supprimer ce plan.</span><span class="sxs-lookup"><span data-stu-id="d2258-170">If hello answer toohello previous question is “Yes” hello Publisher has an option toocompletely remove this plan from appearing in hello UI of hello Marketplace.</span></span> <span data-ttu-id="d2258-171">Cela signifie que, les clients verront pas ce plan dans la page de détails de l’offre de hello.</span><span class="sxs-lookup"><span data-stu-id="d2258-171">It means, customers will not see this plan in hello Offer’s details page.</span></span> <span data-ttu-id="d2258-172">Les utilisateurs finaux afin de recevront un toopurchase du promocode, seront tooit toosubscribe en mesure d’à l’aide du promocode.</span><span class="sxs-lookup"><span data-stu-id="d2258-172">End-users which will receive a promocode toopurchase it, will be able toosubscribe tooit using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="d2258-173">6.    Créez votre contenu marketing pour Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d2258-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="d2258-174">Pour la façon dont les informations de tooprovide requises dans **Marketing, tarification, prise en charge et des catégories** onglets, visitez [Guide de contenu Marketing Marketplace](marketplace-publishing-push-to-staging.md) qui est commun tooall artefacts publiées Bonjour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d2258-174">For How tooprovide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common tooall artifacts published in hello Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="d2258-175">7.    Connectez votre tooyour offre de Service (en fonction de SQL Azure ou repose sur le Service Web).</span><span class="sxs-lookup"><span data-stu-id="d2258-175">7.    Connect your offer tooyour Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="d2258-176">Cliquez sur hello **Data Services** sous-menu.</span><span class="sxs-lookup"><span data-stu-id="d2258-176">Click on hello **Data Services** sub-menu.</span></span>

<span data-ttu-id="d2258-177">Sur la moitié supérieure de hello de page de hello vous serez invité à indiquer l’offre de hello tooprovide **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="d2258-177">On hello upper half of hello page you’ll be asked tooprovide hello offer’s **Namespace**.</span></span>  

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="d2258-179">Hello ci-dessous question définit comment hello Publisher va tooexpose nouvellement créé offre tooAzure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d2258-179">hello below question will define how hello Publisher is going tooexpose newly created offer tooAzure Marketplace.</span></span> <span data-ttu-id="d2258-180">(Pour plus d’informations, consultez hello [Guide requis technique des Services données](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="d2258-180">(For more details see hello [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="d2258-182">**Hello de publication de base de données basée service**</span><span class="sxs-lookup"><span data-stu-id="d2258-182">**Publishing hello Database based service**</span></span>

<span data-ttu-id="d2258-183">Cliquez sur **Base de données**.</span><span class="sxs-lookup"><span data-stu-id="d2258-183">Click on **Database**.</span></span> <span data-ttu-id="d2258-184">Hello suivant page s’affiche :</span><span class="sxs-lookup"><span data-stu-id="d2258-184">hello following page will appear:</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="d2258-186">toocreate un mappage de CSDL pour hello Dataset basé sur hello de base de données SQL Azure :</span><span class="sxs-lookup"><span data-stu-id="d2258-186">toocreate a CSDL mapping for hello Dataset based on hello SQL Azure DB:</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="d2258-188">Puis pour chaque table</span><span class="sxs-lookup"><span data-stu-id="d2258-188">And then for each table</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="d2258-191">Dans le cas d’un service web</span><span class="sxs-lookup"><span data-stu-id="d2258-191">If Web Service</span></span>

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="d2258-193">Lecture [mappage existant web tooOData service via CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) pour obtenir des instructions détaillées et des exemples de création d’un Service Web de CSDL.</span><span class="sxs-lookup"><span data-stu-id="d2258-193">Read [Mapping an existing web service tooOData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d2258-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d2258-194">Next Steps</span></span>
<span data-ttu-id="d2258-195">Maintenant que vous avez créé votre offre de Service de données, assurez-vous d’effectuer les instructions hello Bonjour [Guide de contenu Marketing Marketplace](marketplace-publishing-push-to-staging.md) avant de vous déplacez vers le bas trop[votre Service de données de test dans la mise en lots](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="d2258-195">Now that you've created your Data Service offer, please ensure that you complete hello instructions in hello [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward too[Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d2258-196">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d2258-196">See Also</span></span>
* [<span data-ttu-id="d2258-197">Mise en route : Comment toopublish une toohello offre Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="d2258-197">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="d2258-198">Si vous êtes intéressé par le fonctionnement hello le processus de mappage global OData et leur objectif, lisez cet article [mappage du Service de données OData](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview définitions, des structures et des instructions.</span><span class="sxs-lookup"><span data-stu-id="d2258-198">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="d2258-199">Si vous êtes intéressé par apprentissage et comprendre les nœuds spécifiques hello et leurs paramètres, lisez cet article [nœuds de mappage de données Service OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) pour les définitions et des explications, des exemples et contexte de cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="d2258-199">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="d2258-200">Si vous souhaitez parcourir les exemples, consultez cet article [exemples de mappage de données Service OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee exemple de code et comprendre la syntaxe du code et du contexte.</span><span class="sxs-lookup"><span data-stu-id="d2258-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
