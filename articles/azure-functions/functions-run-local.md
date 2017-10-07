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
# <a name="code-and-test-azure-functions-locally"></a>Coder et tester des fonctions Azure localement

Lors de hello [portail Azure] fournit un ensemble complet d’outils de développement et des fonctions de test Azure, de nombreux développeurs préfèrent une expérience de développement local. Fonctions Azure rend facile toouse vos favoris du code éditeur et toodevelop des outils de développement local et tester vos fonctions sur votre ordinateur local. Vos fonctions peuvent se déclencher sur des événements dans Azure, et vous pouvez déboguer vos fonctions C# et JavaScript sur votre ordinateur local. 

Si vous êtes un développeur Visual Studio C#, Azure Functions [s’intègre aussi à Visual Studio 2017](functions-develop-vs.md).

## <a name="install-hello-azure-functions-core-tools"></a>Installer les outils de base fonctions hello Azure

Outils de principaux de fonctions Azure est une version locale du runtime Azure fonctions hello que vous pouvez exécuter sur votre ordinateur Windows local. Ce n’est pas un émulateur ni un simulateur. Il a hello même runtime qui alimente les fonctions dans Azure.

Hello [outils principaux de fonctions Azure] est fourni comme un package npm. Vous devez d’abord [installer NodeJS](https://docs.npmjs.com/getting-started/installing-node), qui inclut npm.  

>[!NOTE]
>À ce stade, aucun package d’outils de base de fonctions Azure hello ne peut être installé sur les ordinateurs Windows. Cette restriction est due tooa limitation temporaire dans l’hôte de fonctions hello.

[outils principaux de fonctions Azure] ajoute hello suivant des alias de commande :
* **func**
* **azfun**
* **azurefunctions**

Ces alias peuvent être utilisés à la place de `func` indiqué dans les exemples hello dans cette rubrique.

## <a name="create-a-local-functions-project"></a>Créer un projet Functions local

Lorsque vous exécutez localement, un projet de fonctions est un répertoire qui a local.settings.json et host.json de fichiers hello. Ce répertoire est hello équivalent d’une application de la fonction dans Azure. toolearn en savoir plus sur hello structure de dossiers de fonctions d’Azure, consultez hello [guide du développeur de fonctions d’Azure](functions-reference.md#folder-structure).

À l’invite de commandes, exécutez hello de commande suivante :

```
func init MyFunctionProj
```

sortie de Hello ressemble à hello l’exemple suivant :

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

tooopt en dehors de la création d’un référentiel Git, l’option hello d’utilisation `--no-source-control [-n]`.

<a name="local-settings"></a>

## <a name="local-settings-file"></a>Fichier de paramètres locaux

Hello fichier local.settings.json stocke les paramètres de l’application, les chaînes de connexion et les paramètres pour les outils de base de fonctions Azure. Il a hello suivant structure :

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
| Paramètre      | Description                            |
| ------------ | -------------------------------------- |
| **IsEncrypted** | Lorsque la valeur trop**true**, toutes les valeurs sont chiffrées à l’aide d’une clé d’ordinateur local. Utilisé avec les commandes `func settings`. La valeur par défaut est **false**. |
| **Valeurs** | Collection de paramètres d’application utilisés lors de l’exécution locale. Ajoutez votre objet de toothis paramètres application.  |
| **AzureWebJobsStorage** | Jeux de hello toohello de chaîne de connexion compte de stockage Azure qui est utilisée en interne par le runtime de fonctions d’Azure hello. compte de stockage Hello prend en charge les déclencheurs de votre fonction. Ce paramètre de connexion du compte de stockage est requis pour toutes les fonctions à l’exception des fonctions déclenchées par HTTP.  |
| **AzureWebJobsDashboard** | Définit hello connexion chaîne toohello compte de stockage Azure qui est utilisé toostore hello fonction journaux. Cette valeur facultative rend les journaux hello accessible dans le portail de hello.|
| **Hôte** | Paramètres de cette section Personnaliser le processus hôte de fonctions hello lors de l’exécution localement. | 
| **LocalHttpPort** | Jeux de hello port par défaut utilisé lors de l’exécution d’hôte de fonctions hello local (`func host start` et `func run`). Hello `--port` option de ligne de commande est prioritaire sur cette valeur. |
| **CORS** | Définit les origines hello autorisés pour [ressources cross-origin (CORS) de partage](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Les origines sont fournies sous la forme d’une liste séparée par des virgules, sans espaces. Hello valeur générique (**\***) est pris en charge, ce qui autorise les demandes d’origine. |
| **ConnectionStrings** | Contient les chaînes de connexion de base de données de hello pour vos fonctions. Chaînes de connexion de cet objet sont ajoutés environnement toohello avec le type de fournisseur hello de **System.Data.SqlClient**.  | 

La plupart des déclencheurs et les liaisons ont un **connexion** propriété qui mappe le nom d’un paramètre d’application ou de la variable d’environnement toohello. Pour chaque propriété de connexion, un paramètre d’application doit être défini dans le fichier local.settings.json. 

Ces paramètres peuvent aussi être lus dans votre code en tant que variables d’environnement. Dans C#, utilisez [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) ou [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx). En JavaScript, utilisez `process.env`. Paramètres spécifiés comme une variable d’environnement système sont prioritaires sur les valeurs dans le fichier de local.settings.json hello. 

Paramètres dans le fichier de local.settings.json hello sont uniquement utilisés par les outils de fonctions lors de l’exécution localement. Par défaut, ces paramètres ne migrent pas automatiquement lorsque le projet de hello est tooAzure publiée. Hello d’utilisation `--publish-local-settings` commutateur [lorsque vous publiez](#publish) toomake que ces paramètres sont ajoutés toohello fonction application dans Azure.

Quand aucune chaîne de connexion de stockage valide n’est définie pour **AzureWebJobsStorage**, hello message d’erreur suivant s’affiche :  

>Valeur manquante pour AzureWebJobsStorage dans local.settings.json. Cette valeur est nécessaire pour tous les déclencheurs autres que HTTP. Vous pouvez exécuter 'func azure functionary fetch-app-settings <functionAppName>' ou spécifier une chaîne de connexion dans local.settings.json.
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a>Configuration des paramètres d’application

tooset une valeur pour les chaînes de connexion, vous pouvez effectuer une des manières suivantes les hello :
* Entrez la chaîne de connexion hello [Azure Storage Explorer](http://storageexplorer.com/).
* Utilisez une des hello suivant de commandes :

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    Les deux commandes nécessitent vous toofirst connexion tooAzure.

## <a name="create-a-function"></a>Créer une fonction

toocreate une fonction, exécutez hello de commande suivante :

```
func new
``` 
`func new`hello prend en charge des arguments facultatifs suivants :

| Argument     | Description                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | modèle Hello programmation langage, tel que c#, F # ou JavaScript. |
| **`--template -t`** | nom du modèle Hello. |
| **`--name -n`** | nom de la fonction Hello. |

Par exemple, toocreate un déclencheur JavaScript HTTP, exécutez :

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

toocreate une fonction déclenché à la file d’attente, exécutez :

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a>Exécuter des fonctions localement

toorun un projet de fonctions, exécuter l’hôte de fonctions hello. hôte de Hello permet de déclencheurs pour toutes les fonctions dans le projet de hello :

```
func host start
```

`func host start`prend en charge hello options suivantes :

| Option     | Description                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | toolisten de port local Hello sur. Valeur par défaut : 7071. |
| **`--debug <type>`** | options de Hello sont `VSCode` et `VS`. |
| **`--cors`** | Liste séparée par des virgules d’origines CORS, sans espaces. |
| **`--nodeDebugPort -n`** | port Hello pour hello nœud débogueur toouse. Valeur par défaut : une valeur issue de launch.json ou 5858. |
| **`--debugLevel -d`** | niveau de trace Hello console (désactivé, verbose, info, avertissement ou erreur). Valeur par défaut : info.|
| **`--timeout -t`** | expiration du délai Hello pour hello fonctions hôte pour démarrer, en secondes. Valeur par défaut : 20 secondes.|
| **`--useHttps`** | Lier toohttps://localhost : {port} plutôt que de toohttp://localhost : {port}. Par défaut, cette option crée un certificat de confiance sur votre ordinateur.|
| **`--pause-on-error`** | Suspendre des entrées supplémentaires avant de quitter le processus de hello. Utile au lancement d’Azure Functions Core Tools à partir d’un environnement de développement intégré (IDE).|

Au démarrage de l’hôte de fonctions hello, il génère des fonctions de hello déclenchés par l’URL de HTTP :

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a>Débogage dans VS Code ou Visual Studio

tooattach un débogueur, passez hello `--debug` argument. les fonctions JavaScript toodebug, utilisez Visual Studio Code. Pour les fonctions C#, utilisez Visual Studio.

toodebug c#, utilisez `--debug vs`. Vous pouvez également utiliser [Visual Studio 2017 Tools pour Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/). 

hôte de hello toolaunch et une configuration de débogage de JavaScript, exécutez :

```
func host start --debug vscode
```

Ensuite, dans Visual Studio Code, Bonjour **déboguer** afficher, sélectionnez **joignez des fonctions de tooAzure**. Vous pouvez joindre des points d’arrêt, inspecter des variables et parcourir le code.

![Débogage JavaScript avec Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a>Fonction de tooa de données de test de passage

Vous pouvez également appeler une fonction directement à l’aide `func run <FunctionName>` et fournissent des données d’entrée pour la fonction hello. Cette commande est similaire toorunning une fonction à l’aide de hello **Test** onglet Bonjour portail Azure. Cette commande lance l’hôte de fonctions hello entier.

`func run`prend en charge hello options suivantes :

| Option     | Description                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | Contenu inclus. |
| **`--debug -d`** | Attacher un processus hôte de toohello débogueur avant d’exécuter la fonction hello.|
| **`--timeout -t`** | Toowait de temps (en secondes) jusqu'à ce que l’hôte de fonctions hello local est prêt.|
| **`--file -f`** | Bonjour toouse de nom de fichier en tant que contenu.|
| **`--no-interactive`** | Ne pas demander d’entrée. Utile pour les scénarios d’automatisation.|

Par exemple, toocall une fonction a déclenché l’HTTP et le corps de contenu pass, exécutez hello commande suivante :

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <a name="publish"></a>Publication tooAzure

toopublish une application de fonction fonctions projet tooa dans Azure, utilisez hello `publish` commande :

```
func azure functionapp publish <FunctionAppName>
```

Vous pouvez utiliser hello options suivantes :

| Option     | Description                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  Paramètres de publication dans tooAzure local.settings.json, invitant toooverwrite si hello le paramètre existe déjà.|
| **`--overwrite-settings -y`** | Doit être utilisé avec `-i`. Remplace les paramètres d’application dans Azure par la valeur locale s’ils sont différents. Par défaut, l’accord de l’utilisateur est sollicité.|

Hello `publish` commande télécharge le contenu hello du répertoire de projet de fonctions hello. Si vous supprimez les fichiers localement, hello `publish` commande ne supprime pas les à partir d’Azure. Vous pouvez supprimer des fichiers dans Azure à l’aide de hello [outil de Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) Bonjour [portail Azure].

## <a name="next-steps"></a>Étapes suivantes

Azure Functions Core Tools est [disponible en open source et hébergé sur GitHub](https://github.com/azure/azure-functions-cli).  
toofile une demande de bogue ou de fonctionnalité, [ouvrir un problème GitHub](https://github.com/azure/azure-functions-cli/issues). 

<!-- LINKS -->

[outils principaux de fonctions Azure]: https://www.npmjs.com/package/azure-functions-core-tools
[portail Azure]: https://portal.azure.com 
