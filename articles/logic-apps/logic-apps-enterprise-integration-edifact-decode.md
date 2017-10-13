---
title: "Décoder des messages EDIFACT - Azure Logic Apps | Microsoft Docs"
description: "Valider l’EDI et générer les accusés de réception avec le décodeur de messages EDIFACT dans Enterprise Integration Pack pour Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e3787b48037360bf6066ddce2bacba6842213b2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a>Décodez des messages EDIFACT pour Azure Logic Apps avec Enterprise Integration Pack

Avec le connecteur de messages Decode EDIFACT, vous pouvez valider l’EDI et les propriétés spécifiques du partenaire, fractionner des échanges en documents informatisés ou conserver les échanges entiers et générer des accusés de réception pour les transactions traitées. Pour utiliser ce connecteur, vous devez ajouter le connecteur à un déclencheur existant dans votre application logique.

## <a name="before-you-start"></a>Avant de commencer

Voici les éléments dont vous avez besoin :

* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure. Vous devez disposer d’un compte d’intégration pour pouvoir utiliser le connecteur Decode EDIFACT Message. 
* Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration
* Un [contrat EDIFACT](logic-apps-enterprise-integration-edifact.md) déjà défini dans votre compte d’intégration

## <a name="decode-edifact-messages"></a>Messages Decode EDIFACT

1. [Créer une application logique](logic-apps-create-a-logic-app.md).

2. Le connecteur Decode EDIFACT Message ne possède aucun déclencheur, ce qui signifie que vous devez ajouter un déclencheur pour le démarrage de votre application logique, par exemple un déclencheur de requête. Dans le concepteur d’applications logiques, ajoutez un déclencheur, puis ajoutez une action à votre application logique.

3. Dans la zone de recherche, entrez « EDIFACT » comme filtre. Sélectionnez **Decode EDIFACT Message**.
   
    ![recherche EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. Si vous n’avez pas encore créé de connexions à votre compte d’intégration, vous êtes invité à le faire à cette étape. Donnez un nom à votre connexion, puis sélectionnez le compte d’intégration auquel vous souhaitez vous connecter.
   
    ![créer un compte d’intégration](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    Les propriétés marquées d’un astérisque sont obligatoires.

    | Propriété | Détails |
    | --- | --- |
    | Nom de connexion * |Entrez un nom pour votre connexion. |
    | Compte d’intégration * |Entrez un nom pour votre compte d’intégration. Vérifiez que votre compte d’intégration et votre application logique se trouvent dans le même emplacement Azure. |

4. Pour terminer la création de votre connexion, sélectionnez l’option **Créer**. Les détails de votre connexion doivent apparaître tels qu’indiqués dans l’exemple suivant :

    ![détails du compte d’intégration](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. Une fois votre connexion est créée, comme indiqué dans cet exemple, sélectionnez le message de fichier plat EDIFACT à décoder.

    ![connexion de compte d’intégration créée](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    Par exemple :

    ![Sélectionner le message de fichier plat EDIFACT à décoder](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a>Détails sur le décodeur EDIFACT

Le connecteur Decode EDIFACT effectue les tâches suivantes : 

* Valide l’enveloppe par rapport à l’accord de partenariat commercial.
* Résout l’accord en mettant en correspondance les identificateurs et les qualificateurs de l’expéditeur et du récepteur.
* Fractionne un échange en plusieurs transactions lorsque l’échange a plusieurs transactions basées sur la configuration des paramètres de réception de l’accord.
* Désassemble l’échange.
* Valide l’EDI et les propriétés spécifiques du partenaire, y compris :
  * Validation de la structure de l’enveloppe d’échange
  * Validation de schéma de l’enveloppe par rapport au schéma de contrôle
  * Validation de schéma des éléments de données du document informatisé par rapport au schéma de message
  * Validation EDI effectuée sur les éléments de données du document informatisé.
* Vérifie que les numéros de contrôle de l’échange, du groupe et du document informatisé ne sont pas des doublons (si configuré) 
  * Vérifie le numéro de contrôle de l’échange par rapport aux échanges reçus précédemment. 
  * Vérifie le numéro de contrôle du groupe par rapport aux autres numéros de contrôle de groupe dans l’échange. 
  * Vérifie le numéro de contrôle du document informatisé par rapport aux autres numéros de contrôle de document informatisé dans ce groupe.
* Fractionne l’échange en documents informatisés ou conserve l’échange entier :
  * Scinder l’échange en documents informatisés : suspendre les documents informatisés en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé. 
  L’action X12 Decode ne génère que les documents informatisés qui échouent à la validation `badMessages` et produit les documents informatisés restants en tant que `goodMessages`.
  * Scinder l’échange en documents informatisés : suspendre l’échange en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé. 
  Si la validation d’un ou de plusieurs documents informatisés de l’échange échoue, l’action X12 Decode génère tous les documents informatisés dans cet échange en tant que `badMessages`.
  * Préserver l'échange : suspendre les documents informatisés en cas d'erreur : conserve l’échange et traite l’intégralité de l’échange par lot. 
  L’action X12 Decode ne génère que les documents informatisés qui échouent à la validation `badMessages` et produit les documents informatisés restants en tant que `goodMessages`.
  * Préserver l’échange : suspendre l’échange en cas d’erreur : conserve l’échange et traite l’intégralité de l’échange par lot. 
  Si la validation d’un ou de plusieurs documents informatisés de l’échange échoue, l’action X12 Decode génère tous les documents informatisés dans cet échange en tant que `badMessages`.
* Génère un accusé de réception fonctionnel et/ou technique (contrôle) (si configuré).
  * Un accusé de réception technique ou l’ACK CONTRL renvoie les résultats d’une vérification syntaxique de tout l’échange reçu.
  * Un accusé de réception fonctionnel accuse réception de l’acceptation ou du refus d’un groupe ou d’un échange reçu

## <a name="view-swagger-file"></a>Afficher le fichier Swagger
Pour afficher les détails Swagger du connecteur EDIFACT, consultez [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Découvrez Enterprise Integration Pack") 

