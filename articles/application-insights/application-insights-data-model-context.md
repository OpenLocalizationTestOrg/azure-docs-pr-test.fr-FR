---
title: "aaaAzure modèle de données d’Application Insights télémétrie - contexte de données de télémétrie | Documents Microsoft"
description: "Modèle de données du contexte de télémétrie d’Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a>Contexte de télémétrie : modèle de données d’Application Insights

Chaque élément de télémétrie peut avoir des champs de contexte fortement typés. Chaque champ permet un scénario de surveillance spécifique. Utilisez hello propriétés personnalisées collection toostore personnalisées ou spécifiques à l’application des informations contextuelles.


##<a name="application-version"></a>Version de l’application

Les informations dans les champs de contexte d’application hello sont toujours sur l’application hello qui envoie les données de télémétrie hello. Version de l’application est utilisée tooanalyze des modifications de tendance dans le comportement de l’application hello et ses déploiements toohello de corrélation.

Longueur maximale : 1024


##<a name="client-ip-address"></a>Adresse IP du client

adresse IP de Hello de périphérique de client hello. IPv4 et IPv6 sont pris en charge. Lors de la télémétrie est envoyée à partir d’un service, contexte d’emplacement hello est sur l’utilisateur hello qui a lancé une opération de service de hello hello. Application Insights extraire des informations de géolocalisation hello à partir de l’adresse IP du client hello et puis de le tronquer. Ainsi, l’adresse IP du client en elle-même ne peut pas être utilisée comme information identifiable de l’utilisateur final. 

Longueur maximale : 46


##<a name="device-type"></a>Type d’appareil

À l’origine de ce champ a été utilisé à l’aide de type hello de tooindicate de hello hello fin utilisateur de l’application hello. Nous sommes utilisé principalement les données de télémétrie de JavaScript toodistinguish hello type d’appareil « Browser » à partir des données de télémétrie côté serveur avec le type d’appareil hello « PC ».

Longueur maximale : 64


##<a name="operation-id"></a>ID d’opération

Identificateur unique de l’opération de racine hello. Cet identificateur permet de télémétrie de toogroup sur plusieurs composants. Pour plus d’informations, consultez [Corrélation de la télémétrie](application-insights-correlation.md). id d’opération Hello est créé par une demande ou un affichage de page. Toutes les autres données de télémétrie définit cette valeur du champ toohello pour hello contenant la demande ou la page de vue. 

Longueur maximale : 128


##<a name="parent-operation-id"></a>ID d’opération parent

Bonjour identificateur unique du parent immédiat de l’élément de données de télémétrie hello. Pour plus d’informations, consultez [Corrélation de la télémétrie](application-insights-correlation.md).

Longueur maximale : 128


##<a name="operation-name"></a>Nom d’opération

nom Hello (groupe) de l’opération de hello. nom de l’opération Hello est créé par une demande ou un affichage de page. Tous les autres éléments de télémétrie définir cette valeur de toohello de champ pour hello contenant la demande ou la page de vue. Nom de l’opération est utilisée pour rechercher tous les éléments de télémétrie hello pour un groupe d’opérations (par exemple ' GET Home/Index »). Cette propriété de contexte est utilisé tooanswer questions du type « quels sont les exceptions standard hello levées sur cette page. »

Longueur maximale : 1024


##<a name="synthetic-source-of-hello-operation"></a>Source synthétique d’opération de hello

Nom de la source synthétique. Certaines données de télémétrie à partir de l’application hello peuvent représenter le trafic synthétique. Il peut être du robot d’indexation hello web site web, tests de disponibilité de site ou des traces à partir de bibliothèques de diagnostic à Application Insights SDK lui-même.

Longueur maximale : 1024


##<a name="session-id"></a>ID de session

ID de session - instance hello d’interaction de l’utilisateur hello avec application hello. Les informations dans les champs de contexte de session hello sont toujours sur l’utilisateur final de hello. Lors de la télémétrie est envoyée à partir d’un service, le contexte de session hello est sur l’utilisateur hello qui a lancé une opération de service de hello hello.

Longueur maximale : 64


##<a name="anonymous-user-id"></a>ID d’utilisateur anonyme

ID d’utilisateur anonyme. Représente l’utilisateur final de hello de l’application hello. Lors de la télémétrie est envoyée à partir d’un service, contexte de l’utilisateur hello est sur l’utilisateur hello qui a lancé une opération de service de hello hello.

[Échantillonnage](app-insights-sampling.md) est un des hello techniques toominimize hello quantité des données de télémétrie collectées. Échantillonnage algorithme tentatives tooeither exemple ou annuler tous les hello corrélés télémétrie. L’ID d’utilisateur anonyme est utilisé pour la génération de score d’échantillonnage. L’ID d’utilisateur anonyme doit donc être une valeur suffisamment aléatoire. 

À l’aide du nom d’utilisateur utilisateur anonyme id toostore est une utilisation incorrecte d’un champ de hello. Utilisez un ID d’utilisateur authentifié.

Longueur maximale : 128


##<a name="authenticated-user-id"></a>ID d’utilisateur authentifié

Id de l’utilisateur authentifié. Hello opposé de l’id d’utilisateur anonyme, ce champ représente l’utilisateur hello avec un nom convivial. Comme il s’agit de ses informations d’identification personnelle, par défaut, il n’est pas collecté par la plupart des SDK.

Longueur maximale : 1024


##<a name="account-id"></a>ID de compte

Dans les applications mutualisées agit hello l’ID de compte ou nom, les utilisateurs hello agit avec. C’est par exemple l’ID d’abonnement pour le portail Azure ou un nom de blogueur pour une plateforme de blog.

Longueur maximale : 1024


##<a name="cloud-role"></a>Rôle cloud

Nom de l’application de hello hello rôle fait partie de. Mappe directement le nom du rôle toohello dans azure. Peut également être utilisé toodistinguish micro services, qui font partie d’une application unique.

Longueur maximale : 256


##<a name="cloud-role-instance"></a>Instance de rôle cloud

Nom d’instance hello où l’application hello est en cours d’exécution. Nom de l’ordinateur pour un ordinateur local, nom de l’instance pour Azure.

Longueur maximale : 256


##<a name="internal-sdk-version"></a>Interne : version du SDK

Version du SDK. Pour plus d’informations, consultez https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification.

Longueur maximale : 64


##<a name="internal-node-name"></a>Interne : nom du nœud

Ce champ représente le nom du nœud hello utilisé à des fins de facturation. Utiliser toooverride hello standard la détection des nœuds.

Longueur maximale : 256


## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment trop[étendre et de filtrer les données de télémétrie](app-insights-api-filtering-sampling.md).
- Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).
- Découvrez la [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) de la collection de propriétés de contexte standard.
