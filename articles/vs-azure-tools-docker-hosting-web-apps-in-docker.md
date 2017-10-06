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
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a>Déployer un hôte Docker distant tooa ASP.NET conteneur
## <a name="overview"></a>Vue d'ensemble
Docker est un moteur de conteneur léger, semblable dans une machine virtuelle de façons tooa, que vous pouvez utiliser toohost applications et services.
Ce didacticiel vous guide à l’aide de hello [Visual Studio Tools pour Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension toodeploy un hôte Docker de ASP.NET Core application tooa sur Azure à l’aide de PowerShell.

## <a name="prerequisites"></a>Composants requis
suivant de Hello est requis toocomplete ce didacticiel :

* Créez une machine virtuelle d’hôte Docker Azure comme décrit dans [comment toouse docker-machine avec Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Installer la version la plus récente de hello [Visual Studio](https://www.visualstudio.com/downloads/)
* Télécharger hello [Kit de développement logiciel Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)
* Installer [Docker pour Windows](https://docs.docker.com/docker-for-windows/install/)

## <a name="1-create-an-aspnet-core-web-app"></a>1. Créez une application web ASP.NET Core
Hello suit guide de création d’une application ASP.NET Core base qui sera utilisée dans ce didacticiel.

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Ajouter la prise en charge Docker
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a>3. Utilisez hello DockerTask.ps1 de PowerShell Script
1. Ouvrez un répertoire de racine toohello Invite PowerShell de votre projet. 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. Valider les hôte distant hello sont en cours d’exécution. L’état (State) doit indiquer « Running » (En cours d’exécution) 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. À l’aide de build hello application hello - paramètre de Build
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. Exécutez l’application hello, à l’aide de hello - paramètre d’exécution
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   Une fois que docker est terminée, vous devez voir s’afficher des résultats similaires toohello :
   
   ![Affichez votre application][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
