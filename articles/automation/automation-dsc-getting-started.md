---
title: "aaaGetting main d’Azure Automation DSC | Documents Microsoft"
description: "Explication et des exemples de tâches les plus courantes de hello dans Azure Automation état Configuration souhaité (DSC)"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a>Prise en main d’Azure Automation DSC
Cette rubrique explique comment toodo hello tâches les plus courantes avec Azure Automation état Configuration souhaité (DSC), telles que la création, l’importation et la compilation des configurations, l’intégration trop gérer les ordinateurs et l’affichage de rapports. Pour une vue d’ensemble d’Azure Automation DSC, consultez [Vue d’ensemble d’Azure Automation DSC](automation-dsc-overview.md). Pour la documentation DSC, consultez l’article [Vue d’ensemble de la fonctionnalité Desired State Configuration de Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).

Cette rubrique fournit un guide pas à pas de toousing Azure Automation DSC. Si vous souhaitez un exemple d’environnement qui est déjà configuré sans suivant hello les étapes décrites dans cette rubrique, vous pouvez utiliser [hello suivant un modèle ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup). Ce modèle configure un environnement Azure Automation DSC complet, comprenant une machine virtuelle Azure gérée par Azure Automation DSC.

## <a name="prerequisites"></a>Composants requis
exemples de hello toocomplete dans cette rubrique, hello Voici requis :

* Un compte Azure Automation. Pour obtenir des instructions sur la création d’un compte d’identification Azure Automation, consultez [Authentifier des Runbooks avec un compte d’identification Azure](automation-sec-configure-azure-runas-account.md).
* Une machine virtuelle Azure Resource Manager (non classique) exécutant Windows Server 2008 R2 ou version ultérieure. Pour obtenir des instructions sur la création d’une machine virtuelle, consultez [créer votre première machine virtuelle de Windows Bonjour portail Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)

## <a name="creating-a-dsc-configuration"></a>Création d’une configuration DSC
Nous allons créer une simple [configuration DSC](https://msdn.microsoft.com/powershell/dsc/configurations) qui garantit la présence de hello ou d’absence de hello **Web-Server** Windows fonctionnalité (IIS), en fonction de l’attribution des nœuds.

1. Démarrer Windows PowerShell ISE de hello (ou n’importe quel éditeur de texte).
2. Tapez hello suivant du texte :
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. Enregistrer le fichier hello sous `TestConfig.ps1`.

Cette configuration appelle une ressource dans chaque bloc de nœud, hello [ressource WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), qui garantit la présence de hello ou d’absence de hello **Web-Server** fonctionnalité.

## <a name="importing-a-configuration-into-azure-automation"></a>Importation d’une configuration dans Azure Automation
Ensuite, nous allons importer configuration de hello dans hello compte Automation.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.
3. Sur hello **compte Automation** panneau, cliquez sur **les Configurations DSC**.
4. Sur hello **les Configurations DSC** panneau, cliquez sur **ajouter une configuration**.
5. Sur hello **importer la Configuration** toohello de parcourir les lames, `TestConfig.ps1` fichier sur votre ordinateur.
   
    ![Capture d’écran de hello ** Panneau de Configuration d’importation **](./media/automation-dsc-getting-started/AddConfig.png)
6. Cliquez sur **OK**.

## <a name="viewing-a-configuration-in-azure-automation"></a>Affichage d’une configuration dans Azure Automation
Après avoir importé une configuration, vous pouvez l’afficher dans hello portail Azure.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.
3. Sur hello **compte Automation** panneau, cliquez sur **les Configurations DSC**
4. Sur hello **les Configurations DSC** panneau, cliquez sur **TestConfig** (il s’agit hello nom de configuration hello vous avez importé dans la procédure précédente de hello).
5. Sur hello **TestConfig Configuration** panneau, cliquez sur **afficher la source configuration**.
   
    ![Capture d’écran du Panneau de configuration hello TestConfig](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    A **source de Configuration de TestConfig** s’ouvre le panneau, affichage du code de PowerShell hello pour la configuration de hello.

## <a name="compiling-a-configuration-in-azure-automation"></a>Compilation d’une configuration dans Azure Automation
Avant de pouvoir appliquer un nœud de tooa d’état souhaité, une configuration DSC définissant cet état doit être compilée dans un ou plusieurs configurations de nœuds (document MOF) et placée sur hello serveur d’extraction Automation DSC. Pour obtenir une description plus détaillée de la compilation des configurations dans Azure Automation DSC, consultez [Compilation de configurations dans Azure Automation DSC](automation-dsc-compile.md). Pour plus d’informations sur la compilation des configurations, consultez [Configurations DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.
3. Sur hello **compte Automation** panneau, cliquez sur **les Configurations DSC**
4. Sur hello **les Configurations DSC** panneau, cliquez sur **TestConfig** (nom hello Hello précédemment importé configuration).
5. Sur hello **TestConfig Configuration** panneau, cliquez sur **compiler**, puis cliquez sur **Oui**. Une tâche de compilation démarre.
   
    ![Capture d’écran du Panneau de configuration hello TestConfig mise en surbrillance le bouton de la compilation](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> Lorsque vous compilez une configuration dans Azure Automation, il déploie automatiquement n’importe quel serveur collecteur toohello de MOF de configuration nœud créé.
> 
> 

## <a name="viewing-a-compilation-job"></a>Affichage d’une tâche de compilation
Une fois que vous démarrez une compilation, vous pouvez les consulter dans hello **travaux de Compilation** vignette Bonjour **Configuration** panneau. Hello **travaux de Compilation** vignette montre en cours d’exécution, terminé et travaux en échec. Lorsque vous ouvrez un panneau de tâche de compilation, elle affiche des informations sur cette tâche, y compris les erreurs ou les avertissements rencontrés, paramètres d’entrée utilisés dans hello, compilation et la configuration des journaux.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.
3. Sur hello **compte Automation** panneau, cliquez sur **les Configurations DSC**.
4. Sur hello **les Configurations DSC** panneau, cliquez sur **TestConfig** (nom hello Hello précédemment importé configuration).
5. Sur hello **travaux de Compilation** vignette Hello **TestConfig Configuration** panneau, cliquez sur un des travaux hello répertoriés. A **tâche de Compilation** s’ouvre le panneau, étiquetés avec la date de hello hello la tâche de compilation a été démarré.
   
    ![Capture d’écran du Panneau de tâche de Compilation hello](./media/automation-dsc-getting-started/CompilationJob.png)
6. Cliquez sur n’importe quelle vignette Bonjour **tâche de Compilation** toosee panneau davantage des détails sur les travaux hello.

## <a name="viewing-node-configurations"></a>Affichage des configurations de nœuds
La réussite d’une tâche de compilation a pour effet de créer une ou plusieurs configurations de nœud. Une configuration de nœud est un document MOF est le serveur du collecteur toohello déployé et prêt toobe extraites et appliquées par un ou plusieurs nœuds. Vous pouvez afficher les configurations de nœuds hello dans votre compte Automation Bonjour **Configurations de nœuds DSC** panneau. Une configuration de nœud a un nom de la forme de hello *ConfigurationName*. *NodeName*.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.
3. Sur hello **compte Automation** panneau, cliquez sur **Configurations de nœuds DSC**.
   
    ![Capture d’écran du Panneau de configuration de nœuds DSC hello](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a>Intégration d’une machine virtuelle Azure pour la gérer avec Azure Automation DSC
Vous pouvez utiliser Azure Automation DSC toomanage machines virtuelles de Azure (classique et le Gestionnaire de ressources), machines virtuelles de local, machines Linux, machines virtuelles de AWS et machines physiques locales. Dans cette rubrique, nous abordons la tooonboard uniquement machines virtuelles Azure Resource Manager. Pour plus d’informations sur l’intégration d’autres types d’ordinateur, consultez [Gestion de machines avec Azure Automation DSC](automation-dsc-onboarding.md).

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a>tooonboard un gestionnaire de ressources d’Azure VM pour la gestion par Azure Automation DSC
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.
3. Sur hello **compte Automation** panneau, cliquez sur **nœuds DSC**.
4. Bonjour **nœuds DSC** panneau, cliquez sur **ajouter Azure VM**.
   
    ![Capture d’écran du Panneau de nœuds DSC hello mise en surbrillance le bouton d’ajout de machine virtuelle Azure hello](./media/automation-dsc-getting-started/OnboardVM.png)
5. Bonjour **ajouter des machines virtuelles Azure** panneau, cliquez sur **sélectionner des machines virtuelles tooonboard**.
6. Bonjour **sélectionner les machines virtuelles** panneau, sélectionnez hello machine virtuelle que vous souhaitez tooonboard, puis cliquez sur **OK**.
   
   > [!IMPORTANT]
   > Il doit s’agir d’une machine virtuelle Azure Resource Manager exécutant Windows Server 2008 R2 ou version ultérieure.
   > 
   > 
7. Bonjour **ajouter des machines virtuelles Azure** panneau, cliquez sur **configurer les données d’inscription**.
8. Bonjour **inscription** panneau, entrez le nom de hello de configuration du nœud hello souhaité tooapply toohello VM Bonjour **nom de Configuration de nœud** boîte. Cela doit correspondre exactement à nom hello d’une configuration de nœud Bonjour compte Automation. Vous n’êtes pas obligé de fournir un nom à ce stade. Vous pouvez modifier la configuration du nœud hello affecté après le nœud de hello d’intégration.
   Cochez la case **Redémarrer le nœud si nécessaire**, puis cliquez sur **OK**.
   
    ![Capture d’écran du Panneau de l’inscription de hello](./media/automation-dsc-getting-started/RegisterVM.png)
   
    configuration de nœud Hello spécifiée sera appliqué toohello VM selon l’intervalle spécifié par hello **fréquence de Mode de Configuration**, et vérifie pour la configuration du nœud toohello mises à jour selon l’intervalle spécifié par hello hellomachinevirtuelle **Fréquence d’actualisation**. Pour plus d’informations sur la façon dont ces valeurs sont utilisées, consultez [configuration hello Gestionnaire de Configuration Local](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).
9. Bonjour **ajouter des machines virtuelles Azure** panneau, cliquez sur **créer**.

Azure démarre processus hello de l’intégration hello machine virtuelle. Lorsqu’il est terminé, hello machine virtuelle s’afficheront dans hello **nœuds DSC** panneau Bonjour compte Automation.

## <a name="viewing-hello-list-of-dsc-nodes"></a>Affichage de liste de hello de nœuds DSC
Vous pouvez afficher la liste de hello de tous les ordinateurs qui ont été intégrées pour la gestion de votre compte Automation Bonjour **nœuds DSC** panneau.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.
3. Sur hello **compte Automation** panneau, cliquez sur **nœuds DSC**.

## <a name="viewing-reports-for-dsc-nodes"></a>Affichage des rapports de nœuds DSC
Chaque fois que Azure Automation DSC effectue une vérification de cohérence sur un nœud géré, nœud de hello envoie un état rapport toohello différé par extraction de données serveur. Vous pouvez consulter ces rapports sur le panneau hello pour ce nœud.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.
3. Sur hello **compte Automation** panneau, cliquez sur **nœuds DSC**.
4. Sur hello **rapports** vignette, cliquez sur un des rapports hello dans la liste de hello.
   
    ![Capture d’écran du Panneau de rapport hello](./media/automation-dsc-getting-started/NodeReport.png)

Dans Panneau de hello pour un rapport individuel, vous pouvez voir hello suit les informations d’état de cohérence correspondante de hello vérifier :

* Hello état — si le nœud de hello est « Conforme », la configuration de hello « Failed », ou nœud de hello est « Non conforme » (lorsque le nœud de hello est à **applyandmonitor** mode et hello machine n’est pas en état de hello souhaité).
* Hello heure de début de la vérification de cohérence hello.
* temps total d’exécution Hello par souci de cohérence hello vérifier.
* vérification de type Hello de cohérence.
* Toutes les erreurs, y compris le message d’erreur et le code erreur hello. 
* Toutes les ressources DSC utilisées dans la configuration de hello et état hello de chaque ressource (si hello nœud est en état hello souhaité pour cette ressource) : vous pouvez cliquer sur chaque ressource tooget des informations plus détaillées pour cette ressource.
* nom de Hello, adresse IP et le mode de configuration du nœud de hello.

Vous pouvez également cliquer sur **affichage brut** toosee hello données effectivement hello nœud envoie toohello server. Pour plus d’informations sur l’utilisation de ces données, consultez la page [Utilisation d’un serveur de rapports DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).

Il peut prendre un certain temps, une fois un nœud embarquées avant hello premier état est disponible. Vous devrez peut-être toowait des too30 minutes pour le premier rapport de hello après avoir intégrer un nœud.

## <a name="reassigning-a-node-tooa-different-node-configuration"></a>Réaffectation d’une configuration de nœud différents nœuds tooa
Vous pouvez affecter un toouse nœud une configuration de nœud autre que hello une qu'initialement affecté.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.
3. Sur hello **compte Automation** panneau, cliquez sur **nœuds DSC**.
4. Sur hello **nœuds DSC** panneau, cliquez sur le nom hello du nœud de hello souhaité tooreassign.
5. Dans le panneau de hello pour ce nœud, cliquez sur **nœud Assign**.
   
    ![Capture d’écran du Panneau de nœud hello mise en surbrillance le bouton d’attribuer un nœud hello](./media/automation-dsc-getting-started/AssignNode.png)
6. Sur hello **attribuer une Configuration de nœud** panneau, sélectionnez hello nœud configuration toowhich vous souhaitez tooassign hello nœud, puis cliquez sur **OK**.
   
    ![Capture d’écran du Panneau de Configuration du nœud affecter hello](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a>Annulation de l’inscription d’un nœud
Si vous ne voulez plus un toobe de nœud géré par Azure Automation DSC, vous pouvez annuler son inscription.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, cliquez sur **toutes les ressources** , puis hello nom de votre compte Automation.
3. Sur hello **compte Automation** panneau, cliquez sur **nœuds DSC**.
4. Sur hello **nœuds DSC** panneau, cliquez sur le nom hello du nœud de hello souhaité toounregister.
5. Dans le panneau de hello pour ce nœud, cliquez sur **Unregister**.
   
    ![Capture d’écran du Panneau de nœud hello mise en surbrillance le bouton Annuler l’enregistrement de hello](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a>Articles connexes
* [Vue d’ensemble d’Azure Automation DSC](automation-dsc-overview.md)
* [Gestion de machines avec Azure Automation DSC](automation-dsc-onboarding.md)
* [Vue d’ensemble d’Azure Automation DSC](https://msdn.microsoft.com/powershell/dsc/overview)
* [Applets de commande Azure Automation DSC](/powershell/module/azurerm.automation/#automation)
* [Tarification d’Azure Automation DSC](https://azure.microsoft.com/pricing/details/automation/)

