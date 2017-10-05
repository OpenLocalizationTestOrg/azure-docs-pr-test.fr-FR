---
title: "Acheter un nom de domaine personnalisé pour Azure Web Apps"
description: "Découvrez comment acheter un nom de domaine personnalisé avec une application web dans Azure App Service."
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
ms.openlocfilehash: 3cb22b935624041ab51e64028a1b668fd694f9b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="ea2c8-103">Acheter un nom de domaine personnalisé pour Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="ea2c8-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="ea2c8-104">Les domaines App Service (version préliminaire) sont des domaines de niveau supérieur gérés directement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="ea2c8-105">Ils facilitent la gestion des domaines personnalisés pour [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-105">They make it easy to manage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="ea2c8-106">Ce didacticiel explique comment acheter un domaine App Service et attribuer des noms de domaine (DNS) dans Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-106">This tutorial shows you how to buy an App Service domain and assign DNS names to Azure Web Apps.</span></span>

<span data-ttu-id="ea2c8-107">Cet article concerne Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="ea2c8-108">Pour la machine virtuelle Azure ou le stockage Azure, consultez [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/) (Attribuer un domaine App Service à une machine virtuelle Azure ou un stockage Azure).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-108">For Azure VM or Azure Storage, see [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="ea2c8-109">Pour Services cloud, consultez [Configuration d’un nom de domaine personnalisé pour un service cloud Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea2c8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ea2c8-110">Prerequisites</span></span>

<span data-ttu-id="ea2c8-111">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="ea2c8-111">To complete this tutorial:</span></span>

* <span data-ttu-id="ea2c8-112">[Créez une application App Service](/azure/app-service/), ou utilisez une application créée pour un autre didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-the-app"></a><span data-ttu-id="ea2c8-113">Préparer l’application</span><span class="sxs-lookup"><span data-stu-id="ea2c8-113">Prepare the app</span></span>

<span data-ttu-id="ea2c8-114">Pour utiliser des domaines personnalisés dans Azure Web Apps, le [plan App Service](https://azure.microsoft.com/pricing/details/app-service/) de votre application web doit correspondre à un niveau payant (**Partagé**, **De base**, **Standard** ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-114">To use custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="ea2c8-115">Au cours de cette étape, vous allez vous assurer que votre application web se trouve dans le niveau de tarification pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-115">In this step, you make sure that the web app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="ea2c8-116">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="ea2c8-116">Sign in to Azure</span></span>

<span data-ttu-id="ea2c8-117">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-117">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="ea2c8-118">Accéder à l’application dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ea2c8-118">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="ea2c8-119">Dans le menu de gauche, sélectionnez **App Services**, puis le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-119">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Navigation au sein du portail pour accéder à l’application Azure](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="ea2c8-121">La page de gestion de l’application App Service s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-121">You see the management page of the App Service app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="ea2c8-122">Vérification du niveau tarifaire</span><span class="sxs-lookup"><span data-stu-id="ea2c8-122">Check the pricing tier</span></span>

<span data-ttu-id="ea2c8-123">Dans la navigation gauche de la page de l’application, faites défiler jusqu’à la section **Paramètres** et sélectionnez **Monter en puissance (plan App Service)**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-123">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Monter en puissance](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="ea2c8-125">Le niveau actuel de l’application est encadré d’un rectangle bleu.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-125">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="ea2c8-126">Vérifiez que l’application ne se trouve pas dans le niveau **Gratuit**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-126">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="ea2c8-127">Les DNS personnalisés ne sont pas pris en charge dans le niveau **Gratuit**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-127">Custom DNS is not supported in the **Free** tier.</span></span> 

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="ea2c8-129">Si le plan App Service n’est pas **Gratuit**, fermez la page **Choisir votre niveau de tarification** et passez à [Acheter le domaine](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-129">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Buy the domain](#buy-the-domain).</span></span>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="ea2c8-130">Monter en puissance le plan App Service</span><span class="sxs-lookup"><span data-stu-id="ea2c8-130">Scale up the App Service plan</span></span>

<span data-ttu-id="ea2c8-131">Sélectionnez l’un des niveaux payants (**Partagé**, **De base**, **Standard** ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-131">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="ea2c8-132">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-132">Click **Select**.</span></span>

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="ea2c8-134">Lorsque la notification suivante s’affiche, cela signifie que l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-134">When you see the following notification, the scale operation is complete.</span></span>

![Confirmation d’opération de mise à l’échelle](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-the-domain"></a><span data-ttu-id="ea2c8-136">Acheter le domaine</span><span class="sxs-lookup"><span data-stu-id="ea2c8-136">Buy the domain</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="ea2c8-137">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="ea2c8-137">Sign in to Azure</span></span>
<span data-ttu-id="ea2c8-138">Ouvrez le [portail Azure](https://portal.azure.com/) et connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-138">Open the [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="ea2c8-139">Lancer Acheter des domaines</span><span class="sxs-lookup"><span data-stu-id="ea2c8-139">Launch Buy domains</span></span>
<span data-ttu-id="ea2c8-140">Dans l’onglet **Web Apps**, cliquez sur le nom de votre application web, puis sélectionnez **Paramètres** et **Domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-140">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="ea2c8-141">Sur la page **Domaines personnalisés**, cliquez sur **Acheter des domaines**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-141">In the **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-the-domain-purchase"></a><span data-ttu-id="ea2c8-142">Configurer l’achat de domaine</span><span class="sxs-lookup"><span data-stu-id="ea2c8-142">Configure the domain purchase</span></span>

<span data-ttu-id="ea2c8-143">Sur la page **Domaine App Service**, dans la zone **Recherche de domaine**, tapez le nom de domaine que vous souhaitez acheter et tapez `Enter`.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-143">In the **App Service Domain** page, in the **Search for domain** box, type the domain name you want to buy and type `Enter`.</span></span> <span data-ttu-id="ea2c8-144">Les domaines disponibles proposés s'affichent juste en dessous de la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-144">The suggested available domains are shown just below the text box.</span></span> <span data-ttu-id="ea2c8-145">Sélectionnez un ou plusieurs domaines que vous souhaitez acheter.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-145">Select one or more domains you want to buy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="ea2c8-146">Cliquez sur **Informations de contact** et remplissez le formulaire d’informations de contact du domaine.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-146">Click the **Contact Information** and fill out the domain's contact information form.</span></span> <span data-ttu-id="ea2c8-147">Lorsque vous avez terminé, cliquez sur **OK** pour revenir à la page Domaine App Service.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-147">When finished, click **OK** to return to the App Service Domain page.</span></span>
   
<span data-ttu-id="ea2c8-148">Il est très important de remplir tous les champs obligatoires aussi précisément que possible.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="ea2c8-149">L’inexactitude des informations de contact fournies peut empêcher l’achat des domaines.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-149">Incorrect data for contact information can result in failure to purchase domains.</span></span> 

<span data-ttu-id="ea2c8-150">Sélectionnez ensuite les options souhaitées pour votre domaine.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-150">Next, select the desired options for your domain.</span></span> <span data-ttu-id="ea2c8-151">Pour plus de précisions, consultez le tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="ea2c8-151">See the following table for explanations:</span></span>

| <span data-ttu-id="ea2c8-152">Paramètre</span><span class="sxs-lookup"><span data-stu-id="ea2c8-152">Setting</span></span> | <span data-ttu-id="ea2c8-153">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="ea2c8-153">Suggested Value</span></span> | <span data-ttu-id="ea2c8-154">Description</span><span class="sxs-lookup"><span data-stu-id="ea2c8-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="ea2c8-155">Renouvellement automatique</span><span class="sxs-lookup"><span data-stu-id="ea2c8-155">Auto renew</span></span> | <span data-ttu-id="ea2c8-156">**Activer**</span><span class="sxs-lookup"><span data-stu-id="ea2c8-156">**Enable**</span></span> | <span data-ttu-id="ea2c8-157">Renouvelle automatiquement votre domaine App Service chaque année.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="ea2c8-158">Au moment du renouvellement, vous serez facturé le même prix sur votre carte de crédit.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-158">Your credit card is charged the same purchase price at the time of renewal.</span></span> |
|<span data-ttu-id="ea2c8-159">Protection des données personnelles</span><span class="sxs-lookup"><span data-stu-id="ea2c8-159">Privacy protection</span></span> | <span data-ttu-id="ea2c8-160">Activer</span><span class="sxs-lookup"><span data-stu-id="ea2c8-160">Enable</span></span> | <span data-ttu-id="ea2c8-161">Optez pour la « Protection des données personnelles », incluse dans le prix d’achat _gratuitement_ (à l’exception des domaines de niveau supérieur dont le registre ne prend pas en charge la protection des données, comme _.co.in_, _.co.uk_, et ainsi de suite).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-161">Opt in to "Privacy protection", which is included in the purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="ea2c8-162">Attribuer des noms d’hôte par défaut</span><span class="sxs-lookup"><span data-stu-id="ea2c8-162">Assign default hostnames</span></span> | <span data-ttu-id="ea2c8-163">**www** et **@**</span><span class="sxs-lookup"><span data-stu-id="ea2c8-163">**www** and **@**</span></span> | <span data-ttu-id="ea2c8-164">Si vous le souhaitez, vous pouvez sélectionner les liaisons de nom d’hôte souhaitées.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-164">Select the desired hostname bindings, if desired.</span></span> <span data-ttu-id="ea2c8-165">Lorsque l’opération d’achat de domaine est terminée, votre application web est accessible aux noms d’hôtes choisis.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-165">When the domain purchase operation is complete, your web app can be accessed at the selected hostnames.</span></span> <span data-ttu-id="ea2c8-166">Si l’application web se trouve derrière [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), vous ne verrez pas l’option pour attribuer le domaine racine (@), parce que Traffic Manager ne prend pas en charge les enregistrements A.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-166">If the web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see the option to assign the root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="ea2c8-167">Vous pouvez apporter des modifications aux attributions de nom d’hôte après l’achat de domaine.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-167">You can make changes to the hostname assignments after the domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="ea2c8-168">Accepter les mentions et acheter</span><span class="sxs-lookup"><span data-stu-id="ea2c8-168">Accept terms and purchase</span></span>

<span data-ttu-id="ea2c8-169">Cliquez sur **Mentions légales** pour consulter les mentions et les frais, puis cliquez sur **Acheter**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-169">Click **Legal Terms** to review the terms and the charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="ea2c8-170">Les domaines App Service utilisent Azure DNS pour héberger les domaines.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-170">App Service Domains use Azure DNS to host the domains.</span></span> <span data-ttu-id="ea2c8-171">Outre les frais d’inscription de domaine, les frais d’utilisation d’Azure DNS s’appliquent aussi.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-171">In addition to the domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="ea2c8-172">Pour en savoir plus, consultez la page relative à la [tarification Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="ea2c8-173">Retournez sur la page **Domaine App Service**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-173">Back in the **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="ea2c8-174">Pendant que l’opération, vous voyez apparaître les notifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea2c8-174">While the operation is in progress, you see the following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="ea2c8-175">Test des noms d’hôte</span><span class="sxs-lookup"><span data-stu-id="ea2c8-175">Test the hostnames</span></span>

<span data-ttu-id="ea2c8-176">Si vous avez attribué des noms d’hôte par défaut à votre application web, vous voyez également une notification de réussite pour chaque nom d’hôte choisi.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-176">If you have assigned default hostnames to your web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="ea2c8-177">Vous voyez également les noms d’hôtes choisis sur la page **Domaines personnalisés**, dans la section **Noms d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-177">You also see the selected hostnames in the **Custom domains** page, in the **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="ea2c8-178">Pour tester des noms d’hôte, accédez à ceux qui sont répertoriés dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-178">To test the hostnames, navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="ea2c8-179">Dans l’exemple de la capture d’écran précédente, essayez d’accéder à _kontoso.net_ et _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-179">In the example in the preceding screenshot, try navigating to _kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-to-web-app"></a><span data-ttu-id="ea2c8-180">Attribuer des noms d’hôte à une application web</span><span class="sxs-lookup"><span data-stu-id="ea2c8-180">Assign hostnames to web app</span></span>

<span data-ttu-id="ea2c8-181">Si vous choisissez de ne pas attribuer un ou plusieurs noms d’hôte par défaut à votre application web lors de l’achat, ou si vous devez attribuer un nom d’hôte non répertorié, sachez que vous pouvez attribuer ce nom à tout moment.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-181">If you choose not to assign one or more default hostnames to your web app during the purchase process, or if you need to assign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="ea2c8-182">Vous pouvez également attribuer des noms d’hôte dans le domaine App Service à n’importe quelle application web.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-182">You can also assign hostnames in the App Service Domain to any other web app.</span></span> <span data-ttu-id="ea2c8-183">La procédure varie si le domaine App Service et l’application web appartiennent au même abonnement.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-183">The steps depend on whether the App Service Domain and the web app belong to the same subscription.</span></span>

- <span data-ttu-id="ea2c8-184">Autre abonnement : mapper des enregistrements DNS personnalisés depuis le domaine App Service vers l’application web comme un domaine acheté en externe.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-184">Different subscription: Map custom DNS records from the App Service Domain to the web app like an externally purchased domain.</span></span> <span data-ttu-id="ea2c8-185">Pour en savoir plus sur l’ajout de noms DNS personnalisés à un domaine App Service, consultez [Gérer les enregistrements DNS personnalisés](#custom).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-185">For information on adding custom DNS names to an App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="ea2c8-186">Pour mapper un domaine acheté en externe à une application web, consultez [Mapper un nom DNS personnalisé existant à des applications web Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-186">To map an external purchased domain to a web app, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="ea2c8-187">Abonnement similaire : procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-187">Same subscription: Use the following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="ea2c8-188">Lancer Ajouter un nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="ea2c8-188">Launch add hostname</span></span>
<span data-ttu-id="ea2c8-189">Sur la page **App Services**, sélectionnez le nom de l’application web à laquelle vous souhaitez attribuer des noms d’hôte, puis **Paramètres**, et **Domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-189">In the **App Services** page, select the name of your web app that you want to assign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="ea2c8-190">Vérifiez que votre domaine acheté est répertorié dans la section **Domaines App Service**, mais ne le sélectionnez pas.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-190">Make sure that your purchased domain is listed in the **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="ea2c8-191">Tous les domaines App Service du même abonnement sont affichés sur la page **Domaines personnalisés**de l’application web.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-191">All App Service Domains in the same subscription are shown in the web app's **Custom domains** page.</span></span> <span data-ttu-id="ea2c8-192">Si votre domaine est inclus dans l’abonnement de l’application web, mais qu’il ne s’affiche pas sur la page **Domaines personnalisés** de l’application web, ouvrez à nouveau la page **Domaines personnalisés** ou actualisez la page web.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-192">If your domain is in the web app's subscription, but you cannot see it in the web app's **Custom domains** page, try reopening the **Custom domains** page or refresh the webpage.</span></span> <span data-ttu-id="ea2c8-193">Vérifiez également la cloche de notification en haut du portail Azure pour savoir s’il y a des échecs lors de la création ou de la progression.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-193">Also, check the notification bell at the top of the Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="ea2c8-194">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="ea2c8-195">Configurer le nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="ea2c8-195">Configure hostname</span></span>
<span data-ttu-id="ea2c8-196">Dans la boîte de dialogue **Ajouter un nom d’hôte**, entrez le nom de domaine complet du domaine App Service ou de n’importe quel sous-domaine.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-196">In the **Add hostname** dialog, type the fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="ea2c8-197">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ea2c8-197">For example:</span></span>

- <span data-ttu-id="ea2c8-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="ea2c8-198">kontoso.net</span></span>
- <span data-ttu-id="ea2c8-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="ea2c8-199">www.kontoso.net</span></span>
- <span data-ttu-id="ea2c8-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="ea2c8-200">abc.kontoso.net</span></span>

<span data-ttu-id="ea2c8-201">Lorsque vous avez terminé, sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-201">When finished, select **Validate**.</span></span> <span data-ttu-id="ea2c8-202">Le type d’enregistrement de nom d’hôte est automatiquement sélectionné pour vous.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-202">The hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="ea2c8-203">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-203">Select **Add hostname**.</span></span>

<span data-ttu-id="ea2c8-204">Une fois l’opération terminée, vous voyez une notification de réussite concernant le nom d’hôte attribué.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-204">When the operation is complete, you see a success notification for the assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="ea2c8-205">Fermer Ajouter un nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="ea2c8-205">Close add hostname</span></span>
<span data-ttu-id="ea2c8-206">Sur la page **Ajouter un nom d’hôte**, vous pouvez attribuer n’importe quel nom d’hôte à votre application web, si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-206">In the **Add hostname** page, assign any other hostname to your web app, as desired.</span></span> <span data-ttu-id="ea2c8-207">Lorsque vous avez terminé, fermez la page **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-207">When finished, close the **Add hostname** page.</span></span>

<span data-ttu-id="ea2c8-208">Vous devez maintenant voir le ou les noms d’hôte nouvellement attribués sur la page **Domaines personnalisés** de l’application web.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-208">You should now see the newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="ea2c8-209">Test des noms d’hôte</span><span class="sxs-lookup"><span data-stu-id="ea2c8-209">Test the hostnames</span></span>

<span data-ttu-id="ea2c8-210">Accédez aux noms d’hôte répertoriés dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-210">Navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="ea2c8-211">Dans l’exemple sur la capture d’écran précédente, essayez d’accéder à _abc.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-211">In the example in the preceding screenshot, try navigating to _abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="ea2c8-212">Gérer des enregistrements DNS personnalisés</span><span class="sxs-lookup"><span data-stu-id="ea2c8-212">Manage custom DNS records</span></span>

<span data-ttu-id="ea2c8-213">Dans Azure, les enregistrements DNS d’un domaine App Service sont gérés à l’aide d’[Azure DNS](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="ea2c8-214">Vous pouvez ajouter, supprimer et mettre à jour les enregistrements DNS, comme pour un domaine acheté en externe.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="ea2c8-215">Ouvrir le domaine App Service</span><span class="sxs-lookup"><span data-stu-id="ea2c8-215">Open App Service Domain</span></span>

<span data-ttu-id="ea2c8-216">Dans le portail Azure, dans le menu de gauche, sélectionnez **More Services** (Plus de services)  > **Domaine App Service**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-216">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="ea2c8-217">Sélectionnez le domaine à gérer.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-217">Select the domain to manage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="ea2c8-218">Accéder à la zone DNS</span><span class="sxs-lookup"><span data-stu-id="ea2c8-218">Access DNS zone</span></span>

<span data-ttu-id="ea2c8-219">Dans le menu de gauche du domaine, sélectionnez **Zone DNS**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-219">In the domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="ea2c8-220">Cette action ouvre la page [Zone DNS](../dns/dns-zones-records.md) de votre domaine App Service dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-220">This action opens the [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="ea2c8-221">Pour savoir comment modifier des enregistrements DNS, consultez [Gérer des zones DNS dans le portail Azure](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ea2c8-221">For information on how to edit DNS records, see [How to manage DNS Zones in the Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="ea2c8-222">Annuler l’achat (supprimer le domaine)</span><span class="sxs-lookup"><span data-stu-id="ea2c8-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="ea2c8-223">Après avoir acheté le domaine App Service, vous disposez de cinq jours pour annuler votre achat et bénéficier d’un remboursement intégral.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-223">After you purchase the App Service Domain, you have five days to cancel your purchase for a full refund.</span></span> <span data-ttu-id="ea2c8-224">Au-delà de cinq jours, vous pouvez supprimer le domaine App Service, mais vous ne serez pas remboursé.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-224">After five days, you can delete the App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="ea2c8-225">Ouvrir le domaine App Service</span><span class="sxs-lookup"><span data-stu-id="ea2c8-225">Open App Service Domain</span></span>

<span data-ttu-id="ea2c8-226">Dans le portail Azure, dans le menu de gauche, sélectionnez **More Services** (Plus de services)  > **Domaine App Service**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-226">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="ea2c8-227">Sélectionnez le domaine que vous souhaitez annuler ou supprimer.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-227">Select the domain to you want to cancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="ea2c8-228">Supprimer des liaisons de noms d’hôte</span><span class="sxs-lookup"><span data-stu-id="ea2c8-228">Delete hostname bindings</span></span>

<span data-ttu-id="ea2c8-229">Dans le menu de gauche du domaine, sélectionnez **Liaisons de noms d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-229">In the domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="ea2c8-230">Les liaisons de nom d’hôte de tous les services Azure sont répertoriées ici.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-230">The hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="ea2c8-231">Vous ne pouvez pas supprimer le domaine App Service avant d’avoir supprimé toutes les liaisons de nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-231">You cannot delete the App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="ea2c8-232">Supprimez chaque liaison de nom d’hôte en sélectionnant **...** > **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="ea2c8-233">Après avoir supprimé toutes les liaisons, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-233">After all the bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="ea2c8-234">Annuler ou supprimer</span><span class="sxs-lookup"><span data-stu-id="ea2c8-234">Cancel or delete</span></span>

<span data-ttu-id="ea2c8-235">Dans le menu de gauche du domaine, sélectionnez **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-235">In the domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="ea2c8-236">Si la période d’annulation pour domaine acheté n’est pas écoulée, sélectionnez **Annuler l’achat**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-236">If the cancellation period on the purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="ea2c8-237">Dans le cas contraire, vous verrez le bouton **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="ea2c8-238">Pour supprimer le domaine sans remboursement, sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-238">To delete the domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="ea2c8-239">Sélectionnez **OK** pour confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-239">Select **OK** to confirm the operation.</span></span> <span data-ttu-id="ea2c8-240">Si vous ne souhaitez pas continuer, cliquez n’importe où en dehors de la boîte de dialogue de confirmation.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-240">If you don't want to proceed, click anywhere outside of the confirmation dialog.</span></span>

<span data-ttu-id="ea2c8-241">Une fois l’opération terminée, le domaine n’est plus lié à votre abonnement et est de nouveau disponible à l’achat.</span><span class="sxs-lookup"><span data-stu-id="ea2c8-241">After the operation is complete, the domain is released from your subscription and available for anyone to purchase again.</span></span> 
