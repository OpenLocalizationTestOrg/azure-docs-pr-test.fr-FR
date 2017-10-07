---
title: les messages EDIFACT aaaDecode - Azure Logic Apps | Documents Microsoft
description: "Validation EDI et générer des accusés de réception avec un décodeur de message EDIFACT hello en hello Enterprise Integration Pack pour Azure Logic Apps"
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
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Décoder les messages EDIFACT pour Azure Logic Apps avec hello Pack d’intégration Enterprise

Avec le connecteur de message EDIFACT de décoder hello, vous pouvez valider EDI et des propriétés spécifiques aux partenaires, fractionner des échanges en ensembles de transactions ou conserver les échanges entières et générer des accusés de réception pour les transactions traitées. toouse ce connecteur, vous devez ajouter tooan de connecteur hello existant déclencheur dans votre application logique.

## <a name="before-you-start"></a>Avant de commencer

Voici les éléments hello que vous devez :

* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure. Vous devez disposer d’un connecteur de message intégration compte toouse hello EDIFACT de décoder. 
* Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration
* Un [contrat EDIFACT](logic-apps-enterprise-integration-edifact.md) déjà défini dans votre compte d’intégration

## <a name="decode-edifact-messages"></a>Messages Decode EDIFACT

1. [Créer une application logique](logic-apps-create-a-logic-app.md).

2. connecteur de message de décoder les EDIFACT Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande. Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.

3. Dans la zone de recherche de hello, entrez « EDIFACT » comme filtre. Sélectionnez **Decode EDIFACT Message**.
   
    ![recherche EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion. Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect.
   
    ![créer un compte d’intégration](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    Les propriétés marquées d’un astérisque sont obligatoires.

    | Propriété | Détails |
    | --- | --- |
    | Nom de connexion * |Entrez un nom pour votre connexion. |
    | Compte d’intégration * |Entrez un nom pour votre compte d’intégration. Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement. |

4. Lorsque vous avez terminé la création de votre connexion de toofinish, choisissez **créer**. Détails de votre connexion doivent ressembler exemple toothis similaire :

    ![détails du compte d’intégration](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. Une fois que votre connexion est créée, comme indiqué dans cet exemple, sélectionnez toodecode de message de fichier plat de EDIFACT hello.

    ![connexion de compte d’intégration créée](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    Par exemple :

    ![Sélectionner le message de fichier plat EDIFACT à décoder](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a>Détails sur le décodeur EDIFACT

connecteur de décoder les EDIFACT Hello effectue ces tâches : 

* Valide l’enveloppe hello par rapport à l’accord de partenariat commercial.
* Résout l’accord de hello en mettant en correspondance le qualificateur de l’expéditeur hello et identificateur et qualificateur du récepteur et identificateur.
* Fractionne un échange en plusieurs transactions lors de l’échange de hello a plus d’une transaction en fonction de l’accord hello configuration des paramètres de réception.
* Désassemble l’échange de hello.
* Valide l’EDI et les propriétés spécifiques du partenaire, y compris :
  * Validation de la structure de l’enveloppe échange hello
  * Validation du schéma d’enveloppe hello contre le schéma de contrôle hello
  * Validation du schéma des éléments de données de document informatisé hello contre le schéma de message hello
  * Validation EDI effectuée sur les éléments de données du document informatisé.
* Vérifie que hello échange, groupe et transaction numéros de contrôle ne sont pas les doublons (si configuré) 
  * Vérifie le numéro de contrôle d’échange hello par rapport aux échanges reçus précédemment. 
  * Vérifie le numéro de contrôle de groupe hello par rapport à d’autres numéros de contrôle de groupe dans l’échange de hello. 
  * Vérifie les transactions hello définit le numéro de contrôle par rapport à d’autres numéros de contrôle de transaction de ce groupe.
* Fractionne échange hello en documents informatisés ou conserve l’ensemble de l’échange hello :
  * Scinder l’échange en documents informatisés : suspendre les documents informatisés en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé. 
  action de décodage Hello X12 génère uniquement ces documents informatisés dont la validation échouent trop`badMessages`et fournit en sortie hello transactions restantes définit trop`goodMessages`.
  * Scinder l’échange en documents informatisés : suspendre l’échange en cas d’erreur : fractionne l’échange en documents informatisés et analyse chaque document informatisé. 
  Si une ou plusieurs transactions définit dans la validation a échoué échange hello, action de décodage hello X12 génère toutes les transactions hello définit dans cet échange trop`badMessages`.
  * Préserver l’échange : suspendre les documents informatisés en cas d’erreur : échange de hello Preserve et processus hello tout échange par lot. 
  action de décodage Hello X12 génère uniquement ces documents informatisés dont la validation échouent trop`badMessages`et fournit en sortie hello transactions restantes définit trop`goodMessages`.
  * Préserver l’échange : suspendre l’échange en cas d’erreur : échange de hello Preserve et processus hello tout échange par lot. 
  Si une ou plusieurs transactions définit dans la validation a échoué échange hello, action de décodage hello X12 génère toutes les transactions hello définit dans cet échange trop`badMessages`.
* Génère un accusé de réception fonctionnel et/ou technique (contrôle) (si configuré).
  * Un accusé de réception technique ou le hello CONTRL ACK signale les résultats de hello d’une vérification syntaxique d’échange de hello complet reçu.
  * Un accusé de réception fonctionnel accuse réception de l’acceptation ou du refus d’un groupe ou d’un échange reçu

## <a name="view-swagger-file"></a>Afficher le fichier Swagger
Détails de Swagger tooview hello pour le connecteur d’EDIFACT hello, consultez [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise") 

