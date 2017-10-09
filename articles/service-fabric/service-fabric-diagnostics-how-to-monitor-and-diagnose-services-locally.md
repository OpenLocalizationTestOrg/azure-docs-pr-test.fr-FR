---
title: aaaDebug microservices Azure dans Windows | Documents Microsoft
description: "Découvrez comment toomonitor et diagnostiquer vos services écrits à l’aide de Microsoft Azure Service Fabric sur un ordinateur de développement local."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 24868aa194b8a28fa3e6de95c1de5506d912a544
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Surveillance et diagnostic des services dans une configuration de développement d’ordinateur local
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

Surveillance, détection, diagnostic et résolution des problèmes permettent toocontinue de services avec l’expérience de l’utilisateur toohello perturbations minimales. Lors de la surveillance et diagnostic est critiques dans un environnement de production déployée réelle, l’efficacité de hello dépend adopter un modèle semblable au cours du développement de tooensure services qu’ils fonctionnent lorsque vous déplacez le programme d’installation de tooa réel. Service Fabric facilite les diagnostics tooimplement service aux développeurs qui peut fonctionner en toute transparence aux configurations de développement local d’ordinateur unique et configurations de cluster de production réel.

## <a name="event-tracing-for-windows"></a>Suivi d’événements pour Windows
[Le suivi d’événements pour Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) est hello recommandé de technologie pour le suivi des messages dans l’infrastructure de Service. Voici quelques avantages liés à l’utilisation d’ETW :

* **ETW est rapide.** Il a été créé en tant que technologie de suivi avec un impact minimal sur le temps d’exécution du code.
* **Le suivi ETW fonctionne parfaitement dans des environnements de développement local ainsi que dans les configurations de cluster réel.** Cela signifie que vous n’avez pas toorewrite code de traçage lorsque vous êtes prêt toodeploy votre cluster réel tooa de code.
* **Le code système de Service Fabric utilise également ETW pour le suivi interne.** Cela vous permet de tooview vos traces d’application entrelacées avec des traces de l’infrastructure de Service système. Cela permet également vous toomore facilement comprendre les séquences hello et les relations entre votre code d’application et les événements dans le système sous-jacent de hello.
* **Il existe une prise en charge intégrée de l’infrastructure de Service Visual Studio tools tooview des événements ETW.** Événements ETW apparaissent dans hello affichage des événements de Diagnostic de Visual Studio une fois que Visual Studio est correctement configurée avec l’infrastructure de Service. 

## <a name="view-service-fabric-system-events-in-visual-studio"></a>Afficher les événements système de Service Fabric dans Visual Studio
Service Fabric émet des événements ETW de développeurs d’applications toohelp comprennent ce qui se passe dans la plateforme de hello. Si vous n’avez pas déjà fait, pour commencer, suivez les étapes de hello dans [créer votre première application dans Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md). Ces informations vous aideront vous obtenez une application en cours d’exécution avec hello Observateur d’événements de Diagnostics affichant des messages de trace hello.

1. Si les diagnostics hello fenêtre événements n’affiche pas automatiquement, accédez à toohello **vue** onglet dans Visual Studio, choisissez **autres fenêtres** , puis **Observateur d’événements de Diagnostic**.
2. Chaque événement comporte des informations de métadonnées standard qui vous indique d’événement de hello de nœud, l’application et service hello est issu. Vous pouvez également filtrer la liste des événements hello à l’aide de hello **filtrer les événements** zone en haut de hello hello de fenêtre d’événements. Par exemple, vous pouvez filtrer sur **Nom du nœud** ou **Nom du service**. Et lorsque vous examinez les détails de l’événement, vous pouvez également interrompre à l’aide de hello **suspendre** situé en haut de hello hello de fenêtre d’événements et reprendre ultérieurement sans aucune perte d’événements.
   
   ![Observateur d'événements de diagnostic de Visual Studio](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-toohello-application-code"></a>Ajoutez votre propre code d’application toohello traces personnalisées
modèles de projet Visual Studio de Service Fabric Hello contiennent des exemples de code. Hello de code montre comment le code d’application personnalisé tooadd ETW effectue le suivi qui montrent les dans l’Observateur de Visual Studio ETW hello en même temps que les traces du système à partir de l’infrastructure de Service. Bonjour avantage de cette méthode est que les métadonnées sont ajoutées automatiquement tootraces et hello Observateur d’événements de Diagnostic Visual Studio est déjà configuré toodisplay les.

Pour les projets créés à partir de hello **les modèles de service** (sans état ou avec état) recherche uniquement pour hello `RunAsync` implémentation :

1. Hello appel trop`ServiceEventSource.Current.ServiceMessage` Bonjour `RunAsync` méthode montre un exemple d’un suivi ETW personnalisée hello du code d’application.
2. Bonjour **ServiceEventSource.cs** fichier, vous trouverez une surcharge pour hello `ServiceEventSource.ServiceMessage` méthode qui doit être utilisé pour les événements à haute fréquence d’échéance tooperformance raisons.

Pour les projets créés à partir de hello **modèles d’acteur** (sans état ou avec état) :

1. Ouvrez hello **« ProjectName » .cs** fichier où *nom_projet* est le nom hello choisi pour votre projet Visual Studio.  
2. Rechercher du code de hello `ActorEventSource.Current.ActorMessage(this, "Doing Work");` Bonjour *DoWorkAsync* (méthode).  Il s'agit d'un exemple de suivi écrit ETW personnalisé à partir du code d'application.  
3. Dans le fichier **ActorEventSource.cs**, vous trouverez une surcharge pour hello `ActorEventSource.ActorMessage` méthode qui doit être utilisé pour les événements à haute fréquence d’échéance tooperformance raisons.

Après avoir ajouté ETW personnalisé tooyour service code de traçage, vous pouvez générer, déployer et exécuter l’application hello toosee à nouveau votre événement (s) dans l’Observateur d’événements de Diagnostic de hello. Si vous déboguez l’application hello avec **F5**, hello Observateur d’événements de Diagnostic s’ouvre automatiquement.

## <a name="next-steps"></a>Étapes suivantes
Hello même code de traçage que vous avez ajouté l’application tooyour ci-dessus pour obtenir des diagnostics locales fonctionne avec les outils que vous pouvez utiliser tooview ces événements lors de l’exécution de votre application sur un cluster Azure. Consultez ces articles qui portent sur hello différentes options pour les outils hello et expliquent comment vous pouvez les définir.

* [Mode de journalisation des toocollect avec Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md)
* [Agrégation et collection d’événements avec EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)

