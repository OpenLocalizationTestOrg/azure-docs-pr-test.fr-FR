---
title: "module aaaPowerShell pour l’apprentissage | Documents Microsoft"
description: "module PowerShell de Hello pour Azure Machine Learning est disponible en version préliminaire publique. Utilisez PowerShell toocreate et gérer des espaces de travail, des expériences, des services web et bien plus encore."
keywords: "expérience,régression linéaire,algorithmes d’apprentissage automatique,didacticiel d’apprentissage automatique,techniques de modélisation prédictive,expérience de science de données"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: garye;haining
ms.openlocfilehash: 59362027356b86bf286b7c07380db677ae1d71c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a>Module PowerShell pour Microsoft Azure Machine Learning
Hello du module PowerShell pour Azure Machine Learning est un outil puissant qui vous permet d’espaces de travail toomanage toouse Windows PowerShell, expériences, jeux de données, des services web standard et bien plus encore.

Vous pouvez afficher la documentation de hello et télécharger le module de hello, ainsi que le code source complet hello à [https://aka.ms/amlps](https://aka.ms/amlps). 

> [!NOTE]
> Bonjour Azure Machine Learning module PowerShell est actuellement en mode Aperçu. module de Hello continue toobe amélioré et développé pendant cette période d’évaluation. Garder un œil sur hello [Cortana Intelligence et Machine Learning Blog](https://blogs.technet.microsoft.com/machinelearning/) nouvelles et informations.

## <a name="what-is-hello-machine-learning-powershell-module"></a>Qu’est hello Machine Learning PowerShell module ?
le module Machine Learning PowerShell Hello est un. Module DLL Internet qui vous permet de toofully gérer les espaces de travail Azure Machine Learning, expériences, des datasets, des services web classique et points de terminaison de service standard web à partir de Windows PowerShell. 

En même temps que le module de hello, vous pouvez télécharger le code source complet hello qui inclut un correctement séparés [couche API C#](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs). Vous pouvez référencer cette DLL depuis votre propre projet .NET et gérer Azure Machine Learning par le biais du code .NET. En outre, hello DLL dépend de l’API REST sous-jacentes que vous pouvez utiliser directement à partir de votre client favori.

## <a name="what-can-i-do-with-hello-powershell-module"></a>Que puis-je faire avec le module PowerShell de hello ?
Voici quelques-unes des tâches hello que vous pouvez effectuer avec ce module PowerShell. Extraire hello [complète la documentation](https://aka.ms/amlps) pour celles-ci et davantage de fonctions.

* Approvisionner un nouvel espace de travail à l’aide d’un certificat de gestion ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))
* Exporter et importer un fichier JSON représentant un graphique d’expérience ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) et [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))
* Exécuter une expérience ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))
* Créer un service web à partir d’une expérimentation prédictive ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))
* Créer un point de terminaison sur un service web publié ([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))
* Appeler un point de terminaison de service web RRS et/ou BES ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) et [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))

Voici un exemple rapide de l’utilisation de PowerShell toorun une expérience existante :

        #Find hello first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run hello Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

Pour un cas d’usage plus détaillé, consultez l’article sur l’utilisation de hello PowerShell module tooautomate une tâche couramment demandées : [créer plusieurs modèles d’apprentissage et web points de terminaison de service à partir d’une expérience à l’aide de PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).

## <a name="how-do-i-get-started"></a>Comment faire pour démarrer ?
tooget main Machine Learning PowerShell, téléchargez hello [package de version](https://github.com/hning86/azuremlps/releases) à partir de GitHub et suivez hello [instructions d’installation](https://github.com/hning86/azuremlps/blob/master/README.md). les instructions Hello expliquent comment toounblock hello téléchargé/décompressé DLL et puis l’importer dans votre environnement PowerShell. La plupart des applets de commande nécessitent que vous fournissez l’ID d’espace de travail hello, jeton d’autorisation de l’espace de travail hello et hello région Azure qui hello d’espace de travail de hello est dans. Hello la plus simple des tooprovide hello valeurs se fait via un fichier de config.json par défaut. les instructions Hello expliquent également comment tooconfigure ce fichier. 

Et si vous le souhaitez, vous pouvez cloner arborescence git de hello, modifier le code de hello et compilez-le localement à l’aide de Visual Studio.

## <a name="next-steps"></a>Étapes suivantes
Vous trouverez une documentation complète pour le module PowerShell de hello dans hello [https://aka.ms/amlps](https://aka.ms/amlps). 

Pour obtenir un exemple d’étendue de la façon dont toouse hello module dans un scénario réel, extraction hello approfondie cas d’utilisation et [créer plusieurs modèles d’apprentissage et web points de terminaison de service à partir d’une expérience à l’aide de PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).
