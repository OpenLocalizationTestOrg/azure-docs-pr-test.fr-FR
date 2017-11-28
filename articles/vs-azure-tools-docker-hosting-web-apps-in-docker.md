---
title: "aaaDeploy un hôte Docker distant ASP.NET Core Linux Docker conteneur tooa | Documents Microsoft"
description: "Découvrez comment toouse Visual Studio Tools pour Docker toodeploy une ASP.NET Core web conteneur Docker de tooa application en cours d’exécution sur une machine virtuelle de Azure Docker hôte Linux"
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
ms.openlocfilehash: 27b0c6420628c73220200bc071b47a4cd89fff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a><span data-ttu-id="9e831-103">Déployer un hôte Docker distant tooa ASP.NET conteneur</span><span class="sxs-lookup"><span data-stu-id="9e831-103">Deploy an ASP.NET container tooa remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="9e831-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9e831-104">Overview</span></span>
<span data-ttu-id="9e831-105">Docker est un moteur de conteneur léger, semblable dans une machine virtuelle de façons tooa, que vous pouvez utiliser toohost applications et services.</span><span class="sxs-lookup"><span data-stu-id="9e831-105">Docker is a lightweight container engine, similar in some ways tooa virtual machine, which you can use toohost applications and services.</span></span>
<span data-ttu-id="9e831-106">Ce didacticiel vous guide à l’aide de hello [Visual Studio Tools pour Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension toodeploy un hôte Docker de ASP.NET Core application tooa sur Azure à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e831-106">This tutorial walks you through using hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension toodeploy an ASP.NET Core app tooa Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e831-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9e831-107">Prerequisites</span></span>
<span data-ttu-id="9e831-108">suivant de Hello est requis toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="9e831-108">hello following is required toocomplete this tutorial:</span></span>

* <span data-ttu-id="9e831-109">Créez une machine virtuelle d’hôte Docker Azure comme décrit dans [comment toouse docker-machine avec Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9e831-109">Create an Azure Docker Host VM as described in [How toouse docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="9e831-110">Installer la version la plus récente de hello [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="9e831-110">Install hello latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="9e831-111">Télécharger hello [Kit de développement logiciel Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="9e831-111">Download hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="9e831-112">Installer [Docker pour Windows](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="9e831-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="9e831-113">1. Créez une application web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="9e831-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="9e831-114">Hello suit guide de création d’une application ASP.NET Core base qui sera utilisée dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9e831-114">hello following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="9e831-115">2. Ajouter la prise en charge Docker</span><span class="sxs-lookup"><span data-stu-id="9e831-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a><span data-ttu-id="9e831-116">3. Utilisez hello DockerTask.ps1 de PowerShell Script</span><span class="sxs-lookup"><span data-stu-id="9e831-116">3. Use hello DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="9e831-117">Ouvrez un répertoire de racine toohello Invite PowerShell de votre projet.</span><span class="sxs-lookup"><span data-stu-id="9e831-117">Open a PowerShell prompt toohello root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="9e831-118">Valider les hôte distant hello sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9e831-118">Validate hello remote host is running.</span></span> <span data-ttu-id="9e831-119">L’état (State) doit indiquer « Running » (En cours d’exécution)</span><span class="sxs-lookup"><span data-stu-id="9e831-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="9e831-120">À l’aide de build hello application hello - paramètre de Build</span><span class="sxs-lookup"><span data-stu-id="9e831-120">Build hello app using hello -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="9e831-121">Exécutez l’application hello, à l’aide de hello - paramètre d’exécution</span><span class="sxs-lookup"><span data-stu-id="9e831-121">Run hello app, using hello -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="9e831-122">Une fois que docker est terminée, vous devez voir s’afficher des résultats similaires toohello :</span><span class="sxs-lookup"><span data-stu-id="9e831-122">Once docker completes, you should see results similar toohello following:</span></span>
   
   ![Affichez votre application][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
