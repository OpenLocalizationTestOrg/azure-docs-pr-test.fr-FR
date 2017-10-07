---
title: "interface utilisateur de gestionnaire d’instantanés aaaStorSimple | Documents Microsoft"
description: "Décrit l’interface utilisateur de gestionnaire d’instantanés StorSimple hello et explique comment toouse il toomanage les travaux de sauvegarde et hello catalogue de sauvegarde."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: c7d91892-2881-41a2-a7a2-908dc3646493
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.custom: 
ms.openlocfilehash: 865520fdaf1b559714b52b428ad136b084d65c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-user-interface-toomanage-backup-jobs-and-backup-catalog"></a>Travaux de sauvegarde utilisez StorSimple Snapshot Manager utilisateur interface toomanage et le catalogue de sauvegarde

## <a name="overview"></a>Vue d'ensemble
Hello Gestionnaire d’instantanés StorSimple a une interface utilisateur intuitive que vous pouvez utiliser tootake et gérer des sauvegardes. Ce didacticiel fournit une interface utilisateur de toohello introduction, puis explique comment toouse des composants de hello. Pour obtenir une description détaillée de hello Gestionnaire d’instantanés StorSimple, consultez [Nouveautés du Gestionnaire d’instantanés StorSimple ?](storsimple-what-is-snapshot-manager.md)

### <a name="console-description"></a>Description de la console
utilisateur de hello tooview l’interface, cliquez sur icône du Gestionnaire d’instantanés StorSimple hello sur votre bureau. fenêtre de console Hello s’affiche, comme indiqué dans hello après l’illustration.

![Volets du gestionnaire d’instantanés StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_gui_panes.png)

fenêtre de console Hello comporte cinq éléments principaux. Cliquez sur le lien approprié de hello pour une description complète de chaque élément.

* [Barre de menus](#menu-bar) 
* [Barre d’outils](#tool-bar) 
* [Volet Étendue](#scope-pane) 
* [Volet Résultats](#results-pane) 
* [Volet Actions](#actions-pane) 

En outre, les hello prend en charge du Gestionnaire d’instantanés StorSimple [navigation et un nombre de raccourcis de clavier](#keyboard-navigation-and-shortcuts).

### <a name="console-accessibility"></a>Accessibilité de la console
interface utilisateur de gestionnaire d’instantanés StorSimple Hello prend en charge les fonctionnalités d’accessibilité hello fournies par le système d’exploitation de Windows hello et hello Microsoft Management Console (MMC), ainsi que certains raccourcis clavier de gestionnaire d’instantanés StorSimple spécifiques. 

* Pour obtenir une description des fonctionnalités d’accessibilité Windows hello, accédez trop[raccourcis clavier pour Windows](https://support.microsoft.com/kb/126449). 
* Pour obtenir une description des fonctionnalités d’accessibilité hello MMC, accédez trop[accessibilité à MMC 3.0](https://technet.microsoft.com/library/cc766075.aspx)
* Pour obtenir une description des fonctionnalités d’accessibilité du Gestionnaire d’instantanés StorSimple hello, accédez trop[navigation et raccourcis de clavier](#keyboard-navigation-and-shortcuts).

## <a name="menu-bar"></a>Barre de menus
barre de menus Hello haut hello de fenêtre de console hello contient [fichier](#file-menu), [Action](#action-menu), [vue](#view-menu), [favoris](#favorites-menu), [fenêtre ](#window-menu), et [aide](#help-menu) menus.

Cliquez sur n’importe quel élément sur hello menu barre toosee une liste des commandes disponibles dans ce menu. exemple Hello présente hello **vue** menu sélectionné sur la barre de menus hello.

![Menu Affichage sélectionné](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png)

### <a name="file-menu"></a>Menu Fichier
Hello **fichier** menu contient des commandes standard de Microsoft Management Console (MMC).

#### <a name="menu-access"></a>Accès au menu
tooview hello **fichier** menu, cliquez sur **fichier** sur la barre de menus hello. Hello suivant menu s’affiche.

![Menu Fichier Gestionnaire d’instantanés StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_FileMenu.png) 

#### <a name="menu-description"></a>Description de menu
Hello tableau suivant décrit les éléments qui apparaissent sur hello **fichier** menu.

| Élément de menu | Description |
|:--- |:--- |
| Nouveau |Cliquez sur **nouveau** toocreate une nouvelle console basée sur hello Gestionnaire d’instantanés StorSimple. |
| Ouverts |Cliquez sur **ouvrir** tooopen une console existante. |
| Enregistrer |Cliquez sur **enregistrer** console en cours de toosave hello. |
| Enregistrer sous |Cliquez sur **enregistrer en tant que** toocreate une nouvelle instance de la console actuelle de hello renommée. Hello d’utilisation **Enregistrer sous** option toocustomize une vue et l’enregistrer pour une récupération ultérieure. Par exemple, vous pouvez créer des composants logiciels enfichables Gestionnaire d’instantanés StorSimple dont les serveurs toospecific de point. |
| Ajouter/Supprimer le composant logiciel enfichable |Cliquez sur **ajouter/supprimer un composant logiciel enfichable** tooadd ou supprimer des composants logiciel enfichables et tooorganize nœuds Bonjour **étendue** volet. Pour plus d’informations, consultez trop[ajouter, supprimer, organiser des composants logiciels enfichables et des Extensions dans MMC 3.0](https://technet.microsoft.com/library/cc722035.aspx). |
| Options |Cliquez sur **Options** toochange icône de la console hello, spécifier les autorisations et les modes d’accès utilisateur ou suppression de l’espace disque disponible de console fichiers tooincrease. |
| Liste des chemins d’accès |Cliquez sur un chemin d’accès dans hello numérotée liste tooreopen un fichier que vous avez récemment ouvert. |
| Quitter |Cliquez sur **Exit** tooclose hello **fichier** menu. |

### <a name="action-menu"></a>Menu Action
Hello d’utilisation **Action** tooselect menu Actions disponibles. tooyou de Hello éléments disponibles dépendent de la sélection hello dans hello **étendue** volet ou **résultats** volet.

#### <a name="menu-access"></a>Accès au menu
tooview hello **Action** menu, effectuez l’une des hello suivantes :

* Cliquez sur un élément Bonjour **étendue** volet ou **résultats** volet.
* Sélectionnez un élément dans hello **étendue** volet ou **résultats** volet, puis cliquez sur **Action** sur la barre de menus hello. 

Par exemple, si vous sélectionnez le nœud supérieur de hello Bonjour **étendue** volet, puis avec le bouton droit ou cliquez sur **Action** dans la barre de menus de hello, hello menu suivant s’affiche.

![Menu Action du Gestionnaire d’instantanés StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_Action_menu.png)

Hello **Actions** volet (hello à droite de la console de hello) contient hello même liste d’actions que hello **Action** menu. En outre, hello **Actions** volet contient hello **vue** les options de menu, qui vous permettent de toocreate une vue personnalisée des hello **résultats** volet.

![Volet Actions avec menu Affichage ouvert](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

#### <a name="menu-description"></a>Description de menu
Hello tableau suivant contient une liste alphabétique des actions du Gestionnaire d’instantanés StorSimple. 

* Hello **Action** colonne répertorie les actions que vous pouvez effectuer sur les nœuds et les résultats. 
* Hello **Navigation** colonne explique comment toodisplay hello approprié **Action** menu afin que vous pouvez sélectionner hello action. Certaines actions apparaissent dans plusieurs menus **Action** . Pour ces actions, sélectionnez une **Navigation** option à partir de la liste à puces de hello. 
* Hello **Description** colonne décrit comment toouse chaque action hello **Action** menu ou le volet Actions et explique ce qu’il fait.

> [!NOTE]
> Hello **Actions** volet et **Action** menus contiennent des options supplémentaires, tels que **vue**, **nouvelle fenêtre**,  **Actualiser**, **exporter la liste**, et **aide**. Ces options sont disponibles dans le cadre de hello MMC et ne sont pas spécifique tooStorSimple Gestionnaire d’instantanés. table de Hello inclut les descriptions de ces options.
> 
> 

| Action | Navigation | Description |
|:--- |:--- |:--- |
| Authentifier |Cliquez sur hello **périphériques** nœud et avec le bouton d’un appareil Bonjour **résultats** volet. |Cliquez sur **authentifier** tooenter hello mot de passe que vous avez configuré pour le périphérique de hello. |
| Cloner |Développez **catalogue de sauvegarde**, développez **instantanés Cloud**et cliquez sur une sauvegarde datée, puis sélectionnez un volume Bonjour **résultats** volet. |Cliquez sur **Clone** toocreate une copie d’un cloud d’instantané et le stocker dans un emplacement que vous désignez. |
| Configuration d’un appareil |Avec le bouton hello **périphériques** nœud. |Cliquez sur **configurer un appareil** tooconfigure un ou plusieurs périphériques tooconnect toohello Windows ordinateur hôte. |
| Créer la stratégie de sauvegarde |Effectuez l’une des manières suivantes les hello :<ul><li>Cliquez avec le bouton droit sur **Stratégies de sauvegarde**.</li><li>Cliquez sur ou développez **Groupes de volumes**, puis cliquez avec le bouton droit sur un groupe de volumes.</li><li>Cliquez sur ou développez **Catalogue de sauvegarde**, puis cliquez avec le bouton droit sur un groupe de volumes.</li></ul> |Cliquez sur **créer une stratégie de sauvegarde** tooconfigure une sauvegarde planifiée pour un groupe de volumes. |
| Créer un groupe de volumes |Effectuez l’une des manières suivantes les hello :<ul><li>Cliquez sur hello **Volumes** nœud et avec le bouton droit puis un volume Bonjour **résultats** volet.</li><li>Avec le bouton hello **groupes de volumes** nœud.</li></ul> |Cliquez sur **créer un groupe de volumes** groupe de volumes tooa tooassign volumes. |
| Supprimer |Cliquez sur un nœud ou sur un résultat (cet élément apparaît dans de nombreux menus **Action** et volets **Actions**). |Cliquez sur **supprimer** toodelete hello nœud ou un résultat que vous avez sélectionné. Lors de la boîte de dialogue de confirmation hello s’affiche, confirmez ou annuler la suppression de hello. |
| Détails |Cliquez sur hello **périphériques** nœud et avec le bouton droit puis un appareil Bonjour **résultats** volet. |Cliquez sur **détails** détails de configuration toosee hello pour un périphérique. |
| Modifier |Cliquez sur **stratégies de sauvegarde**, cliquez sur une stratégie Bonjour **résultats** volet. |Cliquez sur **modifier** toochange hello planification de la sauvegarde pour un groupe de volumes. |
| Exporter la liste |Cliquez sur un nœud ou un résultat (cet élément apparaît dans tous les menus **Action** et les volets **Actions**). |Cliquez sur **exporter la liste** toosave une liste dans un fichier de valeurs séparées par des virgules (CSV). Vous pouvez ensuite importer ce fichier dans un tableur pour analyse. |
| Aide |Cliquez sur un nœud ou un résultat. (Cet élément apparaît dans tous les menus **Action** et les volets **Actions**.) |Cliquez sur **aide** tooopen aide en ligne dans une fenêtre de navigateur distincte. |
| Nouvelle fenêtre à partir d’ici |Cliquez sur un nœud ou un résultat (cet élément apparaît dans tous les menus **Action** et les volets **Actions**). |Cliquez sur **nouvelle fenêtre** tooopen une nouvelle fenêtre du Gestionnaire d’instantanés StorSimple. |
| Actualiser |Cliquez sur un nœud ou un résultat (cet élément apparaît dans tous les menus **Action** et les volets **Actions**). |Cliquez sur **Actualiser** fenêtre de gestionnaire d’instantanés StorSimple tooupdate hello actuellement affiché. |
| Actualiser l’appareil |Cliquez sur hello **périphériques** nœud et avec le bouton d’un appareil Bonjour **résultats** volet. |Cliquez sur **actualiser l’appareil** toosynchronize un appareil connecté spécifique avec Gestionnaire d’instantanés StorSimple. |
| Actualiser la liste des appareils |Avec le bouton hello **périphériques** nœud. |Cliquez sur **actualiser les périphériques** toosynchronize la liste des périphériques connectés avec Gestionnaire d’instantanés StorSimple. |
| Relancer l’analyse des volumes |Avec le bouton hello **Volumes** nœud. |Cliquez sur **rescanner les volumes** tooupdate hello liste des volumes de hello **résultats** volet. |
| Restauration |Développez **Catalogue de sauvegarde**, développez un groupe de volumes, développez **Instantanés locaux** ou **Instantanés Cloud**, puis cliquez avec le bouton droit sur une sauvegarde. |Cliquez sur **restaurer** tooreplace hello volume groupe données actuelles avec des données à partir de la sauvegarde sélectionnée de hello hello. |
| Effectuer la sauvegarde |Effectuez l’une des manières suivantes les hello :<ul><li>Développez **Groupes de volumes**, puis cliquez avec le bouton droit sur un groupe de volumes.</li><li>Développez **Catalogue de sauvegarde**, puis cliquez avec le bouton droit sur un groupe de volumes.</li></ul> |Cliquez sur **créer une sauvegarde** toostart immédiatement un travail de sauvegarde. |
| Activer/désactiver l’affichage des importations |Nœud supérieur de clic droit hello Bonjour **étendue** volet (hello **StorSimple Snapshot Manager** nœud dans les exemples hello). |Cliquez sur **activer/désactiver l’affichage des importations** tooshow ou masquer les groupes de volumes hello et les sauvegardes associées qui ont été importées à partir de tableau de bord de service Gestionnaire de périphériques StorSimple hello. |

### <a name="view-menu"></a>Menu Affichage
Hello d’utilisation **vue** menu toocreate une vue personnalisée des hello **résultats** contenu du volet. Hello **vue** menu contient **Ajout/Suppression de colonnes** et **personnaliser** options.

#### <a name="menu-access"></a>Accès au menu
Vous pouvez accéder à hello **vue** menu sur la barre de menus hello ou Bonjour **Actions** volet.

![Menu Affichage du Gestionnaire d’instantanés StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png) 

#### <a name="menu-description"></a>Description de menu
Hello tableau suivant décrit les éléments qui apparaissent sur hello **vue** menu.

| Élément de menu | Description |
|:--- |:--- |
| Ajouter/supprimer des colonnes |Cliquez sur **Ajout/Suppression de colonnes** tooadd ou supprimer des colonnes dans hello **résultats** volet. |
| Personnaliser |Cliquez sur **personnaliser** tooshow ou masquer des éléments dans la fenêtre de console du Gestionnaire d’instantanés StorSimple hello. |

### <a name="favorites-menu"></a>Menu Favoris
Utilisez hello **favoris** menu tooadd, supprimer et organiser des vues de page et les tâches que vous utilisez fréquemment. 

#### <a name="menu-access"></a>Accès au menu
Vous pouvez accéder à hello **favoris** menu hello barre de menus.

![Menu Favoris du Gestionnaire d’instantanés StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_FavoritesMenu.png)

#### <a name="menu-description"></a>Description de menu
Hello tableau suivant décrit les éléments qui apparaissent sur hello **favoris** menu.

| Élément de menu | Description |
|:--- |:--- |
| Ajouter tooFavorites |Cliquez sur **ajouter tooFavorites** tooadd hello tooyour liste actuelle des Favoris. |
| Organiser les Favoris |Cliquez sur **organiser les favoris** contenu de hello tooorganize de votre dossier Favoris. |

### <a name="window-menu"></a>Menu Fenêtre
Hello d’utilisation **fenêtre** fenêtres de console du Gestionnaire d’instantanés StorSimple tooadd et réorganiser des menus.

#### <a name="menu-access"></a>Accès au menu
Vous pouvez accéder à hello **fenêtre** menu hello barre de menus.

![Menu de la Fenêtre Gestionnaire d’instantanés StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_WindowMenu.png)

liste numérotée de Hello dans hello hello menu affiche hello qui sont actuellement ouvertes. Cliquez sur n’importe quelle fenêtre dans cette fenêtre de hello toobring liste au premier plan de hello. 

#### <a name="menu-description"></a>Description de menu
Hello tableau suivant décrit les éléments hello qui apparaissent sur le menu de la fenêtre hello.

| Élément de menu | Description |
|:--- |:--- |
| Nouvelle fenêtre |Cliquez sur **nouvelle fenêtre** tooopen une nouvelle fenêtre de console (dans la fenêtre existante de toohello ajout). |
| Cascade |Cliquez sur **Cascade** fenêtres de console ouvertes toodisplay hello dans un style en cascade. |
| Mosaïque horizontale |Cliquez sur **mosaïque horizontale** fenêtres de console ouvertes hello toodisplay sous forme de vignette (ou grille). |
| Réorganiser les icônes |Si vous avez plusieurs console windows ouvrant et éparpillées sur votre bureau, réduisez-les, puis cliquez sur **réorganiser les icônes** tooarrange dans une ligne horizontale sous hello de votre écran. |

### <a name="help-menu"></a>Menu aide
Hello d’utilisation **aide** menu tooview aide en ligne disponible pour le Gestionnaire d’instantanés StorSimple et hello MMC. Vous pouvez également afficher des informations sur hello MMC et Gestionnaire d’instantanés StorSimple versions des logiciels qui sont actuellement installés sur votre système. 

Vous pouvez accéder à hello **aide** menu hello barre de menus. Vous pouvez également accéder des rubriques d’aide du Gestionnaire d’instantanés StorSimple de hello **Actions** volet.

![Menu Aide du Gestionnaire d’instantanés StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpMenu.png)

#### <a name="menu-description"></a>Description de menu
Hello tableau suivant décrit les éléments qui apparaissent sur le menu aide de hello.

| Élément de menu | Description |
|:--- |:--- |
| Aide du Gestionnaire d’instantanés StorSimple |Cliquez sur **aide sur Gestionnaire d’instantanés StorSimple** tooopen aide du Gestionnaire d’instantanés StorSimple dans une fenêtre distincte. |
| Rubriques d’aide |Cliquez sur **rubriques d’aide** aide en ligne de MMC tooopen dans une fenêtre distincte. |
| Site web TechCenter |Cliquez sur **Site Web TechCenter** page d’accueil Microsoft TechNet Tech Center tooopen hello dans une fenêtre distincte. |
| À propos de Microsoft Management Console |Cliquez sur **sur la Console de gestion Microsoft** toosee version de hello Microsoft Management Console est installé sur votre système. |
| À propos du Gestionnaire d’instantanés StorSimple |Cliquez sur **sur Gestionnaire d’instantanés StorSimple** toosee quelle version du composant logiciel enfichable hello est installée sur votre système. |

## <a name="tool-bar"></a>Barre d’outils
barre d’outils Hello, situé sous la barre de menus de hello, contient les icônes de tâche et de navigation. Chaque icône est contextuel tooa spécifique.

### <a name="icon-descriptions"></a>Description des icônes
Hello tableau suivant décrit les icônes hello qui apparaissent sur la barre d’outils hello. 

| Icône | Description |
|:--- |:--- |
| ![Flèche gauche](./media/storsimple-use-snapshot-manager/HCS_SSM_LeftArrow.png) |Cliquez sur la page précédente toohello du tooreturn icône hello flèche gauche. |
| ![Flèche droite](./media/storsimple-use-snapshot-manager/HCS_SSM_RightArrow.png) |Cliquez sur la page suivante de hello flèche droite toogo toohello (si la flèche de hello est grisée, action de hello est indisponible). |
| ![Icône Haut](./media/storsimple-use-snapshot-manager/HCS_SSM_Up.png) |Cliquez sur hello des toogo icône d’un niveau dans l’arborescence de la console hello (hello **étendue** volet). |
| ![Afficher/Masquer l’arborescence de console](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowConsoleTree.png) |Cliquez sur hello afficher/masquer console arborescence icône tooshow ou masquer hello **étendue** volet. |
| ![Exporter la liste](./media/storsimple-use-snapshot-manager/HCS_SSM_ExportListIcon.png) |Cliquez sur liste d’exportation hello tooexport icône un fichier CSV de tooa liste que vous spécifiez. |
| ![Icône Aide](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpIcon.png) |Cliquez sur hello aide icône tooopen une rubrique d’aide MMC en ligne. |
| ![Afficher/masquer le volet Actions](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowAction.png) |Cliquez sur Afficher/masquer le hello **Actions** hello des tooshow ou masquer icône volet **Actions** volet. |

## <a name="scope-pane"></a>Volet Étendue
Hello **étendue** volet est volet de gauche hello Bonjour Gestionnaire d’instantanés StorSimple UI. Il contient l’arborescence de la console (ou nœud) hello et est le mécanisme de navigation principal hello Gestionnaire d’instantanés StorSimple. 

### <a name="scope-pane-structure"></a>Structure du volet Étendue
Hello **étendue** volet contient une série d’objets interactifs (nœuds), organisée dans une arborescence. 

![Volet Étendue](./media/storsimple-use-snapshot-manager/HCS_SSM_Scope_pane.png) 

* tooexpand ou réduire un nœud, cliquez sur le nom du nœud toohello suivant hello flèche icône.
* état de hello tooview ou du contenu d’un nœud, cliquez sur nom de nœud hello. informations de Hello s’affichent dans hello **résultats** volet. 

Hello **étendue** volet contient hello suivant de nœuds : 

* [Nœud Appareils](#devices-node) 
* [Nœud Volumes](#volumes-node) 
* [Nœud Groupes de volumes](#volume-groups-node) 
* [Nœud Stratégies de sauvegarde](#backup-policies-node) 
* [Nœud Catalogue de sauvegarde](#backup-catalog-node) 
* [Nœud Travaux](#jobs-node) 

### <a name="scope-pane-tasks"></a>Tâches du volet Étendue
Vous pouvez utiliser hello **étendue** volet toocomplete une action sur un nœud spécifique. tooselect une tâche, procédez comme hello suivantes :

* Cliquez sur le nœud de hello et sélectionnez tâche hello à partir du menu hello qui s’affiche.
* Cliquez sur le nœud de hello, puis cliquez sur **Action** sur la barre de menus hello. Sélectionnez la tâche hello à partir du menu hello qui s’affiche.
* Cliquez sur le nœud de hello et action hello puis Bonjour **Actions** volet.

Lorsque vous sélectionnez un nœud et que vous utilisez une de ces méthodes toosee une liste de tâches, uniquement les actions qui peuvent être effectuées sur ce nœud sont affichées.

### <a name="devices-node"></a>Nœud Appareils
Hello **périphériques** nœud représente les appareils StorSimple hello et les appareils virtuels StorSimple qui sont connecté tooStorSimple Gestionnaire d’instantanés. Sélectionnez tooconnect de ce nœud et configurer un appareil et importer ses volumes associés, les groupes de volumes et des copies de sauvegarde existants. Plusieurs périphériques peuvent être connecté tooa seul hôte.

* nœud de hello tooexpand, cliquez sur icône de flèche hello suivant trop**périphériques**.
* toosee un menu des actions disponibles, avec le bouton droit hello **périphériques** nœud ou avec le bouton droit un des nœuds hello qui s’affichent dans hello affichage agrandi.
* toosee une liste des périphériques configurés, cliquez sur **périphériques** Bonjour **étendue** volet. liste de Hello des périphériques, ainsi que des informations sur chaque appareil, s’affiche dans hello **résultats** volet.

### <a name="volumes-node"></a>Nœud Volumes
Hello **Volumes** nœud représente les lecteurs hello qui correspondent toohello les volumes montés par hôte hello, y compris ceux détectés via iSCSI et ceux détectés via un périphérique. Utilisez cette liste de hello tooview nœud de volumes disponibles et attribuer des volumes individuels toovolume groupes.

* nœud de hello tooexpand, cliquez sur icône de flèche hello suivant trop**Volumes**.
* toosee un menu des actions disponibles, avec le bouton droit hello **Volumes** nœud ou avec le bouton droit un des nœuds hello qui s’affichent dans hello affichage agrandi.
* toosee une liste des volumes, cliquez sur **Volumes** Bonjour **étendue** volet. liste de Hello des volumes, ainsi que des informations sur chaque volume, apparaît dans hello **résultats** volet.

### <a name="volume-groups-node"></a>Nœud Groupes de volumes
Les groupes de volumes sont également appelés groupes de cohérence. Chaque groupe de volumes est un pool de volumes de liés à l’application qui vous aide à la cohérence des applications tooensure pendant les opérations de sauvegarde. Hello d’utilisation **groupes de volumes** nœud tooconfigure ces groupes et les tootake des sauvegardes interactives ou créer des planifications de sauvegarde. 

* nœud de hello tooexpand, cliquez sur icône de flèche hello suivant trop**groupes de volumes**.
* toosee un menu des actions disponibles, avec le bouton droit hello **groupes de volumes** nœud ou avec le bouton droit un des nœuds hello qui s’affichent dans hello affichage agrandi.
* toosee une liste des groupes de volumes, cliquez sur **groupes de volumes** Bonjour **étendue** volet. Hello la liste des groupes de volumes, ainsi que des informations sur chaque groupe de volumes, s’affiche dans hello **résultats** volet.

### <a name="backup-policies-node"></a>Nœud Stratégies de sauvegarde
Les stratégies de sauvegarde sont des planifications de tâches liées à des instantanés locaux et du cloud. Hello d’utilisation **les stratégies de sauvegarde** toospecify nœud la fréquence à laquelle une sauvegarde est créée et la durée pendant laquelle une sauvegarde doit être conservé. 

* nœud de hello tooexpand, cliquez sur icône de flèche hello suivant trop**stratégies de sauvegarde**.
* toosee un menu des actions disponibles, avec le bouton droit hello **stratégies de sauvegarde** nœud ou avec le bouton droit un des nœuds hello qui s’affichent dans hello affichage agrandi.
* toosee une liste des stratégies de sauvegarde, cliquez sur **les stratégies de sauvegarde** Bonjour **étendue** volet. liste de Hello des stratégies de sauvegarde, ainsi que des informations sur chaque stratégie, s’affiche dans hello **résultats** volet.

> [!NOTE]
> Vous pouvez conserver un maximum de 64 sauvegardes.


### <a name="backup-catalog-node"></a>Nœud Catalogue de sauvegarde
Hello **catalogue de sauvegarde** nœud contiennent des listes de site et hors site des sauvegardes de volumes Azure StorSimple. Ce nœud est organisé par groupe de volumes, et chaque conteneur de groupe de volumes contient des structures distinctes pour les instantanés locaux (hello **instantané Local**nœud) et les instantanés cloud (hello **instantanés Cloud** nœud ). Développée, chaque conteneur de groupe de volumes répertorie toutes les sauvegardes réussies hello qui ont été effectuées de façon interactive ou par une stratégie configurée.

* nœud de hello tooexpand, cliquez sur icône de flèche hello suivant trop**catalogue de sauvegarde**.
* toosee un menu des actions disponibles, avec le bouton droit hello **catalogue de sauvegarde** nœud ou avec le bouton droit un des nœuds hello qui s’affichent dans hello affichage agrandi.
* toosee une liste d’instantanés de sauvegarde, cliquez sur **catalogue de sauvegarde** Bonjour **étendue** volet. liste de Hello d’instantanés, ainsi que des informations sur chaque instantané, s’affiche dans hello **résultats** volet.

### <a name="local-snapshots-node"></a>Nœud Instantanés locaux
Hello **instantanés locaux** nœud répertorie les instantanés locaux pour un groupe de volumes spécifique. nœud de Hello se trouve sous hello **catalogue de sauvegarde** nœud Bonjour **étendue** volet. Instantanés locaux sont des copies des données de volume sont stockées sur l’unité Azure StorSimple de hello point-à-temps. En règle générale, ce type de sauvegarde peut être créé et restauré rapidement. Vous pouvez utiliser un instantané local comme vous utiliseriez une copie de sauvegarde locale.

* nœud de hello tooexpand, cliquez sur icône de flèche hello suivant trop**instantanés locaux**.
* toosee un menu des actions disponibles, avec le bouton droit hello **instantanés locaux** nœud ou avec le bouton droit un des nœuds hello qui s’affichent dans hello affichage agrandi.
* toosee une liste des instantanés locaux, cliquez sur **instantanés locaux** Bonjour **étendue** volet. liste de Hello d’instantanés, ainsi que des informations sur chaque instantané, s’affiche dans hello **résultats** volet.

### <a name="cloud-snapshots-node"></a>Nœud Instantanés Cloud
Hello **instantanés Cloud** nœud répertorie les instantanés de cloud pour un groupe de volumes spécifique. nœud de Hello se trouve sous hello **catalogue de sauvegarde** nœud Bonjour **étendue** volet. Instantanés cloud sont des copies des données de volume sont stockées dans le cloud de hello point-à-temps. Un instantané cloud est équivalent instantané tooa répliqué sur un système de stockage hors site, distinct. Les instantanés cloud sont particulièrement utiles dans les scénarios de récupération d’urgence.

* nœud de hello tooexpand, cliquez sur icône de flèche hello suivant trop**instantanés Cloud**.
* toosee un menu des actions disponibles, avec le bouton droit hello **instantanés Cloud** nœud ou avec le bouton droit un des nœuds hello qui s’affichent dans hello affichage agrandi.
* toosee une liste des instantanés de cloud, cliquez sur **instantanés Cloud** Bonjour **étendue** volet. liste de Hello d’instantanés, ainsi que des informations sur chaque instantané, s’affiche dans hello **résultats** volet.

### <a name="jobs-node"></a>Nœud Travaux
Hello **travaux** nœud contient des informations sur les travaux de sauvegarde planifiées, en cours d’exécution ou récemment effectués. 

* nœud de hello tooexpand, cliquez sur icône de flèche hello suivant trop**travaux**.
* toosee un menu des actions disponibles, avec le bouton droit hello **travaux** nœud ou avec le bouton droit un des nœuds hello qui s’affichent dans hello affichage agrandi.
* toosee une liste des tâches planifiées, développez hello **travaux** nœud, puis cliquez sur **planifiée**. Hello liste des travaux précédemment configurés et des informations sur chaque travail apparaît dans hello **résultats** volet. 
* toosee une liste des travaux récemment effectués, développez hello **travaux** nœud, puis cliquez sur **dernières 24 heures**. Une liste de tâches qui ont été effectuées dans hello des dernières 24 heures apparaît dans hello **résultats** volet. Hello **résultats** volet contient également des informations sur chaque travail effectué.
* toosee une liste des tâches en cours d’exécution, développez hello **travaux** nœud, puis cliquez sur **en cours d’exécution**. liste de Hello de tâches en cours et informations sur chaque tâche s’affiche dans hello **résultats** volet.

## <a name="results-pane"></a>Volet Résultats
Hello **résultats** volet est le volet central de hello Bonjour Gestionnaire d’instantanés StorSimple UI. Il contient des listes et des informations d’état détaillées pour le nœud hello sélectionné Bonjour **étendue** volet.

### <a name="example"></a>Exemple
hello toosee exemple, cliquez sur hello **groupes de volumes** nœud Bonjour **étendue** volet. Hello **résultats** volet affiche une liste des groupes de volumes avec des détails sur chaque groupe.

![Volet Résultats](./media/storsimple-use-snapshot-manager/HCS_SSM_Results_pane.png) 

Vous pouvez configurer les détails de hello illustrés hello **résultats** volet : cliquez sur un nœud Bonjour **étendue** volet, cliquez sur **vue**, puis cliquez sur **Ajout/Suppression Colonnes**.

## <a name="actions-pane"></a>Volet Actions
Hello **Actions** volet est le volet de droite hello Bonjour Gestionnaire d’instantanés StorSimple UI. Il contient un menu d’opérations que vous pouvez effectuer sur le nœud de hello, vue ou les données que vous sélectionnez dans hello **étendue** volet ou **résultats** volet. Hello **Actions** volet contient hello même des commandes en tant que hello **Action** menus qui sont disponibles pour les éléments hello **étendue** volet et **résultats**volet. Pour obtenir une description de chaque action, consultez le tableau de hello Bonjour **Action** section de menu.

### <a name="examples"></a>Exemples
hello toosee hello de l’exemple suivant **étendue** volet, développez hello **travaux** nœud et cliquez sur **planifiée**. Hello **Actions** volet affiche les actions disponibles hello pour hello **planifiée** nœud.

![Exemple de tâches planifiées dans le volet Actions](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane.png) 

toosee options plus Bonjour **étendue** volet, développez hello **travaux** nœud, cliquez sur **planifiée**, puis cliquez sur une tâche planifiée dans hello **résultats**volet. Hello **Actions** volet affiche les actions disponibles hello pour la tâche planifiée de hello, comme illustré dans hello l’exemple suivant.

![Exemple d’actions de tâche dans le volet Actions](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

## <a name="keyboard-navigation-and-shortcuts"></a>Navigation et raccourcis clavier
Gestionnaire d’instantanés StorSimple Active les fonctionnalités d’accessibilité de hello du système d’exploitation de Windows hello et hello Microsoft Management Console (MMC). Il inclut également des fonctionnalités de navigation de clavier et les raccourcis sont spécifique toohello Gestionnaire d’instantanés StorSimple, comme décrit dans les sections suivantes de hello.

* [Touches de déplacement clavier](#keyboard-navigation-keys) 
* [Touches de raccourci de la barre de menus](#menu-bar-shortcut-keys) 
* [Touches de raccourci du volet Étendue](#scope-pane-shortcut-keys) 

### <a name="keyboard-navigation-keys"></a>Touches de déplacement clavier
Hello tableau suivant décrit les clés hello que vous pouvez utiliser d’interface utilisateur de toonavigate hello Gestionnaire d’instantanés StorSimple. 

| Touche de navigation | Action |
|:--- |:--- |
| Touche flèche bas |Utilisez hello toomove clé de flèche vers le bas verticalement toohello des élément suivant dans un menu ou d’un volet. |
| Entrez |Appuyez sur hello entrée toocomplete clé une action, puis effectuez la toohello la prochaine étape. Par exemple, vous pouvez appuyer sur entrée tooselect **suivant**, **OK**, ou **créer**, puis passez toohello d’étape suivante de l’Assistant. |
| Échap |Appuyez sur tooclose clé hello ÉCHAP un menu ou une toocancel et fermer une page. |
| F1 |Appuyez sur hello F1 tooview clé une rubrique d’aide pour la fenêtre actuellement active hello. |
| F5 |Appuyez sur hello F5 toorefresh clé un nœud. |
| F6 |Appuyez sur toomove de touche F6 hello de hello **étendue** volet toohello **résultats** volet. |
| F10 |Appuyez sur la barre de menus de hello F10 toogo clé toohello. |
| Touche de flèche gauche |Utilisez hello gauche toomove clé de flèche horizontalement à partir d’une option menu barre option toohello précédente. Lorsque vous déplacez toohello précédente menu de l’élément sur la barre de menu hello, des actions de hello (ou contexte) pour l’élément précédent de hello s’affiche. |
| Touche de direction droite |Utiliser toomove de clé de flèche droite hello horizontalement à partir d’un menu de la barre option toohello ensuite. Lorsque vous déplacez le menu de l’élément sur la barre de menu hello, des actions de hello (ou contexte) suivant toohello pour un nouvel élément hello apparaît. |
| Touche de tabulation |Utilisez volet suivant de hello onglet toomove clé toohello sur hello console ou toohello suivante sélection ou zone de texte dans une page. |
| Touche de direction Haut |Utilisez hello des toomove de clé flèche verticalement toohello des élément précédent dans un menu ou d’un volet. |

### <a name="menu-bar-shortcut-keys"></a>Touches de raccourci de la barre de menus
Hello tableau suivant décrit les combinaisons de touches de raccourci hello pour la barre de menus hello. Une fois que vous appuyez sur les touches de raccourci hello et hello menu s’ouvre, vous pouvez utiliser les touches de raccourci de menu (hello soulignés clés sur le menu de hello). Pour plus d’informations sur la barre de menus hello, accédez trop[barre de menus](#menu-bar).

| Raccourci | Résultat | Touche de raccourci du menu | Résultat |
|:--- |:--- |:--- |:--- |
| ALT + F |Ouvre hello **fichier** menu. |N |Ouvre une nouvelle instance de console. |
|  |O |Ouvre hello **outils d’administration** page. | |
|  |S |Enregistre la console du Gestionnaire d’instantanés StorSimple hello. | |
|  |A |Ouvre hello **Enregistrer sous** page. | |
|  |M |Ouvre hello **ajouter/supprimer un composant logiciel enfichable** page. | |
|  |P |Ouvre hello **Options** page. | |
|  |H |Ouvre l’aide en ligne. | |
| ALT + A |Ouvre hello **Action** menu. |I |Active l’option d’affichage importation hello et désactive. |
|  |W |Ouvre une nouvelle console de gestionnaire d’instantanés StorSimple. | |
|  |F |Met à jour de la console du Gestionnaire d’instantanés StorSimple hello. | |
|  |L |Ouvre hello **exporter la liste** page. | |
|  |H |Ouvre l’aide en ligne. | |
| ALT + V |Ouvre hello **vue** menu. |A |Ouvre hello **Ajout/Suppression de colonnes** page. |
|  |U |Ouvre hello **personnaliser l’affichage** page. | |
| ALT + O |Ouvre hello **favoris** menu. |A |Ouvre hello **ajouter tooFavorites** page. |
|  |O |Ouvre hello **organiser les favoris** page. | |
| ALT + W |Ouvre hello **fenêtre** menu. |N |Ouvre une autre fenêtre de Gestionnaire d’instantanés StorSimple. |
|  |C |Affiche toutes les fenêtres de console ouvertes en cascade. | |
|  |T |Affiche toutes les fenêtres de console ouvertes dans une grille. | |
|  |I |Réorganise les icônes dans une ligne horizontale au bas de hello de votre écran. | |
| ALT + H |Ouvre hello **aide** menu. |H |Ouvre l’aide en ligne. |
|  |T |Ouvre la page web de Microsoft TechNet Tech Center hello. | |
|  |A |Ouvre hello **sur la Console de gestion Microsoft** page. | |

### <a name="scope-pane-shortcut-keys"></a>Touches de raccourci du volet Étendue
Hello tableaux suivants montrent les raccourcis hello combinaisons de touches pour chaque nœud dans hello **étendue** volet. 

* [Touches de raccourci du nœud Périphériques](#devices-node-shortcut-keys)
* [Touches de raccourci du nœud Volumes](#volumes-node-shortcut-keys)
* [Touches de raccourci du nœud Groupes de volumes](#volume-groups-node-shortcut-keys)
* [Touches de raccourci du nœud Stratégies de sauvegarde](#backup-policies-node-shortcut-keys)
* [Touches de raccourci du nœud Catalogue de sauvegarde](#backup-catalog-node-shortcut-keys)
* [Touches de raccourci du nœud Tâches](#jobs-node-shortcut-keys)

#### <a name="devices-node-shortcut-keys"></a>Touches de raccourci du nœud Périphériques
| Raccourci du menu | Résultat |
|:--- |:--- |
| C |Ouvre hello **configurer un appareil** page. |
| D |Actualise la liste hello de périphériques et les détails de l’appareil. |
| V |Ouvre hello **vue** menu. |
| W |Ouvre une nouvelle console du Gestionnaire d’instantanés StorSimple consacrée hello **détails** nœud. |
| F |Met à jour de la console du Gestionnaire d’instantanés StorSimple hello. |
| L |Ouvre hello **exporter la liste** page. |
| H |Ouvre l’aide en ligne. |

#### <a name="volumes-node-shortcut-keys"></a>Touches de raccourci du nœud Volumes
| Raccourci du menu | Résultat |
|:--- |:--- |
| V |Liste de hello mises à jour des volumes. |
| V (appuyer deux fois) |Ouvre hello **vue** menu. |
| W |Ouvre une nouvelle console du Gestionnaire d’instantanés StorSimple consacrée hello **Volumes** nœud. |
| F |Met à jour de la console du Gestionnaire d’instantanés StorSimple hello. |
| L |Ouvre hello **exporter la liste** page. |
| H |Ouvre l’aide en ligne. |

#### <a name="volume-groups-node-shortcut-keys"></a>Touches de raccourci du nœud Groupes de volumes
| Raccourci du menu | Résultat |
|:--- |:--- |
| G |Ouvre hello **créer un groupe de volumes** page. |
| V |Ouvre hello **vue** menu. |
| W |Ouvre une nouvelle console du Gestionnaire d’instantanés StorSimple consacrée hello **groupes de volumes** nœud. |
| F |Met à jour de la console du Gestionnaire d’instantanés StorSimple hello. |
| L |Ouvre hello **exporter la liste** page. |
| H |Ouvre l’aide en ligne. |

#### <a name="backup-policies-node-shortcut-keys"></a>Touches de raccourci du nœud Stratégies de sauvegarde
| Raccourci du menu | Résultat |
|:--- |:--- |
| B |Ouvre hello **créer une stratégie** page. |
| V |Ouvre hello **vue** menu. |
| W |Ouvre une nouvelle console du Gestionnaire d’instantanés StorSimple consacrée hello **groupes de volumes** nœud. |
| F |Met à jour de la console du Gestionnaire d’instantanés StorSimple hello. |
| L |Ouvre hello ** exporter la liste ** page. |
| H |Ouvre l’aide en ligne. |

#### <a name="backup-catalog-node-shortcut-keys"></a>Touches de raccourci du nœud Catalogue de sauvegarde
| Raccourci du menu | Résultat |
|:--- |:--- |
| W |Ouvre une nouvelle console du Gestionnaire d’instantanés StorSimple consacrée hello **groupes de volumes** nœud. |
| F |Met à jour de la console du Gestionnaire d’instantanés StorSimple hello. |
| H |Ouvre l’aide en ligne. |

#### <a name="jobs-node-shortcut-keys"></a>Touches de raccourci du nœud Tâches
| Raccourci du menu | Résultat |
|:--- |:--- |
| V |Ouvre hello **vue** menu. |
| W |Ouvre une nouvelle console du Gestionnaire d’instantanés StorSimple consacrée hello **travaux** nœud. |
| F |Met à jour de la console du Gestionnaire d’instantanés StorSimple hello. |
| L |Ouvre hello **exporter la liste** page. |
| H |Ouvre l’Aide en ligne |

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple tooadminister votre solution StorSimple](storsimple-snapshot-manager-admin.md).
* Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple tooconnect et gérer les périphériques](storsimple-snapshot-manager-manage-devices.md).

