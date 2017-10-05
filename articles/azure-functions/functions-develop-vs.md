---
title: "Développer Azure Functions à l’aide de Visual Studio | Microsoft Docs"
description: "Apprenez à développer et à tester Azure Functions à l’aide d’Azure Functions Tools pour Visual Studio 2017."
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
ms.openlocfilehash: 1e0568bc58e8879cabe409cf8e9b5866f922e7c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="366ee-103">Azure Functions Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="366ee-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="366ee-104">Azure Functions Tools pour Visual Studio 2017 est une extension pour Visual Studio qui vous permet de développer, de tester et de déployer des fonctions C# sur Azure.</span><span class="sxs-lookup"><span data-stu-id="366ee-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions to Azure.</span></span> <span data-ttu-id="366ee-105">S’il s’agit de votre première expérience avec Azure Functions, vous pouvez en apprendre davantage dans l’article [Présentation d’Azure Functions](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="366ee-105">If this is your first experience with Azure Functions, you can learn more at [An introduction to Azure Functions](functions-overview.md).</span></span>

<span data-ttu-id="366ee-106">Azure Functions Tools propose les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="366ee-106">The Azure Functions Tools provides the following benefits:</span></span> 

* <span data-ttu-id="366ee-107">Modifier, générer et exécuter des fonctions sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="366ee-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="366ee-108">Publier votre projet Azure Functions directement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="366ee-108">Publish your Azure Functions project directly to Azure.</span></span> 
* <span data-ttu-id="366ee-109">Utiliser des attributs WebJobs pour déclarer des liaisons de fonction directement dans le code C# au lieu de maintenir une fonction.json distincte pour les définitions de liaison.</span><span class="sxs-lookup"><span data-stu-id="366ee-109">Use WebJobs attributes to declare function bindings directly in the C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="366ee-110">Développer et déployer des fonctions précompilées C#.</span><span class="sxs-lookup"><span data-stu-id="366ee-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="366ee-111">Les fonctions précompilées offrent de meilleures performances de démarrage à froid que les fonctions basées sur un script C#.</span><span class="sxs-lookup"><span data-stu-id="366ee-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="366ee-112">Coder vos fonctions en C# tout en bénéficiant de tous les avantages du développement Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="366ee-112">Code your functions in C# while having all of the benefits of Visual Studio development.</span></span> 

<span data-ttu-id="366ee-113">Cette rubrique vous montre comment utiliser Azure Functions Tools pour Visual Studio 2017 afin de développer vos fonctions en C#.</span><span class="sxs-lookup"><span data-stu-id="366ee-113">This topic shows you how to use the Azure Functions Tools for Visual Studio 2017 to develop your functions in C#.</span></span> <span data-ttu-id="366ee-114">Vous apprenez également à publier votre projet sur Azure en tant qu’assembly .NET.</span><span class="sxs-lookup"><span data-stu-id="366ee-114">You also learn how to publish your project to Azure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="366ee-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="366ee-115">Prerequisites</span></span>

<span data-ttu-id="366ee-116">Azure Functions Tools est inclus dans la charge de travail de développement Azure dans [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/) ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="366ee-116">Azure Functions Tools is included in the Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="366ee-117">Veillez à inclure la charge de travail de **développement Azure** lorsque vous installez Visual Studio 2017 version 15.3 :</span><span class="sxs-lookup"><span data-stu-id="366ee-117">Make sure you include the **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![Installer Visual Studio 2017 avec la charge de travail de développement Azure](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="366ee-119">Pour créer et déployer des fonctions, vous avez également besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="366ee-119">To create and deploy functions, you also need:</span></span>

* <span data-ttu-id="366ee-120">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="366ee-120">An active Azure subscription.</span></span> <span data-ttu-id="366ee-121">Si tel n’est pas le cas, des [comptes gratuits](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="366ee-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="366ee-122">Un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="366ee-122">An Azure Storage account.</span></span> <span data-ttu-id="366ee-123">Pour créer un compte de stockage, consultez [Créez un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="366ee-123">To create a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="366ee-124">Créer un projet Azure Functions</span><span class="sxs-lookup"><span data-stu-id="366ee-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using the Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-the-project-for-local-development"></a><span data-ttu-id="366ee-125">Configurer le projet pour un développement local</span><span class="sxs-lookup"><span data-stu-id="366ee-125">Configure the project for local development</span></span>

<span data-ttu-id="366ee-126">Lorsque vous créez un projet à l’aide du modèle Azure Functions, vous obtenez un projet C# vide qui contient les fichiers suivants:</span><span class="sxs-lookup"><span data-stu-id="366ee-126">When you create a new project using the Azure Functions template, you get an empty C# project that contains the following files:</span></span>

* <span data-ttu-id="366ee-127">**host.json** : vous permet de configurer l’hôte Functions.</span><span class="sxs-lookup"><span data-stu-id="366ee-127">**host.json**: Lets you configure the Functions host.</span></span> <span data-ttu-id="366ee-128">Ces paramètres s’appliquent lors de l’exécution en local et dans Azure.</span><span class="sxs-lookup"><span data-stu-id="366ee-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="366ee-129">Pour plus d’informations, consultez l’article de référence sur [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="366ee-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="366ee-130">**local.settings.json** : maintient les paramètres utilisés lors de l’exécution des fonction en local.</span><span class="sxs-lookup"><span data-stu-id="366ee-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="366ee-131">Ces paramètres ne sont pas utilisés par Azure, ils sont utilisés par [Azure Functions Core Tools](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="366ee-131">These settings are not used by Azure, they are used by the [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="366ee-132">Utilisez ce fichier pour spécifier des paramètres, tels que des chaînes de connexion vers d’autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="366ee-132">Use this file to specify settings, such as connection strings to other Azure services.</span></span> <span data-ttu-id="366ee-133">Ajoutez une clé au tableau **Valeurs** pour chaque connexion requise par les fonctions dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="366ee-133">Add a new key to the **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="366ee-134">Pour plus d’informations, consultez [Local settings file](functions-run-local.md#local-settings-file) (Fichier de paramètres local) dans la rubrique Procédure locale de codage et de test d’Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="366ee-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in the Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="366ee-135">Le runtime de Functions utilise un compte de stockage Azure en interne.</span><span class="sxs-lookup"><span data-stu-id="366ee-135">The Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="366ee-136">Pour tous les types de déclencheur autres que HTTP et webhooks, vous devez définir la clé **Values.AzureWebJobsStorage** sur une chaîne de connexion de compte de stockage Azure valide.</span><span class="sxs-lookup"><span data-stu-id="366ee-136">For all trigger types other than HTTP and webhooks, you must set the **Values.AzureWebJobsStorage** key to a valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="366ee-137">Pour définir la chaîne de connexion de compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="366ee-137">To set the storage account connection string:</span></span>

1. <span data-ttu-id="366ee-138">Dans Visual Studio, ouvrez **Cloud Explorer**, développez **Compte de stockage** > **Votre compte de stockage**, puis sélectionnez **Propriétés** et copiez la valeur **Chaîne de connexion principale**.</span><span class="sxs-lookup"><span data-stu-id="366ee-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy the **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="366ee-139">Dans votre projet, ouvrez le fichier de projet local.settings.json et définissez la valeur de la clé **AzureWebJobsStorage** sur la chaîne de connexion que vous avez copiée.</span><span class="sxs-lookup"><span data-stu-id="366ee-139">In your project, open the local.settings.json project file and set the value of the **AzureWebJobsStorage** key to the connection string you copied.</span></span>

3. <span data-ttu-id="366ee-140">Répétez l’étape précédente pour ajouter des clés uniques au tableau **Valeurs** pour les autres connexions requises par vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="366ee-140">Repeat the previous step to add unique keys to the **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="366ee-141">Créer une fonction</span><span class="sxs-lookup"><span data-stu-id="366ee-141">Create a function</span></span>

<span data-ttu-id="366ee-142">Dans les fonctions précompilées, les liaisons utilisées par la fonction sont définies en appliquant des attributs dans le code.</span><span class="sxs-lookup"><span data-stu-id="366ee-142">In pre-compiled functions, the bindings used by the function are defined by applying attributes in the code.</span></span> <span data-ttu-id="366ee-143">Lorsque vous utilisez Azure Functions Tools pour créer vos fonctions à partir des modèles fournis, ces attributs sont appliqués pour vous.</span><span class="sxs-lookup"><span data-stu-id="366ee-143">When you use the Azure Functions Tools to create your functions from the provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="366ee-144">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le nœud de projet et sélectionnez **Ajouter** > **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="366ee-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="366ee-145">Sélectionnez **Fonction Azure**, tapez un **nom** pour la classe, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="366ee-145">Select **Azure Function**, type a **Name** for the class, and click **Add**.</span></span>

2. <span data-ttu-id="366ee-146">Choisissez votre déclencheur, définissez les propriétés de liaison, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="366ee-146">Choose your trigger, set the binding properties, and click **Create**.</span></span> <span data-ttu-id="366ee-147">L’exemple suivant montre les paramètres lors de la création d’une fonction déclenchée par le stockage File d’attente.</span><span class="sxs-lookup"><span data-stu-id="366ee-147">The following example shows the settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="366ee-148">Une clé de chaîne de connexion nommée **QueueStorage** est fournie, qui est définie dans le fichier local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="366ee-148">A connection string key named **QueueStorage** is supplied, which is defined in the local.settings.json file.</span></span> 
 
3. <span data-ttu-id="366ee-149">Examinez la classe qui vient d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="366ee-149">Examine the newly added class.</span></span> <span data-ttu-id="366ee-150">Vous voyez une méthode statique **Run**, qui est attribuée avec l’attribut **FunctionName**.</span><span class="sxs-lookup"><span data-stu-id="366ee-150">You see a static **Run** method, that is attributed with the **FunctionName** attribute.</span></span> <span data-ttu-id="366ee-151">Cet attribut indique que la méthode est le point d’entrée de la fonction.</span><span class="sxs-lookup"><span data-stu-id="366ee-151">This attribute indicates that the method is the entry point for the function.</span></span> 

    <span data-ttu-id="366ee-152">Par exemple, la classe C# suivante représente une fonction de stockage déclenchée par le stockage File d’attente :</span><span class="sxs-lookup"><span data-stu-id="366ee-152">For example, the following C# class represents a basic Queue storage triggered function:</span></span>

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
 
    <span data-ttu-id="366ee-153">Un attribut spécifique à la liaison est appliqué à chaque paramètre de liaison fourni à la méthode de point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="366ee-153">A binding-specific attribute is applied to each binding parameter supplied to the entry point method.</span></span> <span data-ttu-id="366ee-154">L’attribut accepte les informations de liaison en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="366ee-154">The attribute takes the binding information as parameters.</span></span> <span data-ttu-id="366ee-155">Dans l’exemple précédent, le premier paramètre a un attribut **QueueTrigger** appliqué, qui indique la fonction déclenchée par la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="366ee-155">In the previous example, The first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="366ee-156">Le nom de la file d’attente et le nom du paramètre de la chaîne de connexion sont transmis en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="366ee-156">The queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="366ee-157">Tester les fonctions</span><span class="sxs-lookup"><span data-stu-id="366ee-157">Testing functions</span></span>

<span data-ttu-id="366ee-158">Azure Functions Core Tools vous permet d’exécuter un projet Azure Functions sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="366ee-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="366ee-159">Vous êtes invité à installer ces outils la première fois que vous démarrez une fonction dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="366ee-159">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="366ee-160">Pour tester votre fonction, appuyez sur F5.</span><span class="sxs-lookup"><span data-stu-id="366ee-160">To test your function, press F5.</span></span> <span data-ttu-id="366ee-161">Si vous y êtes invité, acceptez la requête dans Visual Studio pour télécharger et installer Azure Functions Core (CLI) Tools.</span><span class="sxs-lookup"><span data-stu-id="366ee-161">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="366ee-162">Vous devrez peut-être activer une exception de pare-feu afin de permettre aux outils de prendre en charge les requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="366ee-162">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

<span data-ttu-id="366ee-163">Avec le projet en cours d’exécution, vous pouvez tester votre code comme vous testeriez la fonction déployée.</span><span class="sxs-lookup"><span data-stu-id="366ee-163">With the project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="366ee-164">Pour plus d’informations, consultez [Stratégies permettant de tester votre code dans Azure Functions](functions-test-a-function.md).</span><span class="sxs-lookup"><span data-stu-id="366ee-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="366ee-165">Lors de l’exécution en mode débogage, les points d’arrêt sont atteints dans Visual Studio comme prévu.</span><span class="sxs-lookup"><span data-stu-id="366ee-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="366ee-166">Pour obtenir un exemple montrant comment tester une fonction déclenchée par une file d’attente, consultez le [didacticiel de démarrage rapide sur une fonction déclenchée par une file d’attente](functions-create-storage-queue-triggered-function.md#test-the-function).</span><span class="sxs-lookup"><span data-stu-id="366ee-166">For an example of how to test a queue triggered function, see the [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="366ee-167">Pour en savoir plus sur l’utilisation d’Azure Functions Core Tools, consultez [Procédure locale de codage et de test d’Azure Functions](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="366ee-167">To learn more about using the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-to-azure"></a><span data-ttu-id="366ee-168">Publication dans Azure</span><span class="sxs-lookup"><span data-stu-id="366ee-168">Publish to Azure</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="366ee-169">Les paramètres que vous avez ajoutés au fichier local.settings.json doivent être également ajoutés à l’application de fonction dans Azure.</span><span class="sxs-lookup"><span data-stu-id="366ee-169">Any settings you added in the local.settings.json must be also added to the function app in Azure.</span></span> <span data-ttu-id="366ee-170">Ces paramètres ne sont pas ajoutés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="366ee-170">These settings are not added automatically.</span></span> <span data-ttu-id="366ee-171">Vous pouvez ajouter les paramètres requis à votre application de fonction de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="366ee-171">You can add required settings to your function app in one of these ways:</span></span>
>
>* <span data-ttu-id="366ee-172">[Utilisation du portail Azure](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="366ee-172">[Using the Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="366ee-173">[Utilisation de l’option de publication `--publish-local-settings` dans Azure Functions Core Tools](functions-run-local.md#publish).</span><span class="sxs-lookup"><span data-stu-id="366ee-173">[Using the `--publish-local-settings` publish option in the Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="366ee-174">[Utilisation de l’interface CLI Azure](/cli/azure/functionapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="366ee-174">[Using the Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="366ee-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="366ee-175">Next steps</span></span>

<span data-ttu-id="366ee-176">Pour plus d’informations sur Azure Functions Tools, consultez la section Common Questions (Questions courantes) de l’article de blog [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) (Visual Studio 2017 Tools pour Azure Functions).</span><span class="sxs-lookup"><span data-stu-id="366ee-176">For more information about Azure Functions Tools, see the Common Questions section of the [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="366ee-177">Pour en savoir plus sur Azure Functions Core Tools, consultez [Procédure locale de codage et de test d’Azure Functions](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="366ee-177">To learn more about the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="366ee-178">Pour en savoir plus sur le développement de fonctions en tant que bibliothèques de classes .NET, consultez [Utilisation de bibliothèques de classes .NET avec Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="366ee-178">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="366ee-179">Cette rubrique fournit également des exemples d’utilisation d’attributs pour déclarer les différents types de liaisons pris en charge par Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="366ee-179">This topic also provides examples of how to use attributes to declare the various types of bindings supported by Azure Functions.</span></span>    
