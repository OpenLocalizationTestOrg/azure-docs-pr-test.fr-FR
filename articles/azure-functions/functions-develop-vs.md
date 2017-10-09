---
title: "aaaDevelop fonctions Azure à l’aide de Visual Studio | Documents Microsoft"
description: "Découvrez comment les fonctions Azure toodevelop et de test à l’aide des fonctions de Windows Azure Tools pour Visual Studio 2017."
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a>Azure Functions Tools pour Visual Studio  

Outils de fonctions Azure pour Visual Studio 2017 est une extension pour Visual Studio qui vous permet de développer, tester et déployer des fonctions tooAzure de c#. S’il s’agit de votre première expérience avec les fonctions d’Azure, vous pouvez en savoir plus sur [un tooAzure introduction fonctions](functions-overview.md).

Hello, fonctions de Windows Azure Tools fournit hello avantages suivants : 

* Modifier, générer et exécuter des fonctions sur votre ordinateur de développement local. 
* Publier vos fonctions Azure projet directement tooAzure. 
* Utiliser des liaisons de fonction toodeclare WebJobs attributs directement dans hello code c# au lieu de maintenir un function.json distinct pour les définitions de liaison.
* Développer et déployer des fonctions précompilées C#. Les fonctions précompilées offrent de meilleures performances de démarrage à froid que les fonctions basées sur un script C#. 
* Code de vos fonctions en c# bien que tous les avantages de hello de développement Visual Studio. 

Cette rubrique vous montre comment toouse hello fonctions de Windows Azure Tools pour Visual Studio 2017 toodevelop, vos fonctions en c#. Vous apprendrez également comment toopublish tooAzure de votre projet en tant qu’un assembly .NET.

## <a name="prerequisites"></a>Composants requis

Outils de fonctions Azure est inclus dans la charge de travail de développement Azure hello de [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), ou une version ultérieure. Veillez à inclure hello **le développement Azure** la charge de travail dans votre installation de la version 15.3 Visual Studio 2017 :

![Installer Visual Studio 2017 avec une charge de travail de développement Azure hello](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

toocreate et déployer des fonctions, vous devez également :

* Un abonnement Azure actif. Si tel n’est pas le cas, des [comptes gratuits](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) sont disponibles.

* Un compte de stockage Azure. toocreate un compte de stockage, consultez [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
## <a name="create-an-azure-functions-project"></a>Créer un projet Azure Functions 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a>Configurer le projet hello pour le développement local

Lorsque vous créez un nouveau projet à l’aide du modèle de fonctions de Azure hello, vous obtenez un projet c# vide qui contient les fichiers suivants de hello :

* **Host.JSON**: permet de configurer hello hôte de fonctions. Ces paramètres s’appliquent lors de l’exécution en local et dans Azure. Pour plus d’informations, consultez l’article de référence sur [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).
    
* **local.settings.json** : maintient les paramètres utilisés lors de l’exécution des fonction en local. Ces paramètres ne sont pas utilisés par Azure, ils sont utilisés par hello [outils principaux de fonctions Azure](functions-run-local.md). Utiliser ce fichier toospecify les paramètres, tels que des chaînes de connexion tooother Azure services. Ajouter un nouveau toohello clé **valeurs** tableau pour chaque connexion requise par les fonctions dans votre projet. Pour plus d’informations, consultez [fichier de paramètres locaux](functions-run-local.md#local-settings-file) dans la rubrique des outils principaux de fonctions Azure hello.

exécution de fonctions Hello utilise un compte de stockage Azure en interne. Pour tous les déclenchent des types autres que HTTP et de webhooks, vous devez le configurer hello **Values.AzureWebJobsStorage** la clé de chaîne de connexion de compte tooa valide le stockage Azure.

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 chaîne de connexion de compte de stockage de hello de tooset :

1. Dans Visual Studio, ouvrez **Cloud Explorer**, développez **compte de stockage** > **votre compte de stockage**, puis sélectionnez **propriétés**et copie Bonjour **chaîne de connexion principal** valeur.   

2. Dans votre projet, ouvrez le fichier de projet local.settings.json hello et hello valeur hello **AzureWebJobsStorage** la clé de chaîne de connexion toohello vous avez copié.

3. Répétez hello précédente étape tooadd clés uniques toohello **valeurs** tableau de toutes les autres connexions requis par vos fonctions.  

## <a name="create-a-function"></a>Créer une fonction

Dans les fonctions précompilées, les liaisons de hello utilisées par la fonction hello sont définis en appliquant des attributs dans le code hello. Lorsque vous utilisez toocreate des fonctions de Windows Azure Tools hello vos fonctions à partir de modèles de hello fourni, ces attributs sont appliqués pour vous. 

1. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le nœud de projet et sélectionnez **Ajouter** > **Nouvel élément**. Sélectionnez **Azure fonction**, tapez un **nom** classe hello, puis cliquez sur **ajouter**.

2. Choisissez votre déclencheur, définissez des propriétés de liaison hello, puis cliquez sur **créer**. Hello suivant montre les paramètres hello au déclenchement de création d’un stockage de file d’attente (fonction). 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    Une clé de chaîne de connexion nommée **QueueStorage** est fourni, qui est défini dans le fichier de local.settings.json hello. 
 
3. Examinez hello récemment ajouté la classe. Vous consultez statique **exécuter** (méthode), qui est attribuée à hello **FunctionName** attribut. Cet attribut indique que méthode hello est le point d’entrée hello pour la fonction hello. 

    Par exemple, hello suivant classe c# représente une fonction de stockage déclenchée base file d’attente :

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    Un attribut spécifique à la liaison est la méthode de point d’entrée toohello tooeach appliqué liaison paramètre fourni. l’attribut Hello accepte les informations de liaison hello en tant que paramètres. Dans l’exemple précédent de hello, hello premier paramètre a une **QueueTrigger** attribut appliqué, qui indique la fonction de la file d’attente déclenchée. nom de file d’attente Hello et le nom de paramètre de chaîne de connexion sont passés comme paramètres.  

## <a name="testing-functions"></a>Tester les fonctions

Azure Functions Core Tools vous permet d’exécuter un projet Azure Functions sur votre ordinateur de développement local. Vous êtes invité à tooinstall ces outils hello la première fois que vous démarrez une fonction à partir de Visual Studio.  

tootest votre fonction, appuyez sur F5. Si vous y êtes invité, accepter la demande hello toodownload de Visual Studio et installez les outils de base des fonctions Azure (CLI).  Vous devez également tooenable une exception de pare-feu afin que les outils hello peuvent traiter les requêtes HTTP.

Projet hello en cours d’exécution, vous pouvez tester votre code que vous pouvez tester la fonction déployée. Pour plus d’informations, consultez [Stratégies permettant de tester votre code dans Azure Functions](functions-test-a-function.md). Lors de l’exécution en mode débogage, les points d’arrêt sont atteints dans Visual Studio comme prévu. 

Pour obtenir un exemple de la façon dont une file d’attente de tootest déclenché (fonction), consultez hello [didacticiel de démarrage rapide de file d’attente déclenchée fonction](functions-create-storage-queue-triggered-function.md#test-the-function).  

toolearn savoir plus sur l’utilisation des outils de base fonctions hello Azure, consultez [Code et tester des fonctions Azure localement](functions-run-local.md).

## <a name="publish-tooazure"></a>Publication tooAzure

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
>Tous les paramètres que vous avez ajoutée dans hello local.settings.json doivent être également ajoutés toohello fonction application dans Azure. Ces paramètres ne sont pas ajoutés automatiquement. Vous pouvez ajouter des paramètres requis tooyour fonction application dans une des manières suivantes :
>
>* [À l’aide de hello Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).
>* [À l’aide de hello `--publish-local-settings` option Bonjour Azure fonctions principaux outils de publication](functions-run-local.md#publish).
>* [À l’aide de hello CLI d’Azure](/cli/azure/functionapp/config/appsettings#set). 

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les fonctions de Windows Azure Tools, consultez hello section commun de Questions de hello [Visual Studio 2017 Tools pour les fonctions Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) billet de blog.

toolearn en savoir plus sur les fonctions principaux outils hello Azure, consultez [Code et tester des fonctions Azure localement](functions-run-local.md).  
toolearn plus sur le développement des fonctions en tant que bibliothèques de classes .NET, consultez [des bibliothèques de classes à l’aide de .NET avec des fonctions d’Azure](functions-dotnet-class-library.md). Cette rubrique fournit également des exemples de comment toouse attributs toodeclare hello différents types de liaisons prises en charge par les fonctions d’Azure.    
