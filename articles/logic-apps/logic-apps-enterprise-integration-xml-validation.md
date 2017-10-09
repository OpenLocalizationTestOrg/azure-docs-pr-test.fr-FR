---
title: aaaValidate XML - Azure Logic Apps | Documents Microsoft
description: "Valider le code XML avec des schémas pour les scénarios Azure Logic Apps et B2B à l’aide de hello Pack d’intégration Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a>Valider des messages XML pour l’intégration d’entreprise

Souvent dans les scénarios B2B, les partenaires hello dans un accord doivent vous assurer qu’ils échangent des messages de type hello sont valides avant que le traitement des données puisse démarrer. Vous pouvez valider des documents par rapport à un schéma prédéfini à l’aide de connecteur de Validation XML hello utilisez hello Bonjour Pack d’intégration Enterprise.

## <a name="validate-a-document-with-hello-xml-validation-connector"></a>Valider un document avec le connecteur de Validation XML hello

1. Créer une application logique, et [lier le compte d’intégration hello application toohello](../logic-apps/logic-apps-enterprise-integration-accounts.md "savoir toolink une application de la logique de l’intégration compte tooa") qui a hello schéma toouse pour la validation des données XML.

2. Ajouter un **demande - HTTP lors de la demande est reçue** application logique de tooyour déclencheur.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. tooadd hello **Validation XML** action, choisissez **ajouter une action**.

4. toofilter tous hello toohello actions une que vous le souhaitez, entrez *xml* dans la zone de recherche hello. Choisissez **Validation XML**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. toospecify hello contenu XML que vous souhaitez toovalidate, sélectionnez **contenu**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. Sélectionnez body est dupliquée hello hello contenu que vous souhaitez toovalidate.

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. toospecify hello schéma toouse pour la validation de hello précédente *contenu* d’entrée, choisissez **nom de schéma**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. Enregistrez votre travail   

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

Vous avez maintenant terminé de configurer votre connecteur de validation. Dans une application réelle, vous pourriez toostore des données de hello validé dans une application de (LOB) de line-of-business comme SalesForce. toosend hello sortie validée tooSalesforce, ajoutez une action.

tootest votre action de validation, rendre un point de terminaison demande toohello HTTP.

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur hello Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")   

