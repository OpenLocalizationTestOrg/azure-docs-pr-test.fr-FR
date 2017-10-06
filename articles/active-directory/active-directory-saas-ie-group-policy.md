---
title: "aaaDeploy Extension volet d’accès Azure pour Internet Explorer à l’aide d’un objet de stratégie de groupe | Documents Microsoft"
description: "Comment toouse groupe module complémentaire stratégie toodeploy hello Internet Explorer pour le portail de mes applications hello."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a>Comment tooDeploy hello Extension volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe
Ce didacticiel montre comment tooremotely de stratégie de groupe toouse installer extension du volet d’accès hello pour Internet Explorer sur les ordinateurs de vos utilisateurs. Cette extension est nécessaire pour les utilisateurs d’Internet Explorer qui ont besoin de toosign dans des applications qui sont configurées à l’aide de [mot de passe l’authentification unique sur](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

Il est recommandé qu’admins automatiser le déploiement de hello de cette extension. Sinon, les utilisateurs ont toodownload et extension de hello s’installent, qui est toouser susceptible d’engendrer des erreurs et nécessite des autorisations d’administrateur. Ce didacticiel présente une méthode d’automatisation des déploiements de logiciels à l’aide d’une stratégie de groupe. [En savoir plus sur la stratégie de groupe.](https://technet.microsoft.com/windowsserver/bb310732.aspx)

Hello extension du volet d’accès est également disponible pour [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) et [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), qui ne requièrent tooinstall d’autorisations administrateur.

## <a name="prerequisites"></a>Composants requis
* Vous avez configuré [les Services de domaine Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), et vous avez joint le domaine de tooyour ordinateurs de vos utilisateurs.
* Vous devez avoir hello hello « Modifier les paramètres » autorisation tooedit objet de stratégie de groupe (GPO). Par défaut, les membres de hello les groupes de sécurité suivants ont cette autorisation : les administrateurs de domaine, les administrateurs d’entreprise et les propriétaires créateurs de la stratégie de groupe. [En savoir plus.](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a>Étape 1 : Créer le Point de Distribution hello
Tout d’abord, vous devez placer le package de programme d’installation hello sur un emplacement réseau accessible par les ordinateurs de hello que vous souhaitez installer tooremotely une extension hello sur. toodo, procédez comme suit :

1. Ouvrez une session sur le serveur de toohello en tant qu’administrateur
2. Bonjour **le Gestionnaire de serveur** fenêtre, accédez trop**fichiers et Services de stockage**.
   
    ![Ouvrir Services de fichiers et de stockage](./media/active-directory-saas-ie-group-policy/files-services.png)
3. Accédez toohello **partages** onglet. Ensuite, cliquez sur **Tâches** > **Nouveau partage...**
   
    ![Ouvrir Services de fichiers et de stockage](./media/active-directory-saas-ie-group-policy/shares.png)
4. Hello complète **Assistant Nouveau partage** et le jeu d’autorisations tooensure est qu’il est accessible à partir des ordinateurs de vos utilisateurs. [En savoir plus sur les partages.](https://technet.microsoft.com/library/cc753175.aspx)
5. Télécharger hello suivant le package Microsoft Windows Installer (fichier .msi) : [Extension.msi de panneau d’accès](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)
6. Copie hello installer package tooa souhaité emplacement sur le partage de hello.
   
    ![Hello .msi toohello partage de fichiers.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. Vérifiez que vos ordinateurs client sont tooaccess en mesure de package de programme d’installation hello à partir du partage de hello. 

## <a name="step-2-create-hello-group-policy-object"></a>Étape 2 : Créer hello objet stratégie de groupe
1. Ouvrez une session sur le serveur toohello qui héberge votre installation de Services de domaine Active Directory (AD DS).
2. Dans le Gestionnaire de serveur de hello, accédez trop**outils** > **gestion des stratégies de groupe**.
   
    ![Accédez tooTools > Gestion de stratégie de groupe](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. Dans le volet gauche de hello Hello **gestion des stratégies de groupe** fenêtre, affichage de votre hiérarchie de l’unité d’organisation (UO) et déterminer à l’étendue vous souhaitez que la stratégie de groupe tooapply hello. Par exemple, vous pouvez décider que quelques utilisateurs toopick un tooa de toodeploy petite unité d’organisation de test, ou risque de choisir une unité d’organisation toodeploy tooyour ensemble organisation de niveau supérieur.
   
   > [!NOTE]
   > Si vous souhaitez toocreate ou modifier vos unités d’organisation (UO), basculez arrière toohello le Gestionnaire de serveur et accédez trop**outils** > **Active Directory Users and Computers**.
   > 
   > 
4. Une fois que vous avez sélectionné une UO, cliquez dessus avec le bouton droit et sélectionnez **Créer un objet GPO dans ce domaine, et le lier ici...**
   
    ![Créer un objet GPO](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. Bonjour **nouvel objet GPO** invite de commandes, tapez un nom pour hello nouvel objet de stratégie de groupe.
   
    ![Nom hello nouvel objet GPO](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. Avec le bouton hello objet de stratégie de groupe que vous avez créé, sélectionnez **modifier**.
   
    ![Modifier le nouvel objet GPO de hello](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a>Étape 3 : Assigner hello Package d’Installation
1. Déterminer si vous souhaitez qu’extension de hello toodeploy basée sur **Configuration ordinateur** ou **Configuration utilisateur**. Lorsque vous utilisez [configuration ordinateur](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), extension de hello est installée sur l’ordinateur hello quels que soient les utilisateurs ouvrent une session tooit. Avec [configuration utilisateur](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), les utilisateurs ont l’extension hello installée pour eux, quelle que soit la quels ordinateurs ils ouvrent une session sur.
2. Dans le volet gauche de hello Hello **éditeur de gestion de stratégie de groupe** fenêtre, accédez tooeither Hello suivant des chemins d’accès du dossier, selon le type de configuration choisie :
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. Cliquez avec le bouton droit sur **Installation de logiciel**, puis sélectionnez **Nouveau** > **Package...**
   
    ![Créer un package d’installation de logiciel](./media/active-directory-saas-ie-group-policy/new-package.png)
4. Accédez toohello dossier partagé qui contient le package du programme d’installation hello de [étape 1 : créer un Point de Distribution hello](#step-1-create-the-distribution-point), sélectionnez le fichier .msi de hello, puis cliquez sur **ouvrir**.
   
   > [!IMPORTANT]
   > Si le partage de hello se trouve sur le même serveur, vérifiez que vous accédez à hello .msi via le chemin d’accès au fichier hello réseau, plutôt que de chemin d’accès du fichier local hello.
   > 
   > 
   
    ![Sélectionnez le package d’installation Bonjour à partir du dossier partagé hello.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. Bonjour **déploiement du logiciel** invite, sélectionnez **affecté** pour votre méthode de déploiement. Cliquez ensuite sur **OK**.
   
    ![Sélectionnez Affecté, puis cliquez sur OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

Hello extension est désormais déployé toohello unité d’organisation que vous avez sélectionné. [En savoir plus sur l’installation des logiciels de la stratégie de groupe.](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a>Étape 4 : Hello d’activation automatique Extension pour Internet Explorer
En outre les programme d’installation toorunning hello, toutes les extensions pour Internet Explorer doit être activée explicitement avant de pouvoir être utilisé. Suivez les étapes ci-dessous tooenable hello hello Extension volet d’accès à l’aide de la stratégie de groupe :

1. Bonjour **éditeur de gestion de stratégie de groupe** fenêtre, accédez tooeither Hello suivant des chemins d’accès, selon le type de configuration que vous avez choisi dans [étape 3 : assigner hello Package d’Installation](#step-3-assign-the-installation-package):
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. Cliquez avec le bouton droit sur **Liste des modules complémentaires**, puis sélectionnez **Modifier**.
    ![Modifiez la liste des modules complémentaires.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)
3. Bonjour **liste des modules complémentaires** fenêtre, sélectionnez **activé**. Ensuite, sous hello **Options** , cliquez sur **afficher... **.
   
    ![Cliquez sur Activer, puis sur Afficher...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. Bonjour **afficher le contenu** fenêtre, effectuez hello comme suit :
   
   1. Pour la première colonne de hello (hello **nom de la valeur** champ), copier et coller hello ID de classe suivant :`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`
   2. Pour la deuxième colonne de hello (hello **valeur** champ), type Bonjour valeur suivante :`1`
   3. Cliquez sur **OK** tooclose hello **afficher le contenu** fenêtre.
      
      ![Renseignez les valeurs hello comme indiqué ci-dessus.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. Cliquez sur **OK** tooapply vos modifications et les fermer hello **liste des modules complémentaires** fenêtre.

Hello extension doit maintenant être activée pour les ordinateurs hello Bonjour sélectionné unité d’organisation. [En savoir plus sur l’utilisation de tooenable de stratégie de groupe ou de désactiver les modules complémentaires d’Internet Explorer.](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a>Étape 5 (Facultatif) : Désactiver l’invite « Mémoriser le mot de passe »
Lorsque peut d’Internet Explorer toowebsites utilisateurs connectez-vous à l’aide de hello Extension volet d’accès, le message suivant de hello afficher vous demander « Voulez-vous toostore votre mot de passe ? »

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

Si vous le souhaitez tooprevent vos utilisateurs de voir cette invite, puis procédez hello ci-dessous tooprevent semi-automatique de mémoriser des mots de passe :

1. Bonjour **éditeur de gestion de stratégie de groupe** fenêtre, le chemin d’accès toohello accédez répertoriées ci-dessous. Ce paramètre de configuration n’est disponible que sous **Configuration utilisateur**.
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. Recherchez le paramètre hello nommé **activer la fonctionnalité de saisie semi-automatique hello pour les noms d’utilisateur et mots de passe sur les formulaires de**.
   
   > [!NOTE]
   > Les versions précédentes d’Active Directory peuvent répertorier ce paramètre avec le nom de hello **n’autorisent pas les mots de passe toosave de saisie semi-automatique**. configuration Hello pour ce paramètre est différente de hello paramètre décrit dans ce didacticiel.
   > 
   > 
   
    ![N’oubliez pas toolook pour ce sous Paramètres utilisateur.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. Cliquez avec le bouton droit sur hello au-dessus de paramètre, puis sélectionnez **modifier**.
4. Dans la fenêtre hello intitulée **activer la fonctionnalité de saisie semi-automatique hello pour les noms d’utilisateur et mots de passe sur les formulaires de**, sélectionnez **désactivé**.
   
    ![Sélectionner Désactiver](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. Cliquez sur **OK** tooapply ces modifications et une fenêtre hello fermer.

Les utilisateurs ne sont plus être en mesure de toostore leurs informations d’identification ou utiliser informations d’identification tooaccess semi-automatique précédemment stocké. Toutefois, cette stratégie autorise les utilisateurs toocontinue toouse saisie semi-automatique pour les autres types de champs de formulaire, tels que les champs de recherche.

> [!WARNING]
> Si cette stratégie est activée une fois que les utilisateurs ont choisi toostore certaines informations d’identification, cette stratégie sera *pas* effacer les informations d’identification hello qui ont déjà été stockées.
> 
> 

## <a name="step-6-testing-hello-deployment"></a>Étape 6 : Test hello déploiement
Suivez les étapes de hello ci-dessous tooverify si le déploiement d’une extension hello a réussi :

1. Si vous avez déployé à l’aide de **Configuration ordinateur**, l’authentification sur un ordinateur client appartenant toohello unité d’organisation que vous avez sélectionné dans [étape 2 : créer hello objet stratégie de groupe](#step-2-create-the-group-policy-object). Si vous avez déployé à l’aide de **Configuration utilisateur**, assurez-vous que toosign dans en tant qu’utilisateur appartient toothat unité d’organisation.
2. Il peut prendre quelques signe ins pour la stratégie de groupe hello modifie la mise à jour toofully avec cet ordinateur. tooforce hello mise à jour, ouvrez un **invite de commandes** fenêtre et exécution hello commande suivante :`gpupdate /force`
3. Vous devez redémarrer l’ordinateur hello pour cet emplacement de tootake installation hello. Démarrage peut prendre beaucoup plus de temps installe habituel lors de l’extension de hello.
4. Après avoir redémarré, ouvrez **Internet Explorer**. Dans hello haut à droite de la fenêtre hello, cliquez sur **outils** (icône d’engrenage hello), puis sélectionnez **gérer les modules complémentaires**.
   
    ![Accédez tooTools > Gérer les modules complémentaires](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. Bonjour **gérer les modules complémentaires** fenêtre, vérifiez que hello **Extension volet d’accès** a été installé et que ses **état** a été défini trop**activé**.
   
    ![Vérifiez que hello Extension volet d’accès est installée et activée.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a>Articles connexes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Accès aux applications et authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Résolution des problèmes de hello Extension volet d’accès pour Internet Explorer](active-directory-saas-ie-troubleshooting.md)

