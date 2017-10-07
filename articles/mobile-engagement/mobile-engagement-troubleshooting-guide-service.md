---
title: "aaaAzure Guide de dépannage de Engagement Mobile - Service"
description: "Guides de dépannage pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a>Guide de résolution des problèmes de service
Hello Voici les problèmes possibles, que vous pouvez rencontrer avec le mode d’exécution de Azure Mobile Engagement.

## <a name="service-outages"></a>Interruptions de service
### <a name="issue"></a>Problème
* Problèmes apparaissant toobe dû à des interruptions de Service Azure Mobile Engagement.

### <a name="causes"></a>Causes
* Les problèmes apparaissant toobe dû à des interruptions de Service Azure Mobile Engagement peuvent être dû à plusieurs problèmes différents :
  * Problèmes apparaissant à l’origine tooall systémique de Azure Mobile Engagement
  * Problèmes connus provoqués par des pannes de serveur (ne s'affichent pas toujours dans l'état du serveur) :
  * Planification des retards, des erreurs de ciblage, les problèmes de mise à jour de Badge, stop statistiques collecte, par envoi de données s’arrête de fonctionner, cessent de fonctionner, les nouvelles applications ou les utilisateurs de l’API ne peut pas créer, erreurs DNS et délai d’attente dans hello l’interface utilisateur, des API ou des applications sur un appareil.
  * Interruptions de dépendance de cloud [État du Service Azure](http://status.azure.com/)
  * Interruptions de dépendance des Services de notification push (PNS)
  * Interruptions App Store

1) tootest toosee si le problème de hello est systémique, vous pouvez tester hello même fonction à partir d’un autre

* Application intégrée d’Azure Mobile Engagement
* Appareil de test
* Version du système d’exploitation de l’appareil de test
* Campagne
* Compte utilisateur de l’administrateur
* Navigateur (Internet Explorer, Firefox, Chrome, etc.)
* Ordinateur

2) tootest si le problème de hello affecte uniquement hello hello interface utilisateur ou l’API :

* Test hello même fonction à partir de ces deux hello Azure Mobile Engagement UI et hello API Azure Mobile Engagement.

3) tootest si hello problème avec le réseau de votre téléphone cellulaire :

* Test lors de la toohello connecté Internet via le Wi-Fi et tout en étant connecté via le réseau de votre téléphone cellulaire 3G.
* Vérifiez que votre pare-feu ne bloque pas un des Ports ou des adresses IP de hello Azure Mobile Engagement.

4) tootest si hello problème avec votre appareil :

* Tester si votre appareil est en mesure de tooconnect tooAzure Mobile Engagement avec une autre application intégrée Azure Mobile Engagement.
* Vérifiez que vous pouvez générer des incidents, des travaux et des événements à partir de votre téléphone, qui peut être consulté dans hello Azure Mobile Engagement UI. 
* Vérifier si vous pouvez envoyer des notifications push à partir de l’appareil de tooyour de l’interface utilisateur de Azure Mobile Engagement hello en fonction de son ID de périphérique. 

5) tootest si hello problème avec votre application :

* Installez et testez votre application à partir d’un émulateur plutôt qu’à partir d'un appareil physique :

6) tootest si hello problème avec l’utilisateur tooend de mises à niveau du système d’exploitation des appareils, qui nécessitent une tooresolve de mise à niveau du Kit de développement logiciel :

* Tester votre application sur différents appareils avec différentes versions de hello du système d’exploitation.
* Vérifiez que vous utilisez la version la plus récente du Kit de développement logiciel de hello hello.

## <a name="connectivity-and-incorrect-information-issues"></a>Problèmes de connectivité et informations incorrectes
### <a name="issue"></a>Problème
* Problèmes de connexion à Bonjour Azure Mobile Engagement UI.
* Erreurs de connexion avec hello Azure Mobile Engagement API.
* Problèmes lors du chargement des balises d’informations sur application via hello API de l’appareil.
* Problèmes lors du téléchargement des journaux ou des données exportées à partir d'Azure Mobile Engagement.
* Informations incorrectes indiquées Bonjour Azure Mobile Engagement UI.
* Informations incorrectes indiquées dans les journaux Azure Mobile Engagement.

### <a name="causes"></a>Causes
* Confirmez que votre compte d’utilisateur a des tâches de hello de tooperform autorisations suffisantes.
* Vérifiez que ce problème hello n’est pas isolé tooone ordinateur ou votre réseau local.
* Vérifiez que ce service de Azure Mobile Engagement hello ne dispose d’aucune les pannes signalées.
* Vérifiez que vos fichiers de balise d'informations d'application respectent toutes ces règles :
  * Utilisez hello uniquement le jeu de caractères UTF-8 (jeu de caractères ANSI hello n’est pas pris en charge).
  * Utilisez une virgule «, » comme séparateur de hello (vous pouvez ouvrir un caractère de séparation service demande hello toorequest toochange .csv à partir d’une virgule «, » caractères tooanother comme un point-virgule « ; »).
  * Utilisez des minuscules pour les valeurs booléennes « true » et « false ».
  * Utiliser un fichier qui est plus petit que la taille de fichier maximale hello de 35 Mo.

