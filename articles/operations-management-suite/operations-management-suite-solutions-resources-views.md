---
title: Vues dans des solutions de gestion dans Operations Management Suite (OMS) | Microsoft Docs
description: "Les solutions de gestion dans Operations Management Suite (OMS) comprennent généralement une ou plusieurs vues pour visualiser des données.  Cet article décrit comment exporter une vue créée par le Concepteur de vues et l’inclure dans une solution de gestion. "
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
ms.openlocfilehash: 533b5564a805e0b41f2b1a4ad92e12b133220952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="9cd2e-104">Vues dans des solutions de gestion dans Operations Management Suite (OMS) (préversion)</span><span class="sxs-lookup"><span data-stu-id="9cd2e-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="9cd2e-105">Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="9cd2e-106">Tout schéma décrit ci-dessous est susceptible d’être modifié.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-106">Any schema described below is subject to change.</span></span>    
>
>

<span data-ttu-id="9cd2e-107">[Les solutions de gestion dans Operations Management Suite (OMS)](operations-management-suite-solutions.md) comprennent généralement une ou plusieurs vues pour visualiser des données.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views to visualize data.</span></span>  <span data-ttu-id="9cd2e-108">Cet article décrit comment exporter une vue créée par le [Concepteur de vues](../log-analytics/log-analytics-view-designer.md) et l’inclure dans une solution de gestion.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="9cd2e-109">Les exemples dans cet article utilisent des paramètres et des variables qui sont nécessaires ou courants pour les solutions de gestion. Ils sont décrits dans la rubrique [Création de solutions de gestion dans Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="9cd2e-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="9cd2e-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="9cd2e-110">Prerequisites</span></span>
<span data-ttu-id="9cd2e-111">Cet article suppose que vous êtes déjà familiarisé avec la [création d’une solution de gestion](operations-management-suite-solutions-creating.md) et la structure d’un fichier solution.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-111">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="9cd2e-112">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="9cd2e-112">Overview</span></span>
<span data-ttu-id="9cd2e-113">Pour inclure une vue dans une solution de gestion, vous créez une **ressource** lui correspondant dans le [fichier solution](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="9cd2e-113">To include a view in a management solution, you create a **resource** for it in the [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="9cd2e-114">Cependant, le fichier JSON qui décrit la configuration détaillée de la vue est généralement complexe. Un auteur de solution classique ne serait pas en mesure de le créer manuellement.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span></span>  <span data-ttu-id="9cd2e-115">La méthode la plus courante consiste à créer la vue en utilisant le [Concepteur de vues](../log-analytics/log-analytics-view-designer.md), à l’exporter, puis à ajouter ensuite sa configuration détaillée à la solution.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span></span>

<span data-ttu-id="9cd2e-116">Voici les étapes de base pour ajouter une vue à une solution.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-116">The basic steps to add a view to a solution are as follows.</span></span>  <span data-ttu-id="9cd2e-117">Chaque étape est décrite en détail dans les sections ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-117">Each step is described in further detail in the sections below.</span></span>

1. <span data-ttu-id="9cd2e-118">Exportation de la vue dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-118">Export the view to a file.</span></span>
2. <span data-ttu-id="9cd2e-119">Création de la ressource de la vue dans la solution.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-119">Create the view resource in the solution.</span></span>
3. <span data-ttu-id="9cd2e-120">Ajout des détails de la vue.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-120">Add the view details.</span></span>

## <a name="export-the-view-to-a-file"></a><span data-ttu-id="9cd2e-121">Exportation de la vue dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-121">Export the view to a file</span></span>
<span data-ttu-id="9cd2e-122">Suivez les instructions du [Concepteur de vues de Log Analytics](../log-analytics/log-analytics-view-designer.md) pour exporter un affichage dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span></span>  <span data-ttu-id="9cd2e-123">Le fichier exporté sera au format JSON avec les mêmes [éléments que le fichier solution](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="9cd2e-123">The exported file will be in JSON format with the same [elements as the solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="9cd2e-124">L’élément **resources** du fichier de vue aura une ressource de type **Microsoft.OperationalInsights/workspaces** qui représente l’espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the OMS workspace.</span></span>  <span data-ttu-id="9cd2e-125">Cet élément aura un sous-élément de type **views** qui représente la vue et qui contient sa configuration détaillée.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span></span>  <span data-ttu-id="9cd2e-126">Vous copiez les détails de cet élément, puis vous les copiez dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-126">You will copy the details of this element and then copy it into your solution.</span></span>

## <a name="create-the-view-resource-in-the-solution"></a><span data-ttu-id="9cd2e-127">Création de la ressource de la vue dans la solution</span><span class="sxs-lookup"><span data-stu-id="9cd2e-127">Create the view resource in the solution</span></span>
<span data-ttu-id="9cd2e-128">Ajoutez la ressource de la vue suivante à l’élément **resources** de votre fichier solution.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-128">Add the following view resource to the **resources** element of your solution file.</span></span>  <span data-ttu-id="9cd2e-129">Cette procédure utilise des variables décrites ci-dessous que vous devez également ajouter.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="9cd2e-130">Notez que les propriétés **Dashboard** et **OverviewTile** sont des espaces réservés que vous remplacerez par les propriétés correspondantes du fichier de vue exporté.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span></span>

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

<span data-ttu-id="9cd2e-131">Ajoutez les variables suivantes à l’élément variables du fichier de la solution et remplacez les valeurs par celles de votre solution.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


<span data-ttu-id="9cd2e-132">Notez que vous pouvez copier la ressource de vue entière depuis votre fichier de vue exporté, mais que vous devez apporter les modifications suivantes pour qu’elle fonctionne dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span></span>  

* <span data-ttu-id="9cd2e-133">Le **type** pour la ressource de vue doit être modifié de **views** en **Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="9cd2e-134">La propriété **name** pour la ressource de la vue doit être modifiée pour inclure le nom de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-134">The **name** property for the view resource needs to be changed to include the workspace name.</span></span>
* <span data-ttu-id="9cd2e-135">La dépendance vis-à-vis de l’espace de travail doit être supprimée, car la ressource de l’espace de travail n’est pas définie dans la solution.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span></span>
* <span data-ttu-id="9cd2e-136">La propriété **DisplayName** doit être ajoutée à la vue.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-136">**DisplayName** property needs to be added to the view.</span></span>  <span data-ttu-id="9cd2e-137">Les éléments **Id**, **Name**, et **DisplayName** doivent tous correspondre.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-137">The **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="9cd2e-138">Les noms des paramètres doivent être modifiés de manière à correspondre à l’ensemble de paramètres nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-138">Parameter names must be changed to match the required set of parameters.</span></span>
* <span data-ttu-id="9cd2e-139">Les variables doivent être définies dans la solution et utilisées dans les propriétés appropriées.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-139">Variables should be defined in the solution and used in the appropriate properties.</span></span>

## <a name="add-the-view-details"></a><span data-ttu-id="9cd2e-140">Ajout des détails de la vue</span><span class="sxs-lookup"><span data-stu-id="9cd2e-140">Add the view details</span></span>
<span data-ttu-id="9cd2e-141">La ressource de la vue dans le fichier exporté contient deux éléments dans l’élément **properties** nommés **Dashboard** et **OverviewTile** qui contiennent la configuration détaillée de la vue.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-141">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span></span>  <span data-ttu-id="9cd2e-142">Copiez ces deux éléments et leur contenu dans l’élément **properties** de la ressource de vue dans votre fichier solution.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-142">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="9cd2e-143">Exemple</span><span class="sxs-lookup"><span data-stu-id="9cd2e-143">Example</span></span>
<span data-ttu-id="9cd2e-144">Par exemple, l’exemple suivant montre un fichier solution simple avec une vue.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-144">For example, the following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="9cd2e-145">Des points de suspension (...) sont affichés à la place du contenu des éléments **Dashboard** et **OverviewTile** pour des raisons d’espace.</span><span class="sxs-lookup"><span data-stu-id="9cd2e-145">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="9cd2e-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9cd2e-146">Next steps</span></span>
* <span data-ttu-id="9cd2e-147">Découvrez plus de détails sur la création de [solutions de gestion](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="9cd2e-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="9cd2e-148">Inclure [des runbooks Automation dans votre solution de gestion](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="9cd2e-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
