---
title: "tables de données et de recherche de référence dans le flux de données Analytique aaaUse | Documents Microsoft"
description: "Utiliser des données de référence dans une requête Stream Analytics"
keywords: "table de choix, données de référence"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a>Utilisation de données de référence ou de tables de choix dans un flux d’entrée Stream Analytics
Les données de référence (également appelé une table de recherche) sont un jeu de données fini est statique ou ralentir la modification par nature, utilisé tooperform une recherche ou toocorrelate avec votre flux de données. utilisation de toomake de données de référence dans votre tâche Analytique de flux de données Azure, vous utiliserez généralement un [joindre des données de référence](https://msdn.microsoft.com/library/azure/dn949258.aspx) dans votre requête. Analytique de flux de données utilise le stockage d’objets Blob Azure en tant que couche de stockage hello pour les données de référence, et avec la référence d’Azure Data Factory de données transformé et/ou copiés tooAzure stockage d’objets Blob, pour une utilisation en tant que données de référence, à partir de [un nombre quelconque de nuage et magasins de données local](../data-factory/data-factory-data-movement-activities.md). Les données de référence sont modélisées en tant que séquence d’objets BLOB (défini dans la configuration d’entrée de hello) dans l’ordre croissant de hello date/heure spécifié dans le nom d’objet blob hello. Il **uniquement** prend en charge l’ajout de fin toohello de séquence de hello à l’aide d’une date/heure **supérieur** que celui spécifié par le dernier objet blob de hello dans la séquence de hello hello.

Analytique de flux de données a un **limite de 100 Mo par objet blob** , mais les travaux peuvent traiter plusieurs objets BLOB de référence à l’aide de hello **modèle de chemin d’accès** propriété.


## <a name="configuring-reference-data"></a>Configuration des données de référence
tooconfigure vos données de référence, vous devez tout d’abord toocreate une entrée est de type **les données de référence**. tableau Hello ci-dessous décrit chaque propriété que vous devez tooprovide lors de la création des entrées de données de référence hello avec sa description :


<table>
<tbody>
<tr>
<td>Nom de la propriété</td>
<td>Description</td>
</tr>
<tr>
<td>Alias d’entrée</td>
<td>Un nom convivial qui sera utilisé dans hello tâche requête tooreference cette entrée.</td>
</tr>
<tr>
<td>Compte de stockage</td>
<td>nom Hello hello du compte de stockage dans lequel se trouvent vos objets BLOB. S’il s’agit de hello même d’abonnement en tant que votre tâche Analytique de flux de données, vous pouvez le sélectionner hello de liste déroulante.</td>
</tr>
<tr>
<td>Clé du compte de stockage</td>
<td>clé secrète de Hello associée au compte de stockage hello. Il est renseigné automatiquement si le compte de stockage hello est Bonjour même abonnement que votre tâche de flux de données Analytique.</td>
</tr>
<tr>
<td>Conteneur de stockage</td>
<td>Les conteneurs fournissent un regroupement logique des objets BLOB stockés dans hello service Microsoft Azure Blob. Lorsque vous téléchargez un objet blob de toohello service Blob, vous devez spécifier un conteneur pour cet objet blob.</td>
</tr>
<tr>
<td>Modèle de chemin d'accès</td>
<td>chemin d’accès Hello utilisé toolocate vos objets BLOB dans le conteneur spécifié de hello. Dans le chemin d’accès de hello, vous pouvez choisir toospecify une ou plusieurs instances de hello suivant des 2 variables :<BR>{date}, {time}<BR>Exemple 1 : products/{date}/{time}/product-list.csv<BR>Exemple 2 : products/{date}/product-list.csv
</tr>
<tr>
<td>Format de la date [facultatif]</td>
<td>Si vous avez utilisé {date} dans hello modèle de chemin d’accès que vous avez spécifié, vous pouvez sélectionner format de date hello dans lequel vos objets BLOB est organisés dans hello liste déroulante des formats pris en charge.<BR>Exemple : AAAA/MM/JJ, MM/JJ/AAAA, etc.</td>
</tr>
<tr>
<td>Format de l’heure [facultatif]</td>
<td>Si vous avez utilisé {time} dans hello modèle de chemin d’accès que vous avez spécifié, vous pouvez sélectionner format d’heure hello dans lequel vos objets BLOB est organisés dans hello liste déroulante des formats pris en charge.<BR>Exemple : HH, HH/mm ou HH-mm</td>
</tr>
<tr>
<td>Format de sérialisation de l’événement</td>
<td>toomake que vos requêtes fonctionnent comme hello prévu, flux de données Analytique doit tooknow format de sérialisation que vous utilisez pour les flux de données entrantes. Pour les données de référence, les formats de hello pris en charge sont CSV et JSON.</td>
</tr>
<tr>
<td>Encodage</td>
<td>UTF-8 est hello uniquement une prise en charge de format d’encodage pour l’instant</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>Génération de données de référence sur une planification
Si vos données de référence sont un jeu de données à variation lente, la prise en charge pour l’actualisation des données de référence est activée en spécifiant un chemin d’accès modèle dans la configuration d’entrée de hello à l’aide de hello {date} et des variables de substitution {time}. Flux de données Analytique récupère les définitions de données de référence hello mis à jour en fonction de ce modèle de chemin d’accès. Par exemple, un modèle de `sample/{date}/{time}/products.csv` avec le format de date **« AAAA-MM-jj »** et un format d’heure **« HH : mm »** toopick Analytique de flux de données d’objet blob de hello mis à jour fait en sorte que `sample/2015-04-16/17-30/products.csv` à 5 h 30 avril 16, 2015 UTC horaire.

> [!NOTE]
> Tâches de flux de données Analytique recherchent actuellement pour l’actualisation des objets blob hello uniquement lorsque l’heure de l’ordinateur hello avance toohello encodées dans le nom d’objet blob hello. Par exemple, recherchera les travaux hello `sample/2015-04-16/17-30/products.csv` dès que possible, mais aucune version antérieure à 5 h 30 le 16 avril 2015 UTC fuseau horaire. Il sera *jamais* rechercher un objet blob avec un temps codé plus tôt que hello dernière celui qui est découvert.
> 
> Par exemple, une fois que l’objet blob de hello trouve hello `sample/2015-04-16/17-30/products.csv` il ignore tous les fichiers portant une date codée antérieures à 17 h 30 le 16 avril 2015, donc si une liaison tardive qui arrivent `sample/2015-04-16/17-25/products.csv` blob est créé dans hello même tâche hello de conteneur ne l’utilise pas.
> 
> Même si `sample/2015-04-16/17-30/products.csv` se produit uniquement à 10 h 03 le 16 avril 2015, mais aucun objet blob avec une date antérieure n’est présent dans le conteneur de hello, hello travail utiliser ce fichier en commençant à 10 h 03 le 16 avril 2015 et utiliser les données de référence précédentes hello là.
> 
> Une exception toothis est lorsque le travail de hello doit toore-traitement des données dans le temps ou lors du premier démarrage de la tâche de hello. Au démarrage de tâche hello de temps de recherche blob la plus récente de hello produit avant que le travail de hello heure de début spécifiée. Cette opération est effectuée tooensure qu’il existe un **non vide** référencer le jeu de données au démarrage de la tâche de hello. Si un est introuvable, le travail de hello affiche hello suivant diagnostic : `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) peut s’avérer tooorchestrate utilisé hello de création BLOB hello mis à jour requises par les définitions de données de référence tooupdate Analytique de flux de données. Fabrique de données est un service d’intégration de données basés sur le cloud qui orchestre et automatise le déplacement de hello et la transformation de données. Fabrique de données prend en charge [tooa un grand nombre de banques de données locales et de cloud en fonction de connexion](../data-factory/data-factory-data-movement-activities.md) et déplacement de données facilement à intervalles réguliers que vous spécifiez. Pour plus d’informations et des instructions étape par étape sur la façon dont tooset d’une fabrique de données de pipeline toogenerate les données de référence pour l’Analytique de flux de données qui est actualisé selon une planification prédéfinie, consultez ce [GitHub exemple](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Conseils pour l'actualisation de vos données de référence
1. Remplacement des objets BLOB de données de référence ne provoque pas de flux de données Analytique tooreload hello blob, et dans certains cas, cela peut provoquer hello travail toofail. Hello recommandé la façon dont les données de référence toochange sont tooadd un nouvel objet blob à l’aide du même modèle de conteneur et le chemin d’accès défini dans l’entrée de tâche hello de hello et utilisent une date/heure **supérieur** que celui spécifié par le dernier objet blob de hello dans la séquence de hello hello.
2. Référence des objets BLOB sont **pas** classés par heure de « Dernière modification » de l’objet blob de hello, mais uniquement par la date spécifiée dans le nom d’objet blob hello à l’aide de hello {date} et les substitutions de {time} et l’heure de hello.
3. Une tâche doit revenir en arrière à plusieurs reprises. Par conséquent, les objets blobs de données de référence ne doivent pas être modifiés ou supprimés.

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
Vous avez été introduite tooStream Analytique, un service géré de diffusion en continu d’analytique sur les données à partir de hello Internet des objets. toolearn en savoir plus sur ce service, consultez :

* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
