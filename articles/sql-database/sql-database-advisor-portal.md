---
title: "recommandations relatives aux performances aaaApply - base de données SQL Azure | Documents Microsoft"
description: "Vous pouvez utiliser hello toofind portail Azure recommandations relatives aux performances que vous pouvez optimiser les performances de votre base de données SQL Azure ou de toocorrect un problème identifié dans votre charge de travail."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a>Rechercher et appliquer les recommandations en matière de performances

Vous pouvez utiliser hello toofind portail Azure recommandations relatives aux performances que vous pouvez optimiser les performances de votre base de données SQL Azure ou de toocorrect un problème identifié dans votre charge de travail. **Recommandation de performances** page du portail Azure vous permet de meilleures recommandations toofind hello en fonction de leur impact potentiel. 

## <a name="viewing-recommendations"></a>Affichage des recommandations

tooview et appliquer les recommandations relatives aux performances, vous devez hello correct [contrôle d’accès basé sur le rôle](../active-directory/role-based-access-control-what-is.md) autorisations dans Azure. **Lecteur**, **collaborateur de base de données SQL** autorisations sont requises tooview recommandations, et **propriétaire**, **collaborateur de base de données SQL** autorisations sont requises tooexecute toutes les actions ; créer ou supprimer des index et annuler la création d’index.

Utilisez hello suivant les recommandations relatives aux performances d’étapes toofind de portail Azure :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Accédez trop**davantage de services** > **bases de données SQL**, sélectionnez votre base de données.
3. Accédez trop**recommandation de performances** tooview des recommandations disponibles pour la base de données sélectionnée hello.

Recommandations relatives aux performances sont shonw dans toohello similaire hello table celui affiché sur hello figure suivante :

![Recommandations](./media/sql-database-advisor-portal/recommendations.png)

Recommandations sont triées par leur impact potentiel sur les performances en hello suivant des catégories :

| Impact | Description |
|:--- |:--- |
| Élevé |Recommandations de fort impact doivent fournir l’impact sur les performances significatives hello. |
| Moyenne |Les recommandations ayant un impact moyen améliorent les performances, mais pas de manière substantielle. |
| Faible |Les recommandations ayant un faible impact fournissent de meilleures performances, mais les améliorations ne sont toutefois pas significatives. |


> [!NOTE]
> Base de données SQL Azure doit toomonitor activités au moins un jour dans l’ordre tooidentify quelques recommandations. Hello, base de données SQL Azure peut optimiser plus facilement des modèles de requête cohérente que possible pour les pics inégale aléatoires d’activité. Si les recommandations ne sont pas Joins disponibles, hello **recommandation de performances** page affiche un message en explique la raison.
> 

Vous pouvez également afficher des opérations historiques hello état hello. Sélectionnez un toosee recommandation ou état plus de détails.

Voici un exemple de « Créer un index » de recommandation dans hello portail Azure.

![Création d’index](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a>Application des recommandations
Base de données SQL Azure vous offre un contrôle total sur la façon dont les recommandations sont activées à l’aide de hello trois options suivantes : 

* Appliquer les recommandations individuelles une à la fois.
* Activer hello tooautomatically paramétrage automatique appliquer les recommandations.
* tooimplement une recommandation exécuter manuellement, hello recommandé de script T-SQL sur votre base de données.

Sélectionnez n’importe quel tooview recommandation ses détails, puis cliquez **afficher le script** tooreview hello des informations précises concernant la création de recommandation de hello.

base de données Hello reste en ligne pendant que la recommandation de hello est appliquée, à l’aide de la recommandation de performances ou le paramétrage automatique jamais met une base de données hors connexion.

### <a name="apply-an-individual-recommendation"></a>Appliquer une recommandation individuelle
Vous pouvez consulter et accepter les recommandations une à la fois.

1. Sur hello **recommandations** panneau, sélectionnez une recommandation.
2. Sur hello **détails** cliquez sur le panneau **appliquer** bouton.
   
    ![Appliquer une recommandation](./media/sql-database-advisor-portal/apply.png)

Recommandation sélectionnée est appliquée sur la base de données hello.

### <a name="removing-recommendations-from-hello-list"></a>Suppression de recommandations à partir de la liste de hello
Si votre liste de recommandations contient les éléments que vous souhaitez tooremove à partir de la liste de hello, vous pouvez ignorer la recommandation de hello :

1. Sélectionnez une recommandation dans la liste des hello **recommandations** détails de hello tooopen.
2. Cliquez sur **ignorer** sur hello **détails** panneau.

Si vous le souhaitez, vous pouvez ajouter des éléments rejetés sauvegarder toohello **recommandations** liste :

1. Sur hello **recommandations** cliquez sur le panneau **vue ignorée**.
2. Sélectionnez un élément ignoré hello liste tooview ses détails.
3. Si vous le souhaitez, cliquez sur **Annuler ignorer** tooadd hello index différé toohello liste principale de **recommandations**.


### <a name="enable-automatic-tuning"></a>Activer le réglage automatique
Vous pouvez définir automatiquement les recommandations de tooimplement de base de données SQL Azure hello. Dès qu’une recommandation est disponible, elle est automatiquement appliquée. Comme avec toutes les recommandations sont gérées par hello service si l’impact sur les performances hello est recommandation de hello négatif vont être annulée.

1. Sur hello **recommandations** panneau, cliquez sur **automatiser**:
   
    ![Paramètres du conseiller](./media/sql-database-advisor-portal/settings.png)
2. Sélectionnez les actions tooautomate :
   
    ![Index recommandés](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a>Exécuter manuellement hello recommandé de script T-SQL
Sélectionnez une recommandation, puis cliquez sur **Afficher le script**. Exécutez ce script sur votre base de données toomanually appliquer la recommandation de hello.

*Index qui sont exécutés manuellement ne sont pas surveillées et validés pour l’impact sur les performances par le service de hello* donc il est recommandé de surveiller ces index après la création tooverify qu’ils fournissent des gains de performance et ajuster ou supprimez-les nécessaire. Pour plus d’informations sur la création d’index, consultez [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).

### <a name="canceling-recommendations"></a>Annulation de recommandations
Les recommandations ayant l’état **En attente**, **En cours de vérification** ou **Réussite** peuvent être annulées. Les recommandations avec l'état **En cours d'exécution** ne peuvent pas être annulées.

1. Sélectionnez une recommandation Bonjour **de paramétrage de l’historique** hello tooopen de zone **les détails des recommandations** panneau.
2. Cliquez sur **Annuler** tooabort hello consistant à appliquer la recommandation de hello.

## <a name="monitoring-operations"></a>Surveillance des opérations
L’application d’une recommandation ne se produit pas toujours instantanément. portail de Hello fournit des détails concernant l’état de hello de recommandation. Hello Voici les états possibles que peut contenir un index :

| État | Description |
|:--- |:--- |
| Pending |La commande Appliquer la recommandation a été reçue et son exécution est planifiée. |
| En cours d'exécution |recommandation de Hello est appliquée. |
| Vérification |Recommandation a été correctement appliquée et le service de hello mesure les avantages de hello. |
| Succès |La recommandation a été correctement appliquée et les avantages ont été évalués. |
| Error |Une erreur s’est produite pendant le processus hello de l’application de la recommandation de hello. Cela peut être un problème temporaire, ou éventuellement une table de toohello de modifications de schéma et hello script n’est plus valide. |
| Annulation |recommandation de Hello a été appliquée, mais il a été jugée non performantes et est en cours de rétablissement automatiquement. |
| Annulée |recommandation de Hello a été annulée. |

Cliquez sur une recommandation dans le processus de hello liste toosee plus de détails :

![Index recommandés](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a>Annulation d'une recommandation
Si vous avez utilisé la recommandation de hello hello performances recommandations tooapply (ce qui signifie que vous n’avez exécuté pas manuellement les script hello T-SQL) il est automatiquement rétabli il s’il en trouve hello performance impact toobe négatif. Si pour une raison quelconque vous souhaitez simplement toorevert une recommandation faire suivant de hello :

1. Sélectionnez une recommandation appliquée correctement Bonjour **paramétrage historique** zone.
2. Cliquez sur **Revert** sur hello **détails de la recommandation** panneau.

![Index recommandés](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a>Analyse de l’impact des recommandations d’index sur les performances
Une fois que les recommandations sont correctement mises en œuvre (actuellement, les opérations d’index et paramétrer des recommandations de requêtes uniquement) vous pouvez cliquer sur **analyse des requêtes** sur hello recommandation détails panneau tooopen [requête Analyse des performances](sql-database-query-performance.md) et voir l’impact sur les performances hello de vos requêtes principales.

![Surveiller l’impact sur les performances](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a>Résumé
Azure SQL Database fournit des recommandations pour améliorer les performances des bases de données SQL. Les scripts T-SQL, ainsi que les options individuelles et entièrement automatiques, facilitent l’optimisation de votre base de données, avec à la clé une amélioration des performances des requêtes.

## <a name="next-steps"></a>Étapes suivantes
Surveiller vos recommandations et continuer tooapply les performances de toorefine. Les charges de travail d’une base de données sont dynamiques et évoluent en permanence. Base de données SQL Azure seront continuer toomonitor et fournir des recommandations qui peuvent permettre d’améliorer les performances de votre base de données. 

* Consultez [le paramétrage automatique](sql-database-automatic-tuning.md) toolearn savoir plus sur hello réglage automatique dans la base de données SQL Azure.
* Consultez [Recommandations en matière de performances](sql-database-advisor.md) pour obtenir une vue d’ensemble des recommandations relatives aux performances Azure SQL Database.
* Consultez [analyse des performances des requêtes](sql-database-query-performance.md) toolearn sur l’affichage des performances hello de vos requêtes principales.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Magasin de requêtes](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [Contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-what-is.md)

