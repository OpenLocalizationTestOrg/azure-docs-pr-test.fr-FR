---
title: "Modifications apportées à un projet MVC quand vous vous connectez à Azure AD | Microsoft Docs"
description: "Décrit les conséquences sur votre projet MVC lorsque vous vous connectez à Azure AD à l'aide des services connectés Visual Studio"
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 095411a7fc854f4dce11921adb0f57c5389a8e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="0c43a-103">Qu'est-il arrivé à mon projet MVC (service connecté Azure Active Directory Visual Studio) ?</span><span class="sxs-lookup"><span data-stu-id="0c43a-103">What happened to my MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c43a-104">Prise en main</span><span class="sxs-lookup"><span data-stu-id="0c43a-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="0c43a-105">Que s'est-il passé ?</span><span class="sxs-lookup"><span data-stu-id="0c43a-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="0c43a-106">Des références ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="0c43a-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="0c43a-107">Références du package NuGet</span><span class="sxs-lookup"><span data-stu-id="0c43a-107">NuGet package references</span></span>
* <span data-ttu-id="0c43a-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="0c43a-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="0c43a-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="0c43a-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="0c43a-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="0c43a-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="0c43a-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="0c43a-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="0c43a-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="0c43a-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="0c43a-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="0c43a-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="0c43a-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="0c43a-114">**Owin**</span></span>
* <span data-ttu-id="0c43a-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="0c43a-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="0c43a-116">Références .NET</span><span class="sxs-lookup"><span data-stu-id="0c43a-116">.NET references</span></span>
* <span data-ttu-id="0c43a-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="0c43a-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="0c43a-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="0c43a-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="0c43a-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="0c43a-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="0c43a-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="0c43a-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="0c43a-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="0c43a-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="0c43a-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="0c43a-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="0c43a-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="0c43a-123">**Owin**</span></span>
* <span data-ttu-id="0c43a-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="0c43a-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="0c43a-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="0c43a-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="0c43a-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="0c43a-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="0c43a-127">Du code a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="0c43a-127">Code has been added</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="0c43a-128">Des fichiers de code ont été ajoutés à votre projet</span><span class="sxs-lookup"><span data-stu-id="0c43a-128">Code files were added to your project</span></span>
<span data-ttu-id="0c43a-129">La classe de démarrage d’authentification **App_Start/Startup.Auth.cs** a été ajoutée à votre projet. Elle contient la logique de démarrage permettant l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c43a-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="0c43a-130">Une classe de contrôleur, Controllers/AccountController.cs, a aussi été ajoutée. Elle contient les méthodes **SignIn()** et **SignOut()**.</span><span class="sxs-lookup"><span data-stu-id="0c43a-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="0c43a-131">Enfin, une vue partielle, **Views/Shared/_LoginPartial.cshtml**, a été ajoutée. Elle contient un lien d’action pour la fonctionnalité SignIn/SignOut.</span><span class="sxs-lookup"><span data-stu-id="0c43a-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="0c43a-132">Un code de démarrage a été ajouté à votre projet</span><span class="sxs-lookup"><span data-stu-id="0c43a-132">Startup code was added to your project</span></span>
<span data-ttu-id="0c43a-133">Si vous disposiez déjà d’une classe de démarrage dans votre projet, la méthode **Configuration** a été mise à jour pour inclure un appel à **ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="0c43a-133">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**.</span></span> <span data-ttu-id="0c43a-134">Sinon, une classe de démarrage a été ajoutée à votre projet.</span><span class="sxs-lookup"><span data-stu-id="0c43a-134">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="0c43a-135">Votre fichier app.config ou web.config comporte de nouvelles valeurs de configuration</span><span class="sxs-lookup"><span data-stu-id="0c43a-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="0c43a-136">Les entrées de configuration ci-dessous ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="0c43a-136">The following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="The selected Azure AD Domain" />
        <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="0c43a-137">Une application Azure Active Directory (AD) a été créée</span><span class="sxs-lookup"><span data-stu-id="0c43a-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="0c43a-138">Une application Azure AD a été créée dans le répertoire que vous avez sélectionné dans l'Assistant.</span><span class="sxs-lookup"><span data-stu-id="0c43a-138">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="0c43a-139">Si j'ai coché *Désactiver l'authentification des comptes d'utilisateur individuels*, quelles autres modifications ont été apportées à mon projet ?</span><span class="sxs-lookup"><span data-stu-id="0c43a-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="0c43a-140">Des références du package NuGet ont été supprimées, et des fichiers ont été supprimés et sauvegardés.</span><span class="sxs-lookup"><span data-stu-id="0c43a-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="0c43a-141">Selon l’état de votre projet, vous pouvez avoir besoin de supprimer manuellement d’autres références ou fichiers, ou de modifier le code le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="0c43a-141">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="0c43a-142">Références du package NuGet supprimées (pour celles présentes)</span><span class="sxs-lookup"><span data-stu-id="0c43a-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="0c43a-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="0c43a-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="0c43a-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="0c43a-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="0c43a-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="0c43a-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="0c43a-146">Fichiers de code sauvegardés et supprimés (pour ceux présents)</span><span class="sxs-lookup"><span data-stu-id="0c43a-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="0c43a-147">Chacun des fichiers suivants a été sauvegardé et supprimé du projet.</span><span class="sxs-lookup"><span data-stu-id="0c43a-147">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="0c43a-148">Les fichiers de sauvegarde sont situés dans un dossier « Backup » à la racine du répertoire du projet.</span><span class="sxs-lookup"><span data-stu-id="0c43a-148">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="0c43a-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="0c43a-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="0c43a-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="0c43a-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="0c43a-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="0c43a-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="0c43a-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="0c43a-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="0c43a-153">Fichiers de code sauvegardés (pour ceux présents)</span><span class="sxs-lookup"><span data-stu-id="0c43a-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="0c43a-154">Chacun des fichiers suivants a été sauvegardé avant d’être remplacé.</span><span class="sxs-lookup"><span data-stu-id="0c43a-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="0c43a-155">Les fichiers de sauvegarde sont situés dans un dossier « Backup » à la racine du répertoire du projet.</span><span class="sxs-lookup"><span data-stu-id="0c43a-155">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="0c43a-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="0c43a-156">**Startup.cs**</span></span>
* <span data-ttu-id="0c43a-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="0c43a-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="0c43a-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="0c43a-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="0c43a-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="0c43a-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="0c43a-160">Si j’ai coché *Lire les données de l’annuaire*, quelles autres modifications ont été apportées à mon projet ?</span><span class="sxs-lookup"><span data-stu-id="0c43a-160">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
<span data-ttu-id="0c43a-161">Des références supplémentaires ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="0c43a-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="0c43a-162">Références supplémentaires du package NuGet</span><span class="sxs-lookup"><span data-stu-id="0c43a-162">Additional NuGet package references</span></span>
* <span data-ttu-id="0c43a-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="0c43a-163">**EntityFramework**</span></span>
* <span data-ttu-id="0c43a-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="0c43a-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="0c43a-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="0c43a-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="0c43a-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="0c43a-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="0c43a-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="0c43a-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="0c43a-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="0c43a-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="0c43a-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="0c43a-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="0c43a-170">Références .NET supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0c43a-170">Additional .NET references</span></span>
* <span data-ttu-id="0c43a-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="0c43a-171">**EntityFramework**</span></span>
* <span data-ttu-id="0c43a-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="0c43a-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="0c43a-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="0c43a-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="0c43a-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="0c43a-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="0c43a-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="0c43a-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="0c43a-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="0c43a-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="0c43a-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="0c43a-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="0c43a-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="0c43a-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="0c43a-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="0c43a-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-to-your-project"></a><span data-ttu-id="0c43a-180">Des fichiers de code supplémentaires ont été ajoutés à votre projet</span><span class="sxs-lookup"><span data-stu-id="0c43a-180">Additional Code files were added to your project</span></span>
<span data-ttu-id="0c43a-181">Deux fichiers ont été ajoutés pour prendre en charge la mise en cache de jeton : **Models\ADALTokenCache.cs** et **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="0c43a-181">Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="0c43a-182">Un contrôleur et une vue supplémentaires ont été ajoutés pour illustrer l’accès aux informations de profil utilisateur à l’aide des API graphiques Azure.</span><span class="sxs-lookup"><span data-stu-id="0c43a-182">An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="0c43a-183">Ces fichiers sont **Controllers\UserProfileController.cs** et **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="0c43a-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-to-your-project"></a><span data-ttu-id="0c43a-184">Un code de démarrage a été ajouté à votre projet</span><span class="sxs-lookup"><span data-stu-id="0c43a-184">Additional Startup code was added to your project</span></span>
<span data-ttu-id="0c43a-185">Dans le fichier **startup.auth.cs**, un nouvel objet **OpenIdConnectAuthenticationNotifications** a été ajouté au membre **Notifications** de **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="0c43a-185">In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="0c43a-186">Cette opération consiste à activer la réception du code OAuth reçu et à l’échanger contre un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="0c43a-186">This is to enable receiving the OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="0c43a-187">Des modifications supplémentaires ont été apportées à votre fichier app.config ou web.config</span><span class="sxs-lookup"><span data-stu-id="0c43a-187">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="0c43a-188">Les entrées de configuration ci-dessous ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="0c43a-188">The following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="0c43a-189">Les sections de configuration et la chaîne de connexion suivantes ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="0c43a-189">The following configuration sections and connection string have been added.</span></span>

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="0c43a-190">Votre application Azure Active Directory a été mise à jour</span><span class="sxs-lookup"><span data-stu-id="0c43a-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="0c43a-191">Votre application Azure Active Directory a été mise à jour pour inclure l’autorisation *Lire les données de l’annuaire*, et une clé supplémentaire a été créée pour être ensuite utilisée comme *ida:ClientSecret* dans le fichier **web.config**.</span><span class="sxs-lookup"><span data-stu-id="0c43a-191">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c43a-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0c43a-192">Next steps</span></span>
- [<span data-ttu-id="0c43a-193">En savoir plus sur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c43a-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

