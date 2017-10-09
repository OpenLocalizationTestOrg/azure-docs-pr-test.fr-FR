---
title: aaaUpgrading toohello API REST du Service Azure Search version 2016-09-01 | Documents Microsoft
description: "La mise à niveau toohello API REST du Service Azure Search version 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a>La mise à niveau toohello API REST du Service Azure Search version 2016-09-01
Si vous utilisez la version 2015-02-28 ou 2015-02-28-Preview Hello [API REST de Service Azure Search](https://msdn.microsoft.com/library/azure/dn798935.aspx), cet article va vous aider à mettre à niveau votre application toouse hello suivant disponible version de l’API, 2016-09-01.

Version 2016-09-01 de l’API REST de hello contient certaines modifications à partir de versions antérieures. Ces modifications sont, pour la plupart, à compatibilité descendante. La modification de votre code est donc facilitée, selon la version que vous utilisiez précédemment. Consultez [étapes tooupgrade](#UpgradeSteps) pour obtenir des instructions sur la façon de toochange votre code toouse hello nouvelle version de l’API.

> [!NOTE]
> Votre instance du service Azure Search prend en charge plusieurs versions de l’API REST, y compris hello version la plus récente. Vous pouvez continuer toouse une version lorsqu’il n’est plus hello version la plus récente, mais nous vous recommandons de migrer votre code toouse hello dernière version.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a>Nouveautés de la version 2016-09-01
Version 2016-09-01 est la deuxième version généralement disponible hello Hello API REST de Service Azure Search. Cette version de l’API comprend les nouvelles fonctionnalités suivantes :

* [Analyseurs personnalisés](https://aka.ms/customanalyzers), qui vous permettent de contrôler de tootake de processus hello de conversion de texte en jetons indexables et de recherches.
* [Stockage d’objets Blob Azure](search-howto-indexing-azure-blob-storage.md) et [Azure Table Storage](search-howto-indexing-azure-tables.md) indexeurs, ce qui vous tooeasily importer des données depuis le stockage Azure dans Azure Search dans une planification ou d’une demande.
* [Mappages de champ](search-indexer-field-mappings.md), qui vous permettent de toocustomize comment indexeurs importer des données dans Azure Search.
* ETags vous permettant de définitions de hello tooupdate d’index, indexeurs et sources de données de manière concurrentiel. 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Étapes tooupgrade
Si vous mettez à niveau à partir de la version 2015-02-28, vous ne disposez probablement toomake tout code tooyour de modifications, que le numéro de version toochange hello. les situations uniquement Hello dans lesquelles vous devrez peut-être toochange code sont quand :

* Lorsque votre code échoue, car des propriétés non reconnues sont renvoyées dans une réponse de l’API. Par défaut, votre application doit ignorer les propriétés qu’elle ne comprend pas.
* Votre code persiste des demandes de l’API et tente de tooresend les toohello nouvelle version de l’API. Par exemple, cela peut se produire si votre application conserve les jetons de continuation retournés à partir de l’API de recherche de hello (pour plus d’informations, recherchez `@search.nextPageParameters` Bonjour [référence des API de recherche](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).

Si une des situations suivantes s’appliquent tooyou, il vous faudra peut-être toochange votre code en conséquence. Dans le cas contraire, aucune modification ne doit être nécessaire sauf si vous souhaitez toostart à l’aide de hello [nouvelles fonctionnalités](#WhatsNew) de version 2016-09-01.

Si vous mettez à niveau à partir de la version 2015-02-28-Preview, hello ci-dessus s’applique également, mais vous devez également être conscient que certaines fonctionnalités en version préliminaire ne sont pas disponibles dans la version 2016-09-01 :

* Prise en charge des indexeurs Stockage Blob Azure pour les fichiers CSV et les objets Blob contenant des tableaux JSON.
* Synonymes
* Requêtes « More like this »

Si votre code utilise ces fonctionnalités, vous ne serez pas en mesure de tooupgrade too2016-09-01 sans supprimer l’utilisation de leur.

> [!IMPORTANT]
> N’oubliez pas que les API d’évaluation sont destinées à être utilisées à des fins de test et d’évaluation, et non dans les environnements de production.
> 
> 

## <a name="conclusion"></a>Conclusion
Si vous avez besoin de plus de détails sur l’utilisation de hello API REST de Service Azure Search, consultez hello récemment mis à jour [référence de l’API](https://msdn.microsoft.com/library/azure/dn798935.aspx) sur MSDN.

Vos commentaires sur la Recherche Azure sont les bienvenus. Si vous rencontrez des problèmes, vous pouvez tooask libre nous de l’aide sur hello [forum MSDN de recherche Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) ou [StackOverflow](http://stackoverflow.com/). Si vous êtes poser une question concernant Azure rechercher sur StackOverflow, vérifiez les tootag qu’avec `azure-search`.

Merci d’utiliser Azure Search !

