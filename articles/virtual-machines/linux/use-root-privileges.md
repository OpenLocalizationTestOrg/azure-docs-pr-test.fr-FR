---
title: "aaaUse des privilèges de racine sur les ordinateurs virtuels Linux | Documents Microsoft"
description: "Découvrez comment toouse racine des privilèges sur un ordinateur virtuel de Linux dans Azure."
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
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="ff383-103">Utilisation des privilèges root sur les machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="ff383-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ff383-104">Par défaut, hello `root` utilisateur est désactivé sur les ordinateurs virtuels Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ff383-104">By default, hello `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="ff383-105">Les utilisateurs peuvent exécuter des commandes avec des privilèges élevés à l’aide de hello `sudo` commande.</span><span class="sxs-lookup"><span data-stu-id="ff383-105">Users can run commands with elevated privileges by using hello `sudo` command.</span></span> <span data-ttu-id="ff383-106">Toutefois, l’expérience de hello peut-être varier en fonction du mode de configuration de système de hello.</span><span class="sxs-lookup"><span data-stu-id="ff383-106">However, hello experience may vary depending on how hello system was provisioned.</span></span>

1. <span data-ttu-id="ff383-107">**Clé SSH et le mot de passe ou uniquement** -hello virtual machine a été configurée avec un certificat de soit (`.CER` fichier) ou clé SSH ainsi un mot de passe, ou simplement un nom d’utilisateur et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ff383-107">**SSH key and password OR password only** - hello virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="ff383-108">Dans ce cas `sudo` demandera hello mot de passe utilisateur avant d’exécuter la commande hello.</span><span class="sxs-lookup"><span data-stu-id="ff383-108">In this case `sudo` will prompt for hello user's password before executing hello command.</span></span>
2. <span data-ttu-id="ff383-109">**Uniquement la clé SSH** -hello virtual machine a été configurée avec un certificat (`.cer`, `.pem`, ou `.pub` fichier) ou la clé SSH, mais aucun mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ff383-109">**SSH key only** - hello virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="ff383-110">Dans ce cas `sudo` **ne seront pas** demander hello mot de passe utilisateur avant d’exécuter la commande hello.</span><span class="sxs-lookup"><span data-stu-id="ff383-110">In this case `sudo` **will not** prompt for hello user's password before executing hello command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="ff383-111">Clé SSH et mot de passe ou mot de passe uniquement</span><span class="sxs-lookup"><span data-stu-id="ff383-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="ff383-112">Se connecter à la machine virtuelle de hello Linux à l’aide de l’authentification par mot de passe ou clé SSH, puis exécuter des commandes à l’aide de `sudo`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="ff383-112">Log into hello Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="ff383-113">Dans ce cas les utilisateur hello demandera un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ff383-113">In this case hello user will be prompted for a password.</span></span> <span data-ttu-id="ff383-114">Après avoir entré un mot de passe hello `sudo` exécutera commande hello avec `root` des privilèges.</span><span class="sxs-lookup"><span data-stu-id="ff383-114">After entering hello password `sudo` will run hello command with `root` privileges.</span></span>

<span data-ttu-id="ff383-115">Vous pouvez également activer sudo passwordless en modifiant hello `/etc/sudoers.d/waagent` de fichiers, par exemple :</span><span class="sxs-lookup"><span data-stu-id="ff383-115">You can also enable passwordless sudo by editing hello `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="ff383-116">Cette modification permettra sudo passwordless par l’utilisateur hello « azureuser ».</span><span class="sxs-lookup"><span data-stu-id="ff383-116">This change will allow for passwordless sudo by hello user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="ff383-117">Clé SSH uniquement</span><span class="sxs-lookup"><span data-stu-id="ff383-117">SSH Key Only</span></span>
<span data-ttu-id="ff383-118">Se connecter à la machine virtuelle de hello Linux à l’aide de l’authentification par clé SSH, puis exécuter des commandes à l’aide de `sudo`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="ff383-118">Log into hello Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="ff383-119">Dans ce cas les utilisateur hello seront **pas** être invité à entrer un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ff383-119">In this case hello user will **not** be prompted for a password.</span></span> <span data-ttu-id="ff383-120">Après avoir appuyé sur `<enter>`, `sudo` exécutera commande hello avec `root` des privilèges.</span><span class="sxs-lookup"><span data-stu-id="ff383-120">After pressing `<enter>`, `sudo` will run hello command with `root` privileges.</span></span>

