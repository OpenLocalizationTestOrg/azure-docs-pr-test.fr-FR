---
title: notes de publication aaaStorSimple 8000 Series Update 3 | Documents Microsoft
description: "Décrit les nouvelles fonctionnalités de hello, des problèmes et solutions de contournement pour StorSimple 8000 Series Update 3."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 2158aa7a-4ac3-42ba-8796-610d1adb984d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5bfcba61f7f210531437f650eafaad4dbd8c7c45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-3-release-notes-for-your-storsimple-8000-series-device"></a>Notes de publication Update 3 pour votre appareil StorSimple série 8000

## <a name="overview"></a>Vue d'ensemble
Bonjour notes de publication suivantes décrivent les nouvelles fonctionnalités de hello et identifient les problèmes critiques en suspens hello pour StorSimple 8000 Series Update 3. Ils contiennent également une liste de mises à jour du logiciel hello StorSimple inclus dans cette version. 

Mise à jour 3 peut être en cours d’exécution mise en production (GA) ou mise à jour 0.1 à 2.2 de la mise à jour de l’appareil StorSimple tooany appliqué. version de l’appareil Hello associée à 3 de la mise à jour est 6.3.9600.17759.

Veuillez consulter les informations de hello contenues dans la version de hello notes avant de déployer hello mettre à jour dans votre solution StorSimple.

> [!IMPORTANT]
> * Update 3 comprend les mises à jour du logiciel de l’appareil, du microprogramme et du pilote LSI et de Storport et Spaceport. Il prend environ 1,5 à 2 heures tooinstall cette mise à jour. 
> * Pour les nouvelles versions, vous ne voyiez pas les mises à jour immédiatement, car nous effectuer un déploiement échelonné des mises à jour hello. Revérifiez les mises à jour dans quelques jours, car elles seront bientôt disponibles.
> 
> 

## <a name="whats-new-in-update-3"></a>Nouveautés d’Update 3
Hello améliorations clées suivantes et les correctifs de bogues ont été apportées dans Update 3.

* **Automatisée des modifications d’une récupération de l’espace** – démarrage Update 3, les algorithmes de récupération de l’espace hello s’exécuter sur le contrôleur de secours hello du système hello entraîne une exécution plus rapide. Pour plus d’informations sur les ports hello toowork requis avec récupération de l’espace, consultez toohello [StorSimple mise en réseau des exigences](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* **Améliorations des performances** – mise à jour 3 a amélioré les performances en lecture-écriture toohello cloud.
* **Améliorations de la migration** : dans cette version, plusieurs correctifs de bogues et améliorations ont été apportées pour la fonctionnalité de Migration hello à partir de la série 5000/7000 appareils too8000 série des appareils. Pour plus d’informations sur la façon dont toouse hello la fonctionnalité de migration, visitez trop[Migration à partir de la série 5000/7000 too8000 série un périphérique](https://gallery.technet.microsoft.com/Azure-StorSimple-50007000-c1a0460b). 
* **Analyse des correctifs** : dans cette version, bogues liés toomonitoring graphiques, tableaux de bord de service et tableau de bord de périphérique ont été résolus.

## <a name="issues-fixed-in-update-3"></a>Problèmes résolus dans Update 3
Hello les tableaux suivants fournit un résumé des problèmes qui ont été résolus dans Update 3.    

| Non | Fonctionnalité | Problème | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- |
| 1 |Migration des données côté hôte |Bonjour version antérieure, hello StorSimple Cloud Appliance allait hors connexion lors d’une migration de données du côté hôte. Ce problème a été résolu dans cette version. |Non |Oui |
| 2 |Volumes épinglés localement  |Dans la version précédente de hello, comportaient problèmes connexes tooI/O échecs, les échecs de conversion de volume et chemin de données pour les volumes attachés localement. La cause racine de ces problèmes a été identifiée et ils ont été résolus dans cette version. |Oui |Non |
| 3 |Surveillance |Plusieurs problèmes connexes tooreporting unités se sont produites et d’analyse, ainsi que les graphiques du tableau de bord de l’appareil où des informations incorrectes sont affichées pour localement épinglé volumes. Ces problèmes ont été résolus dans cette version. |Oui |Non |
| 4 |E/S à haut volume d’écritures |Lorsque vous utilisez StorSimple pour les charges de travail qui impliquent des écritures lourde, utilisateur de hello exécuteraient dans un bogue peu fréquent où jeu de travail hello a été à plusieurs niveaux dans le cloud de hello. Ce bogue est résolu dans cette version. |Oui |Oui |
| 5 |Sauvegarde |Dans certains cas rares, dans les versions précédentes de hello de logiciels, lorsque l’utilisateur d’effectuer une sauvegarde d’un clone à distance, ils sont des erreurs de cloud et les opération hello sont d’erreur. Dans cette version, hello est résolu et hello terminée avec succès. |Oui |Oui |
| 6 |Stratégie de sauvegarde |Dans certains cas rares, Bonjour les versions antérieures du logiciel, il a été un bogue lié toohello la suppression de la stratégie de sauvegarde. Ce problème a été résolu dans cette version. |Oui |Oui |

## <a name="known-issues-in-update-3"></a>Problèmes connus dans Update 3
Hello tableau suivant fournit un résumé des problèmes connus dans cette version.

| Non. | Fonctionnalité | Problème | Commentaires/Solution de contournement | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- | --- |
| 1 |Disque quorum |Dans de rares cas, si la majorité de hello des disques du boîtier EBOD de hello d’un appareil 8600 se déconnectent et où aucun quorum de disque, puis pool de stockage hello passera en mode hors connexion. Il restera hors connexion, même si les disques hello sont reconnectés. |Vous devrez le périphérique de hello tooreboot. Si hello problème persiste, contactez le Support technique de Microsoft pour les étapes suivantes. |Oui |Non |
| 2 |ID de contrôleur incorrect |Lorsqu’un contrôleur est remplacé, le contrôleur 0 peut apparaître comme contrôleur 1. Pendant le remplacement de contrôleur, lors de l’image de hello est chargée à partir du nœud d’homologue hello, ID de contrôleur hello permettre s’afficher d’abord en tant qu’ID. du contrôleur hello homologue Dans de rares cas, ce comportement peut également se produire après un redémarrage du système. |Aucune action utilisateur n’est requise. Cette situation se résoudra de lui-même après le remplacement du contrôleur hello. |Oui |Non |
| 3 |Comptes de stockage |À l’aide du compte de stockage du service toodelete hello hello stockage est un scénario non pris en charge. Cela entraîne une situation tooa dans lequel les données de l’utilisateur ne peut pas être récupérées. | |Oui |Oui |
| 4 |Basculement de l’appareil |Basculements multiples d’un conteneur de volume à partir de hello même équipements toodifferent appareil source n’est pas pris en charge. Basculement à partir d’un seul morts toomultiple périphériques rend les conteneurs de volumes hello sur hello appareil basculé tout d’abord perdent la propriété de données. Après un tel basculement, ces conteneurs de volumes apparaît ou se comportent différemment lorsque vous les affichez dans hello portail Azure classic. | |Oui |Non |
| 5 |Installation |Au cours de l’adaptateur StorSimple pour l’installation de SharePoint, vous devez tooprovide une adresse IP dans l’ordre pour hello installation toofinish appareil avec succès. | |Oui |Non |
| 6 |Proxy web |Si votre configuration du proxy web a HTTPS comme hello spécifié de protocole, puis votre appareil au service communication est affectée et les appareils de hello passera en mode hors connexion. Prise en charge les packages sont également générés dans le processus de hello, consomment des ressources importantes sur votre appareil. |Assurez-vous que les URL du proxy web hello a HTTP comme hello protocole spécifié. Pour plus d’informations, consultez trop[configurer un proxy web pour votre appareil](storsimple-configure-web-proxy.md). |Oui |Non |
| 7 |Proxy web |Si vous configurez et activez le proxy web sur un appareil inscrit, puis vous devez contrôleur actif de toorestart hello sur votre appareil. | |Oui |Non |
| 8 |Latence de cloud élevée et charge de travail d’E/S élevée |Lorsque votre appareil StorSimple rencontre une combinaison de latences cloud très élevées (ordre de secondes) et la charge de travail d’e/s élevée, volumes du dispositif hello passe dans un état dégradé et hello e/s peut-être échouer avec une erreur « appareil non prêt ». |Vous devez contrôleurs d’appareil toomanually redémarrage hello ou effectuer une toorecover de basculement de périphérique à partir de cette situation. |Oui |Non |
| 9 |Azure PowerShell |Lorsque vous utilisez l’applet de commande StorSimple hello **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object - tout d’abord 1 - attente** tooselect hello premier objet afin que vous pouvez créer un nouveau **VolumeContainer** de l’objet, hello applet de commande retourne tous les objets de hello. |Retour à la ligne hello applet de commande entre parenthèses comme suit : **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - tout d’abord 1 - attente** |Oui |Oui |
| 10 |Migration |Lorsque plusieurs conteneurs de volumes sont transmis pour la migration, hello ATE pour la sauvegarde la plus récente est exacte uniquement pour le premier conteneur de volume hello. En outre, la migration parallèle démarre une fois hello 4 premières sauvegardes dans le conteneur de volume premier hello sont migrés. |Nous vous recommandons de migrer un seul conteneur de volumes à la fois. |Oui |Non |
| 11 |Migration |Après la restauration de hello, les volumes ne sont pas ajoutés toohello sauvegarde hello ou stratégie de groupe de disque virtuel. |Vous devez tooadd ces stratégie de sauvegarde tooa volumes dans les sauvegardes de toocreate de commande. |Oui |Oui |
| 12 |Migration |Une fois la migration de hello terminée, appareil de série hello 5000/7000 ne doit pas accéder hello migrés des conteneurs de données. |Nous vous recommandons de supprimer hello migré les conteneurs de données après la migration hello est terminé et validé. |Oui |Non |
| 13. |Clonage et récupération d’urgence |Un appareil StorSimple 1 de la mise à jour en cours d’exécution ne peut pas cloner ou effectuer l’appareil de tooa de récupération d’urgence avant mise à jour des 1 logiciels en cours d’exécution. |Vous devez tooupdate hello cible appareil tooUpdate 1 tooallow ces opérations |Oui |Oui |
| 14 |Migration |La sauvegarde de la configuration pour la migration peut être mise en échec sur un appareil de série 5000-7000 lorsqu’aucun volume n’est associé à certains groupes de volumes. |Supprimer tous les groupes de volumes vides hello avec aucun des volumes associés, puis réessayez sauvegarde de configuration hello. |Oui |Non |
| 15 |Applets de commande Azure PowerShell et volumes épinglés localement |Vous ne pouvez pas créer un volume épinglé localement via les applets de commande Azure PowerShell. (Tous les volumes que vous créez via Azure PowerShell sont hiérarchisés.) |Utilisez toujours les volumes tooconfigure attaché localement hello StorSimple Manager. |Oui |Non |
| 16 |Espace disponible pour les volumes épinglés localement |Si vous supprimez un volume attaché localement, espace hello disponible pour les nouveaux volumes ne peut pas être mis à jour immédiatement. mises à jour de service de StorSimple Manager Hello hello espace local disponible toutes les heures environ. |Attendre une heure avant d’essayer de nouveau volume de toocreate hello. |Oui |Non |
| 17 |Volumes épinglés localement  |Votre travail de restauration expose de sauvegarde d’instantanés temporaires hello Bonjour catalogue de sauvegarde, mais uniquement pour la durée de hello du travail de restauration hello. En outre, elle expose un groupe de disques virtuels avec le préfixe **tmpCollection** sur hello **stratégies de sauvegarde** page, mais uniquement pour la durée hello Hello le travail de restauration. |Ce comportement peut se produire si votre travail de restauration possède des volumes épinglés localement ou une combinaison de volumes épinglés localement et de volumes hiérarchisés. Si le travail de restauration hello inclut uniquement les volumes hiérarchisés, ce comportement n’a pas lieu. Aucune intervention de l’utilisateur n’est nécessaire. |Oui |Non |
| 18 |Volumes épinglés localement  |Si vous annulez un travail de restauration et un basculement de contrôleur se produit immédiatement par la suite, le travail de restauration hello affichera **n’a pas pu** au lieu de **annulé**. Si un travail de restauration échoue et un basculement de contrôleur se produit immédiatement par la suite, le travail de restauration hello affichera **annulé** au lieu de **n’a pas pu**. |Ce comportement peut se produire si votre travail de restauration possède des volumes épinglés localement ou une combinaison de volumes épinglés localement et de volumes hiérarchisés. Si le travail de restauration hello inclut uniquement les volumes hiérarchisés, ce comportement n’a pas lieu. Aucune intervention de l’utilisateur n’est nécessaire. |Oui |Non |
| 19 |Volumes épinglés localement  |Si vous annulez un travail de restauration ou si une restauration échoue, un basculement de contrôleur se produit, un travail de restauration supplémentaires s’affiche sur hello **travaux** page. |Ce comportement peut se produire si votre travail de restauration possède des volumes épinglés localement ou une combinaison de volumes épinglés localement et de volumes hiérarchisés. Si le travail de restauration hello inclut uniquement les volumes hiérarchisés, ce comportement n’a pas lieu. Aucune intervention de l’utilisateur n’est nécessaire. |Oui |Non |
| 20 |Volumes épinglés localement  |Si vous essayez de tooconvert un volume hiérarchisé (créé et cloné avec mise à jour 1.2 ou version antérieur) tooa localement épinglé volume votre appareil espace est insuffisant ou une coupure de cloud, puis hello onglet « clone » peut être endommagé. |Ce problème se produit uniquement avec les volumes qui ont été créés et clonés avec un logiciel antérieur à Update 2.1. Il s'agit d'un scénario peu fréquent. | | |
| 21 |Conversion des volumes |Ne pas actualiser hello ACR attaché tooa volume lors de la conversion d’un volume est en cours d’exécution (toolocally hiérarchisé épinglée ou vice versa). Mise à jour hello ACR peut entraîner une altération des données. |Si nécessaire, mettre à jour de la conversion du volume hello ACR toohello préalable mais ne rendez pas d’autres mises à jour de l’ACR pendant la conversion de hello. | | |
| 22 |Mises à jour |Lorsque vous appliquez la mise à jour 3, hello **Maintenance** page Bonjour va de portail classique Azure suivants de hello d’affichage de messages connexe tooUpdate 2 - « StorSimple 8000 series Update 2 inclut la capacité hello pour collecter des tooproactively Microsoft enregistrer des informations à partir de votre appareil quand nous détectons des problèmes potentiels ». Cela s’avère trompeur car elle indique que cet appareil hello est en cours de mise à jour tooUpdate 2. Une fois l’appareil de hello succeesfully mis à jour tooUpdate 3, le message disparaît. |Ce problème sera résolu dans une prochaine version. |Oui |Non |

## <a name="controller-and-firmware-updates-in-update-3"></a>Mises à jour du contrôleur et du microprogramme dans Update 3
Cette version contient des mises à jour du microprogramme et du pilote LSI. Pour plus d’informations sur comment pilote de hello LSI tooinstall et mises à jour du microprogramme, consultez [installer la mise à jour 3](storsimple-install-update-3.md) sur votre appareil StorSimple.

## <a name="virtual-device-updates-in-update-3"></a>Mises à jour des appareils virtuels dans Update 3
Cette mise à jour ne peut pas être appliqué toohello StorSimple Appliance de Cloud (également appelé un périphérique virtuel hello). Nouveaux périphériques virtuels devez toobe créé. 

## <a name="next-step"></a>Étape suivante
Découvrez comment trop[installer la mise à jour 3](storsimple-install-update-3.md) sur votre appareil StorSimple.

