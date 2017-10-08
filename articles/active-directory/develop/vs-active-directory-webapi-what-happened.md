---
title: "projet de WebApi tooa aaaChanges effectuées lorsque vous vous connectez tooAzure AD | Documents Microsoft"
description: "Décrit les effets de tooyour WebApi projet lorsque vous vous connectez tooAzure AD à l’aide de Visual Studio"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="afc2d-103">Le projet de WebApi toomy s’est produit (Visual Studio Azure Active Directory un service connecté)</span><span class="sxs-lookup"><span data-stu-id="afc2d-103">What happened toomy WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="afc2d-104">Prise en main</span><span class="sxs-lookup"><span data-stu-id="afc2d-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="afc2d-105">Que s'est-il passé ?</span><span class="sxs-lookup"><span data-stu-id="afc2d-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="afc2d-106">Des références ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="afc2d-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="afc2d-107">Références du package NuGet</span><span class="sxs-lookup"><span data-stu-id="afc2d-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="afc2d-108">Références .NET</span><span class="sxs-lookup"><span data-stu-id="afc2d-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="afc2d-109">Modifications du code</span><span class="sxs-lookup"><span data-stu-id="afc2d-109">Code changes</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="afc2d-110">Fichiers de code ont été ajoutées tooyour projet</span><span class="sxs-lookup"><span data-stu-id="afc2d-110">Code files were added tooyour project</span></span>
<span data-ttu-id="afc2d-111">Une classe de démarrage de l’authentification, **App_Start/Startup.Auth.cs** a été ajouté projet tooyour contenant la logique de démarrage pour l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afc2d-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="afc2d-112">Code de démarrage a été ajouté tooyour projet</span><span class="sxs-lookup"><span data-stu-id="afc2d-112">Startup code was added tooyour project</span></span>
<span data-ttu-id="afc2d-113">Si vous disposez déjà d’une classe de démarrage dans votre projet, hello **Configuration** méthode a été mis à jour tooinclude un appel`ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="afc2d-113">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too`ConfigureAuth(app)`.</span></span> <span data-ttu-id="afc2d-114">Sinon, une classe de démarrage a été ajoutée tooyour projet.</span><span class="sxs-lookup"><span data-stu-id="afc2d-114">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="afc2d-115">Votre fichier app.config ou web.config comporte de nouvelles valeurs de configuration.</span><span class="sxs-lookup"><span data-stu-id="afc2d-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="afc2d-116">Hello suivant des entrées de configuration ont été ajouté.</span><span class="sxs-lookup"><span data-stu-id="afc2d-116">hello following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="afc2d-117">Une application Azure AD App a été créée</span><span class="sxs-lookup"><span data-stu-id="afc2d-117">An Azure AD App was created</span></span>
<span data-ttu-id="afc2d-118">Une Application Azure AD a été créée dans le répertoire hello que vous avez sélectionné dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="afc2d-118">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

[<span data-ttu-id="afc2d-119">En savoir plus sur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="afc2d-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="afc2d-120">Si j’ai vérifié *désactiver l’authentification des comptes d’utilisateur individuels*, les modifications supplémentaires apportées toomy projet ?</span><span class="sxs-lookup"><span data-stu-id="afc2d-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="afc2d-121">Des références du package NuGet ont été supprimées, et des fichiers ont été supprimés et sauvegardés.</span><span class="sxs-lookup"><span data-stu-id="afc2d-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="afc2d-122">Selon l’état hello de votre projet, vous avez toomanually supprimer des références supplémentaires ou des fichiers ou modifier le code comme il convient.</span><span class="sxs-lookup"><span data-stu-id="afc2d-122">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="afc2d-123">Références du package NuGet supprimées (pour celles présentes)</span><span class="sxs-lookup"><span data-stu-id="afc2d-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="afc2d-124">Fichiers de code sauvegardés et supprimés (pour ceux présents)</span><span class="sxs-lookup"><span data-stu-id="afc2d-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="afc2d-125">Chacun des fichiers suivants a été sauvegardé et supprimé du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="afc2d-125">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="afc2d-126">Fichiers de sauvegarde se trouvent dans un dossier racine hello du répertoire du projet hello « Backup ».</span><span class="sxs-lookup"><span data-stu-id="afc2d-126">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="afc2d-127">Fichiers de code sauvegardés (pour ceux présents)</span><span class="sxs-lookup"><span data-stu-id="afc2d-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="afc2d-128">Chacun des fichiers suivants a été sauvegardé avant d’être remplacé.</span><span class="sxs-lookup"><span data-stu-id="afc2d-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="afc2d-129">Fichiers de sauvegarde se trouvent dans un dossier racine hello du répertoire du projet hello « Backup ».</span><span class="sxs-lookup"><span data-stu-id="afc2d-129">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="afc2d-130">Si j’ai vérifié *lire les données d’annuaire*, les modifications supplémentaires apportées toomy projet ?</span><span class="sxs-lookup"><span data-stu-id="afc2d-130">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="afc2d-131">Des modifications supplémentaires apportées tooyour app.config ou web.config</span><span class="sxs-lookup"><span data-stu-id="afc2d-131">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="afc2d-132">Hello des entrées de configuration supplémentaires suivantes ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="afc2d-132">hello following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="afc2d-133">Votre application Azure Active Directory a été mise à jour</span><span class="sxs-lookup"><span data-stu-id="afc2d-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="afc2d-134">Votre application d’Active Directory de Azure a été mis à jour tooinclude hello *lire les données d’annuaire* autorisation et une clé supplémentaire a été créé qui est ensuite utilisé comme hello *ida : mot de passe* Bonjour `web.config` fichier.</span><span class="sxs-lookup"><span data-stu-id="afc2d-134">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:Password* in hello `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afc2d-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="afc2d-135">Next steps</span></span>
- [<span data-ttu-id="afc2d-136">En savoir plus sur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="afc2d-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

