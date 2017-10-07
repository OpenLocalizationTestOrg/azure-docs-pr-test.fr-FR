---
title: "aaaStorSimple localement épinglé Forum aux questions sur les volumes | Documents Microsoft"
description: "Fournit des elles sonttrop des réponses forum de questions StorSimple localement épinglé volumes."
services: storsimple
documentationcenter: NA
author: manuaery
manager: syadav
editor: 
ms.assetid: 7a2f4b1a-4ac9-4ce1-9359-bd40a9cbbb5d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/11/2017
ms.author: manuaery
ms.openlocfilehash: 6a0c742acea836c2b960cb604e4010bcb08c3169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-locally-pinned-volumes-frequently-asked-questions-faq"></a>Volumes StorSimple épinglés localement : forum aux questions (FAQ)
## <a name="overview"></a>Vue d'ensemble
Hello Voici les questions et réponses que vous avez peut-être lorsque vous créez un volume StorSimple attaché localement, convertir un volume de tooa attaché localement volume hiérarchisé (et vice versa), ou sauvegarder et restaurer un volume attaché localement.

Questions et réponses sont organisées en hello suivant des catégories

* Création d’un volume épinglé localement
* Sauvegarde d’un volume épinglé localement
* Conversion d’un volume attaché localement de tooa de volume hiérarchisé
* Restauration d’un volume épinglé localement
* Basculement d’un volume épinglé localement

## <a name="questions-about-creating-a-locally-pinned-volume"></a>Questions sur la création d’un volume épinglé localement
**Q.** Quelle est la taille maximale de hello d’un volume attaché localement sur les périphériques série 8000 hello puis-je créer ?

**A** sur les appareils StorSimple 8000 Series Update 3.0 en cours d’exécution, vous pouvez configurer les volumes attachés localement des too8.5 To ou des volumes hiérarchisés jusqu'à to too200 sur l’appareil 8100 de hello. Sur l’appareil 8600 supérieure de hello, vous pouvez configurer les volumes attachés localement des too22.5 To ou des volumes hiérarchisés jusqu'à too500 to.    
Sur les appareils exécutant la mise à jour de la série StorSimple 8000 2.x, vous pouvez configurer les volumes attachés localement jusqu'à too8 to ou des volumes hiérarchisés jusqu'à to too200 sur l’appareil de hello 8100. Sur l’appareil 8600 supérieure de hello, vous pouvez configurer les volumes attachés localement jusqu'à too20 to ou des volumes hiérarchisés jusqu'à too500 to.   

**Q.** J’ai mon tooUpdate d’appareil 8100 2.0 récemment mis à niveau et lorsque vous essayez de toocreate un volume attaché localement, taille maximale disponible de hello est uniquement 6 et pas 8 To. Pourquoi ne puis-je pas créer un volume de 8 To ?

**A** si votre appareil exécute la mise à jour 2.0, vous pouvez configurer les volumes attachés localement jusqu'à too8 to ou des volumes hiérarchisés jusqu'à to too200 sur hello appareil 8100. Si votre appareil a déjà des volumes hiérarchisé, espace hello disponible pour la création d’un volume attaché localement sera proportionnellement inférieure à cette limite maximale. Par exemple, si 100 To de volumes hiérarchisés a déjà été configurée sur votre appareil 8100 (qui est la moitié des hello multi-niveau la capacité), taille maximale de hello d’un volume local que vous pouvez créer sur l’appareil de hello 8100 sera to too4 relativement réduit (environ la moitié de nombre maximal de Hello localement épinglé capacité du volume).

Espace local sur le périphérique de hello étant hello utilisé toohost jeu de travail de volumes hiérarchisés, hello d’espace disponible pour la création d’un volume attaché localement est réduit si l’appareil de hello a hiérarchisé volumes. À l’inverse, la création d’un volume attaché localement proportionnellement réduit d’espace disponible pour les volumes hiérarchisés hello. Hello les tableaux suivants résume hello à plusieurs niveaux d’une capacité sur les appareils hello 8100 et 8600 lorsque les volumes attachés localement sont créés.

####<a name="update-30"></a>Update 3.0 
| Capacité configurée pour les volumes épinglés localement | Toobe de capacité disponible configuré pour les volumes hiérarchisés - 8100 | Toobe de capacité disponible configuré pour les volumes hiérarchisés - 8600 |
| --- | --- | --- |
| 0 |200 To |500 To |
| 1 To |176,5 To |477,8 To |
| 4 To |105,9 To |411,1 To |
| 8,5 To |0 To |311,1 To |
| 10 To |N/D |277,8 To |
| 15 To |N/D |166,7 To |
| 22,5 To |N/D |0 To |

####<a name="update-2x"></a>Update 2.x  
 | Capacité configurée pour les volumes épinglés localement | Toobe de capacité disponible configuré pour les volumes hiérarchisés - 8100 | Toobe de capacité disponible configuré pour les volumes hiérarchisés - 8600 |  
 | --- | --- | --- |  
 | 0 |200 To |500 To |  
 | 1 To |25 To |475 To |  
 | 4 To |100 To |400 To |  
 | 8 To |0 To |300 To |  
 | 10 To |N/D |250 To |  
 | 15 To |N/D |125 To |  
 | 20 To |N/D |0 To |   

**Q.** Pourquoi la création d’un volume épinglé localement est-elle une opération longue ? 

**A.** Les volumes épinglés localement sont configurés complètement. espace toocreate sur hello niveaux locales de l’appareil de hello, certaines données à partir de volumes hiérarchisés existants peuvent être intégrées à toohello cloud pendant hello processus de configuration. Et car cela dépend de taille hello du volume de hello en cours d’approvisionnement, les données existantes hello sur votre cloud toohello de la bande passante disponible hello et des appareils, les temps de hello toocreate qu'un volume local peut prendre plusieurs heures.

**Q.** Combien de temps faut-il toocreate un volume attaché localement ?

**A.** Étant donné que les volumes attachés localement sont approvisionnés, certaines données existantes à partir de volumes hiérarchisés peuvent être intégrées à toohello cloud pendant hello processus de configuration. Par conséquent, toocreate de durée hello un volume attaché localement dépend de plusieurs facteurs, notamment la taille de hello du volume de hello, hello des données sur votre appareil et hello la bande passante disponible. Sur un appareil nouvellement installé n’a aucun volume, hello temps toocreate un volume attaché localement est environ 10 minutes par téraoctet de données. Toutefois, la création de volumes locales peut prendre plusieurs heures en fonction de facteurs hello expliqués ci-dessus sur un périphérique qui est en cours d’utilisation.

**Q.** Je veux toocreate un volume attaché localement. Quelles sont les meilleures pratiques que je dois toobe prenant en charge de ?

**A.** Les volumes attachés localement ne conviennent pas pour les charges de travail qui requièrent des garanties locales des données en permanence et qui sont sensibles toocloud latences. En prenant en compte l’utilisation des volumes locaux pour un de vos charges de travail, soyez conscient des éléments suivants de hello :

* Les volumes attachés localement sont approvisionnés et création de volumes locales a un impact sur d’espace disponible pour les volumes hiérarchisés hello. Par conséquent, nous vous conseillons de commencer par des volumes de petite taille et de monter en puissance au fur et à mesure que vos besoins de stockage augmentent.
* L’approvisionnement des volumes locaux est une longue opération qui peut impliquer la transmission des données existantes de cloud toohello de volumes hiérarchisés. Par conséquent, les performances sur ces volumes peuvent se trouver amoindries.
* La configuration des volumes locaux est une opération longue. temps réel de Hello impliqués dépend de plusieurs facteurs : hello la taille du volume hello en cours d’approvisionnement, les données sur votre appareil et la bande passante disponible. Si vous n’avez pas sauvegardé votre cloud de toohello volumes existant, la création du volume est plus lente. Nous vous suggérons de prendre des instantanés cloud de vos volumes existants avant de configurer un volume local.
* Vous pouvez convertir des volumes de toolocally épinglé volumes hiérarchisés existants, et cette conversion implique la configuration de l’espace sur l’appareil hello pour hello résultant de volume attaché localement (dans toobringing Ajout des données à plusieurs niveaux [le cas échéant] à partir du cloud de hello). Là encore, il s’agit d’une opération longue qui dépend des facteurs dont nous avons parlé plus haut. Nous vous suggérons de sauvegarder votre tooconversion préalable volumes existants comme processus de hello sera encore plus lente si les volumes existants ne sont pas sauvegardés. Les performances de votre appareil peuvent également être limitées pendant ce processus.

Plus d’informations sur la façon de trop[créer un volume attaché localement](storsimple-manage-volumes-u2.md#add-a-volume)

**Q.** Puis-je créer plusieurs volumes attachés localement à hello même temps ?

**A.** Oui, mais tous les travaux de création et d’extension d’un volume épinglé localement sont traités de manière séquentielle.

Les volumes attachés localement sont approvisionnés et cela nécessite la création d’un espace local sur l’appareil hello (ce qui peut entraîner des données existantes à partir de toobe volumes hiérarchisés intégrés à toohello cloud pendant le processus d’approvisionnement de hello). Par conséquent, si une tâche de configuration est en cours, d’autres tâches de création de volumes locaux seront mises en attente jusqu’à ce que cette tâche soit terminée.

De même, si un volume local en cours d’extension ou un volume hiérarchisé est en cours de conversion tooa localement épinglé volume, puis hello la création d’un nouveau volume attaché localement est en file d’attente jusqu'à ce que la tâche précédente de hello est terminée. Taille hello d’un volume attaché localement de développement implique l’expansion hello d’espace local de hello existante pour ce volume. Conversion d’un volume hiérarchisé toolocally épinglé implique également la création de hello d’espace local pour hello résultant de volume attaché localement. Dans ces deux opérations, la création ou l’extension de l’espace local est une tâche de longue haleine.

Vous pouvez afficher ces travaux Bonjour **travaux** page Hello service Azure StorSimple Manager. Hello travail activement en cours de traitement est continuellement mis à jour de progression de hello tooreflect d’allocation d’espace. Hello restant des tâches de volume attaché localement est marquée comme en cours d’exécution, mais leur progression est bloquée et qu’ils sont collectés dans l’ordre de hello qu’ils ont été en file d’attente.

**Q.** J’ai supprimé un volume épinglé localement. Pourquoi ne puis-je pas voir espace de hello récupéré reflétées dans l’espace disponible de hello lors de le toocreate un nouveau volume ? 

**A.** Si vous supprimez un volume attaché localement, espace hello disponible pour les nouveaux volumes ne peut pas être mis à jour immédiatement. Hello Service StorSimple Manager met à jour un espace local hello disponible toutes les heures environ. Nous vous suggérons de qu'attendre une heure avant d’essayer de nouveau volume de toocreate hello.

**Q.** Les volumes attachés localement sont pris en charge sur l’équipement de cloud hello ?

**A.** Les volumes attachés localement ne sont pas pris en charge sur l’équipement de cloud hello (8010 et 8020 appareils tooas anciennement référencé hello périphérique virtuel StorSimple).

**Q.** Puis-je utiliser toocreate d’applets de commande PowerShell Azure hello et gérer les volumes attachés localement ? 

**A.** Non, il est impossible de créer des volumes épinglés localement avec les applets de commande Azure PowerShell (tous les volumes que vous créez à l’aide d’Azure PowerShell sont hiérarchisés). Il est conseillé de ne pas utiliser toomodify d’applets de commande PowerShell Azure hello toutes les propriétés d’un volume attaché localement, car il sera ont hello effet indésirable de modification tootiered de type hello volume.

## <a name="questions-about-backing-up-a-locally-pinned-volume"></a>Questions sur la sauvegarde d’un volume épinglé localement
**Q.** Les instantanés locaux des volumes épinglés localement sont-ils pris en charge ?

**A.** Oui, vous pouvez prendre des instantanés locaux de vos volumes épinglés localement. Toutefois, nous recommandons vivement que vous régulièrement sauvegarder vos volumes attachés localement avec tooensure instantanés cloud vos données protégées de hello l’éventualité d’un sinistre.

**Q.** Existe-t-il des instructions spécifiques pour la gestion des instantanés locaux des volumes épinglés localement ?

**A.** Les instantanés locaux fréquents avec un taux élevé de données d’évolution du Bonjour localement volume attaché peut entraîner d’espace local sur hello appareil toobe est consommé rapidement et produire des données à partir de volumes hiérarchisés lancés toohello cloud. Par conséquent, nous vous suggérons que vous réduisez le nombre de hello d’instantanés locaux.

**Q.** J’ai reçu une alerte indiquant que mes instantanés locaux des volumes épinglés localement peuvent être rendus non valides. Quand cela peut-il se produire ?

**A.** Les instantanés locaux fréquents avec un taux élevé de données d’évolution du Bonjour localement volume attaché font que l’espace local sur hello appareil toobe est consommé rapidement. Si les niveaux de local hello du périphérique de hello sont utilisées de manière intensive appareil hello saturation peut entraîner une indisponibilité de l’étendue de cloud et volume de toohello écritures entrant peut entraîner l’invalidation d’instantanés de hello (tel qu’aucun espace n’existe tooupdate hello instantanés toorefer toohello plus anciens blocs de données qui ont été remplacées). Dans une telle hello de situation écritures toohello volume va continuer toobe pris en charge, mais les instantanés locaux hello est peut-être non valides. Il n’existe aucun impact tooyour cloud les instantanés existants.

Avertissement d’alerte Hello est toonotify vous que cette situation pourrez se produire et que vous adressez hello même en temps voulu en examinant les vos instantanés locaux planifie tootake moins fréquents instantanés locaux ou de suppression anciens instantanés locaux qui ne sont plus Obligatoire.

Si les instantanés locaux hello ne sont invalidés, vous recevrez une alerte d’information vous informe que les instantanés locaux hello pour la stratégie de sauvegarde spécifique hello ont été invalidés en même temps que la liste de hello des horodatages des instantanés locaux hello qui ont été invalidés. Ces instantanés seront automatiquement supprimés et vous ne pourra plus être en mesure de tooview dans hello **sauvegarde catalogues** page Bonjour portail Azure classic.

## <a name="questions-about-converting-a-tiered-volume-tooa-locally-pinned-volume"></a>Questions sur la conversion d’un volume attaché localement de tooa de volume hiérarchisé
**Q.** Suis d’observation des certains lenteur sur l’appareil de hello lors de la conversion d’un volume attaché localement de tooa de volume hiérarchisé. Que se passe-t-il ? 

**A.** processus de conversion Hello implique deux étapes : 

1. Configuration de l’espace sur l’appareil hello pour hello bientôt converti attaché localement volume.
2. Téléchargement de toutes les données à plusieurs niveaux à partir de la tooensure de cloud hello local garantit.

Ces deux étapes sont longues opérations qui dépendent de la taille de hello du volume de hello en cours de conversion, les données sur le périphérique de hello et la bande passante disponible en cours d’exécution. Comme certaines données à partir de volumes hiérarchisés existants peuvent déborder toohello cloud dans le cadre du processus d’approvisionnement de hello, votre appareil peut rencontrer une baisse des performances pendant ce temps. En outre, le processus de conversion hello peut être plus lente si :

* Les volumes existants n'ont pas été sauvegardés toohello cloud ; donc nous vous suggérons de que sauvegarde de votre tooinitiating préalable de volumes une conversion.
* Stratégies de limitation de bande passante ont été appliquées, ce qui peut freiner le cloud de toohello hello la bande passante disponible ; Nous vous recommandons par conséquent, que vous avez un 40 Mbps dédié ou plus cloud toohello de connexion.
* processus de conversion Hello peut prendre plusieurs heures d’échéance toohello plusieurs facteurs expliqués ci-dessus ; Par conséquent, nous vous suggérons d’effectuer cette opération pendant les heures non-pics ou sur un tooavoid week-end hello impact sur les clients.

Plus d’informations sur la façon de trop[convertir un volume attaché localement de tooa de volume hiérarchisé](storsimple-manage-volumes-u2.md#change-the-volume-type)

**Q.** Puis-je annuler opération de conversion de volume hello ?

**A.** Non, vous ne pouvez pas hello opération de conversion hello annuler une fois démarrée. Comme indiqué dans la question précédente de hello, sachez hello potentielle des problèmes de performances éventuellement rencontrés pendant le processus de hello et suivez hello meilleures pratiques ci-dessus lorsque vous planifiez la conversion.

**Q.** Que passe-t-il toomy volume si l’opération de conversion hello échoue ?

**A.** Conversion de volume peut échouer en raison de problèmes de connectivité toocloud. Appareil de Hello peut finalement cesser de processus de conversion hello après une série de toobring tentatives infructueuses vers le bas des données transmises à partir du cloud de hello. Dans ce scénario, le type de volume hello continue toobe hello source volume type préalable tooconversion, et :

* Une alerte critique sera déclenché toonotify vous hello volume d’échec de conversion. Plus d’informations sur [alertes connexes toolocally épinglé volumes](storsimple-manage-alerts.md#locally-pinned-volume-alerts)
* Si vous convertissez un volume hiérarchisé tooa attaché localement, volume de hello continue tooexhibit des propriétés d’un volume hiérarchisé comme données peuvent toujours résider sur le cloud de hello. Nous vous suggérons de résoudre les problèmes de connectivité hello et puis réessayez opération de conversion hello.
* De même, lors de la conversion à partir d’un tooa attaché localement à plusieurs niveaux volume échoue, bien que le volume de hello sera marquée comme un volume attaché localement, il fonctionne comme un volume hiérarchisé (car les données peuvent avoir répandu toohello cloud). Toutefois, il continue d’espace sur les couches locales hello toooccupy du périphérique de hello. Cet espace ne sera pas disponible pour les autres volumes épinglés localement. Nous vous suggérons de relancer ce tooensure opération que la conversion du volume hello est terminée et hello d’espace local sur l’appareil de hello peut être récupérée.

## <a name="questions-about-restoring-a-locally-pinned-volume"></a>Questions sur la restauration d’un volume épinglé localement
**Q.** Les volumes épinglés localement sont-ils restaurés instantanément ?

**A.** Oui, les volumes épinglés localement sont restaurés instantanément. Dès que des informations de métadonnées hello pour le volume de hello sont extraite à partir du cloud de hello dans le cadre de l’opération de restauration hello, volume de hello est mis en ligne et accessibles par l’hôte de hello. Toutefois, les garanties locales pour le volume de hello données ne seront pas présentes jusqu'à ce que toutes les données hello a été téléchargé à partir du cloud de hello, vous pouvez rencontrer une diminution des performances sur ces volumes pour la durée de la restauration de hello hello.

**Q.** Combien de temps faut-il toorestore un volume attaché localement ?

**A.** Les volumes attachés localement sont restaurés instantanément et mis en ligne dès que des informations de métadonnées volume hello sont récupérées à partir du cloud de hello, tandis que les données de volume salutation continuent toobe téléchargé en arrière-plan de hello. Cette dernière partie de la restauration hello--les garanties local hello pour obtenir des données de volume hello--est une opération longue et peut prendre plusieurs heures pour tous les toobe de données hello redevient local. Bonjour durée toocomplete Bonjour dépend de plusieurs facteurs, telles que la taille du volume hello en cours de restauration hello et hello la bande passante disponible. Si le volume d’origine hello qui est en cours de restauration a été supprimé, un délai supplémentaire à entreprendre toocreate hello local d’espace sur périphérique hello dans le cadre de l’opération de restauration hello.

**Q.** J’ai besoin toorestore mon existant localement épinglé tooan antérieure cliché instantané de volume (effectuée lorsque le volume de hello a été à plusieurs niveaux). Volume de hello reprend comme niveaux dans ce cas ?

**A.** Non, volume de hello sera restauré en tant qu’un volume attaché localement. Bien que l’heure de toohello de dates lorsque les volumes hello a été à plusieurs niveaux, lors de la restauration des volumes existants, de capture instantanée hello StorSimple utilise toujours type hello de volume sur le disque de hello telle qu’elle existe actuellement.

**Q.** J’ai étendu Mon volume attaché localement récemment, mais j’ai besoin maintenant toorestore hello données tooa heure de volume de hello plus petite taille. Restauration redimensionnera volume actuel de hello et devrai-je tooextend hello taille de hello volume une fois la restauration hello est terminée ?

**A.** Oui, restauration de hello sera redimensionner le volume de hello, et vous devez tooextend hello taille de hello volume après que la restauration hello est terminée.

**Q.** Puis-je modifier le type hello d’un volume pendant la restauration ?

**A.**non, vous ne pouvez pas modifier le type de volume hello pendant la restauration.

* Les volumes qui ont été supprimés sont restaurés en tant que type hello stockée dans l’instantané d’hello.
* Les volumes existants sont restaurés en fonction de leur type actuel, quel que soit le type hello stockée dans l’instantané d’hello (consultez les questions toohello deux précédents).

**Q.** Je dois toorestore Mon volume attaché localement, mais j’ai choisi un point incorrect dans l’instantané. Puis-je annuler opération de restauration en cours hello ?

**A.** Oui, vous pouvez annuler une opération de restauration en cours. état Hello du volume de hello sera restaurée toohello état au démarrage de hello de restauration de hello. Toutefois, toutes les écritures qui ont été apportées toohello volume pendant l’exécution de restauration de hello seront perdues.

**Q.** J’ai commencé une opération de restauration sur un de mes volumes épinglés localement, et maintenant un instantané que je ne me souviens pas avoir créé apparaît dans mon catalogue de file d’attente. À quoi sert-il ?

**A.** Il s’agit d’instantané temporaire de hello créé opération de restauration précédente toohello et qui est utilisé pour la restauration en cas de restauration de hello est annulée ou échoue. Ne supprimez pas cet instantané ; Il sera automatiquement supprimé lorsque la restauration hello est terminée. Ce comportement peut se produire si votre travail de restauration possède des volumes épinglés localement ou une combinaison de volumes épinglés localement et de volumes hiérarchisés. Si le travail de restauration hello inclut uniquement les volumes hiérarchisés, ce comportement n’a pas lieu.

**Q.** Puis-je cloner un volume épinglé localement ?

**A.** Oui, vous pouvez. Toutefois, le volume de hello attaché localement est clonée comme un volume hiérarchisé par défaut. Plus d’informations sur la façon de trop[cloner un volume attaché localement](storsimple-clone-volume-u2.md)

## <a name="questions-about-failing-over-a-locally-pinned-volume"></a>Questions sur le basculement d’un volume épinglé localement
**Q.** J’ai besoin toofail sur mon appareil physique tooanother de périphérique. Mes volumes épinglés localement basculeront-ils sous forme de volumes épinglés localement ou de volumes à plusieurs niveaux ?

**A.** Selon la version du logiciel hello du périphérique cible de hello, les volumes attachés localement sont basculés en tant que :

* Attaché localement si l’appareil cible de hello est en cours d’exécution StorSimple 8000 series update 2
* Niveaux si l’appareil cible de hello est en cours d’exécution StorSimple 8000 série mettre à jour 1.x
* Niveaux si l’appareil cible de hello est hello cloud (version mise à jour 2 ou mettre à jour 1.x)

Plus d’informations sur [le basculement et la récupération d’urgence de volumes épinglés localement en fonction des versions](storsimple-device-failover-disaster-recovery.md#device-failover-across-software-versions)

**Q.** Les volumes épinglés localement sont-ils instantanément restaurés lors de la récupération d’urgence ?

**A.** Oui, les volumes épinglés localement sont restaurés instantanément lors du basculement. Dès que des informations de métadonnées hello pour le volume de hello sont extraite à partir du cloud de hello dans le cadre de l’opération de basculement hello, volume de hello est mis en ligne sur l’appareil cible de hello et est accessible par l’hôte de hello. Pendant ce temps, toodownload des données de volume hello se poursuit en arrière-plan de hello, et vous pouvez rencontrer une baisse des performances sur ces volumes pour la durée de basculement de hello hello.

**Q.** Je vois fin du travail de basculement hello, comment puis-je suivre l’avancement hello de volume attaché localement qui est en cours de restauration sur l’appareil cible de hello ?

**A.** Pendant une opération de basculement, travail de basculement hello est marquée comme étant terminée une fois que tous les volumes hello basculements hello ont été restaurés et mis en ligne sur l’appareil cible de hello instantanément. Cela inclut tous les volumes attachés localement peuvent avoir été basculés ; Toutefois, les garanties locales des données de hello seront disponibles lorsque toutes les données hello pour le volume de hello a été téléchargé. Vous pouvez suivre la progression de chaque volume attaché localement a été basculé par analyse hello correspondant travaux de restauration qui est créés dans le cadre du basculement de hello. Ces tâches de restauration individuelles sont créées uniquement pour les volumes épinglés localement.

**Q.** Puis-je modifier le type hello d’un volume pendant le basculement ?

**A.** Non, vous ne pouvez modifier le type de volume hello lors d’un basculement. Si vous basculez sur tooanother physique appareil exécutant mise à jour de la série StorSimple 8000 2, des volumes de hello basculeront basé sur le type de volume stocké dans l’instantané d’hello hello. Lors du basculement tooany autres version de l’appareil, consultez la question toohello ci-dessus sur le type de volume hello après un basculement.

**Q.** Puis-je échoue sur un conteneur de volume avec le matériel de cloud toohello volumes attachés localement ?

**A.** Oui, vous pouvez. les volumes Hello attaché localement sont basculés en tant que volumes hiérarchisés. Plus d’informations sur [le basculement et la récupération d’urgence de volumes épinglés localement en fonction des versions](storsimple-device-failover-disaster-recovery.md#considerations-for-device-failover)

