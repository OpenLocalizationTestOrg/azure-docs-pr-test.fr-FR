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
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a>Le projet de WebApi toomy s’est produit (Visual Studio Azure Active Directory un service connecté)
> [!div class="op_single_selector"]
> * [Prise en main](vs-active-directory-webapi-getting-started.md)
> * [Que s'est-il passé ?](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Des références ont été ajoutées.
### <a name="nuget-package-references"></a>Références du package NuGet
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>Références .NET
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>Modifications du code
### <a name="code-files-were-added-tooyour-project"></a>Fichiers de code ont été ajoutées tooyour projet
Une classe de démarrage de l’authentification, **App_Start/Startup.Auth.cs** a été ajouté projet tooyour contenant la logique de démarrage pour l’authentification Azure AD.

### <a name="startup-code-was-added-tooyour-project"></a>Code de démarrage a été ajouté tooyour projet
Si vous disposez déjà d’une classe de démarrage dans votre projet, hello **Configuration** méthode a été mis à jour tooinclude un appel`ConfigureAuth(app)`. Sinon, une classe de démarrage a été ajoutée tooyour projet.

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>Votre fichier app.config ou web.config comporte de nouvelles valeurs de configuration.
Hello suivant des entrées de configuration ont été ajouté.

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>Une application Azure AD App a été créée
Une Application Azure AD a été créée dans le répertoire hello que vous avez sélectionné dans l’Assistant de hello.

[En savoir plus sur Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Si j’ai vérifié *désactiver l’authentification des comptes d’utilisateur individuels*, les modifications supplémentaires apportées toomy projet ?
Des références du package NuGet ont été supprimées, et des fichiers ont été supprimés et sauvegardés. Selon l’état hello de votre projet, vous avez toomanually supprimer des références supplémentaires ou des fichiers ou modifier le code comme il convient.

### <a name="nuget-package-references-removed-for-those-present"></a>Références du package NuGet supprimées (pour celles présentes)
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Fichiers de code sauvegardés et supprimés (pour ceux présents)
Chacun des fichiers suivants a été sauvegardé et supprimé du projet de hello. Fichiers de sauvegarde se trouvent dans un dossier racine hello du répertoire du projet hello « Backup ».

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>Fichiers de code sauvegardés (pour ceux présents)
Chacun des fichiers suivants a été sauvegardé avant d’être remplacé. Fichiers de sauvegarde se trouvent dans un dossier racine hello du répertoire du projet hello « Backup ».

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Si j’ai vérifié *lire les données d’annuaire*, les modifications supplémentaires apportées toomy projet ?
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Des modifications supplémentaires apportées tooyour app.config ou web.config
Hello des entrées de configuration supplémentaires suivantes ont été ajoutées.

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>Votre application Azure Active Directory a été mise à jour
Votre application d’Active Directory de Azure a été mis à jour tooinclude hello *lire les données d’annuaire* autorisation et une clé supplémentaire a été créé qui est ensuite utilisé comme hello *ida : mot de passe* Bonjour `web.config` fichier.

## <a name="next-steps"></a>Étapes suivantes
- [En savoir plus sur Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

