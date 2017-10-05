---
title: "Démarrage et arrêt de machines virtuelles - Graphique | Microsoft Docs"
description: "La version du workflow PowerShell du scénario Azure Automation inclut des Runbooks pour démarrer et arrêter des machines virtuelles classiques."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 62d93170-ca3d-42ef-ac1d-6d50b61ac87d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 338d5712239356e13cbf480d9655ca3ca499701d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Scénario Azure Automation : démarrage et arrêt de machines virtuelles
Ce scénario Azure Automation inclut des runbooks pour démarrer et arrêter des machines virtuelles classiques.  Vous pouvez utiliser ce scénario dans les cas suivants :  

* Utiliser les runbooks sans modification dans votre propre environnement.
* Modifier les runbooks pour exécuter une fonctionnalité personnalisée.  
* Appeler les runbooks à partir d’un autre runbook dans le cadre d’une solution globale.
* Utiliser les runbooks comme didacticiels pour apprendre les concepts de création de runbook.

> [!div class="op_single_selector"]
> * [Graphique](automation-solution-startstopvm-graphical.md)
> * [Workflow PowerShell](automation-solution-startstopvm-psworkflow.md)
>
>

Il s'agit de la version graphique du Runbook de ce scénario. Elle est également disponible en utilisant des [Runbooks de workflow PowerShell](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-the-scenario"></a>Obtention du scénario
Ce scénario se compose de deux Runbooks graphiques que vous pouvez télécharger à partir des liens suivants.  Consultez la [version du workflow PowerShell](automation-solution-startstopvm-psworkflow.md) de ce scénario pour obtenir des liens vers les Runbooks du workflow PowerShell.

| Runbook | Lien | Type | Description |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Démarrer le Runbook graphique d’une machine virtuelle Azure classique](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Graphique |Démarre toutes les machines virtuelles classiques d’un abonnement Azure ou toutes les machines virtuelles portant un nom de service particulier. |
| StopAzureClassicVM |[Arrêter le Runbook graphique d’une machine virtuelle Azure classique](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Graphique |Arrête toutes les machines virtuelles d’un compte Automation ou toutes les machines virtuelles portant un nom de service particulier. |

## <a name="installing-and-configuring-the-scenario"></a>Installation et configuration du scénario
### <a name="1-install-the-runbooks"></a>1. Installation des runbooks
Après avoir téléchargé les Runbooks, vous pouvez les importer à l'aide de la procédure décrite dans les [Procédures pour Runbooks graphiques](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-the-description-and-requirements"></a>2. Examen de la description et des conditions requises
Les Runbooks incluent une activité appelée **Lisez-moi** qui comprend une description et les ressources requises.  Vous pouvez afficher ces informations en sélectionnant l’activité **Lisez-moi**, puis le paramètre **Script Workflow**.  Vous pouvez également obtenir les mêmes informations à partir de cet article.

### <a name="3-configure-assets"></a>3. Configuration des ressources
Les Runbooks requièrent les ressources suivantes que vous devez créer et remplir avec les valeurs appropriées.  Les noms sont définis par défaut.  Vous pouvez utiliser des ressources avec des noms différents si vous spécifiez ces noms dans les [paramètres d'entrée](#using-the-runbooks) au démarrage du Runbook.

| Type de ressource | Nom par défaut | Description |
|:--- |:--- |:--- |:--- |
| [Informations d'identification](automation-credentials.md) |AzureCredential |Contient des informations d'identification d'un compte ayant les autorisations pour démarrer et arrêter des machines virtuelles dans l'abonnement Azure. |
| [Variable](automation-variables.md) |AzureSubscriptionId |Contient l’ID d’abonnement de votre abonnement Azure. |

## <a name="using-the-scenario"></a>Utilisation du scénario
### <a name="parameters"></a>Paramètres
Les Runbooks ont tous les [paramètres d’entrée](automation-starting-a-runbook.md#runbook-parameters)suivants.  Vous devez fournir des valeurs pour tous les paramètres obligatoires et pouvez éventuellement fournir des valeurs pour les autres paramètres, selon vos besoins.

| Paramètre | Type | Obligatoire | Description |
|:--- |:--- |:--- |:--- |
| ServiceName |string |Non |Si une valeur est fournie, toutes les machines virtuelles portant ce nom de service sont démarrées ou arrêtées.  Si aucune valeur n’est fournie, toutes les machines virtuelles classiques dans l’abonnement Azure sont démarrées ou arrêtées. |
| AzureSubscriptionIdAssetName |string |Non |Contient le nom de la [ressource variable](#installing-and-configuring-the-scenario) qui contient l’ID de votre abonnement Azure.  Si vous ne spécifiez aucune valeur, la valeur *AzureSubscriptionId* est utilisée. |
| AzureCredentialAssetName |string |Non |Contient le nom de la [ressource d’informations d’identification](#installing-and-configuring-the-scenario) qui contient les informations d’identification pour le runbook à utiliser.  Si vous ne spécifiez aucune valeur, la valeur *AzureCredential* est utilisée. |

### <a name="starting-the-runbooks"></a>Démarrage des runbooks
Vous pouvez utiliser n’importe quelle méthode proposée dans [Démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md) pour démarrer le runbook de votre choix dans cet article.

Les exemples de commandes suivant utilisent Windows PowerShell pour exécuter **StartAzureClassicVM** afin de démarrer toutes les machines virtuelles portant le nom de service *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Sortie
Les Runbooks [généreront un message](automation-runbook-output-and-messages.md) pour chaque machine virtuelle, indiquant si l'instruction de démarrage ou d'arrêt a été correctement envoyée.  Vous pouvez rechercher une chaîne spécifique dans la sortie afin de déterminer le résultat pour chaque runbook.  Les chaînes de sortie possibles sont répertoriées dans le tableau suivant.

| Runbook | Condition | Message |
|:--- |:--- |:--- |
| StartAzureClassicVM |Machine virtuelle déjà en cours d'exécution |MyVM déjà en cours d’exécution |
| StartAzureClassicVM |Demande de démarrage de la machine virtuelle envoyée avec succès |MyVM démarrée |
| StartAzureClassicVM |Échec de la demande de démarrage de la machine virtuelle |MyVM n'a pas pu démarrer |
| StopAzureClassicVM |Machine virtuelle déjà en cours d'exécution |MyVM déjà arrêtée |
| StopAzureClassicVM |Demande de démarrage de la machine virtuelle envoyée avec succès |MyVM démarrée |
| StopAzureClassicVM |Échec de la demande de démarrage de la machine virtuelle |MyVM n'a pas pu démarrer |

Voici une image de l'utilisation de **StartAzureClassicVM** comme [Runbook enfant](automation-child-runbooks.md) dans l'exemple d’un Runbook graphique.  Cet exemple utilise les liens conditionnels du tableau suivant.

| Lien | Critères |
|:--- |:--- |
| Lien de réussite |$ActivityOutput['StartAzureClassicVM'] -like "\* a été démarrée" |
| Lien d’erreur |$ActivityOutput['StartAzureClassicVM'] -notlike "\* a été démarrée" |

![Exemple de Runbook enfant](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Analyse détaillée
Voici une analyse détaillée des runbooks de ce scénario.  Vous pouvez utiliser ces informations pour personnaliser les Runbooks ou simplement pour obtenir des informations à partir de ceux-ci afin de créer vos propres scénarios d’automatisation.

### <a name="authentication"></a>Authentification
![Authentification](media/automation-solution-startstopvm/graphical-authentication.png)

Le Runbook démarre avec des activités pour définir les [informations d’identification](automation-credentials.md) et un abonnement Azure qui sera utilisé pour le reste du Runbook.

Les deux premières activités, **Get Subscription Id** et **Get Azure Credential**, récupèrent les [ressources](#installing-the-runbook) utilisées par les deux activités.  Ces activités pourraient spécifier directement les ressources, mais elles ont besoin de leurs noms.  Dans la mesure où nous autorisons l'utilisateur à spécifier ces noms dans les [paramètres d'entrée](#using-the-runbooks), ces activités doivent récupérer les ressources avec un nom spécifié par le paramètre d'entrée.

**Add-AzureAccount** définit les informations d'identification qui seront utilisées pour le reste du Runbook.  La ressource d'informations d'identification qu'il récupère à partir de l’activité **Get Azure Credential** doit pouvoir démarrer et arrêter des machines virtuelles dans l'abonnement Azure.  L’abonnement utilisé est sélectionné par **Select-AzureSubscription**, qui utilise l’ID d’abonnement obtenu à partir de **Get Subscription Id**.

### <a name="get-virtual-machines"></a>Obtenir des machines virtuelles
![Get VMs](media/automation-solution-startstopvm/graphical-getvms.png)

Le Runbook doit déterminer sur quelles machines virtuelles il sera exécuté et si ces machines sont déjà démarrées ou arrêtées (en fonction du Runbook).   Une des deux activités récupérera les machines virtuelles.  **Get VMs in Service** s'exécutera si le paramètre d’entrée *ServiceName* du Runbook contient une valeur.  **Get All VMs** s'exécutera si le paramètre d’entrée *ServiceName* du Runbook ne contient aucune valeur.  Cette logique est appliquée par les liens conditionnels précédant chaque activité.

Les deux activités utilisent l’applet de commande **Get-AzureVM** .  **Get All VMs** utilise le jeu de paramètres **ListAllVMs** pour retourner toutes les machines virtuelles.  **Get VMs in Service** utilise le jeu de paramètres **GetVMByServiceAndVMName** et fournit le paramètre d’entrée **ServiceName** pour le paramètre **ServiceName**.  

### <a name="merge-vms"></a>Fusion de machines virtuelles
![Fusion de machines virtuelles](media/automation-solution-startstopvm/graphical-mergevms.png)

L’activité **Merge VMs** est requise pour fournir une entrée à **Start-AzureVM**, qui a besoin du nom et du nom de service des machines virtuelles pour démarrer.  Cette entrée peut provenir de l’activité **Get All VMs** ou **Get VMs in Service**, mais **Start-AzureVM** ne peut spécifier qu’une activité pour son entrée.   

Le scénario consiste à créer une activité **Merge VMs** qui exécute l’applet de commande **Write-Output**.  Le paramètre **InputObject** pour cette applet de commande est une expression PowerShell qui combine l'entrée des deux activités précédentes.  Comme une seule de ces activités s'exécutera, un seul jeu de sortie est attendu.  **Start-AzureVM** peut utiliser ce résultat pour ses paramètres d'entrée.

### <a name="startstop-virtual-machines"></a>Démarrage/arrêt de machines virtuelles
![Start VMs](media/automation-solution-startstopvm/graphical-startvm.png) ![Stop VMs](media/automation-solution-startstopvm/graphical-stopvm.png)

En fonction du Runbook, les activités suivantes tenteront de démarrer ou d’arrêter le Runbook à l’aide de **Start-AzureVM** ou **Stop-AzureVM**.  Comme l'activité est précédée d'un lien de pipeline, elle s'exécute une fois pour chaque objet retourné par **Merge VMs**.  Le lien est conditionnel pour que l’activité s’exécute uniquement si le paramètre *RunningState* de la machine virtuelle indique *Stopped* pour **Start-AzureVM** et *Started* pour **Stop-AzureVM**. Si cette condition n’est pas remplie, **Notify Already Started** ou **Notify Already Stopped** est exécuté pour envoyer un message à l’aide de **Write-Output**.

### <a name="send-output"></a>Envoi de la sortie
![Notify Start VMs](media/automation-solution-startstopvm/graphical-notifystart.png) ![Notify Stop VMs](media/automation-solution-startstopvm/graphical-notifystop.png)

La dernière étape du Runbook consiste à envoyer la sortie si la demande de démarrage ou d'arrêt pour chaque machine virtuelle a été correctement envoyée. Il existe une activité **Write-Output** distincte pour chaque machine, et nous déterminons celle qui doit s'exécuter à l’aide de liens conditionnels.  **Notify VM Started** ou **Notify VM Stopped** est exécuté si *OperationStatus* indique *Succeeded*.  Si *OperationStatus* affiche une autre valeur, **Notify Failed To Start** ou **Notify Failed to Stop** est exécuté.

## <a name="next-steps"></a>Étapes suivantes
* [Création de graphiques dans Azure Automation](automation-graphical-authoring-intro.md)
* [Runbooks enfants dans Azure Automation](automation-child-runbooks.md)
* [Sortie et messages de Runbook dans Azure Automation](automation-runbook-output-and-messages.md)
