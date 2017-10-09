---
title: administration aaaService pour Azure Search Bonjour portail Azure
description: "Gérer Azure Search, un service de recherche de cloud hébergé sur Microsoft Azure, à l’aide de hello portail Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: c87d1fdd-b3b8-4702-a753-6d7e29dbe0a2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/18/2017
ms.author: heidist
ms.openlocfilehash: 9bb33660d93e068e0f35b856cba0a41c92623644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-administration-for-azure-search-in-hello-azure-portal"></a>Administration des services pour Azure Search dans hello portail Azure
> [!div class="op_single_selector"]
> * [Portail](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> * [Kit SDK .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.search)
> * [Python](https://pypi.python.org/pypi/azure-mgmt-search/0.1.0)> 

Azure Search est un service de recherche entièrement géré, basé sur le cloud, utilisé pour la création d’une expérience de recherche riche dans des applications personnalisées. Cet article traite des hello *service administration* les tâches que vous pouvez effectuer dans hello [portail Azure](https://portal.azure.com) pour un service de recherche que vous avez déjà configurés. *Administration de service* est léger par sa conception, toohello limitée tâches suivantes :

* Gérer et sécuriser les accès toohello *clés api* utilisé pour le service de tooyour accès en lecture ou écriture.
* Ajuster la capacité de service en modifiant l’allocation de partitions et réplicas hello.
* Surveiller l’utilisation des ressources, les limites de toomaximum relatif de votre niveau de service.

**Non compris** 

*Gestion de contenu* (ou de gestion d’index) fait référence toooperations telles que l’analyse de volume de requêtes de recherche du trafic toounderstand, découvrir quels termes personnes rechercher, puis recherchez succès sont des résultats afin de guider les clients toospecific documents dans votre index. Pour obtenir de l’aide dans ce domaine, consultez [Recherche de l’analyse du trafic pour la Recherche Azure](search-traffic-analytics.md).

*Performances des requêtes* est également abordée dans cet article hello. Pour plus d’informations, consultez [Surveiller l’utilisation et les statistiques](search-monitor-usage.md) et [Performances et optimisation](search-performance-optimization.md).

La *mise à niveau* n’est pas une tâche d’administration. Étant donné que les ressources sont allouées lors de la configuration de service de hello, Mobile tooa autre niveau nécessite un nouveau service. Pour plus d’informations, consultez [Création d’un service Azure Search](search-create-service-portal.md).

<a id="admin-rights"></a>

## <a name="administrator-rights"></a>Droits d’administrateur
Mise en service ou de désaffectation service hello lui-même est possible par un administrateur de l’abonnement Azure ou un coadministrateur.

Dans un service, toute personne ayant accès toohello URL du service et une clé d’api admin a accès en lecture-écriture toohello service. Accès en lecture-écriture fournit hello capacité tooadd, supprimer ou modifier des objets de serveur, y compris les clés de l’api, index, indexeurs, sources de données, des planifications et attributions de rôles implémenté par le biais [rôles définis par RBAC](#rbac).

Toutes les interactions utilisateur avec Azure Search est comprise dans un de ces modes : en lecture-écriture accès toohello service (droits d’administrateur), ou accès en lecture seule toohello (droits de requête). Pour plus d’informations, consultez [gérer les clés api hello](#manage-keys).

<a id="sys-info"></a>

## <a name="set-rbac-roles-for-administrative-access"></a>Définir des rôles RBAC pour l’accès des administrateurs
Azure fournit un [modèle global d’autorisation basée sur les rôles](../active-directory/role-based-access-control-configure.md) pour tous les services sont gérés via le portail de hello ou les API du Gestionnaire de ressources. Les rôles de propriétaire, collaborateur et lecteur déterminent le niveau hello d’administration de service de rôle de tooeach attribué de principaux de sécurité, groupes et utilisateurs Active Directory. 

Pour Azure Search, les autorisations de RBAC déterminent hello des tâches d’administration suivantes :

| Rôle | Task |
| --- | --- |
| Propriétaire |Créer ou supprimer le service de hello ou un objet de service hello, y compris les clés de l’api, des index, les indexeurs, sources de données d’indexeur et planifications de l’indexeur.<p>Afficher l’état du service, notamment des compteurs et la taille du stockage.<p>Ajout ou suppression d'appartenance à un rôle (seul un Propriétaire peut gérer l'appartenance à un rôle).<p>Administrateurs des abonnements et les propriétaires de service ont appartenance automatique dans le rôle des propriétaires hello. |
| Collaborateur |Même niveau d’accès que le Propriétaire, à l’exception de la gestion des rôles RBAC. Par exemple, un Collaborateur peut visualiser et régénérer `api-key`, mais il ne peut pas modifier les appartenances aux rôles. |
| Lecteur |Affichage de l'état du service et des clés Requête. Les membres de ce rôle ne peuvent pas modifier la configuration du service, ni afficher des clés Admin. |

Rôles n’accordent pas le point de terminaison de service à toohello accès droits. Les opérations du service Search telles que la gestion ou le remplissage d'index, tout comme les requêtes de données de recherche, sont contrôlées via des clés api, et non par des rôles. Pour en savoir plus, consultez la section « Autorisation pour les opérations de gestion et les opérations de données » de la page [Contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-what-is.md).

<a id="secure-keys"></a>
## <a name="logging-and-system-information"></a>Journalisation et informations système
Azure Search n’expose pas les fichiers journaux pour un service via le portail de hello ou interfaces de programmation. Au niveau de base hello et versions ultérieures, Microsoft surveille tous les services Azure Search pour la disponibilité de 99,9 % par les contrats de niveau de service (SLA). Si le service de hello est lente ou débit des demandes tombe en dessous des seuils de contrat SLA, les équipes de support examinez toothem disponibles des fichiers journaux hello et problème de hello adresse.

En termes d’informations générales sur votre service, vous pouvez obtenir des informations Bonjour suivant façons :

* Dans le portail de hello, tableau de bord de service hello, les notifications, les propriétés et les messages d’état.
* À l’aide de [PowerShell](search-manage-powershell.md) ou hello [API REST de gestion](https://docs.microsoft.com/rest/api/searchmanagement/) trop[obtenir les propriétés du service](https://docs.microsoft.com/rest/api/searchmanagement/services), ou d’état sur l’utilisation des ressources index.
* Via la [recherche du trafic d’analyse](search-traffic-analytics.md), comme indiqué précédemment.

<a id="manage-keys"></a>

## <a name="manage-api-keys"></a>Gérer les clés API
Toutes les demandes de service de recherche tooa ont besoin d’une clé api a été générée pour votre service. Cette clé api est un mécanisme d’exclusive de hello pour authentifier le point de terminaison du service de recherche accès tooyour. 

Une clé API est une chaîne composée de nombres et de lettres générée de manière aléatoire. Via [les autorisations de RBAC](#rbac), vous pouvez supprimer ou de lire les clés de hello, mais vous ne pouvez pas remplacer une clé avec un mot de passe défini par l’utilisateur. 

Deux types de clés sont utilisés tooaccess votre service de recherche :

* Admin (valide pour toute opération de lecture-écriture sur le service de hello)
* Requête (valable pour les opérations en lecture seule, telles que les requêtes par rapport à un index)

Une clé d’api admin est créée lors de la configuration de service de hello. Il existe deux clés d’administration, désignés comme *principal* et *secondaire* tookeep leur directement, mais en fait, ils sont interchangeables. Chaque service a deux clés d’administration afin que vous pouvez restaurer un sans perdre l’accès tooyour service. Vous pouvez régénérer une clé d’administration, mais vous ne pouvez ajouter le nombre de clés toohello total admin. Il y a, au maximum, deux clés Admin par service de recherche.

Les clés Requête sont conçues pour les applications clientes qui appellent directement le service Search. Vous pouvez créer des clés de requête too50. Dans le code d’application, vous spécifiez hello recherche URL et un service de toohello requête clé api tooallow accès en lecture seule. Code de votre application spécifie également les index hello utilisée par votre application. Ensemble, point de terminaison hello, une clé d’api pour l’accès en lecture seule et un index cible définir au niveau de portée et l’accès hello de connexion hello à partir de votre application cliente.

tooget ou régénérer les clés api, tableau de bord de service hello ouvert. Cliquez sur **clés** tooslide ouvrir la page de gestion de clés hello. Commandes pour la régénération ou la création de clés sont en hello haut hello. Par défaut, seules les clés Admin sont créées. Les clés API de requête doivent être créées manuellement.

 ![][9]

<a id="rbac"></a>

## <a name="secure-api-keys"></a>Sécuriser les clés API
Clés de sécurité sont assuré en limitant l’accès via le portail de hello ou des interfaces du Gestionnaire de ressources (PowerShell ou une interface de ligne). Comme indiqué, les administrateurs des abonnements peuvent afficher et régénérer toutes les clés API. Par précaution, passez en revue toounderstand d’attributions de rôle qui a des clés d’accès toohello administration.

1. Dans le tableau de bord du service hello, cliquez sur Panneau de hello accès icône tooslide hello ouvrez utilisateurs.
   ![][7]
2. Dans Utilisateurs, vérifiez les affectations de rôles existantes. Comme prévu, les administrateurs d’abonnements ont déjà toohello d’accès complet via le rôle de propriétaire hello.
3. toodrill de plus, cliquez sur **administrateurs d’abonnements** , puis développez la liste hello rôle affectation toosee disposant des droits d’administration de collaboration sur votre service de recherche.

Autorisations d’accès tooview façon un autre est tooclick **rôles** sur le panneau des utilisateurs hello. Cela affiche les rôles disponibles et nombre hello du rôle de tooeach attribué aux utilisateurs ou groupes.

<a id="sub-5"></a>

## <a name="monitor-resource-usage"></a>surveiller l’utilisation des ressources ;
Dans le tableau de bord hello, l’analyse de ressource est informations toohello limité indiquées dans le tableau de bord de service hello et quelques mesures que vous pouvez obtenir en interrogeant hello service. Tableau de bord de service hello, dans la section de l’utilisation de hello, vous pouvez déterminer rapidement si des niveaux de ressources de partition sont adaptées à votre application.

Hello API de Service de recherche, vous pouvez obtenir un nombre sur des documents et des index. Il existe des limites matérielles associées à ces nombres en fonction de hello niveau tarifaire. Pour plus d’informations, voir [Limites de service de recherche](search-limits-quotas-capacity.md). 

* [Obtention de statistiques d'index](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)
* [Nombre de documents](https://docs.microsoft.com/rest/api/searchservice/count-documents)

> [!NOTE]
> Il arrive qu'une limite soit surévaluée en raison des options de mise en cache. Par exemple, lorsque vous utilisez le service de hello partagé, vous pouvez voir un document count sur la limite de 10 000 documents hello. surévaluation de Hello est temporaire et sera détectée sur la vérification de l’application hello suivante limite. 
> 
> 

## <a name="disaster-recovery-and-service-outages"></a>Récupération d’urgence et pannes de service

Bien que nous pouvons récupérer vos données, Azure Search ne fournit pas de basculement du service de hello instantanés s’il existe une panne au niveau de charge de cluster ou données hello. En cas d’un cluster dans le centre de données hello, équipe hello détectera et toorestore service de travail. Vous subirez un temps d’arrêt lors de la restauration du service. Vous pouvez demander toocompensate de crédits de service pour une indisponibilité de service par hello [contrat de niveau de Service (SLA)](https://azure.microsoft.com/support/legal/sla/search/v1_0/). 

Si le service continu est requise dans les événements hello des erreurs irrécupérables en dehors du contrôle de Microsoft, vous pouvez [configurer un service supplémentaire](search-create-service-portal.md) dans une autre région et implémentez une géo-réplication stratégie tooensure index sont entièrement redondants entre tous les services.

Les clients qui utilisent [indexeurs](search-indexer-overview.md) toopopulate et l’actualisation des index peuvent gérer la récupération d’urgence via des indexeurs géographiques spécifiques en exploitant hello même source de données. Deux services dans des régions différentes, chaque exécution d’un indexeur, Impossible d’index à partir de hello même tooachieve géo-redondance de source de données. Si vous indexez à partir de sources de données qui sont aussi géo-redondantes, sachez que les indexeurs du service Recherche Azure ne peuvent assurer qu’une indexation incrémentielle à partir de réplicas principaux. Dans un événement de basculement, être sûr de point de toore hello indexeur toohello nouveau réplica principal. 

Si vous n’utilisez pas d’indexeurs, vous utiliserez votre code toopush objets et données toodifferent recherche les services d’application en parallèle. Pour plus d’informations, consultez [Performance and optimization in Azure Search](search-performance-optimization.md)(Performances et optimisation dans Azure Search).

## <a name="backup-and-restore"></a>Sauvegarde et restauration

La Recherche Azure n’est pas une solution de stockage de données principal, c’est pourquoi nous ne fournissons pas de mécanisme formel de sauvegarde et de restauration en libre-service. Votre code d’application utilisée pour créer et remplir un index est hello option de restauration de fait, si vous supprimez un index par erreur. 

toorebuild un index, vous supprimer (en supposant qu’il existe), recréez les index hello dans le service hello et recharger en récupérant des données à partir de votre banque de données principale. Ou bien, vous pouvez atteindre trop[support technique]() toosalvage index s’il existe une panne régionale.


<a id="scale"></a>

## <a name="scale-up-or-down"></a>Augmentation ou réduction d'échelle
Au départ, chaque service de recherche comporte, au minimum, un réplica et une partition. Si vous êtes un [couche qui fournit des ressources dédiées](search-limits-quotas-capacity.md), cliquez sur hello **échelle** vignette hello service tableau de bord tooadjust l’utilisation des ressources.

Lorsque vous ajoutez de la capacité à une ressource, service de hello les utilise automatiquement. Aucune action supplémentaire n’est requise de votre part, mais est un court délai avant l’impact hello de ressource hello est réalisé. Il peut prendre 15 minutes ou plus tooprovision des ressources supplémentaires.

 ![][10]

### <a name="add-replicas"></a>Ajout de réplicas
Pour augmenter le nombre de requêtes par seconde (RPS) ou parvenir à une haute disponibilité, il convient d'ajouter des réplicas. Chaque réplica possède une copie d’un index, afin d’ajouter un réplica plus traduit tooone plus d’index disponible pour la gestion des demandes de requête de service. Au moins 3 réplicas sont nécessaires pour la haute disponibilité (pour plus d’informations, consultez [Planification de la capacité](search-capacity-planning.md)).

Un service de recherche qui comporte davantage de réplicas peut équilibrer la charge des demandes de requête sur un plus grand nombre d'index. Étant donné un niveau de volume de requêtes, débit de requête va toobe plus rapidement lorsqu’il y a plus de copies de la demande de hello hello index tooservice disponibles. Si vous rencontrez une latence de la requête, vous verrez un impact positif sur les performances une fois que des réplicas supplémentaires hello sont en ligne.

Bien que le débit de requêtes augmente lorsque vous ajoutez des réplicas, il ne pas précisément double ou triple lorsque vous ajoutez le service de tooyour de réplicas. Toutes les applications de recherche sont des facteurs de tooexternal d’objet qui peuvent empiéter sur les performances des requêtes. Les requêtes complexes et latence du réseau sont deux facteurs qui contribuent toovariations dans le temps de réponse des requêtes.

### <a name="add-partitions"></a>Ajout de partitions
La plupart des applications de service intègrent le besoin de plusieurs réplicas plutôt que de plusieurs partitions. Vous pouvez ajouter des partitions lorsqu'un plus grand nombre de documents est nécessaire si vous êtes inscrit au service Standard. Le niveau De base ne fournit pas d’autres partitions.

Au niveau Standard de hello, les partitions sont ajoutées en multiples de 12 (plus précisément, 1, 2, 3, 4, 6 ou 12). Il s’agit d’un artefact de partitionnement. Un index est créé dans 12 fragments (ou shards) qui peuvent tous être stockés dans 1 partition ou répartis équitablement dans 2, 3, 4, 6 ou 12 partitions (un fragment par partition).

### <a name="remove-replicas"></a>Suppression de réplicas
Après une période de traitement de requêtes intensive, vous pouvez réduire le nombre de réplicas une fois la charge de requêtes de recherche revenue à la normale (à la fin d’une période de soldes, par exemple).

toodo, déplacement hello réplica curseur tooa précédent numéro inférieur. Rien de plus ! Ce qui réduit le nombre de réplicas hello abandonne les machines virtuelles dans le centre de données hello. Désormais, vos opérations de requête et d'ingestion de données s'exécuteront sur un nombre moins élevé de machines virtuelles. limite minimale de Hello est un réplica.

### <a name="remove-partitions"></a>Suppression de partitions
Contrairement à la suppression de réplicas, qui ne nécessite aucun effort supplémentaire de votre part, vous pouvez avoir certaines toodo de travail si vous utilisez plus de stockage peut être réduit. Par exemple, si votre solution utilise trois partitions, effectifs tooone ou les deux partitions génère une erreur si le nouvel espace de stockage hello est inférieur à requis. Comme prévu, votre choix est toodelete index ou des documents d’un toofree index associé de l’espace, ou conserver la configuration actuelle de hello.

Aucune méthode de détection ne vous permet d'identifier les fragments d'index qui sont stockés sur des partitions spécifiques. Chaque partition fournit environ 25 Go de stockage, vous devez tooreduce tooa taille qui permettre être prises en charge par un nombre de partitions que vous avez hello. Si vous souhaitez toorevert tooone partition, toutes les 12 partitions devez toofit.

toohelp avec planification future, vous souhaiterez peut-être toocheck stockage (à l’aide de [obtenir des statistiques d’Index](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)) toosee combien vous avez utilisé. 

<a id="advanced-deployment"></a>

## <a name="best-practices-on-scale-and-deployment"></a>Meilleures pratiques de mise à l’échelle et de déploiement
Cette vidéo de 30 minutes passe en revue les meilleures pratiques pour les scénarios de déploiement avancés, y compris les charges de travail géolocalisées. Vous pouvez également voir [optimisation des performances et dans Azure Search](search-performance-optimization.md) pour aide pages que hello garde même pointe.

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<a id="next-steps"></a>

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous comprenez les concepts hello administration du service, envisagez d’utiliser [PowerShell](search-manage-powershell.md) tooautomate tâches.

Nous vous recommandons également de consulter hello [optimisation des performances et l’article](search-performance-optimization.md).

Un autre recommandation est hello toowatch vidéo indiqué dans la section précédente de hello. Il fournit une couverture plus approfondie des techniques hello indiquées dans cette section.

<!--Image references-->
[7]: ./media/search-manage/rbac-icon.png
[8]: ./media/search-manage/Azure-Search-Manage-1-URL.png
[9]: ./media/search-manage/Azure-Search-Manage-2-Keys.png
[10]: ./media/search-manage/Azure-Search-Manage-3-ScaleUp.png



