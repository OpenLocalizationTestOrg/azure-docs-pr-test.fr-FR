---
title: "aaaDeploy hello service de mobilité de récupération de Site dans Azure Automation DSC | Documents Microsoft"
description: "Décrit comment toouse Azure Automation DSC tooautomatically déployer Azure Site Recovery mobilité hello et agent Azure VM de VMware et de tooAzure de réplication de serveur physique"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a>Déployer le service de mobilité hello dans Azure Automation DSC pour la réplication de machine virtuelle
Dans Operations Management Suite, nous fournissons une solution complète de sauvegarde et de récupération d’urgence que vous pouvez exploiter dans le cadre de votre plan de continuité d’activité.

Nous avions commencé avec Hyper-V en utilisant Hyper-V Replica. Mais nous avons développé toosupport une installation hétérogène, car les clients ont plusieurs hyperviseurs et plateformes dans leurs clouds.

Si vous exécutez les charges de travail VMware et/ou vos serveurs physiques aujourd'hui, un serveur d’administration exécute tous les Hello composants d’Azure Site Recovery dans votre environnement toohandle hello communication et les données de la réplication avec Azure, quand Azure est la destination.

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a>Déployer le service de mobilité de récupération de Site hello à l’aide d’Automation DSC
Commençons par analyser rapidement les opérations réellement effectuées par ce serveur d’administration.

serveur d’administration Hello exécute plusieurs rôles de serveur. L’un de ces rôles est la *configuration*, qui coordonne la communication et gère les processus de réplication et de récupération des données.

En outre, hello *processus* rôle fait Office de passerelle de réplication. Ce rôle reçoit des données de réplication à partir d’ordinateurs de la source protégée, elle optimise avec la mise en cache, la compression et le chiffrement et envoie ensuite compte de stockage Azure tooan. Une des fonctions hello pour le rôle de processus hello est également toopush installation de machines de tooprotected de service de mobilité hello et effectuer la détection automatique des ordinateurs virtuels VMware.

En l’absence d’une restauration à partir d’Azure, hello *cible maître* rôle traitera les données de réplication hello dans le cadre de cette opération.

Pour les ordinateurs de hello protégé, nous s’appuient sur hello *service mobilité*. Ce composant est déployé tooevery machine (VMware VM ou serveur physique) que vous souhaitez tooreplicate tooAzure. Il capture les écritures de données sur l’ordinateur de hello et les transmet le serveur d’administration toohello (rôle de processus).

Lorsque vous êtes confronté à la continuité d’activité, il est important toounderstand vos charges de travail, votre infrastructure et les composants de hello impliqués. Vous pouvez ensuite requise hello pour votre objectif de temps de récupération (RTO) et l’objectif de point de récupération (RPO). Dans ce contexte, hello service mobilité est tooensuring clé vos charges de travail protégés comme prévu.

Alors, comment pouvez-vous nous assurer de manière optimisée que l’installation est protégée et fiable, à l’aide de certains composants Operations Management Suite ?

Cet article fournit un exemple de comment vous pouvez utiliser Azure Automation état Configuration souhaité (DSC), ainsi que de la récupération de Site, tooensure qui :

* service de mobilité Hello et l’agent de machine virtuelle Azure sont toohello déployé des ordinateurs Windows que vous souhaitez tooprotect.
* service de mobilité Hello et l’agent de machine virtuelle Azure sont toujours en cours d’exécution lorsque Azure est la cible de réplication hello.

## <a name="prerequisites"></a>Composants requis
* Un programme d’installation de référentiel toostore hello requis
* Un tooregister de phrase secrète de référentiel toostore hello requis avec le serveur d’administration hello

  > [!NOTE]
  > Une phrase secrète unique est générée pour chaque serveur d’administration. Si vous vous apprêtez à toodeploy plusieurs serveurs d’administration, vous avez tooensure que hello correct de mot de passe est stocké dans le fichier de passphrase.txt hello.
  >
  >
* Windows Management Framework (WMF) 5.0 est installé sur les ordinateurs hello que vous souhaitez tooenable pour la protection (il s’agit d’une exigence pour Automation DSC)

  > [!NOTE]
  > Si vous voulez que les ordinateurs de DSC pour Windows toouse qui disposent de WMF 4.0, consultez la section de hello [DSC d’utilisation dans des environnements déconnectés](## Use DSC in disconnected environments).
  

service de mobilité Hello peut être installé via la ligne de commande hello et accepte plusieurs arguments. C’est pourquoi vous avez besoin des fichiers binaires de hello toohave (après les extraire à partir de votre programme d’installation) et les stocker dans un endroit où vous pouvez les récupérer à l’aide d’une configuration DSC.

## <a name="step-1-extract-binaries"></a>Étape 1 : extraction des fichiers binaires
1. fichiers hello tooextract dont vous avez besoin pour cette configuration, accédez à toohello suivant active sur votre serveur d’administration :

    **\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**

    Dans ce dossier, vous devriez voir un fichier MSI nommé :

    **Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**

    Utilisez hello suivant le programme d’installation de commande tooextract hello :

    **.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**
2. Sélectionnez tous les fichiers et les envoyer tooa de dossier (zippé) compressé.

Vous avez maintenant binaires hello que vous avez besoin du programme d’installation de tooautomate hello Hello service mobilité à l’aide d’Automation DSC.

### <a name="passphrase"></a>Phrase secrète
Ensuite, vous devez toodetermine où vous souhaitez tooplace ce dossier compressé. Vous pouvez utiliser un compte de stockage Azure, comme indiqué par la suite, toostore hello phrase secrète que vous avez besoin pour le programme d’installation hello. l’agent de Hello inscrira puis avec le serveur d’administration hello dans le cadre du processus de hello.

phrase secrète Hello que vous avez obtenu lorsque vous avez déployé le serveur d’administration hello peut être enregistré fichier de texte tooa comme passphrase.txt.

Placez le dossier zippé de hello et mot de passe hello dans un conteneur dédié Bonjour compte de stockage Azure.

![Emplacement du dossier](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

Si vous préférez tookeep ces fichiers sur un partage sur votre réseau, vous pouvez le faire. Vous devez simplement tooensure que les ressources hello DSC que vous utiliserez ultérieurement ont accès et peuvent obtenir le programme d’installation hello et la phrase secrète.

## <a name="step-2-create-hello-dsc-configuration"></a>Étape 2 : Créer la configuration de hello DSC
le programme d’installation Hello dépend de WMF 5.0. Pour hello machine toosuccessfully configuration hello via Automation DSC, WMF 5.0 doit toobe présent.

environnement de Hello utilise hello suivant l’exemple de configuration DSC :

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
configuration de Hello fera suivant de hello :

* les variables Hello indiquera les configuration hello où tooget hello les fichiers binaires pour le service de mobilité hello et agent de machine virtuelle Azure hello, où tooget hello phrase secrète et toostore hello de sortie.
* Hello configuration importera ressources xPSDesiredStateConfiguration DSC de hello, afin que vous puissiez utiliser `xRemoteFile` fichiers hello toodownload référentiel de hello.
* configuration de Hello créera un répertoire où vous souhaitez les fichiers binaires de toostore hello.
* ressource archive de Hello extrait les fichiers hello à partir du dossier compressé hello.
* ressource d’installation de package de Hello installera le service de mobilité de hello de hello UNIFIEDAGENT. Programme d’installation EXE avec des arguments spécifiques hello. (variables hello construire les arguments hello peut-être toobe modifié tooreflect votre environnement.)
* Hello AzureAgent ressource installera l’agent Azure VM hello, ce qui est recommandé sur chaque machine virtuelle qui s’exécute dans Azure. l’agent de machine virtuelle Azure Hello rend également possible tooadd extensions toohello machine virtuelle après le basculement.
* Hello service ou les ressources garantit que hello liées à des services de mobilité et hello services Azure sont toujours en cours d’exécution.

Enregistrer la configuration de hello sous **ASRMobilityService**.

> [!NOTE]
> N’oubliez pas tooreplace hello CSIP dans votre configuration tooreflect hello réel management server, afin que hello agent est connecté correctement et utilisera le mot de passe correct hello.
>
>

## <a name="step-3-upload-tooautomation-dsc"></a>Étape 3 : Téléchargez tooAutomation DSC
Étant donné que configuration hello DSC que vous avez effectuées pour importer un module de ressources DSC requis (xPSDesiredStateConfiguration), vous devez tooimport ce module dans Automation avant le téléchargement de la configuration de hello DSC.

Connexion tooyour compte Automation, parcourir trop**actifs** > **Modules**, puis cliquez sur **parcourir la galerie**.

Ici, vous pouvez rechercher pour le module de hello et importez-le tooyour compte.

![Importer le module](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

Lorsque vous avez terminé de cela, accédez tooyour ordinateur où vous avez des modules du Gestionnaire de ressources Azure hello installés et continuer la configuration de DSC tooimport hello nouvellement créé.

### <a name="import-cmdlets"></a>Importer les applets de commande
Dans PowerShell, connectez-vous tooyour abonnement Azure. Modifier hello applets de commande tooreflect votre environnement et capturer les informations de votre compte Automation dans une variable :

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

Télécharger hello configuration tooAutomation DSC à l’aide de hello suivant l’applet de commande :

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a>Compilation de configuration hello dans Automation DSC
Ensuite, vous devez configuration hello toocompile Automation DSC, afin que vous puissiez démarrer tooregister nœuds tooit. Que faire, hello suivant l’applet de commande en cours d’exécution :

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

Cela peut prendre quelques minutes, étant donné que vous déployez essentiellement le service collecteur DSC hello configuration toohello hébergé.

Une fois que vous compilez la configuration de hello, vous pouvez récupérer des informations sur les travaux hello à l’aide de PowerShell (Get-AzureRmAutomationDscCompilationJob) ou à l’aide de hello [portail Azure](https://portal.azure.com/).

![Tâche de récupération](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

Vous avez maintenant publié et téléchargé votre tooAutomation de configuration DSC DSC.

## <a name="step-4-onboard-machines-tooautomation-dsc"></a>Étape 4 : Machines intégré tooAutomation DSC
> [!NOTE]
> Une des conditions préalables de hello pour ce scénario est que vos ordinateurs Windows sont mis à jour avec la version la plus récente de WMF hello. Vous pouvez télécharger et installer la version correcte de hello pour votre plateforme de hello [centre de téléchargement](https://www.microsoft.com/download/details.aspx?id=50395).
>
>

Vous allez maintenant créer un metaconfig pour DSC que vous allez appliquer tooyour nœuds. toosucceed avec cela, vous devez tooretrieve hello point de terminaison URL et hello clé primaire pour votre compte Automation sélectionné dans Azure. Vous pouvez trouver ces valeurs sous **clés** sur hello **tous les paramètres** panneau pour hello compte Automation.

![Valeurs de clé](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

Dans cet exemple, vous disposez d’un serveur physique Windows Server 2012 R2 que vous souhaitez tooprotect à l’aide de récupération de Site.

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a>Recherchez les opérations de changement de nom de fichier dans le Registre de hello en attente
Avant de commencer serveur hello de tooassociate avec le point de terminaison Automation DSC hello, nous vous recommandons de vérifier pour les opérations de changement de nom de fichier dans le Registre de hello en attente. Ils peuvent interdire le programme d’installation Bonjour de terminer en raison tooa redémarrage en attente.

Exécutez hello suivant tooverify applet de commande qu’il n’existe aucun redémarrage en attente sur le serveur de hello :

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
Si cela apparaît vide, vous êtes tooproceed OK. Si ce n’est pas le cas, vous devez résoudre ce problème en redémarrant le serveur de hello pendant une fenêtre de maintenance.

configuration de hello tooapply sur le serveur de hello, hello PowerShell Integrated Scripting Environment (ISE) de démarrer et exécuter hello script suivant. Il s’agit essentiellement une configuration DSC locale qui sera hello Gestionnaire de Configuration Local moteur tooregister avec hello service Automation DSC de demander et de récupérer la configuration spécifique de hello (ASRMobilityService.localhost).

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

Cette configuration entraîne hello Gestionnaire de Configuration Local tooregister moteur lui-même avec Automation DSC. Il détermine également comment le moteur de hello doit fonctionner, ce qu’il doit faire s’il existe une dérive de la configuration (ApplyAndAutoCorrect) et comment il doit continuer avec la configuration de hello si un redémarrage est nécessaire.

Une fois que vous exécutez ce script, nœud de hello doit démarrer tooregister avec Automation DSC.

![Enregistrement du nœud en cours](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

Si vous revenez toohello portail Azure, vous pouvez voir ce nœud nouvellement inscrit hello maintenant s’affiche dans le portail de hello.

![Nœud dans le portail de hello](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

Sur le serveur de hello, vous pouvez exécuter hello suivant PowerShell tooverify applet de commande qui hello nœud a été correctement enregistré :

```powershell
Get-DscLocalConfigurationManager
```

Une fois la configuration de hello a été extraite et appliquées toohello serveur, vous pouvez vérifier cela en exécutant hello suivant l’applet de commande :

```powershell
Get-DscConfigurationStatus
```

sortie de Hello montre que ce serveur hello a extraite avec succès sa configuration :

![Sortie](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

En outre, le programme d’installation de hello mobilité service a son propre journal qui se trouvent à *lecteur_système*\ProgramData\ASRSetupLogs.

Et voilà ! Vous avez désormais déployé et inscrit le service de mobilité hello sur ordinateur hello que vous souhaitez tooprotect à l’aide de récupération de Site. DSC permet de garantir que les services hello requis sont toujours en cours d’exécution.

![Déploiement réussi](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

Une fois que le serveur d’administration hello détecte un déploiement réussi de hello, vous pouvez configurer la protection et activer la réplication sur l’ordinateur de hello à l’aide de récupération de Site.

## <a name="use-dsc-in-disconnected-environments"></a>Utilisation de DSC dans des environnements déconnectés
Si vos ordinateurs ne sont pas connecté toohello Internet, vous pouvez toujours s’appuient sur DSC toodeploy et configurer le service de mobilité hello sur les charges de travail hello que vous souhaitez tooprotect.

Vous pouvez instancier votre propre serveur de collecteur DSC dans votre environnement tooessentially fournir hello les mêmes fonctionnalités que vous obtenez d’Automation DSC. Autrement dit, les clients de hello seront hello configuration du collecteur (après son inscription) toohello DSC de point de terminaison. Toutefois, une autre option est toomanually push hello DSC configuration tooyour les ordinateurs, localement ou à distance.

Notez que dans cet exemple, il existe un paramètre ajouté pour le nom de l’ordinateur hello. les fichiers distants Hello se trouvent désormais sur un partage distant doit être accessible par les ordinateurs hello que vous souhaitez tooprotect. fin de Hello du script de hello applique la configuration de hello, puis démarre tooapply hello DSC configuration toohello cible ordinateur.

### <a name="prerequisites"></a>Composants requis
Vérifiez que hello xPSDesiredStateConfiguration PowerShell est installé. Pour les ordinateurs Windows où WMF 5.0 est installé, vous pouvez installer le module xPSDesiredStateConfiguration de hello en exécutant hello suivant l’applet de commande sur les ordinateurs cibles de hello :

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

Vous pouvez également télécharger et enregistrer le module de hello en cas de besoin toodistribute il tooWindows les ordinateurs qui disposent de WMF 4.0. Exécutez cette applet de commande sur une machine sur laquelle PowerShellGet (WMF 5.0) est installé :

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

Assurez-vous également de WMF 4.0, ce hello [mise à jour Windows 8.1 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) est installé sur les ordinateurs hello.

Hello configuration suivante peut être appliquée tooWindows les ordinateurs qui ont WMF 5.0 et WMF 4.0 :

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

Si vous souhaitez tooinstantiate votre propre serveur de collecteur DSC sur vos capacités d’hello toomimic réseau d’entreprise que vous pouvez obtenir à partir de l’Automation DSC, consultez [configuration d’un serveur de collecteur web DSC](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a>Déploiement d’une configuration DSC à l’aide d’un modèle Azure Resource Manager (facultatif)
Cet article se sont concentrées sur comment vous pouvez créer votre propre tooautomatically de configuration DSC déployer le service de mobilité hello et hello Agent de machine virtuelle Azure--et vous assurer qu’ils s’exécutent sur des ordinateurs de hello que vous souhaitez tooprotect. Nous avons également un modèle Azure Resource Manager qui sera déployée de ce compte d’Azure Automation DSC configuration tooa nouveau ou existant. modèle de Hello utilisera les paramètres d’entrée toocreate Automation actifs qui contiendront les variables hello pour votre environnement.

Après avoir déployé le modèle de hello, vous pouvez simplement faire référence toostep 4 dans ce guide de tooonboard vos ordinateurs.

modèle de Hello fera suivant de hello :

1. Utilisation d’un compte Automation existant ou création d’un nouveau compte
2. Prenez les paramètres d’entrée pour :
   * ASRRemoteFile--emplacement hello où vous avez stocké le programme d’installation de service de mobilité hello
   * ASRPassphrase--emplacement hello où vous avez stocké le fichier de passphrase.txt hello
   * ASRCSEndpoint--adresse IP de hello de votre serveur d’administration
3. Importer le module PowerShell de xPSDesiredStateConfiguration hello
4. Créer et compiler la configuration DSC de hello

Hello toutes les étapes précédentes aura lieu dans l’ordre de droite hello, afin que vous pouvez démarrer l’intégration de vos ordinateurs pour la protection.

modèle Hello, avec des instructions pour le déploiement, se trouve sur [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).

Déployer le modèle de hello à l’aide de PowerShell :

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous déployez des agents de service de mobilité hello, vous pouvez [activer la réplication](site-recovery-vmware-to-azure.md) pour les ordinateurs virtuels de hello.
