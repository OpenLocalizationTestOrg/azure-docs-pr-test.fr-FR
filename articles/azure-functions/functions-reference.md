---
title: "aaaGuidance pour le développement de fonctions de Azure | Documents Microsoft"
description: "Découvrez les concepts des fonctions de Azure hello et techniques que vous avez besoin de fonctions toodevelop dans Azure, sur tous les langages de programmation et les liaisons."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "guide de développement, azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a>Guide de développement Azure Functions
Dans les fonctions d’Azure, des fonctions spécifiques partagent quelques concepts techniques de base et composants, quelle que soit la langue de hello ou de liaison que vous utilisez. Avant de passer à l’apprentissage des détails spécifiques tooa est fonction de langue ou liaison, être tooread que via cette vue d’ensemble qui s’applique tooall d'entre eux.

Cet article suppose que vous avez déjà lu hello [vue d’ensemble des fonctions d’Azure](functions-overview.md) et vous êtes familiarisé avec [WebJobs SDK concepts tels que les déclencheurs, liaisons et hello JobHost runtime](../app-service-web/websites-dotnet-webjobs-sdk.md). Les fonctions Azure est basé sur hello WebJobs SDK. 

## <a name="function-code"></a>Code de fonction
A *fonction* est hello le concept principal dans les fonctions d’Azure. Écrire du code pour une fonction dans une langue de votre choix et d’enregistrer le code de hello et les fichiers de configuration dans hello même dossier. configuration de Hello est nommée `function.json`, qui contient les données de configuration JSON. Différentes langues sont prises en charge, et chacun d’eux a un toowork expérience légèrement différente optimisé idéal pour cette langue. 

fichier de function.json Hello définit les liaisons de fonction hello et d’autres paramètres de configuration. Hello runtime utilise cette toomonitor d’événements fichier toodetermine hello et le fonctionnement de toopass retournées et données vers et à partir de l’exécution. Hello Voici un exemple de fichier function.json.

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

Ensemble hello `disabled` propriété trop`true` fonction hello tooprevent en cours d’exécution.

Hello `bindings` propriété est où vous permet de configurer des liaisons et des déclencheurs. Chaque liaison partage quelques paramètres communs et certains paramètres, qui sont de type particulier de tooa spécifique de liaison. Chaque liaison nécessite hello suivant les paramètres :

| Propriété | Valeurs/types | Commentaires |
| --- | --- | --- |
| `type` |string |Type de liaison. Par exemple, `queueTrigger`. |
| `direction` |'in', 'out' |Indique si la liaison de hello est pour la réception de données en fonction de hello ou envoi de données à partir de la fonction hello. |
| `name` |string |nom de Hello qui est utilisé pour hello des données liées dans la fonction hello. Pour c#, ceci est un nom d’argument ; pour JavaScript, il s’agit de la clé hello dans une liste de clé/valeur. |

## <a name="function-app"></a>Conteneur de fonctions
Un conteneur de fonctions est constitué d’une ou de plusieurs des fonctions individuelles qui sont gérées ensemble par Azure App Service. Toutes les fonctions hello dans un partage d’application de fonction hello même tarification planifier, de déploiement continu et de version du runtime. Fonctions écrites dans plusieurs langages peuvent que tous partager hello même fonction app. Considérez une application de fonction comme un moyen de tooorganize et collectivement gérer vos fonctions. 

## <a name="runtime-script-host-and-web-host"></a>Runtime (hôte de script et hôte web)
Hello runtime ou hôte de script est hello sous-jacent WebJobs SDK qui écoute les événements, collecte et envoie des données et exécute votre code. 

les déclencheurs toofacilitate HTTP, il existe également un hôte web qui est conçue toosit devant l’ordinateur hôte de script hello dans les scénarios de production. Avoir deux hôtes permet de scripts tooisolate hello du trafic de frontal hello géré par hello web hôte.

## <a name="folder-structure"></a>Structure des dossiers
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

Lorsque vous définissez un projet pour le déploiement d’application de fonction fonctions tooa dans Azure App Service, vous pouvez traiter cette structure de dossiers en tant que votre code de site. Vous pouvez utiliser des outils existants, comme le déploiement et l'intégration continus, ou des scripts de déploiement personnalisés pour effectuer l'installation du package ou la transpilation de code au moment du déploiement.

> [!NOTE]
> Assurez-vous que toodeploy votre `host.json` dossiers de fichiers et de fonction directement toohello `wwwroot` dossier. N’incluez pas hello `wwwroot` dossier dans vos déploiements. Sinon, vous vous retrouverez avec `wwwroot\wwwroot` dossiers. 
> 
> 

## <a id="fileupdate"></a>Fonctionnement des fichiers de l’application tooupdate
éditeur de fonctions Hello intégrée hello portail Azure vous permet de mettre à jour de hello *function.json* de fichiers et le fichier de code hello pour une fonction. tooupload ou mise à jour autres fichiers tels que *package.json* ou *project.json* ou dépendances, vous avez toouse autres méthodes de déploiement.

Applications de fonction sont intégrées sur le Service d’application, afin que tous les hello [options de déploiement des applications web disponible toostandard](../app-service-web/web-sites-deploy.md) sont également disponibles pour les applications de la fonction. Voici certaines méthodes, vous pouvez utiliser tooupload ou mettre à jour les fichiers d’application de fonction. 

#### <a name="toouse-app-service-editor"></a>toouse éditeur de Service d’applications
1. Dans le portail Azure fonctions hello, cliquez sur **paramètres de l’application de la fonction**.
2. Bonjour **paramètres avancés** , cliquez sur **aller paramètres du Service tooApp**.
3. Cliquez sur **Éditeur App Service** dans App Menu Nav sous **OUTILS DE DÉVELOPPEMENT**.
4. Cliquez sur **Atteindre**.
   
   Une fois que la charge de l’éditeur de Service d’application, vous verrez hello *host.json* des dossiers de fichiers et de fonction sous *wwwroot*. 
5. Tooedit de fichiers ouverts, ou faites glisser et déposez des fichiers tooupload machine de développement.

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a>point de terminaison SCM (Kudu) de l’application toouse hello (fonction)
1. Accédez à `https://<function_app_name>.scm.azurewebsites.net`.
2. Cliquez sur **Console de débogage > CMD**.
3. Accédez trop`D:\home\site\wwwroot\` tooupdate *host.json* ou `D:\home\site\wwwroot\<function_name>` tooupdate les fichiers d’une fonction.
4. Glisser-déposer un fichier que vous souhaitez tooupload dans le dossier approprié de hello dans la grille de fichier hello. Il existe deux zones dans la grille de fichier hello dans laquelle vous pouvez déposer un fichier. Pour *.zip* fichiers, une zone s’affiche avec l’étiquette de hello « faites glisser ici tooupload et décompressez. » Pour les autres types de fichier, supprimer dans la grille de fichier hello mais en dehors de la zone de « unzip » hello.

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a>déploiement continu toouse
Suivez les instructions de hello dans la rubrique de hello [déploiement continu pour les fonctions Azure](functions-continuous-deployment.md).

## <a name="parallel-execution"></a>Exécution en parallèle
Lorsque plusieurs événements de déclenchement se produisent plus rapidement qu’un runtime monothread (fonction) pour les traiter, hello runtime peut appeler fonction hello plusieurs fois en parallèle.  Si une application de la fonction à l’aide de hello [consommation plan d’hébergement](functions-scale.md#how-the-consumption-plan-works), application de fonction hello peut monter en charge automatiquement.  Chaque instance de l’application de fonction hello, si l’application hello s’exécute sur hello la consommation de l’hébergement du plan ou une expression régulière [plan d’hébergement du Service d’applications](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), peuvent traiter des appels de fonction simultanés en parallèle à l’aide de plusieurs threads.  nombre maximal de Hello d’appels de fonction simultanés dans chaque instance d’application de fonction varie en fonction de type hello de déclencheur utilisé, ainsi que les ressources hello utilisées par d’autres fonctions au sein de l’application de fonction hello.

## <a name="functions-runtime-versioning"></a>Contrôle de version du runtime Functions

Vous pouvez configurer hello version de runtime de fonctions hello à l’aide de hello `FUNCTIONS_EXTENSION_VERSION` paramètre d’application. Par exemple, la valeur de hello « ~ 1 » indique que votre application de la fonction utilise 1 sa version majeure. Les applications de fonction sont version mineure tooeach mis à niveau qu’elles sont disponibles. Vous pouvez afficher la version exacte de hello de votre application de la fonction Bonjour **paramètres** onglet Bonjour portail Azure.

## <a name="repositories"></a>Référentiels
code Hello pour les fonctions de Azure est open source et stockées dans des référentiels GitHub :

* [Runtime Azure Functions](https://github.com/Azure/azure-webjobs-sdk-script/)
* [Portail Azure Functions](https://github.com/projectkudu/AzureFunctionsPortal)
* [Modèles Azure Functions](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [Kit de développement logiciel Azure WebJobs](https://github.com/Azure/azure-webjobs-sdk/)
* [Extensions du kit de développement logiciel Azure WebJobs](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a>Liaisons
Voici un tableau de toutes les liaisons prises en charge.

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a>Problèmes liés aux rapports
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello suivant des ressources :

* [Meilleures pratiques pour Azure Functions](functions-best-practices.md)
* [Informations de référence pour les développeurs C# sur Azure Functions](functions-reference-csharp.md)
* [Informations de référence pour les développeurs F# sur Azure Functions](functions-reference-fsharp.md)
* [Azure Functions NodeJS developer reference (Référence pour les développeurs NodeJS Azure Functions)](functions-reference-node.md)
* [Déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md)
* [Les fonctions Azure : hello voyage](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) sur le blog de l’équipe du Service d’applications Azure hello. Un historique sur le développement d’Azure Functions.

