---
title: "Azure Active Directory Domain Services : Joindre un domaine géré de RHEL VM tooa | Documents Microsoft"
description: Joindre un ordinateur virtuel de Red Hat Enterprise Linux tooAzure AD les Services de domaine
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
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a><span data-ttu-id="6b842-103">Joindre un domaine géré de tooa de machine virtuelle de Red Hat Enterprise Linux 7</span><span class="sxs-lookup"><span data-stu-id="6b842-103">Join a Red Hat Enterprise Linux 7 virtual machine tooa managed domain</span></span>
<span data-ttu-id="6b842-104">Cet article explique comment toojoin un tooan de machine virtuelle Red Hat Enterprise Linux (RHEL) 7 des Services de domaine Active Directory Azure géré le domaine.</span><span class="sxs-lookup"><span data-stu-id="6b842-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="6b842-105">Configurer une machine virtuelle Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="6b842-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="6b842-106">Effectuer hello suivant les étapes tooprovision un RHEL 7 machine virtuelle hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6b842-106">Perform hello following steps tooprovision a RHEL 7 virtual machine using hello Azure portal.</span></span>

1. <span data-ttu-id="6b842-107">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6b842-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

    ![Tableau de bord du portail Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="6b842-109">Cliquez sur **nouveau** sur hello gauche du volet et le type **Red Hat** dans la barre de recherche hello comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="6b842-109">Click **New** on hello left pane and type **Red Hat** into hello search bar as shown in hello following screenshot.</span></span> <span data-ttu-id="6b842-110">Entrées pour Red Hat Enterprise Linux apparaissent dans les résultats de la recherche hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-110">Entries for Red Hat Enterprise Linux appear in hello search results.</span></span> <span data-ttu-id="6b842-111">Cliquez sur **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="6b842-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Sélectionner RHEL dans les résultats](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="6b842-113">résultats de recherche de Hello en hello **tout** volet doit répertorier les image hello Red Hat Enterprise Linux 7.2.</span><span class="sxs-lookup"><span data-stu-id="6b842-113">hello search results in hello **Everything** pane should list hello Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="6b842-114">Cliquez sur **Red Hat Enterprise Linux 7.2** tooview plus d’informations sur l’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-114">Click **Red Hat Enterprise Linux 7.2** tooview more information about hello virtual machine image.</span></span>

    ![Sélectionner RHEL dans les résultats](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="6b842-116">Bonjour **Red Hat Enterprise Linux 7.2** volet, vous devez voir plus d’informations sur l’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-116">In hello **Red Hat Enterprise Linux 7.2** pane, you should see more information about hello virtual machine image.</span></span> <span data-ttu-id="6b842-117">Bonjour **sélectionner un modèle de déploiement** liste déroulante, sélectionnez **classique**.</span><span class="sxs-lookup"><span data-stu-id="6b842-117">In hello **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="6b842-118">Puis cliquez sur hello **créer** bouton.</span><span class="sxs-lookup"><span data-stu-id="6b842-118">Then click hello **Create** button.</span></span>

    ![Afficher les détails d’une image](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="6b842-120">Bonjour **notions de base** page Hello **créer la machine virtuelle** Assistant, entrez hello **nom d’hôte** pour la machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-120">In hello **Basics** page of hello **Create virtual machine** wizard, enter hello **Host Name** for hello new virtual machine.</span></span> <span data-ttu-id="6b842-121">Également spécifier un nom d’utilisateur administrateur local Bonjour **nom d’utilisateur** champ et un **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6b842-121">Also specify a local administrator user name in hello **User name** field and a **Password**.</span></span> <span data-ttu-id="6b842-122">Vous pouvez également choisir toouse un utilisateur d’administrateur local SSH tooauthenticate clé hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-122">You may also choose toouse an SSH key tooauthenticate hello local administrator user.</span></span> <span data-ttu-id="6b842-123">Sélectionnez également un **niveau tarifaire** pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-123">Also select a **Pricing Tier** for hello virtual machine.</span></span>

    ![Créer une machine virtuelle - Page Concepts de base](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="6b842-125">Bonjour **taille** page Hello **créer la machine virtuelle** taille hello Assistant, sélectionnez pour l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-125">In hello **Size** page of hello **Create virtual machine** wizard, select hello size for hello virtual machine.</span></span>

    ![Créer une machine virtuelle - Sélection de la taille](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="6b842-127">Bonjour **paramètres** page Hello **créer la machine virtuelle** compte de stockage hello Assistant, sélectionnez pour l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-127">In hello **Settings** page of hello **Create virtual machine** wizard, select hello storage account for hello virtual machine.</span></span> <span data-ttu-id="6b842-128">Cliquez sur **réseau virtuel** tooselect Bonjour réseau virtuel toowhich Bonjour Linux VM doit être déployé.</span><span class="sxs-lookup"><span data-stu-id="6b842-128">Click **Virtual Network** tooselect hello virtual network toowhich hello Linux VM should be deployed.</span></span> <span data-ttu-id="6b842-129">Bonjour **réseau virtuel** panneau, réseau virtuel de select hello dans lequel les Services de domaine Active Directory Azure est disponible.</span><span class="sxs-lookup"><span data-stu-id="6b842-129">In hello **Virtual Network** blade, select hello virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="6b842-130">Dans cet exemple, nous choisir réseau virtuel de hello 'MyPreviewVNet'.</span><span class="sxs-lookup"><span data-stu-id="6b842-130">In this example, we pick hello 'MyPreviewVNet' virtual network.</span></span>

    ![Créer une machine virtuelle - Sélection du réseau virtuel](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="6b842-132">Sur hello **Résumé** page Hello **créer la machine virtuelle** hello Assistant, révision, cliquez sur **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="6b842-132">On hello **Summary** page of hello **Create virtual machine** wizard, review and click hello **OK** button.</span></span>

    ![Créer une machine virtuelle - Réseau virtuel sélectionné](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="6b842-134">Déploiement du nouvel ordinateur virtuel hello, basé sur l’image de hello RHEL 7.2 doit démarrer.</span><span class="sxs-lookup"><span data-stu-id="6b842-134">Deployment of hello new virtual machine based on hello RHEL 7.2 image should start.</span></span>

    ![Créer une machine virtuelle - Déploiement démarré](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="6b842-136">Après quelques minutes, hello virtuels doit être déployé avec succès et prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="6b842-136">After a few minutes, hello virtual machine should be deployed successfully and ready for use.</span></span>

    ![Créer une machine virtuelle - Déployée](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="6b842-138">Se connecter à distance une machine virtuelle Linux toohello qui vient d’être mis en service.</span><span class="sxs-lookup"><span data-stu-id="6b842-138">Connect remotely toohello newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="6b842-139">machine virtuelle de Hello RHEL 7.2 a été configuré dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6b842-139">hello RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="6b842-140">la tâche suivante Hello est tooconnect à distance virtuels toohello.</span><span class="sxs-lookup"><span data-stu-id="6b842-140">hello next task is tooconnect remotely toohello virtual machine.</span></span>

<span data-ttu-id="6b842-141">**Connecter toohello RHEL 7.2 virtual machine** suivez les instructions de hello dans l’article de hello [comment toolog sur l’ordinateur virtuel de tooa exécutant Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b842-141">**Connect toohello RHEL 7.2 virtual machine** Follow hello instructions in hello article [How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6b842-142">Hello étapes restantes de hello supposent que vous utilisez hello PuTTY SSH tooconnect toohello RHEL ordinateur virtuel client.</span><span class="sxs-lookup"><span data-stu-id="6b842-142">hello rest of hello steps assume you use hello PuTTY SSH client tooconnect toohello RHEL virtual machine.</span></span> <span data-ttu-id="6b842-143">Pour plus d’informations, consultez hello [page de téléchargement de PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="6b842-143">For more information, see hello [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="6b842-144">Ouvrez hello PuTTY programme.</span><span class="sxs-lookup"><span data-stu-id="6b842-144">Open hello PuTTY program.</span></span>
2. <span data-ttu-id="6b842-145">Entrez hello **nom d’hôte** pour hello nouvellement créé RHEL virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6b842-145">Enter hello **Host Name** for hello newly created RHEL virtual machine.</span></span> <span data-ttu-id="6b842-146">Dans cet exemple, la machine virtuelle a le nom d’hôte hello « contoso-rhel.cloudapp .net ».</span><span class="sxs-lookup"><span data-stu-id="6b842-146">In this example, our virtual machine has hello host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="6b842-147">Si vous n’êtes pas sûr du nom d’hôte hello de votre machine virtuelle, consultez toohello tableau de bord de machine virtuelle sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6b842-147">If you are not sure of hello host name of your VM, refer toohello VM dashboard on hello Azure portal.</span></span>

    ![Connexion PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="6b842-149">Ouvrez une session sur l’ordinateur virtuel de toohello à l’aide des informations d’identification de l’administrateur local hello que vous avez spécifié lors de la machine virtuelle de hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="6b842-149">Log on toohello virtual machine using hello local administrator credentials you specified when hello virtual machine was created.</span></span> <span data-ttu-id="6b842-150">Dans cet exemple, nous avons utilisé le compte d’administrateur local hello « mahesh ».</span><span class="sxs-lookup"><span data-stu-id="6b842-150">In this example, we used hello local administrator account "mahesh".</span></span>

    ![Connexion PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a><span data-ttu-id="6b842-152">Installer les packages requis sur une machine virtuelle Linux hello</span><span class="sxs-lookup"><span data-stu-id="6b842-152">Install required packages on hello Linux virtual machine</span></span>
<span data-ttu-id="6b842-153">Après connexion machine virtuelle toohello, la tâche suivante hello est tooinstall les packages requis pour la jonction de domaine sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-153">After connecting toohello virtual machine, hello next task is tooinstall packages required for domain join on hello virtual machine.</span></span> <span data-ttu-id="6b842-154">Effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6b842-154">Perform hello following steps:</span></span>

1. <span data-ttu-id="6b842-155">**Installer realmd :** package realmd de hello est utilisé pour la jonction de domaine.</span><span class="sxs-lookup"><span data-stu-id="6b842-155">**Install realmd:** hello realmd package is used for domain join.</span></span> <span data-ttu-id="6b842-156">Dans votre terminal PuTTY, tapez Bonjour de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6b842-156">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="6b842-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="6b842-157">sudo yum install realmd</span></span>

    ![Installation de realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="6b842-159">Après quelques minutes, package de realmd hello doit obtenir installé sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-159">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![Package realmd installé](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="6b842-161">**Installer sssd :** hello realmd package en dépend des opérations de jointure sssd tooperform domaine.</span><span class="sxs-lookup"><span data-stu-id="6b842-161">**Install sssd:** hello realmd package depends on sssd tooperform domain join operations.</span></span> <span data-ttu-id="6b842-162">Dans votre terminal PuTTY, tapez Bonjour de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6b842-162">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="6b842-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="6b842-163">sudo yum install sssd</span></span>

    ![Installation de sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="6b842-165">Après quelques minutes, package de sssd hello doit obtenir installé sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-165">After a few minutes, hello sssd package should get installed on hello virtual machine.</span></span>

    ![Package realmd installé](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="6b842-167">**Installer kerberos :** dans votre terminal PuTTY, tapez Bonjour de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6b842-167">**Install kerberos:** In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="6b842-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="6b842-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Installation de Kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="6b842-170">Après quelques minutes, package de realmd hello doit obtenir installé sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-170">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![Kerberos installé](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a><span data-ttu-id="6b842-172">Joindre le domaine géré des toohello machine virtuelle Linux hello</span><span class="sxs-lookup"><span data-stu-id="6b842-172">Join hello Linux virtual machine toohello managed domain</span></span>
<span data-ttu-id="6b842-173">Maintenant que les packages hello requis sont installés sur une machine virtuelle Linux hello, la tâche suivante hello est toojoin hello machine virtuelle toohello domaine géré.</span><span class="sxs-lookup"><span data-stu-id="6b842-173">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

1. <span data-ttu-id="6b842-174">Découvrir le domaine géré de Services de domaine AAD hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-174">Discover hello AAD Domain Services managed domain.</span></span> <span data-ttu-id="6b842-175">Dans votre terminal PuTTY, tapez Bonjour de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6b842-175">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="6b842-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="6b842-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="6b842-178">Si **domaine découvrir** est toofind Impossible de votre domaine géré, assurez-vous que ce domaine hello est accessible à partir de la machine virtuelle de hello (ping réessayer).</span><span class="sxs-lookup"><span data-stu-id="6b842-178">If **realm discover** is unable toofind your managed domain, ensure that hello domain is reachable from hello virtual machine (try ping).</span></span> <span data-ttu-id="6b842-179">Vérifiez également que l’ordinateur virtuel hello a été effectivement déployé toohello même réseau virtuel dans le hello domaine géré est disponible.</span><span class="sxs-lookup"><span data-stu-id="6b842-179">Also ensure that hello virtual machine has indeed been deployed toohello same virtual network in which hello managed domain is available.</span></span>
2. <span data-ttu-id="6b842-180">Initialisez Kerberos.</span><span class="sxs-lookup"><span data-stu-id="6b842-180">Initialize kerberos.</span></span> <span data-ttu-id="6b842-181">Dans votre terminal PuTTY, tapez Bonjour commande suivante.</span><span class="sxs-lookup"><span data-stu-id="6b842-181">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="6b842-182">Veillez à spécifier un utilisateur qui appartient le groupe de toohello « administrateurs de contrôleur de domaine AAD ».</span><span class="sxs-lookup"><span data-stu-id="6b842-182">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="6b842-183">Seuls ces utilisateurs peuvent joindre le domaine géré des ordinateurs toohello.</span><span class="sxs-lookup"><span data-stu-id="6b842-183">Only these users can join computers toohello managed domain.</span></span>

    <span data-ttu-id="6b842-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="6b842-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="6b842-186">Assurez-vous que vous spécifiez le nom de domaine hello en majuscules, kinit autre échoue.</span><span class="sxs-lookup"><span data-stu-id="6b842-186">Ensure that you specify hello domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="6b842-187">Joindre le domaine toohello hello.</span><span class="sxs-lookup"><span data-stu-id="6b842-187">Join hello machine toohello domain.</span></span> <span data-ttu-id="6b842-188">Dans votre terminal PuTTY, tapez Bonjour commande suivante.</span><span class="sxs-lookup"><span data-stu-id="6b842-188">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="6b842-189">Spécifiez hello même utilisateur que vous avez spécifié dans hello précédant l’étape ('kinit »).</span><span class="sxs-lookup"><span data-stu-id="6b842-189">Specify hello same user you specified in hello preceding step ('kinit').</span></span>

    <span data-ttu-id="6b842-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="6b842-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Jonction de domaine](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="6b842-192">Vous devez obtenir un message (« correctement inscrit ordinateur du domaine ») lorsque la machine de hello est domaine géré de toohello a correctement été jointe.</span><span class="sxs-lookup"><span data-stu-id="6b842-192">You should get a message ("Successfully enrolled machine in realm") when hello machine is successfully joined toohello managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="6b842-193">Vérifier la jonction de domaine</span><span class="sxs-lookup"><span data-stu-id="6b842-193">Verify domain join</span></span>
<span data-ttu-id="6b842-194">Vous pouvez vérifier rapidement si la machine de hello a été domaine géré de toohello a correctement été jointe.</span><span class="sxs-lookup"><span data-stu-id="6b842-194">You can quickly verify whether hello machine has been successfully joined toohello managed domain.</span></span> <span data-ttu-id="6b842-195">Se connecter toohello VM RHEL si le compte d’utilisateur hello est correctement résolue à l’aide de SSH et un compte d’utilisateur de domaine, puis cocher toosee qui vient d’être joint à un domaine.</span><span class="sxs-lookup"><span data-stu-id="6b842-195">Connect toohello newly domain joined RHEL VM using SSH and a domain user account and then check toosee if hello user account is resolved correctly.</span></span>

1. <span data-ttu-id="6b842-196">Dans votre terminal, PuTTY hello du type suivant toohello tooconnect de commande qui vient d’être joints à un domaine virtuels RHEL à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="6b842-196">In your PuTTY terminal, type hello following command tooconnect toohello newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="6b842-197">Utiliser un compte de domaine auquel appartient le domaine géré de toohello (par exemple, 'bob@CONTOSO100.COM' dans ce cas.)</span><span class="sxs-lookup"><span data-stu-id="6b842-197">Use a domain account that belongs toohello managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="6b842-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="6b842-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="6b842-199">Dans votre terminal PuTTY, tapez hello suivant commande toosee si répertoire hello a été correctement initialisé.</span><span class="sxs-lookup"><span data-stu-id="6b842-199">In your PuTTY terminal, type hello following command toosee if hello home directory was initialized correctly.</span></span>

    <span data-ttu-id="6b842-200">pwd</span><span class="sxs-lookup"><span data-stu-id="6b842-200">pwd</span></span>
3. <span data-ttu-id="6b842-201">Dans votre terminal PuTTY, tapez hello suivant commande toosee si les appartenances aux groupes hello sont résolus correctement.</span><span class="sxs-lookup"><span data-stu-id="6b842-201">In your PuTTY terminal, type hello following command toosee if hello group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="6b842-202">id</span><span class="sxs-lookup"><span data-stu-id="6b842-202">id</span></span>

<span data-ttu-id="6b842-203">Vous trouverez ci-dessous un exemple de sortie de ces commandes :</span><span class="sxs-lookup"><span data-stu-id="6b842-203">A sample output of these commands follows:</span></span>

![Vérifier la jonction de domaine](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="6b842-205">Résolution des problèmes de jonction de domaine</span><span class="sxs-lookup"><span data-stu-id="6b842-205">Troubleshooting domain join</span></span>
<span data-ttu-id="6b842-206">Consultez toohello [jonction de domaine de résolution des problèmes](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) l’article.</span><span class="sxs-lookup"><span data-stu-id="6b842-206">Refer toohello [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="6b842-207">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="6b842-207">Related Content</span></span>
* [<span data-ttu-id="6b842-208">Services de domaine Azure AD : guide de prise en main</span><span class="sxs-lookup"><span data-stu-id="6b842-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="6b842-209">Joindre un domaine des Services de domaine Active Directory de Azure géré tooan de machine virtuelle Windows Server</span><span class="sxs-lookup"><span data-stu-id="6b842-209">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="6b842-210">[Comment toolog sur l’ordinateur virtuel de tooa exécutant Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b842-210">[How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="6b842-211">Installing Kerberos (Installation de Kerberos)</span><span class="sxs-lookup"><span data-stu-id="6b842-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="6b842-212">Red Hat Enterprise Linux 7 - Windows Integration Guide (Red Hat Enterprise Linux 7 - Guide d’intégration à Windows)</span><span class="sxs-lookup"><span data-stu-id="6b842-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
