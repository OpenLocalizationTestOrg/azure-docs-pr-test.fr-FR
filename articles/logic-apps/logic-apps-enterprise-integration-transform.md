---
title: "données XML aaaConvert transformations - Azure Logic Apps | Documents Microsoft"
description: "Créer des transformations ou mapps tooconvert des données XML entre les formats dans la logique des applications à l’aide de hello SDK de l’intégration d’entreprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a>Intégration d’entreprise avec les transformations XML
## <a name="overview"></a>Vue d'ensemble
connecteur de transformation Hello Enterprise integration convertit les données d’un format tooanother de format. Par exemple, peut avoir un message entrant qui contient hello date actuelle au format de YearMonthDay hello. Vous pouvez utiliser un toobe de transformation tooreformat hello date au format de MonthDayYear hello.

## <a name="what-does-a-transform-do"></a>Que fait une transformation ?
Une transformation, qui est également appelé un mappage, se compose d’un schéma XML de la Source (hello d’entrée) et un schéma XML de la cible (sortie hello). Vous pouvez utiliser différentes fonctions intégrées toohelp manipuler ou contrôler les données de salutation, y compris les manipulations de chaînes, affectations conditionnelles, des expressions arithmétiques, formateurs d’heure date et même des constructions de bouclage.

## <a name="how-toocreate-a-transform"></a>Comment toocreate une transformation ?
Vous pouvez créer un mappage de transformation/à l’aide de Visual Studio de hello [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas). Lorsque vous avez terminé de créer et de test de transformation de hello, vous téléchargez la transformation que hello dans votre compte d’intégration. 

## <a name="how-toouse-a-transform"></a>Comment toouse une transformation
Après avoir téléchargé le mappage de la transformation hello dans votre compte d’intégration, vous pouvez l’utiliser toocreate une application logique. application de la logique de Hello exécute vos transformations chaque fois que l’application logique de hello est déclenchée (et il est contenu d’entrée toobe transformé).

**Voici hello étapes toouse une transformation**:

### <a name="prerequisites"></a>Composants requis

* Créer un compte d’intégration et d’ajouter un mappage tooit  

Maintenant que vous avez pris en charge conditions préalables de hello, il est temps toocreate votre application logique :  

1. Créer une application de la logique et [lier le compte d’intégration tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md "savoir toolink une application de la logique de l’intégration compte tooa") qui contient le mappage de hello.
2. Ajouter un **demande** application logique de tooyour déclencheur  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. Ajouter hello **transformer le XML** action en sélectionnant **ajouter une action**   
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. Entrez le mot hello *transformer* dans toofilter de zone de recherche hello tous hello toohello actions une que vous souhaitez toouse  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. Sélectionnez hello **transformer le XML** action   
6. Ajouter hello XML **contenu** qui vous transformez. Vous pouvez utiliser toutes les données XML que vous recevez dans la demande de hello HTTP en tant que hello **contenu**. Dans cet exemple, sélectionnez hello le corps de demande HTTP hello qui a déclenché application logique de hello.
7. Nom hello sélectionnez Hello **carte** que vous souhaitez transformation de hello toouse tooperform. mappage de Hello doit déjà exister dans votre compte d’intégration. Dans une étape précédente, vous avez déjà donné votre logique application tooyour intégration compte d’accès qui contient votre mappage.      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. Enregistrez votre travail   
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

À ce stade, vous avez terminé de configurer votre mappage. Dans une application réelle, vous pouvez vouloir toostore les données de salutation transformée dans une application métier telles que SalesForce. Vous pouvez facilement en tant que sortie action toosend hello hello transformer tooSalesforce. 

Vous pouvez maintenant tester votre fichier de transformation en effectuant un point de terminaison demande toohello HTTP.  

## <a name="features-and-use-cases"></a>Fonctionnalités et cas d’usage
* transformation Hello créée dans un mappage peut être simple, telles que la copie d’un nom et une adresse à partir d’un document tooanother. Ou bien, vous pouvez créer des transformations plus complexes à l’aide des opérations de mappage de l’emploi de hello.  
* Plusieurs fonctions ou opérations de mappage sont disponibles, y compris des chaînes, des fonctions de date et d'heure, et ainsi de suite.  
* Vous pouvez effectuer une copie de données directe entre les schémas hello. Bonjour que Mappeur inclus dans hello SDK, il s’agit aussi simple que le dessin d’une ligne qui connecte les éléments hello dans le schéma de source de hello avec leurs équivalents dans le schéma de destination hello.  
* Lorsque vous créez un mappage, vous permet d’afficher une représentation graphique de la carte de hello, qui affiche toutes les relations hello et les liens que vous créez.
* Utilisez hello Test Map fonctionnalité tooadd un exemple de message XML. D’un simple clic, vous pouvez tester la carte hello que vous avez créé et consultez la sortie de hello généré.  
* Téléchargement de mappages existants  
* Prend en charge pour le format XML hello.

## <a name="learn-more"></a>En savoir plus
* [En savoir plus sur hello Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")  
* [En savoir plus sur les mappages](../logic-apps/logic-apps-enterprise-integration-maps.md "Découvrez les mappages d’intégration d’entreprise")  

