---
title: "les versions d’Azure Search aaaAPI | Documents Microsoft"
description: "Stratégie de version pour API REST de recherche Azure et hello bibliothèque cliente Bonjour SDK .NET."
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 0458053a-164e-4682-a802-00097ecde981
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 4fa722fad5577c6b254be7fa673eb240fff316a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-versions-in-azure-search"></a>Versions d’API dans Azure Search
Azure Search déploie régulièrement des mises à jour de fonctionnalités. Parfois, mais pas toujours, ces mises à jour nécessitent toopublish une nouvelle version de compatibilité descendante toopreserve API. Une nouvelle version de publication vous permet de toocontrol quand et comment intégrer des mises à jour du service de recherche dans votre code.

En règle générale, nous essayons toopublish nouvelles versions uniquement lorsque cela est nécessaire, car elle peut impliquer certains tooupgrade effort votre version de toouse une nouvelle API de code. Nous publierons uniquement une nouvelle version si nous devons toochange certains aspects de hello API d’une manière qui risquerait de compatibilité descendante. Cela peut se produire en raison des correctifs tooexisting fonctionnalités ou en raison des nouvelles fonctionnalités qui modifient la surface d’exposition des API existante.

Nous suivons hello même règle de mises à jour du Kit de développement logiciel. Bonjour Azure Search SDK suit hello [contrôle de version sémantique](http://semver.org/) règles, ce qui signifie que sa version comprend trois parties : majeure, mineure et le numéro (par exemple, 1.1.0). Nous publiera une nouvelle version majeure de hello Kit de développement logiciel uniquement en cas de modifications qui rompent la compatibilité descendante. Les mises à jour de la fonctionnalité sans rupture, nous incrémente le numéro de version secondaire hello et pour les correctifs de bogues nous augmente uniquement à la version hello.

> [!NOTE]
> Votre instance du service Azure Search prend en charge plusieurs versions de l’API REST, y compris hello version la plus récente. Vous pouvez continuer toouse une version lorsqu’il n’est plus hello version la plus récente, mais nous vous recommandons de migrer votre code toouse hello dernière version. Lorsque vous utilisez l’API REST de hello, vous devez spécifier la version de l’API hello dans chaque demande via un paramètre de version de l’api hello. Lorsque vous utilisez hello .NET SDK, version hello Hello SDK que vous utilisez détermine hello correspond à la version de l’API REST de hello. Si vous utilisez un kit de développement plus anciens, vous pouvez continuer toorun que le code sans aucune modification même si le service de hello est mis à niveau toosupport une API la plus récente version.

## <a name="snapshot-of-current-versions"></a>Instantané des versions actuelles
Voici les versions actuelles de tous les tooAzure interfaces programmation recherche un instantané de hello.

| Interfaces | Version majeure la plus récente | État |
| --- | --- | --- |
| [Kit SDK .NET](https://aka.ms/search-sdk) |3.0 |Mise à la disposition générale en novembre 2016 |
| [Version préliminaire du Kit de développement logiciel (SDK) .NET](https://aka.ms/search-sdk-preview) |2.0-preview |Version préliminaire, publiée en août 2016 |
| [API REST du service](https://docs.microsoft.com/rest/api/searchservice/) |2016-09-01 |Mise à la disposition générale |
| [Version préliminaire de l’API REST Service](search-api-2015-02-28-preview.md) |2015-02-28-Preview |VERSION PRÉLIMINAIRE |
| [.NET Management SDK](https://aka.ms/search-mgmt-sdk) |2015-08-19 |Mise à la disposition générale |
| [l’API REST de gestion ;](https://docs.microsoft.com/rest/api/searchmanagement/) |2015-08-19 |Mise à la disposition générale |

Pourquoi les API REST, y compris hello `api-version` sur chaque appel n’est requise. Il est ainsi facile tootarget une version spécifique, par exemple une API d’aperçu. Hello exemple suivant illustre comment hello `api-version` paramètre est spécifié :

    GET https://adventure-works.search.windows.net/indexes/bikes?api-version=2016-09-01

> [!NOTE]
> Bien que chaque demande un `api-version`, nous vous recommandons d’utiliser hello même version pour toutes les demandes API. Cela est particulièrement vrai lorsque de nouvelles versions d’API introduisent des attributs ou des opérations qui ne sont pas reconnus par les versions précédentes. La combinaison de versions d’API peut avoir des conséquences inattendues et doit être évitée.
>
> Hello API REST du Service et l’API REST de gestion sont gérées indépendamment les uns des autres. Toute ressemblance dans les numéros de version est une coïncidence.

Généralement disponible (ou de la disponibilité générale) API peut être utilisé en production et sont objet tooAzure les contrats de niveau de service. Les versions préliminaires offrent des fonctionnalités expérimentales qui ne sont pas toujours tooa migrés GA version. **Nous vous conseillons vivement d’utiliser des API en version préliminaire dans les applications de production.**

## <a name="about-preview-and-generally-available-versions"></a>À propos des versions préliminaires et mises à la disposition générale
Azure Search toujours préalable libère des fonctionnalités expérimentales via l’API REST de hello tout d’abord, puis par le biais des versions préliminaires de hello du SDK .NET.

Fonctionnalités en version préliminaire ne sont pas garanti que toobe migré tooa GA version. Tandis que les fonctionnalités dans une version GA sont considérées comme stable et peu toochange avec l’exception hello de petits correctifs de compatibilité descendante et des améliorations, les fonctionnalités préliminaires sont disponibles pour le test et d’expérimentation, avec comme objectif hello recueillir des commentaires sur conception et implémentation.

Toutefois, comme fonctionnalités préliminaires sont toochange de sujet, nous vous recommandons par rapport à l’écriture de code de production qui prennent une dépendance sur les versions préliminaires. Si vous utilisez une version antérieure, nous vous recommandons de migrer toohello généralement disponible version en disponibilité générale.

Pourquoi .NET SDK : vous trouverez des conseils pour la migration du code à [hello mise à niveau .NET SDK](search-dotnet-sdk-migration.md).

Disponibilité générale signifie que Azure Search est maintenant sous le contrat de niveau de service (SLA) hello. Hello SLA, consultez [contrats de niveau de Service de recherche Azure](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
