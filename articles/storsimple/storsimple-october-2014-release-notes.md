---
title: "aaaStorSimple 8000 mettre à jour les notes de publication 0,1 | Documents Microsoft"
description: "Décrit les nouvelles fonctionnalités de hello et correctifs, problèmes ouverts et des solutions de contournement disponibles pour hello octobre 2014 mise en production de Microsoft Azure StorSimple (mise à jour 0,1)."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: fd35e3c3-4770-460c-999d-f72ab7053a20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 684e31cb0b356ec59a9d6c245e5d2bc062cc4f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-01-release-notes--october-2014"></a>Notes de publication de StorSimple série 8000 Update 0.1 – Octobre 2014
## <a name="overview"></a>Vue d'ensemble
Hello suivant des notes de mise à identifier les problèmes d’open critiques hello pour la mise à jour de série StorSimple 8000 0,1 publiée en octobre 2014. Elles contiennent également une liste de hello StorSimple logiciels et mises à jour de microprogramme inclus dans cette version. Il s’agit de première version de hello après de la version de StorSimple 8000 Series version hello a été effectuée généralement disponible en juillet 2014 et correspond toosoftware version 6.3.9600.17312.  

Nous vous recommandons de rechercher et d’appliquer les mises à jour disponibles immédiatement après l’installation de périphérique de hello. Vous pouvez également activer toodownload de mises à jour automatiques et installer des mises à jour prioritaires de Microsoft dès qu’ils sont disponibles. Pour plus d’informations, consultez Comment trop[mettre à jour votre appareil StorSimple](storsimple-update-device.md).  

Passez en revue les informations de hello contenues dans les notes de publication hello avant de déployer les mises à jour hello dans votre solution StorSimple.  

> [!IMPORTANT]
> * Utilisez le service StorSimple Manager hello et non Windows PowerShell pour StorSimple tooinstall hello est Qu'octobre met à jour.  
> * mises à jour Hello prennent généralement environ 3 heures toocomplete.  
> * Hello version d’octobre de StorSimple ne contient pas un appareil virtuel de mises à jour toohello StorSimple. Vous pouvez toujours appliquer les mises à jour Windows disponibles, y compris les correctifs de sécurité récents, mais vous ne verrez pas un changement de version pour un appareil virtuel hello.  
> 
> 

Vérifiez que hello après les conditions préalables est rempli tooupdating préalable votre appareil StorSimple.  

* Vérifiez que les deux contrôleurs de l’appareil sont actifs avant de rechercher des mises à jour. Aucun contrôleur ne fonctionne pas, hello analyse échoue. tooverify contrôleurs de hello sont dans un état sain, accédez trop**état du matériel** sous hello **Maintenance** page. Si des composants **nécessitent une attention**, contactez le support technique de Microsoft avant de continuer.  
* Assurez-vous que les adresses IP fixes des contrôleurs 0 et 1 sont routables et peuvent se connecter toohello Internet car elles sont utilisées pour la maintenance des appareils de toohello hello mises à jour. Vous pouvez utiliser hello [applet de commande Test-Connection](https://technet.microsoft.com/library/hh849808.aspx) tooping une adresse connue en dehors du réseau hello, par exemple outlook.com, tooverify qui hello contrôleur a toohello de connectivité en dehors du réseau.  
* Assurez-vous que hello requises des ports sortants sont disponibles sur votre appareil StorSimple pour les communications sortantes. Pour plus d’informations, consultez hello [configuration réseau requise pour votre appareil StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).  
* Si la version du logiciel hello est antérieure à 6.3.9600.17312 (mise à jour d’octobre 2014), désactivez les ports de données 2 et Data 3 des hello, s’il est activé, avant de commencer la mise à jour hello. Si vous laissez hello Data 2 ou 3 ports activés lors de l’application de mise à jour hello, il risque de votre toogo de contrôleur de périphérique en mode de récupération. Notez que lorsque vous désactivez des interfaces réseau de hello, tous les volumes hello associé seront mis hors connexion et pour la durée de mise à jour hello hello hello d’e/s est interrompue.  

## <a name="whats-new-in-hello-october-release"></a>Nouveautés de la version d’octobre hello
Cette mise à jour inclut hello suivant améliorations :

* Vous pouvez maintenant utiliser toomanage de l’interface utilisateur de service de StorSimple Manager hello vos contrôleurs d’appareil. Hello actions de gestion incluent redémarrage, arrêt, ou un contrôleur sous tension. Pour plus d’informations, consultez trop[StorSimple de gérer les contrôleurs de périphérique](storsimple-manage-device-controller.md).  
* Vous pouvez planifier l’allocation de bande passante WAN en fonction de combinaisons tooday de la semaine et heure de la journée. Cela vous permet de toomake améliore l’utilisation de la bande passante WAN pendant les heures creuses. Des modèles de bande passante différents sont autorisés pour des conteneurs de volumes distincts. Pour plus d’informations, consultez trop[gérer vos modèles de bande passante StorSimple](storsimple-manage-bandwidth-templates.md).  
* Vous pouvez configurer des notifications par courrier électronique tooproactively avertir les administrateurs hello et autres problèmes existants ou à venir. Pour plus d’informations, consultez trop[configurer les paramètres d’alerte](storsimple-manage-alerts.md#configure-alert-settings).  

## <a name="issues-fixed-in-hello-october-release"></a>Problèmes résolus dans la version d’octobre hello
Hello tableau suivant fournit un résumé des problèmes qui ont été résolus dans cette mise à jour.  

| Non. | Fonctionnalité | Problème | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- |
| 1 |Interfaces réseau |Bonjour précédente version, les interfaces réseau de hello DATA 2 et 3 étaient interverties dans le logiciel de hello. Ce problème a été résolu dans cette mise à jour. Veuillez effacer hello et désactiver ces interfaces réseau avant d’installer la mise à jour de hello. Après avoir installé la mise à jour hello, vous aurez tooreconfigure de ces interfaces. |Oui |Non |
| 2 |Package de prise en charge |Dans la version précédente de hello, si vous avez exécuté hello Windows PowerShell **Export-HcsSupportPackage** ouvre une applet de commande tooretrieve hello Baseboard Management Controller (BMC), échec avec hello suivant l’avertissement de l’opération hello : hello » opération réussie sur ce contrôleur, mais a échoué sur le contrôleur homologue de hello en raison de toohello suivant (s). Vérifiez si l’homologue de hello est intègre et si le nœud actuel de hello peut se connecter toohello homologue. » » Ce problème est maintenant résolu. |Oui |Non |
| 3 |Basculement de l’appareil |Dans la version précédente de hello, il existait un risque d’incohérence des données, si un **de découvrir une sauvegarde** échouait durant un basculement de l’appareil. » Ce problème est maintenant résolu. |Oui |Non |
| 4 |Basculement de l’appareil |Version hello précédente, après un basculement de l’appareil, les sauvegardes étaient visibles mais conteneur de volumes associé hello n’était pas présent sur l’appareil cible de hello. » Ce problème est maintenant résolu. |Oui |Non |
| 5 |Basculement de l’appareil |Dans la version précédente de hello, il a été un bogue dans l’énumération hello de sauvegardes cloud pendant l’opération de restauration du Registre hello qui pouvait entraîner l’incohérence de toodata si des problèmes de connectivité est cloud. |Oui |Non |
| 6 |Mise à jour du microprogramme |Dans la version précédente de hello, hello travail de mise à jour du microprogramme de périphérique a échoué et affiche une erreur qui indiquait que les applets de commande hello n’étaient pas reconnaissables, et cette mise à jour hello a échoué en conséquence. contrôleur de Hello passait ensuite en mode de récupération. » Ce problème est maintenant résolu. |Oui |Non |
| 7 |Installation |Les erreurs provoquées par périphérique hello ne pas une mise en image correctement lors de l’installation ont été résolus. |Oui |Non |
| 8 |Réinitialisation aux paramètres d’usine |Vous pouvez maintenant éventuellement ignorer la vérification du microprogramme de hello pour les paramètres d’usine. Il s’agit d’une modification à partir de la version précédente de hello. |Oui |Non |
| 9 |Réinitialisation aux paramètres d’usine |Dans la version précédente de hello, lors de l’exécution d’une applet de commande de réinitialisation de fabrique, version du microprogramme uniquement pour certains composants matériels ont été apporté. Vérifications de microprogramme supplémentaires ont été apportées après le redémarrage de première hello dans les processus de hello, qui peut provoquer le toofail de réinitialisation hello. Ce correctif garantit que toutes les vérifications de microprogramme hello effectuées au moment de l’applet de commande hello fabrique réinitialisation est exécutée et avant hello premier système de redémarrer. |Oui |Non |
| 10 |Rotation des clés du compte de stockage |Hello **Invoke-HcsmServiceDataEncryptionKeyChange** applet de commande utilisé clés de compte de stockage toorotate hello maintenant invites hello utilisateur tooenter hello clé de chiffrement. Il s’agit d’une modification à partir de la version précédente de hello dans le hello clé de chiffrement de données de service a été passé comme paramètre inline. |Oui |Non |
| 11 |Restauration automatique dans les 24 heures |Lors de la récupération d’urgence, nettoyage hello sur le périphérique source de hello n’était pas effectué la restauration automatique proprement, entraînant le toofail. Ce problème a été résolu dans cette version. |Oui |Non |

## <a name="known-issues-in-hello-october-release"></a>Problèmes connus dans la version d’octobre hello
Hello tableau suivant fournit un résumé des problèmes connus dans cette version.

| Non. | Fonctionnalité | Problème | Commentaires/solution de contournement | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- | --- |
| 1 |Réinitialisation aux paramètres d’usine |Dans certains cas, lorsque vous effectuez une réinitialisation des paramètres, hello appareil StorSimple peut se bloquer et afficher le message : **toofactory de réinitialisation est en cours (phase 8)**. Cela se produit si vous appuyez sur CTRL + C lors de l’applet de commande hello est en cours d’exécution. |N’appuyez pas sur Ctrl+C après avoir lancé une réinitialisation aux paramètres d’usine. Si vous avez déjà effectué cette opération, contactez le support technique Microsoft. |Oui |Non |
| 2 |Réinitialisation aux paramètres d’usine |Effectuez pas d’usine un appareil StorSimple mis à jour à partir de la version de GA tooOctober 2014. |Cette opération fonctionne uniquement si un correctif est installé. Ce correctif requis, contactez tooget de Support technique de Microsoft. |Oui |Non |
| 3 |Disque quorum |Dans de rares cas, si la majorité de hello des disques du boîtier EBOD de hello d’un appareil 8600 se déconnectent et où aucun quorum de disque, puis pool de stockage hello sera hors connexion. Il restera hors connexion, même si les disques hello sont reconnectés. |Vous devrez le périphérique de hello tooreboot. Si hello problème persiste, contactez le Support technique de Microsoft pour les étapes suivantes. |Oui |Non |
| 4 |Échec des instantanés cloud |Dans de rares cas, un instantané cloud peut échouer avec l’erreur de hello **limite de sauvegarde maximale atteinte**. Cela se produit si vous dépassez 255 clones en ligne sur hello même appareil et hello même volume d’origine qui a été supprimée. | |Oui |Oui |
| 5 |ID de contrôleur incorrect |Lorsqu’un contrôleur est remplacé, le contrôleur 0 peut apparaître comme contrôleur 1. Pendant le remplacement de contrôleur, lors de l’image de hello est chargée à partir du nœud d’homologue hello, ID de contrôleur hello permettre s’afficher d’abord en tant qu’ID. du contrôleur hello homologue Dans de rares cas, ce comportement peut également se produire après un redémarrage du système. |Aucune action utilisateur n’est requise. Cette situation se résoudra de lui-même après le remplacement du contrôleur hello. |Oui |Non |
| 6 |Graphiques d’analyse de l’appareil |Bonjour service StorSimple Manager, les graphiques de surveillance de périphérique hello ne fonctionnent pas lors de la base ou l’authentification NTLM est activée dans la configuration du serveur proxy hello pour appareil de hello. |Modifier la configuration du proxy web hello pour appareil hello inscrit auprès du service StorSimple Manager afin que l’authentification a la valeur tooNONE. toodo, hello hello d’exécution Windows PowerShell pour l’applet de commande Set-HcsWebProxy de StorSimple. |Oui |Oui |
| 7 |Comptes de stockage |À l’aide du compte de stockage du service toodelete hello hello stockage est un scénario non pris en charge. Cela entraîne une situation tooa dans lequel les données de l’utilisateur ne peut pas être récupérées. | |Oui |Oui |
| 8 |Basculement de l’appareil |Basculements multiples d’un conteneur de volume à partir de hello même équipements toodifferent appareil source n’est pas pris en charge. |Basculement à partir d’un seul morts toomultiple périphériques rend les conteneurs de volumes hello sur hello appareil basculé tout d’abord perdent la propriété de données. Après un tel basculement, ces conteneurs de volumes apparaît ou se comportent différemment lorsque vous les affichez dans hello portail Azure classic. |Oui |Non |
| 9 |Installation |Au cours de l’adaptateur StorSimple pour l’installation de SharePoint, vous devez tooprovide une adresse IP dans l’ordre pour hello installation toofinish appareil avec succès. | |Oui |Non |
| 10 |Proxy web |Si votre configuration du proxy web a HTTPS comme hello spécifié de protocole, puis votre appareil au service communication est affectée et les appareils de hello passera en mode hors connexion. Prise en charge les packages sont également générés dans le processus de hello, consomment des ressources importantes sur votre appareil. |Assurez-vous que les URL du proxy web hello a HTTP comme hello protocole spécifié. Plus d’informations sur la façon de trop[configurer un proxy web pour votre appareil](storsimple-configure-web-proxy.md). |Oui |Non |
| 11 |Proxy web |Si vous configurez et activez le proxy web sur un appareil inscrit, puis vous devez contrôleur actif de toorestart hello sur votre appareil. | |Oui |Non |
| 12 |Latence de cloud élevée et charge de travail d’E/S élevée |Lorsque votre appareil StorSimple rencontre une combinaison de latences cloud très élevées (ordre de secondes) et la charge de travail d’e/s élevée, volumes du dispositif hello passe dans un état dégradé et hello e/s peut-être échouer avec une erreur « appareil non prêt ». |Vous devez contrôleurs d’appareil toomanually redémarrage hello ou effectuer une toorecover de basculement de périphérique à partir de cette situation. |Oui |Non |

## <a name="physical-device-updates-in-hello-october-release"></a>Mises à jour de l’unité physique dans la version d’octobre hello
Lorsque ces mises à jour sont appliqués tooa des périphériques physiques, version du logiciel hello change too6.3.9600.17312. Sauf indication contraire, ces notes s’appliquent à des modèles de tooall de l’appareil StorSimple hello. Pour plus d’informations sur ces mises à jour, consultez la page [Mise à jour de l’appareil physique d’octobre 2014 pour Microsoft Azure StorSimple Appliance](http://support.microsoft.com/kb/2986997).  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-october-release"></a>Serial attached SCSI (SAS) contrôleur et du microprogramme des mises à jour dans la version d’octobre hello
Cette version met à jour le pilote de hello et de microprogramme hello sur contrôleur SAS de hello de votre appareil physique. Pour plus d’informations sur la mise à jour du contrôleur hello SAS, consultez [octobre 2014 mise à jour pour les contrôleurs SAS LSI dans Microsoft Azure StorSimple Appliance](http://support.microsoft.com/kb/2987020).   

Cette version s’applique également à une mise à jour de microprogramme cumulative qui résout les problèmes de fiabilité des composants matériels du périphérique hello. Pour plus d’informations sur la mise à jour du microprogramme hello, consultez [mise à jour d’octobre 2014 du microprogramme pour Microsoft Azure StorSimple Appliance](http://support.microsoft.com/kb/2987015).  

## <a name="virtual-device-updates-in-hello-october-release"></a>Mises à jour de l’appareil virtuel dans la version d’octobre hello
Cette version ne contient pas les mises à jour pour un appareil virtuel hello. Appliquer cette mise à jour ne modifie pas la version du logiciel d’un périphérique virtuel hello.

