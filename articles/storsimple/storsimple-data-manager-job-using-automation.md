---
title: aaaUse Azure Automation tootrigger un travail | Documents Microsoft
description: "Découvrez comment toouse Azure Automation pour déclencher des travaux du Gestionnaire de données de StorSimple (aperçu privé)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a>Utilisez Azure Automation tootrigger un travail (aperçu privé)

Cet article explique comment toouse Azure Automation tootrigger une tâche du Gestionnaire de données de StorSimple.

## <a name="prerequisites"></a>Composants requis

Avant de commencer, assurez-vous de satisfaire les exigences suivantes :

*   Azure Powershell installé. [Téléchargez Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Configuration travail paramètres de tooinitialize hello Transformation de données (instructions tooobtain ces paramètres sont inclus ici).
*   Une définition de travail qui a été configurée correctement dans une ressource de données hybride dans un groupe de ressources.
*   Télécharger `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) fichier à partir du référentiel github de hello.
*   Télécharger `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) à partir du référentiel github de hello.
*   Télécharger `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) à partir du référentiel github de hello.

## <a name="step-by-step"></a>Procédure pas à pas

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a>Obtenir les autorisations de Azure Active Directory pour la définition de tâche du travail toorun hello hello automation

1. paramètres de configuration tooretrieve hello pour Active Directory, procédez comme hello comme suit :

    1. Ouvrez Windows PowerShell sur votre ordinateur local. Vérifiez que [Azure PowerShell](https://azure.microsoft.com/downloads/) est installé.
    1. Exécutez hello `Get-ConfigurationParams.ps1` script (dans le dossier hello vous avez téléchargé). Tapez hello commande dans la fenêtre de hello PowerShell suivante :

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        Hello ActiveDirectoryKey est un mot de passe que vous utilisez plus tard. Entrez un mot de passe de votre choix. N’importe quelle chaîne peut être utilisée pour AppName.

2. Ce script génère hello valeurs qui doivent être utilisés lors du déclenchement du runbook automation de hello suivantes. Prenez note de ces valeurs.

    - ID client
    - ID client
    - Clé Active Directory (identique à une entrée ci-dessus hello)
    - Identifiant d’abonnement

### <a name="set-up-hello-automation-account"></a>Configurer hello compte Automation

1. Connectez-vous à tooAzure et ouvrez votre compte Automation.
2. Cliquez sur **actifs** vignette tooopen hello liste de ressources.
3. Cliquez sur **Modules** vignette tooopen hello liste des modules.
4. Cliquez sur **+ ajouter un module** Panneau de module ajouter bouton et hello est lancée.

    ![Paramètres du compte Automation](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. Une fois que vous avez sélectionné hello `DataTransformationApp.zip` de fichiers à partir de votre ordinateur local, cliquez sur **OK** module de hello tooimport.

   Lorsque Azure Automation importe un compte tooyour de module, il extrait les métadonnées sur le module de hello. Cette opération peut prendre plusieurs minutes.

   ![Paramètres du compte Automation](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. Vous recevez une notification indiquant que le module hello est en cours de déploiement et une autre notification lorsque hello est terminée.  Vous pouvez également vérifier l’état de hello **Modules** vignette.

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a>tooimport hello runbook qui déclenche la définition de la tâche hello

1. Bonjour portail Azure, ouvrez votre compte Automation.
2. Cliquez sur **Runbooks** vignette tooopen hello liste des runbooks.
3. Cliquez sur **+ Ajouter un runbook**, puis sur **Importer un Runbook existant**.

   ![Importer un runbook existant](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. Cliquez sur **fichier de Runbook** et sélectionnez hello fichier tooimport `Trigger-DataTransformation-Job.ps1`.
5. Cliquez sur **créer** tooimport hello runbook. Hello nouveau runbook apparaît dans la liste hello des procédures opérationnelles pour hello compte Automation.
7. Cliquez sur le runbook **Trigger-DataTransformation-Job**, puis sur **Modifier**.
8. Cliquez sur **Publier**, puis sur **Oui** lorsque vous êtes invité à confirmer l’opération.


### <a name="toorun-hello-runbook"></a>toorun hello runbook :
1. Bonjour portail Azure, ouvrez votre compte Automation.
2. Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.
3. Cliquez sur **Trigger-DataTransformation-Job**.
4. Cliquez sur **Démarrer** toostart hello runbook.

   ![Démarrer un Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. Bonjour **démarrer runbook** panneau, entrez tous les paramètres de hello. Cliquez sur **OK** tâche de Transformation des données toosubmit hello.

   ![Démarrer un Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a>Étapes suivantes

[Utilisez l’interface utilisateur de gestionnaire de données StorSimple tootransform vos données](storsimple-data-manager-ui.md).
