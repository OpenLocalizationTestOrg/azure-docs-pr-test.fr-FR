---
title: aaaStarting un runbook dans Azure Automation | Documents Microsoft
description: "Résume hello différentes méthodes qui peuvent être utilisé toostart un runbook dans Azure Automation et fournit des détails sur l’utilisation des deux hello portail Azure et Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a>Démarrage d'un Runbook dans Azure Automation
Hello tableau suivant vous aidera à déterminer hello méthode toostart un runbook dans Azure Automation qui est le scénario tooyour plus approprié. Cet article contient des informations sur le démarrage d’un runbook avec hello portail Azure et Windows PowerShell. Détails sur hello autres méthodes sont fournies dans les autres documentations auquel vous pouvez accéder à partir de liens hello ci-dessous.

| **MÉTHODE** | **CARACTÉRISTIQUES** |
| --- | --- |
| [Portail Azure](#starting-a-runbook-with-the-azure-portal) |<li>Méthode la plus simple avec une interface utilisateur interactive.<br> <li>Valeurs de paramètre simple formulaire tooprovide.<br> <li>Suivi aisé de l'état des tâches.<br> <li>Accès authentifié avec ouverture de session Azure. |
| [Windows PowerShell](https://msdn.microsoft.com/library/dn690259.aspx) |<li>Appel à partir de la ligne de commande avec les applets de commande Windows PowerShell.<br> <li>Possibilité d'inclusion dans une solution automatisée à plusieurs étapes.<br> <li>Demande authentifiée avec un certificat ou un principal du service / principal d'utilisateur OAuth.<br> <li>Fourniture de valeurs de paramètres simples et complexes.<br> <li>Suivi de l’état des tâches.<br> <li>Client requis toosupport applets de commande PowerShell. |
| [API Azure Automation](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li>Méthode la plus souple, mais également la plus complexe.<br> <li>Appel à partir de n'importe quel code personnalisé qui peut envoyer des requêtes HTTP.<br> <li>Requête authentifiée avec un certificat ou un principal du service / principal d'utilisateur Oauth.<br> <li>Fourniture de valeurs de paramètres simples et complexes.<br> <li>Suivi de l’état des tâches. |
| [Webhooks](automation-webhooks.md) |<li>Démarrage d'un Runbook à partir d'une simple requête HTTP.<br> <li>Authentification avec un jeton de sécurité dans l'URL.<br> <li>Le client ne peut pas remplacer les valeurs de paramètre spécifiées lors de la création du Webhook. Runbook peut définir un paramètre unique qui est rempli avec les détails de la demande HTTP hello.<br> <li>Aucun état de tâche tootrack possibilité via l’URL du webhook. |
| [Répondre tooAzure alerte](../log-analytics/log-analytics-alerts.md) |<li>Démarrer un runbook dans l’alerte tooAzure de réponse.<br> <li>Configurer le webhook pour le runbook et lier les tooalert.<br> <li>Authentification avec un jeton de sécurité dans l'URL. |
| [Planification](automation-schedules.md) |<li>Démarrage automatique du runbook selon une planification horaire, quotidienne, hebdomadaire ou mensuelle.<br> <li>Manipulation de la planification via le portail Azure, les applets de commande PowerShell ou les API Azure.<br> <li>Fournir toobe de valeurs de paramètre utilisée avec une planification. |
| [À partir d'un autre Runbook](automation-child-runbooks.md) |<li>Utilisation d’un Runbook en tant qu’activité d’un autre Runbook.<br> <li>Utile pour les fonctionnalités utilisées par plusieurs Runbooks.<br> <li>Fournir des runbook de toochild de valeurs de paramètre et utiliser la sortie dans le runbook parent. |

Hello image suivante illustre les processus pas à pas détaillé hello cycle de vie d’un runbook. Il inclut les différentes façons qu'un runbook est démarré dans Azure Automation, les composants requis pour les runbooks d’Azure Automation Runbook Worker hybride tooexecute et les interactions entre les différents composants. toolearn sur l’exécution des runbooks Automation dans votre centre de données, consultez trop[workers hybrides](automation-hybrid-runbook-worker.md)

![Architecture de runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a>Démarrage d’un runbook avec hello portail Azure
1. Bonjour portail Azure, sélectionnez **Automation** , puis cliquez sur nom hello d’un compte automation.
2. Dans le menu du Hub hello, sélectionnez **Runbooks**.
3. Sur hello **Runbooks** panneau, sélectionnez un runbook, puis cliquez sur **Démarrer**.
4. Si hello runbook possède des paramètres, vous serez valeurs tooprovide demandée avec une zone de texte pour chaque paramètre. Pour plus d'informations sur les paramètres, consultez [Paramètres du Runbook](#Runbook-parameters) ci-dessous.
5. Sur hello **travail** panneau, vous pouvez afficher le statut de hello de tâche du runbook hello.

## <a name="starting-a-runbook-with-windows-powershell"></a>Démarrage d'un Runbook avec Windows PowerShell
Vous pouvez utiliser hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook avec Windows PowerShell. Hello exemple de code suivant démarre un runbook appelé Test-Runbook.

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

Retourne AzureRmAutomationRunbook de démarrer un travail de l’objet que vous pouvez utiliser tootrack son état une fois hello runbook est démarré. Vous pouvez ensuite utiliser cet objet de tâche avec [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) état de hello toodetermine du travail de hello et [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget sa sortie. Hello suivant l’exemple de code démarre un runbook appelé Test-Runbook, attend qu’il ait terminé, puis affiche sa sortie.

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

Si hello runbook nécessite des paramètres, vous devez lui fournir en tant qu’un [hashtable](http://technet.microsoft.com/library/hh847780.aspx) où la clé hello de table de hachage hello correspond au nom du paramètre hello et la valeur de hello est la valeur du paramètre hello. Hello suivant montre comment toostart un runbook avec deux paramètres de chaîne nommés FirstName et LastName, un entier nommé RepeatCount et un paramètre booléen nommé Show. Pour plus d'informations sur les paramètres, consultez [Paramètres du Runbook](#Runbook-parameters) .

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a>Paramètres du Runbook
Lorsque vous démarrez un runbook à partir de hello portail Azure ou Windows PowerShell, instruction de hello est envoyée via hello service web Azure Automation. Ce service ne prend pas en charge les paramètres avec des types de données complexes. Si vous avez besoin de tooprovide une valeur pour un paramètre complexe, vous devez l’appeler en ligne à partir d’un autre runbook comme décrit dans [runbooks enfants dans Azure Automation](automation-child-runbooks.md).

Hello service web Azure Automation fournit des fonctionnalités spéciales pour les paramètres utilisant certains types de données, comme décrit dans les sections suivantes de hello.

### <a name="named-values"></a>Valeurs nommées
Si le paramètre hello est un type de données [object], puis vous pouvez utiliser hello suivant toosend du format JSON il une liste de valeurs nommées : *{nom1 : 'Valeur1', nom2 : 'Value2', Nom3 : 'Valeur3'}*. Ces valeurs doivent avoir des types simples. Hello runbook reçoit paramètre hello comme un [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) avec des propriétés qui correspondent tooeach valeur nommée.

Envisagez de hello suivant runbook de test qui accepte un paramètre utilisateur.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

Hello texte suivant peut être utilisé pour le paramètre de l’utilisateur hello.

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

Cela entraîne hello suivant de sortie.

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a>Tableaux
Si le paramètre hello est un tableau tel que [array] ou [string []], vous pouvez ensuite utiliser hello suivant toosend du format JSON une liste de valeurs : *[valeur1, valeur2, valeur3]*. Ces valeurs doivent avoir des types simples.

Envisagez de hello suivant runbook de test qui accepte un paramètre appelé *utilisateur*.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

Hello texte suivant peut être utilisé pour le paramètre de l’utilisateur hello.

```
["Joe","Smith",2,true]
```

Cela entraîne hello suivant de sortie.

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a>Informations d'identification
Si le paramètre hello est le type de données **PSCredential**, vous pouvez fournir le nom hello d’une automatisation Azure [actif d’informations d’identification](automation-credentials.md). Hello runbook récupère des informations d’identification hello nom hello que vous spécifiez.

Envisagez de hello suivant runbook de test qui accepte un paramètre appelé des informations d’identification.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

Hello texte suivant peut être utilisé pour le paramètre de l’utilisateur hello en supposant qu’il existe une ressource d’informations d’identification appelée *My Credential*.

```
My Credential
```

En supposant que le nom d’utilisateur hello dans informations d’identification hello a été *jsmith*, cela entraîne hello suivant de sortie.

```
jsmith
```

## <a name="next-steps"></a>Étapes suivantes
* architecture de runbook Hello dans l’article en cours fournit une vue d’ensemble de la gestion des ressources de runbook dans Azure et locales avec hello Runbook Worker hybride.  toolearn sur l’exécution des runbooks Automation dans votre centre de données, consultez trop[Workers hybrides](automation-hybrid-runbook-worker.md).
* toolearn en savoir plus sur hello création toobe runbooks modulaire utilisé par d’autres runbooks pour les fonctions spécifiques ou courants, consultez trop[Runbooks enfants](automation-child-runbooks.md).

