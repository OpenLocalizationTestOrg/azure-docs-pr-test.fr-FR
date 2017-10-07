---
title: "runbook graphique de première aaaMy dans Azure Automation | Documents Microsoft"
description: "Didacticiel qui vous guide tout au long de la création de hello, test et la publication d’un runbook graphique simple."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "runbook, modèle de runbook, automatisation des runbooks, runbook azure"
ms.assetid: dcb88f19-ed2b-4372-9724-6625cd287c8a
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/17/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 964cf8bae75ca597959bfc39b2b07c22bbc9acb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-graphical-runbook"></a>Mon premier Runbook graphique

> [!div class="op_single_selector"]
> * [Graphique](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Workflow PowerShell](automation-first-runbook-textual.md)
> 
> 

Ce didacticiel vous guide dans la création de hello d’un [runbook graphique](automation-runbook-types.md#graphical-runbooks) dans Azure Automation.  Nous allons commencer avec un simple runbook qui teste et publie pendant que nous expliquons comment tootrack hello état du travail de runbook hello.  Puis nous modifions hello runbook tooactually gérer des ressources Azure, dans ce cas de démarrer une machine virtuelle Azure.  Ensuite, nous allons terminer didacticiel de hello en rendant hello runbook plus fiable en ajoutant des paramètres du runbook et des liaisons conditionnelles.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suivant.

* Abonnement Azure.  Si vous n’avez pas encore d’abonnement, vous pouvez [activer vos avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[créer un compte gratuit](https://azure.microsoft.com/free/).
* [Compte d’automatisation Azure](automation-sec-configure-azure-runas-account.md) toohold hello runbook et authentifier les ressources tooAzure.  Ce compte doit avoir l’autorisation toostart et arrêter l’ordinateur virtuel de hello.
* Une machine virtuelle Azure.  Nous arrêterons et démarrerons cet ordinateur afin qu'il ne soit pas en production.

## <a name="step-1---create-runbook"></a>Étape 1 - Création d’un Runbook
Nous commençons par créer un simple runbook qui génère du texte hello *Hello World*.

1. Bonjour portail Azure, ouvrez votre compte Automation.  
   page compte d’automatisation Hello vous donne un aperçu rapide des ressources de hello dans ce compte.  Vous devriez déjà posséder certains éléments multimédias.  La plupart d'entre eux est des modules hello sont inclus automatiquement dans un compte Automation.  Vous devez également avoir la ressource d’informations d’identification hello qui est mentionné dans hello [conditions préalables](#prerequisites).
2. Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.<br> ![Contrôle des Runbooks](media/automation-first-runbook-graphical/runbooks-resources-tile.png)
3. Créer un runbook en cliquant sur hello **ajouter un runbook** bouton, puis **créer un runbook**.
4. Nommez hello hello runbook *MyFirstRunbook graphique*.
5. Dans ce cas, nous allons toocreate un [runbook graphique](automation-graphical-authoring-intro.md) ainsi sélectionnez **Graphical** pour **le type de Runbook**.<br> ![Nouveau Runbook](media/automation-first-runbook-graphical/create-new-runbook.png)<br>
6. Cliquez sur **créer** toocreate hello runbook et l’éditeur graphique de hello ouvert.

## <a name="step-2---add-activities-toohello-runbook"></a>Étape 2 : ajouter des activités toohello runbook
Hello contrôle bibliothèque hello les côté gauche de l’éditeur de hello vous permet de tooselect activités tooadd tooyour runbook.  Nous allons tooadd un **Write-Output** applet de commande toooutput texte hello runbook.

1. Bonjour contrôle de la bibliothèque, cliquez sur dans la zone de texte Rechercher hello et type **Write-Output**.  résultats de la recherche Hello seront affichera ci-dessous. <br> ![Microsoft.PowerShell.Utility](media/automation-first-runbook-graphical/search-powershell-cmdlet-writeoutput.png)
2. Faites défiler bas toohello de liste de hello.  Vous pouvez soit avec le bouton **Write-Output** et sélectionnez **ajouter toocanvas** ou cliquez sur hello ellipse toohello applet de commande suivante, puis sélectionnez **ajouter toocanvas**.
3. Cliquez sur hello **Write-Output** activité sur la zone de dessin hello.  Cette opération ouvre le panneau de contrôle hello Configuration, ce qui vous permet d’activité de hello tooconfigure.
4. Hello **étiquette** par défaut est le nom de toohello d’applet de commande hello, mais nous pouvons modifier toosomething plus convivial. Modifier trop*écrire Hello World toooutput*.
5. Cliquez sur **paramètres** tooprovide des valeurs pour les paramètres de l’applet de commande hello.  
   Certaines applets de commande ont plusieurs jeux de paramètres, et vous devez tooselect l’un toouse vous. Dans ce cas, **Write-Output** n'a qu’un seul jeu de paramètres, vous n’avez pas besoin de tooselect une. <br> ![Propriétés Write-Output](media/automation-first-runbook-graphical/write-output-properties-b.png)
6. Sélectionnez hello **InputObject** paramètre.  Il s’agit paramètre hello où nous spécifions hello texte toosend toohello le flux de sortie.
7. Bonjour **source de données** liste déroulante, sélectionnez **expression PowerShell**.  Hello **source de données** déroulante propose différentes sources que vous utilisez toopopulate une valeur de paramètre.  
   Vous pouvez utiliser la sortie de ces sources, par exemple une autre activité, un élément multimédia Automation ou une expression PowerShell.  Dans ce cas, nous voulons simplement nous texte hello de toooutput *Hello World*. Nous pouvons utiliser une expression PowerShell et spécifiez une chaîne.
8. Bonjour **Expression** , tapez *« Hello World »* puis cliquez sur **OK** deux fois le canevas de toohello tooreturn.<br> ![PowerShell Expression](media/automation-first-runbook-graphical/expression-hello-world.png)
9. Enregistrer les runbook hello en cliquant sur **enregistrer**.<br> ![Enregistrer un Runbook](media/automation-first-runbook-graphical/runbook-toolbar-save-revised20165.png)

## <a name="step-3---test-hello-runbook"></a>Étape 3 : Test hello runbook
Avant que nous publions hello runbook toomake il disponible en production, nous souhaitons tootest il toomake assurer qu’il fonctionne correctement.  Lorsque vous testez un Runbook, vous exécutez sa version **Brouillon** et affichez sa sortie de manière interactive.

1. Cliquez sur **volet Test** Panneau de Test tooopen hello.<br> ![Volet de test](media/automation-first-runbook-graphical/runbook-toolbar-test-revised20165.png)
2. Cliquez sur **Démarrer** test de hello toostart.  Ce doit être l’option de hello uniquement activé.
3. A [tâche du runbook](automation-runbook-execution.md) est créé et son état affiché dans le volet de hello.  
   état de la tâche Hello démarre en tant que *en file d’attente* indiquant qu’il est en attente d’un runbook worker dans hello toobecome de cloud disponible.  Il déplace ensuite trop*départ* lorsqu’un processus de travail tâche de hello, les revendications, puis *en cours d’exécution* au démarrage de runbook de hello réellement en cours d’exécution.  
4. Fin de la tâche du runbook hello, sa sortie s’affiche. Dans notre cas, nous devrions voir *Hello World*.<br> ![Hello World](media/automation-first-runbook-graphical/runbook-test-results.png)
5. Fermez le canevas toohello tooreturn hello Test lame.

## <a name="step-4---publish-and-start-hello-runbook"></a>Étape 4 : publier et démarrer hello runbook
Hello runbook que vous avez créée est toujours en mode brouillon. Nous devons toopublish avant de l’exécuter en production.  Lorsque vous publiez un runbook, vous remplacez la version publiée existante de hello avec brouillon hello.  Dans notre cas, nous n’avez pas une version publiée encore, car nous avons créé hello runbook.

1. Cliquez sur **publier** toopublish hello runbook, puis **Oui** lorsque vous y êtes invité.<br> ![Publier](media/automation-first-runbook-graphical/runbook-toolbar-publish-revised20166.png)
2. Si vous faites défiler les runbook de hello tooview gauche Bonjour **Runbooks** panneau, il affiche un **état de création** de **publié**.
3. Panneau de hello défilement arrière toohello tooview droite pour **MyFirstRunbook**.  
   Hello options haut hello nous permettent de toostart hello runbook, planifier son toostart à un moment donné dans hello futures ou créer un [webhook](automation-webhooks.md) afin de pouvoir être démarrée par un appel HTTP.
4. Nous voulons simplement nous toostart hello runbook cliquez alors sur **Démarrer** , puis **Oui** lorsque vous y êtes invité.<br> ![Démarrer un Runbook](media/automation-first-runbook-graphical/runbook-controls-start-revised20165.png)
5. Un panneau de travail est ouvert pour la tâche du runbook hello que nous avons créés.  Nous pouvons fermer ce panneau, mais dans ce cas nous laisser ouverte afin de nous pouvons observer la progression du travail hello.
6. état de la tâche Hello est indiqué dans **récapitulatif** et correspondances hello états que nous avons vu lorsque nous avons testé hello runbook.<br> ![Résumé des tâches](media/automation-first-runbook-graphical/runbook-job-summary.png)
7. Une fois hello runbook état indique *terminé*, cliquez sur **sortie**. Hello **sortie** panneau est ouvert, et nous pouvons voir notre *Hello World* dans le volet de hello.<br> ![Résumé des tâches](media/automation-first-runbook-graphical/runbook-job-output.png)  
8. Panneau de sortie de fermeture hello.
9. Cliquez sur **tous les journaux** Panneau de flux tooopen hello pour la tâche du runbook hello.  Nous devons uniquement voir *Hello World* dans la sortie de hello flux, mais cela peut afficher les autres flux pour un travail de runbook telles que des commentaires et d’erreur si hello runbook écrit toothem.<br> ![Résumé des tâches](media/automation-first-runbook-graphical/runbook-job-AllLogs.png)
10. Fermez la lame de tous les journaux hello et panneau de hello travail panneau tooreturn toohello MyFirstRunbook.
11. Cliquez sur **travaux** Panneau de travaux tooopen hello pour ce runbook.  Celle-ci répertorie toutes les tâches de hello créées par ce runbook. Nous devons uniquement voir une tâche répertoriée dans la mesure où nous avons uniquement les travaux hello qu’une seule fois.<br> ![Tâches](media/automation-first-runbook-graphical/runbook-control-jobs.png)
12. Vous pouvez cliquer sur ce travail tooopen hello même volet de travail que nous avons vu lorsque nous avons commencé hello runbook.  Ainsi, vous toogo à temps et consulter les détails de hello d’un travail qui a été créé pour un runbook donné.

## <a name="step-5---create-variable-assets"></a>Étape 5 - Créer des ressources de variables
Nous avons testé et publié notre Runbook, mais jusqu'à présent, il ne fait rien d'utile. Nous souhaitons toohave gérer les ressources Azure.  Avant de configurer la hello runbook tooauthenticate, nous nous créer un ID d’abonnement toohold variable hello et à le référencer une fois que nous configurons tooauthenticate d’activité hello à l’étape 6 ci-dessous.  Y compris un contexte d’abonnement toohello référence vous permet de travail tooeasily entre plusieurs abonnements.  Avant de continuer, copiez votre ID d’abonnement à partir de hello option abonnements de volet de Navigation hello.  

1. Dans le panneau de comptes Automation hello, cliquez sur hello **actifs** vignette et hello **actifs** panneau est ouvert.
2. Dans le panneau des ressources hello, cliquez sur hello **Variables** vignette.
3. Dans le panneau Variables de hello, cliquez sur **ajouter une variable**.<br>![Variable Automation](media/automation-first-runbook-graphical/create-new-subscriptionid-variable.png)
4. Dans Panneau de variable hello nouvelle, Bonjour **nom** , entrez **AzureSubscriptionId** et Bonjour **valeur** Entrez votre ID d’abonnement.  Conserver *chaîne* pour hello **Type** et valeur par défaut de hello **chiffrement**.  
5. Cliquez sur **créer** variable de hello toocreate.  

## <a name="step-6---add-authentication-toomanage-azure-resources"></a>Étape 6 : ajouter l’authentification toomanage ressources Azure
Maintenant que nous disposons d’une variable toohold notre ID d’abonnement, nous pouvons configurer notre tooauthenticate runbook avec hello exécuter en tant qu’informations d’identification qui sont visées tooin hello [conditions préalables](#prerequisites).  Il suffit d’ajouter hello Azure exécuter en tant que connexion **Asset** et **Add-AzureRMAccount** applet de commande toohello canevas.  

1. Éditeur graphique de hello ouvrir en cliquant sur **modifier** sur le panneau de MyFirstRunbook hello.<br> ![Modifier un Runbook](media/automation-first-runbook-graphical/runbook-controls-edit-revised20165.png)
2. Nous ne devons hello **écrire Hello World toooutput** , par conséquent, faites un clic droit et sélectionnez **supprimer**.
3. Bonjour contrôle de la bibliothèque, développez **connexions** et ajoutez **AzureRunAsConnection** toohello de zone de dessin en sélectionnant **ajouter toocanvas**.
4. Dans la zone de dessin hello, sélectionnez **AzureRunAsConnection** et, dans le volet de contrôle de Configuration hello, tapez **obtenir exécuter en tant que connexion** Bonjour **étiquette** zone de texte.  Il s’agit hello connexion
5. Dans le contrôle de la bibliothèque de hello, tapez **Add-AzureRmAccount** dans la zone de texte Rechercher hello.
6. Ajouter **Add-AzureRmAccount** toohello la zone de dessin.<br> ![Add-AzureRMAccount](media/automation-first-runbook-graphical/search-powershell-cmdlet-addazurermaccount.png)
7. Placez le curseur sur **obtenir exécuter en tant que connexion** jusqu'à ce qu’un cercle apparaît sous forme de hello hello. Cliquez sur le cercle de hello et faites glisser la flèche de hello trop**Add-AzureRmAccount**.  flèche Hello que vous avez créé est un *lien*.  Hello runbook démarre avec **obtenir exécuter en tant que connexion** , puis exécutez **Add-AzureRmAccount**.<br> ![Créer un lien entre des activités](media/automation-first-runbook-graphical/runbook-link-auth-activities.png)
8. Dans la zone de dessin hello, sélectionnez **Add-AzureRmAccount** et Bonjour Configuration contrôler le type de volet **connexion tooAzure** Bonjour **étiquette** zone de texte.
9. Cliquez sur **paramètres** et panneau de Configuration de paramètre d’activité hello s’affiche.
10. **AzureRmAccount ajouter** a plusieurs jeux de paramètres, donc nous tooselect un avant que nous pouvons fournir des valeurs de paramètre.  Cliquez sur **paramètre la valeur** , puis sélectionnez hello **ServicePrincipalCertificatewithSubscriptionId** jeu de paramètres.
11. Une fois que vous sélectionnez le jeu de paramètres hello, paramètres de hello s’affichent dans le panneau de Configuration de paramètre d’activité hello.  Cliquez sur **APPLICATIONID**.<br> ![Ajouter des paramètres de compte Azure RM](media/automation-first-runbook-graphical/add-azurermaccount-params.png)
12. Dans le panneau de la valeur du paramètre hello, sélectionnez **sortie d’activité** pour hello **source de données** et sélectionnez **obtenir exécuter en tant que connexion** à partir de la liste hello, Bonjour **champ chemin d’accès** type de zone de texte **ApplicationId**, puis cliquez sur **OK**.  Nous spécifions nom hello de propriété de hello pour le chemin d’accès du champ hello, car l’activité hello génère un objet avec plusieurs propriétés.
13. Cliquez sur **CERTIFICATETHUMBPRINT**et dans le panneau de la valeur du paramètre hello, sélectionnez **sortie d’activité** pour hello **source de données**.  Sélectionnez **obtenir exécuter en tant que connexion** à partir de la liste hello, Bonjour **chemin d’accès du champ** type de zone de texte **CertificateThumbprint**, puis cliquez sur **OK**.
14. Cliquez sur **SERVICEPRINCIPAL**et dans le panneau de la valeur du paramètre hello, sélectionnez **ConstantValue** pour hello **source de données**, cliquez sur hello option **True**, puis cliquez sur **OK**.
15. Cliquez sur **TENANTID**et dans le panneau de la valeur du paramètre hello, sélectionnez **sortie d’activité** pour hello **source de données**.  Sélectionnez **obtenir exécuter en tant que connexion** à partir de la liste hello, Bonjour **chemin d’accès du champ** type de zone de texte **TenantId**, puis cliquez sur **OK** à deux reprises.  
16. Dans le contrôle de la bibliothèque de hello, tapez **Set-AzureRmContext** dans la zone de texte Rechercher hello.
17. Ajouter **Set-AzureRmContext** toohello la zone de dessin.
18. Dans la zone de dessin hello, sélectionnez **Set-AzureRmContext** et Bonjour Configuration contrôler le type de volet **Id d’abonnement spécifier** Bonjour **étiquette** zone de texte.
19. Cliquez sur **paramètres** et panneau de Configuration de paramètre d’activité hello s’affiche.
20. **Set-AzureRmContext** a plusieurs jeux de paramètres, donc nous tooselect un avant que nous pouvons fournir des valeurs de paramètre.  Cliquez sur **paramètre la valeur** , puis sélectionnez hello **SubscriptionId** jeu de paramètres.  
21. Une fois que vous sélectionnez le jeu de paramètres hello, paramètres de hello s’affichent dans le panneau de Configuration de paramètre d’activité hello.  Cliquez sur **SubscriptionID**
22. Dans le panneau de la valeur du paramètre hello, sélectionnez **ressource de Variable** pour hello **source de données** et sélectionnez **AzureSubscriptionId** à partir de la liste de hello, puis cliquez sur **OK**  à deux reprises.   
23. Placez le curseur sur **connexion tooAzure** jusqu'à ce qu’un cercle apparaît sous forme de hello hello. Cliquez sur le cercle de hello et faites glisser la flèche de hello trop**Id d’abonnement spécifier**.

Votre runbook doit ressembler à hello suivant à ce stade : <br>![Configuration de l’authentification de runbook](media/automation-first-runbook-graphical/runbook-auth-config.png)

## <a name="step-7---add-activity-toostart-a-virtual-machine"></a>Étape 7 : ajouter l’activité toostart une machine virtuelle
Ici, nous ajoutons un **Start-AzureRmVM** toostart d’activité une machine virtuelle.  Vous pouvez choisir n’importe quel ordinateur virtuel dans votre abonnement Azure et pour maintenant vous codez nom dans l’applet de commande hello.

1. Dans le contrôle de la bibliothèque de hello, tapez **Start-Azure Resource Manager** dans la zone de texte Rechercher hello.
2. Ajouter **Start-AzureRmVM** toohello canevas puis cliquez et faites-le glisser en dessous **Id d’abonnement spécifier**.
3. Placez le curseur sur **Id d’abonnement spécifier** jusqu'à ce qu’un cercle apparaît sous forme de hello hello.  Cliquez sur le cercle de hello et faites glisser la flèche de hello trop**Start-AzureRmVM**.
4. Sélectionnez **Start-AzureRmVM**.  Cliquez sur **paramètres** , puis **paramètre la valeur** tooview hello définit pour **Start-AzureRmVM**.  Sélectionnez hello **ResourceGroupNameParameterSetName** jeu de paramètres. Notez que des points d’exclamation apparaissent en regard des paramètres **ResourceGroupName** et **Name**.  Ils indiquent que ces paramètres sont obligatoires.  Notez également que les deux attendent des valeurs de chaîne.
5. Sélectionnez **Name**.  Sélectionnez **expression PowerShell** pour hello **source de données** et tapez Bonjour nom d’ordinateur virtuel de hello entouré de guillemets doubles qui nous commençons avec ce runbook.  Cliquez sur **OK**.<br>![Valeur du paramètre Name Start-AzureRmVM](media/automation-first-runbook-graphical/runbook-startvm-nameparameter.png)
6. Sélectionnez **ResourceGroupName**. Utilisez **expression PowerShell** pour hello **source de données** et tapez Bonjour nom du groupe de ressources hello entouré de guillemets doubles.  Cliquez sur **OK**.<br> ![Paramètres Start-AzureRmVM](media/automation-first-runbook-graphical/startazurermvm-params.png)
7. Cliquez sur volet de Test afin que nous puissions tester hello runbook.
8. Cliquez sur **Démarrer** test de hello toostart.  Une fois terminée, vérifiez que l’ordinateur virtuel hello a été démarré.

Votre runbook doit ressembler à hello suivant à ce stade : <br>![Configuration de l’authentification de runbook](media/automation-first-runbook-graphical/runbook-startvm.png)

## <a name="step-8---add-additional-input-parameters-toohello-runbook"></a>Étape 8 - ajouter des paramètres d’entrée supplémentaires toohello runbook
Notre runbook démarre actuellement hello virtual machine dans le groupe de ressources hello que nous avons spécifié dans hello **AzureRmVM de début** applet de commande.  Notre runbook peut être plus utile si nous pouvons spécifier à la fois au démarrage hello runbook.  Nous ajoutons maintenant des paramètres d’entrée toohello runbook tooprovide cette fonctionnalité.

1. Éditeur graphique de hello ouvrir en cliquant sur **modifier** sur hello **MyFirstRunbook** volet.
2. Cliquez sur **d’entrée et de sortie** , puis **Ajout de l’entrée** volet de paramètre d’entrée du Runbook tooopen hello.<br> ![Entrée et sortie de Runbook](media/automation-first-runbook-graphical/runbook-toolbar-InputandOutput-revised20165.png)
3. Spécifiez *VMName* pour hello **nom**.  Conserver *chaîne* pour hello **Type**, mais modifier **obligatoire** trop*Oui*.  Cliquez sur **OK**.
4. Créez un paramètre d’entrée obligatoire ensuite appelé *ResourceGroupName* puis cliquez sur **OK** tooclose hello **d’entrée et sortie** volet.<br> ![Paramètres d'entrée de Runbook](media/automation-first-runbook-graphical/start-azurermvm-params-outputs.png)
5. Sélectionnez hello **Start-AzureRmVM** activité, puis cliquez sur **paramètres**.
6. Hello de modification **source de données** pour **nom** trop**Runbook entrée** , puis sélectionnez **VMName**.<br>
7. Hello de modification **source de données** pour **ResourceGroupName** trop**Runbook entrée** , puis sélectionnez **ResourceGroupName**.<br> ![Paramètres Start-AzureVM](media/automation-first-runbook-graphical/start-azurermvm-params-runbookinput.png)
8. Enregistrer les runbook hello et ouvrir le volet de Test hello.  Notez que vous pouvez maintenant fournir des valeurs pour hello deux variables d’entrée que vous utilisez dans le test de hello.
9. Volet de Test hello fermer.
10. Cliquez sur **publier** toopublish hello nouvelle version du runbook de hello.
11. Arrêter la machine virtuelle hello que vous avez démarrées à l’étape précédente de hello.
12. Cliquez sur **Démarrer** toostart hello runbook.  Type Bonjour **VMName** et **ResourceGroupName** pour la machine virtuelle de hello que vous allez toostart.<br> ![Start Runbook](media/automation-first-runbook-graphical/runbook-start-inputparams.png)
13. Lorsque hello runbook est terminée, vérifiez que l’ordinateur virtuel hello a été démarré.

## <a name="step-9---create-a-conditional-link"></a>Étape 9 - Création d’un lien conditionnel
Nous avons à présent modifier hello runbook afin qu’il tente uniquement toostart hello virtual machine s’il n’est pas déjà démarré.  Pour cela, vous devez ajouter un **Get-AzureRmVM** runbook toohello applet de commande qui obtient l’état de niveau de l’instance de la machine virtuelle de hello hello. Puis vous ajoutez un module de code PowerShell Workflow appelé **obtenir le statut** avec PowerShell un extrait de code de toodetermine hello ordinateur virtuel est en cours d’exécution ou arrêté.  Un lien conditionnel de hello **obtenir le statut** module s’exécute uniquement **Start-AzureRmVM** si l’état d’exécution actuel hello est arrêté.  Enfin, nous avons un tooinform message si hello machine virtuelle a été démarrée correctement ou non à l’aide hello applet de commande PowerShell Write-Output de sortie.

1. Ouvrez **MyFirstRunbook** dans l’éditeur graphique de hello.
2. Supprimer le lien entre hello **spécifiez Id d’abonnement** et **Start-AzureRmVM** en cliquant dessus et en appuyant sur hello *supprimer* clé.
3. Dans le contrôle de la bibliothèque de hello, tapez **Get-AzureRm** dans la zone de texte Rechercher hello.
4. Ajouter **Get-AzureRmVM** toohello la zone de dessin.
5. Sélectionnez **Get-AzureRmVM** , puis **paramètre la valeur** tooview hello définit pour **Get-AzureRmVM**.  Sélectionnez hello **GetVirtualMachineInResourceGroupNameParamSet** jeu de paramètres.  Notez que des points d’exclamation apparaissent en regard des paramètres **ResourceGroupName** et **Name**.  Ils indiquent que ces paramètres sont obligatoires.  Notez également que les deux attendent des valeurs de chaîne.
6. Pour le paramètre **Name** sous **Source de données**, sélectionnez **Entrée du Runbook** puis **VMName**.  Cliquez sur **OK**.
7. Pour le paramètre **ResourceGroupName** sous **Source de données**, sélectionnez **Entrée de Runbook**, puis **ResourceGroupName**.  Cliquez sur **OK**.
8. Pour le paramètre **Status** sous **Source de données**, sélectionnez **Valeur constante**, puis cliquez sur **True**.  Cliquez sur **OK**.  
9. Créer un lien à partir de **Id d’abonnement spécifier** trop**Get-AzureRmVM**.
10. Dans le contrôle de la bibliothèque hello, développez **contrôle de Runbook** et ajoutez **Code** toohello la zone de dessin.  
11. Créer un lien à partir de **Get-AzureRmVM** trop**Code**.  
12. Cliquez sur **Code** et dans le volet de Configuration hello, étiquette également modifier**obtenir le statut de**.
13. Sélectionnez **Code** paramètre et hello **éditeur de Code** panneau s’affiche.  
14. Dans l’éditeur de code hello, collez hello suivant extrait de code :
    
     ```
     $StatusesJson = $ActivityOutput['Get-AzureRmVM'].StatusesText
     $Statuses = ConvertFrom-Json $StatusesJson
     $StatusOut =""
     foreach ($Status in $Statuses){
     if($Status.Code -eq "Powerstate/running"){$StatusOut = "running"}
     elseif ($Status.Code -eq "Powerstate/deallocated") {$StatusOut = "stopped"}
     }
     $StatusOut
     ```
15. Créer un lien à partir de **obtenir le statut** trop**Start-AzureRmVM**.<br> ![Runbook avec module de code](media/automation-first-runbook-graphical/runbook-startvm-get-status.png)  
16. Sélectionnez le lien de hello et dans le volet de Configuration hello, modifiez **appliquer la condition** trop**Oui**.   Lien de hello note active ligne tooa en pointillé indiquant qu’activité de cible de hello s’exécute uniquement si la condition de hello résout tootrue.  
17. Pourquoi **expression de Condition**, type *$ActivityOutput [« obtenir le statut'] - eq « Stopped »*.  **Start-AzureRmVM** exécute désormais uniquement si l’ordinateur virtuel de hello est arrêté.
18. Bonjour contrôle de la bibliothèque, développez **applets de commande** , puis **Microsoft.PowerShell.Utility**.
19. Ajouter **Write-Output** canevas toohello à deux reprises.<br> ![Runbook avec Write-Output](media/automation-first-runbook-graphical/runbook-startazurermvm-complete.png)
20. Sur hello première **Write-Output** contrôler, cliquez sur **paramètres** et modifiez hello **étiquette** valeur trop*notifier le démarrage de machine virtuelle*.
21. Pour **InputObject**, modifiez **source de données** trop**expression PowerShell** et tapez Bonjour expression *« $VMName a démarré ».* .
22. Sur hello deuxième **Write-Output** contrôler, cliquez sur **paramètres** et modifiez hello **étiquette** valeur trop*notifier VM Démarrer a échoué*
23. Pour **InputObject**, modifiez **source de données** trop**expression PowerShell** et tapez Bonjour expression *« $VMName ne peut pas démarrer ».* .
24. Créer un lien à partir de **Start-AzureRmVM** trop**notifier le démarrage de machine virtuelle** et **notifier VM démarrer échec**.
25. Sélectionnez le lien de hello trop**notifier le démarrage de machine virtuelle** et modifiez **appliquer la condition** trop**True**.
26. Pourquoi **expression de Condition**, type *$ActivityOutput [« Start-AzureRmVM']. IsSuccessStatusCode - eq $true*.  Cette Write-Output contrôler s’exécute désormais uniquement si l’ordinateur virtuel de hello a démarré correctement.
27. Sélectionnez le lien de hello trop**notifier VM démarrer échec** et modifiez **appliquer la condition** trop**True**.
28. Pourquoi **expression de Condition**, type *$ActivityOutput [« Start-AzureRmVM']. IsSuccessStatusCode - ne $true*.  Cette Write-Output contrôler maintenant ne fonctionne que si l’ordinateur virtuel de hello n’est pas démarré avec succès.
29. Enregistrer les runbook hello et ouvrir le volet de Test hello.
30. Démarrer hello runbook avec l’ordinateur virtuel de hello s’est arrêté, et il doit commencer.

## <a name="next-steps"></a>Étapes suivantes
* toolearn plus sur la création de graphiques, consultez [création graphique dans Azure Automation](automation-graphical-authoring-intro.md)
* tooget main runbook PowerShell, consultez [mon premier runbook de PowerShell](automation-first-runbook-textual-powershell.md)
* tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md)

