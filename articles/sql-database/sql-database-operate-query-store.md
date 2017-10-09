---
title: "aaaOperating magasin de requêtes de base de données SQL Azure"
description: "Découvrez comment toooperate hello magasin de requêtes de base de données SQL Azure"
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a>Fonctionnement hello magasin de requêtes de base de données SQL Azure
Le magasin de requêtes dans Azure est une fonctionnalité de base de données entièrement gérée qui recueille et présente des informations historiques détaillées sur toutes les requêtes. Vous pouvez considérer le magasin de requêtes en tant que l’enregistreur de données de vol d’avion tooan similaire qui simplifie la résolution des problèmes à la fois pour le cloud de performances de requête et de façon considérable clients locaux. Cet article présente certains aspects de l’utilisation du magasin de requêtes dans Azure. À l’aide des données de requête collectées au préalable, vous pouvez diagnostiquer et résoudre rapidement les problèmes de performances, ce qui vous permet de consacrer davantage de temps à vos activités. 

Le magasin de requêtes est [disponible dans le monde entier](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) via la base de données SQL Azure depuis novembre 2015. Magasin de requêtes est foundation hello pour l’analyse des performances et de réglage des fonctionnalités, telles que [Assistant de base de données SQL et le tableau de bord performances](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). Moment hello de publication de cet article, le magasin de requêtes est en cours d’exécution dans plus de 200 000 bases de données utilisateur dans Azure, collecte des informations liées à la requête depuis plusieurs mois, sans interruption.

> [!IMPORTANT]
> Microsoft est en cours de hello de l’activation du magasin de requêtes pour toutes les bases de données SQL Azure (existants et nouveaux). 
> 
> 

## <a name="optimal-query-store-configuration"></a>Configuration optimale du magasin de requêtes
Cette section décrit les valeurs par défaut de la configuration optimale qui sont conçus tooensure un fonctionnement fiable du magasin de requêtes hello et des composants dépendants, tels que [Assistant de base de données SQL et le tableau de bord performances](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). La configuration par défaut est optimisée pour la collecte des données en continu, c’est-à-dire pour passer le moins de temps possible aux états OFF/READ_ONLY.

| Configuration | Description | Default | Commentaire |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |Spécifie la limite de hello pour l’espace de données hello magasin de requêtes peut prendre au sein de la base de données client z |100 |Appliqué aux nouvelles bases de données |
| INTERVAL_LENGTH_MINUTES |Définit la durée pendant laquelle les statistiques d’exécution collectées pour les plans de requête sont agrégées et rendues persistantes. Chaque plan de requête actif dispose au maximum d’une ligne pour une période définie avec cette configuration |60 |Appliqué aux nouvelles bases de données |
| STALE_QUERY_THRESHOLD_DAYS |Stratégie de nettoyage basée sur le temps qui contrôle la période de rétention de hello de statistiques d’exécution persistantes et des requêtes inactives |30 |Appliqué aux nouvelles bases de données et aux bases de données ayant la valeur par défaut précédente (367) |
| SIZE_BASED_CLEANUP_MODE |Spécifie si le nettoyage automatique des données a lieu lorsque la taille des données de magasin de requêtes est proche de limite de hello |AUTO |Appliqué à toutes les bases de données |
| QUERY_CAPTURE_MODE |Indique si toutes les requêtes sont suivies, ou seulement un sous-ensemble de requêtes |AUTO |Appliqué à toutes les bases de données |
| FLUSH_INTERVAL_SECONDS |Spécifie la durée maximale pendant laquelle les statistiques d’exécution capturé sont conservées en mémoire, avant de vider les toodisk |900 |Appliqué aux nouvelles bases de données |
|  | | | |

> [!IMPORTANT]
> Ces valeurs par défaut sont automatiquement appliquées dans hello dernière étape de l’activation du magasin de requêtes dans toutes les bases de données SQL Azure (voir la Remarque importante ci-dessus). Après cette alléger, base de données SQL Azure ne modifier les valeurs de configuration définies par les clients, sauf si elles un impact négatif sur les opérations fiables Hello magasin de requêtes ou charge de travail principale.
> 
> 

Si vous souhaitez toostay avec vos paramètres personnalisés, utilisez [modifier la base de données avec les options du magasin de requêtes](https://msdn.microsoft.com/library/bb522682.aspx) état précédent de toorevert configuration toohello. Extraire [Best Practices with hello magasin de requêtes](https://msdn.microsoft.com/library/mt604821.aspx) dans l’ordre toolearn comment supérieur choisi des paramètres de configuration optimale.

## <a name="next-steps"></a>Étapes suivantes
[Informations sur les performances des bases de données SQL](sql-database-performance.md)

## <a name="additional-resources"></a>Ressources supplémentaires
Pour plus d’informations extraction hello suivant des articles :

* [Un enregistreur de données pour votre base de données](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [Analyse des performances à l’aide de magasin de requêtes hello](https://msdn.microsoft.com/library/dn817826.aspx)
* [Scénarios d’utilisation du magasin de requêtes](https://msdn.microsoft.com/library/mt614796.aspx)
* [Analyse des performances à l’aide de magasin de requêtes hello](https://msdn.microsoft.com/library/dn817826.aspx) 

