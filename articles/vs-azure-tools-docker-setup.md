---
title: "Configurer un hôte Docker avec VirtualBox | Microsoft Docs"
description: "Instructions pas à pas pour configurer une instance Docker par défaut à l'aide de Docker Machine et de VirtualBox."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: e9465afb560a73d74f853c19094b3ee75b8c470c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="e3915-103">Configurer un hôte Docker avec VirtualBox</span><span class="sxs-lookup"><span data-stu-id="e3915-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="e3915-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e3915-104">Overview</span></span>
<span data-ttu-id="e3915-105">Cet article vous guide tout au long de la configuration d'une instance Docker par défaut à l'aide de Docker Machine et de VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="e3915-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="e3915-106">Si vous utilisez la [version bêta de Docker pour Windows](http://beta.docker.com/), cette configuration n'est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e3915-106">If you’re using the [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3915-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e3915-107">Prerequisites</span></span>
<span data-ttu-id="e3915-108">Les outils suivants doivent être installés.</span><span class="sxs-lookup"><span data-stu-id="e3915-108">The following tools need to be installed.</span></span>

* [<span data-ttu-id="e3915-109">Boîte à outils Docker</span><span class="sxs-lookup"><span data-stu-id="e3915-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-the-docker-client-with-windows-powershell"></a><span data-ttu-id="e3915-110">Configuration du client Docker avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3915-110">Configuring the Docker client with Windows PowerShell</span></span>
<span data-ttu-id="e3915-111">Pour configurer un client Docker, ouvrez Windows PowerShell et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3915-111">To configure a Docker client, simply open Windows PowerShell, and perform the following steps:</span></span>

1. <span data-ttu-id="e3915-112">Créez une instance hôte docker par défaut.</span><span class="sxs-lookup"><span data-stu-id="e3915-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="e3915-113">Vérifiez que l'instance par défaut est configurée et en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="e3915-113">Verify the default instance is configured and running.</span></span> <span data-ttu-id="e3915-114">Vous devriez voir une instance nommée « par défaut » en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e3915-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![Sortie docker-machine ls][0]
3. <span data-ttu-id="e3915-116">Choisissez par défaut l'hôte actuel et configurez votre interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="e3915-116">Set default as the current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="e3915-117">Affichez les conteneurs Docker actifs.</span><span class="sxs-lookup"><span data-stu-id="e3915-117">Display the active Docker containers.</span></span> <span data-ttu-id="e3915-118">La liste doit être vide.</span><span class="sxs-lookup"><span data-stu-id="e3915-118">The list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![Sortie docker ps][1]

> [!NOTE]
> <span data-ttu-id="e3915-120">Chaque fois que vous redémarrez votre machine de développement, vous devrez également redémarrer votre hôte Docker local.</span><span class="sxs-lookup"><span data-stu-id="e3915-120">Each time you reboot your development machine, you’ll need to restart your local docker host.</span></span>
> <span data-ttu-id="e3915-121">Pour ce faire, exécutez la commande suivante à l’invite de commandes : `docker-machine start default`</span><span class="sxs-lookup"><span data-stu-id="e3915-121">To do this, issue the following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
