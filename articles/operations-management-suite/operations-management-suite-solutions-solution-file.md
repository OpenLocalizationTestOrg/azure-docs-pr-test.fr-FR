---
title: solutions de gestion aaaCreating Operations Management Suite (OMS) | Documents Microsoft
description: "Solutions de gestion d’étendent les fonctionnalités de hello Operations Management Suite (OMS) en fournissant des scénarios de gestion empaquetée que les clients peuvent ajouter tootheir espace de travail OMS.  Cet article fournit des détails sur la façon dont vous pouvez créer toobe des solutions de gestion utilisé dans votre propre environnement ou apportées disponible tooyour clients."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a>Création d’un fichier de solutions de gestion dans Operations Management Suite (OMS) (préversion)
> [!NOTE]
> Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion. N’importe quel schéma décrit ci-dessous est un objet toochange.  

Les solutions de gestion dans Operations Management Suite (OMS) sont implémentées en tant que [modèles Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).  tâche principale Hello d’apprentissage de la façon dont les solutions de gestion tooauthor consiste à apprendre comment trop[créer un modèle](../azure-resource-manager/resource-group-authoring-templates.md).  Cet article fournit des détails uniques des modèles utilisés pour les solutions et la manière dont les ressources de solution classique tooconfigure.


## <a name="tools"></a>Outils

Vous pouvez utiliser n’importe quel toowork de l’éditeur de texte avec les fichiers de solution, mais nous vous recommandons en exploitant les fonctionnalités de hello fournies dans Visual Studio ou Visual Studio Code comme décrit dans hello suivant des articles.

- [Création et déploiement de groupes de ressources Azure à l’aide de Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [Utiliser des modèles Azure Resource Manager dans Visual Studio Code](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a>Structure
structure de base Hello d’un fichier de solution de gestion est hello identique à un [modèle Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#template-format) qui est la suivante.  Chacune des sections hello ci-dessous décrit les éléments de niveau supérieur hello et et leur contenu dans une solution.  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a>Paramètres
[Paramètres](../azure-resource-manager/resource-group-authoring-templates.md#parameters) sont des valeurs dont vous avez besoin à partir de l’utilisateur de hello lorsqu’ils installent la solution de gestion hello.  Il existe des paramètres standard compris dans toutes les solutions, et vous pouvez ajouter des paramètres supplémentaires en fonction des besoins spécifiques de votre solution.  Comment les utilisateurs fournit les valeurs de paramètre lors de l’installation de votre solution dépend de paramètre particulier hello et comment hello solution est installée.

Lorsqu’un utilisateur installe votre solution de gestion via hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) ou [modèles de démarrage rapide d’Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions) qu’ils sont invités à tooselect un [OMS espace de travail et le compte Automation ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).  Ceux-ci sont des valeurs de hello toopopulate utilisés de chacun des paramètres standard de hello.  utilisateur de Hello n’est pas invité toodirectly fournir des valeurs pour les paramètres standard hello, mais elles sont demandées par invite tooprovide des valeurs pour tous les paramètres supplémentaires.

Lorsque les utilisateur hello installe votre solution [une autre méthode](operations-management-suite-solutions.md#finding-and-installing-management-solutions), ils doivent fournir une valeur pour tous les paramètres standards et tous les paramètres supplémentaires.

Vous trouverez ci-dessous un exemple de paramètre.  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

Hello tableau suivant décrit les attributs de hello d’un paramètre.

| Attribut | Description |
|:--- |:--- |
| type |Type de données pour le paramètre hello. contrôle d’entrée de Hello affiché à l’utilisateur de hello dépend du type de données hello.<br><br>Valeur booléenne : zone de liste déroulante<br>Chaîne : zone de texte<br>Entier : zone de texte<br>securestring : champ de mot de passe<br> |
| category |Catégorie facultative pour le paramètre hello.  Paramètres Bonjour même catégorie sont regroupés ensemble. |
| contrôle |Fonctionnalité supplémentaire pour les paramètres de type chaîne.<br><br>datetime : le contrôle Datetime est affiché.<br>GUID - valeur Guid est généré automatiquement et paramètre hello n’est pas affiché. |
| description |Description facultative pour le paramètre hello.  Affiché dans un paramètre de toohello suivant informations info-bulle. |

### <a name="standard-parameters"></a>Paramètres standard
Hello tableau suivant répertorie les paramètres standard hello pour toutes les solutions de gestion.  Ces valeurs sont remplies pour utilisateur hello au lieu de demander les lorsque votre solution est installée à partir de modèles Azure Marketplace ou de démarrage rapide de hello.  utilisateur de Hello doit fournir des valeurs pour les si les solutions hello sont installée avec une autre méthode.

> [!NOTE]
> interface utilisateur de Hello dans les modèles Azure Marketplace et Quickstart hello s’attend à des noms de paramètre hello dans la table de hello.  Si vous utilisez des noms de paramètres différents puis hello utilisateur sera invité pour eux, et qu’ils ne sont pas automatiquement peuplées.
>
>

| Paramètre | Type | Description |
|:--- |:--- |:--- |
| accountName |string |Nom de compte Azure Automation. |
| pricingTier |string |Niveau tarifaire de l’espace de travail Log Analytics et du compte Azure Automation. |
| regionId |string |Région de hello compte Azure Automation. |
| solutionName |string |Nom de solution de hello.  Si vous déployez votre solution via des modèles de démarrage rapide, vous devez définir solutionName en tant que paramètre permettant de définir à la place nécessitant hello utilisateur toospecify, une chaîne. |
| workspaceName |string |Nom de l’espace de travail Log Analytics. |
| workspaceRegionId |string |Région de l’espace de travail hello Analytique de journal. |


Voici la structure hello des paramètres standard de hello que vous pouvez copier et coller dans votre fichier solution.  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


Vous faites référence tooparameter des valeurs dans d’autres éléments de solution hello avec la syntaxe hello **paramètres ('parameter name')**.  Par exemple, tooaccess hello nom de l’espace de travail, vous utiliseriez **parameters('workspaceName')**

## <a name="variables"></a>variables
[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) sont des valeurs que vous utiliserez dans reste hello de solution de gestion hello.  Ces valeurs ne sont pas utilisateur toohello exposé installation hello solution.  Ils sont auteur de hello tooprovide prévue avec un emplacement unique où ils peuvent gérer les valeurs qui peuvent être utilisés plusieurs fois dans l’ensemble des solutions de hello. Vous devez placer n’importe quelle solution tooyour spécifique de valeurs dans des variables comme toohard opposé les coder Bonjour **ressources** élément.  Cela améliore la lisibilité du code de hello et vous permet de tooeasily modifier ces valeurs dans les versions ultérieures.

Voici un exemple d’élément **variables** avec des paramètres standard utilisés dans les solutions.

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Vous faites référence à des valeurs de toovariable solution hello avec la syntaxe hello **variables (« nom de la variable')**.  Par exemple, tooaccess hello SolutionName variable, vous utiliseriez **variables('SolutionName')**.

Vous pouvez également définir des variables complexes pour plusieurs ensembles de valeurs.  Elles sont particulièrement utiles dans les solutions de gestion où vous définissez plusieurs propriétés pour différents types de ressources.  Par exemple, vous pourriez restructurer les variables de solution hello ci-dessus toohello suivant.

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Dans ce cas, vous faites référence à des valeurs de toovariable solution hello avec la syntaxe hello **variables('variable name').property**.  Par exemple, tooaccess hello variable du nom de la Solution, vous utiliseriez **variables('Solution'). Nom**.

## <a name="resources"></a>Ressources
[Ressources](../azure-resource-manager/resource-group-authoring-templates.md#resources) définir hello différentes ressources qui installent et configurent votre solution de gestion.  Il s’agit de hello plus grand et plus complexe partie du modèle de hello.  Vous pouvez obtenir la structure de hello et une description complète des éléments de ressource dans [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).  Différentes ressources que vous définirez généralement sont détaillées dans d’autres articles de cette documentation. 


### <a name="dependencies"></a>Dépendances
Hello **dependsOn** éléments spécifie un [dépendance](../azure-resource-manager/resource-group-define-dependencies.md) sur une autre ressource.  Lors de la solution de hello est installée, une ressource n’est pas créée jusqu'à ce que toutes ses dépendances ont été créés.  Par exemple, votre solution peut [démarrer un runbook](operations-management-suite-solutions-resources-automation.md#runbooks) lorsqu’il est installé à l’aide d’une [ressource de tâche](operations-management-suite-solutions-resources-automation.md#automation-jobs).  ressources de travail Hello dépendront hello runbook ressources toomake que ce runbook hello est créé avant que le travail de hello est créé.

### <a name="oms-workspace-and-automation-account"></a>Espace de travail OMS et compte Automation
Exigent des solutions de gestion un [espace de travail OMS](../log-analytics/log-analytics-manage-access.md) toocontain vues et une [compte Automation](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks et les ressources associées.  Ceux-ci doivent être disponibles avant hello ressources dans hello solution sont créés et ne doivent pas être définies dans la solution hello elle-même.  Hello utilisateur [spécifier un compte et un espace de travail](operations-management-suite-solutions.md#oms-workspace-and-automation-account) quand ils déploient votre solution, mais en tant qu’auteur de hello, vous devez envisager hello les points suivants.

## <a name="solution-resource"></a>Ressource de la solution
Chaque solution nécessite une entrée de ressource Bonjour **ressources** élément qui définit la solution hello elle-même.  Cela aura un type de **Microsoft.OperationsManagement/solutions** et avoir hello suivant la structure. Cela inclut les [paramètres standard](#parameters) et [variables](#variables) qui sont des propriétés de toodefine généralement utilisées de la solution de hello.


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a>Dépendances
ressource de solution Hello doit avoir un [dépendance](../azure-resource-manager/resource-group-define-dependencies.md) sur toutes les autres ressources dans la solution hello puisqu’ils doivent tooexist avant la création de solutions de hello.  Pour cela en ajoutant une entrée pour chaque ressource hello **dependsOn** élément.

### <a name="properties"></a>Propriétés
ressources de solution Hello possède des propriétés de hello Bonjour tableau suivant.  Cela inclut des ressources de hello référencé et contenus par solution hello qui définit la gestion de ressources de hello après l’installation de la solution de hello.  Chaque ressource dans une solution de hello doit être répertorié dans soit hello **referencedResources** ou hello **containedResources** propriété.

| Propriété | Description |
|:--- |:--- |
| workspaceResourceId |ID de l’espace de travail hello Analytique de journal sous forme de hello  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<nom de l’espace de travail\>*. |
| referencedResources |Liste des ressources dans la solution hello qui ne doit pas être supprimé lors de la solution de hello est supprimée. |
| containedResources |Liste des ressources dans la solution hello qui doivent être supprimés lorsque la solution de hello est supprimée. |

exemple Hello ci-dessus est une solution avec un runbook, une planification et la vue.  planification de Hello et runbook sont *référencé* Bonjour **propriétés** élément afin qu’ils ne sont pas supprimées lors de la solution de hello est supprimée.  vue de Hello est *contenus* par conséquent, il est supprimé lors de la solution de hello est supprimée.

### <a name="plan"></a>Planification
Hello **plan** entité de ressource de solution hello a les propriétés de hello hello tableau suivant.

| Propriété | Description |
|:--- |:--- |
| name |Nom de solution de hello. |
| version |Version de solution hello comme déterminé par l’auteur de hello. |
| product |Solution de hello tooidentify chaîne unique. |
| publisher |Éditeur de solution de hello. |



## <a name="sample"></a>Exemple
Vous pouvez consulter des exemples de fichiers de solution avec une ressource de la solution à hello emplacements suivants.

- [Ressources Automation](operations-management-suite-solutions-resources-automation.md#sample)
- [Ressources de recherche et d’alerte](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a>Étapes suivantes
* [Ajouter des alertes et les recherches enregistrées](operations-management-suite-solutions-resources-searches-alerts.md) solution de gestion tooyour.
* [Ajouter des vues](operations-management-suite-solutions-resources-views.md) solution de gestion tooyour.
* [Ajouter des procédures opérationnelles et autres ressources Automation](operations-management-suite-solutions-resources-automation.md) solution de gestion tooyour.
* En savoir plus de détails hello de [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Dans [Modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates), recherchez des exemples de modèles Resource Manager.
