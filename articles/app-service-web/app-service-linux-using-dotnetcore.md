---
title: "aaaUse .NET Core dans l’application Web sur Linux | Documents Microsoft"
description: Utilisez .NET Core dans une application web sur Linux.
keywords: azure app service, application web, dotnet, core, linux, oss
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>Utiliser .NET Core dans une application web Azure sur Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Application Web](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) sur Linux fournit un service d’hébergement web hautement évolutifs et correction automatique à l’aide du système d’exploitation de Linux hello. Ce didacticiel contient des instructions pas à pas montrant comment toocreate un [.NET Core](https://docs.microsoft.com/aspnet/core/) application sur l’application web Azure sous Linux. 

![Application web sous Linux][10]

Vous pouvez suivre les étapes de hello ci-dessous à l’aide d’un ordinateur Mac, Windows ou Linux.

## <a name="prerequisites"></a>Composants requis ##

toocomplete ce didacticiel : 

* Installer hello [le Kit de développement .NET Core](https://www.microsoft.com/net/download/core).
* Installez [Git](https://git-scm.com/downloads).

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>Créer une application .NET Core locale ##

Démarrez une nouvelle session de terminal. Créez un répertoire nommé `hellodotnetcore`et modifier hello Active directory tooit. Puis tapez ce qui suit hello : 

```
dotnet new web
``` 

  Cette commande crée trois fichiers (*hellodotnetcore.csproj*, *Program.cs*, et *Startup.cs*) et un dossier vide (*wwwroot /*) sous le répertoire en cours de hello. Hello contenu de `.csproj` fichier doit ressembler à hello suivantes : 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

Étant donné que cette application est une application web, un tooan référence package ASP.NET Core a été automatiquement ajouté toohello *hellodotnetcore.csproj* fichier. numéro de version de Hello du package de hello est définie en fonction de toohello choisi framework. Cet exemple fait référence à ASP.NET Core version 1.1.2, car .NET Core 1.1 est utilisé.

## <a name="build-and-test-hello-application-locally"></a>Générer et tester l’application hello localement ##

Vous pouvez générer et exécuter votre application .NET Core par hello `dotnet restore` commande suivie hello `dotnet run` de commande, comme indiqué ici :

```
dotnet restore
dotnet run
```


Lors de l’application hello démarre, il affiche un message indiquant l’application hello est à l’écoute des demandes tooincoming à un port. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

Testez-le en parcourant trop`http://localhost:5000/` avec votre navigateur. Si tout fonctionne correctement, vous voyez « Hello World! » en tant que texte hello du résultat.

![Tester avec un navigateur][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a>Créer une application .NET Core Bonjour portail Azure ##

Tout d’abord, vous devez toocreate une application web vide. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) et créer un nouveau [l’application Web sur Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).

![Création d’une application web][1]

Hello lorsque **créer** s’ouvre, fournissez des détails sur votre application web :

![Choix d’une pile d’exécution .NET Core][2]

Suivant de hello d’utilisation de table comme un toofill guide out hello **créer** page, puis sélectionnez **OK** et **créer** toocreate hello application.

| Paramètre      | Valeur suggérée  | Description                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| Nom de l’application | hellodotnetcore  | nom Hello de votre application. Ce nom doit être unique. |
| Abonnement | Choisir un abonnement existant | Hello abonnement Azure. |
| Groupe de ressources | myResourceGroup |  ressource Azure groupe toocontain hello web application Hello. |
| Plan App Service | Nom de plan App Service existant |  Hello plan App Service.  |
| Configurer le conteneur | .NET Core 1.1 | type de conteneur pour cette application web de Hello : Registre intégrées, Docker ou Private. |
| Source d’image  | Intégration  |  source de Hello d’image de hello. |
| Pile d’exécution  | .NET Core 1.1  | pile de runtime Hello et la version.  |

## <a name="deploy-your-application-via-git"></a>Déployer votre application via Git ##

Utiliser Git toodeploy hello .NET Core application tooAzure application de Service d’applications Web sur Linux.

application web Azure Hello possède déjà un déploiement Git configuré. Vous trouverez des URL de déploiement Git hello en naviguant toohello suivant URL après avoir inséré le nom de votre application web :

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

Hello URL Git a hello suivant du formulaire basé sur le nom de votre application web :

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Exécutez hello suivant de commandes toodeploy hello application locale tooyour Azure web app : 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

Vous n’avez pas besoin toopush tous les fichiers sous *bin /* ou *obj /* répertoires, car votre application est générée dans le cloud de hello lorsque hello l’application fichiers sources sont envoyées tooAzure. Une fois le processus de génération hello est terminée, les fichiers binaires sont copiés dans le répertoire de l’application hello dans */home/site/wwwroot/*.

Vérifiez que les opérations de déploiement à distance de hello signalent la réussite. Les opérations de push peuvent prendre un certain temps depuis la résolution de package et s’exécutent dans le cloud de hello de processus de génération. Plusieurs messages d’état s’afficheront, y compris ceux indiquant que les fichiers ont été copiés. sortie de Hello doit ressembler similaire toohello suivantes :

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Une fois le déploiement de hello est terminée, redémarrez votre application web pour effet de tootake déploiement hello. toodo, accédez toohello portail Azure et accédez toohello **vue d’ensemble** page de votre application web. Sélectionnez hello **redémarrer** bouton dans la page de hello. Quand une fenêtre contextuelle s’affiche, sélectionnez **Oui** tooconfirm. Vous pouvez ensuite parcourir votre application web, comme illustré ici :

![Navigation .NET Core application déployée tooAzure du Service d’applications sur Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Étapes suivantes
* [FAQ de l’application web Azure App Service sur Linux](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
