---
title: "aaaDevelop et exécution Azure fonctionne localement | Documents Microsoft"
description: "Découvrez comment toocode et test Azure fonctionne sur votre ordinateur local avant de les exécuter sur les fonctions d’Azure."
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
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="e20a4-103">Coder et tester des fonctions Azure localement</span><span class="sxs-lookup"><span data-stu-id="e20a4-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="e20a4-104">Lors de hello [portail Azure] fournit un ensemble complet d’outils de développement et des fonctions de test Azure, de nombreux développeurs préfèrent une expérience de développement local.</span><span class="sxs-lookup"><span data-stu-id="e20a4-104">While hello [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="e20a4-105">Fonctions Azure rend facile toouse vos favoris du code éditeur et toodevelop des outils de développement local et tester vos fonctions sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="e20a4-105">Azure Functions makes it easy toouse your favorite code editor and local development tools toodevelop and test your functions on your local computer.</span></span> <span data-ttu-id="e20a4-106">Vos fonctions peuvent se déclencher sur des événements dans Azure, et vous pouvez déboguer vos fonctions C# et JavaScript sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="e20a4-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="e20a4-107">Si vous êtes un développeur Visual Studio C#, Azure Functions [s’intègre aussi à Visual Studio 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="e20a4-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-hello-azure-functions-core-tools"></a><span data-ttu-id="e20a4-108">Installer les outils de base fonctions hello Azure</span><span class="sxs-lookup"><span data-stu-id="e20a4-108">Install hello Azure Functions Core Tools</span></span>

<span data-ttu-id="e20a4-109">Outils de principaux de fonctions Azure est une version locale du runtime Azure fonctions hello que vous pouvez exécuter sur votre ordinateur Windows local.</span><span class="sxs-lookup"><span data-stu-id="e20a4-109">Azure Functions Core Tools is a local version of hello Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="e20a4-110">Ce n’est pas un émulateur ni un simulateur.</span><span class="sxs-lookup"><span data-stu-id="e20a4-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="e20a4-111">Il a hello même runtime qui alimente les fonctions dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e20a4-111">It's hello same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="e20a4-112">Hello [outils principaux de fonctions Azure] est fourni comme un package npm.</span><span class="sxs-lookup"><span data-stu-id="e20a4-112">hello [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="e20a4-113">Vous devez d’abord [installer NodeJS](https://docs.npmjs.com/getting-started/installing-node), qui inclut npm.</span><span class="sxs-lookup"><span data-stu-id="e20a4-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="e20a4-114">À ce stade, aucun package d’outils de base de fonctions Azure hello ne peut être installé sur les ordinateurs Windows.</span><span class="sxs-lookup"><span data-stu-id="e20a4-114">At this time, hello Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="e20a4-115">Cette restriction est due tooa limitation temporaire dans l’hôte de fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-115">This restriction is due tooa temporary limitation in hello Functions host.</span></span>

<span data-ttu-id="e20a4-116">[outils principaux de fonctions Azure] ajoute hello suivant des alias de commande :</span><span class="sxs-lookup"><span data-stu-id="e20a4-116">[Azure Functions Core Tools] adds hello following command aliases:</span></span>
* <span data-ttu-id="e20a4-117">**func**</span><span class="sxs-lookup"><span data-stu-id="e20a4-117">**func**</span></span>
* <span data-ttu-id="e20a4-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="e20a4-118">**azfun**</span></span>
* <span data-ttu-id="e20a4-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="e20a4-119">**azurefunctions**</span></span>

<span data-ttu-id="e20a4-120">Ces alias peuvent être utilisés à la place de `func` indiqué dans les exemples hello dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="e20a4-120">All of these alias can be used instead of `func` shown in hello examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="e20a4-121">Créer un projet Functions local</span><span class="sxs-lookup"><span data-stu-id="e20a4-121">Create a local Functions project</span></span>

<span data-ttu-id="e20a4-122">Lorsque vous exécutez localement, un projet de fonctions est un répertoire qui a local.settings.json et host.json de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-122">When running locally, a Functions project is a directory that has hello files host.json and local.settings.json.</span></span> <span data-ttu-id="e20a4-123">Ce répertoire est hello équivalent d’une application de la fonction dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e20a4-123">This directory is hello equivalent of a function app in Azure.</span></span> <span data-ttu-id="e20a4-124">toolearn en savoir plus sur hello structure de dossiers de fonctions d’Azure, consultez hello [guide du développeur de fonctions d’Azure](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="e20a4-124">toolearn more about hello Azure Functions folder structure, see hello [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="e20a4-125">À l’invite de commandes, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e20a4-125">At a command prompt, run hello following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="e20a4-126">sortie de Hello ressemble à hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="e20a4-126">hello output looks like hello following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="e20a4-127">tooopt en dehors de la création d’un référentiel Git, l’option hello d’utilisation `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="e20a4-127">tooopt out of creating a Git repository, use hello option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="e20a4-128">Fichier de paramètres locaux</span><span class="sxs-lookup"><span data-stu-id="e20a4-128">Local settings file</span></span>

<span data-ttu-id="e20a4-129">Hello fichier local.settings.json stocke les paramètres de l’application, les chaînes de connexion et les paramètres pour les outils de base de fonctions Azure.</span><span class="sxs-lookup"><span data-stu-id="e20a4-129">hello file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="e20a4-130">Il a hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="e20a4-130">It has hello following structure:</span></span>

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
| <span data-ttu-id="e20a4-131">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e20a4-131">Setting</span></span>      | <span data-ttu-id="e20a4-132">Description</span><span class="sxs-lookup"><span data-stu-id="e20a4-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="e20a4-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="e20a4-133">**IsEncrypted**</span></span> | <span data-ttu-id="e20a4-134">Lorsque la valeur trop**true**, toutes les valeurs sont chiffrées à l’aide d’une clé d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="e20a4-134">When set too**true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="e20a4-135">Utilisé avec les commandes `func settings`.</span><span class="sxs-lookup"><span data-stu-id="e20a4-135">Used with `func settings` commands.</span></span> <span data-ttu-id="e20a4-136">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="e20a4-136">Default value is **false**.</span></span> |
| <span data-ttu-id="e20a4-137">**Valeurs**</span><span class="sxs-lookup"><span data-stu-id="e20a4-137">**Values**</span></span> | <span data-ttu-id="e20a4-138">Collection de paramètres d’application utilisés lors de l’exécution locale.</span><span class="sxs-lookup"><span data-stu-id="e20a4-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="e20a4-139">Ajoutez votre objet de toothis paramètres application.</span><span class="sxs-lookup"><span data-stu-id="e20a4-139">Add your application settings toothis object.</span></span>  |
| <span data-ttu-id="e20a4-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="e20a4-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="e20a4-141">Jeux de hello toohello de chaîne de connexion compte de stockage Azure qui est utilisée en interne par le runtime de fonctions d’Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-141">Sets hello connection string toohello Azure Storage account that is used internally by hello Azure Functions runtime.</span></span> <span data-ttu-id="e20a4-142">compte de stockage Hello prend en charge les déclencheurs de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="e20a4-142">hello storage account supports your function's triggers.</span></span> <span data-ttu-id="e20a4-143">Ce paramètre de connexion du compte de stockage est requis pour toutes les fonctions à l’exception des fonctions déclenchées par HTTP.</span><span class="sxs-lookup"><span data-stu-id="e20a4-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="e20a4-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="e20a4-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="e20a4-145">Définit hello connexion chaîne toohello compte de stockage Azure qui est utilisé toostore hello fonction journaux.</span><span class="sxs-lookup"><span data-stu-id="e20a4-145">Sets hello connection string toohello Azure Storage account that is used toostore hello function logs.</span></span> <span data-ttu-id="e20a4-146">Cette valeur facultative rend les journaux hello accessible dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-146">This optional value makes hello logs accessible in hello portal.</span></span>|
| <span data-ttu-id="e20a4-147">**Hôte**</span><span class="sxs-lookup"><span data-stu-id="e20a4-147">**Host**</span></span> | <span data-ttu-id="e20a4-148">Paramètres de cette section Personnaliser le processus hôte de fonctions hello lors de l’exécution localement.</span><span class="sxs-lookup"><span data-stu-id="e20a4-148">Settings in this section customize hello Functions host process when running locally.</span></span> | 
| <span data-ttu-id="e20a4-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="e20a4-149">**LocalHttpPort**</span></span> | <span data-ttu-id="e20a4-150">Jeux de hello port par défaut utilisé lors de l’exécution d’hôte de fonctions hello local (`func host start` et `func run`).</span><span class="sxs-lookup"><span data-stu-id="e20a4-150">Sets hello default port used when running hello local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="e20a4-151">Hello `--port` option de ligne de commande est prioritaire sur cette valeur.</span><span class="sxs-lookup"><span data-stu-id="e20a4-151">hello `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="e20a4-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="e20a4-152">**CORS**</span></span> | <span data-ttu-id="e20a4-153">Définit les origines hello autorisés pour [ressources cross-origin (CORS) de partage](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="e20a4-153">Defines hello origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="e20a4-154">Les origines sont fournies sous la forme d’une liste séparée par des virgules, sans espaces.</span><span class="sxs-lookup"><span data-stu-id="e20a4-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="e20a4-155">Hello valeur générique (**\***) est pris en charge, ce qui autorise les demandes d’origine.</span><span class="sxs-lookup"><span data-stu-id="e20a4-155">hello wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="e20a4-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="e20a4-156">**ConnectionStrings**</span></span> | <span data-ttu-id="e20a4-157">Contient les chaînes de connexion de base de données de hello pour vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="e20a4-157">Contains hello database connection strings for your functions.</span></span> <span data-ttu-id="e20a4-158">Chaînes de connexion de cet objet sont ajoutés environnement toohello avec le type de fournisseur hello de **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="e20a4-158">Connection strings in this object are added toohello environment with hello provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="e20a4-159">La plupart des déclencheurs et les liaisons ont un **connexion** propriété qui mappe le nom d’un paramètre d’application ou de la variable d’environnement toohello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-159">Most triggers and bindings have a **Connection** property that maps toohello name of an environment variable or app setting.</span></span> <span data-ttu-id="e20a4-160">Pour chaque propriété de connexion, un paramètre d’application doit être défini dans le fichier local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="e20a4-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="e20a4-161">Ces paramètres peuvent aussi être lus dans votre code en tant que variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="e20a4-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="e20a4-162">Dans C#, utilisez [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) ou [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="e20a4-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="e20a4-163">En JavaScript, utilisez `process.env`.</span><span class="sxs-lookup"><span data-stu-id="e20a4-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="e20a4-164">Paramètres spécifiés comme une variable d’environnement système sont prioritaires sur les valeurs dans le fichier de local.settings.json hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-164">Settings specified as a system environment variable take precedence over values in hello local.settings.json file.</span></span> 

<span data-ttu-id="e20a4-165">Paramètres dans le fichier de local.settings.json hello sont uniquement utilisés par les outils de fonctions lors de l’exécution localement.</span><span class="sxs-lookup"><span data-stu-id="e20a4-165">Settings in hello local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="e20a4-166">Par défaut, ces paramètres ne migrent pas automatiquement lorsque le projet de hello est tooAzure publiée.</span><span class="sxs-lookup"><span data-stu-id="e20a4-166">By default, these settings are not migrated automatically when hello project is published tooAzure.</span></span> <span data-ttu-id="e20a4-167">Hello d’utilisation `--publish-local-settings` commutateur [lorsque vous publiez](#publish) toomake que ces paramètres sont ajoutés toohello fonction application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e20a4-167">Use hello `--publish-local-settings` switch [when you publish](#publish) toomake sure these settings are added toohello function app in Azure.</span></span>

<span data-ttu-id="e20a4-168">Quand aucune chaîne de connexion de stockage valide n’est définie pour **AzureWebJobsStorage**, hello message d’erreur suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="e20a4-168">When no valid storage connection string is set for **AzureWebJobsStorage**, hello following error message is shown:</span></span>  

><span data-ttu-id="e20a4-169">Valeur manquante pour AzureWebJobsStorage dans local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="e20a4-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="e20a4-170">Cette valeur est nécessaire pour tous les déclencheurs autres que HTTP.</span><span class="sxs-lookup"><span data-stu-id="e20a4-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="e20a4-171">Vous pouvez exécuter 'func azure functionary fetch-app-settings <functionAppName>' ou spécifier une chaîne de connexion dans local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="e20a4-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="e20a4-172">Configuration des paramètres d’application</span><span class="sxs-lookup"><span data-stu-id="e20a4-172">Configure app settings</span></span>

<span data-ttu-id="e20a4-173">tooset une valeur pour les chaînes de connexion, vous pouvez effectuer une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="e20a4-173">tooset a value for connection strings, you can do one of hello following:</span></span>
* <span data-ttu-id="e20a4-174">Entrez la chaîne de connexion hello [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e20a4-174">Enter hello connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="e20a4-175">Utilisez une des hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="e20a4-175">Use one of hello following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="e20a4-176">Les deux commandes nécessitent vous toofirst connexion tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e20a4-176">Both commands require you toofirst sign-in tooAzure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="e20a4-177">Créer une fonction</span><span class="sxs-lookup"><span data-stu-id="e20a4-177">Create a function</span></span>

<span data-ttu-id="e20a4-178">toocreate une fonction, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e20a4-178">toocreate a function, run hello following command:</span></span>

```
func new
``` 
<span data-ttu-id="e20a4-179">`func new`hello prend en charge des arguments facultatifs suivants :</span><span class="sxs-lookup"><span data-stu-id="e20a4-179">`func new` supports hello following optional arguments:</span></span>

| <span data-ttu-id="e20a4-180">Argument</span><span class="sxs-lookup"><span data-stu-id="e20a4-180">Argument</span></span>     | <span data-ttu-id="e20a4-181">Description</span><span class="sxs-lookup"><span data-stu-id="e20a4-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="e20a4-182">modèle Hello programmation langage, tel que c#, F # ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e20a4-182">hello template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="e20a4-183">nom du modèle Hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-183">hello template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="e20a4-184">nom de la fonction Hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-184">hello function name.</span></span> |

<span data-ttu-id="e20a4-185">Par exemple, toocreate un déclencheur JavaScript HTTP, exécutez :</span><span class="sxs-lookup"><span data-stu-id="e20a4-185">For example, toocreate a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="e20a4-186">toocreate une fonction déclenché à la file d’attente, exécutez :</span><span class="sxs-lookup"><span data-stu-id="e20a4-186">toocreate a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="e20a4-187">Exécuter des fonctions localement</span><span class="sxs-lookup"><span data-stu-id="e20a4-187">Run functions locally</span></span>

<span data-ttu-id="e20a4-188">toorun un projet de fonctions, exécuter l’hôte de fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-188">toorun a Functions project, run hello Functions host.</span></span> <span data-ttu-id="e20a4-189">hôte de Hello permet de déclencheurs pour toutes les fonctions dans le projet de hello :</span><span class="sxs-lookup"><span data-stu-id="e20a4-189">hello host enables triggers for all functions in hello project:</span></span>

```
func host start
```

<span data-ttu-id="e20a4-190">`func host start`prend en charge hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="e20a4-190">`func host start` supports hello following options:</span></span>

| <span data-ttu-id="e20a4-191">Option</span><span class="sxs-lookup"><span data-stu-id="e20a4-191">Option</span></span>     | <span data-ttu-id="e20a4-192">Description</span><span class="sxs-lookup"><span data-stu-id="e20a4-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="e20a4-193">toolisten de port local Hello sur.</span><span class="sxs-lookup"><span data-stu-id="e20a4-193">hello local port toolisten on.</span></span> <span data-ttu-id="e20a4-194">Valeur par défaut : 7071.</span><span class="sxs-lookup"><span data-stu-id="e20a4-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="e20a4-195">options de Hello sont `VSCode` et `VS`.</span><span class="sxs-lookup"><span data-stu-id="e20a4-195">hello options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="e20a4-196">Liste séparée par des virgules d’origines CORS, sans espaces.</span><span class="sxs-lookup"><span data-stu-id="e20a4-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="e20a4-197">port Hello pour hello nœud débogueur toouse.</span><span class="sxs-lookup"><span data-stu-id="e20a4-197">hello port for hello node debugger toouse.</span></span> <span data-ttu-id="e20a4-198">Valeur par défaut : une valeur issue de launch.json ou 5858.</span><span class="sxs-lookup"><span data-stu-id="e20a4-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="e20a4-199">niveau de trace Hello console (désactivé, verbose, info, avertissement ou erreur).</span><span class="sxs-lookup"><span data-stu-id="e20a4-199">hello console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="e20a4-200">Valeur par défaut : info.</span><span class="sxs-lookup"><span data-stu-id="e20a4-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="e20a4-201">expiration du délai Hello pour hello fonctions hôte pour démarrer, en secondes.</span><span class="sxs-lookup"><span data-stu-id="e20a4-201">hello time out for hello Functions host t     o start, in seconds.</span></span> <span data-ttu-id="e20a4-202">Valeur par défaut : 20 secondes.</span><span class="sxs-lookup"><span data-stu-id="e20a4-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="e20a4-203">Lier toohttps://localhost : {port} plutôt que de toohttp://localhost : {port}.</span><span class="sxs-lookup"><span data-stu-id="e20a4-203">Bind toohttps://localhost:{port} rather than toohttp://localhost:{port}.</span></span> <span data-ttu-id="e20a4-204">Par défaut, cette option crée un certificat de confiance sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e20a4-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="e20a4-205">Suspendre des entrées supplémentaires avant de quitter le processus de hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-205">Pause for additional input before exiting hello process.</span></span> <span data-ttu-id="e20a4-206">Utile au lancement d’Azure Functions Core Tools à partir d’un environnement de développement intégré (IDE).</span><span class="sxs-lookup"><span data-stu-id="e20a4-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="e20a4-207">Au démarrage de l’hôte de fonctions hello, il génère des fonctions de hello déclenchés par l’URL de HTTP :</span><span class="sxs-lookup"><span data-stu-id="e20a4-207">When hello Functions host starts, it outputs hello URL of HTTP-triggered functions:</span></span>

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="e20a4-208">Débogage dans VS Code ou Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e20a4-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="e20a4-209">tooattach un débogueur, passez hello `--debug` argument.</span><span class="sxs-lookup"><span data-stu-id="e20a4-209">tooattach a debugger, pass hello `--debug` argument.</span></span> <span data-ttu-id="e20a4-210">les fonctions JavaScript toodebug, utilisez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e20a4-210">toodebug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="e20a4-211">Pour les fonctions C#, utilisez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e20a4-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="e20a4-212">toodebug c#, utilisez `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="e20a4-212">toodebug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="e20a4-213">Vous pouvez également utiliser [Visual Studio 2017 Tools pour Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="e20a4-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="e20a4-214">hôte de hello toolaunch et une configuration de débogage de JavaScript, exécutez :</span><span class="sxs-lookup"><span data-stu-id="e20a4-214">toolaunch hello host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="e20a4-215">Ensuite, dans Visual Studio Code, Bonjour **déboguer** afficher, sélectionnez **joignez des fonctions de tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="e20a4-215">Then, in Visual Studio Code, in hello **Debug** view, select **Attach tooAzure Functions**.</span></span> <span data-ttu-id="e20a4-216">Vous pouvez joindre des points d’arrêt, inspecter des variables et parcourir le code.</span><span class="sxs-lookup"><span data-stu-id="e20a4-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Débogage JavaScript avec Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a><span data-ttu-id="e20a4-218">Fonction de tooa de données de test de passage</span><span class="sxs-lookup"><span data-stu-id="e20a4-218">Passing test data tooa function</span></span>

<span data-ttu-id="e20a4-219">Vous pouvez également appeler une fonction directement à l’aide `func run <FunctionName>` et fournissent des données d’entrée pour la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for hello function.</span></span> <span data-ttu-id="e20a4-220">Cette commande est similaire toorunning une fonction à l’aide de hello **Test** onglet Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e20a4-220">This command is similar toorunning a function using hello **Test** tab in hello Azure portal.</span></span> <span data-ttu-id="e20a4-221">Cette commande lance l’hôte de fonctions hello entier.</span><span class="sxs-lookup"><span data-stu-id="e20a4-221">This command launches hello entire Functions host.</span></span>

<span data-ttu-id="e20a4-222">`func run`prend en charge hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="e20a4-222">`func run` supports hello following options:</span></span>

| <span data-ttu-id="e20a4-223">Option</span><span class="sxs-lookup"><span data-stu-id="e20a4-223">Option</span></span>     | <span data-ttu-id="e20a4-224">Description</span><span class="sxs-lookup"><span data-stu-id="e20a4-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="e20a4-225">Contenu inclus.</span><span class="sxs-lookup"><span data-stu-id="e20a4-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="e20a4-226">Attacher un processus hôte de toohello débogueur avant d’exécuter la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-226">Attach a debugger toohello host process before running hello function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="e20a4-227">Toowait de temps (en secondes) jusqu'à ce que l’hôte de fonctions hello local est prêt.</span><span class="sxs-lookup"><span data-stu-id="e20a4-227">Time toowait (in seconds) until hello local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="e20a4-228">Bonjour toouse de nom de fichier en tant que contenu.</span><span class="sxs-lookup"><span data-stu-id="e20a4-228">hello file name toouse as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="e20a4-229">Ne pas demander d’entrée.</span><span class="sxs-lookup"><span data-stu-id="e20a4-229">Does not prompt for input.</span></span> <span data-ttu-id="e20a4-230">Utile pour les scénarios d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="e20a4-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="e20a4-231">Par exemple, toocall une fonction a déclenché l’HTTP et le corps de contenu pass, exécutez hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e20a4-231">For example, toocall an HTTP-triggered function and pass content body, run hello following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="e20a4-232"><a name="publish"></a>Publication tooAzure</span><span class="sxs-lookup"><span data-stu-id="e20a4-232"><a name="publish"></a>Publish tooAzure</span></span>

<span data-ttu-id="e20a4-233">toopublish une application de fonction fonctions projet tooa dans Azure, utilisez hello `publish` commande :</span><span class="sxs-lookup"><span data-stu-id="e20a4-233">toopublish a Functions project tooa function app in Azure, use hello `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="e20a4-234">Vous pouvez utiliser hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="e20a4-234">You can use hello following options:</span></span>

| <span data-ttu-id="e20a4-235">Option</span><span class="sxs-lookup"><span data-stu-id="e20a4-235">Option</span></span>     | <span data-ttu-id="e20a4-236">Description</span><span class="sxs-lookup"><span data-stu-id="e20a4-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="e20a4-237">Paramètres de publication dans tooAzure local.settings.json, invitant toooverwrite si hello le paramètre existe déjà.</span><span class="sxs-lookup"><span data-stu-id="e20a4-237">Publish settings in local.settings.json tooAzure, prompting toooverwrite if hello setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="e20a4-238">Doit être utilisé avec `-i`.</span><span class="sxs-lookup"><span data-stu-id="e20a4-238">Must be used with `-i`.</span></span> <span data-ttu-id="e20a4-239">Remplace les paramètres d’application dans Azure par la valeur locale s’ils sont différents.</span><span class="sxs-lookup"><span data-stu-id="e20a4-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="e20a4-240">Par défaut, l’accord de l’utilisateur est sollicité.</span><span class="sxs-lookup"><span data-stu-id="e20a4-240">Default is prompt.</span></span>|

<span data-ttu-id="e20a4-241">Hello `publish` commande télécharge le contenu hello du répertoire de projet de fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="e20a4-241">hello `publish` command uploads hello contents of hello Functions project directory.</span></span> <span data-ttu-id="e20a4-242">Si vous supprimez les fichiers localement, hello `publish` commande ne supprime pas les à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="e20a4-242">If you delete files locally, hello `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="e20a4-243">Vous pouvez supprimer des fichiers dans Azure à l’aide de hello [outil de Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) Bonjour [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="e20a4-243">You can delete files in Azure by using hello [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e20a4-244">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e20a4-244">Next steps</span></span>

<span data-ttu-id="e20a4-245">Azure Functions Core Tools est [disponible en open source et hébergé sur GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="e20a4-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="e20a4-246">toofile une demande de bogue ou de fonctionnalité, [ouvrir un problème GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="e20a4-246">toofile a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[outils principaux de fonctions Azure]: https://www.npmjs.com/package/azure-functions-core-tools
[portail Azure]: https://portal.azure.com 
