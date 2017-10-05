---
title: Sauvegarder des serveurs VMware avec le serveur de sauvegarde Azure | Microsoft Docs
description: "Utilisez le serveur de sauvegarde Azure pour sauvegarder des serveurs VMware vCenter et VMware ESXi dans Azure ou sur un disque. Cet article fournit des instructions étape par étape pour sauvegarder (ou protéger) vos charges de travail VMware."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: ad331dffb7c31d12290f4223967c568e4535fe3c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-a-vmware-server-to-azure"></a><span data-ttu-id="7bbda-104">Sauvegarder un serveur VMware dans Azure</span><span class="sxs-lookup"><span data-stu-id="7bbda-104">Back up a VMware server to Azure</span></span>

<span data-ttu-id="7bbda-105">Cet article explique comment configurer un serveur de sauvegarde Azure pour contribuer à la protection des charges de travail de serveur VMware.</span><span class="sxs-lookup"><span data-stu-id="7bbda-105">This article explains how to configure Azure Backup Server to help protect VMware server workloads.</span></span> <span data-ttu-id="7bbda-106">Cet article suppose que vous avez déjà installé le serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="7bbda-107">Si vous n’avez pas installé de serveur de sauvegarde Azure, voir [Préparer la sauvegarde des charges de travail à l’aide du serveur de sauvegarde Azure](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="7bbda-107">If you don't have Azure Backup Server installed, see [Prepare to back up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="7bbda-108">Un serveur de sauvegarde Azure peut sauvegarder ou aider à protéger les versions 6.5, 6.0 et 5.5 de VMware vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="7bbda-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-to-the-vcenter-server"></a><span data-ttu-id="7bbda-109">Créer une connexion sécurisée au serveur vCenter</span><span class="sxs-lookup"><span data-stu-id="7bbda-109">Create a secure connection to the vCenter Server</span></span>

<span data-ttu-id="7bbda-110">Par défaut, le serveur de sauvegarde Azure communique avec chaque serveur vCenter via un canal HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7bbda-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="7bbda-111">Pour activer la communication sécurisée, nous vous recommandons d’installer le certificat de l’autorité de certification VMware sur le serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-111">To turn on the secure communication, we recommend that you install the VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="7bbda-112">Si vous n’avez pas besoin de communication sécurisée et préférez désactiver l’obligation d’utiliser le protocole HTTPS, voir [Désactiver le protocole de communication sécurisée](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="7bbda-112">If you don't require secure communication, and would prefer to disable the HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="7bbda-113">Pour créer une connexion sécurisée entre le serveur de sauvegarde Azure et le serveur vCenter, importez le certificat approuvé sur le serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-113">To create a secure connection between Azure Backup Server and the vCenter Server, import the trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="7bbda-114">En général, vous utilisez un navigateur sur le serveur de sauvegarde Azure pour vous connecter au serveur vCenter via le client web vSphere.</span><span class="sxs-lookup"><span data-stu-id="7bbda-114">Typically, you use a browser on the Azure Backup Server machine to connect to the vCenter Server via the vSphere Web Client.</span></span> <span data-ttu-id="7bbda-115">La première fois que vous utilisez le navigateur du serveur de sauvegarde Azure pour vous connecter au serveur vCenter, la connexion n’est pas sécurisée.</span><span class="sxs-lookup"><span data-stu-id="7bbda-115">The first time you use the Azure Backup Server browser to connect to the vCenter Server, the connection isn't secure.</span></span> <span data-ttu-id="7bbda-116">L’illustration suivante montre une connexion non sécurisée.</span><span class="sxs-lookup"><span data-stu-id="7bbda-116">The following image shows the unsecured connection.</span></span>

![Exemple de connexion non sécurisée à un serveur VMware](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="7bbda-118">Pour résoudre ce problème, et créer une connexion sécurisée, téléchargez les certificats approuvés de l’autorité de certification racine.</span><span class="sxs-lookup"><span data-stu-id="7bbda-118">To fix this issue, and create a secure connection, download the trusted root CA certificates.</span></span>

1. <span data-ttu-id="7bbda-119">Dans le navigateur sur le serveur de sauvegarde Azure, entrez l’URL du client web vSphere.</span><span class="sxs-lookup"><span data-stu-id="7bbda-119">In the browser on Azure Backup Server, enter the URL to the vSphere Web Client.</span></span> <span data-ttu-id="7bbda-120">La page de connexion du client web vSphere s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7bbda-120">The vSphere Web Client login page appears.</span></span>

    ![Client web vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="7bbda-122">En bas des informations destinées aux administrateurs et aux développeurs se trouve le lien **Télécharger les certificats d’autorités de certification racines de confiance**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-122">At the bottom of the information for administrators and developers, locate the **Download trusted root CA certificates** link.</span></span>

    ![Lien de téléchargement des certificats d’autorités de certification racines de confiance](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="7bbda-124">Si la page de connexion au client web vSphere n’apparaît pas, vérifiez les paramètres de proxy de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="7bbda-124">If you don't see the vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="7bbda-125">Cliquez sur **Télécharger les certificats approuvés de l’autorité de certification racine**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="7bbda-126">Le serveur vCenter télécharge un fichier sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="7bbda-126">The vCenter Server downloads a file to your local computer.</span></span> <span data-ttu-id="7bbda-127">Le nom du fichier est **download**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-127">The file's name is named **download**.</span></span> <span data-ttu-id="7bbda-128">En fonction de votre navigateur, vous recevez un message vous demandant d’ouvrir ou d’enregistrer le fichier.</span><span class="sxs-lookup"><span data-stu-id="7bbda-128">Depending on your browser, you receive a message that asks whether to open or save the file.</span></span>

    ![message de téléchargement lorsque les certificats sont téléchargés](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="7bbda-130">Enregistrez le fichier à un emplacement du serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-130">Save the file to a location on Azure Backup Server.</span></span> <span data-ttu-id="7bbda-131">Lorsque vous enregistrez le fichier, ajoutez l’extension de nom de fichier .zip.</span><span class="sxs-lookup"><span data-stu-id="7bbda-131">When you save the file, add the .zip file name extension.</span></span>

    <span data-ttu-id="7bbda-132">Le fichier est un fichier .zip qui contient des informations sur les certificats.</span><span class="sxs-lookup"><span data-stu-id="7bbda-132">The file is a .zip file that contains the information about the certificates.</span></span> <span data-ttu-id="7bbda-133">Avec l’extension .zip, vous pouvez utiliser les outils d’extraction.</span><span class="sxs-lookup"><span data-stu-id="7bbda-133">With the .zip extension, you can use the extraction tools.</span></span>

4. <span data-ttu-id="7bbda-134">Cliquez avec le bouton droit sur **download.zip**, puis sélectionnez **Extraire tout** pour extraire le contenu.</span><span class="sxs-lookup"><span data-stu-id="7bbda-134">Right-click **download.zip**, and then select **Extract All** to extract the contents.</span></span>

    <span data-ttu-id="7bbda-135">Le fichier .zip extrait son contenu dans un dossier nommé **certs**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-135">The .zip file extracts its contents to a folder named **certs**.</span></span> <span data-ttu-id="7bbda-136">Deux types de fichiers figurent dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="7bbda-136">Two types of files appear in the certs folder.</span></span> <span data-ttu-id="7bbda-137">Le fichier de certificat racine est doté d’une extension qui commence par une séquence numérotée comme .0 et .1.</span><span class="sxs-lookup"><span data-stu-id="7bbda-137">The root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="7bbda-138">Le fichier CRL est doté d’une extension qui commence par une séquence comme .r0 ou .r1.</span><span class="sxs-lookup"><span data-stu-id="7bbda-138">The CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="7bbda-139">Le fichier CRL est associé à un certificat.</span><span class="sxs-lookup"><span data-stu-id="7bbda-139">The CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="7bbda-140">Fichier de téléchargement extrait localement</span><span class="sxs-lookup"><span data-stu-id="7bbda-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="7bbda-141">Dans le dossier **certs**, cliquez avec le bouton droit sur le fichier de certificat racine, puis cliquez sur **Renommer**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-141">In the **certs** folder, right-click the root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="7bbda-142">Renommer un certificat racine</span><span class="sxs-lookup"><span data-stu-id="7bbda-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="7bbda-143">Remplacez l’extension du certificat racine par .crt.</span><span class="sxs-lookup"><span data-stu-id="7bbda-143">Change the root certificate's extension to .crt.</span></span> <span data-ttu-id="7bbda-144">Lorsqu’un message s’affiche vous demandant si vous voulez vraiment modifier l’extension, cliquez sur **Oui** ou sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-144">When you're asked if you're sure you want to change the extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="7bbda-145">Dans le cas contraire, vous modifiez la fonction du fichier.</span><span class="sxs-lookup"><span data-stu-id="7bbda-145">Otherwise, you change the file's intended function.</span></span> <span data-ttu-id="7bbda-146">L’icône du fichier est remplacée par une icône représentant un certificat racine.</span><span class="sxs-lookup"><span data-stu-id="7bbda-146">The icon for the file changes to an icon that represents a root certificate.</span></span>

6. <span data-ttu-id="7bbda-147">Cliquez sur le certificat racine et dans le menu contextuel, sélectionnez **Installer le certificat**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-147">Right-click the root certificate and from the pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="7bbda-148">La boîte de dialogue **Assistant Importation de certificat** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="7bbda-148">The **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="7bbda-149">Dans la boîte de dialogue **Assistant Importation de certificat**, sélectionnez **Ordinateur Local** comme destination du certificat, puis cliquez sur **Suivant** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="7bbda-149">In the **Certificate Import Wizard** dialog box, select **Local Machine** as the destination for the certificate, and then click **Next** to continue.</span></span>

    ![<span data-ttu-id="7bbda-150">Options de destination de stockage du certificat</span><span class="sxs-lookup"><span data-stu-id="7bbda-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="7bbda-151">Si un message vous demande si vous voulez autoriser les modifications sur cet ordinateur, cliquez sur **Oui** ou sur **OK**, pour toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="7bbda-151">If you're asked if you want to allow changes to the computer, click **Yes** or **OK**, to all the changes.</span></span>

8. <span data-ttu-id="7bbda-152">Dans la page **Magasin de certificats**, sélectionnez **Placer tous les certificats dans le magasin suivant**, puis cliquez sur **Parcourir** pour choisir un magasin.</span><span class="sxs-lookup"><span data-stu-id="7bbda-152">On the **Certificate Store** page, select **Place all certificates in the following store**, and then click **Browse** to choose the certificate store.</span></span>

    ![Placer des certificats dans une zone de stockage spécifique](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="7bbda-154">La boîte de dialogue **Sélectionner un magasin de certificats** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7bbda-154">The **Select Certificate Store** dialog box appears.</span></span>

    ![Arborescence des dossiers de stockage de certificats](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="7bbda-156">Sélectionnez **Autorités de certification racines de confiance** comme dossier de destination des certificats, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-156">Select **Trusted Root Certification Authorities** as the destination folder for the certificates, and then click **OK**.</span></span>

    ![Dossier de destination des certificats](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="7bbda-158">Le dossier **Autorités de certification racines de confiance**  est confirmé comme magasin de certificats.</span><span class="sxs-lookup"><span data-stu-id="7bbda-158">The **Trusted Root Certification Authorities** folder is confirmed as the certificate store.</span></span> <span data-ttu-id="7bbda-159">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-159">Click **Next**.</span></span>

    ![Dossier de magasin de certificats](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="7bbda-161">Dans la page **Fin de l’Assistant Importation du certificat**, vérifiez que le certificat se trouve dans le dossier souhaité, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-161">On the **Completing the Certificate Import Wizard** page, verify that the certificate is in the desired folder, and then click **Finish**.</span></span>

    ![Vérifier que le certificat se trouve dans le dossier approprié](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="7bbda-163">Une boîte de dialogue s’affiche, confirmant l’importation réussie du certificat.</span><span class="sxs-lookup"><span data-stu-id="7bbda-163">A dialog box appears, the successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="7bbda-164">Connectez-vous au serveur vCenter pour vérifier que votre connexion est sécurisée.</span><span class="sxs-lookup"><span data-stu-id="7bbda-164">Sign in to the vCenter Server to confirm that your connection is secure.</span></span>

  <span data-ttu-id="7bbda-165">Si l’importation du certificat échoue et si vous ne parvenez pas à établir une connexion sécurisée, consultez la documentation sur VMware vSphere dans [Obtaining server certificates (Obtention de certificats de serveur)](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="7bbda-165">If the certificate import is not successful, and you cannot establish a secure connection, consult the VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="7bbda-166">Si votre organisation comprend des limites sécurisées et que vous ne souhaitez pas activer le protocole HTTPS, désactivez la communication sécurisée en procédant comme suit.</span><span class="sxs-lookup"><span data-stu-id="7bbda-166">If you have secure boundaries within your organization, and don't want to turn on the HTTPS protocol, use the following procedure to disable the secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="7bbda-167">Désactiver le protocole de communication sécurisée</span><span class="sxs-lookup"><span data-stu-id="7bbda-167">Disable secure communication protocol</span></span>

<span data-ttu-id="7bbda-168">Si votre organisation n’a pas besoin d’un protocole HTTPS, désactivez-le en procédant comme suit.</span><span class="sxs-lookup"><span data-stu-id="7bbda-168">If your organization doesn't require the HTTPS protocol, use the following steps to disable HTTPS.</span></span> <span data-ttu-id="7bbda-169">Pour désactiver le comportement par défaut, créez une clé de Registre qui ignore le comportement par défaut.</span><span class="sxs-lookup"><span data-stu-id="7bbda-169">To disable the default behavior, create a registry key that ignores the default behavior.</span></span>

1. <span data-ttu-id="7bbda-170">Copiez et collez le texte suivant dans un fichier .txt.</span><span class="sxs-lookup"><span data-stu-id="7bbda-170">Copy and paste the following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="7bbda-171">Enregistrez le fichier sur votre ordinateur serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-171">Save the file to your Azure Backup Server computer.</span></span> <span data-ttu-id="7bbda-172">Utilisez DisableSecureAuthentication.reg comme nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="7bbda-172">For the file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="7bbda-173">Double-cliquez sur le fichier pour activer l’entrée de Registre.</span><span class="sxs-lookup"><span data-stu-id="7bbda-173">Double-click the file to activate the registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-the-vcenter-server"></a><span data-ttu-id="7bbda-174">Créer un rôle et un compte d’utilisateur sur le serveur vCenter</span><span class="sxs-lookup"><span data-stu-id="7bbda-174">Create a role and user account on the vCenter Server</span></span>

<span data-ttu-id="7bbda-175">Sur le serveur vCenter, un rôle est un ensemble de privilèges prédéfini.</span><span class="sxs-lookup"><span data-stu-id="7bbda-175">On the vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="7bbda-176">Un administrateur de serveur vCenter crée les rôles.</span><span class="sxs-lookup"><span data-stu-id="7bbda-176">A vCenter Server administrator creates the roles.</span></span> <span data-ttu-id="7bbda-177">Pour attribuer des autorisations, l’administrateur associe des comptes d’utilisateur à un rôle.</span><span class="sxs-lookup"><span data-stu-id="7bbda-177">To assign permissions, the administrator pairs user accounts with a role.</span></span> <span data-ttu-id="7bbda-178">Pour définir les informations d’identification d’utilisateur nécessaires pour sauvegarder l’ordinateur serveur vCenter, créez un rôle pourvu de privilèges spécifiques, puis associez le compte d’utilisateur au rôle.</span><span class="sxs-lookup"><span data-stu-id="7bbda-178">To establish the necessary user credentials to back up the vCenter Server computer, create a role with specific privileges, and then associate the user account with the role.</span></span>

<span data-ttu-id="7bbda-179">Le serveur de sauvegarde Azure utilise un nom d’utilisateur et un mot de passe pour s’authentifier auprès du serveur vCenter.</span><span class="sxs-lookup"><span data-stu-id="7bbda-179">Azure Backup Server uses a username and password to authenticate with the vCenter Server.</span></span> <span data-ttu-id="7bbda-180">Le serveur de sauvegarde Azure utilise ces informations d’identification comme authentification pour toutes les opérations de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="7bbda-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="7bbda-181">Pour ajouter un rôle de serveur vCenter et ses privilèges pour un administrateur de sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="7bbda-181">To add a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="7bbda-182">Connectez-vous au serveur vCenter, puis, dans le panneau **Navigateur** du serveur vCenter, cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-182">Sign in to the vCenter Server, and then in the vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Option d’administration dans le panneau Navigateur du serveur vCenter](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="7bbda-184">Dans **Administration**, sélectionnez **Rôles**, puis, dans le panneau **Rôles**, cliquez sur l’icône d’ajout de rôle (symbole +).</span><span class="sxs-lookup"><span data-stu-id="7bbda-184">In **Administration** select **Roles**, and then in the **Roles** panel click the add role icon (the + symbol).</span></span>

    ![Ajouter un rôle](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="7bbda-186">La boîte de dialogue **Créer un rôle** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7bbda-186">The **Create Role** dialog box appears.</span></span>

    ![Créer un rôle](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="7bbda-188">Dans la boîte de dialogue **Créer un rôle**, dans la zone **Nom du rôle**, entrez *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="7bbda-188">In the **Create Role** dialog box, in the **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="7bbda-189">Vous pouvez choisir n’importe quel nom de rôle, à condition qu’il permettre de reconnaître l’objectif du rôle.</span><span class="sxs-lookup"><span data-stu-id="7bbda-189">The role name can be whatever you like, but it should be recognizable for the role's purpose.</span></span>

4. <span data-ttu-id="7bbda-190">Sélectionnez les privilèges correspondant à la version appropriée de vCenter, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-190">Select the privileges for the appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="7bbda-191">Le tableau suivant identifie les privilèges requis pour vCenter versions 6.0 et 5.5.</span><span class="sxs-lookup"><span data-stu-id="7bbda-191">The following table identifies the required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="7bbda-192">Lorsque vous sélectionnez les privilèges, cliquez sur l’icône située à côté de l’étiquette du parent pour développer le parent et afficher les privilèges enfant.</span><span class="sxs-lookup"><span data-stu-id="7bbda-192">When you select the privileges, click the icon next to the parent label to expand the parent and view the child privileges.</span></span> <span data-ttu-id="7bbda-193">Pour sélectionner les privilèges VirtualMachine, vous devez atteindre plusieurs niveaux dans la hiérarchie parent-enfant.</span><span class="sxs-lookup"><span data-stu-id="7bbda-193">To select the VirtualMachine privileges, you need to go several levels into the parent child hierarchy.</span></span> <span data-ttu-id="7bbda-194">Vous n’avez pas besoin de sélectionner tous les privilèges enfant au sein d’un privilège parent.</span><span class="sxs-lookup"><span data-stu-id="7bbda-194">You don't need to select all child privileges within a parent privilege.</span></span>

  ![Hiérarchie des privilèges parent-enfant](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="7bbda-196">Après que vous avez cliqué sur **OK**, le nouveau rôle s’affiche dans la liste du panneau Rôles.</span><span class="sxs-lookup"><span data-stu-id="7bbda-196">After you click **OK**, the new role appears in the list on the Roles panel.</span></span>

|<span data-ttu-id="7bbda-197">Privilèges de vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="7bbda-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="7bbda-198">Privilèges de vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="7bbda-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="7bbda-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="7bbda-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="7bbda-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="7bbda-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="7bbda-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="7bbda-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="7bbda-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="7bbda-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="7bbda-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="7bbda-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="7bbda-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="7bbda-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="7bbda-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="7bbda-205">Network.Assign</span></span> |
|<span data-ttu-id="7bbda-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="7bbda-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="7bbda-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="7bbda-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="7bbda-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="7bbda-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="7bbda-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="7bbda-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="7bbda-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="7bbda-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="7bbda-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="7bbda-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="7bbda-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="7bbda-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="7bbda-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="7bbda-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="7bbda-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="7bbda-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="7bbda-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="7bbda-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="7bbda-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="7bbda-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="7bbda-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="7bbda-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="7bbda-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="7bbda-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="7bbda-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="7bbda-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="7bbda-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="7bbda-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="7bbda-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="7bbda-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="7bbda-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="7bbda-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="7bbda-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="7bbda-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="7bbda-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="7bbda-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="7bbda-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="7bbda-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="7bbda-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="7bbda-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="7bbda-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="7bbda-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="7bbda-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="7bbda-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="7bbda-229">Créer un compte d’utilisateur et des autorisations pour un serveur vCenter</span><span class="sxs-lookup"><span data-stu-id="7bbda-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="7bbda-230">Une fois que le rôle est configuré avec des privilèges, créez un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7bbda-230">After the role with privileges is set up, create a user account.</span></span> <span data-ttu-id="7bbda-231">Le compte d’utilisateur possède un nom et un mot de passe, qui représentent les informations d’identification utilisées pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="7bbda-231">The user account has a name and password, which provides the credentials that are used for authentication.</span></span>

1. <span data-ttu-id="7bbda-232">Pour créer un compte d’utilisateur, dans le panneau **Navigateur** du serveur vCenter, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-232">To create a user account, in the vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Option Utilisateurs et groupes](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="7bbda-234">Le panneau **Utilisateurs et groupes vCenter** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7bbda-234">The **vCenter Users and Groups** panel appears.</span></span>

    ![Panneau Utilisateurs et groupes vCenter](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="7bbda-236">Dans le panneau **Utilisateurs et groupes vCenter**, dans l’onglet **Utilisateurs**, cliquez sur l’icône d’ajout d’utilisateurs (symbole +).</span><span class="sxs-lookup"><span data-stu-id="7bbda-236">In the **vCenter Users and Groups** panel, select the **Users** tab, and then click the add users icon (the + symbol).</span></span>

    <span data-ttu-id="7bbda-237">La boîte de dialogue **Nouvel utilisateur** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7bbda-237">The **New User** dialog box appears.</span></span>

3. <span data-ttu-id="7bbda-238">Dans la boîte de dialogue **Nouvel utilisateur**, ajoutez les informations de l’utilisateur, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-238">In the **New User** dialog box, add the user's information and then click **OK**.</span></span> <span data-ttu-id="7bbda-239">Dans cette procédure, le nom d’utilisateur est BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="7bbda-239">In this procedure, the username is BackupAdmin.</span></span>

    ![Boîte de dialogue Nouvel utilisateur](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="7bbda-241">Le nouveau compte d’utilisateur s’affiche dans la liste.</span><span class="sxs-lookup"><span data-stu-id="7bbda-241">The new user account appears in the list.</span></span>

4. <span data-ttu-id="7bbda-242">Pour associer le compte d’utilisateur au rôle, dans le panneau **Navigateur**, cliquez sur **Autorisations globales**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-242">To associate the user account with the role, in the **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="7bbda-243">Dans le panneau **Autorisations globales**, dans l’onglet **Gérer**, cliquez sur l’icône d’ajout (symbole +).</span><span class="sxs-lookup"><span data-stu-id="7bbda-243">In the **Global Permissions** panel, select the **Manage** tab, and then click the add icon (the + symbol).</span></span>

    ![Panneau Autorisations globales](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="7bbda-245">La boîte de dialogue **Global Permissions Root - Add Permission** (Racine des autorisations globales - Ajouter une autorisation) s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="7bbda-245">The **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="7bbda-246">Dans la boîte de dialogue **Global Permissions Root - Add Permission** (Racine des autorisations globales - Ajouter une autorisation), cliquez sur **Ajouter** pour choisir l’utilisateur ou le groupe.</span><span class="sxs-lookup"><span data-stu-id="7bbda-246">In the **Global Permission Root - Add Permission** dialog box, click **Add** to choose the user or group.</span></span>

    ![Choisir un utilisateur ou un groupe](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="7bbda-248">La boîte de dialogue **Sélectionner des utilisateurs/groupes** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="7bbda-248">The **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="7bbda-249">Dans la boîte de dialogue **Sélectionner des utilisateurs/groupes**, sélectionnez **BackupAdmin**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-249">In the **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="7bbda-250">Dans la zone **Utilisateurs**, le format *domain\username* est utilisé pour le compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7bbda-250">In **Users**, the *domain\username* format is used for the user account.</span></span> <span data-ttu-id="7bbda-251">Si vous souhaitez utiliser un autre domaine, sélectionnez-le dans la liste **Domaine**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-251">If you want to use a different domain, choose it from the **Domain** list.</span></span>

    ![Ajouter un utilisateur BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="7bbda-253">Cliquez sur **OK** pour ajouter les utilisateurs sélectionnés à la boîte de dialogue **Ajouter une autorisation**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-253">Click **OK** to add the selected users to the **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="7bbda-254">Maintenant que vous avez identifié l’utilisateur, vous devez lui affecter le rôle.</span><span class="sxs-lookup"><span data-stu-id="7bbda-254">Now that you've identified the user, assign the user to the role.</span></span> <span data-ttu-id="7bbda-255">Dans **Rôle attribué**, dans la liste déroulante, sélectionnez **BackupAdminRole**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-255">In **Assigned Role**, from the drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Affecter un utilisateur à un rôle](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="7bbda-257">Dans l’onglet **Gérer** du panneau **Autorisations globales**, le nouveau compte d’utilisateur et le rôle associé apparaissent dans la liste.</span><span class="sxs-lookup"><span data-stu-id="7bbda-257">On the **Manage** tab in the **Global Permissions** panel, the new user account and the associated role appear in the list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="7bbda-258">Définir les informations d’identification de serveur vCenter sur le serveur de sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="7bbda-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="7bbda-259">Avant d’ajouter le serveur VMware au serveur de sauvegarde Azure, installez la [mise à jour 1 du serveur de sauvegarde Azure](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="7bbda-259">Before you add the VMware server to Azure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="7bbda-260">Pour ouvrir le serveur de sauvegarde Azure, double-cliquez sur l’icône présente sur le Bureau du serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-260">To open Azure Backup Server, double-click the icon on the Azure Backup Server desktop.</span></span>

    ![Icône du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="7bbda-262">Si vous ne trouvez pas l’icône sur le Bureau, ouvrez le serveur de sauvegarde Azure dans la liste des applications installées.</span><span class="sxs-lookup"><span data-stu-id="7bbda-262">If you can't find the icon on the desktop, open Azure Backup Server from the list of installed apps.</span></span> <span data-ttu-id="7bbda-263">Le nom de l’application du serveur de sauvegarde Azure est appelé Sauvegarde Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-263">The Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="7bbda-264">Dans la console du serveur de sauvegarde Azure, cliquez sur **Gestion**, **Serveurs de production**, puis, dans la barre d’outils, sur **Gérer VMware**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-264">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then on the tool ribbon, click **Manage VMware**.</span></span>

    ![Console du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="7bbda-266">La boîte de dialogue **Gérer les informations d’identification** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7bbda-266">The **Manage Credentials** dialog box appears.</span></span>

    ![Boîte de dialogue Gérer les informations d’identification du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="7bbda-268">Dans la boîte de dialogue **Gérer les informations d’identification**, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Ajouter des informations d’identification**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-268">In the **Manage Credentials** dialog box, click **Add** to open the **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="7bbda-269">Dans la boîte de dialogue **Ajouter des informations d’identification**, entrez un nom et une description pour les nouvelles informations d’identification,</span><span class="sxs-lookup"><span data-stu-id="7bbda-269">In the **Add Credential** dialog box, enter a name and a description for the new credential.</span></span> <span data-ttu-id="7bbda-270">puis spécifiez le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7bbda-270">Then specify the username and password.</span></span> <span data-ttu-id="7bbda-271">Le nom *Contoso Vcenter credential* est utilisé pour identifier les informations d’identification dans la procédure suivante.</span><span class="sxs-lookup"><span data-stu-id="7bbda-271">The name, *Contoso Vcenter credential* is used to identify the credential in the next procedure.</span></span> <span data-ttu-id="7bbda-272">Utilisez les mêmes nom d’utilisateur et mot de passe que pour le serveur vCenter.</span><span class="sxs-lookup"><span data-stu-id="7bbda-272">Use the same username and password that is used for the vCenter Server.</span></span> <span data-ttu-id="7bbda-273">Si le serveur vCenter et le serveur de sauvegarde Azure ne se trouvent pas dans le même domaine, spécifiez le domaine dans **Nom d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-273">If the vCenter Server and Azure Backup Server are not in the same domain, in **User name**, specify the domain.</span></span>

    ![Boîte de dialogue Ajouter des informations d’identification du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="7bbda-275">Cliquez sur **Ajouter** pour ajouter les nouvelles informations d’identification au serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-275">Click **Add** to add the new credential to Azure Backup Server.</span></span> <span data-ttu-id="7bbda-276">Les nouvelles informations d’identification s’affichent dans la liste de la boîte de dialogue **Gérer les informations d’identification**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-276">The new credential appears in the list in the **Manage Credentials** dialog box.</span></span>
    
    ![Boîte de dialogue Gérer les informations d’identification du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="7bbda-278">Pour fermer la boîte de dialogue **Gérer les informations d’identification**, cliquez sur le symbole **X** dans l’angle supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="7bbda-278">To close the **Manage Credentials** dialog box, click the **X** in the upper-right corner.</span></span>


## <a name="add-the-vcenter-server-to-azure-backup-server"></a><span data-ttu-id="7bbda-279">Ajouter le serveur vCenter au serveur de sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="7bbda-279">Add the vCenter Server to Azure Backup Server</span></span>

<span data-ttu-id="7bbda-280">L’Assistant Ajout d’un serveur de production permet d’ajouter le serveur vCenter au serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-280">Production Server Addition Wizard is used to add the vCenter Server to Azure Backup Server.</span></span>

<span data-ttu-id="7bbda-281">Pour ouvrir l’Assistant Ajout d’un serveur de production, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7bbda-281">To open Production Server Addition Wizard, complete the following procedure:</span></span>

1. <span data-ttu-id="7bbda-282">Dans la console du serveur de sauvegarde Azure, cliquez sur **Gestion**, sur **Serveurs de production**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-282">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Ouvrir l’Assistant Ajout d’un serveur de production](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="7bbda-284">La boîte de dialogue **Assistant Ajout d’un serveur de production** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7bbda-284">The **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Assistant Ajout d’un serveur de production](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="7bbda-286">Dans la page **Sélectionner un type de serveur de production**, sélectionnez **Serveurs VMware**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-286">On the **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="7bbda-287">Dans **Nom du serveur/Adresse IP**, spécifiez le nom de domaine complet (FQDN) ou l’adresse IP du serveur VMware.</span><span class="sxs-lookup"><span data-stu-id="7bbda-287">In **Server Name/IP Address**, specify the fully qualified domain name (FQDN) or IP address of the VMware server.</span></span> <span data-ttu-id="7bbda-288">Vous pouvez utiliser le nom vCenter si tous les serveurs ESXi sont gérés par le même serveur vCenter.</span><span class="sxs-lookup"><span data-stu-id="7bbda-288">If all the ESXi servers are managed by the same vCenter, you can use the vCenter name.</span></span>

    ![Spécifier l’adresse IP ou le nom de domaine complet du serveur VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="7bbda-290">Dans **Port SSL**, entrez le port utilisé pour communiquer avec le serveur VMware.</span><span class="sxs-lookup"><span data-stu-id="7bbda-290">In **SSL Port**, enter the port that is used to communicate with the VMware server.</span></span> <span data-ttu-id="7bbda-291">Utilisez le port 443 (le port par défaut), sauf si vous savez que vous avez besoin d’un autre port.</span><span class="sxs-lookup"><span data-stu-id="7bbda-291">Use port 443, which is the default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="7bbda-292">Dans **Indiquer les informations d’identification**, sélectionnez les informations d’identification que vous avez créées précédemment.</span><span class="sxs-lookup"><span data-stu-id="7bbda-292">In **Specify Credential**, select the credential that you created earlier.</span></span>

    ![Indiquer les informations d’identification](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="7bbda-294">Cliquez sur **Ajouter** pour ajouter le serveur VMware à la liste des **serveurs VMware ajoutés**, puis cliquez sur **Suivant** pour passer à la page suivante de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="7bbda-294">Click **Add** to add the VMware server to the list of **Added VMware Servers**, and then click **Next** to move to the next page in the wizard.</span></span>

    ![Ajouter un serveur VMware et des informations d’identification](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="7bbda-296">Dans la page **Résumé**, cliquez sur **Ajouter** pour ajouter le serveur VMware spécifié au serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-296">In the **Summary** page, click **Add** to add the specified VMware server to Azure Backup Server.</span></span>

    ![Ajouter le serveur VMware au serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="7bbda-298">La sauvegarde du serveur VMware est une sauvegarde sans agent, et le nouveau serveur est ajouté immédiatement.</span><span class="sxs-lookup"><span data-stu-id="7bbda-298">The VMware server backup is an agentless backup, and the new server is added immediately.</span></span> <span data-ttu-id="7bbda-299">La page **Terminer** affiche les résultats.</span><span class="sxs-lookup"><span data-stu-id="7bbda-299">The **Finish** page shows you the results.</span></span>

  ![Page Terminer](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="7bbda-301">Pour ajouter plusieurs instances du serveur vCenter au serveur de sauvegarde Azure, répétez les étapes précédentes de cette section.</span><span class="sxs-lookup"><span data-stu-id="7bbda-301">To add multiple instances of vCenter Server to Azure Backup Server, repeat the previous steps in this section.</span></span>

<span data-ttu-id="7bbda-302">Après avoir ajouté le serveur vCenter au serveur de sauvegarde Azure, l’étape suivante consiste à créer un groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="7bbda-302">After you add the vCenter Server to Azure Backup Server, the next step is to create a protection group.</span></span> <span data-ttu-id="7bbda-303">Le groupe de protection spécifie les différentes informations de rétention à court ou à long terme, et vous permet de définir et appliquer la stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="7bbda-303">The protection group specifies the various details for short or long-term retention, and it is where you define and apply the backup policy.</span></span> <span data-ttu-id="7bbda-304">La stratégie de sauvegarde permet de planifier la date d’exécution des sauvegardes ainsi que leur contenu.</span><span class="sxs-lookup"><span data-stu-id="7bbda-304">The backup policy is the schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="7bbda-305">Configurer un groupe de protection</span><span class="sxs-lookup"><span data-stu-id="7bbda-305">Configure a protection group</span></span>

<span data-ttu-id="7bbda-306">Si vous n’avez pas encore utilisé System Center Data Protection Manager ni le serveur de sauvegarde Azure, voir [Planification de sauvegardes sur disque](https://technet.microsoft.com/library/hh758026.aspx) pour préparer votre environnement matériel.</span><span class="sxs-lookup"><span data-stu-id="7bbda-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) to prepare your hardware environment.</span></span> <span data-ttu-id="7bbda-307">Après avoir vérifié que vous disposez du stockage approprié, utilisez l’Assistant Création d’un nouveau groupe de protection pour ajouter des machines virtuelles VMware.</span><span class="sxs-lookup"><span data-stu-id="7bbda-307">After you check that you have proper storage, use the Create New Protection Group wizard to add VMware virtual machines.</span></span>

1. <span data-ttu-id="7bbda-308">Dans la console du serveur de sauvegarde Azure, cliquez sur **Protection**, puis cliquez sur **Nouveau** dans la barre d’outils pour ouvrir l’assistant Création d’un nouveau groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="7bbda-308">In the Azure Backup Server console, click **Protection**, and in the tool ribbon, click **New** to open the Create New Protection Group wizard.</span></span>

    ![Ouvrir l’Assistant Création d’un nouveau groupe de protection](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="7bbda-310">L’Assistant **Création d’un nouveau groupe de protection** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7bbda-310">The **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Boîte de dialogue Assistant Création d’un nouveau groupe de protection](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="7bbda-312">Cliquez sur **Suivant** pour passer à la page **Sélectionner le type de groupe de protection**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-312">Click **Next** to advance to the **Select protection group type** page.</span></span>

2. <span data-ttu-id="7bbda-313">Dans la page **Sélectionner le type de groupe de protection**, sélectionnez **Serveurs**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-313">On the **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="7bbda-314">La page **Sélectionner les membres du groupe** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7bbda-314">The **Select group members** page appears.</span></span>

3. <span data-ttu-id="7bbda-315">Dans la page **Sélectionner les membres du groupe**, les membres disponibles et les membres sélectionnés s’affichent.</span><span class="sxs-lookup"><span data-stu-id="7bbda-315">On the **Select group members** page, the available members and the selected members appear.</span></span> <span data-ttu-id="7bbda-316">Sélectionnez les membres que vous souhaitez protéger, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-316">Select the members that you want to protect, and then click **Next**.</span></span>

    ![Sélectionner les membres du groupe](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="7bbda-318">Lorsque vous sélectionnez un membre, si vous sélectionnez un dossier qui contient d’autres dossiers ou machines virtuelles, ces dossiers et machines virtuelles sont également sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="7bbda-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="7bbda-319">On appelle « protection au niveau du dossier » le fait d’inclure des dossiers et des machines virtuelles dans le dossier parent.</span><span class="sxs-lookup"><span data-stu-id="7bbda-319">The inclusion of the folders and VMs in the parent folder is called folder-level protection.</span></span> <span data-ttu-id="7bbda-320">Pour supprimer un dossier ou une machine virtuelle, décochez la case.</span><span class="sxs-lookup"><span data-stu-id="7bbda-320">To remove a folder or VM, clear the check box.</span></span>

    <span data-ttu-id="7bbda-321">Si une machine virtuelle ou un dossier contenant une machine virtuelle est déjà protégé(e) dans Azure, vous ne pouvez pas sélectionner de nouveau cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7bbda-321">If a VM, or a folder containing a VM, is already protected to Azure, you cannot select that VM again.</span></span> <span data-ttu-id="7bbda-322">Autrement dit, une fois qu’une machine virtuelle est protégée dans Azure, elle ne peut pas être de nouveau protégée, ce qui empêche la création de points de récupération en double pour une même machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7bbda-322">That is, after a VM is protected to Azure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="7bbda-323">Si vous souhaitez connaître l’instance de serveur de sauvegarde Azure qui protège déjà un membre, pointez sur le membre pour visualiser le nom du serveur de protection.</span><span class="sxs-lookup"><span data-stu-id="7bbda-323">If you want to see which Azure Backup Server instance already protects a member, point to the member to see the name of the protecting server.</span></span>

4. <span data-ttu-id="7bbda-324">Dans la page **Sélectionner la méthode de protection des données**, entrez le nom du groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="7bbda-324">On the **Select Data Protection Method** page, enter a name for the protection group.</span></span> <span data-ttu-id="7bbda-325">Les options Protection à court terme (sur disque) et Protection en ligne sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="7bbda-325">Short-term protection (to disk) and online protection are selected.</span></span> <span data-ttu-id="7bbda-326">Si vous souhaitez utiliser la protection en ligne (sur Azure), vous devez utiliser la protection à court terme sur disque.</span><span class="sxs-lookup"><span data-stu-id="7bbda-326">If you want to use online protection (to Azure), you must use short-term protection to disk.</span></span> <span data-ttu-id="7bbda-327">Cliquez sur **Suivant** pour passer à la plage de protection à court terme.</span><span class="sxs-lookup"><span data-stu-id="7bbda-327">Click **Next** to proceed to the short-term protection range.</span></span>

    ![Sélectionner la méthode de protection des données](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="7bbda-329">Dans la page **Spécifier les objectifs à court terme**, dans le champ **Durée de rétention**, spécifiez le nombre de jours pendant lesquels vous souhaitez conserver les points de récupération qui sont *stockés sur le disque*.</span><span class="sxs-lookup"><span data-stu-id="7bbda-329">On the **Specify Short-Term Goals** page, for **Retention Range**, specify the number of days that you want to retain recovery points that are *stored to disk*.</span></span> <span data-ttu-id="7bbda-330">Si vous souhaitez modifier l’heure et les jours de création des points de récupération, cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-330">If you want to change the time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="7bbda-331">Les points de récupération à court terme sont des sauvegardes complètes.</span><span class="sxs-lookup"><span data-stu-id="7bbda-331">The short-term recovery points are full backups.</span></span> <span data-ttu-id="7bbda-332">Ils ne fonctionnent pas comme des sauvegardes incrémentielles.</span><span class="sxs-lookup"><span data-stu-id="7bbda-332">They are not incremental backups.</span></span> <span data-ttu-id="7bbda-333">Après avoir défini vos objectifs à court terme, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-333">When you are satisfied with the short-term goals, click **Next**.</span></span>

    ![Spécifier les objectifs à court terme](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="7bbda-335">Dans la page **Vérifier l’allocation de disque**, passez en revue les informations et modifiez l’espace disque des machines virtuelles si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7bbda-335">On the **Review Disk Allocation** page, review and if necessary, modify the disk space for the VMs.</span></span> <span data-ttu-id="7bbda-336">Les allocations de disques recommandées dépendent de la durée de rétention spécifiée dans la page **Spécifier les objectifs à court terme**, du type de charge de travail et de la taille des données protégées (identifiées à l’étape 3).</span><span class="sxs-lookup"><span data-stu-id="7bbda-336">The recommended disk allocations are based on the retention range that is specified in the **Specify Short-Term Goals** page, the type of workload, and the size of the protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="7bbda-337">**Taille des données** : taille des données dans le groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="7bbda-337">**Data size:** Size of the data in the protection group.</span></span>
  - <span data-ttu-id="7bbda-338">**Espace disque** : quantité d’espace disque recommandée pour le groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="7bbda-338">**Disk space:** The recommended amount of disk space for the protection group.</span></span> <span data-ttu-id="7bbda-339">Pour modifier ce paramètre, vous devez allouer un espace total légèrement supérieur au volume de croissance estimé pour chaque source de données.</span><span class="sxs-lookup"><span data-stu-id="7bbda-339">If you want to modify this setting, you should allocate total space that is slightly larger than the amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="7bbda-340">**Colocaliser les données** : si vous activez la colocalisation, plusieurs sources de données dans la protection peuvent être mappées à un seul réplica et à un seul volume de points de récupération.</span><span class="sxs-lookup"><span data-stu-id="7bbda-340">**Colocate data:** If you turn on colocation, multiple data sources in the protection can map to a single replica and recovery point volume.</span></span> <span data-ttu-id="7bbda-341">La colocalisation n’est pas prise en charge pour toutes les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="7bbda-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="7bbda-342">**Augmenter automatiquement :** si vous activez ce paramètre et si les données contenues dans le groupe protégé dépassent l’allocation initiale, System Center Data Protection Manager tente d’augmenter la taille du disque de 25 %.</span><span class="sxs-lookup"><span data-stu-id="7bbda-342">**Automatically grow:** If you turn on this setting, if data in the protected group outgrows the initial allocation, System Center Data Protection Manager tries to increase the disk size by 25 percent.</span></span>
  - <span data-ttu-id="7bbda-343">**Détails de pool de stockage** : affiche l’état du pool de stockage, notamment la taille totale et la taille de disque restante.</span><span class="sxs-lookup"><span data-stu-id="7bbda-343">**Storage pool details:** Shows the status of the storage pool, including total and remaining disk size.</span></span>

    ![Vérifier l’allocation de disque](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="7bbda-345">Après avoir défini l’allocation d’espace, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-345">When you are satisfied with the space allocation, click **Next**.</span></span>

7. <span data-ttu-id="7bbda-346">Dans la page **Choisir la méthode de création de réplica**, indiquez de quelle manière vous souhaitez générer la copie initiale, ou le réplica, des données protégées sur le serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-346">On the **Choose Replica Creation Method** page, specify how you want to generate the initial copy, or replica, of the protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="7bbda-347">Les valeurs **Automatiquement sur le réseau** et **Maintenant** sont définies par défaut.</span><span class="sxs-lookup"><span data-stu-id="7bbda-347">The default is **Automatically over the network** and **Now**.</span></span> <span data-ttu-id="7bbda-348">Si vous utilisez la valeur par défaut, nous vous recommandons de spécifier une heure creuse.</span><span class="sxs-lookup"><span data-stu-id="7bbda-348">If you use the default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="7bbda-349">Choisissez **Ultérieurement** et spécifiez le jour et l’heure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="7bbda-350">Pour de grandes quantités de données ou des conditions réseau peu optimales, pensez à répliquer les données hors connexion à l’aide d’un média amovible.</span><span class="sxs-lookup"><span data-stu-id="7bbda-350">For large amounts of data or less-than-optimal network conditions, consider replicating the data offline by using removable media.</span></span>

    <span data-ttu-id="7bbda-351">Après avoir effectué vos sélections, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-351">After you have made your choices, click **Next**.</span></span>

    ![Choisir la méthode de création d’un réplica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="7bbda-353">Dans la page **Options de vérification de cohérence**, indiquez comment et quand automatiser les vérifications de cohérence.</span><span class="sxs-lookup"><span data-stu-id="7bbda-353">On the **Consistency Check Options** page, select how and when to automate the consistency checks.</span></span> <span data-ttu-id="7bbda-354">Vous pouvez exécuter les vérifications de cohérence lorsque les données du réplica deviennent incohérentes ou en fonction d’une planification définie.</span><span class="sxs-lookup"><span data-stu-id="7bbda-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="7bbda-355">Si vous ne voulez pas configurer de vérifications de cohérence automatiques, vous pouvez exécuter une vérification manuelle.</span><span class="sxs-lookup"><span data-stu-id="7bbda-355">If you don't want to configure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="7bbda-356">Dans la zone de protection de la console du serveur de sauvegarde Azure, cliquez avec le bouton droit sur le groupe de protection, puis sélectionnez **Effectuer une vérification de cohérence**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-356">In the protection area of the Azure Backup Server console, right-click the protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="7bbda-357">Cliquez sur **Suivant** pour passer à la page suivante.</span><span class="sxs-lookup"><span data-stu-id="7bbda-357">Click **Next** to move to the next page.</span></span>

9. <span data-ttu-id="7bbda-358">Dans la page **Indiquer les données de protection en ligne**, sélectionnez une ou plusieurs sources de données que vous souhaitez protéger.</span><span class="sxs-lookup"><span data-stu-id="7bbda-358">On the **Specify Online Protection Data** page, select one or more data sources that you want to protect.</span></span> <span data-ttu-id="7bbda-359">Vous pouvez sélectionner les membres un à un ou cliquer sur **Sélectionner tout** pour choisir tous les membres.</span><span class="sxs-lookup"><span data-stu-id="7bbda-359">You can select the members individually, or click **Select All** to choose all members.</span></span> <span data-ttu-id="7bbda-360">Après avoir sélectionné les membres, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-360">After you choose the members, click **Next**.</span></span>

    ![Spécifier les données de protection en ligne](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="7bbda-362">Dans la page **Spécifier une planification de sauvegarde en ligne**, indiquez la planification qui vous permettra de générer des points de récupération à partir de la sauvegarde sur disque.</span><span class="sxs-lookup"><span data-stu-id="7bbda-362">On the **Specify Online Backup Schedule** page, specify the schedule to generate recovery points from the disk backup.</span></span> <span data-ttu-id="7bbda-363">Le point de récupération généré est transféré vers le coffre Recovery Services dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-363">After the recovery point is generated, it is transferred to the Recovery Services vault in Azure.</span></span> <span data-ttu-id="7bbda-364">Lorsque vous avez fini de paramétrer la planification de sauvegarde en ligne, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-364">When you are satisfied with the online backup schedule, click **Next**.</span></span>

    ![Spécifier la planification de sauvegarde en ligne](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="7bbda-366">Dans la page **Spécifier une stratégie de rétention en ligne**, indiquez la durée de rétention souhaitée des données de sauvegarde dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbda-366">On the **Specify Online Retention Policy** page, indicate how long you want to retain the backup data in Azure.</span></span> <span data-ttu-id="7bbda-367">Après avoir défini la stratégie, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-367">After the policy is defined, click **Next**.</span></span>

    ![Spécifier la stratégie de rétention en ligne](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="7bbda-369">La durée de conservation des données dans Azure n’est soumise à aucune restriction.</span><span class="sxs-lookup"><span data-stu-id="7bbda-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="7bbda-370">Lorsque vous stockez des données de point de récupération dans Azure, la seule limite que vous devez respecter est que vous ne pouvez pas avoir plus de 9 999 points de récupération par instance protégée.</span><span class="sxs-lookup"><span data-stu-id="7bbda-370">When you store recovery point data in Azure, the only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="7bbda-371">Dans cet exemple, l’instance protégée est le serveur VMware.</span><span class="sxs-lookup"><span data-stu-id="7bbda-371">In this example, the protected instance is the VMware server.</span></span>

12. <span data-ttu-id="7bbda-372">Dans la page **Résumé**, passez en revue les détails des paramètres et des membres du groupe de protection, puis cliquez sur **Créer un groupe**.</span><span class="sxs-lookup"><span data-stu-id="7bbda-372">On the **Summary** page, review the details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Résumé des paramètres et des membres du groupe de protection](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="7bbda-374">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7bbda-374">Next steps</span></span>
<span data-ttu-id="7bbda-375">Si vous utilisez le serveur de sauvegarde Azure pour protéger vos charges de travail VMware, vous trouverez peut-être utile d’utiliser le serveur de sauvegarde Azure pour contribuer à la protection d’un [serveur Microsoft Exchange](./backup-azure-exchange-mabs.md), d’une [batterie de serveurs Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md) ou d’une [base de données SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="7bbda-375">If you use Azure Backup Server to protect VMware workloads, you may be interested in using Azure Backup Server to help protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="7bbda-376">Pour plus d’informations sur les problèmes d’inscription de l’agent, de configuration du groupe de protection ou de sauvegarde des travaux, voir [Résoudre les problèmes d’un serveur de sauvegarde Azure](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="7bbda-376">For information on problems with registering the agent, configuring the protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
