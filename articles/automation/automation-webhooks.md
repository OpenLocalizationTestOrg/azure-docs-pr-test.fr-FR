---
title: aaaStarting un runbook Azure Automation avec un webhook | Documents Microsoft
description: "Un webhook qui permet à un client toostart un runbook dans Azure Automation à partir d’un appel HTTP.  Cet article décrit comment toocreate un webhook et comment toostart d’un toocall un runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a>Démarrage d’un runbook Azure Automation avec un webhook
A *webhook* vous permet de toostart un runbook donné dans Azure Automation via une requête HTTP unique. Cela permet à des services externes tels que Visual Studio Team Services, GitHub, Analytique de journal de Microsoft Operations Management Suite ou des applications personnalisées toostart runbooks sans avoir à implémenter une solution complète à l’aide de hello API Azure Automation.  
![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)

Vous pouvez comparer des méthodes de tooother webhooks de démarrage d’un runbook [démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md)

## <a name="details-of-a-webhook"></a>Détails d'un webhook
Hello tableau suivant décrit les propriétés hello que vous devez configurer pour un webhook.

| Propriété | Description |
|:--- |:--- |
| Nom |Vous pouvez fournir le nom de que votre choix pour un webhook car il s’agit pas exposées toohello client.  Elle est utilisée uniquement pour vous tooidentify hello runbook dans Azure Automation. <br>  Comme meilleure pratique, vous devez donner hello webhook un client nom toohello connexes qui l’utilise. |
| URL |URL de Hello de hello webhook est adresse unique de hello qu’un client appelle avec un runbook de hello HTTP POST toostart lié toohello webhook.  Il est généré automatiquement lorsque vous créez hello webhook.  Vous ne pouvez pas spécifier d'URL personnalisée. <br> <br>  URL de Hello contient un jeton de sécurité qui permet de hello runbook toobe est appelée par un système tiers avec aucune authentification supplémentaire. Pour cette raison, elle doit être traitée comme un mot de passe.  Pour des raisons de sécurité, vous pouvez uniquement les hello affichage QU'URL Bonjour Azure portal à hello temps hello webhook est créé. Notez l’URL hello dans un emplacement sécurisé pour un usage ultérieur. |
| Date d'expiration |Comme un certificat, chaque webhook possède une date d'expiration à partir de laquelle il ne peut plus être utilisé.  Cette date d’expiration peut être modifiée après la création de hello webhook. |
| Activé |Un webhook est activé par défaut lorsqu'il est créé.  Si vous lui affectez tooDisabled, aucun client ne peut être en mesure de toouse il.  Vous pouvez définir hello **activé** propriété lorsque vous créez hello webhook ou à tout moment une fois qu’il est créée. |

### <a name="parameters"></a>Paramètres
Un webhook peut définir les valeurs des paramètres de runbook qui sont utilisés quand hello runbook est démarrée par ce webhook. Hello webhook doit inclure des valeurs pour tous les paramètres obligatoires du runbook de hello et peut-être inclure des valeurs pour les paramètres optionnels. Un webhook de tooa de valeur configurée de paramètre peut être modifié même après la création de hello webhoook. Plusieurs webhooks lié tooa unique runbook peut utiliser différentes valeurs de paramètre.

Lorsqu’un client démarre un runbook à l’aide d’un webhook, il ne peut pas remplacer les valeurs de paramètre hello définies dans hello webhook.  tooreceive des données à partir du client de hello, hello runbook peut accepter un paramètre unique appelé **$WebhookData** de type (objet) qui contiendra les données que le client hello inclut dans la demande POST hello.

![Propriétés Webhookdata](media/automation-webhooks/webhook-data-properties.png)

Hello **$WebhookData** objet aura hello propriétés suivantes :

| Propriété | Description |
|:--- |:--- |
| WebhookName |nom de Hello de hello webhook. |
| RequestHeader |Table de hachage qui contient des en-têtes de hello de requête de publication entrant hello. |
| RequestBody |corps Hello de requête de publication entrant hello.  Ceci conserve les mises en forme telles que les chaînes, JSON, XML ou les données de formulaire codées. Hello runbook doit être écrites toowork au format de données hello est attendu. |

Aucune configuration de hello de hello webhook toosupport requis est **$WebhookData** paramètre, et hello runbook n’est pas requis tooaccept il.  Si les runbook hello ne définit pas de paramètre hello, tous les détails de demande hello envoyés à partir du client de hello est ignoré.

Si vous spécifiez une valeur pour $WebhookData lorsque vous créez hello webhook, cette valeur sera remplacée au démarrage hello webhook hello runbook avec des données hello de demande de publication hello client, même si le client de hello n’inclut pas de données dans le corps de la demande hello.  Si vous démarrez un runbook qui a $WebhookData à l’aide d’une méthode autre qu’un webhook, vous pouvez fournir une valeur pour $Webhookdata qui peut être reconnu par les runbook hello.  Cette valeur doit être un objet avec hello même [propriétés](#details-of-a-webhook) comme $Webhookdata afin que runbook hello correctement les utiliser comme s’il fonctionnait avec WebhookData réel passé par un webhook.

Par exemple, si vous démarrez hello suivant runbook hello portail Azure et que vous souhaitez toopass certains exemples WebhookData de test, étant donné que WebhookData est un objet, il doit être passé au format JSON hello l’interface utilisateur.

![Paramètre WebhookData à partir de l'interface utilisateur](media/automation-webhooks/WebhookData-parameter-from-UI.png)

Pourquoi au-dessus de runbook, si vous avez hello propriétés pour le paramètre de WebhookData hello suivantes :

1. WebhookName: *MyWebhook*
2. RequestHeader: *From=Test User*
3. RequestBody: *[“VM1”, “VM2”]*

Vous pouvez ensuite transmettre hello valeur JSON Bonjour l’interface utilisateur pour le paramètre de WebhookData hello suivante :  

* {"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}

![Démarrage du paramètre WebhookData à partir de l'interface utilisateur](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> les valeurs de Hello de tous les paramètres d’entrée sont enregistrées avec la tâche du runbook hello.  Cela signifie que les entrées fournies par le client hello dans la demande de webhook hello sera tooanyone connecté et disponible avec la tâche d’automatisation toohello accès.  Pour cette raison, soyez prudent lorsque vous incluez des informations sensibles dans les appels du webhook.
>

## <a name="security"></a>Sécurité
sécurité Hello d’un webhook s’appuie sur la confidentialité hello de son URL qui contient un jeton de sécurité qui lui permet de toobe appelé. Azure Automation n’effectue pas d’authentification à la demande de hello tant que rend toohello l’URL appropriée. Pour cette raison, webhooks ne doit pas servir de runbook qui exécutent des fonctions très sensibles sans utiliser un autre moyen de la validation de demande de hello.

Vous pouvez inclure une logique dans hello toodetermine de runbook qu’elle a été appelée par un webhook en vérifiant hello **WebhookName** propriété de paramètre hello $WebhookData. Hello runbook peut effectuer une validation supplémentaire en recherchant des informations spécifiques contenues dans hello **RequestHeader** ou **RequestBody** propriétés.

Une autre stratégie consiste à toohave hello runbook effectuer une validation d’une condition externe lorsqu’il a reçu une demande de webhook.  Par exemple, considérez un runbook qui est appelé par GitHub chaque fois qu’il existe un référentiel GitHub tooa validation.  Hello runbook risquent de se connecter toovalidate de tooGitHub une nouvelle validation s’est produite en fait juste avant de continuer.

## <a name="creating-a-webhook"></a>Création d'un webhook
Utilisez hello suivant la procédure toocreate un runbook tooa webhook lié Bonjour portail Azure.

1. À partir de hello **Runbooks panneau** Bonjour portail Azure, cliquez sur runbook hello hello webhook démarrera tooview son panneau de détails.
2. Cliquez sur **Webhook** haut hello hello de hello panneau tooopen **ajouter un Webhook** panneau. <br>
   ![Bouton Webhooks](media/automation-webhooks/webhooks-button.png)
3. Cliquez sur **créer nouveau webhook** tooopen hello **créer webhook panneau**.
4. Spécifiez un **nom**, **Date d’Expiration** pour hello webhook et si elle doit être activée. Pour plus d'informations sur ces propriétés, consultez [Détails d'un webhook](#details-of-a-webhook) .
5. Cliquez sur icône de copie hello et appuyez sur Ctrl + C toocopy hello URL de hello webhook.  Puis enregistrez-la dans un endroit sûr.  **Une fois que vous créez hello webhook, vous ne pouvez pas récupérer l’URL de hello à nouveau.** <br>
   ![URL du webhook](media/automation-webhooks/copy-webhook-url.png)
6. Cliquez sur **paramètres** tooprovide les valeurs des paramètres de runbook hello.  Si hello runbook a des paramètres obligatoires, puis vous ne serez pas en mesure de toocreate hello webhook, sauf si les valeurs sont fournies.
7. Cliquez sur **créer** toocreate hello webhook.

## <a name="using-a-webhook"></a>Utilisation d'un webhook
toouse un webhook après que qu’il a été créé, votre application cliente doit émettre une requête HTTP POST avec l’URL de hello hello webhook.  syntaxe de Hello de hello webhook sera Bonjour suivant le format.

    http://<Webhook Server>/token?=<Token Value>

Hello client reçoit un des hello suivant des codes de retour de demande de publication hello.  

| Code | Texte | Description |
|:--- |:--- |:--- |
| 202 |Acceptée |Hello demande a été acceptée et hello runbook a été correctement en file d’attente. |
| 400 |Demande incorrecte |demande de Hello n’a pas été acceptée pour l’une des hello suivant raisons. <ul> <li>Hello webhook a expiré.</li> <li>Hello webhook est désactivé.</li> <li>jeton Hello dans hello URL n’est pas valide.</li>  </ul> |
| 404 |Introuvable |demande de Hello n’a pas été acceptée pour l’une des hello suivant raisons. <ul> <li>Hello webhook est introuvable.</li> <li>Hello runbook est introuvable.</li> <li>Impossible de trouver le compte de Hello.</li>  </ul> |
| 500 |Erreur interne du serveur |URL de Hello était valide, mais une erreur s’est produite.  Soumettez la demande de hello. |

En supposant que hello demande réussit, la réponse de webhook hello contient les id de tâche hello au format JSON comme suit. Il contient un id de tâche unique, mais permet de format JSON de hello pour les améliorations futures potentielles.

    {"JobIds":["<JobId>"]}  

Impossible de déterminer les client Hello hello runbook tâche se termine ou son état d’achèvement de hello webhook.  Il peut déterminer ces informations à l’aide d’id de tâche hello avec une autre méthode comme [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) ou hello [API Azure Automation](https://msdn.microsoft.com/library/azure/mt163826.aspx).

### <a name="example"></a>Exemple
Bonjour à l’exemple suivant utilise Windows PowerShell toostart un runbook avec un webhook.  Notez que n'importe quel langage qui peut effectuer une requête HTTP peut utiliser un webhook ; Windows PowerShell est uniquement utilisé ici à titre d'exemple.

Hello runbook attend une liste d’ordinateurs virtuels au format JSON dans des corps de hello de demande de hello. Nous allons également inclure des informations qui démarre hello runbook et hello date et l’heure en cours de démarrage dans l’en-tête hello de demande de hello.      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


Hello image suivante montre les informations d’en-tête hello (à l’aide un [Fiddler](http://www.telerik.com/fiddler) trace) à partir de cette demande. Cela inclut les en-têtes standard d’une requête HTTP dans Ajout toohello Date personnalisé et des en-têtes que nous avons ajouté.  Chacune de ces valeurs est runbook toohello disponible Bonjour **RequestHeaders** propriété du **WebhookData**.

![Bouton Webhooks](media/automation-webhooks/webhook-request-headers.png)

Hello image suivante montre les corps de hello de demande de hello (à l’aide un [Fiddler](http://www.telerik.com/fiddler) trace) qui est disponible toohello runbook Bonjour **RequestBody** propriété du **WebhookData**. Il est mis en forme en tant que JSON car il s’agit de format hello qui était inclus dans le corps de hello de demande de hello.     

![Bouton Webhooks](media/automation-webhooks/webhook-request-body.png)

Hello image suivante illustre les demande hello envoyé à partir de Windows PowerShell et les réponses hello.  id de tâche Hello est extraite de la réponse de hello et de chaîne de tooa converti.

![Bouton Webhooks](media/automation-webhooks/webhook-request-response.png)

Bonjour exemple de runbook suivant accepte hello précédent exemple de demande et démarre les ordinateurs virtuels de hello spécifiés dans le corps de la demande hello.

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a>À partir de procédures opérationnelles alertes de réponse de tooAzure
Compatible Webhook les procédures opérationnelles peut être utilisé tooreact trop[alertes Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Ressources dans Azure peuvent être surveillés par la collecte des statistiques telles que les performances, la disponibilité et d’utilisation à l’aide de hello d’alertes Azure hello. Vous pouvez recevoir une alerte basée sur des métriques ou événements de surveillance pour vos ressources Azure ; actuellement les comptes Automation prennent uniquement en charge les métriques. Lorsque la valeur hello d’une métrique spécifique dépasse seuil hello affectée ou si hello configuré est déclenché une notification est envoyée toohello service admin coadministrateurs tooresolve hello alerte ou, pour plus d’informations sur les métriques et événements, consultez trop[ Alertes Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

Outre l’utilisation des alertes Azure comme un système de notification, vous pouvez également déclencher procédures opérationnelles dans la réponse tooalerts. Azure Automation fournit des runbooks hello capacité toorun compatible webhook alertes Azure. Quand une métrique dépasse hello configuré valeur de seuil, une règle d’alerte hello devient active et déclencheurs hello webhook automation qui à son tour exécute hello runbook.

![Webhooks](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a>Contexte de l’alerte
Considérez une ressource Azure comme un ordinateur virtuel, l’utilisation du processeur de cet ordinateur est une des mesures de performance clés hello. Si hello l’utilisation du processeur est de 100 % ou supérieure à une certaine quantité pour une longue période de temps, vous pourriez le problème hello toofix toorestart hello machine virtuelle. Cela peut être résolu en configurant une machine virtuelle de toohello une règle d’alerte et cette règle prend le pourcentage de processeur comme métrique. Pourcentage d’UC est uniquement exécutée par exemple, mais il existe de nombreuses autres métriques que vous pouvez configurer tooyour Azure de ressources et de redémarrer la machine virtuelle de hello est une action qui est effectuée toofix ce problème, vous pouvez configurer d’autres actions hello runbook tootake.

Lorsque cette règle d’alerte hello devient active et déclencheurs hello compatible webhook de runbook, il envoie hello contexte de l’alerte toohello runbook. [Contexte de l’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contient les détails, notamment **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** et **Timestamp** qui sont requis pour hello runbook tooidentify hello ressource sur laquelle il effectuer action. Alerte de contexte est incorporé dans le corps de hello Hello **WebhookData** toohello envoyé runbook de l’objet et il est accessible avec **Webhook.RequestBody** propriété

### <a name="example"></a>Exemple
Créer une machine virtuelle Azure dans votre abonnement et à associer un [toomonitor processeur pourcentage métrique d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Lors de la création d’alerte de hello Assurez-vous de que remplir le champ de webhook hello avec l’URL de hello de webhook hello qui a été généré lors de la création du webhook de hello.

exemple de runbook suivant Hello est déclenchée lorsque la règle d’alerte hello devient active et collecte des paramètres de contexte de l’alerte hello qui sont requis pour hello runbook tooidentify hello ressource sur laquelle il prendra action.

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur les différentes façons toostart un runbook, consultez [démarrage d’un Runbook](automation-starting-a-runbook.md).
* Pour plus d’informations sur l’affichage hello état d’un Job de Runbook, consultez trop[l’exécution du Runbook dans Azure Automation](automation-runbook-execution.md).
* toolearn toouse action de tootake Azure Automation sur Azure, alertes, voir [corriger des alertes de machine virtuelle Azure avec des Runbooks Automation](automation-azure-vm-alert-integration.md).
