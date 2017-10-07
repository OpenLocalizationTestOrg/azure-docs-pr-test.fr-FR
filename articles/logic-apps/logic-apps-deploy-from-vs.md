---
title: "aaaCreate, générer et déployer des applications de logique dans Visual Studio - Azure Logic Apps | Documents Microsoft"
description: "Créez des projets Visual Studio pour concevoir, développer et déployer Azure Logic Apps."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a>Conception, création et déploiement d’Azure Logic Apps dans Visual Studio

Bien que hello [portail Azure](https://portal.azure.com/) offre un excellent moyen de vous toocreate et gérer Azure Logic Apps, vous pouvez utiliser Visual Studio pour concevoir, créer et déployer vos applications logiques. Visual Studio fournit des outils riches comme hello Concepteur d’application logique pour vous toocreate logique applications, configurer des modèles de déploiement et d’automatisation et déployer un environnement de tooany. 

tooget main Azure Logic Apps, en savoir plus [comment toocreate votre première application logique Bonjour Azure portal](logic-apps-create-a-logic-app.md).

## <a name="installation-steps"></a>Procédure d’installation :

tooinstall et configurer les outils de Visual Studio pour Azure Logic Apps, procédez comme suit.

### <a name="prerequisites"></a>Composants requis

* [Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) ou Visual Studio 2015
* [Dernier kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou supérieur)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* Web toohello d’accès lorsque vous utilisez le concepteur incorporé hello

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a>Installer les outils Visual Studio pour Azure Logic Apps

Après avoir installé les composants requis de hello :

1. Ouvrez Visual Studio. Sur hello **outils** menu, sélectionnez **Extensions et mises à jour**.
2. Développez hello **Online** catégorie, vous pouvez rechercher en ligne.
3. Parcourez les résultats ou recherchez **Logic Apps** jusqu’à ce que vous trouviez **Outils Azure Logic Apps pour Visual Studio**.
4. toodownload et installer une extension hello, cliquez sur **télécharger**.
5. Redémarrez Visual Studio après l’installation.

> [!NOTE]
> Vous pouvez également télécharger [Azure logique applications Tools pour Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) et hello [Azure logique applications Tools pour Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directement à partir de hello Visual Studio Marketplace.

Une fois l’installation terminée, vous pouvez utiliser le projet de groupe de ressources Azure hello avec le Concepteur de la logique d’application.

## <a name="create-your-project"></a>Créer votre projet

1. Sur hello **fichier** menu, accédez trop**nouveau**, puis sélectionnez **projet**. Ou tooadd votre tooan projet existant de solution, accédez trop**ajouter**, puis sélectionnez **nouveau projet**.

    ![Menu Fichier](./media/logic-apps-deploy-from-vs/filemenu.png)

2. Bonjour **nouveau projet** fenêtre, recherchez **Cloud**, puis sélectionnez **groupe de ressources Azure**. Nommez votre projet, puis cliquez sur **OK**.

    ![Ajouter un nouveau projet](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. Sélectionnez hello **application logique** modèle qui crée un modèle de déploiement d’application vide logique pour vous toouse. Après avoir sélectionné votre modèle, cliquez sur **OK**.

    ![Sélectionner le modèle Application logique](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    Vous avez maintenant ajouté votre solution de tooyour de projet Application logique. 
    Dans l’Explorateur de solutions de hello, votre fichier de déploiement doit apparaître.

    ![Fichier de déploiement](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a>Créer votre application logique avec le Concepteur d’application logique

Lorsque vous avez un projet de groupe de ressources Azure qui contient une application logique, vous pouvez ouvrir hello Concepteur de logique d’application dans Visual Studio toocreate votre flux de travail. 

> [!NOTE]
> le concepteur Hello requiert une connexion internet trop connecteurs pour les propriétés disponibles et les données de requête. Par exemple, si vous utilisez le connecteur de Dynamics CRM Online hello, Concepteur de hello interroge votre personnalisé CRM instance tooshow disponible et les propriétés par défaut.

1. Cliquez avec le bouton droit sur votre fichier `<template>.json` et sélectionnez **Ouvrir avec le concepteur d’application logique**. (`Ctrl+L`)

2. Choisissez votre abonnement Azure, le groupe de ressources et l’emplacement de votre modèle de déploiement.

    > [!NOTE]
    > La conception d’une application logique crée des ressources Connexion d’API pour rechercher des propriétés lors de la conception. Visual Studio utilise votre toocreate de groupe de ressources sélectionné ces connexions au moment du design. tooview ou modifier les connexions de l’API, accédez toohello portail Azure et recherchez **API connexions**.

    ![Sélecteur d’abonnement](./media/logic-apps-deploy-from-vs/designer_picker.png)

    le concepteur Hello utilise la définition de hello Bonjour `<template>.json` fichier pour le rendu.

4. Créez et concevez votre application logique. Votre modèle de déploiement est mis à jour avec vos modifications.

    ![Concepteur d’applications logiques dans Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

Visual Studio ajoute `Microsoft.Web/connections` trop votre ressource de fichier de ressources pour toutes les connexions toofunction a besoin de votre application logique. Ces propriétés de connexion peuvent être définies lorsque vous déployez et gérées après le déploiement dans **API connexions** Bonjour portail Azure.

### <a name="switch-toojson-code-view"></a>Basculer l’affichage du code tooJSON

tooshow hello représentation JSON pour votre application logique, sélectionnez hello **mode Code** onglet en bas de hello du Concepteur de hello.

tooswitch sauvegarder toohello de ressources complet JSON, avec le bouton droit hello `<template>.json` de fichiers, puis sélectionnez **ouvrir**.

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a>Ajoutez les références de modèles de déploiement de ressources dépendantes tooVisual Studio

Lorsque vous souhaitez que votre logique application tooreference des ressources dépendantes, vous pouvez utiliser [fonctions de modèle Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) dans votre modèle de déploiement d’application logique. Par exemple, vous souhaiterez peut-être votre tooreference d’application logique un compte Azure fonction ou d’intégration que vous souhaitez toodeploy en même temps que votre application logique. Suivez les recommandations sur les paramètres toouse dans votre modèle de déploiement afin que hello Concepteur d’application logique de rendu de correctement. 

Vous pouvez utiliser les paramètres d’application logique dans ces types de déclencheurs et d’actions :

*   Flux de travail enfant
*   Conteneur de fonctions
*   Appel APIM
*   URL d’exécution de connexion d’API
*   Chemin de connexion d’API

Vous pouvez utiliser les fonctions de modèle, telles que les paramètres, les variables, resourceId, concat, etc. Par exemple, voici comment vous pouvez remplacer l’ID de ressource Azure fonction hello :

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

Et où vous pouvez utiliser les paramètres :

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
Autre exemple, vous pouvez paramétrer hello message opération d’envoi de Service Bus :

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> host.runtimeUrl est facultatif et peut être supprimé de votre modèle.
> 


> [!NOTE] 
> Pour toowork du Concepteur d’application logique hello lorsque vous utilisez des paramètres, vous devez fournir les valeurs par défaut, par exemple :
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a>Enregistrer votre application logique

toosave votre application logique à tout moment, accédez trop**fichier** > **enregistrer**. (`Ctrl+S`) 

Si votre application logique a des erreurs lorsque vous enregistrez votre application, ils apparaissent dans hello Visual Studio **sorties** fenêtre.

## <a name="deploy-your-logic-app-from-visual-studio"></a>Déploiement de votre application logique à partir de Visual Studio

Après avoir configuré votre application, vous pouvez procéder directement au déploiement depuis Visual Studio en quelques étapes. 

1. Dans l’Explorateur de solutions, cliquez sur votre projet et accédez trop**déployer** > **nouveau déploiement...**

    ![Nouveau déploiement](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. Lorsque vous y êtes invité, connectez-vous tooyour abonnement Azure. 

3. Maintenant, vous devez sélectionner les détails de hello hello groupe de ressources où vous souhaitez toodeploy votre application logique. Quand vous avez terminé, sélectionnez **Déployer**.

    > [!NOTE]
    > Assurez-vous que vous sélectionnez un modèle correct de hello et un fichier de paramètres pour le groupe de ressources hello. Par exemple, si vous souhaitez environnement de production toodeploy tooa, choisissez le fichier de paramètres de production hello.

    ![Déployer le groupe de tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    état du déploiement Hello s’affiche dans hello **sortie** fenêtre. 
    Vous pouvez avoir tooselect **Azure approvisionnement** Bonjour **afficher la sortie à partir de** liste.

    ![Sortie d’état du déploiement](./media/logic-apps-deploy-from-vs/output.png)

Bonjour futures, vous pouvez modifier votre application de la logique de contrôle de code source et utiliser les nouvelles versions de Visual Studio toodeploy.

> [!NOTE]
> Si vous modifiez directement définition hello Bonjour portail Azure, ces modifications sont remplacées lorsque vous déployez à partir de Visual Studio prochaine. 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a>Ajoutez votre projet de groupe de ressources existant logique application tooan

Si vous avez un projet de groupe de ressources existant, vous pouvez ajouter votre projet toothat d’application logique dans la fenêtre de structure JSON hello. Vous pouvez également ajouter une autre application logique en même temps que l’application hello que vous avez créé précédemment.

1. Ouvrez hello `<template>.json` fichier.

2. tooopen hello fenêtre Plan JSON, accédez trop**vue** > **autres fenêtres** > **structure JSON**.

3. tooadd un fichier de modèle toohello de ressources, cliquez sur **ajouter une ressource** haut hello de fenêtre de structure JSON hello. Ou dans la fenêtre Structure JSON de hello, cliquez sur **ressources**, puis sélectionnez **ajouter une nouvelle ressource**.

    ![Fenêtre Structure JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. Bonjour **ajouter une ressource** boîte de dialogue, recherchez et sélectionnez **application logique**. Donnez un nom à votre application logique, puis choisissez **Ajouter**.

    ![Ajouter une ressource](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a>Étapes suivantes

* [Gérer les applications logiques à l’aide de Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Afficher des exemples et des scénarios courants](logic-apps-examples-and-scenarios.md)
* [Découvrez comment les processus d’entreprise de tooautomate avec Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)
* [Découvrez comment toointegrate vos systèmes avec Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)
