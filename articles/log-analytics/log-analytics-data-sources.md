---
title: "sources de données aaaConfigure Analytique des journaux OMS | Documents Microsoft"
description: "Sources de données définissent les données de hello que collecte Analytique de journal à partir des agents et d’autres sources connectées.  Cet article décrit le concept de hello de l’utilisation des sources de données Analytique de journal, explique en détail hello de façon tooconfigure et fournit un résumé des hello différentes sources de données disponibles."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 67710115-c861-40f8-a377-57c7fa6909b4
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: ebe8d29a2442a654b98004f624181ff406868e2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-in-log-analytics"></a>Sources de données dans Log Analytics
Analytique de journal collecte les données à partir de Sources connectées de hello dans votre espace de travail OMS et le stocke dans le référentiel OMS.  données Hello collectées à partir de chacun sont définies par hello des Sources de données que vous configurez.  Données dans le référentiel OMS est stockée comme un ensemble d’enregistrements hello.  Chaque source de données crée des enregistrements d'un type particulier, chaque type ayant son propre ensemble de propriétés.

![Collecte de données Log Analytics](./media/log-analytics-data-sources/overview.png)

Sources de données sont différents des Solutions OMS qui également collecter des données à partir de Sources connectées et créer des enregistrements dans le référentiel d’OMS hello.  Les solutions peuvent être ajoutées tooyour espace de travail à partir de la galerie des Solutions de hello et fournissent généralement des outils d’analyse supplémentaires dans le portail OMS est hello.  

## <a name="summary-of-data-sources"></a>Résumé des sources de données
les sources de données Hello qui sont actuellement disponibles dans le journal Analytique sont répertoriées dans hello tableau suivant.  Chacun dispose d’un article distinct de lien tooa, fournir des détails pour cette source de données.

| source de données | Type d'événement | Description |
|:--- |:--- |:--- |
| [Journaux personnalisés](log-analytics-data-sources-custom-logs.md) |\<LogName\>_CL |Fichiers texte sur les agents Windows ou Linux, qui contiennent des informations des journal. |
| [Journaux d’événements Windows](log-analytics-data-sources-windows-events.md) |Événement |Événements collectés à partir du journal des événements hello sur les ordinateurs Windows. |
| [Compteurs de performances Windows](log-analytics-data-sources-performance-counters.md) |Perf |Compteurs de performances collectés à partir d’ordinateurs Windows. |
| [Compteurs de performances Linux](log-analytics-data-sources-performance-counters.md) |Perf |Compteurs de performances collectés à partir d’ordinateurs Linux. |
| [Journaux IIS](log-analytics-data-sources-iis-logs.md) |W3CIISLog |Journaux d’Internet Information Services (IIS) au format W3C. |
| [Syslog](log-analytics-data-sources-syslog.md) |syslog |Événements Syslog sur des ordinateurs Windows ou Linux. |

## <a name="configuring-data-sources"></a>Configuration des sources de données
Vous configurez des sources de données à partir de hello **données** menu Analytique de journal **paramètres**.  N’importe quelle configuration est remise sources tooall connecté dans votre espace de travail OMS.  Nous ne pouvez actuellement exclure aucun agents de cette configuration.

![Configurer les événements Windows](./media/log-analytics-data-sources/configure-events.png)

1. Dans la console OMS hello, cliquez sur hello **paramètres** vignette ou hello **paramètres** bouton haut hello écran hello.
2. Sélectionnez **Données**.
3. Cliquez sur tooconfigure de source de données hello.
4. Consultez la documentation de toohello de lien de hello pour chaque source de données Bonjour au-dessus de la table pour plus d’informations sur leur configuration.

> [!NOTE]
> Actuellement, vous ne peut pas configurer les sources de données Analytique de journal Bonjour portail Azure.

## <a name="data-collection"></a>Collecte des données
Configurations de source de données sont remises tooagents qui sont connecté directement tooLog Analytique dans quelques minutes.  Hello spécifié les données sont collectées à partir de l’agent de hello et remises directement tooLog Analytique de source de données spécifique tooeach intervalles.  Consultez la documentation hello pour chaque source de données pour ces caractéristiques.

Pour les agents de System Center Operations Manager (SCOM) dans un groupe d’administration connecté, les configurations de source de données sont traduites en packs d’administration et remises de groupe d’administration toohello toutes les 5 minutes par défaut.  l’agent de Hello télécharge le pack d’administration hello comme tout autre et collecte hello de données spécifié. Bonjour Bonjour de source de données en fonction des données seront que tooa management server, qui transfère hello données toohello Analytique de journal envoyé ou hello agent envoie des données de hello tooLog Analytique sans passer par le serveur d’administration hello. Consultez trop[détails de collecte de données pour les solutions et fonctionnalités OMS](log-analytics-add-solutions.md#data-collection-details) pour plus d’informations.  Vous pouvez lire sur les détails de connexion SCOM et OMS et la modification de la fréquence de hello que la configuration est remis à [configurer l’intégration avec System Center Operations Manager](log-analytics-om-agents.md).

Si l’agent de hello est impossible tooconnect tooLog Analytique ou Operations Manager, il continue des données toocollect qu’elle fournira lorsqu’elle établit une connexion.  Données peuvent être perdues si hello de données atteint hello taille maximale du cache pour le client de hello, ou si l’agent hello n’est pas en mesure de tooestablish une connexion dans les 24 heures.

## <a name="log-analytics-records"></a>Enregistrements Log Analytics
Toutes les données collectées par Analytique de journal est stocké dans le référentiel d’OMS hello sous forme d’enregistrements.  Les enregistrements collectés par différentes sources de données auront leur propre jeu de propriétés et seront identifiés par leur propriété **Type** .  Consultez la documentation de hello pour chaque source de données et de solution pour plus d’informations sur chaque type d’enregistrement.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [solutions](log-analytics-add-solutions.md) qui ajouter des fonctionnalités tooLog Analytique et également collecter des données dans le référentiel d’OMS hello.
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles.  
* Configurer [alertes](log-analytics-alerts.md) tooproactively vous avertir des données critiques collectées à partir de sources de données et les solutions possibles.
