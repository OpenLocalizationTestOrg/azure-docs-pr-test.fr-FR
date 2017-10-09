---
title: "Forum aux questions (FAQ) sur Azure Search d’aaaFrequently | Documents Microsoft"
description: "Obtenir des réponses toocommon des questions sur le Service de recherche de Microsoft Azure"
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 2c573750600d80585b746bfce20d6c0f8df5a262
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Recherche Azure - Questions fréquentes (FAQ)
 
 Trouver toocommonly des réponses aux questions sur les concepts, scénarios et code liées tooAzure recherche.

## <a name="platform"></a>Plateforme

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>En quoi la Recherche Azure est-elle différente de la recherche en texte intégral de mon système de gestion de base de données (SGBD) ?

La Recherche Azure comprend les fonctionnalités suivantes : prise en charge de plusieurs sources de données, [analyse linguistique de nombreuses langues](https://docs.microsoft.com/rest/api/searchservice/language-support), [analyse personnalisée des entrées de données intéressantes et inhabituelles](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search), contrôles de classement des recherches par le biais de [profils de score](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index), tampon clavier, mise en surbrillance des résultats et navigation par facettes. Elle comprend également d’autres fonctionnalités, telles que les synonymes et une syntaxe de requête riche, toutefois ces fonctionnalités ne lui sont pas propres.

### <a name="what-is-hello-difference-between-azure-search-and-elasticsearch"></a>Qu’est la différence hello Azure Search et Elasticsearch ?

Lorsqu’ils comparent les technologies de recherche, les clients demandent souvent des précisions sur les différences entre la Recherche Azure et Elasticsearch. Les clients qui choisissent Azure Search sur Elasticsearch pour leur recherche les projets d’application généralement le faire car nous avons fait plus facilement les tâches importantes ou dont ils ont besoin d’intégration de hello avec d’autres technologies Microsoft :

+ La Recherche Azure est un service cloud entièrement géré, avec 99,9 % de contrats de niveau de service (SLA) lorsqu’elle reçoit suffisamment de redondance (2 réplicas pour l’accès en lecture, 3 réplicas pour l’accès en lecture-écriture).
+ Les [processeurs de langage naturel](https://docs.microsoft.com/rest/api/searchservice/language-support) Microsoft offrent une analyse linguistique à la pointe de la technologie.  
+ Les [indexeurs de la Recherche Azure](search-indexer-overview.md) peuvent analyser diverses sources de données Azure en vue d’une indexation initiale et incrémentielle.
+ Si vous devez toofluctuations une réponse rapide dans la requête ou de l’indexation des volumes, vous pouvez utiliser [contrôles slider](search-manage.md#scale-up-or-down) Bonjour portail Azure, ou exécuter un [script PowerShell](search-manage-powershell.md), en ignorant gestion de partition directement.  
+ [Calcul de score et les fonctionnalités de paramétrage](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) fournir hello pour influencer les scores de classement recherche au-delà du moteur de recherche hello seul peut fournir. 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>Puis-je suspendre le service Recherche Azure et arrêter la facturation ?

Vous ne pouvez pas suspendre le service de hello. Ressources de calcul et de stockage sont allouées pour une utilisation exclusive lorsque hello service est créé. Il n’est pas possible de toorelease et libérer ces ressources à la demande. 

## <a name="indexing-operations"></a>Opérations d’indexation

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>Est-il préférable d’utiliser des index de sauvegarde et de restauration (ou téléchargement et déplacement) ou des instantanés d’index ?

Bien que vous puissiez [obtenir une définition d’index](https://docs.microsoft.com/rest/api/searchservice/get-index) à tout moment, il n’existe aucune extraction de l’index, une capture instantanée ou une fonctionnalité de restauration de sauvegarde pour le téléchargement une *rempli* index en cours d’exécution dans le système local hello cloud tooa, ou déplacer service Azure Search de tooanother. 

Les index sont générés et remplis à partir de code que vous écrivez et s’exécutent uniquement sur Azure Search dans le cloud de hello. En règle générale, les clients qui souhaitent toomove un service de tooanother index faire en modifiant leur toouse code un nouveau point de terminaison et réexécutez l’indexation. Si vous souhaitez hello capacité tootake un instantané ou que vous sauvegardez un index, voter [User Voice](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index).

### <a name="can-i-index-from-sql-database-replicas-applies-tooazure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>Puis-je indexer à partir des réplicas de base de données SQL (s’applique également[indexeurs de la base de données SQL Azure](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers))

 Il n’existe aucune restriction sur l’utilisation de hello de réplicas principaux ou secondaires comme source de données lors de la création d’un index à partir de zéro. Toutefois, l’actualisation d’un index avec des mises à jour incrémentielles (basés sur les enregistrements modifiés) requiert réplica principal de hello. Cela vient du fait que SQL Database assure uniquement le suivi des modifications sur les réplicas principaux. Si vous essayez d’utiliser les réplicas secondaires pour une charge de travail de l’actualisation index, il n’est pas garanti que vous obtenez toutes les données hello.

## <a name="search-operations"></a>Opérations de recherche

### <a name="can-i-search-across-multiple-indexes"></a>Puis-je effectuer une recherche sur plusieurs index ?

Non, cette opération n’est pas prise en charge. Recherche est toujours tooa incluses dans l’étendue d’index.

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>Puis-je restreindre l’accès au corpus de recherche en fonction de l’identité de l’utilisateur ?

La Recherche Azure n’applique pas de modèle de sécurité basée sur les rôles pour l’accès aux données par utilisateur. L’authentification est soit droits d’accès complets ou en lecture seule au niveau de service hello. Certains clients ont implémenté des solutions basées sur le [paramètre de recherche `$filter`](https://docs.microsoft.com/rest/api/searchservice/search-documents), mais il s’agit seulement d’une solution de contournement. Si vous souhaitez que cette fonctionnalité soit ajoutée, votez sur [UserVoice](https://feedback.azure.com/forums/263029-azure-search/category/86074-security).

### <a name="why-are-there-zero-matches-on-terms-i-know-toobe-valid"></a>Pourquoi y a-t-il zéro correspond aux conditions que savoir toobe valide ?

cas le plus courant Hello n'est pas de savoir que chaque type de requête prend en charge les comportements de recherche différente et les niveaux d’analyses linguistiques. Recherche en texte intégral, qui est la charge de travail prédominant hello, comprend une phase d’analyse de langage qui interrompt les termes du contrat tooroot forms vers le bas. Cet aspect de l’analyse de requête convertit un réseau plus large sur les correspondances possibles, car hello terme sous forme de jeton correspond à un plus grand nombre de variantes.

Si vous appelez [d’autres types de requêtes](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (recherche par caractères génériques, recherche approximative, recherche de proximité, suggestions, etc.), aucune analyse linguistique n’est effectuée. Termes du contrat est ajouté toohello arborescence de requête en tant que-est. 

### <a name="why-is-hello-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>Pourquoi hello recherche rang est-il un score de constant ou égal de 1.0 pour chaque test ?

Par défaut, les résultats de la recherche sont notées en fonction de hello [propriétés statistiques des conditions de correspondance](search-lucene-query-architecture.md#stage-4-scoring)et classées toolow élevé dans le jeu de résultats hello. Toutefois, certains types (caractère générique, préfixe, regex) de requête contribue toujours à un score de constant toohello globale score de document. Ce comportement est normal. Azure Search impose une constante score des correspondances tooallow identifiés par la requête d’extension toobe est inclus dans les résultats de hello, sans affecter le classement de hello. 

Par exemple, supposons l’entrée « tour* » dans une recherche par caractères génériques, qui retourne les résultats « tours », « tourettes » et « tourmaline ». Compte tenu de nature hello de ces résultats, il est impossible tooreasonably déduire le termes du contrat est plus utile que d’autres. Pour cette raison, nous ignorons les fréquences de terme lors de la notation des résultats dans les requêtes avec caractère générique, préfixe et expression régulière. Résultats de la recherche basées sur une entrée partielle reçoivent une constante score décalage tooavoid vers correspondances potentiellement inattendus.

## <a name="design-patterns"></a>Modèles de conception

### <a name="what-is-hello-best-approach-for-implementing-localized-search"></a>Nouveautés hello meilleure approche pour l’implémentation d’une recherche localisée

La plupart des clients choisissez les champs dédiés sur une collection lorsqu’il s’agit de toosupporting différents paramètres régionaux (langues) Bonjour même index. Champs spécifiques aux paramètres régionaux rendent possible tooassign un analyseur approprié. Par exemple, affectation de champ de tooa Microsoft Français Analyzer hello contenant des chaînes Français. Cela simplifie également le filtrage. Si vous connaissez qu'une requête est lancée sur une page fr-fr, vous pouvez limiter le champ de toothis de résultats de recherche. Créer un [profil de calcul de score](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) toogive hello champ plus de poids relatif.

## <a name="next-steps"></a>Étapes suivantes

Votre question concerne-t-elle une fonctionnalité manquante ? Demande de fonctionnalité hello sur hello [User Voice web site](https://feedback.azure.com/forums/263029-azure-search).

## <a name="see-also"></a>Voir aussi

 [Stack Overflow : Recherche Azure](https://stackoverflow.com/questions/tagged/azure-search)   
 [Fonctionnement de la recherche en texte intégral dans la Recherche Azure](search-lucene-query-architecture.md)  
 [Présentation de Recherche Azure](search-what-is-azure-search.md)

 