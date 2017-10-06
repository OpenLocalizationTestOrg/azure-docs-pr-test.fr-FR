---
title: aaaPolicies dans Gestion des API Azure | Documents Microsoft
description: "Découvrez comment toocreate, modifier et configurer des stratégies de gestion des API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a>Stratégies dans Gestion des API Azure
Gestion des API Azure, les stratégies sont une fonctionnalité puissante du système hello autoriser la publication de hello toochange hello du comportement de hello API via la configuration. Les stratégies sont une collection d’instructions qui sont exécutées séquentiellement sur la demande de hello ou de réponse d’une API. Les instructions populaires incluent une conversion de format à partir de XML tooJSON et limiter ainsi toorestrict hello d’appels entrants à partir d’un développeur de taux d’appels. De nombreuses stratégies supplémentaires sont disponibles en dehors de la zone de hello.

Consultez hello [référence de stratégie] [ Policy Reference] pour obtenir la liste complète des instructions de stratégie et leurs paramètres.

Stratégies sont appliquées à l’intérieur de passerelle hello qui se situe entre les consommateurs d’API hello et hello géré API. Hello passerelle reçoit toutes les requêtes et les non modifiée transfère généralement toohello sous-jacent API. Cependant une stratégie peut s’appliquer demande entrante de modifications tooboth hello et la réponse sortante.

Expressions de stratégie peuvent être utilisées en tant que valeurs d’attribut ou valeurs de texte dans une des stratégies de gestion des API hello, sauf indication contraire de la stratégie de hello. Certaines stratégies telles que hello [flux de contrôle] [ Control flow] et [Set variable] [ Set variable] stratégies basées sur des expressions de stratégie. Pour plus d’informations, consultez les rubriques [Stratégies avancées][Advanced policies] et [Expressions de stratégie][Policy expressions].

## <a name="scopes"></a>Comment tooconfigure stratégies
Stratégies peuvent être configurées globalement ou au niveau de portée hello d’un [produit][Product], [API] [ API] ou [opération] [Operation]. tooconfigure une stratégie, accédez toohello éditeur de stratégies dans le portail de publication hello.

![Policies menu][policies-menu]

éditeur de stratégies Hello se compose de trois sections principales : hello stratégie étendue (du haut), hello définition de stratégie dans lequel les stratégies sont modifiés (à gauche) et les instructions hello liste (à droite) :

![Policies editor][policies-editor]

toobegin configuration d’une stratégie, que vous devez d’abord sélectionner étendue hello à quels hello stratégie doit s’appliquer. Capture d’écran hello ci-dessous hello **Starter** produit est sélectionné. Notez que ce nom de la stratégie de toohello suivant hello symbole carré indique qu’une stratégie est déjà appliquée à ce niveau.

![Scope][policies-scope]

Dans la mesure où une stratégie a déjà été appliquée, configuration de hello est présentée dans l’affichage de la définition hello.

![Configuration][policies-configure]

stratégie de Hello est affichée en lecture seule dans un premier temps. Dans l’ordre tooedit définition de hello, cliquez sur hello **configurer la stratégie** action.

![Modifier][policies-edit]

définition de stratégie Hello est un document XML simple qui décrit une séquence d’instructions entrantes et sortantes. Hello XML peut être modifiée directement dans la fenêtre de définition de hello. Une liste d’instructions est fournie toohello à droite et l’étendue actuelle d’instructions toohello applicables sont activés et mis en surbrillance ; comme indiqué par hello **le taux d’appels limite** instruction dans la capture d’écran hello ci-dessus.

En cliquant sur une instruction activée ajoutera hello XML approprié à l’emplacement de hello de curseur hello dans l’affichage de la définition hello. 

> [!NOTE]
> Si la stratégie de hello que vous souhaitez tooadd n’est pas activée, assurez-vous que vous êtes dans la portée appropriée de hello pour cette stratégie. Chaque instruction de stratégie est conçue pour une utilisation dans certaines étendues et sections de la stratégie. sections de stratégie tooreview hello et étendues pour une stratégie, vérifiez hello **utilisation** section pour cette stratégie Bonjour [référence de stratégie][Policy Reference].
> 
> 

Une liste complète des instructions de stratégie et leurs paramètres sont disponibles dans hello [référence de stratégie][Policy Reference].

Par exemple, tooadd un nouveau toorestrict d’instruction entrant demande toospecified des adresses IP, placez le curseur hello à l’intérieur de contenu hello Hello `inbound` hello d’élément et cliquez sur XML **Restrict appelant IPs** instruction.

![Restriction policies][policies-restrict]

Cette opération ajoute une toohello d’extrait de code XML `inbound` élément qui fournit des conseils sur la façon dont tooconfigure hello instruction.

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

toolimit les demandes entrantes et acceptez uniquement les à partir d’une adresse IP 1.2.3.4 modifier hello XML comme suit :

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Enregistrer][policies-save]

Configuration des instructions hello pour la stratégie de hello terminé, cliquez sur **enregistrer** et modifications de hello seront passerelle de gestion des API toohello propagées immédiatement.

## <a name="sections"></a>Configuration de la stratégie
Une stratégie est une série d'instructions qui s'exécutent dans l'ordre pour une demande et une réponse. configuration de Hello est divisée en conséquence `inbound`, `backend`, `outbound`, et `on-error` sections comme indiqué dans la configuration suivante de hello.

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

S’il existe une erreur lors du traitement de hello d’une demande, les autres étapes Bonjour `inbound`, `backend`, ou `outbound` sections sont ignorées et l’exécution passe instructions toohello Bonjour `on-error` section. En plaçant des instructions de stratégie Bonjour `on-error` section, vous pouvez consulter les erreurs hello à l’aide de hello `context.LastError` propriété, examiner et personnaliser la réponse d’erreur hello à l’aide de hello `set-body` stratégie et configurer que se passe-t-il si une erreur se produit. Il existe des codes d’erreur pour obtenir des instructions intégrées et les erreurs qui peuvent se produire pendant le traitement de hello des instructions de stratégie. Pour plus d'informations, consultez [Gestion des erreurs dans les stratégies de gestion des API](https://msdn.microsoft.com/library/azure/mt629506.aspx).

Étant donné que les stratégies peuvent être spécifiés à différents niveaux (globale, produit, api et operation) hello configuration offre un moyen vous ordre de hello toospecify dans laquelle les instructions de définition de stratégie hello s’exécutent avec la stratégie de respect toohello parent. 

Étendues de stratégie sont évalués dans hello suivant l’ordre.

1. Étendue globale
2. Étendue produit
3. Étendue API
4. Étendue opération

Hello instructions au sein de celles-ci sont évaluées en fonction de la sélection élective toohello Hello `base` élément, s’il est présent. La stratégie globale a aucune stratégie parent et à l’aide de hello `<base>` élément qu’il n’a aucun effet.

Par exemple, si vous avez une stratégie au niveau global de hello et une stratégie configurée pour une API, puis chaque fois que cette API particulière est utilisée les deux stratégies sont appliquées. Gestion des API permettant d’ordre déterministe des instructions de stratégie combinée via l’élément de base hello. 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

Dans la définition de stratégie exemple hello ci-dessus, hello `cross-domain` instruction exécuterait avant les stratégies plus élevées, qui à leur tour, être suivie hello `find-and-replace` stratégie. 

stratégies de hello toosee dans l’étendue actuelle de hello dans l’éditeur de stratégie de hello, cliquez sur **recalculer la stratégie effective pour l’étendue sélectionnée**.

## <a name="next-steps"></a>Étapes suivantes
Découvrez la vidéo suivante sur les expressions de stratégie.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
