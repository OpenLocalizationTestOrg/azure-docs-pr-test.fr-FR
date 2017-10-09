Fabrique de données est un service de plusieurs locataire qui a hello suivant les limites par défaut dans toomake lieu que les abonnements client sont protégées à partir de l’autre les charges de travail. La plupart des limites de hello peuvent être facilement déclenchés pour votre abonnement de la limite maximale de toohello en contactant le support.

| **Ressource** | **Limite par défaut** | **Limite maximale** |
| --- | --- | --- |
| fabriques de données d’un abonnement Azure |50 |[Contacter le support technique](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| pipelines dans une fabrique de données |2 500 |[Contacter le support technique](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| jeux de données dans une fabrique de données |5 000 |[Contacter le support technique](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| tranches simultanées par jeu de données |10 |10 |
| octets par objet pour les objets pipeline <sup>1</sup> |200 Ko |200 Ko |
| octets par objet pour les objets jeu de données et service lié <sup>1</sup> |100 Ko |2 000 Ko |
| Cœurs de cluster HDInsight à la demande d’un abonnement<sup>2</sup> |60 |[Contacter le support technique](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Unité de déplacement de données cloud <sup>3</sup> |32 |[Contacter le support technique](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Nombre de nouvelles tentatives pour les exécutions d’activités de pipeline |1 000 |MaxInt (32 bits) |

<sup>1</sup> Les objets Pipeline, DataSet et LinkedService correspondent à un regroupement logique de votre charge de travail. Limites de ces objets ne concernent pas tooamount de données, vous pouvez déplacer et traiter avec le service d’Azure Data Factory hello. Fabrique de données est conçue tooscale plusieurs pétaoctets de toohandle de données.

<sup>2</sup> à la demande HDInsight cœurs sont allouées en dehors de l’abonnement hello qui contient la fabrique de données hello. Par conséquent, hello ci-dessus limite est hello Data Factory appliqués limite de cœurs de cœurs de HDInsight à la demande et qu’il est différent de la limite de cœurs hello associé à votre abonnement Azure.

<sup>3</sup> L’unité de déplacement de données cloud est utilisée dans une opération de copie cloud-cloud. Il s’agit d’une mesure qui représente la puissance hello (il s’agit d’une combinaison de l’UC, la mémoire et l’allocation des ressources réseau) d’une seule unité dans la fabrique de données. Vous pouvez obtenir un débit de copie plus élevé en utilisant plus d’unités de déplacement pour certains scénarios. Consultez trop[unités de déplacement des données en nuage](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units) section de détails.

| **Ressource** | **Limite inférieure par défaut** | **Limite minimale** |
| --- | --- | --- |
| Intervalle de planification |15 minutes |15 minutes |
| Intervalle entre les nouvelles tentatives |1 seconde |1 seconde |
| Délai d’expiration des nouvelles tentatives |1 seconde |1 seconde |

### <a name="web-service-call-limits"></a>Limites d’appels du service web
Azure Resource Manager fixe des limites aux appels d’API. Vous pouvez effectuer des appels d’API à un rythme dans hello [limite de l’API Azure Resource Manager](../articles/azure-subscription-service-limits.md#resource-group-limits).
