---
title: "aaaCreate, link, supprimer ou déplacer un compte d’intégration dans les applications Azure logique | Documents Microsoft"
description: "Comment toocreate une intégration de compte et le lier tooyour logique applications"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a>Qu’est-ce qu'un compte d’intégration ?

Un compte d’intégration permet applications d’intégration enterprise toomanage artefacts, y compris des schémas, des mappages, des certificats, des partenaires et des accords. N’importe quelle application d’intégration que vous créez utilise un tooaccess de compte de l’intégration de ces schémas, mappages, certificats et ainsi de suite.

## <a name="create-an-integration-account"></a>Création d’un compte d’intégration

1.  Connectez-vous à toohello [portail Azure](http://portal.azure.com "portail Azure"). Dans le menu de gauche hello, sélectionnez **davantage de services**.

    ![Sélectionnez « Plus de services »](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Dans la zone de recherche de hello, tapez « intégration » pour votre filtre. Dans la liste des résultats hello, sélectionnez **comptes d’intégration**.

    ![Filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. En hello haut hello, choisissez **ajouter**.

    ![Choisir Ajouter](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. Nom de votre compte d’intégration et le sélectionnez hello abonnement Azure que vous souhaitez toouse. Vous pouvez créer un **groupe de ressources** ou sélectionner un groupe de ressources existant. Sélectionnez un **Emplacement** pour l’hébergement de votre compte d’intégration et un **Niveau tarifaire**. 

    Une fois ces opérations effectuées, sélectionnez **Créer**.

    ![Indiquez les détails de votre compte d’intégration](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    Azure configure votre compte d’intégration dans emplacement hello sélectionné, qui doit se terminer dans la minute.

5. Actualisez la page de hello. Votre nouveau compte d’intégration apparaît désormais dans la liste.

    ![Votre nouveau compte d’intégration apparaît](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

Ensuite, liez compte d’intégration hello cette application logique créé tooyour vous. 

## <a name="link-an-integration-account-tooa-logic-app"></a>Lier une application de la logique de l’intégration compte tooa

toogive toomaps, schémas, des contrats et autres artefacts dans votre compte d’intégration, application logique de lien hello intégration compte tooyour accéder à vos applications logiques.

### <a name="prerequisites"></a>Composants requis

* Un compte d’intégration
* Une application logique

> [!NOTE] 
> Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour *même emplacement* avant de commencer.


1. Bonjour portail Azure, sélectionnez votre application de la logique et vérifier l’emplacement de l’application de votre logique.

    ![Sélectionnez votre application logique, vérifiez l’emplacement](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. Sous **Paramètres**, sélectionnez **Compte d’intégration**.

    ![Sélectionner « Compte d’intégration »](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. À partir de hello **sélectionner un compte d’intégration** liste, sélectionnez hello intégration compte toolink tooyour logique application. toofinish liant, choisissez **enregistrer**.

    ![Sélectionnez votre compte d’intégration](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    Vous recevez une notification qui affiche votre intégration compte est lié tooyour logique application, et que tous les artefacts de votre compte d’intégration sont maintenant disponibles tooyour logique application.

    ![Votre application logique est liée tooyour compte d’intégration](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

Maintenant que votre compte d’intégration est lié tooyour logique application, vous pouvez utiliser des connecteurs de hello B2B dans vos applications logiques. Parmi les connecteurs B2B les plus courants figurent la validation XML, et l’encodage et le décodage de fichiers plats.  

## <a name="delete-your-integration-account"></a>Supprimez votre compte d’intégration

1. Sélectionnez **Plus de services**.

    ![Sélectionnez « Plus de services »](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Dans la zone de recherche de hello, tapez « intégration » pour votre filtre. Dans la liste des résultats hello, sélectionnez **comptes d’intégration**.

    ![Filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Sélectionnez le compte d’intégration hello que vous souhaitez toodelete.

    ![Sélectionnez toodelete de compte d’intégration](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. Dans le menu de hello, choisissez **supprimer**.

    ![Choisir « Supprimer »](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. Confirmez votre compte d’intégration hello toodelete choice.

## <a name="move-your-integration-account"></a>Déplacer votre compte d’intégration

toomove un tooanother de compte d’intégration Azure abonnement ou groupe de ressources, procédez comme suit.

> [!IMPORTANT]
> Une fois que vous déplacez un compte d’intégration, vous devez mettre à jour tous les scripts toouse hello nouveaux ID de ressource.

1. Sélectionnez **Plus de services**.

    ![Sélectionnez « Plus de services »](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Dans la zone de recherche de hello, tapez « intégration » pour votre filtre. Dans la liste des résultats hello, sélectionnez **comptes d’intégration**.

    ![Filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. Sélectionnez le compte d’intégration hello que vous souhaitez toomove. Sous **Paramètres**, choisissez **Propriétés**.

    ![Sélectionnez toomove de compte d’intégration. Sous Paramètres, choisir Propriétés](./media/logic-apps-enterprise-integration-accounts/move.png)

5. Modifier le groupe de ressources hello ou un abonnement Azure qui est associé à votre compte d’intégration.

    ![Sélectionner Modifier le groupe de ressources ou Modifier l’abonnement](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur les contrats](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  

