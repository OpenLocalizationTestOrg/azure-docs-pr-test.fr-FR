---
title: "administration du service Gestionnaire d’aaaStorSimple | Documents Microsoft"
description: "Découvrez comment toomanage votre appareil StorSimple à l’aide de hello dans le service StorSimple Manager hello portail Azure classic."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2586582e-d85c-42e1-afb3-be734c1c0461
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 695ebbb785590a0e3d6de4c73125f65b16dcb776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooadminister-your-storsimple-device"></a>Utilisez hello StorSimple Manager service tooadminister votre appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Cet article décrit l’interface de service StorSimple Manager hello, y compris pour tooconnect tooit, hello différentes options disponibles et lie les toohello spécifique des flux de travail qui peut être effectuées via cette interface utilisateur. Ce guide est applicable tooboth ; Hello StorSimple physique et un appareil virtuel hello.

Cet article portera sur les éléments suivants :

* Se connecter tooStorSimple le service Manager
* Accédez hello StorSimple Manager UI
* Administrer l’unité StorSimple via hello service StorSimple Manager

## <a name="connect-toostorsimple-manager-service"></a>Se connecter tooStorSimple le service Manager
Hello service StorSimple Manager s’exécute dans Microsoft Azure et connecte les appareils StorSimple toomultiple. Vous utilisez un portail Microsoft Azure classique central en cours d’exécution dans un navigateur toomanage ces appareils. tooconnect toohello service StorSimple Manager, procédez comme hello suivant.

#### <a name="tooconnect-toohello-service"></a>tooconnect toohello service
1. Accédez trop[https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. À l’aide de vos informations d’identification de compte Microsoft, ouvrez une session sur le portail classique Azure de Microsoft toohello (situé en haut à droite de hello du volet de hello).
3. Faites défiler hello laissé le service StorSimple Manager navigation volet tooaccess hello.

## <a name="navigate-storsimple-manager-service-ui"></a>Navigation dans l’interface utilisateur du service StorSimple Manager
Bonjour la hiérarchie de navigation de l’interface utilisateur est indiqué dans hello tableau suivant le service StorSimple Manager hello.

* **StorSimple Manager** page d’accueil vous amène toohello l’interface utilisateur des pages de niveau de service applicables tooall des appareils au sein d’un service.
* **Appareils** vous redirige périphérique spécifique tooa applicables du pages UI toohello au niveau de l’appareil.
* **Conteneurs de volumes** vous redirige page volume toohello qui affiche tous les volumes hello associés à un appareil.

#### <a name="storsimple-manager-service-navigational-hierarchy"></a>Hiérarchie de navigation du service StorSimple Manager
| Page d’accueil | Pages de niveau de service | Pages de niveau appareil | Pages de niveau appareil |
| --- | --- | --- | --- |
| service StorSimple Manager |Tableau de bord du service |Page du tableau de bord d’un appareil | |
| Appareils → |Surveiller | | |
| Catalogue de sauvegarde |Conteneurs de volume → |Volumes | |
| Configurer (Service) |Stratégies de sauvegarde | | |
| Travaux |Configurer (Appareil) | | |
| Alertes |Maintenance | | |

![Vidéo disponible](./media/storsimple-manager-service-administration/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui vous guide dans l’interface utilisateur du hello StorSimple Manager service, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/storsimple-manager-service-overview/).

## <a name="administer-storsimple-device-using-storsimple-manager-service"></a>Gestion d’un appareil StorSimple via le service StorSimple Manager
Hello tableau suivant présente un résumé de toutes les tâches de gestion courantes hello et flux de travail complexes qui peut être effectuées dans hello interface utilisateur du service StorSimple Manager. Ces tâches sont classées en fonction des pages d’interface utilisateur hello sur lequel elles sont démarrées.

Pour plus d’informations sur chaque flux de travail, cliquez sur hello procédure adéquate décrite dans la table de hello.

#### <a name="storsimple-manager-workflows"></a>Flux de travail de StorSimple Manager
| Si vous le souhaitez toodo... | Atteindre la page de l’interface utilisateur de toothis... | Suivez cette procédure. |
| --- | --- | --- |
| Création d’un service</br>Supprimer un service</br>Obtenir la clé d’inscription au service</br>Régénération d’une clé d’inscription de service |service StorSimple Manager |[Déploiement du service StorSimple Manager](storsimple-manage-service.md) |
| Modifier la clé de chiffrement de données de service hello</br>Afficher les journaux opération hello |Service StorSimple Manager → Tableau de bord |[Utilisez le tableau de bord de service hello StorSimple Manager](storsimple-service-dashboard.md) |
| Désactiver un appareil</br>Suppression d’un appareil |Service StorSimple Manager → Appareil |[Désactivation ou suppression d’un appareil](storsimple-deactivate-and-delete-device.md) |
| En savoir plus sur le basculement entre appareils et la récupération d’urgence</br>Périphérique physique tooa de basculement</br>Périphérique virtuel tooa de basculement</br>Continuité d’activité et récupération d’urgence (Business Continuity Disaster Recovery - BCDR) |Service StorSimple Manager → Appareil |[Basculement et récupération d’urgence pour votre appareil StorSimple](storsimple-device-failover-disaster-recovery.md) |
| Liste des sauvegardes d’un volume</br>Sélectionner un jeu de sauvegarde</br>Suppression d’un jeu de sauvegarde |Service StorSimple Manager → Catalogue de sauvegarde |[Gestion des sauvegardes](storsimple-manage-backup-catalog.md) |
| Clonage d’un volume |Service StorSimple Manager → Catalogue de sauvegarde |[Clonage d’un volume](storsimple-clone-volume.md) |
| Restauration d'un jeu de sauvegarde |Service StorSimple Manager → Catalogue de sauvegarde |[Restauration d'un jeu de sauvegarde](storsimple-restore-from-backup-set.md) |
| À propos des comptes de stockage</br>Ajout d’un compte de stockage</br>Modification d’un compte de stockage</br>Suppression d'un compte de stockage</br>Rotation des clés des comptes de stockage. |Service StorSimple Manager → Configuration |[Gestion des comptes de stockage](storsimple-manage-storage-accounts.md) |
| À propos des modèles de bande passante</br>Ajouter un modèle de bande passante</br>Modifier un modèle de bande passante</br>Supprimer un modèle de bande passante</br>Utiliser un modèle de bande passante par défaut</br>Création d’un modèle de bande passante à la journée commençant à une heure précise |Service StorSimple Manager → Configuration |[Modèles de bande passante](storsimple-manage-bandwidth-templates.md) |
| À propos des enregistrements de contrôle d’accès</br>Création d'un enregistrement de contrôle d’accès</br>Modifier un enregistrement de contrôle d’accès</br>Supprimer un enregistrement de contrôle d’accès |Service StorSimple Manager → Configuration |[Gestion d’enregistrements de contrôle d’accès](storsimple-manage-acrs.md) |
| Affichage des détails d’une tâche</br>Annulation d’un travail |Service StorSimple Manager → Tâches |[Gestion des travaux](storsimple-manage-jobs.md) |
| Réception de notifications d’alerte</br>Gérer les alertes</br>Consulter les alertes |Service StorSimple Manager → Alertes |[Affichage et gestion des alertes StorSimple](storsimple-manage-alerts.md) |
| Affichage des initiateurs connectés</br>Rechercher le numéro de série du périphérique hello</br>Rechercher l’IQN cible de hello |Service StorSimple Manager → Appareils → Tableau de bord |[Utiliser le tableau de bord hello StorSimple périphérique](storsimple-device-dashboard.md) |
| Création de graphiques d’analyse |Service StorSimple Manager → Appareils → Surveillance |[Surveillance de votre appareil StorSimple](storsimple-monitor-device.md) |
| Ajout d’un conteneur de volumes</br>Modifier un conteneur de volumes</br>Suppression d’un conteneur de volumes |Service StorSimple Manager → Appareils → Conteneurs de volume |[Gestion de conteneurs de volume](storsimple-manage-volume-containers.md) |
| Ajout d’un volume</br>Modification d’un volume</br>Mise hors connexion d’un volume</br>Suppression d’un volume</br>Analyse d’un volume |Service StorSimple Manager → Appareils → Conteneurs de volume → Volumes |[Gestion de volumes](storsimple-manage-volumes.md) |
| Modification des paramètres de l’appareil</br>Modification des paramètres d’heure</br>Modification des paramètres DNS.md</br>Configuration d’interfaces réseau |Service StorSimple Manager → Appareils → Configuration |[Modification de la configuration de votre appareil StorSimple](storsimple-modify-device-config.md) |
| Affichage des paramètres de proxy web |Service StorSimple Manager → Appareils → Configuration |[Configuration du proxy web de votre appareil](storsimple-configure-web-proxy.md) |
| Modification du mot de passe administrateur de votre appareil</br>Modification du mot de passe de StorSimple Snapshot Manager |Service StorSimple Manager → Appareils → Configuration |[Modification des mots de passe StorSimple](storsimple-change-passwords.md) |
| Configuration de la gestion à distance |Service StorSimple Manager → Appareils → Configuration |[Se connecter à distance de l’appareil StorSimple tooyour](storsimple-remote-connect.md) |
| Configuration des paramètres d'alerte |Service StorSimple Manager → Appareils → Configuration |[Affichage et gestion des alertes StorSimple](storsimple-manage-alerts.md) |
| Configuration de CHAP pour votre appareil StorSimple |Service StorSimple Manager → Appareils → Configuration |[Configuration de CHAP pour votre appareil StorSimple](storsimple-configure-chap.md) |
| Ajout d’une stratégie de sauvegarde</br>Ajouter ou modifier une planification</br>Supprimer une stratégie de sauvegarde</br>Exécuter une sauvegarde manuelle</br>Création d’une stratégie de sauvegarde personnalisée avec plusieurs volumes et planifications |Service StorSimple Manager → Appareils → Stratégies de sauvegarde |[Gestion des stratégies de sauvegarde](storsimple-manage-backup-policies.md) |
| Arrêt des contrôleurs d’appareil</br>Redémarrage des contrôleurs de l’appareil</br>Arrêt des contrôleurs de l'appareil</br>Réinitialiser les paramètres par défaut toofactory périphérique</br>(Les données ci-dessus s’appliquent aux appareils en local uniquement) |Service StorSimple Manager → Appareils → Maintenance |[Gestion du contrôleur d’appareil StorSimple](storsimple-manage-device-controller.md) |
| En savoir plus sur les composants matériels de StorSimple</br>Surveillance de l'état du matériel</br>(Les données ci-dessus s’appliquent aux appareils en local uniquement) |Service StorSimple Manager → Appareils → Maintenance |[Surveillance des composants matériels](storsimple-monitor-hardware-status.md) |
| Création d’un package de prise en charge |Service StorSimple Manager → Appareils → Maintenance |[Création et gestion d’un package de prise en charge](storsimple-create-manage-support-package.md) |
| Installer les mises à jour logicielles |Service StorSimple Manager → Appareils → Maintenance |[Mise à jour de votre appareil](storsimple-update-device.md) |

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes avec les opérations quotidiennes hello sur votre appareil StorSimple ou avec un de ses composants matériels, reportez-vous à :

* [Résolution des problèmes d’un appareil opérationnel](storsimple-troubleshoot-operational-device.md)
* [Utilisation des indicateurs de surveillance de StorSimple](storsimple-monitoring-indicators.md)

Si vous ne pouvez pas résoudre les problèmes de hello et vous devez toocreate une demande de service, consultez trop[contactez le Support technique Microsoft](storsimple-contact-microsoft-support.md).

