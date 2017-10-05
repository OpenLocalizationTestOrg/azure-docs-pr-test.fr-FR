---
title: "Création, génération et déploiement d’applications logiques dans Visual Studio - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: e7f5cf483d22e4c60dedbe5176ceb0bc8b2b6e66
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="ffa45-103">Conception, création et déploiement d’Azure Logic Apps dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ffa45-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="ffa45-104">Bien que le [portail Azure](https://portal.azure.com/) constitue un excellent moyen pour créer et gérer Azure Logic Apps, vous pouvez utiliser Visual Studio afin de concevoir, créer et déployer vos applications logiques.</span><span class="sxs-lookup"><span data-stu-id="ffa45-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to create and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="ffa45-105">Visual Studio met à votre disposition des outils riches tels que le Concepteur d’application logique pour vous permettre de créer des applications logiques, de configurer les modèles de déploiement et d’automatisation, et de déployer sur n’importe quel environnement.</span><span class="sxs-lookup"><span data-stu-id="ffa45-105">Visual Studio provides rich tools like the Logic App Designer for you to create logic apps, configure deployment and automation templates, and deploy to any environment.</span></span> 

<span data-ttu-id="ffa45-106">Pour vous familiariser avec Azure Logic Apps, consultez la rubrique [Créez votre première application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ffa45-106">To get started with Azure Logic Apps, learn [how to create your first logic app in the Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="ffa45-107">Procédure d’installation :</span><span class="sxs-lookup"><span data-stu-id="ffa45-107">Installation steps</span></span>

<span data-ttu-id="ffa45-108">Pour installer et configurer les outils Visual Studio pour Azure Logic Apps, suivez ces étapes.</span><span class="sxs-lookup"><span data-stu-id="ffa45-108">To install and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ffa45-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ffa45-109">Prerequisites</span></span>

* <span data-ttu-id="ffa45-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) ou Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ffa45-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="ffa45-111">[Dernier kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou supérieur)</span><span class="sxs-lookup"><span data-stu-id="ffa45-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="ffa45-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffa45-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="ffa45-113">Accès au web lors de l’utilisation du concepteur intégré</span><span class="sxs-lookup"><span data-stu-id="ffa45-113">Access to the web when using the embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="ffa45-114">Installer les outils Visual Studio pour Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ffa45-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="ffa45-115">Une fois les composants requis installés :</span><span class="sxs-lookup"><span data-stu-id="ffa45-115">After you install the prerequisites:</span></span>

1. <span data-ttu-id="ffa45-116">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ffa45-116">Open Visual Studio.</span></span> <span data-ttu-id="ffa45-117">Dans le menu **Outils**, sélectionnez **Extensions et mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-117">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="ffa45-118">Développez la catégorie **En ligne** pour effectuer une recherche en ligne.</span><span class="sxs-lookup"><span data-stu-id="ffa45-118">Expand the **Online** category so you can search online.</span></span>
3. <span data-ttu-id="ffa45-119">Parcourez les résultats ou recherchez **Logic Apps** jusqu’à ce que vous trouviez **Outils Azure Logic Apps pour Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="ffa45-120">Pour télécharger et installer l’extension, cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-120">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="ffa45-121">Redémarrez Visual Studio après l’installation.</span><span class="sxs-lookup"><span data-stu-id="ffa45-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="ffa45-122">Vous pouvez également télécharger les [Outils Azure Logic Apps pour Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) et les [Outils Azure Logic Apps pour Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directement à partir de la Place de marché Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ffa45-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and the [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from the Visual Studio Marketplace.</span></span>

<span data-ttu-id="ffa45-123">Une fois l’installation effectuée, vous pouvez utiliser le projet de groupe de ressources Azure avec le Concepteur d’applications logiques.</span><span class="sxs-lookup"><span data-stu-id="ffa45-123">After you finish installation, you can use the Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="ffa45-124">Créer votre projet</span><span class="sxs-lookup"><span data-stu-id="ffa45-124">Create your project</span></span>

1. <span data-ttu-id="ffa45-125">Dans le menu **Fichier**, accédez à **Nouveau**, puis sélectionnez **Projet**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-125">On the **File** menu, go to **New**, and select **Project**.</span></span> <span data-ttu-id="ffa45-126">Ou pour ajouter votre projet à une solution existante, accédez à **Ajouter**, puis sélectionnez **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-126">Or to add your project to an existing solution, go to **Add**, and select **New Project**.</span></span>

    ![Menu Fichier](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="ffa45-128">Dans la fenêtre **Nouveau projet**, recherchez **Cloud**, puis sélectionnez **Groupe de ressources Azure**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-128">In the **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="ffa45-129">Nommez votre projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-129">Name your project, and click **OK**.</span></span>

    ![Ajouter un nouveau projet](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="ffa45-131">Sélectionnez le modèle **Application logique**, qui crée un modèle vierge de déploiement d’application logique que vous pourrez utiliser.</span><span class="sxs-lookup"><span data-stu-id="ffa45-131">Select the **Logic App** template, which creates a blank logic app deployment template for you to use.</span></span> <span data-ttu-id="ffa45-132">Après avoir sélectionné votre modèle, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-132">After you select your template, click **OK**.</span></span>

    ![Sélectionner le modèle Application logique](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="ffa45-134">Vous avez ajouté votre projet d’application logique à votre solution.</span><span class="sxs-lookup"><span data-stu-id="ffa45-134">You've now added your logic app project to your solution.</span></span> 
    <span data-ttu-id="ffa45-135">Votre fichier de déploiement doit apparaître dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="ffa45-135">In the Solution Explorer, your deployment file should appear.</span></span>

    ![Fichier de déploiement](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="ffa45-137">Créer votre application logique avec le Concepteur d’application logique</span><span class="sxs-lookup"><span data-stu-id="ffa45-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="ffa45-138">Une fois que vous disposez d’un projet de groupe de ressources Azure contenant une application logique, vous pouvez ouvrir le Concepteur d’applications logiques dans Visual Studio pour créer votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="ffa45-138">When you have an Azure Resource Group project that contains a logic app, you can open the Logic App Designer in Visual Studio to create your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="ffa45-139">Pour demander les propriétés et données disponibles aux connecteurs, le concepteur doit disposer d’une connexion à Internet.</span><span class="sxs-lookup"><span data-stu-id="ffa45-139">The designer requires an internet connection to query connectors for available properties and data.</span></span> <span data-ttu-id="ffa45-140">Par exemple, si vous utilisez le connecteur Dynamics CRM Online, le concepteur interroge votre instance CRM pour afficher les propriétés par défaut et personnalisées disponibles.</span><span class="sxs-lookup"><span data-stu-id="ffa45-140">For example, if you use the Dynamics CRM Online connector, the designer queries your CRM instance to show available custom and default properties.</span></span>

1. <span data-ttu-id="ffa45-141">Cliquez avec le bouton droit sur votre fichier `<template>.json` et sélectionnez **Ouvrir avec le concepteur d’application logique**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="ffa45-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="ffa45-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="ffa45-143">Choisissez votre abonnement Azure, le groupe de ressources et l’emplacement de votre modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="ffa45-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ffa45-144">La conception d’une application logique crée des ressources Connexion d’API pour rechercher des propriétés lors de la conception.</span><span class="sxs-lookup"><span data-stu-id="ffa45-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="ffa45-145">Visual Studio utilise le groupe de ressources sélectionné pour créer ces connexions au moment de la conception.</span><span class="sxs-lookup"><span data-stu-id="ffa45-145">Visual Studio uses your selected resource group to create those connections during design time.</span></span> <span data-ttu-id="ffa45-146">Pour afficher ou modifier les connexions d’API, accédez au portail Azure, et recherchez **Connexions d’API**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-146">To view or change any API Connections, go to the Azure portal, and browse for **API Connections**.</span></span>

    ![Sélecteur d’abonnement](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="ffa45-148">Le concepteur utilise la définition du fichier `<template>.json` pour le rendu.</span><span class="sxs-lookup"><span data-stu-id="ffa45-148">The designer uses the definition in the `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="ffa45-149">Créez et concevez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="ffa45-149">Create and design your logic app.</span></span> <span data-ttu-id="ffa45-150">Votre modèle de déploiement est mis à jour avec vos modifications.</span><span class="sxs-lookup"><span data-stu-id="ffa45-150">Your deployment template is updated with your changes.</span></span>

    ![Concepteur d’applications logiques dans Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="ffa45-152">Visual Studio ajoute des ressources `Microsoft.Web/connections` à votre fichier de ressources pour toutes les connexions nécessaires au fonctionnement de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="ffa45-152">Visual Studio adds `Microsoft.Web/connections` resources to your resource file for any connections your logic app needs to function.</span></span> <span data-ttu-id="ffa45-153">Ces propriétés de connexion peuvent être définies lors du déploiement et être gérées après le déploiement via le menu **Connexions d’API** du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa45-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in the Azure portal.</span></span>

### <a name="switch-to-json-code-view"></a><span data-ttu-id="ffa45-154">Basculer en mode code JSON</span><span class="sxs-lookup"><span data-stu-id="ffa45-154">Switch to JSON code view</span></span>

<span data-ttu-id="ffa45-155">Pour afficher la représentation JSON de votre application logique, sélectionnez l’onglet **Mode Code** situé en bas du concepteur.</span><span class="sxs-lookup"><span data-stu-id="ffa45-155">To show the JSON representation for your logic app, select the **Code View** tab at the bottom of the designer.</span></span>

<span data-ttu-id="ffa45-156">Pour revenir au code JSON de la ressource complète, cliquez sur le fichier `<template>.json` et sélectionnez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-156">To switch back to the full resource JSON, right-click the `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-to-visual-studio-deployment-templates"></a><span data-ttu-id="ffa45-157">Ajouter les références des ressources dépendantes aux modèles de déploiement Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ffa45-157">Add references for dependent resources to Visual Studio deployment templates</span></span>

<span data-ttu-id="ffa45-158">Si vous souhaitez que votre application logique référence des ressources dépendantes, vous pouvez utiliser les [fonctions de gabarit Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) dans votre modèle de déploiement d’application logique.</span><span class="sxs-lookup"><span data-stu-id="ffa45-158">When you want your logic app to reference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="ffa45-159">Par exemple, vous souhaiterez peut-être que votre application logique référence une fonction Azure ou un compte d’intégration que vous souhaitez déployer avec votre application logique.</span><span class="sxs-lookup"><span data-stu-id="ffa45-159">For example, you might want your logic app to reference an Azure Function or integration account that you want to deploy alongside your logic app.</span></span> <span data-ttu-id="ffa45-160">Suivez ces instructions pour utiliser les paramètres dans votre modèle de déploiement afin que le Concepteur d’applications logiques offre un rendu correct.</span><span class="sxs-lookup"><span data-stu-id="ffa45-160">Follow these guidelines about how to use parameters in your deployment template so that the Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="ffa45-161">Vous pouvez utiliser les paramètres d’application logique dans ces types de déclencheurs et d’actions :</span><span class="sxs-lookup"><span data-stu-id="ffa45-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="ffa45-162">Flux de travail enfant</span><span class="sxs-lookup"><span data-stu-id="ffa45-162">Child workflow</span></span>
*   <span data-ttu-id="ffa45-163">Conteneur de fonctions</span><span class="sxs-lookup"><span data-stu-id="ffa45-163">Function app</span></span>
*   <span data-ttu-id="ffa45-164">Appel APIM</span><span class="sxs-lookup"><span data-stu-id="ffa45-164">APIM call</span></span>
*   <span data-ttu-id="ffa45-165">URL d’exécution de connexion d’API</span><span class="sxs-lookup"><span data-stu-id="ffa45-165">API connection runtime URL</span></span>
*   <span data-ttu-id="ffa45-166">Chemin de connexion d’API</span><span class="sxs-lookup"><span data-stu-id="ffa45-166">API connection path</span></span>

<span data-ttu-id="ffa45-167">Vous pouvez utiliser les fonctions de modèle, telles que les paramètres, les variables, resourceId, concat, etc. Par exemple, voici par quoi vous pouvez remplacer l’ID de ressource de fonction Azure :</span><span class="sxs-lookup"><span data-stu-id="ffa45-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace the Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="ffa45-168">Et où vous pouvez utiliser les paramètres :</span><span class="sxs-lookup"><span data-stu-id="ffa45-168">And where you would use parameters:</span></span>

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
<span data-ttu-id="ffa45-169">Vous pouvez, par exemple, paramétrer l’opération d’envoi de message Service Bus :</span><span class="sxs-lookup"><span data-stu-id="ffa45-169">As another example you can parameterize the Service Bus send message operation:</span></span>

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
> <span data-ttu-id="ffa45-170">host.runtimeUrl est facultatif et peut être supprimé de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="ffa45-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="ffa45-171">Pour que le Concepteur d’applications logiques fonctionne lorsque vous utilisez des paramètres, vous devez fournir des valeurs par défaut, par exemple :</span><span class="sxs-lookup"><span data-stu-id="ffa45-171">For the Logic App Designer to work when you use parameters, you must provide default values, for example:</span></span>
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

### <a name="save-your-logic-app"></a><span data-ttu-id="ffa45-172">Enregistrer votre application logique</span><span class="sxs-lookup"><span data-stu-id="ffa45-172">Save your logic app</span></span>

<span data-ttu-id="ffa45-173">Pour enregistrer votre application logique à tout moment, accédez à **Fichier** > **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-173">To save your logic app at anytime, go to **File** > **Save**.</span></span> <span data-ttu-id="ffa45-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="ffa45-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="ffa45-175">Si votre application logique comporte des erreurs lors de son enregistrement, elles sont répertoriées dans la fenêtre **Sorties** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ffa45-175">If your logic app has any errors when you save your app, they appear in the Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="ffa45-176">Déploiement de votre application logique à partir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ffa45-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="ffa45-177">Après avoir configuré votre application, vous pouvez procéder directement au déploiement depuis Visual Studio en quelques étapes.</span><span class="sxs-lookup"><span data-stu-id="ffa45-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="ffa45-178">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet, puis sélectionnez **Déployer** > **Nouveau déploiement...**</span><span class="sxs-lookup"><span data-stu-id="ffa45-178">In Solution Explorer, right-click your project, and go to **Deploy** > **New Deployment...**</span></span>

    ![Nouveau déploiement](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="ffa45-180">Lorsque vous y êtes invité, connectez-vous à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa45-180">When you're prompted, sign in to your Azure subscription.</span></span> 

3. <span data-ttu-id="ffa45-181">Vous devez alors sélectionner les informations du groupe de ressources dans lequel vous souhaitez déployer votre application logique.</span><span class="sxs-lookup"><span data-stu-id="ffa45-181">Now you must select the details for the resource group where you want to deploy your logic app.</span></span> <span data-ttu-id="ffa45-182">Quand vous avez terminé, sélectionnez **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ffa45-183">Assurez-vous que vous sélectionnez le bon modèle et les paramètres adéquats pour le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ffa45-183">Make sure that you select the correct template and parameters file for the resource group.</span></span> <span data-ttu-id="ffa45-184">Par exemple, si vous souhaitez déployer dans un environnement de production, choisissez le fichier de paramètres de production.</span><span class="sxs-lookup"><span data-stu-id="ffa45-184">For example, if you want to deploy to a production environment, choose the production parameters file.</span></span>

    ![Déploiement vers un groupe de ressources](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="ffa45-186">L’état du déploiement s’affiche dans la fenêtre **Sortie**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-186">The deployment status appears in the **Output** window.</span></span> 
    <span data-ttu-id="ffa45-187">Vous devrez peut-être sélectionner **Approvisionnement Azure** dans la liste **Afficher la sortie à partir de**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-187">You might have to select **Azure Provisioning** in the **Show output from** list.</span></span>

    ![Sortie d’état du déploiement](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="ffa45-189">À l’avenir, vous pourrez modifier votre application logique dans le contrôle de code source et utiliser Visual Studio pour déployer de nouvelles versions.</span><span class="sxs-lookup"><span data-stu-id="ffa45-189">In the future, you can edit your logic app in source control, and use Visual Studio to deploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="ffa45-190">Si vous modifiez la définition directement dans le portail Azure, ces modifications seront remplacées lors de votre prochain déploiement à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ffa45-190">If you change the definition in the Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-to-an-existing-resource-group-project"></a><span data-ttu-id="ffa45-191">Ajouter votre application logique à un projet de groupe de ressources existant</span><span class="sxs-lookup"><span data-stu-id="ffa45-191">Add your logic app to an existing Resource Group project</span></span>

<span data-ttu-id="ffa45-192">Si vous disposez d’un projet de groupe de ressources existant, vous pouvez ajouter votre application logique à ce projet dans la fenêtre Structure JSON.</span><span class="sxs-lookup"><span data-stu-id="ffa45-192">If you have an existing Resource Group project, you can add your logic app to that project in the JSON Outline window.</span></span> <span data-ttu-id="ffa45-193">Vous pouvez également ajouter une autre application logique en même temps que l’application que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="ffa45-193">You can also add another logic app alongside the app you previously created.</span></span>

1. <span data-ttu-id="ffa45-194">Ouvrez le fichier `<template>.json` .</span><span class="sxs-lookup"><span data-stu-id="ffa45-194">Open the `<template>.json` file.</span></span>

2. <span data-ttu-id="ffa45-195">Pour ouvrir la fenêtre Structure JSON, rendez-vous à **Affichage** > **Autres fenêtres** > **Structure JSON**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-195">To open the JSON Outline window, go to **View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="ffa45-196">Pour ajouter une ressource au fichier de modèle, cliquez sur **Ajouter une ressource** en haut de la fenêtre Structure JSON.</span><span class="sxs-lookup"><span data-stu-id="ffa45-196">To add a resource to the template file, click **Add Resource** at the top of the JSON Outline window.</span></span> <span data-ttu-id="ffa45-197">Ou, dans la fenêtre Structure JSON, cliquez avec le bouton droit sur **Ressources**, puis sélectionnez **Ajouter une nouvelle ressource**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-197">Or in the JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![Fenêtre Structure JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="ffa45-199">Dans la boîte de dialogue **Ajouter une ressource**, recherchez et sélectionnez **Application logique**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-199">In the **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="ffa45-200">Donnez un nom à votre application logique, puis choisissez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ffa45-200">Name your logic app, and choose **Add**.</span></span>

    ![Ajouter une ressource](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="ffa45-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ffa45-202">Next Steps</span></span>

* [<span data-ttu-id="ffa45-203">Gérer les applications logiques à l’aide de Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="ffa45-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="ffa45-204">Afficher des exemples et des scénarios courants</span><span class="sxs-lookup"><span data-stu-id="ffa45-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="ffa45-205">Découvrez comment automatiser vos processus métiers avec Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ffa45-205">Learn how to automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="ffa45-206">Apprenez à intégrer vos systèmes avec Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ffa45-206">Learn how to integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
