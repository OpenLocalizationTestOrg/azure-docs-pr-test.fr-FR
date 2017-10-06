---
title: "aaaAzure Automation DSC un déploiement continu avec Chocolatey | Documents Microsoft"
description: "Déploiement continu du DevOps à l’aide d’Azure Automation DSC et du gestionnaire de packages Chocolatey  Exemple avec modèle ARM JSON complet et source PowerShell."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: c0baa411-eb76-4f91-8d14-68f68b4805b6
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/29/2016
ms.author: golive
ms.openlocfilehash: 60af52af5f834fd48e3a0dc4677919397b53f0f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-example-continuous-deployment-toovirtual-machines-using-automation-dsc-and-chocolatey"></a>Exemple d’utilisation : Déploiement continu tooVirtual ordinateurs à l’aide d’Automation DSC et Chocolatey
Dans un monde DevOps, il existe plusieurs outils tooassist, avec différents points dans le pipeline d’intégration continue hello.  Configuration d’état de Azure Automation souhaité (DSC) est un accueil nouvelle addition toohello options DevOps les équipes peuvent utiliser.  Cet article explique comment configurer le déploiement continu (CD) pour un ordinateur Windows.  Vous pouvez facilement étendre hello technique tooinclude les ordinateurs Windows autant que nécessaire dans le rôle hello (par exemple, un site web) et de tooadditional il n’y a également les rôles.

![Déploiement continu pour machines virtuelles IaaS](./media/automation-dsc-cd-chocolatey/cdforiaasvm.png)

## <a name="at-a-high-level"></a>À un niveau élevé
Il y aurait beaucoup à dire sur ce sujet, mais il est heureusement possible de décomposer toutes ces informations en deux grands processus : 

* L’écriture de code et test, la création et publication des packages d’installation pour les versions majeure et mineure du système de hello. 
* Création et gestion des machines virtuelles qui va installer et exécuter du code hello dans les packages de hello.  

Une fois que ces deux principaux processus sont en place, il est un package de hello étape court tooautomatically mise à jour en cours d’exécution sur n’importe quel ordinateur virtuel particulier que de nouvelles versions sont créées et déployées.

## <a name="component-overview"></a>Vue d’ensemble des composants
Gestionnaires de package tel que [apt-get](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool) sont assez bien connus dans Linux Bonjour, mais pas tellement Bonjour de Windows.  [Chocolatey](https://chocolatey.org/) est un tel chose et de Scott Hanselman [blog](http://www.hanselman.com/blog/IsTheWindowsUserReadyForAptget.aspx) sur hello rubrique est une excellente introduction.  En bref, Chocolatey vous permet de tooinstall les packages à partir d’un référentiel central des packages dans un système Windows à l’aide de la ligne de commande hello.  Vous pouvez créer et gérer votre propre référentiel et Chocolatey peut installer des packages à partir de tous les référentiels que vous désignez, quel qu’en soit le nombre.

État de la Configuration souhaité (DSC) ([vue d’ensemble](https://technet.microsoft.com/library/dn249912.aspx)) est un outil PowerShell qui vous permet de configuration hello toodeclare souhaitées pour un ordinateur.  Par exemple, vous pouvez vouloir installer Chocolatey et IIS, ouvrir le port 80 et installer la version 1.0.0 de votre site Web.  Gestionnaire de Configuration Local Hello DSC (LCM) implémente cette configuration. Un serveur Pull DSC contient un référentiel des configurations de vos machines. Hello Gestionnaire de configuration local sur chaque ordinateur vérifie dans toosee régulièrement si sa configuration correspond à la configuration stockée de hello. Il peut signaler l’état ou essayez d’ordinateur de hello toobring en alignement avec une configuration stockée hello. Vous pouvez modifier hello configuration stockée sur hello extraction server toocause un ordinateur ou un ensemble de machines toocome en phase avec une configuration hello modifié.

Azure Automation est un service géré dans Microsoft Azure qui vous permet tooautomate diverses tâches à l’aide de procédures opérationnelles, nœuds, informations d’identification, des ressources telles que les planifications et les variables globales. Azure Automation DSC étend cette automatisation outils de la fonctionnalité tooinclude DSC PowerShell.  En voici une excellente [présentation](automation-dsc-overview.md).

Une ressource DSC est un module de code qui présente des fonctionnalités spécifiques, telles que la gestion de mise en réseau, Active Directory ou SQL Server.  Hello Chocolatey ressource DSC sait comment tooaccess un serveur NuGet (entre autres), télécharger des packages, installer des packages et ainsi de suite.  Il existe de nombreuses autres ressources DSC Bonjour [PowerShell Gallery](http://www.powershellgallery.com/packages?q=dsc+resources&prerelease=&sortOrder=package-title).  Vous-même devez installer ces modules dans le serveur Pull Azure Automation DSC afin qu’ils puissent être utilisés par vos configurations.

Les modèles Resource Manager offrent un moyen de générer votre infrastructure par des déclarations (réseaux, sous-réseaux, sécurité du réseau et routage, équilibreurs de charge, NIC, machines virtuelles, etc.).  Voici une [article](../azure-resource-manager/resource-manager-deployment-model.md) que compare hello modèle de déploiement du Gestionnaire de ressources (déclarative) avec hello Azure Service Management (ASM ou classique) déploiement de modèle (impératif) et décrit les principales ressources de hello fournisseurs, de calcul, stockage et réseau.

Une des principales caractéristiques d’un modèle de gestionnaire de ressources sont son tooinstall possibilité une extension de machine virtuelle dans hello machine virtuelle comme s’il est configuré.  Une extension de machine virtuelle possède des fonctionnalités spécifiques, telles que l’exécution d’un script personnalisé, l’installation d’un logiciel antivirus ou encore l’exécution d’un script de configuration DSC.  Il existe de nombreux autres types d’extensions de machine virtuelle.

## <a name="quick-trip-around-hello-diagram"></a>Voyage rapide autour de diagramme de hello
Partant du haut de hello, vous écrivez votre code, build et de test, puis créer un package d’installation.  Chocolatey peut gérer différents types de packages d’installation, tels que MSI, MSU ou ZIP.  Et vous avez toute la puissance hello d’installation de PowerShell toodo hello réelle si les fonctionnalités natives de Chocolatey ne sont pas assez de tooit.  Placez le package de hello dans un endroit accessible à un référentiel de packages.  Cet exemple utilise un dossier public dans un compte de stockage d’objets blob Azure, mais vous pouvez utiliser n’importe quel emplacement.  Chocolatey fonctionne en mode natif avec des serveurs NuGet et quelques autres serveurs pour la gestion des métadonnées de packages.  [Cet article](https://github.com/chocolatey/choco/wiki/How-To-Host-Feed) décrit les options de hello.  Cet exemple utilise NuGet.  Un Nuspec désigne les métadonnées concernant vos packages.  Hello Nuspec est « compilé » dans de NuPkg et stocké dans un serveur NuGet.  Lors de la configuration de votre demande d’un package par nom et fait référence à un serveur NuGet, hello Chocolatey ressource DSC (sur la machine virtuelle de hello) extrait le package de hello et l’installe pour vous.  Vous pouvez également demander une version spécifique d’un package.

Dans hello partie inférieure gauche de l’image de hello, il existe un modèle Azure Resource Manager (ARM).  Dans cet exemple d’utilisation, hello extension de machine virtuelle inscrit hello VM par hello Azure Automation DSC par extraction de données serveur (autrement dit, un serveur collecteur) en tant que nœud.  configuration de Hello est stockée dans le serveur collecteur de hello.  En fait, elle est stockée à deux reprises : une première fois en tant que texte brut et une deuxième fois compilée dans un fichier MOF (pour ceux qui s’y connaissent).  Dans le portail hello, hello MOF est une « configuration de nœud » (en opposition toosimply « configuration »).  Son hello artefact qui est associé à un nœud par conséquent, le nœud de hello saurez sa configuration.  Détails ci-dessous montrent comment tooassign hello nœud toohello de configuration de nœud.

Sans doute déjà effectué bits hello haut hello ou plus de celui-ci.  Création de hello nuspec, la compilation et le stockage dans un serveur NuGet sont une petite chose.  Et vous gérez déjà des machines virtuelles.  Hello prochaine étape toocontinuous déploiement requiert la configuration hello le serveur collecteur (une fois), l’inscription de vos nœuds avec lui (une fois) et la création et le stockage de configuration hello il (initialement).  Comme les packages sont mis à niveau et déploiement toohello référentiel, actualiser hello Configuration et la Configuration du nœud dans le serveur du collecteur hello (répétition si nécessaire).

Si vous ne commencez pas par un modèle ARM, il n’y a aucun problème.  Il n’y a toohelp d’applets de commande conçues PowerShell vous inscrivez vos machines virtuelles avec serveur collecteur de hello et tous les autres hello. Pour plus d’informations, consultez cet article : [Gestion de machines avec Azure Automation DSC](automation-dsc-onboarding.md)

## <a name="step-1-setting-up-hello-pull-server-and-automation-account"></a>Étape 1 : Configuration de compte de serveur et l’automatisation de collecteur hello
Sur une ligne de commande (Add-AzureRmAccount) PowerShell authentifié : (peut prendre quelques minutes pendant que le serveur collecteur de hello est configuré)

    New-AzureRmResourceGroup –Name MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES
    New-AzureRmAutomationAccount –ResourceGroupName MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES –Name MY-AUTOMATION-ACCOUNT 

Vous pouvez placer votre compte automation dans n’importe quel Hello suivant régions (également appelé location) : est des États-Unis 2, Amérique du Sud, nous Gov Virginie, Europe de l’ouest, Asie du Sud-est, est du Japon, l’Inde centrale et sud-est de l’Australie, centre Canada, Europe du Nord.

## <a name="step-2-vm-extension-tweaks-toohello-arm-template"></a>Étape 2 : Extension de machine virtuelle tweaks modèle ARM de toohello
Détails d’enregistrement de la machine virtuelle (en utilisant l’extension de machine virtuelle de DSC PowerShell hello) indiquées dans ce [modèle de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/dsc-extension-azure-automation-pullserver).  Cette étape inscrit votre nouvelle machine virtuelle avec serveur de collecteur hello dans liste hello de nœuds DSC.  Partie de cet enregistrement est spécifiant hello nœud configuration toobe appliqué toohello.  Cette configuration de nœud n’absence tooexist encore dans le serveur collecteur de hello, il est donc OK étape 4 est où cela est effectuée pour hello première fois.  Mais ici à l’étape 2 vous avez besoin de nœud de hello toohave hello décidé nom et nom de hello de configuration de hello.  Dans cet exemple d’utilisation, nœud de hello est 'isvbox' et la configuration de hello est 'ISVBoxConfig'.  Par conséquent, le nom de configuration du nœud hello (toobe spécifié dans DeploymentTemplate.json) est 'ISVBoxConfig.isvbox'.  

## <a name="step-3-adding-required-dsc-resources-toohello-pull-server"></a>Étape 3 : Ajout de serveur d’extraction toohello de ressources DSC requis
Hello PowerShell Gallery est instrumentée tooinstall des ressources DSC dans votre compte Azure Automation.  Accédez toohello ressource puis sur « Déployer tooAzure Automation » hello.

![Exemple de la PowerShell Gallery](./media/automation-dsc-cd-chocolatey/xNetworking.PNG)

Une autre technique récemment ajouté toohello portail Azure vous permet de toopull dans des modules ou des modules de mise à jour. Cliquez sur ressources du compte Automation hello, vignette de ressources hello et enfin de vignette de Modules hello.  icône de parcourir la galerie Hello vous permet de liste de hello toosee des modules dans la galerie de hello, afficher des détails et finalement importer dans votre compte Automation. Ceci est un excellent moyen tookeep vos modules de toodate de tootime de temps. Et, fonction d’importation hello vérifie les dépendances avec d’autres tooensure modules que Nothing est désynchronisé.

Ou bien, il est approche manuelle de hello.  structure de dossiers Hello d’un Module d’intégration pour un ordinateur Windows PowerShell est un peu différent à partir de la structure de dossiers hello attendu par hello Azure Automation.  Cette différence nécessite une légère modification de votre part.  Mais il n’est pas difficile, et il est effectué en une seule fois par ressource (sauf si vous souhaitez tooupgrade ultérieurement.)  Pour plus d’informations sur la création de modules d’intégration PowerShell, consultez cet article : [Création de modules d’intégration pour Azure Automation](https://azure.microsoft.com/blog/authoring-integration-modules-for-azure-automation/)

* Installez le module hello dont vous avez besoin sur votre station de travail, comme suit :
  * Installez [Windows Management Framework v5](http://aka.ms/wmf5latest) (inutile pour Windows 10)
  * `Install-Module –Name MODULE-NAME`< — extrait hello du module à partir de hello PowerShell Gallery 
* Dossier du module hello copie à partir de `c:\Program Files\WindowsPowerShell\Modules\MODULE-NAME` tooa du dossier temporaire 
* Supprimer les exemples et la documentation à partir du dossier principal hello 
* Dossier principal de hello zip, noms de fichier ZIP de hello exactement identiques hello en tant que dossier de hello 
* Placez le fichier ZIP de hello dans un emplacement accessible HTTP, tels que le stockage blob dans un compte de stockage Azure.
* Exécutez cette commande PowerShell :
  
      New-AzureRmAutomationModule `
          -ResourceGroupName MY-AUTOMATION-RG -AutomationAccountName MY-AUTOMATION-ACCOUNT `
          -Name MODULE-NAME –ContentLink "https://STORAGE-URI/CONTAINERNAME/MODULE-NAME.zip"

exemple de Hello inclus effectue ces étapes pour cChoco et xNetworking. Consultez hello [Notes](#notes) pour un traitement spécial pour cChoco.

## <a name="step-4-adding-hello-node-configuration-toohello-pull-server"></a>Étape 4 : Ajouter le serveur collecteur toohello hello nœud configuration
Il n’est rien de spécial sur hello première fois que vous importez votre configuration dans la compilation et le serveur collecteur de hello.  Tous les importer/compilations suivantes de hello même apparence configuration hello exactement identiques.  Chaque fois que vous mettez à jour votre package et que vous avez besoin de toopush en tooproduction vous effectuez cette étape après avoir vérifié le fichier de configuration hello est correcte : notamment hello une nouvelle version de votre package.  Voici le fichier de configuration hello et PowerShell :

ISVBoxConfig.ps1:

    Configuration ISVBoxConfig 
    { 
        Import-DscResource -ModuleName cChoco 
        Import-DscResource -ModuleName xNetworking

        Node "isvbox" {   

            cChocoInstaller installChoco 
            { 
                InstallDir = "C:\choco" 
            }

            WindowsFeature installIIS 
            { 
                Ensure="Present" 
                Name="Web-Server" 
            }

            xFirewall WebFirewallRule 
            { 
                Direction = "Inbound" 
                Name = "Web-Server-TCP-In" 
                DisplayName = "Web Server (TCP-In)" 
                Description = "IIS allow incoming web site traffic." 
                DisplayGroup = "IIS Incoming Traffic" 
                State = "Enabled" 
                Access = "Allow" 
                Protocol = "TCP" 
                LocalPort = "80" 
                Ensure = "Present" 
            }

            cChocoPackageInstaller trivialWeb 
            {            
                Name = "trivialweb" 
                Version = "1.0.0" 
                Source = “MY-NUGET-V2-SERVER-ADDRESS” 
                DependsOn = "[cChocoInstaller]installChoco", 
                "[WindowsFeature]installIIS" 
            } 
        }    
    }

New-ConfigurationScript.ps1:

    Import-AzureRmAutomationDscConfiguration ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -SourcePath C:\temp\AzureAutomationDsc\ISVBoxConfig.ps1 ` 
        -Published –Force

    $jobData = Start-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -ConfigurationName ISVBoxConfig 

    $compilationJobId = $jobData.Id

    Get-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -Id $compilationJobId

Résultat de ces étapes dans une nouvelle configuration de nœud nommé « ISVBoxConfig.isvbox » qui est placé sur un serveur collecteur de hello.  nom de configuration de nœud Hello est construit comme « configurationName.nodeName ».

## <a name="step-5-creating-and-maintaining-package-metadata"></a>Étape 5 : création et gestion des métadonnées de packages
Pour chaque package que vous placez dans un référentiel de packages hello, vous avez besoin d’un nuspec qui le décrit.  Ce nuspec doit être compilé et stocké sur votre serveur NuGet. Cette opération est décrite [ici](http://docs.nuget.org/create/creating-and-publishing-a-package).  Vous pouvez utiliser MyGet.org comme serveur NuGet.  Bien que ce service soit payant, ils proposent gratuitement une référence SKU pour débutants.  Rendez-vous sur NuGet.org pour obtenir des instructions sur l’installation de votre propre serveur NuGet pour vos packages privés.

## <a name="step-6-tying-it-all-together"></a>Étape 6 : Exemple complet
Chaque fois une version transmet les questions et réponses et est approuvée pour le déploiement, package de hello est créé, nuspec nupkg et mises à jour déployées toohello NuGet serveur.  En outre, la configuration de hello (étape 4 ci-dessus) doit être tooagree mis à jour avec le nouveau numéro de version hello.  Il doit être envoyé du serveur collecteur de toohello et compilé.  À ce stade, il est des machines virtuelles toohello qui dépendent de cette mise à jour de configuration toopull hello et l’installer.  Chacune de ces mises à jour est simple et ne nécessite qu’une ou deux lignes PowerShell.  Dans les cas de hello de Visual Studio Team Services, certains d'entre eux sont encapsulées dans les tâches de génération qui peuvent être chaînées dans une build.  Cet [article](https://www.visualstudio.com/en-us/docs/alm-devops-feature-index#continuous-delivery) fournit plus de détails.  Cela [référentiel GitHub](https://github.com/Microsoft/vso-agent-tasks) détails hello diverses tâches de build disponible.

## <a name="notes"></a>Remarques
Cet exemple d’utilisation commence par une machine virtuelle à partir d’une image de Windows Server 2012 R2 générique hello la galerie Azure.  Vous pouvez commencer à partir de n’importe quelle image stockée, puis modifier à partir de là, avec une configuration DSC hello.  Toutefois, la modification de configuration qui est intégrée dans une image est beaucoup plus difficile que la mise à jour dynamique de configuration de hello à l’aide de DSC.

Vous n’avez toouse un modèle ARM et hello VM extension toouse cette technique avec vos machines virtuelles.  Et toobe n’ont pas vos machines virtuelles sur Azure toobe sous gestion de CD.  Tout ce qui est nécessaire que Chocolatey être installé et hello LCM configurée sur hello machine virtuelle afin qu’il sache où hello serveur collecteur est.  

Bien entendu, lorsque vous mettez à jour un package sur un ordinateur virtuel qui est en production, vous devez tootake cette machine virtuelle hors rotation pendant l’installation de mise à jour hello.  La procédure varie considérablement.  Par exemple, avec une machine virtuelle placée derrière un équilibreur de charge Azure, vous pouvez ajouter une sonde personnalisée.  Lors de la mise à jour hello machine virtuelle, avez point de terminaison de sonde hello retourner un 400.  toocause nécessaires de Hello affinage cette modification peut être à l’intérieur de votre configuration, que pouvez hello tooswitch affinage refaites-le tooreturning 200 une fois la mise à jour hello.

La source complète de cet exemple se trouve dans ce [projet Visual Studio](https://github.com/sebastus/ARM/tree/master/CDIaaSVM) sur GitHub.

## <a name="related-articles"></a>Articles connexes
* [Vue d'ensemble d'Azure Automation DSC](automation-dsc-overview.md)
* [Applets de commande Azure Automation DSC](https://msdn.microsoft.com/library/mt244122.aspx)
* [Gestion de machines avec Azure Automation DSC](automation-dsc-onboarding.md)

