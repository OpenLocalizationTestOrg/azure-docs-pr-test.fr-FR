Hello tableau suivant répertorie les quotas et limite les concentrateurs d’événements tooAzure spécifique. Pour plus d’informations sur la tarification des hubs d’événements, consultez la rubrique [Tarification des hubs d’événements](https://azure.microsoft.com/pricing/details/event-hubs/).

| Limite | Scope | Type | Comportement en cas de dépassement | Valeur |
| --- | --- | --- | --- | --- |
| Nombre d’Event Hubs par espace de noms |Espace de noms |Statique |Les demandes suivantes de création d’un espace de noms seront rejetées. |10 |
| Nombre de partitions par Event Hub |Entité |Statique |- |32 |
| Nombre de groupes de consommateurs par Event Hub |Entité |Statique |- |20 |
| Nombre de connexions AMQP par espace de noms |Espace de noms |statique |Les demandes suivantes pour les connexions supplémentaires sont rejetées et une exception est reçue par hello appeler du code. |5 000 |
| Taille maximale de l’événement Event Hubs|À l’échelle du système |Statique |- |256 KB |
| Taille maximale du nom d’un hub d’événement |Entité |Statique |- |50 caractères |
| Nombre de récepteurs non epoch par groupe de consommateurs |Entité |Statique |- |5 |
| Période de rétention maximale des données d’événement |Entité |Statique |- |1 à 7 jours |
| Unités de débit maximales |Espace de noms |statique |Supérieure à limite d’unité de débit hello provoque votre toobe de données limité et génère une  **[ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception)**. Vous pouvez demander une plus grande quantité d’unités de débit pour le niveau Standard en remplissant une [demande de support](/azure/azure-supportability/how-to-create-azure-support-request). Les [unités de débit supplémentaires](../articles/event-hubs/event-hubs-auto-inflate.md) sont disponibles par blocs de 20 sur la base d’un engagement d’achat ferme. |20 |

