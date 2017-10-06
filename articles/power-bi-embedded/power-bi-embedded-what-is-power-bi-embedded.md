---
title: "aaaWhat est Microsoft Power BI Embedded ?"
description: "Power BI Embedded vous permet des rapports Power BI toointegrate dans vos applications web ou mobiles vous n’avez pas besoin de toobuild des solutions personnalisées."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 03649b72-b7d7-40ca-b077-12356d72d4f3
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/20/2017
ms.author: asaxton
ms.openlocfilehash: 0353938b6cdd9bb58b123b250f45f76b8cc7abe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>Pouvez-vous nous présenter le service Microsoft Power BI Embedded ?
Avec **Power BI Embedded**, vous pouvez intégrer des rapports Power BI dans vos applications web ou mobiles.

![](media/powerbi-embedded-whats-is/what-is.png)

Power BI Embedded est une **service Azure** qui permet des éditeurs de logiciels indépendants et les expériences d’application aux développeurs toosurface données Power BI dans leurs applications. En tant que développeur, vous avez créé des applications, et ces applications disposent de leurs propres utilisateurs et d’un ensemble distinct de fonctionnalités. Ces applications peuvent également arriver toohave certains éléments de données intégrés comme des graphiques et rapports peuvent maintenant être éteints par Microsoft Power BI Embedded. Vous n’avez pas besoin une toouse de compte Power BI votre application. Vous pouvez continuer toosign dans l’application, tooyour exactement comme avant et afficher et interagir avec hello expérience de création de rapports Power BI sans nécessiter des licences supplémentaires.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Gestion des licences pour Microsoft Power BI Embedded
Bonjour **Microsoft Power BI Embedded** modèle d’utilisation, le Gestionnaire de licences pour Power BI n’est pas responsable de hello de l’utilisateur final hello.  Au lieu de cela, **sessions** achetés par le développeur de hello d’application hello qui consomme des éléments visuels hello et sont facturés toohello abonnement qui possède ces ressources. Vous trouverez des informations supplémentaires sur hello [page de tarification](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Modèle conceptuel de Microsoft Power BI Embedded

![](media/powerbi-embedded-whats-is/model.png)

Comme tout autre service dans Azure, les ressources pour Power BI Embedded sont approvisionnés via hello [API du Gestionnaire de ressources Azure](https://msdn.microsoft.com/library/mt712306.aspx). Dans ce cas, les ressources hello que vous préparez est un **collecte d’espace de travail Power BI**.

## <a name="workspace-collection"></a>Collection d’espaces de travail
A **Collection de l’espace de travail** est hello Azure conteneur de niveau supérieur pour les ressources qui contient 0 ou plus **espaces de travail**.  A **espace de travail** **Collection** dispose de toutes les propriétés Azure de hello standard, ainsi que les suivantes de hello :

* **Clés d’accès** – utilisés lors de l’appel de manière sécurisée les clés hello API de Power BI (décrite dans une section ultérieure).
* **Les utilisateurs** – les utilisateurs Azure Active Directory (AAD) qui ont toomanage de droits d’administrateur hello collecte d’espace de travail Power BI via hello portail Azure ou des API Azure Resource Manager.
* **Région** et dans le cadre de la mise en service un **Collection de l’espace de travail**, vous pouvez sélectionner un toobe région configuré dans. Pour plus d’informations, consultez l’article [Régions Azure](https://azure.microsoft.com/regions/).

## <a name="workspace"></a>Espace de travail
Un **espace de travail** est un conteneur de contenu Power BI, qui peut inclure des jeux de données et des rapports. Lors de sa création initiale, un **espace de travail** est vide. Vous allez créer du contenu à l’aide de Power BI Desktop et que vous déploierez par programme hello PBIX dans votre espace de travail à l’aide de hello [API de Power BI importation](https://msdn.microsoft.com/library/mt711504.aspx). Vous pouvez également créer votre jeu de données par programme, puis créer des rapports au sein de votre application au lieu d’utiliser Power BI Desktop.

## <a name="using-workspace-collections-and-workspaces"></a>Utiliser des collections d’espaces de travail et des espaces de travail
**Collections de l’espace de travail** et **espaces de travail** sont des conteneurs de contenu qui sont utilisées et organisées dans conception hello d’application hello vous générez le mieux à quelle que soit la façon la plus adaptée. Il y a différentes manières que vous pourriez organiser le contenu hello. Vous pouvez choisir tooput tout contenu dans un espace de travail, et ensuite ultérieure utilisez application jetons toofurther subdiviser contenu hello dans la liste de vos clients. Vous pouvez également choisir tooput tous vos clients dans les espaces de travail distincts afin qu’il existe une séparation entre eux. Ou bien, vous pouvez choisir les utilisateurs tooorganize par région plutôt que par le client. Cette conception flexible vous permet de toochoose hello meilleure manière tooorganize contenu.

## <a name="cached-datasets"></a>Jeux de données mis en cache
Il est possible d’utiliser des jeux de données mis en cache.  Cependant, vous ne pouvez pas actualiser les données mises en cache une fois qu’elles ont été chargées dans **Microsoft Power BI Embedded**. Un dataset mis en cache signifie que vous avez importé des données de hello dans Power BI Desktop au lieu d’utiliser DirectQuery.

## <a name="authentication-and-authorization-with-app-tokens"></a>Authentification et autorisation avec des jetons d’application
**Microsoft Power BI Embedded** diffère tooyour application tooperform tous l’authentification utilisateur nécessaires hello et autorisation. Vos utilisateurs finaux ne doivent pas nécessairement être des clients Azure Active Directory (Azure AD).  Au lieu de cela, votre application exprime trop**Microsoft Power BI Embedded** d’autorisation toorender un rapport Power BI à l’aide de **jetons d’authentification Application (application jetons)**.  Ces **application jetons** sont créés en fonction des besoins lorsque votre application veut toorender un rapport.

![](media/powerbi-embedded-whats-is/app-tokens.png)

**Les jetons d’authentification application (application jetons)** sont utilisé tooauthenticate contre **Microsoft Power BI Embedded**.  Il existe trois types de **jetons d’application**:

1. Jetons d’approvisionnement : utilisés lors de l’approvisionnement d’un nouvel **espace de travail** dans une **collection d’espaces de travail**
2. Les jetons de développement - utilisés pour appeler directement toohello **API REST de Power BI**
3. Incorporation des jetons - utilisés lors d’appels toorender un rapport Bonjour incorporé iframe

Ces jetons sont utilisés pour hello différentes phases de vos interactions avec **Microsoft Power BI Embedded**.  les jetons de Hello sont conçus afin que vous pouvez déléguer des autorisations à partir de votre application de tooPower BI. Pour plus d’informations, consultez [Flux de jetons d’application](power-bi-embedded-app-token-flow.md).

## <a name="create-or-edit-reports-within-your-application"></a>Créer ou modifier des rapports dans l’application

Vous pouvez maintenant modifier existe rapports ou créer des rapports directement dans votre application sans avoir toouse Power BI Desktop. Cela requiert l’existence d’un jeu de données au sein de votre espace de travail.

## <a name="see-also"></a>Voir aussi

[Scénarios Microsoft Power BI Embedded courants](power-bi-embedded-scenarios.md)  
[Prise en main de Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Prise en main de l’exemple](power-bi-embedded-get-started-sample.md)  
[Incorporer un rapport](power-bi-embedded-embed-report.md)  
[Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Exemple d’incorporation JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Référentiel Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Référentiel Git PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
Des questions ? [Essayez de hello Communauté Power BI](http://community.powerbi.com/)
