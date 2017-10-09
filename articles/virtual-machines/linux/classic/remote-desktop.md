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
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a><span data-ttu-id="bcb69-103">À l’aide du Bureau à distance tooconnect tooa la machine virtuelle Linux Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="bcb69-103">Using Remote Desktop tooconnect tooa Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="bcb69-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bcb69-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bcb69-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="bcb69-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="bcb69-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="bcb69-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="bcb69-107">Pour hello mis à jour la version du Gestionnaire de ressources de cet article, consultez [ici](../use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="bcb69-107">For hello updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="bcb69-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bcb69-108">Overview</span></span>
<span data-ttu-id="bcb69-109">Le protocole RDP (Remote Desktop Protocol) est un protocole propriétaire utilisé pour Windows.</span><span class="sxs-lookup"><span data-stu-id="bcb69-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="bcb69-110">Comment pouvons-nous utiliser RDP tooconnect tooa Linux VM (machine virtuelle) à distance ?</span><span class="sxs-lookup"><span data-stu-id="bcb69-110">How can we use RDP tooconnect tooa Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="bcb69-111">Ce guide vous donnera hello réponse !</span><span class="sxs-lookup"><span data-stu-id="bcb69-111">This guidance will give you hello answer!</span></span> <span data-ttu-id="bcb69-112">Il vous permettra de xrdp tooinstall et de configuration sur votre Microsoft Azure machine virtuelle Linux, ce qui vous permet de connecter tooit avec le Bureau à distance à partir d’un ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="bcb69-112">It will help you tooinstall and config xrdp on your Microsoft Azure Linux VM, which lets you connect tooit with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="bcb69-113">Nous allons utiliser VM Linux en cours d’exécution Ubuntu ou OpenSUSE comme exemple hello dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="bcb69-113">We will use Linux VM running Ubuntu or OpenSUSE as hello example in this guidance.</span></span>

<span data-ttu-id="bcb69-114">outil de xrdp Hello est open source serveur RDP qui vous permet de tooconnect votre serveur Linux avec le Bureau à distance à partir d’un ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="bcb69-114">hello xrdp tool is an open source RDP server that allows you tooconnect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="bcb69-115">Le protocole RDP fonctionne mieux que VNC (Virtual Network Computing).</span><span class="sxs-lookup"><span data-stu-id="bcb69-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="bcb69-116">VNC affiche des graphiques de qualité JPEG et peut être lent, alors que RDP est rapide et parfaitement net.</span><span class="sxs-lookup"><span data-stu-id="bcb69-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="bcb69-117">Vous devez déjà disposer d’une machine virtuelle Microsoft Azure exécutant Linux.</span><span class="sxs-lookup"><span data-stu-id="bcb69-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="bcb69-118">toocreate et configurer un VM Linux, consultez hello [didacticiel de la machine virtuelle de Azure Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="bcb69-118">toocreate and set up a Linux VM, see hello [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="bcb69-119">Créer un point de terminaison pour le Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="bcb69-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="bcb69-120">Nous allons utiliser le point de terminaison par défaut hello 3389 pour Bureau à distance dans le présent document. Définir des points de terminaison 3389 comme `Remote Desktop` tooyour Linux VM comme ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="bcb69-120">We will use hello default endpoint 3389 for Remote Desktop in this doc. Set up 3389 endpoint as `Remote Desktop` tooyour Linux VM like below:</span></span>

![image](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="bcb69-122">Si vous ne savez pas comment tooset un point de terminaison pour votre machine virtuelle, consultez [ce guide](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="bcb69-122">If you don't know how tooset up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="bcb69-123">Installer Gnome Desktop</span><span class="sxs-lookup"><span data-stu-id="bcb69-123">Install Gnome Desktop</span></span>
<span data-ttu-id="bcb69-124">Se connecter tooyour Linux VM via `putty`et installez `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="bcb69-124">Connect tooyour Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="bcb69-125">Pour Ubuntu, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcb69-125">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="bcb69-126">Pour OpenSUSE, utilisez :</span><span class="sxs-lookup"><span data-stu-id="bcb69-126">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="bcb69-127">Installer xdrp</span><span class="sxs-lookup"><span data-stu-id="bcb69-127">Install xrdp</span></span>
<span data-ttu-id="bcb69-128">Pour Ubuntu, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcb69-128">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="bcb69-129">Pour OpenSUSE, utilisez :</span><span class="sxs-lookup"><span data-stu-id="bcb69-129">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="bcb69-130">Mettre à jour de version de OpenSUSE hello avec version hello que vous utilisez Bonjour commande suivante.</span><span class="sxs-lookup"><span data-stu-id="bcb69-130">Update hello OpenSUSE version with hello version you are using in hello following command.</span></span> <span data-ttu-id="bcb69-131">exemple Hello ci-dessous est pour `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="bcb69-131">hello example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="bcb69-132">Démarrez xrdp et paramétrez le service xdrp au démarrage</span><span class="sxs-lookup"><span data-stu-id="bcb69-132">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="bcb69-133">Pour OpenSUSE, utilisez :</span><span class="sxs-lookup"><span data-stu-id="bcb69-133">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="bcb69-134">Pour Ubuntu, xrdp sera démarré et activé au démarrage automatiquement après l’installation.</span><span class="sxs-lookup"><span data-stu-id="bcb69-134">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="bcb69-135">Utilisation de xfce si vous utilisez une version d’Ubuntu ultérieure à 12.04LTS</span><span class="sxs-lookup"><span data-stu-id="bcb69-135">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="bcb69-136">Version actuelle de hello de xrdp ne prenant pas en charge Gnome Desktop pour les versions d’Ubuntu Ubuntu 12.04LTS au plus tard, nous allons utiliser `xfce` Desktop à la place.</span><span class="sxs-lookup"><span data-stu-id="bcb69-136">Because hello current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="bcb69-137">tooinstall `xfce`, utilisez la commande :</span><span class="sxs-lookup"><span data-stu-id="bcb69-137">tooinstall `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="bcb69-138">Activez ensuite `xfce` à l’aide de cette commande :</span><span class="sxs-lookup"><span data-stu-id="bcb69-138">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="bcb69-139">Modifier le fichier de configuration hello `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="bcb69-139">Edit hello config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="bcb69-140">Ajoutez la ligne de hello `xfce4-session` avant la ligne de hello `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="bcb69-140">Add hello line `xfce4-session` before hello line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="bcb69-141">toorestart hello xrdp service, utilisez ceci :</span><span class="sxs-lookup"><span data-stu-id="bcb69-141">toorestart hello xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="bcb69-142">Connectez votre machine virtuelle Linux à partir d’un ordinateur Windows</span><span class="sxs-lookup"><span data-stu-id="bcb69-142">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="bcb69-143">Sur un ordinateur Windows, démarre le client du Bureau à distance hello et entrer votre nom DNS de machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="bcb69-143">In a Windows machine, start hello Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="bcb69-144">Ou accédez toohello tableau de bord de votre machine virtuelle dans hello portail Azure, cliquez sur `Connect` tooconnect votre VM Linux.</span><span class="sxs-lookup"><span data-stu-id="bcb69-144">Or go toohello Dashboard of your VM in hello Azure portal and click `Connect` tooconnect your Linux VM.</span></span> <span data-ttu-id="bcb69-145">Dans ce cas, vous consultez la fenêtre de connexion hello :</span><span class="sxs-lookup"><span data-stu-id="bcb69-145">In that case, you see hello login window:</span></span>

![image](./media/remote-desktop/no2.png)

<span data-ttu-id="bcb69-147">Connectez-vous avec le nom d’utilisateur hello et un mot de passe de votre VM Linux.</span><span class="sxs-lookup"><span data-stu-id="bcb69-147">Log in with hello user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcb69-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcb69-148">Next steps</span></span>
<span data-ttu-id="bcb69-149">Pour plus d’informations sur l’utilisation de xrdp, consultez [http://www.xrdp.org/](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="bcb69-149">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
