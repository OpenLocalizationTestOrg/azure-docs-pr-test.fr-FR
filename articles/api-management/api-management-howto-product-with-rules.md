---
title: aaaProtect votre API avec gestion des API Azure | Documents Microsoft
description: "Découvrez comment tooprotect votre API avec les quotas et la limitation des stratégies (débit maximal)."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a>Protéger votre API avec des limites de débit à l’aide de la gestion des API Azure
Ce guide vous explique comment il est facile de protection tooadd pour votre serveur principal API en configurant des stratégies de quota et la limite de taux avec gestion des API Azure.

Dans ce didacticiel, vous allez créer un produit « Version d’évaluation gratuite « API qui permet aux développeurs toomake too10 des appels par minute et au maximum de 200 appels par semaine tooyour API est à l’aide de hello tooa [taux d’appels limite par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) et [ Définir le quota d’utilisation par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) stratégies. Puis vous publiez hello API et tester la stratégie de limite de taux hello.

Plus avancés de la limitation des scénarios à l’aide de hello [taux limite par clé](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) et [par clé de quota](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) stratégies, consultez [demande avancée limitation avec gestion des API Azure](api-management-sample-flexible-throttling.md).

## <a name="create-product"></a>toocreate un produit
Dans cette étape, vous allez créer un produit en version d’évaluation gratuite, qui ne requiert aucune approbation d’abonnement.

> [!NOTE]
> Si vous avez déjà disposer d’un produit configuré et que vous souhaitez toouse il pour ce didacticiel, vous pouvez sauter trop[configurer les stratégies de quota et la limite de taux d’appels] [ Configure call rate limit and quota policies] et suivez le didacticiel de hello à partir de là, l’utilisation du produit à la place de produit d’évaluation gratuite de hello.
> 
> 

tooget démarré, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API.

![Portail des éditeurs][api-management-management-console]

> Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [gérer votre première API de gestion des API Azure] [ Manage your first API in Azure API Management] didacticiel.
> 
> 

Cliquez sur **produits** Bonjour **gestion des API** menu Bonjour toodisplay gauche Bonjour **produits** page.

![Add product][api-management-add-product]

Cliquez sur **ajouter produit** toodisplay hello **ajouter un nouveau produit** boîte de dialogue.

![Ajouter un nouveau produit][api-management-new-product-window]

Bonjour **titre** , tapez **version d’évaluation gratuite**.

Bonjour **Description** boîte, hello du type suivant de texte : **abonnés peuvent être en mesure de toorun 10 appels/minute jusqu'à tooa maximum 200 appels par semaine, après laquelle l’accès est refusé.**

Les produits de Gestion des API peuvent être protégés ou ouverts. Produits protégés doivent être souscrit toobefore ils peuvent être utilisés. Les produits ouverts sont utilisables sans abonnement. Vérifiez que **abonnement** toocreate sélectionné n’est un produit protégé qui nécessite un abonnement. Il s’agit de paramètre par défaut de hello.

Si vous souhaitez un tooreview administrateur et l’accepter ou rejeter abonnement tente toothis produit, sélectionnez **exiger l’approbation de l’abonnement**. Si la case à cocher hello n’est pas sélectionnée, les tentatives d’abonnement sera approuvée automatiquement. Dans cet exemple, les abonnements sont automatiquement approuvées, n’activez ne pas hello à.

tooallow développeur comptes toosubscribe plusieurs fois toohello nouveau produit, sélectionnez hello **autoriser plusieurs abonnements simultanés** case à cocher. Ce didacticiel ne nécessite pas l’utilisation de plusieurs abonnements simultanés. Vous pouvez donc laisser cette case décochée.

Une fois toutes les valeurs sont entrées, cliquez sur **enregistrer** produit de hello toocreate.

![Product added][api-management-product-added]

Par défaut, les nouveaux produits sont visibles toousers Bonjour **administrateurs** groupe. Nous allons tooadd hello **les développeurs** groupe. Cliquez sur **version d’évaluation gratuite**, puis cliquez sur hello **visibilité** onglet.

> Gestion des API, les groupes sont visibilité de hello utilisé toomanage de toodevelopers de produits. Produits accorder toogroups de visibilité, et les développeurs peuvent afficher et s’abonner toohello les produits qui sont des groupes toohello visible dans laquelle ils appartiennent. Pour plus d’informations, consultez [comment toocreate et l’utilisation de groupes dans la gestion des API Azure][How toocreate and use groups in Azure API Management].
> 
> 

![Add developers group][api-management-add-developers-group]

Sélectionnez hello **les développeurs** case à cocher, puis cliquez sur **enregistrer**.

## <a name="add-api"></a>tooadd une API toohello produit
Dans cette étape du didacticiel de hello, nous allons ajouter hello Echo produit API de toohello nouvelle version d’évaluation gratuite.

> Chaque instance de service de gestion des API est préconfigurée avec une API d’écho qui peuvent être utilisé tooexperiment avec et en savoir plus sur la gestion des API. Pour plus d’informations, consultez [Gérer votre première API dans Gestion des API Azure][Manage your first API in Azure API Management].
> 
> 

Cliquez sur **produits** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **version d’évaluation gratuite** produit de hello tooconfigure.

![Configure product][api-management-configure-product]

Cliquez sur **tooproduct d’ajouter les API**.

![Ajouter les API tooproduct][api-management-add-api]

Sélectionnez **API Echo**, puis cliquez sur **Enregistrer**.

![Add Echo API][api-management-add-echo-api]

## <a name="policies"></a>tooconfigure les stratégies de quota et la limite de taux d’appels
Quotas et limites de taux sont configurés dans l’éditeur de stratégie hello. Dans ce didacticiel, nous allons ajouter des stratégies Hello deux sont hello [taux d’appels limite par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) et [définir le quota d’utilisation par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) stratégies. Ces stratégies doivent être appliquées à la portée du produit hello.

Cliquez sur **stratégies** sous hello **gestion des API** menu à gauche de hello. Bonjour **produit** , cliquez sur **version d’évaluation gratuite**.

![Product policy][api-management-product-policy]

Cliquez sur **ajouter une stratégie** tooimport hello du modèle de stratégie et commencer à créer des stratégies de quota et la limite de taux hello.

![Add policy][api-management-add-policy]

Stratégies de quota et la limite de taux sont des stratégies entrants, dans ce curseur hello de position dans l’élément d’entrants hello.

![Policy editor][api-management-policy-editor-inbound]

Faites défiler la liste des stratégies hello et localiser hello **taux d’appels limite par abonnement** entrée de stratégie.

![Policy statements][api-management-limit-policies]

Après avoir hello le curseur est positionné dans hello **entrant** élément de stratégie, cliquez sur la flèche de hello **taux d’appels limite par abonnement** tooinsert son modèle de stratégie.

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

Comme vous pouvez le voir à partir de l’extrait de code hello, stratégie de hello permet de définition des limites pour les opérations et les API du produit hello. Dans ce didacticiel, nous allons ne sera pas utiliser cette fonctionnalité, donc supprimer hello **api** et **opération** éléments à partir de hello **limite de taux** élément, de sorte que seuls hello externe**limite de taux** élément reste, comme indiqué dans hello l’exemple suivant.

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

Dans le produit d’évaluation gratuite de hello, taux d’appels d’autorisée maximale de hello 10 appels par minute, tapez **10** en tant que valeur hello pour hello **appelle** attribut, et **60** pour hello **période de renouvellement** attribut.

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

tooconfigure hello **définir le quota d’utilisation par abonnement** stratégie, la position de votre curseur juste en dessous hello récemment ajouté **limite de taux** élément hello **entrant** élément, puis localisez et cliquez sur hello flèche toohello gauche **définir le quota d’utilisation par abonnement**.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

De même toohello **définir le quota d’utilisation par abonnement** stratégie, **définir le quota d’utilisation par abonnement** stratégie permet de définir des majuscules pour sur les API du produit hello et des opérations. Dans ce didacticiel, nous allons ne sera pas utiliser cette fonctionnalité, donc supprimer hello **api** et **opération** éléments à partir de hello **quota** élément, comme indiqué dans hello l’exemple suivant.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

Les quotas peuvent reposer sur le nombre de hello d’appels par intervalle, la bande passante ou les deux. Dans ce didacticiel, nous sommes sans limitation en fonction de la bande passante, donc supprimer hello **la bande passante** attribut.

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

Dans le produit d’évaluation gratuite de hello, quota de hello est de 200 appels par semaine. Spécifiez **200** en tant que valeur hello pour hello **appelle** d’attribut et spécifiez **604800** en tant que valeur hello pour hello **période de renouvellement** attribut.

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> Les intervalles de stratégie sont spécifiés en secondes. intervalle de salutation toocalculate pendant une semaine, vous pouvez multiplier hello nombre de jours (7) par nombre de hello d’heures par jour (24) par un nombre de minutes dans une heure (60) par un nombre de secondes dans une minute (60) hello hello : 7 * 24 * 60 * 60 = 604800.
> 
> 

Lorsque vous avez terminé la configuration de la stratégie de hello, elle doit correspondre à hello l’exemple suivant.

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

Une fois hello souhaité de stratégies sont configurées, cliquez sur **enregistrer**.

![Save policy][api-management-policy-save]

## <a name="publish-product"></a> produit de hello toopublish
Maintenant que hello hello API ont été ajoutées et hello stratégies sont configurées, produit de hello doit être publié afin qu’il peut être utilisé par les développeurs. Cliquez sur **produits** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **version d’évaluation gratuite** produit de hello tooconfigure.

![Configure product][api-management-configure-product]

Cliquez sur **publier**, puis cliquez sur **Oui, publiez-le** tooconfirm.

![Publish product][api-management-publish-product]

## <a name="subscribe-account"></a>toosubscribe un produit de toohello de compte de développeur
Maintenant ce produit hello est publié, il est tooand toobe disponible abonné utilisé par les développeurs.

> Les administrateurs d’une instance de la gestion des API sont automatiquement souscrit tooevery produit. Dans cette étape du didacticiel, nous peuvent s’abonner à un des comptes de développeur de non-administrateur hello toohello version d’évaluation gratuite produit. Si votre compte de développeur fait partie du rôle des administrateurs de hello, vous pouvez ensuite suivre en même temps que cette étape, même si vous êtes déjà inscrit.
> 
> 

Cliquez sur **utilisateurs** sur hello **gestion des API** hello menu gauche, puis cliquez sur nom hello de votre compte de développeur. Dans cet exemple, nous utilisons hello **Clayton Gragg** compte de développeur.

![Configure developer][api-management-configure-developer]

Cliquez sur **Ajouter un abonnement**.

![Ajouter un abonnement][api-management-add-subscription-menu]

Sélectionnez **Version d’évaluation gratuite**, puis cliquez sur **S’abonner**.

![Ajouter un abonnement][api-management-add-subscription]

> [!NOTE]
> Dans ce didacticiel, plusieurs abonnements simultanées ne sont pas activés pour le produit d’évaluation gratuite de hello. S’il s’agissait, vous serait tooname demandées hello abonnement, comme indiqué dans hello l’exemple suivant.
> 
> 

![Ajouter un abonnement][api-management-add-subscription-multiple]

Après avoir cliqué sur **s’abonner**, produit de hello apparaît dans hello **abonnement** liste pour l’utilisateur de hello.

![Abonnement ajouté][api-management-subscription-added]

## <a name="test-rate-limit"></a>toocall une limite de fréquence hello opération et de test
Maintenant hello produit de la version d’évaluation gratuite est configuré et publié, nous permet appeler certaines opérations et de tester la stratégie de limite de taux hello.
Portail des développeurs commutateur toohello en cliquant sur **portail des développeurs** dans le menu supérieur droit de hello.

![Portail des développeurs][api-management-developer-portal-menu]

Cliquez sur **API** dans hello menu supérieur, puis cliquez sur **Echo API**.

![Portail des développeurs][api-management-developer-portal-api-menu]

Cliquez sur **Ressource GET**, puis sur **Essayez-le**.

![Open console][api-management-open-console]

Conserver les valeurs de paramètre par défaut de hello et sélectionnez votre clé d’abonnement pour le produit d’évaluation gratuite de hello.

![Clé d’abonnement][api-management-select-key]

> [!NOTE]
> Si vous avez plusieurs abonnements, être Vérifiez que la touche tooselect hello pour **version d’évaluation gratuite**, ou autre stratégies hello qui ont été configurés dans les étapes précédentes hello ne sera pas en vigueur.
> 
> 

Cliquez sur **envoyer**, puis affichez la réponse de hello. Hello de note **état de la réponse** de **200 OK**.

![Operation results][api-management-http-get-results]

Cliquez sur **envoyer** à une fréquence supérieure à la stratégie de limite de taux de hello 10 appels par minute. Une fois la stratégie de limite de taux de hello est dépassée, un état de réponse de **429 trop grand nombre de demandes** est retourné.

![Operation results][api-management-http-get-429]

Hello **contenu de la réponse** indique hello restant intervalle avant nouvelle tentative sera établie.

Lors de la stratégie de limite de taux de hello 10 appels par minute, les appels suivants échoueront jusqu'à ce que 60 secondes à partir de hello premier du produit de toohello hello 10 appels réussis avant que la limite du taux de hello a été dépassé. Dans cet exemple, hello restant intervalle est 54 secondes.

## <a name="next-steps"></a>Étapes suivantes
* Regarder une démonstration de la définition de quotas et limites de taux Bonjour suivant vidéo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
