---
title: aaaWhat est Azure Automation | Documents Microsoft
description: "En savoir quelle valeur Azure Automation fournit et obtenir des réponses aux questions de toocommon afin que vous pouvez prise en main de création, à l’aide de procédures opérationnelles et Azure Automation DSC."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "présentation d’automatisation, azure automation, exemples d’applications d’azure automation"
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/10/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 1e5a90e272d6b2beb7b5007e2fea2c110dbd79b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-overview"></a>Vue d’ensemble d’Azure Automation
Microsoft Azure Automation fournit un moyen pour les utilisateurs tooautomate des tâches manuelles, longues, sujettes aux erreurs et répétitives hello qui sont couramment exécutées dans un environnement de cloud et d’entreprise. Il fait gagner du temps et augmente la fiabilité hello des tâches d’administration récurrentes et même les planifie toobe automatiquement effectuées à intervalles réguliers. Vous pouvez automatiser les processus à l'aide de Runbooks ou automatiser la gestion de configuration avec la Configuration de l'état souhaité (DSC, Desired State Configuration). Cet article propose une brève présentation d’Azure Automation et apporte des réponses à certaines questions courantes. Vous pouvez faire référence à tooother des articles dans cette bibliothèque pour des informations détaillées sur les différentes rubriques de hello.

## <a name="automating-processes-with-runbooks"></a>Automatisation des processus avec des Runbooks
Un Runbook est un ensemble de tâches qui exécutent des processus automatisés dans Azure Automation. Il peut être un processus simple tel que de démarrer un ordinateur virtuel et la création d’une entrée de journal, ou avoir un runbook complex qui combine des autres tooperform procédures opérationnelles plus petit un processus complexe sur plusieurs ressources ou même plusieurs clouds et les environnements sur site.  

Par exemple, peut avoir un manuel existant traiter pour la troncation d’une base de données SQL si elle approche de taille maximale qui inclut plusieurs étapes comme connexion serveur toohello, la connexion de base de données toohello, d’obtenir la taille actuelle de hello de base de données, vérifiez si seuil a dépassé tronquer et informer l’utilisateur. Au lieu d'exécuter manuellement chacune de ces étapes, vous pouvez créer un Runbook qui effectue toutes ces tâches comme un processus unique. Vous démarrez hello runbook, fournissent des informations telles que nom hello SQL server, nom de la base de données et messagerie du destinataire hello requis et sont lors hello terminée. 

## <a name="what-can-runbooks-automate"></a>Que peuvent automatiser les Runbooks ?
Comme les runbooks dans Azure Automation reposent sur PowerShell Workflow, ils peuvent accomplir tout ce que permet PowerShell. Un Runbook peut fonctionner avec toute application ou tout service disposant d'une API. Si vous avez un module PowerShell pour l’application hello, vous pouvez charger ce module dans Azure Automation et incluent les applets de commande dans votre runbook. Runbooks Azure Automation exécuter Bonjour cloud Azure et accéder aux ressources de cloud et les ressources externes qui sont accessibles à partir du cloud de hello. À l’aide de [Runbook Worker hybride](automation-hybrid-runbook-worker.md), runbooks peuvent s’exécuter dans vos données locales ressources locales de toomanage center. 

## <a name="getting-runbooks-from-hello-community"></a>Obtention de runbooks à partir de la Communauté de hello
Hello [galerie de runbooks](automation-runbook-gallery.md#runbooks-in-runbook-gallery) contient des runbooks à partir de la Communauté Microsoft et hello que vous pouvez utiliser sans modification dans votre environnement ou les personnaliser selon vos besoins. Ils sont également utiles tooas références toolearn comment toocreate vos propres runbooks. Vous pouvez même contribuer votre propre galerie toohello de runbooks que vous pensez que d’autres utilisateurs peuvent être utiles. 

## <a name="creating-runbooks-with-azure-automation"></a>Création de Runbooks avec Azure Automation
Vous pouvez [créer vos propres runbooks](automation-creating-importing-runbook.md) à partir de travail ou modifier des runbooks à partir de hello [galerie de runbooks](http://msdn.microsoft.com/library/azure/dn781422.aspx) pour vos propres exigences. Vous avez le choix entre trois [types de Runbooks](automation-runbook-types.md), en fonction de vos besoins et de votre expérience concernant PowerShell. Si vous préférez toowork directement avec hello code PowerShell, vous pouvez ensuite utiliser un [runbook PowerShell](automation-runbook-types.md#powershell-runbooks) ou [runbook PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks) que vous modifiez en mode hors connexion ou par hello [éditeurdetexte](http://msdn.microsoft.com/library/azure/dn879137.aspx) Bonjour portail Azure. Si vous préférez tooedit un runbook sans être exposé toohello sous-jacent le code, vous pouvez ensuite créer un [runbook graphique](automation-runbook-types.md#graphical-runbooks) à l’aide de hello [éditeur graphique](automation-graphical-authoring-intro.md) Bonjour portail Azure. 

Préférez la surveillance tooreading ? Jetez un œil sur hello sous la vidéo à partir de la session Microsoft Ignite de mai 2015. Remarque : Alors que hello concepts et fonctionnalités abordées dans cette vidéo sont correctes, Qu'azure Automation a beaucoup progressé depuis cette vidéo a été enregistrée, il a maintenant une interface d’utilisateur plus étendu hello portail Azure, et prend en charge des fonctionnalités supplémentaires.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3451/player]
> 
> 

## <a name="automating-configuration-management-with-desired-state-configuration"></a>Automatisation de la gestion de configuration avec la Configuration d'état souhaité
[DSC PowerShell](https://technet.microsoft.com/library/dn249912.aspx) est une plateforme de gestion qui vous permet de toomanage, déployer et appliquer la configuration pour les hôtes physiques et virtuels à l’aide d’une syntaxe déclarative de PowerShell. Vous pouvez définir des configurations sur un serveur Pull DSC central que les machines cibles peuvent extraire et appliquer automatiquement. DSC offre un ensemble d’applets de commande PowerShell que vous pouvez utiliser les ressources et les configurations de toomanage.  

[Azure Automation DSC](automation-dsc-overview.md) est une solution cloud pour DSC PowerShell qui fournit les services requis aux environnements d’entreprise.  Vous pouvez gérer vos ressources DSC dans Azure Automation et appliquer des configurations toovirtual ou des ordinateurs physiques qui les récupèrent à partir d’un serveur collecteur DSC Bonjour cloud Azure.  Il fournit également des services de création de rapports qui vous informent des événements importants, par exemple lorsque les nœuds s'écartent de leur configuration affectée et lorsqu'une nouvelle configuration a été appliquée. 

## <a name="creating-your-own-dsc-configurations-with-azure-automation"></a>Création de vos propres configurations DSC avec Azure Automation
[Les configurations DSC](automation-dsc-overview.md) spécifier l’état hello souhaité d’un nœud.  Plusieurs nœuds peuvent appliquer hello même tooassure de configuration qu’ils conservent un état identique.  Vous pouvez créer une configuration avec n'importe quel éditeur de texte sur votre machine locale, puis l'importer dans Azure Automation où vous pouvez la compiler et l'appliquer aux nœuds.

## <a name="getting-modules-and-configurations"></a>Récupération de modules et de configurations
Vous pouvez obtenir [modules PowerShell](automation-runbook-gallery.md#modules-in-powershell-gallery) contenant des applets de commande que vous pouvez utiliser dans vos runbooks et les configurations DSC à partir de hello [PowerShell Gallery](http://www.powershellgallery.com/). Vous pouvez lancer cette galerie à partir de hello portail Azure et importer des modules directement dans Azure Automation, ou vous pouvez télécharger et importer manuellement. Vous ne pouvez pas installer les modules hello directement à partir de hello portail Azure, mais vous pouvez les télécharger à les installer comme vous le feriez pour n’importe quel autre module. 

## <a name="example-practical-applications-of-azure-automation"></a>Exemples d'applications pratiques d'Azure Automation
Voici quelques exemples de quels sont les types de hello de scénarios d’automatisation avec Azure Automation. 

* Créer et copier des machines virtuelles dans différents abonnements Azure. 
* Planifier les copies de fichiers à partir d’un conteneur de stockage d’objets Blob Azure tooan ordinateur local. 
* Automatiser les fonctions de sécurité, comme refuser les requêtes d'un client lors de la détection d'une attaque par déni de service. 
* Vérifier que les machines s'alignent en permanence sur la stratégie de sécurité configurée.
* Gérer le déploiement continu du code d'application sur le cloud et sur l'infrastructure locale. 
* Créer une forêt Active Directory dans Azure pour votre environnement lab. 
* Tronquer une table dans une base de données SQL si la base de données approche de la taille maximale. 
* Mettre à jour à distance les paramètres de l’environnement d’un site web Azure. 

## <a name="how-does-azure-automation-relate-tooother-automation-tools"></a>Comment Azure Automation avec les outils d’automatisation tooother ?
[Service Management Automation (SMA)](http://technet.microsoft.com/library/dn469260.aspx) est prévue tooautomate tâches de gestion dans le cloud privé de hello. Il est installé localement dans votre centre de données en tant que composant de [Microsoft Azure Pack](https://www.microsoft.com/en-us/server-cloud/). SMA et Azure Automation utilisent hello même format de runbook basé sur Windows PowerShell et Windows PowerShell Workflow, mais ne prend pas en charge SMA [runbooks graphiques](automation-graphical-authoring-intro.md).  

[System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) est conçu pour l’automatisation de ressources locales. Il utilise un format autre que Azure Automation et Service Management Automation et un runbook de toocreate d’interface graphique sans écrire de script. Ses Runbooks sont constitués d'activités provenant de packs d'intégration spécifiquement écrits pour Orchestrator. 

## <a name="where-can-i-get-more-information"></a>Où puis-je obtenir plus d'informations ?
De nombreuses ressources sont disponibles pour vous toolearn plus d’informations sur Azure Automation, la création de vos propres runbooks. 

* **bibliothèque Azure Automation** . articles Hello dans cette bibliothèque de fournissent une documentation complète sur la configuration de hello et administration d’Azure Automation et de création de vos propres runbooks. 
* [applets de commande Azure PowerShell](http://msdn.microsoft.com/library/jj156055.aspx) fournissent des informations sur les opérations d’automatisation Azure à l’aide de Windows PowerShell. Procédures opérationnelles utilisent toowork de ces applets de commande avec des ressources Azure. 
* [Blog de l’administration](https://azure.microsoft.com/blog/tag/azure-automation/) fournit des informations les plus récentes hello sur Azure Automation et d’autres technologies de gestion de Microsoft. Vous devez vous dernière abonner toostay de blog toothis des toodate avec hello à partir de l’équipe d’Azure Automation hello. 
* [Forum d’Automation](http://go.microsoft.com/fwlink/p/?LinkId=390561) vous permet de toopost questions toobe Azure Automation traité par Microsoft et hello Communauté d’Automation. 
* [applets de commande Azure Automation](https://msdn.microsoft.com/library/mt244122.aspx) fournissent des informations pour l’automatisation des tâches d’administration. Il contient les comptes Automation de toomanage applets de commande, les ressources, les procédures opérationnelles, DSC.

## <a name="can-i-provide-feedback"></a>Puis-je fournir des commentaires ?
**Faites-nous part de vos commentaires !** Si vous recherchez un module d'intégration ou une solution de Runbook Azure Automation, envoyez une demande de script au Centre de scripts. Le cas échéant, publiez vos commentaires ou demandes de fonctionnalités pour Azure Automation sur [User Voice](http://feedback.windowsazure.com/forums/34192--general-feedback). Merci ! 

