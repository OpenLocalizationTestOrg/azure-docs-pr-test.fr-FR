---
title: "Les plateformes Analytique : Apache Storm comparaison tooStream Analytique | Documents Microsoft"
description: "Obtenez des conseils en choisissant une plateforme en nuage analytique à l’aide d’un tooStream de comparaison d’Apache Storm Analytique. Découvrez les fonctionnalités et les différences."
keywords: "plateforme d’analyse, plateformes d’analyse, plateforme d’analyse cloud, comparaison avec storm"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a>Choix d’une plateforme d’analyse de flux : comparaison d’Apache Storm et d’Azure Stream Analytics
Azure fournit plusieurs solutions pour analyser les données de flux : [Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/) et [Apache Storm sur Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/). Les deux plateformes analytique offrent des avantages de hello d’une solution PaaS. Mais les plateformes hello aient des différences significatives dans leurs fonctionnalités, ainsi que dans la façon dont vous configurez et les gérez. 

Cet article offre une comparaison côte-à-côte toohelp fonctionnalités que vous choisissez entre Apache Storm et Analytique de flux de données Azure comme plateforme cloud analytique. 

## <a name="general-features"></a>Fonctionnalités générales

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong></strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm sur HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Open Source ?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Non. Azure Stream Analytics est une offre propriétaire de Microsoft.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Oui. Apache Storm est une technologie sous licence Apache.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Support Microsoft ?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Oui </p>
            </td>
            <td width="246" valign="top">
                <p>
Oui </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Configuration matérielle requise</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Aucune. Azure Stream Analytics est un service Azure.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Aucune. Apache Storm est un service Azure.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Unité de niveau supérieur</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Les utilisateurs déploient et surveillent les travaux de diffusion en continu.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Les utilisateurs déploient et surveillent un cluster entier, qui peut héberger plusieurs travaux Storm ainsi que d’autres charges de travail (notamment le traitement).
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Tarification</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Prix par volume de données traitées et nombre de hello d’unités de diffusion requis par heure qui hello de travail est en cours d’exécution. 
                </p>
                    <p>Pour plus d’informations, voir <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Tarification de Stream Analytics </a>.</p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
unité Hello d’achat est basé sur le cluster et est facturée en fonction hello exécution de cluster de hello, indépendante des tâches de déploiement.
                </p>
                <p>
Pour plus d’informations, voir <a href="http://azure.microsoft.com/pricing/details/hdinsight/">Tarification de HDInsight</a>.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a>Création

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong></strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm sur HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Fonctionnalités : langage DSL SQL ?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Oui. Stream Analytics fournit un langage de type SQL pour créer des transformations.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Non. Les utilisateurs écrivent du code en Java ou en C#, ou ils utilisent les API Trident.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Fonctionnalités : opérateurs temporels ?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Les agrégats fenêtrés et les jointures temporelles sont pris en charge par défaut.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Opérateurs temporels doivent être implémentées par l’utilisateur de hello.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Expérience de développement</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Les utilisateurs peuvent créer, déboguer et surveiller les travaux via hello portail Azure, à l’aide des exemples de données dérivés d’un flux en direct.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
À l’aide de .NET, les utilisateurs peuvent développer, déboguer et surveiller au moyen de Visual Studio. Utilisateurs à l’aide de Java ou autres langages peuvent utiliser hello IDE de leur choix.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Prise en charge du débogage</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Les journaux d’état et les opérations de base de travail sont disponibles toohelp debug. Analytique de flux de données actuellement ne permet pas aux utilisateurs spécifier quel contenu ou la quantité de contenu est inclus dans les journaux hello (autrement dit, le mode détaillé).
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Des journaux détaillés sont disponibles. Les utilisateurs peuvent accéder à des journaux dans Visual Studio ou en vous connectant toohello cluster et accéder directement aux journaux de hello.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Extensibilité à l’aide de code personnalisé ?</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Prend partiellement en charge les fonctions JavaScript. Pour plus d’informations, voir <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">Intégration d’UDF JavaScript</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Oui. Les utilisateurs peuvent écrire du code personnalisé en C#, Java ou dans tout autre langage pris en charge sur Storm.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a>Sources de données (entrées) et sorties ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong></strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm sur HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                 <strong>Sources de données d’entrée</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>Azure Event Hubs et stockage Blob Azure.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Des connecteurs sont disponibles pour Azure Event Hubs, Azure Service Bus, Kafka, etc. Les utilisateurs peuvent créer des connecteurs supplémentaires à l’aide de code personnalisé.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Formats de données d’entrée</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Avro, JSON, CSV </p>
            </td>
            <td width="246" valign="top">
                <p>
Les utilisateurs peuvent implémenter tout format à l’aide de code personnalisé.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Sorties</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Un travail de diffusion en continu peut compter plusieurs sorties. Sorties prises en charge : Azure Event Hubs, stockage Blob Azure, stockage Table Azure, Azure SQL DB et Power BI.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Storm prend en charge de nombreuses sorties dans une topologie, et chacune peut disposer d’une logique personnalisée pour le traitement en aval. Storm inclut des connecteurs pour Power BI, Azure Event Hubs, le stockage Blob Azure, Azure Cosmos DB, SQL et HBase. Les utilisateurs peuvent créer des connecteurs supplémentaires à l’aide de code personnalisé.    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Formats d’encodage des données</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Les données doivent être formatées à l’aide de UTF-8.
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
Les utilisateurs peuvent implémenter tout format d’encodage des données à l’aide de code personnalisé.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a>Gestion et opérations ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong></strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm sur HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Modèle de déploiement de travail</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Portail Azure, PowerShell et interfaces API REST.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Portail Azure, PowerShell, Visual Studio et interfaces API REST.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Analyse (statistiques, compteurs, etc.)</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
L’analyse est implémentée via le portail Azure et les interfaces API REST. Les utilisateurs peuvent également configurer des alertes Azure.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Analyse est implémentée à l’aide de hello Storm UI et l’API REST.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Extensibilité</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
L’évolutivité est déterminée par le nombre de hello d’unités de diffusion en continu (SUs) pour chaque tâche. Chaque unité de diffusion en continu traite des too1 Mo par seconde, avec une capacité maximale de 50. Pour plus d’informations, consultez <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">débit tooincrease de mise à l’échelle</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
L’évolutivité est déterminée par le nombre de hello de nœuds de cluster HDInsight Storm de hello. Hello supérieur hello nombre limite de nœuds est définie par le quota de l’utilisateur hello Azure.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Limites de traitement des données</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Les utilisateurs peuvent augmenter le traitement des données ou optimiser les coûts en augmentant ou diminuant le nombre de hello d’unités de diffusion en continu, avec une limite supérieure de 1 Go par seconde.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Les utilisateurs peuvent mettre à l’échelle la taille du cluster en l’augmentant ou en la réduisant.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Arrêt/Reprise</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Arrêt et reprise à partir du dernier arrêt.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Arrêt et reprise à partir du dernier arrêt basé sur un filigrane.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Mise à jour de service et d’infrastructure</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Mise à jour corrective automatique sans temps d’arrêt.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Mise à jour corrective automatique sans temps d’arrêt.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Continuité d’activité via un service hautement disponible avec contrats SLA garantis</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li>Contrat SLA de temps d’activité de 99,9 %</li>
                <li>Récupération automatique des défaillances</li>
                <li>Récupération intégrée des opérateurs temporels avec état</li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
Contrat SLA de 99,9 % de cluster de Storm hello. 
                </p>
                <p>
Apache Storm est une plateforme de diffusion en continu à tolérance de panne. Toutefois, il est tooensure de responsabilité de l’utilisateur hello que de diffusion en continu exécution des travaux sans interruption.
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a>Fonctionnalités avancées ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong></strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
                    <strong>Azure Stream Analytics</strong>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
                    <strong>Apache Storm sur HDInsight</strong>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Arrivée tardive et gestion des événements de manière désordonnée</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Des stratégies configurables intégrées peuvent réorganiser et supprimer des événements ou régler leur heure.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Les utilisateurs doivent implémenter logique toohandle ce scénario.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Données de référence</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Les données de référence sont disponibles à partir du stockage Blob Azure avec un maximum de 100 Mo de cache en mémoire. Les données de référence sont actualisées par le service de hello.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Aucune limitation de la taille des données. Des connecteurs sont disponibles pour HBase, Azure Cosmos DB, SQL Server et Azure. Les utilisateurs peuvent créer des connecteurs supplémentaires à l’aide de code personnalisé. Les données de référence doivent être actualisées à l’aide de code personnalisé.
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p>
                    <strong>Intégration à Machine Learning</strong>
                </p>
            </td>
            <td width="204" valign="top">
                <p>
Les modèles Azure Machine Learning publiés peuvent être configurés en tant que fonctions lors de la création d’un travail. Pour plus d’informations, voir <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Mettre à l’échelle pour les fonctions Machine Learning</a>.
                </p>
            </td>
            <td width="246" valign="top">
                <p>
Disponible via Storm Bolts.
                </p>
            </td>
        </tr>
    </tbody>
</table>
