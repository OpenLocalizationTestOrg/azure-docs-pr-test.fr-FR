---
title: "aaaBuy un nom de domaine personnalisé pour les applications Web Azure"
description: "Découvrez comment nommer des toobuy un domaine personnalisé avec une application web dans Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="21af4-103">Acheter un nom de domaine personnalisé pour Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="21af4-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="21af4-104">Les domaines App Service (version préliminaire) sont des domaines de niveau supérieur gérés directement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="21af4-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="21af4-105">Il est donc facile toomanage des domaines personnalisés [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="21af4-105">They make it easy toomanage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="21af4-106">Ce didacticiel vous montre comment toobuy un domaine de Service d’application et attribuez DNS noms tooAzure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="21af4-106">This tutorial shows you how toobuy an App Service domain and assign DNS names tooAzure Web Apps.</span></span>

<span data-ttu-id="21af4-107">Cet article concerne Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span><span class="sxs-lookup"><span data-stu-id="21af4-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="21af4-108">Pour la machine virtuelle Azure ou le stockage Azure, consultez [tooAzure de domaine du Service d’applications affecter machine virtuelle ou le stockage Azure](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span><span class="sxs-lookup"><span data-stu-id="21af4-108">For Azure VM or Azure Storage, see [Assign App Service domain tooAzure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="21af4-109">Pour Services cloud, consultez [Configuration d’un nom de domaine personnalisé pour un service cloud Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="21af4-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21af4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="21af4-110">Prerequisites</span></span>

<span data-ttu-id="21af4-111">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="21af4-111">toocomplete this tutorial:</span></span>

* <span data-ttu-id="21af4-112">[Créez une application App Service](/azure/app-service/), ou utilisez une application créée pour un autre didacticiel.</span><span class="sxs-lookup"><span data-stu-id="21af4-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-hello-app"></a><span data-ttu-id="21af4-113">Préparer l’application hello</span><span class="sxs-lookup"><span data-stu-id="21af4-113">Prepare hello app</span></span>

<span data-ttu-id="21af4-114">toouse des domaines personnalisés dans les d’applications Web Azure, votre application web [plan App Service](https://azure.microsoft.com/pricing/details/app-service/) doit être un niveau payant (**Shared**, **base**, **Standard**, ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="21af4-114">toouse custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="21af4-115">Dans cette étape, vous vérifiez que l’application web hello est Bonjour pris en charge niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="21af4-115">In this step, you make sure that hello web app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="21af4-116">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="21af4-116">Sign in tooAzure</span></span>

<span data-ttu-id="21af4-117">Ouvrez hello [portail Azure](https://portal.azure.com) et connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="21af4-117">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="21af4-118">Accédez application toohello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="21af4-118">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="21af4-119">Dans le menu de gauche hello, sélectionnez **des Services d’application**, puis sélectionnez le nom hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="21af4-119">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="21af4-121">Page de gestion hello Hello application de Service de l’application s’affiche.</span><span class="sxs-lookup"><span data-stu-id="21af4-121">You see hello management page of hello App Service app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="21af4-122">Vérifier le niveau tarifaire de hello</span><span class="sxs-lookup"><span data-stu-id="21af4-122">Check hello pricing tier</span></span>

<span data-ttu-id="21af4-123">Bonjour barre de navigation de page de l’application hello gauche, faites défiler toohello **paramètres** section et sélectionnez **montée en puissance (plan App Service)**.</span><span class="sxs-lookup"><span data-stu-id="21af4-123">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Monter en puissance](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="21af4-125">niveau actuel de l’application Hello est mis en surbrillance d’une bordure bleue.</span><span class="sxs-lookup"><span data-stu-id="21af4-125">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="21af4-126">Vérifiez que cette application hello n’est pas hello de toomake **libre** couche.</span><span class="sxs-lookup"><span data-stu-id="21af4-126">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="21af4-127">DNS personnalisé n’est pas pris en charge dans hello **libre** couche.</span><span class="sxs-lookup"><span data-stu-id="21af4-127">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="21af4-129">Si hello plan App Service n’est pas **libre**, fermez hello **choisir votre niveau tarifaire** page et ignorer trop[domaine de hello acheter](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="21af4-129">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Buy hello domain](#buy-the-domain).</span></span>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="21af4-130">Montée en puissance hello plan App Service</span><span class="sxs-lookup"><span data-stu-id="21af4-130">Scale up hello App Service plan</span></span>

<span data-ttu-id="21af4-131">Sélectionnez un des niveaux de hello occupé (**Shared**, **base**, **Standard**, ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="21af4-131">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="21af4-132">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="21af4-132">Click **Select**.</span></span>

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="21af4-134">Lorsque vous voyez hello suivant la notification, l’opération de mise à l’échelle de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="21af4-134">When you see hello following notification, hello scale operation is complete.</span></span>

![Confirmation d’opération de mise à l’échelle](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a><span data-ttu-id="21af4-136">Acheter hello domaine</span><span class="sxs-lookup"><span data-stu-id="21af4-136">Buy hello domain</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="21af4-137">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="21af4-137">Sign in tooAzure</span></span>
<span data-ttu-id="21af4-138">Ouvrez hello [portail Azure](https://portal.azure.com/) et connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="21af4-138">Open hello [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="21af4-139">Lancer Acheter des domaines</span><span class="sxs-lookup"><span data-stu-id="21af4-139">Launch Buy domains</span></span>
<span data-ttu-id="21af4-140">Bonjour **Web Apps** , cliquez sur le nom hello de votre application web, sélectionnez **paramètres**, puis sélectionnez **les domaines personnalisés**</span><span class="sxs-lookup"><span data-stu-id="21af4-140">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="21af4-141">Bonjour **les domaines personnalisés** , cliquez sur **acheter des domaines**.</span><span class="sxs-lookup"><span data-stu-id="21af4-141">In hello **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a><span data-ttu-id="21af4-142">Configurer le fournisseur de domaine hello</span><span class="sxs-lookup"><span data-stu-id="21af4-142">Configure hello domain purchase</span></span>

<span data-ttu-id="21af4-143">Bonjour **domaine d’application Service** page hello **recherche pour le domaine** boîte, de type hello nom du domaine toobuy et type `Enter`.</span><span class="sxs-lookup"><span data-stu-id="21af4-143">In hello **App Service Domain** page, in hello **Search for domain** box, type hello domain name you want toobuy and type `Enter`.</span></span> <span data-ttu-id="21af4-144">Hello suggérées domaines disponibles sont affichés juste en dessous de zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="21af4-144">hello suggested available domains are shown just below hello text box.</span></span> <span data-ttu-id="21af4-145">Sélectionnez un ou plusieurs domaines que vous souhaitez toobuy.</span><span class="sxs-lookup"><span data-stu-id="21af4-145">Select one or more domains you want toobuy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="21af4-146">Cliquez sur hello **coordonnées de contact** et remplissez le formulaire des informations de contact du domaine hello.</span><span class="sxs-lookup"><span data-stu-id="21af4-146">Click hello **Contact Information** and fill out hello domain's contact information form.</span></span> <span data-ttu-id="21af4-147">Lorsque vous avez terminé, cliquez sur **OK** page de domaine d’application Service tooreturn toohello.</span><span class="sxs-lookup"><span data-stu-id="21af4-147">When finished, click **OK** tooreturn toohello App Service Domain page.</span></span>
   
<span data-ttu-id="21af4-148">Il est très important de remplir tous les champs obligatoires aussi précisément que possible.</span><span class="sxs-lookup"><span data-stu-id="21af4-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="21af4-149">Domaines de toopurchase échec peuvent entraîner des données incorrectes pour les informations de contact.</span><span class="sxs-lookup"><span data-stu-id="21af4-149">Incorrect data for contact information can result in failure toopurchase domains.</span></span> 

<span data-ttu-id="21af4-150">Ensuite, sélectionnez les options de hello souhaité pour votre domaine.</span><span class="sxs-lookup"><span data-stu-id="21af4-150">Next, select hello desired options for your domain.</span></span> <span data-ttu-id="21af4-151">Consultez hello tableau pour obtenir des explications suivant :</span><span class="sxs-lookup"><span data-stu-id="21af4-151">See hello following table for explanations:</span></span>

| <span data-ttu-id="21af4-152">Paramètre</span><span class="sxs-lookup"><span data-stu-id="21af4-152">Setting</span></span> | <span data-ttu-id="21af4-153">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="21af4-153">Suggested Value</span></span> | <span data-ttu-id="21af4-154">Description</span><span class="sxs-lookup"><span data-stu-id="21af4-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="21af4-155">Renouvellement automatique</span><span class="sxs-lookup"><span data-stu-id="21af4-155">Auto renew</span></span> | <span data-ttu-id="21af4-156">**Activer**</span><span class="sxs-lookup"><span data-stu-id="21af4-156">**Enable**</span></span> | <span data-ttu-id="21af4-157">Renouvelle automatiquement votre domaine App Service chaque année.</span><span class="sxs-lookup"><span data-stu-id="21af4-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="21af4-158">Votre carte de crédit hello même prix d’achat au moment de hello de renouvellement.</span><span class="sxs-lookup"><span data-stu-id="21af4-158">Your credit card is charged hello same purchase price at hello time of renewal.</span></span> |
|<span data-ttu-id="21af4-159">Protection des données personnelles</span><span class="sxs-lookup"><span data-stu-id="21af4-159">Privacy protection</span></span> | <span data-ttu-id="21af4-160">Activer</span><span class="sxs-lookup"><span data-stu-id="21af4-160">Enable</span></span> | <span data-ttu-id="21af4-161">S’abonner trop « Confidentialité », qui est incluse dans le prix d’achat hello _gratuitement_ (à l’exception des domaines de premier niveau dont le Registre ne prennent pas en charge la protection des données, telles que _. co.in_, _. Co.uk_, et ainsi de suite).</span><span class="sxs-lookup"><span data-stu-id="21af4-161">Opt in too"Privacy protection", which is included in hello purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="21af4-162">Attribuer des noms d’hôte par défaut</span><span class="sxs-lookup"><span data-stu-id="21af4-162">Assign default hostnames</span></span> | <span data-ttu-id="21af4-163">**www** et **@**</span><span class="sxs-lookup"><span data-stu-id="21af4-163">**www** and **@**</span></span> | <span data-ttu-id="21af4-164">Sélectionnez hello souhaitée des liaisons de nom d’hôte, si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="21af4-164">Select hello desired hostname bindings, if desired.</span></span> <span data-ttu-id="21af4-165">Lorsqu’une opération d’achat domaine hello est terminée, votre application web est accessible à des noms d’hôtes hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="21af4-165">When hello domain purchase operation is complete, your web app can be accessed at hello selected hostnames.</span></span> <span data-ttu-id="21af4-166">Si l’application hello web se trouve derrière [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), vous ne voyez pas le domaine racine hello hello option tooassign (@), parce que Traffic Manager ne pas les enregistrements de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="21af4-166">If hello web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see hello option tooassign hello root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="21af4-167">Vous pouvez modifier les attributions de nom d’hôte toohello issue de l’achat de domaine hello.</span><span class="sxs-lookup"><span data-stu-id="21af4-167">You can make changes toohello hostname assignments after hello domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="21af4-168">Accepter les mentions et acheter</span><span class="sxs-lookup"><span data-stu-id="21af4-168">Accept terms and purchase</span></span>

<span data-ttu-id="21af4-169">Cliquez sur **juridiques** tooreview hello générales de frais de hello, puis cliquez sur **acheter**.</span><span class="sxs-lookup"><span data-stu-id="21af4-169">Click **Legal Terms** tooreview hello terms and hello charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="21af4-170">Domaines de Service d’application d’utilisent des domaines de hello toohost Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="21af4-170">App Service Domains use Azure DNS toohost hello domains.</span></span> <span data-ttu-id="21af4-171">En outre frais d’inscription de domaine toohello, frais d’utilisation pour Azure DNS s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="21af4-171">In addition toohello domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="21af4-172">Pour en savoir plus, consultez la page relative à la [tarification Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="21af4-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="21af4-173">Dans hello **domaine d’application Service** , cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="21af4-173">Back in hello **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="21af4-174">Lors de l’opération de hello est en cours d’exécution, vous voyez hello suivant des notifications :</span><span class="sxs-lookup"><span data-stu-id="21af4-174">While hello operation is in progress, you see hello following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="21af4-175">Noms d’hôte de test hello</span><span class="sxs-lookup"><span data-stu-id="21af4-175">Test hello hostnames</span></span>

<span data-ttu-id="21af4-176">Si vous avez attribué par défaut les noms d’hôte tooyour web app, vous voyez également une notification de réussite pour chaque nom d’hôte sélectionné.</span><span class="sxs-lookup"><span data-stu-id="21af4-176">If you have assigned default hostnames tooyour web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="21af4-177">Vous voyez également les noms d’hôte hello sélectionné Bonjour **les domaines personnalisés** page hello **noms d’hôtes** section.</span><span class="sxs-lookup"><span data-stu-id="21af4-177">You also see hello selected hostnames in hello **Custom domains** page, in hello **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="21af4-178">noms d’hôtes de tootest hello, accédez toohello répertorié les noms d’hôtes dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="21af4-178">tootest hello hostnames, navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="21af4-179">Dans l’exemple hello Bonjour précédant la capture d’écran, essayez too_kontoso.net_ et _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="21af4-179">In hello example in hello preceding screenshot, try navigating too_kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-tooweb-app"></a><span data-ttu-id="21af4-180">Affecter des noms d’hôtes tooweb application</span><span class="sxs-lookup"><span data-stu-id="21af4-180">Assign hostnames tooweb app</span></span>

<span data-ttu-id="21af4-181">Si vous ne choisissez pas les tooassign une ou plus par défaut les noms d’hôte tooyour web app pendant hello processus d’achat, ou si vous avez besoin tooassign un nom d’hôte non répertorié, vous pouvez affecter un nom d’hôte à tout moment.</span><span class="sxs-lookup"><span data-stu-id="21af4-181">If you choose not tooassign one or more default hostnames tooyour web app during hello purchase process, or if you need tooassign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="21af4-182">Vous pouvez également affecter des noms d’hôte dans tooany de domaine de Service d’application hello autre application web.</span><span class="sxs-lookup"><span data-stu-id="21af4-182">You can also assign hostnames in hello App Service Domain tooany other web app.</span></span> <span data-ttu-id="21af4-183">Hello étapes dépendent si hello domaine du Service d’application et l’application web hello appartiennent toohello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="21af4-183">hello steps depend on whether hello App Service Domain and hello web app belong toohello same subscription.</span></span>

- <span data-ttu-id="21af4-184">Autre abonnement : mapper les enregistrements DNS personnalisés à partir de domaine de Service d’application hello toohello l’application web à un domaine extérieur achetée.</span><span class="sxs-lookup"><span data-stu-id="21af4-184">Different subscription: Map custom DNS records from hello App Service Domain toohello web app like an externally purchased domain.</span></span> <span data-ttu-id="21af4-185">Pour plus d’informations sur l’ajout de DNS personnalisé des noms tooan domaine du Service d’application, consultez [gérer les enregistrements DNS personnalisés](#custom).</span><span class="sxs-lookup"><span data-stu-id="21af4-185">For information on adding custom DNS names tooan App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="21af4-186">toomap une application web de tooa domaine achetées externe, consultez [mapper un tooAzure de nom DNS personnalisé existant Web Apps](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="21af4-186">toomap an external purchased domain tooa web app, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="21af4-187">Même abonnement : hello utilisation comme suit.</span><span class="sxs-lookup"><span data-stu-id="21af4-187">Same subscription: Use hello following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="21af4-188">Lancer Ajouter un nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="21af4-188">Launch add hostname</span></span>
<span data-ttu-id="21af4-189">Bonjour **des Services d’application** page, le nom hello select de votre application web que vous souhaitez que les noms d’hôte tooassign pour sélectionner **paramètres**, puis sélectionnez **les domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="21af4-189">In hello **App Services** page, select hello name of your web app that you want tooassign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="21af4-190">Assurez-vous que votre domaine achetée est répertorié dans hello **domaines de Service d’application** section, mais ne l’activez pas.</span><span class="sxs-lookup"><span data-stu-id="21af4-190">Make sure that your purchased domain is listed in hello **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="21af4-191">Tous les domaines de Service d’application Bonjour même abonnement sont affichés dans l’application hello web **les domaines personnalisés** page.</span><span class="sxs-lookup"><span data-stu-id="21af4-191">All App Service Domains in hello same subscription are shown in hello web app's **Custom domains** page.</span></span> <span data-ttu-id="21af4-192">Si votre domaine est inclus dans l’abonnement de l’application hello web, mais il ne figure pas dans l’application hello web **les domaines personnalisés** page, essayez de rouvrir hello **les domaines personnalisés** page ou d’actualiser la page Web de hello.</span><span class="sxs-lookup"><span data-stu-id="21af4-192">If your domain is in hello web app's subscription, but you cannot see it in hello web app's **Custom domains** page, try reopening hello **Custom domains** page or refresh hello webpage.</span></span> <span data-ttu-id="21af4-193">Vérifiez également représentant une cloche de notification hello haut hello hello portail Azure pour les échecs de la création ou de progression.</span><span class="sxs-lookup"><span data-stu-id="21af4-193">Also, check hello notification bell at hello top of hello Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="21af4-194">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="21af4-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="21af4-195">Configurer le nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="21af4-195">Configure hostname</span></span>
<span data-ttu-id="21af4-196">Bonjour **ajouter le nom d’hôte** boîte de dialogue, le nom de domaine complet de type hello de votre domaine de Service d’application ou un sous-domaine.</span><span class="sxs-lookup"><span data-stu-id="21af4-196">In hello **Add hostname** dialog, type hello fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="21af4-197">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="21af4-197">For example:</span></span>

- <span data-ttu-id="21af4-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="21af4-198">kontoso.net</span></span>
- <span data-ttu-id="21af4-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="21af4-199">www.kontoso.net</span></span>
- <span data-ttu-id="21af4-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="21af4-200">abc.kontoso.net</span></span>

<span data-ttu-id="21af4-201">Lorsque vous avez terminé, sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="21af4-201">When finished, select **Validate**.</span></span> <span data-ttu-id="21af4-202">type d’enregistrement de nom d’hôte Hello est automatiquement sélectionné pour vous.</span><span class="sxs-lookup"><span data-stu-id="21af4-202">hello hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="21af4-203">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="21af4-203">Select **Add hostname**.</span></span>

<span data-ttu-id="21af4-204">Lors de l’opération de hello est terminée, vous voyez une notification de réussite pour hello affecté le nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="21af4-204">When hello operation is complete, you see a success notification for hello assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="21af4-205">Fermer Ajouter un nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="21af4-205">Close add hostname</span></span>
<span data-ttu-id="21af4-206">Bonjour **ajouter le nom d’hôte** page, attribuer un autre nom d’hôte tooyour web application, comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="21af4-206">In hello **Add hostname** page, assign any other hostname tooyour web app, as desired.</span></span> <span data-ttu-id="21af4-207">Une fois terminé, fermez hello **ajouter le nom d’hôte** page.</span><span class="sxs-lookup"><span data-stu-id="21af4-207">When finished, close hello **Add hostname** page.</span></span>

<span data-ttu-id="21af4-208">Vous devez maintenant voir hello viennent d’être attribué hostname(s) dans votre application **les domaines personnalisés** page.</span><span class="sxs-lookup"><span data-stu-id="21af4-208">You should now see hello newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="21af4-209">Noms d’hôte de test hello</span><span class="sxs-lookup"><span data-stu-id="21af4-209">Test hello hostnames</span></span>

<span data-ttu-id="21af4-210">Accédez de noms d’hôtes toohello répertorié dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="21af4-210">Navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="21af4-211">Dans l’exemple hello Bonjour précédant la capture d’écran, essayez too_abc.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="21af4-211">In hello example in hello preceding screenshot, try navigating too_abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="21af4-212">Gérer des enregistrements DNS personnalisés</span><span class="sxs-lookup"><span data-stu-id="21af4-212">Manage custom DNS records</span></span>

<span data-ttu-id="21af4-213">Dans Azure, les enregistrements DNS d’un domaine App Service sont gérés à l’aide d’[Azure DNS](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="21af4-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="21af4-214">Vous pouvez ajouter, supprimer et mettre à jour les enregistrements DNS, comme pour un domaine acheté en externe.</span><span class="sxs-lookup"><span data-stu-id="21af4-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="21af4-215">Ouvrir le domaine App Service</span><span class="sxs-lookup"><span data-stu-id="21af4-215">Open App Service Domain</span></span>

<span data-ttu-id="21af4-216">Bonjour portail Azure, à partir du menu de gauche hello, sélectionnez **plus Services** > **domaines de Service d’application**.</span><span class="sxs-lookup"><span data-stu-id="21af4-216">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="21af4-217">Sélectionnez hello domaine toomanage.</span><span class="sxs-lookup"><span data-stu-id="21af4-217">Select hello domain toomanage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="21af4-218">Accéder à la zone DNS</span><span class="sxs-lookup"><span data-stu-id="21af4-218">Access DNS zone</span></span>

<span data-ttu-id="21af4-219">Dans le menu de gauche du domaine hello, sélectionnez **zone DNS**.</span><span class="sxs-lookup"><span data-stu-id="21af4-219">In hello domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="21af4-220">Cette action ouvre hello [zone DNS](../dns/dns-zones-records.md) page de votre domaine de Service d’application dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="21af4-220">This action opens hello [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="21af4-221">Pour plus d’informations sur la façon de tooedit les enregistrements DNS, consultez [comment toomanage les Zones DNS dans hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="21af4-221">For information on how tooedit DNS records, see [How toomanage DNS Zones in hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="21af4-222">Annuler l’achat (supprimer le domaine)</span><span class="sxs-lookup"><span data-stu-id="21af4-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="21af4-223">Après avoir acheté hello domaine du Service d’application, vous avez cinq jours toocancel votre achat d’un remboursement intégral.</span><span class="sxs-lookup"><span data-stu-id="21af4-223">After you purchase hello App Service Domain, you have five days toocancel your purchase for a full refund.</span></span> <span data-ttu-id="21af4-224">Après cinq jours, vous pouvez supprimer hello domaine du Service d’application, mais ne peut pas remboursé.</span><span class="sxs-lookup"><span data-stu-id="21af4-224">After five days, you can delete hello App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="21af4-225">Ouvrir le domaine App Service</span><span class="sxs-lookup"><span data-stu-id="21af4-225">Open App Service Domain</span></span>

<span data-ttu-id="21af4-226">Bonjour portail Azure, à partir du menu de gauche hello, sélectionnez **plus Services** > **domaines de Service d’application**.</span><span class="sxs-lookup"><span data-stu-id="21af4-226">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="21af4-227">Sélectionnez hello domaine tooyou que vous souhaitez toocancel ou supprimer.</span><span class="sxs-lookup"><span data-stu-id="21af4-227">Select hello domain tooyou want toocancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="21af4-228">Supprimer des liaisons de noms d’hôte</span><span class="sxs-lookup"><span data-stu-id="21af4-228">Delete hostname bindings</span></span>

<span data-ttu-id="21af4-229">Dans le menu de gauche du domaine hello, sélectionnez **liaisons de nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="21af4-229">In hello domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="21af4-230">liaisons de nom d’hôte Hello de tous les services Azure sont répertoriées ici.</span><span class="sxs-lookup"><span data-stu-id="21af4-230">hello hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="21af4-231">Impossible de supprimer hello App Service de domaine jusqu'à ce que toutes les liaisons de nom d’hôte sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="21af4-231">You cannot delete hello App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="21af4-232">Supprimez chaque liaison de nom d’hôte en sélectionnant **...** > **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="21af4-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="21af4-233">Une fois que toutes les liaisons de hello sont supprimés, sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="21af4-233">After all hello bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="21af4-234">Annuler ou supprimer</span><span class="sxs-lookup"><span data-stu-id="21af4-234">Cancel or delete</span></span>

<span data-ttu-id="21af4-235">Dans le menu de gauche du domaine hello, sélectionnez **vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="21af4-235">In hello domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="21af4-236">Si la période d’annulation hello sur le domaine de hello acheté n’est pas écoulé, sélectionnez **Annuler achat**.</span><span class="sxs-lookup"><span data-stu-id="21af4-236">If hello cancellation period on hello purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="21af4-237">Dans le cas contraire, vous verrez le bouton **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="21af4-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="21af4-238">domaine de hello toodelete sans restitution, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="21af4-238">toodelete hello domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="21af4-239">Sélectionnez **OK** opération hello de tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="21af4-239">Select **OK** tooconfirm hello operation.</span></span> <span data-ttu-id="21af4-240">Si vous ne souhaitez pas tooproceed, cliquez n’importe où en dehors de la boîte de dialogue de confirmation hello.</span><span class="sxs-lookup"><span data-stu-id="21af4-240">If you don't want tooproceed, click anywhere outside of hello confirmation dialog.</span></span>

<span data-ttu-id="21af4-241">Une fois hello terminée, domaine de hello est lancé à partir de votre abonnement et disponibles pour toute personne toopurchase à nouveau.</span><span class="sxs-lookup"><span data-stu-id="21af4-241">After hello operation is complete, hello domain is released from your subscription and available for anyone toopurchase again.</span></span> 
