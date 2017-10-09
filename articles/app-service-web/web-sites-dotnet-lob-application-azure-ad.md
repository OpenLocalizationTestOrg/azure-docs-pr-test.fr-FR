---
title: aaaCreate une application Azure line-of-business avec authentification Azure Active Directory | Documents Microsoft
description: "Découvrez comment application toocreate un ASP.NET MVC-métier dans Azure App Service qui authentifie avec Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="3f61d-103">Créer une application Azure cœur de métier avec authentification Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f61d-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="3f61d-104">Cet article vous explique comment toocreate un .NET line-of-business application [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) à l’aide de hello [l’authentification / autorisation](../app-service/app-service-authentication-overview.md) fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3f61d-104">This article shows you how toocreate a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using hello [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="3f61d-105">Il montre également comment toouse hello [API Azure Active Directory Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery les données d’annuaire dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="3f61d-105">It also shows how toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory data in hello application.</span></span>

<span data-ttu-id="3f61d-106">client Azure Active Directory Hello que vous utilisez peut être un répertoire Azure uniquement.</span><span class="sxs-lookup"><span data-stu-id="3f61d-106">hello Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="3f61d-107">Ou bien, il peut être [synchronisés avec votre Active Directory local](../active-directory/active-directory-aadconnect.md) toocreate une expérience d’authentification unique pour les travailleurs sont locaux et distants.</span><span class="sxs-lookup"><span data-stu-id="3f61d-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) toocreate a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="3f61d-108">Cet article utilise le répertoire par défaut de hello pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3f61d-108">This article uses hello default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="3f61d-109">Ce que vous allez créer</span><span class="sxs-lookup"><span data-stu-id="3f61d-109">What you will build</span></span>
<span data-ttu-id="3f61d-110">Vous allez générer une application de création-lire-mise à jour-suppression (CRUD) line-of-business simple dans une application de Service Web Apps qu’assure le suivi des éléments de travail avec hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="3f61d-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with hello following features:</span></span>

* <span data-ttu-id="3f61d-111">Authentification des utilisateurs à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f61d-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="3f61d-112">Interrogation des utilisateurs et des groupes de répertoires à l’aide de l’ [API Graph Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="3f61d-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="3f61d-113">Utilisez hello ASP.NET MVC *aucune authentification* modèle</span><span class="sxs-lookup"><span data-stu-id="3f61d-113">Use hello ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="3f61d-114">Si vous avez besoin de contrôle d’accès en fonction du rôle (RBAC) pour votre application cœur de métier dans Azure, consultez l’ [étape suivante](#next).</span><span class="sxs-lookup"><span data-stu-id="3f61d-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="3f61d-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="3f61d-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="3f61d-116">Vous devez hello suivant toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="3f61d-116">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="3f61d-117">Un locataire Azure Active Directory avec les utilisateurs de différents groupes</span><span class="sxs-lookup"><span data-stu-id="3f61d-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="3f61d-118">Autorisations des applications toocreate sur le client d’Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="3f61d-118">Permissions toocreate applications on hello Azure Active Directory tenant</span></span>
* <span data-ttu-id="3f61d-119">Visual Studio 2013 Update 4 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="3f61d-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="3f61d-120">Kit de développement logiciel (SDK) Azure 2.8.1 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="3f61d-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a><span data-ttu-id="3f61d-121">Créer et déployer un tooAzure d’application web</span><span class="sxs-lookup"><span data-stu-id="3f61d-121">Create and deploy a web app tooAzure</span></span>
1. <span data-ttu-id="3f61d-122">Dans Visual Studio, cliquez sur **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="3f61d-123">Sélectionnez **Application web ASP.NET**, nommez votre projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="3f61d-124">Sélectionnez hello **MVC** modèle, puis modifier l’authentification hello trop**aucune authentification**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-124">Select hello **MVC** template, then change hello authentication too**No Authentication**.</span></span> <span data-ttu-id="3f61d-125">Assurez-vous que **hôte Bonjour Cloud** est sélectionné, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-125">Make sure **Host in hello Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="3f61d-126">Bonjour **créer un Service application** boîte de dialogue, cliquez sur **ajouter un compte** (puis **ajouter un compte** dans la liste déroulante de hello) toolog dans tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3f61d-126">In hello **Create App Service** dialog, click **Add an account** (and then **Add an account** in hello dropdown) toolog in tooyour Azure account.</span></span>
5. <span data-ttu-id="3f61d-127">Une fois connecté, configurez votre application web.</span><span class="sxs-lookup"><span data-stu-id="3f61d-127">Once logged in configure your web app.</span></span> <span data-ttu-id="3f61d-128">Créer un groupe de ressources et d’un nouveau plan de Service de l’application en cliquant sur hello respectif **nouveau** bouton.</span><span class="sxs-lookup"><span data-stu-id="3f61d-128">Create a resource group and a new App Service plan by clicking hello respective **New** button.</span></span> <span data-ttu-id="3f61d-129">Cliquez sur **Explorer d’autres services Azure** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="3f61d-129">Click **Explore additional Azure services** toocontinue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="3f61d-130">Bonjour **Services** , cliquez sur  **+**  tooadd une base de données SQL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="3f61d-130">In hello **Services** tab, click **+** tooadd a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="3f61d-131">Dans **configurer la base de données SQL**, cliquez sur **nouveau** toocreate une instance de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3f61d-131">In **Configure SQL Database**, click **New** toocreate a SQL Server instance.</span></span>
8. <span data-ttu-id="3f61d-132">Dans **Configurer SQL Server**, configurez votre instance SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3f61d-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="3f61d-133">Ensuite, cliquez sur **OK**, **OK**, et **créer** tookick hors tension de la création d’application hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3f61d-133">Then, click **OK**, **OK**, and **Create** tookick off hello app creation in Azure.</span></span>
9. <span data-ttu-id="3f61d-134">Dans **Azure App Service activité**, vous pouvez voir quand la création d’application hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="3f61d-134">In **Azure App Service Activity**, you can see when hello app creation is finished.</span></span> <span data-ttu-id="3f61d-135">Cliquez sur  **publier &lt;* appname*> toothis application Web maintenant **, puis cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-135">Click **Publish &lt;*appname*> toothis Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="3f61d-136">Une fois que Visual Studio se termine, il ouvre hello publier l’application dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="3f61d-136">Once Visual Studio finishes, it opens hello publish app in hello browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="3f61d-137">Configurer l’authentification et l’accès à l’annuaire</span><span class="sxs-lookup"><span data-stu-id="3f61d-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="3f61d-138">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f61d-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3f61d-139">Dans le menu de gauche hello, cliquez sur **des Services d’application** > **&lt;*appname*> ** > **l’authentification / autorisation**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-139">From hello left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="3f61d-140">Activez l’authentification Azure Active Directory en cliquant sur **Activé** > **Azure Active Directory** > **Express** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="3f61d-141">Cliquez sur **enregistrer** dans la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="3f61d-141">Click **Save** in hello command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="3f61d-142">Une fois que les paramètres d’authentification hello ont été enregistrés correctement, essayez d’application tooyour à nouveau dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="3f61d-142">Once hello authentication settings are saved successfully, try navigating tooyour app again in hello browser.</span></span> <span data-ttu-id="3f61d-143">Les paramètres par défaut assurent une authentification sur l’application entière hello.</span><span class="sxs-lookup"><span data-stu-id="3f61d-143">Your default settings enforce authentication on hello whole app.</span></span> <span data-ttu-id="3f61d-144">Si vous n’êtes pas déjà connecté, vous êtes écran de connexion tooa redirigé.</span><span class="sxs-lookup"><span data-stu-id="3f61d-144">If you aren't already logged in, you are redirected tooa login screen.</span></span> <span data-ttu-id="3f61d-145">Une fois connecté, vous constatez que votre application est sécurisée via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3f61d-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="3f61d-146">Ensuite, vous devez le toodirectory tooenable accéder aux données.</span><span class="sxs-lookup"><span data-stu-id="3f61d-146">Next, you need tooenable access toodirectory data.</span></span> 
5. <span data-ttu-id="3f61d-147">Accédez toohello [portail classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3f61d-147">Navigate toohello [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="3f61d-148">Dans le menu de gauche hello, cliquez sur **Active Directory** > **répertoire par défaut** > **Applications**  >   **&lt;* appname*> **.</span><span class="sxs-lookup"><span data-stu-id="3f61d-148">From hello left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="3f61d-149">Il s’agit d’application Azure Active Directory hello créés pour vous tooenable hello d’autorisation du Service d’applications / fonctionnalité d’authentification.</span><span class="sxs-lookup"><span data-stu-id="3f61d-149">This is hello Azure Active Directory application that App Service created for you tooenable hello Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="3f61d-150">Cliquez sur **utilisateurs** et **groupes** toomake assurer que vous disposez de certains utilisateurs et groupes dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="3f61d-150">Click **Users** and **Groups** toomake sure that you have some users and groups in hello directory.</span></span> <span data-ttu-id="3f61d-151">Dans le cas contraire, créez plusieurs utilisateurs et groupes de test.</span><span class="sxs-lookup"><span data-stu-id="3f61d-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="3f61d-152">Cliquez sur **configurer** tooconfigure cette application.</span><span class="sxs-lookup"><span data-stu-id="3f61d-152">Click **Configure** tooconfigure this application.</span></span>
9. <span data-ttu-id="3f61d-153">Faites défiler vers le bas toohello **clés** section et ajouter une clé en sélectionnant une durée.</span><span class="sxs-lookup"><span data-stu-id="3f61d-153">Scroll down toohello **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="3f61d-154">Ensuite, cliquez sur **Autorisations déléguées** et sélectionnez **Lire les données de l’annuaire**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="3f61d-155">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="3f61d-156">Une fois que vos paramètres sont enregistrés, faites défiler sauvegarder toohello **clés** et cliquez sur hello **copie** clé de client bouton toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="3f61d-156">Once your settings are saved, scroll back up toohello **Keys** section and click hello **Copy** button toocopy hello client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="3f61d-157">Si vous quittez cette page maintenant, vous ne serez pas en mesure de tooaccess jamais la clé de ce client.</span><span class="sxs-lookup"><span data-stu-id="3f61d-157">If you navigate away from this page now, you won't be able tooaccess this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="3f61d-158">Ensuite, vous devez tooconfigure votre application web avec cette clé.</span><span class="sxs-lookup"><span data-stu-id="3f61d-158">Next, you need tooconfigure your web app with this key.</span></span> <span data-ttu-id="3f61d-159">Connectez-vous à toohello [Explorateur de ressources Azure](https://resources.azure.com) avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3f61d-159">Log in toohello [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="3f61d-160">En hello haut hello, cliquez sur **en lecture/écriture** modifications toomake Bonjour Explorateur de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3f61d-160">At hello top of hello page, click **Read/Write** toomake changes in hello Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="3f61d-161">Recherche des paramètres d’authentification pour votre application, situé dans les abonnements hello >  **&lt;* subscriptionname*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **fournisseurs** > **Microsoft.Web**  >  **sites** > **&lt;*appname*> ** > **config**  >  **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-161">Find hello authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="3f61d-162">Cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="3f61d-163">Dans le volet de modification de hello, définissez hello `clientSecret` et `additionalLoginParams` propriétés comme suit.</span><span class="sxs-lookup"><span data-stu-id="3f61d-163">In hello editing pane, set hello `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="3f61d-164">Cliquez sur **Put** à hello toosubmit supérieur vos modifications.</span><span class="sxs-lookup"><span data-stu-id="3f61d-164">Click **Put** at hello top toosubmit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="3f61d-165">Tootest maintenant, si vous avez l’autorisation de hello jeton tooaccess hello API Graph Azure Active Directory, accédez simplement à  **https://&lt;*appname*>.azurewebsites.net/.auth/me** dans votre Navigateur.</span><span class="sxs-lookup"><span data-stu-id="3f61d-165">Now, tootest if you have hello authorization token tooaccess hello Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="3f61d-166">Si vous avez configuré tous les éléments correctement, vous devez voir hello `access_token` propriété Bonjour réponse JSON.</span><span class="sxs-lookup"><span data-stu-id="3f61d-166">If you configured everything correctly, you should see hello `access_token` property in hello JSON response.</span></span>
    
    <span data-ttu-id="3f61d-167">Hello `~/.auth/me` chemin d’accès de l’URL est géré par l’authentification du Service application / toogive d’autorisation vous toutes les informations de hello liées tooyour authentifié session.</span><span class="sxs-lookup"><span data-stu-id="3f61d-167">hello `~/.auth/me` URL path is managed by App Service Authentication / Authorization toogive you all hello information related tooyour authenticated session.</span></span> <span data-ttu-id="3f61d-168">Pour plus d’informations, consultez la page [Authentification et autorisation dans Azure App Service](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3f61d-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="3f61d-169">Hello `access_token` a une période d’expiration.</span><span class="sxs-lookup"><span data-stu-id="3f61d-169">hello `access_token` has an expiration period.</span></span> <span data-ttu-id="3f61d-170">Toutefois, l’authentification/autorisation App Service fournit des fonctionnalités d’actualisation du jeton grâce à `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="3f61d-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="3f61d-171">Pour plus d’informations sur la façon de toouse, consultez [App Store de jeton de Service](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="3f61d-171">For more information on how toouse it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="3f61d-172">Ensuite, vous ferez quelque chose d’utile avec les données d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="3f61d-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a><span data-ttu-id="3f61d-173">Ajouter des fonctionnalités métier-tooyour application</span><span class="sxs-lookup"><span data-stu-id="3f61d-173">Add line-of-business functionality tooyour app</span></span>
<span data-ttu-id="3f61d-174">Nous allons maintenant créer un outil de suivi simple des éléments de travail CRUD.</span><span class="sxs-lookup"><span data-stu-id="3f61d-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="3f61d-175">Dans le dossier de ~\Models hello, créez un fichier de classe appelé WorkItem.cs et remplacez `public class WorkItem {...}` par hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="3f61d-175">In hello ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with hello following code:</span></span>
   
     <span data-ttu-id="3f61d-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="3f61d-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="3f61d-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="3f61d-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="3f61d-178">}</span><span class="sxs-lookup"><span data-stu-id="3f61d-178">}</span></span>
   
     <span data-ttu-id="3f61d-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="3f61d-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="3f61d-180">}</span><span class="sxs-lookup"><span data-stu-id="3f61d-180">}</span></span>
2. <span data-ttu-id="3f61d-181">Générez hello projet toomake votre logique de génération de modèles automatique toohello accessible à nouveau modèle dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3f61d-181">Build hello project toomake your new model accessible toohello scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="3f61d-182">Ajouter un nouvel élément de modèle généré automatiquement `WorkItemsController` toohello ~\Controllers dossier (avec le bouton droit **contrôleurs**, pointez trop**ajouter**, puis sélectionnez **nouvel élément structuré**).</span><span class="sxs-lookup"><span data-stu-id="3f61d-182">Add a new scaffolded item `WorkItemsController` toohello ~\Controllers folder (right-click **Controllers**, point too**Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="3f61d-183">Sélectionnez **Contrôleur MVC 5 avec vues, en utilisant Entity Framework**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="3f61d-184">Modèle hello SELECT que vous avez créé, puis cliquez sur  **+**  , puis **ajouter** tooadd un contexte de données, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-184">Select hello model that you created, then click **+** and then **Add** tooadd a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="3f61d-185">Dans ~\Views\WorkItems\Create.cshtml (un élément de modèle généré automatiquement automatiquement), recherchez hello `Html.BeginForm` méthode d’assistance et hello en surbrillance des modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="3f61d-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find hello `Html.BeginForm` helper method and make hello following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="3f61d-186">Notez que `token` et `tenant` sont utilisés par hello `AadPicker` toomake objet appelle des API Azure Active Directory Graph.</span><span class="sxs-lookup"><span data-stu-id="3f61d-186">Note that `token` and `tenant` are used by hello `AadPicker` object toomake Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="3f61d-187">Vous allez ajouter `AadPicker` ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="3f61d-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="3f61d-188">Vous pouvez également obtenir `token` et `tenant` côté client de hello avec `~/.auth/me`, mais ce serait un appel de serveur supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="3f61d-188">You can just as well get `token` and `tenant` from hello client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="3f61d-189">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3f61d-189">For example:</span></span>
   > 
   > <span data-ttu-id="3f61d-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="3f61d-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="3f61d-191">Apporter des modifications mêmes avec hello ~ \Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="3f61d-191">Make hello same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="3f61d-192">Hello `AadPicker` objet est défini dans un script que vous avez besoin de tooadd tooyour projet.</span><span class="sxs-lookup"><span data-stu-id="3f61d-192">hello `AadPicker` object is defined in a script that you need tooadd tooyour project.</span></span> <span data-ttu-id="3f61d-193">Cliquez sur hello ~\Scripts dossier, pointez trop**ajouter**, puis cliquez sur **fichier JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-193">Right-click hello ~\Scripts folder, point too**Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="3f61d-194">Type `AadPickerLibrary` pour le nom de fichier hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-194">Type `AadPickerLibrary` for hello filename and click **OK**.</span></span>
9. <span data-ttu-id="3f61d-195">Copier le contenu hello [ici](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) dans ~ \Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="3f61d-195">Copy hello content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="3f61d-196">Dans le script de hello, hello `AadPicker` les appels de l’objet [API Azure Active Directory Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch pour les utilisateurs et groupes qui correspondent à des entrées de hello.</span><span class="sxs-lookup"><span data-stu-id="3f61d-196">In hello script, hello `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch for users and groups that match hello input.</span></span>  
10. <span data-ttu-id="3f61d-197">~\Scripts\AadPickerLibrary.js utilise également hello [widget de la saisie semi-automatique de l’interface utilisateur jQuery](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="3f61d-197">~\Scripts\AadPickerLibrary.js also uses hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="3f61d-198">Vous devez donc projet tooyour de tooadd jQuery UI.</span><span class="sxs-lookup"><span data-stu-id="3f61d-198">So you need tooadd jQuery UI tooyour project.</span></span> <span data-ttu-id="3f61d-199">Cliquez avec le bouton droit sur votre projet et cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="3f61d-200">Dans le Gestionnaire de Package NuGet de hello, cliquez sur Parcourir, type **-jquery ui** dans hello barre de recherche, puis cliquez sur **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-200">In hello NuGet Package Manager, click Browse, type **jquery-ui** in hello search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="3f61d-201">Dans le volet droit de hello, cliquez sur **installer**, puis cliquez sur **OK** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="3f61d-201">In hello right pane, click **Install**, then click **OK** tooproceed.</span></span>
13. <span data-ttu-id="3f61d-202">Ouvrez ~\App_Start\BundleConfig.cs et rendre hello en surbrillance des modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="3f61d-202">Open ~\App_Start\BundleConfig.cs and make hello following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="3f61d-203">Il existe plus performant de façons toomanage JavaScript et des fichiers CSS dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3f61d-203">There are more performant ways toomanage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="3f61d-204">Toutefois, par souci de simplicité vous allez juste toopiggyback sur les groupes de hello qui sont chargées avec chaque vue.</span><span class="sxs-lookup"><span data-stu-id="3f61d-204">However, for simplicity you're just going toopiggyback on hello bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="3f61d-205">Enfin, dans ~ \Global.asax, ajouter hello suivant la ligne de code hello `Application_Start()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="3f61d-205">Finally, in ~\Global.asax, add hello following line of code in hello `Application_Start()` method.</span></span> <span data-ttu-id="3f61d-206">`Ctrl`+`.`sur chaque erreur de résolution de noms trop résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="3f61d-206">`Ctrl`+`.` on each naming resolution error too fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="3f61d-207">Vous avez besoin de cette ligne de code, car le modèle MVC par défaut hello utilise <code>[ValidateAntiForgeryToken]</code> décoration sur certaines des actions de hello.</span><span class="sxs-lookup"><span data-stu-id="3f61d-207">You need this line of code because hello default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of hello actions.</span></span> <span data-ttu-id="3f61d-208">En raison du comportement toohello décrite par [Brock Allen](https://twitter.com/BrockLAllen) à [MVC 4, AntiForgeryToken et revendications](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) votre HTTP POST peut échouer la validation du jeton anti-contrefaçon car :</span><span class="sxs-lookup"><span data-stu-id="3f61d-208">Due toohello behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="3f61d-209">Azure Active Directory n’envoie pas http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, qui est requis par défaut par jeton anti-contrefaçon de hello.</span><span class="sxs-lookup"><span data-stu-id="3f61d-209">Azure Active Directory does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by hello anti-forgery token.</span></span>
    > * <span data-ttu-id="3f61d-210">Si Azure Active Directory est répertoire synchronisé avec AD FS, approbation hello AD FS par défaut n’envoie pas de revendication de http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, bien que vous pouvez configurer manuellement les services AD FS toosend cette revendication.</span><span class="sxs-lookup"><span data-stu-id="3f61d-210">If Azure Active Directory is directory synced with AD FS, hello AD FS trust by default does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS toosend this claim.</span></span>
    > 
    > <span data-ttu-id="3f61d-211">`ClaimTypes.NameIdentifies`Spécifie la revendication de hello `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, lequel Azure Active Directory ne fournit pas.</span><span class="sxs-lookup"><span data-stu-id="3f61d-211">`ClaimTypes.NameIdentifies` specifies hello claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="3f61d-212">Maintenant, publiez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="3f61d-212">Now, publish your changes.</span></span> <span data-ttu-id="3f61d-213">Cliquez avec le bouton droit sur votre projet et cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="3f61d-214">Cliquez sur **paramètres**, qu’il reste un tooyour de chaîne de connexion de base de données SQL, sélectionnez **mise à jour de la base de données** toomake hello des modifications de schéma pour votre modèle, puis cliquez sur **publier** .</span><span class="sxs-lookup"><span data-stu-id="3f61d-214">Click **Settings**, make sure there is a connection string tooyour SQL Database, select **Update Database** toomake hello schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="3f61d-215">Dans le navigateur de hello, accédez toohttps : / /&lt;*appname*>.azurewebsites.net/workitems et cliquez sur **créer un nouveau**.</span><span class="sxs-lookup"><span data-stu-id="3f61d-215">In hello browser, navigate toohttps://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="3f61d-216">Cliquez sur Bonjour **AssignedToName** boîte.</span><span class="sxs-lookup"><span data-stu-id="3f61d-216">Click in hello **AssignedToName** box.</span></span> <span data-ttu-id="3f61d-217">Les utilisateurs et les groupes issus de votre client Azure Active Directory s’affichent désormais dans une liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="3f61d-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="3f61d-218">Vous pouvez taper toofilter, ou utilisez hello `Up` ou `Down` de clé, ou cliquez sur tooselect hello utilisateur ou un groupe.</span><span class="sxs-lookup"><span data-stu-id="3f61d-218">You can type toofilter, or use hello `Up` or `Down` key or click tooselect hello user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="3f61d-219">Cliquez sur **créer** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="3f61d-219">Click **Create** toosave hello changes.</span></span> <span data-ttu-id="3f61d-220">Ensuite, cliquez sur **modifier** sur le travail de hello créé élément tooobserve hello même comportement.</span><span class="sxs-lookup"><span data-stu-id="3f61d-220">Then, click **Edit** on hello created work item tooobserve hello same behavior.</span></span>

<span data-ttu-id="3f61d-221">Félicitations, vous exécutez à présent une application cœur de métier dans Azure avec accès aux annuaires !</span><span class="sxs-lookup"><span data-stu-id="3f61d-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="3f61d-222">Il est beaucoup plus, que vous pouvez faire avec hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="3f61d-222">There's a lot more you can do with hello Graph API.</span></span> <span data-ttu-id="3f61d-223">Reportez-vous à la documentation de [référence sur l’API Graph Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="3f61d-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="3f61d-224">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="3f61d-224">Next Step</span></span>
<span data-ttu-id="3f61d-225">Si vous avez besoin de contrôle d’accès basé sur un rôle (RBAC) pour votre application line-of-business dans azure, consultez [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) pour obtenir un exemple à partir de l’équipe d’Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="3f61d-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from hello Azure Active Directory team.</span></span> <span data-ttu-id="3f61d-226">Il vous montre comment les rôles tooenable pour votre application Azure Active Directory et autoriser les utilisateurs avec hello `[Authorize]` décoration.</span><span class="sxs-lookup"><span data-stu-id="3f61d-226">It shows you how tooenable roles for your Azure Active Directory application, and then authorize users with hello `[Authorize]` decoration.</span></span>

<span data-ttu-id="3f61d-227">Si votre application line-of-business doit accéder aux données locales tooon, consultez [accès aux ressources locales à l’aide de connexions hybrides dans Azure App Service](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3f61d-227">If your line-of-business app needs access tooon-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="3f61d-228">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3f61d-228">Further resources</span></span>
* [<span data-ttu-id="3f61d-229">Authentification et autorisation dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3f61d-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="3f61d-230">Authentification avec Active Directory en local dans votre application Azure</span><span class="sxs-lookup"><span data-stu-id="3f61d-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="3f61d-231">Création d’une application cœur de métier dans Azure avec authentification AD FS</span><span class="sxs-lookup"><span data-stu-id="3f61d-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="3f61d-232">Authentification de Service d’application et hello API Azure AD Graph</span><span class="sxs-lookup"><span data-stu-id="3f61d-232">App Service Auth and hello Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="3f61d-233">Documentation et exemples Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f61d-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="3f61d-234">Types de jeton et de revendication pris en charge par Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f61d-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
