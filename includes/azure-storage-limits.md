| Ressource | Limite par défaut |
| --- | --- |
| Nombre de comptes de stockage par abonnement |200<sup>1</sup> |
| Capacité maximale du compte de stockage |500 TO<sup>2</sup> |
| Nombre maximal de conteneurs d'objets blob, de partages de fichiers, de tables, de files d'attente, d'entités ou de messages par compte de stockage |Aucune limite |
| Taille maximale d'un conteneur d'objets blob, d'une table ou d'une file d'attente |Identique à la capacité maximale du compte de stockage |
| Nombre maximal de blocs dans un objet blob de blocs ou ajouter des objets blob |50 000 |
| Taille maximale d'un bloc dans un objet blob de blocs |100 Mo |
| Taille maximale d'un objet blob de blocs |50 000 x 100 Mo (4,75 Go environ) |
| Taille maximale d’un bloc dans un objet blob d’ajout |4 Mo |
| Taille maximale d’un objet blob d’ajout |50 000 X 4 Mo (195 Go environ) |
| Taille maximale d'un objet blob de pages |8 To |
| Taille maximale d'une entité de table |1 Mo |
| Nombre maximal de propriétés dans une entité de table |252 |
| Taille maximale d'un message dans une file d'attente |64 Ko |
| Taille maximale d'un partage de fichiers |5 To |
| Taille maximale d'un fichier dans un partage de fichiers |1 To |
| Nombre maximal de fichiers dans un partage de fichiers |La seule limite est celle de 5 To de la capacité totale du partage de fichiers |
| Nb max. d’E/S par seconde par partage |1 000 |
| Nombre maximal de fichiers dans un partage de fichiers |La seule limite est celle de 5 To de la capacité totale du partage de fichiers |
| Nombre maximal de stratégies d'accès stockées par conteneur, partage de fichiers, table ou file d'attente |5 |
| Taux de requête maximal par compte de stockage |Objets blob : 20 000 requêtes par seconde<sup>2</sup> pour les objets blob de toute taille valide (limitées uniquement par les limites d’entrées/sorties du compte) <br />Fichiers : 1 000 IOPS (8 Ko) par partage de fichiers <br />Files d’attente : 20 000 messages par seconde (en supposant que la taille des messages soit de 1 Ko)<br />Tables : 20 000 transactions par seconde (en supposant que la taille d’entité soit de 1 Ko) |
| Débit cible pour un objet blob unique |Jusqu'à 60 Mo par seconde ou jusqu'à 500 demandes par seconde |
| Débit cible pour une file d'attente unique (messages de 1 Ko) |Jusqu'à 2 000 messages par seconde |
| Débit cible pour une partition de table unique (entités de 1 Ko) |Jusqu'à 2 000 entités par seconde |
| Débit cible pour un partage de fichier unique |Jusqu’à 60 Mo par seconde |
| Entrée max.<sup>3</sup> par compte de stockage (régions des États-Unis) |10 Gbit/s si GRS/ZRS<sup>4</sup> est activé, 20 Gbit/s pour LRS<sup>2</sup> |
| Sortie max.<sup>3</sup> par compte de stockage (régions des États-Unis) |20 Gbit/s si RA-GRS/GRS/ZRS<sup>4</sup> est activé, 30 Gbit/s pour LRS<sup>2</sup> |
| Entrée max.<sup>3</sup> par compte de stockage (régions hors États-Unis) |5 Gbit/s si GRS/ZRS<sup>4</sup> est activé, 10 Gbit/s pour LRS<sup>2</sup> |
| Sortie max.<sup>3</sup> par compte de stockage (régions hors États-Unis) |10 Gbit/s si RA-GRS/GRS/ZRS<sup>4</sup> est activé, 15 Gbit/s pour LRS<sup>2</sup> |

<sup>1</sup>Cela inclut à la fois les comptes de stockage standard et Premium. Si vous avez besoin de plus de 200 comptes de stockage, sollicitez le [Support Azure](https://azure.microsoft.com/support/faq/)pour obtenir une assistance. L’équipe Azure Storage examinera votre cas d’entreprise et pourra approuver jusqu’à 250 comptes de stockage. 

<sup>2</sup> Pour que votre compte de stockage standard puisse dépasser les limites indiquées en matière de capacité, de taux d’entrée/sortie et de requêtes, envoyez une demande via le [Support Azure](https://azure.microsoft.com/support/faq/). L’équipe d’Azure Storage examinera la requête et peut approuver une augmentation des limites au cas par cas.

<sup>3</sup>*Entrée* désigne toutes les données (requêtes) envoyées à un compte de stockage. *Sortie* désigne toutes les données (réponses) reçues d'un compte de stockage.  

<sup>4</sup>Les options de réplication Azure Storage sont les suivantes :
* **RA-GRS**: stockage géo-redondant avec accès en lecture. Si RA-GRS est activé, les cibles de sortie pour l’emplacement secondaire sont identiques à celles de l’emplacement principal.
* **GRS** : stockage géo-redondant. 
* **ZRS**: stockage redondant dans une zone. Uniquement disponible pour les objets blob de blocs. 
* **LRS**: stockage localement redondant. 


