---
title: "concepts d’Engagement aaaMobile | Documents Microsoft"
description: "Concepts d’Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 5aa7f28c00cd641a36a6e040c6b13d802ea6ae41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-concepts"></a>Concepts d’Azure Mobile Engagement
Mobile Engagement définit des plateformes de tooall pris en charge courantes de quelques concepts. Cet article décrit brièvement ces concepts.

Cet article est un bon début si vous êtes de nouveau tooMobile Engagement. Également vous assurer tooread hello documentation spécifique toohello plate-forme que vous utilisez, comme il affinerons concepts hello décrits dans cet article avec plusieurs détails et exemples ainsi que les limitations possibles.

## <a name="devices-and-users"></a>Appareils et utilisateurs
Mobile Engagement identifie les utilisateurs en générant un identificateur unique pour chaque appareil. Cet identificateur est appelé identificateur de l’appareil hello (ou `deviceid`). Il est généré de manière à ce que toutes les applications s’exécuter de hello même partage de périphérique hello même identificateur de l’appareil.

Implicitement, cela signifie que Mobile Engagement considère un toobelong tooexactly un utilisateur de l’appareil, et par conséquent, les utilisateurs et les appareils sont des concepts équivalents.

## <a name="sessions-and-activities"></a>Sessions et activités
Une session est une utilisation de l’application hello effectuée par un utilisateur, à partir de l’utilisateur hello hello démarre à l’aide, jusqu'à ce que hello, utilisateur s’arrête.

Une activité est une utilisation d’un article de l’application hello effectuée par un utilisateur secondaire (il s’agit généralement d’un écran, mais il peut être approprié n’est pas défini toohello application).

Un utilisateur peut effectuer seulement une activité à la fois.

Une activité est identifiée par un nom (caractères too64 limité) et permettre incorporer éventuellement certaines données supplémentaires (dans la limite de hello de 1 024 octets).

Les sessions sont calculées automatiquement à partir de la séquence de hello d’activités effectuées par les utilisateurs. Une session démarre lorsque l’utilisateur de hello démarre sa première activité et s’arrête lorsqu’il termine sa dernière activité. Cela signifie qu’une session n’a pas besoin toobe explicitement démarré ou arrêté. En revanche, les activités sont démarrées ou arrêtées de manière explicite. Si aucune activité n’est signalée, aucune session n’est signalée.

## <a name="events"></a>Événements
Les événements sont des actions d’instantanée tooreport utilisé (par exemple, le bouton enfoncé ou articles lus par les utilisateurs).

Un événement peut être connexe toohello la session active, tooa exécute le travail, ou il peut être un événement autonome.

Un événement est identifié par un nom (caractères too64 limité) et permettre incorporer éventuellement certaines données supplémentaires (dans la limite de hello de 1 024 octets).

## <a name="error"></a>Error
Les erreurs sont des problèmes tooreport utilisés correctement détectées par l’application hello (comme les actions utilisateur incorrect, ou d’échecs d’appel API).

Une erreur peut être connexe toohello la session active, tooa exécute le travail, ou il peut être une erreur autonome.

Une erreur est identifiée par un nom (caractères too64 limité) et permettre incorporer éventuellement certaines données supplémentaires (dans la limite de hello de 1 024 octets).

## <a name="job"></a>Travail
Les travaux sont les actions utilisées tooreport ayant une durée (comme la durée des appels d’API, afficher les temps de publicités, la durée des tâches d’arrière-plan ou la durée des actions utilisateur).

Un travail n’est pas associée tooa session, car une tâche peut être effectuée en arrière-plan hello, sans intervention de l’utilisateur.

Une tâche est identifiée par un nom (caractères too64 limité) et permettre incorporer éventuellement certaines données supplémentaires (dans la limite de hello de 1 024 octets).

## <a name="crash"></a>Blocage
Pannes émis automatiquement par hello application tooreport de kit de développement logiciel de Mobile Engagement où problèmes non détectés par l’application hello rendent des échecs se bloquer.

## <a name="application-information"></a>Informations de l'application
Informations sur l’application (ou des informations sur l’application) sont utilisé tootag utilisateurs, tooassociate, certains utilisateurs toohello de données d’une application (il s’agit des cookies tooweb similaire, à ceci près que les informations sur l’application sont stockée sur le côté du serveur hello sur la plateforme Azure Mobile Engagement de hello).

Informations sur l’application peuvent être inscrit à l’aide des API de kit de développement logiciel de Mobile Engagement de hello ou à l’aide de plateforme Mobile Engagement de hello API de l’appareil.

Informations sur l’application sont un périphérique tooa associé de paire clé/valeur. clé de Hello est nom hello d’informations sur l’application hello (too64 limité lettres ASCII [a-zA-Z], [0-9] de nombres et des traits de soulignement [_]). valeur de Hello (caractères limité too1024) peut être toute chaîne, entier, date (AAAA-MM-JJ) ou valeur booléenne (true ou false).

N’importe quel nombre d’informations sur l’application peut être associé tooa périphérique, dans les limites de hello défini par les termes du contrat de tarification hello Mobile Engagement. Pour une clé donnée, Mobile Engagement uniquement effectue le suivi de hello dernière valeur définie (aucun historique). Définition ou la modification de valeur hello des informations d’application Mobile Engagement toore de force-évaluer les critères d’audience définie sur cette application info (le cas échéant), ce qui signifie que les informations de cette application peut être utilisé tootrigger en temps réel push.

## <a name="extra-data"></a>Données supplémentaires
Données supplémentaires (ou extras) sont certaines données arbitraires qui peuvent être attachés tooevents, les erreurs, les activités et les tâches.

Fonctionnalités supplémentaires sont structurés de même tooJSON objets : ils sont constitués d’une arborescence de paires clé/valeur. Les clés sont les lettres ASCII de too64 limité [a-zA-Z], des nombres [0-9] et des traits de soulignement [_]) et hello total extras caractères too1024 limitée (une fois encodées au format JSON par hello Kit de développement logiciel de Mobile Engagement).

Hello intégralité de l’arborescence de paires clé/valeur est stockée en tant qu’objet JSON. Néanmoins, seul hello premier niveau de clés/valeurs est décomposée toobe directement accessible toosome avancé fonctions comme les Segments (par exemple, vous pouvez facilement définir un segment appelé « SciFi ventilateurs » qui est constitué de tous les utilisateurs ayant envoyé l’événement de hello au moins 10 fois nommé « content_viewed » avec type_contenu « hello clé supplémentaire » scifi « jeu toohello valeur « Bonjour le mois dernier). Par conséquent, il est vivement recommandé de toosend seules fonctionnalités supplémentaires de listes simples de paires clé/valeur à l’aide de valeurs scalaires (par exemple, les chaînes, les dates, les entiers ou booléen).

## <a name="next-steps"></a>Étapes suivantes
* [Vue d’ensemble du Kit de développement logiciel (SDK) de Windows Universal pour Azure Engagement Mobile](mobile-engagement-windows-store-sdk-overview.md)
* [Vue d’ensemble du Kit de développement logiciel (SDK) Silverlight de Windows Phone pour Azure Engagement Mobile](mobile-engagement-windows-phone-sdk-overview.md)
* [Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement](mobile-engagement-ios-sdk-overview.md)
* [SDK Android pour Azure Mobile Engagement](mobile-engagement-android-sdk-overview.md)

