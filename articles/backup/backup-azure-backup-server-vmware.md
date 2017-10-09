---
title: aaaBack des serveurs VMware avec Azure Backup Server | Documents Microsoft
description: "Utilisez tooback Azure Backup Server un VMware vCenter/ESXi serveurs tooAzure ou un disque. Cet article fournit des instructions étape par étape pour sauvegarder (ou protéger) vos charges de travail VMware."
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
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a><span data-ttu-id="19649-104">Sauvegarder un tooAzure du serveur VMware</span><span class="sxs-lookup"><span data-stu-id="19649-104">Back up a VMware server tooAzure</span></span>

<span data-ttu-id="19649-105">Cet article explique comment tooconfigure Azure Backup Server toohelp protéger les charges de travail VMware server.</span><span class="sxs-lookup"><span data-stu-id="19649-105">This article explains how tooconfigure Azure Backup Server toohelp protect VMware server workloads.</span></span> <span data-ttu-id="19649-106">Cet article suppose que vous avez déjà installé le serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="19649-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="19649-107">Si vous n’avez pas installé Azure Backup Server, consultez [préparer tooback des charges de travail à l’aide d’Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="19649-107">If you don't have Azure Backup Server installed, see [Prepare tooback up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="19649-108">Un serveur de sauvegarde Azure peut sauvegarder ou aider à protéger les versions 6.5, 6.0 et 5.5 de VMware vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="19649-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-toohello-vcenter-server"></a><span data-ttu-id="19649-109">Créer un connexion sécurisée toohello du serveur vCenter</span><span class="sxs-lookup"><span data-stu-id="19649-109">Create a secure connection toohello vCenter Server</span></span>

<span data-ttu-id="19649-110">Par défaut, le serveur de sauvegarde Azure communique avec chaque serveur vCenter via un canal HTTPS.</span><span class="sxs-lookup"><span data-stu-id="19649-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="19649-111">tooturn sur une communication sécurisée hello, nous vous recommandons d’installer le certificat d’autorité de certification (CA) VMware hello sur Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="19649-111">tooturn on hello secure communication, we recommend that you install hello VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="19649-112">Si vous ne nécessitent pas une communication sécurisée, préférez l’exigence de toodisable hello HTTPS, consultez [désactiver le protocole de communication sécurisé](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="19649-112">If you don't require secure communication, and would prefer toodisable hello HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="19649-113">toocreate une connexion sécurisée entre le serveur de sauvegarde Azure et hello du serveur vCenter, importez le certificat de confiance de hello sur Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="19649-113">toocreate a secure connection between Azure Backup Server and hello vCenter Server, import hello trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="19649-114">En règle générale, vous utilisez un navigateur sur hello Azure Backup Server machine tooconnect toohello serveur vCenter via hello vSphere Client Web.</span><span class="sxs-lookup"><span data-stu-id="19649-114">Typically, you use a browser on hello Azure Backup Server machine tooconnect toohello vCenter Server via hello vSphere Web Client.</span></span> <span data-ttu-id="19649-115">Hello première fois que vous utilisez hello Azure Backup Server navigateur tooconnect toohello vCenter Server, connexion de hello n’est pas sécurisée.</span><span class="sxs-lookup"><span data-stu-id="19649-115">hello first time you use hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connection isn't secure.</span></span> <span data-ttu-id="19649-116">Hello suivant image montre les connexions hello non sécurisé.</span><span class="sxs-lookup"><span data-stu-id="19649-116">hello following image shows hello unsecured connection.</span></span>

![Exemple de connexion non sécurisée tooVMware serveur](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="19649-118">toofix ce problème et créer une connexion sécurisée, télécharger des certificats d’autorité de certification racine hello approuvé.</span><span class="sxs-lookup"><span data-stu-id="19649-118">toofix this issue, and create a secure connection, download hello trusted root CA certificates.</span></span>

1. <span data-ttu-id="19649-119">Dans le navigateur de hello sur Azure Backup Server, entrez hello URL toohello vSphere Client Web.</span><span class="sxs-lookup"><span data-stu-id="19649-119">In hello browser on Azure Backup Server, enter hello URL toohello vSphere Web Client.</span></span> <span data-ttu-id="19649-120">page de connexion du Client Web Hello vSphere s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-120">hello vSphere Web Client login page appears.</span></span>

    ![Client web vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="19649-122">Bas hello informations hello pour les développeurs et administrateurs, recherchez hello **téléchargement les certificats d’autorité de certification racine de confiance** lien.</span><span class="sxs-lookup"><span data-stu-id="19649-122">At hello bottom of hello information for administrators and developers, locate hello **Download trusted root CA certificates** link.</span></span>

    ![Certificats d’autorité de certification racine lien toodownload hello approuvé](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="19649-124">Si vous ne voyez la page de connexion du Client Web hello vSphere, vérifiez les paramètres de proxy de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="19649-124">If you don't see hello vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="19649-125">Cliquez sur **Télécharger les certificats approuvés de l’autorité de certification racine**.</span><span class="sxs-lookup"><span data-stu-id="19649-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="19649-126">Hello vCenter Server télécharge un ordinateur local tooyour de fichier.</span><span class="sxs-lookup"><span data-stu-id="19649-126">hello vCenter Server downloads a file tooyour local computer.</span></span> <span data-ttu-id="19649-127">Hello nom de fichier est nommé **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="19649-127">hello file's name is named **download**.</span></span> <span data-ttu-id="19649-128">En fonction de votre navigateur, vous recevez un message vous demandant si tooopen ou enregistrer le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-128">Depending on your browser, you receive a message that asks whether tooopen or save hello file.</span></span>

    ![message de téléchargement lorsque les certificats sont téléchargés](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="19649-130">Enregistrer l’emplacement du fichier de hello tooa sur Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="19649-130">Save hello file tooa location on Azure Backup Server.</span></span> <span data-ttu-id="19649-131">Lorsque vous enregistrez le fichier de hello, ajoutez l’extension de nom de fichier .zip hello.</span><span class="sxs-lookup"><span data-stu-id="19649-131">When you save hello file, add hello .zip file name extension.</span></span>

    <span data-ttu-id="19649-132">fichier de Hello est un fichier .zip qui contient des informations sur les certificats de hello hello.</span><span class="sxs-lookup"><span data-stu-id="19649-132">hello file is a .zip file that contains hello information about hello certificates.</span></span> <span data-ttu-id="19649-133">Avec l’extension .zip de hello, vous pouvez utiliser les outils d’extraction hello.</span><span class="sxs-lookup"><span data-stu-id="19649-133">With hello .zip extension, you can use hello extraction tools.</span></span>

4. <span data-ttu-id="19649-134">Avec le bouton droit **download.zip**, puis sélectionnez **extraire tout** contenu de hello tooextract.</span><span class="sxs-lookup"><span data-stu-id="19649-134">Right-click **download.zip**, and then select **Extract All** tooextract hello contents.</span></span>

    <span data-ttu-id="19649-135">fichier .zip de Hello extrait son contenu tooa sous-dossier **certificats**.</span><span class="sxs-lookup"><span data-stu-id="19649-135">hello .zip file extracts its contents tooa folder named **certs**.</span></span> <span data-ttu-id="19649-136">Deux types de fichiers s’affichent dans le dossier de certificats hello.</span><span class="sxs-lookup"><span data-stu-id="19649-136">Two types of files appear in hello certs folder.</span></span> <span data-ttu-id="19649-137">fichier de certificat racine Hello possède une extension qui commence par un numéro de séquence comme.0 et.1.</span><span class="sxs-lookup"><span data-stu-id="19649-137">hello root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="19649-138">fichier de liste de révocation Hello possède une extension qui commence par une séquence comme .r0 ou .r1.</span><span class="sxs-lookup"><span data-stu-id="19649-138">hello CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="19649-139">fichier de liste de révocation de Hello est associé à un certificat.</span><span class="sxs-lookup"><span data-stu-id="19649-139">hello CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="19649-140">Fichier de téléchargement extrait localement</span><span class="sxs-lookup"><span data-stu-id="19649-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="19649-141">Bonjour **certificats** dossier, cliquez sur le fichier de certificat racine hello, puis cliquez sur **renommer**.</span><span class="sxs-lookup"><span data-stu-id="19649-141">In hello **certs** folder, right-click hello root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="19649-142">Renommer un certificat racine</span><span class="sxs-lookup"><span data-stu-id="19649-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="19649-143">Modification extension too.crt du certificat d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="19649-143">Change hello root certificate's extension too.crt.</span></span> <span data-ttu-id="19649-144">Lorsque le système vous demande si vous êtes sûr de vouloir extension de hello toochange, cliquez sur **Oui** ou **OK**.</span><span class="sxs-lookup"><span data-stu-id="19649-144">When you're asked if you're sure you want toochange hello extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="19649-145">Dans le cas contraire, vous modifiez fonction du fichier hello.</span><span class="sxs-lookup"><span data-stu-id="19649-145">Otherwise, you change hello file's intended function.</span></span> <span data-ttu-id="19649-146">icône Hello hello fichier modifications tooan icône qui représente un certificat racine.</span><span class="sxs-lookup"><span data-stu-id="19649-146">hello icon for hello file changes tooan icon that represents a root certificate.</span></span>

6. <span data-ttu-id="19649-147">Cliquez sur le certificat racine de hello et dans le menu contextuel de hello, sélectionnez **installer le certificat**.</span><span class="sxs-lookup"><span data-stu-id="19649-147">Right-click hello root certificate and from hello pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="19649-148">Hello **Assistant Importation de certificat** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-148">hello **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="19649-149">Bonjour **Assistant Importation de certificat** boîte de dialogue, sélectionnez **ordinateur Local** en tant que destination hello pour les certificats hello, puis cliquez sur **suivant** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="19649-149">In hello **Certificate Import Wizard** dialog box, select **Local Machine** as hello destination for hello certificate, and then click **Next** toocontinue.</span></span>

    ![<span data-ttu-id="19649-150">Options de destination de stockage du certificat</span><span class="sxs-lookup"><span data-stu-id="19649-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="19649-151">Si vous demande si vous souhaitez que l’ordinateur de toohello de modifications de tooallow, cliquez sur **Oui** ou **OK**, modifications de hello tooall.</span><span class="sxs-lookup"><span data-stu-id="19649-151">If you're asked if you want tooallow changes toohello computer, click **Yes** or **OK**, tooall hello changes.</span></span>

8. <span data-ttu-id="19649-152">Sur hello **magasin de certificats** page, sélectionnez **placer tous les certificats dans hello suivant magasin**, puis cliquez sur **Parcourir** magasin de certificats toochoose hello.</span><span class="sxs-lookup"><span data-stu-id="19649-152">On hello **Certificate Store** page, select **Place all certificates in hello following store**, and then click **Browse** toochoose hello certificate store.</span></span>

    ![Placer des certificats dans une zone de stockage spécifique](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="19649-154">Hello **sélectionner un magasin de certificats** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-154">hello **Select Certificate Store** dialog box appears.</span></span>

    ![Arborescence des dossiers de stockage de certificats](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="19649-156">Sélectionnez **autorités de Certification racines de confiance** en tant que dossier de destination hello pour les certificats hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="19649-156">Select **Trusted Root Certification Authorities** as hello destination folder for hello certificates, and then click **OK**.</span></span>

    ![Dossier de destination des certificats](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="19649-158">Hello **autorités de Certification racines de confiance** dossier est confirmé comme magasin de certificats hello.</span><span class="sxs-lookup"><span data-stu-id="19649-158">hello **Trusted Root Certification Authorities** folder is confirmed as hello certificate store.</span></span> <span data-ttu-id="19649-159">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="19649-159">Click **Next**.</span></span>

    ![Dossier de magasin de certificats](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="19649-161">Sur hello **fin hello Assistant Importation de certificat** page, vérifiez que le certificat hello est dans le dossier de votre choix hello, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="19649-161">On hello **Completing hello Certificate Import Wizard** page, verify that hello certificate is in hello desired folder, and then click **Finish**.</span></span>

    ![Vérifier le certificat se trouve dans le dossier approprié de hello](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="19649-163">Une boîte de dialogue s’affiche, l’importation du certificat réussie hello est confirmée.</span><span class="sxs-lookup"><span data-stu-id="19649-163">A dialog box appears, hello successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="19649-164">Se connecter toohello vCenter tooconfirm serveur que votre connexion est sécurisée.</span><span class="sxs-lookup"><span data-stu-id="19649-164">Sign in toohello vCenter Server tooconfirm that your connection is secure.</span></span>

  <span data-ttu-id="19649-165">Si l’importation du certificat hello ne réussit pas, et vous ne pouvez pas établir une connexion sécurisée, la documentation hello VMware vSphere sur [obtention de certificats de serveur](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="19649-165">If hello certificate import is not successful, and you cannot establish a secure connection, consult hello VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="19649-166">Si vous avez des limites sécurisés au sein de votre organisation et que vous ne souhaitez pas tooturn sur hello le protocole HTTPS, utilisez hello suivant la procédure toodisable hello sécuriser les communications.</span><span class="sxs-lookup"><span data-stu-id="19649-166">If you have secure boundaries within your organization, and don't want tooturn on hello HTTPS protocol, use hello following procedure toodisable hello secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="19649-167">Désactiver le protocole de communication sécurisée</span><span class="sxs-lookup"><span data-stu-id="19649-167">Disable secure communication protocol</span></span>

<span data-ttu-id="19649-168">Si votre organisation ne nécessite pas le protocole HTTPS hello, utilisez hello suivant les étapes toodisable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="19649-168">If your organization doesn't require hello HTTPS protocol, use hello following steps toodisable HTTPS.</span></span> <span data-ttu-id="19649-169">toodisable hello le comportement par défaut, créez une clé de Registre qui ignore le comportement par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-169">toodisable hello default behavior, create a registry key that ignores hello default behavior.</span></span>

1. <span data-ttu-id="19649-170">Copiez et collez hello après le texte dans un fichier .txt.</span><span class="sxs-lookup"><span data-stu-id="19649-170">Copy and paste hello following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="19649-171">Enregistrer l’ordinateur de serveur de sauvegarde Azure hello fichier tooyour.</span><span class="sxs-lookup"><span data-stu-id="19649-171">Save hello file tooyour Azure Backup Server computer.</span></span> <span data-ttu-id="19649-172">Nom de fichier hello, utilisez DisableSecureAuthentication.reg.</span><span class="sxs-lookup"><span data-stu-id="19649-172">For hello file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="19649-173">Double-cliquez sur entrée de Registre hello fichier tooactivate hello.</span><span class="sxs-lookup"><span data-stu-id="19649-173">Double-click hello file tooactivate hello registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a><span data-ttu-id="19649-174">Créer un compte d’utilisateur et le rôle sur hello du serveur vCenter</span><span class="sxs-lookup"><span data-stu-id="19649-174">Create a role and user account on hello vCenter Server</span></span>

<span data-ttu-id="19649-175">Sur le serveur vCenter de hello, un rôle est un ensemble prédéfini de privilèges.</span><span class="sxs-lookup"><span data-stu-id="19649-175">On hello vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="19649-176">Un administrateur de serveur vCenter crée des rôles de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-176">A vCenter Server administrator creates hello roles.</span></span> <span data-ttu-id="19649-177">tooassign autorisations, administrateur de hello paires de comptes d’utilisateur à un rôle.</span><span class="sxs-lookup"><span data-stu-id="19649-177">tooassign permissions, hello administrator pairs user accounts with a role.</span></span> <span data-ttu-id="19649-178">tooback d’informations d’identification tooestablish hello utilisateur nécessaires d’ordinateur du serveur vCenter hello, créez un rôle avec des privilèges spécifiques et l’associer compte d’utilisateur hello rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-178">tooestablish hello necessary user credentials tooback up hello vCenter Server computer, create a role with specific privileges, and then associate hello user account with hello role.</span></span>

<span data-ttu-id="19649-179">Serveur de sauvegarde Azure utilise un tooauthenticate nom d’utilisateur et mot de passe avec hello du serveur vCenter.</span><span class="sxs-lookup"><span data-stu-id="19649-179">Azure Backup Server uses a username and password tooauthenticate with hello vCenter Server.</span></span> <span data-ttu-id="19649-180">Le serveur de sauvegarde Azure utilise ces informations d’identification comme authentification pour toutes les opérations de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="19649-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="19649-181">tooadd un rôle de serveur vCenter et ses privilèges pour un administrateur de sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="19649-181">tooadd a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="19649-182">Se connecter dans toohello vCenter Server, puis dans hello du serveur vCenter **Navigator** du panneau, cliquez sur **Administration**.</span><span class="sxs-lookup"><span data-stu-id="19649-182">Sign in toohello vCenter Server, and then in hello vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Option d’administration dans le panneau Navigateur du serveur vCenter](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="19649-184">Dans **Administration** sélectionnez **rôles**, puis dans hello **rôles** cliquez sur le panneau de configuration hello ajouter l’icône de rôle (symbole + hello).</span><span class="sxs-lookup"><span data-stu-id="19649-184">In **Administration** select **Roles**, and then in hello **Roles** panel click hello add role icon (hello + symbol).</span></span>

    ![Ajouter un rôle](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="19649-186">Hello **Create Role** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-186">hello **Create Role** dialog box appears.</span></span>

    ![Créer un rôle](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="19649-188">Bonjour **Create Role** la boîte de dialogue hello **nom de rôle** , entrez *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="19649-188">In hello **Create Role** dialog box, in hello **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="19649-189">nom du rôle Hello peut être comme vous le souhaitez, mais il doit être reconnaissable fins du rôle hello.</span><span class="sxs-lookup"><span data-stu-id="19649-189">hello role name can be whatever you like, but it should be recognizable for hello role's purpose.</span></span>

4. <span data-ttu-id="19649-190">Sélectionnez les privilèges hello pour la version appropriée de hello de vCenter, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="19649-190">Select hello privileges for hello appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="19649-191">Hello tableau suivant identifie les privilèges de hello requise de vCenter 6.0 et vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="19649-191">hello following table identifies hello required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="19649-192">Lorsque vous sélectionnez des privilèges de hello, cliquez sur hello icône suivant toohello parent étiquette tooexpand hello parent et vue hello enfants des privilèges.</span><span class="sxs-lookup"><span data-stu-id="19649-192">When you select hello privileges, click hello icon next toohello parent label tooexpand hello parent and view hello child privileges.</span></span> <span data-ttu-id="19649-193">privilèges de VirtualMachine tooselect hello, vous devez toogo plusieurs niveaux dans hello parent de hiérarchie enfant.</span><span class="sxs-lookup"><span data-stu-id="19649-193">tooselect hello VirtualMachine privileges, you need toogo several levels into hello parent child hierarchy.</span></span> <span data-ttu-id="19649-194">Vous n’avez pas besoin tooselect tous les privilèges enfant au sein d’un privilège de parent.</span><span class="sxs-lookup"><span data-stu-id="19649-194">You don't need tooselect all child privileges within a parent privilege.</span></span>

  ![Hiérarchie des privilèges parent-enfant](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="19649-196">Après avoir cliqué sur **OK**, hello nouveau rôle s’affiche dans la liste hello sur Panneau de configuration de rôles hello.</span><span class="sxs-lookup"><span data-stu-id="19649-196">After you click **OK**, hello new role appears in hello list on hello Roles panel.</span></span>

|<span data-ttu-id="19649-197">Privilèges de vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="19649-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="19649-198">Privilèges de vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="19649-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="19649-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="19649-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="19649-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="19649-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="19649-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="19649-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="19649-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="19649-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="19649-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="19649-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="19649-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="19649-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="19649-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="19649-205">Network.Assign</span></span> |
|<span data-ttu-id="19649-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="19649-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="19649-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="19649-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="19649-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="19649-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="19649-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="19649-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="19649-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="19649-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="19649-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="19649-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="19649-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="19649-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="19649-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="19649-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="19649-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="19649-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="19649-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="19649-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="19649-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="19649-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="19649-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="19649-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="19649-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="19649-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="19649-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="19649-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="19649-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="19649-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="19649-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="19649-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="19649-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="19649-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="19649-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="19649-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="19649-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="19649-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="19649-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="19649-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="19649-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="19649-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="19649-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="19649-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="19649-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="19649-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="19649-229">Créer un compte d’utilisateur et des autorisations pour un serveur vCenter</span><span class="sxs-lookup"><span data-stu-id="19649-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="19649-230">Après avoir configuré la rôle hello avec des privilèges, créez un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="19649-230">After hello role with privileges is set up, create a user account.</span></span> <span data-ttu-id="19649-231">compte d’utilisateur Hello a un nom et un mot de passe, qui fournit les informations d’identification de hello sont utilisées pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="19649-231">hello user account has a name and password, which provides hello credentials that are used for authentication.</span></span>

1. <span data-ttu-id="19649-232">toocreate un compte d’utilisateur dans le serveur vCenter Server hello **Navigator** du panneau, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="19649-232">toocreate a user account, in hello vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Option Utilisateurs et groupes](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="19649-234">Hello **vCenter utilisateurs et groupes** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-234">hello **vCenter Users and Groups** panel appears.</span></span>

    ![Panneau Utilisateurs et groupes vCenter](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="19649-236">Bonjour **vCenter utilisateurs et groupes** Panneau de configuration, sélectionnez hello **utilisateurs** onglet, puis cliquez sur hello ajouter les utilisateurs icône (symbole + hello).</span><span class="sxs-lookup"><span data-stu-id="19649-236">In hello **vCenter Users and Groups** panel, select hello **Users** tab, and then click hello add users icon (hello + symbol).</span></span>

    <span data-ttu-id="19649-237">Hello **nouvel utilisateur** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-237">hello **New User** dialog box appears.</span></span>

3. <span data-ttu-id="19649-238">Bonjour **nouvel utilisateur** boîte de dialogue zone, ajouter des informations de l’utilisateur hello, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="19649-238">In hello **New User** dialog box, add hello user's information and then click **OK**.</span></span> <span data-ttu-id="19649-239">Dans cette procédure, le nom d’utilisateur hello est BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="19649-239">In this procedure, hello username is BackupAdmin.</span></span>

    ![Boîte de dialogue Nouvel utilisateur](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="19649-241">nouveau compte d’utilisateur Hello s’affiche dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-241">hello new user account appears in hello list.</span></span>

4. <span data-ttu-id="19649-242">compte d’utilisateur tooassociate hello avec rôle hello, Bonjour **Navigator** du panneau, cliquez sur **autorisations globales**.</span><span class="sxs-lookup"><span data-stu-id="19649-242">tooassociate hello user account with hello role, in hello **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="19649-243">Bonjour **autorisations globales** Panneau de configuration, sélectionnez hello **gérer** onglet, puis cliquez sur hello ajouter icône (symbole + hello).</span><span class="sxs-lookup"><span data-stu-id="19649-243">In hello **Global Permissions** panel, select hello **Manage** tab, and then click hello add icon (hello + symbol).</span></span>

    ![Panneau Autorisations globales](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="19649-245">Hello **Global autorisations racine - ajouter une autorisation** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-245">hello **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="19649-246">Bonjour **racine autorisation globale - ajouter une autorisation** boîte de dialogue, cliquez sur **ajouter** toochoose hello utilisateur ou un groupe.</span><span class="sxs-lookup"><span data-stu-id="19649-246">In hello **Global Permission Root - Add Permission** dialog box, click **Add** toochoose hello user or group.</span></span>

    ![Choisir un utilisateur ou un groupe](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="19649-248">Hello **sélectionner des utilisateurs/groupes** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-248">hello **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="19649-249">Bonjour **sélectionner des utilisateurs/groupes** boîte de dialogue, choisissez **BackupAdmin** puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="19649-249">In hello **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="19649-250">Dans **utilisateurs**, hello *domaine om_utilisateur* format est utilisé pour le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="19649-250">In **Users**, hello *domain\username* format is used for hello user account.</span></span> <span data-ttu-id="19649-251">Si vous voulez toouse un autre domaine, sélectionnez-le dans hello **domaine** liste.</span><span class="sxs-lookup"><span data-stu-id="19649-251">If you want toouse a different domain, choose it from hello **Domain** list.</span></span>

    ![Ajouter un utilisateur BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="19649-253">Cliquez sur **OK** tooadd hello sélectionné d’utilisateurs toohello **ajouter une autorisation** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="19649-253">Click **OK** tooadd hello selected users toohello **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="19649-254">Maintenant que vous avez identifié les utilisateur hello, attribuer le rôle toohello hello.</span><span class="sxs-lookup"><span data-stu-id="19649-254">Now that you've identified hello user, assign hello user toohello role.</span></span> <span data-ttu-id="19649-255">Dans **affecté le rôle**, dans la liste déroulante hello, sélectionnez **BackupAdminRole**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="19649-255">In **Assigned Role**, from hello drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Affecter des utilisateurs toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="19649-257">Sur hello **gérer** onglet Bonjour **autorisations globales** Panneau de configuration, nouveau compte d’utilisateur hello et rôle de hello associé s’affichent dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-257">On hello **Manage** tab in hello **Global Permissions** panel, hello new user account and hello associated role appear in hello list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="19649-258">Définir les informations d’identification de serveur vCenter sur le serveur de sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="19649-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="19649-259">Avant d’ajouter hello VMware server tooAzure sauvegarde du serveur, installez [1 de mise à jour pour Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="19649-259">Before you add hello VMware server tooAzure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="19649-260">tooopen Azure Backup Server, double-cliquez sur l’icône de hello sur le bureau du serveur de sauvegarde Azure hello.</span><span class="sxs-lookup"><span data-stu-id="19649-260">tooopen Azure Backup Server, double-click hello icon on hello Azure Backup Server desktop.</span></span>

    ![Icône du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="19649-262">Si vous ne trouvez l’icône de hello sur le bureau de hello, ouvrez Azure Backup Server à partir de la liste de hello des applications installées.</span><span class="sxs-lookup"><span data-stu-id="19649-262">If you can't find hello icon on hello desktop, open Azure Backup Server from hello list of installed apps.</span></span> <span data-ttu-id="19649-263">nom de l’application Hello Azure Backup Server est appelé Microsoft Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="19649-263">hello Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="19649-264">Dans la console Azure Backup Server hello, cliquez sur **gestion**, cliquez sur **les serveurs de Production**, puis cliquez sur la barre d’outils hello, **gestion de VMware**.</span><span class="sxs-lookup"><span data-stu-id="19649-264">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then on hello tool ribbon, click **Manage VMware**.</span></span>

    ![Console du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="19649-266">Hello **gérer les informations d’identification** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-266">hello **Manage Credentials** dialog box appears.</span></span>

    ![Boîte de dialogue Gérer les informations d’identification du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="19649-268">Bonjour **gérer les informations d’identification** boîte de dialogue, cliquez sur **ajouter** tooopen hello **ajouter les informations d’identification** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="19649-268">In hello **Manage Credentials** dialog box, click **Add** tooopen hello **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="19649-269">Bonjour **ajouter les informations d’identification** boîte de dialogue, entrez un nom et une description pour les nouvelles informations d’identification de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-269">In hello **Add Credential** dialog box, enter a name and a description for hello new credential.</span></span> <span data-ttu-id="19649-270">Spécifier un mot de passe et nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="19649-270">Then specify hello username and password.</span></span> <span data-ttu-id="19649-271">nom de Hello, *informations d’identification de Contoso Vcenter* sert tooidentify hello dans informations d’identification suit hello.</span><span class="sxs-lookup"><span data-stu-id="19649-271">hello name, *Contoso Vcenter credential* is used tooidentify hello credential in hello next procedure.</span></span> <span data-ttu-id="19649-272">Utilisez hello même nom d’utilisateur et mot de passe utilisé pour hello du serveur vCenter.</span><span class="sxs-lookup"><span data-stu-id="19649-272">Use hello same username and password that is used for hello vCenter Server.</span></span> <span data-ttu-id="19649-273">Si le serveur vCenter Server hello et Azure Backup Server ne sont pas dans hello du même domaine, dans **nom d’utilisateur**, spécifiez le domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-273">If hello vCenter Server and Azure Backup Server are not in hello same domain, in **User name**, specify hello domain.</span></span>

    ![Boîte de dialogue Ajouter des informations d’identification du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="19649-275">Cliquez sur **ajouter** tooadd hello de nouvelles informations d’identification tooAzure sauvegarde du serveur.</span><span class="sxs-lookup"><span data-stu-id="19649-275">Click **Add** tooadd hello new credential tooAzure Backup Server.</span></span> <span data-ttu-id="19649-276">des informations d’identification de Hello s’affiche dans la liste hello Bonjour **gérer les informations d’identification** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="19649-276">hello new credential appears in hello list in hello **Manage Credentials** dialog box.</span></span>
    
    ![Boîte de dialogue Gérer les informations d’identification du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="19649-278">tooclose hello **gérer les informations d’identification** boîte de dialogue, cliquez sur hello **X** dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-278">tooclose hello **Manage Credentials** dialog box, click hello **X** in hello upper-right corner.</span></span>


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a><span data-ttu-id="19649-279">Ajouter hello vCenter Server tooAzure sauvegarde du serveur</span><span class="sxs-lookup"><span data-stu-id="19649-279">Add hello vCenter Server tooAzure Backup Server</span></span>

<span data-ttu-id="19649-280">Assistant d’ajout de serveur de production est utilisé tooadd hello vCenter Server tooAzure sauvegarde du serveur.</span><span class="sxs-lookup"><span data-stu-id="19649-280">Production Server Addition Wizard is used tooadd hello vCenter Server tooAzure Backup Server.</span></span>

<span data-ttu-id="19649-281">Assistant Ajout de serveur Production, hello complet suivant la procédure de tooopen :</span><span class="sxs-lookup"><span data-stu-id="19649-281">tooopen Production Server Addition Wizard, complete hello following procedure:</span></span>

1. <span data-ttu-id="19649-282">Dans la console Azure Backup Server hello, cliquez sur **gestion**, cliquez sur **les serveurs de Production**, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="19649-282">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Ouvrir l’Assistant Ajout d’un serveur de production](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="19649-284">Hello **Assistant d’ajout de serveur de Production** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-284">hello **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Assistant Ajout d’un serveur de production](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="19649-286">Sur hello **type de sélectionner un serveur de Production** , sélectionnez **serveurs VMware**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19649-286">On hello **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="19649-287">Dans **serveur nom/adresse IP**, spécifiez le nom de domaine complet de hello (FQDN) ou l’adresse IP du serveur de VMware hello.</span><span class="sxs-lookup"><span data-stu-id="19649-287">In **Server Name/IP Address**, specify hello fully qualified domain name (FQDN) or IP address of hello VMware server.</span></span> <span data-ttu-id="19649-288">Si tous les serveurs de ESXi hello sont gérés par hello vCenter même, vous pouvez utiliser le nom hello vCenter.</span><span class="sxs-lookup"><span data-stu-id="19649-288">If all hello ESXi servers are managed by hello same vCenter, you can use hello vCenter name.</span></span>

    ![Spécifier l’adresse IP ou le nom de domaine complet du serveur VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="19649-290">Dans **Port SSL**, entrez le port hello toocommunicate utilisé avec VMware server de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-290">In **SSL Port**, enter hello port that is used toocommunicate with hello VMware server.</span></span> <span data-ttu-id="19649-291">Utiliser le port 443, qui est le port par défaut de hello, sauf si vous savez qu’un autre port est requis.</span><span class="sxs-lookup"><span data-stu-id="19649-291">Use port 443, which is hello default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="19649-292">Dans **spécifier les informations d’identification**, sélectionnez hello d’informations d’identification que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="19649-292">In **Specify Credential**, select hello credential that you created earlier.</span></span>

    ![Indiquer les informations d’identification](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="19649-294">Cliquez sur **ajouter** tooadd hello VMware toohello une liste de serveur **ajouté des serveurs VMware**, puis cliquez sur **suivant** toomove toohello page suivante dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-294">Click **Add** tooadd hello VMware server toohello list of **Added VMware Servers**, and then click **Next** toomove toohello next page in hello wizard.</span></span>

    ![Ajouter un serveur VMware et des informations d’identification](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="19649-296">Bonjour **Résumé** , cliquez sur **ajouter** tooadd hello spécifié VMware server tooAzure sauvegarde du serveur.</span><span class="sxs-lookup"><span data-stu-id="19649-296">In hello **Summary** page, click **Add** tooadd hello specified VMware server tooAzure Backup Server.</span></span>

    ![Ajouter VMware server tooAzure sauvegarde du serveur](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="19649-298">sauvegarde du serveur VMware Hello est une sauvegarde sans agent et hello nouveau serveur est ajouté immédiatement.</span><span class="sxs-lookup"><span data-stu-id="19649-298">hello VMware server backup is an agentless backup, and hello new server is added immediately.</span></span> <span data-ttu-id="19649-299">Hello **Terminer** page affiche hello de résultats.</span><span class="sxs-lookup"><span data-stu-id="19649-299">hello **Finish** page shows you hello results.</span></span>

  ![Page Terminer](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="19649-301">tooadd plusieurs instances de vCenter Server tooAzure sauvegarde du serveur, répétez hello précédentes étapes de cette section.</span><span class="sxs-lookup"><span data-stu-id="19649-301">tooadd multiple instances of vCenter Server tooAzure Backup Server, repeat hello previous steps in this section.</span></span>

<span data-ttu-id="19649-302">Après avoir ajouté hello vCenter Server tooAzure sauvegarde du serveur, étape suivante de hello est toocreate un groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="19649-302">After you add hello vCenter Server tooAzure Backup Server, hello next step is toocreate a protection group.</span></span> <span data-ttu-id="19649-303">groupe de protection Hello spécifie hello différentes informations de rétention à court ou à long terme, et il est où vous définissez et appliquez la stratégie de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="19649-303">hello protection group specifies hello various details for short or long-term retention, and it is where you define and apply hello backup policy.</span></span> <span data-ttu-id="19649-304">stratégie de sauvegarde Hello est planification hello pour les cas de sauvegardes, et ce qui est sauvegardé.</span><span class="sxs-lookup"><span data-stu-id="19649-304">hello backup policy is hello schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="19649-305">Configurer un groupe de protection</span><span class="sxs-lookup"><span data-stu-id="19649-305">Configure a protection group</span></span>

<span data-ttu-id="19649-306">Si vous n’avez pas utilisé System Center Data Protection Manager ou Azure Backup Server avant, consultez [planifier les sauvegardes de disque](https://technet.microsoft.com/library/hh758026.aspx) tooprepare votre environnement matériel.</span><span class="sxs-lookup"><span data-stu-id="19649-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) tooprepare your hardware environment.</span></span> <span data-ttu-id="19649-307">Après avoir vérifié que vous disposez de stockage approprié, utilisez des ordinateurs virtuels hello créer un nouveau groupe de Protection Assistant tooadd VMware.</span><span class="sxs-lookup"><span data-stu-id="19649-307">After you check that you have proper storage, use hello Create New Protection Group wizard tooadd VMware virtual machines.</span></span>

1. <span data-ttu-id="19649-308">Dans la console Azure Backup Server hello, cliquez sur **Protection**, dans la barre d’outils hello, cliquez sur **nouveau** Assistant de créer un nouveau groupe de Protection tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="19649-308">In hello Azure Backup Server console, click **Protection**, and in hello tool ribbon, click **New** tooopen hello Create New Protection Group wizard.</span></span>

    ![Assistant créer un nouveau groupe de Protection de hello ouvert](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="19649-310">Hello **créer un nouveau groupe de Protection** boîte de dialogue Assistant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-310">hello **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Boîte de dialogue Assistant Création d’un nouveau groupe de protection](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="19649-312">Cliquez sur **suivant** tooadvance toohello **sélectionner le type de groupe de protection** page.</span><span class="sxs-lookup"><span data-stu-id="19649-312">Click **Next** tooadvance toohello **Select protection group type** page.</span></span>

2. <span data-ttu-id="19649-313">Sur hello **type de groupe de Protection de sélectionner** , sélectionnez **serveurs** puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19649-313">On hello **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="19649-314">Hello **sélectionner les membres du groupe** page s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19649-314">hello **Select group members** page appears.</span></span>

3. <span data-ttu-id="19649-315">Sur hello **sélectionner les membres du groupe** page, les membres disponibles hello et membres de hello sélectionné s’affichent.</span><span class="sxs-lookup"><span data-stu-id="19649-315">On hello **Select group members** page, hello available members and hello selected members appear.</span></span> <span data-ttu-id="19649-316">Sélectionner les membres hello que vous souhaitez tooprotect, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19649-316">Select hello members that you want tooprotect, and then click **Next**.</span></span>

    ![Sélectionner les membres du groupe](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="19649-318">Lorsque vous sélectionnez un membre, si vous sélectionnez un dossier qui contient d’autres dossiers ou machines virtuelles, ces dossiers et machines virtuelles sont également sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="19649-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="19649-319">inclusion de Hello des dossiers de hello et des machines virtuelles dans le dossier parent de hello est appelée une protection au niveau du dossier.</span><span class="sxs-lookup"><span data-stu-id="19649-319">hello inclusion of hello folders and VMs in hello parent folder is called folder-level protection.</span></span> <span data-ttu-id="19649-320">tooremove un dossier ou la machine virtuelle, hello désactivez case à cocher.</span><span class="sxs-lookup"><span data-stu-id="19649-320">tooremove a folder or VM, clear hello check box.</span></span>

    <span data-ttu-id="19649-321">Si une machine virtuelle, ou un dossier qui contient un ordinateur virtuel, est déjà protégé tooAzure, vous ne pouvez pas sélectionner de nouveau cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="19649-321">If a VM, or a folder containing a VM, is already protected tooAzure, you cannot select that VM again.</span></span> <span data-ttu-id="19649-322">Autrement dit, une fois un ordinateur virtuel protégé tooAzure, il ne peut pas être protégé là encore, les points de récupération en double qui empêche la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="19649-322">That is, after a VM is protected tooAzure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="19649-323">Si vous souhaitez toosee quelle instance de serveur de sauvegarde Azure protège déjà un membre, le nom de hello de toosee de membre de toohello du point de protection du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-323">If you want toosee which Azure Backup Server instance already protects a member, point toohello member toosee hello name of hello protecting server.</span></span>

4. <span data-ttu-id="19649-324">Sur hello **sélectionner la méthode de Protection des données** , entrez un nom pour le groupe de protection hello.</span><span class="sxs-lookup"><span data-stu-id="19649-324">On hello **Select Data Protection Method** page, enter a name for hello protection group.</span></span> <span data-ttu-id="19649-325">En ligne et la protection à court terme (toodisk) sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="19649-325">Short-term protection (toodisk) and online protection are selected.</span></span> <span data-ttu-id="19649-326">Si vous souhaitez que la protection en ligne toouse (tooAzure), vous devez utiliser toodisk de protection à court terme.</span><span class="sxs-lookup"><span data-stu-id="19649-326">If you want toouse online protection (tooAzure), you must use short-term protection toodisk.</span></span> <span data-ttu-id="19649-327">Cliquez sur **suivant** tooproceed toohello une plage d’une protection à court terme.</span><span class="sxs-lookup"><span data-stu-id="19649-327">Click **Next** tooproceed toohello short-term protection range.</span></span>

    ![Sélectionner la méthode de protection des données](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="19649-329">Sur hello **spécifier les objectifs à court terme** page, pour **de rétention**, spécifiez le nombre hello de jours pendant lesquels vous souhaitez que les points de récupération de tooretain est *stockées toodisk*.</span><span class="sxs-lookup"><span data-stu-id="19649-329">On hello **Specify Short-Term Goals** page, for **Retention Range**, specify hello number of days that you want tooretain recovery points that are *stored toodisk*.</span></span> <span data-ttu-id="19649-330">Si vous souhaitez que les jours lorsque les points de récupération sont effectuées et hello toochange, cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="19649-330">If you want toochange hello time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="19649-331">points de récupération à court terme Hello sont des sauvegardes complètes.</span><span class="sxs-lookup"><span data-stu-id="19649-331">hello short-term recovery points are full backups.</span></span> <span data-ttu-id="19649-332">Ils ne fonctionnent pas comme des sauvegardes incrémentielles.</span><span class="sxs-lookup"><span data-stu-id="19649-332">They are not incremental backups.</span></span> <span data-ttu-id="19649-333">Lorsque vous êtes satisfait des objectifs à court terme de hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19649-333">When you are satisfied with hello short-term goals, click **Next**.</span></span>

    ![Spécifier les objectifs à court terme](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="19649-335">Sur hello **vérifier l’Allocation de disque** , examinez, si nécessaire, modifiez l’espace disque hello hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="19649-335">On hello **Review Disk Allocation** page, review and if necessary, modify hello disk space for hello VMs.</span></span> <span data-ttu-id="19649-336">Hello recommandé d’allocations de disques sont basées sur la rétention hello est spécifiée dans hello **spécifier les objectifs à court terme** , page de type hello de charge de travail et la taille de hello Hello des données protégées (identifiées à l’étape 3).</span><span class="sxs-lookup"><span data-stu-id="19649-336">hello recommended disk allocations are based on hello retention range that is specified in hello **Specify Short-Term Goals** page, hello type of workload, and hello size of hello protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="19649-337">**Taille des données :** taille des données hello dans le groupe de protection hello.</span><span class="sxs-lookup"><span data-stu-id="19649-337">**Data size:** Size of hello data in hello protection group.</span></span>
  - <span data-ttu-id="19649-338">**Espace disque :** hello quantité d’espace disque pour le groupe de protection hello recommandée.</span><span class="sxs-lookup"><span data-stu-id="19649-338">**Disk space:** hello recommended amount of disk space for hello protection group.</span></span> <span data-ttu-id="19649-339">Si vous souhaitez toomodify ce paramètre, vous devez allouer un espace total légèrement supérieur à la quantité hello que vous estimez que chaque source de données augmente.</span><span class="sxs-lookup"><span data-stu-id="19649-339">If you want toomodify this setting, you should allocate total space that is slightly larger than hello amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="19649-340">**Colocalisation de données :** si vous activez la colocalisation, plusieurs sources de données dans la protection de hello peuvent mapper tooa même réplica et volume des points de récupération.</span><span class="sxs-lookup"><span data-stu-id="19649-340">**Colocate data:** If you turn on colocation, multiple data sources in hello protection can map tooa single replica and recovery point volume.</span></span> <span data-ttu-id="19649-341">La colocalisation n’est pas prise en charge pour toutes les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="19649-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="19649-342">**Croissance automatique :** si vous activez ce paramètre, si des données dans le groupe de hello protégé dépassent l’allocation initiale hello, System Center Data Protection Manager tente de taille du disque tooincrease hello de 25 pour cent.</span><span class="sxs-lookup"><span data-stu-id="19649-342">**Automatically grow:** If you turn on this setting, if data in hello protected group outgrows hello initial allocation, System Center Data Protection Manager tries tooincrease hello disk size by 25 percent.</span></span>
  - <span data-ttu-id="19649-343">**Détails du pool de stockage :** affiche l’état de hello hello du pool de stockage, y compris le total et la taille de disque restante.</span><span class="sxs-lookup"><span data-stu-id="19649-343">**Storage pool details:** Shows hello status of hello storage pool, including total and remaining disk size.</span></span>

    ![Vérifier l’allocation de disque](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="19649-345">Lorsque vous êtes satisfait de l’allocation d’espace hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19649-345">When you are satisfied with hello space allocation, click **Next**.</span></span>

7. <span data-ttu-id="19649-346">Sur hello **choisir la méthode de création de réplica** page, spécifiez comment vous souhaitez que la copie initiale toogenerate hello ou réplica, des données de hello protégé sur Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="19649-346">On hello **Choose Replica Creation Method** page, specify how you want toogenerate hello initial copy, or replica, of hello protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="19649-347">valeur par défaut Hello est **automatiquement sur le réseau de hello** et **maintenant**.</span><span class="sxs-lookup"><span data-stu-id="19649-347">hello default is **Automatically over hello network** and **Now**.</span></span> <span data-ttu-id="19649-348">Si vous utilisez la valeur par défaut de hello, nous vous recommandons de spécifier une heure creuse.</span><span class="sxs-lookup"><span data-stu-id="19649-348">If you use hello default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="19649-349">Choisissez **Ultérieurement** et spécifiez le jour et l’heure.</span><span class="sxs-lookup"><span data-stu-id="19649-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="19649-350">Pour grandes quantités de données ou des conditions réseau moins optimales, envisagez de répliquer des données hello hors connexion à l’aide d’un support amovible.</span><span class="sxs-lookup"><span data-stu-id="19649-350">For large amounts of data or less-than-optimal network conditions, consider replicating hello data offline by using removable media.</span></span>

    <span data-ttu-id="19649-351">Après avoir effectué vos sélections, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="19649-351">After you have made your choices, click **Next**.</span></span>

    ![Choisir la méthode de création d’un réplica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="19649-353">Sur hello **Options de vérification de cohérence** page, sélectionnez comment et quand des vérifications de cohérence de hello tooautomate.</span><span class="sxs-lookup"><span data-stu-id="19649-353">On hello **Consistency Check Options** page, select how and when tooautomate hello consistency checks.</span></span> <span data-ttu-id="19649-354">Vous pouvez exécuter les vérifications de cohérence lorsque les données du réplica deviennent incohérentes ou en fonction d’une planification définie.</span><span class="sxs-lookup"><span data-stu-id="19649-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="19649-355">Si vous ne souhaitez pas les vérifications de cohérence automatiques tooconfigure, vous pouvez exécuter une vérification manuelle.</span><span class="sxs-lookup"><span data-stu-id="19649-355">If you don't want tooconfigure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="19649-356">Dans la zone de protection hello de console du serveur de sauvegarde Azure hello, cliquez sur le groupe de protection hello, puis sélectionnez **effectuer une vérification de cohérence**.</span><span class="sxs-lookup"><span data-stu-id="19649-356">In hello protection area of hello Azure Backup Server console, right-click hello protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="19649-357">Cliquez sur **suivant** page suivante de toomove toohello.</span><span class="sxs-lookup"><span data-stu-id="19649-357">Click **Next** toomove toohello next page.</span></span>

9. <span data-ttu-id="19649-358">Sur hello **spécifier les données de Protection en ligne** , sélectionnez une ou plusieurs sources de données que vous souhaitez tooprotect.</span><span class="sxs-lookup"><span data-stu-id="19649-358">On hello **Specify Online Protection Data** page, select one or more data sources that you want tooprotect.</span></span> <span data-ttu-id="19649-359">Vous pouvez sélectionner les membres hello individuellement, ou cliquez sur **sélectionner tout** toochoose tous les membres.</span><span class="sxs-lookup"><span data-stu-id="19649-359">You can select hello members individually, or click **Select All** toochoose all members.</span></span> <span data-ttu-id="19649-360">Après avoir choisi les membres hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19649-360">After you choose hello members, click **Next**.</span></span>

    ![Spécifier les données de protection en ligne](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="19649-362">Sur hello **spécifier la planification de sauvegarde en ligne** , spécifiez les points de récupération toogenerate hello planification de sauvegarde sur disque hello.</span><span class="sxs-lookup"><span data-stu-id="19649-362">On hello **Specify Online Backup Schedule** page, specify hello schedule toogenerate recovery points from hello disk backup.</span></span> <span data-ttu-id="19649-363">Une fois le point de récupération hello est généré, il est coffre des Services de récupération toohello transférées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="19649-363">After hello recovery point is generated, it is transferred toohello Recovery Services vault in Azure.</span></span> <span data-ttu-id="19649-364">Lorsque vous êtes satisfait de la planification de sauvegarde en ligne hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19649-364">When you are satisfied with hello online backup schedule, click **Next**.</span></span>

    ![Spécifier la planification de sauvegarde en ligne](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="19649-366">Sur hello **spécifier la stratégie de rétention en ligne** page, indiquez si la durée pendant laquelle vous souhaitez que les données de sauvegarde de hello tooretain dans Azure.</span><span class="sxs-lookup"><span data-stu-id="19649-366">On hello **Specify Online Retention Policy** page, indicate how long you want tooretain hello backup data in Azure.</span></span> <span data-ttu-id="19649-367">Après avoir défini la stratégie de hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19649-367">After hello policy is defined, click **Next**.</span></span>

    ![Spécifier la stratégie de rétention en ligne](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="19649-369">La durée de conservation des données dans Azure n’est soumise à aucune restriction.</span><span class="sxs-lookup"><span data-stu-id="19649-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="19649-370">Lorsque vous stockez des données de point de récupération dans Azure, hello uniquement limite est que vous ne peut pas avoir plus de 9999 points de récupération par instance protégée.</span><span class="sxs-lookup"><span data-stu-id="19649-370">When you store recovery point data in Azure, hello only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="19649-371">Dans cet exemple, les instance protégée hello est serveur VMware de hello.</span><span class="sxs-lookup"><span data-stu-id="19649-371">In this example, hello protected instance is hello VMware server.</span></span>

12. <span data-ttu-id="19649-372">Sur hello **Résumé** page, passez en revue les détails de hello pour vos paramètres et les membres du groupe de protection, puis cliquez sur **créer un groupe**.</span><span class="sxs-lookup"><span data-stu-id="19649-372">On hello **Summary** page, review hello details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Résumé des paramètres et des membres du groupe de protection](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="19649-374">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19649-374">Next steps</span></span>
<span data-ttu-id="19649-375">Si vous utilisez des charges de travail Azure Backup Server tooprotect VMware, peuvent vous intéresser à l’aide d’Azure Backup Server toohelp protéger un [Microsoft Exchange server](./backup-azure-exchange-mabs.md), un [batterie de serveurs Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md), ou un [Base de données SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="19649-375">If you use Azure Backup Server tooprotect VMware workloads, you may be interested in using Azure Backup Server toohelp protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="19649-376">Pour plus d’informations sur les problèmes avec l’inscription de l’agent de hello, la configuration du groupe de protection hello ou sauvegarder des travaux, consultez [dépanner Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="19649-376">For information on problems with registering hello agent, configuring hello protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
