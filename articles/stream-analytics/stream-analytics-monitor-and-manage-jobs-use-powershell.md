---
title: "aaaMonitor et gérer des tâches de flux de données Analytique avec PowerShell | Documents Microsoft"
description: "Découvrez comment toomonitor d’Azure PowerShell et les applets de commande toouse et gérer des tâches de flux de données Analytique."
keywords: azure powershell, applets de commande azure powershell, commande powershell, scripts powershell
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a>Surveillance et gestion des travaux Stream Analytics à l’aide des applets de commande Azure PowerShell
Découvrez comment toomonitor et gérer les ressources de flux de données Analytique avec les applets de commande PowerShell de Azure et l’écriture de scripts powershell qui exécutent des tâches de flux de données Analytique base.

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a>Conditions requises pour l'exécution des applets de commande Azure PowerShell pour Stream Analytics
* Créez un groupe de ressources Azure dans votre abonnement. Hello Voici un exemple de script Azure PowerShell. Pour obtenir des informations sur Azure PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).  

Azure PowerShell 0.9.8 :  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

Azure PowerShell 1.0 :  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> Par défaut, la surveillance n’est pas activée pour les travaux Stream Analytics créés par programme.  Vous pouvez manuellement activer l’analyse dans le portail Azure en parcourant la page de surveillance de la tâche toohello de hello et en cliquant sur le bouton Activer de hello ou vous pouvez le faire par programme en suivant les étapes de hello situés [Analytique de flux de données Azure - analyse de flux de données Analytique des travaux par programmation](stream-analytics-monitor-jobs.md).
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a>Applets de commande Azure PowerShell pour Stream Analytics
Hello suivant d’applets de commande PowerShell de Azure peut être utilisé toomonitor et gérer des tâches d’Analytique de flux de données Azure. Notez qu'il existe différentes versions d'Azure PowerShell. 
**Dans les exemples hello hello répertoriés première commande est de Azure PowerShell 0.9.8, commande deuxième hello est pour Azure PowerShell 1.0.** commandes Hello Azure PowerShell 1.0 aura toujours « Azure Resource Manager » dans la commande hello.

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a>Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob
Répertorie toutes les tâches de flux de données Analytique définies dans hello abonnement Azure ou le groupe de ressources spécifié, ou obtient des informations sur une tâche spécifique au sein d’un groupe de ressources.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Get-AzureStreamAnalyticsJob

Azure PowerShell 1.0 :  

    Get-AzureRMStreamAnalyticsJob

Cette commande PowerShell retourne des informations sur toutes les tâches de flux de données Analytique hello Bonjour abonnement Azure.

**Exemple 2**

Azure PowerShell 0.9.8 :  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Azure PowerShell 1.0 :  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Cette commande PowerShell retourne des informations sur toutes les tâches de flux de données Analytique hello dans le groupe de ressources hello Stream Analytics par défaut-Centre des États-Unis.

**Exemple 3**

Azure PowerShell 0.9.8 :  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Azure PowerShell 1.0 :  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Cette commande PowerShell retourne des informations sur la tâche de flux de données Analytique hello StreamingJob dans le groupe de ressources hello Stream Analytics par défaut-Centre des États-Unis.

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a>Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput
Répertorie toutes les entrées de hello qui sont définies dans une tâche de flux de données Analytique spécifiée ou obtient des informations sur une entrée spécifique.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0 :  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Cette commande PowerShell retourne des informations sur toutes les entrées de hello définis dans le travail hello StreamingJob.

**Exemple 2**

Azure PowerShell 0.9.8 :  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0 :  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Cette commande PowerShell retourne des informations sur les entrées hello nommée EntryStream défini dans le travail hello StreamingJob.

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a>Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput
Répertorie toutes les sorties hello qui sont définies dans une tâche de flux de données Analytique spécifiée ou obtient des informations sur une sortie spécifique.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0 :  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Cette commande PowerShell retourne des informations sur les sorties hello définies dans la tâche de hello StreamingJob.

**Exemple 2**

Azure PowerShell 0.9.8 :  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Azure PowerShell 1.0 :  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Cette commande PowerShell retourne des informations sur la sortie hello nommé défini dans le travail hello StreamingJob de sortie.

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a>Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota
Obtient les informations de quota de hello de diffusion en continu les unités dans la région spécifiée.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

Azure PowerShell 1.0 :  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

Cette commande PowerShell retourne des informations sur le quota de hello et de l’utilisation des unités de diffusion en continu dans la région du centre des États-Unis hello.

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a>Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation
Obtient des informations sur une transformation spécifique définie dans un travail Stream Analytics.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Azure PowerShell 1.0 :  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Cette commande PowerShell retourne des informations sur la transformation hello appelée StreamingJob dans la tâche de hello StreamingJob.

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a>New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput
Crée une entrée dans un travail Stream Analytics ou met à jour une entrée spécifiée existante.

Hello nom de l’entrée de hello peut être spécifié dans le fichier .json de hello ou sur la ligne de commande hello. Si les deux sont spécifiées, nom hello sur la ligne de commande hello doit hello identique hello un fichier de hello.

Si vous spécifiez une entrée existe déjà et que vous ne spécifiez pas hello – paramètre Force, applet de commande hello demandera ou non tooreplace hello entrée existante.

Si vous spécifiez hello – paramètre Force et spécifiez un existant, nom d’entrée, hello entrée sera remplacée sans confirmation.

Pour plus d’informations sur la structure du fichier JSON hello et de contenu, consultez toohello [créer une entrée (Analytique de flux de données Azure)] [ msdn-rest-api-create-stream-analytics-input] section Hello [API REST de gestion des flux de données Analytique Bibliothèque de référence][stream.analytics.rest.api.reference].

**Exemple 1**

Azure PowerShell 0.9.8 :  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Azure PowerShell 1.0 :  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Cette commande PowerShell crée une nouvelle entrée à partir du fichier de hello Input.json. Si une entrée existante avec le nom hello spécifié dans le fichier de définition d’entrée de hello est déjà définie, l’applet de commande hello vous demande ou non tooreplace il.

**Exemple 2**

Azure PowerShell 0.9.8 :  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Azure PowerShell 1.0 :  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Cette commande PowerShell crée une entrée dans la tâche hello appelé EntryStream. Si une entrée existante portant ce nom est déjà définie, l’applet de commande hello vous demande ou non tooreplace il.

**Exemple 3**

Azure PowerShell 0.9.8 :  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Azure PowerShell 1.0 :  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Cette commande PowerShell remplace la définition de hello de source d’entrée existante hello appelé EntryStream avec définition hello à partir du fichier de hello.

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a>New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob
Crée une tâche de flux de données Analytique dans Microsoft Azure, ou met à jour de définition de hello d’une tâche spécifiée existante.

nom de Hello du travail de hello peut être spécifié dans le fichier .json de hello ou sur la ligne de commande hello. Si les deux sont spécifiées, nom hello sur la ligne de commande hello doit hello identique hello un fichier de hello.

Si vous spécifiez un nom de tâche existe déjà et que vous ne spécifiez pas hello – paramètre Force, applet de commande hello demandera ou non tooreplace hello travail existant.

Si vous spécifiez hello – paramètre Force et spécifiez un nom de travail existant, définition de la tâche hello est remplacée sans confirmation.

Pour plus d’informations sur la structure du fichier JSON hello et de contenu, consultez toohello [créer une tâche de flux de données Analytique] [ msdn-rest-api-create-stream-analytics-job] section Hello [référence d’API REST gestion des flux de données Analytique Bibliothèque][stream.analytics.rest.api.reference].

**Exemple 1**

Azure PowerShell 0.9.8 :  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Azure PowerShell 1.0 :  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Cette commande PowerShell crée une nouvelle tâche à partir de la définition de hello dans JobDefinition.json. Si un travail existant avec le nom hello spécifié dans le fichier de définition de tâche hello est déjà défini, l’applet de commande hello vous demande ou non tooreplace il.

**Exemple 2**

Azure PowerShell 0.9.8 :  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Azure PowerShell 1.0 :  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Cette commande PowerShell remplace la définition de tâche hello StreamingJob.

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a>New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput
Crée une sortie dans un travail Stream Analytics ou met à jour une sortie existante.  

nom de Hello de sortie de hello peut être spécifié dans le fichier .json de hello ou sur la ligne de commande hello. Si les deux sont spécifiées, nom hello sur la ligne de commande hello doit hello identique hello un fichier de hello.

Si vous spécifiez une sortie qui existe déjà et que vous ne spécifiez pas hello – paramètre Force, applet de commande hello demandera ou non tooreplace hello sortie existant.

Si vous spécifiez hello – paramètre Force et spécifiez le nom de sortie existant, la sortie de hello est remplacé sans confirmation.

Pour plus d’informations sur la structure du fichier JSON hello et de contenu, consultez toohello [créer une sortie (Analytique de flux de données Azure)] [ msdn-rest-api-create-stream-analytics-output] section Hello [API REST de gestion des flux de données Analytique Bibliothèque de référence][stream.analytics.rest.api.reference].

**Exemple 1**

Azure PowerShell 0.9.8 :  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Azure PowerShell 1.0 :  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Cette commande PowerShell crée une sortie appelée « sortie » dans la tâche de hello StreamingJob. Si une sortie existante portant ce nom est déjà définie, l’applet de commande hello vous demande ou non tooreplace il.

**Exemple 2**

Azure PowerShell 0.9.8 :  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Azure PowerShell 1.0 :  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Cette commande PowerShell remplace la définition de hello de « sortie » dans la tâche de hello StreamingJob.

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a>New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation
Crée une nouvelle transformation au sein d’une tâche de flux de données Analytique ou met à jour de la transformation de hello existant.

nom de Hello de transformation de hello peut être spécifié dans le fichier .json de hello ou sur la ligne de commande hello. Si les deux sont spécifiées, nom hello sur la ligne de commande hello doit hello identique hello un fichier de hello.

Si vous spécifiez une transformation qui existe déjà et que vous ne spécifiez pas hello – paramètre Force, applet de commande hello demandera ou non tooreplace hello transformation existante.

Si vous spécifiez hello – paramètre Force et spécifiez un nom existant de la transformation, la transformation de hello est remplacée sans confirmation.

Pour plus d’informations sur la structure du fichier JSON hello et de contenu, consultez toohello [créer une Transformation (Analytique de flux de données Azure)] [ msdn-rest-api-create-stream-analytics-transformation] section Hello [gestion des flux de données Analytique Bibliothèque de référence d’API REST][stream.analytics.rest.api.reference].

**Exemple 1**

Azure PowerShell 0.9.8 :  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Azure PowerShell 1.0 :  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Cette commande PowerShell crée une nouvelle transformation appelée StreamingJobTransform dans la tâche de hello StreamingJob. Si une transformation existante est déjà définie avec ce nom, l’applet de commande hello vous demande ou non tooreplace il.

**Exemple 2**

Azure PowerShell 0.9.8 :  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

Azure PowerShell 1.0 :  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 Cette commande PowerShell remplace la définition de hello de StreamingJobTransform dans la tâche de hello StreamingJob.

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a>Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput
Supprime de manière asynchrone une entrée spécifique d'un travail Stream Analytics dans Microsoft Azure.  
Si vous spécifiez hello – paramètre Force, hello d’entrée est supprimée sans confirmation.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Azure PowerShell 1.0 :  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Cette commande PowerShell supprime hello EventStream d’entrée dans la tâche de hello StreamingJob.  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a>Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob
Supprime de manière asynchrone un travail Stream Analytics spécifique dans Microsoft Azure.  
Si vous spécifiez hello – paramètre Force, hello travail sera supprimée sans confirmation.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0 :  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Cette commande PowerShell supprime le travail de hello StreamingJob.  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a>Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput
Supprime de manière asynchrone une sortie spécifique d'un travail Stream Analytics dans Microsoft Azure.  
Si vous spécifiez hello – paramètre Force, hello sortie sera supprimée sans confirmation.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0 :  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Sortie de sortie de cette commande supprime hello de PowerShell dans la tâche de hello StreamingJob.  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a>Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob
Déploie et démarre un travail Stream Analytics dans Microsoft Azure de façon asynchrone.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Azure PowerShell 1.0 :  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Cette commande PowerShell démarre hello travail StreamingJob avec une heure de début de sortie personnalisée définie tooDecember 12, 2012, 12:12:12 UTC.

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a>Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob
Arrête l'exécution d'un travail Stream Analytics dans Microsoft Azure de façon asynchrone et libère les ressources qui étaient utilisées. Hello métadonnées et la définition de la tâche reste disponibles au sein de votre abonnement via hello portail Azure et les API de gestion, telles que hello travail peut être modifié et redémarré. Vous ne serez pas facturé pour une tâche dans l’état de hello s’est arrêté.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0 :  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Cette commande PowerShell arrête le travail hello StreamingJob.  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a>Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput
Possibilité de hello de tests de flux de données Analytique tooconnect tooa spécifié d’entrée.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0 :  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Cet état connexion hello de tests de commande PowerShell de hello entrée EntryStream dans StreamingJob.  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a>Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput
Possibilité de hello de tests de flux de données Analytique tooconnect tooa spécifié de sortie.

**Exemple 1**

Azure PowerShell 0.9.8 :  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0 :  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Cet état connexion hello de tests de commande PowerShell de hello output sortie dans StreamingJob.  

## <a name="get-support"></a>Obtenir de l'aide
Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) 

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

