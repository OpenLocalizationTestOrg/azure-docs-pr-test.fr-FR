---
title: "aaaAzure intégration du contrôle Source Automation avec GitHub Enterprise | Documents Microsoft"
description: "Décrit les détails hello d’intégration tooconfigure GitHub Enterprise pour le contrôle de code source de runbooks Automation."
services: automation
documentationCenter: 
authors: mgoedtel
manager: jwhit
editor: 
ms.assetid: e01d817c-7d38-421c-adf5-647a4b526eb4
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: magoedte
ms.openlocfilehash: 915d36ccabb72fdee1dba663049a0b331249cd73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a>Scénario Azure Automation - Intégration du contrôle de code source Automation avec GitHub Enterprise

Automation prend actuellement en charge l’intégration du contrôle de code source, qui vous permet de runbooks tooassociate dans votre référentiel de contrôle de code source Automation compte tooa GitHub.  Toutefois, les clients qui ont déployé [GitHub Enterprise](https://enterprise.github.com/home) toosupport pratiques de leur DevOps, également toouse il toomanage hello du cycle de vie des procédures opérationnelles qui sont développées tooautomate des processus d’entreprise et de gestion des services opérations.  

Dans ce scénario, vous disposez d’un ordinateur de Windows dans votre centre de données configurée comme un Runbook Worker hybride avec les modules du Gestionnaire de ressources Azure hello et des outils Git.  ordinateur de travail hybride Hello a un clone de référentiel Git hello.  Lorsque hello runbook est exécuté sur un worker hybride hello, hello Git Active synchronisé et le contenu du fichier runbook hello est importé dans hello compte Automation.

Cet article décrit comment tooset cette configuration dans votre environnement Azure Automation. Nous allons commencer par la configuration de l’Automation avec les informations d’identification de sécurité hello, procédures opérationnelles requis toosupport ce scénario et déploiement d’un Runbook Worker hybride dans vos données center toorun hello runbooks et accéder à votre toosynchronize de référentiel GitHub Enterprise procédures opérationnelles avec votre compte Automation.  


## <a name="getting-hello-scenario"></a>Scénario de hello mise en route

Ce scénario se compose de deux procédures opérationnelles PowerShell que vous pouvez importer directement à partir de hello [galerie de runbooks](automation-runbook-gallery.md) dans hello portail Azure ou les télécharger à partir de hello [PowerShell Gallery](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbooks

Runbook | Description| 
--------|------------|
Export-RunAsCertificateToHybridWorker | Runbook exporte un certificat d’identification à partir d’un processus de travail hybride de tooa compte Automation afin que les procédures opérationnelles sur le travail de hello peut s’authentifier avec Azure dans l’ordre tooimport runbooks dans hello compte Automation.| 
Sync-LocalGitFolderToAutomationAccount | Les synchronisations Runbook hello dossier Git local sur l’ordinateur de hybride hello, puis importer les fichiers de runbook de hello (*.ps1) dans le compte d’automatisation hello.|

### <a name="credentials"></a>Informations d'identification

Informations d'identification | Description|
-----------|------------|
GitHRWCredential | Ressource d’informations d’identification vous créez le nom d’utilisateur de toocontain hello et un mot de passe pour un utilisateur avec worker hybride de toohello autorisations.|

## <a name="installing-and-configuring-this-scenario"></a>Installation et configuration de ce scénario

### <a name="prerequisites"></a>Composants requis

1. Hello LocalGitFolderToAutomationAccount de synchronisation runbook s’authentifie à l’aide de hello [Azure exécuter en tant que compte](automation-sec-configure-azure-runas-account.md). 

2. Un espace de travail de Microsoft Operations Management Suite (OMS) avec hello solution Azure Automation activée et configurée est également requis.  Si vous n’avez pas celui qui est associé à hello Automation compte utilisé tooinstall et configurer ce scénario, il est créé et configuré pour vous lorsque vous exécutez hello **New-OnPremiseHybridWorker.ps1** script à partir de hybride de hello travail de runbook.        

    > [!NOTE]
    > Actuellement hello régions suivantes prennent uniquement en charge l’intégration Automation avec OMS - **sud-est de l’Australie**, **est des États-Unis 2**, **Asie du Sud-est**, et **ouest Europe**. 

3. Un ordinateur pouvant servir d’un travail de Runbook hybride dédié qui hébergera les logiciels de GitHub hello et mettre à jour les fichiers de runbook hello également (*runbook*.ps1) dans un répertoire source sur toosynchronize de système de fichiers hello entre GitHub et votre Compte Automation.

### <a name="import-and-publish-hello-runbooks"></a>Importer et publier des runbooks de hello

tooimport hello *Export-RunAsCertificateToHybridWorker* et *LocalGitFolderToAutomationAccount de synchronisation* runbooks à partir de hello galerie de runbooks à partir de votre compte Automation Bonjour portail Azure, Suivez les procédures de hello dans [Runbook d’importation à partir de la galerie de runbooks de hello](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal). La publication de runbooks de hello après que qu’ils ont été correctement importés dans votre compte Automation.

### <a name="deploy-and-configure-hybrid-runbook-worker"></a>Déployer et configurer un Runbook Worker hybride

Si vous ne disposez pas d’un travail de Runbook hybride déjà déployés dans votre centre de données, vous devez passer en revue les exigences de hello et suivez les étapes d’installation hello automatisée à l’aide de la procédure hello dans [Azure Automation Workers hybrides - automatiser l’installation Configuration et](automation-hybrid-runbook-worker.md#automated-deployment).  Vous avez correctement installé worker hybride de hello sur un ordinateur, vous effectuerez hello suivant les étapes toocomplete son toosupport configuration ce scénario.

1. Inscrivez-vous toohello hébergement hello Runbook Worker hybride rôle d’ordinateur avec un compte disposant des droits d’administrateur local et créer un fichier de runbook Active toohold hello Git.  Clone hello interne Git toohello répertoire du référentiel.
2. Si vous n’avez pas déjà un compte d’identification créé ou toocreate un dédié à cette fin, à partir de hello portail Azure accédez tooAutomation comptes, sélectionnez votre compte Automation et créer un [actif d’informations d’identification](automation-credentials.md) qui contient le nom d’utilisateur hello et un mot de passe pour un utilisateur avec le travail d’autorisations toohello hybride.  
3. À partir de votre compte Automation, [modifier hello runbook](automation-edit-textual-runbook.md)**Export-RunAsCertificateToHybridWorker** et modifier la valeur hello pour la variable de hello *$Password* avec un nom fort mot de passe.    Après avoir modifié la valeur de hello, cliquez sur **publier** brouillon toohave hello de hello runbook publié. 
5. Démarrer hello runbook **Export-RunAsCertificateToHybridWorker**et Bonjour **démarrer le Runbook** panneau, sous l’option de hello **des paramètres d’exécution** sélectionnez l’option hello **Worker hybride** et dans le groupe worker hello liste déroulante, sélectionnez hello hybride vous avez créé précédemment pour ce scénario.  

    Cette opération exporte un worker hybride de toohello certificat afin que les procédures opérationnelles sur le travail de hello peut s’authentifier avec Azure à l’aide de hello exécuter en tant que connexion dans l’ordre toomanage des ressources Azure (en particulier pour ce scénario - importation runbooks toohello compte Automation).

4. À partir de votre compte Automation, sélectionnez hello le groupe worker hybride créé précédemment et [spécifier un compte d’identification](automation-hrw-run-runbooks.md#runas-account) pour le groupe de travail hybride hello et d’élément multimédia d’informations d’identification choisi hello uniquement ou déjà avoir créé.  Cela garantit que ce runbook de synchronisation hello peut exécuter des commandes de Git. 
5. Démarrer hello runbook **LocalGitFolderToAutomationAccount de synchronisation**, fournir suivant de hello requise des valeurs de paramètre d’entrée et Bonjour **démarrer le Runbook** panneau, sous l’option de hello **exécuter paramètres** l’option hello **Worker hybride** et dans le groupe worker hello liste déroulante, sélectionnez hello hybride vous avez créé précédemment pour ce scénario :
    * *Le groupe de ressources* hello - nom de votre groupe de ressources associé à votre compte Automation
    * *AutomationAccountName* hello - nom de votre compte Automation
    * *GitPath* - hello dossier local ou de fichiers sur hello où Git est paramétré à toopull dernières modifications dans un Runbook Worker hybride

    Cela synchroniser hello Git dossier local sur ordinateur de travail hybride hello et puis importer les fichiers .ps1 hello hello source directory toohello compte Automation.

    ![Démarrer le runbook Sync-LocalGitFolderToAutomationAccount](media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. Afficher les détails de résumé de travail pour les runbook hello en le sélectionnant dans hello **Runbooks** panneau dans votre compte Automation, puis sélectionnez hello **travaux** vignette.  Vérifiez qu’il a réussi en sélectionnant hello **tous les journaux** vignette et flux de journal détaillé hello révision.  

## <a name="next-steps"></a>Étapes suivantes

-  tooknow en savoir plus sur les types de runbook, leurs avantages et les limitations, consultez [types de runbook Azure Automation](automation-runbook-types.md)
-  Pour plus d’informations sur la fonctionnalité de prise en charge de script PowerShell, consultez [Prise en charge de script PowerShell natif dans Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
