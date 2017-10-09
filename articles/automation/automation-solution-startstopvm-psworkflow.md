---
title: "aaaStarting et l’arrêt des machines virtuelles avec Azure Automation - flux de travail PowerShell | Documents Microsoft"
description: "Version graphique du scénario Azure Automation, y compris des procédures opérationnelles toostart et arrêter les machines virtuelles classiques."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
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

Il s’agit de hello version du runbook PowerShell Workflow de ce scénario. Elle est également disponible à l’aide des [runbooks graphiques](automation-solution-startstopvm-graphical.md).

## <a name="getting-hello-scenario"></a>Scénario de hello mise en route
Ce scénario se compose de deux runbook PowerShell Workflow que vous pouvez télécharger à partir de hello suivant liens.  Consultez hello [version graphique](automation-solution-startstopvm-graphical.md) de ce scénario pour les runbooks graphiques toohello de liens.

| Runbook | Lien | Type | Description |
|:--- |:--- |:--- |:--- |
| Start-AzureVMs |[Démarrer les machines virtuelles Azure classiques](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |Workflow PowerShell |Démarre toutes les machines virtuelles classiques d’un abonnement Azure ou toutes les machines virtuelles portant un nom de service particulier. |
| Stop-AzureVMs |[Arrêter les machines virtuelles Azure classiques](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |Workflow PowerShell |Arrête toutes les machines virtuelles d’un compte Automation ou toutes les machines virtuelles portant un nom de service particulier. |

## <a name="installing-and-configuring-hello-scenario"></a>Installation et configuration de scénario de hello
### <a name="1-install-hello-runbooks"></a>1. Installer les procédures opérationnelles de hello
Après avoir téléchargé hello runbooks, vous pouvez les importer à l’aide de la procédure hello dans [importation d’un Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-hello-description-and-requirements"></a>2. Révision hello description et configuration requise
Hello runbooks inclure le texte d’aide commentées qui inclut une description et les ressources requises.  Vous pouvez également obtenir hello les mêmes informations à partir de cet article.

### <a name="3-configure-assets"></a>3. Configuration des ressources
les runbooks de Hello nécessitent hello suivant les ressources que vous devez créer et remplir avec les valeurs appropriées.

| Type de ressource | Nom de la ressource | Description |
|:--- |:--- |:--- |:--- |
| Informations d'identification |AzureCredential |Contient des informations d’identification d’un compte qui a l’autorité toostart arrêter les machines virtuelles dans hello abonnement Azure.  Vous pouvez également spécifier une autre ressource d’informations d’identification Bonjour **informations d’identification** paramètre Hello **Add-AzureAccount** activité. |
| Variable |AzureSubscriptionId |Contient l’ID d’abonnement hello de votre abonnement Azure. |

## <a name="using-hello-scenario"></a>À l’aide du scénario de hello
### <a name="parameters"></a>Paramètres
Hello procédures opérationnelles chaque ont hello paramètres suivants.  Vous devez fournir des valeurs pour tous les paramètres obligatoires et pouvez éventuellement fournir des valeurs pour les autres paramètres, selon vos besoins.

| Paramètre | Type | Obligatoire | Description |
|:--- |:--- |:--- |:--- |
| ServiceName |string |Non |Si une valeur est fournie, toutes les machines virtuelles portant ce nom de service sont démarrées ou arrêtées.  Si aucune valeur n’est fournie, toutes les machines virtuelles classiques Bonjour abonnement Azure sont démarrés ou arrêtés. |
| AzureSubscriptionIdAssetName |string |Non |Contient le nom hello Hello [ressource de variable](#installing-and-configuring-the-scenario) qui contient l’ID d’abonnement hello de votre abonnement Azure.  Si vous ne spécifiez aucune valeur, la valeur *AzureSubscriptionId* est utilisée. |
| AzureCredentialAssetName |string |Non |Contient le nom hello Hello [actif d’informations d’identification](#installing-and-configuring-the-scenario) qui contient les informations d’identification de hello pour hello runbook toouse.  Si vous ne spécifiez aucune valeur, la valeur *AzureCredential* est utilisée. |

### <a name="starting-hello-runbooks"></a>Démarrage des runbook de hello
Vous pouvez utiliser une des méthodes hello dans [démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md) toostart une des procédures opérationnelles de hello dans ce scénario.

Hello suivant des exemples de commandes utilise Windows PowerShell toorun **StartAzureVMs** toostart tous les ordinateurs virtuels avec le nom du service hello *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Sortie
Hello runbooks sera [un message de sortie](automation-runbook-output-and-messages.md) pour chaque ordinateur virtuel indiquant hello ou non de démarrer ou d’instruction stop a été correctement envoyée.  Vous pouvez rechercher une chaîne spécifique dans le résultat de hello toodetermine hello sortie pour chaque runbook.  chaînes de sortie Hello sont répertoriées dans hello tableau suivant.

| Runbook | Condition | Message |
|:--- |:--- |:--- |
| Start-AzureVMs |Machine virtuelle déjà en cours d’exécution |MyVM déjà en cours d’exécution |
| Start-AzureVMs |Demande de démarrage de la machine virtuelle envoyée avec succès |MyVM démarrée |
| Start-AzureVMs |Échec de la demande de démarrage de la machine virtuelle |Échec de MyVM toostart |
| Stop-AzureVMs |Machine virtuelle déjà arrêtée |MyVM déjà arrêtée |
| Stop-AzureVMs |Demande d’arrêt de la machine virtuelle envoyée avec succès |MyVM arrêtée |
| Stop-AzureVMs |Échec de la demande d’arrêt de la machine virtuelle |Échec de MyVM toostop |

Par exemple, hello suivant extrait de code à partir d’un runbook tente toostart tous les ordinateurs virtuels avec le nom du service hello *MyServiceName*.  Si un des hello démarre demandes échouent, les actions d’erreur peuvent entreprendre.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a>Analyse détaillée
Voici une description détaillée des procédures opérationnelles de hello dans ce scénario.  Vous pouvez utiliser ces informations tooeither personnaliser hello runbooks ou toolearn uniquement à partir de celles-ci pour la création de vos propres scénarios d’automatisation.

### <a name="parameters"></a>Paramètres
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

Hello workflow démarre en obtenant les valeurs hello pour hello [paramètres d’entrée](#using-the-scenario).  Si les noms des éléments hello ne sont pas fournies noms par défaut sont utilisés.

### <a name="output"></a>Sortie
    # Returns strings with status messages
    [OutputType([String])]

Cette ligne déclare que la sortie hello de hello runbook sera une chaîne.  Cela n’est pas obligatoire mais est recommandé pour lorsque hello runbook est utilisé comme un [runbook enfant](automation-child-runbooks.md) afin qu’un runbook parent connaissent la sortie de hello tooexpect de type.

### <a name="authentication"></a>Authentification
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

les lignes suivantes Hello définissent hello [informations d’identification](automation-credentials.md) et un abonnement Azure qui sera utilisé pour le reste de hello de hello runbook.
Tout d’abord, nous utilisons **Get-AutomationPSCredential** asset hello tooget qui contient les informations d’identification de hello avec accès des machines virtuelles toostart et d’arrêter Bonjour abonnement Azure. **Ajouter-AzureAccount** utilise ensuite cette informations d’identification de ressource tooset hello.  sortie de Hello est attribué variable factice de tooa afin qu’il n’est pas inclus dans la sortie du runbook hello.  

ressource de variable Hello avec abonnement hello ID est ensuite extraite avec **Get-AutomationVariable** et abonnement hello avec **Select-AzureSubscription**.

### <a name="get-vms"></a>Obtention de machines virtuelles
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** est utilisé tooretrieve virtuels hello hello runbook fonctionnera avec.  Si une valeur est fournie dans hello **ServiceName** d’entrée variable, puis uniquement des machines virtuelles hello portant ce nom de service sont récupérés.  Si **ServiceName** est vide, toutes les machines virtuelles sont récupérées.

### <a name="startstop-virtual-machines-and-send-output"></a>Démarrage/arrêt des machines virtuelles et envoi de sorties
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

les lignes suivantes Hello Parcourez chaque ordinateur virtuel.  Tout d’abord hello **PowerState** hello machine virtuelle est activé toosee si elle est déjà en cours d’exécution ou arrêté, selon les runbook hello.  Si elle est déjà dans l’état cible de hello, un message est envoyé toooutput et se termine le runbook hello.  Si ce n’est pas le cas, puis **Start-AzureVM** ou **Stop-AzureVM** est utilisé tooattempt toostart ou arrêt hello virtuels avec un résultat de variable de hello demande tooa stockée hello.  Un message est ensuite envoyé toooutput spécifiant si hello demande toostart ou arrêt a été soumise.

## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur l’utilisation des procédures opérationnelles enfant, consultez [runbooks enfants dans Azure Automation](automation-child-runbooks.md)
* toolearn en savoir plus sur les messages pendant l’exécution du runbook et de journalisation toohelp résoudre les problèmes de sortie, consultez [Runbook sortie et les messages dans Azure Automation](automation-runbook-output-and-messages.md)

