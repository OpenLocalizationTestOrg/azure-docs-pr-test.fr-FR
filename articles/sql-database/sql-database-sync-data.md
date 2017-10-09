---
title: "données d’aaaSync (version préliminaire) | Documents Microsoft"
description: "Cette vue d’ensemble présente Azure SQL Data Sync (aperçu)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: douglasl
ms.openlocfilehash: d5b2bbd6a502ba94dba7fb309a6583d2d95cc1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a>Synchroniser des données sur plusieurs bases de données cloud et locales avec SQL Data Sync

Synchronisation des données SQL est un service basé sur la base de données SQL Azure qui vous permet de synchroniser les données hello sélectionnées de façon bidirectionnelle entre plusieurs bases de données SQL et les instances de SQL Server.

Synchronisation des données est basée sur le concept de hello d’un groupe de synchronisation. Un groupe de synchronisation est un groupe de bases de données que vous souhaitez toosynchronize.

Un groupe de synchronisation a hello propriétés suivantes :

-   Hello **schéma de synchronisation** décrit les données sont en cours de synchronisation.

-   Hello **sens de synchronisation** peut être bidirectionnel ou peuvent circuler dans une seule direction. Autrement dit, les hello sens de synchronisation peut être *Hub tooMember* ou *membre tooHub*, ou les deux.

-   Hello **intervalle de synchronisation** est la fréquence à laquelle la synchronisation se produit.

-   Hello **stratégie de résolution de conflit** est une stratégie au niveau groupe, qui peut être *priorité au concentrateur* ou *wins de membre*.

Synchronisation des données utilise un hub et spoke topologie toosynchronize de données. Définissez une des bases de données hello dans le groupe de hello comme hello de base de données concentrateur. Hello autres bases de données hello sont des bases de données de membre. La synchronisation se produit uniquement entre hello Hub et les membres individuels.
-   Hello **base de données concentrateur** doit être une base de données SQL Azure.
-   Hello **bases de données membres** peuvent être des bases de données SQL, des bases de données SQL Server sur site ou des instances de SQL Server sur des machines virtuelles.
-   Hello **base de données de synchronisation** contient les journaux et les métadonnées de hello pour synchronisation de données. hello de base de données de synchronisation a toobe une base de données SQL Azure situé dans hello même région que hello de base de données concentrateur. Hello de base de données de synchronisation est client créé et la propriété du client.

> [!NOTE]
> Si vous utilisez une base de données sur site, vous avez trop[configurer un agent local.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)

![Synchroniser des données entre des bases de données](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-toouse-data-sync"></a>Lors de la synchronisation des données toouse

Synchronisation des données est utile dans les cas où les données doivent toobe tenir toodate entre plusieurs bases de données SQL Azure ou les bases de données SQL Server. Voici hello principaux cas d’utilisation pour la synchronisation des données :

-   **La synchronisation de données hybride :** avec synchronisation des données, vous pouvez conserver les données synchronisées entre vos bases de données locales et les applications de bases de données SQL Azure tooenable hybrides. Cette fonctionnalité peut faire appel toocustomers qui envisagent de déplacement toohello cloud et souhaitez tooput certaines de leurs applications dans Azure.

-   **Les Applications distribuées :** dans de nombreux cas, il est bénéfique tooseparate différentes charges de travail entre les différentes bases de données. Par exemple, si vous disposez d’une base de données de production de grande taille, mais vous devez également toorun une création de rapports ou la charge de travail analytique sur ces données, il est utile toohave une seconde base de données pour cette charge de travail supplémentaire. Cette approche réduit l’impact sur les performances hello sur votre charge de travail de production. Vous pouvez utiliser tookeep de synchronisation des données ces deux bases de données synchronisées.

-   **Applications distribuées globalement :** De nombreuses entreprises sont présentes dans plusieurs régions et même dans plusieurs pays. toominimize latence du réseau, il s’agit des meilleures toohave vos données dans une région de fermer tooyou. Avec la synchronisation des données, vous pouvez facilement conserver des bases de données dans des régions monde hello synchronisé.

Nous ne recommandons pas de synchronisation des données pourquoi les scénarios suivants :

-   Récupération d’urgence

-   Mise à l’échelle en lecture

-   ETL (tooOLAP OLTP)

-   Migration à partir de tooAzure de SQL Server sur site de la base de données SQL

## <a name="how-does-data-sync-work"></a>Comment fonctionne Data Sync ? 

-   **Suivi des modifications de données :** Data Sync effectue le suivi des modifications en utilisant des déclencheurs d’insertion, de mise à jour et de suppression. modifications de Hello sont enregistrées dans une table latérale dans la base de données utilisateur hello.

-   **Synchronisation des données :** Data Sync est conçu dans un modèle de Hub and Spoke. Hello concentrateur se synchronise avec chaque membre individuellement. Modifications de hello Hub sont téléchargées toohello membre et puis modifications du membre de hello sont téléchargée toohello Hub.

-   **Résolution des conflits :** Data Sync fournit deux options pour la résolution de conflit, *Priorité au hub* ou *Priorité au membre*.
    -   Si vous sélectionnez *priorité au concentrateur*, modifications hello dans le hub de hello remplacent toujours les modifications dans le membre de hello.
    -   Si vous sélectionnez *wins de membre*, hello des modifications dans les modifications dans le hub de hello remplacer des membres hello. S’il existe plusieurs membres, valeur finale de hello varie selon le membre qui se synchronise tout d’abord.

## <a name="limitations-and-considerations"></a>Limitations et considérations

### <a name="performance-impact"></a>Impact sur les performances
Synchronisation de données utilise insérer, mettre à jour et supprimer les modifications de tootrack de déclencheurs. Il crée les tables de côté dans la base de données utilisateur hello pour le suivi des modifications. Ces activités de suivi des modifications ont un impact sur votre charge de travail de base de données. Évaluez votre niveau de service et effectuez une mise à niveau si nécessaire.

### <a name="eventual-consistency"></a>Cohérence éventuelle
Étant donné que Data Sync est basé sur le déclencheur, la cohérence transactionnelle n’est pas garantie. Microsoft garantit que toutes les modifications sont effectuées par la suite et que Data Sync n’entraîne pas de perte de données.

### <a name="unsupported-data-types"></a>Types de données non pris en charge

-   FileStream

-   SQL/CLR UDT

-   XMLSchemaCollection (prise en charge de XML)

-   Curseur, horodateur, hierarchyid

### <a name="requirements"></a>Configuration requise

-   Chaque table doit avoir une clé primaire.

-   Une table ne peut pas avoir une colonne d’identité qui n’est pas de clé primaire de hello.

-   noms Hello d’objets (bases de données, tables et colonnes) ne peut pas contenir hello caractères imprimables point (.), crochets ([et]), de gauche ou crochet droit (]).

### <a name="limitations-on-service-and-database-dimensions"></a>Limitations des dimensions de la base de données et du service

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| **Dimensions**                                                      | **Limite**              | **Solution de contournement**              |
| Nombre maximal de groupes de synchronisation auquel peut appartenir une base de données.       | 5                      |                             |
| Nombre maximal de points de terminaison dans un seul groupe de synchronisation              | 30                     | Créer plusieurs groupes de synchronisation |
| Nombre maximal de points de terminaison locaux dans un seul groupe de synchronisation. | 5                      | Créer plusieurs groupes de synchronisation |
| Noms de la base de données, de la table, du schéma et des colonnes                       | 50 caractères par nom |                             |
| Tables dans un groupe de synchronisation                                          | 500                    | Créer plusieurs groupes de synchronisation |
| Colonnes d’une table dans un groupe de synchronisation                              | 1 000                   |                             |
| Taille de ligne de données sur une table                                        | 24 Mo                  |                             |
| Intervalle de synchronisation minimale                                           | 5 minutes              |                             |

## <a name="common-questions"></a>Questions courantes

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a>À quelle fréquence Data Sync synchronise-t-il mes données ? 
une fréquence minimale Hello est de cinq minutes.

### <a name="can-i-use-data-sync-toosync-between-sql-server-on-premises-databases-only"></a>Puis-je utiliser toosync de synchronisation des données entre SQL Server sur les bases de données locales uniquement ? 
Pas directement. Vous pouvez synchroniser entre les bases de données SQL Server sur site indirectement, toutefois, en créant une base de données concentrateur dans Azure et en ajoutant ensuite le groupe de synchronisation toohello hello local bases de données.
   
### <a name="can-i-use-data-sync-tooseed-data-from-my-production-database-tooan-empty-database-and-then-keep-them-synchronized"></a>Puis-je utiliser des données de tooseed de synchronisation des données de ma base de données de production de base de données tooan vide et alors puis de les garder synchronisés ? 
Oui. Créer manuellement le schéma de hello dans la nouvelle base de données hello par script hello d’origine. Après avoir créé le schéma de hello, ajouter des données hello toocopy de la synchronisation tooa hello tables groupe et qu’il soit synchronisé.

### <a name="why-do-i-see-tables-that-i-did-not-create"></a>Pourquoi puis-je voir des tables que je n’ai pas créées ?  
Data Sync crée des tables latérales dans votre base de données utilisateur pour le suivi des modifications. Ne les supprimez pas, sinon Data Sync cessera de fonctionner.
   
### <a name="i-got-an-error-message-that-said-cannot-insert-hello-value-null-into-hello-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-hello-error"></a>J’ai reçu un message d’erreur qui dit » ne peut pas insérer de valeur de hello NULL dans la colonne de hello \<colonne\>. Cette colonne n’accepte pas les valeurs NULL. » Cela signifie et comment puis-je corriger l’erreur de hello ? 
Ce message d’erreur indique un des problèmes suivants de hello deux :
1.  Une table sans clé primaire existe peut-être. toofix ce problème, ajoutez une tooall de clé primaire des tables hello vous synchronisez.
2.  Une clause WHERE existe peut-être dans votre instruction CREATE INDEX. La synchronisation ne gère pas cette condition. toofix ce problème, supprimez hello clause WHERE ou modifier manuellement hello tooall de bases de données. 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-hello-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a>Comment Data Sync traite-t-il les références circulaires ? Autrement dit, lorsque hello mêmes données est synchronisées dans plusieurs groupes de synchronisation et change constamment en conséquence ?
Data Sync ne traite pas les références circulaires. Être tooavoid que les. 

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur SQL Data Sync, consultez :

-   [Prise en main de SQL Data Sync](sql-database-get-started-sql-data-sync.md)

-   Exécuter PowerShell des exemples qui montrent comment la synchronisation des données SQL tooconfigure :
    -   [Utilisez toosync PowerShell entre plusieurs bases de données SQL Azure](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [Utilisez toosync PowerShell entre une base de données SQL Azure et une base de données locale SQL Server](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [Téléchargez la documentation technique hello complète synchronisation des données SQL](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [Télécharger la documentation des API REST de SQL Data Sync hello](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

Pour plus d’informations sur SQL Database, consultez :

-   [Vue d’ensemble des bases de données SQL](sql-database-technical-overview.md)

-   [Gestion du cycle de vie des bases de données](https://msdn.microsoft.com/library/jj907294.aspx)
