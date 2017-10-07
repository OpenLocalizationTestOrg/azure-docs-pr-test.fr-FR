---
title: messages aaaDecode X12 - Azure Logic Apps | Documents Microsoft
description: "Valider EDI et de générer des accusés de réception avec un décodeur de message hello X12 Bonjour Enterprise Integration Pack pour Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Décoder X12 messages pour Azure Logic Apps avec hello Pack d’intégration Enterprise

Avec le connecteur de message hello Decode X12, vous pouvez valider l’enveloppe hello par rapport à un accord de partenariat commercial, valider EDI et des propriétés spécifiques au partenaire, fractionner des échanges en ensembles de transactions ou conserver les échanges entières et générer accusés de réception pour les transactions traitées. toouse ce connecteur, vous devez ajouter tooan de connecteur hello existant déclencheur dans votre application logique.

## <a name="before-you-start"></a>Avant de commencer

Voici les éléments hello que vous devez :

* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md) déjà défini et associé à votre abonnement Azure. Vous devez disposer d’un connecteur de message de décodage X12 intégration compte toouse hello.
* Au moins deux [partenaires](logic-apps-enterprise-integration-partners.md) déjà définis dans votre compte d’intégration
* Un [contrat X12](logic-apps-enterprise-integration-x12.md) déjà défini dans votre compte d’intégration

## <a name="decode-x12-messages"></a>Décoder des messages X12

1. [Créer une application logique](logic-apps-create-a-logic-app.md).

2. connecteur de message de décodage X12 Hello n’a pas les déclencheurs, vous devez donc ajouter un déclencheur pour démarrer votre application logique, comme un déclencheur de la demande. Dans le Concepteur d’application logique de hello, ajouter un déclencheur, puis ajoutez une application de la logique de tooyour action.

3.  Dans la zone de recherche de hello, entrez « x12 » pour votre filtre. Sélectionnez **X12 – Decode X12 Message**.
   
    ![Recherchez « x12 »](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. Si vous n’avez pas précédemment créé toutes les connexions tooyour compte d’intégration, vous êtes invité à entrer toocreate maintenant cette connexion. Nommez votre connexion et sélectionnez le compte d’intégration hello que vous souhaitez tooconnect. 

    ![Fournir les détails de connexion de compte d’intégration](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    Les propriétés marquées d’un astérisque sont obligatoires.

    | Propriété | Détails |
    | --- | --- |
    | Nom de connexion * |Entrez un nom pour votre connexion. |
    | Compte d’intégration * |Entrez un nom pour votre compte d’intégration. Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour même emplacement. |

5.  Lorsque vous avez terminé, les détails de votre connexion doivent ressembler exemple toothis similaire. toofinish création de votre connexion, choisissez **créer**.
   
    ![détails de connexion de compte d’intégration](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. Une fois que votre connexion est créée, comme indiqué dans cet exemple, sélectionnez toodecode de message de fichier plat hello X12.

    ![connexion de compte d’intégration créée](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    Par exemple :

    ![Sélectionner le message de fichier plat X12 à décoder](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a>Informations sur X12 Decode

connecteur de décodage Hello X12 effectue ces tâches :

* Valide l’enveloppe hello par rapport à l’accord de partenariat commercial
* Valide l’EDI et les propriétés spécifiques au partenaire
  * Validation de la structure EDI et validation du schéma étendue
  * Validation de la structure hello d’enveloppe d’échange hello.
  * Validation du schéma d’enveloppe hello contre le schéma de contrôle hello.
  * Validation du schéma des éléments de données de document informatisé hello contre le schéma de message hello.
  * Validation EDI effectuée sur les éléments de données du document informatisé. 
* Vérifie que hello échange, groupe et transaction numéros de contrôle ne sont pas des doublons
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
* Génère un accusé de réception fonctionnel et/ou technique (si configuré).
  * Suite à la validation de l’en-tête, un accusé de réception technique est généré. accusé de réception technique Hello signale l’état de hello du traitement hello d’un en-tête de l’échange et le code de fin par le récepteur d’adresse hello.
  * Suite à la validation du corps, un accusé de réception fonctionnel est généré. Hello accusé de réception fonctionnel signale chaque erreur rencontrée lors du traitement hello a reçu de document

## <a name="view-hello-swagger"></a>Swagger hello de vue
Consultez hello [swagger détails](/connectors/x12/). 

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur hello Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise") 

