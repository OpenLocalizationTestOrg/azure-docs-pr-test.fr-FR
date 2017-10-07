---
title: les runbook PowerShell Workflow premier aaaMy dans Azure Automation | Documents Microsoft
description: "Didacticiel qui vous guide tout au long de la création de hello, test et la publication d’un runbook de texte simple à l’aide de flux de travail PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: powershell workflow, exemples de workflows powershell, workflows powershell
ms.assetid: 0002d7f7-e2b5-46e3-b5eb-4596b84fd526
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;bwren
ms.openlocfilehash: b5a34d363ef4865878f3f68119833367b5280f83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-workflow-runbook"></a>Mon premier runbook PowerShell Workflow

> [!div class="op_single_selector"]
> * [Graphique](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Workflow PowerShell](automation-first-runbook-textual.md)
> 
> 

Ce didacticiel vous guide dans la création de hello d’un [runbook PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks) dans Azure Automation. Nous allons commencer avec un runbook simple que nous testons et publier tout en expliquant comment tootrack hello état du travail de runbook hello. Puis nous modifions hello runbook tooactually gérer des ressources Azure, dans ce cas de démarrer une machine virtuelle Azure. Enfin, nous faisons hello runbook plus fiable en ajoutant des paramètres de runbook.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suivant :

* Abonnement Azure. Si vous n’avez pas encore d’abonnement, vous pouvez [activer vos avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[créer un compte gratuit](https://azure.microsoft.com/free/).
* [Compte Automation](automation-sec-configure-azure-runas-account.md) toohold hello runbook et authentifier les ressources tooAzure.  Ce compte doit avoir l’autorisation toostart et arrêter l’ordinateur virtuel de hello.
* Une machine virtuelle Azure. Nous arrêtons et démarrons cette machine afin qu’elle ne soit pas une machine virtuelle de production.

## <a name="step-1---create-new-runbook"></a>Étape 1 - Création d’un Runbook
Nous allons commencer par la création d’un runbook simple qui génère du texte hello *Hello World*.

1. Bonjour portail Azure, ouvrez votre compte Automation.  
   page compte d’automatisation Hello vous donne un aperçu rapide des ressources de hello dans ce compte. Vous devriez déjà posséder certains éléments. La plupart d'entre eux est des modules hello sont inclus automatiquement dans un compte Automation. Vous devez également avoir la ressource d’informations d’identification hello qui est mentionné dans hello [conditions préalables](#prerequisites).
2. Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.<br><br> ![Contrôle des Runbooks](media/automation-first-runbook-textual/runbooks-control-tiles.png)
3. Créer un runbook en cliquant sur hello **ajouter un runbook** bouton, puis **créer un runbook**.
4. Nommez hello hello runbook *MyFirstRunbook-flux de travail*.
5. Dans ce cas, nous allons toocreate un [runbook PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks) ainsi sélectionnez **Powershell Workflow** pour **le type de Runbook**.<br><br> ![Nouveau Runbook](media/automation-first-runbook-textual/new-runbook-properties.png)
6. Cliquez sur **créer** toocreate hello runbook et l’éditeur de texte hello ouvert.

## <a name="step-2---add-code-toohello-runbook"></a>Étape 2 : ajouter du code toohello runbook
Vous pouvez soit code type directement dans les runbook hello, ou vous pouvez sélectionner des applets de commande, les runbooks et les ressources de hello contrôle de la bibliothèque et ont les ajoutés runbook toohello avec tous les paramètres associés. Pour cette procédure pas à pas, nous allons taper directement dans les runbook de hello.

1. Notre runbook est actuellement vide avec uniquement les hello requis *workflow* (mot clé), le nom hello de nos runbook et les accolades hello appliquer à l’ensemble du workflow hello.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   }
   ```
2. Tapez *Write-Output « Hello World. »* entre accolades de hello.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   Write-Output "Hello World"
   }
   ```
3. Enregistrer les runbook hello en cliquant sur **enregistrer**.<br><br> ![Enregistrer un Runbook](media/automation-first-runbook-textual/automation-runbook-edit-controls-save.png)

## <a name="step-3---test-hello-runbook"></a>Étape 3 : Test hello runbook
Avant que nous publions hello runbook toomake il disponible en production, nous souhaitons tootest il toomake assurer qu’il fonctionne correctement. Lorsque vous testez un Runbook, vous exécutez sa version **Brouillon** et affichez sa sortie de manière interactive.

1. Cliquez sur **volet Test** volet de Test tooopen hello.<br><br> ![Volet de test](media/automation-first-runbook-textual/automation-runbook-edit-controls-test.png)
2. Cliquez sur **Démarrer** test de hello toostart. Ce doit être l’option de hello uniquement activé.
3. Une [tâche de Runbook](automation-runbook-execution.md) est créée et son état apparaît.  
   état de la tâche Hello démarrera en tant que *en file d’attente* indiquant qu’il est en attente d’un runbook worker dans hello toocome de cloud disponible. Il passe alors trop*départ* lorsqu’un processus de travail tâche de hello, les revendications, puis *en cours d’exécution* démarrage hello runbook réellement en cours d’exécution.  
4. Fin de la tâche du runbook hello, sa sortie s’affiche. Dans notre cas, nous devrions voir *Hello World*.<br><br> ![Hello World](media/automation-first-runbook-textual/test-output-hello-world.png)
5. Fermez la zone de dessin hello Test volet tooreturn toohello.

## <a name="step-4---publish-and-start-hello-runbook"></a>Étape 4 : publier et démarrer hello runbook
runbook Hello que nous venons de créer est toujours en mode brouillon. Nous devons toopublish avant de l’exécuter en production. Lorsque vous publiez un runbook, vous remplacez la version publiée existante de hello avec brouillon hello. Dans notre cas, nous n’avez pas une version publiée encore, car nous avons créé hello runbook.

1. Cliquez sur **publier** toopublish hello runbook, puis **Oui** lorsque vous y êtes invité.<br><br> ![Publier](media/automation-first-runbook-textual/automation-runbook-edit-controls-publish.png)
2. Si vous faites défiler les runbook de hello tooview gauche Bonjour **Runbooks** volet maintenant, il affiche un **état de création** de **publié**.
3. Défilement arrière toohello tooview droite hello volet **MyFirstRunbook-flux de travail**.  
   Hello options haut hello nous permettent de toostart hello runbook, planifier son toostart à un moment donné dans hello futures ou créer un [webhook](automation-webhooks.md) afin de pouvoir être démarrée par un appel HTTP.
4. Nous voulons simplement nous toostart hello runbook cliquez alors sur **Démarrer** , puis **Oui** lorsque vous y êtes invité.<br><br> ![Démarrer un Runbook](media/automation-first-runbook-textual/automation-runbook-controls-start.png)
5. Un volet de travail est ouvert pour la tâche du runbook hello que nous venons de créer. Nous pouvons fermer ce volet, mais dans ce cas nous allons laisser ouverte afin de nous pouvons observer la progression du travail hello.
6. état de la tâche Hello est indiqué dans **récapitulatif** et correspondances hello états que nous avons vu lorsque nous avons testé hello runbook.<br><br> ![Résumé des tâches](media/automation-first-runbook-textual/job-pane-status-blade-jobsummary.png)
7. Une fois hello runbook état indique *terminé*, cliquez sur **sortie**. volet de sortie Hello est ouvert, et nous pouvons voir notre *Hello World*.<br><br> ![Résumé des tâches](media/automation-first-runbook-textual/job-pane-status-blade-outputtile.png)  
8. Volet de sortie de fermeture hello.
9. Cliquez sur **tous les journaux** volet de flux tooopen hello pour la tâche du runbook hello. Nous devons uniquement voir *Hello World* dans la sortie de hello flux, mais cela peut afficher les autres flux pour un travail de runbook telles que des commentaires et d’erreur si hello runbook écrit toothem.<br><br> ![Résumé des tâches](media/automation-first-runbook-textual/job-pane-status-blade-alllogstile.png)
10. Fermez hello flux volets et hello travail volet tooreturn toohello MyFirstRunbook.
11. Cliquez sur **travaux** volet de tâches tooopen hello pour ce runbook. Répertorie tous les travaux de hello créés par ce runbook. Nous devons uniquement voir une tâche répertoriée dans la mesure où nous avons uniquement les travaux hello qu’une seule fois.<br><br> ![Tâches](media/automation-first-runbook-textual/runbook-control-job-tile.png)
12. Vous pouvez cliquer sur cette hello tooopen de travail même volet de travail que nous avons vu lorsque nous avons commencé hello runbook. Ainsi, vous toogo à temps et consulter les détails de hello d’un travail qui a été créé pour un runbook donné.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>Étape 5 : ajouter l’authentification toomanage ressources Azure
Nous avons testé et publié notre Runbook, mais jusqu'à présent, il ne fait rien d'utile. Nous souhaitons toohave gérer les ressources Azure. Il ne sera pas en mesure de toodo que s’il s’authentifier à moins que nous avons à l’aide des informations d’identification hello qui sont référencés par tooin hello [conditions préalables](#prerequisites). Cela se fait par hello **Add-AzureRMAccount** applet de commande.

1. Éditeur de texte hello ouvrir en cliquant sur **modifier** dans le volet de hello MyFirstRunbook-flux de travail.<br><br> ![Modifier un Runbook](media/automation-first-runbook-textual/automation-runbook-controls-edit.png)
2. Nous ne devons hello **Write-Output** plus de ligne, par conséquent, continuez et le supprimer.
3. Placer le curseur hello sur une ligne vide entre les accolades hello.
4. Tapez ou copiez-collez hello suivant le code qui gère l’authentification avec votre compte d’identification Automation hello :

   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
5. Cliquez sur **Test volet** afin que nous puissions tester hello runbook.
6. Cliquez sur **Démarrer** test de hello toostart. Une fois terminée, vous devez recevoir toohello similaire de sortie suivant, l’affichage des informations de base à partir de votre compte. Cela confirme que ces informations d’identification hello sont valide.<br><br> ![Authentifier](media/automation-first-runbook-textual/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>Étape 6 : ajouter du code toostart une machine virtuelle
Maintenant que notre runbook authentifie tooour abonnement Azure, nous pouvons gérer les ressources. Nous ajoutons un toostart commande une machine virtuelle. Vous pouvez choisir n’importe quel ordinateur virtuel dans votre abonnement Azure, et pour l’instant, nous sera coder en dur ce nom dans les runbook hello.

1. Après avoir *Add-AzureRmAccount*, type *AzureRmVM de démarrage-nom 'VMName' - ResourceGroupName 'NameofResourceGroup'* fournissant les noms de hello et groupe de ressources de toostart de machine virtuelle hello.  

   ```
   workflow MyFirstRunbook-Workflow
   {
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   }
   ```
2. Enregistrer hello runbook, puis cliquez sur **Test volet** afin que nous puissions le tester.
3. Cliquez sur **Démarrer** test de hello toostart. Une fois terminée, vérifiez que l’ordinateur virtuel hello a été démarré.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>Étape 7 : ajouter un runbook toohello de paramètre d’entrée
Notre runbook démarre actuellement hello virtuel de l’ordinateur que nous codé en dur dans les runbook hello, mais il est plus utile si nous pouvons spécifier virtuels hello lorsque hello runbook est démarré. Nous allons maintenant ajouter des paramètres d’entrée toohello runbook tooprovide cette fonctionnalité.

1. Ajouter des paramètres pour *VMName* et *ResourceGroupName* toohello runbook et utilisation de ces variables hello **AzureRmVM de début** applet de commande comme exemple hello ci-dessous.

   ```
   workflow MyFirstRunbook-Workflow
   {
    Param(
     [string]$VMName,
     [string]$ResourceGroupName
    )  
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   }
   ```
2. Enregistrer les runbook hello et ouvrir le volet de Test hello. Notez que vous pouvez maintenant fournir des valeurs pour hello deux variables d’entrée qui seront utilisées dans le test de hello.
3. Volet de Test hello fermer.
4. Cliquez sur **publier** toopublish hello nouvelle version du runbook de hello.
5. Arrêter la machine virtuelle hello que vous avez démarrées à l’étape précédente de hello.
6. Cliquez sur **Démarrer** toostart hello runbook. Type Bonjour **VMName** et **ResourceGroupName** pour la machine virtuelle de hello que vous allez toostart.<br><br> ![Start Runbook](media/automation-first-runbook-textual/automation-pass-params.png)<br>  
7. Lorsque hello runbook est terminée, vérifiez que l’ordinateur virtuel hello a été démarré.  

## <a name="next-steps"></a>Étapes suivantes
* tooget main runbooks graphiques, consultez [mon premier runbook graphique](automation-first-runbook-graphical.md)
* tooget main runbook PowerShell, consultez [mon premier runbook de PowerShell](automation-first-runbook-textual-powershell.md)
* toolearn en savoir plus sur les types de runbook, leurs avantages et les limitations, consultez [types de runbook Azure Automation](automation-runbook-types.md)
* Pour plus d’informations sur la fonctionnalité de prise en charge de script PowerShell, consultez [Prise en charge de script PowerShell natif dans Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
