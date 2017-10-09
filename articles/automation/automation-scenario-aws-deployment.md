---
title: "déploiement aaaAutomating d’une machine virtuelle dans Amazon Web Services | Documents Microsoft"
description: "Cet article explique comment toouse la création de tooautomate Azure Automation d’une machine virtuelle de Amazon Web Services"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a>Scénario Azure Automation – Approvisionner une machine virtuelle AWS
Dans cet article, nous allons montrer comment vous pouvez tirer parti de Azure Automation tooprovision une machine virtuelle dans votre abonnement Amazon Web Services (AWS) et nommez cette machine virtuelle spécifique – les AWS fait référence tooas « marquage « hello machine virtuelle.

## <a name="prerequisites"></a>Composants requis
Pour des raisons de hello de cet article, vous devez toohave un compte Azure Automation et un abonnement AWS. Pour plus d’informations sur la création d’un compte Azure Automation et sur sa configuration avec les informations d’identification de votre abonnement AWS, consultez l’article [Authentification des Runbooks avec Amazon Web Services](automation-configure-aws-account.md).  Ce compte doit être créé ou mis à jour avec vos informations d’identification d’abonnement AWS avant de continuer, car nous avons fait référence à ce compte dans les étapes de hello ci-dessous.

## <a name="deploy-amazon-web-services-powershell-module"></a>Déployer le module PowerShell Amazon Web Services
Notre approvisionnement de runbook d’ordinateur virtuel reposera hello AWS PowerShell module toodo son travail. Effectuer hello suivant les étapes tooadd hello module tooyour compte Automation qui est configuré avec vos informations d’identification AWS abonnement.  

1. Ouvrez votre navigateur web et accédez toohello [PowerShell Gallery](http://www.powershellgallery.com/packages/AWSPowerShell/) , puis cliquez sur hello **bouton d’Automation déployer tooAzure**.<br><br> ![Importation du module PS AWS](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)
2. Page de connexion Azure toohello s’affiche et après l’authentification, vous serez routé toohello portail Azure et présenté par hello suivant du panneau.<br><br> ![Panneau Importer un module](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. Sélectionnez hello groupe de ressources à partir de hello **groupe de ressources** déroulante liste et sur le panneau de paramètres hello, fournir hello informations suivantes :
   
   * À partir de hello **nouveau ou existant compte Automation (string)** liste déroulante, sélectionnez **existant**.  
   * Bonjour **nom du compte Automation (string)** zone, tapez dans le nom exact de hello Hello compte Automation qui inclut des informations d’identification hello pour votre abonnement AWS.  Par exemple, si vous avez créé un compte dédié nommé **AWSAutomation**, alors c’est ce que vous tapez dans la zone de hello.
   * Sélectionnez hello région appropriée à partir de hello **emplacement du compte Automation** liste déroulante.
4. Lorsque vous avez terminé d’entrer des informations hello requis, cliquez sur **créer**.
   
   > [!NOTE]
   > Lors de l’importation d’un module PowerShell dans Azure Automation, il est également extraction applets de commande hello et ces activités n’apparaissent que hello module est complètement terminé l’importation et l’extraction des applets de commande hello. Ce processus peut prendre plusieurs minutes.  
   > <br>
   > 
   > 
5. Bonjour portail Azure, ouvrez votre compte Automation référencé à l’étape 3.
6. Cliquez sur hello **actifs** vignette et hello **actifs** panneau, sélectionnez hello **Modules** vignette.
7. Sur hello **Modules** panneau vous verrez hello **AWSPowerShell** module dans la liste de hello.

## <a name="create-aws-deploy-vm-runbook"></a>Créer un runbook de machine virtuelle de déploiement AWS
Une fois hello QU'AWS PowerShell Module a été déployé, nous pouvons maintenant créer un tooautomate runbook approvisionner un ordinateur virtuel dans AWS à l’aide d’un script PowerShell. étapes Hello ci-dessous va vous montrer comment tooleverage PowerShell native de script dans Azure Automation.  

> [!NOTE]
> Pour plus d’options et d’informations sur ce script, consultez hello [PowerShell Gallery](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).
> 

1. Téléchargez les script PowerShell de hello AwsVM de nouveau à partir de hello galerie PowerShell en ouvrant une session PowerShell et en tapant hello suivante :<br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. À partir de hello portail Azure, ouvrez votre compte Automation, puis cliquez sur hello **Runbooks** vignette.  
3. À partir de hello **Runbooks** panneau, sélectionnez **ajouter un runbook**.
4. Sur hello **ajouter un runbook** panneau, sélectionnez **création rapide** (créer un runbook).
5. Sur hello **Runbook** panneau des propriétés, tapez un nom dans la zone de nom hello pour votre runbook et de hello **le type de Runbook** liste déroulante, sélectionnez **PowerShell**, puis cliquez sur  **Créer**.<br><br> ![Panneau Importer un module](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)
6. Lorsque le panneau de modifier le PowerShell Runbook hello s’affiche, copier- coller de script PowerShell hello dans runbook hello canevas de création.<br><br> ![Script PowerShell de runbook](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > Remarque suivant de hello lorsque vous travaillez avec l’exemple hello script PowerShell :
    > 
    > * Hello runbook contient un nombre de valeurs de paramètre par défaut. Veuillez évaluer toutes les valeurs par défaut et procéder aux mises à jour nécessaires.
    > * Si vous avez stocké vos informations d’identification AWS comme une ressource d’informations d’identification portant des noms différents à **AWScred**, vous devez script hello tooupdate ligne 57 toomatch en conséquence.  
    > * Lorsque vous travaillez hello commandes AWS CLI dans PowerShell, en particulier avec cet exemple de runbook, vous devez spécifier la région AWS hello. Sinon, les applets de commande hello risque d’échouer.  Afficher la rubrique AWS [spécifier la région de AWS](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) Bonjour AWS outils pour le document de PowerShell pour obtenir plus de détails.  
    >

7. tooretrieve une liste de noms d’images à partir de votre abonnement AWS, lancez PowerShell ISE, puis importer hello AWS PowerShell Module.  Authentifiez-vous auprès d’AWS en remplaçant **Get-AutomationPSCredential** dans votre environnement ISE par **AWScred = Get-Credential**.  Il vous sera demandé pour vos informations d’identification et vous pouvez fournir votre **ID de clé d’accès** pour le nom d’utilisateur hello et **clé d’accès Secret** mot de passe hello.  Consultez l’exemple hello ci-dessous :  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    Hello le résultat suivant :<br><br>
   ![Obtenir des images AWS](./media/automation-scenario-aws-deployment/powershell-ise-output.png)<br>  
8. Copiez et collez hello un des noms d’images hello dans une variable Automation référencés dans les runbook hello en tant que **$InstanceType**. Étant donné que dans cet exemple, nous utilisons hello AWS libre à plusieurs niveaux d’abonnement, nous allons utiliser **t2.micro** dans notre exemple de runbook.  
9. Enregistrer hello runbook, puis cliquez sur **publier** toopublish hello runbook, puis **Oui** lorsque vous y êtes invité.

### <a name="testing-hello-aws-vm-runbook"></a>Test hello AWS VM runbook
Avant de poursuivre avec les runbook hello test, nous devons tooverify quelques éléments. Plus précisément :  

* Un élément multimédia pour s’authentifier auprès de AWS a été créé appelé **AWScred** ou script de hello a été nom de hello tooreference mis à jour de votre élément multimédia d’informations d’identification.    
* module de AWS PowerShell Hello a été importé dans Azure Automation  
* Un runbook a été créé et les valeurs de paramètre ont été vérifiées et mises à jour lorsque c’était nécessaire  
* **Journaliser les enregistrements détaillés** et éventuellement **journaliser les informations de progression** sous hello runbook **journalisation et le suivi** ont été définies trop**sur**.<br><br> ![Journalisation et suivi de runbook](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)  

1. Nous souhaitez toostart hello runbook, cliquez sur **Démarrer** puis cliquez sur **OK** lorsque le panneau de démarrer le Runbook hello s’ouvre.
2. Dans Panneau de démarrer le Runbook hello, fournissez un **VMname**.  Accepter les valeurs par défaut de hello pour hello autres paramètres que vous avez préconfiguré dans le script de hello.  Cliquez sur **OK** tâche du runbook toostart hello.<br><br> ![Démarrer un runbook New-AwsVM](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)
3. Un volet de travail est ouvert pour la tâche du runbook hello que nous venons de créer. Fermez ce panneau.
4. Nous pouvons afficher la progression de la sortie de projet et afficher hello **flux** en sélectionnant hello **tous les journaux** vignette à partir du Panneau de travail de runbook hello.<br><br> ![Sortie de flux](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)
5. tooconfirm hello de machine virtuelle est en cours d’approvisionnement, connectez-vous à hello Console de gestion AWS si vous n’êtes pas actuellement connecté.<br><br> ![Machine virtuelle déployée par la console AWS](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a>Étapes suivantes
* tooget main runbooks graphiques, consultez [mon premier runbook graphique](automation-first-runbook-graphical.md)
* tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md)
* tooknow en savoir plus sur les types de runbook, leurs avantages et les limitations, consultez [types de runbook Azure Automation](automation-runbook-types.md)
* Pour plus d’informations sur la fonctionnalité de prise en charge de script PowerShell, consultez [Prise en charge de script PowerShell natif dans Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

