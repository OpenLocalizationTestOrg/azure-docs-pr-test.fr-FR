---
title: "aaaStorSimple 8000 mettre à jour les notes de publication 0,2 | Documents Microsoft"
description: "Décrit les nouvelles fonctionnalités de hello et correctifs, problèmes ouverts et des solutions de contournement disponibles pour hello janvier 2015 mise en production de Microsoft Azure StorSimple (mise à jour 0,2)."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d9684ae3-b38f-4678-9d70-e5dbc6b03350
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: 1cee795df0b53d9b9276bc33074cf1a7aa188835
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-02-release-notes---january-2015"></a>Notes de publication de StorSimple série 8000 Update 0.2 - Janvier 2015
## <a name="overview"></a>Vue d'ensemble
Hello notes de publication suivantes identifient les problèmes critiques ouverts hello pour hello version de janvier 2015 de Microsoft Azure StorSimple. Elles contiennent également une liste de hello StorSimple logiciels et mises à jour de microprogramme inclus dans cette version. Il s’agit de mise en production de la deuxième hello après que la version de StorSimple 8000 Series version hello a été effectuée généralement disponible en juillet 2014.

Cette mise à jour ne modifie pas la version du logiciel hello périphérique physique à partir de la mise à jour de hello octobre. Il continue toobe version 6.3.9600.17312. image Hello utilisée par l’image de périphérique virtuel hello a changé dans cette version. Par conséquent, tous les hello nouveaux appareils virtuels créés après le 20/1/2015 indiquent version de hello 6.3.9600.17361.  

Passez en revue hello suit les informations contenues dans les notes de publication hello pour la mise à jour de janvier 2015 hello.

> [!IMPORTANT]
> * Cette mise à jour n’est pas disponible via Windows Update et ne peut pas être installée comme les autres mises à jour. Votre appareil ne recevra pas cette mise à jour même si vous avez appliqué des mises à jour hello à l’aide de hello portail Azure classic. Cette mise à jour s’applique uniquement aux périphériques toovirtual créés après le 20 janvier 2015. 
> * Hello version de janvier de StorSimple ne contient pas un appareil physique de mises à jour toohello StorSimple. Vous pouvez toujours appliquer n’importe quel disponible Windows mises à jour toohello périphérique virtuel, y compris de sécurité récents correctifs, mais vous ne verrez pas un changement de version à l’appareil physique StorSimple hello.
> 
> 

## <a name="whats-new-in-hello-january-release"></a>Nouveautés de la version de janvier hello
Cette mise à jour contient un correctif liées volumes toohello mise hors connexion sur un appareil virtuel hello. (Voir [Problèmes résolus dans cette version](#issues-fixed-in-the-january-release).)  

mise à jour Hello ne contient pas de nouvelles fonctionnalités ou des fonctionnalités.  

## <a name="issues-fixed-in-hello-january-release"></a>Problèmes résolus dans la version de janvier hello
Hello tableau suivant décrit hello problème a été résolu dans cette mise à jour.

| Non. | Fonctionnalité | Problème | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- |
| 1 |Les volumes se mettent hors connexion |Lorsque les latences élevées cloud persistent pendant plusieurs minutes, les volumes de périphérique virtuel StorSimple hello mis hors connexion sur les ordinateurs hôtes de hello. Ce correctif augmente le seuil hello de latences du cloud, réduisant ainsi les situations hello qui provoquent l’hello volumes toogo hors connexion sur les ordinateurs hôtes. |Non |Oui |

## <a name="known-issues-in-hello-january-release"></a>Problèmes connus dans la version de janvier hello
Hello tableau suivant fournit un résumé des problèmes connus dans cette version.

| Non. | Fonctionnalité | Problème | Commentaires/solution de contournement | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- | --- |
| 1 |Réinitialisation aux paramètres d’usine |Dans certains cas, lorsque vous effectuez une réinitialisation des paramètres, hello appareil StorSimple peut se bloquer et afficher le message : **toofactory de réinitialisation est en cours (phase 8).** Cela se produit si vous appuyez sur CTRL + C lors de l’applet de commande hello est en cours d’exécution. |N’appuyez pas sur Ctrl+C après avoir lancé une réinitialisation aux paramètres d’usine. Si vous avez déjà effectué cette opération, contactez le support technique Microsoft. |Oui |Non |
| 2 |Disque quorum |Dans de rares cas, si la majorité de hello des disques du boîtier EBOD de hello d’un appareil 8600 se déconnectent et où aucun quorum de disque, puis pool de stockage hello sera hors connexion. Il restera hors connexion, même si les disques hello sont reconnectés. |Vous devrez le périphérique de hello tooreboot. Si hello problème persiste, contactez le Support technique de Microsoft pour les étapes suivantes. |Oui |Non |
| 3 |Échec des instantanés cloud |Dans de rares cas, un instantané cloud peut échouer avec l’erreur de hello **limite de sauvegarde maximale atteinte**. Cela se produit si vous dépassez 255 clones en ligne sur hello même appareil et hello même volume d’origine qui a été supprimée. | |Oui |Oui |
| 4 |ID de contrôleur incorrect |Lorsqu’un contrôleur est remplacé, le contrôleur 0 peut apparaître comme contrôleur 1. Pendant le remplacement de contrôleur, lors de l’image de hello est chargée à partir du nœud d’homologue hello, ID de contrôleur hello permettre s’afficher d’abord en tant qu’ID. du contrôleur hello homologue  Dans de rares cas, ce comportement peut également se produire après un redémarrage du système. |Aucune action utilisateur n’est requise. Cette situation se résoudra de lui-même après le remplacement du contrôleur hello. |Oui |Non |
| 5 |Graphiques d’analyse de l’appareil |Bonjour service StorSimple Manager, les graphiques de surveillance de périphérique hello ne fonctionnent pas lors de la base ou l’authentification NTLM est activée dans la configuration du serveur proxy hello pour appareil de hello. |Modifier la configuration du proxy web hello pour appareil hello inscrit auprès du service StorSimple Manager afin que l’authentification a la valeur tooNONE. toodo, hello hello d’exécution Windows PowerShell pour l’applet de commande Set-HcsWebProxy de StorSimple. |Oui |Oui |
| 6 |Comptes de stockage |À l’aide du compte de stockage du service toodelete hello hello stockage est un scénario non pris en charge. Cela entraîne une situation tooa dans lequel les données de l’utilisateur ne peut pas être récupérées. | |Oui |Oui |
| 7 |Basculement de l’appareil |Basculements multiples d’un conteneur de volume à partir de hello même équipements toodifferent appareil source n’est pas pris en charge. |Basculement à partir d’un seul morts toomultiple périphériques rend les conteneurs de volumes hello sur hello appareil basculé tout d’abord perdent la propriété de données. Après un tel basculement, ces conteneurs de volumes apparaît ou se comportent différemment lorsque vous les affichez dans hello portail Azure classic. |Oui |Non |
| 8 |Installation |Au cours de l’adaptateur StorSimple pour l’installation de SharePoint, vous devez tooprovide une adresse IP dans l’ordre pour hello installation toofinish appareil avec succès. | |Oui |Non |
| 9 |Proxy web |Si votre configuration du proxy web a HTTPS comme hello spécifié de protocole, puis votre appareil au service communication est affectée et les appareils de hello passera en mode hors connexion. Prise en charge les packages sont également générés dans le processus de hello, consomment des ressources importantes sur votre appareil. |Assurez-vous que les URL du proxy web hello a HTTP comme hello protocole spécifié. Voir plus d’informations sur la façon de trop[configurer un proxy web pour votre appareil](storsimple-configure-web-proxy.md). |Oui |Non |
| 10 |Proxy web |Si vous configurez et activez le proxy web sur un appareil inscrit, puis vous devez contrôleur actif de toorestart hello sur votre appareil. | |Oui |Non |
| 11 |Latence de cloud élevée et charge de travail d’E/S élevée |Lorsque votre appareil StorSimple rencontre une combinaison de latences cloud très élevées (ordre de secondes) et la charge de travail d’e/s élevée, volumes du dispositif hello passe dans un état dégradé et hello e/s peut-être échouer avec une erreur « appareil non prêt ». |Vous devez contrôleurs d’appareil toomanually redémarrage hello ou effectuer une toorecover de basculement de périphérique à partir de cette situation. |Oui |Non |

## <a name="physical-device-updates-in-hello-january-release"></a>Mises à jour de l’unité physique dans la version de janvier hello
Cette mise à jour ne contient pas de tout autre périphérique de StorSimple de toohello modifications.

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-january-release"></a>Serial attached SCSI (SAS) contrôleur et du microprogramme des mises à jour dans la version de janvier hello
Cette version ne contient pas de n’importe quel contrôleur de mises à jour toohello serial attached SCSI (SAS) ou le microprogramme de hello. mise à jour du pilote Hello a hello octobre, version 2014. 

## <a name="virtual-device-updates-in-hello-january-release"></a>Mises à jour de l’appareil virtuel dans la version de janvier hello
Cette version contient une image mise à jour pour un appareil virtuel hello. Tous les périphériques virtuels hello créés après le 20 janvier 2015 indiquent hello logiciel version 6.3.9600.17361.

