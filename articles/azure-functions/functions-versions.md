---
title: Comment cibler des versions du runtime Azure Functions
description: "Azure Functions prend en charge plusieurs versions du runtime. Découvrez comment spécifier la version du runtime d’une application de fonction hébergée dans Azure."
services: functions
documentationcenter: 
author: ggailey777
manager: cfowler
editor: 
ms.service: functions
ms.workload: na
ms.devlang: na
ms.topic: article
ms.date: 11/21/2017
ms.author: glenga
ms.openlocfilehash: 588437af80ecf60b7c4b24dbf6bccc67fc33da7a
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/29/2017
---
# <a name="how-to-target-azure-functions-runtime-versions"></a>Comment cibler des versions du runtime Azure Functions

Une application de fonction s’exécute sur une version spécifique du runtime Azure Functions. Il existe deux versions majeures : 1.x et 2.x. Cet article explique comment choisir la version majeure à utiliser et comment configurer une application de fonction dans Azure pour qu’elle s’exécute sur la version de votre choix. Pour plus d’informations sur la façon de configurer un environnement de développement local pour une version spécifique, consultez [Coder et tester Azure Functions localement](functions-run-local.md).

## <a name="differences-between-runtime-1x-and-2x"></a>Différences entre le runtime 1.x et 2.x

> [!IMPORTANT] 
> Runtime 1.x est la seule version approuvée pour une utilisation en production.

| Runtime | État |
|---------|---------|
|1.x|Disponibilité générale (GA)|
|2.x|VERSION PRÉLIMINAIRE|

Les sections suivantes expliquent les différences de prise en charge des langages, des liaisons et du développement multiplateforme.

### <a name="languages"></a>Langues

Le tableau suivant montre les langages de programmation qui sont pris en charge dans chaque version du runtime.

[!INCLUDE [functions-supported-languages](../../includes/functions-supported-languages.md)]

Pour en savoir plus, consultez [Langages pris en charge](supported-languages.md).

### <a name="bindings"></a>Liaisons 

Le runtime 2.x vous permet de créer des [extensions de liaison](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) personnalisées. Les liaisons intégrées qui utilisent ce modèle d’extensibilité sont disponibles uniquement dans la version 2.x. Parmi les principales figurent les [liaisons Microsoft Graph](functions-bindings-microsoft-graph.md).

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

Pour plus d’informations sur la prise en charge des liaisons et d’autres écarts fonctionnels dans la version 2.x, consultez [Runtime 2.0 known issues (Problèmes connus dans le runtime 2.0)](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Azure-Functions-runtime-2.0-known-issues).

### <a name="cross-platform-development"></a>Développement multiplateforme

Le runtime 1.x prend en charge le développement de fonctions uniquement dans le portail ou sur Windows. Avec la version 2.x, vous pouvez développer et exécuter Azure Functions sur Linux ou macOS.

## <a name="automatic-and-manual-version-updates"></a>Mises à jour de versions automatiques et manuelles

Azure Functions vous permet de cibler une version spécifique du runtime en utilisant le paramètre d’application `FUNCTIONS_EXTENSION_VERSION` dans une application de fonction. L’application de fonction est conservée sur la version majeure spécifiée jusqu’à ce que vous décidiez de passer à une nouvelle version.

Si vous spécifiez uniquement la version majeure (« ~ 1 » pour 1.x ou « bêta » pour 2.x), l’application de fonction est automatiquement mise à jour vers les nouvelles versions mineures du runtime quand elles deviennent disponibles. Les nouvelles versions mineures n’introduisent pas de changements importants. Si vous spécifiez une version mineure (par exemple, « 1.0.11360 »), l’application de fonction est maintenue sur cette version jusqu’à ce que vous la changiez explicitement. 

Quand une nouvelle version est disponible publiquement, une invite dans le portail vous donne la possibilité de basculer vers cette version. Après le passage à une nouvelle version, vous avez toujours la possibilité d’utiliser le paramètre d’application `FUNCTIONS_EXTENSION_VERSION` pour revenir à une version précédente.

Un changement de version du runtime provoque un redémarrage de l’application de fonction.

Les valeurs que vous pouvez définir dans le paramètre d’application `FUNCTIONS_EXTENSION_VERSION` pour activer les mises à jour automatiques sont actuellement « ~1 » pour le runtime 1.x et « bêta » pour le runtime 2.x.

## <a name="view-the-current-runtime-version"></a>Afficher la version actuelle du runtime

Appliquez la procédure suivante pour afficher la version du runtime utilisée actuellement par une application de fonction. 

1. Dans le [portail Azure](https://portal.azure.com), accédez à l’application de fonction et, sous **Fonctionnalités configurées**, choisissez **Paramètres de l’application de fonction**. 

    ![Sélectionnez Paramètres de l’application de fonction](./media/functions-versions/add-update-app-setting.png)

2. Dans l’onglet **Paramètres de l’application de fonction**, trouvez la **Version du runtime**. Prenez note de la version spécifique du runtime ainsi que de la version majeure souhaitée. Dans l’exemple ci-dessous, le paramètre d’application FUNCTIONS\_EXTENSION\_VERSION a la valeur `~1`.
 
   ![Sélectionnez Paramètres de l’application de fonction](./media/functions-versions/function-app-view-version.png)

## <a name="target-the-version-20-runtime"></a>Cible le runtime version 2.0

>[!IMPORTANT]   
> Le runtime d’Azure Functions 2.0 est en préversion ; pour le moment, toutes les fonctionnalités d’Azure Functions ne sont pas prises en charge. Pour plus d’informations, consultez [Différences entre le runtime 1.x et 2.x](#differences-between-runtime-1x-and-2x) plus haut dans cet article.

Vous pouvez mettre à jour une application de fonction vers la préversion du runtime 2.0 dans le portail Azure. Dans l’onglet **Paramètres de l’application de fonction**, sélectionnez **Beta** sous **Version du runtime**.  

![Sélectionnez Paramètres de l’application de fonction](./media/functions-versions/function-app-view-version.png)

Ce paramètre revient à définir le paramètre d’application `FUNCTIONS_EXTENSION_VERSION` sur `beta`. Choisissez le bouton **~1** pour repasser à la version majeure actuelle prise en charge publiquement. Vous pouvez aussi utiliser Azure CLI pour mettre à jour ce paramètre d’application. 

## <a name="target-a-version-using-the-portal"></a>Cibler une version à l’aide du portail

Quand vous avez besoin de cibler une version autre que la version majeure actuelle ou la version 2.0, vous devez définir le paramètre d’application `FUNCTIONS_EXTENSION_VERSION`.

1. Dans le [portail Azure](https://portal.azure.com), accédez à votre application de fonction, et sous **Fonctionnalités configurées**, choisissez **Paramètres d’application**.

    ![Sélectionnez Paramètres de l’application de fonction](./media/functions-versions/add-update-app-setting1a.png)

2. Sous l’onglet **Paramètres d’application**, recherchez le paramètre `FUNCTIONS_EXTENSION_VERSION` puis remplacez la valeur par une version valide du runtime 1.x ou `beta` pour la version 2.0. 

    ![Définir le paramètre de l’application de fonction](./media/functions-versions/add-update-app-setting2.png)

3. Cliquez sur **Enregistrer** pour enregistrer la mise à jour du paramètre d’application. 

## <a name="target-a-version-using-azure-cli"></a>Cibler une version à l’aide d’Azure CLI

 Vous pouvez aussi définir l’élément `FUNCTIONS_EXTENSION_VERSION` à partir d’Azure CLI. À l’aide d’Azure CLI, mettez à jour ce paramètre d’application dans l’application de fonction, à l’aide de la commande [az functionapp config appsettings set](/cli/azure/functionapp/config/appsettings#set).

```azurecli-interactive
az functionapp config appsettings set --name <function_app> \
--resource-group <my_resource_group> \
--settings FUNCTIONS_EXTENSION_VERSION=<version>
```
Dans ce code, remplacez `<function_app>` par le nom de votre application de fonction. Remplacez également `<my_resource_group>` par le nom du groupe de ressources de votre application de fonction. Remplacez `<version>` par une version valide du runtime 1.x ou `beta` pour la version 2.0. 

Vous pouvez exécuter cette commande à partir de [Azure Cloud Shell](../cloud-shell/overview.md) en choisissant **Essayer** dans l’exemple de code qui précède. Vous pouvez également utiliser [Azure CLI en local](/cli/azure/install-azure-cli) pour exécuter cette commande après avoir lancé la commande [az login](/cli/azure#az_login) pour vous connecter.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Cibler le runtime 2.0 dans votre environnement de développement local](functions-run-local.md)

> [!div class="nextstepaction"]
> [Consulter les notes de publication pour les versions du runtime](https://github.com/Azure/azure-webjobs-sdk-script/releases)