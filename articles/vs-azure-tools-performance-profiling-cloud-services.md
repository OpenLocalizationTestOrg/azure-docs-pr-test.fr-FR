---
title: "performances de hello aaaTesting d’un service cloud | Documents Microsoft"
description: "Tester les performances de hello d’un service cloud à l’aide du Générateur de profils Visual Studio hello"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7a5501aa-f92c-457c-af9b-92ea50914e24
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 98bd775e6ffcf948e737c5ec26399c81f4770fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service"></a>Test des performances de hello d’un service cloud
## <a name="overview"></a>Vue d'ensemble
Vous pouvez tester les performances hello d’un service cloud dans hello suivant façons :

* Utilisez les informations de toocollect de Diagnostics Windows Azure sur les demandes et les connexions et les statistiques du site tooreview qui montrent le fonctionnement d’un service de hello à partir d’un point de vue du client. tooget main, consultez [configuration des diagnostics pour Azure Cloud Services et Machines virtuelles](http://go.microsoft.com/fwlink/p/?LinkId=623009).
* Utilisez hello Visual Studio profiler tooget une analyse approfondie des aspects de calcul hello de la façon dont le service de hello s’exécute. Comme décrit dans cette rubrique, vous pouvez utiliser les performances de toomeasure profiler hello comme un service s’exécute dans Azure. Pour plus d’informations sur la façon dont les performances de toomeasure toouse hello du Générateur de profils en tant que service s’exécute localement dans un émulateur de calcul, consultez [hello du test de performances d’un Azure Cloud Service localement dans hello calcul émulateur à l’aide de hello profileur Visual Studio ](http://go.microsoft.com/fwlink/p/?LinkId=262845).

## <a name="choosing-a-performance-testing-method"></a>Choix d’une méthode de test des performances
### <a name="use-azure-diagnostics-toocollect"></a>Utilisez les Diagnostics Azure toocollect :
* Statistiques concernant les pages ou services web (par exemple, les demandes et les connexions).
* Statistiques sur les rôles (par exemple, le nombre de fois où un rôle est redémarré).
* Ensemble d’informations sur l’utilisation de la mémoire, comme le pourcentage de temps qui hello garbage collector prend ou hello mémoire hello définie d’un rôle en cours d’exécution.

### <a name="use-hello-visual-studio-profiler-to"></a>Utilisez le profileur Visual Studio de hello pour :
* Déterminer les fonctions hello essentiel du temps.
* Évaluer le temps nécessaire à chaque partie d’un programme utilisant de nombreuses ressources de calcul.
* Comparer des rapports de performances détaillés pour deux versions d’un service.
* Analyser l’allocation de mémoire de manière plus détaillée niveau hello allocations de mémoire individuelles.
* Analyser les problèmes d’accès concurrentiel dans du code multithread.

Lorsque vous utilisez le Générateur de profils hello, vous pouvez collecter des données lorsqu’un service cloud s’exécute localement ou dans Azure.

### <a name="collect-profiling-data-locally-to"></a>Collectez des données de profilage localement pour effectuer les tâches suivantes :
* Test des performances de hello d’une partie d’un service cloud, tels que l’exécution de hello du rôle de travail spécifique, qui ne nécessite pas une charge réaliste simulée.
* Tester les performances de hello d’un service cloud de manière isolée, dans des conditions contrôlées.
* Tester les performances d’un service cloud avant hello déployer tooAzure.
* Tester les performances de hello d’un service de cloud privé, sans perturber déploiements hello.
* Tester les performances de hello du service de hello sans entraîner de frais pour l’exécution dans Azure.

### <a name="collect-profiling-data-in-azure-to"></a>Collectez des données de profilage dans Azure pour effectuer les tâches suivantes :
* Test des performances de hello d’un service cloud sous une charge simulée ou réelle.
* Utilisez la méthode d’instrumentation hello de collecte des données de profilage, comme décrit plus loin dans cette rubrique.
* Tester les performances de hello du service de hello Bonjour même environnement que lorsque le service de hello s’exécute en production.

Vous simulez généralement une charge tootest les services cloud sous normal ou conditions de contraintes.

## <a name="profiling-a-cloud-service-in-azure"></a>Profilage d’un service cloud dans Azure
Lorsque vous publiez votre service cloud depuis Visual Studio, vous pouvez hello service de profil et hello paramètres du profilage qui permettent de que vous hello informations que vous souhaitez. Une session de profilage est démarrée pour chaque instance d’un rôle. Pour plus d’informations sur comment toopublish votre service à partir de Visual Studio, consultez [publication tooan Azure Cloud Service à partir de Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx).

toounderstand en savoir plus sur le profilage des performances dans Visual Studio, consultez [tooPerformance du Guide du débutant en profilage](https://msdn.microsoft.com/library/azure/ms182372.aspx) et [analyse des performances des applications à l’aide des outils de profilage](https://msdn.microsoft.com/library/azure/z9z62c29.aspx).

> [!NOTE]
> Quand vous publiez votre service cloud, activez IntelliTrace ou le profilage. Vous ne pouvez pas activer les deux méthodes.
> 
> 

### <a name="profiler-collection-methods"></a>Méthodes de collecte des données par le profileur
Vous avez le choix entre plusieurs méthodes de collecte pour le profilage, selon les problèmes de performances rencontrés :

* **Échantillonnage de l’UC** : cette méthode collecte des statistiques de l’application qui sont utiles pour l’analyse initiale des problèmes d’utilisation de l’UC. Échantillonnage de l’UC est hello méthode suggérée pour commencer la plupart des investigations sur les performances. Il existe un faible impact sur l’application hello que vous profilez lorsque vous collectez des données d’échantillonnage de l’UC.
* **Instrumentation** : cette méthode collecte des données de temporisation détaillées qui sont utiles pour l’analyse ciblée et l’analyse des problèmes de performances des entrées/sorties. méthode d’instrumentation Hello enregistre chaque entrée, sortie et appel de fonction des fonctions de hello dans un module pendant une exécution du profilage. Cette méthode est utile pour collecter des informations de temporisation détaillées à propos d’une section de votre code et pour comprendre l’impact hello d’opérations d’entrée et de sortie sur les performances de l’application. Cette méthode est désactivée sur un ordinateur exécutant un système d’exploitation 32 bits. Cette option est disponible uniquement lorsque vous exécutez le service cloud hello dans Azure, et pas localement dans l’émulateur de calcul hello.
* **Allocation de mémoire .NET** -cette méthode collecte des données d’allocation de mémoire .NET Framework en utilisant la méthode de profilage par échantillonnage hello. Hello les données collectées incluent nombre de hello et la taille des objets alloués.
* **Accès concurrentiel** : cette méthode collecte des données sur la contention de ressources, ainsi que des données sur l’exécution des threads et processus qui sont utiles pour analyser les applications multithread et multiprocessus. méthode de concurrence Hello collecte les données de chaque événement qui bloque l’exécution de votre code, notamment lorsqu’un thread attend verrouillée accès tooan application ressource toobe libérée. Cette méthode est utile pour l’analyse des applications multithread.
* Vous pouvez également activer **profilage d’Interaction de couche**, qui fournit des informations supplémentaires sur les temps d’exécution hello d’ADO.NET synchrones appelle dans des fonctions des applications multicouches qui communiquent avec un ou plusieurs bases de données. Vous pouvez collecter des données d’interaction de couche avec les méthodes de profilage de hello. Pour plus d’informations sur le profilage d’interaction de couche, consultez [Vue Interactions de couche](https://msdn.microsoft.com/library/azure/dd557764.aspx).

## <a name="configuring-profiling-settings"></a>Configuration des paramètres de profilage
Hello suivant montre l’illustration comment tooconfigure vos paramètres de profilage à partir de la boîte de dialogue Publier l’Application Azure hello.

![Configurer les paramètres de profilage](./media/vs-azure-tools-performance-profiling-cloud-services/IC526984.png)

> [!NOTE]
> tooenable hello **activer le profilage** case à cocher, vous devez disposer du Générateur de profils hello installé sur l’ordinateur local de hello que vous utilisez toopublish votre service cloud. Par défaut, le Générateur de profils hello est installé lorsque vous installez Visual Studio.
> 
> 

### <a name="tooconfigure-profiling-settings"></a>tooconfigure paramètres de profilage
1. Dans l’Explorateur de solutions, ouvrez le menu contextuel de hello pour votre projet Windows Azure, puis choisissez **publier**. Pour obtenir des instructions détaillées sur la façon toopublish un service cloud, consultez [publication d’un cloud à l’aide du service hello Windows Azure tools](http://go.microsoft.com/fwlink/p?LinkId=623012).
2. Bonjour **publier l’Application Azure** boîte de dialogue, choisissez hello **paramètres avancés** onglet.
3. tooenable de profilage, sélectionnez hello **activer le profilage** case à cocher.
4. tooconfigure vos paramètres de profilage, choisissez hello **paramètres** lien hypertexte. boîte de dialogue Paramètres de profilage Hello s’affiche.
5. À partir de hello **quelle méthode de profilage voulez-vous toouse** cases d’option, choisissez le type hello de profilage dont vous avez besoin.
6. Sélectionnez hello, les données de profilage d’interaction de couche toocollect hello **activer le profilage d’Interaction de couche** case à cocher.
7. paramètres de hello toosave, choisissez hello **OK** bouton.
   
    Lorsque vous publiez cette application, ces paramètres sont hello toocreate utilisé session pour chaque rôle de profilage.

## <a name="viewing-profiling-reports"></a>Affichage des rapports de profilage
Une session de profilage est créée pour chaque instance de rôle dans votre service cloud. tooview votre profilage signale de chaque session à partir de Visual Studio, vous pouvez afficher la fenêtre de l’Explorateur de serveurs hello, puis tooselect du nœud de calcul Windows Azure hello à une instance d’un rôle. Vous pouvez ensuite afficher hello comme indiqué dans hello suivant illustration du rapport de profilage.

![Afficher un rapport de profilage à partir d’Azure](./media/vs-azure-tools-performance-profiling-cloud-services/IC748914.png)

### <a name="tooview-profiling-reports"></a>tooview rapports de profilage
1. tooview hello Explorateur de serveurs dans Visual Studio, sur hello menu barre, sélectionnez la vue, l’Explorateur de serveurs.
2. Choisissez le nœud de calcul Azure hello, puis choisissez le nœud de déploiement Azure hello pour le service cloud hello que vous avez sélectionné tooprofile lorsque vous avez publié à partir de Visual Studio.
3. profilage de tooview rapports pour une instance, choisissez le rôle de hello dans service hello, menu contextuel hello ouvrir une instance spécifique, puis **afficher le rapport de profilage**.
   
    Hello rapport, un fichier .vsp, est maintenant téléchargé à partir d’Azure, et état de hello du téléchargement de hello s’affiche dans le journal des activités Azure de hello. Lorsque hello téléchargement terminé, hello du rapport de profilage s’affiche dans un onglet de l’éditeur pour Visual Studio nommé hello <Role name>  *<Instance Number>*  <identifier>.vsp. Données de synthèse pour les rapports hello s’affiche.
4. toodisplay différentes vues du rapport hello, dans la liste Affichage actuel hello, choisissez le type hello d’affichage que vous souhaitez. Pour plus d’informations, consultez [Vues des rapports d’outils de profilage](https://msdn.microsoft.com/library/azure/bb385755.aspx).

## <a name="next-steps"></a>Étapes suivantes
[Débogage de Cloud Services](https://msdn.microsoft.com/library/azure/ee405479.aspx)

[Publication tooan Azure Cloud Service à partir de Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)

