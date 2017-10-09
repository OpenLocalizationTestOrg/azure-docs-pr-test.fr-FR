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
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Vues dans des solutions de gestion dans Operations Management Suite (OMS) (préversion)
> [!NOTE]
> Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion. N’importe quel schéma décrit ci-dessous est un objet toochange.    
>
>

[Solutions de gestion Operations Management Suite (OMS)](operations-management-suite-solutions.md) inclut généralement une ou plusieurs vues des données toovisualize.  Cet article décrit comment tooexport une vue créée par hello [Concepteur de vue](../log-analytics/log-analytics-view-designer.md) et l’inclure dans une solution de gestion.  

> [!NOTE]
> Hello exemples dans cet article utilisent les paramètres et les variables qui sont deux solutions toomanagement requises ou courantes et décrites dans [création de solutions de gestion Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)
>
>

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous êtes déjà familiarisé avec le trop[créer une solution de gestion](operations-management-suite-solutions-creating.md) et la structure de hello d’un fichier de solution.

## <a name="overview"></a>Vue d'ensemble
tooinclude une vue dans une solution de gestion, vous créez un **ressource** pour lui dans hello [fichier solution](operations-management-suite-solutions-creating.md).  Hello JSON qui décrit la configuration détaillée de la vue hello est généralement complexe cependant et pas quelque chose qu’un auteur de la solution classique serait en mesure de toocreate manuellement.  méthode la plus courante Hello est vue de hello toocreate à l’aide de hello [Concepteur de vue](../log-analytics/log-analytics-view-designer.md), exporter, puis ajoutez sa solution toohello de configuration détaillées.

Hello étapes de base tooadd une solution tooa de vue sont les suivantes.  Chaque étape est décrite en détail dans les sections hello ci-dessous.

1. Hello vue tooa fichier d’exportation.
2. Créez des ressources de vue hello de solution de hello.
3. Ajouter les détails de l’affichage hello.

## <a name="export-hello-view-tooa-file"></a>Hello vue tooa fichier d’exportation
Suivez les instructions de hello à [Concepteur de vue Analytique de journal](../log-analytics/log-analytics-view-designer.md) tooexport un tooa afficher le fichier.  Hello fichier exporté sera être au format JSON avec hello même [éléments en tant que fichier de solution hello](operations-management-suite-solutions-solution-file.md).  

Hello **ressources** élément du fichier de vue hello possède une ressource avec un type de **Microsoft.OperationalInsights/workspaces** que représente hello espace de travail OMS.  Cet élément a un sous-élément de type **vues** qui représente la vue de hello et contient sa configuration détaillée.  Copiez les détails hello de cet élément et puis le copier dans votre solution.

## <a name="create-hello-view-resource-in-hello-solution"></a>Créer une ressource de vue de hello dans la solution de hello
Ajouter hello suivant vue ressource toohello **ressources** élément de votre fichier de solution.  Cette procédure utilise des variables décrites ci-dessous que vous devez également ajouter.  Notez que hello **tableau de bord** et **OverviewTile** propriétés sont des espaces réservés qui vous remplacerez avec les propriétés correspondantes hello hello exportée afficher le fichier.

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

Ajouter hello suivant variables toohello variables élément hello du fichier de solution et remplacez toothose de valeurs hello pour votre solution.

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


Notez que vous pouvez copier des ressources de toute vue hello à partir de votre fichier de vue exportée, mais vous devez alors hello toomake modifications suivantes pour qu’il toowork dans votre solution.  

* Hello **type** de vue de hello ressource doit être toobe a été remplacée par **vues** trop**Microsoft.OperationalInsights/workspaces**.
* Hello **nom** propriété pour afficher la ressource hello doit nom d’espace de travail toobe modifié tooinclude hello.
* dépendance Hello sur l’espace de travail hello doit toobe supprimée, car la ressource d’espace de travail hello n’est pas défini dans la solution de hello.
* **DisplayName** toobe des besoins de propriété ajouté toohello vue.  Hello **Id**, **nom**, et **DisplayName** doivent toutes correspondre.
* Les noms de paramètres doivent être modifiés toomatch hello requis de jeu de paramètres.
* Variables doivent être définies dans la solution de hello et utilisés dans les propriétés appropriées hello.

## <a name="add-hello-view-details"></a>Ajouter des détails de l’affichage hello
afficher la ressource Hello Bonjour exporté affichage fichier contient deux éléments Bonjour **propriétés** élément nommé **tableau de bord** et **OverviewTile** qui contiennent hello configuration détaillée de la vue de hello.  Copiez ces deux éléments et leur contenu hello **propriétés** élément de ressource de vue hello dans votre fichier de solution.

## <a name="example"></a>Exemple
Par exemple, hello suivant l’exemple montre un fichier solution simple avec une vue.  Points de suspension (...) sont affichées pour hello **tableau de bord** et **OverviewTile** contenu pour des raisons d’espace.

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




## <a name="next-steps"></a>Étapes suivantes
* Découvrez plus de détails sur la création de [solutions de gestion](operations-management-suite-solutions-creating.md).
* Inclure [des runbooks Automation dans votre solution de gestion](operations-management-suite-solutions-resources-automation.md).
