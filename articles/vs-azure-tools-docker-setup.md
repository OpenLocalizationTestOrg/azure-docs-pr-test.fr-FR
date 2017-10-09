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
# <a name="configure-a-docker-host-with-virtualbox"></a>Configurer un hôte Docker avec VirtualBox
## <a name="overview"></a>Vue d'ensemble
Cet article vous guide tout au long de la configuration d'une instance Docker par défaut à l'aide de Docker Machine et de VirtualBox. Si vous utilisez hello [Docker pour Windows version bêta](http://beta.docker.com/), cette configuration n’est pas nécessaire.

## <a name="prerequisites"></a>Composants requis
Hello outils suivants doivent toobe installé.

* [Boîte à outils Docker](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a>Configuration du client de Docker de hello avec Windows PowerShell
tooconfigure un client Docker, simplement ouvrir Windows PowerShell et exécutez hello comme suit :

1. Créez une instance hôte docker par défaut.
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. Vérifiez l’instance par défaut de hello est configuré et en cours d’exécution. Vous devriez voir une instance nommée « par défaut » en cours d’exécution.
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![Sortie docker-machine ls][0]
3. Par défaut en tant qu’ordinateur hôte actuel de hello et configurez votre interpréteur de commandes.
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. Afficher les conteneurs Docker Directory hello. liste de Hello doit être vide.
   
    ```PowerShell
    docker ps
    ```
   
    ![Sortie docker ps][1]

> [!NOTE]
> Chaque fois que vous redémarrez votre ordinateur de développement, vous devez toorestart l’hôte docker local.
> toodo, hello problème commande à l’invite de commande suivante : `docker-machine start default`.
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
