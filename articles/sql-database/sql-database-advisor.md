---
title: "recommandations aaaPerformance - base de données SQL Azure | Documents Microsoft"
description: "Hello, base de données SQL Azure fournit des recommandations pour vos bases de données SQL qui peut améliorer les performances des requêtes en cours."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: 1db441ff-58f5-45da-8d38-b54dc2aa6145
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 77db338a0a395aec78c9e02849ae5ba4f2d01680
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-recommendations"></a>Recommandations en matière de performances

Base de données SQL Azure apprend et s’adapte à votre application et fournit des recommandations personnalisées, ce qui vous toomaximize hello vos bases de données SQL. Vos performances sont évaluées en permanence grâce à l’analyse de votre historique d’utilisation de SQL Database. recommandations Hello fournis sont basées sur un modèle de charge de travail unique de base de données et d’améliorer ses performances.

> [!NOTE]
> Il est conseillé d’utiliser les recommandations en activant l’option de réglage automatique sur votre base de données. Pour en savoir plus, consultez la page [Réglage automatique](sql-database-automatic-tuning.md).
>

## <a name="create-index-recommendations"></a>Recommandations relatives à la création d’un index
Base de données SQL Azure surveille les requêtes hello en cours d’exécution et identifie les index hello qui peut améliorer les performances de hello en continu. Dès que la base de données estime qu’un index manque, une recommandation **Créer un index** est créée. Confiance de builds de la base de données SQL Azure en estimant index hello du gain de performances se traduirait par heure. Selon le gain de performances hello estimé, les recommandations sont classées comme haute, moyenne ou faible. 

Les index créés à l’aide de recommandations portent toujours l’indicateur auto_created. Vous pouvez voir quels index possèdent l’indicateur auto_created en examinant la vue sys.indexes. Les index créés automatiquement ne bloquent pas les commandes ALTER/RENAME. Si vous essayez de colonne hello toodrop ayant une automatique créée des index sur celle-ci, commande hello passe et auto hello créé l’index est supprimé avec la commande hello ainsi. Index classiques sont sont de bloquer commande ALTER/changement de nom de hello sur les colonnes qui sont indexées.

Une fois la création de hello recommandation d’index est appliquée, base de données SQL Azure seront comparer les performances des requêtes de hello aux performances de ligne de base hello. Si le nouvel index de remise des améliorations des performances hello, recommandation est signalée comme réussie et impact sur le rapport sera disponible. En cas d’index de hello n’a pas été avantageux hello, il vont être annulée automatiquement. Cette base de données SQL Azure de façon garantit qu’à l’aide des recommandations uniquement améliorera les performances de base de données hello.

N’importe quel **Create index** a une stratégie qui empêche l’application de la recommandation de hello si l’usage de DTU de base de données ou un pool hello était supérieure à 80 % en derniers 20 minutes ou si le stockage de hello est supérieure à 90 % de l’utilisation d’interruption. Dans ce cas, la recommandation de hello sera suspendue.

## <a name="drop-index-recommendations"></a>Recommandations relatives à la suppression d’index
En outre toodetecting un index manquant, Azure SQL Database en permanence analyse des performances de hello des index existants. Si l’index n’est pas utilisé, Azure SQL Database recommande sa suppression. Il est recommandé de supprimer un index dans deux cas :
* L’index est un doublon d’un autre index (même colonne, schéma de partition et filtres indexés et inclus)
* L’index n’est pas utilisé pendant une période prolongée (93 jours)

DROP index recommandations également passent par vérification hello après l’implémentation. Si les performances de hello impact hello améliorée rapport seront disponible. Si une dégradation du niveau de performance est détectée, la recommandation est restaurée.


## <a name="parameterize-queries-recommendations"></a>Recommandations de paramétrage de requêtes
**Paramétrez des requêtes** recommandations s’affichent lorsque vous en avez un ou plusieurs requêtes qui sont recompilées en permanence, mais au finissent hello même plan d’exécution de requête. Cette condition ouvre une tooapply opportunité forcé de paramétrage, ce qui permettra de plans de requête toobe mis en cache et réutilisée Bonjour futures améliore les performances et réduire l’utilisation des ressources. 

Chaque requête adressée à SQL Server initialement doit toobe compilé toogenerate un plan d’exécution. Chaque plan généré est ajouté toohello mémoire cache des plans et les exécutions ultérieures de hello même requête peut réutiliser ce plan à partir du cache de hello, hello évite une compilation supplémentaire. 

Les applications qui envoient des requêtes, y compris les valeurs non paramétrée, peuvent entraîner des tooa surcharge de performances, où pour chaque requête de ce type avec différentes valeurs de paramètre hello l’exécution du plan est compilé à nouveau. Dans nombreux hello de cas mêmes requêtes avec des paramètres différents génèrent des valeurs hello même plans d’exécution, mais ces plans sont ajoutés toujours séparément le cache du plan de toohello. Recompilation des plans d’exécution utilisent des ressources de base de données, augmentez hello durée temps et dépassement de capacité hello plan de requête à l’origine de la mémoire cache des plans toobe supprimé du cache de hello. Ce comportement de SQL Server peut être modifié en définissant hello forcé option parameterization sur la base de données hello. 

toohelp vous estimez impact hello de cette recommandation, vous sont fournies avec une comparaison entre les UC réel hello hello et l’utilisation projetée l’utilisation du processeur (comme si la recommandation de hello a été appliquée). En outre les économies tooCPU, votre durée de requête diminue pour hello temps de compilation. Il sera également beaucoup moins de surcharge sur le cache du plan, autorisant la majorité des hello toostay dans le cache des plans et être réutilisée. Vous pouvez appliquer cette recommandation rapidement et facilement en cliquant sur hello **appliquer** commande. 

Une fois que vous appliquez cette recommandation, il active le paramétrage forcé dans les minutes sur votre base de données et démarre hello analyse des processus qui dure environ 24 heures. Après cette période, vous allez être en mesure de toosee hello validation rapport qui affiche l’utilisation du processeur de votre base de données des dernières 24 heures avant et après avoir appliqué la recommandation de hello. Assistant de base de données SQL utilise un mécanisme de sécurité qui revient automatiquement la recommandation de hello appliqué au cas où une régression des performances a été détectée.

## <a name="fix-schema-issues-recommendations"></a>Recommandations de résolution des problèmes de schéma
**Résoudre les problèmes de schéma** recommandations s’affichent lorsque hello notifications de service de base de données SQL d’anomalie dans nombre hello d’erreurs SQL liées au schéma qui se passe sur votre base de données SQL Azure. Cette recommandation s’affiche généralement lorsque votre base de données rencontre plusieurs erreurs liées au schéma (nom de colonne non valide, nom d’objet non valide, etc.) dans la même heure.

« Problèmes de schéma » sont une classe d’erreurs de syntaxe dans SQL Server qui se produisent lors de la définition de hello de la requête SQL hello et la définition de hello du schéma de base de données hello ne sont pas alignées. Par exemple, une des colonnes hello attendus par la requête de hello est peut-être manquante dans la table cible de hello, ou vice versa. 

Recommandation de « Corriger le problème de schéma » s’affiche lorsque le service de base de données SQL Azure avis d’anomalie dans nombre hello d’erreurs SQL liées au schéma qui se passe sur votre base de données SQL Azure. Hello table affiche hello erreurs qui sont les problèmes connexes tooschema suivantes :

| Code d'erreur SQL | Message |
| --- | --- |
| 201 |La procédure ou fonction '*’ attend le paramètre ’*', qui n’a pas été fourni. |
| 207 |Nom de colonne non valide '*'. |
| 208 |Nom d'objet non valide ’*’. |
| 213 |Le nom de la colonne ou le nombre de valeurs fournies ne correspond pas à la définition de la table. |
| 2812 |Impossible de trouver la procédure stockée '*'. |
| 8144 |La procédure ou la fonction * a trop d’arguments spécifiés. |

## <a name="next-steps"></a>Étapes suivantes
Surveiller vos recommandations et continuer tooapply les performances de toorefine. Les charges de travail d’une base de données sont dynamiques et évoluent en permanence. Conseiller de la base de données SQL continue toomonitor et fournir des recommandations qui peuvent permettre d’améliorer les performances de votre base de données. 

* Consultez [recommandations relatives aux performances Bonjour Azure portal](sql-database-advisor-portal.md) pour savoir comment les recommandations relatives aux performances de toouse dans hello portail Azure.
* Consultez [analyse des performances des requêtes](sql-database-query-performance.md) toolearn sur et vue hello impact sur les performances de vos requêtes principales.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Magasin de requêtes](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [Contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-what-is.md)

