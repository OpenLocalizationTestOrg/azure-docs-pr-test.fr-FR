---
title: "Gestionnaire d’instantanés StorSimple d’aaaDeploy | Documents Microsoft"
description: "Découvrez comment toodownload et installez hello Gestionnaire d’instantanés StorSimple, un composant logiciel enfichable MMC pour la gestion des fonctionnalités de protection et la sauvegarde de données de StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a>Déployer hello enfichable MMC du Gestionnaire d’instantanés StorSimple

## <a name="overview"></a>Vue d'ensemble
Hello StorSimple Snapshot Manager est un composant logiciel enfichable Microsoft Management Console (MMC) qui simplifie la protection des données et gestion de sauvegarde dans un environnement Microsoft Azure StorSimple. Avec le Gestionnaire d’instantanés StorSimple, vous pouvez gérer le stockage Microsoft Azure StorSimple local et dans le cloud comme s’il s’agissait d’un système de stockage entièrement intégré, ce qui simplifie les processus de sauvegarde et de restauration et contribue à réduire les coûts. 

Ce didacticiel décrit la configuration requise, ainsi que les procédures d’installation, de suppression et de mise à niveau du Gestionnaire d’instantanés StorSimple.

> [!NOTE]
> * Vous ne pouvez pas utiliser le Gestionnaire d’instantanés StorSimple toomanage Microsoft Azure StorSimple tableaux virtuels (également appelé StorSimple local périphériques virtuels).
> * Si vous envisagez tooinstall 2 de mise à jour StorSimple sur votre appareil StorSimple, que toodownload hello version la plus récente du Gestionnaire d’instantanés StorSimple et l’installer **avant d’installer StorSimple mise à jour 2**. version la plus récente de StorSimple Snapshot Manager Hello est à compatibilité descendante et fonctionne avec les versions de Microsoft Azure StorSimple. Si vous utilisez une version précédente de hello du Gestionnaire d’instantanés StorSimple, vous devez tooupdate informatique (il est inutile version précédente de hello toouninstall avant d’installer de la nouvelle version de hello).


## <a name="storsimple-snapshot-manager-installation"></a>Installation du Gestionnaire d’instantanés StorSimple
Gestionnaire d’instantanés StorSimple peut être installé sur les ordinateurs qui exécutent le système de d’exploitation Windows Server 2008 R2 SP1, Windows Server 2012 ou Windows Server 2012 R2 hello. Sur les serveurs exécutant Windows 2008 R2, vous devez aussi installer Windows Server 2008 SP1 et Windows Management Framework 3.0.

Avant d’installer ou mettre à niveau hello StorSimple Snapshot Manager-composant logiciel enfichable pour hello Microsoft Management Console (MMC), vérifiez que cet appareil de Microsoft Azure StorSimple hello et serveur hôte sont configurés correctement.

## <a name="configure-prerequisites"></a>Configuration préalable requise
Hello étapes suivantes fournissent une vue d’ensemble des tâches de configuration que vous devez effectuer avant d’installer hello Gestionnaire d’instantanés StorSimple. Pour obtenir des informations complètes sur la configuration et l’installation de Microsoft Azure StorSimple, y compris la configuration système requise et des instructions pas à pas, consultez la page [Déploiement de votre appareil StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).

> [!IMPORTANT]
> Avant de commencer, passez en revue hello [liste de vérification de configuration déploiement](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) et et [conditions préalables au déploiement](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) dans [déployer l’appareil StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a>Avant d’installer le Gestionnaire d’instantanés StorSimple
1. Décompressez, montez et connectez le dispositif de Microsoft Azure StorSimple hello comme décrit dans [installer votre appareil StorSimple 8100](storsimple-8100-hardware-installation.md) ou [installer votre appareil StorSimple 8600](storsimple-8600-hardware-installation.md).
2. Assurez-vous que votre ordinateur hôte exécute l’un des hello suivant des systèmes d’exploitation :
   
   * Windows Server 2008 R2 (sur les serveurs exécutant Windows 2008 R2, vous devez aussi installer Windows Server 2008 SP1 et Windows Management Framework 3.0)
   * Windows Server 2012
   * Windows Server 2012 R2
     
     Pour un périphérique virtuel StorSimple, hôte de hello doit être un ordinateur virtuel de Microsoft Azure.
3. Assurez-vous que vous remplissez toutes les exigences de configuration de Microsoft Azure StorSimple hello. Pour plus d’informations, consultez trop[conditions préalables au déploiement](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).
4. Connecter l’hôte de toohello périphérique hello et effectuer la configuration initiale de hello. Pour plus d’informations, consultez trop[les étapes de déploiement](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).
5. Créer des volumes sur l’appareil de hello, affectez-les toohello hôte et vérifiez que cet hôte hello peut monter et les utiliser. Gestionnaire d’instantanés StorSimple hello de prend en charge les types de volumes suivants :
   
   * Volumes de base
   * Volumes simples
   * Volumes dynamiques
   * Volumes dynamiques en miroir (RAID 1)
   * Volumes partagés de cluster
     
     Pour plus d’informations sur la création de volumes sur l’appareil StorSimple hello ou un appareil virtuel StorSimple, accédez trop[étape 6 : création d’un volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume), dans [déployer l’appareil StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).

## <a name="install-a-new-storsimple-snapshot-manager"></a>Installation d’un nouveau Gestionnaire d’instantanés StorSimple
Avant d’installer le Gestionnaire d’instantanés StorSimple, assurez-vous que volumes hello vous avez créé sur l’appareil StorSimple hello ou un appareil virtuel StorSimple sont montés, initialisés et formatés comme indiqué dans [configurer les composants requis](#configure-prerequisites).

> [!IMPORTANT]
> * Pour un périphérique virtuel StorSimple, hôte de hello doit être un ordinateur virtuel de Microsoft Azure. 
> * hôte de Hello doit être en cours d’exécution pour Windows 2008 R2, Windows Server 2012 ou Windows Server 2012 R2. Si votre serveur exécute Windows Server 2008 R2, vous devez aussi installer Windows Server 2008 SP1 et Windows Management Framework 3.0.
> * Vous devez configurer une connexion iSCSI à partir de l’appareil StorSimple hello hôte toohello avant de pouvoir connecter hello appareil tooStorSimple Gestionnaire d’instantanés.

Suivez ces étapes de toocomplete une nouvelle installation du Gestionnaire d’instantanés StorSimple. Si vous installez une mise à niveau, passez trop[mise à niveau ou réinstaller le Gestionnaire d’instantanés StorSimple](#upgrade-or-reinstall-storsimple-snapshot-manager).

* Étape 1 : installation du Gestionnaire d’instantanés StorSimple 
* Étape 2 : Se connecter à StorSimple Snapshot Manager tooa périphérique 
* Étape 3 : Vérifier le périphérique de hello connexion toohello 

### <a name="step-1-install-storsimple-snapshot-manager"></a>Étape 1 : installation du Gestionnaire d’instantanés StorSimple
Utilisez hello suivant les étapes tooinstall Gestionnaire d’instantanés StorSimple.

#### <a name="tooinstall-storsimple-snapshot-manager"></a>tooinstall Gestionnaire d’instantanés StorSimple
1. Télécharger le logiciel de gestionnaire d’instantanés StorSimple hello (passez trop[StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) Bonjour Microsoft Download Center) et enregistrez-le en local sur l’ordinateur hôte de hello.
2. Dans l’Explorateur de fichiers, cliquez sur le dossier compressé de hello, puis cliquez sur **extraire tout**.
3. Bonjour **dossiers compressés (zippés)** fenêtre hello **sélectionner une destination et extraire les fichiers** , tapez ou recherchez chemin toohello où vous souhaitez toobe toofile extraite.
   
    > [!IMPORTANT]
    > Vous devez installer le Gestionnaire d’instantanés StorSimple sur hello lecteur C:.
    
4. Sélectionnez hello **afficher les fichiers lorsque vous avez terminé extraits** case à cocher, puis cliquez sur **extraire**.
   
    ![Boîte de dialogue Extraire les fichiers](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. Lors de l’extraction de hello est finie, le dossier de destination hello s’ouvre. Double-cliquez sur icône le programme d’installation de l’application hello qui apparaît dans le dossier de destination hello.
6. Hello lorsque **installation réussie** message s’affiche, cliquez sur **fermer**. Vous devez voir l’icône du Gestionnaire d’instantanés StorSimple hello sur votre bureau.
   
    ![Icône du Bureau](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a>Étape 2 : Se connecter à StorSimple Snapshot Manager tooa périphérique
Utilisez hello suivant les étapes tooconnect appareil StorSimple Snapshot Manager tooa StorSimple.

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a>tooconnect tooa de gestionnaire d’instantanés StorSimple périphérique
1. Cliquez sur icône du Gestionnaire d’instantanés StorSimple hello sur votre bureau. fenêtre du Gestionnaire d’instantanés StorSimple Hello s’affiche. fenêtre Hello contient un **étendue** volet, un **résultats** volet et un **Actions** volet. 
   
    ![Interface utilisateur du gestionnaire d’instantanés StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * Hello **étendue** (volet hello gauche) contient une liste de nœuds organisés dans une structure arborescente. Vous pouvez développer certains nœuds tooselect une vue ou un nœud toothat connexes de données spécifique. Cliquez sur hello flèche icône tooexpand ou réduire un nœud. Cliquez sur un élément Bonjour **étendue** volet toosee une liste des actions disponibles pour cet élément.
   * Hello **résultats** volet (hello center) contient des informations d’état détaillées sur le nœud de hello, vue ou les données que vous avez sélectionné dans hello **étendue** volet.
   * Hello **Actions** volet répertorie les opérations hello que vous pouvez effectuer sur le nœud de hello, vue ou les données que vous avez sélectionné dans hello **étendue** volet.
     
     Pour obtenir une description complète de l’interface utilisateur de gestionnaire d’instantanés StorSimple hello, consultez [interface utilisateur de gestionnaire d’instantanés StorSimple](storsimple-use-snapshot-manager.md).
2. Bonjour **étendue** volet, avec le bouton hello **périphériques** nœud, puis cliquez sur **configurer un appareil**. Hello **configurer un appareil** boîte de dialogue s’affiche.
   
    ![Configurer un appareil](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. Bonjour **périphérique** liste boîte, adresse IP de hello select de l’appareil de Microsoft Azure StorSimple hello ou un périphérique virtuel. Bonjour **mot de passe** zone de texte, de type hello Gestionnaire d’instantanés StorSimple un mot de passe que vous avez créé pour appareil de hello en hello portail Azure. Cliquez sur **OK**.
4. Gestionnaire d’instantanés StorSimple recherche le périphérique hello que vous avez identifié. Si l’appareil de hello est disponible, le Gestionnaire d’instantanés StorSimple ajoute une connexion. Vous pouvez [Vérifiez hello connexion toohello périphérique](#to-verify-the-connection) tooconfirm qui hello connexion a été ajouté avec succès.
   
    Si l’appareil de hello est indisponible pour une raison quelconque, le Gestionnaire d’instantanés StorSimple retourne un message d’erreur. Cliquez sur **OK** tooclose hello du message d’erreur, puis cliquez sur **Annuler** tooclose hello **configurer un appareil** boîte de dialogue.
5. Lorsqu’il connecte les appareils tooa, gestionnaire d’instantanés StorSimple importe chaque groupe de volumes configuré pour ce périphérique, condition que hello groupe de volumes dispose des sauvegardes associées. Les groupes de volumes qui ne sont associés à aucune sauvegarde ne sont pas importés. De plus, les stratégies de sauvegarde créées pour un groupe de volumes ne sont pas importées. toosee hello groupes importés, avec le bouton droit supérieur hello **groupes de volumes** nœud Bonjour **étendue** volet, puis cliquez sur **activer/désactiver les groupes importés**.

### <a name="step-3-verify-hello-connection-toohello-device"></a>Étape 3 : Vérifier le périphérique de hello connexion toohello
Utilisez hello suivant tooverify étapes que le Gestionnaire d’instantanés StorSimple est toohello connecté l’appareil StorSimple.

#### <a name="tooverify-hello-connection"></a>connexion de hello tooverify
1. Bonjour **étendue** volet, cliquez sur hello **périphériques** nœud.
   
    ![État de l’appareil dans le Gestionnaire d’instantanés StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. Vérifiez hello **résultats** volet : 
   
   * Si un indicateur vert apparaît sur l’icône de périphérique hello et **disponible** s’affiche dans hello **état** colonne, puis appareil de hello est connecté. 
   * Si un indicateur rouge apparaît sur l’icône de périphérique hello et non disponible apparaît dans hello **état** colonne, puis appareil de hello n’est pas connecté. 
   * Si **actualisation** s’affiche dans hello **état** colonne, puis sur Gestionnaire d’instantanés StorSimple est la récupération des groupes de volumes et les sauvegardes associées pour un appareil connecté.

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a>Mise à niveau ou réinstallation du Gestionnaire d’instantanés StorSimple
Vous devez désinstaller le Gestionnaire d’instantanés StorSimple complètement avant de mettre à niveau ou réinstaller le logiciel de hello. 

Avant de réinstaller le Gestionnaire d’instantanés StorSimple, sauvegardez hello Gestionnaire d’instantanés StorSimple base de données existante sur l’ordinateur hôte hello. Il enregistre les informations de configuration et les stratégies de sauvegarde hello afin que vous pouvez facilement restaurer ces données à partir de la sauvegarde.

Pour mettre à niveau ou réinstaller le Gestionnaire d’instantanés StorSimple, suivez ces étapes :

* Étape 1 : désinstallation du Gestionnaire d’instantanés StorSimple 
* Étape 2 : Sauvegarder la base de données du Gestionnaire d’instantanés StorSimple hello 
* Étape 3 : Réinstallez le Gestionnaire d’instantanés StorSimple et restaurez la base de données hello 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a>Étape 1 : désinstallation du Gestionnaire d’instantanés StorSimple
Utilisez hello suivant les étapes toouninstall Gestionnaire d’instantanés StorSimple.

#### <a name="toouninstall-storsimple-snapshot-manager"></a>toouninstall Gestionnaire d’instantanés StorSimple
1. Sur l’ordinateur hôte hello, ouvrez hello **le panneau de configuration**, cliquez sur **programmes**, puis cliquez sur **programmes et fonctionnalités**.
2. Dans le volet gauche de hello, cliquez sur **désinstaller ou modifier un programme**.
3. Cliquez avec le bouton droit sur **Gestionnaire d’instantanés StorSimple**, puis cliquez sur **Désinstaller**.
4. Cette commande démarre hello programme d’installation du Gestionnaire d’instantanés StorSimple. Cliquez sur **Modifier l’installation**, puis sur **Désinstaller**.
   
   > [!NOTE]
   > S’il existe des processus MMC en cours d’exécution en arrière-plan de hello, telles que le Gestionnaire d’instantanés StorSimple ou la gestion des disques, hello désinstallation échoue et vous recevez un message tooclose toutes les instances de MMC avant de tentent de programme de hello toouninstall. Sélectionnez **automatiquement fermer les applications et essayez de toorestart une fois le programme d’installation terminer**, puis cliquez sur **OK**.
   > 
   > 
5. Lors de la désinstallation de hello est terminée, un **installation réussie** message s’affiche. Cliquez sur **Fermer**.

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a>Étape 2 : Sauvegarder la base de données du Gestionnaire d’instantanés StorSimple hello
Utilisez hello suivant les étapes toocreate et enregistrer une copie de base de données du Gestionnaire d’instantanés StorSimple hello.

#### <a name="tooback-up-hello-database"></a>tooback base de données hello
1. Arrêter hello Service de gestion StorSimple de Microsoft :
   
   1. Démarrez le Gestionnaire de serveur.
   2. Sur hello du tableau de bord Gestionnaire de serveur, sur hello **outils** menu, sélectionnez **Services**.
   3. Sur hello **Services** page, sélectionnez **Microsoft StorSimple Management Service**.
   4. Bonjour avec le bouton droit volet, sous **Microsoft StorSimple Management Service**, cliquez sur **arrêter le service de hello**.
      
        ![Arrêter le service du Gestionnaire de périphériques StorSimple hello](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. Parcourir tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData est un dossier masqué.
  
3. Rechercher le fichier XML de catalogue hello, copier le fichier hello et stocker hello copier dans un emplacement sûr ou dans le cloud de hello.
   
    ![Fichier de catalogue de sauvegarde StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. Redémarrez hello Service de gestion StorSimple de Microsoft : 
   
   1. Sur hello du tableau de bord Gestionnaire de serveur, sur hello **outils** menu, sélectionnez **Services**.
   2. Sur hello **Services** page, sélectionnez hello **Microsoft StorSimple Management service**e.
   3. Bonjour avec le bouton droit volet, sous **Microsoft StorSimple Management Service**, cliquez sur **redémarrer hello service**. 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a>Étape 3 : Réinstallez le Gestionnaire d’instantanés StorSimple et restaurez la base de données hello
tooreinstall Gestionnaire d’instantanés StorSimple, suivez les étapes de hello dans [installer un nouveau gestionnaire d’instantanés StorSimple](#install-a-new-storsimple-snapshot-manager). Ensuite, utilisez hello suivant de base de données du Gestionnaire d’instantanés StorSimple procédure toorestore hello.

#### <a name="toorestore-hello-database"></a>base de données toorestore hello
1. Arrêter hello Service de gestion StorSimple de Microsoft :
   
   1. Démarrez le Gestionnaire de serveur.
   2. Sur hello du tableau de bord Gestionnaire de serveur, sur hello **outils** menu, sélectionnez **Services**.
   3. Sur hello **Services** page, sélectionnez **Microsoft StorSimple Management Service**.
   4. Bonjour avec le bouton droit volet, sous **Microsoft StorSimple Management Service**, cliquez sur **arrêter le service de hello**.
2. Parcourir tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   
   > [!NOTE]
   > ProgramData est un dossier masqué.
   > 
   > 
3. Supprimer le fichier XML de catalogue hello et remplacez-le par version hello que vous avez enregistré précédemment.
4. Redémarrez hello Service de gestion StorSimple de Microsoft : 
   
   1. Sur hello du tableau de bord Gestionnaire de serveur, sur hello **outils** menu, sélectionnez **Services**.
   2. Sur hello **Services** page, sélectionnez **Microsoft StorSimple Management Service**.
   3. Bonjour avec le bouton droit volet, sous **Microsoft StorSimple Management Service**, cliquez sur **redémarrer hello service**.

## <a name="next-steps"></a>Étapes suivantes
* toolearn plus sur StorSimple Snapshot Manager, accédez trop[Nouveautés du Gestionnaire d’instantanés StorSimple ?](storsimple-what-is-snapshot-manager.md).
* toolearn savoir plus sur l’interface utilisateur de gestionnaire d’instantanés StorSimple hello, accédez trop[interface utilisateur de gestionnaire d’instantanés StorSimple](storsimple-use-snapshot-manager.md).
* toolearn plus sur l’utilisation de gestionnaire d’instantanés StorSimple, accédez trop[tooadminister de gestionnaire d’instantanés StorSimple utiliser votre solution StorSimple](storsimple-snapshot-manager-admin.md).

