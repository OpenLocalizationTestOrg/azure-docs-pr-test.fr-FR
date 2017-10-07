---
title: aaaSchemas pour la validation XML - Azure Logic Apps | Documents Microsoft
description: "Valider des documents XML avec des schémas pour Azure Logic Apps et Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a>Valider le code XML avec des schémas pour Azure Logic Apps et hello Pack d’intégration Enterprise

Schémas de confirmer que vous recevez des documents XML hello sont valides et ont hello attendu de données dans un format prédéfini. Les schémas aident également à valider les messages échangés dans un scénario d’entreprise à entreprise (B2B).

## <a name="add-a-schema"></a>Ajout d’un schéma

1. Bonjour portail Azure, sélectionnez **davantage de services**.

    ![Portail Azure, « Plus de services »](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. Dans la zone de recherche de filtre hello, entrez **intégration**, puis sélectionnez **comptes d’intégration** à partir de la liste des résultats hello.

    ![Zone de recherche de filtre](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. Sélectionnez hello **compte d’intégration** où vous souhaitez le schéma de hello tooadd.

    ![Liste des comptes d’intégration](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. Choisissez hello **schémas** vignette.

    ![Exemple de compte d’intégration, « Schémas »](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a>Ajout d’un fichier de schéma d’une taille inférieure à 2 Mo

1. Bonjour **schémas** panneau s’affiche (à partir de hello étapes précédentes), sélectionnez **ajouter**.

    ![Panneau Schémas, « Ajouter »](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. Saisissez un nom pour votre schéma. Télécharger le fichier de schéma hello en sélectionnant hello dossier icône suivant toohello **schéma** boîte. Après la fin du processus de téléchargement hello, sélectionnez **OK**.

    ![Capture d’écran d’« Ajouter un schéma » avec « Fichier de petite taille » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a>Ajouter un fichier de schéma supérieur à 2 Mo (haut too8 Mo maximum)

Ces étapes varient en fonction de niveau d’accès hello blob conteneur : **Public** ou **aucun accès anonyme**.

**toodetermine ce niveau d’accès**

1.  Ouvrez **l’Explorateur de stockage Azure**. 

2.  Sous **conteneurs d’objets Blob**, sélectionnez conteneur d’objets blob hello souhaité. 

3.  Sélectionnez **Sécurité**, **Niveau d’accès**.

Si le niveau d’accès sécurité hello blob est **Public**, procédez comme suit.

![Explorateur de stockage Azure, avec « Conteneurs d’objets Blob », « Sécurité » et « Public » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. Compte de stockage hello schéma tooyour de télécharger et copier hello URI.

    ![Compte de stockage avec l’URI mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. Dans **ajouter un schéma**, sélectionnez **d’un fichier volumineux**et fournir hello URI Bonjour **URI contenu** zone de texte.

    ![Schémas, avec le bouton « Ajouter » et « Fichier volumineux » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

Si le niveau d’accès sécurité hello blob est **aucun accès anonyme**, procédez comme suit.

![Explorateur de stockage Azure, avec « Conteneurs d’objets Blob », « Sécurité » et « No anonymous access » (Aucun accès anonyme) mis en surbrillance](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. Téléchargez le compte de stockage tooyour hello schéma.

    ![Compte de stockage](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. Générer une signature d’accès partagé pour le schéma de hello.

    ![Compte de stockage, avec l’onglet des signatures d’accès partagé mis en surbrillance](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. Dans **ajouter un schéma**, sélectionnez **d’un fichier volumineux**et fournissent l’URI de signature d’accès partagé hello Bonjour **URI contenu** zone de texte.

    ![Schémas, avec le bouton « Ajouter » et « Fichier volumineux » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. Bonjour **schémas** Panneau de votre compte d’intégration, votre schéma nouvellement ajoutée doit apparaître.

    ![Votre compte d’intégration, avec « Schémas » et hello nouveau schéma mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a>Modification de schémas

1. Choisissez hello **schémas** vignette.

2. Après avoir hello **schémas** panneau s’ouvre, sélectionnez hello schéma que tooedit.

3. Sur hello **schémas** panneau, choisissez **modifier**.

    ![Panneau Schémas](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. Fichier de schéma hello SELECT que vous souhaitez tooedit, puis sélectionnez **ouvrir**.

    ![Ouvrir le schéma fichier tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

Azure affiche un message qui hello schéma téléchargé avec succès.

## <a name="delete-schemas"></a>Suppression de schémas

1. Choisissez hello **schémas** vignette.

2. Après avoir hello **schémas** panneau s’ouvre, sélectionnez hello schéma de toodelete.

3. Sur hello **schémas** panneau, choisissez **supprimer**.

    ![Panneau Schémas](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. tooconfirm que vous souhaitez toodelete hello sélectionné de schéma, choisissez **Oui**.

    ![Message de confirmation « Supprimer le schéma »](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    Bonjour **schémas** panneau, liste de schéma hello actualise et n’inclut plus schéma hello que vous avez supprimé.

    ![Votre compte d’intégration, avec « Schémas » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration de hello entreprise").  

