---
title: "aaaInteract avec des rapports à l’aide de hello API JavaScript | Documents Microsoft"
description: "Power BI Embedded, interagir avec les rapports à l’aide de hello API JavaScript"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a>Interagir avec les rapports Power BI à l’aide de hello API JavaScript
Permet d’API de Power BI JavaScript Hello tooeasily vous incorporez des rapports Power BI dans vos applications. Avec l’API de hello, vos applications peuvent interagir par programme avec les différents éléments de rapport comme des pages et des filtres. Cette interactivité intègre les rapports Power BI plus étroitement dans votre application.

Vous incorporez un rapport Power BI dans votre application à l’aide d’un iframe qui est hébergé dans le cadre de l’application hello. Hello iframe agit comme une limite entre votre application et le rapport de hello, comme vous pouvez le voir Bonjour suivant l’image. 

![Iframe Power BI Embedded sans API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

Hello iframe fait hello incorporation processus beaucoup plus facile, mais sans hello d’API JavaScript hello rapport et votre application ne peut pas interagir avec eux. Ce manque d’interaction peut rendre le sentiment rapport de hello ne faisait pas partie de l’application hello. application et les rapports hello réellement besoin toocommunicate dans les deux sens, comme dans hello suivant l’image.

![Iframe Power BI Embedded avec API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

Hello JavaScript API de Power BI vous permet de code toowrite en toute sécurité traverser les limites d’iframe hello. Cela permet tooprogrammatically de votre application réaliser une action dans un rapport et toolisten pour les événements des actions effectuées par les utilisateurs au sein du rapport de hello.

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a>Que pouvez-vous faire avec hello JavaScript API de Power BI ?
Avec hello API JavaScript, vous pouvez gérer des rapports, accédez toopages dans un rapport, filtrer un rapport et gérer l’incorporation des événements. Hello diagramme suivant montre structure hello Hello API.

![Diagramme de l’API JavaScript de Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a>Gérer les rapports
Hello API Javascript vous permet de comportement toomanage au niveau de rapport et de page hello :

* Incorporer un rapport Power BI en toute sécurité dans votre application - essayez de hello [incorporer l’application de démonstration](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)
  * Définir le jeton d’accès
* Configurer les rapports de hello
  * Activer et désactiver le volet de filtre hello et le volet de navigation de page : essayez hello [mettre à jour d’application de démonstration de paramètres](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)
  * Définir les valeurs par défaut des pages et des filtres - essayez de hello [ensemble démo sur les valeurs par défaut](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)
* Afficher et quitter le mode plein écran

[En savoir plus sur l’incorporation d’un rapport](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a>Accédez toopages dans un rapport
Hello API JavaScript enbales vous toodiscover toutes les pages dans un rapport et tooset hello actuel une page. Essayez de hello [application de démonstration de navigation](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).

[En savoir plus sur la navigation entre les pages](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a>Filtrer un rapport
Hello API JavaScript fournit de base et avancés des fonctionnalités pour les rapports intégrés et les pages du rapport de filtre. Essayez de hello [le filtrage d’application de démonstration](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)et passez en revue du code introduction ici.  

#### <a name="basic-filters"></a>Filtres de base
Un filtre de base est placé sur un niveau de la colonne ou de la hiérarchie et contient une liste de valeurs tooinclude ou exclure.

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a>Filtres avancés
Les filtres avancés utilisent l’opérateur logique de hello et ou ou et acceptez les conditions d’une ou deux, chacun avec leur propre opérateur et la valeur. Les conditions prises en charge sont les suivantes :

* Aucun
* LessThan
* LessThanOrEqual
* GreaterThan
* GreaterThanOrEqual
* Contient
* DoesNotContain
* StartsWith
* DoesNotStartWith
* Is
* IsNot
* IsBlank
* IsNotBlank

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[En savoir plus sur le filtrage](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a>Gestion des événements
En outre informations toosending dans hello iframe, votre application peut également recevoir des informations sur hello suivant des événements provenant de hello iframe :

* Embed
  * chargé
  * error
* Rapports
  * pageChanged
  * dataSelected (disponible prochainement)

[En savoir plus sur la gestion des événements](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur hello JavaScript API de Power BI, consultez hello suivant liens :

* [Wiki d’API JavaScript](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [Référence du modèle d’objet](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* Exemples
  * [Angular](http://azure-samples.github.io/powerbi-angular-client)
  * [Ember](https://github.com/Microsoft/powerbi-ember)
* [Démonstration en direct](https://microsoft.github.io/PowerBI-JavaScript/demo/)

