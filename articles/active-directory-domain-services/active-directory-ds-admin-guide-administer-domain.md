---
title: "Version préliminaire des services de domaine Azure Active Directory : administrer un domaine géré | Microsoft Docs"
description: "Administrer les domaines gérés par les services de domaine Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a>Administrer un domaine géré par les services de domaine Azure Active Directory
Cet article explique comment tooadminister un Services de domaine Azure Active Directory (AD) géré le domaine.

## <a name="before-you-begin"></a>Avant de commencer
tâches de hello tooperform répertoriées dans cet article, vous devez :

1. Un **abonnement Azure**valide.
2. Un **répertoire Azure AD** , synchronisé avec un répertoire local ou un répertoire cloud uniquement.
3. **Les Services de domaine Active Directory Azure** doit être activée pour le répertoire de hello Azure AD. Si vous n’avez pas encore fait, suivez toutes les tâches de hello présentées dans hello [guide Mise en route](active-directory-ds-getting-started.md).
4. A **appartenant à un domaine un ordinateur virtuel** à partir de laquelle vous administrez hello domaine géré des Services de domaine Active Directory de Azure. Si vous n’avez pas cet un ordinateur virtuel, suivez toutes les tâches hello décrites dans l’article hello intitulé [joindre un domaine géré du tooa d’ordinateur virtuel Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Vous avez besoin des informations d’identification hello d’un **le groupe 'Administrateurs du contrôleur de domaine AAD' toohello utilisateur compte appartenant** dans votre annuaire, tooadminister votre domaine géré.

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a>Tâches d’administration pouvant être effectuées sur un domaine géré
Les membres du groupe « Administrateurs de contrôleur de domaine AAD » de hello ont des privilèges sur le domaine géré de hello qui leur permettent de tooperform tâches telles que :

* Joindre un domaine géré toohello de machines.
* Configurer hello des GPO intégrés pour les conteneurs de « Ordinateurs AADDC » et « Utilisateurs AADDC » hello domaine géré de hello.
* Gérer DNS sur un domaine géré de hello.
* Créer et administrer personnalisé unités d’organisation (UO) sur un domaine géré de hello.
* Gain d’un accès administratif toocomputers joints à un domaine géré de toohello.

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a>Privilèges d’administrateur dont vous ne disposez pas concernant un domaine géré
domaine de Hello est géré par Microsoft, y compris les activités telles que la mise à jour corrective, analyse et, pour effectuer des sauvegardes. Par conséquent, domaine de hello est verrouillé et que vous n’avez pas des privilèges tooperform certaines tâches administratives sur le domaine de hello. Voici quelques exemples de tâches que vous ne pouvez pas exécuter.

* Vous disposez pas des privilèges d’administrateur de domaine ou administrateur d’entreprise pour le domaine géré de hello.
* Vous ne pouvez pas étendre le schéma hello domaine géré de hello.
* Vous ne pouvez pas vous connecter toodomain contrôleurs hello gérés à l’aide du Bureau à distance.
* Impossible d’ajouter des contrôleurs de domaine toohello domaine géré.

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a>Tâche 1 : configurer un tooremotely joint au domaine d’un ordinateur virtuel Windows Server administrer le domaine géré de hello
Domaines gérés des Services de domaine Active Directory Azure peuvent être gérés à l’aide des outils d’administration Active Directory familiers tels que hello Active Directory Administrative Center (ADAC) ou Active Directory PowerShell. Les administrateurs clients ne disposent pas de contrôleurs de privilèges tooconnect toodomain sur hello le domaine géré via le Bureau à distance. Par conséquent, les membres de groupe « Administrateurs de contrôleur de domaine AAD » peut administrer de hello gérée domaines à distance à l’aide des outils d’administration Active Directory à partir d’un ordinateur client Windows Server qui est le domaine géré de toohello jointes. Les outils d’administration Active Directory peuvent être installés comme partie d’une fonctionnalité facultative de hello outils d’Administration de serveur distant (RSAT) sur les ordinateurs serveur et client Windows joints à un domaine de toohello géré.

première étape de Hello est tooset une machine virtuelle Windows Server qui est jointe toohello géré domaine. Pour obtenir des instructions, consultez l’article toohello intitulé [joindre un domaine des Services de domaine Active Directory de Azure géré tooan de machine virtuelle Windows Server](active-directory-ds-admin-guide-join-windows-vm.md).

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a>Administrer à distance le domaine géré de hello à partir d’un ordinateur client (par exemple, Windows 10)
instructions Hello dans cet article utilisent un hello de tooadminister de l’ordinateur virtuel Windows Server AAD-DS géré de domaine. Toutefois, vous pouvez également choisir toouse un toodo de machine virtuelle Windows client (par exemple, Windows 10) donc.

Vous pouvez [installer les outils d’Administration de serveur distant (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) sur un ordinateur Windows client virtuel en suivant les instructions de hello sur TechNet.

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a>Tâche 2 - Outils d’administration Active Directory d’installation sur l’ordinateur virtuel de hello
Effectuer hello suivant des outils d’Administration Active Directory étapes tooinstall hello sur l’ordinateur virtuel de joints à un domaine hello. Pour en savoir plus sur [l’installation et l’utilisation des Outils d’administration de serveur distant](https://technet.microsoft.com/library/hh831501.aspx), voir TechNet.

1. Accédez trop**virtuels** nœud Bonjour portail Azure classic. Sélectionnez l’ordinateur virtuel de hello vous avez créé dans la tâche 1, cliquez sur **Connect** sur la barre de commandes hello bas hello de fenêtre hello.

    ![Connecter l’ordinateur virtuel de tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portail classique de Hello vous invite tooopen ou enregistrer un fichier avec l’extension '.rdp', qui est utilisé tooconnect toohello virtual machine. Cliquez sur fichier de hello tooopen lorsqu’il a terminé le téléchargement.
3. À l’invite de connexion hello, utilisez des références de hello d’un utilisateur appartenant groupe 'Administrateurs du contrôleur de domaine AAD' de toohello. Par exemple, nous utilisons 'bob@domainservicespreview.onmicrosoft.com' dans le cas présent.
4. À partir de l’écran d’accueil hello, ouvrez **le Gestionnaire de serveur**. Cliquez sur **Ajout de rôles et fonctionnalités** dans le volet central de hello de la fenêtre du Gestionnaire de serveur hello.

    ![Lancer le gestionnaire de serveur sur la machine virtuelle](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. Sur hello **avant de commencer** page Hello **Assistant Ajouter des rôles et fonctionnalités**, cliquez sur **suivant**.

    ![Page Avant de commencer](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. Sur hello **le Type d’Installation** page, laissez l’option hello **installation basée sur un rôle ou une fonctionnalité** activée, puis cliquez sur **suivant**.

    ![Page Type d’installation](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. Sur hello **sélection du serveur** page, sélectionnez l’ordinateur virtuel en cours de hello hello pool de serveurs, puis cliquez sur **suivant**.

    ![Page Sélection du serveur](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. Sur hello **rôles serveur** , cliquez sur **suivant**. Nous permet d’ignorer cette page, car nous ne sommes pas installer les rôles sur le serveur de hello.
9. Sur hello **fonctionnalités** , cliquez sur tooexpand hello **outils d’Administration de serveur distant** nœud puis cliquez sur tooexpand hello **outils d’Administration de rôles** nœud. Sélectionnez **outils AD DS et AD LDS** fonctionnalité à partir de la liste de hello des outils d’administration de rôles.

    ![Page Fonctionnalités](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. Sur hello **Confirmation** , cliquez sur **installer** tooinstall hello AD et les outils AD LDS fonctionnalité sur l’ordinateur virtuel de hello. Lorsque la fonctionnalité installation terminée, cliquez sur **fermer** tooexit hello **Ajout de rôles et fonctionnalités** Assistant.

    ![Page Confirmation](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a>Tâche 3 : connecter tooand Explorer hello les domaines gérés
Maintenant que les outils d’administration hello Active Directory sont installés sur hello domaine joints à un ordinateur virtuel, nous pouvons utiliser tooexplore de ces outils et administrer le domaine géré de hello.

> [!NOTE]
> Vous devez toobe un membre du groupe « Administrateurs de contrôleur de domaine AAD » de hello, tooadminister hello géré de domaine.
>
>

1. À partir de l’écran d’accueil hello, cliquez sur **outils d’administration**. Vous devez voir les outils d’administration hello AD installés sur l’ordinateur virtuel de hello.

    ![Outils d’administration installés sur le serveur](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Cliquez sur **Centre d’administration Active Directory**.

    ![Centre d'administration Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. domaine de hello tooexplore, cliquez sur le nom de domaine hello dans le volet de gauche hello (par exemple, « contoso100.com »). Vous pouvez remarquer deux conteneurs appelés « Ordinateurs AADDC » et « Utilisateurs AADDC », respectivement.

    ![ADAC - Affichage du domaine](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. Cliquez sur le conteneur hello appelé **AADDC utilisateurs** toosee tous les utilisateurs et les groupes qui appartiennent toohello gérés domaine. Les comptes d’utilisateur et groupes de votre client Azure AD doivent apparaître dans ce conteneur. Notez que dans cet exemple, un compte d’utilisateur pour l’utilisateur hello appelé « bob » et le groupe « Administrateurs de contrôleur de domaine AAD » sont disponibles dans ce conteneur.

    ![ADAC - Utilisateurs du domaine](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. Cliquez sur le conteneur hello appelé **AADDC ordinateurs** les ordinateurs hello toosee joints à un domaine géré de toothis. Vous devez voir une entrée pour la machine virtuelle en cours de hello, qui est toohello joint à un domaine. Comptes d’ordinateur pour tous les ordinateurs qui sont joint toohello domaine géré sont stockées dans ce conteneur « Ordinateurs AADDC » des Services de domaine Azure AD.

    ![ADAC - Ordinateurs joints au domaine](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a>Contenu connexe
* [Services de domaine Azure AD : guide de prise en main](active-directory-ds-getting-started.md)
* [Joindre un domaine des Services de domaine Active Directory de Azure géré tooan de machine virtuelle Windows Server](active-directory-ds-admin-guide-join-windows-vm.md)
* [Déployer les Outils d’administration de serveur distant](https://technet.microsoft.com/library/hh831501.aspx)
