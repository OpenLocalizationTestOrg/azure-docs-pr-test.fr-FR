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
# <a name="back-up-a-vmware-server-tooazure"></a>Sauvegarder un tooAzure du serveur VMware

Cet article explique comment tooconfigure Azure Backup Server toohelp protéger les charges de travail VMware server. Cet article suppose que vous avez déjà installé le serveur de sauvegarde Azure. Si vous n’avez pas installé Azure Backup Server, consultez [préparer tooback des charges de travail à l’aide d’Azure Backup Server](backup-azure-microsoft-azure-backup.md).

Un serveur de sauvegarde Azure peut sauvegarder ou aider à protéger les versions 6.5, 6.0 et 5.5 de VMware vCenter Server.


## <a name="create-a-secure-connection-toohello-vcenter-server"></a>Créer un connexion sécurisée toohello du serveur vCenter

Par défaut, le serveur de sauvegarde Azure communique avec chaque serveur vCenter via un canal HTTPS. tooturn sur une communication sécurisée hello, nous vous recommandons d’installer le certificat d’autorité de certification (CA) VMware hello sur Azure Backup Server. Si vous ne nécessitent pas une communication sécurisée, préférez l’exigence de toodisable hello HTTPS, consultez [désactiver le protocole de communication sécurisé](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol). toocreate une connexion sécurisée entre le serveur de sauvegarde Azure et hello du serveur vCenter, importez le certificat de confiance de hello sur Azure Backup Server.

En règle générale, vous utilisez un navigateur sur hello Azure Backup Server machine tooconnect toohello serveur vCenter via hello vSphere Client Web. Hello première fois que vous utilisez hello Azure Backup Server navigateur tooconnect toohello vCenter Server, connexion de hello n’est pas sécurisée. Hello suivant image montre les connexions hello non sécurisé.

![Exemple de connexion non sécurisée tooVMware serveur](./media/backup-azure-backup-server-vmware/unsecure-url.png)

toofix ce problème et créer une connexion sécurisée, télécharger des certificats d’autorité de certification racine hello approuvé.

1. Dans le navigateur de hello sur Azure Backup Server, entrez hello URL toohello vSphere Client Web. page de connexion du Client Web Hello vSphere s’affiche.

    ![Client web vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    Bas hello informations hello pour les développeurs et administrateurs, recherchez hello **téléchargement les certificats d’autorité de certification racine de confiance** lien.

    ![Certificats d’autorité de certification racine lien toodownload hello approuvé](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  Si vous ne voyez la page de connexion du Client Web hello vSphere, vérifiez les paramètres de proxy de votre navigateur.

2. Cliquez sur **Télécharger les certificats approuvés de l’autorité de certification racine**.

    Hello vCenter Server télécharge un ordinateur local tooyour de fichier. Hello nom de fichier est nommé **télécharger**. En fonction de votre navigateur, vous recevez un message vous demandant si tooopen ou enregistrer le fichier de hello.

    ![message de téléchargement lorsque les certificats sont téléchargés](./media/backup-azure-backup-server-vmware/download-certs.png)

3. Enregistrer l’emplacement du fichier de hello tooa sur Azure Backup Server. Lorsque vous enregistrez le fichier de hello, ajoutez l’extension de nom de fichier .zip hello.

    fichier de Hello est un fichier .zip qui contient des informations sur les certificats de hello hello. Avec l’extension .zip de hello, vous pouvez utiliser les outils d’extraction hello.

4. Avec le bouton droit **download.zip**, puis sélectionnez **extraire tout** contenu de hello tooextract.

    fichier .zip de Hello extrait son contenu tooa sous-dossier **certificats**. Deux types de fichiers s’affichent dans le dossier de certificats hello. fichier de certificat racine Hello possède une extension qui commence par un numéro de séquence comme.0 et.1.
    
    fichier de liste de révocation Hello possède une extension qui commence par une séquence comme .r0 ou .r1. fichier de liste de révocation de Hello est associé à un certificat.

    ![Fichier de téléchargement extrait localement ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. Bonjour **certificats** dossier, cliquez sur le fichier de certificat racine hello, puis cliquez sur **renommer**.

    ![Renommer un certificat racine ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    Modification extension too.crt du certificat d’origine hello. Lorsque le système vous demande si vous êtes sûr de vouloir extension de hello toochange, cliquez sur **Oui** ou **OK**. Dans le cas contraire, vous modifiez fonction du fichier hello. icône Hello hello fichier modifications tooan icône qui représente un certificat racine.

6. Cliquez sur le certificat racine de hello et dans le menu contextuel de hello, sélectionnez **installer le certificat**.

    Hello **Assistant Importation de certificat** boîte de dialogue s’affiche.

7. Bonjour **Assistant Importation de certificat** boîte de dialogue, sélectionnez **ordinateur Local** en tant que destination hello pour les certificats hello, puis cliquez sur **suivant** toocontinue.

    ![Options de destination de stockage du certificat ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    Si vous demande si vous souhaitez que l’ordinateur de toohello de modifications de tooallow, cliquez sur **Oui** ou **OK**, modifications de hello tooall.

8. Sur hello **magasin de certificats** page, sélectionnez **placer tous les certificats dans hello suivant magasin**, puis cliquez sur **Parcourir** magasin de certificats toochoose hello.

    ![Placer des certificats dans une zone de stockage spécifique](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    Hello **sélectionner un magasin de certificats** boîte de dialogue s’affiche.

    ![Arborescence des dossiers de stockage de certificats](./media/backup-azure-backup-server-vmware/cert-store.png)

9. Sélectionnez **autorités de Certification racines de confiance** en tant que dossier de destination hello pour les certificats hello, puis cliquez sur **OK**.

    ![Dossier de destination des certificats](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    Hello **autorités de Certification racines de confiance** dossier est confirmé comme magasin de certificats hello. Cliquez sur **Suivant**.

    ![Dossier de magasin de certificats](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. Sur hello **fin hello Assistant Importation de certificat** page, vérifiez que le certificat hello est dans le dossier de votre choix hello, puis cliquez sur **Terminer**.

    ![Vérifier le certificat se trouve dans le dossier approprié de hello](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    Une boîte de dialogue s’affiche, l’importation du certificat réussie hello est confirmée.

11. Se connecter toohello vCenter tooconfirm serveur que votre connexion est sécurisée.

  Si l’importation du certificat hello ne réussit pas, et vous ne pouvez pas établir une connexion sécurisée, la documentation hello VMware vSphere sur [obtention de certificats de serveur](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).

  Si vous avez des limites sécurisés au sein de votre organisation et que vous ne souhaitez pas tooturn sur hello le protocole HTTPS, utilisez hello suivant la procédure toodisable hello sécuriser les communications.

### <a name="disable-secure-communication-protocol"></a>Désactiver le protocole de communication sécurisée

Si votre organisation ne nécessite pas le protocole HTTPS hello, utilisez hello suivant les étapes toodisable HTTPS. toodisable hello le comportement par défaut, créez une clé de Registre qui ignore le comportement par défaut de hello.

1. Copiez et collez hello après le texte dans un fichier .txt.

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. Enregistrer l’ordinateur de serveur de sauvegarde Azure hello fichier tooyour. Nom de fichier hello, utilisez DisableSecureAuthentication.reg.

3. Double-cliquez sur entrée de Registre hello fichier tooactivate hello.


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a>Créer un compte d’utilisateur et le rôle sur hello du serveur vCenter

Sur le serveur vCenter de hello, un rôle est un ensemble prédéfini de privilèges. Un administrateur de serveur vCenter crée des rôles de hello. tooassign autorisations, administrateur de hello paires de comptes d’utilisateur à un rôle. tooback d’informations d’identification tooestablish hello utilisateur nécessaires d’ordinateur du serveur vCenter hello, créez un rôle avec des privilèges spécifiques et l’associer compte d’utilisateur hello rôle de hello.

Serveur de sauvegarde Azure utilise un tooauthenticate nom d’utilisateur et mot de passe avec hello du serveur vCenter. Le serveur de sauvegarde Azure utilise ces informations d’identification comme authentification pour toutes les opérations de sauvegarde.

tooadd un rôle de serveur vCenter et ses privilèges pour un administrateur de sauvegarde :

1. Se connecter dans toohello vCenter Server, puis dans hello du serveur vCenter **Navigator** du panneau, cliquez sur **Administration**.

    ![Option d’administration dans le panneau Navigateur du serveur vCenter](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. Dans **Administration** sélectionnez **rôles**, puis dans hello **rôles** cliquez sur le panneau de configuration hello ajouter l’icône de rôle (symbole + hello).

    ![Ajouter un rôle](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    Hello **Create Role** boîte de dialogue s’affiche.

    ![Créer un rôle](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. Bonjour **Create Role** la boîte de dialogue hello **nom de rôle** , entrez *BackupAdminRole*. nom du rôle Hello peut être comme vous le souhaitez, mais il doit être reconnaissable fins du rôle hello.

4. Sélectionnez les privilèges hello pour la version appropriée de hello de vCenter, puis cliquez sur **OK**. Hello tableau suivant identifie les privilèges de hello requise de vCenter 6.0 et vCenter 5.5.

  Lorsque vous sélectionnez des privilèges de hello, cliquez sur hello icône suivant toohello parent étiquette tooexpand hello parent et vue hello enfants des privilèges. privilèges de VirtualMachine tooselect hello, vous devez toogo plusieurs niveaux dans hello parent de hiérarchie enfant. Vous n’avez pas besoin tooselect tous les privilèges enfant au sein d’un privilège de parent.

  ![Hiérarchie des privilèges parent-enfant](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  Après avoir cliqué sur **OK**, hello nouveau rôle s’affiche dans la liste hello sur Panneau de configuration de rôles hello.

|Privilèges de vCenter 6.0| Privilèges de vCenter 5.5|
|--------------------------|---------------------------|
|Datastore.AllocateSpace   | Datastore.AllocateSpace|
|Global.ManageCustomFields | Global.ManageCustomerFields|
|Global.SetCustomFields    |   |
|Host.Local.CreateVM       | Network.Assign |
|Network.Assign            |  |
|Resource.AssignVMToPool   |  |
|VirtualMachine.Config.AddNewDisk  | VirtualMachine.Config.AddNewDisk   |
|VirtualMachine.Config.AdvanceConfig| VirtualMachine.Config.AdvancedConfig|
|VirtualMachine.Config.ChangeTracking| VirtualMachine.Config.ChangeTracking |
|VirtualMachine.Config.HostUSBDevice||
|VirtualMachine.Config.QueryUnownedFiles|    |
|VirtualMachine.Config.SwapPlacement| VirtualMachine.Config.SwapPlacement |
|VirtualMachine.Interact.PowerOff| VirtualMachine.Interact.PowerOff |
|VirtualMachine.Inventory.Create| VirtualMachine.Inventory.Create |
|VirtualMachine.Provisioning.DiskRandomAccess| |
|VirtualMachine.Provisioning.DiskRandomRead|VirtualMachine.Provisioning.DiskRandomRead |
|VirtualMachine.State.CreateSnapshot| VirtualMachine.State.CreateSnapshot|
|VirtualMachine.State.RemoveSnapshot|VirtualMachine.State.RemoveSnapshot |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a>Créer un compte d’utilisateur et des autorisations pour un serveur vCenter

Après avoir configuré la rôle hello avec des privilèges, créez un compte d’utilisateur. compte d’utilisateur Hello a un nom et un mot de passe, qui fournit les informations d’identification de hello sont utilisées pour l’authentification.

1. toocreate un compte d’utilisateur dans le serveur vCenter Server hello **Navigator** du panneau, cliquez sur **utilisateurs et groupes**.

    ![Option Utilisateurs et groupes](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    Hello **vCenter utilisateurs et groupes** panneau s’affiche.

    ![Panneau Utilisateurs et groupes vCenter](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. Bonjour **vCenter utilisateurs et groupes** Panneau de configuration, sélectionnez hello **utilisateurs** onglet, puis cliquez sur hello ajouter les utilisateurs icône (symbole + hello).

    Hello **nouvel utilisateur** boîte de dialogue s’affiche.

3. Bonjour **nouvel utilisateur** boîte de dialogue zone, ajouter des informations de l’utilisateur hello, puis sur **OK**. Dans cette procédure, le nom d’utilisateur hello est BackupAdmin.

    ![Boîte de dialogue Nouvel utilisateur](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    nouveau compte d’utilisateur Hello s’affiche dans la liste de hello.

4. compte d’utilisateur tooassociate hello avec rôle hello, Bonjour **Navigator** du panneau, cliquez sur **autorisations globales**. Bonjour **autorisations globales** Panneau de configuration, sélectionnez hello **gérer** onglet, puis cliquez sur hello ajouter icône (symbole + hello).

    ![Panneau Autorisations globales](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    Hello **Global autorisations racine - ajouter une autorisation** boîte de dialogue s’affiche.

5. Bonjour **racine autorisation globale - ajouter une autorisation** boîte de dialogue, cliquez sur **ajouter** toochoose hello utilisateur ou un groupe.

    ![Choisir un utilisateur ou un groupe](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    Hello **sélectionner des utilisateurs/groupes** boîte de dialogue s’affiche.

6. Bonjour **sélectionner des utilisateurs/groupes** boîte de dialogue, choisissez **BackupAdmin** puis cliquez sur **ajouter**.

    Dans **utilisateurs**, hello *domaine om_utilisateur* format est utilisé pour le compte d’utilisateur hello. Si vous voulez toouse un autre domaine, sélectionnez-le dans hello **domaine** liste.

    ![Ajouter un utilisateur BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    Cliquez sur **OK** tooadd hello sélectionné d’utilisateurs toohello **ajouter une autorisation** boîte de dialogue.

7. Maintenant que vous avez identifié les utilisateur hello, attribuer le rôle toohello hello. Dans **affecté le rôle**, dans la liste déroulante hello, sélectionnez **BackupAdminRole**, puis cliquez sur **OK**.

    ![Affecter des utilisateurs toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  Sur hello **gérer** onglet Bonjour **autorisations globales** Panneau de configuration, nouveau compte d’utilisateur hello et rôle de hello associé s’affichent dans la liste de hello.


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a>Définir les informations d’identification de serveur vCenter sur le serveur de sauvegarde Azure

Avant d’ajouter hello VMware server tooAzure sauvegarde du serveur, installez [1 de mise à jour pour Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).

1. tooopen Azure Backup Server, double-cliquez sur l’icône de hello sur le bureau du serveur de sauvegarde Azure hello.

    ![Icône du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    Si vous ne trouvez l’icône de hello sur le bureau de hello, ouvrez Azure Backup Server à partir de la liste de hello des applications installées. nom de l’application Hello Azure Backup Server est appelé Microsoft Azure Backup.

2. Dans la console Azure Backup Server hello, cliquez sur **gestion**, cliquez sur **les serveurs de Production**, puis cliquez sur la barre d’outils hello, **gestion de VMware**.

    ![Console du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    Hello **gérer les informations d’identification** boîte de dialogue s’affiche.

    ![Boîte de dialogue Gérer les informations d’identification du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. Bonjour **gérer les informations d’identification** boîte de dialogue, cliquez sur **ajouter** tooopen hello **ajouter les informations d’identification** boîte de dialogue.

4. Bonjour **ajouter les informations d’identification** boîte de dialogue, entrez un nom et une description pour les nouvelles informations d’identification de hello. Spécifier un mot de passe et nom d’utilisateur hello. nom de Hello, *informations d’identification de Contoso Vcenter* sert tooidentify hello dans informations d’identification suit hello. Utilisez hello même nom d’utilisateur et mot de passe utilisé pour hello du serveur vCenter. Si le serveur vCenter Server hello et Azure Backup Server ne sont pas dans hello du même domaine, dans **nom d’utilisateur**, spécifiez le domaine de hello.

    ![Boîte de dialogue Ajouter des informations d’identification du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    Cliquez sur **ajouter** tooadd hello de nouvelles informations d’identification tooAzure sauvegarde du serveur. des informations d’identification de Hello s’affiche dans la liste hello Bonjour **gérer les informations d’identification** boîte de dialogue.
    
    ![Boîte de dialogue Gérer les informations d’identification du serveur de sauvegarde Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. tooclose hello **gérer les informations d’identification** boîte de dialogue, cliquez sur hello **X** dans le coin supérieur droit de hello.


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a>Ajouter hello vCenter Server tooAzure sauvegarde du serveur

Assistant d’ajout de serveur de production est utilisé tooadd hello vCenter Server tooAzure sauvegarde du serveur.

Assistant Ajout de serveur Production, hello complet suivant la procédure de tooopen :

1. Dans la console Azure Backup Server hello, cliquez sur **gestion**, cliquez sur **les serveurs de Production**, puis cliquez sur **ajouter**.

    ![Ouvrir l’Assistant Ajout d’un serveur de production](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    Hello **Assistant d’ajout de serveur de Production** boîte de dialogue s’affiche.

    ![Assistant Ajout d’un serveur de production](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. Sur hello **type de sélectionner un serveur de Production** , sélectionnez **serveurs VMware**, puis cliquez sur **suivant**.

3. Dans **serveur nom/adresse IP**, spécifiez le nom de domaine complet de hello (FQDN) ou l’adresse IP du serveur de VMware hello. Si tous les serveurs de ESXi hello sont gérés par hello vCenter même, vous pouvez utiliser le nom hello vCenter.

    ![Spécifier l’adresse IP ou le nom de domaine complet du serveur VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. Dans **Port SSL**, entrez le port hello toocommunicate utilisé avec VMware server de hello. Utiliser le port 443, qui est le port par défaut de hello, sauf si vous savez qu’un autre port est requis.

5. Dans **spécifier les informations d’identification**, sélectionnez hello d’informations d’identification que vous avez créé précédemment.

    ![Indiquer les informations d’identification](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. Cliquez sur **ajouter** tooadd hello VMware toohello une liste de serveur **ajouté des serveurs VMware**, puis cliquez sur **suivant** toomove toohello page suivante dans l’Assistant de hello.

    ![Ajouter un serveur VMware et des informations d’identification](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. Bonjour **Résumé** , cliquez sur **ajouter** tooadd hello spécifié VMware server tooAzure sauvegarde du serveur.

    ![Ajouter VMware server tooAzure sauvegarde du serveur](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  sauvegarde du serveur VMware Hello est une sauvegarde sans agent et hello nouveau serveur est ajouté immédiatement. Hello **Terminer** page affiche hello de résultats.

  ![Page Terminer](./media/backup-azure-backup-server-vmware/summary-screen.png)

  tooadd plusieurs instances de vCenter Server tooAzure sauvegarde du serveur, répétez hello précédentes étapes de cette section.

Après avoir ajouté hello vCenter Server tooAzure sauvegarde du serveur, étape suivante de hello est toocreate un groupe de protection. groupe de protection Hello spécifie hello différentes informations de rétention à court ou à long terme, et il est où vous définissez et appliquez la stratégie de sauvegarde hello. stratégie de sauvegarde Hello est planification hello pour les cas de sauvegardes, et ce qui est sauvegardé.


## <a name="configure-a-protection-group"></a>Configurer un groupe de protection

Si vous n’avez pas utilisé System Center Data Protection Manager ou Azure Backup Server avant, consultez [planifier les sauvegardes de disque](https://technet.microsoft.com/library/hh758026.aspx) tooprepare votre environnement matériel. Après avoir vérifié que vous disposez de stockage approprié, utilisez des ordinateurs virtuels hello créer un nouveau groupe de Protection Assistant tooadd VMware.

1. Dans la console Azure Backup Server hello, cliquez sur **Protection**, dans la barre d’outils hello, cliquez sur **nouveau** Assistant de créer un nouveau groupe de Protection tooopen hello.

    ![Assistant créer un nouveau groupe de Protection de hello ouvert](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    Hello **créer un nouveau groupe de Protection** boîte de dialogue Assistant s’affiche.

    ![Boîte de dialogue Assistant Création d’un nouveau groupe de protection](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    Cliquez sur **suivant** tooadvance toohello **sélectionner le type de groupe de protection** page.

2. Sur hello **type de groupe de Protection de sélectionner** , sélectionnez **serveurs** puis cliquez sur **suivant**. Hello **sélectionner les membres du groupe** page s’affiche.

3. Sur hello **sélectionner les membres du groupe** page, les membres disponibles hello et membres de hello sélectionné s’affichent. Sélectionner les membres hello que vous souhaitez tooprotect, puis cliquez sur **suivant**.

    ![Sélectionner les membres du groupe](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    Lorsque vous sélectionnez un membre, si vous sélectionnez un dossier qui contient d’autres dossiers ou machines virtuelles, ces dossiers et machines virtuelles sont également sélectionnés. inclusion de Hello des dossiers de hello et des machines virtuelles dans le dossier parent de hello est appelée une protection au niveau du dossier. tooremove un dossier ou la machine virtuelle, hello désactivez case à cocher.

    Si une machine virtuelle, ou un dossier qui contient un ordinateur virtuel, est déjà protégé tooAzure, vous ne pouvez pas sélectionner de nouveau cette machine virtuelle. Autrement dit, une fois un ordinateur virtuel protégé tooAzure, il ne peut pas être protégé là encore, les points de récupération en double qui empêche la création d’une machine virtuelle. Si vous souhaitez toosee quelle instance de serveur de sauvegarde Azure protège déjà un membre, le nom de hello de toosee de membre de toohello du point de protection du serveur de hello.

4. Sur hello **sélectionner la méthode de Protection des données** , entrez un nom pour le groupe de protection hello. En ligne et la protection à court terme (toodisk) sont sélectionnés. Si vous souhaitez que la protection en ligne toouse (tooAzure), vous devez utiliser toodisk de protection à court terme. Cliquez sur **suivant** tooproceed toohello une plage d’une protection à court terme.

    ![Sélectionner la méthode de protection des données](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. Sur hello **spécifier les objectifs à court terme** page, pour **de rétention**, spécifiez le nombre hello de jours pendant lesquels vous souhaitez que les points de récupération de tooretain est *stockées toodisk*. Si vous souhaitez que les jours lorsque les points de récupération sont effectuées et hello toochange, cliquez sur **modifier**. points de récupération à court terme Hello sont des sauvegardes complètes. Ils ne fonctionnent pas comme des sauvegardes incrémentielles. Lorsque vous êtes satisfait des objectifs à court terme de hello, cliquez sur **suivant**.

    ![Spécifier les objectifs à court terme](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. Sur hello **vérifier l’Allocation de disque** , examinez, si nécessaire, modifiez l’espace disque hello hello machines virtuelles. Hello recommandé d’allocations de disques sont basées sur la rétention hello est spécifiée dans hello **spécifier les objectifs à court terme** , page de type hello de charge de travail et la taille de hello Hello des données protégées (identifiées à l’étape 3).  

  - **Taille des données :** taille des données hello dans le groupe de protection hello.
  - **Espace disque :** hello quantité d’espace disque pour le groupe de protection hello recommandée. Si vous souhaitez toomodify ce paramètre, vous devez allouer un espace total légèrement supérieur à la quantité hello que vous estimez que chaque source de données augmente.
  - **Colocalisation de données :** si vous activez la colocalisation, plusieurs sources de données dans la protection de hello peuvent mapper tooa même réplica et volume des points de récupération. La colocalisation n’est pas prise en charge pour toutes les charges de travail.
  - **Croissance automatique :** si vous activez ce paramètre, si des données dans le groupe de hello protégé dépassent l’allocation initiale hello, System Center Data Protection Manager tente de taille du disque tooincrease hello de 25 pour cent.
  - **Détails du pool de stockage :** affiche l’état de hello hello du pool de stockage, y compris le total et la taille de disque restante.

    ![Vérifier l’allocation de disque](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    Lorsque vous êtes satisfait de l’allocation d’espace hello, cliquez sur **suivant**.

7. Sur hello **choisir la méthode de création de réplica** page, spécifiez comment vous souhaitez que la copie initiale toogenerate hello ou réplica, des données de hello protégé sur Azure Backup Server.

    valeur par défaut Hello est **automatiquement sur le réseau de hello** et **maintenant**. Si vous utilisez la valeur par défaut de hello, nous vous recommandons de spécifier une heure creuse. Choisissez **Ultérieurement** et spécifiez le jour et l’heure.

    Pour grandes quantités de données ou des conditions réseau moins optimales, envisagez de répliquer des données hello hors connexion à l’aide d’un support amovible.

    Après avoir effectué vos sélections, cliquez sur **Suivant**.

    ![Choisir la méthode de création d’un réplica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. Sur hello **Options de vérification de cohérence** page, sélectionnez comment et quand des vérifications de cohérence de hello tooautomate. Vous pouvez exécuter les vérifications de cohérence lorsque les données du réplica deviennent incohérentes ou en fonction d’une planification définie.

    Si vous ne souhaitez pas les vérifications de cohérence automatiques tooconfigure, vous pouvez exécuter une vérification manuelle. Dans la zone de protection hello de console du serveur de sauvegarde Azure hello, cliquez sur le groupe de protection hello, puis sélectionnez **effectuer une vérification de cohérence**.

    Cliquez sur **suivant** page suivante de toomove toohello.

9. Sur hello **spécifier les données de Protection en ligne** , sélectionnez une ou plusieurs sources de données que vous souhaitez tooprotect. Vous pouvez sélectionner les membres hello individuellement, ou cliquez sur **sélectionner tout** toochoose tous les membres. Après avoir choisi les membres hello, cliquez sur **suivant**.

    ![Spécifier les données de protection en ligne](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. Sur hello **spécifier la planification de sauvegarde en ligne** , spécifiez les points de récupération toogenerate hello planification de sauvegarde sur disque hello. Une fois le point de récupération hello est généré, il est coffre des Services de récupération toohello transférées dans Azure. Lorsque vous êtes satisfait de la planification de sauvegarde en ligne hello, cliquez sur **suivant**.

    ![Spécifier la planification de sauvegarde en ligne](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. Sur hello **spécifier la stratégie de rétention en ligne** page, indiquez si la durée pendant laquelle vous souhaitez que les données de sauvegarde de hello tooretain dans Azure. Après avoir défini la stratégie de hello, cliquez sur **suivant**.

    ![Spécifier la stratégie de rétention en ligne](./media/backup-azure-backup-server-vmware/retention-policy.png)

    La durée de conservation des données dans Azure n’est soumise à aucune restriction. Lorsque vous stockez des données de point de récupération dans Azure, hello uniquement limite est que vous ne peut pas avoir plus de 9999 points de récupération par instance protégée. Dans cet exemple, les instance protégée hello est serveur VMware de hello.

12. Sur hello **Résumé** page, passez en revue les détails de hello pour vos paramètres et les membres du groupe de protection, puis cliquez sur **créer un groupe**.

    ![Résumé des paramètres et des membres du groupe de protection](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a>Étapes suivantes
Si vous utilisez des charges de travail Azure Backup Server tooprotect VMware, peuvent vous intéresser à l’aide d’Azure Backup Server toohelp protéger un [Microsoft Exchange server](./backup-azure-exchange-mabs.md), un [batterie de serveurs Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md), ou un [Base de données SQL Server](./backup-azure-sql-mabs.md).

Pour plus d’informations sur les problèmes avec l’inscription de l’agent de hello, la configuration du groupe de protection hello ou sauvegarder des travaux, consultez [dépanner Azure Backup Server](./backup-azure-mabs-troubleshoot.md).
