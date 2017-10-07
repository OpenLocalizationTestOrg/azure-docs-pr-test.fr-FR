---
title: "aaaManage intégration de métadonnées de l’artefact - compte Azure Logic Apps | Documents Microsoft"
description: "Ajout ou suppression de métadonnées d’artefact à partir de comptes d’intégration pour Azure Logic Apps"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a>Gestion de métadonnées d’artefact dans des comptes d’intégration pour des applications logiques

Vous pouvez définir des métadonnées personnalisées pour les artefacts dans les comptes d’intégration et récupérer ces métadonnées pendant l’exécution pour votre application logique. Par exemple, vous pouvez spécifier des métadonnées pour les artefacts tels que des partenaires, des contrats, des schémas et mappages - tous stockent les métadonnées à l’aide de paires clé-valeur. Actuellement, les artefacts ne peut pas créer les métadonnées via l’interface utilisateur, mais vous pouvez utiliser les API REST toocreate métadonnées. métadonnées tooadd lorsque vous créez ou sélectionnez un partenaire, un accord ou un schéma Bonjour portail Azure, choisissez **modifier en tant que JSON**. métadonnées d’artefact tooretrieve dans les applications de la logique, vous pouvez utiliser fonctionnalité d’intégration compte artefact recherche hello.

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a>Ajouter des métadonnées tooartifacts dans les comptes d’intégration

1. Créez un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md).

2. Ajouter un compte d’intégration tooyour artefact, par exemple, un [partenaire](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [accord](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), ou [schéma](logic-apps-enterprise-integration-schemas.md).

3.  Sélectionnez l’artefact de hello, choisissez **modifier en tant que JSON**et entrez les informations de métadonnées.

    ![Saisie des métadonnées](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a>Récupération des métadonnées à partir d’artefacts pour les applications logiques

1. Créez une [application logique](logic-apps-create-a-logic-app.md).

2. Créer un [lien à partir de votre compte d’intégration logique application tooyour](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app). 

3. Dans le Concepteur d’application logique, ajouter un déclencheur comme *demande* ou *HTTP* tooyour logique application.

4.  Choisissez **Étape suivante** > **Ajouter une action**. Recherchez *Intégration*, puis recherchez et sélectionnez **Compte d’intégration - Recherche d’artefact de compte d’intégration**.

    ![Sélectionner Recherche d’artefact de compte d’intégration](media/logic-apps-enterprise-integration-metadata/image2.png)

5. Sélectionnez hello **le Type d’artefact**et fournir hello **nom de l’objet**.

    ![Sélectionner le type d’artefact et spécifiez son nom](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a>Exemple : récupération des métadonnées du partenaire

Les métadonnées du partenaire ont ces détails `routingUrl` :

![Rechercher des métadonnées de « routingURL » de partenaire](media/logic-apps-enterprise-integration-metadata/image6.png)

1. Dans votre application logique, ajoutez votre déclencheur, une action **Compte d’intégration - Recherche d’artefact de compte d’intégration** pour votre partenaire et une requête **HTTP**.

    ![Ajouter le déclencheur, la recherche de l’artefact et application de « HTTP » tooyour logique](media/logic-apps-enterprise-integration-metadata/image4.png)

2. tooretrieve hello URI, accédez tooCode affichage pour votre application logique. La définition de votre application logique doit ressembler à cet exemple :

    ![Recherche](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur les contrats](logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  
