---
title: "administration du Gestionnaire d’instantanés d’aaaStorSimple | Documents Microsoft"
description: "Fournit une vue d’ensemble et les liens toomore d’informations sur les tâches d’administration de solution de gestionnaire d’instantanés StorSimple et de flux de travail."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 1cdbb61d-bd16-4be4-ade2-ceab11508acb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2016
ms.author: v-sharos
ms.openlocfilehash: d875f2efbdeb844b412cf8d9f1f971f18da7526e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooadminister-your-storsimple-solution"></a>Utilisez le Gestionnaire d’instantanés StorSimple tooadminister votre solution StorSimple

## <a name="overview"></a>Vue d'ensemble
Gestionnaire d’instantanés StorSimple est un composant logiciel enfichable Microsoft Management Console (MMC) qui simplifie la protection des données et la gestion des sauvegardes dans l’environnement Microsoft Azure StorSimple. Avec Gestionnaire d’instantanés StorSimple, vous pouvez gérer les données de Microsoft Azure StorSimple dans le centre de données hello et dans le cloud de hello comme une solution de stockage intégrée unique, par conséquent, ce qui simplifie le processus de sauvegarde et de réduire les coûts.

console de gestion centrale Hello StorSimple Snapshot Manager vous permet de toocreate cohérente et point-à-temps copies de sauvegarde locale et des données cloud. Par exemple, vous pouvez utiliser la console hello pour :

* Configurer, sauvegarder et supprimer des volumes.
* Configurer le volume tooensure de groupes les données sauvegardées est cohérente avec les applications.
* Gérer les stratégies de sauvegarde afin que les données soient sauvegardées selon un calendrier prédéterminé.
* Créer des copies indépendantes des données, ce qui peuvent être stockées dans le cloud de hello et utilisées pour la récupération d’urgence.

Cet article fournit des liens tootutorials qui décrivent le Gestionnaire d’instantanés StorSimple et comment toouse il toocomplete les workflows et les tâches d’administration système.

* Pour plus d’informations sur l’architecture et les composants du Gestionnaire d’instantanés StorSimple, consultez l’article [Qu’est-ce que le Gestionnaire d’instantanés StorSimple ?](storsimple-what-is-snapshot-manager.md) 
* toodownload StorSimple Snapshot Manager, accédez trop[page de téléchargement du Gestionnaire d’instantanés StorSimple hello](https://www.microsoft.com/download/details.aspx?id=44220).
* Pour les procédures de déploiement de StorSimple Snapshot Manager, accédez trop[déployer le Gestionnaire d’instantanés StorSimple](storsimple-snapshot-manager-deployment.md).

> [!NOTE]
> Vous ne pouvez pas utiliser le Gestionnaire d’instantanés StorSimple toomanage Microsoft Azure StorSimple tableaux virtuels (également appelé StorSimple local périphériques virtuels).


## <a name="storsimple-snapshot-manager-tasks-and-workflows"></a>Tâches et flux de travail du Gestionnaire d’instantanés StorSimple
Vous pouvez utiliser hello toomonitor de gestionnaire d’instantanés StorSimple et gérer des travaux de sauvegarde en cours, planifiées et terminées. En outre, le Gestionnaire d’instantanés StorSimple fournit un catalogue de sauvegarde too64 s’est terminée. Vous pouvez utiliser hello catalogue toofind et restaurer des volumes ou des fichiers individuels. 

| IF tooDO vous souhaitez que ce... | SUIVEZ CE DIDACTICIEL... |
|:--- |:--- |
| En savoir plus sur le Gestionnaire d’instantanés StorSimple |[Qu’est-ce que le Gestionnaire d’instantanés StorSimple ? ](storsimple-what-is-snapshot-manager.md) |
| Installer le Gestionnaire d’instantanés StorSimple<br>Réinstallation du Gestionnaire d’instantanés StorSimple<br>Supprimer le Gestionnaire d’instantanés StorSimple |[Déployer le Gestionnaire d’instantanés StorSimple](storsimple-snapshot-manager-deployment.md) |
| Utiliser les menus et les fonctionnalités du Gestionnaire d’instantanés StorSimple :<ul><li>Barre de menus</li><li>Barre d’outils</li><li>Volet Étendue</li><li>Volet Résultats</li><li>Volet Actions</li><li>Navigation et raccourcis clavier</li></ul> |[Interface utilisateur du Gestionnaire d’instantanés StorSimple](storsimple-use-snapshot-manager.md) |
| Utilisez fonctionnalités MMC communes hello incluses dans Gestionnaire d’instantanés StorSimple :<ul><li>Affichage</li><li>Nouvelle fenêtre à partir d’ici</li><li>Actualiser</li><li>Exporter la liste</li><li>Aide</li></ul> |[Utilisez les actions du menu MMC hello dans Gestionnaire d’instantanés StorSimple](storsimple-snapshot-manager-mmc-menu.md) |
| Ajout ou remplacement d’un appareil<br>Connexion d'un appareil<br>Vérification des groupes de volumes importés<br>Actualisation des appareils connectés<br>Authentification d’un appareil<br>Affichage des détails sur l’appareil<br>Suppression de la configuration d’un appareil<br>Modification du mot de passe d’un appareil<br>Remplacement d’un appareil défaillant<br> |[Utilisez le Gestionnaire d’instantanés StorSimple tooconnect et gérer les appareils StorSimple](storsimple-snapshot-manager-manage-devices.md) |
| Monter les volumes<br>Afficher des informations sur les volumes<br>Suppression d’un volume<br>Relancer l’analyse des volumes<br>Configurer et sauvegarder un volume de base<br>Configurer et sauvegarder un volume dynamique en miroir |[Utilisez le Gestionnaire d’instantanés StorSimple tooview et gestion des volumes](storsimple-snapshot-manager-manage-volumes.md) |
| Afficher les groupes de volumes<br>Créer un groupe de volumes<br>Sauvegarder un groupe de volumes<br>Modifier un groupe de volumes<br>Supprimer un groupe de volumes |[Utilisez le Gestionnaire d’instantanés StorSimple toocreate et gérer des groupes de volumes](storsimple-snapshot-manager-manage-volume-groups.md) |
| Créer une stratégie de sauvegarde <br>Modifier une stratégie de sauvegarde<br>Supprimer une stratégie de sauvegarde |[Utilisez le Gestionnaire d’instantanés StorSimple toocreate et gérer des stratégies de sauvegarde](storsimple-snapshot-manager-manage-backup-policies.md) |
| Afficher et gérer les tâches de sauvegarde planifiés<br>Affichage et gestion des tâches de sauvegarde récentes<br>Afficher et gérer les tâches de sauvegarde en cours d’exécution |[Utilisez le Gestionnaire d’instantanés StorSimple tooview et gérer des travaux de sauvegarde](storsimple-snapshot-manager-manage-backup-jobs.md) |
| Restaurer un volume<br>Cloner un volume ou un groupe de volumes<br>Supprimer une sauvegarde<br>Récupérer un fichier<br>Restaurer la base de données du Gestionnaire d’instantanés StorSimple hello |[Catalogue de sauvegarde de gestionnaire d’instantanés StorSimple utilisation toomanage hello](storsimple-snapshot-manager-manage-backup-catalog.md) |

## <a name="next-steps"></a>Étapes suivantes
[Télécharger le Gestionnaire d’instantanés StorSimple](https://www.microsoft.com/download/details.aspx?id=44220).

