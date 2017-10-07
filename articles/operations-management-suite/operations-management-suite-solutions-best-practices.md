---
title: meilleures pratiques de solution aaaOMSManagement | Documents Microsoft
description: 
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 08cf1c101e301d24fb5c2bf4bc02a978e508a198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-management-solutions-in-operations-management-suite-oms-preview"></a>Meilleures pratiques pour la création de solutions de gestion dans Operations Management Suite (OMS) (version préliminaire)
> [!NOTE]
> Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion. N’importe quel schéma décrit ci-dessous est un objet toochange.  

Cet article décrit les méthodes conseillées pour la [création d’un fichier de solution de gestion](operations-management-suite-solutions-solution-file.md) dans Operations Management Suite (OMS).  Ces informations seront mises à jour lorsque de meilleures pratiques supplémentaires seront identifiées.

## <a name="data-sources"></a>Sources de données
- Des sources de données peuvent être [configurées avec un modèle Resource Manager](../log-analytics/log-analytics-template-workspace-configuration.md), mais elles ne doivent pas être incluses dans un fichier solution.  Hello parce que les sources de données de configuration n’est pas actuellement idempotent, c'est-à-dire que votre solution peut remplacer la configuration existante dans l’espace de travail de l’utilisateur hello.<br><br>Par exemple, votre solution peut nécessiter des événements d’avertissement et d’erreur à partir du journal des événements Application hello.  Si vous spécifiez ce comme source de données dans votre solution, vous risquez de supprimer des événements d’Information si l’utilisateur de hello possède ce type de configuration dans leur espace de travail.  Si vous avez inclus tous les événements, puis peut effectuer la collecte d’excessives événements d’Information dans l’espace de travail de l’utilisateur hello.

- Si votre solution nécessite des données à partir d’une des sources de données standard de hello, vous devez définir cela comme une condition préalable.  État dans la documentation de ce client hello doit configurer source de données hello sur leurs propres.  
- Ajouter un [vérification des flux de données](../log-analytics/log-analytics-view-designer-tiles.md) message tooany des vues dans votre utilisateur de hello tooinstruct solution sur des sources de données qui toobe besoin configuré pour les données requises toobe collectées.  Ce message s’affiche sur la vignette hello de vue de hello lorsque les données requises sont introuvable.


## <a name="runbooks"></a>Runbooks
- Ajouter un [planification Automation](../automation/automation-schedules.md) pour chaque runbook dans votre solution nécessitant toorun selon une planification.
- Inclure hello [IngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) dans votre toobe solution utilisé par les procédures opérationnelles de l’écriture d’un référentiel de données toohello Analytique de journal.  Configurer une solution de hello trop[référence](operations-management-suite-solutions-solution-file.md#solution-resource) cette ressource afin qu’il reste si les solutions hello sont supprimée.  Cela permet plusieurs solutions tooshare hello module.
- Utilisez [variables Automation](../automation/automation-schedules.md) tooprovide valeurs solution toohello que les utilisateurs veulent toochange plus tard.  Même si les solutions hello est configuré toocontain hello, sa valeur peut toujours être modifiée.

## <a name="views"></a>Views
- Toutes les solutions doivent inclure une vue unique qui s’affiche dans le portail de l’utilisateur hello.  Hello affichage peut contenir plusieurs [des parties de visualisation](../log-analytics/log-analytics-view-designer-parts.md) tooillustrate différents jeux de données.
- Ajouter un [vérification des flux de données](../log-analytics/log-analytics-view-designer-tiles.md) message tooany des vues dans votre utilisateur de hello tooinstruct solution sur des sources de données qui toobe besoin configuré pour les données requises toobe collectées.
- Configurer une solution de hello trop[contiennent](operations-management-suite-solutions-solution-file.md#solution-resource) hello affichage afin qu’il est retiré si les solutions hello sont supprimée.

## <a name="alerts"></a>Alertes
- Définir la liste des destinataires hello en tant que paramètre dans le fichier de solution hello afin de l’utilisateur de hello définissez-les lorsqu’ils installent la solution de hello.
- Configurer une solution de hello trop[référence](operations-management-suite-solutions-solution-file.md#solution-resource) afin de cet utilisateur peut modifier la configuration de règles d’alerte.  Ils peuvent veulent toomake des modifications telles que la modification de la liste de destinataires hello, la modification du seuil de hello d’alerte de hello ou la désactivation d’une règle d’alerte hello. 


## <a name="next-steps"></a>Étapes suivantes
* Parcourez processus basic de hello de [concevoir et créer une solution de gestion](operations-management-suite-solutions-creating.md).
* Découvrez comment trop[créer un fichier de solution](operations-management-suite-solutions-solution-file.md).
* [Ajouter des alertes et les recherches enregistrées](operations-management-suite-solutions-resources-searches-alerts.md) solution de gestion tooyour.
* [Ajouter des vues](operations-management-suite-solutions-resources-views.md) solution de gestion tooyour.
* [Ajouter des runbooks Automation et autres ressources](operations-management-suite-solutions-resources-automation.md) solution de gestion tooyour.

