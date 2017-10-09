---
title: "aaaChoose une référence (SKU) ou le niveau de tarification pour Azure Search | Documents Microsoft"
description: "Azure Search peut être configuré sur ces niveaux de référence (SKU) : Gratuit, De base et Standard, où Standard est disponible dans différentes configurations de ressources et différents niveaux de capacité."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 8d4b7bca-02a5-43ee-b3f8-03551dfb32fd
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/24/2016
ms.author: heidist
ms.openlocfilehash: eac9a09266db9da4900766808be3bc3b3ff11519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-sku-or-pricing-tier-for-azure-search"></a>Choisir une référence (SKU) ou un niveau tarifaire pour Azure Search
Dans Azure Search, un [service est configuré](search-create-service-portal.md) sur un niveau tarifaire ou une SKU spécifique. Vous avez le choix entre les options suivantes : **Gratuit**, **De base** ou **Standard**, où **Standard** est disponible dans plusieurs configurations et capacités.

Hello cet article vise toohelp vous choisissez un niveau. Si capacité d’un niveau s’élève toobe trop bas, vous aurez besoin des tooprovision un nouveau service de niveau supérieur de hello et recharger votre index. Il n’existe aucune mise à niveau in situ de hello même service à partir d’une référence (SKU) tooanother.

> [!NOTE]
> Une fois que vous choisissez un niveau et [configurer un service de recherche](search-create-service-portal.md), vous pouvez augmenter le réplica et les nombres de partition dans le service de hello. Consultez [Mettre à l’échelle les niveaux de ressources pour interroger et indexer les charges de travail](search-capacity-planning.md) pour en savoir plus.
>
>

## <a name="how-tooapproach-a-pricing-tier-decision"></a>Comment la décision de niveau tooapproach une tarification
Dans Azure Search, couche de hello détermine la capacité, la disponibilité des fonctionnalités pas. De manière générale, les fonctionnalités sont disponibles à chaque niveau, notamment les fonctionnalités préliminaires. une exception de Hello n’est aucune prise en charge pour les indexeurs dans S3 HD.

> [!TIP]
> Nous vous recommandons de toujours configurer un service **Gratuit** (un par abonnement, sans date d’expiration) afin qu’il soit facilement disponible pour les petits projets. Hello d’utilisation **libre** service de test et d’évaluation ; créez un deuxième service facturable à hello **base** ou **Standard** couche de grandes charges de travail de test ou de production.
>
>

La capacité et les coûts de l’exécution du service de hello accédez dans pair. Informations de cet article peuvent vous aider à décider quels SKU remet équilibre hello, mais pour un de ses toobe utile, vous devez au moins les estimations sur les éléments suivants de hello :

* Nombre et la taille des index vous envisagez de toocreate
* Nombre et taille de tooupload de documents
* Volume de requêtes, en termes de requêtes par seconde (RPS).

Nombre et taille sont importants, car les limites maximales sont accessibles via une limite inconditionnelle sur nombre hello d’index ou de documents dans un service, ou sur les ressources (stockage ou des réplicas) utilisées par le service de hello. Bonjour limite réelle pour votre service est retenue utilisée en premier : ressources ou des objets.

Des estimations dans main, hello suit doit simplifier hello :

* **Étape 1** examiner les descriptions de référence (SKU) hello ci-dessous toolearn sur les options disponibles.
* **Étape 2** répondre aux questions de hello ci-dessous tooarrive à une décision préliminaire.
* **Étape 3** Valider votre décision en passant en revue des limites strictes en matière de stockage et de tarification.

## <a name="sku-descriptions"></a>Descriptions de la référence (SKU)
Hello tableau suivant fournit des descriptions de chaque couche.

| Niveau | Principaux scénarios |
| --- | --- |
| **Gratuit** |Un service partagé, sans frais, utilisé pour l’évaluation, l’investigation ou de petites charges de travail. Car il est partagé avec d’autres abonnés, débit de requête et d’indexation varie en fonction qui d’autre utilise un service de hello. Faible capacité (50 Mo ou 3 index contenant jusqu’à 10 000 documents chacun). |
| **De base** |Charges de travail de production de petite taille sur du matériel dédié. Hautement disponible. La capacité est too3 réplicas et 1 partition (2 Go). |
| **S1** |Standard 1 prend en charge les combinaisons flexibles de partitions (12) et de réplicas (12), utilisées pour des charges de travail de taille moyenne sur du matériel dédié. Vous pouvez allouer des partitions et des réplicas dans des combinaisons prises en charge par un nombre maximal de 36 unités de recherche facturables. À ce niveau, les partitions sont de 25 Go chacune et le RPS est d’environ 15 requêtes par seconde. |
| **S2** |Standard 2 s’exécute de grandes charges de travail de production à l’aide d’unités de recherche hello même 36 que S1, mais avec des réplicas et des partitions de tailles supérieure. À ce niveau, les partitions sont de 100 Go chacune et le RPS est d’environ 60 requêtes par seconde. |
| **S3** |3 standard s’exécute les charges de production proportionnellement plus volumineux sur les systèmes haut de gamme, dans des configurations de too12 partitions ou des 12 réplicas sous 36 unités de recherche. À ce niveau, les partitions sont de 200 Go chacune et le RPS est d’environ 60 requêtes par seconde. |
| **S3 HD** |Standard 3 haute densité est conçu pour un grand nombre d’index plus petits. Vous pouvez avoir des partitions too3, à 200 Go. Le RPS est supérieur à 60 requêtes par seconde. |

> [!NOTE]
> Valeurs maximales de réplica et de la partition sont facturées comme unités de recherche (36 unité maximum par service), qui impose une limite inférieure effective que le maximum de hello implique à la valeur de la face. Par exemple, au maximum hello toouse 12 réplicas, vous pouvez avoir au maximum 3 partitions (12 * 3 = 36 unités). De même, toouse nombre maximal de partitions, réduire too3 de réplicas. Pour accéder à un graphique sur les combinaisons autorisées, voir [Mettre à l’échelle les niveaux de ressources pour interroger et indexer les charges de travail dans Azure Search](search-capacity-planning.md) .
>
>

## <a name="review-limits-per-tier"></a>Passer en revue les limites par couche
Hello graphique suivant est un sous-ensemble des limites hello de [limites de Service dans Azure Search](search-limits-quotas-capacity.md). Il répertorie hello facteurs tooimpact probablement une décision de référence (SKU). Vous pouvez faire référence toothis graphique lorsque vous parcourez les questions de hello ci-dessous.

| Ressource | Gratuit | De base | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Contrat de Niveau de Service (SLA) |Nonn <sup>1</sup> |Oui |Oui |Oui |Oui |Oui |
| Limites d’index |3 |5 |50 |200 |200 |1000 <sup>2</sup> |
| Limites du document |10 000 au total |1 million par service |15 millions par partition |60 millions par partition |120 millions par partition |1 million par index |
| Partitions maximales |N/A |1 |12 |12 |12 |3 <sup>2</sup> |
| Taille de partition |50 Mo au total |2 Go par service |25 Go par partition |100 Go par partition (haut tooa maximum 1,2 To par service) |200 Go par partition (haut tooa to au maximum 2,4 par service) |200 Go (haut tooa maximum 600 Go par service) |
| Réplicas maximales |N/A |3 |12 |12 |12 |12 |
| Requêtes par seconde |N/A |~3 par réplica |~15 par réplica |~60 par réplica |Moins de 60 par réplica |Moins de 60 par réplica |

<sup>1</sup> Les fonctionnalités de niveau Gratuit et d’évaluation ne sont pas fournies avec des Contrats de niveau de service (SLA). Pour tous les niveaux facturables, les SLA entrent en vigueur lorsque vous approvisionnez une redondance suffisante pour votre service. Un SLA de requête (lecture) requiert au moins deux réplicas. Un SLA de requête et d’indexation (lecture-écriture) nécessite au moins trois réplicas. nombre de Hello de partitions n’est pas un facteur de contrat SLA. 

<sup>2</sup> Les niveaux S3 et S3 HD sont soutenus par une infrastructure haute capacité identique, mais chacun d’eux atteint sa limite maximale de différentes façons. S3 permet de cibler un plus petit nombre d’index très volumineux. Par conséquent, sa limite maximale est liée à la ressource (2,4 To pour chaque service). S3 HD cible un grand nombre de très petits index. Au niveau des index de 1 000, S3 HD atteint ses limites sous forme de hello de contraintes d’index. Si vous êtes un client S3 HD qui nécessite plus de 1 000 index, contactez le Support Microsoft pour plus d’informations sur la façon de tooproceed.

## <a name="eliminate-skus-that-dont-meet-requirements"></a>Éliminer les références qui ne répondent pas aux exigences
Hello suivant questions peut vous aider à arriver à la bonne décision de référence (SKU) hello pour votre charge de travail.

1. Avez-vous des exigences en matière de **contrat de niveau de service (SLA)** ? Vous pouvez utiliser n’importe quel niveau facturable (De base et plus), mais vous devez configurer votre service pour assurer la redondance. Un SLA de requête (lecture) requiert au moins deux réplicas. Un SLA de requête et d’indexation (lecture-écriture) nécessite au moins trois réplicas. nombre de Hello de partitions n’est pas un facteur de contrat SLA.
2. **De combien d’index** avez-vous besoin ? Une des variables de plus grands hello factorisant à une décision de référence (SKU) est le nombre de hello d’index pris en charge par chaque référence (SKU). Prise en charge de l’index est à nettement différents niveaux dans hello inférieur niveaux tarifaires. Les exigences en matière de nombre d’index sont déterminantes dans le choix d’une référence (SKU).
3. **Le nombre de documents** sera chargée dans chaque index ? nombre de hello et la taille des documents déterminera la taille finale de hello d’index de hello. En supposant que vous pouvez estimer hello taille prévue de l’index de hello, vous pouvez comparer ce nombre par rapport à la taille de la partition hello par référence (SKU), étendu par nombre de hello de toostore requis de partitions d’un index de cette taille.
4. **Quelle est la charge de requête attendu hello**? Une fois que les besoins de stockage sont compris, penchez-vous sur les charges de travail de requête. Les références (SKU) S2 et S3 offrent un débit presque équivalent, mais les exigences du contrat SLA écartent toute référence (SKU) de version préliminaire.
5. Si vous envisagez de hello S2 ou S3 niveau, déterminez si vous avez besoin [indexeurs](search-indexer-overview.md). Les indexeurs ne sont pas encore disponibles pour le niveau de S3 HD hello. Autre approche consiste à toouse un modèle d’émission pour les mises à jour de l’index, où vous écrivez toopush de code d’application, un index de tooan du jeu de données.

La plupart des clients peuvent de règle d’un SKU spécifique ou de sortie en fonction de leur toohello réponses ci-dessus. Si vous savez toujours le toogo de référence (SKU) avec, vous pouvez publier des questions tooMSDN ou forums de dépassement de capacité, ou contactez le Support technique Azure pour obtenir des instructions.

## <a name="decision-validation-does-hello-sku-offer-sufficient-storage-and-qps"></a>La décision de validation : hello référence (SKU) offre suffisamment de stockage et de requêtes par seconde ?
La dernière étape, réexaminer hello [page de tarification](https://azure.microsoft.com/pricing/details/search/) et hello [sections par service et par index dans les limites de Service](search-limits-quotas-capacity.md) toodouble-Vérifiez vos estimations par rapport aux limites d’abonnement et le service.

Si deux exigences de prix ou le stockage de hello sont hors limites, vous pourriez les charges de travail hello toorefactor parmi plusieurs services plus petits (par exemple). Sur un niveau plus granulaire, vous pourriez redéfinir toobe index plus petit, ou utilisez filtres toomake des requêtes plus efficaces.

> [!NOTE]
> Les besoins de stockage peuvent être augmentés de façon excessive si les documents contiennent des données superflues. Dans l’idéal, les documents sont constitués uniquement de métadonnées ou de données interrogeables. Données binaires sont non interrogeables et doivent être stockées séparément (peut-être dans un stockage de table ou un objet blob Azure) avec un champ hello index toohold un données externe de toohello référence d’une URL. Hello d’un document individuel est de 16 Mo (ou moins se vous sont plusieurs documents dans une demande de chargement en bloc). Pour plus d’informations, voir [Limites de service d’Azure Search](search-limits-quotas-capacity.md) .
>
>

## <a name="next-step"></a>Étape suivante
Une fois que vous savez qui référence (SKU) est hello ajuster à droite, poursuivez comme suit :

* [Créer un service de recherche dans le portail de hello](search-create-service-portal.md)
* [Modifier l’allocation de partitions et réplicas tooscale hello votre service](search-capacity-planning.md)
