---
title: notes de publication aaaStorSimple 8000 Series Update 2 | Documents Microsoft
description: "Décrit les nouvelles fonctionnalités de hello, des problèmes et solutions de contournement pour StorSimple 8000 Series Update 2."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: e2c8bffd-7fc5-4b77-b632-a4f59edacc3a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 36c75aad900c7b1286a924732967b8ee519a3d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-2-release-notes"></a>Notes de publication de StorSimple série 8000 Update 2
## <a name="overview"></a>Vue d'ensemble
Bonjour notes de publication suivantes décrivent les nouvelles fonctionnalités de hello et identifient les problèmes critiques en suspens hello pour StorSimple 8000 Series Update 2. Ils contiennent également une liste de hello StorSimple logiciels, pilotes et mises à jour du microprogramme de disque inclus dans cette version. 

Mise à jour 2 peut être en cours d’exécution mise en production (GA) ou mise à jour 0.1 via 1.2 de mise à jour de l’appareil StorSimple tooany appliqué. version de l’appareil Hello associée 2 de la mise à jour est 6.3.9600.17673.

Veuillez consulter les informations de hello contenues dans la version de hello notes avant de déployer hello mettre à jour dans votre solution StorSimple.

> [!IMPORTANT]
> * Il prend environ 4 à 7 heures tooinstall cette mise à jour (y compris les mises à jour de Windows hello). 
> * La solution Update 2 contient des mises à jour du logiciel, du microprogramme, du pilote LSI et du microprogramme SSD.
> * Pour les nouvelles versions, vous ne voyiez pas les mises à jour immédiatement, car nous effectuer un déploiement échelonné des mises à jour hello. Revérifiez les mises à jour dans quelques jours, car elles seront bientôt disponibles.
> 
> 

## <a name="whats-new-in-update-2"></a>Nouveautés d'Update 2
Mise à jour 2 introduit hello nouvelles fonctions suivantes.

* **Attaché localement volumes** – dans les versions précédentes de la série de hello StorSimple 8000, blocs de données ont été cloud à plusieurs niveaux toohello basée sur l’utilisation. Il a été tooguarantee aucune façon blocs conservées sur l’ordinateur local. Dans la mise à jour 2, lorsque vous créez un volume, vous pouvez désigner un volume comme principales et attachées localement les données sur le volume ne sera pas toohello hiérarchisé cloud. Instantanés de volumes attachés localement seront toujours copiés cloud toohello pour la sauvegarde afin que le cloud de hello peut être utilisé pour les données d’urgence et de mobilité des fins de récupération. En outre, vous pouvez modifier le type de volume hello (autrement dit, convertir des volumes toolocally épinglé volumes hiérarchisés et convertir localement épinglé volumes tootiered). 
* **Améliorations de périphérique virtuel StorSimple** – précédemment, hello série StorSimple 8000 positionné un appareil virtuel hello comme solution de développement et de test ou de récupération d’urgence. Il n’existait alors qu’un seul modèle d’appareil virtuel (modèle 1100). La solution Update 2 propose deux modèles d’appareil virtuel : 
  
  * 8010 (anciennement appelé hello 1100) – aucune modification ; a une capacité de 30 To et utilise le stockage Azure standard.
  * Le modèle 8020 : il dispose d’une capacité de 64 To et utilise le stockage Premium d’Azure pour de meilleures performances.
    
    Il existe un seul disque dur virtuel pour les deux modèles d’appareil virtuel (8010/8020). Lorsque vous démarrez un appareil virtuel hello, il détecte des paramètres de plateforme hello et applique la version du modèle correct hello.
* **Améliorations de mise en réseau** – mise à jour 2 contient hello suivant des améliorations de la mise en réseau :
  
  * Plusieurs cartes réseau peut être activée pour le cloud de hello afin que le basculement peut se produire si une carte réseau échoue.
  * Améliorations du routage, avec des mesures fixes pour les blocs compatibles avec le cloud.
  * Tentatives en ligne des ressources en cas d’échec avant un basculement.
  * Nouvelles alertes pour les échecs de service.
* **Améliorations de mise à jour** : mettre à jour 1.2 et versions antérieures, série de hello StorSimple 8000 a été mis à jour via deux canaux : mise à jour de Windows pour le clustering, iSCSI et ainsi de suite et Microsoft Update pour les fichiers binaires et de microprogramme.
    Update 2 utilise Microsoft Update pour tous les packages de mise à jour. Cela doit entraîner des temps accessible sans mise à jour corrective ou effectuer des basculements. 
* **Mises à jour de microprogramme** : hello suivants du microprogramme des mises à jour sont inclus :
  
  * LSI: lsi_sas2.sys Version du produit 2.00.72.10
  * Disque SSD uniquement (aucune mise à jour du disque dur) : XMGG, XGEG, KZ50, F6C2 et VR08
* **Prise en charge proactive** – Update 2 permet à Microsoft toopull informations de diagnostic supplémentaires à partir de l’appareil de hello. Lors de notre équipe d’exploitation identifie les appareils qui rencontrent des problèmes, nous sont des informations plus riches toocollect équipés de périphériques de hello et diagnostiquer les problèmes. **En acceptant la mise à jour 2, vous nous permettez tooprovide cette prise en charge proactive**.    

## <a name="issues-fixed-in-update-2"></a>Problèmes résolus dans Update 2
Hello les tableaux suivants fournit un résumé des problèmes qui ont été résolus dans les mises à jour 2.    

| Non. | Fonctionnalité | Problème | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- |
| 1 |Interfaces réseau |Après une mise à niveau 1 de tooUpdate, hello service StorSimple Manager a signalé que les ports Data2 et Data3 hello a échoué sur un seul contrôleur. Ce problème est à présent résolu. |Oui |Non |
| 2 |Mises à jour |Après une mise à niveau 1 de tooUpdate, alertes d’alarme sonore s’est produite dans hello portail classique Azure sur plusieurs appareils. Ce problème est à présent résolu. |Oui |Non |
| 3 |Authentification OpenStack |Lorsque vous utilisiez OpenStack comme fournisseur de services cloud, vous pouviez recevoir une erreur indiquant que la chaîne d'authentification cloud était trop longue. Ce problème a été résolu. |Oui |Non |

## <a name="known-issues-in-update-2"></a>Problèmes connus dans Update 2
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
| 20 |Volumes épinglés localement  |Si vous essayez de tooconvert un volume hiérarchisé (créé et cloné avec mise à jour 1.2 ou version antérieur) tooa localement épinglé volume votre appareil espace est insuffisant ou une coupure de cloud, puis hello onglet « clone » peut être endommagé. |Ce problème se produit uniquement avec les volumes qui ont été créés et clonés avec un logiciel antérieur à Update 2. Il s'agit d'un scénario peu fréquent. | | |
| 21 |Conversion des volumes |Ne pas actualiser hello ACR attaché tooa volume lors de la conversion d’un volume est en cours d’exécution (toolocally hiérarchisé épinglée ou vice versa). Mise à jour hello ACR peut entraîner une altération des données. |Si nécessaire, mettre à jour de la conversion du volume hello ACR toohello préalable mais ne rendez pas d’autres mises à jour de l’ACR pendant la conversion de hello. | | |

## <a name="controller-and-firmware-updates-in-update-2"></a>Mises à jour du contrôleur et du microprogramme dans Update 2
Cette version met à jour le pilote de hello et de microprogramme de disque hello sur votre appareil.

* Pour plus d’informations sur le microprogramme de LSI hello mise à jour, consultez l’article 3121900 de la base de connaissances Microsoft. 
* Pour plus d’informations sur le microprogramme du disque hello mise à jour, consultez l’article 3121899 de la base de connaissances Microsoft.

## <a name="virtual-device-updates-in-update-2"></a>Mises à jour des appareils virtuels dans Update 2
Cette mise à jour ne peut pas être appliqué toohello un appareil virtuel. Nouveaux périphériques virtuels devez toobe créé. 

## <a name="next-step"></a>Étape suivante
Découvrez comment trop[installer la mise à jour 2](storsimple-install-update-2.md) sur votre appareil StorSimple.

