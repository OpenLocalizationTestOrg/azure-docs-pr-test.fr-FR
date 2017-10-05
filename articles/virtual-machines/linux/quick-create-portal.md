---
title: "Démarrage rapide avec Azure - Portail pour la création d’une machine virtuelle | Microsoft Docs"
description: "Démarrage rapide avec Azure - Portail pour la création d’une machine virtuelle"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: d009020e86fdfed6a45b5b63b9664c623bcb1843
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="21cc3-103">Créer un groupe de machines virtuelles identiques Linux avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="21cc3-103">Create a Linux virtual machine with the Azure portal</span></span>

<span data-ttu-id="21cc3-104">Les machines virtuelles Azure peuvent être créées via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21cc3-104">Azure virtual machines can be created through the Azure portal.</span></span> <span data-ttu-id="21cc3-105">Cette méthode fournit une interface utilisateur basée sur navigateur pour créer et configurer des machines virtuelles et toutes les ressources liées.</span><span class="sxs-lookup"><span data-stu-id="21cc3-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="21cc3-106">Ce démarrage rapide décrit les étapes permettant de créer une machine virtuelle et d’installer un serveur web sur celle-ci.</span><span class="sxs-lookup"><span data-stu-id="21cc3-106">This Quickstart steps through creating a virtual machine and installing a webserver on the VM.</span></span>

<span data-ttu-id="21cc3-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="21cc3-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-ssh-key-pair"></a><span data-ttu-id="21cc3-108">Créer la paire de clés SSH</span><span class="sxs-lookup"><span data-stu-id="21cc3-108">Create SSH key pair</span></span>

<span data-ttu-id="21cc3-109">Vous avez besoin d’une paire de clés SSH pour effectuer ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="21cc3-109">You need an SSH key pair to complete this quick start.</span></span> <span data-ttu-id="21cc3-110">Si vous disposez déjà d’une paire de clés SSH, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="21cc3-110">If you have an existing SSH key pair, this step can be skipped.</span></span>

<span data-ttu-id="21cc3-111">Dans un interpréteur de commandes Bash, exécutez la commande suivante et suivez les instructions qui s’affichent à l’écran.</span><span class="sxs-lookup"><span data-stu-id="21cc3-111">From a Bash shell, run this command and follow the on-screen directions.</span></span> <span data-ttu-id="21cc3-112">La sortie de la commande inclut le nom du fichier de clé publique.</span><span class="sxs-lookup"><span data-stu-id="21cc3-112">The command output includes the file name of the public key file.</span></span> <span data-ttu-id="21cc3-113">Copiez le contenu du fichier de clé publique dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="21cc3-113">Copy the contents of the public key file to the clipboard.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-to-azure"></a><span data-ttu-id="21cc3-114">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="21cc3-114">Log in to Azure</span></span> 

<span data-ttu-id="21cc3-115">Connectez-vous au Portail Azure à l’adresse http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="21cc3-115">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="21cc3-116">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="21cc3-116">Create virtual machine</span></span>

1. <span data-ttu-id="21cc3-117">Cliquez sur le bouton **Nouveau** dans le coin supérieur gauche du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21cc3-117">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="21cc3-118">Sélectionnez **Compute**, puis sélectionnez **Ubuntu Server 16.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-118">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span></span> 

3. <span data-ttu-id="21cc3-119">Saisissez les informations de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="21cc3-119">Enter the virtual machine information.</span></span> <span data-ttu-id="21cc3-120">Dans **Type d’authentification**, sélectionnez **Clé publique SSH**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-120">For **Authentication type**, select **SSH public key**.</span></span> <span data-ttu-id="21cc3-121">Lorsque vous collez votre clé publique SSH, veillez à supprimer les espaces au début ou à la fin.</span><span class="sxs-lookup"><span data-stu-id="21cc3-121">When pasting in your SSH public key, take care to remove any leading or trailing white space.</span></span> <span data-ttu-id="21cc3-122">Lorsque vous avez terminé, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-122">When complete, click **OK**.</span></span>

    ![Saisie des informations de base sur votre machine virtuelle dans le panneau du portail](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. <span data-ttu-id="21cc3-124">Choisissez la taille de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="21cc3-124">Select a size for the VM.</span></span> <span data-ttu-id="21cc3-125">Pour voir plus de tailles, sélectionnez **Afficher tout** ou modifiez le filtre **Type de disque pris en charge**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-125">To see more sizes, select **View all** or change the **Supported disk type** filter.</span></span> 

    ![Capture d’écran montrant les tailles de machine virtuelle](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. <span data-ttu-id="21cc3-127">Conservez les valeurs par défaut dans le panneau des paramètres et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-127">On the settings blade, keep the defaults and click **OK**.</span></span>

6. <span data-ttu-id="21cc3-128">Sur la page Résumé, cliquez sur **OK** pour lancer le déploiement de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="21cc3-128">On the summary page, click **Ok** to start the virtual machine deployment.</span></span>

7. <span data-ttu-id="21cc3-129">La machine virtuelle sera épinglée au tableau de bord du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21cc3-129">The VM will be pinned to the Azure portal dashboard.</span></span> <span data-ttu-id="21cc3-130">Une fois le déploiement terminé, le volet de résumé de la machine virtuelle s’ouvre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="21cc3-130">Once the deployment has completed, the VM summary blade automatically opens.</span></span>


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="21cc3-131">Connexion à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="21cc3-131">Connect to virtual machine</span></span>

<span data-ttu-id="21cc3-132">Créez une connexion SSH avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="21cc3-132">Create an SSH connection with the virtual machine.</span></span>

1. <span data-ttu-id="21cc3-133">Cliquez sur le bouton **Connexion** dans le volet de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="21cc3-133">Click the **Connect** button on the virtual machine blade.</span></span> <span data-ttu-id="21cc3-134">Le bouton de connexion affiche une chaîne de connexion SSH qui peut être utilisée pour se connecter à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="21cc3-134">The connect button displays an SSH connection string that can be used to connect to the virtual machine.</span></span>

    ![Portail 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="21cc3-136">Exécutez la commande suivante pour créer une session SSH.</span><span class="sxs-lookup"><span data-stu-id="21cc3-136">Run the following command to create an SSH session.</span></span> <span data-ttu-id="21cc3-137">Remplacez la chaîne de connexion avec celle que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21cc3-137">Replace the connection string with the one you copied from the Azure portal.</span></span>

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a><span data-ttu-id="21cc3-138">Installer NGINX</span><span class="sxs-lookup"><span data-stu-id="21cc3-138">Install NGINX</span></span>

<span data-ttu-id="21cc3-139">Utilisez le script Bash suivant pour mettre à jour les sources de package et installer le dernier package NGINX.</span><span class="sxs-lookup"><span data-stu-id="21cc3-139">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="21cc3-140">Lorsque vous avez terminé, quittez la session SSH et revenez aux propriétés de la machine virtuelle dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21cc3-140">When done, exit the SSH session and return the VM properties in the Azure portal.</span></span>


## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="21cc3-141">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="21cc3-141">Open port 80 for web traffic</span></span> 

<span data-ttu-id="21cc3-142">Un groupe de sécurité réseau (NSG) sécurise les trafics entrant et sortant.</span><span class="sxs-lookup"><span data-stu-id="21cc3-142">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="21cc3-143">Lorsqu’une machine virtuelle est créée à partir du portail Azure, une règle de trafic entrant est créée sur le port 22 pour les connexions SSH.</span><span class="sxs-lookup"><span data-stu-id="21cc3-143">When a VM is created from the Azure portal, an inbound rule is created on port 22 for SSH connections.</span></span> <span data-ttu-id="21cc3-144">Comme cette machine virtuelle héberge un serveur web, vous devez créer une règle NSG pour le port 80.</span><span class="sxs-lookup"><span data-stu-id="21cc3-144">Because this VM hosts a webserver, an NSG rule needs to be created for port 80.</span></span>

1. <span data-ttu-id="21cc3-145">Sur la machine virtuelle, cliquez sur le nom du **Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-145">On the virtual machine, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="21cc3-146">Sélectionnez le **groupe de sécurité réseau**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-146">Select the **network security group**.</span></span> <span data-ttu-id="21cc3-147">Le groupe de sécurité réseau peut être identifié à l’aide de la colonne **Type**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-147">The NSG can be identified using the **Type** column.</span></span> 
3. <span data-ttu-id="21cc3-148">Dans le menu de gauche, sous Paramètres, cliquez sur **Règles de sécurité entrantes**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-148">On the left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="21cc3-149">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-149">Click on **Add**.</span></span>
5. <span data-ttu-id="21cc3-150">Dans **Nom**, tapez **http**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-150">In **Name**, type **http**.</span></span> <span data-ttu-id="21cc3-151">Assurez-vous que l’option **Plage de ports** est définie sur 80 et l’option **Action** sur **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-151">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span> 
6. <span data-ttu-id="21cc3-152">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-152">Click **OK**.</span></span>


## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="21cc3-153">Afficher la page d’accueil NGINX</span><span class="sxs-lookup"><span data-stu-id="21cc3-153">View the NGINX welcome page</span></span>

<span data-ttu-id="21cc3-154">Avec NGINX installé et le port 80 ouvert pour votre machine virtuelle, le serveur web est désormais accessible à partir d’internet.</span><span class="sxs-lookup"><span data-stu-id="21cc3-154">With NGINX installed, and port 80 open to your VM, the webserver can now be accessed from the internet.</span></span> <span data-ttu-id="21cc3-155">Ouvrez un navigateur web et saisissez l’adresse IP publique de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="21cc3-155">Open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="21cc3-156">L’adresse IP publique se trouve dans le panneau de la machine virtuelle sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21cc3-156">The public IP address can be found on the VM blade in the Azure portal.</span></span>

![Site par défaut NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="21cc3-158">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="21cc3-158">Clean up resources</span></span>

<span data-ttu-id="21cc3-159">Lorsque vous n’en avez plus besoin, supprimez le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="21cc3-159">When no longer needed, delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="21cc3-160">Pour ce faire, sélectionnez le groupe de ressources à partir du panneau de la machine virtuelle, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="21cc3-160">To do so, select the resource group from the virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21cc3-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="21cc3-161">Next steps</span></span>

<span data-ttu-id="21cc3-162">Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web.</span><span class="sxs-lookup"><span data-stu-id="21cc3-162">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="21cc3-163">Pour en savoir plus sur les machines virtuelles Azure, suivez le didacticiel pour les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="21cc3-163">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="21cc3-164">Didacticiels sur les machines virtuelles Azure Linux</span><span class="sxs-lookup"><span data-stu-id="21cc3-164">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
