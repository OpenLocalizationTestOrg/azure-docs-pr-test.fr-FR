---
title: "Pouvez-vous nous présenter le service Microsoft Power BI Embedded ?"
description: "Power BI Embedded vous permet d’intégrer des rapports Power BI dans vos applications web ou mobiles. Vous n’avez donc pas besoin de créer des solutions personnalisées."
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
ms.openlocfilehash: 0b5f7a2c3fd16ac32b0bc382616ca6600d378bb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>Pouvez-vous nous présenter le service Microsoft Power BI Embedded ?
Avec **Power BI Embedded**, vous pouvez intégrer des rapports Power BI dans vos applications web ou mobiles.

![](media/powerbi-embedded-whats-is/what-is.png)

**Power BI Embedded** est un service Azure qui permet aux éditeurs de logiciels indépendants (ISV) et aux développeurs d’applications de proposer des expériences de données Power BI au sein de leurs applications. En tant que développeur, vous avez créé des applications, et ces applications disposent de leurs propres utilisateurs et d’un ensemble distinct de fonctionnalités. Ces applications peuvent également contenir des éléments de données intégrés, tels que des graphiques et des rapports, qui peuvent désormais être fournis par Microsoft Power BI Embedded. Vous n'avez pas besoin de compte Power BI pour utiliser votre application. Vous pouvez continuer à vous connecter à votre application comme avant, et afficher et interagir avec la création de rapports de Power BI sans nécessiter de licence supplémentaire.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Gestion des licences pour Microsoft Power BI Embedded
Dans le modèle d’utilisation **Microsoft Power BI Embedded** , la gestion des licences Power BI n’est pas la responsabilité de l’utilisateur final.  Au lieu de cela, les **sessions** sont achetées par le développeur de l’application qui consomme les effets visuels et ils sont facturés à l’abonnement propriétaire de ces ressources. Pour plus d’informations, consultez la page [Tarification](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Modèle conceptuel de Microsoft Power BI Embedded

![](media/powerbi-embedded-whats-is/model.png)

Comme pour tout autre service dans Azure, les ressources de Power BI Embedded sont approvisionnées via les [API Azure Resource Manager](https://msdn.microsoft.com/library/mt712306.aspx). Dans ce cas, la ressource approvisionnée constitue une **collection d’espaces de travail Power BI**.

## <a name="workspace-collection"></a>Collection d’espaces de travail
Une **collection d’espaces de travail** est le conteneur Azure de plus haut niveau pour les ressources contenant 0 **espaces de travail**.  Une **collection** **d’espaces de travail** dispose de toutes les propriétés Azure standard, ainsi que des éléments suivants:

* **Clés d’accès** : clés utilisées lors de l’appel sécurisé aux API de Power BI (fonction décrite dans une section ultérieure).
* **Utilisateurs** : les utilisateurs Azure Active Directory (AAD) qui ont des droits d’administrateur pour gérer la collection d’espaces de travail Power BI via le portail Azure ou l’API Azure Resource Manager.
* **Région** : dans le cadre de l’approvisionnement d’une **collection d’espaces de travail**, vous pouvez sélectionner une région pour l’approvisionnement. Pour plus d’informations, consultez l’article [Régions Azure](https://azure.microsoft.com/regions/).

## <a name="workspace"></a>Espace de travail
Un **espace de travail** est un conteneur de contenu Power BI, qui peut inclure des jeux de données et des rapports. Lors de sa création initiale, un **espace de travail** est vide. Vous allez créer du contenu avec Power BI Desktop et déployer par programmation le PBIX sur votre espace de travail avec les [API Power BI Import](https://msdn.microsoft.com/library/mt711504.aspx). Vous pouvez également créer votre jeu de données par programme, puis créer des rapports au sein de votre application au lieu d’utiliser Power BI Desktop.

## <a name="using-workspace-collections-and-workspaces"></a>Utiliser des collections d’espaces de travail et des espaces de travail
Les **collections d’espaces de travail** et les **espaces de travail** sont des conteneurs de contenu qui sont utilisés et organisés de la façon la plus adaptée à la conception de l’application que vous créez. Vous pouvez en organiser le contenu de plusieurs façons. Vous pouvez choisir de placer tout le contenu dans un seul espace de travail, puis d’utiliser des jetons d’application pour subdiviser le contenu entre vos clients. Vous pouvez également choisir de placer tous vos clients dans des espaces de travail distincts afin de les séparer. Ou, vous pouvez choisir d’organiser les utilisateurs par région, et non par client. Cette conception flexible vous permet de choisir la meilleure façon d’organiser le contenu.

## <a name="cached-datasets"></a>Jeux de données mis en cache
Il est possible d’utiliser des jeux de données mis en cache.  Cependant, vous ne pouvez pas actualiser les données mises en cache une fois qu’elles ont été chargées dans **Microsoft Power BI Embedded**. Un jeu de données mis en cache signifie que vous avez importé les données dans Power BI Desktop au lieu d’utiliser DirectQuery.

## <a name="authentication-and-authorization-with-app-tokens"></a>Authentification et autorisation avec des jetons d’application
**Microsoft Power BI Embedded** s’appuie sur votre application pour l’autorisation et l’authentification requises des utilisateurs. Vos utilisateurs finaux ne doivent pas nécessairement être des clients Azure Active Directory (Azure AD).  Au lieu de cela, votre application donne à **Microsoft Power BI Embedded** l’autorisation d’afficher un rapport Power BI en utilisant des **jetons d’authentification d’application (jetons d’application)**.  Ces **jetons d’application** sont créés en fonction des besoins lorsque votre application veut afficher un rapport.

![](media/powerbi-embedded-whats-is/app-tokens.png)

Les **jetons d’authentification d’application (jetons d’application)** sont utilisés pour l’authentification auprès de **Microsoft Power BI Embedded**.  Il existe trois types de **jetons d’application**:

1. Jetons d’approvisionnement : utilisés lors de l’approvisionnement d’un nouvel **espace de travail** dans une **collection d’espaces de travail**
2. Jetons de développement : utilisés lors des appels directs aux **API REST de Power BI**
3. Jetons d’incorporation : utilisés lors d’appels servant à afficher un rapport dans l’iframe incorporé

Ces jetons sont utilisés pour les différentes phases de vos interactions avec **Microsoft Power BI Embedded**.  Les jetons sont conçus de sorte que vous pouvez déléguer des autorisations de votre application à Power BI. Pour plus d’informations, consultez [Flux de jetons d’application](power-bi-embedded-app-token-flow.md).

## <a name="create-or-edit-reports-within-your-application"></a>Créer ou modifier des rapports dans l’application

Vous pouvez maintenant modifier des rapports existants ou créer des rapports directement dans votre application sans avoir à utiliser Power BI Desktop. Cela requiert l’existence d’un jeu de données au sein de votre espace de travail.

## <a name="see-also"></a>Voir aussi

[Scénarios Microsoft Power BI Embedded courants](power-bi-embedded-scenarios.md)  
[Prise en main de Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Prise en main de l’exemple](power-bi-embedded-get-started-sample.md)  
[Incorporer un rapport](power-bi-embedded-embed-report.md)  
[Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Exemple d’incorporation JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Référentiel Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Référentiel Git PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
Des questions ? [Essayer la communauté Power BI](http://community.powerbi.com/)
