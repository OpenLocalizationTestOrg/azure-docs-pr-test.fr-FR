---
title: aaaIntegrate un service cloud Azure avec Azure CDN | Documents Microsoft
description: "Découvrez comment toodeploy un service cloud qui fait Office de contenu à partir d’un point de terminaison CDN Azure intégrée"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="62ad0-103"><a name="intro"></a> Intégration d’un service cloud à Azure CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="62ad0-104">Un service cloud peut être intégré à Azure CDN, servant le contenu de l’emplacement du service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-104">A cloud service can be integrated with Azure CDN, serving any content from hello cloud service's location.</span></span> <span data-ttu-id="62ad0-105">Cela donne approche vous hello suivants avantages :</span><span class="sxs-lookup"><span data-stu-id="62ad0-105">This approach gives you hello following advantages:</span></span>

* <span data-ttu-id="62ad0-106">Facilité de déploiement et de mise à jour des images, scripts et feuilles de style dans les annuaires de projet du service cloud</span><span class="sxs-lookup"><span data-stu-id="62ad0-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="62ad0-107">Mettre à niveau facilement les packages NuGet hello dans votre service cloud, tels que jQuery ou versions d’amorçage</span><span class="sxs-lookup"><span data-stu-id="62ad0-107">Easily upgrade hello NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="62ad0-108">Gérer votre application Web et votre CDN-pris en charge de contenu à partir d’hello même interface de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62ad0-108">Manage your Web application and your CDN-served content all from hello same Visual Studio interface</span></span>
* <span data-ttu-id="62ad0-109">Flux de travail unifié pour le déploiement de votre application web et de votre contenu CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="62ad0-110">Intégration du regroupement et de la minimisation d'ASP.NET avec Azure CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="62ad0-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="62ad0-111">What you will learn</span></span>
<span data-ttu-id="62ad0-112">Ce didacticiel vous apprendra à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="62ad0-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="62ad0-113">Intégration d'un point de terminaison Azure CDN à votre service cloud et traitement du contenu statique dans vos pages Web depuis Azure CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="62ad0-114">Configuration des paramètres du cache pour le contenu statique de votre service cloud</span><span class="sxs-lookup"><span data-stu-id="62ad0-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="62ad0-115">Distribution du contenu à partir d'actions de contrôleur via Azure CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="62ad0-116">Serve groupée et réduire le contenu via le CDN Azure tout en conservant le script hello débogage dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62ad0-116">Serve bundled and minified content through Azure CDN while preserving hello script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="62ad0-117">Configuration de secours de vos scripts et feuilles de style CSS quand votre service Azure CDN est hors connexion</span><span class="sxs-lookup"><span data-stu-id="62ad0-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="62ad0-118">Ce que vous allez créer</span><span class="sxs-lookup"><span data-stu-id="62ad0-118">What you will build</span></span>
<span data-ttu-id="62ad0-119">Vous déployez un rôle Web de service cloud à l’aide de la valeur par défaut de hello modèle ASP.NET MVC, ajouter du contenu de tooserve de code à partir d’un CDN Azure intégré, comme une image, les résultats d’action de contrôleur et les fichiers JavaScript et CSS par défaut hello et également écrire hello tooconfigure de code mécanisme de secours pour les groupes pris en charge dans les événements hello que hello CDN est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="62ad0-119">You will deploy a cloud service Web role using hello default ASP.NET MVC template, add code tooserve content from an integrated Azure CDN, such as an image, controller action results, and hello default JavaScript and CSS files, and also write code tooconfigure hello fallback mechanism for bundles served in hello event that hello CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="62ad0-120">Éléments requis</span><span class="sxs-lookup"><span data-stu-id="62ad0-120">What you will need</span></span>
<span data-ttu-id="62ad0-121">Ce didacticiel n’hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="62ad0-121">This tutorial has hello following prerequisites:</span></span>

* <span data-ttu-id="62ad0-122">Un [compte Microsoft Azure](/account/)</span><span class="sxs-lookup"><span data-stu-id="62ad0-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="62ad0-123">Visual Studio 2015 avec le [Kit SDK Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="62ad0-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="62ad0-124">Vous avez besoin une toocomplete compte Azure ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="62ad0-124">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="62ad0-125">Vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/) -vous obtenez des crédits vous pouvez utiliser tootry à payer des services Azure et même après qu’ils soient utilisés jusqu'à vous pouvez conserver le compte de hello et libérer de l’utilisation des services Azure, comme les sites Web.</span><span class="sxs-lookup"><span data-stu-id="62ad0-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="62ad0-126">Vous pouvez [activer les avantages de l'abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) : votre abonnement MSDN vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.</span><span class="sxs-lookup"><span data-stu-id="62ad0-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="62ad0-127">Déploiement d'un service cloud</span><span class="sxs-lookup"><span data-stu-id="62ad0-127">Deploy a cloud service</span></span>
<span data-ttu-id="62ad0-128">Dans cette section, vous déploie la valeur par défaut de hello modèle d’application ASP.NET MVC dans le rôle du service Web de Visual Studio 2015 tooa cloud et puis l’intégrer à un point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-128">In this section, you will deploy hello default ASP.NET MVC application template in Visual Studio 2015 tooa cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="62ad0-129">Suivez les instructions de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="62ad0-129">Follow hello instructions below:</span></span>

1. <span data-ttu-id="62ad0-130">Dans Visual Studio 2015, créez un nouveau service cloud Azure à partir de la barre de menus hello en accédant trop**fichier > Nouveau > projet > Cloud > Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="62ad0-130">In Visual Studio 2015, create a new Azure cloud service from hello menu bar by going too**File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="62ad0-131">Attribuez-lui un nom et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="62ad0-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="62ad0-132">Sélectionnez **rôle Web ASP.NET** et cliquez sur hello  **>**  bouton.</span><span class="sxs-lookup"><span data-stu-id="62ad0-132">Select **ASP.NET Web Role** and click hello **>** button.</span></span> <span data-ttu-id="62ad0-133">Cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="62ad0-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="62ad0-134">Sélectionnez **MVC** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="62ad0-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="62ad0-135">À présent, publier cette tooan de rôle Web service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="62ad0-135">Now, publish this Web role tooan Azure cloud service.</span></span> <span data-ttu-id="62ad0-136">Cliquez sur le projet de service cloud hello et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="62ad0-136">Right-click hello cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="62ad0-137">Si vous n’êtes pas encore inscrit dans Microsoft Azure, cliquez sur hello **ajouter un compte...**  hello de liste déroulante et cliquez sur **ajouter un compte** élément de menu.</span><span class="sxs-lookup"><span data-stu-id="62ad0-137">If you have not yet signed into Microsoft Azure, click hello **Add an account...** dropdown and click hello **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="62ad0-138">Dans la page de connexion hello, connectez-vous à hello compte Microsoft que vous avez utilisé tooactivate votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="62ad0-138">In hello sign-in page, sign in with hello Microsoft account you used tooactivate your Azure account.</span></span>
7. <span data-ttu-id="62ad0-139">Une fois que vous êtes connecté, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="62ad0-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="62ad0-140">En supposant que vous n'avez pas créé de compte de service cloud ou de stockage, Visual Studio vous aide à créer les deux.</span><span class="sxs-lookup"><span data-stu-id="62ad0-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="62ad0-141">Bonjour **créer un Service Cloud et compte** boîte de dialogue, nom de service désiré de type hello et la région souhaités hello select.</span><span class="sxs-lookup"><span data-stu-id="62ad0-141">In hello **Create Cloud Service and Account** dialog, type hello desired service name and select hello desired region.</span></span> <span data-ttu-id="62ad0-142">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="62ad0-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="62ad0-143">Bonjour une page de paramètres de publication, vérifiez la configuration de hello, cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="62ad0-143">In hello publish settings page, verify hello configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="62ad0-144">processus de publication Hello pour les services de cloud prend beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="62ad0-144">hello publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="62ad0-145">Hello activer Web Deploy pour l’option de tous les rôles peut rendre le débogage de votre service cloud beaucoup plus rapide en fournissant des mises à jour rapide (mais temporaire) tooyour rôles Web.</span><span class="sxs-lookup"><span data-stu-id="62ad0-145">hello Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates tooyour Web roles.</span></span> <span data-ttu-id="62ad0-146">Pour plus d’informations sur cette option, consultez [publication d’un Service Cloud à l’aide des outils d’Azure hello](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="62ad0-146">For more information on this option, see [Publishing a Cloud Service using hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="62ad0-147">Hello lorsque **journal des activités Microsoft Azure** indique que l’état de publication est **terminé**, vous allez créer un point de terminaison CDN est intégré à ce service cloud.</span><span class="sxs-lookup"><span data-stu-id="62ad0-147">When hello **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="62ad0-148">Si, après la publication, le service de cloud computing hello déployé affiche un écran d’erreur, il est probable que vous avez déployé le service cloud hello utilise un [invité du système d’exploitation qui n’inclut pas de .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="62ad0-148">If, after publishing, hello deployed cloud service displays an error screen, it's likely because hello cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="62ad0-149">Vous pouvez contourner ce problème en [déployant .NET 4.5.2 en tant que tâche de démarrage](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="62ad0-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="62ad0-150">Créer un profil CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-150">Create a new CDN profile</span></span>
<span data-ttu-id="62ad0-151">Un profil CDN est une collection de points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="62ad0-152">Chaque profil contient un ou plusieurs points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="62ad0-153">Vous souhaiterez peut-être toouse plusieurs profils tooorganize vos points de terminaison CDN par domaine internet, application web ou d’autres critères.</span><span class="sxs-lookup"><span data-stu-id="62ad0-153">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="62ad0-154">Si vous avez déjà un profil CDN que vous souhaitez toouse pour ce didacticiel, passez trop[créer un nouveau point de terminaison CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="62ad0-154">If you already have a CDN profile that you want toouse for this tutorial, proceed too[Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="62ad0-155">Créer un point de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="62ad0-156">**toocreate un nouveau point de terminaison CDN pour votre compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="62ad0-156">**toocreate a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="62ad0-157">Bonjour [portail de gestion Azure](https://portal.azure.com), accédez tooyour le profil CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-157">In hello [Azure Management Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="62ad0-158">Vous pouvez avoir épinglée toohello le tableau de bord à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-158">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="62ad0-159">Si vous ne vous le trouverez en cliquant sur **Parcourir**, puis **profils CDN**, et en cliquant sur le profil de hello vous prévoyez de tooadd votre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="62ad0-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="62ad0-160">Panneau de profil CDN Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="62ad0-160">hello CDN profile blade appears.</span></span>
   
    ![Profil CDN][cdn-profile-settings]
2. <span data-ttu-id="62ad0-162">Cliquez sur hello **ajouter le point de terminaison** bouton.</span><span class="sxs-lookup"><span data-stu-id="62ad0-162">Click hello **Add Endpoint** button.</span></span>
   
    ![Bouton Ajouter un point de terminaison][cdn-new-endpoint-button]
   
    <span data-ttu-id="62ad0-164">Hello **ajouter un point de terminaison** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="62ad0-164">hello **Add an endpoint** blade appears.</span></span>
   
    ![Panneau Ajouter un point de terminaison][cdn-add-endpoint]
3. <span data-ttu-id="62ad0-166">Entrez un **nom** pour ce point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="62ad0-167">Ce nom sera utilisé tooaccess vos ressources mises en cache au niveau du domaine de hello `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="62ad0-167">This name will be used tooaccess your cached resources at hello domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="62ad0-168">Bonjour **type d’origine** liste déroulante, sélectionnez *service de cloud computing*.</span><span class="sxs-lookup"><span data-stu-id="62ad0-168">In hello **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="62ad0-169">Bonjour **nom d’hôte d’origine** liste déroulante, sélectionnez votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="62ad0-169">In hello **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="62ad0-170">Laisser les valeurs par défaut hello pour **chemin d’origine**, **en-tête hôte d’origine**, et **port de protocole/origine**.</span><span class="sxs-lookup"><span data-stu-id="62ad0-170">Leave hello defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="62ad0-171">Vous devez spécifier au moins un protocole (HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="62ad0-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="62ad0-172">Cliquez sur hello **ajouter** bouton toocreate hello nouveau point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="62ad0-172">Click hello **Add** button toocreate hello new endpoint.</span></span>
8. <span data-ttu-id="62ad0-173">Une fois que le point de terminaison hello est créé, il apparaît dans une liste de points de terminaison pour le profil de hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-173">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="62ad0-174">Hello liste affiche hello URL toouse tooaccess mis en cache le contenu, ainsi que le domaine d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-174">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
   
    ![Point de terminaison CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="62ad0-176">point de terminaison Hello pas immédiatement sera disponible pour utilisation.</span><span class="sxs-lookup"><span data-stu-id="62ad0-176">hello endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="62ad0-177">Il peut prendre jusqu'à minutes too90 toopropagate d’inscription hello via réseau CDN de hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-177">It can take up too90 minutes for hello registration toopropagate through hello CDN network.</span></span> <span data-ttu-id="62ad0-178">Les utilisateurs qui essaient de nom de domaine CDN toouse hello immédiatement peuvent recevoir le code d’état 404 jusqu'à ce que le contenu hello est disponible via hello CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-178">Users who try toouse hello CDN domain name immediately may receive status code 404 until hello content is available via hello CDN.</span></span>
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="62ad0-179">Hello de test point de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-179">Test hello CDN endpoint</span></span>
<span data-ttu-id="62ad0-180">Lorsque l’état de publication de hello est **terminé**, ouvrez une fenêtre de navigateur et accédez trop**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="62ad0-180">When hello publishing status is **Completed**, open a browser window and navigate too**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="62ad0-181">Dans ma configuration, cette URL est la suivante :</span><span class="sxs-lookup"><span data-stu-id="62ad0-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="62ad0-182">Qui correspond à toohello suivant l’URL d’origine au point de terminaison CDN hello :</span><span class="sxs-lookup"><span data-stu-id="62ad0-182">Which corresponds toohello following origin URL at hello CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="62ad0-183">Lorsque vous accédez trop**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, en fonction de votre navigateur, vous serez toodownload demandée ou ouvrez hello bootstrap.css qui fournie à partir de votre application Web publiée.</span><span class="sxs-lookup"><span data-stu-id="62ad0-183">When you navigate too**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted toodownload or open hello bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="62ad0-184">De même, vous pouvez accéder à toute URL accessible publiquement à l’adresse **http://*&lt;nom_service>*.cloudapp.net/**, directement à partir de votre point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="62ad0-185">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="62ad0-185">For example:</span></span>

* <span data-ttu-id="62ad0-186">Un fichier .js à partir du chemin d’accès de hello /Script</span><span class="sxs-lookup"><span data-stu-id="62ad0-186">A .js file from hello /Script path</span></span>
* <span data-ttu-id="62ad0-187">N’importe quel fichier de contenu à partir de hello/Content chemin d’accès</span><span class="sxs-lookup"><span data-stu-id="62ad0-187">Any content file from hello /Content path</span></span>
* <span data-ttu-id="62ad0-188">un contrôleur/une action ;</span><span class="sxs-lookup"><span data-stu-id="62ad0-188">Any controller/action</span></span>
* <span data-ttu-id="62ad0-189">Si la chaîne de requête hello est activé au point de terminaison CDN, n’importe quelle URL avec des chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="62ad0-189">If hello query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="62ad0-190">En fait, avec hello au-dessus de configuration, vous pouvez héberger service cloud entière hello  **http://*&lt;cdnName >*.azureedge.net/**. Si vous accédez trop**http://camservice.azureedge.net/ **, je reçois résultat d’action hello de Home/Index.</span><span class="sxs-lookup"><span data-stu-id="62ad0-190">In fact, with hello above configuration, you can host hello entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**. If I navigate too**http://camservice.azureedge.net/**, I get hello action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="62ad0-191">Cela ne signifie pas, toutefois, qu’il s’agit toujours d’un tooserve conseillé un service cloud entière via le CDN Azure.</span><span class="sxs-lookup"><span data-stu-id="62ad0-191">This does not mean, however, that it's always a good idea tooserve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="62ad0-192">Un CDN avec optimisation de la remise statique ne pas nécessairement accélérer la remise de ressources dynamiques qui ne sont pas destinés toobe mis en cache ou sont mis à jour très fréquemment, étant donné que hello CDN doit extraire une nouvelle version de l’élément multimédia de hello à partir du serveur d’origine hello très souvent.</span><span class="sxs-lookup"><span data-stu-id="62ad0-192">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant toobe cached, or are updated very frequently, since hello CDN must pull a new version of hello asset from hello Origin server very often.</span></span> <span data-ttu-id="62ad0-193">Pour ce scénario, vous pouvez activer [accélération de Site dynamique](cdn-dynamic-site-acceleration.md) optimisation (DSA) sur votre point de terminaison CDN qui utilise différents toospeed techniques paramétrer la livraison de ressources dynamiques non mise en cache.</span><span class="sxs-lookup"><span data-stu-id="62ad0-193">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques toospeed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="62ad0-194">Si vous avez un site avec un mélange de contenu statique et dynamique, vous pouvez choisir tooserve votre contenu statique de distribution de contenu avec un type de l’optimisation statique (par exemple, la remise de web général) et le contenu dynamique tooserve directement à partir de serveur d’origine hello, ou via un réseau CDN point de terminaison avec l’optimisation de DSA activée sur un cas par cas.</span><span class="sxs-lookup"><span data-stu-id="62ad0-194">If you have a site with a mix of static and dynamic content, you can choose tooserve your static content from CDN with a static optimization type (such as general web delivery), and tooserve dynamic content either directly from hello origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="62ad0-195">fin de toothat, vous avez déjà vu comment tooaccess le contenu des fichiers à partir du point de terminaison CDN hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-195">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="62ad0-196">Je vous montrera comment tooserve une action de contrôleur spécifique via un point de terminaison CDN spécifique dans servir contenu à partir d’actions de contrôleur via le CDN Azure.</span><span class="sxs-lookup"><span data-stu-id="62ad0-196">I will show you how tooserve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="62ad0-197">Hello consiste toodetermine qui tooserve à partir d’Azure CDN sur un cas par cas dans votre service cloud de contenu.</span><span class="sxs-lookup"><span data-stu-id="62ad0-197">hello alternative is toodetermine which content tooserve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="62ad0-198">fin de toothat, vous avez déjà vu comment tooaccess le contenu des fichiers à partir du point de terminaison CDN hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-198">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="62ad0-199">Je vous montrera comment tooserve une action de contrôleur spécifique via hello point de terminaison CDN dans [traiter du contenu à partir d’actions de contrôleur via Azure CDN](#controller).</span><span class="sxs-lookup"><span data-stu-id="62ad0-199">I will show you how tooserve a specific controller action through hello CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="62ad0-200">Configuration des options de mise en cache des fichiers statiques dans votre service cloud</span><span class="sxs-lookup"><span data-stu-id="62ad0-200">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="62ad0-201">Avec l’intégration d’Azure CDN dans votre service cloud, vous pouvez spécifier comment vous souhaitez que statique toobe contenu mis en cache dans le point de terminaison CDN hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-201">With Azure CDN integration in your cloud service, you can specify how you want static content toobe cached in hello CDN endpoint.</span></span> <span data-ttu-id="62ad0-202">toodo, ouvrez *Web.config* à partir de votre rôle Web de projet (par exemple, WebRole1) et ajoutez un `<staticContent>` élément trop`<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="62ad0-202">toodo this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element too`<system.webServer>`.</span></span> <span data-ttu-id="62ad0-203">Hello XML ci-après configure hello cache tooexpire dans les 3 jours.</span><span class="sxs-lookup"><span data-stu-id="62ad0-203">hello XML below configures hello cache tooexpire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="62ad0-204">Une fois que vous faites cela, tous les fichiers statiques dans votre service cloud observera hello même règle dans le cache du CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-204">Once you do this, all static files in your cloud service will observe hello same rule in your CDN cache.</span></span> <span data-ttu-id="62ad0-205">Pour un contrôle plus granulaire des paramètres du cache, ajoutez un fichier *Web.config* dans un dossier et ajoutez-lui vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="62ad0-205">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="62ad0-206">Par exemple, ajouter un *Web.config* toohello de fichiers *\Content* dossier et remplacer hello contenu par hello XML suivant :</span><span class="sxs-lookup"><span data-stu-id="62ad0-206">For example, add a *Web.config* file toohello *\Content* folder and replace hello content with hello following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="62ad0-207">Avec ce paramètre, tous les fichiers statiques à partir de hello *\Content* toobe dossier mis en cache pendant 15 jours.</span><span class="sxs-lookup"><span data-stu-id="62ad0-207">This setting causes all static files from hello *\Content* folder toobe cached for 15 days.</span></span>

<span data-ttu-id="62ad0-208">Pour plus d’informations sur la façon de tooconfigure hello `<clientCache>` élément, consultez [cache du Client &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="62ad0-208">For more information on how tooconfigure hello `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="62ad0-209">Dans [traiter du contenu à partir d’actions de contrôleur via Azure CDN](#controller), je vous montrera également comment vous pouvez configurer les paramètres de cache pour les résultats d’action de contrôleur Bonjour cache du CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-209">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in hello CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="62ad0-210">Distribution du contenu à partir d'actions de contrôleur via Azure CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-210">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="62ad0-211">Lorsque vous intégrez un rôle Web de service cloud avec Azure CDN, il est relativement facile tooserve le contenu à partir d’actions de contrôleur via hello Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-211">When you integrate a cloud service Web role with Azure CDN, it is relatively easy tooserve content from controller actions through hello Azure CDN.</span></span> <span data-ttu-id="62ad0-212">Autre que desservant votre cloud service directement par le biais d’Azure CDN (illustré ci-dessus), [Maarten Balliauw](https://twitter.com/maartenballiauw) vous montre comment toodo avec un fun contrôleur MemeGenerator [ce qui réduit la latence sur le web hello avec hello CDN Azure ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="62ad0-212">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how toodo it with a fun MemeGenerator controller in [Reducing latency on hello web with hello Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="62ad0-213">Je reproduis simplement cette page ici.</span><span class="sxs-lookup"><span data-stu-id="62ad0-213">I will simply reproduce it here.</span></span>

<span data-ttu-id="62ad0-214">Supposons que votre service cloud, vous souhaitez memes toogenerate basée sur une image Chuck Norris jeune (photo par [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) comme suit :</span><span class="sxs-lookup"><span data-stu-id="62ad0-214">Suppose in your cloud service you want toogenerate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="62ad0-215">Vous avez un simple `Index` qui permet aux clients de hello superlatifs de hello toospecify dans l’image de hello, puis génère hello MIME une fois qu’ils publient toohello action.</span><span class="sxs-lookup"><span data-stu-id="62ad0-215">You have a simple `Index` action that allows hello customers toospecify hello superlatives in hello image, then generates hello meme once they post toohello action.</span></span> <span data-ttu-id="62ad0-216">Dans la mesure où il s’agit de Chuck Norris, vous vous attendez toobecome de cette page grandement populaires globalement.</span><span class="sxs-lookup"><span data-stu-id="62ad0-216">Since it's Chuck Norris, you would expect this page toobecome wildly popular globally.</span></span> <span data-ttu-id="62ad0-217">Cet exemple illustre bien la distribution de contenu semi-dynamique avec Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-217">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="62ad0-218">Suivez les étapes ci-dessus toosetup, hello cette action de contrôleur :</span><span class="sxs-lookup"><span data-stu-id="62ad0-218">Follow hello steps above toosetup this controller action:</span></span>

1. <span data-ttu-id="62ad0-219">Bonjour *\Controllers* dossier, créez un nouveau fichier .cs appelé *MemeGeneratorController.cs* et hello remplacer avec hello après le code.</span><span class="sxs-lookup"><span data-stu-id="62ad0-219">In hello *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace hello content with hello following code.</span></span> <span data-ttu-id="62ad0-220">Être vraiment partie en surbrillance tooreplace hello avec le nom de votre CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-220">Be sure tooreplace hello highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="62ad0-221">Avec le bouton droit dans la valeur par défaut hello `Index()` action et sélectionnez **ajouter une vue**.</span><span class="sxs-lookup"><span data-stu-id="62ad0-221">Right-click in hello default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="62ad0-222">Acceptez les paramètres hello ci-dessous et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="62ad0-222">Accept hello settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="62ad0-223">Ouvrez hello nouvelle *Views\MemeGenerator\Index.cshtml* et remplacez le contenu hello hello suivant HTML simple pour l’envoi de superlatifs de hello :</span><span class="sxs-lookup"><span data-stu-id="62ad0-223">Open hello new *Views\MemeGenerator\Index.cshtml* and replace hello content with hello following simple HTML for submitting hello superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="62ad0-224">Publiez de nouveau service de cloud computing hello et accédez trop**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="62ad0-224">Publish hello cloud service again and navigate too**http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="62ad0-225">Lorsque vous envoyez des valeurs de formulaire hello trop`/MemeGenerator/Index`, hello `Index_Post` méthode d’action renvoie un lien de toohello `Show` méthode d’action avec l’identificateur d’entrée de hello respectifs.</span><span class="sxs-lookup"><span data-stu-id="62ad0-225">When you submit hello form values too`/MemeGenerator/Index`, hello `Index_Post` action method returns a link toohello `Show` action method with hello respective input identifier.</span></span> <span data-ttu-id="62ad0-226">Lorsque vous cliquez sur le lien de hello, vous atteignez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="62ad0-226">When you click hello link, you reach hello following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="62ad0-227">Si votre débogueur local est connecté, vous obtiendrez expérience de débogage normal hello avec une redirection locale.</span><span class="sxs-lookup"><span data-stu-id="62ad0-227">If your local debugger is attached, then you will get hello regular debug experience with a local redirect.</span></span> <span data-ttu-id="62ad0-228">Si elle est en cours d’exécution dans le service cloud hello, elle sera rediriger vers :</span><span class="sxs-lookup"><span data-stu-id="62ad0-228">If it's running in hello cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="62ad0-229">Qui correspond à toohello suivant l’URL d’origine au point de terminaison CDN :</span><span class="sxs-lookup"><span data-stu-id="62ad0-229">Which corresponds toohello following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="62ad0-230">Vous pouvez ensuite utiliser hello `OutputCacheAttribute` attribut sur hello `Generate` toospecify méthode comment résultat d’action hello doit être mise en cache, qui respecte Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-230">You can then use hello `OutputCacheAttribute` attribute on hello `Generate` method toospecify how hello action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="62ad0-231">code Hello ci-dessous spécifient une expiration du cache de 1 heure (3 600 secondes).</span><span class="sxs-lookup"><span data-stu-id="62ad0-231">hello code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="62ad0-232">De même, vous pouvez traiter le contenu à partir d’une action de contrôleur dans votre service cloud via le CDN Azure, avec l’option de mise en cache hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="62ad0-232">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with hello desired caching option.</span></span>

<span data-ttu-id="62ad0-233">Dans la section suivante de hello, je vous indiquera comment tooserve hello groupée et réduire les scripts et CSS via le CDN Azure.</span><span class="sxs-lookup"><span data-stu-id="62ad0-233">In hello next section, I will show you how tooserve hello bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="62ad0-234">Intégration du regroupement et de la minimisation d'ASP.NET avec Azure CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-234">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="62ad0-235">Feuilles de style CSS et des scripts changent peu souvent et sont des candidats idéaux pour hello du cache du CDN Azure.</span><span class="sxs-lookup"><span data-stu-id="62ad0-235">Scripts and CSS stylesheets change infrequently and are prime candidates for hello Azure CDN cache.</span></span> <span data-ttu-id="62ad0-236">Service hello ensemble Web du rôle via le CDN Azure est toointegrate de façon plus simple de hello groupement et la minimisation avec Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-236">Serving hello entire Web role through your Azure CDN is hello easiest way toointegrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="62ad0-237">Toutefois, comme vous ne voulez pas toodo cela, je vous indiquera comment toodo qu’il tout en conservant hello souhaité expérience de programme de groupement d’ASP.NET et la minimisation, telles que :</span><span class="sxs-lookup"><span data-stu-id="62ad0-237">However, as you may not want toodo this, I will show you how toodo it while preserving hello desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="62ad0-238">Mode débogage puissant</span><span class="sxs-lookup"><span data-stu-id="62ad0-238">Great debug mode experience</span></span>
* <span data-ttu-id="62ad0-239">Facilité de déploiement</span><span class="sxs-lookup"><span data-stu-id="62ad0-239">Streamlined deployment</span></span>
* <span data-ttu-id="62ad0-240">Tooclients mises à jour immédiate des mises à niveau de version de script/CSS</span><span class="sxs-lookup"><span data-stu-id="62ad0-240">Immediate updates tooclients for script/CSS version upgrades</span></span>
* <span data-ttu-id="62ad0-241">Mécanisme de secours en cas de défaillance de votre point de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-241">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="62ad0-242">Modifications minimales du code</span><span class="sxs-lookup"><span data-stu-id="62ad0-242">Minimize code modification</span></span>

<span data-ttu-id="62ad0-243">Bonjour **WebRole1** projet que vous avez créé dans [intégrer un point de terminaison CDN Azure avec votre site Web Azure et du contenu statique dans vos pages Web à partir d’Azure CDN](#deploy), ouvrez *App_Start\ BundleConfig.cs* et examinez hello `bundles.Add()` les appels de méthode.</span><span class="sxs-lookup"><span data-stu-id="62ad0-243">In hello **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at hello `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="62ad0-244">Hello tout d’abord `bundles.Add()` instruction ajoute un regroupement de script au répertoire virtuel de hello `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="62ad0-244">hello first `bundles.Add()` statement adds a script bundle at hello virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="62ad0-245">Ensuite, ouvrez *Views\Shared\_Layout.cshtml* toosee la balise de regroupement de script hello est rendu.</span><span class="sxs-lookup"><span data-stu-id="62ad0-245">Then, open *Views\Shared\_Layout.cshtml* toosee how hello script bundle tag is rendered.</span></span> <span data-ttu-id="62ad0-246">Vous devez être hello toofind en mesure de la ligne de code Razor suivante :</span><span class="sxs-lookup"><span data-stu-id="62ad0-246">You should be able toofind hello following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="62ad0-247">Lorsque ce code Razor est exécuté dans le rôle Web Azure de hello, il affichera une `<script>` hello balise de script suivant toohello similaire de regroupement :</span><span class="sxs-lookup"><span data-stu-id="62ad0-247">When this Razor code is run in hello Azure Web role, it will render a `<script>` tag for hello script bundle similar toohello following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="62ad0-248">Toutefois, lors de son exécution dans Visual Studio en tapant `F5`, il doit rendre individuellement chaque fichier de script dans une offre groupée de hello (dans le cas de hello ci-dessus, uniquement un fichier de script est dans le groupe de hello) :</span><span class="sxs-lookup"><span data-stu-id="62ad0-248">However, when it is run in Visual Studio by typing `F5`, it will render each script file in hello bundle individually (in hello case above, only one script file is in hello bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="62ad0-249">Cela vous permet du code JavaScript dans votre environnement de développement toodebug hello lors de la réduction des connexions clientes simultanées (regroupement) et l’amélioration de fichier téléchargement performances (minimisation) en production.</span><span class="sxs-lookup"><span data-stu-id="62ad0-249">This enables you toodebug hello JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="62ad0-250">Il s’agit d’un toopreserve fonctionnalité intéressante avec intégration d’Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-250">It's a great feature toopreserve with Azure CDN integration.</span></span> <span data-ttu-id="62ad0-251">En outre, étant donné que le groupe de hello rendu contient déjà une chaîne de version généré automatiquement, vous souhaitez tooreplicate fonctionnalité hello par conséquent, lorsque vous mettez à jour votre version de jQuery via NuGet, il peut être mis à jour côté client de hello dès que possible.</span><span class="sxs-lookup"><span data-stu-id="62ad0-251">Furthermore, since hello rendered bundle already contains an automatically generated version string, you want tooreplicate that functionality so hello whenever you update your jQuery version through NuGet, it can be updated at hello client side as soon as possible.</span></span>

<span data-ttu-id="62ad0-252">Suivez les étapes de hello ci-dessous groupement de ASP.NET de toointegration et la minimisation avec votre point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-252">Follow hello steps below toointegration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="62ad0-253">Dans les *App_Start\BundleConfig.cs*, modifier hello `bundles.Add()` toouse méthodes une autre [constructeur d’offre groupée](http://msdn.microsoft.com/library/jj646464.aspx), qui spécifie une adresse CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-253">Back in *App_Start\BundleConfig.cs*, modify hello `bundles.Add()` methods toouse a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="62ad0-254">toodo, hello remplacer `RegisterBundles` définition de méthode par hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="62ad0-254">toodo this, replace hello `RegisterBundles` method definition with hello following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="62ad0-255">Être vraiment tooreplace `<yourCDNName>` nom hello de votre CDN Azure.</span><span class="sxs-lookup"><span data-stu-id="62ad0-255">Be sure tooreplace `<yourCDNName>` with hello name of your Azure CDN.</span></span>
   
    <span data-ttu-id="62ad0-256">Clairement, vous définissez `bundles.UseCdn = true` et ajouté un regroupement de tooeach URL du CDN élaborées avec soin.</span><span class="sxs-lookup"><span data-stu-id="62ad0-256">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL tooeach bundle.</span></span> <span data-ttu-id="62ad0-257">Par exemple, hello premier constructeur dans le code hello :</span><span class="sxs-lookup"><span data-stu-id="62ad0-257">For example, hello first constructor in hello code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="62ad0-258">est hello identique :</span><span class="sxs-lookup"><span data-stu-id="62ad0-258">is hello same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="62ad0-259">Ce constructeur indique à ASP.NET groupement et la minimisation toorender des fichiers de script individuels lors du débogage localement, mais utilisez hello spécifié CDN tooaccess hello un script adresses en question.</span><span class="sxs-lookup"><span data-stu-id="62ad0-259">This constructor tells ASP.NET bundling and minification toorender individual script files when debugged locally, but use hello specified CDN address tooaccess hello script in question.</span></span> <span data-ttu-id="62ad0-260">Cependant, notez deux caractéristiques importantes avec cette URL CDN correctement formatée :</span><span class="sxs-lookup"><span data-stu-id="62ad0-260">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="62ad0-261">l’origine de cette URL CDN Hello est `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, qui est réellement hello répertoire virtuel du regroupement de script hello dans votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="62ad0-261">hello origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually hello virtual directory of hello script bundle in your cloud service.</span></span>
   * <span data-ttu-id="62ad0-262">Étant donné que vous utilisez le constructeur CDN, hello balise de script CDN pour le regroupement de hello contient ne sont plus chaîne de version de hello généré automatiquement Bonjour rendu d’URL.</span><span class="sxs-lookup"><span data-stu-id="62ad0-262">Since you are using CDN constructor, hello CDN script tag for hello bundle no longer contains hello automatically generated version string in hello rendered URL.</span></span> <span data-ttu-id="62ad0-263">Vous devez générer manuellement une chaîne de version unique chaque fois que regroupement de script hello est modifié tooforce un cache manquent à votre Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-263">You must manually generate a unique version string every time hello script bundle is modified tooforce a cache miss at your Azure CDN.</span></span> <span data-ttu-id="62ad0-264">AT hello même temps, cette chaîne de version unique doit rester constante via vie hello hello déploiement toomaximize d’accès du cache à votre Azure CDN après le regroupement de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="62ad0-264">At hello same time, this unique version string must remain constant through hello life of hello deployment toomaximize cache hits at your Azure CDN after hello bundle is deployed.</span></span>
   * <span data-ttu-id="62ad0-265">chaîne de requête v de Hello = extrait < W.X.Y.Z > à partir de *Properties\AssemblyInfo.cs* dans votre projet de rôle Web.</span><span class="sxs-lookup"><span data-stu-id="62ad0-265">hello query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="62ad0-266">Vous pouvez avoir un flux de travail de déploiement qui inclut l’incrémentation de version de l’assembly hello chaque fois que vous publiez tooAzure.</span><span class="sxs-lookup"><span data-stu-id="62ad0-266">You can have a deployment workflow that includes incrementing hello assembly version every time you publish tooAzure.</span></span> <span data-ttu-id="62ad0-267">Ou bien, vous pouvez simplement modifier *Properties\AssemblyInfo.cs* dans votre chaîne de version de projet tooautomatically incrément hello chaque fois que vous générez, à l’aide de caractère générique de hello ' *'.</span><span class="sxs-lookup"><span data-stu-id="62ad0-267">Or, you can just modify *Properties\AssemblyInfo.cs* in your project tooautomatically increment hello version string every time you build, using hello wildcard character '*'.</span></span> <span data-ttu-id="62ad0-268">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="62ad0-268">For example:</span></span>
     
        <span data-ttu-id="62ad0-269">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="62ad0-269">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="62ad0-270">Toutes les autres toostreamline stratégie générant une chaîne unique pour la durée de vie hello d’un déploiement fonctionne ici.</span><span class="sxs-lookup"><span data-stu-id="62ad0-270">Any other strategy toostreamline generating a unique string for hello life of a deployment will work here.</span></span>
2. <span data-ttu-id="62ad0-271">Republier hello cloud service et l’accès hello page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="62ad0-271">Republish hello cloud service and access hello home page.</span></span>
3. <span data-ttu-id="62ad0-272">Hello vue code HTML de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-272">View hello HTML code for hello page.</span></span> <span data-ttu-id="62ad0-273">Vous devez être en mesure de toosee hello URL du CDN rendu, avec une chaîne de version unique chaque fois que vous republiez le service de cloud de tooyour de modifications.</span><span class="sxs-lookup"><span data-stu-id="62ad0-273">You should be able toosee hello CDN URL rendered, with a unique version string every time you republish changes tooyour cloud service.</span></span> <span data-ttu-id="62ad0-274">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="62ad0-274">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="62ad0-275">Dans Visual Studio, déboguer le service de cloud computing hello dans Visual Studio en tapant `F5`.,</span><span class="sxs-lookup"><span data-stu-id="62ad0-275">In Visual Studio, debug hello cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="62ad0-276">Hello vue code HTML de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-276">View hello HTML code for hello page.</span></span> <span data-ttu-id="62ad0-277">Vous voyez chaque fichier de script restitué individuellement de façon à effectuer un débogage cohérent dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="62ad0-277">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="62ad0-278">Mécanisme de secours pour les URL CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-278">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="62ad0-279">Lorsque votre point de terminaison CDN Azure échoue pour une raison quelconque, vous souhaitez que votre toobe page Web actives suffisamment tooaccess votre serveur Web d’origine comme solution de secours hello pour charger JavaScript ou amorçage.</span><span class="sxs-lookup"><span data-stu-id="62ad0-279">When your Azure CDN endpoint fails for any reason, you want your Web page toobe smart enough tooaccess your origin Web server as hello fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="62ad0-280">Il est suffisamment graves toolose des images sur votre site Web en raison de tooCDN indisponibilité, mais beaucoup plus grave fonctionnalité de page cruciale toolose fournie par vos scripts et les feuilles de style.</span><span class="sxs-lookup"><span data-stu-id="62ad0-280">It's serious enough toolose images on your website due tooCDN unavailability, but much more severe toolose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="62ad0-281">Hello [groupe](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) classe contient une propriété appelée [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) qui vous permet de mécanisme de secours hello tooconfigure de l’échec CDN.</span><span class="sxs-lookup"><span data-stu-id="62ad0-281">hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you tooconfigure hello fallback mechanism for CDN failure.</span></span> <span data-ttu-id="62ad0-282">toouse cette propriété, hello suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="62ad0-282">toouse this property, follow hello steps below:</span></span>

1. <span data-ttu-id="62ad0-283">Dans votre projet de rôle Web, ouvrez *App_Start\BundleConfig.cs*, où vous avez ajouté une URL du CDN dans chaque [constructeur d’offre groupée](http://msdn.microsoft.com/library/jj646464.aspx)et suit hello mis en surbrillance change tooadd mécanisme de secours toohello lots de la valeur par défaut :</span><span class="sxs-lookup"><span data-stu-id="62ad0-283">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make hello following highlighted changes tooadd fallback mechanism toohello default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="62ad0-284">Lorsque `CdnFallbackExpression` est non null, script injecter hello HTML tootest si l’offre groupée de hello est chargée avec succès et dans le cas contraire, accéder hello regroupement directement à partir de serveur Web d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-284">When `CdnFallbackExpression` is not null, script is injected into hello HTML tootest whether hello bundle is loaded successfully and, if not, access hello bundle directly from hello origin Web server.</span></span> <span data-ttu-id="62ad0-285">Cette propriété doit toobe ensemble expression tooa JavaScript qui teste si l’offre groupée de hello respectif CDN est chargée correctement.</span><span class="sxs-lookup"><span data-stu-id="62ad0-285">This property needs toobe set tooa JavaScript expression that tests whether hello respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="62ad0-286">expression de Hello requise tootest chaque lot diffère en fonction toohello contenu.</span><span class="sxs-lookup"><span data-stu-id="62ad0-286">hello expression needed tootest each bundle differs according toohello content.</span></span> <span data-ttu-id="62ad0-287">Pour les offres de valeur par défaut hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="62ad0-287">For hello default bundles above:</span></span>
   
   * <span data-ttu-id="62ad0-288">`window.jquery` est défini dans jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="62ad0-288">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="62ad0-289">`$.validator` est défini dans jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="62ad0-289">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="62ad0-290">`window.Modernizr` est défini dans modernizer-{version}.js</span><span class="sxs-lookup"><span data-stu-id="62ad0-290">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="62ad0-291">`$.fn.modal` est défini dans bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="62ad0-291">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="62ad0-292">Vous avez peut-être remarqué que vous n’avez pas défini CdnFallbackExpression pour hello `~/Cointent/css` offre groupée.</span><span class="sxs-lookup"><span data-stu-id="62ad0-292">You might have noticed that I did not set CdnFallbackExpression for hello `~/Cointent/css` bundle.</span></span> <span data-ttu-id="62ad0-293">Il s’agit, car il n’y a un [bogue dans System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) qui injecte un `<script>` balise pour hello attendu de secours CSS au lieu de hello `<link>` balise.</span><span class="sxs-lookup"><span data-stu-id="62ad0-293">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for hello fallback CSS instead of hello expected `<link>` tag.</span></span>
     
     <span data-ttu-id="62ad0-294">Il existe néanmoins un bon [mécanisme de secours pour les styles](https://github.com/EmberConsultingGroup/StyleBundleFallback) proposé par [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="62ad0-294">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="62ad0-295">solution de contournement toouse hello pour CSS, créer un nouveau fichier .cs dans votre projet de rôle Web *App_Start* dossier appelé *StyleBundleExtensions.cs*et remplacez son contenu hello [à partir de code GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="62ad0-295">toouse hello workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with hello [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="62ad0-296">Dans *App_Start\StyleFundleExtensions.cs*, renommez le nom du rôle Web hello espace de noms tooyour (par exemple, **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="62ad0-296">In *App_Start\StyleFundleExtensions.cs*, rename hello namespace tooyour Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="62ad0-297">Revenir en arrière trop`App_Start\BundleConfig.cs` et modifier hello dernière `bundles.Add` instruction avec hello suivant le code en surbrillance :</span><span class="sxs-lookup"><span data-stu-id="62ad0-297">Go back too`App_Start\BundleConfig.cs` and modify hello last `bundles.Add` statement with hello following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="62ad0-298">Cette nouvelle méthode d’extension utilise hello même idée tooinject script hello HTML toocheck hello DOM pourquoi un nom de classe correspondant, nom de la règle et valeur de la règle définie dans hello CSS lot et se situe toohello précédent serveur Web d’origine en cas d’échec de correspondance de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="62ad0-298">This new extension method uses hello same idea tooinject script in hello HTML toocheck hello DOM for hello a matching class name, rule name, and rule value defined in hello CSS bundle, and falls back toohello origin Web server if it fails toofind hello match.</span></span>
5. <span data-ttu-id="62ad0-299">Publier à nouveau le service cloud hello et la page d’accueil access hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-299">Publish hello cloud service again and access hello home page.</span></span>
6. <span data-ttu-id="62ad0-300">Hello vue code HTML de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="62ad0-300">View hello HTML code for hello page.</span></span> <span data-ttu-id="62ad0-301">Vous devez rechercher les scripts injecté similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="62ad0-301">You should find injected scripts similar toohello following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="62ad0-302">Notez que script injecté hello CSS regroupement contient encore restante exempte de malintentionné hello de hello `CdnFallbackExpression` propriété dans la ligne de hello :</span><span class="sxs-lookup"><span data-stu-id="62ad0-302">Note that injected script for hello CSS bundle still contains hello errant remnant from hello `CdnFallbackExpression` property in hello line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="62ad0-303">Mais depuis la première partie de hello Hello || expression retourne toujours true (sur ligne hello directement au-dessus), la fonction de hello document.Write () ne sera jamais exécuté.</span><span class="sxs-lookup"><span data-stu-id="62ad0-303">But since hello first part of hello || expression will always return true (in hello line directly above that), hello document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="62ad0-304">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="62ad0-304">More Information</span></span>
* [<span data-ttu-id="62ad0-305">Vue d’ensemble de hello réseau de distribution contenu (CDN) Azure</span><span class="sxs-lookup"><span data-stu-id="62ad0-305">Overview of hello Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="62ad0-306">Utilisation d’Azure CDN</span><span class="sxs-lookup"><span data-stu-id="62ad0-306">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="62ad0-307">Regroupement et minimisation d’ASP.NET</span><span class="sxs-lookup"><span data-stu-id="62ad0-307">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
