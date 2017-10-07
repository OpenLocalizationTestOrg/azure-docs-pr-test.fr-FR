---
title: "ressources d’automatisation aaaAzure dans les solutions OMS | Documents Microsoft"
description: "Solutions dans OMS inclut généralement des procédures opérationnelles dans Azure Automation tooautomate des processus tels que la collecte et de traitement des données d’analyse.  Cet article décrit comment les runbooks tooinclude et leurs ressources associées dans une solution."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a>Ajout de solution de gestion Azure Automation ressources tooan OMS (version préliminaire)
> [!NOTE]
> Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion. N’importe quel schéma décrit ci-dessous est un objet toochange.   


[Solutions de gestion OMS](operations-management-suite-solutions.md) inclut généralement des procédures opérationnelles dans Azure Automation tooautomate des processus tels que la collecte et de traitement des données d’analyse.  En outre toorunbooks, comptes Automation inclut des ressources telles que des variables et des planifications qui prennent en charge les runbooks hello utilisés dans les solutions hello.  Cet article décrit comment les runbooks tooinclude et leurs ressources associées dans une solution.

> [!NOTE]
> Hello exemples dans cet article utilisent les paramètres et les variables qui sont deux solutions toomanagement requises ou courantes et décrites dans [création de solutions de gestion Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md) 


## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous êtes déjà familiarisé avec hello informations suivantes.

- Comment trop[créer une solution de gestion](operations-management-suite-solutions-creating.md).
- Hello la structure d’un [fichier solution](operations-management-suite-solutions-solution-file.md).
- Comment trop[créent des modèles de gestionnaire de ressources](../azure-resource-manager/resource-group-authoring-templates.md)

## <a name="automation-account"></a>Compte Automation
Toutes les ressources dans Azure Automation sont contenues dans un [compte Automation](../automation/automation-security-overview.md#automation-account-overview).  Comme décrit dans [OMS espace de travail et le compte Automation](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello compte Automation n’est pas inclus dans la solution de gestion hello mais doit exister pour que la solution de hello est installée.  Si elle n’est pas disponible, hello solution installation échouera.

Hello nom de chaque ressource Automation hello du inclut son compte Automation.  Cette opération est effectuée dans la solution hello avec hello **accountName** paramètre comme hello, exemple d’une ressource de runbook suivant.

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a>Runbooks
Vous devez inclure tous les runbooks utilisés par la solution hello dans le fichier de solution hello afin qu’ils sont créés lors de la solution de hello est installée.  Vous ne peut pas contenir des corps de hello du runbook hello dans le modèle de hello, vous devez publier emplacement public hello runbook tooa où il est accessible par tout utilisateur de l’installation de votre solution.

[Azure Automation runbook](../automation/automation-runbook-types.md) ressources ont un type de **Microsoft.Automation/automationAccounts/runbooks** et avoir hello suivant la structure. Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello. 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


Décrit les propriétés de Hello pour les procédures opérationnelles Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| runbookType |Spécifie les types de hello de hello runbook. <br><br> Script : script PowerShell <br>PowerShell : workflow PowerShell <br> GraphPowerShell : runbook de script PowerShell graphique <br> GraphPowerShellWorkflow : runbook de workflow PowerShell graphique |
| logProgress |Spécifie si [enregistrements de progression](../automation/automation-runbook-output-and-messages.md) doit être généré pour les runbook hello. |
| logVerbose |Spécifie si [les enregistrements détaillés](../automation/automation-runbook-output-and-messages.md) doit être généré pour les runbook hello. |
| description |Description facultative pour le runbook de hello. |
| publishContentLink |Spécifie le contenu du runbook de hello hello. <br><br>URI - Uri toohello le contenu du runbook de hello.  Il s’agit d’un fichier .ps1 pour des runbooks PowerShell et Script et d’un fichier de runbook graphique exporté pour un runbook Graph.  <br> version - Version de runbook hello pour votre propre suivi. |


## <a name="automation-jobs"></a>Tâches Automation
Lorsque vous démarrez un Runbook dans Azure Automation, il crée un travail d’automatisation.  Vous pouvez ajouter une automatisation travail ressource tooyour solution tooautomatically début d’un runbook lors de la solution de gestion hello est installée.  Cette méthode est généralement utilisées toostart runbooks qui sont utilisés pour la configuration initiale de la solution de hello.  toostart un runbook à intervalles réguliers, créez un [planification](#schedules) et un [planification du travail](#job-schedules)

Ressources de travail ont un type de **Microsoft.Automation/automationAccounts/jobs** et avoir hello suivant la structure.  Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello. 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

Décrit les propriétés de Hello pour les tâches d’automatisation Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| runbook |Entité de nom unique portant le nom de hello de hello runbook toostart. |
| parameters |Entité pour chaque valeur de paramètre requis par les runbook hello. |

le travail de Hello inclut le nom du runbook hello et n’importe quel toobe de valeurs de paramètre envoyés toohello runbook.  travail de Hello doit [dépendent](operations-management-suite-solutions-solution-file.md#resources) runbook de hello il démarre depuis hello runbook doit être créé avant la tâche de hello.  Si vous avez plusieurs runbooks qui doivent être lancés, vous pouvez définir leur ordre en rendant un travail dépendant des autres travaux qui doivent être exécutés en premier.

nom de Hello d’une ressource de travail doit contenir un GUID qui est généralement affecté par un paramètre.  Vous trouverez plus d’informations sur les paramètres GUID dans la rubrique [Création de solutions dans Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).  


## <a name="certificates"></a>Certificats
[Certificats Automation Azure](../automation/automation-certificates.md) ont un type de **Microsoft.Automation/automationAccounts/certificates** et avoir hello suivant la structure. Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



Décrit les propriétés de Hello pour les ressources de certificats Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| base64Value |Valeur de la base 64 pour le certificat de hello. |
| thumbprint |Empreinte numérique du certificat de hello. |



## <a name="credentials"></a>Informations d'identification
[Les informations d’identification Automation Azure](../automation/automation-credentials.md) ont un type de **Microsoft.Automation/automationAccounts/credentials** et avoir hello suivant la structure.  Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello. 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

Décrit les propriétés de Hello pour les ressources d’informations d’identification Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| userName |Nom d’utilisateur pour les informations d’identification hello. |
| password |Mot de passe pour les informations d’identification hello. |


## <a name="schedules"></a>Planifications
[Planifications d’automatisation Azure](../automation/automation-schedules.md) ont un type de **Microsoft.Automation/automationAccounts/schedules** et avoir hello hello suivant la structure. Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

Décrit les propriétés de Hello pour planifier des ressources Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| description |Description facultative pour la planification de hello. |
| startTime |Spécifie l’heure de début de hello d’une planification en tant qu’objet DateTime. Une chaîne peut être fournie si elle peut être convertie tooa DateTime valide. |
| isEnabled |Spécifie si la planification de hello est activée. |
| interval |type de Hello d’intervalle de planification de hello.<br><br>day<br>hour |
| frequency |Fréquence à laquelle hello planification doit se déclencher dans le nombre de jours ou d’heures. |

Les planifications doivent avoir une heure de début avec une valeur supérieure à hello heure actuelle.  Vous ne peut pas fournir cette valeur avec une variable dans la mesure où vous n’auriez aucun moyen de savoir quand il est toobe continu installé.

Utilisez une des hello suivant deux stratégies lors de l’utilisation des ressources de planification dans une solution.

- Utiliser un paramètre pour l’heure de début hello de planification de hello.  Il vous est demandé hello utilisateur tooprovide une valeur lorsqu’ils installent la solution de hello.  Si vous avez plusieurs planifications, vous pouvez utiliser une valeur de paramètre unique pour plusieurs d'entre eux.
- Créer des planifications de hello à l’aide d’un runbook qui démarre lorsqu’hello solution est installée.  Cela supprime la spécification hello hello utilisateur toospecify est une heure, mais vous ne peut pas contenir planification hello dans votre solution afin qu’il sera supprimé lors de la solution de hello est supprimée.


### <a name="job-schedules"></a>Planifications de travaux
Les ressources de planification de tâche lient un runbook à une planification.  Ils ont un type de **Microsoft.Automation/automationAccounts/jobSchedules** et avoir hello hello suivant la structure.  Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


Décrit les propriétés de Hello pour les planifications de travaux Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| nom de la planification |Seul **nom** entité portant le nom hello de planification de hello. |
| nom du runbook  |Seul **nom** entité portant le nom hello de hello runbook.  |



## <a name="variables"></a>variables
[Les variables Automation Azure](../automation/automation-variables.md) ont un type de **Microsoft.Automation/automationAccounts/variables** et avoir hello suivant la structure.  Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

Décrit les propriétés de Hello pour les ressources variables Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| description | Description facultative de la variable de hello. |
| isEncrypted | Spécifie si la variable de hello doit être chiffrée. |
| type | Cette propriété n’a actuellement aucun effet.  type de données Hello de variable de hello sera déterminé par la valeur initiale de hello. |
| value | Valeur de variable de hello. |

> [!NOTE]
> Hello **type** propriété actuellement n’a aucun effet sur la variable hello en cours de création.  type de données Hello pour la variable de hello sera déterminée par la valeur de hello.  

Si vous définissez la valeur initiale de hello pour la variable de hello, il doit être configuré en tant que type de données correct hello.  Hello tableau suivant fournit hello différents types de données autorisées et leur syntaxe.  Notez que les valeurs au format JSON sont attendus tooalways être encadrée de guillemets avec des caractères spéciaux entre guillemets de hello.  Par exemple, une valeur de chaîne serait être spécifiée par des guillemets autour de chaîne hello (à l’aide du caractère d’échappement de hello (\\)) pendant une valeur numérique est être spécifiée avec un seul jeu de guillemets doubles.

| Type de données | Description | Exemple | Résout trop|
|:--|:--|:--|:--|
| string   | Placer la valeur entre des guillemets doubles.  | "\"Hello world\"" | "Hello world" |
| numérique  | Valeur numérique avec des guillemets simples.| "64" | 64 |
| booléenne  | **true** ou **false** entre guillemets.  Notez que cette valeur doit être en minuscules. | "true" | true |
| Datetime | Valeur de date sérialisée.<br>Vous pouvez utiliser hello applet de commande ConvertTo-Json dans PowerShell toogenerate cette valeur pour une date particulière.<br>Exemple : get-date "5/24/2017 13:14:57" \| ConvertTo-Json | "\\/Date(1495656897378)\\/" | 2017-05-24 13:14:57 |

## <a name="modules"></a>Modules
Votre solution de gestion n’a pas besoin toodefine [modules globales](../automation/automation-integration-modules.md) utilisé par les procédures opérationnelles, car ils seront toujours disponibles dans votre compte Automation.  Vous avez besoin de tooinclude une ressource pour d’autres modules utilisés par les procédures opérationnelles.

[Modules d’intégration](../automation/automation-integration-modules.md) ont un type de **Microsoft.Automation/automationAccounts/modules** et avoir hello suivant la structure.  Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


Décrit les propriétés de Hello pour les ressources de module Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| contentLink |Spécifie le contenu du module de hello hello. <br><br>URI - Uri toohello le contenu du module de hello.  Il s’agit d’un fichier .ps1 pour des runbooks PowerShell et Script et d’un fichier de runbook graphique exporté pour un runbook Graph.  <br> version - Version du module de hello pour votre propre suivi. |

Hello runbook doit s’appuyer sur hello module ressource tooensure qu’il a créées avant hello runbook.

### <a name="updating-modules"></a>Mise à jour des modules
Si vous mettez à jour une solution de gestion qui inclut un runbook qui utilise une planification et hello nouvelle version de votre solution a un nouveau module utilisé par ce runbook, hello runbook peut utiliser hello ancienne version du module de hello.  Vous devez inclure hello suivant les procédures opérationnelles dans votre solution et créer un travail toorun leur avant les autres runbooks.  Cela garantit que tous les modules sont mis à jour en tant que hello requis avant de charger des runbooks.

* [Mise à jour-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) garantit que tous les modules hello utilisées par les runbooks dans votre solution sont version la plus récente hello.  
* [ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) sera réinscrire tous hello Planification ressources tooensure que hello runbooks liés toothem avec des modules de dernière utilisation hello.




## <a name="sample"></a>Exemple
Voici un exemple d’une solution qui incluent ce qui inclut hello suivant des ressources :

- Runbook.  Il s’agit d’un exemple de runbook stocké dans un référentiel GitHub public.
- Travail d’Automation qui démarre hello runbook lors de la solution de hello est installée.
- Planification et travail de planification toostart hello runbook à intervalles réguliers.
- Certificat.
- Informations d'identification.
- Variable.
- Module.  Il s’agit de hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) pour l’écriture de données tooLog Analytique. 

exemples d’utilisation de Hello [paramètres de solution standard](operations-management-suite-solutions-solution-file.md#parameters) variables sont communément utilisées dans une solution en opposition toohardcoding des valeurs dans les définitions de ressource hello.


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a>Étapes suivantes
* [Ajouter une solution de tooyour vue](operations-management-suite-solutions-resources-views.md) toovisualize les données collectées.
