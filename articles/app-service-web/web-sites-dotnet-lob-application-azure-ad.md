---
title: "Créer une application Azure cœur de métier avec authentification Azure Active Directory | Microsoft Docs"
description: "Apprenez à créer une application cœur de métier ASP.NET MVC dans Azure App Service qui s’authentifie avec Azure Active Directory."
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
ms.openlocfilehash: 6eadf0a521a32c5bc580908e4e4b7f4305e2bf7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="4b2b6-103">Créer une application Azure cœur de métier avec authentification Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b2b6-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="4b2b6-104">Cet article vous montre comment créer une application Azure cœur de métier dans [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) à l’aide de la fonctionnalité d’[authentification/autorisation](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4b2b6-104">This article shows you how to create a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using the [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="4b2b6-105">Il indique également comment utiliser l’ [API Graph Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) pour interroger les données d’annuaire dans l’application.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-105">It also shows how to use the [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to query directory data in the application.</span></span>

<span data-ttu-id="4b2b6-106">Le client Azure Active Directory que vous utilisez peut être un annuaire Azure uniquement.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-106">The Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="4b2b6-107">Il peut également être [synchronisé avec votre Active Directory local](../active-directory/active-directory-aadconnect.md) pour créer une expérience d’authentification unique pour les employés locaux et distants.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) to create a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="4b2b6-108">Cet article utilise le répertoire par défaut pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-108">This article uses the default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="4b2b6-109">Ce que vous allez créer</span><span class="sxs-lookup"><span data-stu-id="4b2b6-109">What you will build</span></span>
<span data-ttu-id="4b2b6-110">Vous allez créer une application CRUD (Create-Read-Update-Delete) métier simple dans App Service Web Apps qui assure le suivi des éléments de travail et qui présente les caractéristiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b2b6-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with the following features:</span></span>

* <span data-ttu-id="4b2b6-111">Authentification des utilisateurs à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b2b6-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="4b2b6-112">Interrogation des utilisateurs et des groupes de répertoires à l’aide de l’ [API Graph Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="4b2b6-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="4b2b6-113">Utilisation du modèle ASP.NET MVC *Aucune authentification*</span><span class="sxs-lookup"><span data-stu-id="4b2b6-113">Use the ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="4b2b6-114">Si vous avez besoin de contrôle d’accès en fonction du rôle (RBAC) pour votre application cœur de métier dans Azure, consultez l’ [étape suivante](#next).</span><span class="sxs-lookup"><span data-stu-id="4b2b6-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="4b2b6-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="4b2b6-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="4b2b6-116">Vous devez disposer des éléments suivants pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="4b2b6-116">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="4b2b6-117">Un locataire Azure Active Directory avec les utilisateurs de différents groupes</span><span class="sxs-lookup"><span data-stu-id="4b2b6-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="4b2b6-118">Les autorisations permettant de créer des applications sur le locataire AAD</span><span class="sxs-lookup"><span data-stu-id="4b2b6-118">Permissions to create applications on the Azure Active Directory tenant</span></span>
* <span data-ttu-id="4b2b6-119">Visual Studio 2013 Update 4 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="4b2b6-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="4b2b6-120">Kit de développement logiciel (SDK) Azure 2.8.1 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="4b2b6-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-to-azure"></a><span data-ttu-id="4b2b6-121">Créer et déployer une application web sur Azure</span><span class="sxs-lookup"><span data-stu-id="4b2b6-121">Create and deploy a web app to Azure</span></span>
1. <span data-ttu-id="4b2b6-122">Dans Visual Studio, cliquez sur **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="4b2b6-123">Sélectionnez **Application web ASP.NET**, nommez votre projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="4b2b6-124">Sélectionnez le modèle **MVC**, puis définissez l’authentification sur **Aucune authentification**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-124">Select the **MVC** template, then change the authentication to **No Authentication**.</span></span> <span data-ttu-id="4b2b6-125">Vérifiez que **Héberger dans le cloud** est sélectionné et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-125">Make sure **Host in the Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="4b2b6-126">Dans la boîte de dialogue **Créer App Service**, cliquez sur **Ajouter un compte** (puis sur **Ajouter un compte** dans la liste déroulante) pour vous connecter à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-126">In the **Create App Service** dialog, click **Add an account** (and then **Add an account** in the dropdown) to log in to your Azure account.</span></span>
5. <span data-ttu-id="4b2b6-127">Une fois connecté, configurez votre application web.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-127">Once logged in configure your web app.</span></span> <span data-ttu-id="4b2b6-128">Créez un groupe de ressources et un plan App Service en cliquant sur le bouton **Nouveau** correspondant.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-128">Create a resource group and a new App Service plan by clicking the respective **New** button.</span></span> <span data-ttu-id="4b2b6-129">Cliquez sur **Exploration d’autres services Azure** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-129">Click **Explore additional Azure services** to continue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="4b2b6-130">Dans l’onglet **Services**, cliquez sur **+** pour ajouter une base de données SQL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-130">In the **Services** tab, click **+** to add a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="4b2b6-131">Dans **Configurer la base de données SQL**, cliquez sur **Nouveau** pour créer une instance SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-131">In **Configure SQL Database**, click **New** to create a SQL Server instance.</span></span>
8. <span data-ttu-id="4b2b6-132">Dans **Configurer SQL Server**, configurez votre instance SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="4b2b6-133">Ensuite, cliquez sur **OK**, **OK** et **Créer** pour lancer la création de l’application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-133">Then, click **OK**, **OK**, and **Create** to kick off the app creation in Azure.</span></span>
9. <span data-ttu-id="4b2b6-134">Dans **Activité d’Azure App Service**, vous pouvez voir lorsque la création de l’application est terminée.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-134">In **Azure App Service Activity**, you can see when the app creation is finished.</span></span> <span data-ttu-id="4b2b6-135">Cliquez sur **Publier &lt;*nom_application*> dans cette application web maintenant**, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-135">Click **Publish &lt;*appname*> to this Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="4b2b6-136">Une fois que Visual Studio a terminé, il ouvre l’application de publication dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-136">Once Visual Studio finishes, it opens the publish app in the browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="4b2b6-137">Configurer l’authentification et l’accès à l’annuaire</span><span class="sxs-lookup"><span data-stu-id="4b2b6-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="4b2b6-138">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b2b6-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4b2b6-139">Dans le menu de gauche, cliquez sur **App Services** > **&lt;*nom_application*>** > **Authentification/Autorisation**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-139">From the left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="4b2b6-140">Activez l’authentification Azure Active Directory en cliquant sur **Activé** > **Azure Active Directory** > **Express** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="4b2b6-141">Cliquez sur **Enregistrer** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-141">Click **Save** in the command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="4b2b6-142">Une fois les paramètres d’authentification enregistrés correctement, essayez de nouveau d’accéder à votre application dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-142">Once the authentication settings are saved successfully, try navigating to your app again in the browser.</span></span> <span data-ttu-id="4b2b6-143">Les paramètres par défaut assurent une authentification sur l’ensemble de l’application.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-143">Your default settings enforce authentication on the whole app.</span></span> <span data-ttu-id="4b2b6-144">Si vous n’êtes pas encore connecté, vous êtes redirigé vers un écran de connexion.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-144">If you aren't already logged in, you are redirected to a login screen.</span></span> <span data-ttu-id="4b2b6-145">Une fois connecté, vous constatez que votre application est sécurisée via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="4b2b6-146">Ensuite, vous devez activer l’accès aux données de l’annuaire.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-146">Next, you need to enable access to directory data.</span></span> 
5. <span data-ttu-id="4b2b6-147">Accédez au [Portail Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4b2b6-147">Navigate to the [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="4b2b6-148">Dans le menu de gauche, cliquez sur **Active Directory** > **Répertoire par défaut** > **Applications** > **&lt;*appname*>**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-148">From the left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="4b2b6-149">Il s’agit de l’application Azure Active Directory créée pour vous par App Service pour activer la fonctionnalité d’autorisation/authentification.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-149">This is the Azure Active Directory application that App Service created for you to enable the Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="4b2b6-150">Cliquez sur **Utilisateurs** et **Groupes** pour vous assurer que l’annuaire contient des utilisateurs et des groupes.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-150">Click **Users** and **Groups** to make sure that you have some users and groups in the directory.</span></span> <span data-ttu-id="4b2b6-151">Dans le cas contraire, créez plusieurs utilisateurs et groupes de test.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="4b2b6-152">Cliquez sur **Configurer** pour configurer cette application.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-152">Click **Configure** to configure this application.</span></span>
9. <span data-ttu-id="4b2b6-153">Faites défiler jusqu’à la section **Clés** et ajoutez une clé en sélectionnant une durée.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-153">Scroll down to the **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="4b2b6-154">Ensuite, cliquez sur **Autorisations déléguées** et sélectionnez **Lire les données de l’annuaire**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="4b2b6-155">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="4b2b6-156">Une fois que vos paramètres sont enregistrés, revenez à la section **Clés** et cliquez sur le bouton **Copier** pour copier la clé du client.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-156">Once your settings are saved, scroll back up to the **Keys** section and click the **Copy** button to copy the client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="4b2b6-157">Si vous quittez cette page maintenant, vous ne pourrez plus accéder à cette clé de client.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-157">If you navigate away from this page now, you won't be able to access this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="4b2b6-158">Ensuite, vous devez configurer votre application web avec cette clé.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-158">Next, you need to configure your web app with this key.</span></span> <span data-ttu-id="4b2b6-159">Connectez-vous à [Azure Resource Explorer](https://resources.azure.com) avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-159">Log in to the [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="4b2b6-160">En haut de la page, cliquez sur **Lecture/écriture** pour apporter des modifications dans Azure Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-160">At the top of the page, click **Read/Write** to make changes in the Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="4b2b6-161">Recherchez les paramètres d’authentification de votre application, situés dans subscriptions > **&lt;*nom_abonnement*>** > **resourceGroups** > **&lt;*nom_groupe_ressources*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*nom_application*>** > **config** > **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-161">Find the authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="4b2b6-162">Cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="4b2b6-163">Dans le volet d’édition, définissez les propriétés `clientSecret` et `additionalLoginParams` comme suit.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-163">In the editing pane, set the `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from the Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="4b2b6-164">Cliquez sur **Put** en haut pour soumettre vos modifications.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-164">Click **Put** at the top to submit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="4b2b6-165">Maintenant, pour vérifier si vous disposez du jeton d’autorisation permettant d’accéder à l’API Graph Azure Active Directory, accédez à **https://&lt;*appname*>.azurewebsites.net/.auth/me** dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-165">Now, to test if you have the authorization token to access the Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="4b2b6-166">Si vous avez configuré tous les éléments correctement, vous devez voir la propriété `access_token` dans la réponse JSON.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-166">If you configured everything correctly, you should see the `access_token` property in the JSON response.</span></span>
    
    <span data-ttu-id="4b2b6-167">Le chemin d’accès de l’URL `~/.auth/me` est géré par l’authentification/autorisation App Service, afin de vous donner toutes les informations relatives à votre session authentifiée.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-167">The `~/.auth/me` URL path is managed by App Service Authentication / Authorization to give you all the information related to your authenticated session.</span></span> <span data-ttu-id="4b2b6-168">Pour plus d’informations, consultez la page [Authentification et autorisation dans Azure App Service](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4b2b6-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4b2b6-169">Le chemin d’accès de l’URL `access_token` a un délai d’expiration.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-169">The `access_token` has an expiration period.</span></span> <span data-ttu-id="4b2b6-170">Toutefois, l’authentification/autorisation App Service fournit des fonctionnalités d’actualisation du jeton grâce à `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="4b2b6-171">Pour plus d’informations sur son utilisation, consultez la page [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/)(Boutique de jetons App Service).</span><span class="sxs-lookup"><span data-stu-id="4b2b6-171">For more information on how to use it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="4b2b6-172">Ensuite, vous ferez quelque chose d’utile avec les données d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-to-your-app"></a><span data-ttu-id="4b2b6-173">Ajouter une fonctionnalité cœur de métier à votre application</span><span class="sxs-lookup"><span data-stu-id="4b2b6-173">Add line-of-business functionality to your app</span></span>
<span data-ttu-id="4b2b6-174">Nous allons maintenant créer un outil de suivi simple des éléments de travail CRUD.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="4b2b6-175">Dans le dossier ~\Models, créez un fichier de classe intitulé WorkItem.cs et remplacez le code `public class WorkItem {...}` par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="4b2b6-175">In the ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with the following code:</span></span>
   
     <span data-ttu-id="4b2b6-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="4b2b6-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="4b2b6-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="4b2b6-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="4b2b6-178">}</span><span class="sxs-lookup"><span data-stu-id="4b2b6-178">}</span></span>
   
     <span data-ttu-id="4b2b6-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="4b2b6-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="4b2b6-180">}</span><span class="sxs-lookup"><span data-stu-id="4b2b6-180">}</span></span>
2. <span data-ttu-id="4b2b6-181">Générez le projet pour rendre votre nouveau modèle accessible à la logique de génération de modèles automatique dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-181">Build the project to make your new model accessible to the scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="4b2b6-182">Ajoutez un nouvel élément généré automatiquement `WorkItemsController` au dossier ~\Controllers (cliquez avec le bouton sur **Contrôleurs**, pointez sur **Ajouter**, puis sélectionnez **Nouvel élément généré automatiquement**).</span><span class="sxs-lookup"><span data-stu-id="4b2b6-182">Add a new scaffolded item `WorkItemsController` to the ~\Controllers folder (right-click **Controllers**, point to **Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="4b2b6-183">Sélectionnez **Contrôleur MVC 5 avec vues, en utilisant Entity Framework**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="4b2b6-184">Sélectionnez le modèle que vous avez créé, puis cliquez sur **+**, puis sur **Ajouter** pour ajouter un contexte de données, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-184">Select the model that you created, then click **+** and then **Add** to add a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="4b2b6-185">Dans ~\Views\WorkItems\Create.cshtml (élément généré automatiquement), recherchez la méthode d’assistance `Html.BeginForm` et modifiez-la comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b2b6-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find the `Html.BeginForm` helper method and make the following highlighted changes:</span></span>  
   
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
    @Html.ActionLink(&quot;Back to List&quot;, &quot;Index&quot;)
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
   
        // Submit the selected user/group to be asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="4b2b6-186">Notez que `token` et `tenant` sont utilisés par l’objet `AadPicker` pour effectuer des appels API Graph Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-186">Note that `token` and `tenant` are used by the `AadPicker` object to make Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="4b2b6-187">Vous allez ajouter `AadPicker` ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="4b2b6-188">Vous pouvez également obtenir `token` et `tenant` à partir du client avec `~/.auth/me`, mais ce serait un appel de serveur supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-188">You can just as well get `token` and `tenant` from the client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="4b2b6-189">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4b2b6-189">For example:</span></span>
   > 
   > <span data-ttu-id="4b2b6-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="4b2b6-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="4b2b6-191">Apportez les mêmes modifications avec ~\Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-191">Make the same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="4b2b6-192">L’objet `AadPicker` est défini dans un script que vous souhaitez ajouter à votre projet.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-192">The `AadPicker` object is defined in a script that you need to add to your project.</span></span> <span data-ttu-id="4b2b6-193">Cliquez avec le bouton droit sur le dossier ~\Scripts, pointez sur **Ajouter**, et cliquez sur **Fichier JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-193">Right-click the ~\Scripts folder, point to **Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="4b2b6-194">Tapez `AadPickerLibrary` pour le nom de fichier et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-194">Type `AadPickerLibrary` for the filename and click **OK**.</span></span>
9. <span data-ttu-id="4b2b6-195">Copiez le contenu à partir d’[ici](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) dans ~\Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-195">Copy the content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="4b2b6-196">Dans le script, l’objet `AadPicker` appelle l’ [API Graph Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) pour rechercher des utilisateurs et des groupes qui correspondent à l’entrée.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-196">In the script, the `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to search for users and groups that match the input.</span></span>  
10. <span data-ttu-id="4b2b6-197">~\Scripts\AadPickerLibrary.js utilise également le [widget de saisie semi-automatique de l’interface utilisateur jQuery](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="4b2b6-197">~\Scripts\AadPickerLibrary.js also uses the [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="4b2b6-198">Par conséquent, vous devez ajouter l’interface utilisateur jQuery à votre projet.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-198">So you need to add jQuery UI to your project.</span></span> <span data-ttu-id="4b2b6-199">Cliquez avec le bouton droit sur votre projet et cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="4b2b6-200">Dans le Gestionnaire de Package NuGet, cliquez sur Parcourir, tapez **jquery-ui** dans la barre de recherche, et cliquez sur **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-200">In the NuGet Package Manager, click Browse, type **jquery-ui** in the search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="4b2b6-201">Dans le volet droit, cliquez sur **Installer**, puis sur **OK** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-201">In the right pane, click **Install**, then click **OK** to proceed.</span></span>
13. <span data-ttu-id="4b2b6-202">Ouvrez ~\App_Start\BundleConfig.cs et apportez les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b2b6-202">Open ~\App_Start\BundleConfig.cs and make the following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
        // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
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
    
    <span data-ttu-id="4b2b6-203">Il existe d’autres manières de gérer de manière performante les fichiers JavaScript et CSS dans votre application.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-203">There are more performant ways to manage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="4b2b6-204">Toutefois, par souci de simplicité vous allez juste procéder à une superposition sur les offres groupées chargées avec chaque vue.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-204">However, for simplicity you're just going to piggyback on the bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="4b2b6-205">Enfin, dans ~ \Global.asax, ajoutez la ligne de code suivante à la méthode `Application_Start()`.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-205">Finally, in ~\Global.asax, add the following line of code in the `Application_Start()` method.</span></span> <span data-ttu-id="4b2b6-206">`Ctrl`+`.` sur chaque erreur de résolution d’affectation de noms pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-206">`Ctrl`+`.` on each naming resolution error to fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="4b2b6-207">Vous avez besoin de cette ligne de code, car le modèle MVC par défaut utilise la décoration <code>[ValidateAntiForgeryToken]</code> sur certaines des actions.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-207">You need this line of code because the default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of the actions.</span></span> <span data-ttu-id="4b2b6-208">En raison du comportement décrit par [Brock Allen](https://twitter.com/BrockLAllen) dans son article intitulé [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) (en anglais), votre HTTP POST risque d’échouer lors de la validation du jeton anti-contrefaçon pour les motifs suivants :</span><span class="sxs-lookup"><span data-stu-id="4b2b6-208">Due to the behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="4b2b6-209">Azure Active Directory n’envoie pas la revendication http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider qui, par défaut, est nécessaire au jeton d’anti-contrefaçon.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-209">Azure Active Directory does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by the anti-forgery token.</span></span>
    > * <span data-ttu-id="4b2b6-210">S’il y a synchronisation d’annuaire entre Azure Active Directory et AD FS, l’approbation AD FS par défaut n’envoie pas la revendication http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, même si vous pouvez configurer manuellement l’envoi de cette revendication par les services AD FS.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-210">If Azure Active Directory is directory synced with AD FS, the AD FS trust by default does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS to send this claim.</span></span>
    > 
    > <span data-ttu-id="4b2b6-211">`ClaimTypes.NameIdentifies` spécifie la revendication `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, qu’Azure Active Directory ne fournit pas.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-211">`ClaimTypes.NameIdentifies` specifies the claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="4b2b6-212">Maintenant, publiez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-212">Now, publish your changes.</span></span> <span data-ttu-id="4b2b6-213">Cliquez avec le bouton droit sur votre projet et cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="4b2b6-214">Cliquez sur **Paramètres**, assurez-vous qu’il y a une chaîne de connexion à votre base de données SQL, sélectionnez **Mettre à jour la base de données** pour apporter les modifications de schéma pour votre modèle, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-214">Click **Settings**, make sure there is a connection string to your SQL Database, select **Update Database** to make the schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="4b2b6-215">Dans le navigateur, accédez à https://&lt;*appname*>.azurewebsites.net/workitems, puis cliquez sur **Créer nouveau**.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-215">In the browser, navigate to https://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="4b2b6-216">Cliquez dans la zone **AssignedToName** .</span><span class="sxs-lookup"><span data-stu-id="4b2b6-216">Click in the **AssignedToName** box.</span></span> <span data-ttu-id="4b2b6-217">Les utilisateurs et les groupes issus de votre client Azure Active Directory s’affichent désormais dans une liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="4b2b6-218">Vous pouvez saisir du texte pour filtrer, ou utiliser la clé `Up` ou `Down` pour sélectionner l’utilisateur ou le groupe.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-218">You can type to filter, or use the `Up` or `Down` key or click to select the user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="4b2b6-219">Cliquez sur **Créer** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-219">Click **Create** to save the changes.</span></span> <span data-ttu-id="4b2b6-220">Ensuite, cliquez sur **Modifier** sur l’élément de travail créé pour observer le même comportement.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-220">Then, click **Edit** on the created work item to observe the same behavior.</span></span>

<span data-ttu-id="4b2b6-221">Félicitations, vous exécutez à présent une application cœur de métier dans Azure avec accès aux annuaires !</span><span class="sxs-lookup"><span data-stu-id="4b2b6-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="4b2b6-222">L’API Graph vous offre de nombreuses autres possibilités.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-222">There's a lot more you can do with the Graph API.</span></span> <span data-ttu-id="4b2b6-223">Reportez-vous à la documentation de [référence sur l’API Graph Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="4b2b6-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="4b2b6-224">étape suivante</span><span class="sxs-lookup"><span data-stu-id="4b2b6-224">Next Step</span></span>
<span data-ttu-id="4b2b6-225">Si vous avez besoin d’un contrôle d’accès en fonction du rôle (RBAC) pour votre application cœur de métier dans Azure, consultez [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) pour obtenir un exemple de l’équipe Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b2b6-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from the Azure Active Directory team.</span></span> <span data-ttu-id="4b2b6-226">Ce dernier montre comment activer des rôles pour votre application Azure Active Directory et autoriser des utilisateurs disposant de la décoration `[Authorize]` .</span><span class="sxs-lookup"><span data-stu-id="4b2b6-226">It shows you how to enable roles for your Azure Active Directory application, and then authorize users with the `[Authorize]` decoration.</span></span>

<span data-ttu-id="4b2b6-227">Si votre application cœur de métier doit accéder à des données locales, consultez la page [Accéder à des ressources locales à l’aide de connexions hybrides dans Azure App Service](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4b2b6-227">If your line-of-business app needs access to on-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="4b2b6-228">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4b2b6-228">Further resources</span></span>
* [<span data-ttu-id="4b2b6-229">Authentification et autorisation dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4b2b6-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="4b2b6-230">Authentification avec Active Directory en local dans votre application Azure</span><span class="sxs-lookup"><span data-stu-id="4b2b6-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="4b2b6-231">Création d’une application cœur de métier dans Azure avec authentification AD FS</span><span class="sxs-lookup"><span data-stu-id="4b2b6-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="4b2b6-232">Authentification App Service et API Graph Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b2b6-232">App Service Auth and the Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="4b2b6-233">Documentation et exemples Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b2b6-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="4b2b6-234">Types de jeton et de revendication pris en charge par Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b2b6-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
