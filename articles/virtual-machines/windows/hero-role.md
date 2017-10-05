---
title: "Installer IIS sur votre première machine virtuelle Windows | Microsoft Docs"
description: "Testez votre première machine virtuelle Windows en installant IIS et en ouvrant le port 80 à l’aide du Portail Azure."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: b11ce1eab0c26a802c31bc418cdf725cbc4fba30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="45816-103">Tester l’installation d’un rôle sur votre machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="45816-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="45816-104">Une fois que votre première machine virtuelle est opérationnelle, vous pouvez passer à l’installation des logiciels et services.</span><span class="sxs-lookup"><span data-stu-id="45816-104">Once you have your first virtual machine (VM) up and running, you can move on to installing software and services.</span></span> <span data-ttu-id="45816-105">Pour ce didacticiel, nous allons utiliser le Gestionnaire de serveur sur la machine virtuelle Windows Server pour installer IIS.</span><span class="sxs-lookup"><span data-stu-id="45816-105">For this tutorial, we are going to use Server Manager on the Windows Server VM to install IIS.</span></span> <span data-ttu-id="45816-106">Ensuite, nous allons créer un groupe de sécurité réseau (NSG) à l’aide du Portail Azure pour ouvrir le port 80 au trafic IIS.</span><span class="sxs-lookup"><span data-stu-id="45816-106">Then, we will create a Network Security Group (NSG) using the Azure portal to open port 80 to IIS traffic.</span></span> 

<span data-ttu-id="45816-107">Si vous n’avez pas encore créé votre première machine virtuelle, vous devez revenir à [Créer votre première machine virtuelle Windows dans le Portail Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant de poursuivre ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="45816-107">If you haven't already created your first VM, you should go back to [Create your first Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-the-vm-is-running"></a><span data-ttu-id="45816-108">Vérifier que la machine virtuelle est en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="45816-108">Make sure the VM is running</span></span>
1. <span data-ttu-id="45816-109">Ouvrez le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="45816-109">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="45816-110">Dans le menu hub, cliquez sur **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="45816-110">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="45816-111">Sélectionnez la machine virtuelle dans la liste.</span><span class="sxs-lookup"><span data-stu-id="45816-111">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="45816-112">Si l’état est **Arrêté (Libéré)**, cliquez sur le bouton **Démarrer** sur le panneau **Bases** de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="45816-112">If the status is **Stopped (Deallocated)**, click the **Start** button on the **Essentials** blade of the VM.</span></span> <span data-ttu-id="45816-113">Si l’état est **En cours d’exécution**, vous pouvez passer à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="45816-113">If the status is **Running**, you can move on to the next step.</span></span>

## <a name="connect-to-the-virtual-machine-and-sign-in"></a><span data-ttu-id="45816-114">Se connecter à la machine virtuelle et ouvrir une session</span><span class="sxs-lookup"><span data-stu-id="45816-114">Connect to the virtual machine and sign in</span></span>
1. <span data-ttu-id="45816-115">Dans le menu hub, cliquez sur **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="45816-115">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="45816-116">Sélectionnez la machine virtuelle dans la liste.</span><span class="sxs-lookup"><span data-stu-id="45816-116">Select the virtual machine from the list.</span></span>
2. <span data-ttu-id="45816-117">Dans le panneau de la machine virtuelle, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="45816-117">On the blade for the virtual machine, click **Connect**.</span></span> <span data-ttu-id="45816-118">Cette opération crée et télécharge un fichier .rdp (Remote Desktop Protocol) qui s’apparente à un raccourci de connexion à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="45816-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut to connect to your machine.</span></span> <span data-ttu-id="45816-119">Si vous le souhaitez, vous pouvez enregistrer le fichier sur votre bureau pour y accéder facilement.</span><span class="sxs-lookup"><span data-stu-id="45816-119">You might want to save the file to your desktop for easy access.</span></span> <span data-ttu-id="45816-120">**Ouvrez** ce fichier pour vous connecter à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="45816-120">**Open** this file to connect to your VM.</span></span>
   
    ![Capture d'écran du portail Azure montrant comment se connecter à votre machine virtuelle](./media/hero-role/connect.png)
3. <span data-ttu-id="45816-122">Un message vous avertit que le fichier .rdp provient d’un éditeur inconnu.</span><span class="sxs-lookup"><span data-stu-id="45816-122">You get a warning that the .rdp is from an unknown publisher.</span></span> <span data-ttu-id="45816-123">C’est normal.</span><span class="sxs-lookup"><span data-stu-id="45816-123">This is normal.</span></span> <span data-ttu-id="45816-124">Dans la fenêtre Bureau à distance, cliquez sur **Connecter** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="45816-124">In the Remote Desktop window, click **Connect** to continue.</span></span>
   
    ![Capture d’écran d’un avertissement relatif à un éditeur inconnu](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="45816-126">Dans la fenêtre Sécurité de Windows, tapez le nom d’utilisateur et le mot de passe du compte local que vous avez créé lorsque vous avez créé la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="45816-126">In the Windows Security window, type the username and password for the local account that you created when you created the VM.</span></span> <span data-ttu-id="45816-127">Le nom d’utilisateur est entré en tant que *vmname*&#92;*username*. Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="45816-127">The username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Capture d’écran de saisie du nom de la machine virtuelle, du nom d’utilisateur et du mot de passe](./media/hero-role/credentials.png)
5. <span data-ttu-id="45816-129">Vous êtes alors averti que le certificat ne peut pas être vérifié.</span><span class="sxs-lookup"><span data-stu-id="45816-129">You get a warning that the certificate cannot be verified.</span></span> <span data-ttu-id="45816-130">C’est normal.</span><span class="sxs-lookup"><span data-stu-id="45816-130">This is normal.</span></span> <span data-ttu-id="45816-131">Cliquez sur **Oui** pour vérifier l’identité de la machine virtuelle et terminer la connexion.</span><span class="sxs-lookup"><span data-stu-id="45816-131">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span></span>
   
   ![Capture d'écran montrant un message relatif à la vérification de l'identité de la machine virtuelle](./media/hero-role/cert-warning.png)

<span data-ttu-id="45816-133">En cas de problème de connexion, consultez [Résolution des problèmes de connexion Bureau à distance avec une machine virtuelle Azure Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45816-133">If you run in to trouble when you try to connect, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="45816-134">Installation d’IIS sur votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="45816-134">Install IIS on your VM</span></span>
<span data-ttu-id="45816-135">Maintenant que vous êtes connecté à la machine virtuelle, nous allons installer un rôle de serveur afin d’optimiser votre expérience.</span><span class="sxs-lookup"><span data-stu-id="45816-135">Now that you are logged in to the VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="45816-136">Si ce n’est pas déjà fait, ouvrez le **Gestionnaire de serveur** .</span><span class="sxs-lookup"><span data-stu-id="45816-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="45816-137">Cliquez sur le menu **Démarrer**, puis sur **Gestionnaire de serveur**.</span><span class="sxs-lookup"><span data-stu-id="45816-137">Click the **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="45816-138">Dans le volet gauche du **Gestionnaire de serveur**, sélectionnez **Serveur local**.</span><span class="sxs-lookup"><span data-stu-id="45816-138">In **Server Manager**, select **Local Server** from the left pane.</span></span> 
3. <span data-ttu-id="45816-139">Dans le menu, sélectionnez **Gérer** > **Ajouter des rôles et des fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="45816-139">In the menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="45816-140">Dans l’Assistant Ajout de rôles et de fonctionnalités, sur la page **Type d’installation**, choisissez **Installation basée sur un rôle ou une fonctionnalité**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="45816-140">In the Add Roles and Features Wizard, on the **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Capture d’écran montrant l’onglet Assistant Ajout de rôles et de fonctionnalités pour le type d’installation](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="45816-142">Sélectionnez la machine virtuelle dans le pool de serveurs, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="45816-142">Select the VM from the server pool and click **Next**.</span></span>
6. <span data-ttu-id="45816-143">Sur la page **Rôles de serveur**, cliquez sur **Serveur Web (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="45816-143">On the **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Capture d’écran montrant l’onglet Assistant Ajout de rôles et de fonctionnalités pour les rôles de serveur](./media/hero-role/add-iis.png)
7. <span data-ttu-id="45816-145">Dans la fenêtre contextuelle concernant l’ajout des fonctionnalités requises pour IIS, assurez-vous que l’option **Inclure les outils de gestion** est sélectionnée, puis cliquez sur **Ajouter des fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="45816-145">In the pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="45816-146">Lorsque la fenêtre contextuelle se ferme, cliquez sur **Suivant** dans l’assistant.</span><span class="sxs-lookup"><span data-stu-id="45816-146">When the pop-up closes, click **Next** in the wizard.</span></span>
   
    ![Capture d’écran montrant la fenêtre contextuelle permettant de confirmer l’ajout du rôle IIS](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="45816-148">Sur la page des fonctionnalités, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="45816-148">On the features page, click **Next**.</span></span>
9. <span data-ttu-id="45816-149">Sur la page **Rôle Web Server (IIS)**, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="45816-149">On the **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="45816-150">Sur la page **Services de rôle**, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="45816-150">On the **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="45816-151">Sur la page **Confirmation**, cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="45816-151">On the **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="45816-152">Une fois l’installation terminée, cliquez sur **Fermer** dans l’assistant.</span><span class="sxs-lookup"><span data-stu-id="45816-152">When the installation is complete, click **Close** on the wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="45816-153">Ouverture du port 80</span><span class="sxs-lookup"><span data-stu-id="45816-153">Open port 80</span></span>
<span data-ttu-id="45816-154">Pour que votre machine virtuelle accepte le trafic entrant sur le port 80, vous devez ajouter une règle de trafic entrant pour le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="45816-154">In order for your VM to accept inbound traffic over port 80, you need to add an inbound rule to the network security group.</span></span> 

1. <span data-ttu-id="45816-155">Ouvrez le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="45816-155">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="45816-156">Dans **Machines virtuelles** , sélectionnez la machine virtuelle que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="45816-156">In **Virtual machines** select the VM that you created.</span></span>
3. <span data-ttu-id="45816-157">Dans les paramètres des machines virtuelles, choisissez **Interfaces réseau** , puis sélectionnez l’interface réseau existante.</span><span class="sxs-lookup"><span data-stu-id="45816-157">In the virtual machines settings, select **Network interfaces** and then select the existing network interface.</span></span>
   
    ![Capture d’écran montrant le paramètre de la machine virtuelle pour les interfaces réseau](./media/hero-role/network-interface.png)
4. <span data-ttu-id="45816-159">Dans les **bases** de l’interface réseau, cliquez sur le **groupe de sécurité réseau**.</span><span class="sxs-lookup"><span data-stu-id="45816-159">In **Essentials** for the network interface, click the **Network security group**.</span></span>
   
    ![Capture d’écran montrant la section Bases pour l’interface réseau](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="45816-161">Dans le panneau **Bases** du groupe de sécurité réseau, une règle de trafic entrant doit exister par défaut pour **default-allow-rdp**. Elle vous permet de vous connecter à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="45816-161">In the **Essentials** blade for the NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you to log in to the VM.</span></span> <span data-ttu-id="45816-162">Pour autoriser le trafic IIS, vous allez ajouter une autre règle de trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="45816-162">You will add another inbound rule to allow IIS traffic.</span></span> <span data-ttu-id="45816-163">Cliquez sur **Règle de sécurité de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="45816-163">Click **Inbound security rule**.</span></span>
   
    ![Capture d’écran montrant la section Bases pour le groupe de sécurité réseau](./media/hero-role/inbound.png)
6. <span data-ttu-id="45816-165">Dans **Règles de sécurité de trafic entrant**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="45816-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Capture d’écran affichant le bouton d’ajout d’une règle de sécurité](./media/hero-role/add-rule.png)
7. <span data-ttu-id="45816-167">Dans **Règles de sécurité de trafic entrant**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="45816-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="45816-168">Entrez **80** dans la plage de ports et vérifiez que l’option **Autoriser** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="45816-168">Type **80** in the port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="45816-169">Une fois ces opérations effectuées, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="45816-169">When you are done, click **OK**.</span></span>
   
    ![Capture d’écran affichant le bouton d’ajout d’une règle de sécurité](./media/hero-role/port-80.png)

<span data-ttu-id="45816-171">Pour plus d’informations sur les groupes de sécurité réseau et sur les règles de trafic entrant et sortant, voir [Autoriser l’accès externe à votre machine virtuelle à l’aide du portail Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="45816-171">For more information about NSGs, inbound and outbound rules, see [Allow external access to your VM using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-to-the-default-iis-website"></a><span data-ttu-id="45816-172">Connexion au site Web IIS par défaut</span><span class="sxs-lookup"><span data-stu-id="45816-172">Connect to the default IIS website</span></span>
1. <span data-ttu-id="45816-173">Dans le portail Azure, cliquez sur **Machines virtuelles** , puis sélectionnez votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="45816-173">In the Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="45816-174">Dans le panneau **Bases**, copiez votre **adresse IP publique**.</span><span class="sxs-lookup"><span data-stu-id="45816-174">In the **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Capture d’écran indiquant où trouver l’adresse IP publique de votre machine virtuelle](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="45816-176">Ouvrez un navigateur et, dans la barre d’adresse, tapez l’adresse IP publique comme suit : http://<publicIPaddress>, puis appuyez sur **Entrée** pour accéder à cette adresse.</span><span class="sxs-lookup"><span data-stu-id="45816-176">Open a browser and in the address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** to go to that address.</span></span>
4. <span data-ttu-id="45816-177">Votre navigateur ouvre la page web IIS par défaut.</span><span class="sxs-lookup"><span data-stu-id="45816-177">Your browser should open the default IIS web page.</span></span> <span data-ttu-id="45816-178">Voici ce à quoi elle ressemble :</span><span class="sxs-lookup"><span data-stu-id="45816-178">It looks something like this:</span></span>
   
    ![Capture d’écran montrant à quoi ressemble la page IIS par défaut dans un navigateur](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="45816-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45816-180">Next steps</span></span>
* <span data-ttu-id="45816-181">Vous pouvez également tester [l’association d’un disque de données](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="45816-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to your virtual machine.</span></span> <span data-ttu-id="45816-182">Les disques de données fournissent plus de stockage pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="45816-182">Data disks provide more storage for your virtual machine.</span></span>

