---
title: "partenaires aaaCreate pour les messages de l’entreprise-entreprise (B2B) - Azure Logic Apps | Documents Microsoft"
description: "Découvrez comment l’intégration de tooyour tooadd partenaires compte avec hello Pack d’intégration Enterprise et Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a>Ajout ou mise à jour des partenaires dans les contrats d’entreprise à entreprise de votre flux de travail

Les partenaires sont des entités qui participent aux transactions d’entreprise à entreprise (B2B) et qui échangent des messages entre eux. Avant de pouvoir créer des partenaires qui vous représentent et qui représentent une autre organisation dans le cadre de ces transactions, vous devez partager des informations qui identifient et valident les messages envoyés par chacun. Une fois que vous présentent ces détails et que vous êtes prêt toostart votre relation commerciale, vous pouvez créer des partenaires dans votre toorepresent de compte d’intégration vous à la fois.

## <a name="what-roles-do-partners-have-in-your-integration-account"></a>Quels rôles jouent les partenaires dans votre compte d’intégration ?

toodefine plus d’informations sur les messages hello échangés entre partenaires, vous créez des accords entre les partenaires. Toutefois, avant de pouvoir créer un accord, vous devez avoir ajouté le compte d’au moins deux serveurs partenaires d’intégration tooyour. Votre organisation doit faire partie du contrat de hello hello **partenaire hôte**. Hello autre partenaire, ou **partenaire invité** représente hello organisation qui échange des messages avec votre organisation. partenaire invité de Hello peut être une autre société, ou même un service de votre organisation.

Après avoir ajouté ces partenaires, vous pouvez créer un contrat.

Réception et paramètres d’envoi sont orientés hello point de vue de hello Hosted partenaire. Par exemple, hello paramètres de réception dans un accord déterminent comment les partenaires hello hébergé reçoit les messages envoyés à partir d’un partenaire invité. De même, les paramètres d’envoi hello sur l’accord de hello indiquent comment les partenaires hello hébergé envoie partenaire de messages toohello invité.

## <a name="how-toocreate-a-partner"></a>Comment toocreate un partenaire ?

1. Bonjour portail Azure, sélectionnez **Parcourir**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Dans la zone de recherche de filtre hello, entrez **intégration**, puis sélectionnez **comptes d’intégration** dans la liste des résultats hello.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Sélectionnez le compte d’intégration hello où vous souhaitez tooadd vos partenaires.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Sélectionnez hello **partenaires** vignette.

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. Dans le panneau de partenaires hello, choisissez **ajouter**.

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. Entrez un nom pour votre partenaire, puis sélectionnez un **qualificateur**. Enfin, vous devez entrer un **valeur** toohelp identifier des documents qui entrent dans vos applications.

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. progression de hello toosee pour votre processus de création de partenaire, sélectionnez hello *représentant une cloche* icône de notification.

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. tooconfirm vos nouveaux partenaires a été correctement ajouté, sélectionnez hello **partenaires** vignette.

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    Une fois que vous sélectionnez la vignette de partenaires hello, vous verrez également partenaires nouvellement ajoutés dans le panneau de partenaires hello.

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a>Comment des partenaires de tooedit existant dans votre compte d’intégration

1. Sélectionnez hello **partenaires** vignette.
2. Une fois le panneau de partenaires hello s’ouvre, sélectionnez partenaire hello tooedit.
3. Sur hello **partenaire de mise à jour** vignette, apportez vos modifications.
4. Une fois que vous avez terminé, choisissez **enregistrer**, ou sélectionnez de vos modifications, toocancel **ignorer**.

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a>Comment toodelete un partenaire

1. Sélectionnez hello **partenaires** vignette.
2. Une fois le panneau de partenaire hello s’ouvre, sélectionnez partenaire hello que vous souhaitez toodelete.
3. Choisissez **Supprimer**.

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur les contrats](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  

