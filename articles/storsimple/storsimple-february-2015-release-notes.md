---
title: "aaaStorSimple 8000 mettre à jour les notes de publication 0,3 | Documents Microsoft"
description: "Décrit les nouvelles fonctionnalités de hello et correctifs, problèmes ouverts et des solutions de contournement disponibles pour hello février 2015 mise en production de Microsoft Azure StorSimple (mise à jour 0.3)."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: b01bfd04-f9f8-45f4-ade8-95ac2b979e6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 53638f9d286b2085c6b45f9e3fae75c34fc73e7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-03-release-notes---february-2015"></a>Notes de publication de StorSimple série 8000 Update 0.3 - Février 2015
## <a name="overview"></a>Vue d'ensemble
Hello suivant des notes de mise à identifier les problèmes d’open critiques hello pour la mise à jour de série StorSimple 8000 0,3 publiée en février 2015. Elles contiennent également une liste de hello StorSimple logiciels et mises à jour de microprogramme inclus dans cette version. Il s’agit de mise en production de la troisième hello après que la version de StorSimple 8000 Series version hello a été effectuée généralement disponible en juillet 2014.

Cette mise à jour ne modifie pas la version du logiciel hello à partir de la mise à jour de janvier hello. Il continue toobe version 6.3.9600.17312. Vous pouvez vérifier cette mise à jour hello a été installé en vérifiant hello **dernière mise à jour** date. Si la date de hello est 2/10/2015 ou version ultérieure, mise à jour hello a été installé avec succès.  

Nous vous recommandons de rechercher les mises à jour éventuelles et de les appliquer immédiatement après avoir installé l’appareil StorSimple. Vous pouvez également activer toodownload de mises à jour automatiques et installer des mises à jour prioritaires de Microsoft dès qu’ils sont disponibles. Pour plus d’informations, consultez [Mise à jour de votre appareil StorSimple](storsimple-update-device.md).  

Veuillez consulter les informations de hello contenues dans la version de hello notes avant de déployer hello mettre à jour dans votre solution StorSimple.  

> [!IMPORTANT]
> * Utilisez le service StorSimple Manager hello et non Windows PowerShell pour la mise à jour de StorSimple tooinstall hello février.   
> * Il prend environ une tooinstall heure cette mise à jour. Toutefois, si vous installez des mises à jour cumulatives, hello peut durer environ 3 heures toocomplete.  
> * Hello version de février de StorSimple ne contient pas un appareil virtuel de mises à jour toohello StorSimple. Vous pouvez toujours appliquer n’importe quel disponible Windows mises à jour toohello périphérique virtuel, y compris de sécurité récents correctifs, mais vous ne verrez pas un changement de version pour un appareil virtuel hello.  
> 
> 

Vérifiez que hello après les conditions préalables est rempli tooupdating préalable votre appareil StorSimple.  

* Vérifiez que les deux contrôleurs de l’appareil sont actifs avant de rechercher des mises à jour. Aucun contrôleur ne fonctionne pas, hello analyse échoue. tooverify contrôleurs de hello sont dans un état sain, accédez trop**état du matériel** sous hello **Maintenance** page. Si des composants **nécessitent une attention**, contactez le support technique de Microsoft avant de continuer.
* Assurez-vous que les adresses IP fixes pour les contrôleurs 0 et 1 sont routable et peuvent se connecter toohello Internet car elles sont utilisées pour la maintenance des appareils de toohello hello mises à jour. Vous pouvez utiliser hello [applet de commande Test-Connection](https://technet.microsoft.com/library/hh849808.aspx) tooping une adresse connue en dehors du réseau hello, tels que outlook.com, tooverify qui hello contrôleur a toohello de connectivité en dehors du réseau.
* Vérifiez que les ports 80 et 443 sont disponibles pour la communication sortante sur l’appareil StorSimple. Pour plus d’informations, consultez hello [configuration réseau requise pour votre appareil StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* Si la version du logiciel hello est antérieure à 6.3.9600.17312 (mise à jour d’octobre 2014), désactivez les ports de données 2 et Data 3 des hello, s’il est activé, avant de commencer la mise à jour hello. En laissant hello Data 2 ou 3 ports activées lorsque vous appliquez la mise à jour hello risque de votre toogo de contrôleur de périphérique en mode de récupération. Notez que lorsque vous désactivez des interfaces réseau de hello, tous les volumes hello associé seront mis hors connexion et pour la durée de mise à jour hello hello hello e/s est interrompue.  

## <a name="whats-new-in-hello-february-release"></a>Nouveautés de la version de février hello
Cette mise à jour contient un correctif pour un problème de réinitialisation des paramètres d’usine hello qui se sont produites sur les périphériques qui avaient été mis à niveau à partir de la version de hello GA toohello version d’octobre 2014. Pour plus d’informations, reportez-vous à [Problèmes résolus dans cette version](#issues-fixed-in-the-february-release).   

Cette mise à jour ne contient pas de nouvelles fonctions ou fonctionnalités.  

## <a name="issues-fixed-in-hello-february-release"></a>Problèmes résolus dans la version de février hello
Hello tableau suivant décrit hello problème a été résolu dans cette mise à jour.  

| Non. | Fonctionnalité | Problème | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- |
| 1 |Réinitialisation aux paramètres d’usine |Vous essayez de tooperform usine sur un appareil qui avait hello GA de version (6.3.9600.17215) installé mais a été mis à jour toohello version d’octobre (version 6.3.9600.17312). Échec de réinitialisation de la fabrique de Hello et hello devient instable. |Oui |Non |

## <a name="known-issues-in-hello-february-release"></a>Problèmes connus dans la version de février hello
Hello tableau suivant fournit un résumé des problèmes connus dans cette version.

| Non. | Fonctionnalité | Problème | Commentaires/solution de contournement | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- | --- |
| 1 |Réinitialisation aux paramètres d’usine |Dans certains cas, lorsque vous effectuez une réinitialisation des paramètres, hello appareil StorSimple peut se bloquer et afficher le message : **toofactory de réinitialisation est en cours (phase 8)**. Cela se produit si vous appuyez sur CTRL + C lors de l’applet de commande hello est en cours d’exécution. |N’appuyez pas sur Ctrl+C après avoir lancé une réinitialisation aux paramètres d’usine. Si vous avez déjà effectué cette opération, contactez le support technique Microsoft. |Oui |Non |
| 2 |Disque quorum |Dans de rares cas, si la majorité de hello des disques du boîtier EBOD de hello d’un 8600device se déconnectent et où aucun quorum de disque, puis pool de stockage hello sera hors connexion. Il restera hors connexion, même si les disques hello sont reconnectés. |Vous devrez le périphérique de hello tooreboot. Si hello problème persiste, contactez le Support technique de Microsoft pour les étapes suivantes. |Oui |Non |
| 3 |Échec des instantanés cloud |Dans de rares cas, un instantané cloud peut échouer avec l’erreur de hello **limite de sauvegarde maximale atteinte**. Cela se produit si vous dépassez 255 clones en ligne sur hello même appareil et hello même volume d’origine qui a été supprimée. | |Oui |Oui |
| 4 |ID de contrôleur incorrect |Lorsqu’un contrôleur est remplacé, le contrôleur 0 peut apparaître comme contrôleur 1. Pendant le remplacement de contrôleur, lors de l’image de hello est chargée à partir du nœud d’homologue hello, ID de contrôleur hello permettre s’afficher d’abord en tant qu’ID. du contrôleur hello homologue Dans de rares cas, ce comportement peut également se produire après un redémarrage du système. |Aucune action utilisateur n’est requise. Cette situation se résoudra de lui-même après le remplacement du contrôleur hello. |Oui |Non |
| 5 |Graphiques d’analyse de l’appareil |Bonjour service StorSimple Manager, les graphiques de surveillance de périphérique hello ne fonctionnent pas lors de la base ou l’authentification NTLM est activée dans la configuration du serveur proxy hello pour appareil de hello. |Modifier la configuration du proxy web hello pour appareil hello inscrit auprès du service StorSimple Manager afin que l’authentification a la valeur tooNONE. toodo, hello hello d’exécution Windows PowerShell pour l’applet de commande Set-HcsWebProxy de StorSimple. |Oui |Oui |
| 6 |Comptes de stockage |À l’aide du compte de stockage du service toodelete hello hello stockage est un scénario non pris en charge. Cela entraîne une situation tooa dans lequel les données de l’utilisateur ne peut pas être récupérées. | |Oui |Oui |
| 7 |Basculement de l’appareil |Basculements multiples d’un conteneur de volume à partir de hello même équipements toodifferent appareil source n’est pas pris en charge.    Basculement à partir d’un seul morts toomultiple périphériques rend les conteneurs de volumes hello sur hello appareil basculé tout d’abord perdent la propriété de données. Après un tel basculement, ces conteneurs de volumes apparaît ou se comportent différemment lorsque vous les affichez dans hello portail Azure classic. | |Oui |Non |
| 8 |Installation |Au cours de l’adaptateur StorSimple pour l’installation de SharePoint, vous devez tooprovide une adresse IP dans l’ordre pour hello installation toofinish appareil avec succès. | |Oui |Non |
| 9 |Proxy web |Si votre configuration du proxy web a HTTPS comme hello spécifié de protocole, puis votre appareil au service communication est affectée et les appareils de hello passera en mode hors connexion. Prise en charge les packages sont également générés dans le processus de hello, consomment des ressources importantes sur votre appareil. |Assurez-vous que les URL du proxy web hello a HTTP comme hello protocole spécifié. Plus d’informations sur la façon de trop[configurer un proxy web pour votre appareil](storsimple-configure-web-proxy.md). |Oui |Non |
| 10 |Proxy web |Si vous configurez et activez le proxy web sur un appareil inscrit, puis vous devez contrôleur actif de toorestart hello sur votre appareil. | |Oui |Non |
| 11 |Latence de cloud élevée et charge de travail d’E/S élevée |Lorsque votre appareil StorSimple rencontre une combinaison de latences cloud très élevées (ordre de secondes) et la charge de travail d’e/s élevée, volumes du dispositif hello passe dans un état dégradé et hello e/s peut-être échouer avec une erreur « appareil non prêt ». |Vous devez contrôleurs d’appareil toomanually redémarrage hello ou effectuer une toorecover de basculement de périphérique à partir de cette situation. |Oui |Non |

## <a name="physical-device-updates-in-hello-february-release"></a>Mises à jour de l’unité physique dans la version de février hello
Cette mise à jour de correctifs hello réinitialisation problème qui s’est produite sur les appareils qui avaient été mis à niveau à partir de la version de hello GA toohello version d’octobre 2014. Il ne contient pas de tout autre périphérique de StorSimple de toohello mises à jour.  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-february-release"></a>Serial attached SCSI (SAS) contrôleur et du microprogramme des mises à jour dans la version de février hello
Cette version ne contient pas de n’importe quel contrôleur de mises à jour toohello serial attached SCSI (SAS) ou le microprogramme de hello. mise à jour du pilote Hello a hello octobre, version 2014.  

## <a name="virtual-device-updates-in-hello-february-release"></a>Mises à jour de l’appareil virtuel dans la version de février hello
Cette version ne contient pas les mises à jour pour un appareil virtuel hello. Appliquer cette mise à jour ne modifie pas la version du logiciel d’un périphérique virtuel hello.

