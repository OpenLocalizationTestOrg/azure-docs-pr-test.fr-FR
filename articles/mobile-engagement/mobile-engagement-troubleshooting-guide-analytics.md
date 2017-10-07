---
title: aaaAzure Mobile Engagement Troubleshooting Guide - Analytique
description: "Dépannage des problèmes d’analyse, de surveillance, de segmentation et de tableau de bord dans Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a>Guide de dépannage pour les problèmes d’analyse, de surveillance, de segmentation et de tableau de bord
Hello Voici les éventuels problèmes rencontrés avec la façon dont Azure Mobile Engagement rassemble des informations sur vos applications, utilisateurs et appareils.

## <a name="missingdelayed-information"></a>Informations manquantes/retardées
### <a name="issue"></a>Problème
* Les informations sont retardées dans l'analyse, la segmentation ou le tableau de bord.
* Il manque des informations de surveillance.
* Il manque des informations d'analyse, de segmentation ou du tableau de bord.
* Limites de segmentation atteinte.

### <a name="causes"></a>Causes
* Vous pouvez utiliser hello Analytique API, API d’analyse, et API de Segments toosee si toutes les données, vous êtes absent de l’interface utilisateur de hello est visible via hello API.
* Si hello Azure Mobile Engagement SDK n’est pas correctement intégré dans votre application vous ne serez pas en mesure de toosee des informations Bonjour Analytique, Segmentation, analyse ou tableaux de bord.
* Les segments ne peuvent pas être modifiée après avoir été créés, ils peuvent uniquement être « clonés » (copiés) ou « détruits » (supprimés). Les segments peuvent uniquement contenir 10 critères.
* meilleures tootest de façon Hello pas les informations de l’analyse est toosetup un appareil de test, désinstaller ou réinstaller l’application hello sur l’appareil de test hello.
* Les informations sont actualisées toutes les 24 heures pour l'analyse, la segmentation ou les tableaux de bord.
* Informations contenues dans les nouveaux segments ne peuvent pas s’afficher jusqu'à 24 heures après leur création même si le segment de hello est basée sur les informations précédentes.
* Filtrage des données analytique Bonjour l’interface utilisateur affiche tous les exemples de ce type, quelle que soit la version de hello de votre application (par exemple) les « Incidents » filtrés par nom s’afficheront depuis la version 1 et la version 2 de votre application).
* Hello laps de temps pour l’Analytique est basé sur hello date à partir des paramètres de périphérique hello utilisateurs, pour un utilisateur dont le téléphone a date de hello mal définie pourrait s’afficher dans hello incorrect laps de temps.
* Exécute un push d’aucun côté serveur données sont enregistrées lorsque vous utilisez le bouton de hello trop « ne test », les données sont enregistrées uniquement pour les campagnes push réel.

## <a name="cant-locate-items-in-ui"></a>Impossible de trouver des éléments dans l'interface utilisateur
### <a name="issue"></a>Problème
* Impossible de créer des segments en fonction de certains critères de balise d'informations d'application intégrés ou personnalisés.
* Impossible de trouver certains critères de balise d'informations d'application intégrés ou personnalisés dans l'analyse, la surveillance ou les tableaux de bord.
* Ne peut pas interpréter les données de salutation dans Analytique, surveillance, Segmentation ou tableaux de bord.

### <a name="causes"></a>Causes
* Certains générés dans les éléments et informations sur l’application sont uniquement disponibles en tant que critères de push de balises, mais ne peuvent pas être ajouté tooa segment ou visibles depuis Analytique, de surveillance ou de tableau de bord. 
* Pour la génération dans les éléments et les informations sur l’application des balises qui ne peut pas être ajoutées tooa segment, vous devez toosetup la liste des critères dans chaque hello tooperform de campagne même fonction que le ciblage basé sur un segment de ciblage.
* Voir les menus contextuels hello dans les sections hello Analytique, de surveillance, de Segmentation et de tableaux de bord de hello Azure Mobile Engagement UI pour plus d’informations et la manière dont tooinformation.

## <a name="crash-troubleshooting"></a>Dépannage d'incident
### <a name="issue"></a>Problème
* Incidents d'application apparaissant dans l'analyse, la surveillance ou le tableau de bord.

### <a name="causes"></a>Causes
* tootroubleshoot Application se bloque dans Analytique, de surveillance ou de tableau de bord Assurez-vous que toocheck hello notes de publication pour les problèmes connus avec les versions précédentes du Kit de développement logiciel de hello.
* toofurther dépanner application tombe en panne, effectuer un événement à partir d’un appareil de test avec votre application installée et recherche l’ID de votre appareil dans la section de hello « événements – analyse » de hello Azure Mobile Engagement UI. Puis exécuter l’événement hello toocrash de votre application à l’origine et consulter des informations supplémentaires dans hello « Analyse – incident » section hello Azure Mobile Engagement UI. 

