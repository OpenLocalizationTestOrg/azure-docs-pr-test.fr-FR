---
title: aaaError gestion dans Azure Automation des runbooks graphiques | Documents Microsoft
description: "Cet article décrit comment tooimplement gestion d’erreur logique dans Azure Automation des runbooks graphiques."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/26/2016
ms.author: magoedte
ms.openlocfilehash: b9ff01361d2ebd9c0174b074a7a290b1cc2fd1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-azure-automation-graphical-runbooks"></a>Gestion des erreurs dans les runbooks graphiques Azure Automation

Un tooconsider principal de création de runbook clé consiste à identifier différents problèmes liés à un runbook peut rencontrer. Ces problèmes peuvent être liés à la réussite, aux états d’erreur attendus et aux conditions d’erreur inattendue.

Les runbooks doivent inclure une gestion des erreurs. toovalidate hello la sortie d’une activité ou gérer une erreur avec des runbooks graphiques, vous pourriez utiliser une activité de code Windows PowerShell, définir la logique conditionnelle sur le lien de sortie hello d’activité hello ou appliquer une autre méthode.          

Souvent, s’il existe une erreur sans fin d’exécution qui se produit avec une activité de runbook, toute activité qui suit est traitée, quelle que soit l’erreur de hello. Erreur de Hello est toogenerate probablement une exception, mais l’activité suivante de hello est toujours autorisée toorun. Il s’agit de façon hello que PowerShell est conçue toohandle erreurs.    

types Hello des erreurs PowerShell qui peuvent se produire lors de l’exécution sont arrête ou sans fin d’exécution. différences de Hello entre les erreurs sans fin d’exécution et de fin sont les suivantes :

* **Erreur de fin**: une erreur grave lors de l’exécution qui arrête complètement la commande hello (ou l’exécution du script). Il peut s’agir de cmdlets inexistantes, d’erreurs de syntaxe qui empêchent une cmdlet de s’exécuter ou d’autres erreurs irrécupérables.

* **Erreur de fin d’exécution non**: une erreur non grave qui permet de toocontinue de l’exécution en dépit de l’échec de hello. Il peut s’agit d’erreurs opérationnelles comme un fichier introuvable et de problèmes d’autorisation.

Azure Automation runbooks graphiques ont été améliorés hello capacité tooinclude gestion d’erreurs. Vous pouvez maintenant convertir les exceptions en erreurs sans fin d’exécution et créer des liens d’erreur entre les activités. Ce processus permet à un auteur de runbook toocatch erreurs et gérez les conditions réalisées ou inattendues.  

## <a name="when-toouse-error-handling"></a>Lors de la gestion des erreurs toouse

Chaque fois qu’il existe une activité critique qui lève une erreur ou une exception, il est important tooprevent hello prochaine activité dans votre runbook à partir de l’erreur traitement toohandle hello en conséquence. Cela est tout particulièrement vital lorsque vos runbooks prennent en charge un processus d’entreprise ou de service.

Pour chaque activité qui peut générer une erreur, auteur de runbook hello peut ajouter un lien d’erreur pointant tooany autre activité.  activité de destination Hello peut être de tout type, y compris les activités de code, appelez une applet de commande, appel d’un autre runbook et ainsi de suite.

En outre, activité de destination hello peut également avoir des liens sortants. Ces liens peuvent être des liens réguliers ou des liens d’erreur. Cela signifie que l’auteur de runbook hello peut implémenter la logique de gestion des erreurs complexe sans avoir recours les tooa activité de code. Hello recommandé consiste toocreate un runbook de gestion des erreurs dédié avec des fonctionnalités communes, mais il n’est pas obligatoire. Logique de gestion des erreurs dans une activité de code PowerShell qu’il n’est pas hello seule option.  

Par exemple, prenons un runbook qui tente de toostart une machine virtuelle et installer une application sur ce dernier. Si hello machine virtuelle ne démarre pas correctement, il effectue deux actions :

1. Il envoie une notification concernant le problème.
2. Il démarre un autre runbook qui configure automatiquement une nouvelle machine virtuelle.

Une solution est toohave un lien d’erreur pointant activité tooan que gère la première étape. Par exemple, vous pouvez connecter hello **Write-Warning** activité de tooan d’applet de commande pour l’étape 2, par exemple hello **AzureRmAutomationRunbook de début** applet de commande.

Vous pourriez également généraliser ce comportement pour une utilisation dans nombreuses procédures opérationnelles en plaçant ces deux activités dans un runbook de la gestion des erreurs distinct et les conseils qui suivent hello suggéré précédemment. Avant d’appeler ce runbook de gestion des erreurs, vous pourriez construire un message personnalisé à partir des données hello dans les runbook d’origine hello et puis passez-le en tant qu’un runbook de gestion des erreurs de paramètre toohello.

## <a name="how-toouse-error-handling"></a>Comment la gestion des erreurs toouse

Chaque activité possède un paramètre de configuration permettant de transformer les exceptions en erreurs sans fin d’exécution. Par défaut, ce paramètre est désactivé. Nous vous recommandons d’activer ce paramètre sur toute activité dans laquelle vous souhaitez que les erreurs de toohandle.  

En activant cette configuration, vous sont garantissant que les erreurs avec ou sans fin d’exécution dans l’activité hello sont gérées comme des erreurs de sans fin d’exécution et peuvent être gérées avec un lien d’erreur.  

Après avoir configuré ce paramètre, vous créez une activité qui gère l’erreur de hello. Si une activité génère une erreur, puis hello erreur sortant des liens sont suivies et hello de liens réguliers ne sont pas, même si l’activité hello génère une sortie normale ainsi.<br><br> ![Exemple de lien d’erreur d’un runbook Automation](media/automation-runbook-graphical-error-handling/error-link-example.png)

Bonjour l’exemple suivant, un runbook récupère une variable qui contient le nom de l’ordinateur hello d’un ordinateur virtuel. Il tente alors de machine virtuelle de hello toostart avec l’activité suivante de hello.<br><br> ![Exemple de gestion des erreurs d’un runbook Automation](media/automation-runbook-graphical-error-handling/runbook-example-error-handling.png)<br><br>      

Hello **Get-AutomationVariable** activité et **Start-AzureRmVm** sont tooerrors d’exceptions tooconvert configuré.  S’il n’y hello difficultés variable ou départ hello machine virtuelle, puis les erreurs sont générées.<br><br> ![Paramètres d’activité de gestion des erreurs d’un runbook Automation](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)

Liens d’erreur de flux à partir de ces activités tooa unique **la gestion des erreurs** activité (code). Cette activité est configurée avec une expression PowerShell simple qui utilise hello *lever* toostop mot clé du traitement, ainsi que par *$Error.Exception.Message* tooget message de type hello qui décrit hello exception actuelle.<br><br> ![Exemple de code de gestion des erreurs d’un runbook Automation](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)


## <a name="next-steps"></a>Étapes suivantes

* toolearn en savoir plus sur les liens et les types de liens dans les runbooks graphiques, consultez [de création graphique dans Azure Automation](automation-graphical-authoring-intro.md#links-and-workflow).

* toolearn plus d’informations sur l’exécution du runbook, comment les tâches de runbook toomonitor et d’autres détails techniques, consultez [suivre un travail de runbook](automation-runbook-execution.md).
