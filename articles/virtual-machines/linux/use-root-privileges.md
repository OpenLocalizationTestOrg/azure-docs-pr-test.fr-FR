---
title: "Utilisation des privilèges racines sur les machines virtuelles Linux | Microsoft Docs"
description: "Apprenez à utiliser les privilèges root sur une machine virtuelle Linux dans Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: dc39db1f5fecffb60499a5420bfe72850e2fffd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="8746e-103">Utilisation des privilèges root sur les machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="8746e-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="8746e-104">Par défaut, l’utilisateur `root` est désactivé sur les machines virtuelles Linux dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8746e-104">By default, the `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="8746e-105">Les utilisateurs peuvent exécuter des commandes avec des privilèges élevés à l’aide de la commande `sudo` .</span><span class="sxs-lookup"><span data-stu-id="8746e-105">Users can run commands with elevated privileges by using the `sudo` command.</span></span> <span data-ttu-id="8746e-106">Toutefois, l'expérience peut varier en fonction du mode de déploiement du système.</span><span class="sxs-lookup"><span data-stu-id="8746e-106">However, the experience may vary depending on how the system was provisioned.</span></span>

1. <span data-ttu-id="8746e-107">**Clé SSH et mot de passe OU mot de passe uniquement :** la machine virtuelle a été déployée soit avec un certificat (fichier `.CER`) ou une clé SSH et un mot de passe, soit avec seulement un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8746e-107">**SSH key and password OR password only** - the virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="8746e-108">Dans ce cas, `sudo` demande le mot de passe de l’utilisateur avant d’exécuter la commande.</span><span class="sxs-lookup"><span data-stu-id="8746e-108">In this case `sudo` will prompt for the user's password before executing the command.</span></span>
2. <span data-ttu-id="8746e-109">**Clé SSH uniquement :** la machine virtuelle a été configurée avec un certificat (fichier `.cer`, `.pem` ou `.pub`) ou une clé SSH, mais sans mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8746e-109">**SSH key only** - the virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="8746e-110">Dans ce cas, `sudo` **ne demande pas** le mot de passe de l’utilisateur avant d’exécuter la commande.</span><span class="sxs-lookup"><span data-stu-id="8746e-110">In this case `sudo` **will not** prompt for the user's password before executing the command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="8746e-111">Clé SSH et mot de passe ou mot de passe uniquement</span><span class="sxs-lookup"><span data-stu-id="8746e-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="8746e-112">Connectez-vous à la machine virtuelle Linux à l’aide de l’authentification par clé SSH ou par mot de passe, puis exécutez les commandes à l’aide de `sudo`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="8746e-112">Log into the Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="8746e-113">Dans ce cas, l'utilisateur est invité à fournir un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8746e-113">In this case the user will be prompted for a password.</span></span> <span data-ttu-id="8746e-114">Une fois le mot de passe entré, `sudo` exécute la commande avec les privilèges `root`.</span><span class="sxs-lookup"><span data-stu-id="8746e-114">After entering the password `sudo` will run the command with `root` privileges.</span></span>

<span data-ttu-id="8746e-115">Vous pouvez également activer la méthode sudo sans mot de passe en modifiant le fichier `/etc/sudoers.d/waagent` , par exemple :</span><span class="sxs-lookup"><span data-stu-id="8746e-115">You can also enable passwordless sudo by editing the `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="8746e-116">Cette modification permet à l’utilisateur « azureuser » de poursuivre sans entrer de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8746e-116">This change will allow for passwordless sudo by the user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="8746e-117">Clé SSH uniquement</span><span class="sxs-lookup"><span data-stu-id="8746e-117">SSH Key Only</span></span>
<span data-ttu-id="8746e-118">Connectez-vous à la machine virtuelle Linux à l’aide de l’authentification par clé SSH, puis exécutez les commandes à l’aide de `sudo`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="8746e-118">Log into the Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="8746e-119">Dans ce cas, l'utilisateur **n'est pas** invité à fournir un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8746e-119">In this case the user will **not** be prompted for a password.</span></span> <span data-ttu-id="8746e-120">Une fois la touche `<enter>` activée, `sudo` exécute la commande avec les privilèges `root`.</span><span class="sxs-lookup"><span data-stu-id="8746e-120">After pressing `<enter>`, `sudo` will run the command with `root` privileges.</span></span>

