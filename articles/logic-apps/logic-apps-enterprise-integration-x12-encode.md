---
title: Encoder des messages X12 - Azure Logic Apps | Microsoft Docs
description: "Valider des documents EDI et convertir des messages encodés en XML avec l’encodeur de messages X12 dans Enterprise Integration Pack pour Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 29d19364b9a98e351c95f13e68a2e63b9f6439f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a>Encodez des messages X12 pour Azure Logic Apps avec Enterprise Integration Pack

Avec le connecteur Encode X12 Message, vous pouvez valider l’EDI et les propriétés spécifiques au partenaire, convertir des messages codés au format XML en documents informatisés EDI au sein de l’échange, et demander un accusé de réception technique et/ou fonctionnel.
Pour utiliser ce connecteur, vous devez ajouter le connecteur à un déclencheur existant dans votre application logique.

## <a name="before-you-start"></a>Avant de commencer

Voici les éléments dont vous avez besoin :

* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure. Vous devez disposer d’un compte d’intégration pour pouvoir utiliser le connecteur Encode X12 Message.
* Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration
* Un [contrat X12](logic-apps-enterprise-integration-x12.md) déjà défini dans votre compte d’intégration

## <a name="encode-x12-messages"></a>Encoder des messages X12

1. [Créer une application logique](logic-apps-create-a-logic-app.md).

2. Le connecteur Encode X12 Message ne possède aucun déclencheur, ce qui signifie que vous devez ajouter un déclencheur pour le démarrage de votre application logique, par exemple un déclencheur de requête. Dans le concepteur d’applications logiques, ajoutez un déclencheur, puis ajoutez une action à votre application logique.

3.  Dans la zone de recherche, entrez le filtre « x12 ». Sélectionnez **X12 - Encode X12 Message par nom de contrat** ou **X12 - Encode to X 12 message par identités**.
   
    ![Recherchez « x12 »](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. Si vous n’avez pas encore créé de connexions à votre compte d’intégration, vous êtes invité à le faire à cette étape. Donnez un nom à votre connexion, puis sélectionnez le compte d’intégration auquel vous souhaitez vous connecter. 
   
    ![connexion de compte d’intégration](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    Les propriétés marquées d’un astérisque sont obligatoires.

    | Propriété | Détails |
    | --- | --- |
    | Nom de connexion * |Entrez un nom pour votre connexion. |
    | Compte d’intégration * |Entrez un nom pour votre compte d’intégration. Vérifiez que votre compte d’intégration et votre application logique se trouvent dans le même emplacement Azure. |

5.  Lorsque vous avez terminé, les détails de votre connexion doivent apparaître tels qu’indiqués dans l’exemple suivant. Pour terminer la création de votre connexion, sélectionnez l’option **Créer**.

    ![connexion de compte d’intégration créée](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    Votre connexion est maintenant créée.

    ![détails de connexion de compte d’intégration](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a>Encode X12 message par nom de contrat

Si vous choisissez d’encoder des messages X12 par nom du contrat, ouvrez la liste **Nom de l’accord X12**, entrez ou sélectionnez votre contrat X12 existant. Saisissez le message XML à encoder.

![Entrez le nom du contrat X12 et le nom du message XML à encoder](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a>Encode X12 message par identités

Si vous choisissez d’encoder des messages X12 par identités, indiquez l’identificateur et le qualificateur de l’expéditeur ainsi que l’identificateur et le qualificateur du récepteur tels que configurés dans votre contrat X12. Sélectionnez le message XML à encoder.
   
![Renseigner les identités de l’expéditeur et du destinataire, sélectionner le message XML à encoder](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a>Détails sur X12 Encode

Le connecteur X12 Encode effectue les tâches suivantes :

* Résolution du contrat en faisant correspondre les propriétés de contexte de l’expéditeur et du récepteur.
* Sérialise l’échange EDI en convertissant les messages codés au format XML en documents informatisés EDI au sein de l’échange.
* Applique les segments d’en-tête et de code de fin du document informatisé
* Génère un numéro de contrôle d’échange, un numéro de contrôle de groupe et un numéro de contrôle de document informatisé pour chaque échange sortant
* Remplace les séparateurs dans les données de charge utile
* Valide l’EDI et les propriétés spécifiques au partenaire
  * Validation de schéma des éléments de données du document informatisé par rapport au schéma de message
  * Validation EDI effectuée sur les éléments de données du document informatisé.
  * Validation étendue effectuée sur les éléments de données du document informatisé
* Demande un accusé de réception fonctionnel et/ou technique (si configuré).
  * Suite à la validation de l’en-tête, un accusé de réception technique est généré. L’accusé de réception technique renvoie l’état du traitement de l’en-tête et du code de fin d’un échange par le récepteur de l’adresse
  * Suite à la validation du corps, un accusé de réception fonctionnel est généré. L’accusé de réception fonctionnel signale chaque erreur rencontrée lors du traitement du document reçu

## <a name="view-the-swagger"></a>Afficher Swagger
Consultez les [détails sur Swagger](/connectors/x12/). 

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Découvrez Enterprise Integration Pack") 

