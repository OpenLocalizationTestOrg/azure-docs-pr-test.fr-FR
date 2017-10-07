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
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="be925-103">Conception, création et déploiement d’Azure Logic Apps dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="be925-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="be925-104">Bien que hello [portail Azure](https://portal.azure.com/) offre un excellent moyen de vous toocreate et gérer Azure Logic Apps, vous pouvez utiliser Visual Studio pour concevoir, créer et déployer vos applications logiques.</span><span class="sxs-lookup"><span data-stu-id="be925-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toocreate and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="be925-105">Visual Studio fournit des outils riches comme hello Concepteur d’application logique pour vous toocreate logique applications, configurer des modèles de déploiement et d’automatisation et déployer un environnement de tooany.</span><span class="sxs-lookup"><span data-stu-id="be925-105">Visual Studio provides rich tools like hello Logic App Designer for you toocreate logic apps, configure deployment and automation templates, and deploy tooany environment.</span></span> 

<span data-ttu-id="be925-106">tooget main Azure Logic Apps, en savoir plus [comment toocreate votre première application logique Bonjour Azure portal](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="be925-106">tooget started with Azure Logic Apps, learn [how toocreate your first logic app in hello Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="be925-107">Procédure d’installation :</span><span class="sxs-lookup"><span data-stu-id="be925-107">Installation steps</span></span>

<span data-ttu-id="be925-108">tooinstall et configurer les outils de Visual Studio pour Azure Logic Apps, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="be925-108">tooinstall and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="be925-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="be925-109">Prerequisites</span></span>

* <span data-ttu-id="be925-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) ou Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="be925-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="be925-111">[Dernier kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou supérieur)</span><span class="sxs-lookup"><span data-stu-id="be925-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="be925-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="be925-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="be925-113">Web toohello d’accès lorsque vous utilisez le concepteur incorporé hello</span><span class="sxs-lookup"><span data-stu-id="be925-113">Access toohello web when using hello embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="be925-114">Installer les outils Visual Studio pour Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="be925-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="be925-115">Après avoir installé les composants requis de hello :</span><span class="sxs-lookup"><span data-stu-id="be925-115">After you install hello prerequisites:</span></span>

1. <span data-ttu-id="be925-116">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be925-116">Open Visual Studio.</span></span> <span data-ttu-id="be925-117">Sur hello **outils** menu, sélectionnez **Extensions et mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="be925-117">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="be925-118">Développez hello **Online** catégorie, vous pouvez rechercher en ligne.</span><span class="sxs-lookup"><span data-stu-id="be925-118">Expand hello **Online** category so you can search online.</span></span>
3. <span data-ttu-id="be925-119">Parcourez les résultats ou recherchez **Logic Apps** jusqu’à ce que vous trouviez **Outils Azure Logic Apps pour Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="be925-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="be925-120">toodownload et installer une extension hello, cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="be925-120">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="be925-121">Redémarrez Visual Studio après l’installation.</span><span class="sxs-lookup"><span data-stu-id="be925-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="be925-122">Vous pouvez également télécharger [Azure logique applications Tools pour Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) et hello [Azure logique applications Tools pour Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directement à partir de hello Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="be925-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and hello [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from hello Visual Studio Marketplace.</span></span>

<span data-ttu-id="be925-123">Une fois l’installation terminée, vous pouvez utiliser le projet de groupe de ressources Azure hello avec le Concepteur de la logique d’application.</span><span class="sxs-lookup"><span data-stu-id="be925-123">After you finish installation, you can use hello Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="be925-124">Créer votre projet</span><span class="sxs-lookup"><span data-stu-id="be925-124">Create your project</span></span>

1. <span data-ttu-id="be925-125">Sur hello **fichier** menu, accédez trop**nouveau**, puis sélectionnez **projet**.</span><span class="sxs-lookup"><span data-stu-id="be925-125">On hello **File** menu, go too**New**, and select **Project**.</span></span> <span data-ttu-id="be925-126">Ou tooadd votre tooan projet existant de solution, accédez trop**ajouter**, puis sélectionnez **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="be925-126">Or tooadd your project tooan existing solution, go too**Add**, and select **New Project**.</span></span>

    ![Menu Fichier](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="be925-128">Bonjour **nouveau projet** fenêtre, recherchez **Cloud**, puis sélectionnez **groupe de ressources Azure**.</span><span class="sxs-lookup"><span data-stu-id="be925-128">In hello **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="be925-129">Nommez votre projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="be925-129">Name your project, and click **OK**.</span></span>

    ![Ajouter un nouveau projet](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="be925-131">Sélectionnez hello **application logique** modèle qui crée un modèle de déploiement d’application vide logique pour vous toouse.</span><span class="sxs-lookup"><span data-stu-id="be925-131">Select hello **Logic App** template, which creates a blank logic app deployment template for you toouse.</span></span> <span data-ttu-id="be925-132">Après avoir sélectionné votre modèle, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="be925-132">After you select your template, click **OK**.</span></span>

    ![Sélectionner le modèle Application logique](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="be925-134">Vous avez maintenant ajouté votre solution de tooyour de projet Application logique.</span><span class="sxs-lookup"><span data-stu-id="be925-134">You've now added your logic app project tooyour solution.</span></span> 
    <span data-ttu-id="be925-135">Dans l’Explorateur de solutions de hello, votre fichier de déploiement doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="be925-135">In hello Solution Explorer, your deployment file should appear.</span></span>

    ![Fichier de déploiement](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="be925-137">Créer votre application logique avec le Concepteur d’application logique</span><span class="sxs-lookup"><span data-stu-id="be925-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="be925-138">Lorsque vous avez un projet de groupe de ressources Azure qui contient une application logique, vous pouvez ouvrir hello Concepteur de logique d’application dans Visual Studio toocreate votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="be925-138">When you have an Azure Resource Group project that contains a logic app, you can open hello Logic App Designer in Visual Studio toocreate your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="be925-139">le concepteur Hello requiert une connexion internet trop connecteurs pour les propriétés disponibles et les données de requête.</span><span class="sxs-lookup"><span data-stu-id="be925-139">hello designer requires an internet connection too query connectors for available properties and data.</span></span> <span data-ttu-id="be925-140">Par exemple, si vous utilisez le connecteur de Dynamics CRM Online hello, Concepteur de hello interroge votre personnalisé CRM instance tooshow disponible et les propriétés par défaut.</span><span class="sxs-lookup"><span data-stu-id="be925-140">For example, if you use hello Dynamics CRM Online connector, hello designer queries your CRM instance tooshow available custom and default properties.</span></span>

1. <span data-ttu-id="be925-141">Cliquez avec le bouton droit sur votre fichier `<template>.json` et sélectionnez **Ouvrir avec le concepteur d’application logique**.</span><span class="sxs-lookup"><span data-stu-id="be925-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="be925-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="be925-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="be925-143">Choisissez votre abonnement Azure, le groupe de ressources et l’emplacement de votre modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="be925-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="be925-144">La conception d’une application logique crée des ressources Connexion d’API pour rechercher des propriétés lors de la conception.</span><span class="sxs-lookup"><span data-stu-id="be925-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="be925-145">Visual Studio utilise votre toocreate de groupe de ressources sélectionné ces connexions au moment du design.</span><span class="sxs-lookup"><span data-stu-id="be925-145">Visual Studio uses your selected resource group toocreate those connections during design time.</span></span> <span data-ttu-id="be925-146">tooview ou modifier les connexions de l’API, accédez toohello portail Azure et recherchez **API connexions**.</span><span class="sxs-lookup"><span data-stu-id="be925-146">tooview or change any API Connections, go toohello Azure portal, and browse for **API Connections**.</span></span>

    ![Sélecteur d’abonnement](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="be925-148">le concepteur Hello utilise la définition de hello Bonjour `<template>.json` fichier pour le rendu.</span><span class="sxs-lookup"><span data-stu-id="be925-148">hello designer uses hello definition in hello `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="be925-149">Créez et concevez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="be925-149">Create and design your logic app.</span></span> <span data-ttu-id="be925-150">Votre modèle de déploiement est mis à jour avec vos modifications.</span><span class="sxs-lookup"><span data-stu-id="be925-150">Your deployment template is updated with your changes.</span></span>

    ![Concepteur d’applications logiques dans Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="be925-152">Visual Studio ajoute `Microsoft.Web/connections` trop votre ressource de fichier de ressources pour toutes les connexions toofunction a besoin de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="be925-152">Visual Studio adds `Microsoft.Web/connections` resources too your resource file for any connections your logic app needs toofunction.</span></span> <span data-ttu-id="be925-153">Ces propriétés de connexion peuvent être définies lorsque vous déployez et gérées après le déploiement dans **API connexions** Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="be925-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in hello Azure portal.</span></span>

### <a name="switch-toojson-code-view"></a><span data-ttu-id="be925-154">Basculer l’affichage du code tooJSON</span><span class="sxs-lookup"><span data-stu-id="be925-154">Switch tooJSON code view</span></span>

<span data-ttu-id="be925-155">tooshow hello représentation JSON pour votre application logique, sélectionnez hello **mode Code** onglet en bas de hello du Concepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="be925-155">tooshow hello JSON representation for your logic app, select hello **Code View** tab at hello bottom of hello designer.</span></span>

<span data-ttu-id="be925-156">tooswitch sauvegarder toohello de ressources complet JSON, avec le bouton droit hello `<template>.json` de fichiers, puis sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="be925-156">tooswitch back toohello full resource JSON, right-click hello `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a><span data-ttu-id="be925-157">Ajoutez les références de modèles de déploiement de ressources dépendantes tooVisual Studio</span><span class="sxs-lookup"><span data-stu-id="be925-157">Add references for dependent resources tooVisual Studio deployment templates</span></span>

<span data-ttu-id="be925-158">Lorsque vous souhaitez que votre logique application tooreference des ressources dépendantes, vous pouvez utiliser [fonctions de modèle Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) dans votre modèle de déploiement d’application logique.</span><span class="sxs-lookup"><span data-stu-id="be925-158">When you want your logic app tooreference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="be925-159">Par exemple, vous souhaiterez peut-être votre tooreference d’application logique un compte Azure fonction ou d’intégration que vous souhaitez toodeploy en même temps que votre application logique.</span><span class="sxs-lookup"><span data-stu-id="be925-159">For example, you might want your logic app tooreference an Azure Function or integration account that you want toodeploy alongside your logic app.</span></span> <span data-ttu-id="be925-160">Suivez les recommandations sur les paramètres toouse dans votre modèle de déploiement afin que hello Concepteur d’application logique de rendu de correctement.</span><span class="sxs-lookup"><span data-stu-id="be925-160">Follow these guidelines about how toouse parameters in your deployment template so that hello Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="be925-161">Vous pouvez utiliser les paramètres d’application logique dans ces types de déclencheurs et d’actions :</span><span class="sxs-lookup"><span data-stu-id="be925-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="be925-162">Flux de travail enfant</span><span class="sxs-lookup"><span data-stu-id="be925-162">Child workflow</span></span>
*   <span data-ttu-id="be925-163">Conteneur de fonctions</span><span class="sxs-lookup"><span data-stu-id="be925-163">Function app</span></span>
*   <span data-ttu-id="be925-164">Appel APIM</span><span class="sxs-lookup"><span data-stu-id="be925-164">APIM call</span></span>
*   <span data-ttu-id="be925-165">URL d’exécution de connexion d’API</span><span class="sxs-lookup"><span data-stu-id="be925-165">API connection runtime URL</span></span>
*   <span data-ttu-id="be925-166">Chemin de connexion d’API</span><span class="sxs-lookup"><span data-stu-id="be925-166">API connection path</span></span>

<span data-ttu-id="be925-167">Vous pouvez utiliser les fonctions de modèle, telles que les paramètres, les variables, resourceId, concat, etc. Par exemple, voici comment vous pouvez remplacer l’ID de ressource Azure fonction hello :</span><span class="sxs-lookup"><span data-stu-id="be925-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace hello Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="be925-168">Et où vous pouvez utiliser les paramètres :</span><span class="sxs-lookup"><span data-stu-id="be925-168">And where you would use parameters:</span></span>

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
<span data-ttu-id="be925-169">Autre exemple, vous pouvez paramétrer hello message opération d’envoi de Service Bus :</span><span class="sxs-lookup"><span data-stu-id="be925-169">As another example you can parameterize hello Service Bus send message operation:</span></span>

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
> <span data-ttu-id="be925-170">host.runtimeUrl est facultatif et peut être supprimé de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="be925-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="be925-171">Pour toowork du Concepteur d’application logique hello lorsque vous utilisez des paramètres, vous devez fournir les valeurs par défaut, par exemple :</span><span class="sxs-lookup"><span data-stu-id="be925-171">For hello Logic App Designer toowork when you use parameters, you must provide default values, for example:</span></span>
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

### <a name="save-your-logic-app"></a><span data-ttu-id="be925-172">Enregistrer votre application logique</span><span class="sxs-lookup"><span data-stu-id="be925-172">Save your logic app</span></span>

<span data-ttu-id="be925-173">toosave votre application logique à tout moment, accédez trop**fichier** > **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="be925-173">toosave your logic app at anytime, go too**File** > **Save**.</span></span> <span data-ttu-id="be925-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="be925-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="be925-175">Si votre application logique a des erreurs lorsque vous enregistrez votre application, ils apparaissent dans hello Visual Studio **sorties** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="be925-175">If your logic app has any errors when you save your app, they appear in hello Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="be925-176">Déploiement de votre application logique à partir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="be925-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="be925-177">Après avoir configuré votre application, vous pouvez procéder directement au déploiement depuis Visual Studio en quelques étapes.</span><span class="sxs-lookup"><span data-stu-id="be925-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="be925-178">Dans l’Explorateur de solutions, cliquez sur votre projet et accédez trop**déployer** > **nouveau déploiement...**</span><span class="sxs-lookup"><span data-stu-id="be925-178">In Solution Explorer, right-click your project, and go too**Deploy** > **New Deployment...**</span></span>

    ![Nouveau déploiement](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="be925-180">Lorsque vous y êtes invité, connectez-vous tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="be925-180">When you're prompted, sign in tooyour Azure subscription.</span></span> 

3. <span data-ttu-id="be925-181">Maintenant, vous devez sélectionner les détails de hello hello groupe de ressources où vous souhaitez toodeploy votre application logique.</span><span class="sxs-lookup"><span data-stu-id="be925-181">Now you must select hello details for hello resource group where you want toodeploy your logic app.</span></span> <span data-ttu-id="be925-182">Quand vous avez terminé, sélectionnez **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="be925-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="be925-183">Assurez-vous que vous sélectionnez un modèle correct de hello et un fichier de paramètres pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="be925-183">Make sure that you select hello correct template and parameters file for hello resource group.</span></span> <span data-ttu-id="be925-184">Par exemple, si vous souhaitez environnement de production toodeploy tooa, choisissez le fichier de paramètres de production hello.</span><span class="sxs-lookup"><span data-stu-id="be925-184">For example, if you want toodeploy tooa production environment, choose hello production parameters file.</span></span>

    ![Déployer le groupe de tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="be925-186">état du déploiement Hello s’affiche dans hello **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="be925-186">hello deployment status appears in hello **Output** window.</span></span> 
    <span data-ttu-id="be925-187">Vous pouvez avoir tooselect **Azure approvisionnement** Bonjour **afficher la sortie à partir de** liste.</span><span class="sxs-lookup"><span data-stu-id="be925-187">You might have tooselect **Azure Provisioning** in hello **Show output from** list.</span></span>

    ![Sortie d’état du déploiement](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="be925-189">Bonjour futures, vous pouvez modifier votre application de la logique de contrôle de code source et utiliser les nouvelles versions de Visual Studio toodeploy.</span><span class="sxs-lookup"><span data-stu-id="be925-189">In hello future, you can edit your logic app in source control, and use Visual Studio toodeploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="be925-190">Si vous modifiez directement définition hello Bonjour portail Azure, ces modifications sont remplacées lorsque vous déployez à partir de Visual Studio prochaine.</span><span class="sxs-lookup"><span data-stu-id="be925-190">If you change hello definition in hello Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a><span data-ttu-id="be925-191">Ajoutez votre projet de groupe de ressources existant logique application tooan</span><span class="sxs-lookup"><span data-stu-id="be925-191">Add your logic app tooan existing Resource Group project</span></span>

<span data-ttu-id="be925-192">Si vous avez un projet de groupe de ressources existant, vous pouvez ajouter votre projet toothat d’application logique dans la fenêtre de structure JSON hello.</span><span class="sxs-lookup"><span data-stu-id="be925-192">If you have an existing Resource Group project, you can add your logic app toothat project in hello JSON Outline window.</span></span> <span data-ttu-id="be925-193">Vous pouvez également ajouter une autre application logique en même temps que l’application hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="be925-193">You can also add another logic app alongside hello app you previously created.</span></span>

1. <span data-ttu-id="be925-194">Ouvrez hello `<template>.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="be925-194">Open hello `<template>.json` file.</span></span>

2. <span data-ttu-id="be925-195">tooopen hello fenêtre Plan JSON, accédez trop**vue** > **autres fenêtres** > **structure JSON**.</span><span class="sxs-lookup"><span data-stu-id="be925-195">tooopen hello JSON Outline window, go too**View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="be925-196">tooadd un fichier de modèle toohello de ressources, cliquez sur **ajouter une ressource** haut hello de fenêtre de structure JSON hello.</span><span class="sxs-lookup"><span data-stu-id="be925-196">tooadd a resource toohello template file, click **Add Resource** at hello top of hello JSON Outline window.</span></span> <span data-ttu-id="be925-197">Ou dans la fenêtre Structure JSON de hello, cliquez sur **ressources**, puis sélectionnez **ajouter une nouvelle ressource**.</span><span class="sxs-lookup"><span data-stu-id="be925-197">Or in hello JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![Fenêtre Structure JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="be925-199">Bonjour **ajouter une ressource** boîte de dialogue, recherchez et sélectionnez **application logique**.</span><span class="sxs-lookup"><span data-stu-id="be925-199">In hello **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="be925-200">Donnez un nom à votre application logique, puis choisissez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="be925-200">Name your logic app, and choose **Add**.</span></span>

    ![Ajouter une ressource](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="be925-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="be925-202">Next Steps</span></span>

* [<span data-ttu-id="be925-203">Gérer les applications logiques à l’aide de Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="be925-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="be925-204">Afficher des exemples et des scénarios courants</span><span class="sxs-lookup"><span data-stu-id="be925-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="be925-205">Découvrez comment les processus d’entreprise de tooautomate avec Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="be925-205">Learn how tooautomate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="be925-206">Découvrez comment toointegrate vos systèmes avec Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="be925-206">Learn how toointegrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
