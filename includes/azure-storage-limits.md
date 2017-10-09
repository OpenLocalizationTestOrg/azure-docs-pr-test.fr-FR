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
| Nombre maximal de fichiers dans un partage de fichiers |Limite uniquement est la capacité totale de 5 to hello hello du partage de fichiers |
| Nb max. d’E/S par seconde par partage |1 000 |
| Nombre maximal de fichiers dans un partage de fichiers |Limite uniquement est la capacité totale de 5 to hello hello du partage de fichiers |
| Nombre maximal de stratégies d'accès stockées par conteneur, partage de fichiers, table ou file d'attente |5 |
| Taux de requête maximal par compte de stockage |Objets BLOB : 20 000 demandes par seconde<sup>2</sup> pour les objets BLOB de toute taille valide (limitée uniquement par les limites d’entrées/sorties du compte hello) <br />Fichiers : 1 000 IOPS (8 Ko) par partage de fichiers <br />Files d’attente : 20 000 messages par seconde (en supposant que la taille des messages soit de 1 Ko)<br />Tables : 20 000 transactions par seconde (en supposant que la taille d’entité soit de 1 Ko) |
| Débit cible pour un objet blob unique |Des too60 Mo par seconde, ou des too500 demandes par seconde |
| Débit cible pour une file d'attente unique (messages de 1 Ko) |Les messages too2000 par seconde |
| Débit cible pour une partition de table unique (entités de 1 Ko) |Les entités too2000 par seconde |
| Débit cible pour un partage de fichier unique |Mo too60 par seconde |
| Entrée max.<sup>3</sup> par compte de stockage (régions des États-Unis) |10 Gbit/s si GRS/ZRS<sup>4</sup> est activé, 20 Gbit/s pour LRS<sup>2</sup> |
| Sortie max.<sup>3</sup> par compte de stockage (régions des États-Unis) |20 Gbit/s si RA-GRS/GRS/ZRS<sup>4</sup> est activé, 30 Gbit/s pour LRS<sup>2</sup> |
| Entrée max.<sup>3</sup> par compte de stockage (régions hors États-Unis) |5 Gbit/s si GRS/ZRS<sup>4</sup> est activé, 10 Gbit/s pour LRS<sup>2</sup> |
| Sortie max.<sup>3</sup> par compte de stockage (régions hors États-Unis) |10 Gbit/s si RA-GRS/GRS/ZRS<sup>4</sup> est activé, 15 Gbit/s pour LRS<sup>2</sup> |

<sup>1</sup>Cela inclut à la fois les comptes de stockage standard et Premium. Si vous avez besoin de plus de 200 comptes de stockage, sollicitez le [Support Azure](https://azure.microsoft.com/support/faq/)pour obtenir une assistance. équipe du stockage Azure Hello Examinez vos cas et peut approuver les comptes de stockage too250. 

<sup>2</sup> tooget toogrow dernières les comptes de votre stockage standard hello publiés limites de taux de capacité, l’entrée/sortie et demande, veuillez effectuer une demande via [prise en charge Azure](https://azure.microsoft.com/support/faq/). équipe du stockage Azure Hello examinez demande de hello et peut approuver les limites supérieures sur un cas par cas.

<sup>3</sup>*entrée* fait référence à des données tooall (demandes) envoyées compte de stockage tooa. *Sortie* fait référence tooall des données (réponses) reçues d’un compte de stockage.  

<sup>4</sup>Les options de réplication Azure Storage sont les suivantes :
* **RA-GRS**: stockage géo-redondant avec accès en lecture. Si RA-GRS est activé, les cibles de sortie pour l’emplacement secondaire de hello sont toothose identiques pour l’emplacement principal de hello.
* **GRS** : stockage géo-redondant. 
* **ZRS**: stockage redondant dans une zone. Uniquement disponible pour les objets blob de blocs. 
* **LRS**: stockage localement redondant. 


