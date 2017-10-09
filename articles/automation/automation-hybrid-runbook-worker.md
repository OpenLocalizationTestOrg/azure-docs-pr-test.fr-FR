---
title: aaaAzure Workers hybrides de Automation | Documents Microsoft
description: "Cet article fournit des informations sur l’installation et à l’aide de Runbook Worker hybride qui est une fonctionnalité d’automatisation Azure qui vous permet de toorun runbooks sur des ordinateurs dans votre centre de données local ou d’un fournisseur de cloud."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: ccee35e8324149a79ff692a867e5ce7801299bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resources-in-your-data-center-or-cloud-with-hybrid-runbook-worker"></a>Automatiser des ressources dans votre centre de données ou votre cloud à l’aide d’un Runbook Worker hybride
Runbooks d’Azure Automation l’accès aux ressources dans d’autres clouds ou dans votre environnement local, car ils s’exécutent dans hello cloud Azure.  Hello Runbook Worker hybride fonctionnalité d’Azure Automation vous permet toorun runbooks directement sur l’ordinateur hello hébergeant le rôle de hello et sur des ressources dans hello environnement toomanage ces ressources locales. Procédures opérationnelles sont stockés et gérés dans Azure Automation et sa livraison tooone ou plus les ordinateurs désignés.  

Cette fonctionnalité est illustrée dans hello suivant l’image :<br>  

![Vue d'ensemble des Runbooks Workers hybrides](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Pour obtenir une vue d’ensemble technique des considérations de rôle et de déploiement de Runbook Worker hybride hello, consultez [présentation de l’architecture Automation](automation-offering-get-started.md#automation-architecture-overview).    

## <a name="hybrid-runbook-worker-groups"></a>Groupes de Runbooks Workers hybrides
Chaque Runbook Worker hybride est un membre d’un groupe de travail de Runbook hybride que vous spécifiez lorsque vous installez l’agent de hello.  Un groupe peut inclure un seul agent, mais vous pouvez installer plusieurs agents dans un groupe pour une haute disponibilité.

Lorsque vous démarrez un runbook sur un Runbook Worker hybride, vous spécifiez groupe hello il s’exécute.  les membres du groupe de hello Hello déterminent quel travail services demande de hello.  Vous ne pouvez pas spécifier un Worker particulier.

## <a name="relationship-tooservice-management-automation"></a>Relation tooService Management Automation
[Service Management Automation (SMA)](https://technet.microsoft.com/library/dn469260.aspx) vous permet de toorun hello même runbooks qui sont pris en charge par Azure Automation dans votre centre de données local. SMA est généralement déployé avec Windows Azure Pack, qui contient une interface graphique de gestion de SMA. Contrairement à Azure Automation, SMA requiert une installation locale qui inclut hello toohost de serveurs web API, un runbook de toocontain de base de données SMA configuration et des travaux tooexecute Runbook Worker. Azure Automation fournit ces services de cloud de hello et nécessite uniquement toomaintain hello Workers hybrides dans votre environnement local.

Si vous êtes un utilisateur SMA existant, vous pouvez déplacer votre toobe d’Automation tooAzure runbooks utilisé avec un Runbook Worker hybride sans modification, en supposant qu’ils effectuent leur propre tooresources d’authentification comme décrit dans [exécuter runbook sur un Runbook hybride Travail](automation-hrw-run-runbooks.md).  Runbooks dans SMA s’exécutent dans le contexte hello hello du compte de service sur serveur de traitement hello qui peut fournir l’authentification pour les runbooks hello.

Vous pouvez utiliser hello suivant des critères toodetermine si Azure Automation Runbook Worker hybride ou Service Management Automation est plus appropriée à vos besoins.

* SMA requiert une installation locale de ses composants sous-jacents qui sont connectés tooWindows Azure Pack si une interface de gestion graphique n’est requise. Des ressources locales sont nécessaires avec des coûts de maintenance plus élevés qu’Azure Automation, qui nécessite uniquement l’installation d’un agent sur des Runbooks Workers locaux. les agents Hello sont gérés par Operations Management Suite, davantage de réduire les coûts de maintenance.
* Azure Automation stocke ses procédures opérationnelles dans le cloud de hello et remet les Workers hybrides de tooon local. Si votre stratégie de sécurité n’autorise pas ce comportement, vous devez utiliser SMA.
* SMA est fourni avec System Center ; par conséquent, il requiert une licence System Center 2012 R2. Azure Automation est basé sur un modèle d’abonnement à plusieurs niveaux.
* Azure Automation dispose de fonctionnalités avancées, comme les runbooks graphiques, qui ne sont pas disponibles dans SMA.

## <a name="installing-hello-windows-hybrid-runbook-worker"></a>Lors de l’installation hello Runbook Worker hybride de Windows 

tooinstall et configurer un Runbook Worker hybride de Windows, il existe deux méthodes disponibles.  Hello recommandé que vous pouvez utiliser une automatisation runbook toocompletely automatiser hello requis tooconfigure un ordinateur Windows.  méthode deuxième Hello est après une installation toomanually de procédure pas à pas et configurer le rôle de hello.  

> [!NOTE]
> configuration de hello toomanage de vos serveurs prenant en charge le rôle de travail de Runbook hybride hello avec Configuration d’état souhaité (DSC), vous devez tooadd en tant que nœuds DSC.  Pour plus d’informations sur leur intégration pour les gérer avec DSC, consultez la page [Gestion de machines avec Azure Automation DSC](automation-dsc-onboarding.md).           
><br>
>Si vous activez hello [solution de gestion de la mise à jour](../operations-management-suite/oms-solution-update-management.md), n’importe quel ordinateur Windows connecté tooyour espace de travail OMS est automatiquement configuré comme un runbook toosupport de Runbook Worker hybride inclus dans cette solution.  Toutefois, il n’est enregistré auprès d’aucun des groupes de Workers hybrides déjà définis dans votre compte Automation.  Hello ordinateur peut être ajouté groupe de travail de Runbook hybride tooa dans votre toosupport de compte d’automatisation de runbook Automation tant que vous utilisez le même compte pour les solutions hello et l’appartenance au groupe de travail de Runbook hybride de hello.  Cette fonctionnalité a été ajoutée tooversion 7.2.12024.0 Hello Runbook Worker hybride.  

Hello révision suivant des informations concernant hello [matérielle et logicielle requise](automation-offering-get-started.md#hybrid-runbook-worker) et [plus d’informations pour la préparation de votre réseau](automation-offering-get-started.md#network-planning) avant de commencer le déploiement d’un Runbook Worker hybride.  Une fois que vous avez correctement déployé un runbook worker, passez en revue [exécuter runbook sur un Runbook Worker hybride](automation-hrw-run-runbooks.md) toolearn comment tooconfigure votre tooautomate runbooks traite dans votre centre de données local ou un autre environnement cloud.  
 
### <a name="automated-deployment"></a>Déploiement automatisé

Hello suivants étapes d’installation de hello tooautomate et configuration du rôle de travail hybride de Windows hello.  

1. Télécharger hello *New-OnPremiseHybridWorker.ps1* script à partir de hello [PowerShell Gallery](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/1.0/DisplayScript) directement à partir de l’ordinateur hello exécutant le rôle de travail de Runbook hybride hello ou depuis un autre ordinateur dans votre environnement et copiez-le toohello travail.  

    Hello *New-OnPremiseHybridWorker.ps1* script nécessite hello paramètres suivants lors de l’exécution :

  * *AutomationAccountName* (obligatoire) - nom hello de votre compte Automation.  
  * *ResourceGroupName* (obligatoire) - nom hello hello du groupe de ressources associé à votre compte Automation.  
  * *HybridGroupName* (obligatoire) - nom hello d’un groupe de travail de Runbook hybride que vous spécifiez en tant que cible pour les runbooks hello prenant en charge ce scénario. 
  *  *ID d’abonnement* (obligatoire) - hello Id d’abonnement Azure figurant dans votre compte Automation.
  *  *WorkspaceName* OMS de hello (facultatif) : nom de l’espace de travail.  Si vous n’avez pas un espace de travail OMS, script de hello crée et configure un.  

     > [!NOTE]
     > Actuellement pris en charge pour l’intégration avec OMS des régions Automation uniquement hello sont - **sud-est de l’Australie**, **est des États-Unis 2**, **Asie du Sud-est**, et **ouest Europe**.  Si votre compte Automation n’est pas dans un de ces régions, script de hello crée un espace de travail OMS, mais il vous avertit qu’il ne peut pas les relier.
     > 
2. Sur votre ordinateur, démarrez **Windows PowerShell** de hello **Démarrer** écran en mode administrateur.  
3. À partir de l’interface de ligne de commande PowerShell de hello, accédez à dossier toohello, qui contient le script hello vous avez téléchargé et exécuter la modification de valeurs hello pour les paramètres *- AutomationAccountName*, *- ResourceGroupName* , *- HybridGroupName*, *- SubscriptionId*, et *- WorkspaceName*.

     > [!NOTE] 
     > Vous êtes invité à tooauthenticate avec Azure après avoir exécuté le script de hello.  Vous **doit** connectez-vous avec un compte qui est membre du rôle des administrateurs d’abonnements hello et coadministrateur de l’abonnement de hello.  
     >  
    
        .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> `
        -ResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
        -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfOMSWorkspace>

4. Vous êtes invité à tooagree tooinstall **NuGet** et que vous êtes invité à tooauthenticate avec vos informations d’identification Azure.<br><br> ![Exécution du script New-OnPremiseHybridWorker](media/automation-hybrid-runbook-worker/new-onpremisehybridworker-scriptoutput.png)

5. Une fois le script de hello est terminée, panneau de groupes de travail hybride hello présentent nouveau groupe de hello et le nombre de membres ou si un groupe existant, le nombre de hello de membres est incrémenté.  Vous pouvez sélectionner le groupe de hello dans liste hello hello **groupes de travail hybride** panneau et sélectionnez hello **Workers hybrides** vignette.  Sur hello **Workers hybrides** panneau, vous consultez chaque membre du groupe hello répertoriés.  

### <a name="manual-deployment"></a>Déploiement manuel 
Effectuer les deux premières étapes de hello qu’une seule fois pour votre environnement d’automatisation, puis répétez hello restant étapes pour chaque ordinateur de travail.

#### <a name="1-create-operations-management-suite-workspace"></a>1. Création d’un espace de travail Operations Management Suite
Si vous ne disposez pas déjà d’un espace de travail Operations Management Suite, créez-en un en suivant les instructions mentionnées à la page [Gérer votre espace de travail](../log-analytics/log-analytics-manage-access.md). Vous pouvez utiliser un espace de travail existant si vous en avez déjà un.

#### <a name="2-add-automation-solution-toooperations-management-suite-workspace"></a>2. Ajouter l’Automation solution tooOperations espace de travail Management Suite
Solutions ajoutent des fonctionnalités tooOperations Management Suite.  Hello solution Automation ajoute des fonctionnalités d’automatisation Azure, y compris la prise en charge de travail de Runbook hybride.  Lorsque vous ajoutez tooyour espace de travail solution hello, il transmet automatiquement vers le bas travail composants toohello agent ordinateur que vous allez installer à l’étape suivante de hello.

Suivez les instructions de hello à [tooadd une solution à l’aide de la galerie des Solutions hello](../log-analytics/log-analytics-add-solutions.md) tooadd hello **Automation** espace de travail de solution tooyour Operations Management Suite.

#### <a name="3-install-hello-microsoft-monitoring-agent"></a>3. Installer hello Microsoft Monitoring Agent
Hello Microsoft Monitoring Agent connecte les ordinateurs tooOperations Management Suite.  Lorsque vous installez l’agent de hello sur votre ordinateur local et le connectez tooyour espace de travail, il télécharge automatiquement les composants hello requis pour un Runbook Worker hybride.

Suivez les instructions de hello à [tooLog d’ordinateurs Windows de se connecter Analytique](../log-analytics/log-analytics-windows-agents.md) agent de hello tooinstall sur l’ordinateur local de hello.  Vous pouvez répéter ce processus pour plusieurs ordinateurs tooadd environnement tooyour à plusieurs threads de travail.

Lorsque l’agent de hello connecté tooOperations Management Suite, il sera répertorié sur hello **Sources connectées** onglet Hello Operations Management Suite **paramètres** volet.  Vous pouvez vérifier que l’agent hello a téléchargé correctement la solution d’automatisation hello lorsqu’il a un dossier appelé **AzureAutomationFiles** dans C:\Program Files\Microsoft Monitoring Agent\Agent.  version hello tooconfirm hello Runbook Worker hybride, vous pouvez naviguer hello Agent\Agent\AzureAutomation\ de surveillance et de note de tooC:\Program Files\Microsoft \\ *version* sous-dossier.   

#### <a name="4-install-hello-runbook-environment-and-connect-tooazure-automation"></a>4. Installer l’environnement du runbook hello et se connecter tooAzure Automation
Lorsque vous ajoutez une tooOperations agent Management Suite, hello solution Automation exécute un push vers le bas hello **HybridRegistration** module PowerShell, qui contient les hello **Add-HybridRunbookWorker** applet de commande.  Vous utilisez cet applet de commande tooinstall hello de runbooks environnement sur l’ordinateur de hello et l’inscrivez avec Azure Automation.

Ouvrez une session PowerShell en mode administrateur et exécutez hello suivant du module de commandes tooimport hello.

    cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
    Import-Module HybridRegistration.psd1

Puis exécutez hello **Add-HybridRunbookWorker** applet de commande à l’aide de la syntaxe de hello :

    Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>

Vous pouvez obtenir des informations de hello requises pour cette applet de commande hello **gérer les clés** panneau Bonjour portail Azure.  Pour ouvrir ce panneau en sélectionnant hello **clés** option hello **paramètres** panneau dans votre compte Automation.

![Vue d'ensemble des Runbooks Workers hybrides](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName** hello désigne hello groupe Runbook Worker hybride. Si ce groupe existe déjà dans le compte d’automatisation hello, ordinateur hello est ajouté tooit.  S'il n'existe pas encore, il est alors ajouté.
* **Point de terminaison** est hello **URL** champ hello **gérer les clés** panneau.
* **Jeton** est hello **clé d’accès primaire** Bonjour **gérer les clés** panneau.  

Hello d’utilisation **-Verbose** basculer **Add-HybridRunbookWorker** tooreceive des informations détaillées sur les installation hello.

#### <a name="5-install-powershell-modules"></a>5. Installer des modules PowerShell
Procédures opérationnelles peut utiliser des activités de hello et des applets de commande définis dans les modules hello installés dans votre environnement Azure Automation.  Ces modules ne sont pas les ordinateurs local tooon automatiquement déployé, vous devez les installer manuellement.  exception de Hello est hello module Windows Azure, qui est installé par défaut en fournissant des accès toocmdlets pour toutes les activités et les services Azure pour Azure Automation.

Hello principal objectif de fonctionnalité de Runbook Worker hybride hello étant toomanage des ressources locales, probablement inutile modules hello tooinstall qui prennent en charge de ces ressources.  Vous pouvez faire référence trop[l’installation des Modules](http://msdn.microsoft.com/library/dd878350.aspx) pour plus d’informations sur l’installation de modules Windows PowerShell.  Les modules qui sont installés doivent être dans un emplacement référencé par la variable d’environnement PSModulePath afin qu’ils sont automatiquement importés par processus de travail hybride hello.  Pour plus d’informations, consultez [modification hello chemin d’Installation de PSModulePath](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx). 

## <a name="removing-hybrid-runbook-worker"></a>Suppression de la fonctionnalité Runbook Worker hybride 
Vous pouvez supprimer une Workers hybrides à partir d’un groupe, ou vous pouvez supprimer le groupe de hello, selon vos besoins.  tooremove un Runbook Worker hybride à partir d’un ordinateur local, exécutez hello comme suit.

1. Bonjour portail Azure, accédez à compte Automation de tooyour.  
2. À partir de hello **paramètres** panneau, sélectionnez **clés** et notez les valeurs hello pour le champ **URL** et **clé d’accès primaire**.  Ces informations sont nécessaires pour l’étape suivante de hello.
3. Ouvrez une session PowerShell en mode administrateur et exécutez hello command - `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>`.  Hello d’utilisation **-Verbose** basculer pour un journal détaillé du processus de suppression hello.

> [!NOTE]
> Cela ne supprime pas hello Microsoft Monitoring Agent à partir de l’ordinateur hello, uniquement les fonctionnalités de hello et configuration du rôle de travail de Runbook hybride hello.  

## <a name="remove-hybrid-worker-groups"></a>Suppression de groupes de Workers hybrides
tooremove un groupe, vous devez tout d’abord tooremove hello Runbook Worker hybride à partir de chaque ordinateur qui est membre du groupe de hello à l’aide de la procédure hello présentée précédemment et que vous effectuez hello suivant du groupe d’étapes tooremove hello.  

1. Ouvrez le compte Automation de hello Bonjour portail Azure.
2. Sélectionnez hello **groupes de travail hybride** vignette et Bonjour **groupes de travail hybride** panneau, groupe hello sélectionnez toodelete.  Après avoir sélectionné un groupe spécifique de hello, hello **groupe worker hybride** panneau des propriétés s’affiche.<br> ![Panneau Groupes de Runbook Workers hybrides](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
3. Dans le panneau des propriétés hello pour le groupe sélectionné de hello, cliquez sur **supprimer**.  Un message s’affiche vous demandant tooconfirm vous cette action, sélectionnez **Oui** si vous êtes sûr de vouloir tooproceed.<br> ![Boîte de dialogue de confirmation de suppression du groupe](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> Ce processus peut prendre plusieurs secondes toocomplete et que vous pouvez suivre sa progression sous **Notifications** à partir du menu de hello.  

## <a name="troubleshooting"></a>Résolution des problèmes 
Hello Runbook Worker hybride dépend de hello toocommunicate Microsoft Monitoring Agent avec votre processus de travail Automation compte tooregister hello, travaux et l’état de réception. Si l’inscription du traitement de hello échoue, voici les causes possibles de l’erreur de hello :  

1. processus de travail hybride Hello est derrière un pare-feu ou proxy.  
    Vérifiez que hello est équipé d’un accès sortant too*.azure-automation.net sur le port 443.  

2. Hello worker hybride de hello ordinateur est en cours d’exécution est inférieure à la configuration matérielle minimale hello [exigences](automation-offering-get-started.md#hybrid-runbook-worker).  
    Ordinateurs exécutant hello Runbook Worker hybride doit satisfaire aux hello configuration matérielle minimale requise avant de désigner toohost cette fonctionnalité. Sinon, en fonction de l’utilisation des ressources hello d’autres processus d’arrière-plan et la contention provoqué par des procédures opérationnelles lors de l’exécution, ordinateur de hello sera devenir surchargé et entraîner des retards de travail de runbook ou des délais d’attente.
   Vérifiez que hello désigné la fonctionnalité de Runbook Worker hybride toorun hello requise hello matérielle minimale.  Dans ce cas, surveillez toodetermine de l’utilisation du processeur et mémoire toute corrélation entre les performances hello de processus de travail de Runbook hybride et Windows.  S’il existe de mémoire ou surcharge des ressources processeur, cela peut indiquer hello besoin tooupgrade ou ajoutez des processeurs supplémentaires ou augmentation mémoire tooaddress hello goulot d’étranglement des ressources et résoudre l’erreur de hello. Vous pouvez également sélectionner une ressource de calcul différents qui peut prendre en charge les exigences minimales hello et mettre à l’échelle lorsque les charges de travail indiquent qu'une augmentation est nécessaire.
    
3. Hello service Microsoft Monitoring Agent ne fonctionne pas.  
    Si hello service Windows de l’Agent d’analyse Microsoft ne fonctionne pas, cela empêche hello Runbook Worker hybride de communiquer avec Azure Automation.  Vérifier l’agent de hello est en cours d’exécution en entrant hello commande dans PowerShell suivante : `get-service healthservice`.  Si l’arrêt du service de hello, entrez hello suivant de commande PowerShell toostart hello service : `start-service healthservice`.  

4. Bonjour **Application et le Gestionnaire des Services Logs\Operations** journal des événements, vous voyez l’événement 4502 et EventMessage contenant **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**avec hello suivant description : *certificat hello présenté par le service de hello <wsid>. oms.opinsights.azure.com n’a pas été émis par une autorité de certification utilisée pour les services Microsoft. Veuillez contacter votre toosee d’administrateur réseau s’ils exécutent un proxy qui intercepte les communications TLS/SSL. article de Hello KB3126513 contient des informations de dépannage supplémentaires pour les problèmes de connectivité.*
    Cela peut être dû à votre réseau ou proxy pare-feu blockking communication tooMicrosoft Azure.  Vérifiez que hello est équipé d’un accès sortant too*.azure-automation.net sur les ports 443.

Les journaux sont stockés localement sur chaque Worker hybride à l’emplacement C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Vous pouvez vérifier s’il existe des événements d’avertissement ou erreur écrits toohello **d’Application et de Services Logs\Microsoft-SMA\Operations** et **Application et le Gestionnaire des Services Logs\Operations** journal des événements Indique une connectivité ou tout autre problème affectant l’intégration d’hello rôle tooAzure Automation ou de problème lors de l’exécution d’opérations normales.  

## <a name="next-steps"></a>Étapes suivantes
Révision [exécuter runbook sur un Runbook Worker hybride](automation-hrw-run-runbooks.md) toolearn comment tooconfigure votre tooautomate runbooks traite dans votre centre de données local ou un autre environnement cloud.
