---
title: "aaaConfigure un hôte Docker avec VirtualBox | Documents Microsoft"
description: "Tooconfigure des instructions détaillées de l’instance par défaut Docker à l’aide d’une Machine Docker et VirtualBox"
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
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="fd661-103">Configurer un hôte Docker avec VirtualBox</span><span class="sxs-lookup"><span data-stu-id="fd661-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="fd661-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="fd661-104">Overview</span></span>
<span data-ttu-id="fd661-105">Cet article vous guide tout au long de la configuration d'une instance Docker par défaut à l'aide de Docker Machine et de VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="fd661-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="fd661-106">Si vous utilisez hello [Docker pour Windows version bêta](http://beta.docker.com/), cette configuration n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fd661-106">If you’re using hello [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd661-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fd661-107">Prerequisites</span></span>
<span data-ttu-id="fd661-108">Hello outils suivants doivent toobe installé.</span><span class="sxs-lookup"><span data-stu-id="fd661-108">hello following tools need toobe installed.</span></span>

* [<span data-ttu-id="fd661-109">Boîte à outils Docker</span><span class="sxs-lookup"><span data-stu-id="fd661-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a><span data-ttu-id="fd661-110">Configuration du client de Docker de hello avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd661-110">Configuring hello Docker client with Windows PowerShell</span></span>
<span data-ttu-id="fd661-111">tooconfigure un client Docker, simplement ouvrir Windows PowerShell et exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd661-111">tooconfigure a Docker client, simply open Windows PowerShell, and perform hello following steps:</span></span>

1. <span data-ttu-id="fd661-112">Créez une instance hôte docker par défaut.</span><span class="sxs-lookup"><span data-stu-id="fd661-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="fd661-113">Vérifiez l’instance par défaut de hello est configuré et en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fd661-113">Verify hello default instance is configured and running.</span></span> <span data-ttu-id="fd661-114">Vous devriez voir une instance nommée « par défaut » en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fd661-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![Sortie docker-machine ls][0]
3. <span data-ttu-id="fd661-116">Par défaut en tant qu’ordinateur hôte actuel de hello et configurez votre interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="fd661-116">Set default as hello current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="fd661-117">Afficher les conteneurs Docker Directory hello.</span><span class="sxs-lookup"><span data-stu-id="fd661-117">Display hello active Docker containers.</span></span> <span data-ttu-id="fd661-118">liste de Hello doit être vide.</span><span class="sxs-lookup"><span data-stu-id="fd661-118">hello list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![Sortie docker ps][1]

> [!NOTE]
> <span data-ttu-id="fd661-120">Chaque fois que vous redémarrez votre ordinateur de développement, vous devez toorestart l’hôte docker local.</span><span class="sxs-lookup"><span data-stu-id="fd661-120">Each time you reboot your development machine, you’ll need toorestart your local docker host.</span></span>
> <span data-ttu-id="fd661-121">toodo, hello problème commande à l’invite de commande suivante : `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="fd661-121">toodo this, issue hello following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
