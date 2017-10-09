---
title: "extensions de PostgreSQL aaaUsing dans la base de données Azure pour PostgreSQL | Documents Microsoft"
description: "Décrit les fonctionnalités de hello tooextend hello capacité de votre base de données à l’aide des extensions dans la base de données Azure pour PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: af2462d7a923b934bc0329153be7079ba86e8856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a>Extensions PostgreSQL dans une base de données Azure pour PostgreSQL
PostgreSQL fournit des fonctionnalités de hello hello capacité tooextend de votre base de données à l’aide des extensions. Extensions permettant à plusieurs toobe objets SQL associée regroupée dans un package unique et peuvent être chargées ou supprimées de votre base de données avec une seule commande. Une fois chargées dans la base de données hello des extensions peuvent fonctionner comme des fonctionnalités qui sont intégrées dans. Pour plus d’informations sur les extensions PostgreSQL, consultez la page [Empaqueter des objets liés dans une extension](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).

## <a name="how-toouse-postgresql-extensions"></a>Comment les extensions PostgreSQL toouse ?
Les extensions de PostgreSQL doivent toobe installé pour votre base de données avant de les utiliser. tooinstall une extension particulière, exécutez le [créer une EXTENSION](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) commande à partir de tooload d’outil psql hello objets empaquetées dans votre base de données.

La base de données Azure pour PostgreSQL prend en charge un sous-ensemble d’extensions clés, comme indiqué ici. Au-delà de ceux qui sont répertoriés de hello, les autres extensions ne sont pas pris en charge. Vous ne pouvez pas créer votre propre extension avec le service de base de données Azure pour PostgreSQL.

## <a name="extensions-supported-by-azure-database-for-postgresql"></a>Extensions prises en charge par la base de données Azure pour PostgreSQL
les tables suivantes de Hello liste hello PostgreSQL extensions standard qui sont actuellement pris en charge par la base de données Azure pour PostgreSQL. Vous pouvez également obtenir ces informations en interrogeant pg\_available\_extensions. 

### <a name="data-types-extensions"></a>Extensions de types de données

> [!div class="mx-tableFixed"]
| **Extension** | **Description** |
|---|---|
| [citext](https://www.postgresql.org/docs/9.6/static/citext.html) | Fournit un type de chaîne de caractères avec respect de la casse. |
| [hstore](https://www.postgresql.org/docs/9.6/static/hstore.html) | Fournit un type de données permettant de stocker des ensembles de paires clé/valeur. |

### <a name="functions-extensions"></a>Extensions de fonctions

> [!div class="mx-tableFixed"]
| **Extension** | **Description** |
|---|---|
| [fuzzystrmatch](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | Fournit plusieurs similitudes toodetermine de fonctions et la distance entre des chaînes. |
| [intarray](https://www.postgresql.org/docs/9.6/static/intarray.html) | Fournit des fonctions et des opérateurs permettant de manipuler des tableaux d’entiers non Null. |
| [pgcrypto](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | Fournit des fonctions de chiffrement. |
| [pg\_partman](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | Gère les tables partitionnées par date ou par ID. |
| [pg\_trgm](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | Fournit des fonctions et des opérateurs pour déterminer la similarité hello du texte alphanumérique basée sur la correspondance de TRIGRAMME |
| [uuid-ossp](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | Génère des identificateurs uniques universels (UUID). |

### <a name="full-text-search-extensions"></a>Extensions de recherche en texte intégral

> [!div class="mx-tableFixed"]
| **Extension** | **Description** |
|---|---|
| [unaccent](https://www.postgresql.org/docs/9.6/static/unaccent.html) | Dictionnaire de recherche de texte qui supprime les accents (signes diacritiques) des lexèmes. |

### <a name="index-types-extensions"></a>Extensions de types d’index

> [!div class="mx-tableFixed"]
| **Extension** | **Description** |
|---|---|
| [btree\_gin](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | Fournit des exemples de classes d’opérateurs GIN qui implémentent des comportements de type arbre B pour certains types de données. |
| [btree\_gist](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | Fournit des classes d’opérateurs d’index GiST qui implémentent l’arbre B. |

### <a name="language-extensions"></a>Extensions de langage

> [!div class="mx-tableFixed"]
| **Extension** | **Description** |
|---|---|
| [plpgsql](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | Langage procédural chargeable PL/pgSQL. |

### <a name="miscellaneous-extensions"></a>Extensions diverses

> [!div class="mx-tableFixed"]
| **Extension** | **Description** |
|---|---|
| [pg\_buffercache](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | Fournit un moyen pour examiner ce qui se passe dans le cache des tampons hello partagé en temps réel. |
| [pg\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | Fournit un moyen tooload relation de données dans le cache des tampons hello. |
| [pg\_stat\_statements](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | Fournit un moyen de suivre les statistiques d’exécution de toutes les instructions SQL exécutées par un serveur. |
| [postgres\_fdw](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | Wrapper de données à l’étranger utilisé tooaccess les données stockées dans des serveurs externes PostgreSQL |

### <a name="postgis"></a>PostGIS

> [!div class="mx-tableFixed"]
| **Extension** | **Description** |
|---|---|
| [PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal | Objets spatiaux et géographiques pour PostgreSQL. |
| address\_standardizer, address\_standardizer\_data\_us | Tooparse utilisé une adresse en éléments constituants. Utilisé l’étape de normalisation toosupport géocodage adresse. |
| [pgrouting](http://pgrouting.org/) | Étend hello PostGIS / fonctionnalités de routage de geospatial tooprovide de base de données PostgreSQL géographiques. |

## <a name="next-steps"></a>Étapes suivantes
Ne voyez pas une extension que vous souhaitez que toouse ? Dites-le-nous. Votez pour les demandes existantes ou envoyez de nouveaux commentaires et souhaits dans notre [Forum de commentaires client](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).
