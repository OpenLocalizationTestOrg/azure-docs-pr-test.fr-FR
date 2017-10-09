---
title: aaaViews dans les solutions de gestion Operations Management Suite (OMS) | Documents Microsoft
description: "Solutions de gestion Operations Management Suite (OMS) inclut généralement une ou plusieurs vues des données toovisualize.  Cet article décrit comment tooexport une vue créée par hello Concepteur de vue et l’inclure dans une solution de gestion. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="1600e-104">Vues dans des solutions de gestion dans Operations Management Suite (OMS) (préversion)</span><span class="sxs-lookup"><span data-stu-id="1600e-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="1600e-105">Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="1600e-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="1600e-106">N’importe quel schéma décrit ci-dessous est un objet toochange.</span><span class="sxs-lookup"><span data-stu-id="1600e-106">Any schema described below is subject toochange.</span></span>    
>
>

<span data-ttu-id="1600e-107">[Solutions de gestion Operations Management Suite (OMS)](operations-management-suite-solutions.md) inclut généralement une ou plusieurs vues des données toovisualize.</span><span class="sxs-lookup"><span data-stu-id="1600e-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views toovisualize data.</span></span>  <span data-ttu-id="1600e-108">Cet article décrit comment tooexport une vue créée par hello [Concepteur de vue](../log-analytics/log-analytics-view-designer.md) et l’inclure dans une solution de gestion.</span><span class="sxs-lookup"><span data-stu-id="1600e-108">This article describes how tooexport a view created by hello [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="1600e-109">Hello exemples dans cet article utilisent les paramètres et les variables qui sont deux solutions toomanagement requises ou courantes et décrites dans [création de solutions de gestion Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="1600e-109">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="1600e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1600e-110">Prerequisites</span></span>
<span data-ttu-id="1600e-111">Cet article suppose que vous êtes déjà familiarisé avec le trop[créer une solution de gestion](operations-management-suite-solutions-creating.md) et la structure de hello d’un fichier de solution.</span><span class="sxs-lookup"><span data-stu-id="1600e-111">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="1600e-112">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1600e-112">Overview</span></span>
<span data-ttu-id="1600e-113">tooinclude une vue dans une solution de gestion, vous créez un **ressource** pour lui dans hello [fichier solution](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="1600e-113">tooinclude a view in a management solution, you create a **resource** for it in hello [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="1600e-114">Hello JSON qui décrit la configuration détaillée de la vue hello est généralement complexe cependant et pas quelque chose qu’un auteur de la solution classique serait en mesure de toocreate manuellement.</span><span class="sxs-lookup"><span data-stu-id="1600e-114">hello JSON that describes hello view's detailed configuration is typically complex though and not something that a typical solution author would be able toocreate manually.</span></span>  <span data-ttu-id="1600e-115">méthode la plus courante Hello est vue de hello toocreate à l’aide de hello [Concepteur de vue](../log-analytics/log-analytics-view-designer.md), exporter, puis ajoutez sa solution toohello de configuration détaillées.</span><span class="sxs-lookup"><span data-stu-id="1600e-115">hello most common method is toocreate hello view using hello [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration toohello solution.</span></span>

<span data-ttu-id="1600e-116">Hello étapes de base tooadd une solution tooa de vue sont les suivantes.</span><span class="sxs-lookup"><span data-stu-id="1600e-116">hello basic steps tooadd a view tooa solution are as follows.</span></span>  <span data-ttu-id="1600e-117">Chaque étape est décrite en détail dans les sections hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1600e-117">Each step is described in further detail in hello sections below.</span></span>

1. <span data-ttu-id="1600e-118">Hello vue tooa fichier d’exportation.</span><span class="sxs-lookup"><span data-stu-id="1600e-118">Export hello view tooa file.</span></span>
2. <span data-ttu-id="1600e-119">Créez des ressources de vue hello de solution de hello.</span><span class="sxs-lookup"><span data-stu-id="1600e-119">Create hello view resource in hello solution.</span></span>
3. <span data-ttu-id="1600e-120">Ajouter les détails de l’affichage hello.</span><span class="sxs-lookup"><span data-stu-id="1600e-120">Add hello view details.</span></span>

## <a name="export-hello-view-tooa-file"></a><span data-ttu-id="1600e-121">Hello vue tooa fichier d’exportation</span><span class="sxs-lookup"><span data-stu-id="1600e-121">Export hello view tooa file</span></span>
<span data-ttu-id="1600e-122">Suivez les instructions de hello à [Concepteur de vue Analytique de journal](../log-analytics/log-analytics-view-designer.md) tooexport un tooa afficher le fichier.</span><span class="sxs-lookup"><span data-stu-id="1600e-122">Follow hello instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) tooexport a view tooa file.</span></span>  <span data-ttu-id="1600e-123">Hello fichier exporté sera être au format JSON avec hello même [éléments en tant que fichier de solution hello](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="1600e-123">hello exported file will be in JSON format with hello same [elements as hello solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="1600e-124">Hello **ressources** élément du fichier de vue hello possède une ressource avec un type de **Microsoft.OperationalInsights/workspaces** que représente hello espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="1600e-124">hello **resources** element of hello view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents hello OMS workspace.</span></span>  <span data-ttu-id="1600e-125">Cet élément a un sous-élément de type **vues** qui représente la vue de hello et contient sa configuration détaillée.</span><span class="sxs-lookup"><span data-stu-id="1600e-125">This element will have a subelement with a type of **views** that represents hello view and contains its detailed configuration.</span></span>  <span data-ttu-id="1600e-126">Copiez les détails hello de cet élément et puis le copier dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="1600e-126">You will copy hello details of this element and then copy it into your solution.</span></span>

## <a name="create-hello-view-resource-in-hello-solution"></a><span data-ttu-id="1600e-127">Créer une ressource de vue de hello dans la solution de hello</span><span class="sxs-lookup"><span data-stu-id="1600e-127">Create hello view resource in hello solution</span></span>
<span data-ttu-id="1600e-128">Ajouter hello suivant vue ressource toohello **ressources** élément de votre fichier de solution.</span><span class="sxs-lookup"><span data-stu-id="1600e-128">Add hello following view resource toohello **resources** element of your solution file.</span></span>  <span data-ttu-id="1600e-129">Cette procédure utilise des variables décrites ci-dessous que vous devez également ajouter.</span><span class="sxs-lookup"><span data-stu-id="1600e-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="1600e-130">Notez que hello **tableau de bord** et **OverviewTile** propriétés sont des espaces réservés qui vous remplacerez avec les propriétés correspondantes hello hello exportée afficher le fichier.</span><span class="sxs-lookup"><span data-stu-id="1600e-130">Note that hello **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with hello corresponding properties from hello exported view file.</span></span>

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

<span data-ttu-id="1600e-131">Ajouter hello suivant variables toohello variables élément hello du fichier de solution et remplacez toothose de valeurs hello pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="1600e-131">Add hello following variables toohello variables element of hello solution file and replace hello values toothose for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


<span data-ttu-id="1600e-132">Notez que vous pouvez copier des ressources de toute vue hello à partir de votre fichier de vue exportée, mais vous devez alors hello toomake modifications suivantes pour qu’il toowork dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="1600e-132">Note that you could copy hello entire view resource from your exported view file, but you would need toomake hello following changes for it toowork in your solution.</span></span>  

* <span data-ttu-id="1600e-133">Hello **type** de vue de hello ressource doit être toobe a été remplacée par **vues** trop**Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="1600e-133">hello **type** for hello view resource needs toobe changed from **views** too**Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="1600e-134">Hello **nom** propriété pour afficher la ressource hello doit nom d’espace de travail toobe modifié tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="1600e-134">hello **name** property for hello view resource needs toobe changed tooinclude hello workspace name.</span></span>
* <span data-ttu-id="1600e-135">dépendance Hello sur l’espace de travail hello doit toobe supprimée, car la ressource d’espace de travail hello n’est pas défini dans la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="1600e-135">hello dependency on hello workspace needs toobe removed since hello workspace resource isn't defined in hello solution.</span></span>
* <span data-ttu-id="1600e-136">**DisplayName** toobe des besoins de propriété ajouté toohello vue.</span><span class="sxs-lookup"><span data-stu-id="1600e-136">**DisplayName** property needs toobe added toohello view.</span></span>  <span data-ttu-id="1600e-137">Hello **Id**, **nom**, et **DisplayName** doivent toutes correspondre.</span><span class="sxs-lookup"><span data-stu-id="1600e-137">hello **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="1600e-138">Les noms de paramètres doivent être modifiés toomatch hello requis de jeu de paramètres.</span><span class="sxs-lookup"><span data-stu-id="1600e-138">Parameter names must be changed toomatch hello required set of parameters.</span></span>
* <span data-ttu-id="1600e-139">Variables doivent être définies dans la solution de hello et utilisés dans les propriétés appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="1600e-139">Variables should be defined in hello solution and used in hello appropriate properties.</span></span>

## <a name="add-hello-view-details"></a><span data-ttu-id="1600e-140">Ajouter des détails de l’affichage hello</span><span class="sxs-lookup"><span data-stu-id="1600e-140">Add hello view details</span></span>
<span data-ttu-id="1600e-141">afficher la ressource Hello Bonjour exporté affichage fichier contient deux éléments Bonjour **propriétés** élément nommé **tableau de bord** et **OverviewTile** qui contiennent hello configuration détaillée de la vue de hello.</span><span class="sxs-lookup"><span data-stu-id="1600e-141">hello view resource in hello exported view file will contain two elements in hello **properties** element named **Dashboard** and **OverviewTile** which contain hello detailed configuration of hello view.</span></span>  <span data-ttu-id="1600e-142">Copiez ces deux éléments et leur contenu hello **propriétés** élément de ressource de vue hello dans votre fichier de solution.</span><span class="sxs-lookup"><span data-stu-id="1600e-142">Copy these two elements and their contents into hello **properties** element of hello view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="1600e-143">Exemple</span><span class="sxs-lookup"><span data-stu-id="1600e-143">Example</span></span>
<span data-ttu-id="1600e-144">Par exemple, hello suivant l’exemple montre un fichier solution simple avec une vue.</span><span class="sxs-lookup"><span data-stu-id="1600e-144">For example, hello following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="1600e-145">Points de suspension (...) sont affichées pour hello **tableau de bord** et **OverviewTile** contenu pour des raisons d’espace.</span><span class="sxs-lookup"><span data-stu-id="1600e-145">Ellipses (...) are shown for hello **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a><span data-ttu-id="1600e-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1600e-146">Next steps</span></span>
* <span data-ttu-id="1600e-147">Découvrez plus de détails sur la création de [solutions de gestion](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="1600e-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="1600e-148">Inclure [des runbooks Automation dans votre solution de gestion](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="1600e-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
