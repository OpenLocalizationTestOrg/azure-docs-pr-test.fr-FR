---
title: aaaLearning du flux de travail PowerShell pour Azure Automation | Documents Microsoft
description: "Cet article est destiné à une rapide leçon auteurs familiarisés avec PowerShell toounderstand hello des différences spécifiques entre PowerShell et PowerShell Workflow et les procédures opérationnelles de concepts tooAutomation applicable."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a>Découvrir les principaux concepts de workflow Windows PowerShell pour les runbooks Automation 
Les Runbooks d'Azure Automation sont implémentés en tant que workflows Windows PowerShell.  Un Workflow Windows PowerShell est semblable tooa de script Windows PowerShell, mais présente des différences importantes qui peuvent être déroutant tooa nouvel utilisateur.  Alors que cet article est prévue toohelp écrire des runbooks à l’aide de flux de travail PowerShell, nous vous recommandons de que écrire des runbooks à l’aide de PowerShell, sauf si vous avez besoin de points de contrôle.  Il existe plusieurs différences de syntaxe pour créer des flux de travail PowerShell runbook et ces différences nécessitent un peu plus travail toowrite efficace des flux de travail.  

Un flux de travail est une séquence d’étapes programmées et connectées qui effectuent des tâches longues ou requièrent une coordination hello de plusieurs étapes sur plusieurs appareils ou nœuds gérés. Hello d’un flux de travail sur un script normal avantages hello permettre toosimultaneously effectuer une action sur plusieurs appareils et hello capacité tooautomatically récupérer après des défaillances. Un workflow Windows PowerShell est un script Windows PowerShell qui utilise Windows Workflow Foundation. Bien que les flux de travail hello sont écrit avec la syntaxe Windows PowerShell et lancé par Windows PowerShell, il est traité par Windows Workflow Foundation.

Pour plus d’informations sur les rubriques hello dans cet article, consultez [prise en main de Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).

## <a name="basic-structure-of-a-workflow"></a>Structure de base d'un workflow
Hello première étape tooconverting un flux de travail PowerShell script tooa PowerShell est plaçant avec hello **Workflow** (mot clé).  Un flux de travail démarre avec hello **Workflow** mot clé suivi des corps hello du script hello entouré accolades. nom de Hello du flux de travail hello suit hello **Workflow** mot clé, comme indiqué dans la syntaxe de hello :

    Workflow Test-Workflow
    {
       <Commands>
    }

nom Hello du flux de travail hello doit correspondre au nom hello de runbook Automation de hello. Si hello runbook est en cours d’importation, nom de fichier hello doit correspondre au nom de flux de travail hello et doit se terminer par *.ps1*.

tooadd paramètres toohello flux de travail, utilisez hello **Param** mot clé comme vous le feriez tooa script.

## <a name="code-changes"></a>Modifications du code
Code de flux de travail PowerShell recherche le code de script tooPowerShell presque identique à l’exception de quelques modifications importantes.  Hello les sections suivantes décrire les modifications que vous avez besoin toomake tooa PowerShell script pour qu’il toorun dans un flux de travail.

### <a name="activities"></a>Activités
Une activité est une tâche spécifique dans un workflow. Tout comme un script se compose d'une ou de plusieurs commandes, un workflow se compose d'une ou de plusieurs activités exécutées en séquence. Flux de travail Windows PowerShell convertit automatiquement la plupart de hello tooactivities d’applets de commande Windows PowerShell lors de l’exécution d’un flux de travail. Lorsque vous spécifiez une de ces applets de commande dans votre runbook, activité correspondante hello est exécutée par Windows Workflow Foundation. Pour ces applets de commande sans activité correspondante, Windows PowerShell Workflow exécute automatiquement l’applet de commande hello dans un [InlineScript](#inlinescript) activité. Il existe un ensemble d'applets de commande qui sont exclues et ne peuvent pas être utilisées dans un workflow, à moins que vous ne les incluiez explicitement dans un bloc InlineScript. Pour plus d'informations sur ces concepts, consultez [Utilisation des activités dans les workflows de script](http://technet.microsoft.com/library/jj574194.aspx).

Activités de flux de travail partagent un ensemble de tooconfigure de paramètres courants de leur fonctionnement. Pour plus d’informations sur les paramètres communs de workflow hello, consultez [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="positional-parameters"></a>Paramètres positionnels
Vous ne pouvez pas utiliser les paramètres positionnels avec les activités et les applets de commande dans un workflow.  Cela signifie que vous devez utiliser des noms de paramètres.

Par exemple, considérez hello suivant de code qui obtient tous les services en cours d’exécution.

     Get-Service | Where-Object {$_.Status -eq "Running"}

Si vous essayez toorun ce même code dans un flux de travail, vous recevez un message comme « Paramètre ensemble ne peut pas être résolu à l’aide de hello spécifié des paramètres nommés. »  toocorrect, nom de paramètre hello comme dans les éléments suivants de hello.

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a>Objets désérialisés
Dans les workflows, les objets sont désérialisés.  Cela signifie que leurs propriétés restent disponibles, mais pas leurs méthodes.  Par exemple, considérez hello suivant de code PowerShell qui arrête un service à l’aide de la méthode Stop de hello hello d’objet de Service.

    $Service = Get-Service -Name MyService
    $Service.Stop()

Si vous essayez toorun dans un flux de travail, vous recevez une erreur indiquant que « l’appel de méthode n'est pas prise en charge dans un Workflow Windows PowerShell. »  

Une option consiste à toowrap ces deux lignes de code dans un [InlineScript](#inlinescript) bloquer dans quels cas $Service serait un objet de service au sein du bloc de hello.

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

Une autre option consiste à toouse une autre applet de commande qui exécute hello les mêmes fonctionnalités que la méthode hello, si celle-ci est disponible.  Dans notre exemple, hello Stop-Service fournit hello même fonctionnalité que la méthode Stop de hello et que vous pouvez utiliser suivant de hello pour un flux de travail.

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a>InlineScript
Hello **InlineScript** activité est utile lorsque vous devez toorun une ou plusieurs commandes en tant que script PowerShell traditionnel au lieu de flux de travail PowerShell.  Alors que les commandes dans un flux de travail sont envoyées tooWindows Workflow Foundation pour le traitement, les commandes dans un bloc InlineScript sont traitées par Windows PowerShell.

InlineScript utilise hello selon la syntaxe ci-dessous.

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

Vous pouvez retourner la sortie à partir d’un InlineScript en affectant hello sortie tooa variable. Bonjour exemple suivant arrête un service et génère ensuite le nom du service hello.

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


Vous pouvez passer des valeurs dans un bloc InlineScript, mais vous devez utiliser le modificateur de portée **$Using** .  Hello suivant est identique toohello précédent exemple, sauf que le nom de service hello est fourni par une variable.

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


InlineScript activités peuvent être essentielles pour certains flux de travail, ils ne prennent pas en charge les constructions de flux de travail et doivent être utilisés uniquement lorsque cela est nécessaire pour hello suivant raisons :

* Vous ne pouvez pas utiliser de [points de contrôle](#checkpoints) à l’intérieur d’un bloc InlineScript. Si une défaillance se produit dans le bloc de hello, il doit être reprise à partir du début de hello du bloc de hello.
* Vous ne pouvez pas effectuer [d’exécution en parallèle](#parallel-processing) à l’intérieur d’un bloc InlineScriptBlock.
* InlineScript affecte l’évolutivité des flux de travail hello puisqu’elle maintient la session Windows PowerShell de hello pour hello toute longueur du bloc InlineScript de hello.

Pour plus d’informations sur l’utilisation d’InlineScript, consultez [Exécution des commandes Windows PowerShell dans un workflow](http://technet.microsoft.com/library/jj574197.aspx) et [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).

## <a name="parallel-processing"></a>Traitement en parallèle
Un avantage de flux de travail Windows PowerShell est hello capacité tooperform un ensemble de commandes en parallèle à la place de séquentielle comme avec un script typique.

Vous pouvez utiliser hello **parallèles** mot clé toocreate un bloc de script avec plusieurs commandes qui s’exécutent simultanément. Cette méthode utilise hello selon la syntaxe ci-dessous. Dans ce cas, Activity1 et Activity2 démarre à hello même temps. Activity3 démarre uniquement quand Activity1 et Activity2 sont toutes deux terminées.

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


Par exemple, considérez hello suivant les commandes PowerShell qui copie plusieurs fichiers destination réseau tooa.  Ces commandes sont exécutées de manière séquentielle afin qu’un fichier doit se terminer copie avant hello est redémarrée.     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

Hello suivant du flux de travail exécute ces mêmes commandes en parallèle afin que tous les démarrer la copie à hello même temps.  Uniquement une fois qu’ils sont tous copiés message d’achèvement hello apparaît.

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


Vous pouvez utiliser hello **ForEach-Parallel** construire des commandes tooprocess pour chaque élément dans une collection simultanément. éléments Hello dans la collection de hello sont traités en parallèle pendant l’exécutent des commandes hello dans le bloc de script hello séquentiellement. Cette méthode utilise hello selon la syntaxe ci-dessous. Dans ce cas, Activity1 commence hello la même heure pour tous les éléments de collection de hello. Pour chaque élément, Activity2 démarre une fois Activity1 terminée. Activity3 démarre uniquement quand Activity1 et Activity2 sont toutes deux terminées pour tous les éléments.

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

Bonjour à l’exemple suivant est similaire exemple précédent toohello copie des fichiers en parallèle.  Dans ce cas, un message s'affiche pour chaque fichier après la copie.  Uniquement une fois qu’ils sont tous complètement copié message d’achèvement finale hello apparaît.

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> Nous vous déconseillons d’exécution des runbooks enfants en parallèle, car il a été prouvé toogive produisent des résultats incertains.  Hello sortie du runbook parfois de hello enfant ne s’affiche pas, et peuvent affecter les paramètres dans un seul enfant runbook hello autres procédures opérationnelles enfant parallèle
>

## <a name="checkpoints"></a>Points de contrôle
A *point de contrôle* est un instantané de l’état actuel de hello du flux de travail hello qui inclut la valeur actuelle de hello pour les variables et toute sortie est généré toothat point. Si un flux de travail se termine par erreur ou est interrompu, puis hello prochaine exécution qu’il démarre à partir de son dernier point de contrôle au lieu de démarrer hello de travail de sous-découpage hello.  Vous pouvez définir un point de contrôle dans un flux de travail avec hello **Checkpoint-Workflow** activité.

Bonjour suivant l’exemple de code, une exception se produit après Activity2 à l’origine hello tooend de flux de travail. Flux de travail hello est exécuté à nouveau, il commence par exécuter Activity2 puisqu’il s’agissait juste après que le dernier point de contrôle hello définie.

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

Vous devez définir des points de contrôle dans un flux de travail une fois que les activités qui peuvent être sujette tooexception et ne doivent pas être répété si le flux de travail hello reprend. Par exemple, votre workflow peut créer une machine virtuelle. Vous pouvez définir un point de contrôle avant et après l’ordinateur virtuel de hello commandes toocreate hello. En cas de création de hello, commandes hello sont répétés si le flux de travail hello est démarrée à nouveau. Si le travail de sous-découpage hello échoue après que la création d’hello réussit, puis hello ordinateur virtuel ne sera pas créé à nouveau lors de la reprise du workflow hello.

Bonjour à l’exemple suivant copie plusieurs fichiers tooa du réseau et définit un point de contrôle après chaque fichier.  Si l’emplacement de réseau hello est perdu, les flux de travail hello se termine par erreur.  Lorsqu’il est démarré à nouveau, il reprend au dernier point de contrôle hello ce qui signifie que que seuls les fichiers hello qui ont déjà été copiés sont ignorés.

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

Étant donné que les informations d’identification de nom d’utilisateur ne sont pas conservées après avoir appelé hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activité ou après hello dernier point de contrôle, vous devez toonull d’informations d’identification tooset hello, puis les extraire à nouveau hello asset magasin après  **Suspend-Workflow** ou point de contrôle est appelée.  Dans le cas contraire, hello message d’erreur suivant peut s’afficher : *ne peut pas reprendre la tâche de flux de travail de hello, soit parce que les données de persistance est complètement enregistrées, ou enregistrées les données de persistance a été endommagées. Vous devez redémarrer le flux de travail hello.*

Hello suivant le même code montre comment toohandle cela dans vos runbook PowerShell Workflow.

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


Cette procédure n’est pas nécessaire si vous vous authentifiez à l’aide d’un compte d’identification configuré avec un service principal.  

Pour plus d’informations sur les points de contrôle, consultez [tooa d’ajouter des points de contrôle du Workflow de Script](http://technet.microsoft.com/library/jj574114.aspx).

## <a name="next-steps"></a>Étapes suivantes
* tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md)
