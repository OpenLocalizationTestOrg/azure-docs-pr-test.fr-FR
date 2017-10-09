---
title: aaaDebugging Azure cloud service ou machine virtuelle dans Visual Studio | Documents Microsoft
description: "Débogage d’un service cloud ou d’une machine virtuelle dans Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 945e06e0-2100-41af-b218-72347367ddab
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 32a326430021ba2ea9317a6a71fa005d4b87c273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>Débogage d'un service cloud ou d'une machine virtuelle Azure dans Visual Studio
Visual Studio vous offre différentes options de débogage des machines virtuelles et services cloud Azure.

## <a name="debug-your-cloud-service-on-your-local-computer"></a>Déboguer votre service cloud sur votre ordinateur local
Vous pouvez enregistrer temps et l’argent à l’aide de toodebug d’émulateur de calcul Azure hello votre service cloud sur un ordinateur local. Déboguer un service localement avant de le déployer vous permet d’améliorer la fiabilité et les performances, tout en évitant les coûts de temps de calcul. Certaines erreurs peuvent toutefois se produire quand vous exécutez un service cloud directement dans Azure. Vous pouvez déboguer ces erreurs si vous activez le débogage distant lorsque vous publiez votre service, puis attachez l’instance de rôle du débogueur tooa hello.

émulateur de Hello simule le service de calcul Azure hello et s’exécute dans votre environnement local afin que vous pouvez tester et déboguer votre service cloud avant de le déployer. Hello émulateur handles hello du cycle de vie de vos instances de rôle et fournit l’accès des ressources toosimulated, tels que le stockage local. Lorsque vous déboguez ou exécutez votre service à partir de Visual Studio, il démarre automatiquement émulateur de hello comme une application en arrière-plan et puis déploie un émulateur toohello de votre service. Vous pouvez utiliser hello émulateur tooview votre service lorsqu’il s’exécute dans l’environnement local de hello. Vous pouvez exécuter hello complète version ou hello express de l’émulateur de hello. (Version express de hello de l’émulateur de hello à partir de Azure 2.3, est par défaut de hello.) Consultez [tooRun d’à l’aide de l’émulateur Express et déboguer un Service Cloud localement](https://msdn.microsoft.com/library/dn339018.aspx).

### <a name="toodebug-your-cloud-service-on-your-local-computer"></a>toodebug votre cloud service sur votre ordinateur local
1. Dans la barre de menus de hello, choisissez **déboguer**, **démarrer le débogage** toorun votre projet de service cloud Azure. Vous pouvez aussi appuyer sur F5. Vous verrez un message hello émulateur de calcul démarre. Au démarrage de l’émulateur de hello, l’icône de barre d’état système hello le confirme.

    ![Émulateur Azure dans la barre d’état système hello](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)
2. Afficher l’interface utilisateur de hello pour l’émulateur de calcul hello en ouvrant le menu contextuel hello hello icône Azure dans la zone de notification hello et sélectionnez **Show Compute Emulator UI**.

    volet de gauche de Hello Hello l’interface utilisateur affiche les services de hello qui sont actuellement déployés toohello calcul émulateur et hello instances de rôle que chaque service est en cours d’exécution. Vous pouvez choisir hello service ou des rôles toodisplay cycle de vie de la journalisation et des informations de diagnostic dans le volet de droite hello. Si vous placez le focus de hello dans la marge supérieure de hello d’une fenêtre incluse, il développe le volet de droite toofill hello.
3. Étapes à l’application hello en sélectionnant les commandes hello **déboguer** menu et en définissant des points d’arrêt dans votre code. À mesure que vous parcourez l’application hello dans le débogueur de hello, les volets de hello sont mis à jour avec l’état actuel de hello de l’application hello. Lorsque vous arrêtez le débogage, le déploiement de l’application hello est supprimé. Si votre application inclut un rôle web et que vous avez défini le navigateur web hello de la propriété action hello démarrage toostart, Visual Studio démarre votre application web dans le navigateur de hello. Si vous modifiez le nombre de hello d’instances d’un rôle dans la configuration du service hello, vous devez arrêter votre service cloud et puis redémarrez le débogage afin que vous puissiez déboguer ces nouvelles instances de rôle de hello.

    **Remarque :** lorsque vous arrêtez en cours d’exécution ou débogage de votre service, hello émulateur de calcul local et l’émulateur de stockage ne sont pas arrêtés. Vous devez les arrêter explicitement à partir de la zone de notification hello.

## <a name="debug-a-cloud-service-in-azure"></a>Déboguer un service cloud dans Azure
toodebug un service cloud à partir d’un ordinateur distant, vous devez activer cette fonctionnalité explicitement lorsque vous déployez votre service cloud afin que requis (msvsmon.exe, par exemple) de services sont installés sur des machines virtuelles hello qui exécutent vos instances de rôle. Si vous n’avez pas activé le débogage distant lorsque vous avez publié le service de hello, vous avez le service de hello toorepublish avec le débogage distant activé.

L’activation du débogage distant pour un service cloud n’entraîne pas de baisse des performances, ni de coûts supplémentaires. Vous ne devez pas utiliser le débogage distant sur un service de production, car les clients qui utilisent le service de hello peuvent être compromises.

> [!NOTE]
> Lorsque vous publiez un service cloud à partir de Visual Studio, vous pouvez activer **IntelliTrace** pour tous les rôles dans ce service qui hello cible .NET Framework 4 ou hello .NET Framework 4.5. À l’aide de **IntelliTrace**, vous pouvez examiner les événements qui se sont produites dans une instance de rôle Bonjour passées et reproduire le contexte hello à ce stade. Consultez [Débogage d’un service cloud publié avec IntelliTrace et Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016) et [Utilisation d’IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx).
>
>

### <a name="tooenable-remote-debugging-for-a-cloud-service"></a>tooenable pour un service cloud du débogage distant
1. Ouvrez le menu contextuel hello hello projet Windows Azure, puis **publier**.
2. Sélectionnez hello **intermédiaire** environnement et hello **déboguer** configuration.

    Il s’agit simplement d’une indication. Vous pouvez choisir toorun vos environnements de test dans un environnement de Production. Toutefois, vous pouvez affecter les utilisateurs si vous activez le débogage distant sur l’environnement de Production hello. Vous pouvez choisir la configuration Release de hello, mais la configuration de débogage hello rend le débogage.

    ![Choisissez la configuration de débogage hello](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)
3. Suivez les étapes habituelles hello, mais sélectionnez hello **activer le débogueur distant pour tous les rôles** case à cocher sur hello **paramètres avancés** onglet.

    ![Configuration Debug](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="tooattach-hello-debugger-tooa-cloud-service-in-azure"></a>service de cloud tooattach hello débogueur tooa dans Azure
1. Dans l’Explorateur de serveurs, développez le nœud de hello pour votre service cloud.
2. Menu contextuel de hello ouverte pour le rôle de hello ou toowhich d’instance de rôle que vous souhaitez tooattach, puis sélectionnez **attacher le débogueur**.

    Si vous déboguez un rôle, le débogueur de Visual Studio hello attache instance tooeach de ce rôle. Hello s’y arrête pas sur un point d’arrêt pour hello première instance de rôle qui exécute cette ligne de code et respecte les conditions de ce point d’arrêt. Si vous déboguez une instance, hello débogueur est attaché tooonly que l’instance et s’interrompt sur un point d’arrêt uniquement lorsque cette instance spécifique exécute cette ligne de code et respecte hello les conditions du point d’arrêt.

    ![Attacher le débogueur](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)
3. Une fois que le débogueur de hello attache tooan instance, de débogage comme d’habitude. Hello est automatiquement attaché toohello des processus de l’ordinateur hôte approprié pour votre rôle. Selon quel hello est rôle, hello débogueur attache toow3wp.exe, WaWorkerHost.exe ou WaIISHost.exe. tooverify hello processus toowhich hello débogueur est attaché, développez le nœud d’instance hello dans l’Explorateur de serveurs. Pour plus d’informations sur les processus Azure, consultez [Architecture de rôle Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).

    ![Boîte de dialogue Sélectionner le type de code](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
4. tooidentify hello processus toowhich hello est associé, ouvrez hello boîte de dialogue processus, sur hello barre de menus, en choisissant le débogage, Windows, les processus. (Clavier : Ctrl + Alt + Z) toodetach un processus spécifique, ouvrez le menu contextuel et sélectionnez **détacher le processus**. Ou, recherchez le nœud d’instance hello dans l’Explorateur de serveurs, de trouver le processus de hello, ouvrez son menu contextuel, puis sélectionnez **détacher le processus**.

    ![Processus de débogage](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> Évitez les arrêts longs aux points d'arrêt avec le débogage à distance. Azure traite un processus est arrêté pendant plus de quelques minutes comme non réactif et cesse d’envoyer l’instance toothat de trafic. Si vous arrêtez pendant trop longtemps, msvsmon.exe est détaché du processus de hello.
>
>

débogueur de hello toodetach de tous les processus dans votre instance ou le rôle, le menu contextuel Ouvrir hello hello rôle ou cette instance que vous déboguez, puis sélectionnez **détacher le débogueur**.

## <a name="limitations-of-remote-debugging-in-azure"></a>Limitations du débogage distant dans Azure
À partir d’Azure SDK 2.3, le débogage distant a hello limites suivantes.

* Quand le débogage distant est activé, vous ne pouvez pas publier un service cloud dans lequel un rôle comporte plus de 25 instances.
* débogueur de Hello utilise too30424 30400 de ports, 31400 too31424 et too32424 32400. Si vous essayez toouse ces ports, vous ne serez pas en mesure de toopublish votre service et l’une des hello messages d’erreur suivants seront affiche dans le journal d’activité hello pour Azure :

  * Erreur lors de la validation du fichier .cscfg de hello sur le fichier de .csdef hello.
    Hello réservé la plage de ports 'plage' pour le point de terminaison que Microsoft.windowsazure.plugins.remotedebugger.Connector du rôle « rôle » chevauche un port déjà défini ou la plage.
  * L’allocation a échoué. Veuillez réessayer plus tard, essayez de réduire hello taille de machine virtuelle ou le nombre d’instances de rôle ou essayez de déployer tooa autre région.

## <a name="debugging-azure-virtual-machines"></a>Déboguer des machines virtuelles Azure
Vous pouvez déboguer des programmes exécutés sur des machines virtuelles Azure à l’aide de l’Explorateur de serveurs dans Visual Studio. Lorsque vous activez le débogage distant sur une machine virtuelle Azure, Azure installe l’extension hello de débogage distant sur l’ordinateur virtuel de hello. Ensuite, vous pouvez attacher tooprocesses sur l’ordinateur virtuel de hello et de débogage comme vous le feriez normalement.

> [!NOTE]
> Machines virtuelles créées par pile de gestionnaire de ressources Azure hello peuvent être débogués à distance à l’aide de l’Explorateur de Cloud dans Visual Studio 2015. Pour plus d’informations, consultez [Gestion des ressources Azure avec Cloud Explorer](http://go.microsoft.com/fwlink/?LinkId=623031).
>
>

### <a name="toodebug-an-azure-virtual-machine"></a>toodebug une machine virtuelle Azure
1. Dans l’Explorateur de serveurs, développez les nœuds de Machines virtuelles hello et sélectionnez hello de machine virtuelle de hello que vous souhaitez toodebug.
2. Ouvrez le menu contextuel de hello et sélectionnez **activer le débogage**. Lorsque le système demande si vous êtes certain que si vous souhaitez que le débogage sur l’ordinateur virtuel hello, sélectionnez tooenable **Oui**.

    Azure installe l’extension de débogage distant hello sur le débogage de tooenable hello machine virtuelle.

    ![Commande d’activation du débogage de machine virtuelle](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Journal des activités Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
3. Une fois que l’extension de débogage distant hello a terminé l’installation, ouvrez le menu contextuel de l’ordinateur virtuel de hello et sélectionnez **attacher le débogueur...**

    Azure Obtient une liste des processus de hello sur l’ordinateur virtuel de hello et les affiche dans la boîte de dialogue tooProcess hello attacher.

    ![Commande Attacher le débogueur](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
4. Bonjour **attacher tooProcess** boîte de dialogue, sélectionnez **sélectionnez** tooshow seuls les types hello la liste des résultats de hello toolimit de code vous souhaitez toodebug. Vous pouvez déboguer du code managé 32 ou 64 bits, du code natif ou les deux.

    ![Boîte de dialogue Sélectionner le type de code](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
5. Sélectionner les processus hello vous souhaitez toodebug sur l’ordinateur virtuel de hello, puis sélectionnez **attacher**. Par exemple, vous pouvez choisir le processus w3wp.exe de hello si vous souhaitiez toodebug une application web sur l’ordinateur virtuel de hello. Pour plus d’informations, consultez [Déboguer un ou plusieurs processus dans Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) et [Architecture de rôle Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>Créer un projet web et une machine virtuelle pour le débogage
Avant de publier votre projet Windows Azure, il peut s’avérer utile tootest dans un environnement contrôlé prenant en charge le débogage et scénarios de test, et où vous pouvez installer le test et surveillance des programmes. Une façon toodo il s’agit de tooremotely déboguer votre application sur un ordinateur virtuel.

Projets ASP.NET Visual Studio offrent une option toocreate une machine virtuelle que vous pouvez utiliser pour tester les applications. machine virtuelle de Hello inclut des points de terminaison généralement requis tels que PowerShell, Bureau à distance et WebDeploy.

### <a name="toocreate-a-web-project-and-a-virtual-machine-for-debugging"></a>toocreate un projet web et un ordinateur virtuel pour le débogage
1. Dans Visual Studio, créez une application web ASP.NET.
2. Dans le dialogue de nouveau projet ASP.NET hello, Bonjour section Azure, choisissez **Machine virtuelle** dans la zone de liste déroulante hello. Laissez hello **créer des ressources distantes** case à cocher activée. Sélectionnez **OK** tooproceed.

    Hello **créer un ordinateur virtuel sur Azure** boîte de dialogue s’affiche.

    ![Boîte de dialogue de création de projet web ASP.NET](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    **Remarque :** vous serez invité à indiquer toosign dans tooyour compte Azure si vous n’êtes pas déjà connecté.

1. Sélectionnez hello divers paramètres pour la machine virtuelle de hello, puis sélectionnez **OK**. Pour plus d’informations, consultez [Machines virtuelles](http://go.microsoft.com/fwlink/?LinkId=623033) .

    nom Hello que vous entrez pour le nom DNS sera nom hello de machine virtuelle de hello.

    ![Boîte de dialogue Créer une machine virtuelle sur Microsoft Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    Azure crée hello virtual machine, puis déploie et configure les points de terminaison hello, telles que le Bureau à distance et Web Deploy
2. Une fois que l’ordinateur virtuel de hello est entièrement configuré, sélectionnez le nœud de l’ordinateur virtuel de hello dans l’Explorateur de serveurs.
3. Ouvrez le menu contextuel de hello et sélectionnez **activer le débogage**. Lorsque le système demande si vous êtes certain que si vous souhaitez que le débogage sur l’ordinateur virtuel hello, sélectionnez tooenable **Oui**.

    Azure installe hello débogage extension toohello machine virtuelle tooenable débogage distant.

    ![Commande d’activation du débogage de machine virtuelle](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Journal des activités Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
4. Publiez votre projet comme décrit dans la rubrique [Déploiement d’un projet web à l’aide de la publication en un clic dans Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx). Pour que vous puissiez toodebug sur machine virtuelle hello, sur hello **paramètres** page Hello **publier le site Web** Assistant, sélectionnez **déboguer** en tant que la configuration de hello. Ceci permet de s’assurer que les symboles de code sont disponibles pendant le débogage.

    ![Paramètres de publication](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)
5. Bonjour **Options de publication du fichier**, sélectionnez **supprimer les fichiers supplémentaires à la destination** si le projet de hello a déjà été déployé à un moment antérieur.
6. Une fois le projet de hello publie, sur le menu contextuel de l’ordinateur virtuel de hello dans l’Explorateur de serveurs, sélectionnez **attacher le débogueur...**

    Azure Obtient une liste des processus de hello sur l’ordinateur virtuel de hello et les affiche dans la boîte de dialogue tooProcess hello attacher.

    ![Commande Attacher le débogueur](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
7. Bonjour **attacher tooProcess** boîte de dialogue, sélectionnez **sélectionnez** tooshow seuls les types hello la liste des résultats de hello toolimit de code vous souhaitez toodebug. Vous pouvez déboguer du code managé 32 ou 64 bits, du code natif ou les deux.

    ![Boîte de dialogue Sélectionner le type de code](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
8. Sélectionner les processus hello vous souhaitez toodebug sur l’ordinateur virtuel de hello, puis sélectionnez **attacher**. Par exemple, vous pouvez choisir le processus w3wp.exe de hello si vous souhaitiez toodebug une application web sur l’ordinateur virtuel de hello. Pour plus d’informations, consultez [Déboguer un ou plusieurs processus dans Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) .

## <a name="next-steps"></a>Étapes suivantes
* Utilisez **Intellitrace** toocollect un journal des événements à partir d’un serveur de publication et des appels. Consultez [Débogage d’un service cloud publié avec IntelliTrace et Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016).
* Utilisez **Azure Diagnostics** toolog obtenir des informations détaillées à partir de l’exécution de code dans des rôles, si les rôles hello sont en cours d’exécution dans l’environnement de développement hello ou dans Azure. Consultez [Collecter des données de journalisation avec les diagnostics Azure](http://go.microsoft.com/fwlink/p/?LinkId=400450).
