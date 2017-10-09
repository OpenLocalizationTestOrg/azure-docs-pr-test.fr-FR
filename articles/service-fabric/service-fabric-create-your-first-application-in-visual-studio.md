---
title: aaaCreate un service fiable Azure Service Fabric avec c#
description: "Créer, déployer et déboguer une application Reliable Service basée sur Azure Service Fabric avec Visual Studio."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>Création de votre première application de services fiables avec état c# Service Fabric

Découvrez comment toodeploy votre première application de Service Fabric pour .NET sur Windows dans quelques minutes. Une fois l’opération terminée, vous obtenez un cluster local fonctionnant avec une application de service fiable.

## <a name="prerequisites"></a>Composants requis

Avant de commencer, assurez-vous que vous avez bien [configuré votre environnement de développement](service-fabric-get-started.md). Cela inclut l’installation de type hello Service Fabric SDK et Visual Studio 2017 ou 2015.

## <a name="create-hello-application"></a>Créer l’application hello

Lancez Visual Studio en tant qu’**administrateur**.

Créer un projet avec `CTRL`+`SHIFT`+`N`

Bonjour **nouveau projet** boîte de dialogue, choisissez **Cloud > Application Service Fabric**.

Nommez l’application hello **MyApplication** et appuyez sur **OK**.

   
![Boîte de dialogue Nouveau projet dans Visual Studio][1]

Vous pouvez créer n’importe quel type d’application de Service Fabric à partir de la boîte de dialogue suivante hello. Pour ce démarrage rapide, choisissez **Service avec état**.

Nom de votre service de hello **MyStatefulService** et appuyez sur **OK**.

![Boîte de dialogue Nouveau service dans Visual Studio.][2]


Visual Studio crée le projet d’application hello et de projet de service avec état hello et les affiche dans l’Explorateur de solutions.

![Explorateur de solutions après la création de l’application de service avec état][3]

projet d’application Hello (**MyApplication**) ne contient pas de code directement. Au lieu de cela, il fait référence à un ensemble de projets de service. En outre, il contient trois autres types de contenu :

* **Profils de publication**  
Profils pour le déploiement d’environnements de toodifferent.

* **Scripts**  
Script PowerShell de déploiement/mise à niveau de votre application.

* **Définition d’application**  
Inclut le fichier ApplicationManifest.xml hello *ApplicationPackageRoot* qui décrit la composition de votre application. Fichiers de paramètres d’application associée sont sous *ApplicationParameters*, qui peut être utilisé toospecify paramètres spécifiques à l’environnement. Profil de publication Visual sélectionne Studio associé d’un fichier de paramètres d’application qui est spécifié dans hello au cours de l’environnement de déploiement tooa spécifique.
    
Pour une vue d’ensemble du contenu hello hello du projet de service, consultez [prise en main des Services fiables](service-fabric-reliable-services-quick-start.md).

## <a name="deploy-and-debug-hello-application"></a>Déployer et déboguer l’application hello

Maintenant que vous disposez d’une application, exécutez-la.

Dans Visual Studio, appuyez sur `F5` application hello de toodeploy pour le débogage.

>[!NOTE]
>Hello la première fois que vous exécutez et déployez l’application hello localement, Visual Studio crée un cluster local pour le débogage. Cette opération peut prendre un certain temps. état de la création de cluster Hello s’affiche dans la fenêtre de sortie de Visual Studio hello.

Lorsque le cluster de hello est prêt, vous recevez une notification d’une application hello cluster local système bac manager incluse avec le Kit de développement logiciel de hello.
   
![Notification de barre d’état système de cluster local][4]

Une fois hello démarrage de l’application, Visual Studio appelle automatiquement hello **Observateur d’événements de diagnostic**, où vous pouvez consulter la sortie de trace à partir de vos services.
   
![Observateur d’événements de diagnostic][5]

Hello modèle de service avec état nous utilisés affiche simplement une valeur de compteur incrémenté Bonjour `RunAsync` méthode **MyStatefulService.cs**.

Développez un des hello événements toosee de plus de détails, y compris le nœud hello où hello code est exécuté. Dans ce cas, il s’agit du \_Node\_2, bien que cela puisse être différent sur votre ordinateur.
   
![Détails de l’Observateur d’événements de diagnostic][6]

le cluster local Hello contient cinq nœuds hébergés sur un seul ordinateur. Dans un environnement de production, chaque nœud est hébergé sur une machine virtuelle ou physique distincte. débogueur de perte de hello toosimulate d’un ordinateur lors de l’exercice hello Visual Studio au hello même temps, nous allons prendre un des nœuds hello sur le cluster local de hello.

Bonjour **l’Explorateur de solutions** fenêtre, ouvrez **MyStatefulService.cs**. 

Recherche hello `RunAsync` (méthode) et définissez un point d’arrêt sur la première ligne de hello de méthode hello.

![Point d’arrêt dans la méthode RunAsync de service avec état][7]

Lancez hello **Service Fabric Explorer** outil en cliquant sur hello **le Gestionnaire du Cluster Local** application de barre d’état système et choisissez **gérer un Cluster Local**.

![Lancer le Service Fabric Explorer à partir de hello Gestionnaire du Cluster Local][systray-launch-sfx]

[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offre une représentation visuelle d’un cluster. Elle inclut ensemble hello des applications déployées tooit et ensemble hello nœuds physiques qui le composent.

Dans le volet gauche de hello, développez **Cluster > nœuds** et nœud de hello rechercher où votre code est en cours d’exécution.

Cliquez sur **Actions > désactiver (Redémarrer)** toosimulate un redémarrage de l’ordinateur.

![Arrêter un nœud Service Fabric Explorer][sfx-stop-node]

Bientôt, vous devez voir votre point d’arrêt atteint dans Visual Studio que vous faisiez en toute transparence sur un nœud de calcul de hello bascule tooanother.


Ensuite, retourner toohello Observateur d’événements de Diagnostic et observez les messages de type hello. compteur de Hello a continué à incrémentation, même si les événements hello réellement provenant d’un autre nœud.

![Observateur d’événements de diagnostic après basculement][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a>Nettoyage de cluster local de hello (facultatif)

N’oubliez pas que ce cluster local est réel. L’arrêt du débogueur de hello supprime l’instance d’application et annule l’inscription du type de l’application hello. Toutefois, le cluster de hello continue toorun en arrière-plan de hello. Lorsque vous êtes le cluster local de prêt toostop hello, il existe deux options.

### <a name="keep-application-and-trace-data"></a>Conserver les données d’application et de trace

Arrêter le cluster de hello en cliquant sur hello **le Gestionnaire du Cluster Local** application de barre d’état système, puis **arrêter le Cluster Local**.

### <a name="delete-hello-cluster-and-all-data"></a>Supprimer le cluster de hello et toutes les données

Supprimer le cluster de hello en cliquant sur hello **le Gestionnaire du Cluster Local** application de barre d’état système, puis **supprimer le Cluster Local**. 

Si vous choisissez cette option, Visual Studio redéployer hello de cluster hello prochaine fois que vous exécutez hello application. Choisissez cette option si vous n’envisagez pas cluster local de hello toouse pendant un certain temps, ou si vous avez besoin des ressources de tooreclaim.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les [services fiables](service-fabric-reliable-services-introduction.md).
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
