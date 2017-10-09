---
title: "aaaStarting et les machines virtuelles de l’arrêt - graphique | Documents Microsoft"
description: "Version de flux de travail PowerShell du scénario Azure Automation, y compris des procédures opérationnelles toostart et arrêter les machines virtuelles classiques."
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
redirect_document_id: False
ms.openlocfilehash: 5add8d8cf35ea2e89a570744755ac7db0a6feb07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Scénario Azure Automation : démarrage et arrêt de machines virtuelles
Ce scénario Azure Automation inclut des procédures opérationnelles toostart et arrêter les machines virtuelles classiques.  Vous pouvez utiliser ce scénario pour hello suivants :  

* Utiliser des runbooks de hello sans modification dans votre propre environnement.
* Modifier les fonctionnalités de tooperform personnalisé de procédures opérationnelles de hello.  
* Appeler des procédures opérationnelles de hello à partir d’un autre runbook dans le cadre d’une solution globale.
* Permet d’utiliser des runbooks de hello en tant que runbook toolearn de didacticiels concepts de création.

> [!div class="op_single_selector"]
> * [Graphique](automation-solution-startstopvm-graphical.md)
> * [Workflow PowerShell](automation-solution-startstopvm-psworkflow.md)
>
>

Il s’agit de version de runbook graphique hello de ce scénario. Elle est également disponible en utilisant des [Runbooks de workflow PowerShell](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-hello-scenario"></a>Scénario de hello mise en route
Ce scénario se compose de deux deux runbooks graphiques que vous pouvez télécharger à partir de hello les liens suivants.  Consultez hello [version de flux de travail PowerShell](automation-solution-startstopvm-psworkflow.md) de ce scénario pour les liens toohello les runbooks PowerShell Workflow.

| Runbook | Lien | Type | Description |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Démarrer le Runbook graphique d’une machine virtuelle Azure classique](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Graphique |Démarre toutes les machines virtuelles classiques d’un abonnement Azure ou toutes les machines virtuelles portant un nom de service particulier. |
| StopAzureClassicVM |[Arrêter le Runbook graphique d’une machine virtuelle Azure classique](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Graphique |Arrête toutes les machines virtuelles d’un compte Automation ou toutes les machines virtuelles portant un nom de service particulier. |

## <a name="installing-and-configuring-hello-scenario"></a>Installation et configuration de scénario de hello
### <a name="1-install-hello-runbooks"></a>1. Installer les procédures opérationnelles de hello
Après avoir téléchargé hello runbooks, vous pouvez les importer à l’aide de la procédure hello dans [runbook graphique procédures](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-hello-description-and-requirements"></a>2. Révision hello description et configuration requise
Hello runbooks inclut une activité appelée **Lisez-moi** qui inclut une description et les ressources requises.  Vous pouvez afficher ces informations en sélectionnant hello **Lisez-moi** activité, puis hello **Script de flux de travail** paramètre.  Vous pouvez également obtenir hello les mêmes informations à partir de cet article.

### <a name="3-configure-assets"></a>3. Configuration des ressources
les runbooks de Hello nécessitent hello suivant les ressources que vous devez créer et remplir avec les valeurs appropriées.  les noms de Hello sont par défaut.  Vous pouvez utiliser des ressources avec des noms différents si vous spécifiez ces noms Bonjour [paramètres d’entrée](#using-the-runbooks) lorsque vous démarrez hello runbook.

| Type de ressource | Nom par défaut | Description |
|:--- |:--- |:--- |:--- |
| [Informations d'identification](automation-credentials.md) |AzureCredential |Contient des informations d’identification d’un compte qui a l’autorité toostart arrêter les machines virtuelles dans hello abonnement Azure. |
| [Variable](automation-variables.md) |AzureSubscriptionId |Contient l’ID d’abonnement hello de votre abonnement Azure. |

## <a name="using-hello-scenario"></a>À l’aide du scénario de hello
### <a name="parameters"></a>Paramètres
Hello procédures opérationnelles chaque disposer de hello [paramètres d’entrée](automation-starting-a-runbook.md#runbook-parameters).  Vous devez fournir des valeurs pour tous les paramètres obligatoires et pouvez éventuellement fournir des valeurs pour les autres paramètres, selon vos besoins.

| Paramètre | Type | Obligatoire | Description |
|:--- |:--- |:--- |:--- |
| ServiceName |string |Non |Si une valeur est fournie, toutes les machines virtuelles portant ce nom de service sont démarrées ou arrêtées.  Si aucune valeur n’est fournie, toutes les machines virtuelles classiques Bonjour abonnement Azure sont démarrés ou arrêtés. |
| AzureSubscriptionIdAssetName |string |Non |Contient le nom hello Hello [ressource de variable](#installing-and-configuring-the-scenario) qui contient l’ID d’abonnement hello de votre abonnement Azure.  Si vous ne spécifiez aucune valeur, la valeur *AzureSubscriptionId* est utilisée. |
| AzureCredentialAssetName |string |Non |Contient le nom hello Hello [actif d’informations d’identification](#installing-and-configuring-the-scenario) qui contient les informations d’identification de hello pour hello runbook toouse.  Si vous ne spécifiez aucune valeur, la valeur *AzureCredential* est utilisée. |

### <a name="starting-hello-runbooks"></a>Démarrage des runbook de hello
Vous pouvez utiliser une des méthodes hello dans [démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md) toostart une des procédures opérationnelles de hello dans cet article.

Hello suivant des exemples de commandes utilise Windows PowerShell toorun **StartAzureClassicVM** toostart tous les ordinateurs virtuels avec le nom du service hello *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Sortie
Hello runbooks sera [un message de sortie](automation-runbook-output-and-messages.md) pour chaque ordinateur virtuel indiquant hello ou non de démarrer ou d’instruction stop a été correctement envoyée.  Vous pouvez rechercher une chaîne spécifique dans le résultat de hello toodetermine hello sortie pour chaque runbook.  chaînes de sortie Hello sont répertoriées dans hello tableau suivant.

| Runbook | Condition | Message |
|:--- |:--- |:--- |
| StartAzureClassicVM |Machine virtuelle déjà en cours d'exécution |MyVM déjà en cours d’exécution |
| StartAzureClassicVM |Demande de démarrage de la machine virtuelle envoyée avec succès |MyVM démarrée |
| StartAzureClassicVM |Échec de la demande de démarrage de la machine virtuelle |Échec de MyVM toostart |
| StopAzureClassicVM |Machine virtuelle déjà en cours d'exécution |MyVM déjà arrêtée |
| StopAzureClassicVM |Demande de démarrage de la machine virtuelle envoyée avec succès |MyVM démarrée |
| StopAzureClassicVM |Échec de la demande de démarrage de la machine virtuelle |Échec de MyVM toostart |

Voici une image de l’utilisation de hello **StartAzureClassicVM** comme un [runbook enfant](automation-child-runbooks.md) dans un exemple de runbook graphique.  Cette méthode utilise les liaisons conditionnelles hello Bonjour tableau suivant.

| Lien | Critères |
|:--- |:--- |
| Lien de réussite |$ActivityOutput['StartAzureClassicVM'] -like "\* a été démarrée" |
| Lien d’erreur |$ActivityOutput['StartAzureClassicVM'] -notlike "\* a été démarrée" |

![Exemple de Runbook enfant](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Analyse détaillée
Voici une description détaillée des procédures opérationnelles de hello dans ce scénario.  Vous pouvez utiliser ces informations tooeither personnaliser hello runbooks ou toolearn uniquement à partir de celles-ci pour la création de vos propres scénarios d’automatisation.

### <a name="authentication"></a>Authentification
![Authentification](media/automation-solution-startstopvm/graphical-authentication.png)

Hello runbook commence par hello de tooset activités [informations d’identification](automation-credentials.md) et un abonnement Azure qui sera utilisé pour le reste de hello de hello runbook.

Hello tout d’abord deux activités, **obtenir l’Id abonnement** et **obtenir les informations d’identification Azure**, récupérer hello [actifs](#installing-the-runbook) qui sont utilisés par les activités de deux hello.  Ces activités peuvent spécifier directement les ressources hello, mais dont ils ont besoin des noms d’élément multimédia hello.  Étant donné que nous autorisons hello utilisateur toospecify ces noms Bonjour [paramètres d’entrée](#using-the-runbooks), nous avons besoin de ces ressources de hello tooretrieve activités avec un nom spécifié par le paramètre d’entrée.

**Ajouter-AzureAccount** jeux hello des informations d’identification qui seront utilisées pour le reste de hello de hello runbook.  ressource d’informations d’identification Hello qu’il extrait à partir de **obtenir les informations d’identification Azure** doit avoir accès toostart arrêt des machines virtuelles et Bonjour abonnement Azure.  abonnement utilisé Hello est sélectionné par **Select-AzureSubscription** qui utilise l’Id d’abonnement hello de **obtenir l’Id abonnement**.

### <a name="get-virtual-machines"></a>Obtenir des machines virtuelles
![Obtention de machines virtuelles](media/automation-solution-startstopvm/graphical-getvms.png)

Hello runbook doit toodetermine virtuels il travaillez et si elles sont déjà démarrés ou arrêtés (en fonction de runbook de hello).   Une des deux activités récupère les machines virtuelles de hello.  **Obtenir les machines virtuelles dans le Service** s’exécutera si hello *ServiceName* paramètre d’entrée pour hello runbook contient une valeur.  **Obtenir toutes les machines virtuelles** s’exécutera si hello *ServiceName* paramètre d’entrée pour hello runbook ne contient pas une valeur.  Cette logique est effectuée par des liaisons conditionnelles hello précédant chaque activité.

Les deux activités utilisent hello **Get-AzureVM** applet de commande.  **Obtenir toutes les machines virtuelles** utilise hello **ListAllVMs** paramètre défini tooreturn tous les ordinateurs virtuels.  **Obtenir les machines virtuelles dans le Service** utilise hello **GetVMByServiceAndVMName** paramètre défini et fournit hello **ServiceName** paramètre d’entrée pour hello **ServiceName**paramètre.  

### <a name="merge-vms"></a>Fusion de machines virtuelles
![Fusion de machines virtuelles](media/automation-solution-startstopvm/graphical-mergevms.png)

Hello **fusionner les machines virtuelles** activité est requis tooprovide d’entrée trop**Start-AzureVM** qui nécessite le nom de hello et service de toostart de machines virtuelles hello.  Cette entrée peut provenir de l’activité **Get All VMs** ou **Get VMs in Service**, mais **Start-AzureVM** ne peut spécifier qu’une activité pour son entrée.   

scénario de Hello est toocreate **fusionner les machines virtuelles** qui s’exécute hello **Write-Output** applet de commande.  Hello **InputObject** paramètre pour cette applet de commande est une Expression PowerShell qui combine entrée hello d’activités de hello deux précédents.  Comme une seule de ces activités s'exécutera, un seul jeu de sortie est attendu.  **Start-AzureVM** peut utiliser ce résultat pour ses paramètres d'entrée.

### <a name="startstop-virtual-machines"></a>Démarrage/arrêt de machines virtuelles
![Start VMs](media/automation-solution-startstopvm/graphical-startvm.png) ![Stop VMs](media/automation-solution-startstopvm/graphical-stopvm.png)

Selon hello runbook, les activités suivantes hello essayez toostart ou arrêt de l’utilisation de runbook hello **Start-AzureVM** ou **Stop-AzureVM**.  Étant donné que l’activité hello est précédée d’un lien de pipeline, il s’exécute une fois pour chaque objet retourné à partir de **fusionner les machines virtuelles**.  Bonjour lien est conditionnel afin que l’activité hello s’exécutera uniquement si hello *RunningState* Hello machine virtuelle est *arrêté* pour **Start-AzureVM** et  *Démarré* pour **Stop-AzureVM**. Si cette condition n’est pas remplie, puis **notifier a déjà été démarré** ou **notifier a déjà été arrêté** est exécutée toosend un message à l’aide de **Write-Output**.

### <a name="send-output"></a>Envoi de la sortie
![Notify Start VMs](media/automation-solution-startstopvm/graphical-notifystart.png) ![Notify Stop VMs](media/automation-solution-startstopvm/graphical-notifystop.png)

étape finale de Hello dans les runbook hello est toosend sortie hello indique si le début ou la demande d’arrêt pour chaque ordinateur virtuel a été correctement envoyée. Il existe un distinct **Write-Output** activité pour chacun, et nous déterminons le toorun un seul avec des liaisons conditionnelles.  **Notify VM Started** ou **Notify VM Stopped** est exécuté si *OperationStatus* indique *Succeeded*.  Si *OperationStatus* est une autre valeur, puis **Échec de la notification de tooStart** ou **tooStop d’échec de la notification** est exécuté.

## <a name="next-steps"></a>Étapes suivantes
* [Création de graphiques dans Azure Automation](automation-graphical-authoring-intro.md)
* [Runbooks enfants dans Azure Automation](automation-child-runbooks.md)
* [Sortie et messages de Runbook dans Azure Automation](automation-runbook-output-and-messages.md)
