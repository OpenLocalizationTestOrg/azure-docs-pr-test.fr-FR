---
title: "messages aaaAS2 pour l’intégration d’entreprise B2B - Azure Logic Apps | Documents Microsoft"
description: "Échangez des messages AS2 dans le cadre d’une intégration d’entreprise B2B avec Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a>Échangez des messages AS2 dans le cadre d’une intégration d’entreprise avec Logic Apps

Avant de pouvoir échanger des messages AS2 pour Azure Logic Apps, vous devez créer un contrat AS2 et le stocker dans votre compte d’intégration. Voici les étapes de hello pour l’accord de toocreate un AS2.

## <a name="before-you-start"></a>Avant de commencer

Voici les éléments hello que vous devez :

* Un [compte d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md) déjà défini et associé à votre abonnement Azure
* Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) qui sont déjà définis dans votre compte d’intégration et configuré avec un qualificateur hello AS2 sous **des identités d’entreprise**

> [!NOTE]
> Lorsque vous créez un accord, le contenu dans le fichier de contrat hello hello doit correspondre au type de contrat de hello.    

Une fois que vous avez [créé un compte d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md) et [ajouté des partenaires](logic-apps-enterprise-integration-partners.md), vous pouvez créer un contrat AS2 en procédant comme suit.

## <a name="create-an-as2-agreement"></a>Créer un contrat AS2

1.  Connectez-vous à toohello [portail Azure](http://portal.azure.com "portail Azure").  

2.  Dans le menu de gauche hello, sélectionnez **davantage de services**. Dans la zone de recherche de hello, entrez **intégration** comme filtre. Dans la liste des résultats hello, sélectionnez **comptes d’intégration**.

    > [!TIP]
    > Si vous ne voyez pas **davantage de services**, vous pouvez avoir des menus de hello tooexpand tout d’abord. Haut hello du menu de hello réduit, sélectionnez **menu Afficher**.

    ![Plus de services, filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. Bonjour **comptes d’intégration** panneau qui s’ouvre, le compte d’intégration hello sélectionnez où vous souhaitez l’accord de hello toocreate.
Si aucun compte d’intégration ne s’affiche, [créez-en un](../logic-apps/logic-apps-enterprise-integration-accounts.md "Tout sur les comptes d’intégration").  

    ![Sélectionnez compte d’intégration hello où toocreate hello accord](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Choisissez hello **accords** vignette. Si vous n’avez pas une vignette de contrats, ajoutez d’abord les mosaïques hello.

    ![Choisissez la mosaïque « Contrats »](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. Dans le panneau des accords hello qui s’ouvre, choisissez **ajouter**.

    ![Choisir « Ajouter »](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. Sous **Ajouter**, entrez le **nom** de votre contrat. Pour le **type de contrat**, sélectionnez **AS2**. Sélectionnez hello **partenaire hôte**, **identité de l’hôte**, **partenaire invité**, et **invité identité** pour votre accord.

    ![Renseigner les détails relatifs au contrat](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | Propriété | Description |
    | --- | --- |
    | Nom |Nom de contrat de hello |
    | Type de contrat | Doit être AS2 |
    | Partenaire hôte |Un contrat nécessite un partenaire hôte et un partenaire invité. partenaire d’accueil Hello représente l’organisation hello qui configure l’accord de hello. |
    | Identité de l’hôte |Un identificateur pour le partenaire d’accueil hello |
    | Partenaire invité |Un contrat nécessite un partenaire hôte et un partenaire invité. partenaire invité de Hello représente l’organisation hello qui effectue l’entreprise avec le partenaire d’accueil hello. |
    | identité de l’invité |Un identificateur de partenaire invité de hello |
    | Paramètres de réception |Ces propriétés s’appliquent tooall les messages reçus par un accord. |
    | Paramètres d’envoi |Ces propriétés s’appliquent tooall les messages envoyés par un accord. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configuration du traitement des messages reçus

Maintenant que vous avez défini les propriétés de l’accord hello, vous pouvez configurer comment cet accord identifie et traite les messages entrants reçus à partir de votre partenaire via ce contrat.

1.  Sous **Ajouter**, sélectionnez **Paramètres de réception**.
Configurez ces propriétés en fonction de votre accord avec le partenaire hello qui échange des messages avec vous. Pour obtenir des descriptions de propriété, consultez le tableau de hello dans cette section.

    ![Configurer les « Paramètres de réception »](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. Si vous le souhaitez, vous pouvez remplacer les propriétés de hello de messages entrants en sélectionnant **remplacer les propriétés du message**.

3. toorequire signé de tous les toobe de messages entrants, sélectionnez **Message doit être signé**. À partir de hello **certificat** , sélectionnez un existant [certificat public du partenaire invité](../logic-apps/logic-apps-enterprise-integration-certificates.md) pour la validation de signature hello sur les messages de type hello. Ou créer le certificat de hello, si vous n’en avez pas.

4.  sélectionner de tous les toobe de messages entrants chiffrés, toorequire **Message doit être chiffré**. À partir de hello **certificat** , sélectionnez un existant [certificat privé du partenaire hôte](../logic-apps/logic-apps-enterprise-integration-certificates.md) pour le déchiffrement des messages entrants. Ou créer le certificat de hello, si vous n’en avez pas.

5. toorequire toobe de messages compressé, sélectionnez **Message doit être compressé**.

6. toosend une notification de disposition de messages synchrone (MDN) pour les messages reçus, sélectionnez **envoyer le MDN**.

7. toosend signé MDN pour les messages reçus, sélectionnez **envoyer le MDN signé**.

8. Sélectionnez des MDN asynchrones pour les messages reçus, toosend **envoyez un MDN asynchrone**.

9. Une fois que vous avez terminé, assurez-vous que toosave vos paramètres en choisissant **OK**.

À présent, votre contrat toohandle prêt entrante messages conformes tooyour les paramètres sélectionnés.

| Propriété | Description |
| --- | --- |
| Override message properties |Indique que les propriétés dans les messages reçus peuvent être remplacées. |
| Le message doit être signé |Requiert toobe messages signé numériquement. Configurer le certificat public de partenaire invité hello pour vérifier la signature.  |
| Le message doit être chiffré |Requiert toobe de messages chiffré. Les messages non chiffrés sont rejetés. Configurer un certificat privé de partenaire hôte hello pour le déchiffrement des messages de type hello.  |
| Le message doit être compressé |Requiert toobe messages compressé. Les messages non compressés sont rejetés. |
| Texte du MDN |Hello par défaut message disposition notification (MDN) toobe toohello envoyé expéditeur du message. |
| Send MDN (Envoyer MDN) |Requiert toobe MDN envoyé. |
| Send signed MDN (Envoyer MDN signé) |Requiert toobe MDN signé. |
| MIC Algorithm (Algorithme MIC) |Sélectionnez toouse d’algorithme hello pour signer les messages. |
| Send asynchronous MDN (Envoyer MDN asynchrone) | Requiert toobe de messages envoyé de façon asynchrone. |
| URL | Spécifiez les URL hello où toosend hello MDN. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configuration de l’envoi des messages

Vous pouvez configurer comment cet accord identifie et gère les messages sortants que vous envoyez des partenaires tooyour via ce contrat.

1.  Sous **Ajouter**, sélectionnez **Paramètres d’envoi**.
Configurez ces propriétés en fonction de votre accord avec le partenaire hello qui échange des messages avec vous. Pour obtenir des descriptions de propriété, consultez le tableau de hello dans cette section.

    ![Définir les propriétés de « Paramètres d’envoi » hello](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. toosend messages signés tooyour partenaire, sélectionnez **activer la signature des messages**. Pour signer les messages hello, Bonjour **algorithme MIC** liste, sélectionnez hello *certificat privé du partenaire hôte algorithme MIC*. Et Bonjour **certificat** , sélectionnez un existant [certificat privé du partenaire hôte](../logic-apps/logic-apps-enterprise-integration-certificates.md).

3. toosend des messages chiffrés toohello partenaire, sélectionnez **activer le chiffrement de message**. Pour chiffrer les messages hello, Bonjour **algorithme de chiffrement** liste, sélectionnez hello *algorithme de certificat public de partenaire invité*.
Et Bonjour **certificat** , sélectionnez un existant [certificat public du partenaire invité](../logic-apps/logic-apps-enterprise-integration-certificates.md).

4. message de type hello toocompress, sélectionnez **activer la compression des messages**.

5. en-tête de content-type toounfold hello HTTP sur une seule ligne, sélectionnez **dérouler les en-têtes HTTP**.

6. tooreceive MDN synchrones pour hello envoyé des messages, sélectionnez **exiger le MDN**.

7. tooreceive signé MDN pour les messages hello envoyé, sélectionnez **exiger le MDN signé**.

8. tooreceive MDN asynchrones pour hello envoyé des messages, sélectionnez **exiger le MDN asynchrone**. Si vous sélectionnez cette option, entrez les URL hello où toosend hello MDN.

9. toorequire non-répudiation de réception, sélectionnez **activer NRR**.  

10. toospecify algorithme format toouse Bonjour MIC ou signature Bonjour sortant des en-têtes de message de type hello AS2 ou MDN, sélectionnez **format d’algorithme SHA2**.  

11. Une fois que vous avez terminé, assurez-vous que toosave vos paramètres en choisissant **OK**.

Votre accord est à présent prêt toohandle les messages qui se conforment tooyour sélectionné Paramètres sortants.

| Propriété | Description |
| --- | --- |
| Enable message signing (Activer la signature des messages) |Nécessite tous les messages sont envoyés à partir de toobe d’accord hello signé. |
| MIC Algorithm (Algorithme MIC) |Bonjour toouse algorithme pour signer les messages. Configure le certificat privé de partenaire hôte hello algorithme MIC pour la signature des messages de type hello. |
| Certificat |Sélectionnez toouse de certificat hello pour signer les messages. Configure un certificat privé de partenaire hôte hello pour la signature des messages de type hello. |
| Enable message encryption (Activer le chiffrement du message) |Exige que tous les messages envoyés à partir du contrat soient chiffrés. Configure l’algorithme de certificat public hello invité partenaire pour le chiffrement des messages de type hello. |
| Algorithme de chiffrement |Bonjour toouse algorithme de chiffrement pour le chiffrement du message. Configure un certificat public de partenaire invité hello pour le chiffrement des messages de type hello. |
| Certificat |messages de salutation certificat toouse tooencrypt. Configure un certificat privé de partenaire invité hello pour le chiffrement des messages de type hello. |
| Enable message compression (Activer la compression des messages) |Exige que tous les messages envoyés à partir du contrat soient compressés. |
| Dérouler les en-têtes HTTP |Place un en-tête de content-type HTTP hello sur une seule ligne. |
| Exiger le MDN |Exige l’envoi d’un MDN pour tous les messages envoyés à partir du contrat. |
| Exiger le MDN signé |Nécessite tous les MDN envoyés accord toothis toobe signé. |
| Exiger le MDN asynchrone |Requiert un contrat de toothis de toobe envoyé MDN asynchrone. |
| URL |Spécifiez les URL hello où toosend hello MDN. |
| Enable NRR (Activer NRR) |Requiert la non-répudiation de réception (NRR), un attribut de communication qui constitue une preuve que les données hello a été reçue comme traité. |
| Format de l’algorithme SHA2 |Sélectionnez toouse de format d’algorithme dans hello MIC ou signature Bonjour en-têtes de message de type hello AS2 ou MDN sortants |

## <a name="find-your-created-agreement"></a>Comment retrouver le contrat que vous avez créé

1.  Une fois que vous terminez la définition de toutes les propriétés de votre accord, sur hello **ajouter** panneau, choisissez **OK** toofinish créer votre accord et le panneau de compte d’intégration tooyour retour.

    Le contrat que vous venez d’ajouter s’affiche dans votre liste **Contrats**.

2.  Vous pouvez également afficher vos contrats dans la vue d’ensemble de votre compte d’intégration. Dans le panneau de compte integration, choisissez **vue d’ensemble**, puis sélectionnez hello **accords** vignette. 

    ![Choisissez « Accord » vignette tooview tous les contrats](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a>Swagger hello de vue
Consultez hello [swagger détails](/connectors/as2/). 

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")  
