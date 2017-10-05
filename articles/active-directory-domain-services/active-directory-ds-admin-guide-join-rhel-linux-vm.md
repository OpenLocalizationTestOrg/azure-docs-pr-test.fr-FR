---
title: "Version préliminaire des services de domaine Azure Active Directory : associer une machine virtuelle RHEL à un domaine géré | Microsoft Docs"
description: Joindre une machine virtuelle Linux Red Hat Enterprise aux services de domaine Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="60c3a-103">Joindre une machine virtuelle Red Hat Enterprise Linux 7 à un domaine géré</span><span class="sxs-lookup"><span data-stu-id="60c3a-103">Join a Red Hat Enterprise Linux 7 virtual machine to a managed domain</span></span>
<span data-ttu-id="60c3a-104">Cet article indique comment joindre une machine virtuelle Red Hat Enterprise Linux (RHEL) 7 à un domaine géré par les services de domaine Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60c3a-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="60c3a-105">Configurer une machine virtuelle Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="60c3a-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="60c3a-106">Pour approvisionner une machine virtuelle RHEL 7 à l’aide du portail Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="60c3a-106">Perform the following steps to provision a RHEL 7 virtual machine using the Azure portal.</span></span>

1. <span data-ttu-id="60c3a-107">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60c3a-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

    ![Tableau de bord du portail Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="60c3a-109">Dans le volet gauche, cliquez sur **Nouveau** et tapez **Red Hat** dans le volet de recherche, comme illustré dans la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="60c3a-109">Click **New** on the left pane and type **Red Hat** into the search bar as shown in the following screenshot.</span></span> <span data-ttu-id="60c3a-110">Les entrées relatives à Red Hat Enterprise Linux s’affichent dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="60c3a-110">Entries for Red Hat Enterprise Linux appear in the search results.</span></span> <span data-ttu-id="60c3a-111">Cliquez sur **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="60c3a-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Sélectionner RHEL dans les résultats](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="60c3a-113">Dans le volet **Tous les fichiers** , l’image relative à Red Hat Enterprise Linux 7.2 doit apparaître dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="60c3a-113">The search results in the **Everything** pane should list the Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="60c3a-114">Cliquez sur **Red Hat Enterprise Linux 7.2** pour afficher plus d’informations sur l’image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-114">Click **Red Hat Enterprise Linux 7.2** to view more information about the virtual machine image.</span></span>

    ![Sélectionner RHEL dans les résultats](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="60c3a-116">Le volet **Red Hat Enterprise Linux 7.2** doit afficher plus d’informations sur l’image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-116">In the **Red Hat Enterprise Linux 7.2** pane, you should see more information about the virtual machine image.</span></span> <span data-ttu-id="60c3a-117">Dans la liste déroulante **Sélectionner un modèle de déploiement**, choisissez **Classique**.</span><span class="sxs-lookup"><span data-stu-id="60c3a-117">In the **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="60c3a-118">Ensuite, cliquez sur le bouton **Créer** .</span><span class="sxs-lookup"><span data-stu-id="60c3a-118">Then click the **Create** button.</span></span>

    ![Afficher les détails d’une image](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="60c3a-120">Sur la page **Concepts de base** de l’Assistant **Créer une machine virtuelle**, entrez le **nom d’hôte** de la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-120">In the **Basics** page of the **Create virtual machine** wizard, enter the **Host Name** for the new virtual machine.</span></span> <span data-ttu-id="60c3a-121">Spécifiez également un nom d’utilisateur d’administrateur local dans le champ **Nom d’utilisateur** et indiquez une valeur dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="60c3a-121">Also specify a local administrator user name in the **User name** field and a **Password**.</span></span> <span data-ttu-id="60c3a-122">Vous pouvez aussi choisir d’utiliser une clé SSH pour authentifier l’utilisateur d’administrateur local.</span><span class="sxs-lookup"><span data-stu-id="60c3a-122">You may also choose to use an SSH key to authenticate the local administrator user.</span></span> <span data-ttu-id="60c3a-123">Sélectionnez également un **niveau tarifaire** pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-123">Also select a **Pricing Tier** for the virtual machine.</span></span>

    ![Créer une machine virtuelle - Page Concepts de base](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="60c3a-125">Sur la page **Taille** de l’Assistant **Créer une machine virtuelle**, sélectionnez la taille de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-125">In the **Size** page of the **Create virtual machine** wizard, select the size for the virtual machine.</span></span>

    ![Créer une machine virtuelle - Sélection de la taille](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="60c3a-127">Sur la page **Paramètres** de l’Assistant **Créer une machine virtuelle**, sélectionnez le compte de stockage de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-127">In the **Settings** page of the **Create virtual machine** wizard, select the storage account for the virtual machine.</span></span> <span data-ttu-id="60c3a-128">Cliquez sur **Réseau virtuel** pour sélectionner le réseau virtuel sur lequel la machine virtuelle Linux doit être déployée.</span><span class="sxs-lookup"><span data-stu-id="60c3a-128">Click **Virtual Network** to select the virtual network to which the Linux VM should be deployed.</span></span> <span data-ttu-id="60c3a-129">Dans le panneau **Réseau virtuel**, sélectionnez le réseau virtuel dans lequel les services de domaine Azure AD sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="60c3a-129">In the **Virtual Network** blade, select the virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="60c3a-130">Pour les besoins de cet exemple, nous allons sélectionner le réseau virtuel « MyPreviewVNet ».</span><span class="sxs-lookup"><span data-stu-id="60c3a-130">In this example, we pick the 'MyPreviewVNet' virtual network.</span></span>

    ![Créer une machine virtuelle - Sélection du réseau virtuel](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="60c3a-132">Sur la page **Résumé** de l’Assistant **Créer une machine virtuelle**, passez les informations en revue et cliquez sur le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="60c3a-132">On the **Summary** page of the **Create virtual machine** wizard, review and click the **OK** button.</span></span>

    ![Créer une machine virtuelle - Réseau virtuel sélectionné](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="60c3a-134">Le déploiement de la nouvelle machine virtuelle basée sur l’image de RHEL 7.2 doit commencer.</span><span class="sxs-lookup"><span data-stu-id="60c3a-134">Deployment of the new virtual machine based on the RHEL 7.2 image should start.</span></span>

    ![Créer une machine virtuelle - Déploiement démarré](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="60c3a-136">Au bout de quelques minutes, la machine virtuelle est déployée et prête à être utilisée.</span><span class="sxs-lookup"><span data-stu-id="60c3a-136">After a few minutes, the virtual machine should be deployed successfully and ready for use.</span></span>

    ![Créer une machine virtuelle - Déployée](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="60c3a-138">Connexion à distance à la machine virtuelle Linux qui vient d’être configurée</span><span class="sxs-lookup"><span data-stu-id="60c3a-138">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="60c3a-139">La machine virtuelle RHEL 7.2 a été configurée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="60c3a-139">The RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="60c3a-140">La tâche suivante consiste à se connecter à distance à cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-140">The next task is to connect remotely to the virtual machine.</span></span>

<span data-ttu-id="60c3a-141">**connecter à la machine virtuelle RHEL 7.2** , suivez les instructions de l’article [Connexion à une machine virtuelle exécutant Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60c3a-141">**Connect to the RHEL 7.2 virtual machine** Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="60c3a-142">Les étapes restantes indiquées partent du principe que vous utilisez le client SSH PuTTY pour vous connecter à la machine virtuelle RHEL.</span><span class="sxs-lookup"><span data-stu-id="60c3a-142">The rest of the steps assume you use the PuTTY SSH client to connect to the RHEL virtual machine.</span></span> <span data-ttu-id="60c3a-143">Pour voir en savoir plus, consultez la page [Téléchargement PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="60c3a-143">For more information, see the [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="60c3a-144">Ouvrez le programme PuTTY.</span><span class="sxs-lookup"><span data-stu-id="60c3a-144">Open the PuTTY program.</span></span>
2. <span data-ttu-id="60c3a-145">Saisissez une valeur dans le champ **Nom de l’hôte** de la machine virtuelle RHEL.</span><span class="sxs-lookup"><span data-stu-id="60c3a-145">Enter the **Host Name** for the newly created RHEL virtual machine.</span></span> <span data-ttu-id="60c3a-146">Dans cet exemple, notre machine virtuelle présente le nom d’hôte « contoso-rhel.cloudapp .net ».</span><span class="sxs-lookup"><span data-stu-id="60c3a-146">In this example, our virtual machine has the host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="60c3a-147">Si vous n’êtes pas sûr du nom d’hôte de votre machine virtuelle, reportez-vous au tableau de bord de la machine virtuelle sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="60c3a-147">If you are not sure of the host name of your VM, refer to the VM dashboard on the Azure portal.</span></span>

    ![Connexion PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="60c3a-149">Connectez-vous à la machine virtuelle en utilisant les informations d’identification de l’administrateur local que vous avez spécifiées lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-149">Log on to the virtual machine using the local administrator credentials you specified when the virtual machine was created.</span></span> <span data-ttu-id="60c3a-150">Dans cet exemple, nous avons utilisé le compte d’administrateur local appelé « mahesh ».</span><span class="sxs-lookup"><span data-stu-id="60c3a-150">In this example, we used the local administrator account "mahesh".</span></span>

    ![Connexion PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="60c3a-152">Installer les packages requis sur la machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="60c3a-152">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="60c3a-153">Lorsque vous êtes connecté à la machine virtuelle, la tâche suivante consiste à installer les packages requis pour la jonction de domaine sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-153">After connecting to the virtual machine, the next task is to install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="60c3a-154">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="60c3a-154">Perform the following steps:</span></span>

1. <span data-ttu-id="60c3a-155">**Installer realmd :** le package realmd est utilisé pour la jonction de domaine.</span><span class="sxs-lookup"><span data-stu-id="60c3a-155">**Install realmd:** The realmd package is used for domain join.</span></span> <span data-ttu-id="60c3a-156">Sur votre terminal PuTTY, saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="60c3a-156">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="60c3a-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="60c3a-157">sudo yum install realmd</span></span>

    ![Installation de realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="60c3a-159">Après quelques minutes, le package realmd doit être installé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-159">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![Package realmd installé](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="60c3a-161">**Installer sssd :** le package realmd s’appuie sur sssd pour effectuer des jonctions aux domaines.</span><span class="sxs-lookup"><span data-stu-id="60c3a-161">**Install sssd:** The realmd package depends on sssd to perform domain join operations.</span></span> <span data-ttu-id="60c3a-162">Sur votre terminal PuTTY, saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="60c3a-162">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="60c3a-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="60c3a-163">sudo yum install sssd</span></span>

    ![Installation de sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="60c3a-165">Après quelques minutes, le package sssd doit être installé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-165">After a few minutes, the sssd package should get installed on the virtual machine.</span></span>

    ![Package realmd installé](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="60c3a-167">**Installer Kerberos :** dans votre terminal PuTTY, saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="60c3a-167">**Install kerberos:** In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="60c3a-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="60c3a-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Installation de Kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="60c3a-170">Après quelques minutes, le package realmd doit être installé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60c3a-170">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![Kerberos installé](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="60c3a-172">Joindre la machine virtuelle Linux au domaine géré</span><span class="sxs-lookup"><span data-stu-id="60c3a-172">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="60c3a-173">Maintenant que les packages requis sont installés sur la machine virtuelle Linux, la tâche suivante consiste à joindre cette machine virtuelle au domaine géré.</span><span class="sxs-lookup"><span data-stu-id="60c3a-173">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="60c3a-174">Découvrez le domaine géré par les services de domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60c3a-174">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="60c3a-175">Sur votre terminal PuTTY, saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="60c3a-175">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="60c3a-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="60c3a-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="60c3a-178">Si la commande **realm discover** ne parvient pas à découvrir votre domaine géré, vérifiez que ce dernier est accessible depuis la machine virtuelle (exécutez une commande ping).</span><span class="sxs-lookup"><span data-stu-id="60c3a-178">If **realm discover** is unable to find your managed domain, ensure that the domain is reachable from the virtual machine (try ping).</span></span> <span data-ttu-id="60c3a-179">Assurez-vous également que la machine virtuelle a bien été déployée dans le réseau virtuel au sein duquel le domaine géré est disponible.</span><span class="sxs-lookup"><span data-stu-id="60c3a-179">Also ensure that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
2. <span data-ttu-id="60c3a-180">Initialisez Kerberos.</span><span class="sxs-lookup"><span data-stu-id="60c3a-180">Initialize kerberos.</span></span> <span data-ttu-id="60c3a-181">Sur votre terminal PuTTY, saisissez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="60c3a-181">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="60c3a-182">Vérifiez que vous spécifiez un utilisateur appartenant au groupe « AAD DC Administrators ».</span><span class="sxs-lookup"><span data-stu-id="60c3a-182">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="60c3a-183">Seuls ces utilisateurs peuvent joindre des ordinateurs au domaine géré.</span><span class="sxs-lookup"><span data-stu-id="60c3a-183">Only these users can join computers to the managed domain.</span></span>

    <span data-ttu-id="60c3a-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="60c3a-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="60c3a-186">Veillez à spécifier le nom de domaine en majuscules. Dans le cas contraire, kinit échoue.</span><span class="sxs-lookup"><span data-stu-id="60c3a-186">Ensure that you specify the domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="60c3a-187">Joignez l’ordinateur au domaine.</span><span class="sxs-lookup"><span data-stu-id="60c3a-187">Join the machine to the domain.</span></span> <span data-ttu-id="60c3a-188">Sur votre terminal PuTTY, saisissez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="60c3a-188">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="60c3a-189">Spécifiez le même utilisateur qu’à l’étape précédente (« kinit »).</span><span class="sxs-lookup"><span data-stu-id="60c3a-189">Specify the same user you specified in the preceding step ('kinit').</span></span>

    <span data-ttu-id="60c3a-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="60c3a-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Jonction de domaine](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="60c3a-192">Vous devez voir apparaître un message signalant que l’ordinateur a bien été joint au domaine géré : « La machine a bien été inscrite dans le domaine ».</span><span class="sxs-lookup"><span data-stu-id="60c3a-192">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="60c3a-193">Vérifier la jonction de domaine</span><span class="sxs-lookup"><span data-stu-id="60c3a-193">Verify domain join</span></span>
<span data-ttu-id="60c3a-194">Vous pouvez vérifier rapidement si l’ordinateur a bien été joint au domaine géré.</span><span class="sxs-lookup"><span data-stu-id="60c3a-194">You can quickly verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="60c3a-195">Connectez-vous à la machine virtuelle RHEL qui vient d’être jointe au domaine via SSH et un compte d’utilisateur de domaine, puis vérifiez que le compte d’utilisateur est correctement résolu.</span><span class="sxs-lookup"><span data-stu-id="60c3a-195">Connect to the newly domain joined RHEL VM using SSH and a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="60c3a-196">Sur votre terminal PuTTY, saisissez la commande suivante pour vous connecter à la machine virtuelle RHEL qui vient d’être jointe au domaine, à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="60c3a-196">In your PuTTY terminal, type the following command to connect to the newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="60c3a-197">Utilisez un compte de domaine appartenant au domaine géré (par exemple dans ce cas, « bob@CONTOSO100.COM »).</span><span class="sxs-lookup"><span data-stu-id="60c3a-197">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="60c3a-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="60c3a-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="60c3a-199">Sur votre terminal PuTTY, tapez la commande suivante pour voir si le répertoire de base a été initialisé correctement.</span><span class="sxs-lookup"><span data-stu-id="60c3a-199">In your PuTTY terminal, type the following command to see if the home directory was initialized correctly.</span></span>

    <span data-ttu-id="60c3a-200">pwd</span><span class="sxs-lookup"><span data-stu-id="60c3a-200">pwd</span></span>
3. <span data-ttu-id="60c3a-201">Sur votre terminal PuTTY, tapez la commande suivante pour voir si les membres du groupe ont été correctement résolus.</span><span class="sxs-lookup"><span data-stu-id="60c3a-201">In your PuTTY terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="60c3a-202">id</span><span class="sxs-lookup"><span data-stu-id="60c3a-202">id</span></span>

<span data-ttu-id="60c3a-203">Vous trouverez ci-dessous un exemple de sortie de ces commandes :</span><span class="sxs-lookup"><span data-stu-id="60c3a-203">A sample output of these commands follows:</span></span>

![Vérifier la jonction de domaine](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="60c3a-205">Résolution des problèmes de jonction de domaine</span><span class="sxs-lookup"><span data-stu-id="60c3a-205">Troubleshooting domain join</span></span>
<span data-ttu-id="60c3a-206">Reportez-vous à l’article relatif à la [résolution des problèmes de jonction de domaine](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) .</span><span class="sxs-lookup"><span data-stu-id="60c3a-206">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="60c3a-207">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="60c3a-207">Related Content</span></span>
* [<span data-ttu-id="60c3a-208">Services de domaine Azure AD : guide de prise en main</span><span class="sxs-lookup"><span data-stu-id="60c3a-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="60c3a-209">Joindre une machine virtuelle Windows Server à un domaine géré par les services de domaine Azure AD</span><span class="sxs-lookup"><span data-stu-id="60c3a-209">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="60c3a-210">[Connexion à une machine virtuelle exécutant Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60c3a-210">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="60c3a-211">Installing Kerberos (Installation de Kerberos)</span><span class="sxs-lookup"><span data-stu-id="60c3a-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="60c3a-212">Red Hat Enterprise Linux 7 - Windows Integration Guide (Red Hat Enterprise Linux 7 - Guide d’intégration à Windows)</span><span class="sxs-lookup"><span data-stu-id="60c3a-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
