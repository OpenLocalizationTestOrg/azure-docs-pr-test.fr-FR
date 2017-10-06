---
title: "aaaGraphical création dans Azure Automation | Documents Microsoft"
description: "Création du graphique vous permet de toocreate runbooks pour Azure Automation sans utilisation du code. Cet article fournit une introduction toographical de création et tous les détails de hello nécessaires toostart création d’un runbook graphique."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 4b6f840c-e941-4293-a728-b33407317943
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 6ddf18b992d5e5f7f4af95f344007a63ac498549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="graphical-authoring-in-azure-automation"></a>Création de graphiques dans Azure Automation
## <a name="introduction"></a>Introduction
Création graphique vous permet de toocreate runbooks d’automatisation Azure sans complexités hello du code sous-jacent de Windows PowerShell ou PowerShell Workflow hello. Ajouter les activités toohello canevas à partir d’une bibliothèque d’applets de commande et les procédures opérationnelles, les relier et de configurer tooform un flux de travail.  Si vous avez déjà travaillé avec System Center Orchestrator ou Service Management Automation (SMA), cela doit ressembler tooyou familier.   

Cet article fournit une présentation toographical hello et création des concepts qu'essentiels tooget démarré pour la création d’un runbook graphique.

## <a name="graphical-runbooks"></a>Runbooks graphiques
Dans Azure Automation, tous les Runbooks sont des workflows Windows PowerShell.  Procédures opérationnelles de flux de travail PowerShell graphique et graphique génèrent un code PowerShell qui est exécuté par une workers Automation de hello, mais vous n’êtes pas en mesure de tooview il ou le modifier directement.  Runbook graphique peut être converti tooa graphique PowerShell Workflow runbook et vice versa, mais ils ne peut pas être convertie tooa des runbook textuelle. Un runbook textuels existant ne peut pas être importé dans l’éditeur graphique hello.  

## <a name="overview-of-graphical-editor"></a>Vue d'ensemble de l'éditeur graphique
Vous pouvez ouvrir l’éditeur graphique de hello Bonjour portail Azure en créant ou modifiant un runbook graphique.

![Espace de travail graphique](media/automation-graphical-authoring-intro/runbook-graphical-editor.png)

Hello sections suivantes décrivent les contrôles de hello dans l’éditeur graphique de hello.

### <a name="canvas"></a>Canevas
Hello canevas est lorsque vous concevez votre runbook.  Vous ajoutez des activités à partir des nœuds hello hello bibliothèque contrôle toohello runbook et les connectez avec une logique hello liens toodefine de hello runbook.

Vous pouvez utiliser des contrôles de hello bas hello hello canevas toozoom et l’extraction.

![Espace de travail graphique](media/automation-graphical-authoring-intro/runbook-canvas-controls.png)

### <a name="library-control"></a>Contrôle Bibliothèque
est de Hello contrôle de la bibliothèque où vous sélectionnez [activités](#activities) tooadd tooyour runbook.  Ajoutez-les canevas toohello où vous vous connectez les activités de tooother.  Il comprend quatre sections décrites dans hello tableau suivant.

| Section | Description |
|:--- |:--- |
| Applets de commande |Inclut toutes les applets de commande hello, ce qui peuvent être utilisés dans votre runbook.  Les applets de commande sont organisées par module.  Tous les modules hello que vous avez installés dans votre compte automation seront disponibles. |
| Runbooks |Inclut des procédures opérationnelles de hello dans votre compte automation. Toobe de zone de dessin toohello utilisé en tant que runbooks enfants peuvent être ajoutés à ces procédures opérationnelles. Runbooks uniquement du même type de base comme hello runbook en cours de modification de hello sont affichés ; pour les graphiques runbooks uniquement basé sur PowerShell de procédures opérationnelles sont indiqués, tandis que pour les flux de travail PowerShell graphique runbook uniquement PowerShell Workflow basés sur les procédures opérationnelles sont. |
| Éléments multimédias |Inclut hello [ressources automation](http://msdn.microsoft.com/library/dn939988.aspx) dans votre compte automation qui peut être utilisée dans votre runbook.  Lorsque vous ajoutez un runbook de tooa actif, il ajoute une activité de flux de travail qui obtient l’élément sélectionné de hello.  Dans le cas de hello des ressources de variables, vous pouvez sélectionner si tooadd un tooget activité hello variable de hello variable ou définie. |
| Contrôle de Runbook |Inclut des activités de contrôle de Runbook qui peuvent être utilisées dans votre Runbook actuel. A *jonction* accepte plusieurs entrées et attend jusqu'à ce que toutes sont terminées avant la poursuite de l’opération du flux de travail hello. A *Code* activité s’exécute une ou plusieurs lignes de code PowerShell ou de flux de travail PowerShell selon le type de runbook graphique hello.  Vous pouvez utiliser cette activité pour le code personnalisé ou pour une fonctionnalité qui est difficile tooachieve avec d’autres activités. |

### <a name="configuration-control"></a>Contrôle Configuration
Hello contrôle de Configuration est où vous fournir des détails pour un objet sélectionné sur la zone de dessin hello. propriétés de Hello disponibles dans ce contrôle dépendent de type hello d’objet sélectionné.  Lorsque vous sélectionnez une option dans le contrôle de la Configuration de hello, il s’ouvre lames supplémentaires dans les informations de commande tooprovide supplémentaires.

### <a name="test-control"></a>Contrôle Test
Hello contrôle de Test n’est pas affichée lors du premier démarrage de l’éditeur graphique hello. Il s'ouvre lorsque vous [testez un Runbook graphique](#graphical-runbook-procedures)de manière interactive.  

## <a name="graphical-runbook-procedures"></a>Procédures relatives aux Runbooks graphiques
### <a name="exporting-and-importing-a-graphical-runbook"></a>Exportation et importation d'un Runbook graphique
Vous pouvez uniquement exporter hello la version publiée d’un runbook graphique.  Si hello runbook n’a pas encore été publiée, puis hello **exportation publiée** bouton est désactivé.  Lorsque vous cliquez sur hello **exportation publiée** bouton, hello runbook n’est téléchargé tooyour ordinateur local.  nom du fichier de hello de Hello correspond au nom de hello du runbook hello avec un *graphrunbook* extension.

![Exportation publiée](media/automation-graphical-authoring-intro/runbook-export.png)

Vous pouvez importer un fichier de runbook graphique ou de flux de travail PowerShell graphique en sélectionnant hello **importer** option lors de l’ajout d’un runbook.   Lorsque vous sélectionnez hello fichier tooimport, vous pouvez conserver hello même **nom** ou fournir un nouveau.  Hello champ Type de Runbook affichera le type hello de runbook une fois qu’il évalue le fichier hello sélectionné et si vous essayez de tooselect un autre type qui n’est pas correct, qu'un message s’affiche en notant les conflits potentiels et lors de la conversion, il peut y avoir erreurs de syntaxe.  

![Importer un Runbook](media/automation-graphical-authoring-intro/runbook-import-revised20165.png)

### <a name="testing-a-graphical-runbook"></a>Test d'un Runbook graphique
Vous pouvez tester hello brouillon d’un runbook dans hello portail Azure pendant que laissant hello version publiée de runbook hello inchangée, ou vous pouvez tester un runbook avant sa publication. Cela permet de tooverify qui hello runbook fonctionne correctement avant de remplacer la version publiée de hello. Lorsque vous testez un runbook, hello brouillon de runbook est exécuté et toutes les actions qu’il effectue sont terminées. Aucun historique des travaux ne sont créée, mais la sortie s’affiche dans le volet sortie de Test de hello. 

Ouvrir le contrôle de Test de hello pour un runbook en ouvrant runbook hello pour les modifier, puis cliquez sur hello **volet Test** bouton.

![Bouton Volet de test](media/automation-graphical-authoring-intro/runbook-edit-test-pane.png)

invite Hello contrôle de Test pour les paramètres d’entrée, et vous pouvez démarrer des runbook de hello en cliquant sur hello **Démarrer** bouton.

![Boutons de contrôle Test](media/automation-graphical-authoring-intro/runbook-test-start.png)

### <a name="publishing-a-graphical-runbook"></a>Publication d'un Runbook graphique
Dans Azure Automation, chaque Runbook a un brouillon et une version publiée. Seule la version publiée hello est disponible toobe exécuter, et uniquement hello brouillon peut être modifiée. version publiée de Hello n’est pas affectée par n’importe quelle version de brouillon de toohello de modifications. Lorsque le brouillon hello est prêt toobe disponible, publiez-la en remplacement hello publié version brouillon hello.

Vous pouvez publier un runbook graphique en ouvrant runbook hello pour la modification et puis en cliquant sur hello **publier** bouton.

![Bouton Publier](media/automation-graphical-authoring-intro/runbook-edit-publish.png)

Lorsqu'un Runbook n'a pas encore été publié, il a le statut **Nouveau**.  Une fois publié, il a le statut **Publié**.  Si vous modifiez hello runbook une fois qu’il a été publié, et les versions brouillon et publiée hello sont différentes, hello runbook a le statut **en cours de modification**.

![États du Runbook](media/automation-graphical-authoring-intro/runbook-statuses-revised20165.png) 

Vous avez également la version hello option toorevert toohello publiée d’un runbook.  Il rejette les modifications apportées depuis la dernière publication de hello runbook et remplace hello brouillon du runbook de hello avec la version publiée de hello.

![Toopublished bouton par défaut](media/automation-graphical-authoring-intro/runbook-edit-revert-published.png)

## <a name="activities"></a>Activités
Les activités sont hello des blocs de construction d’un runbook.  Une activité peut être une applet de commande PowerShell, un Runbook enfant ou une activité de workflow.  Vous ajoutez un runbook de toohello d’activité avec le bouton droit en cliquant dessus dans le contrôle de la bibliothèque de hello en sélectionnant **ajouter toocanvas**.  Vous pouvez cliquez et faites glisser tooplace d’activité hello n’importe où sur hello canevas que vous le souhaitez.  emplacement de hello d’activité hello sur la zone de dessin hello Hello n’effectue pas d’opération hello du runbook hello en aucune façon.  Vous pouvez disposition votre runbook toutefois s’avérer plus approprié toovisualize son fonctionnement. 

![Ajouter toocanvas](media/automation-graphical-authoring-intro/add-to-canvas-revised20165.png)

Sélectionnez activité hello sur hello canevas tooconfigure ses propriétés et les paramètres dans le panneau de Configuration hello.  Vous pouvez modifier hello **étiquette** de hello activité toosomething qui est tooyou descriptif.  applet de commande Hello d’origine est toujours en cours d’exécution, vous modifiez simplement son nom complet qui sera utilisé dans l’éditeur graphique de hello.  étiquette de Hello doit être unique dans les runbook hello. 

### <a name="parameter-sets"></a>Jeux de paramètres
Un jeu de paramètres définit des paramètres obligatoires et facultatives hello qui acceptent les valeurs pour une applet de commande particulière.  Toutes les applets de commande ont au moins un jeu de paramètres ; certaines en ont plusieurs.  Si une applet de commande a plusieurs jeux de paramètres, vous devez sélectionner celui que vous allez utiliser avant de pouvoir configurer les paramètres.  hello paramètre défini que vous choisissez dépend de paramètres Hello que vous pouvez configurer.  Vous pouvez modifier le jeu de paramètres hello utilisée par une activité en sélectionnant **paramètre la valeur** et en sélectionnant un autre jeu.  Dans ce cas, toutes les valeurs de paramètres que vous avez configurées sont perdues.

Dans l’exemple suivant de hello, applet de commande Get-AzureRmVM de hello possède trois jeux de paramètres.  Vous ne pouvez pas configurer les valeurs de paramètre jusqu'à ce que vous sélectionnez un des jeux de paramètres hello.  Hello ListVirtualMachineInResourceGroupParamSet paramètre défini est de retourner tous les ordinateurs virtuels dans un groupe de ressources et ayant un seul paramètre facultatif.  Hello GetVirtualMachineInResourceGroupParamSet est pour la spécification hello virtuels vous le souhaitez tooreturn et a deux obligatoires et un paramètre facultatif.

![Jeu de paramètres](media/automation-graphical-authoring-intro/get-azurermvm-parameter-sets.png)

#### <a name="parameter-values"></a>Valeurs de paramètres
Lorsque vous spécifiez une valeur pour un paramètre, vous sélectionnez un toodetermine de source de données la valeur de hello sera spécifié.  les sources de données Hello qui sont disponibles pour un paramètre particulier dépendent des valeurs valides de hello pour ce paramètre.  Par exemple, Null ne sera pas une option disponible pour un paramètre qui n'autorise pas les valeurs null.

| Source de données | Description |
|:--- |:--- |
| Valeur constante |Tapez une valeur pour le paramètre hello.  Cela est uniquement disponible pour hello les types de données suivants : Int32, Int64, String, Boolean, DateTime, commutateur. |
| Sortie d'activité |Sortie d’une activité qui précède l’activité en cours hello dans le flux de travail hello.  Toutes les activités valides sont répertoriées.  Sélectionnez simplement les toouse activité hello sa sortie pour la valeur du paramètre hello.  Si l’activité hello génère un objet avec plusieurs propriétés, vous pouvez tapez hello nom de propriété de hello après avoir sélectionné l’activité hello. |
| Entrée de Runbook |Sélectionnez un paramètre d’entrée du runbook en tant que paramètre d’entrée toohello de l’activité. |
| Ressource de variable |Sélectionnez une variable Automation comme entrée. |
| Ressource d’informations d’identification |Sélectionnez les informations d'identification Automation comme entrée. |
| Ressource de certificat |Sélectionnez un certificat Automation comme entrée. |
| Ressource de connexion |Sélectionnez une connexion Automation comme entrée. |
| Expression PowerShell |Spécifiez une [expression PowerShell](#powershell-expressions)simple.  Hello expression sera évaluée avant que résultat d’activité et hello hello utilisé comme valeur du paramètre hello.  Vous pouvez utiliser la sortie de toohello toorefer de variables d’une activité ou un paramètre d’entrée du runbook. |
| Non configuré |Efface toute valeur qui a été précédemment configurée. |

#### <a name="optional-additional-parameters"></a>Autres paramètres facultatifs
Toutes les applets de commande aura les paramètres de l’option hello tooprovide supplémentaires.  Il s'agit de paramètres communs PowerShell ou d'autres paramètres personnalisés.  Une zone de texte dans laquelle vous pouvez fournir des paramètres en utilisant la syntaxe PowerShell s'affiche.  Par exemple, toouse hello **Verbose** paramètre commun, vous devez spécifier **»-Verbose : $True »**.

### <a name="retry-activity"></a>Nouvelles tentatives d’activité
**Comportement des nouvelles tentatives** permet une toobe activité exécuter plusieurs fois jusqu'à ce qu’une condition particulière est remplie, tout comme une boucle.  Vous pouvez utiliser cette fonctionnalité pour les activités qui doit s’exécuter plusieurs fois, sont sujets à erreur et peut devez plusieurs tenter de réussite, ou tester hello les informations de sortie de l’activité hello de données valide.    

Lorsque vous activez les nouvelles tentatives pour une activité, vous pouvez définir un délai et une condition.  délai de Hello est heure hello (exprimé en secondes ou minutes) ce runbook hello attend avant d’exécuter à nouveau activité hello.  Si aucun délai n’est spécifié, hello activité est exécutée à nouveau immédiatement après la fin. 

![Délai de nouvelle tentative d’activité](media/automation-graphical-authoring-intro/retry-delay.png)

condition de nouvelle tentative Hello est une expression PowerShell qui est évaluée après l’exécution de chaque activité hello.  Si l’expression de hello résout tooTrue, hello activité s’exécute à nouveau.  Si l’expression de hello résout tooFalse puis hello activité ne s’exécute pas à nouveau et hello runbook se déplace sur l’activité suivante de toohello. 

![Délai de nouvelle tentative d’activité](media/automation-graphical-authoring-intro/retry-condition.png)

condition de nouvelle tentative Hello peut utiliser une variable appelée $RetryData qui fournit des tooinformation d’accès sur les nouvelles tentatives de hello activité.  Cette variable possède des propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| NumberOfAttempts |Nombre de fois que l’activité hello a été exécutée. |
| Sortie |Sortie de hello la dernière exécution de l’activité hello. |
| TotalDuration |A dépassé le délai écoulé depuis le début de l’activité hello hello la première fois. |
| StartedAt |A été démarré pour la première fois dans l’activité de hello format UTC. |

Voici des exemples de conditions de nouvelles tentatives d’activité.

    # Run hello activity exactly 10 times.
    $RetryData.NumberOfAttempts -ge 10 

    # Run hello activity repeatedly until it produces any output.
    $RetryData.Output.Count -ge 1 

    # Run hello activity repeatedly until 2 minutes has elapsed. 
    $RetryData.TotalDuration.TotalMinutes -ge 2

Après avoir configuré une condition de nouvelle tentative pour une activité, activité hello inclut deux signaux visuels tooremind vous.  Un est présenté dans l’activité hello et hello autres est lorsque vous passez en revue la configuration hello d’activité hello.

![Indicateurs visuels de nouvelle tentative d’activité](media/automation-graphical-authoring-intro/runbook-activity-retry-visual-cue.png)

### <a name="workflow-script-control"></a>Contrôle Script de workflow
Un contrôle de Code est une activité spéciale qui accepte un script PowerShell ou PowerShell de flux de travail en fonction de type hello de runbook graphique créé dans la fonctionnalité tooprovide de bons de commande qui sinon peut-être pas disponible.  Il n'accepte pas de paramètres, mais il peut utiliser des variables pour les paramètres de sortie d'activité et d'entrée de Runbook.  Toute sortie de l’activité hello est ajouté toohello databus, à moins ne qu’aucun lien sortant dans lequel cas il est ajouté une sortie toohello de hello runbook.

Par exemple hello de code suivant effectue les calculs de date à l’aide d’une variable d’entrée du runbook appelée $NumberOfDays.  Il envoie ensuite une heure date calculée en tant que toobe de sortie utilisé par les activités suivantes dans les runbook hello.

    $DateTimeNow = (Get-Date).ToUniversalTime()
    $DateTimeStart = ($DateTimeNow).AddDays(-$NumberOfDays)}
    $DateTimeStart


## <a name="links-and-workflow"></a>Liens et workflow
Dans un Runbook graphique, un **lien** connecte deux activités.  Il est affiché sur la zone de dessin hello par une flèche pointant à partir de l’activité de destination hello toohello de l’activité source.  activités de Hello s’exécutent dans le sens hello de flèche de hello avec l’activité de destination hello à partir de la fin de l’activité source hello.  

### <a name="create-a-link"></a>Créer un lien
Créer un lien entre deux activités par l’activité source hello en sélectionnant et en cliquant sur cercle de hello en bas de hello de forme de hello.  Faites glisser activité de destination hello flèche toohello et mise en production.

![Créer un lien](media/automation-graphical-authoring-intro/create-link-revised20165.png)

Sélectionnez hello lien tooconfigure ses propriétés dans le panneau de Configuration hello.  Cela inclut les type de lien de hello qui est décrit dans hello tableau suivant.

| Type de lien | Description |
|:--- |:--- |
| Pipeline |activité de destination Hello est exécutée une fois pour chaque objet de sortie à partir de l’activité source hello.  activité de destination Hello ne s’exécute pas si l’activité source hello entraîne aucun résultat.  Sortie de l’activité source hello est disponible en tant qu’objet. |
| Séquence |activité de destination Hello s’exécute qu’une seule fois.  Il reçoit un tableau d’objets à partir de l’activité source hello.  Sortie de l’activité source hello est disponible en tant que tableau d’objets. |

### <a name="starting-activity"></a>Activité de départ
Un Runbook graphique commence par toute activité qui n'a pas un lien entrant.  Ce sera souvent qu’une seule activité qui fait Office de hello démarrer activité hello runbook.  Si plusieurs activités n’ont pas un lien entrant, hello runbook démarrera en les exécutant en parallèle.  Il suivra alors hello liens toorun autres activités que chacun est terminée.

### <a name="conditions"></a>Conditions
Lorsque vous spécifiez une condition sur un lien, activité de destination hello est exécutée uniquement si la condition de hello résout tootrue.  En règle générale, vous utiliserez une variable $ActivityOutput dans une sortie de hello tooretrieve condition à partir de l’activité source hello.  

Pour un lien de pipeline, vous spécifiez une condition pour un seul objet et condition de hello est évaluée pour chaque objet retourné par l’activité source hello.  activité de destination Hello est ensuite exécutée pour chaque objet qui satisfait la condition de hello.  Par exemple, avec une activité de la source de Get-AzureRmVm, hello selon la syntaxe peut servir pour un tooretrieve de lien de pipeline conditionnel uniquement les ordinateurs virtuels de hello groupe de ressources nommé *Group1*.  

    $ActivityOutput['Get Azure VMs'].Name -match "Group1"

Pour un lien de la séquence, la condition de hello est évaluée uniquement une fois depuis un tableau est retourné qui contient toutes les sorties d’objets à partir de l’activité source hello.  Pour cette raison, un lien de la séquence ne peut pas être utilisé pour le filtrage comme un lien de pipeline, mais simplement déterminent ou non l’activité suivante de hello est exécutée. Prenons l’exemple hello suivant l’ensemble d’activités dans notre runbook de démarrer un ordinateur virtuel.<br> ![Lien conditionnel avec séquences](media/automation-graphical-authoring-intro/runbook-conditional-links-sequence.png)<br>
Il existe trois liens autre séquence qui la vérification des valeurs fournies les paramètres d’entrée runbook tootwo représentant le nom d’ordinateur virtuel et le nom du groupe de ressources dans toodetermine ordre qui est hello action appropriée tootake - démarrer une machine virtuelle unique, démarrer tous les ordinateurs virtuels Bonjour groupe de ressources, ou toutes les machines virtuelles dans un abonnement.  Lien de séquence hello entre tooAzure de se connecter et Get seule machine virtuelle est logique de condition hello :

    <# 
    Both VMName and ResourceGroupName runbook input parameters have values 
    #>
    (
    (($VMName -ne $null) -and ($VMName.Length -gt 0))
    ) -and (
    (($ResourceGroupName -ne $null) -and ($ResourceGroupName.Length -gt 0))
    )

Lorsque vous utilisez un lien conditionnel, données hello disponibles à partir d’activités de tooother activité hello source dans cette branche sont filtrées par la condition de hello.  Si une activité est toomultiple des liens de la source hello, puis hello tooactivities disponibles dans chaque branche varient selon la condition hello dans lien hello toothat branche de connexion de données.

Par exemple, hello **AzureRmVm de début** activité dans runbook hello ci-dessous démarre tous les ordinateurs virtuels.  Elle comporte deux liens conditionnels.  lien conditionnel Hello utilise l’expression de hello *$ActivityOutput [« Start-AzureRmVM']. IsSuccessStatusCode - eq $true* toofilter si hello AzureRmVm de début de l’activité terminé avec succès.  Hello utilise ensuite les expression hello *$ActivityOutput [« Start-AzureRmVM']. IsSuccessStatusCode - ne $true* toofilter si l’activité hello AzureRmVm de démarrage a échoué toostart hello virtual machine.  

![Exemple de lien conditionnel](media/automation-graphical-authoring-intro/runbook-conditional-links.png)

Toute activité qui suit le premier lien de hello et utilise la sortie d’activité hello de Get-AzureVM obtiendrez hello virtuels qui ont été démarrées au moment hello Get-AzureVM a été exécuté.  Toute activité qui suit le second lien de hello obtiendrez hello hello virtuels qui ont été arrêtées au moment hello Get-AzureVM a été exécuté.  Toute activité de lien de tiers hello obtenez toutes les machines virtuelles, quelle que soit leur état en cours d’exécution.

### <a name="junctions"></a>Jonctions
Une jonction est une activité spéciale qui attend que toutes les branches entrantes aient terminé.  Cela vous permet de toorun plusieurs activités en parallèle et vous assurer que toutes sont terminées avant de continuer.

Alors qu'une jonction peut avoir un nombre illimité de liens entrants, un seul de ces liens peut être un pipeline.  nombre de Hello de liens entrants de séquence n’est pas limitée.  Vous ne sera autorisé jonction de hello toocreate avec plusieurs liens de pipeline entrant et enregistrez hello runbook, mais il échoue lorsqu’il est exécuté.

exemple Hello ci-dessous fait partie d’un runbook qui démarre un ensemble d’ordinateurs virtuels, bien que le téléchargement simultanément des correctifs toobe appliqué toothose machines.  Une jointure est utilisée tooensure que les deux processus sont terminées avant hello runbook se poursuit.

![jonction](media/automation-graphical-authoring-intro/runbook-junction.png)

### <a name="cycles"></a>Cycles
Un cycle est quand une activité de destination est lié précédent tooits source d’activité ou tooanother activité que finalement revient tooits source.  Les cycles ne sont actuellement pas autorisés dans la création de graphiques.  Si votre Runbook a un cycle, il s'enregistrera correctement, mais il recevra une erreur lorsqu'il s'exécutera.

![Cycle](media/automation-graphical-authoring-intro/runbook-cycle.png)

### <a name="sharing-data-between-activities"></a>Partage de données entre des activités
Toutes les données qui sont générée par une activité avec un lien sortant sont écrit toohello *databus* hello runbook.  Toutes les activités de runbook de hello peuvent utiliser des données sur les valeurs de paramètre hello databus toopopulate ou inclure dans le code de script.  Sortie hello de toute activité précédente dans le flux de travail hello peut accéder à une activité.     

Manière dont les données de salutation sont écrit toohello databus dépend de type hello de lien sur l’activité hello.  Pour un **pipeline**, les données de salutation sont sortie en tant qu’objets de multiples.  Pour un **séquence** lier, données hello sont sortie sous forme de tableau.  S'il n'y a qu'une seule valeur, elle sera sortie sous la forme d'un tableau à un seul élément.

Vous pouvez accéder aux données hello de bus de données à l’aide d’une des deux méthodes.  Tout d’abord utilise un **sortie d’activité** un paramètre d’une autre activité toopopulate de source de données.  Si la sortie de hello est un objet, vous pouvez spécifier une seule propriété.

![Sortie d'activité](media/automation-graphical-authoring-intro/activity-output-datasource-revised20165.png)

Vous pouvez également récupérer la sortie hello d’une activité dans un **Expression PowerShell** source de données ou à partir d’un **Script de flux de travail** activité avec une variable ActivityOutput.  Si la sortie de hello est un objet, vous pouvez spécifier une seule propriété.  Les variables ActivityOutput utilisent hello selon la syntaxe.

    $ActivityOutput['Activity Label']
    $ActivityOutput['Activity Label'].PropertyName 

### <a name="checkpoints"></a>Points de contrôle
Vous pouvez définir des [points de contrôle](automation-powershell-workflow.md#checkpoints) dans un Runbook de workflow PowerShell graphique en sélectionnant *Runbook de point de contrôle* sur n’importe quelle activité.  Cela provoque une toobe de point de contrôle défini après l’exécution de l’activité hello.

![Point de contrôle](media/automation-graphical-authoring-intro/set-checkpoint.png)

Les points de contrôle sont activés uniquement dans les Runbooks de workflow PowerShell graphique ; ils ne sont pas disponibles dans les Runbooks graphiques.  Si hello runbook utilise les applets de commande Azure, vous devez suivre toute activité de point de contrôle avec un Add-AzureRMAccount en cas de hello runbook est interrompu et redémarre à partir de ce point de contrôle sur un autre traitement. 

## <a name="authenticating-tooazure-resources"></a>L’authentification des ressources de tooAzure
Runbooks dans Azure Automation qui gèrent les ressources Azure nécessite l’authentification tooAzure.  Hello [exécuter en tant que compte](automation-offering-get-started.md#creating-an-automation-account) (également désignée tooas un principal de service) est tooaccess de méthode par défaut hello ressources Azure Resource Manager dans votre abonnement aux runbooks Automation.  Vous pouvez ajouter des fonctionnalités tooa runbook graphique en ajoutant hello **AzureRunAsConnection** ressource de connexion, qui est à l’aide de hello PowerShell [Get-AutomationConnection](https://technet.microsoft.com/library/dn919922%28v=sc.16%29.aspx) applet de commande et [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande toohello canevas. Bonjour à l’exemple suivant illustre ce concept.<br>![Activités d’authentification de l’identification](media/automation-graphical-authoring-intro/authenticate-run-as-account.png)<br>
Hello l’activité obtenir exécuter en tant que connexion (par exemple, Get-AutomationConnection), est configuré avec une source de données de valeur de constante nommée AzureRunAsConnection.<br>![Configuration de la connexion d’identification](media/automation-graphical-authoring-intro/authenticate-runas-parameterset.png)<br>
activité suivante de Hello, Add-AzureRmAccount, ajoute hello authentifié compte d’identification pour une utilisation dans les runbook hello.<br>
![Jeu de paramètres Add-AzureRmAccount](media/automation-graphical-authoring-intro/authenticate-conn-to-azure-parameter-set.png)<br>
Pour les paramètres de hello **APPLICATIONID**, **CERTIFICATETHUMBPRINT**, et **TENANTID** vous devez nom hello de toospecify de propriété de hello pour le chemin d’accès du champ hello car activité Hello génère un objet avec plusieurs propriétés.  Dans le cas contraire, lorsque vous exécutez hello runbook, il échouera tooauthenticate lors de le.  C’est ce que vous avez besoin à un minimum tooauthenticate votre runbook avec hello s’exécuter en tant que compte.

toomaintain descendante compatibilité pour les abonnés qui ont créé une Automation de compte à l’aide un [compte d’utilisateur Active Directory de Azure](automation-create-aduser-account.md) toomanage déploiement classique Azure ou pour les ressources Azure Resource Manager, hello tooauthenticate de méthode applet de commande hello Add-AzureAccount avec un [actif d’informations d’identification](automation-credentials.md) qui représente un utilisateur Active Directory avec accès toohello compte Azure.

Vous pouvez ajouter des fonctionnalités tooa runbook graphique en ajoutant une zone de dessin actif d’informations d’identification toohello suivie d’une activité Add-AzureAccount.  Ajouter-AzureAccount utilise l’activité des informations d’identification hello pour son entrée.  Bonjour à l’exemple suivant illustre ce concept.

![Activités d'authentification](media/automation-graphical-authoring-intro/authentication-activities.png)

Vous avez tooauthenticate hello début du runbook de hello et après chaque point de contrôle.  Cela signifie qu'une activité Add-AzureAccount doit être ajoutée après chaque activité Checkpoint-Workflow. Vous n’avez pas besoin d’informations d’identification de l’addition activité car vous pouvez utiliser hello même 

![Sortie d'activité](media/automation-graphical-authoring-intro/authentication-activity-output.png)

## <a name="runbook-input-and-output"></a>Entrée et sortie de Runbook
### <a name="runbook-input"></a>Entrée de Runbook
Un runbook peut nécessiter une entrée à partir d’un utilisateur au démarrage hello runbook via hello portail Azure ou à partir d’un autre runbook si hello actuel est utilisé en tant qu’enfant.
Par exemple, si vous disposez d’un runbook qui crée un ordinateur virtuel, vous devrez peut-être tooprovide des informations telles que nom de hello de machine virtuelle de hello et d’autres propriétés chaque fois que vous démarrez hello runbook.  

Vous acceptez une entrée pour un Runbook en définissant un ou plusieurs paramètres d'entrée.  Vous indiquez des valeurs pour ces paramètres de que chaque runbook hello de temps est démarré.  Lorsque vous démarrez un runbook avec hello portail Azure, il vous invite valeurs tooprovide pour hello paramètres du runbook hello d’entrée.

Vous pouvez accéder à des paramètres d’entrée d’un runbook en cliquant sur hello **d’entrée et de sortie** bouton de barre d’outils de runbook hello.  

![Entrée/sortie de Runbook](media/automation-graphical-authoring-intro/runbook-edit-input-output.png) 

Cette opération ouvre hello **d’entrée et sortie** contrôle où vous pouvez modifier un paramètre d’entrée existant ou créez-en un en cliquant sur **Ajout de l’entrée**. 

![Ajouter une entrée](media/automation-graphical-authoring-intro/runbook-edit-add-input.png)

Chaque paramètre d’entrée est défini par les propriétés hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| Nom |nom unique de Hello du paramètre hello.  Il ne peut contenir que des caractères alphanumériques et ne peut pas contenir d'espace. |
| Description |Description facultative pour le paramètre d’entrée de hello. |
| Type |Type de données attendu pour la valeur du paramètre hello.  Hello portail Azure fournit un contrôle approprié pour le type de données hello pour chaque paramètre lors de l’entrée. |
| Obligatoire |Spécifie si une valeur doit être fournie pour le paramètre hello.  Hello runbook ne peut pas être démarré si vous ne fournissez pas une valeur pour chaque paramètre obligatoire qui n’a pas de valeur par défaut définie. |
| Valeur par défaut |Spécifie quelle valeur est utilisée pour le paramètre hello si aucune n’est pas fournie.  Cela peut être Null ou une valeur spécifique. |

### <a name="runbook-output"></a>Sortie de Runbook
Les données créées par toute activité qui ne dispose pas d’un lien sortant seront ajoutées toohello [sortie du runbook de hello](http://msdn.microsoft.com/library/azure/dn879148.aspx).  sortie de Hello est enregistrée avec la tâche du runbook hello et est disponible tooa le runbook parent lorsque hello runbook est utilisé en tant qu’enfant.  

## <a name="powershell-expressions"></a>Expressions PowerShell
Un des avantages de hello de création graphique vous apporte hello capacité toobuild un runbook avec des connaissances minimales de PowerShell.  Actuellement, vous avez besoin de tooknow un peu de PowerShell si utilisé pour remplir certaines [les valeurs de paramètre](#activities) et pour le paramètre [conditions de lien](#links-and-workflow).  Cette section fournit une introduction rapide tooPowerShell des expressions pour les utilisateurs qui ne sont peut-être pas familiarisés avec lui.  La totalité des informations sur PowerShell est disponible dans [Écriture de scripts avec Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). 

### <a name="powershell-expression-data-source"></a>Source de données d’expressions PowerShell
Vous pouvez utiliser une expression PowerShell comme une valeur de données source toopopulate hello un [paramètre d’activité](#activities) avec des résultats d’un code PowerShell hello.  Il peut s'agir d'une seule ligne de code qui exécute une fonction simple ou de plusieurs lignes qui suivent une logique complexe.  Toute sortie issue d’une commande qui n’est pas affecté tooa variable est la valeur de paramètre de sortie toohello. 

Par exemple, hello commande suivante affiche hello date actuelle. 

    Get-Date

Hello commandes générer une chaîne à partir de hello date actuelle et affectez-le tooa variable.  Hello contenu de la variable de hello est ensuite envoyé toohello sortie 

    $string = "hello current date is " + (Get-Date)
    $string

Bonjour commandes suivantes évaluent hello date actuelle et retournent une chaîne indiquant si hello jour actuel est un week-end ou un jour de la semaine. 

    $date = Get-Date
    if (($date.DayOfWeek = "Saturday") -or ($date.DayOfWeek = "Sunday")) { "Weekend" }
    else { "Weekday" }


### <a name="activity-output"></a>Sortie d'activité
sortie de hello toouse à partir d’une activité précédente dans runbook hello, utiliser la variable hello $ActivityOutput avec la syntaxe de hello.

    $ActivityOutput['Activity Label'].PropertyName

Par exemple, vous pouvez avoir une activité avec une propriété qui requiert le nom hello d’un ordinateur virtuel dans ce cas, vous pouvez utiliser hello expression suivante.

    $ActivityOutput['Get-AzureVm'].Name

Si la propriété hello nécessitant d’objet de machine virtuelle hello au lieu de simplement une propriété, puis vous renvoie à l’aide de l’objet complet hello hello selon la syntaxe.

    $ActivityOutput['Get-AzureVm']

Vous pouvez également utiliser la sortie hello d’une activité dans une expression plus complexe, telle que suivante hello qui concatène le nom d’ordinateur virtuel de toohello de texte.

    "hello computer name is " + $ActivityOutput['Get-AzureVm'].Name


### <a name="conditions"></a>Conditions
Utilisez [opérateurs de comparaison](https://technet.microsoft.com/library/hh847759.aspx) toocompare valeurs ou déterminer si une valeur correspond à un modèle spécifié.  Une comparaison renvoie la valeur $true ou $false.

Par exemple, hello suivant condition détermine si la machine virtuelle de hello à partir d’une activité nommée *Get-AzureVM* est actuellement *arrêté*. 

    $ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped"

vérifications de condition suivante de Hello si hello même ordinateur virtuel est dans un état autre que *arrêté*.

    $ActivityOutput["Get-AzureVM"].PowerState –ne "Stopped"

Vous pouvez joindre plusieurs conditions en utilisant un [opérateur logique](https://technet.microsoft.com/library/hh847789.aspx) comme **-and** ou **-or**.  Par exemple, hello suivants pour la condition vérifie si hello même machine virtuelle dans l’exemple précédent de hello est dans un état de *arrêté* ou *arrêt*.

    ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped") -or ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopping") 


### <a name="hashtables"></a>Tables de hachage
[Tables de hachage](http://technet.microsoft.com/library/hh847780.aspx) sont des paires nom/valeur servant à renvoyer un ensemble de valeurs.  Les propriétés de certaines activités peuvent attendre une table de hachage plutôt qu'une valeur simple.  Vous pouvez également voir la table de hachage visés tooas un dictionnaire. 

Vous créez une table de hachage avec la syntaxe de hello.  Une table de hachage peut contenir un nombre quelconque d'entrées, chacune étant définie par un nom et une valeur.

    @{ <name> = <value>; [<name> = <value> ] ...}

Par exemple, hello expression suivante crée un toobe de la table de hachage utilisé dans la source de données hello pour un paramètre d’activité qui attendu d’une table de hachage avec des valeurs pour une recherche sur internet.

    $query = "Azure Automation"
    $count = 10
    $h = @{'q'=$query; 'lr'='lang_ja';  'count'=$Count}
    $h

Hello exemple suivant utilise la sortie à partir d’une activité nommée *obtenir la connexion Twitter* toopopulate une table de hachage.

    @{'ApiKey'=$ActivityOutput['Get Twitter Connection'].ConsumerAPIKey;
      'ApiSecret'=$ActivityOutput['Get Twitter Connection'].ConsumerAPISecret;
      'AccessToken'=$ActivityOutput['Get Twitter Connection'].AccessToken;
      'AccessTokenSecret'=$ActivityOutput['Get Twitter Connection'].AccessTokenSecret}



## <a name="next-steps"></a>Étapes suivantes
* tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md) 
* tooget main runbooks graphiques, consultez [mon premier runbook graphique](automation-first-runbook-graphical.md)
* tooknow en savoir plus sur les types de runbook, leurs avantages et les limitations, consultez [types de runbook Azure Automation](automation-runbook-types.md)
* toounderstand à l’aide de tooauthenticate hello Automation comme compte d’identification, voir [configurer Azure compte d’identification](automation-sec-configure-azure-runas-account.md)

