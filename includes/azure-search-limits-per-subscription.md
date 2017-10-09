Vous pouvez créer plusieurs services au sein d’un abonnement, chacun d’eux mis en service à un niveau spécifique, limité uniquement par le nombre de hello des services autorisés à chaque niveau. Par exemple, vous pouvez créer des services de too12 au niveau de base hello et 12 un autre services au niveau de hello S1 dans hello même abonnement. Pour en savoir plus sur ces niveaux, voir [Choisir une référence (SKU) ou un niveau tarifaire pour Azure Search](../articles/search/search-sku-tier.md).

Les limites de service maximales peuvent être augmentées sur demande. Contactez le Support technique Azure si vous avez besoin de plusieurs services au sein de hello même abonnement.

| Ressource | Gratuit | De base | S1 | S2 | S3 | S3 HD <sup>1</sup> |
| --- | --- | --- | --- | --- | --- | --- |
| Nombre de services maximum |1 |12 |12 |6 |6 |6 |
| Mise à l’échelle maximale en unités de recherche <sup>2</sup> |N/A <sup>3</sup> |3 unités de recherche <sup>4</sup> |36 unités de recherche |36 unités de recherche |36 unités de recherche |36 unités de recherche |

<sup>1</sup> S3 HD ne prend pas en charge les [indexeurs](../articles/search/search-indexer-overview.md) pour l’instant. 

<sup>2</sup> Les unités de recherche sont des unités de facturation, allouées en tant que *réplicas* ou *partitions*. Vous avez besoin des deux types de ressource pour les opérations de stockage, d’indexation et d’interrogation. toolearn plus d’informations sur la façon dont les unités de recherche sont calculées, ainsi qu’un graphique de combinaisons valides de dépasser les limites maximales hello, consultez [mettre à l’échelle des niveaux de ressources pour les charges de travail de requête et d’index](../articles/search/search-capacity-planning.md). 

<sup>3</sup> La gratuité repose sur des ressources partagées utilisées par plusieurs abonnés. Dans ce niveau, il n’existe aucune ressource dédiée à un abonné particulier. Pour cette raison, l’échelle maximale est signalée comme n’était pas applicable.

<sup>4</sup> Le niveau « De base » présente une partition fixe. À ce niveau, des unités de recherche supplémentaires sont utilisées pour allouer davantage de réplicas pour les charges de travail de requête accrues.

