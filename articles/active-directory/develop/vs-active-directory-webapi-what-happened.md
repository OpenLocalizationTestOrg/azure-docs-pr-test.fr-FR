---
title: "Modifications apportées à un projet WebApi quand vous vous connectez à Azure AD | Microsoft Docs"
description: "Décrit ce qui se passe dans votre projet WebApi quand vous vous connectez à Azure AD en utilisant Visual Studio"
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
ms.openlocfilehash: 086e5a9622cad681cd282345d97e0c28ee7de2fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="f1986-103">Qu’est-il arrivé à mon projet WebApi (service connecté Azure Active Directory de Visual Studio) ?</span><span class="sxs-lookup"><span data-stu-id="f1986-103">What happened to my WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1986-104">Prise en main</span><span class="sxs-lookup"><span data-stu-id="f1986-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="f1986-105">Que s'est-il passé ?</span><span class="sxs-lookup"><span data-stu-id="f1986-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="f1986-106">Des références ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="f1986-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="f1986-107">Références du package NuGet</span><span class="sxs-lookup"><span data-stu-id="f1986-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="f1986-108">Références .NET</span><span class="sxs-lookup"><span data-stu-id="f1986-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="f1986-109">Modifications du code</span><span class="sxs-lookup"><span data-stu-id="f1986-109">Code changes</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="f1986-110">Des fichiers de code ont été ajoutés à votre projet</span><span class="sxs-lookup"><span data-stu-id="f1986-110">Code files were added to your project</span></span>
<span data-ttu-id="f1986-111">La classe de démarrage d’authentification **App_Start/Startup.Auth.cs** a été ajoutée à votre projet. Elle contient la logique de démarrage permettant l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1986-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="f1986-112">Un code de démarrage a été ajouté à votre projet</span><span class="sxs-lookup"><span data-stu-id="f1986-112">Startup code was added to your project</span></span>
<span data-ttu-id="f1986-113">Si vous disposiez déjà d’une classe de démarrage dans votre projet, la méthode **Configuration** a été mise à jour pour inclure un appel vers `ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="f1986-113">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to `ConfigureAuth(app)`.</span></span> <span data-ttu-id="f1986-114">Sinon, une classe de démarrage a été ajoutée à votre projet.</span><span class="sxs-lookup"><span data-stu-id="f1986-114">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="f1986-115">Votre fichier app.config ou web.config comporte de nouvelles valeurs de configuration.</span><span class="sxs-lookup"><span data-stu-id="f1986-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="f1986-116">Les entrées de configuration ci-dessous ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="f1986-116">The following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="The App ID Uri from the wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="f1986-117">Une application Azure AD App a été créée</span><span class="sxs-lookup"><span data-stu-id="f1986-117">An Azure AD App was created</span></span>
<span data-ttu-id="f1986-118">Une application Azure AD a été créée dans le répertoire que vous avez sélectionné dans l'Assistant.</span><span class="sxs-lookup"><span data-stu-id="f1986-118">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

[<span data-ttu-id="f1986-119">En savoir plus sur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1986-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="f1986-120">Si j’ai coché *Désactiver l’authentification des comptes d’utilisateur individuels*, quelles autres modifications ont été apportées à mon projet ?</span><span class="sxs-lookup"><span data-stu-id="f1986-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="f1986-121">Des références du package NuGet ont été supprimées, et des fichiers ont été supprimés et sauvegardés.</span><span class="sxs-lookup"><span data-stu-id="f1986-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="f1986-122">Selon l’état de votre projet, vous pouvez avoir besoin de supprimer manuellement d’autres références ou fichiers, ou de modifier le code le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="f1986-122">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="f1986-123">Références du package NuGet supprimées (pour celles présentes)</span><span class="sxs-lookup"><span data-stu-id="f1986-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="f1986-124">Fichiers de code sauvegardés et supprimés (pour ceux présents)</span><span class="sxs-lookup"><span data-stu-id="f1986-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="f1986-125">Chacun des fichiers suivants a été sauvegardé et supprimé du projet.</span><span class="sxs-lookup"><span data-stu-id="f1986-125">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="f1986-126">Les fichiers de sauvegarde sont situés dans un dossier « Backup » à la racine du répertoire du projet.</span><span class="sxs-lookup"><span data-stu-id="f1986-126">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="f1986-127">Fichiers de code sauvegardés (pour ceux présents)</span><span class="sxs-lookup"><span data-stu-id="f1986-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="f1986-128">Chacun des fichiers suivants a été sauvegardé avant d’être remplacé.</span><span class="sxs-lookup"><span data-stu-id="f1986-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="f1986-129">Les fichiers de sauvegarde sont situés dans un dossier « Backup » à la racine du répertoire du projet.</span><span class="sxs-lookup"><span data-stu-id="f1986-129">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="f1986-130">Si j’ai coché *Lire les données de l’annuaire*, quelles autres modifications ont été apportées à mon projet ?</span><span class="sxs-lookup"><span data-stu-id="f1986-130">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="f1986-131">Des modifications supplémentaires ont été apportées à votre fichier app.config ou web.config</span><span class="sxs-lookup"><span data-stu-id="f1986-131">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="f1986-132">Les entrées de configuration ci-dessous ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="f1986-132">The following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="f1986-133">Votre application Azure Active Directory a été mise à jour</span><span class="sxs-lookup"><span data-stu-id="f1986-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="f1986-134">Votre application Azure Active Directory a été mise à jour pour inclure l’autorisation *Lire les données de l’annuaire*, et une clé supplémentaire a été créée pour être ensuite utilisée comme *ida:Password* dans le fichier `web.config`.</span><span class="sxs-lookup"><span data-stu-id="f1986-134">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:Password* in the `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1986-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1986-135">Next steps</span></span>
- [<span data-ttu-id="f1986-136">En savoir plus sur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1986-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

