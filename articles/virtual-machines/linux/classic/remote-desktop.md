---
title: tooa de bureau aaaRemote Linux VM | Documents Microsoft
description: "Découvrez comment tooinstall et configurer le Bureau à distance tooconnect tooa la machine virtuelle Linux Microsoft Azure pour le modèle de déploiement classique de hello"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a>À l’aide du Bureau à distance tooconnect tooa la machine virtuelle Linux Microsoft Azure
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour hello mis à jour la version du Gestionnaire de ressources de cet article, consultez [ici](../use-remote-desktop.md).

## <a name="overview"></a>Vue d'ensemble
Le protocole RDP (Remote Desktop Protocol) est un protocole propriétaire utilisé pour Windows. Comment pouvons-nous utiliser RDP tooconnect tooa Linux VM (machine virtuelle) à distance ?

Ce guide vous donnera hello réponse ! Il vous permettra de xrdp tooinstall et de configuration sur votre Microsoft Azure machine virtuelle Linux, ce qui vous permet de connecter tooit avec le Bureau à distance à partir d’un ordinateur Windows. Nous allons utiliser VM Linux en cours d’exécution Ubuntu ou OpenSUSE comme exemple hello dans ce guide.

outil de xrdp Hello est open source serveur RDP qui vous permet de tooconnect votre serveur Linux avec le Bureau à distance à partir d’un ordinateur Windows. Le protocole RDP fonctionne mieux que VNC (Virtual Network Computing). VNC affiche des graphiques de qualité JPEG et peut être lent, alors que RDP est rapide et parfaitement net.

> [!NOTE]
> Vous devez déjà disposer d’une machine virtuelle Microsoft Azure exécutant Linux. toocreate et configurer un VM Linux, consultez hello [didacticiel de la machine virtuelle de Azure Linux](createportal.md).
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a>Créer un point de terminaison pour le Bureau à distance
Nous allons utiliser le point de terminaison par défaut hello 3389 pour Bureau à distance dans le présent document. Définir des points de terminaison 3389 comme `Remote Desktop` tooyour Linux VM comme ci-dessous :

![image](./media/remote-desktop/endpoint-for-linux-server.png)

Si vous ne savez pas comment tooset un point de terminaison pour votre machine virtuelle, consultez [ce guide](setup-endpoints.md).

## <a name="install-gnome-desktop"></a>Installer Gnome Desktop
Se connecter tooyour Linux VM via `putty`et installez `Gnome Desktop`.

Pour Ubuntu, procédez comme suit :

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


Pour OpenSUSE, utilisez :

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>Installer xdrp
Pour Ubuntu, procédez comme suit :

    #sudo apt-get install xrdp

Pour OpenSUSE, utilisez :

> [!NOTE]
> Mettre à jour de version de OpenSUSE hello avec version hello que vous utilisez Bonjour commande suivante. exemple Hello ci-dessous est pour `OpenSUSE 13.2`.
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>Démarrez xrdp et paramétrez le service xdrp au démarrage
Pour OpenSUSE, utilisez :

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

Pour Ubuntu, xrdp sera démarré et activé au démarrage automatiquement après l’installation.

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a>Utilisation de xfce si vous utilisez une version d’Ubuntu ultérieure à 12.04LTS
Version actuelle de hello de xrdp ne prenant pas en charge Gnome Desktop pour les versions d’Ubuntu Ubuntu 12.04LTS au plus tard, nous allons utiliser `xfce` Desktop à la place.

tooinstall `xfce`, utilisez la commande :

    #sudo apt-get install xubuntu-desktop

Activez ensuite `xfce` à l’aide de cette commande :

    #echo xfce4-session >~/.xsession

Modifier le fichier de configuration hello `/etc/xrdp/startwm.sh`:

    #sudo vi /etc/xrdp/startwm.sh   

Ajoutez la ligne de hello `xfce4-session` avant la ligne de hello `/etc/X11/Xsession`.

toorestart hello xrdp service, utilisez ceci :

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>Connectez votre machine virtuelle Linux à partir d’un ordinateur Windows
Sur un ordinateur Windows, démarre le client du Bureau à distance hello et entrer votre nom DNS de machine virtuelle Linux. Ou accédez toohello tableau de bord de votre machine virtuelle dans hello portail Azure, cliquez sur `Connect` tooconnect votre VM Linux. Dans ce cas, vous consultez la fenêtre de connexion hello :

![image](./media/remote-desktop/no2.png)

Connectez-vous avec le nom d’utilisateur hello et un mot de passe de votre VM Linux.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation de xrdp, consultez [http://www.xrdp.org/](http://www.xrdp.org/).
