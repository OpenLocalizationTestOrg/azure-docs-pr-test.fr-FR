---
title: "aaaCreate votre première fonction dans Azure à l’aide de Visual Studio | Documents Microsoft"
description: "Créer et publier un tooAzure de fonction HTTP déclenchée simple à l’aide des fonctions de Windows Azure Tools pour Visual Studio."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, traitement des événements, calcul, architecture sans serveur"
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a>Créer votre première fonction à l’aide de Visual Studio

Les fonctions Azure vous permet d’exécuter votre code dans un environnement sans serveur sans avoir toofirst créer une machine virtuelle ou publier une application web.

Dans cette rubrique, vous découvrez comment toouse hello tools de Visual Studio 2017 pour toocreate des fonctions d’Azure et tester localement une fonction de « hello world ». Vous allez ensuite publier tooAzure de code de fonction hello. Ces outils sont disponibles dans le cadre de la charge de travail de développement Azure dans Visual Studio 2017 version 15.3 hello, ou une version ultérieure.

![Code Azure Functions dans un projet Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, installer :

* [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), y compris hello **le développement Azure** la charge de travail.

    ![Installer Visual Studio 2017 avec une charge de travail de développement Azure hello](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    Une fois que vous installez ou mettez à niveau tooVisual Studio 2017 version 15.3, vous devrez peut-être outils de hello Visual Studio 2017 toomanually mises à jour pour les fonctions d’Azure. Vous pouvez mettre à jour des outils hello hello **outils** menu sous **Extensions et mises à jour...**   >  **Mises à jour** > **Visual Studio Marketplace** > **outils des travaux Web et des fonctions Azure**  >  **Mise à jour**. 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a>Créer un projet Azure Functions dans Visual Studio

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

Maintenant que vous avez créé le projet de hello, vous pouvez créer votre première fonction.

## <a name="create-hello-function"></a>Créer la fonction hello

1. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le nœud de projet et sélectionnez **Ajouter** > **Nouvel élément**. Sélectionnez **Azure Function** et cliquez sur **Ajouter**.

2. Sélectionnez **HttpTrigger**, tapez un **nom de fonction**, sélectionnez **Anonyme** pour les **Droits d’accès**, puis cliquez sur **Créer**. fonction Hello créée est accessible par une requête HTTP à partir de n’importe quel client. 

    ![Créer une fonction Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    Un fichier de code est ajouté le projet tooyour qui contient une classe qui implémente votre code de fonction. Ce code est basé sur un modèle, qui reçoit une valeur de nom, puis la renvoie. Hello **FunctionName** attribut définit le nom hello de votre fonction. Hello **HttpTrigger** attribut indique le message de type hello qui déclenche la fonction hello. 

    ![Fichier du code de fonction](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

Maintenant que vous avez créé une fonction HTTP déclenchée, vous pouvez la tester sur votre ordinateur local.

## <a name="test-hello-function-locally"></a>Tester la fonction hello localement

Azure Functions Core Tools vous permet d’exécuter un projet Azure Functions sur votre ordinateur de développement local. Vous êtes invité à tooinstall ces outils hello la première fois que vous démarrez une fonction à partir de Visual Studio.  

1. tootest votre fonction, appuyez sur F5. Si vous y êtes invité, accepter la demande hello toodownload de Visual Studio et installez les outils de base des fonctions Azure (CLI).  Vous devez également tooenable une exception de pare-feu afin que les outils hello peuvent traiter les requêtes HTTP.

2. Copier l’URL de votre fonction de l’exécution de fonctions d’Azure hello hello de sortie.  

    ![Azure runtime local](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. Collez l’URL hello pour la requête HTTP de hello dans la barre d’adresse de votre navigateur. Ajouter la chaîne de requête hello `&name=<yourname>` toothis URL et l’exécution de la demande de hello. les Voici Hello réponse de hello dans hello navigateur toohello local une demande GET retournée par la fonction hello : 

    ![Réponse de localhost de fonction dans le navigateur de hello](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. toostop de débogage, cliquez sur hello **arrêter** bouton de barre d’outils de Visual Studio hello.

Après avoir vérifié que la fonction hello s’exécute correctement sur votre ordinateur local, il est temps toopublish hello projet tooAzure.

## <a name="publish-hello-project-tooazure"></a>Publier hello projet tooAzure

Vous devez disposer d’une application de fonction dans votre abonnement Azure avant de pouvoir publier votre projet. Vous pouvez créer une application de fonction directement à partir de Visual Studio.

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a>Tester votre fonction dans Azure

1. URL de base hello copie de l’application de fonction hello à partir de la page de profil de publication hello. Remplacez hello `localhost:port` partie de l’URL de hello utilisée lors du test de fonction hello localement avec la nouvelle URL de base hello. Comme précédemment, vérifiez que chaîne de requête hello tooappend `&name=<yourname>` toothis URL et l’exécution de la demande de hello.

    URL de Hello qui appelle votre HTTP déclenchée présente de fonction comme suit :

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. Collez cette nouvelle URL de demande de hello HTTP dans la barre d’adresse de votre navigateur. les Voici Hello réponse de hello dans hello navigateur toohello à distance une demande GET retourné par la fonction hello : 

    ![Réponse de fonction dans le navigateur de hello](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a>Étapes suivantes

Vous avez utilisé l’application de fonction toocreate C# de Visual Studio avec une fonction HTTP déclenchée simple. 

+ toolearn comment tooconfigure toosupport de votre projet autres types de déclencheurs et les liaisons, consultez hello [projet hello de configurer pour le développement local](functions-develop-vs.md#configure-the-project-for-local-development) section [Azure fonctions Tools pour Visual Studio](functions-develop-vs.md).
+ toolearn en savoir plus sur le test local et de débogage à l’aide des outils de base Azure fonctions hello, consultez [Code et test, les fonctions Azure localement](functions-run-local.md). 
+ toolearn plus sur le développement des fonctions en tant que bibliothèques de classes .NET, consultez [des bibliothèques de classes à l’aide de .NET avec des fonctions d’Azure](functions-dotnet-class-library.md). 

