---
title: "aaaDeploy et mettre à niveau microservices Azure localement | Documents Microsoft"
description: "Découvrez comment tooset configuration d’un cluster Service Fabric local, déployez un tooit d’application existant et puis mise à niveau de cette application."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a>Prise en main avec le déploiement et la mise à niveau d’applications sur votre cluster local
Bonjour Azure Service Fabric SDK inclut un environnement de développement local complet que vous pouvez utiliser tooquickly prise en main déploiement et gestion des applications sur un cluster local. Dans cet article, vous créez un cluster local, déployez une tooit d’application existant et puis mettre à niveau cette version de nouvelle application tooa, à partir de Windows PowerShell.

> [!NOTE]
> Cet article suppose que vous avez déjà [configuré votre environnement de développement](service-fabric-get-started.md).
> 
> 

## <a name="create-a-local-cluster"></a>Créer un cluster local
Un cluster Service Fabric représente un ensemble de ressources matérielles sur lequel vous pouvez déployer des applications. En règle générale, un cluster est constitué de n’importe où à partir de cinq réduire des milliers d’ordinateurs. Toutefois, hello Service Fabric SDK inclut une configuration de cluster pouvant s’exécuter sur un seul ordinateur.

Il est important de toounderstand qui hello cluster local Service Fabric n’est pas un émulateur ou un simulateur. Il s’exécute hello même code de plate-forme qui se trouve sur des clusters comportant plusieurs ordinateurs. Hello seule différence est qu’elle s’exécute le processus de plateforme hello qui sont normalement réparties sur cinq ordinateurs sur un ordinateur.

Hello SDK fournit deux façons tooset, configuration d’un cluster local : une Windows PowerShell script et hello Gestionnaire du Cluster Local système barre d’état d’application. Dans ce didacticiel, nous utilisons de script PowerShell hello.

> [!NOTE]
> Si vous avez déjà créé un cluster local en déployant une application depuis Visual Studio, vous pouvez ignorer cette section.
> 
> 

1. Lancez une nouvelle fenêtre PowerShell en tant qu’administrateur.
2. Exécutez le script d’installation de cluster hello à partir du dossier du Kit de développement logiciel hello :
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    L’installation du cluster prend quelques instants. Une fois l’installation terminée, vous devriez obtenir un résultat similaire à ceci :
   
    ![Résultat de configuration du cluster][cluster-setup-success]
   
    Vous êtes maintenant prêt tootry déploiement d’un cluster de tooyour d’application.

## <a name="deploy-an-application"></a>Déployer une application
Hello Service Fabric SDK comprend un ensemble complet des infrastructures et outils pour créer des applications de développeur. Si vous souhaitez en savoir comment les applications toocreate dans Visual Studio, consultez [créer votre première application de Service Fabric dans Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).

Dans ce didacticiel, vous utilisez un exemple d’application existant (appelé WordCount) afin de pouvoir vous concentrer sur les aspects de gestion hello de plateforme de hello : déploiement, la surveillance et la mise à niveau.

1. Lancez une nouvelle fenêtre PowerShell en tant qu’administrateur.
2. Importez le module de Service Fabric SDK PowerShell hello.
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. Créez une application hello de toostore de répertoire que vous téléchargez et déployez, tels que C:\ServiceFabric.
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. [Télécharger l’application WordCount de hello](http://aka.ms/servicefabric-wordcountapp) emplacement toohello vous avez créé.  Remarque : le navigateur Microsoft Edge de hello enregistre fichier hello avec un *.zip* extension.  Changent d’extension de fichier hello*.sfpkg*.
5. Connecter le cluster local de toohello :
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. Créez une application à l’aide de la commande de déploiement du Kit de développement hello avec un nom et un package d’application toohello chemin d’accès.
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    Si tout se passe bien, vous devez voir hello suivant de sortie :
   
    ![Déployer un cluster local toohello d’application][deploy-app-to-local-cluster]
7. application de hello toosee en action, lancer hello navigateur et accédez trop[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html). Ce qui suit doit s’afficher :
   
    ![Interface utilisateur des applications déployées.][deployed-app-ui]
   
    Hello WordCount application est simple. Il inclut côté client JavaScript toogenerate aléatoire cinq caractères « mots », qui sont ensuite relayés application toohello via l’API Web ASP.NET. Un service avec état effectue le suivi de nombre hello de mots comptabilisées. Ils sont partitionnées selon hello premier caractère de mot de hello. Vous pouvez trouver le code source de hello pour application WordCount hello hello [classique route exemples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).
   
    application Hello que nous avons déployé contient quatre partitions. Pour les mots qui commencent par A à G sont stockés dans la première partition de hello, mots qui commencent par H et N sont stockés dans hello deuxième partition et ainsi de suite.

## <a name="view-application-details-and-status"></a>Afficher les détails et l’état de l’application
Maintenant que nous avons déployé l’application hello, examinons certains détails de l’application hello dans PowerShell.

1. Interroger toutes les applications déployées sur le cluster de hello :
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    En supposant que vous avez uniquement hello WordCount application déployée, vous voyez quelque chose de similaire à :
   
    ![Interroger toutes les applications déployées sur PowerShell :][ps-getsfapp]
2. Atteindre le niveau suivant de toohello en interrogeant l’ensemble de hello de services qui sont inclus dans l’application WordCount de hello.
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Liste des services d’application hello dans PowerShell][ps-getsfsvc]
   
    application Hello est constituée de deux services, hello serveur web frontal et le service avec état hello qui gère les mots hello.
3. Enfin, recherchez liste hello de partitions WordCountService :
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Afficher les partitions de service hello dans PowerShell][ps-getsfpartitions]
   
    Hello ensemble de commandes que vous avez utilisé, comme toutes les commandes PowerShell de l’infrastructure de Service, sont disponibles pour n’importe quel cluster que vous pouvez vous connecter, local ou distant.
   
    Pour un toointeract de manière plus visuelle avec cluster de hello, vous pouvez utiliser les outils Service Fabric Explorer hello web en naviguant trop[http://localhost:19080/Explorer](http://localhost:19080/Explorer) dans le navigateur de hello.
   
    ![Afficher les détails de l’application dans Fabric Service Explorer][sfx-service-overview]
   
   > [!NOTE]
   > toolearn en savoir plus sur le Service Fabric Explorer, consultez [visualiser votre cluster avec Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
   > 
   > 

## <a name="upgrade-an-application"></a>Mettre à niveau une application
L’infrastructure de service fournit des mises à niveau sans temps mort en surveillant la santé de l’application hello hello comme il déploie sur le cluster de hello. Effectuer une mise à niveau de hello WordCount application.

Hello nouvelle version d’application hello maintenant compte uniquement les mots qui commencent par une voyelle. Comme la mise à niveau hello déploie des, nous voyons deux modifications de comportement de l’application hello. Taux hello auquel augmente le nombre de hello doit tout d’abord, lent, étant donné que moins de mots sont comptabilisées. En second lieu, étant donné que la première partition de hello possède deux voyelles (A et E), et toutes les autres partitions contient un seul chaque, son nombre doit finalement démarrer toooutpace hello d’autres.

1. [Télécharger le package de version 2 WordCount hello](http://aka.ms/servicefabric-wordcountappv2) toohello même emplacement où vous avez téléchargé le package de version 1 hello.
2. Retourne la fenêtre de PowerShell tooyour et utilisez la commande de mise à niveau du Kit de développement hello tooregister hello la nouvelle version dans le cluster de hello. Commencez la mise à niveau de l’ensemble fibre optique hello : / WordCount application.
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    Vous devez voir hello sortie suivante dans PowerShell comme hello mise à niveau commence.
   
    ![Progression de la mise à niveau dans PowerShell][ps-appupgradeprogress]
3. Lors de la mise à niveau hello est continuer, il peut s’avérer plus facile toomonitor son état de Service Fabric Explorer. Lancez une fenêtre de navigateur et accédez trop[http://localhost:19080/Explorer](http://localhost:19080/Explorer). Développez **Applications** dans l’arborescence hello hello gauche, puis choisissez **WordCount**et enfin **fabric : / WordCount**. Dans l’onglet d’essentials hello, vous voyez état hello de mise à niveau hello elle parcoure les domaines de mise à niveau du cluster hello.
   
    ![Progression de la mise à niveau dans Service Fabric Explorer][sfx-upgradeprogress]
   
    Comme la mise à niveau hello se poursuit dans chaque domaine, contrôles d’intégrité sont effectuée tooensure qui application hello se comporte correctement.
4. Si vous réexécutez hello précédemment de requête d’ensemble de hello de services dans l’ensemble fibre optique hello : / WordCount application, notez que hello version WordCountService modifiée mais hello WordCountWebService version n’a pas :
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Services d’application de requête après mise à niveau][ps-getsfsvc-postupgrade]
   
    Cet exemple met en évidence la façon dont Service Fabric gère les mises à niveau d’application. Il touche uniquement hello ensemble de services (ou des packages de code/de configuration au sein de ces services) qui ont été modifiés, ce qui rend le processus de mise à niveau plus rapide et plus fiable de hello.
5. Enfin, retourner le comportement de hello toohello navigateur tooobserve version nouvelle de l’application hello. Comme prévu, hello nombre progresse plus lentement et partition de première hello se termine par légèrement plus du volume de hello.
   
    ![Vue hello nouvelle version de l’application hello dans le navigateur de hello][deployed-app-ui-v2]

## <a name="cleaning-up"></a>Nettoyage
Avant de conclure, il est important de tooremember qui hello cluster local est de type real. Applications continuent toorun en arrière-plan de hello jusqu'à ce que vous les supprimez.  Selon la nature hello de vos applications, une application en cours d’exécution peut prendre des ressources importantes sur votre ordinateur. Vous avez plusieurs applications de toomanage options et cluster de hello :

1. tooremove une application individuelle et toutes ses données, exécutez hello de commande suivante :
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    Ou bien, supprimez l’application hello de hello Service Fabric Explorer **ACTIONS** un menu ou hello dans la vue de liste de gauche application hello.
   
    ![Supprimer une application dans Service Fabric Explorer][sfe-delete-application]
2. Après avoir supprimé l’application hello du cluster de hello, annulez l’enregistrement de versions 1.0.0 et 2.0.0 Hello WordCount type d’application. Suppression supprime les packages d’application hello, y compris le code de hello et la configuration, à partir du magasin d’images du cluster hello.
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    Ou, dans l’Explorateur de l’infrastructure de Service, choisissez **la mise hors service Type** pour une application hello.
3. tooshut cluster de hello mais conserver les données application hello et traces, cliquez sur **arrêter le Cluster Local** dans l’application de barre d’état système hello.
4. est entièrement, cliquez sur cluster de hello toodelete **supprimer le Cluster Local** dans l’application de barre d’état système hello. Cette option entraîne une autre hello de déploiement lente prochaine fois que vous appuyez sur F5 dans Visual Studio. Supprimer cluster local de hello uniquement si vous n’envisagez pas toouse pendant un certain temps, ou si vous avez besoin des ressources de tooreclaim.

## <a name="one-node-and-five-node-cluster-mode"></a>Modes de cluster un nœud et cinq nœuds
Lorsque vous développez des applications, vous êtes souvent amené à effectuer des itérations rapides d’écriture de code, de débogage, de modification de code et de débogage. toohelp optimiser ce processus, le cluster local de hello peut exécuter dans deux modes : un nœud ou cinq nœuds. Ces deux modes de cluster présentent chacun des avantages. Cinq nœuds permet de toowork avec un cluster réel. Vous pouvez tester des scénarios de basculement, et travailler avec un plus grand nombre d’instances et de réplicas de vos services. Un nœud est un déploiement rapide toodo optimisé et l’inscription des services, toohelp vous validez rapidement le code à l’aide du runtime de Service Fabric hello.

Ni le mode de cluster un nœud, ni le mode de cluster cinq nœuds ne constituent un émulateur ou un simulateur. cluster de développement local Hello exécute hello même code de plate-forme qui se trouve sur des clusters comportant plusieurs ordinateurs.

> [!WARNING]
> Lorsque vous modifiez le mode de cluster hello, le cluster actuel hello est supprimé de votre système et un nouveau cluster est créé. données Hello stockées dans un cluster de hello sont supprimées lorsque vous modifiez le mode de cluster.
> 
> 

toochange hello mode tooone cluster à nœud, sélectionnez **le Mode Cluster** Bonjour Gestionnaire du Cluster Service Fabric Local.

![Changer de mode de cluster][switch-cluster-mode]

Ou bien, modifier le mode de cluster hello à l’aide de PowerShell :

1. Lancez une nouvelle fenêtre PowerShell en tant qu’administrateur.
2. Exécutez le script d’installation de cluster hello à partir du dossier du Kit de développement logiciel hello :
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    L’installation du cluster prend quelques instants. Une fois l’installation terminée, vous devriez obtenir un résultat similaire à ceci :
   
    ![Résultat de configuration du cluster][cluster-setup-success-1-node]

## <a name="next-steps"></a>Étapes suivantes
* Maintenant que vous avez déployé et mis à niveau certaines des applications pré intégrées, vous pouvez [Réessayer de générer les vôtres dans Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).
* Toutes les actions de hello effectuées sur le cluster local de hello dans cet article peuvent être effectuées sur un [cluster Azure](service-fabric-cluster-creation-via-portal.md) également.
* mise à niveau de Hello que nous avons effectué dans cet article a été base. Consultez hello [mise à niveau de la documentation](service-fabric-application-upgrade.md) toolearn plus d’informations sur la puissance de hello et la flexibilité de mises à niveau de Service Fabric.

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
