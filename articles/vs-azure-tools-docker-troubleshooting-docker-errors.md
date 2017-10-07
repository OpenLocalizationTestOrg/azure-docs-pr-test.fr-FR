---
title: "aaaTroubleshooting erreurs du client Docker sur Windows à l’aide de Visual Studio | Documents Microsoft"
description: "Résoudre les problèmes rencontrés lors de l’utilisation de Visual Studio toocreate et déployer tooDocker d’applications web sur Windows à l’aide de Visual Studio."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a>Résoudre des problèmes de développement avec Docker pour Visual Studio

Lorsque vous travaillez avec Visual Studio Tools pour Docker Preview, vous pouvez rencontrer des problèmes en raison de la nature hello de version d’évaluation hello.
Voici quelques problèmes courants et leurs solutions.  

## <a name="visual-studio-2017-rc"></a>Visual Studio 2017 RC

### <a name="linux-containers"></a>**Conteneurs Linux**

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a>Des erreurs de build se produisent lors du débogage d’une application de console ou web .NET Core  

Cela peut être toonot connexe partage lecteur hello où se trouve le projet de hello avec Docker pour Windows.  Vous pouvez recevoir l’erreur hello suivante :

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
tooresolve ce problème :

1. Avec le bouton droit **Docker pour Windows** dans hello la zone de notification, puis sélectionnez **paramètres**.  
2. Sélectionnez **des lecteurs partagés** et partager lecteur hello où hello projet réside.

### <a name="windows-containers"></a>**Conteneurs Windows**

Hello problèmes suivants sont applications de console et web de .NET Framework dans les conteneurs Windows toodebugging spécifique.

#### <a name="prerequisites"></a>Composants requis

1. Visual Studio 2017 RC (ou version ultérieure) avec hello .NET Core et la charge de travail aperçu du Docker doit être installé.
2. Mise à jour anniversaire de Windows 10 avec les derniers correctifs de mise à jour Windows. En particulier [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) doit être installé. 
3. [Docker pour Windows](https://docs.docker.com/docker-for-windows/) (version 1.13.0 ou version ultérieure) doit être installé.
4. **Basculer les conteneurs tooWindows** doit être sélectionnée. Dans la zone de notification de hello, cliquez sur **Docker pour Windows**, puis sélectionnez **basculer les conteneurs tooWindows**. Après le redémarrage de l’ordinateur de hello, assurez-vous que ce paramètre est conservé.

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a>La sortie de la console n’apparaît pas dans la fenêtre de sortie de Visual Studio pendant le débogage d’une application de console

Il s’agit d’un problème connu avec le débogueur de Visual Studio hello (msvsmon.exe), ce qui n’est actuellement pas conçu pour ce scénario. La prise en charge de ce scénario peut être incluse dans une version ultérieure. sortie de toosee à partir de l’application de console hello dans Visual Studio, utilisez **Docker : démarrer le projet**, qui est équivalent**démarrer sans débogage**.

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a>Échec de la configuration avec l’erreur (403) interdit de version de débogage d’applications web avec hello

toowork ce problème, ouvrez web.release.config dans les solutions hello et commenter ou supprimer des hello lignes suivantes :

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a>Visual Studio 2015

### <a name="linux-containers"></a>**Conteneurs Linux**

#### <a name="unable-toovalidate-volume-mapping"></a>Mappage du volume toovalidate Impossible
Mappage du volume est le code source de hello tooshare requis et les fichiers binaires de votre application avec le dossier de l’application hello dans le conteneur de hello.  Les mappages de volume spécifique sont contenus dans docker-compose.dev.debug.yml et docker-compose.dev.release.yml. Comme les fichiers modifiés sur votre ordinateur hôte, les conteneurs hello reflètent ces modifications dans une structure de dossiers similaire.

mappage du volume tooenable :

1. Cliquez sur **Moby** dans la zone de notification hello et sélectionnez **paramètres**.
2. Sélectionnez **Lecteurs partagés**.
3. Sélectionnez un lecteur qui héberge votre projet et hello le lecteur de résidence % USERPROFILE% hello.
4. Cliquez sur **Apply**.

tootest si le mappage du volume fonctionne, reconstruire et sélectionnez F5 à partir de Visual Studio après qu’un ou plusieurs disques partagés ou exécutez hello après le code à partir d’une invite de commandes.

> [!NOTE]
> Cet exemple suppose que le dossier Utilisateurs se trouve sur le lecteur C et qu’il a été partagé.
> Le cas échéant, procédez à une révision si vous avez partagé un autre lecteur.

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

Exécutez hello suivant de code dans le conteneur de Linux hello.

```
/ # ls
```

Vous devez voir une liste de hello utilisateurs et des dossiers publics de répertoires. Si aucun fichier ne s’affiche et que votre dossier /c/Users/Public n’est pas vide, le mappage des volumes n’est pas configuré correctement.

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

Modifier toohello repère toosee hello le contenu du répertoire de hello `/c/Users/Public` active :

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> Lorsque vous travaillez avec les machines virtuelles Linux, le système de fichiers de conteneur hello respecte la casse.

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a>Build : échec inattendu de la tâche PrepareForBuild

Microsoft.DotNet.Docker.CommandLine.ClientException : Une erreur s’est produite lors de la tentative de tooconnect.

Vérifiez que cet hôte de Docker hello par défaut est en cours d’exécution. Ouvrez une invite de commandes et exécutez :

```
docker info
```

Si elle retourne une erreur, puis essayez de toostart hello **Docker pour Windows** application de bureau. Si l’application de bureau hello est en cours d’exécution, puis **Moby** doit être visible dans la zone de notification hello. Cliquez avec le bouton droit sur **Moby**, puis ouvrez **Paramètres**. Cliquez sur **Réinitialiser**, puis redémarrez Docker.

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a>Une boîte de dialogue d’erreur se produit lors de la tentative de tooadd prise en charge Docker ou débogage (F5) une application ASP.NET Core dans un conteneur

Après la désinstallation et installation des extensions, hello cache Managed Extensibility Framework (MEF) dans Visual Studio peut être endommagé. Lorsque cela se produit, elle peut entraîner plusieurs messages d’erreur lorsque vous êtes Ajout d’un Support Docker et/ou tentative toorun ou débogage (F5) de votre application ASP.NET Core. En tant que solution de contournement temporaire, utilisez hello suivant les étapes toodelete et régénérez hello MEF la mémoire cache.

1. Fermez toutes les instances de Visual Studio.
1. Ouvrez %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.
1. Supprimer hello suivant des dossiers :
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. Ouvrez Visual Studio.
1. Essayez à nouveau de scénario de hello.
