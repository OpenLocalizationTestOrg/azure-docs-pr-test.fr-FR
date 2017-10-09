---
title: "aaaSource l’intégration du contrôle dans Azure Automation | Documents Microsoft"
description: "Cet article décrit l’intégration du contrôle de code source avec GitHub dans Azure Automation."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 224d7375-9887-44dd-b137-06ffe396a4b4
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 6ceee1de8065fafe85a13bbd7f585e74dbc96b47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Intégration du contrôle de code source dans Azure Automation
Intégration du contrôle de code source vous permet de runbooks tooassociate dans votre référentiel de contrôle de code source Automation compte tooa GitHub. Contrôle de code source vous permet de tooeasily collaborer avec votre équipe, le suivi des modifications et restaurer des versions tooearlier de vos runbook. Par exemple, contrôle de code source permet de vous toosync différentes branches de contrôle de code source comptes Automation de développement, test ou production tooyour, rendant toopromote facilement le code qui a été testé dans votre automatisation de la production de tooyour environnement de développement compte.

Contrôle de code source vous permet de code toopush du contrôle de code Azure Automation toosource ou extraire vos runbook à partir du contrôle de code source tooAzure Automation. Cet article décrit comment contrôler les tooset source dans votre environnement Azure Automation. Nous allons commencer par configurer Azure Automation tooaccess votre référentiel GitHub et parcourir les différentes opérations qui peuvent être effectuées à l’aide de l’intégration du contrôle source. 

> [!NOTE]
> Le contrôle de code source prend en charge l’extraction et la transmission de [Runbooks de workflow PowerShell](automation-runbook-types.md#powershell-workflow-runbooks), ainsi que de [Runbooks PowerShell](automation-runbook-types.md#powershell-runbooks). Les [Runbooks graphiques](automation-runbook-types.md#graphical-runbooks) ne sont pas encore pris en charge.<br><br>
> 
> 

Il existe deux étapes simples requis tooconfigure contrôle de code source pour votre compte Automation et une seule si vous avez déjà un compte GitHub. Il s'agit de :

## <a name="step-1--create-a-github-repository"></a>Étape 1 : Création d’un référentiel GitHub
Si vous avez déjà un compte GitHub et un espace de stockage que vous souhaitez toolink tooAzure Automation, puis tooyour de connexion existante et démarrer à partir de l’étape 2 ci-dessous. Dans le cas contraire, accédez trop[GitHub](https://github.com/), inscrivez-vous pour un nouveau compte et [créer un nouveau référentiel](https://help.github.com/articles/create-a-repo/).

## <a name="step-2--set-up-source-control-in-azure-automation"></a>Étape 2 : Configuration du contrôle de code source dans Azure Automation
1. Dans le panneau de compte Automation hello Bonjour portail Azure, cliquez sur **configuration des contrôle de code Source.** 
   
    ![Définition du contrôle de code source](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. Hello **contrôle de code Source** panneau s’ouvre, où vous pouvez configurer les détails de votre compte GitHub. Vous trouverez ci-dessous la liste de hello de paramètres tooconfigure :  
   
   | **Paramètre** | **Description** |
   |:--- |:--- |
   | Choisir une source |Sélectionnez la source de hello. Actuellement, seul **GitHub** est pris en charge. |
   | Autorisation |Cliquez sur hello **Authorize** référentiel GitHub de bouton toogrant Azure Automation accès tooyour. Si vous êtes déjà connecté tooyour compte GitHub dans une autre fenêtre, puis hello les informations d’identification de ce compte sont utilisées. Une fois que l’autorisation a réussi, panneau de hello affiche votre nom d’utilisateur GitHub sous **d’autorisation propriété**. |
   | Choisir un référentiel |Sélectionnez un référentiel GitHub à partir de la liste de hello des référentiels disponibles. |
   | Choisir une branche |Sélectionnez la branche à partir de la liste hello de branches disponibles. Hello uniquement **master** branche s’affiche si vous n’avez pas créé une branche. |
   | Chemin d’accès au dossier de runbooks |chemin d’accès de dossier de runbook Hello Spécifie le chemin d’accès de l’hello dans le référentiel de GitHub hello à partir de laquelle vous voulez toopush ou par extraction de votre code. Il doit être entré au format de hello **/NomDossier/nomsousdossier**. Seuls les runbooks du chemin d’accès de dossier de runbook hello seront synchronisé tooyour compte Automation. Procédures opérationnelles dans les sous-dossiers de hello du chemin d’accès de dossier de runbook hello seront **pas** synchronisés. Utilisez  **/**  toosync tous hello procédures opérationnelles sous référentiel de hello. |
3. Par exemple, si vous disposez d’un référentiel nommé **PowerShellScripts** qui contient un dossier nommé **RootFolder**, lequel contient un dossier nommé **SubFolder**. Vous pouvez utiliser hello suivant chaînes toosync chaque au niveau du dossier :
   
   1. runbooks toosync de **référentiel**, chemin d’accès du dossier de runbook*/*
   2. runbooks toosync de **RootFolder**, chemin d’accès du dossier de runbook est */RootFolder*
   3. runbooks toosync de **sous-dossier**, chemin d’accès du dossier de runbook est *RootFolder/sous-dossier*.
4. Une fois que vous configurez les paramètres de hello, ils sont affichés sur hello **Panneau de configuration des contrôle de code Source.**  
   
    ![Panneau Configurer](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. Une fois que vous avez cliqué sur OK, l’intégration du contrôle de code source est configurée pour votre compte Automation et doit être mise à jour avec vos informations GitHub. Vous pouvez maintenant cliquer sur cette tooview partie tous de votre contrôle de source de l’historique des travaux de synchronisation.  
   
    ![Valeurs du référentiel](media/automation-source-control-integration/automation_03_RepoValues.png)
6. Après avoir configuré le contrôle de code source, hello ressources Automation suivantes seront créés dans votre compte Automation :  
   Deux [composants variables](automation-variables.md) sont créés.  
   
   * variable de Hello **Microsoft.Azure.Automation.SourceControl.Connection** contient des valeurs hello hello chaîne de connexion, comme indiqué ci-dessous.  
     
     | **Paramètre** | **Valeur** |
     |:--- |:--- |
     | Nom |Microsoft.Azure.Automation.SourceControl.Connection |
     | Type |String |
     | Valeur |{"Branch" :\<*Nom de votre branche*>,"RunbookFolderPath" :\<*Chemin d’accès au dossier de Runbooks*>,"ProviderType" :\<*possède une valeur 1 pour GitHub*>,"Repository" :\<*Nom de votre référentiel*>,"Username" :\<*Votre nom d’utilisateur GitHub*>} |

    * variable de Hello **Microsoft.Azure.Automation.SourceControl.OAuthToken**, contient la valeur chiffrée de hello sécurisé de votre OAuthToken.  

    |**Paramètre**            |**Valeur** |
    |:---|:---|
    | Nom  | Microsoft.Azure.Automation.SourceControl.OauthToken |
    | Type | Inconnue (chiffrée) |
    | Valeur | <*OAuthToken chiffré*> |  

    ![variables](media/automation-source-control-integration/automation_04_Variables.png)  

    * **Contrôle de code Source Automation** est ajouté en tant qu’une application autorisée de tooyour compte GitHub. application de hello tooview : à partir de votre page d’accueil GitHub, accédez à tooyour **profil** > **paramètres** > **Applications**. Cette application permet à Azure Automation toosync votre tooan de référentiel GitHub compte Automation.  

    ![Application Git](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>Utilisation du contrôle de code source dans Automation
### <a name="check-in-a-runbook-from-azure-automation-toosource-control"></a>Archivage à un runbook à partir du contrôle de toosource Azure Automation
Archiver le Runbook vous permet de toopush hello apportées tooa runbook dans Azure Automation dans votre référentiel de contrôle de code source. Voici les étapes de hello toocheck dans un runbook :

1. À partir de votre compte Automation, [créez un Runbook textuel](automation-first-runbook-textual.md) ou [modifiez un Runbook textuel existant](automation-edit-textual-runbook.md). Ce runbook peut être un flux de travail PowerShell ou un runbook de script PowerShell.  
2. Une fois que vous modifiez votre runbook, enregistrez-le, puis cliquez sur **archivage** de hello **modifier** panneau.  
   
    ![Bouton d’archivage](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > Archivage d’Azure Automation remplacera code hello qui existent actuellement dans votre contrôle de code source. Hello instruction de ligne de commande Git dans toocheck est **git ajouter + validation git + git push**  

1. Lorsque vous cliquez sur **archivage**, vous serez invité avec un message de confirmation, cliquez sur Oui toocontinue.  
   
    ![Message d’archivage](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. Archiver démarre hello runbook de contrôle de code source : **MicrosoftAzureAutomationAccountToGitHubV1 de synchronisation**. Ce runbook connecte tooGitHub et exécute un push des modifications à partir du référentiel de tooyour Azure Automation. tooview hello archiver l’historique des travaux, de revenir en arrière toohello **intégration du contrôle de code Source** onglet et cliquez sur Panneau de synchronisation du référentiel tooopen hello. Ce panneau affiche toutes vos tâches de contrôle de code source.  Sélectionnez la tâche hello tooview et cliquez sur Détails de hello tooview.  
   
    ![Runbook d’archivage](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > Les runbooks de contrôle de code source sont des runbooks Automation spéciaux que vous ne pouvez pas afficher ni modifier. Ils n’apparaîtront pas dans votre liste de runbooks, mais les tâches de synchronisation apparaîtront dans votre liste de tâches.
   > 
   > 
3. nom de Hello du runbook de hello modifié est envoyé en tant qu’un toohello archivage runbook de paramètre d’entrée. Vous pouvez [afficher les détails du travail hello](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) en développant des runbook dans **référentiel synchronisation** panneau.  
   
    ![Entrée d’archivage](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. Actualiser votre référentiel GitHub, une fois que les modifications de hello tooview de fin de travail de hello.  Il doit y avoir une validation de votre référentiel avec un message de validation : **mise à jour *le nom du Runbook* dans Azure Automation.**  

### <a name="sync-runbooks-from-source-control-tooazure-automation"></a>Synchronisation des runbooks à partir du contrôle de code source tooAzure Automation
bouton de synchronisation Hello sur le panneau de synchronisation du référentiel hello vous permet de toopull tous hello runbooks dans le chemin d’accès du dossier de runbook hello de votre référentiel de tooyour compte Automation. Hello même référentiel peut être synchronisé toomore à un compte Automation. Voici un runbook hello étapes toosync :

1. À partir de hello compte Automation où vous définissez contrôle de code source, ouvrez hello **Panneau de synchronisation de l’intégration/référentiel de contrôle Source** et cliquez sur **synchronisation** puis vous demandera une confirmation message, cliquez sur **Oui** toocontinue.  
   
    ![Bouton de synchronisation](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. La synchronisation démarre hello runbook : **MicrosoftAzureAutomationAccountFromGitHubV1 de synchronisation**. Ce runbook connecte tooGitHub et extrait les modifications hello à partir de votre référentiel de tooAzure Automation. Vous devez voir une nouvelle tâche sur hello **référentiel synchronisation** panneau pour cette action. tooview plus d’informations sur la tâche de synchronisation hello, cliquez sur Panneau de détails du travail tooopen hello.  
   
    ![Runbook de synchronisation](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > Une synchronisation à partir du contrôle de code source remplace hello brouillon du runbook hello qui existent actuellement dans votre compte Automation pour **tous les** procédures opérationnelles qui sont en cours de contrôle de code source. Hello Git toosync d’instruction de ligne de commande est **extraction git**


## <a name="troubleshooting-source-control-problems"></a>Résolution des problèmes de contrôle de code source
S’il existe des erreurs avec un travail de l’archivage ou la synchronisation, état de la tâche hello doit être suspendu et vous pouvez afficher plus de détails sur l’erreur de hello dans le panneau de tâche hello.  Hello **tous les journaux** partie va vous montrer toutes hello flux PowerShell associés à cette tâche. Cela fournit que des détails de hello nécessaire toohelp vous résolvez les problèmes avec votre archivage ou la synchronisation. Elle vous montrera également hello séquence d’actions qui s’est produite lors de la synchronisation ou un runbook dans la vérification.  

![Image AllLogs](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>Déconnexion du contrôle de code source
toodisconnect à partir de votre compte GitHub, ouvrir le panneau de synchronisation du référentiel hello et cliquez sur **déconnexion**. Une fois que vous vous déconnectez de contrôle de code source, les runbook qui ont été synchronisés précédemment reste dans votre compte Automation mais Panneau de synchronisation du référentiel hello n’est pas activé.  

  ![Bouton de déconnexion](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’intégration du contrôle de code source, consultez hello suivant des ressources :  

* [Azure Automation : Intégration du contrôle de code source dans Azure Automation](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [Voter pour votre système de contrôle de code source préféré](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Azure Automation : Intégration du contrôle de code source de Runbook à l’aide de Visual Studio Team Services](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

