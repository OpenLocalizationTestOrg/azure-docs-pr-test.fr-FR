---
title: "aaaAzure démarrage rapide : créer un portail de machine virtuelle Windows | Documents Microsoft"
description: "Démarrage rapide avec Azure - Portail pour la création d’une machine virtuelle Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="68b4f-103">Créer une machine virtuelle Windows avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="68b4f-103">Create a Windows virtual machine with hello Azure portal</span></span>

<span data-ttu-id="68b4f-104">Machines virtuelles peuvent être créés via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="68b4f-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="68b4f-105">Cette méthode fournit une interface utilisateur basée sur navigateur pour créer et configurer des machines virtuelles et toutes les ressources liées.</span><span class="sxs-lookup"><span data-stu-id="68b4f-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="68b4f-106">Cette procédure de démarrage rapide via la création d’une machine virtuelle et l’installation d’un serveur Web sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="68b4f-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="68b4f-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="68b4f-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="68b4f-108">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="68b4f-108">Log in tooAzure</span></span>

<span data-ttu-id="68b4f-109">Ouvrez une session dans toohello portail Azure à http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="68b4f-109">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="68b4f-110">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="68b4f-110">Create virtual machine</span></span>

1. <span data-ttu-id="68b4f-111">Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="68b4f-111">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="68b4f-112">Sélectionnez **Compute**, puis **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="68b4f-113">Entrez les informations de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="68b4f-113">Enter hello virtual machine information.</span></span> <span data-ttu-id="68b4f-114">nom d’utilisateur Hello et le mot de passe entré ici est toolog utilisé dans la machine virtuelle de toohello.</span><span class="sxs-lookup"><span data-stu-id="68b4f-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="68b4f-115">Lorsque vous avez terminé, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-115">When complete, click **OK**.</span></span>

    ![Entrez les informations de base sur votre machine virtuelle dans le panneau de portail hello](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="68b4f-117">Sélectionnez une taille de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="68b4f-117">Select a size for hello VM.</span></span> <span data-ttu-id="68b4f-118">Sélectionnez des tailles de plus, toosee **afficher toutes les** ou modifier hello **pris en charge le type de disque** filtre.</span><span class="sxs-lookup"><span data-stu-id="68b4f-118">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![Capture d’écran montrant les tailles de machine virtuelle](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="68b4f-120">Dans le panneau de paramètres hello, conserver les valeurs par défaut hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-120">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="68b4f-121">Dans la page de résumé hello, cliquez sur **Ok** déploiement d’ordinateur virtuel toostart hello.</span><span class="sxs-lookup"><span data-stu-id="68b4f-121">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="68b4f-122">Hello machine virtuelle sera épinglé toohello tableau de bord de portail Azure.</span><span class="sxs-lookup"><span data-stu-id="68b4f-122">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="68b4f-123">Une fois que la fin du déploiement de hello, panneau de résumé de machine virtuelle hello s’ouvre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="68b4f-123">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="68b4f-124">Connecter toovirtual machine</span><span class="sxs-lookup"><span data-stu-id="68b4f-124">Connect toovirtual machine</span></span>

<span data-ttu-id="68b4f-125">Créer un ordinateur virtuel de toohello connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="68b4f-125">Create a remote desktop connection toohello virtual machine.</span></span>

1. <span data-ttu-id="68b4f-126">Cliquez sur hello **Connect** bouton sur les propriétés d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="68b4f-126">Click hello **Connect** button on hello virtual machine properties.</span></span> <span data-ttu-id="68b4f-127">Un fichier de protocole Remote Desktop Protocol (fichier .rdp) est créé et téléchargé.</span><span class="sxs-lookup"><span data-stu-id="68b4f-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![Portail 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="68b4f-129">tooconnect tooyour machine virtuelle, ouvrez hello téléchargé le fichier RDP.</span><span class="sxs-lookup"><span data-stu-id="68b4f-129">tooconnect tooyour VM, open hello downloaded RDP file.</span></span> <span data-ttu-id="68b4f-130">À l’invite, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="68b4f-131">Sur un Mac, vous avez besoin d’un client RDP telles [Client Bureau à distance](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) de hello Mac App Store.</span><span class="sxs-lookup"><span data-stu-id="68b4f-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from hello Mac App Store.</span></span>

3. <span data-ttu-id="68b4f-132">Entrez le nom d’utilisateur hello et le mot de passe spécifié lors de la création d’ordinateur virtuel de hello, puis cliquez sur **Ok**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-132">Enter hello user name and password you specified when creating hello virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="68b4f-133">Vous pouvez recevoir un avertissement de certificat au cours du processus de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="68b4f-133">You may receive a certificate warning during hello sign-in process.</span></span> <span data-ttu-id="68b4f-134">Cliquez sur **Oui** ou **continuer** tooproceed avec une connexion hello.</span><span class="sxs-lookup"><span data-stu-id="68b4f-134">Click **Yes** or **Continue** tooproceed with hello connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="68b4f-135">Installation de IIS à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="68b4f-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="68b4f-136">Sur l’ordinateur virtuel de hello, démarrez une session PowerShell et exécutez hello suivant tooinstall de commande IIS.</span><span class="sxs-lookup"><span data-stu-id="68b4f-136">On hello virtual machine, start a PowerShell session and run hello following command tooinstall IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="68b4f-137">Lorsque vous avez terminé, quittez la session RDP de hello et retourner les propriétés de machine virtuelle hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="68b4f-137">When done, exit hello RDP session and return hello VM properties in hello Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="68b4f-138">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="68b4f-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="68b4f-139">Un groupe de sécurité réseau (NSG) sécurise les trafics entrant et sortant.</span><span class="sxs-lookup"><span data-stu-id="68b4f-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="68b4f-140">Lorsqu’un ordinateur virtuel est créé à partir de hello portail Azure, une règle de trafic entrant est créée sur le port 3389 pour les connexions RDP.</span><span class="sxs-lookup"><span data-stu-id="68b4f-140">When a VM is created from hello Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="68b4f-141">Étant donné que cet ordinateur virtuel héberge un serveur Web, une règle de groupe de sécurité réseau doit toobe créé pour le port 80.</span><span class="sxs-lookup"><span data-stu-id="68b4f-141">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="68b4f-142">Sur l’ordinateur virtuel de hello, cliquez sur nom hello Hello **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-142">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="68b4f-143">Sélectionnez hello **groupe de sécurité réseau**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-143">Select hello **network security group**.</span></span> <span data-ttu-id="68b4f-144">Hello groupe de sécurité réseau peut être identifié à l’aide de hello **Type** colonne.</span><span class="sxs-lookup"><span data-stu-id="68b4f-144">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="68b4f-145">Dans le menu de gauche hello, sous Paramètres, cliquez sur **les règles de sécurité de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-145">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="68b4f-146">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-146">Click on **Add**.</span></span>
5. <span data-ttu-id="68b4f-147">Dans **Nom**, tapez **http**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-147">In **Name**, type **http**.</span></span> <span data-ttu-id="68b4f-148">Assurez-vous que **étendue du Port** a la valeur too80 et **Action** est défini trop**autoriser**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-148">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="68b4f-149">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-149">Click **OK**.</span></span>


## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="68b4f-150">Hello d’affichage page d’accueil IIS</span><span class="sxs-lookup"><span data-stu-id="68b4f-150">View hello IIS welcome page</span></span>

<span data-ttu-id="68b4f-151">Avec IIS installé et le port 80 ouvrir tooyour VM, hello webserver sont maintenant accessibles à partir de hello internet.</span><span class="sxs-lookup"><span data-stu-id="68b4f-151">With IIS installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="68b4f-152">Ouvrez un navigateur web et entrez les adresse IP publique hello Hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="68b4f-152">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="68b4f-153">adresse IP publique de Hello sont accessibles sur le panneau de machine virtuelle hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="68b4f-153">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![Site IIS par défaut](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="68b4f-155">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="68b4f-155">Clean up resources</span></span>

<span data-ttu-id="68b4f-156">Si n’est plus nécessaire, supprimez hello groupe de ressources, ordinateur virtuel et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="68b4f-156">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="68b4f-157">toodo par conséquent, sélectionnez le groupe de ressources hello à partir du Panneau de machine virtuelle hello et cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="68b4f-157">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68b4f-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="68b4f-158">Next steps</span></span>

<span data-ttu-id="68b4f-159">Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web.</span><span class="sxs-lookup"><span data-stu-id="68b4f-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="68b4f-160">toolearn en savoir plus sur les machines virtuelles, continuer toohello didacticiel pour les machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="68b4f-160">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="68b4f-161">Didacticiels sur les machines virtuelles Azure Windows</span><span class="sxs-lookup"><span data-stu-id="68b4f-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
