---
title: aaaBuild une application sans dans Visual Studio | Documents Microsoft
description: "Prise en main votre première application sans serveur avec ce guide sur la création, de déploiement et de gestion d’application hello dans Visual Studio."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a>Création d’une application dans Visual Studio à l’aide de Logic Apps et Functions

Les outils et fonctionnalités sans serveur dans Azure permettent un développement rapide et le déploiement d’applications cloud.  Ce document se concentre sur la façon de tooget démarré dans Visual Studio, créez une application sans serveur.  [Vous trouverez dans cet article](logic-apps-serverless-overview.md) une vue d’ensemble de la création d’une application sans serveur dans Azure.

## <a name="getting-everything-ready"></a>Tout préparer

Voici une application sans serveur à partir de Visual Studio hello requis toobuild :

* [Visual Studio 2017](https://www.visualstudio.com/vs/) ou Visual Studio 2015 : Communauté, Professionnel ou Entreprise
* [Outils Logic Apps pour Visual Studio](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* [Dernier kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou supérieur)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* [Outils de principaux de fonctions Azure](https://www.npmjs.com/package/azure-functions-core-tools) toodebug fonctions localement
* Web toohello d’accès lors de l’utilisation de hello incorporé Concepteur d’application logique

## <a name="getting-started-with-a-deployment-template"></a>Prise en main avec un modèle de déploiement

La gestion des ressources dans Azure est effectuée au sein d’un groupe de ressources.  Un groupe de ressources est un regroupement logique de ressources.  Les groupes de ressources permettent le déploiement et la gestion d’une collecte de ressources.  Pour une application sans serveur dans Azure, notre groupe de ressources comprend Azure Logic Apps et Azure Functions.  En utilisant le projet de groupe de ressources hello dans Visual Studio, nous sommes en mesure de toodevelop, gérer et déployer l’application entière hello en tant qu’un seul élément multimédia.

### <a name="create-a-resource-group-project-in-visual-studio"></a>Création d’un projet de groupe de ressources dans Visual Studio

1. Dans Visual Studio, cliquez sur tooadd un **nouveau projet**
1. Bonjour **Cloud** catégorie, sélectionnez toocreate Azure **groupe de ressources** projet  
 * Si vous ne voyez pas le projet répertoriés ou hello, veillez à ce que vous avez hello Azure SDK est installé pour Visual Studio
1. Donnez à hello projet un nom et un emplacement, puis sélectionnez **Ok** toocreate Visual Studio vous invite à entrer un modèle de tooselect.  Vous pouvez sélectionner toostart de démarrer avec une logique d’application, vide ou une autre ressource.  Toutefois, nous utilisons dans ce cas un tooget de modèle de démarrage rapide Azure que nous a démarré avec une application sans serveur.
1. Sélectionner les modèles de tooshow de **démarrage rapide d’Azure** ![les modèles en sélectionnant le démarrage rapide Azure][1]
1. Modèle de démarrage rapide sans Select hello : **101-logic-app-and-function-app** et cliquez sur **Ok**

modèle de démarrage rapide de Hello crée un modèle de déploiement dans votre projet de groupe de ressources.  modèle de Hello contient une application logique simple qui appelle un fonctions Azure et retourne le résultat de hello.  Si vous ouvrez hello `azuredeploy.json` fichier hello l’Explorateur de solutions, vous pouvez voir les ressources hello pour une application sans serveur hello.

## <a name="deploying-hello-serverless-application"></a>Déploiement d’application sans serveur hello

Avant de pouvoir ouvrir le concepteur visual hello application logique dans Visual Studio, il doit y toobe un groupe de ressources Azure déjà déployés.  Ainsi, toocreate de concepteur hello et utilisez connexions tooresources et services dans l’application logique de hello.  tooget démarré, il suffit de solution de hello toodeploy créée.

1. Projet de hello avec le bouton droit dans Visual Studio, sélectionnez **déployer**et créer un **nouveau** déploiement ![en sélectionnant le nouveau déploiement de ressources][2]
1. Sélectionnez un abonnement Azure et un groupe de ressources valides
1. Sélectionnez trop**déployer** hello solution
1. Entrez nom hello pour hello application logique et hello fonction l’application Azure.  nom de la fonction d’Azure Hello doit-elle toobe globalement unique.

les solutions sans serveur Hello déploiement dans le groupe de ressources spécifié hello.  Si vous examinez hello **sortie** dans Visual Studio, vous pouvez voir État hello du déploiement de hello.

## <a name="editing-hello-logic-app-in-visual-studio"></a>Modification d’application logique de hello dans Visual Studio

Une fois la solution de hello a été déployée dans n’importe quel groupe de ressources, concepteur visuel de hello pouvez tooedit utilisé et les rendre l’application de modifications toohello logique.

1. Avec le bouton hello `azuredeploy.json` fichier hello l’Explorateur de solutions et sélectionnez **ouvrir avec logique applications Designer**
1. Sélectionnez hello **groupe de ressources** et **emplacement** hello solution a été déployé tooand sélectionnez **OK**

Concepteur visuel de Hello application logique doit maintenant être visible avec Visual Studio.  Vous pouvez continuer tooadd étapes, modifier le flux de travail hello et enregistrer les modifications.  Vous pouvez également créer des applications logiques à partir de Visual Studio.  Si vous cliquez sur hello **ressources** dans le navigateur de modèle hello, vous pouvez choisir tooadd un **application logique** toohello projet.  Les applications logique vide chargent dans le concepteur visual hello sans un avant déploiement dans un groupe de ressources.

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a>Gestion et affichage de l’historique d’exécution d’une application logique déployée

Vous pouvez également gérer et afficher l’historique de hello exécuter pour les applications de logique déployées dans Azure.  Si vous ouvrez hello **Cloud Explorer** outil dans Visual Studio, vous pouvez avec le bouton droit n’importe quelle application logique et choisissez tooedit, désactiver, afficher les propriétés ou la vue de l’historique d’exécution.  En cliquant sur Modifier vous permet également toodownload une application publiée logique dans un projet de groupe de ressources Visual Studio.  Cela signifie que même si vous avez démarré la génération de votre application logique Bonjour portail Azure, vous pouvez toujours importer et gérer à partir de Visual Studio.

## <a name="developing-an-azure-function-in-visual-studio"></a>Développement d’une fonction Azure Function dans Visual Studio

modèle de déploiement Hello déploie toutes les fonctions d’Azure qui sont contenus dans la solution hello pour le référentiel git de hello spécifié dans hello `azuredeploy.json` variables.  Si vous créez un projet de fonction au sein de la solution de hello, archivez-le dans le contrôle de code source (GitHub, Visual Studio Team Services, etc.) et mettre à jour de hello `repo` variable, modèle de hello déployer hello Azure (fonction).

### <a name="creating-an-azure-function-project"></a>Création d’un projet Azure Function

Si à l’aide de JavaScript, Python, F #, un interpréteur de commandes, lot ou de PowerShell, suivez hello [étapes Bonjour fonctions CLI](../azure-functions/functions-run-local.md) toocreate un projet.  Si vous développez une fonction en c#, vous pouvez utiliser un [bibliothèque de classes c#](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) dans la solution actuelle de hello pour hello Azure (fonction).

## <a name="next-steps"></a>Étapes suivantes

* [Découvrez comment toobuild un tableau de bord social sans serveur](logic-apps-scenario-social-serverless.md)
* [Gestion d’une application logique à partir de Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Langage de définition de flux de travail d’application logique](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
