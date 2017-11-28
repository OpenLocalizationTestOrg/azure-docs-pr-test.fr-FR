---
title: aaaAdd un tooan CDN Azure App Service | Documents Microsoft
description: "Ajouter un toocache de Azure App Service de réseau de distribution de contenu (CDN) tooan et remettre vos fichiers statiques à partir de serveurs clients de fermer tooyour hello du monde."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a><span data-ttu-id="d328b-103">Ajouter un tooan de réseau de distribution de contenu (CDN) Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d328b-103">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>

<span data-ttu-id="d328b-104">[Réseau de distribution de contenu (CDN) Azure](../cdn/cdn-overview.md) met en cache le contenu web statique au débit maximal de tooprovide emplacements stratégiques pour la diffusion de contenu toousers.</span><span class="sxs-lookup"><span data-stu-id="d328b-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations tooprovide maximum throughput for delivering content toousers.</span></span> <span data-ttu-id="d328b-105">Hello CDN réduit également la charge du serveur sur votre application web.</span><span class="sxs-lookup"><span data-stu-id="d328b-105">hello CDN also decreases server load on your web app.</span></span> <span data-ttu-id="d328b-106">Ce didacticiel montre comment tooadd Azure CDN tooa [application web dans Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d328b-106">This tutorial shows how tooadd Azure CDN tooa [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="d328b-107">Voici la page d’accueil hello de hello exemple site HTML statique que vous allez travailler avec :</span><span class="sxs-lookup"><span data-stu-id="d328b-107">Here's hello home page of hello sample static HTML site that you'll work with:</span></span>

![Page d’accueil de l’exemple d’application](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="d328b-109">Ce que vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="d328b-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d328b-110">Créer un point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d328b-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="d328b-111">Actualiser les ressources mises en cache.</span><span class="sxs-lookup"><span data-stu-id="d328b-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="d328b-112">Utiliser la requête des chaînes de versions de toocontrol mis en cache.</span><span class="sxs-lookup"><span data-stu-id="d328b-112">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="d328b-113">Utilisez un domaine personnalisé pour le point de terminaison CDN hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-113">Use a custom domain for hello CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d328b-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d328b-114">Prerequisites</span></span>

<span data-ttu-id="d328b-115">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="d328b-115">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="d328b-116">Installez Git</span><span class="sxs-lookup"><span data-stu-id="d328b-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="d328b-117">Installation d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d328b-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a><span data-ttu-id="d328b-118">Créer une application web de hello</span><span class="sxs-lookup"><span data-stu-id="d328b-118">Create hello web app</span></span>

<span data-ttu-id="d328b-119">toocreate hello web application que vous allez travailler avec suivi hello [démarrage rapide HTML statique](app-service-web-get-started-html.md) via hello **Parcourir toohello application** étape.</span><span class="sxs-lookup"><span data-stu-id="d328b-119">toocreate hello web app that you'll work with, follow hello [static HTML quickstart](app-service-web-get-started-html.md) through hello **Browse toohello app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="d328b-120">Nécessité d’avoir un nom de domaine</span><span class="sxs-lookup"><span data-stu-id="d328b-120">Have a custom domain ready</span></span>

<span data-ttu-id="d328b-121">étape de domaine personnalisé hello toocomplete de ce didacticiel, vous devez tooown un domaine personnalisé et disposer du Registre de l’accès tooyour DNS pour votre fournisseur de domaine (par exemple, GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="d328b-121">toocomplete hello custom domain step of this tutorial, you need tooown a custom domain and have access tooyour DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="d328b-122">Par exemple, les entrées DNS tooadd pour `contoso.com` et `www.contoso.com`, tooconfigure accès hello vos paramètres DNS pour hello doivent être `contoso.com` domaine racine.</span><span class="sxs-lookup"><span data-stu-id="d328b-122">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must have access tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

<span data-ttu-id="d328b-123">Si vous n’avez pas encore un nom de domaine, envisagez d’hello [didacticiel du domaine du Service d’applications](custom-dns-web-site-buydomains-web-app.md) toopurchase un domaine à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d328b-123">If you don't already have a domain name, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="d328b-124">Ouvrez une session dans toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d328b-124">Log in toohello Azure portal</span></span>

<span data-ttu-id="d328b-125">Ouvrez un navigateur et accédez toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d328b-125">Open a browser and navigate toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="d328b-126">Création d’un profil CDN et d’un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="d328b-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="d328b-127">Bonjour barre de navigation gauche, sélectionnez **des Services d’application**, puis sélectionnez application hello que vous avez créé dans hello [démarrage rapide HTML statique](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="d328b-127">In hello left navigation, select **App Services**, and then select hello app that you created in hello [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Sélectionnez l’application de Service d’applications dans le portail de hello](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="d328b-129">Bonjour **du Service d’applications** page hello **paramètres** section, sélectionnez **mise en réseau > configurer le CDN Azure pour votre application**.</span><span class="sxs-lookup"><span data-stu-id="d328b-129">In hello **App Service** page, in hello **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Sélectionnez le CDN dans le portail de hello](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="d328b-131">Bonjour **Azure Content Delivery Network** , fournissez hello **nouveau point de terminaison** paramètres comme spécifié dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-131">In hello **Azure Content Delivery Network** page, provide hello **New endpoint** settings as specified in hello table.</span></span>

![Créer le point de terminaison et un profil dans le portail de hello](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="d328b-133">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d328b-133">Setting</span></span> | <span data-ttu-id="d328b-134">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="d328b-134">Suggested value</span></span> | <span data-ttu-id="d328b-135">Description</span><span class="sxs-lookup"><span data-stu-id="d328b-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="d328b-136">**Profil CDN**</span><span class="sxs-lookup"><span data-stu-id="d328b-136">**CDN profile**</span></span> | <span data-ttu-id="d328b-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="d328b-137">myCDNProfile</span></span> | <span data-ttu-id="d328b-138">Sélectionnez **nouvel** toocreate profil CDN.</span><span class="sxs-lookup"><span data-stu-id="d328b-138">Select **Create new** toocreate a CDN profile.</span></span> <span data-ttu-id="d328b-139">Profil CDN est une collection de points de terminaison CDN avec hello même niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="d328b-139">A CDN profile is a collection of CDN endpoints with hello same pricing tier.</span></span> |
| <span data-ttu-id="d328b-140">**Niveau tarifaire**</span><span class="sxs-lookup"><span data-stu-id="d328b-140">**Pricing tier**</span></span> | <span data-ttu-id="d328b-141">Standard Akamai</span><span class="sxs-lookup"><span data-stu-id="d328b-141">Standard Akamai</span></span> | <span data-ttu-id="d328b-142">Hello [tarification](../cdn/cdn-overview.md#azure-cdn-features) Spécifie le fournisseur de hello et les fonctionnalités disponibles.</span><span class="sxs-lookup"><span data-stu-id="d328b-142">hello [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies hello provider and available features.</span></span> <span data-ttu-id="d328b-143">Dans ce didacticiel, nous utilisons Standard Akamai.</span><span class="sxs-lookup"><span data-stu-id="d328b-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="d328b-144">**Nom du point de terminaison CDN**</span><span class="sxs-lookup"><span data-stu-id="d328b-144">**CDN endpoint name**</span></span> | <span data-ttu-id="d328b-145">N’importe quel nom qui est unique dans le domaine de azureedge.net hello</span><span class="sxs-lookup"><span data-stu-id="d328b-145">Any name that is unique in hello azureedge.net domain</span></span> | <span data-ttu-id="d328b-146">Accéder à vos ressources mises en cache au niveau du domaine de hello  *\<endpointname >. azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="d328b-146">You access your cached resources at hello domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="d328b-147">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d328b-147">Select **Create**.</span></span>

<span data-ttu-id="d328b-148">Azure crée le point de terminaison et le profil de hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-148">Azure creates hello profile and endpoint.</span></span> <span data-ttu-id="d328b-149">nouveau point de terminaison Hello s’affiche dans hello **points de terminaison** liste hello même page, et lorsqu’elle est approvisionnée hello statut **en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="d328b-149">hello new endpoint appears in hello **Endpoints** list on hello same page, and when it's provisioned hello status is **Running**.</span></span>

![Nouveau point de terminaison dans la liste](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="d328b-151">Hello de test point de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="d328b-151">Test hello CDN endpoint</span></span>

<span data-ttu-id="d328b-152">Si vous avez sélectionné le niveau tarifaire Verizon, il faut généralement compter environ 90 minutes pour la propagation du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d328b-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="d328b-153">Pour Akamai, la propagation prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="d328b-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="d328b-154">exemple d’application Hello a un `index.html` fichier et *css*, *img*, et *js* dossiers qui contiennent d’autres ressources statiques.</span><span class="sxs-lookup"><span data-stu-id="d328b-154">hello sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="d328b-155">Hello contenu sont des chemins d’accès pour tous ces fichiers hello identique au point de terminaison CDN hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-155">hello content paths for all of these files are hello same at hello CDN endpoint.</span></span> <span data-ttu-id="d328b-156">Par exemple, les deux URL suivantes de hello accéder hello *bootstrap.css* fichier Bonjour *css* dossier :</span><span class="sxs-lookup"><span data-stu-id="d328b-156">For example, both of hello following URLs access hello *bootstrap.css* file in hello *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="d328b-157">Accédez à un toohello navigateur suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="d328b-157">Navigate a browser toohello following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Page d’accueil de l’exemple d’application traitée à partir du CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="d328b-159">Vous consultez hello même page que vous avez exécuté précédemment dans une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="d328b-159">You see hello same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="d328b-160">Azure CDN a récupéré les ressources de l’application web hello origine et sert de point de terminaison CDN hello</span><span class="sxs-lookup"><span data-stu-id="d328b-160">Azure CDN has retrieved hello origin web app's assets and is serving them from hello CDN endpoint</span></span>

<span data-ttu-id="d328b-161">tooensure que cette page est mise en cache dans hello CDN, page hello d’actualisation.</span><span class="sxs-lookup"><span data-stu-id="d328b-161">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> <span data-ttu-id="d328b-162">Deux demandes pour hello même actif sont parfois requis pour hello CDN toocache hello contenu demandé.</span><span class="sxs-lookup"><span data-stu-id="d328b-162">Two requests for hello same asset are sometimes required for hello CDN toocache hello requested content.</span></span>

<span data-ttu-id="d328b-163">Pour plus d’informations sur la création de profils et de points de terminaison Azure CDN, consultez [Prise en main d’Azure CDN](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="d328b-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-hello-cdn"></a><span data-ttu-id="d328b-164">Purge hello CDN</span><span class="sxs-lookup"><span data-stu-id="d328b-164">Purge hello CDN</span></span>

<span data-ttu-id="d328b-165">Hello CDN actualise régulièrement ses ressources de l’application web de hello origine selon hello time-to-live (TTL) configuration.</span><span class="sxs-lookup"><span data-stu-id="d328b-165">hello CDN periodically refreshes its resources from hello origin web app based on hello time-to-live (TTL) configuration.</span></span> <span data-ttu-id="d328b-166">la valeur par défaut de Hello durée de vie est de sept jours.</span><span class="sxs-lookup"><span data-stu-id="d328b-166">hello default TTL is seven days.</span></span>

<span data-ttu-id="d328b-167">Dans certains cas vous devrez peut-être toorefresh hello CDN avant hello date d’expiration de la durée de vie : par exemple, lorsque vous déployez l’application web toohello contenu mis à jour.</span><span class="sxs-lookup"><span data-stu-id="d328b-167">At times you might need toorefresh hello CDN before hello TTL expiration -- for example, when you deploy updated content toohello web app.</span></span> <span data-ttu-id="d328b-168">tootrigger une actualisation, vous pouvez purger manuellement les ressources CDN hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-168">tootrigger a refresh, you can manually purge hello CDN resources.</span></span> 

<span data-ttu-id="d328b-169">Dans cette section du didacticiel de hello, vous déployez une application web de toohello modification et purgez hello CDN tootrigger hello CDN toorefresh son cache.</span><span class="sxs-lookup"><span data-stu-id="d328b-169">In this section of hello tutorial, you deploy a change toohello web app and purge hello CDN tootrigger hello CDN toorefresh its cache.</span></span>

### <a name="deploy-a-change-toohello-web-app"></a><span data-ttu-id="d328b-170">Déployer une application web de toohello modification</span><span class="sxs-lookup"><span data-stu-id="d328b-170">Deploy a change toohello web app</span></span>

<span data-ttu-id="d328b-171">Ouvrez hello `index.html` et ajoutez «-V2 « toohello H1 en-tête, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d328b-171">Open hello `index.html` file and add "- V2" toohello H1 heading, as shown in hello following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="d328b-172">Valider votre modification et déployer l’application web toohello.</span><span class="sxs-lookup"><span data-stu-id="d328b-172">Commit your change and deploy it toohello web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="d328b-173">Une fois le déploiement terminé, parcourir toohello URL de l’application web et que vous consultez hello modifier.</span><span class="sxs-lookup"><span data-stu-id="d328b-173">Once deployment has completed, browse toohello web app URL and you see hello change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![V2 dans le titre de l’application web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="d328b-175">URL de point de terminaison CDN Parcourir toohello pour la page d’accueil hello et que vous ne voyez pas hello modifier, car la version de mise en cache hello Bonjour CDN n’a pas encore expiré.</span><span class="sxs-lookup"><span data-stu-id="d328b-175">Browse toohello CDN endpoint URL for hello home page and you don't see hello change because hello cached version in hello CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Pas de V2 dans le titre du CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a><span data-ttu-id="d328b-177">Purge hello CDN dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="d328b-177">Purge hello CDN in hello portal</span></span>

<span data-ttu-id="d328b-178">tootrigger hello CDN tooupdate sa version mise en cache, la purge hello CDN.</span><span class="sxs-lookup"><span data-stu-id="d328b-178">tootrigger hello CDN tooupdate its cached version, purge hello CDN.</span></span>

<span data-ttu-id="d328b-179">Dans hello portail de navigation gauche, sélectionnez **groupes de ressources**, puis sélectionnez le groupe de ressources hello que vous avez créé pour votre application web (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="d328b-179">In hello portal left navigation, select **Resource groups**, and then select hello resource group that you created for your web app (myResourceGroup).</span></span>

![Sélection du groupe de ressources](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="d328b-181">Dans la liste hello des ressources, sélectionnez votre point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d328b-181">In hello list of resources, select your CDN endpoint.</span></span>

![Sélection du point de terminaison](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="d328b-183">En haut de hello Hello **point de terminaison** , cliquez sur **purger**.</span><span class="sxs-lookup"><span data-stu-id="d328b-183">At hello top of hello **Endpoint** page, click **Purge**.</span></span>

![Sélection de l’option Vider](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="d328b-185">Entrez les chemins de contenu hello toopurge vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d328b-185">Enter hello content paths you wish toopurge.</span></span> <span data-ttu-id="d328b-186">Vous pouvez passer un toopurge de chemin d’accès complet du fichier, un fichier individuel ou un toopurge de segment de chemin d’accès et actualiser tout le contenu dans un dossier.</span><span class="sxs-lookup"><span data-stu-id="d328b-186">You can pass a complete file path toopurge an individual file, or a path segment toopurge and refresh all content in a folder.</span></span> <span data-ttu-id="d328b-187">Étant donné que vous avez modifié `index.html`, assurez-vous qu’est un des chemins d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-187">Since you changed `index.html`, make sure that is one of hello paths.</span></span>

<span data-ttu-id="d328b-188">Au bas de hello de page de hello, sélectionnez **purger**.</span><span class="sxs-lookup"><span data-stu-id="d328b-188">At hello bottom of hello page, select **Purge**.</span></span>

![Vidage de la page](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a><span data-ttu-id="d328b-190">Vérifiez que hello que CDN est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="d328b-190">Verify that hello CDN is updated</span></span>

<span data-ttu-id="d328b-191">Attendez que la demande de vidage hello termine le traitement, en général de quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="d328b-191">Wait until hello purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="d328b-192">état actuel toosee hello icône de cloche sélectionnez hello en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-192">toosee hello current status, select hello bell icon at hello top of hello page.</span></span> 

![Notification de vidage](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="d328b-194">Parcourir les URL de point de terminaison CDN toohello pour `index.html`, et vous voyez à présent hello V2 que vous avez ajouté toohello titre sur la page d’accueil hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-194">Browse toohello CDN endpoint URL for `index.html`, and now you see hello V2 that you added toohello title on hello home page.</span></span> <span data-ttu-id="d328b-195">Cela indique que le cache CDN hello a été actualisé.</span><span class="sxs-lookup"><span data-stu-id="d328b-195">This shows that hello CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![V2 dans le titre du CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="d328b-197">Pour plus d’informations, consultez [Purger un point de terminaison CDN Azure](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="d328b-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-tooversion-content"></a><span data-ttu-id="d328b-198">Utiliser le contenu de tooversion de chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="d328b-198">Use query strings tooversion content</span></span>

<span data-ttu-id="d328b-199">Bonjour Azure CDN offre hello mise en cache des options de comportement suivantes :</span><span class="sxs-lookup"><span data-stu-id="d328b-199">hello Azure CDN offers hello following caching behavior options:</span></span>

* <span data-ttu-id="d328b-200">Ignorer les chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="d328b-200">Ignore query strings</span></span>
* <span data-ttu-id="d328b-201">Contourner la mise en cache pour les chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="d328b-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="d328b-202">Mettre en cache chaque URL unique</span><span class="sxs-lookup"><span data-stu-id="d328b-202">Cache every unique URL</span></span> 

<span data-ttu-id="d328b-203">Hello tout d’abord ces est par défaut hello, ce qui ne signifie qu’une version mise en cache d’un élément multimédia, quelle que soit la chaîne de requête hello hello URL.</span><span class="sxs-lookup"><span data-stu-id="d328b-203">hello first of these is hello default, which means there is only one cached version of an asset regardless of hello query string in hello URL.</span></span> 

<span data-ttu-id="d328b-204">Dans cette section du didacticiel de hello, vous modifiez hello mise en cache de comportement toocache chaque URL unique.</span><span class="sxs-lookup"><span data-stu-id="d328b-204">In this section of hello tutorial, you change hello caching behavior toocache every unique URL.</span></span>

### <a name="change-hello-cache-behavior"></a><span data-ttu-id="d328b-205">Modifier le comportement de cache hello</span><span class="sxs-lookup"><span data-stu-id="d328b-205">Change hello cache behavior</span></span>

<span data-ttu-id="d328b-206">Bonjour Azure portal **point de terminaison CDN** page, sélectionnez **Cache**.</span><span class="sxs-lookup"><span data-stu-id="d328b-206">In hello Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="d328b-207">Sélectionnez **mettre en Cache chaque URL unique** de hello **comportement de mise en cache de chaîne de requête** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="d328b-207">Select **Cache every unique URL** from hello **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="d328b-208">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d328b-208">Select **Save**.</span></span>

![Sélection du comportement de mise en cache de chaîne de requête](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="d328b-210">Vérification de la mise en cache séparée des URL uniques</span><span class="sxs-lookup"><span data-stu-id="d328b-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="d328b-211">Dans un navigateur, accédez de page d’accueil toohello au point de terminaison CDN hello, mais inclure une chaîne de requête :</span><span class="sxs-lookup"><span data-stu-id="d328b-211">In a browser, navigate toohello home page at hello CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="d328b-212">Hello CDN retourne hello web application contenu actuel, qui inclut « V2 » dans l’en-tête de hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-212">hello CDN returns hello current web app content, which includes "V2" in hello heading.</span></span> 

<span data-ttu-id="d328b-213">tooensure que cette page est mise en cache dans hello CDN, page hello d’actualisation.</span><span class="sxs-lookup"><span data-stu-id="d328b-213">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> 

<span data-ttu-id="d328b-214">Ouvrez `index.html` et également de modifier « V2 » « V3 » et déployer les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-214">Open `index.html` and change "V2" too"V3", and deploy hello change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="d328b-215">Dans un navigateur, accédez toohello URL de point de terminaison CDN avec une chaîne de requête, tel que `q=2`.</span><span class="sxs-lookup"><span data-stu-id="d328b-215">In a browser, go toohello CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="d328b-216">Hello CDN obtient hello actuel `index.html` de fichiers et affiche « V3 ».</span><span class="sxs-lookup"><span data-stu-id="d328b-216">hello CDN gets hello current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="d328b-217">Toutefois, si vous accédez toohello point de terminaison CDN avec hello `q=1` chaîne de requête, vous voyez « V2 ».</span><span class="sxs-lookup"><span data-stu-id="d328b-217">But if you navigate toohello CDN endpoint with hello `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 dans le titre dans le CDN, chaîne de requête 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 dans le titre dans le CDN, chaîne de requête 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="d328b-220">Cette sortie montre que chaque chaîne de requête est traitée différemment :</span><span class="sxs-lookup"><span data-stu-id="d328b-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="d328b-221">Comme la chaîne de requête q=1 a été utilisée précédemment, le contenu mis en cache est retourné (V2).</span><span class="sxs-lookup"><span data-stu-id="d328b-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="d328b-222">q = 2 est nouvelle, afin de contenu application web plus récente de hello est récupérés et retournée (V3).</span><span class="sxs-lookup"><span data-stu-id="d328b-222">q=2 is new, so hello latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="d328b-223">Pour plus d’informations, consultez [Contrôle du comportement de mise en cache du CDN Azure avec des chaînes de requête](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="d328b-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a><span data-ttu-id="d328b-224">Mapper un point de terminaison CDN tooa domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="d328b-224">Map a custom domain tooa CDN endpoint</span></span>

<span data-ttu-id="d328b-225">Vous allez mapper votre domaine personnalisé de tooyour point de terminaison CDN en créant un enregistrement CNAME.</span><span class="sxs-lookup"><span data-stu-id="d328b-225">You'll map your custom domain tooyour CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="d328b-226">Un enregistrement CNAME est une fonctionnalité DNS qui mappe un domaine de destination de tooa de domaine source.</span><span class="sxs-lookup"><span data-stu-id="d328b-226">A CNAME record is a DNS feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="d328b-227">Par exemple, vous pouvez mapper `cdn.contoso.com` ou `static.contoso.com` trop`contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="d328b-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` too`contoso.azureedge.net`.</span></span>

<span data-ttu-id="d328b-228">Si vous n’avez pas un domaine personnalisé, envisagez d’hello [didacticiel du domaine du Service d’applications](custom-dns-web-site-buydomains-web-app.md) toopurchase un domaine à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d328b-228">If you don't have a custom domain, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a><span data-ttu-id="d328b-229">Rechercher toouse de nom d’hôte hello avec hello CNAME</span><span class="sxs-lookup"><span data-stu-id="d328b-229">Find hello hostname toouse with hello CNAME</span></span>

<span data-ttu-id="d328b-230">Bonjour Azure portal **point de terminaison** , vérifiez que **vue d’ensemble** est sélectionné dans hello gauche de navigation, puis sélectionnez hello **+ un domaine personnalisé** bouton en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-230">In hello Azure portal **Endpoint** page, make sure **Overview** is selected in hello left navigation, and then select hello **+ Custom Domain** button at hello top of hello page.</span></span>

![Sélection de l’ajout d’un domaine personnalisé](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="d328b-232">Bonjour **ajouter un domaine personnalisé** page, vous voyez hello point de terminaison hôte nom toouse pour la création d’un enregistrement CNAME.</span><span class="sxs-lookup"><span data-stu-id="d328b-232">In hello **Add a custom domain** page, you see hello endpoint host name toouse in creating a CNAME record.</span></span> <span data-ttu-id="d328b-233">nom d’hôte Hello est dérivée de l’URL de point de terminaison CDN :  **&lt;EndpointName >. azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="d328b-233">hello host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Ajout d’une page de domaine](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a><span data-ttu-id="d328b-235">Configurer hello CNAME avec votre bureau d’enregistrement de domaine</span><span class="sxs-lookup"><span data-stu-id="d328b-235">Configure hello CNAME with your domain registrar</span></span>

<span data-ttu-id="d328b-236">Parcourir le site web de tooyour de domaines et recherchez la section hello pour la création d’enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="d328b-236">Navigate tooyour domain registrar's web site, and locate hello section for creating DNS records.</span></span> <span data-ttu-id="d328b-237">Vous pourrez trouver ces informations dans une section telle que **Domain Name**, **DNS** ou **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="d328b-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="d328b-238">Rechercher la section de hello pour la gestion des enregistrements CNAME.</span><span class="sxs-lookup"><span data-stu-id="d328b-238">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="d328b-239">Vous pouvez posséder de page de paramètres avancés de tooan toogo et recherchez les mots hello CNAME, Alias ou sous-domaines.</span><span class="sxs-lookup"><span data-stu-id="d328b-239">You may have toogo tooan advanced settings page and look for hello words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="d328b-240">Créer un enregistrement CNAME qui mappe votre sous-domaine choisi (par exemple, **statique** ou **cdn**) toohello **nom d’hôte de point de terminaison** indiqué plus haut dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) toohello **Endpoint host name** shown earlier in hello portal.</span></span> 

### <a name="enter-hello-custom-domain-in-azure"></a><span data-ttu-id="d328b-241">Entrez un domaine personnalisé de hello dans Azure</span><span class="sxs-lookup"><span data-stu-id="d328b-241">Enter hello custom domain in Azure</span></span>

<span data-ttu-id="d328b-242">Retourner toohello **ajouter un domaine personnalisé** page et entrez votre domaine personnalisé, y compris les sous-domaine hello, dans la boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-242">Return toohello **Add a custom domain** page, and enter your custom domain, including hello subdomain, in hello dialog box.</span></span> <span data-ttu-id="d328b-243">Par exemple, entrez : `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d328b-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="d328b-244">Azure vérifie que l’enregistrement CNAME de hello existe pour le nom de domaine hello que vous avez entré.</span><span class="sxs-lookup"><span data-stu-id="d328b-244">Azure verifies that hello CNAME record exists for hello domain name you have entered.</span></span> <span data-ttu-id="d328b-245">Si hello CNAME est correct, votre domaine personnalisé est validé.</span><span class="sxs-lookup"><span data-stu-id="d328b-245">If hello CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="d328b-246">Peut prendre du temps pour les serveurs de tooname toopropagate enregistrement hello CNAME sur hello Internet.</span><span class="sxs-lookup"><span data-stu-id="d328b-246">It can take time for hello CNAME record toopropagate tooname servers on hello Internet.</span></span> <span data-ttu-id="d328b-247">Si votre domaine n’est pas validé immédiatement, patientez quelques minutes, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="d328b-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-hello-custom-domain"></a><span data-ttu-id="d328b-248">Domaine personnalisé hello de test</span><span class="sxs-lookup"><span data-stu-id="d328b-248">Test hello custom domain</span></span>

<span data-ttu-id="d328b-249">Dans un navigateur, accédez à toohello `index.html` de fichiers à l’aide de votre domaine personnalisé (par exemple, `cdn.contoso.com/index.html`) tooverify qui en résulte hello hello même que lorsque vous accédez directement trop`<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="d328b-249">In a browser, navigate toohello `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) tooverify that hello result is hello same as when you go directly too`<endpointname>azureedge.net/index.html`.</span></span>

![Page d’accueil d’exemple d’application utilisant l’URL du domaine personnalisé](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="d328b-251">Pour plus d’informations, consultez [domaine personnalisé de carte Azure CDN contenu tooa](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d328b-251">For more information, see [Map Azure CDN content tooa custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="d328b-252">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d328b-252">Next steps</span></span>

<span data-ttu-id="d328b-253">Vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d328b-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d328b-254">Créer un point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d328b-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="d328b-255">Actualiser les ressources mises en cache.</span><span class="sxs-lookup"><span data-stu-id="d328b-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="d328b-256">Utiliser la requête des chaînes de versions de toocontrol mis en cache.</span><span class="sxs-lookup"><span data-stu-id="d328b-256">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="d328b-257">Utilisez un domaine personnalisé pour le point de terminaison CDN hello.</span><span class="sxs-lookup"><span data-stu-id="d328b-257">Use a custom domain for hello CDN endpoint.</span></span>

<span data-ttu-id="d328b-258">Découvrez comment les articles de performances du CDN toooptimize Bonjour suivant :</span><span class="sxs-lookup"><span data-stu-id="d328b-258">Learn how toooptimize CDN performance in hello following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d328b-259">Compression des fichiers dans Azure CDN pour améliorer les performances</span><span class="sxs-lookup"><span data-stu-id="d328b-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="d328b-260">Préchargement d’éléments multimédias sur un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="d328b-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
