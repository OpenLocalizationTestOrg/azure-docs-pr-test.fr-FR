---
title: aaaAdd hello Twilio connecteur dans vos applications Azure logique | Documents Microsoft
description: "Vue d’ensemble de hello Twilio connecteur avec des paramètres de l’API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a>Prise en main connecteur de Twilio hello
Se connecter tooTwilio toosend et recevoir des messages SMS et MMS IP globales. Avec Twilio, vous pouvez :

* Générer des flux de votre entreprise en fonction des données hello que vous obtenez à partir de Twilio. 
* Utiliser des actions pour obtenir un message, répertorier les messages, et plus encore. Ces actions Obtient une réponse et puis disposition de sortie de hello pour d’autres actions. Par exemple, quand vous recevez un nouveau message Twilio, vous pouvez prendre ce message et l’utiliser comme flux de travail Service Bus. 

Commencez par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tootwilio"></a>Créer un tooTwilio de connexion
Lorsque vous ajoutez ce connecteur tooyour les applications logique, entrez hello Twilio valeurs suivantes :

| Propriété | Requis | Description |
| --- | --- | --- |
| ID de compte |Oui |Entrez votre ID de compte Twilio |
| Jeton d'accès |Oui |Entrez votre jeton d’accès Twilio |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

Si vous n’avez pas un jeton d’accès Twilio, consultez [Identité de l’utilisateur et jetons d’accès](https://www.twilio.com/docs/api/chat/guides/identity).

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/twilio/).

## <a name="more-connectors"></a>Autres connecteurs
Revenir en arrière toohello [liste des API](apis-list.md).
