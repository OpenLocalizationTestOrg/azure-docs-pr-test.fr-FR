---
title: "Ajouter un réseau de distribution de contenu (CDN) à un service Azure App Service | Microsoft Docs"
description: "Ajoutez un réseau de distribution de contenu (CDN) à un Azure App Service pour mettre en cache et distribuer vos fichiers statiques à partir de serveurs proches de vos clients dans le monde entier."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 257b75d01f3904661c1a188a2d53ffcb74f48f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-content-delivery-network-cdn-to-an-azure-app-service"></a><span data-ttu-id="6b550-103">Ajouter un réseau de distribution de contenu (CDN) à un Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6b550-103">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>

<span data-ttu-id="6b550-104">Le [réseau de distribution de contenu (CDN) Azure](../cdn/cdn-overview.md) met en cache le contenu web statique à des emplacements stratégiques afin de fournir un débit maximal pour la distribution de contenu aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6b550-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="6b550-105">Le CDN réduit également la charge du serveur sur votre application web.</span><span class="sxs-lookup"><span data-stu-id="6b550-105">The CDN also decreases server load on your web app.</span></span> <span data-ttu-id="6b550-106">Ce didacticiel montre comment ajouter Azure CDN à une [application web dans Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b550-106">This tutorial shows how to add Azure CDN to a [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="6b550-107">Voici la page d’accueil de l’exemple de site HTML statique que vous allez utiliser :</span><span class="sxs-lookup"><span data-stu-id="6b550-107">Here's the home page of the sample static HTML site that you'll work with:</span></span>

![Page d’accueil de l’exemple d’application](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="6b550-109">Ce que vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="6b550-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b550-110">Créer un point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="6b550-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="6b550-111">Actualiser les ressources mises en cache.</span><span class="sxs-lookup"><span data-stu-id="6b550-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="6b550-112">Utiliser des chaînes de requête pour contrôler les versions mises en cache.</span><span class="sxs-lookup"><span data-stu-id="6b550-112">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="6b550-113">Utiliser un domaine personnalisé pour le point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="6b550-113">Use a custom domain for the CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b550-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6b550-114">Prerequisites</span></span>

<span data-ttu-id="6b550-115">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="6b550-115">To complete this tutorial:</span></span>

- [<span data-ttu-id="6b550-116">Installez Git</span><span class="sxs-lookup"><span data-stu-id="6b550-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="6b550-117">Installation d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6b550-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-web-app"></a><span data-ttu-id="6b550-118">Créer l’application web</span><span class="sxs-lookup"><span data-stu-id="6b550-118">Create the web app</span></span>

<span data-ttu-id="6b550-119">Pour créer l’application web que vous allez utiliser, suivez les instructions de l’article [Créer une application web HTML statique dans Azure](app-service-web-get-started-html.md) jusqu’à la fin de l’étape **Accéder à l’application**.</span><span class="sxs-lookup"><span data-stu-id="6b550-119">To create the web app that you'll work with, follow the [static HTML quickstart](app-service-web-get-started-html.md) through the **Browse to the app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="6b550-120">Nécessité d’avoir un nom de domaine</span><span class="sxs-lookup"><span data-stu-id="6b550-120">Have a custom domain ready</span></span>

<span data-ttu-id="6b550-121">Pour suivre l’étape relative au domaine personnalisé de ce didacticiel, vous devez posséder un domaine personnalisé et avoir accès à votre registre DNS pour votre fournisseur de domaine (tel que GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="6b550-121">To complete the custom domain step of this tutorial, you need to own a custom domain and have access to your DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="6b550-122">Par exemple, pour ajouter des entrées DNS pour `contoso.com` et `www.contoso.com`, vous devez pouvoir configurer les paramètres DNS du domaine racine `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="6b550-122">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must have access to configure the DNS settings for the `contoso.com` root domain.</span></span>

<span data-ttu-id="6b550-123">Si vous n’avez pas encore de nom de domaine, suivez le [didacticiel sur le domaine App Service](custom-dns-web-site-buydomains-web-app.md) pour acheter un domaine à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6b550-123">If you don't already have a domain name, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="6b550-124">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6b550-124">Log in to the Azure portal</span></span>

<span data-ttu-id="6b550-125">Ouvrez un navigateur et accédez au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6b550-125">Open a browser and navigate to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="6b550-126">Création d’un profil CDN et d’un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="6b550-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="6b550-127">Dans le volet de navigation gauche, sélectionnez **App Services**, puis sélectionnez l’application que vous avez créée à la rubrique [Créer une application web HTML statique dans Azure en 5 minutes](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="6b550-127">In the left navigation, select **App Services**, and then select the app that you created in the [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Sélection de l’application App Service dans le portail](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="6b550-129">Dans la page **App Service**, dans la section **Paramètres**, sélectionnez **Mise en réseau > Configurer Azure CDN pour votre application**.</span><span class="sxs-lookup"><span data-stu-id="6b550-129">In the **App Service** page, in the **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Sélection de CDN dans le portail](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="6b550-131">Dans la page **Azure Content Delivery Network**, fournissez les paramètres du **Nouveau point de terminaison**, comme spécifié dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="6b550-131">In the **Azure Content Delivery Network** page, provide the **New endpoint** settings as specified in the table.</span></span>

![Création d’un profil et d’un point de terminaison dans le portail](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="6b550-133">Paramètre</span><span class="sxs-lookup"><span data-stu-id="6b550-133">Setting</span></span> | <span data-ttu-id="6b550-134">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="6b550-134">Suggested value</span></span> | <span data-ttu-id="6b550-135">Description</span><span class="sxs-lookup"><span data-stu-id="6b550-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="6b550-136">**Profil CDN**</span><span class="sxs-lookup"><span data-stu-id="6b550-136">**CDN profile**</span></span> | <span data-ttu-id="6b550-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="6b550-137">myCDNProfile</span></span> | <span data-ttu-id="6b550-138">Sélectionnez **Créer** pour créer un profil CDN.</span><span class="sxs-lookup"><span data-stu-id="6b550-138">Select **Create new** to create a CDN profile.</span></span> <span data-ttu-id="6b550-139">Un profil CDN est une collection de points de terminaison CDN possédant le même niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="6b550-139">A CDN profile is a collection of CDN endpoints with the same pricing tier.</span></span> |
| <span data-ttu-id="6b550-140">**Niveau de tarification**</span><span class="sxs-lookup"><span data-stu-id="6b550-140">**Pricing tier**</span></span> | <span data-ttu-id="6b550-141">Standard Akamai</span><span class="sxs-lookup"><span data-stu-id="6b550-141">Standard Akamai</span></span> | <span data-ttu-id="6b550-142">Le [niveau tarifaire](../cdn/cdn-overview.md#azure-cdn-features) spécifie le fournisseur et les fonctionnalités disponibles.</span><span class="sxs-lookup"><span data-stu-id="6b550-142">The [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies the provider and available features.</span></span> <span data-ttu-id="6b550-143">Dans ce didacticiel, nous utilisons Standard Akamai.</span><span class="sxs-lookup"><span data-stu-id="6b550-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="6b550-144">**Nom du point de terminaison CDN**</span><span class="sxs-lookup"><span data-stu-id="6b550-144">**CDN endpoint name**</span></span> | <span data-ttu-id="6b550-145">N’importe quel nom qui est unique dans le domaine azureedge.net</span><span class="sxs-lookup"><span data-stu-id="6b550-145">Any name that is unique in the azureedge.net domain</span></span> | <span data-ttu-id="6b550-146">Vous accédez à vos ressources mises en cache au niveau du *\<Nom_Point_Terminaison>.azureedge.net* du domaine.</span><span class="sxs-lookup"><span data-stu-id="6b550-146">You access your cached resources at the domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="6b550-147">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6b550-147">Select **Create**.</span></span>

<span data-ttu-id="6b550-148">Azure crée le profil et le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6b550-148">Azure creates the profile and endpoint.</span></span> <span data-ttu-id="6b550-149">Le nouveau point de terminaison s’affiche dans la liste **Points de terminaison** sur la même page, et lorsqu’il est configuré, l’état est **Exécution en cours**.</span><span class="sxs-lookup"><span data-stu-id="6b550-149">The new endpoint appears in the **Endpoints** list on the same page, and when it's provisioned the status is **Running**.</span></span>

![Nouveau point de terminaison dans la liste](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-the-cdn-endpoint"></a><span data-ttu-id="6b550-151">Test du point de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="6b550-151">Test the CDN endpoint</span></span>

<span data-ttu-id="6b550-152">Si vous avez sélectionné le niveau tarifaire Verizon, il faut généralement compter environ 90 minutes pour la propagation du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6b550-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="6b550-153">Pour Akamai, la propagation prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="6b550-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="6b550-154">L’exemple d’application comprend un fichier `index.html` et des dossiers *css*, *img* et *js* contenant d’autres ressources statiques.</span><span class="sxs-lookup"><span data-stu-id="6b550-154">The sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="6b550-155">Les chemins d’accès de contenu pour tous ces fichiers sont identiques au point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="6b550-155">The content paths for all of these files are the same at the CDN endpoint.</span></span> <span data-ttu-id="6b550-156">Par exemple, les deux URL suivantes accèdent au fichier *bootstrap.css* dans le dossier *css* :</span><span class="sxs-lookup"><span data-stu-id="6b550-156">For example, both of the following URLs access the *bootstrap.css* file in the *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="6b550-157">Dans un navigateur, accédez à l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="6b550-157">Navigate a browser to the following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Page d’accueil de l’exemple d’application traitée à partir du CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="6b550-159">Vous consultez la page que vous avez exécutée précédemment dans une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="6b550-159">You see the same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="6b550-160">Azure CDN a récupéré les ressources de l’application web d’origine et les traite à partir du point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="6b550-160">Azure CDN has retrieved the origin web app's assets and is serving them from the CDN endpoint</span></span>

<span data-ttu-id="6b550-161">Pour vous assurer que cette page est mise en cache dans le CDN, actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="6b550-161">To ensure that this page is cached in the CDN, refresh the page.</span></span> <span data-ttu-id="6b550-162">Deux demandes pour la même ressource sont parfois nécessaires pour que le CDN mette en cache le contenu demandé.</span><span class="sxs-lookup"><span data-stu-id="6b550-162">Two requests for the same asset are sometimes required for the CDN to cache the requested content.</span></span>

<span data-ttu-id="6b550-163">Pour plus d’informations sur la création de profils et de points de terminaison Azure CDN, consultez [Prise en main d’Azure CDN](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="6b550-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-the-cdn"></a><span data-ttu-id="6b550-164">Vidage du CDN</span><span class="sxs-lookup"><span data-stu-id="6b550-164">Purge the CDN</span></span>

<span data-ttu-id="6b550-165">Le CDN actualise régulièrement ses ressources à partir de l’application web d’origine en fonction de la configuration de la durée de vie (TTL).</span><span class="sxs-lookup"><span data-stu-id="6b550-165">The CDN periodically refreshes its resources from the origin web app based on the time-to-live (TTL) configuration.</span></span> <span data-ttu-id="6b550-166">La valeur TTL par défaut est de sept jours.</span><span class="sxs-lookup"><span data-stu-id="6b550-166">The default TTL is seven days.</span></span>

<span data-ttu-id="6b550-167">Dans certains cas, vous devrez peut-être actualiser le CDN avant l’expiration de la durée de vie ; par exemple, lorsque vous déployez un contenu mis à jour dans l’application web.</span><span class="sxs-lookup"><span data-stu-id="6b550-167">At times you might need to refresh the CDN before the TTL expiration -- for example, when you deploy updated content to the web app.</span></span> <span data-ttu-id="6b550-168">Pour déclencher une actualisation, vous pouvez vider manuellement les ressources CDN.</span><span class="sxs-lookup"><span data-stu-id="6b550-168">To trigger a refresh, you can manually purge the CDN resources.</span></span> 

<span data-ttu-id="6b550-169">Dans cette section du didacticiel, vous déployez une modification dans l’application web et videz le CDN pour le forcer à actualiser son cache.</span><span class="sxs-lookup"><span data-stu-id="6b550-169">In this section of the tutorial, you deploy a change to the web app and purge the CDN to trigger the CDN to refresh its cache.</span></span>

### <a name="deploy-a-change-to-the-web-app"></a><span data-ttu-id="6b550-170">Déploiement d’une modification dans l’application web</span><span class="sxs-lookup"><span data-stu-id="6b550-170">Deploy a change to the web app</span></span>

<span data-ttu-id="6b550-171">Ouvrez le fichier `index.html` et ajoutez « - V2 » au titre H1, comme illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6b550-171">Open the `index.html` file and add "- V2" to the H1 heading, as shown in the following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="6b550-172">Validez votre modification et déployez-la dans l’application web.</span><span class="sxs-lookup"><span data-stu-id="6b550-172">Commit your change and deploy it to the web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="6b550-173">Une fois le déploiement terminé, accédez à l’URL de l’application web pour constater la modification.</span><span class="sxs-lookup"><span data-stu-id="6b550-173">Once deployment has completed, browse to the web app URL and you see the change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![V2 dans le titre de l’application web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="6b550-175">Accédez à l’URL du point de terminaison CDN pour ouvrir la page d’accueil ; vous ne voyez pas la modification car la version mise en cache dans le CDN n’a pas encore expiré.</span><span class="sxs-lookup"><span data-stu-id="6b550-175">Browse to the CDN endpoint URL for the home page and you don't see the change because the cached version in the CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Pas de V2 dans le titre du CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-the-cdn-in-the-portal"></a><span data-ttu-id="6b550-177">Vidage du CDN dans le portail</span><span class="sxs-lookup"><span data-stu-id="6b550-177">Purge the CDN in the portal</span></span>

<span data-ttu-id="6b550-178">Pour forcer le CDN à mettre à jour sa version mise en cache, videz le CDN.</span><span class="sxs-lookup"><span data-stu-id="6b550-178">To trigger the CDN to update its cached version, purge the CDN.</span></span>

<span data-ttu-id="6b550-179">Dans le portail de navigation gauche, sélectionnez **Groupes de ressources**, puis sélectionnez le groupe de ressources que vous avez créé pour votre application web (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="6b550-179">In the portal left navigation, select **Resource groups**, and then select the resource group that you created for your web app (myResourceGroup).</span></span>

![Sélection du groupe de ressources](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="6b550-181">Dans la liste des ressources, sélectionnez votre point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="6b550-181">In the list of resources, select your CDN endpoint.</span></span>

![Sélection du point de terminaison](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="6b550-183">En haut de la page **Point de terminaison**, cliquez sur **Vider**.</span><span class="sxs-lookup"><span data-stu-id="6b550-183">At the top of the **Endpoint** page, click **Purge**.</span></span>

![Sélection de l’option Vider](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="6b550-185">Tapez les chemins d’accès de contenu que vous souhaitez vider.</span><span class="sxs-lookup"><span data-stu-id="6b550-185">Enter the content paths you wish to purge.</span></span> <span data-ttu-id="6b550-186">Vous pouvez transmettre un chemin d’accès complet pour vider un fichier individuel ou un segment de chemin d’accès pour vider et actualiser tout le contenu d’un dossier.</span><span class="sxs-lookup"><span data-stu-id="6b550-186">You can pass a complete file path to purge an individual file, or a path segment to purge and refresh all content in a folder.</span></span> <span data-ttu-id="6b550-187">Étant donné que vous avez modifié `index.html`, vérifiez qu’il s’agit de l’un des chemins d’accès.</span><span class="sxs-lookup"><span data-stu-id="6b550-187">Since you changed `index.html`, make sure that is one of the paths.</span></span>

<span data-ttu-id="6b550-188">En bas de la page, sélectionnez **Vider**.</span><span class="sxs-lookup"><span data-stu-id="6b550-188">At the bottom of the page, select **Purge**.</span></span>

![Vidage de la page](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-the-cdn-is-updated"></a><span data-ttu-id="6b550-190">Vérification de la mise à jour du CDN</span><span class="sxs-lookup"><span data-stu-id="6b550-190">Verify that the CDN is updated</span></span>

<span data-ttu-id="6b550-191">Attendez que le traitement de la demande de vidage soit terminé, généralement quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="6b550-191">Wait until the purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="6b550-192">Pour afficher l’état actuel, sélectionnez l’icône représentant une cloche en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="6b550-192">To see the current status, select the bell icon at the top of the page.</span></span> 

![Notification de vidage](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="6b550-194">Accédez à la page `index.html` de l’URL du point de terminaison CDN ; à présent, le V2 que vous avez ajouté au titre est affiché sur la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="6b550-194">Browse to the CDN endpoint URL for `index.html`, and now you see the V2 that you added to the title on the home page.</span></span> <span data-ttu-id="6b550-195">Cela indique que le cache du CDN a été actualisé.</span><span class="sxs-lookup"><span data-stu-id="6b550-195">This shows that the CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![V2 dans le titre du CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="6b550-197">Pour plus d’informations, consultez [Purger un point de terminaison CDN Azure](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="6b550-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-to-version-content"></a><span data-ttu-id="6b550-198">Utiliser des chaînes de requête pour contrôler la version du contenu</span><span class="sxs-lookup"><span data-stu-id="6b550-198">Use query strings to version content</span></span>

<span data-ttu-id="6b550-199">Le CDN Azure offre les options de comportement de mise en cache suivantes :</span><span class="sxs-lookup"><span data-stu-id="6b550-199">The Azure CDN offers the following caching behavior options:</span></span>

* <span data-ttu-id="6b550-200">Ignorer les chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="6b550-200">Ignore query strings</span></span>
* <span data-ttu-id="6b550-201">Contourner la mise en cache pour les chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="6b550-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="6b550-202">Mettre en cache chaque URL unique</span><span class="sxs-lookup"><span data-stu-id="6b550-202">Cache every unique URL</span></span> 

<span data-ttu-id="6b550-203">La première option est la valeur par défaut, ce qui signifie qu’il n’existe qu’une seule version mise en cache d’une ressource, quelle que soit la chaîne de requête de l’URL.</span><span class="sxs-lookup"><span data-stu-id="6b550-203">The first of these is the default, which means there is only one cached version of an asset regardless of the query string in the URL.</span></span> 

<span data-ttu-id="6b550-204">Dans cette section du didacticiel, vous modifiez le comportement de mise en cache pour mettre en cache chaque URL unique.</span><span class="sxs-lookup"><span data-stu-id="6b550-204">In this section of the tutorial, you change the caching behavior to cache every unique URL.</span></span>

### <a name="change-the-cache-behavior"></a><span data-ttu-id="6b550-205">Modification du comportement de mise en cache</span><span class="sxs-lookup"><span data-stu-id="6b550-205">Change the cache behavior</span></span>

<span data-ttu-id="6b550-206">Dans la page **Point de terminaison CDN** du portail Azure, sélectionnez **Cache**.</span><span class="sxs-lookup"><span data-stu-id="6b550-206">In the Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="6b550-207">Sélectionnez **Mettre en cache chaque URL unique** dans la liste déroulante **Comportement de mise en cache des chaînes de requête**.</span><span class="sxs-lookup"><span data-stu-id="6b550-207">Select **Cache every unique URL** from the **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="6b550-208">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6b550-208">Select **Save**.</span></span>

![Sélection du comportement de mise en cache de chaîne de requête](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="6b550-210">Vérification de la mise en cache séparée des URL uniques</span><span class="sxs-lookup"><span data-stu-id="6b550-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="6b550-211">Dans un navigateur, accédez à la page d’accueil au niveau du point de terminaison CDN, mais incluez une chaîne de requête :</span><span class="sxs-lookup"><span data-stu-id="6b550-211">In a browser, navigate to the home page at the CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="6b550-212">Le CDN retourne le contenu de l’application web actuelle, qui inclut « V2 » dans le titre.</span><span class="sxs-lookup"><span data-stu-id="6b550-212">The CDN returns the current web app content, which includes "V2" in the heading.</span></span> 

<span data-ttu-id="6b550-213">Pour vous assurer que cette page est mise en cache dans le CDN, actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="6b550-213">To ensure that this page is cached in the CDN, refresh the page.</span></span> 

<span data-ttu-id="6b550-214">Ouvrez `index.html` et remplacez « V2 » par « V3 », puis déployez la modification.</span><span class="sxs-lookup"><span data-stu-id="6b550-214">Open `index.html` and change "V2" to "V3", and deploy the change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="6b550-215">Dans un navigateur, accédez à l’URL du point de terminaison CDN avec une nouvelle chaîne de requête telle que `q=2`.</span><span class="sxs-lookup"><span data-stu-id="6b550-215">In a browser, go to the CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="6b550-216">Le CDN obtient le fichier `index.html` actuel et affiche « V3 ».</span><span class="sxs-lookup"><span data-stu-id="6b550-216">The CDN gets the current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="6b550-217">Mais si vous naviguez vers le point de terminaison CDN avec la chaîne de requête `q=1`, vous voyez « V2 ».</span><span class="sxs-lookup"><span data-stu-id="6b550-217">But if you navigate to the CDN endpoint with the `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 dans le titre dans le CDN, chaîne de requête 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 dans le titre dans le CDN, chaîne de requête 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="6b550-220">Cette sortie montre que chaque chaîne de requête est traitée différemment :</span><span class="sxs-lookup"><span data-stu-id="6b550-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="6b550-221">Comme la chaîne de requête q=1 a été utilisée précédemment, le contenu mis en cache est retourné (V2).</span><span class="sxs-lookup"><span data-stu-id="6b550-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="6b550-222">Comme la chaîne de requête q=2 est nouvelle, le contenu le plus récent de l’application web est récupéré et retourné (V3).</span><span class="sxs-lookup"><span data-stu-id="6b550-222">q=2 is new, so the latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="6b550-223">Pour plus d’informations, consultez [Contrôle du comportement de mise en cache du CDN Azure avec des chaînes de requête](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="6b550-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-to-a-cdn-endpoint"></a><span data-ttu-id="6b550-224">Mappage d’un domaine personnalisé à un point de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="6b550-224">Map a custom domain to a CDN endpoint</span></span>

<span data-ttu-id="6b550-225">Vous mappez votre domaine personnalisé à votre point de terminaison CDN en créant un enregistrement CNAME.</span><span class="sxs-lookup"><span data-stu-id="6b550-225">You'll map your custom domain to your CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="6b550-226">Un enregistrement CNAME est une fonctionnalité DNS qui mappe un domaine source à un domaine cible.</span><span class="sxs-lookup"><span data-stu-id="6b550-226">A CNAME record is a DNS feature that maps a source domain to a destination domain.</span></span> <span data-ttu-id="6b550-227">Par exemple, vous pouvez mapper `cdn.contoso.com` ou `static.contoso.com` à `contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="6b550-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` to `contoso.azureedge.net`.</span></span>

<span data-ttu-id="6b550-228">Si vous n’avez pas de domaine personnalisé, suivez le [didacticiel sur le domaine App Service](custom-dns-web-site-buydomains-web-app.md) pour acheter un domaine à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6b550-228">If you don't have a custom domain, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

### <a name="find-the-hostname-to-use-with-the-cname"></a><span data-ttu-id="6b550-229">Recherche du nom d’hôte à utiliser avec l’enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="6b550-229">Find the hostname to use with the CNAME</span></span>

<span data-ttu-id="6b550-230">Dans la page **Point de terminaison** du portail Azure, vérifiez que **Vue d’ensemble** est sélectionné dans le volet de navigation gauche, puis sélectionnez le bouton **+ Domaine personnalisé** en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="6b550-230">In the Azure portal **Endpoint** page, make sure **Overview** is selected in the left navigation, and then select the **+ Custom Domain** button at the top of the page.</span></span>

![Sélection de l’ajout d’un domaine personnalisé](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="6b550-232">Dans la page **Ajouter un domaine personnalisé**, vous voyez le nom d’hôte du point de terminaison à utiliser pour la création d’un enregistrement CNAME.</span><span class="sxs-lookup"><span data-stu-id="6b550-232">In the **Add a custom domain** page, you see the endpoint host name to use in creating a CNAME record.</span></span> <span data-ttu-id="6b550-233">Le nom d’hôte est dérivé de votre URL de point de terminaison CDN : **&lt;Nom_Point_Terminaison>.azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="6b550-233">The host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Ajout d’une page de domaine](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-the-cname-with-your-domain-registrar"></a><span data-ttu-id="6b550-235">Configuration de l’enregistrement CNAME avec votre bureau d’enregistrement de domaines</span><span class="sxs-lookup"><span data-stu-id="6b550-235">Configure the CNAME with your domain registrar</span></span>

<span data-ttu-id="6b550-236">Accédez au site web de votre bureau d'enregistrement de domaines et recherchez la section de la création d'enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="6b550-236">Navigate to your domain registrar's web site, and locate the section for creating DNS records.</span></span> <span data-ttu-id="6b550-237">Vous pourrez trouver ces informations dans une section telle que **Domain Name**, **DNS** ou **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="6b550-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="6b550-238">Recherchez la section relative à la gestion des enregistrements CNAME.</span><span class="sxs-lookup"><span data-stu-id="6b550-238">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="6b550-239">Pour cela, accédez à une page de paramètres avancés et recherchez les mots CNAME, Alias ou Sous-domaines.</span><span class="sxs-lookup"><span data-stu-id="6b550-239">You may have to go to an advanced settings page and look for the words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="6b550-240">Créez un enregistrement CNAME qui mappe votre sous-domaine choisi (par exemple, **static** ou **cdn**) au **nom d’hôte du point de terminaison** affiché précédemment dans le portail.</span><span class="sxs-lookup"><span data-stu-id="6b550-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) to the **Endpoint host name** shown earlier in the portal.</span></span> 

### <a name="enter-the-custom-domain-in-azure"></a><span data-ttu-id="6b550-241">Saisie du domaine personnalisé dans Azure</span><span class="sxs-lookup"><span data-stu-id="6b550-241">Enter the custom domain in Azure</span></span>

<span data-ttu-id="6b550-242">Revenez à la page **Ajouter un domaine personnalisé**, puis entrez votre domaine personnalisé, dont le sous-domaine, dans la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6b550-242">Return to the **Add a custom domain** page, and enter your custom domain, including the subdomain, in the dialog box.</span></span> <span data-ttu-id="6b550-243">Par exemple, entrez : `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="6b550-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="6b550-244">Azure vérifie que l’enregistrement CNAME existe pour le nom de domaine que vous avez entré.</span><span class="sxs-lookup"><span data-stu-id="6b550-244">Azure verifies that the CNAME record exists for the domain name you have entered.</span></span> <span data-ttu-id="6b550-245">Si l'enregistrement CNAME est correct, votre domaine personnalisé est validé.</span><span class="sxs-lookup"><span data-stu-id="6b550-245">If the CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="6b550-246">La propagation de l’enregistrement CNAME aux serveurs de noms sur Internet peut prendre du temps.</span><span class="sxs-lookup"><span data-stu-id="6b550-246">It can take time for the CNAME record to propagate to name servers on the Internet.</span></span> <span data-ttu-id="6b550-247">Si votre domaine n’est pas validé immédiatement, patientez quelques minutes, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="6b550-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-the-custom-domain"></a><span data-ttu-id="6b550-248">Test du domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="6b550-248">Test the custom domain</span></span>

<span data-ttu-id="6b550-249">Dans un navigateur, accédez au fichier `index.html` à l’aide de votre domaine personnalisé (par exemple, `cdn.contoso.com/index.html`) pour vérifier que le résultat est le même que lorsque vous accédez directement à `<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="6b550-249">In a browser, navigate to the `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) to verify that the result is the same as when you go directly to `<endpointname>azureedge.net/index.html`.</span></span>

![Page d’accueil d’exemple d’application utilisant l’URL du domaine personnalisé](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="6b550-251">Pour plus d’informations, consultez [Mapper du contenu Azure CDN à un domaine personnalisé](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="6b550-251">For more information, see [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="6b550-252">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6b550-252">Next steps</span></span>

<span data-ttu-id="6b550-253">Vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6b550-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b550-254">Créer un point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="6b550-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="6b550-255">Actualiser les ressources mises en cache.</span><span class="sxs-lookup"><span data-stu-id="6b550-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="6b550-256">Utiliser des chaînes de requête pour contrôler les versions mises en cache.</span><span class="sxs-lookup"><span data-stu-id="6b550-256">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="6b550-257">Utiliser un domaine personnalisé pour le point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="6b550-257">Use a custom domain for the CDN endpoint.</span></span>

<span data-ttu-id="6b550-258">Découvrez comment optimiser les performances du réseau CDN dans les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="6b550-258">Learn how to optimize CDN performance in the following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b550-259">Compression des fichiers dans Azure CDN pour améliorer les performances</span><span class="sxs-lookup"><span data-stu-id="6b550-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b550-260">Préchargement d’éléments multimédias sur un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="6b550-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
