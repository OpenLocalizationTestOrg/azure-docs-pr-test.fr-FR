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
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a>Joindre un domaine géré de tooa de machine virtuelle de Red Hat Enterprise Linux 7
Cet article explique comment toojoin un tooan de machine virtuelle Red Hat Enterprise Linux (RHEL) 7 des Services de domaine Active Directory Azure géré le domaine.

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>Configurer une machine virtuelle Red Hat Enterprise Linux
Effectuer hello suivant les étapes tooprovision un RHEL 7 machine virtuelle hello portail Azure.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

    ![Tableau de bord du portail Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. Cliquez sur **nouveau** sur hello gauche du volet et le type **Red Hat** dans la barre de recherche hello comme indiqué dans hello suivant capture d’écran. Entrées pour Red Hat Enterprise Linux apparaissent dans les résultats de la recherche hello. Cliquez sur **Red Hat Enterprise Linux 7.2**.

    ![Sélectionner RHEL dans les résultats](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. résultats de recherche de Hello en hello **tout** volet doit répertorier les image hello Red Hat Enterprise Linux 7.2. Cliquez sur **Red Hat Enterprise Linux 7.2** tooview plus d’informations sur l’image de machine virtuelle hello.

    ![Sélectionner RHEL dans les résultats](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. Bonjour **Red Hat Enterprise Linux 7.2** volet, vous devez voir plus d’informations sur l’image de machine virtuelle hello. Bonjour **sélectionner un modèle de déploiement** liste déroulante, sélectionnez **classique**. Puis cliquez sur hello **créer** bouton.

    ![Afficher les détails d’une image](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. Bonjour **notions de base** page Hello **créer la machine virtuelle** Assistant, entrez hello **nom d’hôte** pour la machine virtuelle hello. Également spécifier un nom d’utilisateur administrateur local Bonjour **nom d’utilisateur** champ et un **mot de passe**. Vous pouvez également choisir toouse un utilisateur d’administrateur local SSH tooauthenticate clé hello. Sélectionnez également un **niveau tarifaire** pour la machine virtuelle de hello.

    ![Créer une machine virtuelle - Page Concepts de base](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. Bonjour **taille** page Hello **créer la machine virtuelle** taille hello Assistant, sélectionnez pour l’ordinateur virtuel de hello.

    ![Créer une machine virtuelle - Sélection de la taille](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. Bonjour **paramètres** page Hello **créer la machine virtuelle** compte de stockage hello Assistant, sélectionnez pour l’ordinateur virtuel de hello. Cliquez sur **réseau virtuel** tooselect Bonjour réseau virtuel toowhich Bonjour Linux VM doit être déployé. Bonjour **réseau virtuel** panneau, réseau virtuel de select hello dans lequel les Services de domaine Active Directory Azure est disponible. Dans cet exemple, nous choisir réseau virtuel de hello 'MyPreviewVNet'.

    ![Créer une machine virtuelle - Sélection du réseau virtuel](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. Sur hello **Résumé** page Hello **créer la machine virtuelle** hello Assistant, révision, cliquez sur **OK** bouton.

    ![Créer une machine virtuelle - Réseau virtuel sélectionné](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. Déploiement du nouvel ordinateur virtuel hello, basé sur l’image de hello RHEL 7.2 doit démarrer.

    ![Créer une machine virtuelle - Déploiement démarré](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. Après quelques minutes, hello virtuels doit être déployé avec succès et prêt à être utilisé.

    ![Créer une machine virtuelle - Déployée](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a>Se connecter à distance une machine virtuelle Linux toohello qui vient d’être mis en service.
machine virtuelle de Hello RHEL 7.2 a été configuré dans Azure. la tâche suivante Hello est tooconnect à distance virtuels toohello.

**Connecter toohello RHEL 7.2 virtual machine** suivez les instructions de hello dans l’article de hello [comment toolog sur l’ordinateur virtuel de tooa exécutant Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello étapes restantes de hello supposent que vous utilisez hello PuTTY SSH tooconnect toohello RHEL ordinateur virtuel client. Pour plus d’informations, consultez hello [page de téléchargement de PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Ouvrez hello PuTTY programme.
2. Entrez hello **nom d’hôte** pour hello nouvellement créé RHEL virtual machine. Dans cet exemple, la machine virtuelle a le nom d’hôte hello « contoso-rhel.cloudapp .net ». Si vous n’êtes pas sûr du nom d’hôte hello de votre machine virtuelle, consultez toohello tableau de bord de machine virtuelle sur hello portail Azure.

    ![Connexion PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. Ouvrez une session sur l’ordinateur virtuel de toohello à l’aide des informations d’identification de l’administrateur local hello que vous avez spécifié lors de la machine virtuelle de hello a été créé. Dans cet exemple, nous avons utilisé le compte d’administrateur local hello « mahesh ».

    ![Connexion PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a>Installer les packages requis sur une machine virtuelle Linux hello
Après connexion machine virtuelle toohello, la tâche suivante hello est tooinstall les packages requis pour la jonction de domaine sur l’ordinateur virtuel de hello. Effectuez hello comme suit :

1. **Installer realmd :** package realmd de hello est utilisé pour la jonction de domaine. Dans votre terminal PuTTY, tapez Bonjour de commande suivante :

    sudo yum install realmd

    ![Installation de realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    Après quelques minutes, package de realmd hello doit obtenir installé sur l’ordinateur virtuel de hello.

    ![Package realmd installé](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **Installer sssd :** hello realmd package en dépend des opérations de jointure sssd tooperform domaine. Dans votre terminal PuTTY, tapez Bonjour de commande suivante :

    sudo yum install sssd

    ![Installation de sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    Après quelques minutes, package de sssd hello doit obtenir installé sur l’ordinateur virtuel de hello.

    ![Package realmd installé](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **Installer kerberos :** dans votre terminal PuTTY, tapez Bonjour de commande suivante :

    sudo yum install krb5-workstation krb5-libs

    ![Installation de Kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    Après quelques minutes, package de realmd hello doit obtenir installé sur l’ordinateur virtuel de hello.

    ![Kerberos installé](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a>Joindre le domaine géré des toohello machine virtuelle Linux hello
Maintenant que les packages hello requis sont installés sur une machine virtuelle Linux hello, la tâche suivante hello est toojoin hello machine virtuelle toohello domaine géré.

1. Découvrir le domaine géré de Services de domaine AAD hello. Dans votre terminal PuTTY, tapez Bonjour de commande suivante :

    sudo realm discover CONTOSO100.COM

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    Si **domaine découvrir** est toofind Impossible de votre domaine géré, assurez-vous que ce domaine hello est accessible à partir de la machine virtuelle de hello (ping réessayer). Vérifiez également que l’ordinateur virtuel hello a été effectivement déployé toohello même réseau virtuel dans le hello domaine géré est disponible.
2. Initialisez Kerberos. Dans votre terminal PuTTY, tapez Bonjour commande suivante. Veillez à spécifier un utilisateur qui appartient le groupe de toohello « administrateurs de contrôleur de domaine AAD ». Seuls ces utilisateurs peuvent joindre le domaine géré des ordinateurs toohello.

    kinit bob@CONTOSO100.COM

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    Assurez-vous que vous spécifiez le nom de domaine hello en majuscules, kinit autre échoue.
3. Joindre le domaine toohello hello. Dans votre terminal PuTTY, tapez Bonjour commande suivante. Spécifiez hello même utilisateur que vous avez spécifié dans hello précédant l’étape ('kinit »).

    sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'

    ![Jonction de domaine](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

Vous devez obtenir un message (« correctement inscrit ordinateur du domaine ») lorsque la machine de hello est domaine géré de toohello a correctement été jointe.

## <a name="verify-domain-join"></a>Vérifier la jonction de domaine
Vous pouvez vérifier rapidement si la machine de hello a été domaine géré de toohello a correctement été jointe. Se connecter toohello VM RHEL si le compte d’utilisateur hello est correctement résolue à l’aide de SSH et un compte d’utilisateur de domaine, puis cocher toosee qui vient d’être joint à un domaine.

1. Dans votre terminal, PuTTY hello du type suivant toohello tooconnect de commande qui vient d’être joints à un domaine virtuels RHEL à l’aide de SSH. Utiliser un compte de domaine auquel appartient le domaine géré de toohello (par exemple, 'bob@CONTOSO100.COM' dans ce cas.)

    ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net
2. Dans votre terminal PuTTY, tapez hello suivant commande toosee si répertoire hello a été correctement initialisé.

    pwd
3. Dans votre terminal PuTTY, tapez hello suivant commande toosee si les appartenances aux groupes hello sont résolus correctement.

    id

Vous trouverez ci-dessous un exemple de sortie de ces commandes :

![Vérifier la jonction de domaine](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>Résolution des problèmes de jonction de domaine
Consultez toohello [jonction de domaine de résolution des problèmes](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) l’article.

## <a name="related-content"></a>Contenu connexe
* [Services de domaine Azure AD : guide de prise en main](active-directory-ds-getting-started.md)
* [Joindre un domaine des Services de domaine Active Directory de Azure géré tooan de machine virtuelle Windows Server](active-directory-ds-admin-guide-join-windows-vm.md)
* [Comment toolog sur l’ordinateur virtuel de tooa exécutant Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* [Installing Kerberos (Installation de Kerberos)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7 - Windows Integration Guide (Red Hat Enterprise Linux 7 - Guide d’intégration à Windows)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
