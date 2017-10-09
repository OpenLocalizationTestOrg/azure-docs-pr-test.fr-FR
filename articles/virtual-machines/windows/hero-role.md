---
title: "aaaInstall IIS sur votre première machine virtuelle de Windows | Documents Microsoft"
description: "Faire des essais avec votre première machine virtuelle de Windows par l’installation d’IIS et l’ouverture à l’aide du port 80 hello portail Azure."
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
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="d09cc-103">Tester l’installation d’un rôle sur votre machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="d09cc-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="d09cc-104">Une fois que vous avez votre première machine virtuelle (VM) haut et en cours d’exécution, vous pouvez déplacer sur tooinstalling logiciels et services.</span><span class="sxs-lookup"><span data-stu-id="d09cc-104">Once you have your first virtual machine (VM) up and running, you can move on tooinstalling software and services.</span></span> <span data-ttu-id="d09cc-105">Pour ce didacticiel, nous allons toouse le Gestionnaire de serveur sur la machine virtuelle Windows Server de hello tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="d09cc-105">For this tutorial, we are going toouse Server Manager on hello Windows Server VM tooinstall IIS.</span></span> <span data-ttu-id="d09cc-106">Ensuite, nous allons créer un groupe de sécurité réseau (NSG) à l’aide du port 80 tooIIS trafic hello tooopen portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d09cc-106">Then, we will create a Network Security Group (NSG) using hello Azure portal tooopen port 80 tooIIS traffic.</span></span> 

<span data-ttu-id="d09cc-107">Si vous n’avez pas encore créé votre première machine virtuelle, vous devez revenir en arrière trop[créer votre première machine virtuelle de Windows Bonjour Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant de poursuivre ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d09cc-107">If you haven't already created your first VM, you should go back too[Create your first Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-hello-vm-is-running"></a><span data-ttu-id="d09cc-108">Vérifiez que hello que machine virtuelle est en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="d09cc-108">Make sure hello VM is running</span></span>
1. <span data-ttu-id="d09cc-109">Ouvrez hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d09cc-109">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d09cc-110">Dans le menu du hub hello, cliquez sur **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-110">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="d09cc-111">Sélectionnez hello virtuels à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="d09cc-111">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="d09cc-112">Si l’état de hello est **arrêté (désalloué)**, cliquez sur hello **Démarrer** bouton sur hello **Essentials** Panneau de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d09cc-112">If hello status is **Stopped (Deallocated)**, click hello **Start** button on hello **Essentials** blade of hello VM.</span></span> <span data-ttu-id="d09cc-113">Si l’état de hello est **en cours d’exécution**, vous pouvez déplacer sur l’étape suivante de toohello.</span><span class="sxs-lookup"><span data-stu-id="d09cc-113">If hello status is **Running**, you can move on toohello next step.</span></span>

## <a name="connect-toohello-virtual-machine-and-sign-in"></a><span data-ttu-id="d09cc-114">Connecter l’ordinateur virtuel de toohello et se connecter</span><span class="sxs-lookup"><span data-stu-id="d09cc-114">Connect toohello virtual machine and sign in</span></span>
1. <span data-ttu-id="d09cc-115">Dans le menu du hub hello, cliquez sur **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-115">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="d09cc-116">Sélectionnez hello virtuels à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="d09cc-116">Select hello virtual machine from hello list.</span></span>
2. <span data-ttu-id="d09cc-117">Dans le panneau hello pour la machine virtuelle de hello, cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-117">On hello blade for hello virtual machine, click **Connect**.</span></span> <span data-ttu-id="d09cc-118">Crée et télécharge un fichier de protocole Bureau à distance (fichier .rdp) qui s’apparente à un ordinateur de tooyour tooconnect contextuel.</span><span class="sxs-lookup"><span data-stu-id="d09cc-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut tooconnect tooyour machine.</span></span> <span data-ttu-id="d09cc-119">Vous pourriez bureau de tooyour fichier toosave hello pour faciliter l’accès.</span><span class="sxs-lookup"><span data-stu-id="d09cc-119">You might want toosave hello file tooyour desktop for easy access.</span></span> <span data-ttu-id="d09cc-120">**Ouvrez** cette tooyour de tooconnect fichier machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d09cc-120">**Open** this file tooconnect tooyour VM.</span></span>
   
    ![Capture d’écran de hello montrant portail Azure comment tooconnect tooyour machine virtuelle](./media/hero-role/connect.png)
3. <span data-ttu-id="d09cc-122">Vous obtenez un avertissement qui .rdp hello est un serveur de publication inconnu.</span><span class="sxs-lookup"><span data-stu-id="d09cc-122">You get a warning that hello .rdp is from an unknown publisher.</span></span> <span data-ttu-id="d09cc-123">C’est normal.</span><span class="sxs-lookup"><span data-stu-id="d09cc-123">This is normal.</span></span> <span data-ttu-id="d09cc-124">Dans la fenêtre du Bureau à distance hello, cliquez sur **Connect** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d09cc-124">In hello Remote Desktop window, click **Connect** toocontinue.</span></span>
   
    ![Capture d’écran d’un avertissement relatif à un éditeur inconnu](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="d09cc-126">Dans la fenêtre de sécurité Windows hello, le nom d’utilisateur de type hello et un mot de passe pour le compte local hello que vous avez créé lorsque vous avez créé hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d09cc-126">In hello Windows Security window, type hello username and password for hello local account that you created when you created hello VM.</span></span> <span data-ttu-id="d09cc-127">nom d’utilisateur Hello est entré en tant que *vmname*&#92; *nom d’utilisateur*, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-127">hello username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Capture d’écran de saisie du nom d’ordinateur virtuel hello, nom d’utilisateur et mot de passe](./media/hero-role/credentials.png)
5. <span data-ttu-id="d09cc-129">Vous obtenez un avertissement de certificat hello ne peut pas être vérifié.</span><span class="sxs-lookup"><span data-stu-id="d09cc-129">You get a warning that hello certificate cannot be verified.</span></span> <span data-ttu-id="d09cc-130">C’est normal.</span><span class="sxs-lookup"><span data-stu-id="d09cc-130">This is normal.</span></span> <span data-ttu-id="d09cc-131">Cliquez sur **Oui** tooverify hello l’identité de l’ordinateur virtuel de hello et terminer la session.</span><span class="sxs-lookup"><span data-stu-id="d09cc-131">Click **Yes** tooverify hello identity of hello virtual machine and finish logging on.</span></span>
   
   ![Capture d’écran montrant un message à propos de vérification d’identité hello Hello machine virtuelle](./media/hero-role/cert-warning.png)

<span data-ttu-id="d09cc-133">Si vous exécutez dans tootrouble lorsque vous essayez de tooconnect, consultez [tooa de connexions de résoudre les problèmes de bureau à distance basé sur Windows Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d09cc-133">If you run in tootrouble when you try tooconnect, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="d09cc-134">Installation d’IIS sur votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d09cc-134">Install IIS on your VM</span></span>
<span data-ttu-id="d09cc-135">Maintenant que vous êtes connecté toohello machine virtuelle, nous allons installer un rôle de serveur afin que vous pouvez faire des essais plus.</span><span class="sxs-lookup"><span data-stu-id="d09cc-135">Now that you are logged in toohello VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="d09cc-136">Si ce n’est pas déjà fait, ouvrez le **Gestionnaire de serveur** .</span><span class="sxs-lookup"><span data-stu-id="d09cc-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="d09cc-137">Cliquez sur hello **Démarrer** menu, puis sur **le Gestionnaire de serveur**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-137">Click hello **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="d09cc-138">Dans **le Gestionnaire de serveur**, sélectionnez **serveur Local** hello volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="d09cc-138">In **Server Manager**, select **Local Server** from hello left pane.</span></span> 
3. <span data-ttu-id="d09cc-139">Dans le menu de hello, sélectionnez **gérer** > **Ajout de rôles et fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-139">In hello menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="d09cc-140">Dans Ajouter des rôles hello Assistant et fonctionnalités, sur hello **le Type d’Installation** choisissez **installation basée sur un rôle ou une fonctionnalité**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-140">In hello Add Roles and Features Wizard, on hello **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Onglet Capture d’écran montrant hello Assistant Ajouter des rôles et fonctionnalités de Type d’Installation](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="d09cc-142">Sélectionnez hello VM hello pool de serveurs, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-142">Select hello VM from hello server pool and click **Next**.</span></span>
6. <span data-ttu-id="d09cc-143">Sur hello **rôles serveur** page, sélectionnez **serveur Web (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-143">On hello **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Onglet Capture d’écran montrant hello Assistant Ajouter des rôles et fonctionnalités pour les rôles de serveur](./media/hero-role/add-iis.png)
7. <span data-ttu-id="d09cc-145">Bonjour contextuelle sur l’ajout de fonctionnalités requises pour IIS, assurez-vous que **les outils d’administration** est sélectionné, puis cliquez sur **ajouter des fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-145">In hello pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="d09cc-146">Lorsque hello contextuelle se ferme, cliquez sur **suivant** dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="d09cc-146">When hello pop-up closes, click **Next** in hello wizard.</span></span>
   
    ![Capture d’écran contextuel tooconfirm ajouter le rôle IIS hello](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="d09cc-148">Dans la page de composants hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-148">On hello features page, click **Next**.</span></span>
9. <span data-ttu-id="d09cc-149">Sur hello **rôle de serveur Web (IIS)** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-149">On hello **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="d09cc-150">Sur hello **les Services de rôle** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-150">On hello **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="d09cc-151">Sur hello **Confirmation** , cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-151">On hello **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="d09cc-152">Lors de l’installation de hello est terminée, cliquez sur **fermer** sur l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="d09cc-152">When hello installation is complete, click **Close** on hello wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="d09cc-153">Ouverture du port 80</span><span class="sxs-lookup"><span data-stu-id="d09cc-153">Open port 80</span></span>
<span data-ttu-id="d09cc-154">Dans l’ordre pour votre tooaccept de machine virtuelle du trafic entrant sur le port 80, vous devez tooadd un groupe de sécurité réseau toohello règle de trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="d09cc-154">In order for your VM tooaccept inbound traffic over port 80, you need tooadd an inbound rule toohello network security group.</span></span> 

1. <span data-ttu-id="d09cc-155">Ouvrez hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d09cc-155">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d09cc-156">Dans **virtuels** sélectionnez hello machine virtuelle que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="d09cc-156">In **Virtual machines** select hello VM that you created.</span></span>
3. <span data-ttu-id="d09cc-157">Dans paramètres de machines virtuelles hello, sélectionnez **interfaces réseau** et puis sélectionnez hello interface réseau existante.</span><span class="sxs-lookup"><span data-stu-id="d09cc-157">In hello virtual machines settings, select **Network interfaces** and then select hello existing network interface.</span></span>
   
    ![Capture d’écran de configuration de machine virtuelle hello pour hello interfaces réseau](./media/hero-role/network-interface.png)
4. <span data-ttu-id="d09cc-159">Dans **Essentials** pour l’interface de réseau hello, cliquez sur hello **groupe de sécurité réseau**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-159">In **Essentials** for hello network interface, click hello **Network security group**.</span></span>
   
    ![Capture d’écran de section d’Essentials hello pour l’interface de réseau hello](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="d09cc-161">Bonjour **Essentials** panneau pour hello groupe de sécurité réseau, vous devez disposer d’une valeur par défaut existante règle de trafic entrant **rdp par défaut autoriser** qui vous permet de toolog dans toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d09cc-161">In hello **Essentials** blade for hello NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you toolog in toohello VM.</span></span> <span data-ttu-id="d09cc-162">Vous allez ajouter un autre trafic IIS tooallow règle de trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="d09cc-162">You will add another inbound rule tooallow IIS traffic.</span></span> <span data-ttu-id="d09cc-163">Cliquez sur **Règle de sécurité de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-163">Click **Inbound security rule**.</span></span>
   
    ![Capture d’écran montrant la section Essentials hello hello NSG](./media/hero-role/inbound.png)
6. <span data-ttu-id="d09cc-165">Dans **Règles de sécurité de trafic entrant**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Capture d’écran hello bouton tooadd une règle de sécurité](./media/hero-role/add-rule.png)
7. <span data-ttu-id="d09cc-167">Dans **Règles de sécurité de trafic entrant**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="d09cc-168">Type **80** dans hello la plage de ports et assurez-vous que **autoriser** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="d09cc-168">Type **80** in hello port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="d09cc-169">Une fois ces opérations effectuées, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-169">When you are done, click **OK**.</span></span>
   
    ![Capture d’écran hello bouton tooadd une règle de sécurité](./media/hero-role/port-80.png)

<span data-ttu-id="d09cc-171">Pour plus d’informations sur les groupes de sécurité réseau, des règles entrantes et sortantes, consultez [autoriser un accès externe tooyour machine virtuelle en utilisant hello portail Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d09cc-171">For more information about NSGs, inbound and outbound rules, see [Allow external access tooyour VM using hello Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-toohello-default-iis-website"></a><span data-ttu-id="d09cc-172">Connecter le site Web IIS de toohello par défaut</span><span class="sxs-lookup"><span data-stu-id="d09cc-172">Connect toohello default IIS website</span></span>
1. <span data-ttu-id="d09cc-173">Bonjour portail Azure, cliquez sur **virtuels** , puis sélectionnez votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d09cc-173">In hello Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="d09cc-174">Bonjour **Essentials** panneau, copiez votre **adresse IP publique**.</span><span class="sxs-lookup"><span data-stu-id="d09cc-174">In hello **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Capture d’écran montrant où toofind hello adresse IP publique de votre machine virtuelle](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="d09cc-176">Ouvrez un navigateur et dans la barre d’adresses hello, tapez votre adresse IP publique comme suit : http://<publicIPaddress> et cliquez sur **entrée** toogo toothat adresse.</span><span class="sxs-lookup"><span data-stu-id="d09cc-176">Open a browser and in hello address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** toogo toothat address.</span></span>
4. <span data-ttu-id="d09cc-177">Votre navigateur doit ouvrir la page web de hello par défaut IIS.</span><span class="sxs-lookup"><span data-stu-id="d09cc-177">Your browser should open hello default IIS web page.</span></span> <span data-ttu-id="d09cc-178">Voici ce à quoi elle ressemble :</span><span class="sxs-lookup"><span data-stu-id="d09cc-178">It looks something like this:</span></span>
   
    ![Capture d’écran montrant la page par défaut IIS hello ressemble dans un navigateur](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="d09cc-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d09cc-180">Next steps</span></span>
* <span data-ttu-id="d09cc-181">Vous pouvez également faire des essais avec [y attacher un disque de données](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtuels.</span><span class="sxs-lookup"><span data-stu-id="d09cc-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine.</span></span> <span data-ttu-id="d09cc-182">Les disques de données fournissent plus de stockage pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d09cc-182">Data disks provide more storage for your virtual machine.</span></span>

