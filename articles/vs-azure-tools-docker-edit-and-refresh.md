---
title: applications aaaDebugging dans un conteneur Docker local | Documents Microsoft
description: "Découvrez comment toomodify une application qui s’exécute dans un conteneur Docker local, actualiser le conteneur hello via modifier et actualiser et définir des points d’arrêt de débogage"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a>Débogage d’applications dans un conteneur Docker local
## <a name="overview"></a>Vue d'ensemble
Hello Visual Studio Tools pour Docker fournit un toodevelop de manière cohérente dans et valider votre application localement dans un conteneur Linux Docker.
Vous n’avez conteneur de hello toorestart chaque fois que vous modifiez un code.
Cet article explique comment toouse hello « Modifier et actualiser » fonctionnalité toostart une application ASP.NET Core Web dans un conteneur Docker local, apportez les modifications nécessaires, puis actualisez hello navigateur toosee ces modifications.
Cet article montre également comment tooset les points d’arrêt pour le débogage.

> [!NOTE]
> La prise en charge des conteneurs Windows sera proposée dans une version ultérieure
>
>

## <a name="prerequisites"></a>Composants requis
Hello suivant outils doit être installé.

* [Dernière version de Visual Studio](https://www.visualstudio.com/downloads/)
* [Kit de développement logiciel (SDK) Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)

toorun Docker localement des conteneurs, vous aurez besoin d’un client local docker.
Vous pouvez utiliser hello [boîte à outils Docker](https://www.docker.com/products/docker-toolbox), ce qui nécessite toobe Hyper-V désactivé, ou vous pouvez utiliser [Docker pour Windows](https://www.docker.com/get-docker), qui utilise Hyper-V et qui nécessite Windows 10.

Si vous utilisez la boîte à outils Docker, vous devez trop[configurer hello Docker client](vs-azure-tools-docker-setup.md)

## <a name="1-create-a-web-app"></a>1. Créer une application web
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Ajouter la prise en charge Docker
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a>3. Modifier votre code et actualiser
tooquickly itérer au sein des modifications, vous pouvez démarrer votre application dans un conteneur et continuer toomake modifications, les afficher comme vous le feriez avec IIS Express.

1. Définir hello Configuration de Solution trop`Debug` et appuyez sur  **&lt;CTRL + F5 >** toobuild votre docker de l’image et l’exécuter localement.

    Une fois l’image de conteneur hello a été généré et s’exécute dans un conteneur Docker, Visual Studio lance l’application Web de hello dans votre navigateur par défaut.
    Si vous utilisez le navigateur Microsoft Edge de hello ou comportent des erreurs, consultez [dépannage](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.
2. Accédez à toohello sur la page, ce qui est là que nous allons toomake nos modifications.
3. Retournez tooVisual Studio et ouvrez `Views\Home\About.cshtml`.
4. Ajouter hello suivant HTML toohello contenu de la fin du fichier de hello et enregistrez les modifications de hello.

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. Affichage de fenêtre de sortie hello, lorsque hello build de .NET est terminée et vous voyez ces lignes, commutateur tooyour arrière navigateur et hello sur la page d’actualisation.

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. Vos modifications ont été appliquées !

## <a name="4-debug-with-breakpoints"></a>4. Déboguer à l’aide de points d’arrêt
Souvent, modifications devez davantage inspection, en tirant parti des fonctionnalités de Visual Studio de débogage de hello.

1. Retournez tooVisual Studio et ouvrez`Controllers\HomeController.cs`
2. Remplacez contenu hello de méthode de About() hello par hello qui suit :

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. Ensemble d’un point d’arrêt toohello à gauche de hello `string message`... ligne.
4. Accès  **&lt;F5 >** toostart de débogage.
5. Accédez à toohello sur la page toohit votre point d’arrêt.
6. Basculer le point d’arrêt de tooVisual Studio tooview hello et inspecter la valeur hello du message.

   ![][2]

## <a name="summary"></a>Résumé
Avec [Visual Studio 2015 Tools pour Docker](https://aka.ms/DockerToolsForVS), vous pouvez obtenir la productivité hello de travailler localement, réalisme hello production de développement dans un conteneur Docker.

## <a name="troubleshooting"></a>Résolution des problèmes
[Résolution des problèmes de développement avec Docker pour Visual Studio](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>En savoir plus sur Docker avec Visual Studio, Windows et Azure
* [Outils Docker pour Visual Studio](http://aka.ms/dockertoolsforvs) : développer votre code .NET Core dans un conteneur
* [Outils Docker pour Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) : créez et déployez des conteneurs Docker
* [Outils Docker pour Visual Studio Code](http://aka.ms/dockertoolsforvscode) : services linguistiques pour la modification de fichiers Docker, avec plus de scénarios E2E à venir
* [Informations sur le conteneur Windows](http://aka.ms/containers): informations sur Windows Server et Nano Server
* [Service de conteneur Azure](https://azure.microsoft.com/services/container-service/) - [Contenu du service de conteneur Azure](http://aka.ms/AzureContainerService)
* Pour plus d’exemples de l’utilisation de Docker, consultez [utilisation de Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) de hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 connexion [démonstration](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/). Pour plus des Démarrages rapides à partir de la démonstration de HealthClinic.biz hello, consultez [Démarrages rapides outils de développement Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).

## <a name="various-docker-tools"></a>Divers outils Docker
[D’excellents outils Docker (blog de Steve Lasker)](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a>Articles intéressants
[Présentation des tooMicroservices de NGINX](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a>Présentations
* [Steve Lasker : Visual Studio Live Las Vegas 2016 - E2E Docker](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [Introduction tooASP.NET Core @ build 2016 - où vous à démonstration](https://channel9.msdn.com/Events/Build/2016/B810)
* [Développement d’applications .NET dans des conteneurs, Channel 9](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
