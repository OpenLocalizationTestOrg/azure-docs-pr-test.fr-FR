---
title: "Présentation de l’API Engagement exporter d’aaaMobile"
description: "Découvrez les principes de base hello sur l’exportation de vos données brutes généré par tooleverage de périphériques de vos utilisateurs il dans vos propres outils"
services: mobile-engagement
documentationcenter: mobile
author: kpiteira
manager: erikre
editor: 
ms.assetid: 9380d47b-d7fa-4d4c-888f-97e6482196bb
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 04/26/2016
ms.author: kapiteir
ms.openlocfilehash: f55be29a29878e74f6a33419f08a5574a07a7478
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mobile-engagement-export-api-overview"></a>Vue d’ensemble de l'API d’exportation Mobile Engagement
## <a name="introduction"></a>Introduction
Dans ce document, vous allez apprendre bases hello sur l’exportation de vos données brutes généré par tooleverage de périphériques de l’utilisateur de votre dans vos propres outils.

## <a name="pre-requisites"></a>Conditions préalables
Exportation des données brutes de hello de Mobile Engagement nécessite :

* Toobe toouse en mesure de hello API API d’authentification le programme d’installation (consultez [le programme d’installation manuelle de l’authentification](mobile-engagement-api-authentication-manual.md)),
* Utilisez hello API REST ou hello [.net SDK](mobile-engagement-dotnet-sdk-service-api.md),
* Un compte de stockage Azure.

> [!NOTE]
> Nous vous conseillons également de hello excellent [Microsoft Azure Storage Explorer](http://storageexplorer.com/), au moins pendant la phase de développement hello tel qu’il fournit une interface utilisateur de toouse facile d’interagir avec le stockage Azure.
> 
> 

## <a name="what-can-be-exported"></a>Que peut-on exporter ?
Mobile Engagement permet son toocollect les utilisateurs de nombreux types de données et par conséquent, plusieurs types d’exportation a adapté toothese différents types de données.
Il existe 2 types d'exportation principaux :

* Instantané : utilisé en général tooexport des données qui représente un état et pour lequel Mobile Engagement n’a pas de l’historique. Cela inclut par exemple les balises (app-info), les jetons ou les retours d’expérience de campagnes push. Par conséquent ces types d’exportation ne sont pas liées tooa date.
* Historique : ce type d'exportation est utilisé pour les données qui s'accumulent au fil du temps, par exemple des événements ou des activités.

tableau de Hello ci-dessous décrit la manière exhaustive toutes les exportations possible hello :

| Type d’exportation | Type de données | Description |
| --- | --- | --- |
| Instantané |Émettre |Génère une exportation de retours d’expérience de campagnes push, ID d’appareil/d'utilisateur par ID d’appareil/d’utilisateur |
| Instantané |Tag |Génère une exportation de périphériques de tooeach hello induits (app-info) |
| Instantané |Appareil |Génère une exportation de la plupart des données de hello sur des appareils tels que technicals hello (modèle, paramètres régionaux, fuseau horaire,...), les balises hello, première vu... |
| Instantané |Jeton |Génère une exportation de tous les jetons valides hello |
| Historique |Activité |Génère une exportation de toutes les activités hello pour chaque périphérique sur une période donnée |
| Historique |Événement |Génère une exportation de toutes les activités hello pour chaque périphérique sur une période donnée |
| Historique |Travail |Génère une exportation de tous les travaux hello pour chaque périphérique sur une période donnée |
| Historique |Error |Génère une exportation de toutes les erreurs de hello pour chaque périphérique sur une période donnée |

## <a name="how-does-it-work"></a>Comment cela fonctionne-t-il ?
Les exportations sont des tâches de longue durée qui peuvent produire des fichiers de données volumineux. Pour cette raison, ils ne peut pas être appelée tooreturn immédiatement un toodownload de fichier.
Données de commandes tooexport de Mobile Engagement, vous devez toocreate une **tâche d’exportation** via l’API dans lequel vous spécifiez généralement :

* type Hello d’exportation (instantanée ou historique)
* type de données Hello,
* Hello **conteneur de stockage Azure** (y compris une SAP valide avec un accès en écriture) où le résultat de hello d’exportation de hello sera écrit.
* Par exemple, un paramètre d’URL de conteneur serait https://[StorageAccountName].blob.core.windows.net/[ContainerName]?[SASWritePermissionsToken]  

Voici un exemple réel. https://testazmeexport.blob.core.windows.net/test1234azme?sv=2015-12-11&ss=b&srt=sco&sp=rwdlac&se=2016-12-17T04:59:26Z&st=2016-12-16T20:59:26Z&spr=https&sig=KRF3aVWjp2NEJDzjlmoplmu0M9HHlLdkBWRPAFmw90Q%3D

Notez que peut prendre quelques minutes pour votre toobe de travail a démarré, et, il peut s’exécuter à partir de quelques secondes pour les heures de tooseveral de petites applications pour les applications avec un grand nombre d’utilisateurs ou d’activité.

Une fois le travail de hello est créé, il est possible de toocheck son toosee état si elle est toujours en cours d’exécution ou si elle est terminée.

Une fois que le travail de hello est réussi, fichier de données résultant hello est disponible sur hello fourni le conteneur de stockage.

