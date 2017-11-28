---
title: "Lorsque vous vous connectez tooAzure AD aaaChanges apportées tooa MVC du projet | Documents Microsoft"
description: "Décrit les effets de projet MVC tooyour lorsque vous vous connectez tooAzure AD à l’aide des services de Visual Studio connecté"
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
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="b992c-103">Le projet MVC toomy s’est produit (Visual Studio Azure Active Directory un service connecté) ?</span><span class="sxs-lookup"><span data-stu-id="b992c-103">What happened toomy MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b992c-104">Prise en main</span><span class="sxs-lookup"><span data-stu-id="b992c-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="b992c-105">Que s'est-il passé ?</span><span class="sxs-lookup"><span data-stu-id="b992c-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="b992c-106">Des références ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="b992c-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="b992c-107">Références du package NuGet</span><span class="sxs-lookup"><span data-stu-id="b992c-107">NuGet package references</span></span>
* <span data-ttu-id="b992c-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="b992c-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="b992c-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="b992c-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="b992c-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="b992c-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="b992c-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="b992c-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="b992c-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="b992c-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="b992c-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="b992c-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="b992c-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="b992c-114">**Owin**</span></span>
* <span data-ttu-id="b992c-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="b992c-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="b992c-116">Références .NET</span><span class="sxs-lookup"><span data-stu-id="b992c-116">.NET references</span></span>
* <span data-ttu-id="b992c-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="b992c-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="b992c-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="b992c-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="b992c-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="b992c-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="b992c-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="b992c-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="b992c-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="b992c-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="b992c-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="b992c-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="b992c-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="b992c-123">**Owin**</span></span>
* <span data-ttu-id="b992c-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="b992c-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="b992c-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="b992c-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="b992c-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="b992c-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="b992c-127">Du code a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="b992c-127">Code has been added</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="b992c-128">Fichiers de code ont été ajoutées tooyour projet</span><span class="sxs-lookup"><span data-stu-id="b992c-128">Code files were added tooyour project</span></span>
<span data-ttu-id="b992c-129">Une classe de démarrage de l’authentification, **App_Start/Startup.Auth.cs** a été ajouté projet tooyour contenant la logique de démarrage pour l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b992c-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="b992c-130">Une classe de contrôleur, Controllers/AccountController.cs, a aussi été ajoutée. Elle contient les méthodes **SignIn()** et **SignOut()**.</span><span class="sxs-lookup"><span data-stu-id="b992c-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="b992c-131">Enfin, une vue partielle, **Views/Shared/_LoginPartial.cshtml**, a été ajoutée. Elle contient un lien d’action pour la fonctionnalité SignIn/SignOut.</span><span class="sxs-lookup"><span data-stu-id="b992c-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="b992c-132">Code de démarrage a été ajouté tooyour projet</span><span class="sxs-lookup"><span data-stu-id="b992c-132">Startup code was added tooyour project</span></span>
<span data-ttu-id="b992c-133">Si vous disposez déjà d’une classe de démarrage dans votre projet, hello **Configuration** méthode a été mis à jour tooinclude un appel**ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="b992c-133">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too**ConfigureAuth(app)**.</span></span> <span data-ttu-id="b992c-134">Sinon, une classe de démarrage a été ajoutée tooyour projet.</span><span class="sxs-lookup"><span data-stu-id="b992c-134">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="b992c-135">Votre fichier app.config ou web.config comporte de nouvelles valeurs de configuration</span><span class="sxs-lookup"><span data-stu-id="b992c-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="b992c-136">Hello suivant des entrées de configuration ont été ajouté.</span><span class="sxs-lookup"><span data-stu-id="b992c-136">hello following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="b992c-137">Une application Azure Active Directory (AD) a été créée</span><span class="sxs-lookup"><span data-stu-id="b992c-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="b992c-138">Une Application Azure AD a été créée dans le répertoire hello que vous avez sélectionné dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="b992c-138">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="b992c-139">Si j’ai vérifié *désactiver l’authentification des comptes d’utilisateur individuels*, les modifications supplémentaires apportées toomy projet ?</span><span class="sxs-lookup"><span data-stu-id="b992c-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="b992c-140">Des références du package NuGet ont été supprimées, et des fichiers ont été supprimés et sauvegardés.</span><span class="sxs-lookup"><span data-stu-id="b992c-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="b992c-141">Selon l’état hello de votre projet, vous avez toomanually supprimer des références supplémentaires ou des fichiers ou modifier le code comme il convient.</span><span class="sxs-lookup"><span data-stu-id="b992c-141">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="b992c-142">Références du package NuGet supprimées (pour celles présentes)</span><span class="sxs-lookup"><span data-stu-id="b992c-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="b992c-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="b992c-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="b992c-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="b992c-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="b992c-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="b992c-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="b992c-146">Fichiers de code sauvegardés et supprimés (pour ceux présents)</span><span class="sxs-lookup"><span data-stu-id="b992c-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="b992c-147">Chacun des fichiers suivants a été sauvegardé et supprimé du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="b992c-147">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="b992c-148">Fichiers de sauvegarde se trouvent dans un dossier racine hello du répertoire du projet hello « Backup ».</span><span class="sxs-lookup"><span data-stu-id="b992c-148">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="b992c-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="b992c-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="b992c-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="b992c-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="b992c-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="b992c-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="b992c-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="b992c-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="b992c-153">Fichiers de code sauvegardés (pour ceux présents)</span><span class="sxs-lookup"><span data-stu-id="b992c-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="b992c-154">Chacun des fichiers suivants a été sauvegardé avant d’être remplacé.</span><span class="sxs-lookup"><span data-stu-id="b992c-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="b992c-155">Fichiers de sauvegarde se trouvent dans un dossier racine hello du répertoire du projet hello « Backup ».</span><span class="sxs-lookup"><span data-stu-id="b992c-155">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="b992c-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="b992c-156">**Startup.cs**</span></span>
* <span data-ttu-id="b992c-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="b992c-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="b992c-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="b992c-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="b992c-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="b992c-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="b992c-160">Si j’ai vérifié *lire les données d’annuaire*, les modifications supplémentaires apportées toomy projet ?</span><span class="sxs-lookup"><span data-stu-id="b992c-160">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="b992c-161">Des références supplémentaires ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="b992c-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="b992c-162">Références supplémentaires du package NuGet</span><span class="sxs-lookup"><span data-stu-id="b992c-162">Additional NuGet package references</span></span>
* <span data-ttu-id="b992c-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="b992c-163">**EntityFramework**</span></span>
* <span data-ttu-id="b992c-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="b992c-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="b992c-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="b992c-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="b992c-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="b992c-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="b992c-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="b992c-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="b992c-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="b992c-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="b992c-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="b992c-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="b992c-170">Références .NET supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b992c-170">Additional .NET references</span></span>
* <span data-ttu-id="b992c-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="b992c-171">**EntityFramework**</span></span>
* <span data-ttu-id="b992c-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="b992c-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="b992c-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="b992c-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="b992c-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="b992c-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="b992c-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="b992c-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="b992c-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="b992c-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="b992c-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="b992c-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="b992c-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="b992c-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="b992c-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="b992c-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-tooyour-project"></a><span data-ttu-id="b992c-180">Les fichiers de Code supplémentaires ont été ajoutées tooyour projet</span><span class="sxs-lookup"><span data-stu-id="b992c-180">Additional Code files were added tooyour project</span></span>
<span data-ttu-id="b992c-181">Deux fichiers ont été ajoutées toosupport mise en cache de jeton : **Models\ADALTokenCache.cs** et **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="b992c-181">Two files were added toosupport token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="b992c-182">Un contrôleur supplémentaire et la vue ont été ajoutées tooillustrate l’accès aux informations de profil utilisateur à l’aide d’Azure graph API.</span><span class="sxs-lookup"><span data-stu-id="b992c-182">An additional controller and view were added tooillustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="b992c-183">Ces fichiers sont **Controllers\UserProfileController.cs** et **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="b992c-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-tooyour-project"></a><span data-ttu-id="b992c-184">Code de démarrage supplémentaire a été ajouté tooyour projet</span><span class="sxs-lookup"><span data-stu-id="b992c-184">Additional Startup code was added tooyour project</span></span>
<span data-ttu-id="b992c-185">Bonjour **startup.auth.cs** un nouveau fichier **OpenIdConnectAuthenticationNotifications** objet a été ajouté toohello **Notifications** membre hello  **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="b992c-185">In hello **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added toohello **Notifications** member of hello **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="b992c-186">Il s’agit de tooenable réception hello OAuth code et il échange de jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="b992c-186">This is tooenable receiving hello OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="b992c-187">Des modifications supplémentaires apportées tooyour app.config ou web.config</span><span class="sxs-lookup"><span data-stu-id="b992c-187">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="b992c-188">Hello des entrées de configuration supplémentaires suivantes ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="b992c-188">hello following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="b992c-189">Hello des sections de configuration suivantes et la chaîne de connexion ont été ajoutés.</span><span class="sxs-lookup"><span data-stu-id="b992c-189">hello following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="b992c-190">Votre application Azure Active Directory a été mise à jour</span><span class="sxs-lookup"><span data-stu-id="b992c-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="b992c-191">Votre application d’Active Directory de Azure a été mis à jour tooinclude hello *lire les données d’annuaire* autorisation et une clé supplémentaire a été créé qui est ensuite utilisé comme hello *ida : ClientSecret* Bonjour  **Web.config** fichier.</span><span class="sxs-lookup"><span data-stu-id="b992c-191">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:ClientSecret* in hello **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b992c-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b992c-192">Next steps</span></span>
- [<span data-ttu-id="b992c-193">En savoir plus sur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b992c-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

