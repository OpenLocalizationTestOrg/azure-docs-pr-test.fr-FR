Stockage est limité par l’espace disque ou à une limite inconditionnelle sur hello *nombre maximal* d’index ou de documents, selon ce qui se produit en premier.

| Ressource | Gratuit | De base | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Contrat de Niveau de Service (SLA) |Nonn <sup>1</sup> |Oui |Oui |Oui |Oui |Oui |
| Stockage par partition |50 Mo |2 Go |25 Go |100 Go |200 Go |200 Go |
| Partitions par service |N/A |1 |12 |12 |12 |3 <sup>2</sup> |
| Taille de partition |N/A |2 Go |25 Go |100 Go |200 Go |200 Go |
| Réplicas |N/A |3 |12 |12 |12 |12 |
| Nombre maximal d’index |3 |5 |50 |200 |200 |1 000 par partition ou 3 000 par service |
| Nombre maximal d’indexeurs |3 |5 |50 |200 |200 |Aucun indexeur pris en charge |
| Nombre maximal de sources de données |3 |5 |50 |200 |200 |Aucun indexeur pris en charge |
| Nombre maximal de documents |10 000 |1 million |15 millions par partition ou 180 millions par service |60 millions par partition ou 720 millions par service |120 millions par partition ou 1,4 milliard par service |1 million par index ou 200 millions par partition |
| Nombre de requêtes par seconde (QPS) estimé |N/A |~3 par réplica |~15 par réplica |~60 par réplica |~60 par réplica |Moins de 60 par réplica |

<sup>1</sup> Les fonctionnalités de niveau Gratuit et d’évaluation ne sont pas fournies avec des Contrats de niveau de service (SLA). Pour tous les niveaux facturables, les SLA entrent en vigueur lorsque vous approvisionnez une redondance suffisante pour votre service. Un SLA de requête (lecture) requiert au moins deux réplicas. Un SLA de requête et d’indexation (lecture-écriture) nécessite au moins trois réplicas. nombre de Hello de partitions n’est pas un facteur de contrat SLA. 

<sup>2</sup> S3 HD a une limite inconditionnelle de 3 partitions, qui est inférieur à la limite de partition hello pour S3. limite de partition inférieure Hello est imposée, car le nombre d’index hello pour S3 HD est sensiblement plus élevé. Étant donné que les limites de service existent pour les deux ressources de calcul (de stockage et de traitement) et contenu (index et documents), hello contenu limite est atteinte tout d’abord.
