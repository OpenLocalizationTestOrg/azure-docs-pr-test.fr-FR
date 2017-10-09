---
title: aaaRunbook sortie et les Messages dans Azure Automation | Documents Microsoft
description: "Décrit comment les messages toocreate et récupérer la sortie et erreur provenant de runbooks dans Azure Automation."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 13a414f5-0e2c-4be2-9558-a3e3ec84b6b2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: magoedte;bwren
ms.openlocfilehash: c1505fa889473766bfa47e43aaed2449d60ad851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-output-and-messages-in-azure-automation"></a>Sortie et messages de Runbook dans Azure Automation
La plupart des runbooks Azure Automation ont une forme de sortie telle qu’un utilisateur de toohello message erreur ou un objet complexe destiné toobe consommée par un autre workflow. Windows PowerShell fournit [plusieurs flux](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) sortie toosend à partir d’un script ou un flux de travail. Azure Automation fonctionnant avec chacun de ces flux différemment, et vous devez suivre les meilleures pratiques pour le toouse chaque lorsque vous créez un runbook.

Hello tableau suivant fournit une brève description de chacun des flux de données hello et leur comportement dans le portail de gestion de hello lorsqu’un runbook publié en cours d’exécution et [test d’un runbook](automation-testing-runbook.md). Pour plus de détails sur chaque flux, reportez-vous aux sections suivantes.

| Stream | Description | Publié | Test |
|:--- |:--- |:--- |:--- |
| Sortie |Objets destinés toobe consommé par d’autres runbooks. |Historique des travaux toohello écrite. |Affiché dans le volet sortie de Test de hello. |
| Avertissement |Message d’avertissement destiné à hello utilisateur. |Historique des travaux toohello écrite. |Affiché dans le volet sortie de Test de hello. |
| Error |Message d’erreur destiné à hello utilisateur. Contrairement à une exception, hello runbook se poursuit après un message d’erreur par défaut. |Historique des travaux toohello écrite. |Affiché dans le volet sortie de Test de hello. |
| Détaillé |Messages fournissant des informations générales ou de débogage. |Écrit l’historique toojob uniquement si la journalisation documentée est activée pour les runbook hello. |Affiché dans le volet de sortie de Test hello uniquement si $VerbosePreference a la valeur tooContinue dans les runbook hello. |
| Progression |Enregistrements générés automatiquement avant et après chaque activité du runbook de hello. Hello runbook ne doit pas tenter toocreate ses propres informations de progression dans la mesure où ils sont destinés à un utilisateur interactif. |Écrit l’historique toojob uniquement si la journalisation de progression est activée pour hello runbook. |Non affiché dans hello volet sortie de Test. |
| Déboguer |Messages destinés à un utilisateur interactif. Utilisation proscrite dans les Runbooks. |Non écrit toojob historique. |Non écrit tooTest volet de sortie. |

## <a name="output-stream"></a>Flux de sortie
flux de sortie Hello est prévu pour la sortie des objets créés par un script ou un flux de travail quand il s’exécute correctement. Dans Azure Automation, ce flux est principalement utilisé pour toobe objets destinés consommée par [runbooks parents qui appellent le runbook en cours hello](automation-child-runbooks.md). Lorsque vous [appeler un runbook inline](automation-child-runbooks.md#invoking-a-child-runbook-using-inline-execution) à partir d’un runbook parent, il retourne des données à partir du parent de toohello de flux de sortie hello. Vous devez uniquement utiliser hello sortie flux toocommunicate général informations toohello précédent de l’utilisateur si vous connaissez hello runbook ne sera jamais être appelé par un autre runbook. Comme meilleure pratique, cependant, vous devez généralement utiliser hello [flux détaillé](#Verbose) utilisateur de toohello toocommunicate des informations générales.

Vous pouvez écrire le flux de données de sortie de toohello avec [Write-Output](http://technet.microsoft.com/library/hh849921.aspx) ou en plaçant l’objet de hello sur sa propre ligne dans les runbook hello.

    #hello following lines both write an object toohello output stream.
    Write-Output –InputObject $object
    $object

### <a name="output-from-a-function"></a>Sortie à partir d’une fonction
Lorsque vous écrivez le flux de sortie toohello dans une fonction qui est incluse dans votre runbook, sortie de hello est passé toohello précédent runbook. Si hello runbook affecte cette variable tooa de sortie, il est écrit pas toohello le flux de sortie. L’écriture d’autres flux à partir de fonction hello tooany écrira toohello le flux correspondant pour hello runbook.

Envisagez de hello suivant l’exemple de runbook.

    Workflow Test-Runbook
    {
        Write-Verbose "Verbose outside of function" -Verbose
        Write-Output "Output outside of function"
        $functionOutput = Test-Function
        $functionOutput

    Function Test-Function
     {
        Write-Verbose "Verbose inside of function" -Verbose
        Write-Output "Output inside of function"
      }
    }


flux de sortie de Hello pour la tâche du runbook hello serait :

    Output inside of function
    Output outside of function

flux détaillé de Hello pour la tâche du runbook hello serait :

    Verbose outside of function
    Verbose inside of function

Une fois que vous avez publié le runbook de hello et avant de le démarrer, vous devez également activer la journalisation dans les paramètres de runbook hello Bonjour tooget de commande Verbose diffuser la sortie détaillée.

### <a name="declaring-output-data-type"></a>Déclaration du type de données de sortie
Un flux de travail peut spécifier le type de données de hello de sa sortie à l’aide de hello [attribut OutputType](http://technet.microsoft.com/library/hh847785.aspx). Cet attribut n’a aucun effet lors de l’exécution, mais il fournit un auteur de runbook indication toohello au moment du design de sortie hello attendue du runbook de hello. Au fil de l’ensemble d’outils hello pour les runbooks tooevolve, hello de déclaration des types de données de sortie au moment du design est de plus en plus importante. Par conséquent, il est constitue une pratique recommandée tooinclude cette déclaration dans les runbooks que vous créez.

Voici une liste d’exemples de types de sortie :

* System.String
* System.Int32
* System.Collections.Hashtable
* Microsoft.Azure.Commands.Compute.Models.PSVirtualMachine

Bonjour exemple de runbook suivant génère un objet string et inclut une déclaration de son type de sortie. Si votre runbook génère un tableau d’un certain type, vous devez toujours spécifier hello type en tant que tableau tooan opposés du type de hello.

    Workflow Test-Runbook
    {
       [OutputType([string])]

       $output = "This is some string output."
       Write-Output $output
    }

toodeclare une sortie de type dans les runbooks Grapical ou flux de travail PowerShell graphique, vous pouvez sélectionner hello **d’entrée et sortie** option de menu et tapez le nom de hello Hello de type de sortie.  Nous vous recommandons d’utiliser toomake .NET complet du nom de classe hello il facilement identifiable quand vous le référencez à partir d’un runbook parent.  Cela expose toutes les propriétés de hello de ce bus de données de classe toohello dans les runbook hello et fournit une grande flexibilité lors de leur utilisation pour la logique conditionnelle, journalisation et de référence en tant que valeurs pour d’autres activités dans les runbook hello.<br> ![Option Entrée et sortie de Runbook](media/automation-runbook-output-and-messages/runbook-menu-input-and-output-option.png)

Bonjour l’exemple suivant, nous avons deux runbooks graphiques toodemonstrate cette fonctionnalité.  Si nous appliquer le modèle de conception de runbook modulaire hello, nous avons un runbook qui sert de hello *modèle d’authentification Runbook* gestion de l’authentification avec Azure à l’aide de hello compte d’identification.  Notre deuxième runbook, qui est généralement assurée hello core logique tooautomate un scénario donné va dans ce cas tooexecute hello *modèle d’authentification Runbook* et afficher hello résultats tooyour **Test** volet de sortie.  Dans des circonstances normales, nous devons ce runbook faire quelque chose par rapport à une sortie hello en tirant parti de ressources du runbook enfant de hello.    

Voici logique de base hello Hello **AuthenticateTo-Azure** runbook.<br> ![Exemple de modèle Runbook d’authentification](media/automation-runbook-output-and-messages/runbook-authentication-template.png).  

Il inclut le type de sortie hello *Microsoft.Azure.Commands.Profile.Models.PSAzureContext*, qui retournera des propriétés de profil d’authentification hello.<br> ![Exemple de type de sortie Runbook](media/automation-runbook-output-and-messages/runbook-input-and-output-add-blade.png) 

Ce runbook est très simple, mais il existe un toocall d’élément de configuration déconnecter ici.  la dernière activité Hello exécute hello **Write-Output** applet de commande et les écritures de données tooa $_ variable du profil à l’aide d’une expression PowerShell pour hello hello **Inputobject** paramètre, qui est requis pour qui applet de commande.  

Hello runbook deuxième dans cet exemple, nommé *Test-ChildOutputType*, nous avons simplement deux activités.<br> ![Exemple de type de sortie enfant Runbook](media/automation-runbook-output-and-messages/runbook-display-authentication-results-example.png) 

la première activité Hello appelle hello **AuthenticateTo-Azure** runbook et hello deuxième activité est en cours d’exécution hello **Write-Verbose** applet de commande avec hello **source de données** de  **Sortie d’activité** et la valeur hello pour **chemin d’accès du champ** est **Context.Subscription.SubscriptionName**, qui spécifie la sortie contexte hello hello  **Azure-AuthenticateTo** runbook.<br> ![Source de données du paramètre d’applet de commande Write-Verbose](media/automation-runbook-output-and-messages/runbook-write-verbose-parameters-config.png)    

résultat de Hello est nom hello d’abonnement de hello.<br> ![Résultats du Runbook Test-ChildOutputType](media/automation-runbook-output-and-messages/runbook-test-childoutputtype-results.png)

Une remarque sur le comportement de hello Hello contrôle de Type de sortie.  Lorsque vous tapez une valeur dans le champ Type de sortie hello hello d’entrée et le panneau des propriétés de sortie, vous avez tooclick en dehors du contrôle de hello après avoir tapé, afin que votre toobe entrée reconnu par le contrôle de hello.  

## <a name="message-streams"></a>Flux de messages
Contrairement au flux de sortie hello, flux de messages sont prévues toocommunicate informations toohello de l’utilisateur. Il existe plusieurs flux de messages pour les différents types d’informations, et chacun d’eux est traité différemment par Azure Automation.

### <a name="warning-and-error-streams"></a>Flux d’erreurs et d’avertissements
flux d’erreur et d’avertissement Hello sont toolog prévue des problèmes qui se produisent dans un runbook. Ils sont écrits toohello l’historique des travaux quand un runbook est exécuté et sont incluses dans hello volet sortie de Test dans le portail de gestion de hello lorsqu’un runbook est testé. Par défaut, hello runbook continue à s’exécuter après un avertissement ou une erreur. Vous pouvez spécifier ce runbook hello doit être suspendu sur un avertissement ou une erreur en définissant un [variable de préférence](#PreferenceVariables) dans runbook hello avant de créer le message de type hello. Par exemple, toocause un toosuspend de runbook en cas d’erreur comme il le ferait une exception, définissez **$ErrorActionPreference** tooStop.

Créer un message d’avertissement ou d’erreur à l’aide de hello [Write-Warning](https://technet.microsoft.com/library/hh849931.aspx) ou [Write-Error](http://technet.microsoft.com/library/hh849962.aspx) applet de commande. Les activités peuvent également écrire des flux de données toothese.

    #hello following lines create a warning message and then an error message that will suspend hello runbook.

    $ErrorActionPreference = "Stop"
    Write-Warning –Message "This is a warning message."
    Write-Error –Message "This is an error message that will stop hello runbook because of hello preference variable."

### <a name="verbose-stream"></a>flux des commentaires
flux de message détaillé Hello est pour des informations générales sur le fonctionnement du runbook hello. Depuis hello [flux de débogage](#Debug) n’est pas disponible dans un runbook, les messages détaillés doivent être utilisés pour les informations de débogage. Par défaut, les messages détaillés provenant de runbooks publiés ne sont pas stockées dans l’historique des travaux hello. toostore les messages détaillés, configurez les runbooks publiés tooLog les enregistrements détaillés sur l’onglet configurer de hello du runbook hello Bonjour portail de gestion Azure. Dans la plupart des cas, vous devez conserver le paramètre par défaut de hello de ne pas journaliser les enregistrements détaillés d’un runbook pour des raisons de performances. Activer cette tootroubleshoot seule option ou déboguer un runbook.

Lorsque [test d’un runbook](automation-testing-runbook.md), les messages détaillés ne s’affichent pas même si hello runbook est configuré toolog les enregistrements détaillés. les messages détaillés toodisplay lors de la [test d’un runbook](automation-testing-runbook.md), vous devez définir les tooContinue variable hello $VerbosePreference. Cette variable définie, les messages détaillés seront affichera dans hello volet de résultats des tests de hello portail Azure.

Créer un message détaillé à l’aide de hello [Write-Verbose](http://technet.microsoft.com/library/hh849951.aspx) applet de commande.

    #hello following line creates a verbose message.

    Write-Verbose –Message "This is a verbose message."

### <a name="debug-stream"></a>flux de débogage
flux de débogage Hello est destiné à un utilisateur interactif et ne doit pas être utilisé dans les runbooks.

## <a name="progress-records"></a>Informations de progression
Si vous configurez une progression de toolog runbook enregistre (sur l’onglet configurer de hello du runbook hello Bonjour portail Azure), puis un enregistrement écrit toohello l’historique des travaux avant et après l’exécution de chaque activité. Dans la plupart des cas, vous devez conserver le paramètre par défaut de hello de ne pas journaliser les enregistrements de progression d’un runbook des performances de toomaximize de commande. Activer cette tootroubleshoot seule option ou déboguer un runbook. Lorsque vous testez un runbook, les messages de progression ne s’affichent pas même si hello runbook est configuré toolog de progression.

Hello [Write-Progress](http://technet.microsoft.com/library/hh849902.aspx) applet de commande n’est pas valide dans un runbook, car elle est destinée à un utilisateur interactif.

## <a name="preference-variables"></a>Variables de préférence
Windows PowerShell utilise [variables de préférence](http://technet.microsoft.com/library/hh847796.aspx) toodetermine comment toorespond toodata envoyé toodifferent flux de sortie. Vous pouvez définir ces variables dans un toocontrol runbook mode de réponse toodata envoyées aux différents flux.

Hello tableau suivant répertorie les variables de préférence hello qui peuvent être utilisés dans les runbooks avec leurs valide et les valeurs par défaut. Notez que ce tableau inclut uniquement les valeurs hello qui sont valides dans un runbook. Les valeurs supplémentaires sont valides pour les variables de préférence hello lorsqu’il est utilisé dans Windows PowerShell en dehors d’Azure Automation.

| Variable | Valeur par défaut | Valeurs valides |
|:--- |:--- |:--- |
| WarningPreference |Continue |Stop<br>Continue<br>SilentlyContinue |
| ErrorActionPreference |Continue |Stop<br>Continue<br>SilentlyContinue |
| VerbosePreference |SilentlyContinue |Stop<br>Continue<br>SilentlyContinue |

Hello tableau suivant répertorie le comportement hello pour hello préférence valeurs des variables qui sont valides dans les runbooks.

| Valeur | Comportement |
|:--- |:--- |
| Continue |Enregistre le message de type hello et poursuit l’exécution de runbook de hello. |
| SilentlyContinue |Poursuit l’exécution hello runbook sans journaliser le message de type hello. Cela influe hello d’ignorer le message de type hello. |
| Arrêter |Enregistre le message de type hello et interrompt hello runbook. |

## <a name="retrieving-runbook-output-and-messages"></a>Récupération de la sortie et des messages de Runbook
### <a name="azure-portal"></a>Portail Azure
Vous pouvez afficher les détails de hello d’un travail de runbook Bonjour portail Azure à partir de l’onglet tâches de hello d’un runbook. Affiche les paramètres d’entrée hello et hello Hello résumé du travail de hello [le flux de sortie](#Output) dans toogeneral plus d’informations sur la tâche de hello et toutes les exceptions si elles se sont produites. Hello historique inclura des messages à partir de hello [le flux de sortie](#Output) et [Warning and Error Streams](#WarningError) dans Ajout toohello [flux détaillé](#Verbose) et [progression Enregistrements](#Progress) si hello runbook est configuré toolog détaillée et des informations de progression.

### <a name="windows-powershell"></a>Windows PowerShell
Dans Windows PowerShell, vous pouvez récupérer la sortie et les messages à partir d’un runbook à l’aide de hello [Get-AzureAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) applet de commande. Cette applet de commande requiert hello ID de tâche de hello et a un paramètre appelé flux où vous spécifiez le tooreturn de flux de données. Vous pouvez spécifier n’importe quel tooreturn tous les flux de travail de hello.

Bonjour à l’exemple suivant démarre un exemple de runbook, puis attend qu’il toocomplete. Une fois terminé, son flux de sortie est collectée à partir de la tâche de hello.

    $job = Start-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook"

    $doLoop = $true
    While ($doLoop) {
       $job = Get-AzureRmAutomationJob -ResourceGroupName "ResourceGroup01" `
       –AutomationAccountName "MyAutomationAccount" -Id $job.JobId
       $status = $job.Status
       $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
    }

    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" -Id $job.JobId –Stream Output

### <a name="graphical-authoring"></a>Création graphique
Pour les runbooks graphiques, journalisation supplémentaire est disponible sous forme de hello de traçage au niveau de l’activité.  Il existe deux niveaux de suivi : de base et détaillé.  Dans le suivi de base, vous pouvez voir hello démarrer et heure de fin de chaque activité de runbook de hello ainsi que des informations liées tooany de tentatives d’activité, tels que le nombre de tentatives et l’heure de début de l’activité hello.  Dans le suivi détaillé, vous obtenez le suivi de base, ainsi que des données d’entrée et de sortie pour chaque activité.  Notez qu’actuellement les enregistrements de trace hello sont écrits à l’aide de flux détaillé de hello, ainsi, vous devez activer la journalisation détaillée lorsque vous activez le traçage.  Pour les runbooks graphiques avec le suivi activé il est inutile de progression toolog, étant donné que sert de suivi de base hello hello même objectif et des informations plus détaillées.

![Vue du flux de travail de création graphique](media/automation-runbook-output-and-messages/job-streams-view-blade.png)

Vous pouvez voir que lorsque vous activez la journalisation et le suivi pour les runbooks graphiques de commentaires, beaucoup plus d’informations est disponible en production hello que permet d’afficher les flux de travail à partir de hello ci-dessus capture d’écran.  Ces informations supplémentaires peuvent être essentielles pour résoudre les problèmes de production pour un runbook. Il est donc conseillé de l’activer uniquement à cet effet et pas de manière générale.    
les enregistrements de Trace Hello peuvent être particulièrement nombreux.  Avec runbook graphique le traçage vous pouvez obtenir deux enregistrements toofour par activité selon que vous avez configuré le suivi de base ou détaillé.  Si vous ne devez progression hello informations tootrack d’un runbook pour la résolution des problèmes, vous pourriez tookeep que le suivi est désactivé.

**tooenable au niveau de l’activité de suivi, effectuer hello comme suit.**

1. Bonjour portail Azure, ouvrez votre compte Automation.
2. Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.
3. Dans Panneau de procédures opérationnelles hello, cliquez sur tooselect un runbook graphique à partir de votre liste de runbooks.
4. Dans Panneau de paramètres hello pour les runbook hello sélectionné, cliquez sur **Logging and Tracing**.
5. Hello journalisation et le suivi du panneau, sous journaliser les enregistrements détaillés, en cliquant sur **sur** tooenable la journalisation documentée et udner au niveau de l’activité de suivi, niveau de trace hello également modifier**base** ou **détaillé**  selon le niveau de hello du suivi, vous avez besoin.<br>
   
   ![Panneau Journalisation et suivi de la création graphique](media/automation-runbook-output-and-messages/logging-and-tracing-settings-blade.png)

### <a name="microsoft-operations-management-suite-oms-log-analytics"></a>Microsoft Operations Management Suite (OMS) Log Analytics
Automation peut envoyer des runbook travail état et la tâche de flux de données tooyour Analytique de journal de Microsoft Operations Management Suite (OMS) espace de travail.  Avec Log Analytics, vous pouvez :

* Obtenir des informations sur vos travaux Automation 
* Déclencher un e-mail ou une alerte basé(e) sur le statut de votre tâche de runbook (par exemple, échec ou état suspendu) 
* Écrire des requêtes avancées sur vos flux de travail 
* Mettre en corrélation des travaux sur différents comptes Automation 
* Visualiser l’historique de vos travaux dans le temps    

Pour plus d’informations sur l’intégration tooconfigure avec Analytique de journal toocollect, mettre en corrélation et agir sur les données de la tâche, consultez [transférer l’état du travail et flux de travail à partir de l’Automation tooLog Analytique (OMS)](automation-manage-send-joblogs-log-analytics.md).

## <a name="next-steps"></a>Étapes suivantes
* toolearn plus d’informations sur l’exécution du runbook, comment les tâches de runbook toomonitor et d’autres détails techniques, consultez [suivre un travail de runbook](automation-runbook-execution.md)
* toounderstand runbooks enfants toodesign et l’utilisation, voir [runbooks enfants dans Azure Automation](automation-child-runbooks.md)

