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
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="b6559-103">Résoudre des problèmes de développement avec Docker pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b6559-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="b6559-104">Lorsque vous travaillez avec Visual Studio Tools pour Docker Preview, vous pouvez rencontrer des problèmes en raison de la nature hello de version d’évaluation hello.</span><span class="sxs-lookup"><span data-stu-id="b6559-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of hello nature of hello preview.</span></span>
<span data-ttu-id="b6559-105">Voici quelques problèmes courants et leurs solutions.</span><span class="sxs-lookup"><span data-stu-id="b6559-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="b6559-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="b6559-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="b6559-107">**Conteneurs Linux**</span><span class="sxs-lookup"><span data-stu-id="b6559-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="b6559-108">Des erreurs de build se produisent lors du débogage d’une application de console ou web .NET Core</span><span class="sxs-lookup"><span data-stu-id="b6559-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="b6559-109">Cela peut être toonot connexe partage lecteur hello où se trouve le projet de hello avec Docker pour Windows.</span><span class="sxs-lookup"><span data-stu-id="b6559-109">This could be related toonot sharing hello drive where hello project resides with Docker for Windows.</span></span>  <span data-ttu-id="b6559-110">Vous pouvez recevoir l’erreur hello suivante :</span><span class="sxs-lookup"><span data-stu-id="b6559-110">You may receive an error like hello following:</span></span>

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="b6559-111">tooresolve ce problème :</span><span class="sxs-lookup"><span data-stu-id="b6559-111">tooresolve this issue:</span></span>

1. <span data-ttu-id="b6559-112">Avec le bouton droit **Docker pour Windows** dans hello la zone de notification, puis sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="b6559-112">Right-click **Docker for Windows** in hello notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="b6559-113">Sélectionnez **des lecteurs partagés** et partager lecteur hello où hello projet réside.</span><span class="sxs-lookup"><span data-stu-id="b6559-113">Select **Shared Drives** and share hello drive where hello project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="b6559-114">**Conteneurs Windows**</span><span class="sxs-lookup"><span data-stu-id="b6559-114">**Windows containers**</span></span>

<span data-ttu-id="b6559-115">Hello problèmes suivants sont applications de console et web de .NET Framework dans les conteneurs Windows toodebugging spécifique.</span><span class="sxs-lookup"><span data-stu-id="b6559-115">hello following issues are specific toodebugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="b6559-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b6559-116">Prerequisites</span></span>

1. <span data-ttu-id="b6559-117">Visual Studio 2017 RC (ou version ultérieure) avec hello .NET Core et la charge de travail aperçu du Docker doit être installé.</span><span class="sxs-lookup"><span data-stu-id="b6559-117">Visual Studio 2017 RC (or later) with hello .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="b6559-118">Mise à jour anniversaire de Windows 10 avec les derniers correctifs de mise à jour Windows.</span><span class="sxs-lookup"><span data-stu-id="b6559-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="b6559-119">En particulier [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) doit être installé.</span><span class="sxs-lookup"><span data-stu-id="b6559-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="b6559-120">[Docker pour Windows](https://docs.docker.com/docker-for-windows/) (version 1.13.0 ou version ultérieure) doit être installé.</span><span class="sxs-lookup"><span data-stu-id="b6559-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="b6559-121">**Basculer les conteneurs tooWindows** doit être sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="b6559-121">**Switch tooWindows containers** must be selected.</span></span> <span data-ttu-id="b6559-122">Dans la zone de notification de hello, cliquez sur **Docker pour Windows**, puis sélectionnez **basculer les conteneurs tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="b6559-122">In hello notification area, click **Docker for Windows**, and then select **Switch tooWindows containers**.</span></span> <span data-ttu-id="b6559-123">Après le redémarrage de l’ordinateur de hello, assurez-vous que ce paramètre est conservé.</span><span class="sxs-lookup"><span data-stu-id="b6559-123">After hello machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="b6559-124">La sortie de la console n’apparaît pas dans la fenêtre de sortie de Visual Studio pendant le débogage d’une application de console</span><span class="sxs-lookup"><span data-stu-id="b6559-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="b6559-125">Il s’agit d’un problème connu avec le débogueur de Visual Studio hello (msvsmon.exe), ce qui n’est actuellement pas conçu pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="b6559-125">This is a known issue with hello Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="b6559-126">La prise en charge de ce scénario peut être incluse dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b6559-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="b6559-127">sortie de toosee à partir de l’application de console hello dans Visual Studio, utilisez **Docker : démarrer le projet**, qui est équivalent**démarrer sans débogage**.</span><span class="sxs-lookup"><span data-stu-id="b6559-127">toosee output from hello console application in Visual Studio, use **Docker: Start Project**, which is equivalent too**Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="b6559-128">Échec de la configuration avec l’erreur (403) interdit de version de débogage d’applications web avec hello</span><span class="sxs-lookup"><span data-stu-id="b6559-128">Debugging web applications with hello release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="b6559-129">toowork ce problème, ouvrez web.release.config dans les solutions hello et commenter ou supprimer des hello lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6559-129">toowork around this issue, open web.release.config in hello solution and comment out or delete hello following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="b6559-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b6559-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="b6559-131">**Conteneurs Linux**</span><span class="sxs-lookup"><span data-stu-id="b6559-131">**Linux containers**</span></span>

#### <a name="unable-toovalidate-volume-mapping"></a><span data-ttu-id="b6559-132">Mappage du volume toovalidate Impossible</span><span class="sxs-lookup"><span data-stu-id="b6559-132">Unable toovalidate volume mapping</span></span>
<span data-ttu-id="b6559-133">Mappage du volume est le code source de hello tooshare requis et les fichiers binaires de votre application avec le dossier de l’application hello dans le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="b6559-133">Volume mapping is required tooshare hello source code and binaries of your application with hello app folder in hello container.</span></span>  <span data-ttu-id="b6559-134">Les mappages de volume spécifique sont contenus dans docker-compose.dev.debug.yml et docker-compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="b6559-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="b6559-135">Comme les fichiers modifiés sur votre ordinateur hôte, les conteneurs hello reflètent ces modifications dans une structure de dossiers similaire.</span><span class="sxs-lookup"><span data-stu-id="b6559-135">As files are changed on your host machine, hello containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="b6559-136">mappage du volume tooenable :</span><span class="sxs-lookup"><span data-stu-id="b6559-136">tooenable volume mapping:</span></span>

1. <span data-ttu-id="b6559-137">Cliquez sur **Moby** dans la zone de notification hello et sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="b6559-137">Click **Moby** in hello notification area and select **Settings**.</span></span>
2. <span data-ttu-id="b6559-138">Sélectionnez **Lecteurs partagés**.</span><span class="sxs-lookup"><span data-stu-id="b6559-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="b6559-139">Sélectionnez un lecteur qui héberge votre projet et hello le lecteur de résidence % USERPROFILE% hello.</span><span class="sxs-lookup"><span data-stu-id="b6559-139">Select hello drive that hosts your project and hello drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="b6559-140">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="b6559-140">Click **Apply**.</span></span>

<span data-ttu-id="b6559-141">tootest si le mappage du volume fonctionne, reconstruire et sélectionnez F5 à partir de Visual Studio après qu’un ou plusieurs disques partagés ou exécutez hello après le code à partir d’une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="b6559-141">tootest if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run hello following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="b6559-142">Cet exemple suppose que le dossier Utilisateurs se trouve sur le lecteur C et qu’il a été partagé.</span><span class="sxs-lookup"><span data-stu-id="b6559-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="b6559-143">Le cas échéant, procédez à une révision si vous avez partagé un autre lecteur.</span><span class="sxs-lookup"><span data-stu-id="b6559-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="b6559-144">Exécutez hello suivant de code dans le conteneur de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="b6559-144">Run hello following code in hello Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="b6559-145">Vous devez voir une liste de hello utilisateurs et des dossiers publics de répertoires.</span><span class="sxs-lookup"><span data-stu-id="b6559-145">You should see a directory listing from hello Users/Public folder.</span></span> <span data-ttu-id="b6559-146">Si aucun fichier ne s’affiche et que votre dossier /c/Users/Public n’est pas vide, le mappage des volumes n’est pas configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="b6559-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="b6559-147">Modifier toohello repère toosee hello le contenu du répertoire de hello `/c/Users/Public` active :</span><span class="sxs-lookup"><span data-stu-id="b6559-147">Change toohello wormhole directory toosee hello contents of hello `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="b6559-148">Lorsque vous travaillez avec les machines virtuelles Linux, le système de fichiers de conteneur hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="b6559-148">When you're working with Linux VMs, hello container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="b6559-149">Build : échec inattendu de la tâche PrepareForBuild</span><span class="sxs-lookup"><span data-stu-id="b6559-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="b6559-150">Microsoft.DotNet.Docker.CommandLine.ClientException : Une erreur s’est produite lors de la tentative de tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b6559-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying tooconnect.</span></span>

<span data-ttu-id="b6559-151">Vérifiez que cet hôte de Docker hello par défaut est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b6559-151">Verify that hello default Docker host is running.</span></span> <span data-ttu-id="b6559-152">Ouvrez une invite de commandes et exécutez :</span><span class="sxs-lookup"><span data-stu-id="b6559-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="b6559-153">Si elle retourne une erreur, puis essayez de toostart hello **Docker pour Windows** application de bureau.</span><span class="sxs-lookup"><span data-stu-id="b6559-153">If this returns an error, then attempt toostart hello **Docker for Windows** desktop app.</span></span> <span data-ttu-id="b6559-154">Si l’application de bureau hello est en cours d’exécution, puis **Moby** doit être visible dans la zone de notification hello.</span><span class="sxs-lookup"><span data-stu-id="b6559-154">If hello desktop app is running, then **Moby** should be visible in hello notification area.</span></span> <span data-ttu-id="b6559-155">Cliquez avec le bouton droit sur **Moby**, puis ouvrez **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="b6559-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="b6559-156">Cliquez sur **Réinitialiser**, puis redémarrez Docker.</span><span class="sxs-lookup"><span data-stu-id="b6559-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="b6559-157">Une boîte de dialogue d’erreur se produit lors de la tentative de tooadd prise en charge Docker ou débogage (F5) une application ASP.NET Core dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="b6559-157">An error dialog occurs when attempting tooadd Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="b6559-158">Après la désinstallation et installation des extensions, hello cache Managed Extensibility Framework (MEF) dans Visual Studio peut être endommagé.</span><span class="sxs-lookup"><span data-stu-id="b6559-158">After uninstalling and installing extensions, hello Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="b6559-159">Lorsque cela se produit, elle peut entraîner plusieurs messages d’erreur lorsque vous êtes Ajout d’un Support Docker et/ou tentative toorun ou débogage (F5) de votre application ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="b6559-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting toorun or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="b6559-160">En tant que solution de contournement temporaire, utilisez hello suivant les étapes toodelete et régénérez hello MEF la mémoire cache.</span><span class="sxs-lookup"><span data-stu-id="b6559-160">As a temporary workaround, use hello following steps toodelete and regenerate hello MEF cache.</span></span>

1. <span data-ttu-id="b6559-161">Fermez toutes les instances de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6559-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="b6559-162">Ouvrez %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="b6559-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="b6559-163">Supprimer hello suivant des dossiers :</span><span class="sxs-lookup"><span data-stu-id="b6559-163">Delete hello following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="b6559-164">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6559-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="b6559-165">Essayez à nouveau de scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="b6559-165">Attempt hello scenario again.</span></span>
