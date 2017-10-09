---
title: "échecs d’aaaDiagnose - Azure Logic Apps | Documents Microsoft"
description: "Common toounderstand façons échouent où les applications de logique"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a>Diagnostiquer des échecs d’applications logiques
Si vous rencontrez des problèmes ou défaillances de vos applications logiques, il existe quelques approches peuvent vous aider à mieux comprendre la provenant des échecs de hello.  

## <a name="azure-portal-tools"></a>Outils du Portail Azure
Hello portail Azure fournit de nombreux outils toodiagnose chaque application logique à chaque étape.

### <a name="trigger-history"></a>Historique du déclencheur

Chaque application logique comporte au moins un déclencheur. Si vous remarquez que les applications ne sont pas déclencher, recherchez la première historique de déclencheur hello pour plus d’informations. Vous pouvez accéder à l’historique de déclencheur hello sur le panneau de hello logique app'ss principal.

![Localisation de l’historique de déclencheur hello][1]

historique de déclencheur Hello répertorie toutes les tentatives de déclencheur effectuée par votre application logique. Vous pouvez cliquer sur chaque toodrill de la tentative de déclencheur dans les détails de hello, plus précisément, les entrées ou les sorties qui hello tentative de déclencheur généré. Si vous trouvez des déclencheurs ayant échouées, sélectionnez la tentative de déclencheur hello et choisissez hello **sorties** lien tooreview tout générée message d’erreur, par exemple, pour les informations d’identification FTP qui ne sont pas valides.

Vous pouvez voir des états différents de Hello sont :

* **Ignoré**. point de terminaison Hello a été toocheck interrogée pour les données et a reçu une réponse qu’aucune donnée n’est disponible.
* **Réussi**. déclencheur de Hello a reçu une réponse que les données étaient disponibles. Cet état peut provenir d’un déclencheur manuel, d’un déclencheur de périodicité ou d’un déclencheur d’interrogation. Cet état est généralement accompagné par hello **déclenché** état, mais peut-être ne pas si vous avez une condition ou une commande de SplitOn en mode code qui n’a pas été satisfaite.
* **Échec**. Une erreur a été générée.

#### <a name="start-a-trigger-manually"></a>Démarrer un déclencheur manuellement

Si vous souhaitez toocheck d’application hello logique pour un déclencheur disponible immédiatement, sans attendre la prochaine récurrence de hello, cliquez sur **sélectionner le déclencheur** sur hello panneau principal tooforce une vérification. Par exemple, en cliquant sur ce lien avec un déclencheur d’échange, hello workflow tooimmediately interrogez Dropbox de nouveaux fichiers.

### <a name="run-history"></a>Historique d’exécution

Chaque déclenchement entraîne une exécution. Vous pouvez accéder à des informations d’exécution à partir du panneau principal hello, qui contient de nombreuses informations qui peuvent vous aider à comprendre le déroulement du flux de travail hello.

![Localisation hello l’historique d’exécution][2]

Une série de tests affiche l’un des hello suivant des États :

* **Réussi**. Toutes les actions ont réussi. Si une erreur s’est produite, cet échec a été géré par une action qui s’est produite plus loin dans le flux de travail hello. Autrement dit, Échec de hello était traitée par une action qui a été définie toorun après une action qui a échoué.
* **Échec**. Au moins une action a eu une défaillance qui n’a pas été gérée par une action plus loin dans le flux de travail hello.
* **Annulé**. flux de travail Hello était en cours d’exécution, mais a reçu une demande d’annulation.
* **Exécution en cours**. flux de travail Hello est en cours d’exécution. Cet état peut se produire pour les workflows d’accélérée, ou en raison de hello actuel de plan de tarification. Pour plus d’informations, consultez [limites d’action sur la page de tarification de hello](https://azure.microsoft.com/pricing/details/app-service/plans/). Configuration des diagnostics (graphiques hello qui apparaissent sous l’historique d’exécution de hello) peut également fournir plus d’informations sur les événements de limitation de bande passante qui se produisent.

Lorsque vous examinez un historique d’exécution, vous pouvez rechercher des détails supplémentaires.  

#### <a name="trigger-outputs"></a>Sorties du déclencheur

Déclencheur génère des données hello provient d’un déclencheur de hello. Ces sorties peuvent vous aider à déterminer si toutes les propriétés ont renvoyé les valeurs attendues.

> [!NOTE]
> Si vous rencontrez un contenu que vous ne comprenez pas, découvrez comment Azure Logic Apps [gère les différents types de contenu](../logic-apps/logic-apps-content-type.md).
> 

![Exemples de sorties du déclencheur][3]

#### <a name="action-inputs-and-outputs"></a>Entrées et sorties d’actions

Vous pouvez explorer les entrées hello et sorties reçue d’une action. Ces données sont utiles pour comprendre la taille de hello et la forme de sorties de hello et également pour rechercher des messages d’erreur qui ont été générées.

![Entrées et sorties d’actions][4]

## <a name="debug-workflow-runtime"></a>Déboguer le runtime du workflow

En même temps que l’analyse hello entrées, sorties et les déclencheurs d’une exécution, vous pouvez ajouter certains flux de travail tooa étapes aider au débogage. 
[RequestBin](http://requestb.in) est un outil puissant que vous pouvez ajouter en tant qu’étape d’un workflow. À l’aide de RequestBin, vous pouvez configurer un inspecteur toodetermine hello exacte taille des requêtes HTTP, la forme et le format d’une requête HTTP. Vous pouvez créer un RequestBin et coller des URL de hello dans une action de publication HTTP avec le contenu du corps que vous souhaitez tootest, par exemple, une expression ou une autre sortie de l’étape d’application logique. Après avoir exécuté l’application logique de hello, vous pouvez actualiser votre toosee RequestBin la demande de hello formée lors de la génération à partir du moteur de Logic Apps hello.

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
