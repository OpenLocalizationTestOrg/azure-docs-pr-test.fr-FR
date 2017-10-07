---
title: notes de publication de version Release aaaStorSimple 8000 | Documents Microsoft
description: "Décrit les nouvelles fonctionnalités de hello, problèmes ouverts et les solutions disponibles pour hello juillet 2014 version de Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 12f1796e-37c3-42b4-b997-a84fc1950c20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 74863a3e2811dc7be5e6f482a5be4bbc37e3cd71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-release-version-release-notes---july-2014"></a>Notes de publication de StorSimple série 8000 Release Version - Juillet 2014
## <a name="overview"></a>Vue d'ensemble
notes de publication Hello suivez identifient hello problèmes critiques en suspens pour hello StorSimple 8000 Series version disponibilité générale (GA) de juillet 2014 de Microsoft Azure StorSimple. Cette version correspond toosoftware version 6.3.9600.17215.  

Sauf indication contraire, ces notes s’appliquent à des modèles de tooall de l’appareil StorSimple hello. notes de publication Hello sont régulièrement mis à jour ; dès qu’un problème important nécessitant une solution de contournement est détecté, ils sont ajoutés. Avant de déployer votre solution Microsoft Azure StorSimple, envisagez de hello informations suivantes.  

## <a name="known-issues-in-this-release"></a>Problèmes connus dans cette version
Hello tableau suivant fournit un résumé des problèmes connus dans cette version.  

| Non. | Fonctionnalité | Problème | Commentaires/solution de contournement | S’applique toophysical périphérique | S’applique toovirtual périphérique |
| --- | --- | --- | --- | --- | --- |
| 1 |Réinitialisation aux paramètres d’usine |Dans certains cas, lorsque vous effectuez une réinitialisation des paramètres, hello appareil StorSimple peut se bloquer et afficher le message : **toofactory de réinitialisation est en cours (phase 8)**. Cela se produit si vous appuyez sur CTRL + C lors de l’applet de commande hello est en cours d’exécution. |N’appuyez pas sur Ctrl+C après avoir lancé une réinitialisation aux paramètres d’usine. Si vous avez déjà effectué cette opération, contactez le support technique Microsoft. |Oui |Non |
| 2 |Disque quorum |Dans de rares cas, si la majorité de hello des disques du boîtier EBOD de hello d’un appareil 8600 se déconnectent et où aucun quorum de disque, puis pool de stockage hello sera hors connexion. Il restera hors connexion, même si les disques hello sont reconnectés. |Vous devrez le périphérique de hello tooreboot. Si hello problème persiste, contactez le Support technique de Microsoft pour les étapes suivantes. |Oui |Non |
| 3 |Échec des instantanés cloud |Dans de rares cas, un instantané cloud peut échouer avec l’erreur de hello **limite de sauvegarde maximale atteinte**. Cela se produit si vous dépassez 255 clones en ligne sur hello même appareil et hello même volume d’origine qui a été supprimée. | |Oui |Oui |
| 4 |ID de contrôleur incorrect |Lorsqu’un contrôleur est remplacé, le contrôleur 0 peut apparaître comme contrôleur 1. Pendant le remplacement de contrôleur, lors de l’image de hello est chargée à partir du nœud d’homologue hello, ID de contrôleur hello permettre s’afficher d’abord en tant qu’ID. du contrôleur hello homologue Dans de rares cas, ce comportement peut également se produire après un redémarrage du système. |Aucune action utilisateur n’est requise. Cette situation se résoudra de lui-même après le remplacement du contrôleur hello. |Oui |Non |
| 5 |Graphiques d’analyse de l’appareil |Bonjour service StorSimple Manager, les graphiques de surveillance de périphérique hello ne fonctionnent pas lors de la base ou l’authentification NTLM est activée dans la configuration du serveur proxy hello pour appareil de hello. |Modifier la configuration du proxy web hello pour appareil hello inscrit auprès du service StorSimple Manager afin que l’authentification a la valeur tooNONE. toodo, hello hello d’exécution Windows PowerShell pour l’applet de commande Set-HcsWebProxy de StorSimple. |Oui |Oui |
| 6 |Comptes de stockage |À l’aide du compte de stockage du service toodelete hello hello stockage est un scénario non pris en charge. Cela entraîne une situation tooa dans lequel les données de l’utilisateur ne peut pas être récupérées. | |Oui |Oui |
| 7 |Restauration automatique |La restauration automatique dans les 24 heures qui suivent une récupération d’urgence n’est pas prise en charge. | |Oui |Non |
| 8 |Basculement de l’appareil |Basculements multiples d’un conteneur de volume à partir de hello même équipements toodifferent appareil source n’est pas pris en charge. Basculement à partir d’un seul morts toomultiple périphériques rend les conteneurs de volumes hello sur hello appareil basculé tout d’abord perdent la propriété de données. Après un tel basculement, ces conteneurs de volumes apparaît ou se comportent différemment lorsque vous les affichez dans hello portail Azure classic. | |Oui |Non |
| 9 |Installation |Au cours de l’adaptateur StorSimple pour l’installation de SharePoint, vous devez tooprovide une adresse IP de périphérique pour hello installation toofinish avec succès. | |Oui |Non |
| 10 |Interfaces réseau |Interfaces réseau DATA 2 et 3 étaient interverties dans le logiciel de hello. |Contactez le Support Microsoft si vous devez tooconfigure ces interfaces. |Oui |Non |

