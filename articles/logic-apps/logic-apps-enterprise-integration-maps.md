---
title: aaaTransform XML avec XSLT mappages - Azure Logic Apps | Documents Microsoft
description: "Ajouter que XSLT mappe des données XML tootransform avec Azure Logic Apps et hello Pack d’intégration Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a>Ajouter des mappages de conversion des données XML

Enterprise integration utilise maps tootransform XML des données entre les formats. Un mappage est un document XML qui définit les données de salutation dans un document qui doit être transformé en un autre format. 

## <a name="why-use-maps"></a>Pourquoi utiliser des mappages ?

Supposons que vous recevez régulièrement B2B commandes ou des factures à partir d’un client qui utilise le format YYYMMDD hello pour les dates. Toutefois, dans votre organisation, vous stockez les dates au format MMDDYYY hello. Vous pouvez utiliser un mappage trop*transformer* format de date YYYMMDD hello en hello MMDDYYY avant le stockage des détails de commande ou une facture hello dans votre base de données de l’activité client.

## <a name="how-do-i-create-a-map"></a>Comment créer un mappage ?

Vous pouvez créer des projets d’intégration de BizTalk avec hello [Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration de hello entreprise") pour Visual Studio 2015. Vous pouvez ensuite créer un fichier de mappage d’intégration qui vous permet de représenter graphiquement les éléments entre les deux fichiers de schéma XML. Après avoir créé ce projet, vous disposerez d’un document XSLT.

## <a name="how-do-i-add-a-map"></a>Comment ajouter un mappage ?

1. Bonjour portail Azure, sélectionnez **Parcourir**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Dans la zone de recherche de filtre hello, entrez **intégration**, puis sélectionnez **comptes d’intégration** à partir de la liste des résultats hello.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Sélectionnez le compte d’intégration hello où vous souhaitez que le plan de hello de tooadd.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Sélectionnez hello **cartes** vignette.

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. Une fois que le panneau de mappages hello s’ouvre, choisissez **ajouter**.

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. Entrez un **nom** pour votre mappage. mappage de hello tooupload fichier, choisissez l’icône de dossier hello sur le côté droit de hello Hello **carte** zone de texte. Après la fin du processus de téléchargement hello, choisissez **OK**.

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. Une fois Azure ajoute le compte d’intégration tooyour hello carte, vous obtenez un message à l’écran qui affiche si votre fichier de mappage a été ajoutée ou non. Une fois que vous obtenez ce message, choisissez hello **cartes** vignette afin que vous puissiez afficher hello qui vient d’être ajouté de mappage.

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a>Comment modifier un mappage ?

Vous devez télécharger un nouveau fichier de mappage avec les modifications hello que vous souhaitez. Vous pouvez tout d’abord télécharger carte hello pour la modification.

tooupload un nouveau mappage qui remplace le mappage existant de hello, procédez comme suit.

1. Choisissez hello **cartes** vignette.

2. Une fois le panneau de mappages hello s’ouvre, sélectionnez hello mappage que tooedit.

3. Sur hello **cartes** panneau, choisissez **mise à jour**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. Dans le sélecteur de fichier hello, sélectionnez le fichier de mappage de hello que vous souhaitez tooupload, puis sélectionnez **ouvrir**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a>Comment toodelete une carte ?

1. Choisissez hello **cartes** vignette.

2. Une fois le panneau de mappages hello s’ouvre, sélectionnez le mappage hello toodelete.

3. Choisissez **Supprimer**.

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. Confirmer la carte de hello toodelete.

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")  
* [En savoir plus sur les contrats](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  
* [En savoir plus sur les transformations](logic-apps-enterprise-integration-transform.md "Découvrez les transformations d’intégration d’entreprise")  

