---
title: "Intégration d’un service cloud Azure à Azure CDN | Microsoft Docs"
description: "Découvrez comment déployer un service cloud qui traite le contenu à partir d’un point de terminaison CDN Azure intégré"
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
ms.openlocfilehash: f2849fe25fd0d5b3dc26598ffba7591cb7433161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="d3a4d-103"><a name="intro"></a> Intégration d’un service cloud à Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="d3a4d-104">Vous pouvez intégrer un service cloud à Azure CDN pour distribuer du contenu à partir de l'emplacement du service cloud.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-104">A cloud service can be integrated with Azure CDN, serving any content from the cloud service's location.</span></span> <span data-ttu-id="d3a4d-105">Cette approche offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-105">This approach gives you the following advantages:</span></span>

* <span data-ttu-id="d3a4d-106">Facilité de déploiement et de mise à jour des images, scripts et feuilles de style dans les annuaires de projet du service cloud</span><span class="sxs-lookup"><span data-stu-id="d3a4d-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="d3a4d-107">Facilité de mise à niveau des packages NuGet dans votre service cloud (par exemple, les versions de jQuery ou de Bootstrap)</span><span class="sxs-lookup"><span data-stu-id="d3a4d-107">Easily upgrade the NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="d3a4d-108">Gestion de votre application web et de votre contenu CDN, le tout depuis la même interface Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3a4d-108">Manage your Web application and your CDN-served content all from the same Visual Studio interface</span></span>
* <span data-ttu-id="d3a4d-109">Flux de travail unifié pour le déploiement de votre application web et de votre contenu CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="d3a4d-110">Intégration du regroupement et de la minimisation d'ASP.NET avec Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d3a4d-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="d3a4d-111">What you will learn</span></span>
<span data-ttu-id="d3a4d-112">Ce didacticiel vous apprendra à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="d3a4d-113">Intégration d'un point de terminaison Azure CDN à votre service cloud et traitement du contenu statique dans vos pages Web depuis Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="d3a4d-114">Configuration des paramètres du cache pour le contenu statique de votre service cloud</span><span class="sxs-lookup"><span data-stu-id="d3a4d-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="d3a4d-115">Distribution du contenu à partir d'actions de contrôleur via Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="d3a4d-116">Traitement du contenu regroupé et minimisé via Azure CDN tout en préservant le débogage des scripts dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3a4d-116">Serve bundled and minified content through Azure CDN while preserving the script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="d3a4d-117">Configuration de secours de vos scripts et feuilles de style CSS quand votre service Azure CDN est hors connexion</span><span class="sxs-lookup"><span data-stu-id="d3a4d-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="d3a4d-118">Ce que vous allez créer</span><span class="sxs-lookup"><span data-stu-id="d3a4d-118">What you will build</span></span>
<span data-ttu-id="d3a4d-119">Vous allez déployer un rôle Web de service cloud en utilisant le modèle ASP.NET MVC par défaut, ajouter du code pour distribuer le contenu depuis un service Azure CDN intégré (ex. image, résultats de l'action d'un contrôleur, et fichiers JavaScript et CSS par défaut) et écrire du code pour configurer le mécanisme de secours des lots traités si le service CDN est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-119">You will deploy a cloud service Web role using the default ASP.NET MVC template, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="d3a4d-120">Éléments requis</span><span class="sxs-lookup"><span data-stu-id="d3a4d-120">What you will need</span></span>
<span data-ttu-id="d3a4d-121">Ce didacticiel nécessite les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-121">This tutorial has the following prerequisites:</span></span>

* <span data-ttu-id="d3a4d-122">Un [compte Microsoft Azure](/account/)</span><span class="sxs-lookup"><span data-stu-id="d3a4d-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="d3a4d-123">Visual Studio 2015 avec le [Kit SDK Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="d3a4d-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="d3a4d-124">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-124">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="d3a4d-125">Vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/) : vous obtenez alors des crédits dont vous pouvez vous servir pour tester les services Azure payants, et même lorsqu'ils sont épuisés, vous pouvez conserver le compte et utiliser les services Azure gratuits, notamment Sites Web.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="d3a4d-126">Vous pouvez [activer les avantages de l'abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) : votre abonnement MSDN vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="d3a4d-127">Déploiement d'un service cloud</span><span class="sxs-lookup"><span data-stu-id="d3a4d-127">Deploy a cloud service</span></span>
<span data-ttu-id="d3a4d-128">Dans cette section, vous allez déployer le modèle d'application ASP.NET MVC par défaut dans Visual Studio 2015 dans un rôle web de service cloud, puis l'intégrer à un nouveau point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-128">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to a cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="d3a4d-129">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-129">Follow the instructions below:</span></span>

1. <span data-ttu-id="d3a4d-130">Dans Visual Studio 2015, créez un service cloud Azure à partir de la barre de menus : **Fichier > Nouveau > Projet > Cloud > Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-130">In Visual Studio 2015, create a new Azure cloud service from the menu bar by going to **File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="d3a4d-131">Attribuez-lui un nom et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="d3a4d-132">Sélectionnez **Rôle Web ASP.NET** et cliquez sur le bouton **>**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-132">Select **ASP.NET Web Role** and click the **>** button.</span></span> <span data-ttu-id="d3a4d-133">Cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="d3a4d-134">Sélectionnez **MVC** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="d3a4d-135">Publiez ce rôle web dans un service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-135">Now, publish this Web role to an Azure cloud service.</span></span> <span data-ttu-id="d3a4d-136">Cliquez avec le bouton droit sur le projet de service cloud et sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-136">Right-click the cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="d3a4d-137">Si vous n’êtes pas encore connecté à Microsoft Azure, cliquez sur la liste déroulante **Ajouter un compte** et cliquez sur l’élément de menu **Ajouter un compte**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-137">If you have not yet signed into Microsoft Azure, click the **Add an account...** dropdown and click the **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="d3a4d-138">Dans la page de connexion, connectez-vous au compte Microsoft que vous avez utilisé pour activer votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-138">In the sign-in page, sign in with the Microsoft account you used to activate your Azure account.</span></span>
7. <span data-ttu-id="d3a4d-139">Une fois que vous êtes connecté, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="d3a4d-140">En supposant que vous n'avez pas créé de compte de service cloud ou de stockage, Visual Studio vous aide à créer les deux.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="d3a4d-141">Dans la boîte de dialogue **Créer un service cloud et un compte** , tapez le nom souhaité pour le service et sélectionnez la région souhaitée.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-141">In the **Create Cloud Service and Account** dialog, type the desired service name and select the desired region.</span></span> <span data-ttu-id="d3a4d-142">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="d3a4d-143">Dans la page des paramètres de publication, vérifiez la configuration et cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-143">In the publish settings page, verify the configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="d3a4d-144">La publication des services cloud prend beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-144">The publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="d3a4d-145">L'option Activer Web Deploy pour tous les rôles accélère notablement le débogage de votre service cloud en fournissant des mises à jour rapides (mais provisoires) à vos rôles web.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-145">The Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates to your Web roles.</span></span> <span data-ttu-id="d3a4d-146">Pour en savoir plus sur cette option, consultez la page [Publication d'un service cloud en utilisant les Outils Azure](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3a4d-146">For more information on this option, see [Publishing a Cloud Service using the Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="d3a4d-147">Quand le **Journal des activités Microsoft Azure** indique que la publication est **Terminée**, vous devez créer un point de terminaison CDN intégré à ce service cloud.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-147">When the **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="d3a4d-148">Si, après la publication, le service cloud déployé affiche un écran d'erreur, il est probable que le service cloud que vous avez déployé utilise un [système d'exploitation invité qui n'inclut pas .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="d3a4d-148">If, after publishing, the deployed cloud service displays an error screen, it's likely because the cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="d3a4d-149">Vous pouvez contourner ce problème en [déployant .NET 4.5.2 en tant que tâche de démarrage](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d3a4d-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="d3a4d-150">Créer un profil CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-150">Create a new CDN profile</span></span>
<span data-ttu-id="d3a4d-151">Un profil CDN est une collection de points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="d3a4d-152">Chaque profil contient un ou plusieurs points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="d3a4d-153">Vous pouvez utiliser plusieurs profils pour organiser vos points de terminaison CDN par domaine Internet, application web ou d'autres critères.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-153">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="d3a4d-154">Si vous disposez déjà d'un profil CDN que vous souhaitez utiliser pour ce didacticiel, passez à la section [Créer un point de terminaison CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="d3a4d-154">If you already have a CDN profile that you want to use for this tutorial, proceed to [Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="d3a4d-155">Créer un point de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="d3a4d-156">**Pour créer un point de terminaison CDN pour votre compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="d3a4d-156">**To create a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="d3a4d-157">Dans le [portail de gestion Azure](https://portal.azure.com), accédez à votre profil CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-157">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="d3a4d-158">Vous l'avez peut-être épinglé au tableau de bord à l'étape précédente.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-158">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="d3a4d-159">Dans le cas contraire, vous le trouverez en cliquant sur **Parcourir**, puis **Profils CDN** et en cliquant sur le profil auquel vous voulez ajouter le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="d3a4d-160">Le panneau du profil CDN s'affiche.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-160">The CDN profile blade appears.</span></span>
   
    ![Profil CDN][cdn-profile-settings]
2. <span data-ttu-id="d3a4d-162">Cliquez sur le bouton **Ajouter un point de terminaison** .</span><span class="sxs-lookup"><span data-stu-id="d3a4d-162">Click the **Add Endpoint** button.</span></span>
   
    ![Bouton Ajouter un point de terminaison][cdn-new-endpoint-button]
   
    <span data-ttu-id="d3a4d-164">Le panneau **Ajouter un point de terminaison** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-164">The **Add an endpoint** blade appears.</span></span>
   
    ![Panneau Ajouter un point de terminaison][cdn-add-endpoint]
3. <span data-ttu-id="d3a4d-166">Entrez un **nom** pour ce point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="d3a4d-167">Ce nom servira à accéder à vos ressources en cache au niveau du domaine `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-167">This name will be used to access your cached resources at the domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="d3a4d-168">Dans la liste déroulante **Type d'origine** , sélectionnez *Service cloud*.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-168">In the **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="d3a4d-169">Dans la liste déroulante **Nom d'hôte d'origine** , sélectionnez votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-169">In the **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="d3a4d-170">Conservez les valeurs par défaut pour le **chemin d’accès d’origine**, l’**en-tête de l’hôte d’origine** et le **port de protocole/origine**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-170">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="d3a4d-171">Vous devez spécifier au moins un protocole (HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="d3a4d-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="d3a4d-172">Cliquez sur le bouton **Ajouter** pour créer le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-172">Click the **Add** button to create the new endpoint.</span></span>
8. <span data-ttu-id="d3a4d-173">Une fois le point de terminaison créé, il s'affiche dans la liste des points de terminaison pour le profil.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-173">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="d3a4d-174">L’affichage sous forme de liste montre l’URL à utiliser pour accéder au contenu mis en cache et le domaine d’origine.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-174">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
   
    ![Point de terminaison CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="d3a4d-176">Le point de terminaison ne sera pas immédiatement disponible pour utilisation.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-176">The endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="d3a4d-177">La propagation de l'inscription à travers le réseau CDN peut prendre jusqu'à 90 minutes.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-177">It can take up to 90 minutes for the registration to propagate through the CDN network.</span></span> <span data-ttu-id="d3a4d-178">Les utilisateurs qui tentent d'utiliser immédiatement le nom de domaine CDN peuvent recevoir le code d'état 404 jusqu'à ce que le contenu soit disponible via le CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-178">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span></span>
   > 
   > 

## <a name="test-the-cdn-endpoint"></a><span data-ttu-id="d3a4d-179">Test du point de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-179">Test the CDN endpoint</span></span>
<span data-ttu-id="d3a4d-180">Quand l’état de la publication est **Terminé**, ouvrez une fenêtre de navigateur et accédez à l’adresse **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-180">When the publishing status is **Completed**, open a browser window and navigate to **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="d3a4d-181">Dans ma configuration, cette URL est la suivante :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="d3a4d-182">Elle correspond à l'URL d'origine suivante au niveau du point de terminaison CDN :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-182">Which corresponds to the following origin URL at the CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="d3a4d-183">Quand vous atteignez la page **http://*&lt;nom_CDN>*.azureedge.net/Content/bootstrap.css**, en fonction de votre navigateur, vous êtes invité à télécharger ou à ouvrir le fichier bootstrap.css provenant de votre application web publiée.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-183">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted to download or open the bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="d3a4d-184">De même, vous pouvez accéder à toute URL accessible publiquement à l’adresse **http://*&lt;nom_service>*.cloudapp.net/**, directement à partir de votre point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="d3a4d-185">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-185">For example:</span></span>

* <span data-ttu-id="d3a4d-186">un fichier .js à partir du chemin d'accès /Script ;</span><span class="sxs-lookup"><span data-stu-id="d3a4d-186">A .js file from the /Script path</span></span>
* <span data-ttu-id="d3a4d-187">un fichier de contenu à partir du chemin d'accès /Content ;</span><span class="sxs-lookup"><span data-stu-id="d3a4d-187">Any content file from the /Content path</span></span>
* <span data-ttu-id="d3a4d-188">un contrôleur/une action ;</span><span class="sxs-lookup"><span data-stu-id="d3a4d-188">Any controller/action</span></span>
* <span data-ttu-id="d3a4d-189">si la chaîne de requête est activée sur le point de terminaison CDN, une URL avec des chaînes de requête.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-189">If the query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="d3a4d-190">En effet, avec la configuration précédente, vous pouvez héberger l’ensemble du service cloud depuis **http://*&lt;cdnName>*.azureedge.net/**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-190">In fact, with the above configuration, you can host the entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**.</span></span> <span data-ttu-id="d3a4d-191">Si vous accédez à l’adresse **http://camservice.azureedge.net/** , vous obtenez le résultat de l’action à partir de Home/Index.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-191">If I navigate to **http://camservice.azureedge.net/**, I get the action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="d3a4d-192">Cependant, cela ne signifie pas que ce soit toujours une bonne idée de traiter l’ensemble du service cloud par l’intermédiaire d’Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-192">This does not mean, however, that it's always a good idea to serve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="d3a4d-193">Un CDN avec optimisation de la remise statique n’accélère pas forcément la distribution des ressources dynamiques qui ne sont pas censées être mises en cache, ou qui sont mises à jour très fréquemment, étant donné que le CDN doit extraire très souvent une nouvelle version de la ressource à partir du serveur d’origine.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-193">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant to be cached, or are updated very frequently, since the CDN must pull a new version of the asset from the Origin server very often.</span></span> <span data-ttu-id="d3a4d-194">Pour ce scénario, vous pouvez activer l’optimisation [Accélération de site dynamique](cdn-dynamic-site-acceleration.md) sur votre point de terminaison CDN, qui utilise diverses techniques pour accélérer la distribution des ressources dynamiques ne pouvant pas être mises en cache.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-194">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques to speed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="d3a4d-195">Si vous avez un site avec un mélange de contenu statique et dynamique, vous pouvez choisir de traiter votre contenu statique à partir de CDN avec un type d’optimisation statique (par exemple la livraison web générale) et de traiter le contenu dynamique directement à partir du serveur d’origine ou par le biais d’un point de terminaison CDN avec l’optimisation Accélération de site dynamique activée au cas par cas.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-195">If you have a site with a mix of static and dynamic content, you can choose to serve your static content from CDN with a static optimization type (such as general web delivery), and to serve dynamic content either directly from the origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="d3a4d-196">À cette fin, vous avez déjà vu comment accéder à des fichiers de contenu individuels depuis le point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-196">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="d3a4d-197">Je vais vous montrer comment traiter une action sur un contrôleur donné par le biais d’un point de terminaison CDN spécifique dans la section Distribution de contenu à partir d’actions de contrôleur via Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-197">I will show you how to serve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="d3a4d-198">La solution alternative consiste à déterminer au cas par cas le contenu à traiter à partir d'Azure CDN dans votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-198">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="d3a4d-199">À cette fin, vous avez déjà vu comment accéder à des fichiers de contenu individuels depuis le point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-199">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="d3a4d-200">Je vais vous montrer comment traiter une action sur un contrôleur donné via le point de terminaison CDN dans la section [Distribution de contenu à partir d'actions de contrôleur via Azure CDN](#controller).</span><span class="sxs-lookup"><span data-stu-id="d3a4d-200">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="d3a4d-201">Configuration des options de mise en cache des fichiers statiques dans votre service cloud</span><span class="sxs-lookup"><span data-stu-id="d3a4d-201">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="d3a4d-202">Avec l'intégration d'Azure CDN à votre service cloud, vous pouvez spécifier comment vous voulez que le contenu statique soit mis en cache dans le point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-202">With Azure CDN integration in your cloud service, you can specify how you want static content to be cached in the CDN endpoint.</span></span> <span data-ttu-id="d3a4d-203">Pour cela, ouvrez *Web.config* à partir de votre projet de rôle web (par exemple, WebRole1) et ajoutez un élément `<staticContent>` à `<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-203">To do this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element to `<system.webServer>`.</span></span> <span data-ttu-id="d3a4d-204">Le code XML ci-dessous configure l'expiration du cache dans 3 jours.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-204">The XML below configures the cache to expire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="d3a4d-205">Lorsque vous faites cela, tous les fichiers statiques de votre service cloud respectent la même règle dans le cache de votre CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-205">Once you do this, all static files in your cloud service will observe the same rule in your CDN cache.</span></span> <span data-ttu-id="d3a4d-206">Pour un contrôle plus granulaire des paramètres du cache, ajoutez un fichier *Web.config* dans un dossier et ajoutez-lui vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-206">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="d3a4d-207">Exemple : ajoutez un fichier *Web.config* au dossier *\Content* et remplacez son contenu par le code XML suivant :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-207">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="d3a4d-208">Ce paramètre entraîne la mise en cache de tous les fichiers statiques du dossier *\Content* pendant 15 jours.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-208">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span></span>

<span data-ttu-id="d3a4d-209">Pour en savoir plus sur la configuration de l’élément `<clientCache>`, consultez [Cache du client &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="d3a4d-209">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="d3a4d-210">Dans la rubrique [Distribution de contenu à partir d'actions de contrôleur via Azure CDN](#controller), je vais également vous montrer comment configurer les paramètres du cache pour les résultats de l'action du contrôleur dans le cache du CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-210">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in the CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="d3a4d-211">Distribution du contenu à partir d'actions de contrôleur via Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-211">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="d3a4d-212">Lorsque vous intégrez un rôle web de service cloud à Azure CDN, il est relativement facile de distribuer du contenu à partir d'actions de contrôleur via le réseau de distribution de contenu (CDN) Azure.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-212">When you integrate a cloud service Web role with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span></span> <span data-ttu-id="d3a4d-213">En dehors du traitement de votre service cloud directement par le biais d’Azure CDN (démontré ci-dessus), [Maarten Balliauw](https://twitter.com/maartenballiauw) vous démontre comment le faire avec le contrôleur MemeGenerator à la page [Reducing latency on the web with the Azure CDN (Réduction de la latence sur Internet avec le réseau de distribution de contenu (CDN) Azure)](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="d3a4d-213">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="d3a4d-214">Je reproduis simplement cette page ici.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-214">I will simply reproduce it here.</span></span>

<span data-ttu-id="d3a4d-215">Supposez que, dans votre service cloud, vous vouliez créer des idées culturelles basées sur une image de Chuck Norris jeune (photo de [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) ainsi :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-215">Suppose in your cloud service you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="d3a4d-216">Une simple action `Index` permet aux clients de spécifier les superlatifs dans l’image, puis de créer l’idée lorsqu’ils publient vers l’action.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-216">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span></span> <span data-ttu-id="d3a4d-217">Comme il s'agit de Chuck Norris, vous espérez que cette page devienne extrêmement populaire dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-217">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span></span> <span data-ttu-id="d3a4d-218">Cet exemple illustre bien la distribution de contenu semi-dynamique avec Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-218">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="d3a4d-219">Procédez comme ci-dessus pour configurer cette action de contrôleur :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-219">Follow the steps above to setup this controller action:</span></span>

1. <span data-ttu-id="d3a4d-220">Dans le dossier *\Controllers*, créez un fichier .cs nommé *MemeGeneratorController.cs* et remplacez son contenu par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-220">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span></span> <span data-ttu-id="d3a4d-221">N'oubliez pas de remplacer la partie en surbrillance par le nom de votre CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-221">Be sure to replace the highlighted portion with your CDN name.</span></span>  
   
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
   
                    if (Debugger.IsAttached) // Preserve the debug experience
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
2. <span data-ttu-id="d3a4d-222">Cliquez avec le bouton droit sur l’action `Index()` par défaut et sélectionnez **Ajouter une vue**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-222">Right-click in the default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="d3a4d-223">Acceptez les paramètres ci-dessous et cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-223">Accept the settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="d3a4d-224">Ouvrez le nouveau fichier *Views\MemeGenerator\Index.cshtml* et remplacez son contenu par le simple code HTML suivant pour envoyer les superlatifs :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-224">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="d3a4d-225">Republiez le service cloud et accédez à l’adresse **http://*&lt;nom_service>*.cloudapp.net/MemeGenerator/Index** dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-225">Publish the cloud service again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="d3a4d-226">Quand vous envoyez les valeurs du formulaire dans `/MemeGenerator/Index`, la méthode d’action `Index_Post` renvoie un lien vers la méthode d’action `Show` avec l’identificateur d’entrée respectif.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-226">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span></span> <span data-ttu-id="d3a4d-227">Quand vous cliquez sur ce lien, vous accédez au code suivant :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-227">When you click the link, you reach the following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve the debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="d3a4d-228">Si votre débogueur local est lié, vous effectuez un débogage normal avec une redirection locale.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-228">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span></span> <span data-ttu-id="d3a4d-229">S'il est exécuté dans le service cloud, il redirige vers :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-229">If it's running in the cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="d3a4d-230">Qui correspond à l'URL d'origine suivante au niveau de votre point de terminaison CDN :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-230">Which corresponds to the following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="d3a4d-231">Vous pouvez alors appliquer l’attribut `OutputCacheAttribute` à la méthode `Generate` pour spécifier la manière dont l’action doit être mise en cache, et qu’Azure CDN respectera.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-231">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="d3a4d-232">Le code ci-dessous spécifie 1 heure (3 600 secondes) pour l'expiration du cache.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-232">The code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="d3a4d-233">De même, vous pouvez distribuer le contenu de l'action d'un contrôleur dans votre service cloud via le réseau de distribution de contenu (CDN) Azure avec l'option de mise en cache voulue.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-233">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with the desired caching option.</span></span>

<span data-ttu-id="d3a4d-234">Dans la section suivante, je vais vous montrer comment distribuer les scripts et les feuilles de style CSS regroupés et minimisés via Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-234">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="d3a4d-235">Intégration du regroupement et de la minimisation d'ASP.NET avec Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-235">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="d3a4d-236">Les scripts et les feuilles de style CSS, qui ne changent pas fréquemment, sont les principaux candidats pour le cache Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-236">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span></span> <span data-ttu-id="d3a4d-237">La distribution de l'ensemble du rôle web via votre réseau de distribution de contenu (CDN) Azure est la manière la plus facile d'intégrer le regroupement et la minimisation à Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-237">Serving the entire Web role through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="d3a4d-238">Cependant, comme vous ne voudrez peut-être pas faire cela, je vais vous montrer comment le faire en conservant l'approche souhaitée par le développeur concernant le regroupement et la minimisation ASP.NET, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-238">However, as you may not want to do this, I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="d3a4d-239">Mode débogage puissant</span><span class="sxs-lookup"><span data-stu-id="d3a4d-239">Great debug mode experience</span></span>
* <span data-ttu-id="d3a4d-240">Facilité de déploiement</span><span class="sxs-lookup"><span data-stu-id="d3a4d-240">Streamlined deployment</span></span>
* <span data-ttu-id="d3a4d-241">Mises à jour immédiates à destination des clients lors des mises à niveau des versions des scripts et des feuilles de style CSS</span><span class="sxs-lookup"><span data-stu-id="d3a4d-241">Immediate updates to clients for script/CSS version upgrades</span></span>
* <span data-ttu-id="d3a4d-242">Mécanisme de secours en cas de défaillance de votre point de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-242">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="d3a4d-243">Modifications minimales du code</span><span class="sxs-lookup"><span data-stu-id="d3a4d-243">Minimize code modification</span></span>

<span data-ttu-id="d3a4d-244">Dans le projet **WebRole1** créé à l’étape [Intégration d’un point de terminaison Azure CDN à votre service cloud et traitement du contenu statique dans vos pages Web depuis Azure CDN](#deploy), ouvrez *App_Start\BundleConfig.cs* et observez les appels de la méthode `bundles.Add()`.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-244">In the **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="d3a4d-245">La première instruction `bundles.Add()` ajoute un regroupement de script dans le répertoire virtuel `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-245">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="d3a4d-246">Ouvrez ensuite le fichier *Views\Shared\_Layout.cshtml* pour voir comment la balise de regroupement de script est rendue.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-246">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span></span> <span data-ttu-id="d3a4d-247">Vous devez trouver la ligne de code Razor suivante :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-247">You should be able to find the following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="d3a4d-248">Quand ce code Razor est exécuté dans le rôle web Azure, il restitue une balise `<script>` pour le regroupement du script similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-248">When this Razor code is run in the Azure Web role, it will render a `<script>` tag for the script bundle similar to the following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="d3a4d-249">Cependant, quand il est exécuté dans Visual Studio en appuyant sur `F5`, il restitue individuellement chaque fichier de script dans le regroupement (dans le cas ci-dessus, un seul fichier de script se trouve dans le regroupement) :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-249">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="d3a4d-250">Cela permet de déboguer le code JavaScript dans votre environnement de développement tout en réduisant les connexions clientes simultanées (regroupement) et en améliorant les performances de téléchargement (minimisation) en production.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-250">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="d3a4d-251">Cette fonctionnalité est très intéressante à conserver avec l'intégration Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-251">It's a great feature to preserve with Azure CDN integration.</span></span> <span data-ttu-id="d3a4d-252">De plus, du fait que le regroupement restitué contient déjà une chaîne de version générée automatiquement, vous voudrez répliquer cette fonctionnalité de façon que, chaque fois que vous mettrez à jour votre version jQuery via NuGet, il sera possible de la mettre à jour côté client le plus rapidement possible.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-252">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so the whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span></span>

<span data-ttu-id="d3a4d-253">Procédez comme suit pour l'intégration du regroupement et de la minimisation ASP.NET à votre point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-253">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="d3a4d-254">De retour dans *App_Start\BundleConfig.cs*, modifiez les méthodes `bundles.Add()` pour utiliser un autre [constructeur de regroupement](http://msdn.microsoft.com/library/jj646464.aspx) qui spécifie une adresse CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-254">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="d3a4d-255">Pour cela, remplacez la définition de la méthode `RegisterBundles` par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-255">To do this, replace the `RegisterBundles` method definition with the following code:</span></span>  
   
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
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you're
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="d3a4d-256">N'oubliez pas de remplacer `<yourCDNName>` par le nom de votre réseau de distribution de contenu (CDN) Azure.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-256">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span></span>
   
    <span data-ttu-id="d3a4d-257">Exprimé simplement, vous configurez `bundles.UseCdn = true` et ajoutez une URL CDN correctement formatée à chaque regroupement.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-257">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span></span> <span data-ttu-id="d3a4d-258">Par exemple : le premier constructeur dans le code :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-258">For example, the first constructor in the code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="d3a4d-259">est identique à :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-259">is the same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="d3a4d-260">Ce constructeur indique au regroupement et à la minimisation ASP.NET de restituer des fichiers de script individuels lorsqu'ils sont débogués localement, mais d'utiliser l'adresse CDN spécifiée pour accéder au script en question.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-260">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span></span> <span data-ttu-id="d3a4d-261">Cependant, notez deux caractéristiques importantes avec cette URL CDN correctement formatée :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-261">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="d3a4d-262">L'origine de cette URL CDN est `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, qui est en vérité le répertoire virtuel du regroupement de script dans votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-262">The origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your cloud service.</span></span>
   * <span data-ttu-id="d3a4d-263">Comme vous utilisez un constructeur CDN, la balise du script CDN pour le regroupement ne contient plus la chaîne de caractères de la version automatiquement générée dans l'URL restituée.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-263">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span></span> <span data-ttu-id="d3a4d-264">Vous devez créer manuellement une chaîne de version unique à chaque modification du regroupement de script pour forcer une erreur dans le cache de votre réseau de distribution de contenu (CDN) Azure.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-264">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span></span> <span data-ttu-id="d3a4d-265">En même temps, cette chaîne de version unique doit rester constante tout au long du déploiement pour un accès maximal au cache de votre réseau de distribution de contenu (CDN) Azure après le déploiement du regroupement.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-265">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span></span>
   * <span data-ttu-id="d3a4d-266">La chaîne de requête v=<W.X.Y.Z> est extraite de *Properties\AssemblyInfo.cs* dans votre projet de rôle web.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-266">The query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="d3a4d-267">Vous pouvez avoir un flux de travail de déploiement qui inclut l'incrémentation de la version de l'assembly chaque fois que vous publiez dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-267">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span></span> <span data-ttu-id="d3a4d-268">Vous pouvez également modifier *Properties\AssemblyInfo.cs* dans votre projet pour incrémenter automatiquement la chaîne de caractères de la version à chaque génération en utilisant le caractère générique ’*’.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-268">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '*'.</span></span> <span data-ttu-id="d3a4d-269">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-269">For example:</span></span>
     
        <span data-ttu-id="d3a4d-270">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="d3a4d-270">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="d3a4d-271">Toute autre stratégie pour simplifier la génération d'une chaîne unique tout au long d'un déploiement fonctionne dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-271">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span></span>
2. <span data-ttu-id="d3a4d-272">Republiez le service cloud et accédez à la page d'accueil.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-272">Republish the cloud service and access the home page.</span></span>
3. <span data-ttu-id="d3a4d-273">Affichez le code HTML de la page.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-273">View the HTML code for the page.</span></span> <span data-ttu-id="d3a4d-274">Vous devez voir l'URL CDN restituée avec une chaîne de version unique chaque fois que vous republiez des modifications dans votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-274">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your cloud service.</span></span> <span data-ttu-id="d3a4d-275">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-275">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="d3a4d-276">Dans Visual Studio, tapez `F5`pour déboguer le service cloud.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-276">In Visual Studio, debug the cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="d3a4d-277">Affichez le code HTML de la page.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-277">View the HTML code for the page.</span></span> <span data-ttu-id="d3a4d-278">Vous voyez chaque fichier de script restitué individuellement de façon à effectuer un débogage cohérent dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-278">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
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

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="d3a4d-279">Mécanisme de secours pour les URL CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-279">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="d3a4d-280">Lorsque le point de terminaison de votre réseau de distribution de contenu (CDN) présente une défaillance pour quelque raison que ce soit, vous voulez que votre page web soit suffisamment bien conçue pour accéder à votre serveur web d'origine comme option de secours pour le chargement de JavaScript ou Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-280">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="d3a4d-281">C'est une chose de perdre des images sur votre site web à cause d'une indisponibilité CDN, c'en est une autre de perdre dans une page une fonctionnalité vitale fournie par vos scripts et vos feuilles de style.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-281">It's serious enough to lose images on your website due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="d3a4d-282">La classe [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) contient la propriété [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) qui vous permet de configurer le mécanisme de secours en cas de défaillance CDN.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-282">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span></span> <span data-ttu-id="d3a4d-283">Pour utiliser cette propriété, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-283">To use this property, follow the steps below:</span></span>

1. <span data-ttu-id="d3a4d-284">Dans votre projet de rôle web, ouvrez *App_Start\BundleConfig.cs*, où vous avez ajouté une URL CDN dans chaque [constructeur de regroupement](http://msdn.microsoft.com/library/jj646464.aspx), puis apportez les modifications en surbrillance pour ajouter un mécanisme de secours aux regroupements par défaut :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-284">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make the following highlighted changes to add fallback mechanism to the default bundles:</span></span>  
   
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
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
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
   
    <span data-ttu-id="d3a4d-285">Quand `CdnFallbackExpression` n’a pas la valeur null, le script est injecté dans le code HTML pour tester où le regroupement est correctement chargé et, dans le cas contraire, pour accéder au regroupement directement depuis le serveur web d’origine.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-285">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span></span> <span data-ttu-id="d3a4d-286">Cette propriété doit être configurée avec une expression JavaScript qui teste si le regroupement CDN correspondant est correctement chargé.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-286">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="d3a4d-287">L'expression nécessaire pour tester chaque regroupement est différente en fonction du contenu.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-287">The expression needed to test each bundle differs according to the content.</span></span> <span data-ttu-id="d3a4d-288">Pour les regroupements par défaut ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-288">For the default bundles above:</span></span>
   
   * <span data-ttu-id="d3a4d-289">`window.jquery` est défini dans jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="d3a4d-289">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="d3a4d-290">`$.validator` est défini dans jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="d3a4d-290">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="d3a4d-291">`window.Modernizr` est défini dans modernizer-{version}.js</span><span class="sxs-lookup"><span data-stu-id="d3a4d-291">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="d3a4d-292">`$.fn.modal` est défini dans bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="d3a4d-292">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="d3a4d-293">Vous aurez peut-être remarqué que je n’ai pas configuré CdnFallbackExpression pour le regroupement `~/Cointent/css` .</span><span class="sxs-lookup"><span data-stu-id="d3a4d-293">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span></span> <span data-ttu-id="d3a4d-294">Cela est dû au fait qu’un [bogue dans System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) injecte une balise `<script>` pour le fichier CSS de secours à la place de la balise attendue `<link>`.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-294">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span></span>
     
     <span data-ttu-id="d3a4d-295">Il existe néanmoins un bon [mécanisme de secours pour les styles](https://github.com/EmberConsultingGroup/StyleBundleFallback) proposé par [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="d3a4d-295">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="d3a4d-296">Pour utiliser cette solution pour le CSS, créez un fichier .cs dans le répertoire *App_Start*, en le nommant *StyleBundleExtensions.cs*, puis remplacez son contenu par du [code issu de GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="d3a4d-296">To use the workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="d3a4d-297">Dans *App_Start\StyleFundleExtensions.cs*, renommez l’espace de noms avec le nom de votre rôle web (par exemple, **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="d3a4d-297">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="d3a4d-298">Revenez à `App_Start\BundleConfig.cs` et remplacez la dernière instruction `bundles.Add` par le code suivant en surbrillance :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-298">Go back to `App_Start\BundleConfig.cs` and modify the last `bundles.Add` statement with the following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="d3a4d-299">Cette nouvelle méthode d'extension utilise la même idée pour injecter un script dans le code HTML afin de vérifier le DOM pour le nom de classe, le nom de règle et la valeur de règle correspondants dans le regroupement CSS. Elle rétablit le serveur web d'origine si elle ne trouve pas de correspondance.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-299">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span></span>
5. <span data-ttu-id="d3a4d-300">Republiez le service cloud et accédez à la page d'accueil.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-300">Publish the cloud service again and access the home page.</span></span>
6. <span data-ttu-id="d3a4d-301">Affichez le code HTML de la page.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-301">View the HTML code for the page.</span></span> <span data-ttu-id="d3a4d-302">Vous devez trouver des scripts injectés similaires à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-302">You should find injected scripts similar to the following:</span></span>    
   
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

    <span data-ttu-id="d3a4d-303">Notez que le script injecté pour le regroupement CSS contient toujours les éléments restants provenant de la propriété `CdnFallbackExpression` dans la ligne :</span><span class="sxs-lookup"><span data-stu-id="d3a4d-303">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="d3a4d-304">Mais, du fait que la première partie de l'expression || renvoie toujours la valeur true (dans la ligne juste au-dessus), la fonction document.write() ne s'exécute jamais.</span><span class="sxs-lookup"><span data-stu-id="d3a4d-304">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="d3a4d-305">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="d3a4d-305">More Information</span></span>
* [<span data-ttu-id="d3a4d-306">Vue d’ensemble du réseau de distribution de contenu (CDN) Azure</span><span class="sxs-lookup"><span data-stu-id="d3a4d-306">Overview of the Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="d3a4d-307">Utilisation d’Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d3a4d-307">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="d3a4d-308">Regroupement et minimisation d’ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3a4d-308">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
