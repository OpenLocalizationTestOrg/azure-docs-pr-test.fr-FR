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
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a>Le projet MVC toomy s’est produit (Visual Studio Azure Active Directory un service connecté) ?
> [!div class="op_single_selector"]
> * [Prise en main](vs-active-directory-dotnet-getting-started.md)
> * [Que s'est-il passé ?](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Des références ont été ajoutées.
### <a name="nuget-package-references"></a>Références du package NuGet
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel.Tokens.Jwt**

### <a name="net-references"></a>Références .NET
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel**
* **System.IdentityModel.Tokens.Jwt**
* **System.Runtime.Serialization**

## <a name="code-has-been-added"></a>Du code a été ajouté.
### <a name="code-files-were-added-tooyour-project"></a>Fichiers de code ont été ajoutées tooyour projet
Une classe de démarrage de l’authentification, **App_Start/Startup.Auth.cs** a été ajouté projet tooyour contenant la logique de démarrage pour l’authentification Azure AD. Une classe de contrôleur, Controllers/AccountController.cs, a aussi été ajoutée. Elle contient les méthodes **SignIn()** et **SignOut()**. Enfin, une vue partielle, **Views/Shared/_LoginPartial.cshtml**, a été ajoutée. Elle contient un lien d’action pour la fonctionnalité SignIn/SignOut.

### <a name="startup-code-was-added-tooyour-project"></a>Code de démarrage a été ajouté tooyour projet
Si vous disposez déjà d’une classe de démarrage dans votre projet, hello **Configuration** méthode a été mis à jour tooinclude un appel**ConfigureAuth(app)**. Sinon, une classe de démarrage a été ajoutée tooyour projet.

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a>Votre fichier app.config ou web.config comporte de nouvelles valeurs de configuration
Hello suivant des entrées de configuration ont été ajouté.

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a>Une application Azure Active Directory (AD) a été créée
Une Application Azure AD a été créée dans le répertoire hello que vous avez sélectionné dans l’Assistant de hello.

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Si j’ai vérifié *désactiver l’authentification des comptes d’utilisateur individuels*, les modifications supplémentaires apportées toomy projet ?
Des références du package NuGet ont été supprimées, et des fichiers ont été supprimés et sauvegardés. Selon l’état hello de votre projet, vous avez toomanually supprimer des références supplémentaires ou des fichiers ou modifier le code comme il convient.

### <a name="nuget-package-references-removed-for-those-present"></a>Références du package NuGet supprimées (pour celles présentes)
* **Microsoft.AspNet.Identity.Core**
* **Microsoft.AspNet.Identity.EntityFramework**
* **Microsoft.AspNet.Identity.Owin**

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Fichiers de code sauvegardés et supprimés (pour ceux présents)
Chacun des fichiers suivants a été sauvegardé et supprimé du projet de hello. Fichiers de sauvegarde se trouvent dans un dossier racine hello du répertoire du projet hello « Backup ».

* **App_Start\IdentityConfig.cs**
* **Controllers\ManageController.cs**
* **Models\IdentityModels.cs**
* **Models\ManageViewModels.cs**

### <a name="code-files-backed-up-for-those-present"></a>Fichiers de code sauvegardés (pour ceux présents)
Chacun des fichiers suivants a été sauvegardé avant d’être remplacé. Fichiers de sauvegarde se trouvent dans un dossier racine hello du répertoire du projet hello « Backup ».

* **Startup.cs**
* **App_Start\Startup.Auth.cs**
* **Controllers\AccountController.cs**
* **Views\Shared\_LoginPartial.cshtml**

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Si j’ai vérifié *lire les données d’annuaire*, les modifications supplémentaires apportées toomy projet ?
Des références supplémentaires ont été ajoutées.

### <a name="additional-nuget-package-references"></a>Références supplémentaires du package NuGet
* **EntityFramework**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **System.Spatial**

### <a name="additional-net-references"></a>Références .NET supplémentaires
* **EntityFramework**
* **EntityFramework.SqlServer**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**
* **System.Spatial**

### <a name="additional-code-files-were-added-tooyour-project"></a>Les fichiers de Code supplémentaires ont été ajoutées tooyour projet
Deux fichiers ont été ajoutées toosupport mise en cache de jeton : **Models\ADALTokenCache.cs** et **Models\ApplicationDbContext.cs**.  Un contrôleur supplémentaire et la vue ont été ajoutées tooillustrate l’accès aux informations de profil utilisateur à l’aide d’Azure graph API.  Ces fichiers sont **Controllers\UserProfileController.cs** et **Views\UserProfile\Index.cshtml**.

### <a name="additional-startup-code-was-added-tooyour-project"></a>Code de démarrage supplémentaire a été ajouté tooyour projet
Bonjour **startup.auth.cs** un nouveau fichier **OpenIdConnectAuthenticationNotifications** objet a été ajouté toohello **Notifications** membre hello  **OpenIdConnectAuthenticationOptions**.  Il s’agit de tooenable réception hello OAuth code et il échange de jeton d’accès.

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Des modifications supplémentaires apportées tooyour app.config ou web.config
Hello des entrées de configuration supplémentaires suivantes ont été ajoutées.

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

Hello des sections de configuration suivantes et la chaîne de connexion ont été ajoutés.

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


### <a name="your-azure-active-directory-app-was-updated"></a>Votre application Azure Active Directory a été mise à jour
Votre application d’Active Directory de Azure a été mis à jour tooinclude hello *lire les données d’annuaire* autorisation et une clé supplémentaire a été créé qui est ensuite utilisé comme hello *ida : ClientSecret* Bonjour  **Web.config** fichier.

## <a name="next-steps"></a>Étapes suivantes
- [En savoir plus sur Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

