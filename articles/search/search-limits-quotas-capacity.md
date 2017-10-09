---
title: limites aaaService dans Azure Search | Documents Microsoft
description: "Limites de service permettant de planifier la capacité et limites maximales des requêtes et réponses de la Recherche Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/07/2017
ms.author: heidist
ms.openlocfilehash: cb13a0f1c87a654fb5845c9c741f74a91da5b372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-limits-in-azure-search"></a>Limites de service d’Azure Search
Les limites maximales de stockage, de charges de travail et de quantités d’index, de documents et d’autres objets dépendent du niveau tarifaire (**Gratuit**, **De base** ou **Standard**) de la [Recherche Azure](search-create-service-portal.md).

* **Gratuit** est un service partagé multi-locataire qui est fourni avec votre abonnement Azure. Il est une option de coût supplémentaire non pour les abonnés existants qui vous permet de tooexperiment avec le service de hello avant de s’inscrire pour des ressources dédiées.
* Le niveau **De base** fournit des ressources informatiques dédiées aux charges de production à petite échelle.
* Le niveau **Standard** est exécuté sur des ordinateurs dédiés, avec une capacité de stockage et de traitement beaucoup plus grande, et ce, à chaque niveau. Le niveau Standard apparaît dans : S1, S2, S3 et S3 Haute densité (S3 HD).

> [!NOTE]
> Un service est approvisionné à un niveau spécifique. Si vous devez toojump niveaux tooget plus la capacité, vous devez configurer un nouveau service (il n’existe aucune mise à niveau sur place). Pour en savoir plus, consultez [Choisir une référence (SKU) ou un niveau tarifaire](search-sku-tier.md). toolearn plus d’informations sur l’ajustement de la capacité d’un service, vous avez déjà configuré, consultez [mettre à l’échelle des niveaux de ressources pour les requêtes et indexation des charges de travail](search-capacity-planning.md).
>

## <a name="per-subscription-limits"></a>Limites par abonnement
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>Limites par service
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>Limites par index
Il existe une correspondance biunivoque entre les limites sur les index et les limites sur les indexeurs. Étant donné une limite de 200 index, hello limite maximale pour les indexeurs est également 200 pour hello même service.

| Ressource | Gratuit | De base | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Index : nombre maximal de champs par index |1 000 |100 <sup>1</sup> |1 000 |1 000 |1 000 |1 000 |
| Index : nombre maximal de profils de score par index |100 |100 |100 |100 |100 |100 |
| Index : nombre maximal de fonctions par profil |8 |8 |8 |8 |8 |8 |
| Indexeurs : quantité maximale de charge d’indexation par appel |10 000 documents |Limité uniquement par le nombre maximal de documents |Limité uniquement par le nombre maximal de documents |Limité uniquement par le nombre maximal de documents |Limité uniquement par le nombre maximal de documents |N/A <sup>2</sup> |
| Indexeurs : durée maximale d’exécution | 1-3 minutes <sup>3</sup> |24 heures |24 heures |24 heures |24 heures |N/A <sup>2</sup> |
| Indexeur d’objets blob : taille maximale des objets blob, en Mo |16 |16 |128 |256 |256 |N/A <sup>2</sup> |
| Indexeur d’objets blob : nombre maximal de caractères du contenu extrait d’un objet blob |32 000 |64 000 |4 millions |4 millions |4 millions |N/A <sup>2</sup> |

<sup>1</sup> le niveau de base est hello uniquement référence (SKU) avec une limite inférieure de 100 champs par index.

<sup>2</sup> S3 HD ne prend actuellement pas en charge les indexeurs. Contactez le support Azure si vous avez un besoin urgent de cette fonctionnalité.

<sup>3</sup> indexeur une durée d’exécution maximale pour le niveau gratuit de hello est 3 minutes pour les sources d’objets blob et 1 minute pour toutes les autres sources de données.

## <a name="document-size-limits"></a>Limites de taille des documents
| Ressource | Gratuit | De base | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Taille de chaque document par API d’index |< 16 Mo |< 16 Mo |< 16 Mo |< 16 Mo |< 16 Mo |< 16 Mo |

Désigne la taille maximale des documents de toohello lors de l’appel d’une API d’Index. Taille du document est en fait une limite de taille de hello Hello corps de demande d’API de l’Index. Étant donné que vous pouvez passer un lot de plusieurs documents toohello API de l’Index à la fois, limite de taille hello est réellement varie selon le nombre de documents est dans un lot de hello. Pour un lot avec un seul document, hello maximal de documents est 16 Mo de JSON.

taille du document tookeep vers le bas, n’oubliez pas les données non requêtable tooexclude à partir de la demande de hello. Images et autres données binaires ne sont pas directement utilisable dans une requête et ne doivent pas être stockées dans les index hello. toointegrate des données non requêtable dans les résultats de recherche, définissez un champ non interrogeables mais qui stocke une ressource de toohello référence URL.

## <a name="workload-limits-queries-per-second"></a>Limites de charge de travail (requêtes par seconde)
| Ressource | Gratuit | De base | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| RPS |N/A  |~3 par réplica |~15 par réplica |~60 par réplica |Moins de 60 par réplica |Moins de 60 par réplica |

Requêtes par seconde (QPS) est une approximation basée sur l’heuristique, en utilisant les valeurs de tooderive estimé de charges de travail client simulé et réelles. Débit de requêtes par seconde exact varie selon votre nature hello et les données de requête de hello.

Bien que les estimations sont fournies ci-dessus, un taux réel est toodetermine difficile, en particulier dans hello que gratuit partagé service où le débit est basé sur la bande passante disponible et la concurrence pour les ressources système. Dans le niveau gratuit de hello, les ressources de calcul et de stockage sont partagés par plusieurs abonnés, requêtes par seconde pour votre solution sera toujours varient selon le nombre d’autres charges de travail sont exécutent au hello même temps.

Au niveau standard de hello, vous pouvez estimer QPS plus étroitement, car vous pouvez contrôler plusieurs des paramètres de hello. Consultez la section des pratiques recommandées hello dans [gérer votre solution de recherche](search-manage.md) pour obtenir des conseils sur la façon de toocalculate QPS pour vos charges de travail.

## <a name="api-request-limits"></a>Limites de requête d’API
* 16 Mo maximum par requête <sup>1</sup>
* La longueur maximale d’une URL est de 8 Ko
* 1 000 documents maximum par lot de charges, de fusions ou de suppressions d’index
* 32 champs maximum dans la clause $orderby
* La taille maximale des termes de recherche du texte encodé en UTF-8 est de 32 766 octets (32 Ko moins 2 octets)

<sup>1</sup> dans Azure Search, corps hello d’une requête est sujet tooan limite de 16 Mo, en imposant une limite pratique contenu hello de champs individuels ou des collections qui ne sont pas contraints par la limite théorique (consultez [pris en charge types de données](https://msdn.microsoft.com/library/azure/dn798938.aspx) pour plus d’informations sur la composition de champ et les restrictions).

## <a name="api-response-limits"></a>Limites de réponse d’API
* 1 000 documents maximum retournés par page de résultats de recherche
* 100 suggestions maximum retournées par requête d’API de suggestion

## <a name="api-key-limits"></a>Limites de clés API
Les clés API sont utilisées pour l'authentification de service. Il existe deux types de clé API. Clés d’administration sont spécifiées dans l’en-tête de demande hello et accordez l’accès en lecture-écriture complète toohello service. Les clés de requête sont en lecture seule, spécifié sur l’URL de hello et tooclient généralement distributed applications.

* 2 clés administrateur maximum par service
* 50 clés de requête maximum par service
