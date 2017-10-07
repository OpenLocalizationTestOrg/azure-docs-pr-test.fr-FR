---
title: "portail des développeurs gestion des API hello aaaCustomize à l’aide de modèles-Azure | Documents Microsoft"
description: "Découvrez comment toocustomize hello portail des développeurs gestion des API Azure à l’aide de modèles."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: a195675b-f7d0-4fc9-90bf-860e6f17ccf7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: b00d5f1534e9466f30ff3920e7aae048feb8b8c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-hello-azure-api-management-developer-portal-using-templates"></a>Comment toocustomize hello portail des développeurs gestion des API Azure à l’aide de modèles

Il existe trois méthodes fondamentales toocustomize hello portail destiné aux développeurs dans Gestion des API Azure :

* [Modifier le contenu de hello de pages statiques et des éléments de mise en page][modify-content-layout]
* [Mettre à jour les styles de hello utilisés pour les éléments de la page sur le portail des développeurs hello][customize-styles]
* [Modifier les modèles hello utilisés pour les pages générées par le portail de hello] [ portal-templates] (présentés dans ce guide)

Les modèles sont hello toocustomize utilisé le contenu des pages du portail généré par le système de développement (par exemple, documents de l’API, produits, l’authentification des utilisateurs, etc.). À l’aide de [DotLiquid](http://dotliquidmarkup.org/) syntaxe et un ensemble fourni de ressources de chaîne localisée, les icônes et les contrôles de page, vous avez une grande souplesse tooconfigure hello contenu hello pages comme vous le souhaitez.

## <a name="developer-portal-templates-overview"></a>Vue d’ensemble des modèles du portail des développeurs
Modification des modèles est effectuée à partir de hello **portail des développeurs** tout en étant connecté en tant qu’administrateur. tooget il tout d’abord ouvrir hello portail Azure et cliquez sur **portail de publication** à partir de la barre d’outils du service hello de votre instance de la gestion des API.

![Portail des éditeurs][api-management-management-console]

Cliquez ensuite sur **portail des développeurs** sur hello en haut à droite. 

![Menu du portail des développeurs][api-management-developer-portal-menu]

tooaccess hello modèles portail des développeurs, cliquez sur hello personnaliser l’icône dans le menu de personnalisation hello hello toodisplay gauche, puis cliquez sur **modèles**.

![Modèles du portail des développeurs][api-management-customize-menu]

liste de modèles Hello affiche plusieurs catégories de modèles couvrant hello différentes pages de portail des développeurs hello. Chaque modèle est différent, mais hello étapes tooedit les et publier les modifications de hello sont hello identiques. tooedit un modèle, cliquez sur nom hello du modèle de hello.

![Modèles du portail des développeurs][api-management-templates-menu]

En cliquant sur un modèle vous amène page portail toohello développeur qui est personnalisable par ce modèle. Dans cette hello exemple **liste de produits** modèle s’affiche. Hello **liste de produits** contrôles de modèle hello d’écran hello indiqué par le rectangle de hello rouge. 

![Modèle Products list (Liste de produits)][api-management-developer-portal-templates-overview]

Certains modèles, comme hello **profil utilisateur** modèles, personnaliser les différentes parties de hello même page. 

![Modèles User profile (Profil utilisateur)][api-management-user-profile-templates]

éditeur de Hello pour chaque modèle de portail de développement a deux sections sont affichées en bas de hello de page de hello. partie gauche Hello affiche hello modification du volet de modèle de hello et droite hello affiche le modèle de données hello pour le modèle de hello. 

modèle Hello modification volet contient le balisage de hello qui contrôle l’apparence de hello et le comportement de la page correspondante de hello dans le portail des développeurs hello. balisage Hello dans le modèle de hello utilise hello [DotLiquid](http://dotliquidmarkup.org/) syntaxe. Pour DotLiquid, il existe un éditeur assez répandu : [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers). N’importe quel modèle de toohello des modifications apportées lors de la modification sont affichés dans en temps réel dans le navigateur de hello, mais sont les clients tooyour n’est pas visible jusqu'à ce que vous [enregistrer](#to-save-a-template) et [publier](#to-publish-a-template) modèle de hello.

![Balisage de modèle][api-management-template]

Hello **les données de modèle** volet fournit un guide toohello données pour les entités hello qui sont disponibles pour une utilisation dans un modèle particulier. Il fournit ce guide en affichant les données actives hello qui sont actuellement affichées dans le portail des développeurs hello. Vous pouvez développer les volets de modèle de hello en cliquant sur le rectangle hello dans le coin supérieur droit de hello Hello **les données de modèle** volet.

![Modèle de données du modèle][api-management-template-data]

Dans l’exemple précédent de hello, il existe deux produits affichés dans le portail des développeurs hello qui ont été récupérées à partir des données hello affichées dans hello **les données de modèle** volet, comme indiqué dans hello l’exemple suivant.

```json
{
    "Paging": {
        "Page": 1,
        "PageSize": 10,
        "TotalItemCount": 2,
        "ShowAll": false,
        "PageCount": 1
    },
    "Filtering": {
        "Pattern": null,
        "Placeholder": "Search products"
    },
    "Products": [
        {
            "Id": "56ec64c380ed850042060001",
            "Title": "Starter",
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",
            "Terms": "",
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        },
        {
            "Id": "56ec64c380ed850042060002",
            "Title": "Unlimited",
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",
            "Terms": null,
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        }
    ]
}
```

balisage Hello Bonjour **liste de produits** processus du modèle hello la sortie de données tooprovide hello souhaitée en effectuant une itération via la collection hello des informations sur les produits toodisplay et un produit individuel tooeach de lien. Hello de note `<search-control>` et `<page-control>` les éléments dans le balisage de hello. Ils contrôlent l’affichage hello Hello recherche et la pagination des contrôles sur la page de hello. `ProductsStrings|PageTitleProducts`est une référence de chaîne localisée contenant hello `h2` texte d’en-tête de page de hello. Pour obtenir la liste des ressources de chaîne, des contrôles de page et des icônes à utiliser dans les modèles du portail des développeurs, consultez les [informations de référence sur les modèles du portail des développeurs Gestion des API](api-management-developer-portal-templates-reference.md).

```html
<search-control></search-control>
<div class="row">
    <div class="col-md-9">
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>
    </div>
</div>
<div class="row">
    <div class="col-md-12">
    {% if products.size > 0 %}
    <ul class="list-unstyled">
    {% for product in products %}
        <li>
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>
            {{product.description}}
        </li>    
    {% endfor %}
    </ul>
    <paging-control></paging-control>
    {% else %}
    {% localized "CommonResources|NoItemsToDisplay" %}
    {% endif %}
    </div>
</div>
```

## <a name="toosave-a-template"></a>toosave un modèle
toosave un modèle, cliquez sur Enregistrer dans l’éditeur de modèle hello.

![Enregistrer un modèle][api-management-save-template]

Les modifications enregistrées ne sont pas actifs dans le portail des développeurs hello jusqu'à ce qu’ils sont publiés.

## <a name="toopublish-a-template"></a>toopublish un modèle
Les modèles enregistrés peuvent être publiés individuellement ou en bloc. toopublish un modèle particulier, cliquez sur Publier dans l’éditeur de modèle hello.

![Publier un modèle][api-management-publish-template]

Cliquez sur **Oui** tooconfirm et modèle hello en direct sur le portail des développeurs hello.

![Confirmer une publication][api-management-publish-template-confirm]

toopublish publiés toutes les versions de modèle, cliquez sur **publier** dans la liste de modèles hello. Modèles non publiés sont désignées par un astérisque après le nom du modèle hello. Dans cet exemple, hello **liste de produits** et **produit** modèles sont publiés.

![Publier des modèles][api-management-publish-templates]

Cliquez sur **publier les personnalisations** tooconfirm.

![Confirmer une publication][api-management-publish-customizations]

Les modèles publiés récemment sont efficaces immédiatement dans le portail des développeurs hello.

## <a name="toorevert-a-template-toohello-previous-version"></a>toorevert une version précédente du modèle toohello
toorevert modèle toohello précédente version publiée, cliquez sur Rétablir dans l’éditeur de modèle hello.

![Rétablir un modèle][api-management-revert-template]

Cliquez sur **Oui** tooconfirm.

![Confirmer][api-management-revert-template-confirm]

Hello précédemment la version publiée d’un modèle est live dans le portail des développeurs hello une fois hello annuler l’opération est terminée.

## <a name="toorestore-a-template-toohello-default-version"></a>toorestore une version par défaut du modèle de toohello
Version par défaut de tootheir restauration modèles est un processus en deux étapes. Les modèles hello première doivent être restaurées, et ensuite les versions hello restauré doivent être publiées.

toorestore une version par défaut de toohello modèle unique cliquez sur Restaurer dans l’éditeur de modèle hello.

![Rétablir un modèle][api-management-reset-template]

Cliquez sur **Oui** tooconfirm.

![Confirmer][api-management-reset-template-confirm]

Cliquez sur les versions par défaut tous les modèles tootheir, toorestore **restaurer les modèles par défaut** sur la liste des modèles hello.

![Restaurer des modèles][api-management-restore-templates]

Hello modèles restaurées doivent ensuite être publiés individuellement ou tous en même temps en suivant les étapes de hello dans [toopublish un modèle](#to-publish-a-template).

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations de référence sur les modèles du portail des développeurs, les ressources de chaîne, les icônes et les contrôles de page, consultez les [informations de référence sur les modèles du portail des développeurs Gestion des API](api-management-developer-portal-templates-reference.md).

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customize-menu]: ./media/api-management-developer-portal-templates/api-management-customize-menu.png
[api-management-templates-menu]: ./media/api-management-developer-portal-templates/api-management-templates-menu.png
[api-management-developer-portal-templates-overview]: ./media/api-management-developer-portal-templates/api-management-developer-portal-templates-overview.png
[api-management-template]: ./media/api-management-developer-portal-templates/api-management-template.png
[api-management-template-data]: ./media/api-management-developer-portal-templates/api-management-template-data.png
[api-management-developer-portal-menu]: ./media/api-management-developer-portal-templates/api-management-developer-portal-menu.png
[api-management-management-console]: ./media/api-management-developer-portal-templates/api-management-management-console.png
[api-management-browse]: ./media/api-management-developer-portal-templates/api-management-browse.png
[api-management-user-profile-templates]: ./media/api-management-developer-portal-templates/api-management-user-profile-templates.png
[api-management-save-template]: ./media/api-management-developer-portal-templates/api-management-save-template.png
[api-management-publish-template]: ./media/api-management-developer-portal-templates/api-management-publish-template.png
[api-management-publish-template-confirm]: ./media/api-management-developer-portal-templates/api-management-publish-template-confirm.png
[api-management-publish-templates]: ./media/api-management-developer-portal-templates/api-management-publish-templates.png
[api-management-publish-customizations]: ./media/api-management-developer-portal-templates/api-management-publish-customizations.png
[api-management-revert-template]: ./media/api-management-developer-portal-templates/api-management-revert-template.png
[api-management-revert-template-confirm]: ./media/api-management-developer-portal-templates/api-management-revert-template-confirm.png
[api-management-reset-template]: ./media/api-management-developer-portal-templates/api-management-reset-template.png
[api-management-reset-template-confirm]: ./media/api-management-developer-portal-templates/api-management-reset-template-confirm.png
[api-management-restore-templates]: ./media/api-management-developer-portal-templates/api-management-restore-templates.png







