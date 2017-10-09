---
title: aaaCreate une application Azure line-of-business avec authentification AD FS | Documents Microsoft
description: "Découvrez comment une application métier-dans Azure App Service s’authentifie auprès de toocreate local STS. Ce didacticiel cible AD FS comme hello STS local."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="c766c-104">Créer une application cœur de métier Azure avec authentification AD FS</span><span class="sxs-lookup"><span data-stu-id="c766c-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="c766c-105">Cet article vous explique comment toocreate un ASP.NET MVC line-of-business application [Azure App Service](../app-service/app-service-value-prop-what-is.md) à l’aide d’un site local [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) en tant que fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-105">This article shows you how toocreate an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as hello identity provider.</span></span> <span data-ttu-id="c766c-106">Ce scénario peut fonctionner lorsque vous voulez les applications line-of-business toocreate dans Azure App Service votre organisation nécessite Active toobe de données stockée sur site.</span><span class="sxs-lookup"><span data-stu-id="c766c-106">This scenario can work when you want toocreate line-of-business applications in Azure App Service but your organization requires directory data toobe stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="c766c-107">Pour une vue d’ensemble des options de l’authentification et l’autorisation d’enterprise différents pour le Service d’applications Azure hello, consultez [authentifier avec Active Directory locale dans votre application Azure](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="c766c-107">For an overview of hello different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="c766c-108">Ce que vous allez créer</span><span class="sxs-lookup"><span data-stu-id="c766c-108">What you will build</span></span>
<span data-ttu-id="c766c-109">Vous allez générer une application ASP.NET de base dans Azure App Service Web Apps avec hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="c766c-109">You will build a basic ASP.NET application in Azure App Service Web Apps with hello following features:</span></span>

* <span data-ttu-id="c766c-110">Authentification des utilisateurs auprès d’AD FS</span><span class="sxs-lookup"><span data-stu-id="c766c-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="c766c-111">Utilise `[Authorize]` utilisateurs tooauthorize pour différentes actions</span><span class="sxs-lookup"><span data-stu-id="c766c-111">Uses `[Authorize]` tooauthorize users for different actions</span></span>
* <span data-ttu-id="c766c-112">Configuration statique pour le débogage dans Visual Studio et de publication d’applications Web de Service tooApp (configurer qu’une seule fois, déboguer et publier à tout moment)</span><span class="sxs-lookup"><span data-stu-id="c766c-112">Static configuration for both debugging in Visual Studio and publishing tooApp Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="c766c-113">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="c766c-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="c766c-114">Vous devez hello suivant toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="c766c-114">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="c766c-115">Un site local déploiement AD FS (pour une procédure de bout en bout hello de laboratoire de test utilisé dans ce didacticiel, consultez [du laboratoire de Test : STS autonome avec AD FS dans une machine virtuelle Azure (pour le test)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="c766c-115">An on-premises AD FS deployment (for an end-to-end walkthrough of hello test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="c766c-116">Approbations de partie de confiance autorisations toocreate dans Gestion AD FS</span><span class="sxs-lookup"><span data-stu-id="c766c-116">Permissions toocreate relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="c766c-117">Visual Studio 2013 Update 4 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="c766c-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="c766c-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="c766c-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="c766c-119">Utiliser l’exemple d’application pour le modèle métier</span><span class="sxs-lookup"><span data-stu-id="c766c-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="c766c-120">Hello exemple d’application dans ce didacticiel, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), est créé par l’équipe d’Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-120">hello sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by hello Azure Active Directory team.</span></span> <span data-ttu-id="c766c-121">Étant donné que AD FS prend en charge WS-Federation, vous pouvez l’utiliser comme un toocreate modèles d’applications line-of-business en toute simplicité.</span><span class="sxs-lookup"><span data-stu-id="c766c-121">Since AD FS supports WS-Federation, you can use it as a template toocreate line-of-business applications with ease.</span></span> <span data-ttu-id="c766c-122">Il a hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="c766c-122">It has hello following features:</span></span>

* <span data-ttu-id="c766c-123">Utilise [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate avec un site local déploiement AD FS</span><span class="sxs-lookup"><span data-stu-id="c766c-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="c766c-124">Fonctionnalités de connexion et de déconnexion</span><span class="sxs-lookup"><span data-stu-id="c766c-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="c766c-125">Utilise [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (au lieu de Windows Identity Foundation), qui est hello ultérieure d’ASP.NET et tooset beaucoup plus simple pour l’authentification et d’autorisation à WIF</span><span class="sxs-lookup"><span data-stu-id="c766c-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is hello future of ASP.NET and much simpler tooset up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a><span data-ttu-id="c766c-126">Installer l’application d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="c766c-126">Set up hello sample application</span></span>
1. <span data-ttu-id="c766c-127">Cloner ou télécharger l’exemple de solution hello à [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) répertoire local de tooyour.</span><span class="sxs-lookup"><span data-stu-id="c766c-127">Clone or download hello sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c766c-128">Hello les instructions de la section [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) vous montrent comment tooset application hello avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c766c-128">hello instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how tooset up hello application with Azure Active Directory.</span></span> <span data-ttu-id="c766c-129">Mais dans ce didacticiel, vous configurer avec AD FS, par conséquent, suivez les étapes de hello ici à la place.</span><span class="sxs-lookup"><span data-stu-id="c766c-129">But in this tutorial, you set it up with AD FS, so follow hello steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="c766c-130">Ouvrez la solution de hello, puis ouvrez Controllers\AccountController.cs Bonjour **l’Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="c766c-130">Open hello solution, and then open Controllers\AccountController.cs in hello **Solution Explorer**.</span></span>
   
   <span data-ttu-id="c766c-131">Vous verrez que les code hello émet simplement un authentification stimulation tooauthenticate hello utilisateur à l’aide de WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="c766c-131">You will see that hello code simply issues an authentication challenge tooauthenticate hello user using WS-Federation.</span></span> <span data-ttu-id="c766c-132">Toute l’authentification est configurée dans App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="c766c-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="c766c-133">Ouvrez App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="c766c-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="c766c-134">Bonjour `ConfigureAuth` (méthode), ligne de hello Remarque :</span><span class="sxs-lookup"><span data-stu-id="c766c-134">In hello `ConfigureAuth` method, note hello line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="c766c-135">Dans le monde OWIN hello, cet extrait de code est réellement hello strict que minimum, vous devez le tooconfigure l’authentification WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="c766c-135">In hello OWIN world, this snippet is really hello bare minimum you need tooconfigure WS-Federation authentication.</span></span> <span data-ttu-id="c766c-136">Il est beaucoup plus simple et plus élégante à WIF, où Web.config est injecté avec XML partout dans l’emplacement de hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over hello place.</span></span> <span data-ttu-id="c766c-137">Hello uniquement les informations dont vous avez besoin sont hello partie de confiance (RP) identificateur et hello l’URL du fichier de métadonnées de votre service AD FS.</span><span class="sxs-lookup"><span data-stu-id="c766c-137">hello only information you need is hello relying party's (RP) identifier and hello URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="c766c-138">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="c766c-138">Here's an example:</span></span>
   
   * <span data-ttu-id="c766c-139">Identificateur de la partie de confiance : `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="c766c-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="c766c-140">Adresse des métadonnées : `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="c766c-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="c766c-141">Dans App_Start\Startup.Auth.cs, modifiez hello suivant des définitions de type chaîne statique :</span><span class="sxs-lookup"><span data-stu-id="c766c-141">In App_Start\Startup.Auth.cs, change hello following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="c766c-142">Maintenant, modifiez hello correspondant dans le fichier Web.config. Ouvrez hello Web.config et modifier hello suivant les paramètres de l’application :</span><span class="sxs-lookup"><span data-stu-id="c766c-142">Now, make hello corresponding changes in Web.config. Open hello Web.config and modify hello following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="c766c-143">Renseignez les valeurs de clé hello en fonction de votre environnement respectif.</span><span class="sxs-lookup"><span data-stu-id="c766c-143">Fill in hello key values based on your respective environment.</span></span>
6. <span data-ttu-id="c766c-144">Toomake d’application hello qu’il n’y a aucune erreur de build.</span><span class="sxs-lookup"><span data-stu-id="c766c-144">Build hello application toomake sure there are no errors.</span></span>

<span data-ttu-id="c766c-145">Vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="c766c-145">That's it.</span></span> <span data-ttu-id="c766c-146">Exemple d’application hello est à présent prêt toowork avec AD FS.</span><span class="sxs-lookup"><span data-stu-id="c766c-146">Now hello sample application is ready toowork with AD FS.</span></span> <span data-ttu-id="c766c-147">Vous devez toujours tooconfigure une approbation de partie de confiance avec cette application dans AD FS plus tard.</span><span class="sxs-lookup"><span data-stu-id="c766c-147">You still need tooconfigure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a><span data-ttu-id="c766c-148">Déployer hello exemple application tooAzure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="c766c-148">Deploy hello sample application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="c766c-149">Ici, vous publiez hello application tooa l’application web dans les applications Web App Service tout en conservant les environnement de débogage hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-149">Here, you publish hello application tooa web app in App Service Web Apps while preserving hello debug environment.</span></span> <span data-ttu-id="c766c-150">Notez que vous prévoyez d’application de hello toopublish avant qu’il ait une relation d’approbation RP avec AD FS, donc l’authentification ne fonctionne toujours pas encore.</span><span class="sxs-lookup"><span data-stu-id="c766c-150">Note that you're going toopublish hello application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="c766c-151">Toutefois, si vous le faites maintenant vous pouvez avoir URL de l’application web hello que vous pouvez utiliser d’approbation de partie de confiance tooconfigure hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="c766c-151">However, if you do it now you can have hello web app URL that you can use tooconfigure hello RP trust later.</span></span>

1. <span data-ttu-id="c766c-152">Cliquez avec le bouton droit sur votre projet et sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="c766c-152">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="c766c-153">Cliquez sur **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="c766c-153">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="c766c-154">Si vous n’avez pas encore connecté tooAzure, cliquez sur **connexion** et utiliser un compte Microsoft de hello pour toosign de votre abonnement Azure dans.</span><span class="sxs-lookup"><span data-stu-id="c766c-154">If you haven't signed in tooAzure, click **Sign In** and use hello Microsoft account for your Azure subscription toosign in.</span></span>
4. <span data-ttu-id="c766c-155">Une fois connecté, cliquez sur **nouveau** toocreate une application web.</span><span class="sxs-lookup"><span data-stu-id="c766c-155">Once signed in, click **New** toocreate a web app.</span></span>
5. <span data-ttu-id="c766c-156">Renseignez tous les champs obligatoires.</span><span class="sxs-lookup"><span data-stu-id="c766c-156">Fill in all required fields.</span></span> <span data-ttu-id="c766c-157">Vous allez tooconnect tooon locale, les données plus tard, donc vous ne pouvez pas créer une base de données pour cette application web.</span><span class="sxs-lookup"><span data-stu-id="c766c-157">You are going tooconnect tooon-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="c766c-158">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c766c-158">Click **Create**.</span></span> <span data-ttu-id="c766c-159">Une fois l’application hello web est créée, la boîte de dialogue Publier le site Web hello est ouvert.</span><span class="sxs-lookup"><span data-stu-id="c766c-159">Once hello web app is created, hello Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="c766c-160">Dans **URL de Destination**, modifiez **http** trop**https**.</span><span class="sxs-lookup"><span data-stu-id="c766c-160">In **Destination URL**, change **http** too**https**.</span></span> <span data-ttu-id="c766c-161">Copiez hello entière URL tooa éditeur de texte pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c766c-161">Copy hello entire URL tooa text editor for later use.</span></span> <span data-ttu-id="c766c-162">Cliquez ensuite sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="c766c-162">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="c766c-163">Dans Visual Studio, ouvrez **Web.Release.config** dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="c766c-163">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="c766c-164">Insérer hello XML suivant dans hello `<configuration>` balise et remplacez la valeur de clé hello avec l’URL de l’application web de votre publication.</span><span class="sxs-lookup"><span data-stu-id="c766c-164">Insert hello following XML into hello `<configuration>` tag, and replace hello key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="c766c-165">Lorsque vous avez terminé, vous avez deux identificateurs RP configurés dans votre projet, une pour votre environnement de débogage dans Visual Studio, et l’autre pour hello publié l’application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c766c-165">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for hello published web app in Azure.</span></span> <span data-ttu-id="c766c-166">Vous allez configurer une approbation de partie de confiance pour chacun des deux environnements de hello dans AD FS.</span><span class="sxs-lookup"><span data-stu-id="c766c-166">You will set up an RP trust for each of hello two environments in AD FS.</span></span> <span data-ttu-id="c766c-167">Pendant le débogage, les paramètres dans le fichier Web.config de l’application hello sont toomake utilisé votre **déboguer** travail de configuration avec AD FS.</span><span class="sxs-lookup"><span data-stu-id="c766c-167">During debugging, hello app settings in Web.config are used toomake your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="c766c-168">Lorsqu’elle est publiée (par défaut, hello **version** configuration est publiée), un fichier Web.config transformé qui intègre les modifications du paramètre d’application hello dans Web.Release.config téléchargé.</span><span class="sxs-lookup"><span data-stu-id="c766c-168">When it's published (by default, hello **Release** configuration is published), a transformed Web.config is uploaded that incorporates hello app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="c766c-169">Si vous souhaitez l’application web publiée de hello tooattach dans Azure toohello débogueur (autrement dit, vous devez télécharger les symboles de débogage de votre code dans l’application web publiée de hello), vous pouvez créer un clone de hello déboguer la configuration de débogage Azure, mais avec son propre fichier Web.config personnalisé transformer) par exemple, Web.AzureDebug.config) qui utilise les paramètres de l’application à partir de Web.Release.config hello. Ainsi, vous toomaintain une configuration statique dans différents environnements de hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-169">If you want tooattach hello published web app in Azure toohello debugger (i.e. you must upload debug symbols of your code in hello published web app), you can create a clone of hello Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses hello app settings from Web.Release.config. This allows you toomaintain a static configuration across hello different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="c766c-170">Configuration d’approbations de partie de confiance dans Gestion AD FS</span><span class="sxs-lookup"><span data-stu-id="c766c-170">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="c766c-171">Vous devez maintenant tooconfigure une approbation de partie de confiance dans Gestion AD FS avant de pouvoir utiliser votre exemple d’application et en fait s’authentifier avec AD FS.</span><span class="sxs-lookup"><span data-stu-id="c766c-171">Now you need tooconfigure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="c766c-172">Vous devez tooset les deux approbations de partie de confiance distinctes, une pour votre environnement de débogage et un pour votre application web publiée.</span><span class="sxs-lookup"><span data-stu-id="c766c-172">You will need tooset up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="c766c-173">Assurez-vous que vous répétez hello comme suit pour les deux de vos environnements.</span><span class="sxs-lookup"><span data-stu-id="c766c-173">Make sure that you repeat hello following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="c766c-174">Sur votre serveur AD FS, connectez-vous avec les informations d’identification disposant des droits de gestion tooAD FS.</span><span class="sxs-lookup"><span data-stu-id="c766c-174">On your AD FS server, log in with credentials that have management rights tooAD FS.</span></span>
2. <span data-ttu-id="c766c-175">Ouvrez Gestion AD FS.</span><span class="sxs-lookup"><span data-stu-id="c766c-175">Open AD FS Management.</span></span> <span data-ttu-id="c766c-176">Cliquez avec le bouton droit sur **AD FS\Relations de confiance\Approbations de partie de confiance** et sélectionnez **Ajouter une approbation de partie de confiance**.</span><span class="sxs-lookup"><span data-stu-id="c766c-176">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="c766c-177">Bonjour **sélectionner une Source de données** , sélectionnez **entrer manuellement les données sur la partie de confiance hello**.</span><span class="sxs-lookup"><span data-stu-id="c766c-177">In hello **Select Data Source** page, select **Enter data about hello relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="c766c-178">Bonjour **indiquer le nom complet** page, tapez un nom complet pour l’application hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="c766c-178">In hello **Specify Display Name** page, type a display name for hello application and click **Next**.</span></span>
5. <span data-ttu-id="c766c-179">Bonjour **choisissez un protocole** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="c766c-179">In hello **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="c766c-180">Bonjour **configurer le certificat** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="c766c-180">In hello **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c766c-181">Étant donné que vous utilisez déjà HTTPS, les jetons chiffrés sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="c766c-181">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="c766c-182">Si vous voulez vraiment tooencrypt des jetons à partir d’AD FS sur cette page, vous devez également ajouter la logique de déchiffrement de jeton dans votre code.</span><span class="sxs-lookup"><span data-stu-id="c766c-182">If you really want tooencrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="c766c-183">Pour plus d’informations, consultez la page [Configuration manuelle de l’intergiciel (middleware) OWIN WS-Federation et acceptation des jetons chiffrés](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="c766c-183">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="c766c-184">Avant de passer à l’étape suivante de hello, vous devez une information de votre projet Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c766c-184">Before you move onto hello next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="c766c-185">Dans Propriétés du projet hello, notez hello **URL SSL** de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-185">In hello project properties, note hello **SSL URL** of hello application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="c766c-186">Dans Gestion AD FS, Bonjour **configurer l’URL** page Hello **Assistant Ajouter une partie confiance**, sélectionnez **activer la prise en charge de protocole WS-Federation passif de hello** et tapez Bonjour URL SSL de votre projet Visual Studio que vous avez noté à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-186">Back in AD FS Management, in hello **Configure URL** page of hello **Add Relying Party Trust Wizard**, select **Enable support for hello WS-Federation Passive protocol** and type in hello SSL URL of your Visual Studio project that you noted in hello previous step.</span></span> <span data-ttu-id="c766c-187">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c766c-187">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="c766c-188">URL spécifie où le client de hello toosend après l’authentification réussit.</span><span class="sxs-lookup"><span data-stu-id="c766c-188">URL specifies where toosend hello client after authentication succeeds.</span></span> <span data-ttu-id="c766c-189">Pour un environnement de débogage hello, il doit être <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="c766c-189">For hello debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="c766c-190">Pour l’application web publiée de hello, elle doit être hello URL de l’application web.</span><span class="sxs-lookup"><span data-stu-id="c766c-190">For hello published web app, it should be hello web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="c766c-191">Bonjour **configurer les identificateurs** page, vérifiez que votre projet URL SSL est déjà répertorié, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="c766c-191">In hello **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="c766c-192">Cliquez sur **suivant** tous hello fin toohello de moyen de l’Assistant hello avec les sélections par défaut.</span><span class="sxs-lookup"><span data-stu-id="c766c-192">Click **Next** all hello way toohello end of hello wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c766c-193">Dans App_Start\Startup.Auth.cs de votre projet Visual Studio, cet identificateur est mis en correspondance par rapport à la valeur hello <code>WsFederationAuthenticationOptions.Wtrealm</code> lors de l’authentification fédérée.</span><span class="sxs-lookup"><span data-stu-id="c766c-193">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against hello value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="c766c-194">Par défaut, les URL de l’application hello à partir de l’étape précédente de hello est ajouté comme un identificateur de partie de confiance.</span><span class="sxs-lookup"><span data-stu-id="c766c-194">By default, hello application's URL from hello previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="c766c-195">Vous avez terminé de configurer hello application de partie de confiance pour votre projet dans AD FS.</span><span class="sxs-lookup"><span data-stu-id="c766c-195">You have now finished configuring hello RP application for your project in AD FS.</span></span> <span data-ttu-id="c766c-196">Ensuite, vous configurez ce toosend application hello revendications requises par votre application.</span><span class="sxs-lookup"><span data-stu-id="c766c-196">Next, you configure this application toosend hello claims needed by your application.</span></span> <span data-ttu-id="c766c-197">Hello **modifier les règles de revendication** boîte de dialogue est ouverte par défaut pour vous à fin hello d’Assistant de hello afin que vous pouvez démarrer immédiatement.</span><span class="sxs-lookup"><span data-stu-id="c766c-197">hello **Edit Claim Rules** dialog is opened by default for you at hello end of hello wizard so you can start immediately.</span></span> <span data-ttu-id="c766c-198">Permet de configurer au moins hello après les revendications (avec les schémas entre parenthèses) :</span><span class="sxs-lookup"><span data-stu-id="c766c-198">Let's configure at least hello following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="c766c-199">Nom (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - utilisé par ASP.NET toohydrate `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="c766c-199">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET toohydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="c766c-200">Utilisateur nom principal (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - utilisé toouniquely identifier les utilisateurs de l’organisation de hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-200">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used toouniquely identify users in hello organization.</span></span>
    * <span data-ttu-id="c766c-201">Appartenances aux groupes en tant que rôles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - peut être utilisé avec `[Authorize(Roles="role1, role2,...")]` décoration tooauthorize contrôleurs/actions.</span><span class="sxs-lookup"><span data-stu-id="c766c-201">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize controllers/actions.</span></span> <span data-ttu-id="c766c-202">En réalité, cette approche ne peut pas être hello plus performantes pour l’autorisation de rôle.</span><span class="sxs-lookup"><span data-stu-id="c766c-202">In reality, this approach may not be hello most performant for role authorization.</span></span> <span data-ttu-id="c766c-203">Si vos utilisateurs AD appartiennent toohundreds des groupes de sécurité, ils deviennent des centaines de revendications de rôle dans le jeton SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-203">If your AD users belong toohundreds of security groups, they become hundreds of role claims in hello SAML token.</span></span> <span data-ttu-id="c766c-204">Une autre approche consiste à toosend un seul rôle de revendication conditionnellement en fonction de l’appartenance de l’utilisateur hello dans un groupe particulier.</span><span class="sxs-lookup"><span data-stu-id="c766c-204">An alternative approach is toosend a single role claim conditionally depending on hello user's membership in a particular group.</span></span> <span data-ttu-id="c766c-205">Toutefois, pour ce didacticiel, nous allons procéder plus simplement.</span><span class="sxs-lookup"><span data-stu-id="c766c-205">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="c766c-206">ID de nom (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - peut être utilisé pour la validation anti-contrefaçon.</span><span class="sxs-lookup"><span data-stu-id="c766c-206">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="c766c-207">Pour plus d’informations sur la façon dont toomake il anti-contrefaçon validation, consultez hello **ajouter des fonctionnalités métier-** section de [créer une application Azure line-of-business avec authentification Azure Active Directory ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="c766c-207">For more information on how toomake it work with anti-forgery validation, see hello **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c766c-208">Hello revendication types que vous avez besoin de tooconfigure pour votre application est déterminée par les besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="c766c-208">hello claim types you need tooconfigure for your application is determined by your application's needs.</span></span> <span data-ttu-id="c766c-209">Pour la liste hello de revendications pris en charge par les applications Azure Active Directory (autrement dit, des approbations de partie de confiance), par exemple, consultez [prise en charge du jeton et Types de revendications](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="c766c-209">For hello list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="c766c-210">Dans la boîte de dialogue Modifier les règles de revendication hello, cliquez sur **ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="c766c-210">In hello Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="c766c-211">Configurer des revendications de nom UPN et rôle hello comme indiqué dans la capture d’écran de hello et cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="c766c-211">Configure hello name, UPN, and role claims as shown in hello screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="c766c-212">Ensuite, créez un nom temporaire ID de revendication à l’aide des étapes de hello illustrées dans [les identificateurs de nom dans les assertions SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="c766c-212">Next, you create a transient name ID claim using hello steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="c766c-213">Cliquez de nouveau sur **Ajouter une règle** .</span><span class="sxs-lookup"><span data-stu-id="c766c-213">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="c766c-214">Sélectionnez **Envoyer les revendications en utilisant une règle personnalisée**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c766c-214">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="c766c-215">Langage de règle suivante hello de coller dans hello **règle personnalisée** zone, une règle de hello nom **par l’identificateur de Session** et cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="c766c-215">Paste hello following rule language into hello **Custom rule** box, name hello rule **Per Session Identifier** and click **Finish**.</span></span>  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    <span data-ttu-id="c766c-216">Votre règle personnalisée doit ressembler à cette capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="c766c-216">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="c766c-217">Cliquez de nouveau sur **Ajouter une règle** .</span><span class="sxs-lookup"><span data-stu-id="c766c-217">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="c766c-218">Sélectionnez **Transformer une revendication entrante** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c766c-218">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="c766c-219">Configurer la règle de hello comme indiqué dans la capture d’écran hello (à l’aide du type de revendication hello vous avez créé dans une règle personnalisée de hello) et cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="c766c-219">Configure hello rule as shown in hello screenshot (using hello claim type you created in hello custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="c766c-220">Pour plus d’informations sur les étapes de hello pour la revendication de nom ID hello temporaire, consultez [les identificateurs de nom dans les assertions SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="c766c-220">For detailed information on hello steps for hello transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="c766c-221">Cliquez sur **appliquer** Bonjour **modifier les règles de revendication** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c766c-221">Click **Apply** in hello **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="c766c-222">Il doit maintenant ressembler à hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="c766c-222">It should now look like hello following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="c766c-223">Là encore, assurez-vous que vous répétez ces étapes pour votre environnement de débogage et l’application web publiée.</span><span class="sxs-lookup"><span data-stu-id="c766c-223">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="c766c-224">Tester l’authentification fédérée pour votre application</span><span class="sxs-lookup"><span data-stu-id="c766c-224">Test federated authentication for your application</span></span>
<span data-ttu-id="c766c-225">Vous est tootest prêt logique d’authentification de votre application par rapport à ADFS.</span><span class="sxs-lookup"><span data-stu-id="c766c-225">You are ready tootest your application's authentication logic against AD FS.</span></span> <span data-ttu-id="c766c-226">Dans mon environnement de laboratoire AD FS, j’ai un utilisateur de test auquel appartient le groupe de test tooa dans Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="c766c-226">In my AD FS lab environment, I have a test user that belongs tooa test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="c766c-227">authentification tootest dans le débogueur hello, il vous suffit de toodo maintenant est de type `F5`.</span><span class="sxs-lookup"><span data-stu-id="c766c-227">tootest authentication in hello debugger, all you need toodo now is type `F5`.</span></span> <span data-ttu-id="c766c-228">Si vous souhaitez que l’authentification de tootest dans l’application web publiée de hello, accédez toohello URL.</span><span class="sxs-lookup"><span data-stu-id="c766c-228">If you want tootest authentication in hello published web app, navigate toohello URL.</span></span>

<span data-ttu-id="c766c-229">Une fois le charge de l’application web de hello, cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="c766c-229">After hello web application loads, click **Sign In**.</span></span> <span data-ttu-id="c766c-230">Soit une boîte de dialogue ou hello login page de connexion pris en charge par AD FS, en fonction de la méthode d’authentification hello choisi par AD FS doit maintenant s’afficher.</span><span class="sxs-lookup"><span data-stu-id="c766c-230">You should now get either a login dialog or hello login page served by AD FS, depending on hello authentication method chosen by AD FS.</span></span> <span data-ttu-id="c766c-231">Voici ce que nous obtenons dans Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="c766c-231">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="c766c-232">Une fois que vous vous connectez avec un utilisateur de domaine hello AD du déploiement de hello AD FS, vous devez maintenant voir la page d’accueil de hello avec **Hello, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="c766c-232">Once you log in with a user in hello AD domain of hello AD FS deployment, you should now see hello homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="c766c-233">dans l’angle de hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-233">in hello corner.</span></span> <span data-ttu-id="c766c-234">Voici ce que nous obtenons.</span><span class="sxs-lookup"><span data-stu-id="c766c-234">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="c766c-235">Jusqu'à présent, vous avez réussi Bonjour suivant façons :</span><span class="sxs-lookup"><span data-stu-id="c766c-235">So far, you've succeeded in hello following ways:</span></span>

* <span data-ttu-id="c766c-236">Votre application a atteint l’AD FS et un identificateur de partie de confiance correspondant est trouvé dans la base de données AD FS de hello</span><span class="sxs-lookup"><span data-stu-id="c766c-236">Your application has successfully reached AD FS and a matching RP identifier is found in hello AD FS database</span></span>
* <span data-ttu-id="c766c-237">AD FS a été authentifié un utilisateur Active Directory et rediriger la page d’accueil de l’application toohello</span><span class="sxs-lookup"><span data-stu-id="c766c-237">AD FS has successfully authenticated an AD user and redirect you back toohello application's homepage</span></span>
* <span data-ttu-id="c766c-238">AD FS en tant que nom de hello envoyé avec succès de revendication (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, comme indiqué par le fait de hello cet utilisateur hello nom s’affiche dans l’angle de hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-238">AD FS as successfully sent hello name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, as indicated by hello fact that hello user name is displayed in hello corner.</span></span> 

<span data-ttu-id="c766c-239">Si la revendication de nom hello est manquante, vous auriez vu **Bonjour !**.</span><span class="sxs-lookup"><span data-stu-id="c766c-239">If hello name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="c766c-240">Si vous examinez Views\Shared\_LoginPartial.cshtml, vous trouvez qu’il utilise `User.Identity.Name` nom d’utilisateur toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-240">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` toodisplay hello user name.</span></span> <span data-ttu-id="c766c-241">Comme mentionné précédemment, si le nom de hello revendication Hello authentifié l’utilisateur n’est disponible dans le jeton SAML de hello, ASP.NET hydrates de cette propriété avec lui.</span><span class="sxs-lookup"><span data-stu-id="c766c-241">As mentioned previously, if hello name claim of hello authenticated user is available in hello SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="c766c-242">toosee que tous hello des revendications qui sont envoyés par AD FS, placez un point d’arrêt dans Controllers\HomeController.cs, Bonjour de méthode d’action Index.</span><span class="sxs-lookup"><span data-stu-id="c766c-242">toosee all hello claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in hello Index action method.</span></span> <span data-ttu-id="c766c-243">Une fois hello utilisateur est authentifié, inspecter hello `System.Security.Claims.Current.Claims` collection.</span><span class="sxs-lookup"><span data-stu-id="c766c-243">After hello user is authenticated, inspect hello `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="c766c-244">Autorisation des utilisateurs pour des contrôleurs ou des actions spécifiques</span><span class="sxs-lookup"><span data-stu-id="c766c-244">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="c766c-245">Étant donné que vous avez inclus les appartenances aux groupes en tant que revendications de rôle dans votre configuration d’approbation de partie de confiance, vous pouvez désormais les utiliser directement dans hello `[Authorize(Roles="...")]` décoration pour les contrôleurs et les actions.</span><span class="sxs-lookup"><span data-stu-id="c766c-245">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in hello `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="c766c-246">Dans une application métier-avec modèle de création-lire-mise à jour-suppression (CRUD) hello, vous pouvez autoriser des rôles spécifiques tooaccess chaque action.</span><span class="sxs-lookup"><span data-stu-id="c766c-246">In a line-of-business application with hello Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles tooaccess each action.</span></span> <span data-ttu-id="c766c-247">Pour l’instant, vous allez simplement essayer cette fonctionnalité sur le contrôleur Home existant de hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-247">For now, you will just try out this feature on hello existing Home controller.</span></span>

1. <span data-ttu-id="c766c-248">Ouvrez Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="c766c-248">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="c766c-249">Décorer hello `About` et `Contact` toohello similaire action méthodes suivante de code, à l’aide des appartenances de sécurité de l’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="c766c-249">Decorate hello `About` and `Contact` action methods similar toohello following code, using security group memberships that your authenticated user has.</span></span>  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    <span data-ttu-id="c766c-250">Étant donné que j’ai ajouté **utilisateur Test** trop**groupe Test** dans mon environnement de laboratoire AD FS, je vais utiliser d’autorisation de groupe Test tootest sur `About`.</span><span class="sxs-lookup"><span data-stu-id="c766c-250">Since I added **Test User** too**Test Group** in my AD FS lab environment, I'll use Test Group tootest authorization on `About`.</span></span> <span data-ttu-id="c766c-251">Pour `Contact`, de tester cas négatif de hello de **Admins du domaine**, toowhich **utilisateur de Test** n’appartient pas.</span><span class="sxs-lookup"><span data-stu-id="c766c-251">For `Contact`, I'll test hello negative case of **Domain Admins**, toowhich **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="c766c-252">Démarrez le débogueur de hello en tapant `F5` et connectez-vous, puis cliquez sur **sur**.</span><span class="sxs-lookup"><span data-stu-id="c766c-252">Start hello debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="c766c-253">Vous devriez maintenant afficher hello `~/About/Index` page avec succès, si votre utilisateur authentifié est autorisé pour cette action.</span><span class="sxs-lookup"><span data-stu-id="c766c-253">You should now be viewing hello `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="c766c-254">Maintenant, cliquez sur **Contact**, dans mon cas ne doivent pas autoriser **utilisateur Test** pour l’action de hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-254">Now click **Contact**, which in my case should not authorize **Test User** for hello action.</span></span> <span data-ttu-id="c766c-255">Toutefois, le navigateur de hello est redirigé tooAD FS, ce qui est finalement affiche ce message :</span><span class="sxs-lookup"><span data-stu-id="c766c-255">However, hello browser is redirected tooAD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="c766c-256">Si vous examinez cette erreur dans l’Observateur d’événements sur hello serveur AD FS, vous consultez le message d’exception :</span><span class="sxs-lookup"><span data-stu-id="c766c-256">If you investigate this error in Event Viewer on hello AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="c766c-257">Hello pour corriger cette erreur parce que par défaut, MVC retourne un 401 non autorisé lorsque les rôles d’un utilisateur ne sont pas autorisés.</span><span class="sxs-lookup"><span data-stu-id="c766c-257">hello reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="c766c-258">Cela déclenche un fournisseur d’identité de la réauthentification demande tooyour (AD FS).</span><span class="sxs-lookup"><span data-stu-id="c766c-258">This triggers a reauthentication request tooyour identity provider (AD FS).</span></span> <span data-ttu-id="c766c-259">Étant donné que hello utilisateur est déjà authentifié, AD FS retourne toohello même page, qui émet alors un autre 401, création d’une boucle de redirection.</span><span class="sxs-lookup"><span data-stu-id="c766c-259">Since hello user is already authenticated, AD FS returns toohello same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="c766c-260">Vous substituez d’AuthorizeAttribute `HandleUnauthorizedRequest` méthode avec une logique simple tooshow quelque chose qui soit parlante au lieu de la boucle de redirection hello poursuite de l’opération.</span><span class="sxs-lookup"><span data-stu-id="c766c-260">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic tooshow something that makes sense instead of continuing hello redirect loop.</span></span>
5. <span data-ttu-id="c766c-261">Créez un fichier de projet hello appelé AuthorizeAttribute.cs et hello Coller après le code dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="c766c-261">Create a file in hello project called AuthorizeAttribute.cs, and paste hello following code into it.</span></span>
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    <span data-ttu-id="c766c-262">Hello remplacer le code envoie un HTTP 403 (interdit) au lieu de HTTP 401 (non autorisé) dans les cas authentifiés mais non autorisés.</span><span class="sxs-lookup"><span data-stu-id="c766c-262">hello override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="c766c-263">Exécuter le débogueur hello avec `F5`.</span><span class="sxs-lookup"><span data-stu-id="c766c-263">Run hello debugger again with `F5`.</span></span> <span data-ttu-id="c766c-264">Lorsque vous cliquez sur **Contact** , un message d’erreur plus explicite s’affiche à présent :</span><span class="sxs-lookup"><span data-stu-id="c766c-264">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="c766c-265">Publiez de nouveau hello application tooAzure App Service Web Apps et tester le comportement de hello d’application en temps réel de hello.</span><span class="sxs-lookup"><span data-stu-id="c766c-265">Publish hello application tooAzure App Service Web Apps again, and test hello behavior of hello live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a><span data-ttu-id="c766c-266">Se connecter aux données local tooon</span><span class="sxs-lookup"><span data-stu-id="c766c-266">Connect tooon-premises data</span></span>
<span data-ttu-id="c766c-267">Une raison que vous souhaiteriez tooimplement votre application métier-avec AD FS au lieu d’Azure Active Directory est problèmes de conformité avec la conservation des données organisation désactivé en local.</span><span class="sxs-lookup"><span data-stu-id="c766c-267">A reason that you would want tooimplement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="c766c-268">Cela signifie également que votre application web dans Azure doive accéder aux bases de données locales, étant donné que vous n’êtes pas autorisé toouse [base de données SQL](/services/sql-database/) comme couche de données hello pour vos applications web.</span><span class="sxs-lookup"><span data-stu-id="c766c-268">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed toouse [SQL Database](/services/sql-database/) as hello data tier for your web apps.</span></span>

<span data-ttu-id="c766c-269">Azure App Service Web Apps prend en charge l’accès aux bases de données locales avec deux approches : [Connexions hybrides](../biztalk-services/integration-hybrid-connection-overview.md) et [Réseaux virtuels](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="c766c-269">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="c766c-270">Pour plus d’informations, consultez la rubrique [Utilisation de l’intégration VNET et des connexions hybrides avec Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="c766c-270">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="c766c-271">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c766c-271">Further resources</span></span>
* [<span data-ttu-id="c766c-272">Authentification avec Active Directory en local dans votre application Azure</span><span class="sxs-lookup"><span data-stu-id="c766c-272">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="c766c-273">Créer une application Azure cœur de métier avec authentification Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c766c-273">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="c766c-274">Utilisez hello Option d’authentification d’organisation locale (ADFS) avec ASP.NET dans Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c766c-274">Use hello On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="c766c-275">Migrer un tooKatana VS2013 projet Web à partir de WIF</span><span class="sxs-lookup"><span data-stu-id="c766c-275">Migrate a VS2013 Web Project From WIF tooKatana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="c766c-276">Vue d’ensemble des services AD FS</span><span class="sxs-lookup"><span data-stu-id="c766c-276">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="c766c-277">Spécification WS-Federation 1.1</span><span class="sxs-lookup"><span data-stu-id="c766c-277">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

