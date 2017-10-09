---
title: "aaaMy première PowerShell runbook dans Azure Automation | Documents Microsoft"
description: "Didacticiel qui vous guide tout au long de la création de hello, test et la publication d’un runbook PowerShell simple."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: azure powershell, didacticiel sur le script powershell, automatisation powershell
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;sngun
ms.openlocfilehash: abff94abe666cd8423c35b970b4162ba9247bcf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-runbook"></a>Mon premier Runbook PowerShell

> [!div class="op_single_selector"]
> * [Graphique](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Workflow PowerShell](automation-first-runbook-textual.md)
> 
> 

Ce didacticiel vous guide dans la création de hello d’un [runbook PowerShell](automation-runbook-types.md#powershell-runbooks) dans Azure Automation. Nous allons commencer avec un runbook simple que nous testons et publier pendant que nous expliquons comment tootrack hello état du travail de runbook hello. Puis nous modifions hello runbook tooactually gérer des ressources Azure, dans ce cas de démarrer une machine virtuelle Azure. Enfin, nous faisons hello runbook plus fiable en ajoutant des paramètres de runbook.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suivant :

* Abonnement Azure. Si vous n’avez pas encore d’abonnement, vous pouvez [activer vos avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[créer un compte gratuit](https://azure.microsoft.com/free/).
* [Compte Automation](automation-sec-configure-azure-runas-account.md) toohold hello runbook et authentifier les ressources tooAzure.  Ce compte doit avoir l’autorisation toostart et arrêter l’ordinateur virtuel de hello.
* Une machine virtuelle Azure. Nous arrêtons et démarrons cette machine afin qu’elle ne soit pas une machine virtuelle de production.

## <a name="step-1---create-new-runbook"></a>Étape 1 - Création d’un Runbook
Nous allons commencer par la création d’un runbook simple qui génère du texte hello *Hello World*.

1. Bonjour portail Azure, ouvrez votre compte Automation.  
   page compte d’automatisation Hello vous donne un aperçu rapide des ressources de hello dans ce compte. Vous devriez déjà posséder certains éléments. La plupart d'entre eux est des modules hello sont inclus automatiquement dans un compte Automation. Vous devez également avoir la ressource d’informations d’identification hello qui est mentionné dans hello [conditions préalables](#prerequisites).
2. Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.<br><br> ![RunbooksControl](media/automation-first-runbook-textual-powershell/runbooks-control-tiles.png)  
3. Créer un runbook en cliquant sur hello **ajouter un runbook** bouton, puis **créer un runbook**.
4. Nommez hello hello runbook *MyFirstRunbook-PowerShell*.
5. Dans ce cas, nous allons toocreate un [runbook PowerShell](automation-runbook-types.md#powershell-runbooks) ainsi sélectionnez **Powershell** pour **le type de Runbook**.<br><br> ![Types de Runbook](media/automation-first-runbook-textual-powershell/automation-runbook-type.png)  
6. Cliquez sur **créer** toocreate hello runbook et l’éditeur de texte hello ouvert.

## <a name="step-2---add-code-toohello-runbook"></a>Étape 2 : ajouter du code toohello runbook
Vous pouvez soit code type directement dans les runbook hello, ou vous pouvez sélectionner des applets de commande, les runbooks et les ressources de hello contrôle de la bibliothèque et ont les ajoutés runbook toohello avec tous les paramètres associés. Pour cette procédure pas à pas, vous tapez directement dans les runbook hello.

1. Notre Runbook est actuellement vide, saisissez *Write-Output « Hello World »*.<br><br> ![Hello World](media/automation-first-runbook-textual-powershell/automation-helloworld.png)  
2. Enregistrer les runbook hello en cliquant sur **enregistrer**.<br><br> ![Bouton Enregistrer](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-save.png)  

## <a name="step-3---test-hello-runbook"></a>Étape 3 : Test hello runbook
Avant que nous publions hello runbook toomake il disponible en production, nous souhaitons tootest il toomake assurer qu’il fonctionne correctement. Lorsque vous testez un Runbook, vous exécutez sa version **Brouillon** et affichez sa sortie de manière interactive.

1. Cliquez sur **volet Test** volet de Test tooopen hello.<br><br> ![Test Pane](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-test.png)  
2. Cliquez sur **Démarrer** test de hello toostart. Ce doit être l’option de hello uniquement activé.
3. Une [tâche de Runbook](automation-runbook-execution.md) est créée et son état apparaît.  
   état de la tâche Hello démarre en tant que *en file d’attente* indiquant qu’il est en attente d’un runbook worker dans hello toocome de cloud disponible. Il passe alors trop*départ* lorsqu’un processus de travail tâche de hello, les revendications, puis *en cours d’exécution* démarrage hello runbook réellement en cours d’exécution.  
4. Fin de la tâche du runbook hello, sa sortie s’affiche. Dans notre cas, nous devrions voir *Hello World*.<br><br> ![Résultat du volet de test](media/automation-first-runbook-textual-powershell/automation-testpane-output.png)  
5. Fermez la zone de dessin hello Test volet tooreturn toohello.

## <a name="step-4---publish-and-start-hello-runbook"></a>Étape 4 : publier et démarrer hello runbook
Hello runbook que vous avez créée est toujours en mode brouillon. Nous devons toopublish avant de l’exécuter en production.  Lorsque vous publiez un runbook, vous remplacez la version publiée existante de hello avec brouillon hello.  Dans notre cas, nous n’avez pas une version publiée encore, car nous avons créé hello runbook.

1. Cliquez sur **publier** toopublish hello runbook, puis **Oui** lorsque vous y êtes invité.<br><br> ![Bouton Publier](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-publish.png)  
2. Si vous faites défiler les runbook de hello tooview gauche Bonjour **Runbooks** volet maintenant, il affiche un **état de création** de **publié**.
3. Défilement arrière toohello tooview droite hello volet **MyFirstRunbook-PowerShell**.  
   Hello options haut hello nous permettent de toostart hello runbook, afficher hello runbook, planifier son toostart à un moment donné dans hello future ou créer un [webhook](automation-webhooks.md) afin de pouvoir être démarrée par un appel HTTP.
4. Nous souhaitez toostart hello runbook, cliquez sur **Démarrer** puis cliquez sur **Ok** lorsque le panneau de démarrer le Runbook hello s’ouvre.<br><br> ![Bouton Démarrer](media/automation-first-runbook-textual-powershell/automation-runbook-controls-start.png)<br>    
5. Un volet de travail est ouvert pour la tâche du runbook hello que nous avons créés. Nous pouvons fermer ce volet, mais dans ce cas nous laisser ouverte afin de nous pouvons observer la progression du travail hello.
6. état de la tâche Hello est indiqué dans **récapitulatif** et correspondances hello états que nous avons vu lorsque nous avons testé hello runbook.<br><br> ![Résumé des tâches](media/automation-first-runbook-textual-powershell/job-pane-status-blade-jobsummary.png)<br>  
7. Une fois hello runbook état indique *terminé*, cliquez sur **sortie**. volet de sortie Hello est ouvert, et nous pouvons voir notre *Hello World*.<br><br> ![Sortie de travail](media/automation-first-runbook-textual-powershell/job-pane-status-blade-outputtile.png)<br> 
8. Volet de sortie de fermeture hello.
9. Cliquez sur **tous les journaux** volet de flux tooopen hello pour la tâche du runbook hello. Nous devons uniquement voir *Hello World* dans la sortie de hello flux, mais cela peut afficher les autres flux pour un travail de runbook telles que des commentaires et d’erreur si hello runbook écrit toothem.<br><br> ![Tous les journaux](media/automation-first-runbook-textual-powershell/job-pane-status-blade-alllogstile.png)<br>   
10. Fermez hello flux volets et hello travail volet tooreturn toohello MyFirstRunbook-PowerShell.
11. Cliquez sur **travaux** volet de tâches tooopen hello pour ce runbook. Répertorie tous les travaux de hello créés par ce runbook. Nous devons uniquement voir une tâche répertoriée dans la mesure où nous avons uniquement les travaux hello qu’une seule fois.<br><br> ![Liste des postes](media/automation-first-runbook-textual-powershell/runbook-control-job-tile.png)  
12. Vous pouvez cliquer sur ce travail tooopen hello même volet de travail que nous avons vu lorsque nous avons commencé hello runbook. Ainsi, vous toogo à temps et consulter les détails de hello d’un travail qui a été créé pour un runbook donné.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>Étape 5 : ajouter l’authentification toomanage ressources Azure
Nous avons testé et publié notre Runbook, mais jusqu'à présent, il ne fait rien d'utile. Nous souhaitons toohave gérer les ressources Azure. Il ne sera pas en mesure de toodo que s’il s’authentifier à moins que nous avons à l’aide des informations d’identification hello qui sont référencés par tooin hello [conditions préalables](#prerequisites). Cela se fait par hello **Add-AzureRmAccount** applet de commande.

1. Éditeur de texte hello ouvrir en cliquant sur **modifier** dans le volet de hello MyFirstRunbook-PowerShell.<br><br> ![Modifier un Runbook](media/automation-first-runbook-textual-powershell/automation-runbook-controls-edit.png)<br>   
2. Nous ne devons hello **Write-Output** plus de ligne, par conséquent, continuez et le supprimer.
3. Tapez ou copiez-collez hello suivant le code qui gère l’authentification de hello avec votre compte Automation exécuter en tant que :
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
   <br>
4. Cliquez sur **Test volet** afin que nous puissions tester hello runbook.
5. Cliquez sur **Démarrer** test de hello toostart. Une fois terminée, vous devez recevoir toohello similaire de sortie suivant, l’affichage des informations de base à partir de votre compte. Cela confirme que ces informations d’identification hello sont valide.<br><br> ![Authentifier](media/automation-first-runbook-textual-powershell/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>Étape 6 : ajouter du code toostart une machine virtuelle
Maintenant que notre runbook authentifie tooour abonnement Azure, nous pouvons gérer les ressources. Nous ajoutons un toostart commande une machine virtuelle. Vous pouvez choisir n’importe quel ordinateur virtuel dans votre abonnement Azure, et pour l’instant, nous allons coder ce nom dans les runbook hello.

1. Après avoir *Add-AzureRmAccount*, type *AzureRmVM de démarrage-nom 'VMName' - ResourceGroupName 'NameofResourceGroup'* fournissant les noms de hello et groupe de ressources de toostart de machine virtuelle hello.  
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   ```
   <br>
2. Enregistrer hello runbook, puis cliquez sur **Test volet** afin que nous puissions le tester.
3. Cliquez sur **Démarrer** test de hello toostart. Une fois terminée, vérifiez que l’ordinateur virtuel hello a été démarré.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>Étape 7 : ajouter un runbook toohello de paramètre d’entrée
Notre runbook démarre actuellement hello virtuel de l’ordinateur que nous codé en dur dans les runbook hello, mais il est plus utile si nous spécifions la machine virtuelle de hello lorsque hello runbook est démarré. Nous allons maintenant ajouter des paramètres d’entrée toohello runbook tooprovide cette fonctionnalité.

1. Ajouter des paramètres pour *VMName* et *ResourceGroupName* toohello runbook et utilisation de ces variables hello **AzureRmVM de début** applet de commande comme exemple hello ci-dessous.  
   
   ```
   Param(
    [string]$VMName,
    [string]$ResourceGroupName
   )
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   ```
   <br>
2. Enregistrer les runbook hello et ouvrir le volet de Test hello. Vous pouvez maintenant fournir des valeurs pour hello deux variables d’entrée qui sont utilisés dans les tests de hello.
3. Volet de Test hello fermer.
4. Cliquez sur **publier** toopublish hello nouvelle version du runbook de hello.
5. Arrêter la machine virtuelle hello que vous avez démarrées à l’étape précédente de hello.
6. Cliquez sur **Démarrer** toostart hello runbook. Type Bonjour **VMName** et **ResourceGroupName** pour la machine virtuelle de hello que vous allez toostart.<br><br> ![Paramètre de réussite](media/automation-first-runbook-textual-powershell/automation-pass-params.png)<br>  
7. Lorsque hello runbook est terminée, vérifiez que l’ordinateur virtuel hello a été démarré.

## <a name="differences-from-powershell-workflow"></a>Différences par rapport à PowerShell Workflow
Runbook PowerShell ont hello même cycle de vie, les fonctionnalités et gestion en tant que les runbooks PowerShell Workflow, mais il existe certaines différences et les limitations :

1. Runbooks PowerShell exécuter tooPowerShell comparé rapide runbooks de flux de travail car ils n’ont pas étape de compilation.
2. Les runbooks PowerShell Workflow prend en charge les points de contrôle, à l’aide de points de contrôle, les runbooks PowerShell Workflow peut reprendre à partir de n’importe quel point dans le runbook de hello, tandis que les runbooks PowerShell peut reprendre uniquement à partir du début de hello.
3. Les Runbooks PowerShell Workflow prennent en charge l’exécution parallèle et série, alors que les Runbooks PowerShell peuvent exécuter des commandes en série uniquement.
4. Dans un runbook PowerShell Workflow, une activité, une commande ou un bloc de script peut avoir sa propre instance d’exécution, alors que dans un Runbook PowerShell, tous les éléments du script s’exécutent dans une instance d’exécution unique. Il existe également certaines [différences syntaxiques](https://technet.microsoft.com/magazine/dn151046.aspx) entre un Runbook PowerShell natif et un Runbook PowerShell Workflow.

## <a name="next-steps"></a>Étapes suivantes
* tooget main runbooks graphiques, consultez [mon premier runbook graphique](automation-first-runbook-graphical.md)
* tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md)
* tooknow en savoir plus sur les types de runbook, leurs avantages et les limitations, consultez [types de runbook Azure Automation](automation-runbook-types.md)
* Pour plus d’informations sur la fonctionnalité de prise en charge de script PowerShell, consultez [Prise en charge de script PowerShell natif dans Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

