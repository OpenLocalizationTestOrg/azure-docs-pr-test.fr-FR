---
title: "Déployer un conteneur Linux Docker ASP.NET Core sur un hôte Docker distant | Microsoft Docs"
description: "Découvrez comment utiliser Visual Studio Tools pour Docker pour déployer une application web ASP.NET Core dans un conteneur Docker fonctionnant sur une machine virtuelle hôte Azure Docker"
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 4a87ee69f23779bf4f6f5db40bc05edbcfc7668d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-aspnet-container-to-a-remote-docker-host"></a><span data-ttu-id="61dd9-103">Déployer un conteneur ASP.NET sur un hôte Docker distant</span><span class="sxs-lookup"><span data-stu-id="61dd9-103">Deploy an ASP.NET container to a remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="61dd9-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="61dd9-104">Overview</span></span>
<span data-ttu-id="61dd9-105">Docker est un moteur de conteneur léger, semblable à certains égards à une machine virtuelle, que vous pouvez utiliser pour héberger des applications et des services.</span><span class="sxs-lookup"><span data-stu-id="61dd9-105">Docker is a lightweight container engine, similar in some ways to a virtual machine, which you can use to host applications and services.</span></span>
<span data-ttu-id="61dd9-106">Ce didacticiel vous guide dans l’utilisation de l’extension [Visual Studio Tools pour Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) pour déployer une application ASP.NET Core sur un hôte Docker sur Azure à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61dd9-106">This tutorial walks you through using the [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension to deploy an ASP.NET Core app to a Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61dd9-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="61dd9-107">Prerequisites</span></span>
<span data-ttu-id="61dd9-108">Ce qui suit est requis pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="61dd9-108">The following is required to complete this tutorial:</span></span>

* <span data-ttu-id="61dd9-109">Créer une machine virtuelle hôte Azure Docker, comme le décrit la rubrique [Utiliser Docker Machine avec Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="61dd9-109">Create an Azure Docker Host VM as described in [How to use docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="61dd9-110">Installer la dernière version de [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="61dd9-110">Install the latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="61dd9-111">Télécharger le [kit de développement logiciel (SDK) Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="61dd9-111">Download the [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="61dd9-112">Installer [Docker pour Windows](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="61dd9-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="61dd9-113">1. Créez une application web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="61dd9-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="61dd9-114">La procédure suivante vous accompagne dans la création d’une application ASP.NET Core qui sera utilisée dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="61dd9-114">The following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="61dd9-115">2. Ajouter la prise en charge Docker</span><span class="sxs-lookup"><span data-stu-id="61dd9-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-the-dockertaskps1-powershell-script"></a><span data-ttu-id="61dd9-116">3. Utilisez le Script PowerShell DockerTask.ps1</span><span class="sxs-lookup"><span data-stu-id="61dd9-116">3. Use the DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="61dd9-117">Ouvrez une invite de commandes PowerShell vers le répertoire racine de votre projet.</span><span class="sxs-lookup"><span data-stu-id="61dd9-117">Open a PowerShell prompt to the root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="61dd9-118">Confirmez l’exécution de l’hôte distant.</span><span class="sxs-lookup"><span data-stu-id="61dd9-118">Validate the remote host is running.</span></span> <span data-ttu-id="61dd9-119">L’état (State) doit indiquer « Running » (En cours d’exécution)</span><span class="sxs-lookup"><span data-stu-id="61dd9-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="61dd9-120">Générez l’application à l’aide du paramètre -Build</span><span class="sxs-lookup"><span data-stu-id="61dd9-120">Build the app using the -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="61dd9-121">Exécutez l’application à l’aide du paramètre -Run</span><span class="sxs-lookup"><span data-stu-id="61dd9-121">Run the app, using the -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="61dd9-122">Une fois Docker terminé, vous devriez obtenir un résultat semblable à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="61dd9-122">Once docker completes, you should see results similar to the following:</span></span>
   
   ![Affichez votre application][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
