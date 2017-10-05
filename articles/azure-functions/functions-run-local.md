---
title: "Développer et exécuter des fonctions Azure en local | Microsoft Docs"
description: "Apprenez à coder et à tester des fonctions Azure sur votre ordinateur local avant de les exécuter dans Azure Functions."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: bbe03973dbd7c70463caa6d1a45efae2ec722c05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="8c27a-103">Coder et tester des fonctions Azure localement</span><span class="sxs-lookup"><span data-stu-id="8c27a-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="8c27a-104">Bien que le [portail Azure] fournisse un ensemble complet d’outils pour le développement et le test d’Azure Functions, nombreux sont les développeurs qui privilégient une expérience de développement local.</span><span class="sxs-lookup"><span data-stu-id="8c27a-104">While the [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="8c27a-105">Azure Functions facilite l’utilisation de votre éditeur de code et de vos outils de développement local préférés pour développer et tester vos fonctions sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="8c27a-105">Azure Functions makes it easy to use your favorite code editor and local development tools to develop and test your functions on your local computer.</span></span> <span data-ttu-id="8c27a-106">Vos fonctions peuvent se déclencher sur des événements dans Azure, et vous pouvez déboguer vos fonctions C# et JavaScript sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="8c27a-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="8c27a-107">Si vous êtes un développeur Visual Studio C#, Azure Functions [s’intègre aussi à Visual Studio 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="8c27a-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-the-azure-functions-core-tools"></a><span data-ttu-id="8c27a-108">Installer Azure Functions Core Tools</span><span class="sxs-lookup"><span data-stu-id="8c27a-108">Install the Azure Functions Core Tools</span></span>

<span data-ttu-id="8c27a-109">Azure Functions Core Tools est une version locale du runtime Azure Functions que vous pouvez exécuter sur votre ordinateur Windows local.</span><span class="sxs-lookup"><span data-stu-id="8c27a-109">Azure Functions Core Tools is a local version of the Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="8c27a-110">Ce n’est pas un émulateur ni un simulateur.</span><span class="sxs-lookup"><span data-stu-id="8c27a-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="8c27a-111">Il s’agit du même runtime que celui qui alimente les fonctions dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8c27a-111">It's the same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="8c27a-112">[Azure Functions Core Tools] est fourni en tant que package npm.</span><span class="sxs-lookup"><span data-stu-id="8c27a-112">The [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="8c27a-113">Vous devez d’abord [installer NodeJS](https://docs.npmjs.com/getting-started/installing-node), qui inclut npm.</span><span class="sxs-lookup"><span data-stu-id="8c27a-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="8c27a-114">À ce stade, le package Azure Functions Core Tools ne peut être installé que sur les ordinateurs Windows.</span><span class="sxs-lookup"><span data-stu-id="8c27a-114">At this time, the Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="8c27a-115">Cette restriction est due à une limitation temporaire dans l’hôte d’Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="8c27a-115">This restriction is due to a temporary limitation in the Functions host.</span></span>

<span data-ttu-id="8c27a-116">[Azure Functions Core Tools] ajoute les alias de commande suivants :</span><span class="sxs-lookup"><span data-stu-id="8c27a-116">[Azure Functions Core Tools] adds the following command aliases:</span></span>
* <span data-ttu-id="8c27a-117">**func**</span><span class="sxs-lookup"><span data-stu-id="8c27a-117">**func**</span></span>
* <span data-ttu-id="8c27a-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="8c27a-118">**azfun**</span></span>
* <span data-ttu-id="8c27a-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="8c27a-119">**azurefunctions**</span></span>

<span data-ttu-id="8c27a-120">Ces alias peuvent être utilisés à la place de `func` indiqué dans les exemples de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="8c27a-120">All of these alias can be used instead of `func` shown in the examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="8c27a-121">Créer un projet Functions local</span><span class="sxs-lookup"><span data-stu-id="8c27a-121">Create a local Functions project</span></span>

<span data-ttu-id="8c27a-122">Quand il est exécuté localement, un projet Functions est un répertoire qui contient les fichiers host.json et local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="8c27a-122">When running locally, a Functions project is a directory that has the files host.json and local.settings.json.</span></span> <span data-ttu-id="8c27a-123">Ce répertoire est l’équivalent d’une application de fonction dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8c27a-123">This directory is the equivalent of a function app in Azure.</span></span> <span data-ttu-id="8c27a-124">Pour plus d’informations sur la structure de dossiers Azure Functions, consultez le [Guide de développement Azure Functions](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="8c27a-124">To learn more about the Azure Functions folder structure, see the [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="8c27a-125">Depuis une invite de commandes, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8c27a-125">At a command prompt, run the following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="8c27a-126">La sortie ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8c27a-126">The output looks like the following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="8c27a-127">Pour ne pas créer de dépôt Git, utilisez l’option `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="8c27a-127">To opt out of creating a Git repository, use the option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="8c27a-128">Fichier de paramètres locaux</span><span class="sxs-lookup"><span data-stu-id="8c27a-128">Local settings file</span></span>

<span data-ttu-id="8c27a-129">Le fichier local.settings.json stocke les paramètres de l’application, les chaînes de connexion et les paramètres d’Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="8c27a-129">The file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="8c27a-130">Sa structure est la suivante :</span><span class="sxs-lookup"><span data-stu-id="8c27a-130">It has the following structure:</span></span>

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| <span data-ttu-id="8c27a-131">Paramètre</span><span class="sxs-lookup"><span data-stu-id="8c27a-131">Setting</span></span>      | <span data-ttu-id="8c27a-132">Description</span><span class="sxs-lookup"><span data-stu-id="8c27a-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="8c27a-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="8c27a-133">**IsEncrypted**</span></span> | <span data-ttu-id="8c27a-134">Lorsque la valeur est définie sur **true**, toutes les valeurs sont chiffrées à l’aide d’une clé d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="8c27a-134">When set to **true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="8c27a-135">Utilisé avec les commandes `func settings`.</span><span class="sxs-lookup"><span data-stu-id="8c27a-135">Used with `func settings` commands.</span></span> <span data-ttu-id="8c27a-136">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="8c27a-136">Default value is **false**.</span></span> |
| <span data-ttu-id="8c27a-137">**Valeurs**</span><span class="sxs-lookup"><span data-stu-id="8c27a-137">**Values**</span></span> | <span data-ttu-id="8c27a-138">Collection de paramètres d’application utilisés lors de l’exécution locale.</span><span class="sxs-lookup"><span data-stu-id="8c27a-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="8c27a-139">Ajoutez les paramètres de votre application à cet objet.</span><span class="sxs-lookup"><span data-stu-id="8c27a-139">Add your application settings to this object.</span></span>  |
| <span data-ttu-id="8c27a-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="8c27a-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="8c27a-141">Définit la chaîne de connexion sur le compte Stockage Azure qui est utilisé en interne par le runtime Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="8c27a-141">Sets the connection string to the Azure Storage account that is used internally by the Azure Functions runtime.</span></span> <span data-ttu-id="8c27a-142">Le compte de stockage prend en charge les déclencheurs de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="8c27a-142">The storage account supports your function's triggers.</span></span> <span data-ttu-id="8c27a-143">Ce paramètre de connexion du compte de stockage est requis pour toutes les fonctions à l’exception des fonctions déclenchées par HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c27a-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="8c27a-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="8c27a-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="8c27a-145">Définit la chaîne de connexion sur le compte Stockage Azure qui est utilisé pour stocker les journaux de fonction.</span><span class="sxs-lookup"><span data-stu-id="8c27a-145">Sets the connection string to the Azure Storage account that is used to store the function logs.</span></span> <span data-ttu-id="8c27a-146">Cette valeur facultative rend les journaux accessibles dans le portail.</span><span class="sxs-lookup"><span data-stu-id="8c27a-146">This optional value makes the logs accessible in the portal.</span></span>|
| <span data-ttu-id="8c27a-147">**Hôte**</span><span class="sxs-lookup"><span data-stu-id="8c27a-147">**Host**</span></span> | <span data-ttu-id="8c27a-148">Les paramètres de cette section personnalisent le processus hôte Functions lors de l’exécution locale.</span><span class="sxs-lookup"><span data-stu-id="8c27a-148">Settings in this section customize the Functions host process when running locally.</span></span> | 
| <span data-ttu-id="8c27a-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="8c27a-149">**LocalHttpPort**</span></span> | <span data-ttu-id="8c27a-150">Définit le port par défaut utilisé lors de l’exécution de l’hôte Functions local (`func host start` et `func run`).</span><span class="sxs-lookup"><span data-stu-id="8c27a-150">Sets the default port used when running the local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="8c27a-151">L’option de ligne de commande `--port` est prioritaire sur cette valeur.</span><span class="sxs-lookup"><span data-stu-id="8c27a-151">The `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="8c27a-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="8c27a-152">**CORS**</span></span> | <span data-ttu-id="8c27a-153">Définit les origines autorisées pour [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="8c27a-153">Defines the origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="8c27a-154">Les origines sont fournies sous la forme d’une liste séparée par des virgules, sans espaces.</span><span class="sxs-lookup"><span data-stu-id="8c27a-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="8c27a-155">La valeur de caractère générique (**\***) est prise en charge, ce qui autorise les demandes à partir de n’importe quelle origine.</span><span class="sxs-lookup"><span data-stu-id="8c27a-155">The wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="8c27a-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="8c27a-156">**ConnectionStrings**</span></span> | <span data-ttu-id="8c27a-157">Contient les chaînes de connexion de base de données pour vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="8c27a-157">Contains the database connection strings for your functions.</span></span> <span data-ttu-id="8c27a-158">Les chaînes de connexion dans cet objet sont ajoutées à l’environnement avec le type de fournisseur **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="8c27a-158">Connection strings in this object are added to the environment with the provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="8c27a-159">La plupart des déclencheurs et des liaisons ont une propriété **Connection** qui correspond au nom d’une variable d’environnement ou d’un paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="8c27a-159">Most triggers and bindings have a **Connection** property that maps to the name of an environment variable or app setting.</span></span> <span data-ttu-id="8c27a-160">Pour chaque propriété de connexion, un paramètre d’application doit être défini dans le fichier local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="8c27a-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="8c27a-161">Ces paramètres peuvent aussi être lus dans votre code en tant que variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="8c27a-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="8c27a-162">Dans C#, utilisez [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) ou [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c27a-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="8c27a-163">En JavaScript, utilisez `process.env`.</span><span class="sxs-lookup"><span data-stu-id="8c27a-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="8c27a-164">Les paramètres spécifiés comme variable d’environnement système sont prioritaires sur les valeurs contenues dans le fichier local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="8c27a-164">Settings specified as a system environment variable take precedence over values in the local.settings.json file.</span></span> 

<span data-ttu-id="8c27a-165">Les paramètres dans le fichier local.settings.json sont uniquement utilisés par les outils Functions lors de l’exécution locale.</span><span class="sxs-lookup"><span data-stu-id="8c27a-165">Settings in the local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="8c27a-166">Par défaut, ces paramètres ne sont pas migrés automatiquement lorsque le projet est publié dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8c27a-166">By default, these settings are not migrated automatically when the project is published to Azure.</span></span> <span data-ttu-id="8c27a-167">Utilisez le commutateur `--publish-local-settings` [lors de la publication](#publish) pour vous assurer que ces paramètres sont ajoutés à l’application de fonction dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8c27a-167">Use the `--publish-local-settings` switch [when you publish](#publish) to make sure these settings are added to the function app in Azure.</span></span>

<span data-ttu-id="8c27a-168">Si aucune chaîne de connexion de stockage valide n’est définie pour **AzureWebJobsStorage**, le message d’erreur suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="8c27a-168">When no valid storage connection string is set for **AzureWebJobsStorage**, the following error message is shown:</span></span>  

><span data-ttu-id="8c27a-169">Valeur manquante pour AzureWebJobsStorage dans local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="8c27a-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="8c27a-170">Cette valeur est nécessaire pour tous les déclencheurs autres que HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c27a-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="8c27a-171">Vous pouvez exécuter 'func azure functionary fetch-app-settings <functionAppName>' ou spécifier une chaîne de connexion dans local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="8c27a-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="8c27a-172">Configuration des paramètres d’application</span><span class="sxs-lookup"><span data-stu-id="8c27a-172">Configure app settings</span></span>

<span data-ttu-id="8c27a-173">Pour définir une valeur pour des chaînes de connexion, vous pouvez effectuer une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c27a-173">To set a value for connection strings, you can do one of the following:</span></span>
* <span data-ttu-id="8c27a-174">Entrez la chaîne de connexion à partir de [l’Explorateur de stockage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8c27a-174">Enter the connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="8c27a-175">Utilisez l’une des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c27a-175">Use one of the following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="8c27a-176">Les deux commandes nécessitent que vous vous connectiez d’abord à Azure.</span><span class="sxs-lookup"><span data-stu-id="8c27a-176">Both commands require you to first sign-in to Azure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="8c27a-177">Créer une fonction</span><span class="sxs-lookup"><span data-stu-id="8c27a-177">Create a function</span></span>

<span data-ttu-id="8c27a-178">Exécutez la commande suivante pour créer une fonction :</span><span class="sxs-lookup"><span data-stu-id="8c27a-178">To create a function, run the following command:</span></span>

```
func new
``` 
<span data-ttu-id="8c27a-179">`func new` prend en charge les arguments facultatifs suivants :</span><span class="sxs-lookup"><span data-stu-id="8c27a-179">`func new` supports the following optional arguments:</span></span>

| <span data-ttu-id="8c27a-180">Argument</span><span class="sxs-lookup"><span data-stu-id="8c27a-180">Argument</span></span>     | <span data-ttu-id="8c27a-181">Description</span><span class="sxs-lookup"><span data-stu-id="8c27a-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="8c27a-182">Langage de programmation du modèle, tel que C#, F# ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8c27a-182">The template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="8c27a-183">Nom du modèle.</span><span class="sxs-lookup"><span data-stu-id="8c27a-183">The template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="8c27a-184">Nom de la fonction.</span><span class="sxs-lookup"><span data-stu-id="8c27a-184">The function name.</span></span> |

<span data-ttu-id="8c27a-185">Par exemple, pour créer un déclencheur HTTP JavaScript, exécutez :</span><span class="sxs-lookup"><span data-stu-id="8c27a-185">For example, to create a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="8c27a-186">Pour créer une fonction déclenchée par une file d’attente, exécutez :</span><span class="sxs-lookup"><span data-stu-id="8c27a-186">To create a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="8c27a-187">Exécuter des fonctions localement</span><span class="sxs-lookup"><span data-stu-id="8c27a-187">Run functions locally</span></span>

<span data-ttu-id="8c27a-188">Pour exécuter un projet Functions, exécutez l’hôte Functions.</span><span class="sxs-lookup"><span data-stu-id="8c27a-188">To run a Functions project, run the Functions host.</span></span> <span data-ttu-id="8c27a-189">L’hôte active les déclencheurs pour toutes les fonctions du projet :</span><span class="sxs-lookup"><span data-stu-id="8c27a-189">The host enables triggers for all functions in the project:</span></span>

```
func host start
```

<span data-ttu-id="8c27a-190">`func host start` prend en charge les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c27a-190">`func host start` supports the following options:</span></span>

| <span data-ttu-id="8c27a-191">Option</span><span class="sxs-lookup"><span data-stu-id="8c27a-191">Option</span></span>     | <span data-ttu-id="8c27a-192">Description</span><span class="sxs-lookup"><span data-stu-id="8c27a-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="8c27a-193">Port local à écouter.</span><span class="sxs-lookup"><span data-stu-id="8c27a-193">The local port to listen on.</span></span> <span data-ttu-id="8c27a-194">Valeur par défaut : 7071.</span><span class="sxs-lookup"><span data-stu-id="8c27a-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="8c27a-195">Les options sont `VSCode` et `VS`.</span><span class="sxs-lookup"><span data-stu-id="8c27a-195">The options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="8c27a-196">Liste séparée par des virgules d’origines CORS, sans espaces.</span><span class="sxs-lookup"><span data-stu-id="8c27a-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="8c27a-197">Port du débogueur de nœud à utiliser.</span><span class="sxs-lookup"><span data-stu-id="8c27a-197">The port for the node debugger to use.</span></span> <span data-ttu-id="8c27a-198">Valeur par défaut : une valeur issue de launch.json ou 5858.</span><span class="sxs-lookup"><span data-stu-id="8c27a-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="8c27a-199">Niveau de trace de la console (off, verbose, info, warning ou error).</span><span class="sxs-lookup"><span data-stu-id="8c27a-199">The console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="8c27a-200">Valeur par défaut : info.</span><span class="sxs-lookup"><span data-stu-id="8c27a-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="8c27a-201">Délai d’expiration pour le démarrage de l’hôte Functions, en secondes.</span><span class="sxs-lookup"><span data-stu-id="8c27a-201">The time out for the Functions host t     o start, in seconds.</span></span> <span data-ttu-id="8c27a-202">Valeur par défaut : 20 secondes.</span><span class="sxs-lookup"><span data-stu-id="8c27a-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="8c27a-203">Établir une liaison avec https://localhost:{port} plutôt qu’avec http://localhost:{port}.</span><span class="sxs-lookup"><span data-stu-id="8c27a-203">Bind to https://localhost:{port} rather than to http://localhost:{port}.</span></span> <span data-ttu-id="8c27a-204">Par défaut, cette option crée un certificat de confiance sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8c27a-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="8c27a-205">Marquage d’une pause pour des entrées supplémentaires avant de quitter le processus.</span><span class="sxs-lookup"><span data-stu-id="8c27a-205">Pause for additional input before exiting the process.</span></span> <span data-ttu-id="8c27a-206">Utile au lancement d’Azure Functions Core Tools à partir d’un environnement de développement intégré (IDE).</span><span class="sxs-lookup"><span data-stu-id="8c27a-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="8c27a-207">Quand l’hôte Functions démarre, il génère l’URL des fonctions déclenchées par HTTP :</span><span class="sxs-lookup"><span data-stu-id="8c27a-207">When the Functions host starts, it outputs the URL of HTTP-triggered functions:</span></span>

```
Found the following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="8c27a-208">Débogage dans VS Code ou Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8c27a-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="8c27a-209">Pour joindre un débogueur, passez l’argument `--debug`.</span><span class="sxs-lookup"><span data-stu-id="8c27a-209">To attach a debugger, pass the `--debug` argument.</span></span> <span data-ttu-id="8c27a-210">Pour déboguer des fonctions JavaScript, utilisez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8c27a-210">To debug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="8c27a-211">Pour les fonctions C#, utilisez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c27a-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="8c27a-212">Pour déboguer des fonctions C#, utilisez `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="8c27a-212">To debug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="8c27a-213">Vous pouvez également utiliser [Visual Studio 2017 Tools pour Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="8c27a-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="8c27a-214">Pour lancer l’hôte et configurer le débogage JavaScript, exécutez :</span><span class="sxs-lookup"><span data-stu-id="8c27a-214">To launch the host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="8c27a-215">Ensuite, dans Visual Studio Code, dans la vue **Déboguer**, sélectionnez **Attacher à Azure Functions**.</span><span class="sxs-lookup"><span data-stu-id="8c27a-215">Then, in Visual Studio Code, in the **Debug** view, select **Attach to Azure Functions**.</span></span> <span data-ttu-id="8c27a-216">Vous pouvez joindre des points d’arrêt, inspecter des variables et parcourir le code.</span><span class="sxs-lookup"><span data-stu-id="8c27a-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Débogage JavaScript avec Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-to-a-function"></a><span data-ttu-id="8c27a-218">Transmission de données de test à une fonction</span><span class="sxs-lookup"><span data-stu-id="8c27a-218">Passing test data to a function</span></span>

<span data-ttu-id="8c27a-219">Vous pouvez également appeler une fonction directement à l’aide de `func run <FunctionName>` et fournir des données d’entrée pour la fonction.</span><span class="sxs-lookup"><span data-stu-id="8c27a-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for the function.</span></span> <span data-ttu-id="8c27a-220">Cette commande est similaire à l’exécution d’une fonction à l’aide de l’onglet **Test** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8c27a-220">This command is similar to running a function using the **Test** tab in the Azure portal.</span></span> <span data-ttu-id="8c27a-221">Cette commande lance l’intégralité de l’hôte Functions.</span><span class="sxs-lookup"><span data-stu-id="8c27a-221">This command launches the entire Functions host.</span></span>

<span data-ttu-id="8c27a-222">`func run` prend en charge les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c27a-222">`func run` supports the following options:</span></span>

| <span data-ttu-id="8c27a-223">Option</span><span class="sxs-lookup"><span data-stu-id="8c27a-223">Option</span></span>     | <span data-ttu-id="8c27a-224">Description</span><span class="sxs-lookup"><span data-stu-id="8c27a-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="8c27a-225">Contenu inclus.</span><span class="sxs-lookup"><span data-stu-id="8c27a-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="8c27a-226">Joindre un débogueur au processus hôte avant d’exécuter la fonction.</span><span class="sxs-lookup"><span data-stu-id="8c27a-226">Attach a debugger to the host process before running the function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="8c27a-227">Délai d’attente (en secondes) jusqu’à ce que l’hôte Functions local soit prêt.</span><span class="sxs-lookup"><span data-stu-id="8c27a-227">Time to wait (in seconds) until the local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="8c27a-228">Nom du fichier à utiliser en tant que contenu.</span><span class="sxs-lookup"><span data-stu-id="8c27a-228">The file name to use as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="8c27a-229">Ne pas demander d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8c27a-229">Does not prompt for input.</span></span> <span data-ttu-id="8c27a-230">Utile pour les scénarios d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="8c27a-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="8c27a-231">Par exemple, pour appeler une fonction déclenchée par HTTP et passer un corps de contenu, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8c27a-231">For example, to call an HTTP-triggered function and pass content body, run the following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="8c27a-232"><a name="publish"></a>Publication dans Azure</span><span class="sxs-lookup"><span data-stu-id="8c27a-232"><a name="publish"></a>Publish to Azure</span></span>

<span data-ttu-id="8c27a-233">Pour publier un projet Functions dans une application de fonction au sein d’Azure, utilisez la commande `publish` :</span><span class="sxs-lookup"><span data-stu-id="8c27a-233">To publish a Functions project to a function app in Azure, use the `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="8c27a-234">Vous pouvez utiliser les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c27a-234">You can use the following options:</span></span>

| <span data-ttu-id="8c27a-235">Option</span><span class="sxs-lookup"><span data-stu-id="8c27a-235">Option</span></span>     | <span data-ttu-id="8c27a-236">Description</span><span class="sxs-lookup"><span data-stu-id="8c27a-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="8c27a-237">Publier dans Azure les paramètres figurant dans local.settings.json, avec demande de confirmation du remplacement si le paramètre existe déjà.</span><span class="sxs-lookup"><span data-stu-id="8c27a-237">Publish settings in local.settings.json to Azure, prompting to overwrite if the setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="8c27a-238">Doit être utilisé avec `-i`.</span><span class="sxs-lookup"><span data-stu-id="8c27a-238">Must be used with `-i`.</span></span> <span data-ttu-id="8c27a-239">Remplace les paramètres d’application dans Azure par la valeur locale s’ils sont différents.</span><span class="sxs-lookup"><span data-stu-id="8c27a-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="8c27a-240">Par défaut, l’accord de l’utilisateur est sollicité.</span><span class="sxs-lookup"><span data-stu-id="8c27a-240">Default is prompt.</span></span>|

<span data-ttu-id="8c27a-241">La commande `publish` charge le contenu du répertoire du projet Functions.</span><span class="sxs-lookup"><span data-stu-id="8c27a-241">The `publish` command uploads the contents of the Functions project directory.</span></span> <span data-ttu-id="8c27a-242">Si vous supprimez les fichiers localement, la commande `publish` ne les supprime pas d’Azure.</span><span class="sxs-lookup"><span data-stu-id="8c27a-242">If you delete files locally, the `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="8c27a-243">Vous pouvez supprimer des fichiers dans Azure à l’aide de [l’outil Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) dans le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="8c27a-243">You can delete files in Azure by using the [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in the [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c27a-244">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c27a-244">Next steps</span></span>

<span data-ttu-id="8c27a-245">Azure Functions Core Tools est [disponible en open source et hébergé sur GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="8c27a-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="8c27a-246">Pour enregistrer un bogue ou une demande de fonctionnalité, [créez un problème GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="8c27a-246">To file a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[Azure Functions Core Tools]: https://www.npmjs.com/package/azure-functions-core-tools
[portail Azure]: https://portal.azure.com 
