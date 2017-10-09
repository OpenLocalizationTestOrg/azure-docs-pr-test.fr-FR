---
title: "propriétés de toouse aaaHow dans les stratégies de gestion des API Azure"
description: "Découvrez comment les propriétés de toouse dans les stratégies de gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a>Comment les propriétés de toouse dans les stratégies de gestion des API Azure
Stratégies de gestion des API constituent une puissante capacité du système hello autoriser la publication de hello toochange hello du comportement de hello API via la configuration. Les stratégies sont une collection d’instructions qui sont exécutées séquentiellement sur la demande de hello ou de réponse d’une API. Les instructions de la stratégie peuvent être construites à l’aide de valeurs de texte littéral, d’expressions de stratégie et de propriétés. 

Chaque instance de service de gestion des API possède une collection de propriétés de paires clé/valeur qui sont globales toohello l’instance de service. Ces propriétés peuvent être des valeurs de chaîne constante toomanage utilisé sur toutes les stratégies et de configuration de l’API. Chaque propriété a hello suivant des attributs.

| Attribut | Type | Description |
| --- | --- | --- |
| Name |string |nom de Hello de propriété de hello. Il peut contenir uniquement des lettres, des chiffres, des points, des tirets et des caractères de soulignement. |
| Valeur |string |valeur de propriété de hello de Hello. Elle ne peut pas être vide ni se composer uniquement d’espaces blancs. |
| Secret |booléenne |Détermine si la valeur de hello est une clé secrète et doit être chiffrée ou non. |
| Tags |tableau de chaînes |Facultatif les balises qui fourni peut être utilisé toofilter hello propriété liste. |

Propriétés sont configurées dans le portail de publication hello sur hello **propriétés** onglet. Bonjour l’exemple suivant, trois propriétés sont configurées.

![Propriétés][api-management-properties]

Les valeurs de propriété peuvent contenir des chaînes littérales et des [expressions de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx). Hello tableau suivant montre hello précédente trois exemples de propriétés et leurs attributs. Hello valeur `ExpressionProperty` est une expression de stratégie qui retourne une chaîne contenant hello date et heure actuelles. Hello propriété `ContosoHeaderValue` est marquée en tant que secret, donc sa valeur n’est pas affichée.

| Nom | Valeur | Secret | Balises |
| --- | --- | --- | --- |
| ContosoHeader |TrackingId |False |Contoso |
| ContosoHeaderValue |•••••••••••••••••••••• |True |Contoso |
| ExpressionProperty |@(DateHeure.Now.ToString()) |False | |

## <a name="toouse-a-property"></a>toouse une propriété
nom de la propriété hello sur place à l’intérieur d’une double paire d’accolades de toouse une propriété dans une stratégie, comme `{{ContosoHeader}}`, comme indiqué dans hello l’exemple suivant.

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

Dans cet exemple, `ContosoHeader` est utilisé comme nom hello d’un en-tête dans un `set-header` stratégie, et `ContosoHeaderValue` est utilisé en tant que valeur hello de cet en-tête. Lorsque cette stratégie est évaluée au cours d’une demande ou réponse toohello API passerelle de gestion, `{{ContosoHeader}}` et `{{ContosoHeaderValue}}` sont remplacés par leurs valeurs de propriété respectives.

Propriétés qui peuvent être utilisées en tant qu’attribut complète ou de valeurs d’élément comme indiqué dans l’exemple précédent de hello, mais peut également être insérés dans ou combinés avec partie d’une expression de texte littéral, comme indiqué dans hello l’exemple suivant :`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`

Les propriétés peuvent également contenir des expressions de stratégie. Dans l’exemple suivant de hello, hello `ExpressionProperty` est utilisé.

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

Lorsque cette stratégie est évaluée, `{{ExpressionProperty}}` est remplacé par sa valeur : `@(DateTime.Now.ToString())`. Étant donné que la valeur de hello est une expression de stratégie, hello expression est évaluée et la stratégie de hello se poursuit son exécution.

Vous pouvez tester ce point dans le portail des développeurs hello en appelant une opération qui a une stratégie avec des propriétés dans la portée. Bonjour l’exemple suivant, une opération est appelée avec l’exemple précédent de hello deux `set-header` stratégies avec des propriétés. Notez que les réponse hello contient deux en-têtes personnalisés qui ont été configurés à l’aide de stratégies avec des propriétés.

![Portail des développeurs][api-management-send-results]

Si vous examinez hello [trace de l’inspecteur de l’API](api-management-howto-api-inspector.md) pour un appel qui inclut les hello deux stratégies exemple précédente avec les propriétés, vous pouvez voir hello deux `set-header` stratégies avec les valeurs de propriété hello insérées, ainsi que l’expression de stratégie hello évaluation de propriété hello contenant une expression de stratégie hello.

![Suivi de l’inspecteur d’API][api-management-api-inspector-trace]

Alors que les valeurs de propriété peuvent contenir des expressions de stratégie, elles ne peuvent pas contenir d’autres propriétés. Si le texte qui contient une référence de propriété est utilisée pour une valeur de propriété, telles que `Property value text {{MyProperty}}`, que la référence de propriété ne sera pas remplacé et sera inclus dans le cadre de la valeur de la propriété hello.

## <a name="toocreate-a-property"></a>toocreate une propriété
toocreate une propriété, cliquez sur **Ajouter propriété** sur hello **propriétés** onglet.

![Ajouter une propriété][api-management-properties-add-property-menu]

**Nom** et **Valeur** doivent être renseignés. Si cette valeur de propriété est une clé secrète, vérifiez hello **il s’agit d’une clé secrète** case à cocher. Entrez un ou plusieurs toohelp balises facultatif en organisant les propriétés, puis cliquez sur **enregistrer**.

![Ajouter une propriété][api-management-properties-add-property]

Lorsqu’une nouvelle propriété est enregistrée, hello **propriétés de recherche** textbox est remplie avec le nom de hello de hello nouvelle propriété et la nouvelle propriété de hello s’affiche. Désactivez de toutes les propriétés, toodisplay hello **propriétés de recherche** zone de texte et appuyez sur ENTRÉE.

![Propriétés][api-management-properties-property-saved]

Pour plus d’informations sur la création d’une propriété à l’aide de hello API REST, consultez [créer une propriété à l’aide des API REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).

## <a name="tooedit-a-property"></a>tooedit une propriété
tooedit une propriété, cliquez sur **modifier** en regard de tooedit de propriété hello.

![Modifier la propriété][api-management-properties-edit]

Apportez les modifications souhaitées, puis cliquez sur **Enregistrer**. Si vous modifiez le nom de la propriété hello, toutes les stratégies qui font référence à cette propriété sont nouveau nom de hello toouse mises à jour automatiquement.

![Modifier la propriété][api-management-properties-edit-property]

Pour plus d’informations sur la modification d’une propriété à l’aide de hello API REST, consultez [modifier une propriété à l’aide des API REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).

## <a name="toodelete-a-property"></a>toodelete une propriété
toodelete une propriété, cliquez sur **supprimer** en regard de toodelete de propriété hello.

![Supprimer la propriété][api-management-properties-delete]

Cliquez sur **Oui, supprimez-le** tooconfirm.

![Confirmation de suppression][api-management-delete-confirm]

> [!IMPORTANT]
> Si la propriété de hello est référencée par les stratégies, vous ne pouvez pas toosuccessfully supprimer jusqu'à la suppression de la propriété de hello de toutes les stratégies qui l’utilisent.
> 
> 

Pour plus d’informations sur la suppression d’une propriété à l’aide de hello API REST, consultez [supprimer une propriété à l’aide des API REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).

## <a name="toosearch-and-filter-properties"></a>propriétés toosearch et filtre
Hello **propriétés** onglet inclut la recherche et filtrage toohelp fonctionnalités vous gérez vos propriétés. liste de propriétés toofilter hello par nom de propriété, entrez un terme à rechercher dans hello **propriétés de recherche** zone de texte. Désactivez de toutes les propriétés, toodisplay hello **propriétés de recherche** zone de texte et appuyez sur ENTRÉE.

![Search][api-management-properties-search]

liste de propriétés hello toofilter par des valeurs de balise, entrez une ou plusieurs balises dans hello **filtre par des balises** zone de texte. Désactivez de toutes les propriétés, toodisplay hello **filtre par des balises** zone de texte et appuyez sur ENTRÉE.

![Filtrer][api-management-properties-filter]

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur l’utilisation des stratégies
  * [Stratégies dans Gestion des API](api-management-howto-policies.md)
  * [Référence de stratégie](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [Expressions de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a>Regarder une vidéo de présentation
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

