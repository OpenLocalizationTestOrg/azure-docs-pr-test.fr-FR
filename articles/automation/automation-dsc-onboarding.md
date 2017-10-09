---
title: ordinateurs aaaOnboarding pour la gestion par Azure Automation DSC | Documents Microsoft
description: Comment toosetup machines pour la gestion avec Azure Automation DSC
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a>Gestion de machines avec Azure Automation DSC

## <a name="why-manage-machines-with-azure-automation-dsc"></a>Pourquoi gérer des machines avec Azure Automation DSC ?

Tout comme le service [Desired State Configuration de PowerShell](https://technet.microsoft.com/library/dn249912.aspx), le Desired State Configuration d’Azure Automation est un service de gestion de configuration simple et puissant pour les nœuds DSC (machines physiques et virtuelles) dans n’importe quel centre de données sur le cloud ou sur site. Il permet de faire évoluer des milliers d’ordinateurs rapidement et facilement à partir d’un emplacement central et sécurisé. Vous pouvez facilement intégrer machines, affecter les configurations déclaratives et afficher des rapports affichant chaque ordinateur de l’état toohello souhaité de compatibilité spécifié. couche de gestion Azure Automation DSC Hello est tooDSC quel couche de gestion Azure Automation hello est tooPowerShell écriture de scripts. En d’autres termes, Bonjour comme Azure Automation vous permet de gérer des scripts PowerShell, il vous permet également de gérer les configurations DSC. toolearn en savoir plus sur les avantages de hello de l’utilisation d’Azure Automation DSC, consultez [vue d’ensemble d’Azure Automation DSC](automation-dsc-overview.md).

Azure Automation DSC peut être utilisé toomanage différents ordinateurs :

* Machines virtuelles Azure (classiques)
* Machines virtuelles Azure
* Machines virtuelles Amazon Web Services (AWS)
* Machines physiques/virtuelles Windows locales ou dans un cloud autre qu’Azure/AWS
* Machines physiques/virtuelles Linux sur site, dans Azure, ou dans un cloud autre qu’Azure

En outre, si vous n’êtes pas prêt toomanage configuration de l’ordinateur à partir du cloud de hello, Azure Automation DSC peut également servir comme un point de terminaison de rapport uniquement. Cela vous permet de configuration souhaitée de tooset (push) via DSC sur site et afficher les détails rapports riches sur la conformité du nœud avec hello souhaité état dans Azure Automation.

Hello les sections suivantes décrire comment vous pouvez l’intégrer chaque type d’ordinateur tooAzure Automation DSC.

## <a name="azure-virtual-machines-classic"></a>Machines virtuelles Azure (classiques)

Dans Azure Automation DSC, vous pouvez facilement intégrer des machines virtuelles Azure (classique) pour la gestion de la configuration à l’aide de hello portail Azure ou PowerShell. Dans les coulisses de hello et sans un administrateur ayant tooremote dans hello VM, hello extension de Configuration d’état souhaité Azure VM inscrit hello machine virtuelle dans Azure Automation DSC. Étant donné que hello extension de Configuration d’état souhaité Azure VM s’exécute de façon asynchrone, étapes tootrack sa progression ou de dépanner il sont fournies dans hello [ **l’intégration de machine virtuelle Azure de dépannage** ](#troubleshooting-azure-virtual-machine-onboarding)section ci-dessous.

### <a name="azure-portal"></a>Portail Azure

Bonjour [portail Azure](http://portal.azure.com/), cliquez sur **Parcourir** -> **machines virtuelles (classiques)**. Sélectionnez hello Windows machine virtuelle tooonboard. Dans le panneau de tableau de bord de l’ordinateur virtuel de hello, cliquez sur **tous les paramètres** -> **Extensions** -> **ajouter**  ->   **Azure Automation DSC** -> **créer**. Entrez hello [les valeurs de gestionnaire de Configuration Local DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) requis pour votre cas d’usage, clé d’inscription de votre compte Automation et URL d’inscription et éventuellement un toohello de tooassign de configuration de nœud machine virtuelle.

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

URL d’inscription toofind hello et de clé pour la machine de hello hello Automation compte tooonboard, consultez hello [ **sécuriser l’inscription** ](#secure-registration) section ci-dessous.

### <a name="powershell"></a>PowerShell

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a>Machines virtuelles Azure

Azure Automation DSC vous permet de s’intégrer facilement des machines virtuelles Azure pour la gestion de la configuration à l’aide de hello portail Azure, de modèles Azure Resource Manager ou de PowerShell. Dans les coulisses de hello et sans un administrateur ayant tooremote dans hello VM, hello extension de Configuration d’état souhaité Azure VM inscrit hello machine virtuelle dans Azure Automation DSC. Étant donné que hello extension de Configuration d’état souhaité Azure VM s’exécute de façon asynchrone, étapes tootrack sa progression ou de dépanner il sont fournies dans hello [ **l’intégration de machine virtuelle Azure de dépannage** ](#troubleshooting-azure-virtual-machine-onboarding)section ci-dessous.

### <a name="azure-portal"></a>Portail Azure

Bonjour [portail Azure](https://portal.azure.com/), accédez compte Azure Automation de toohello où vous souhaitez tooonboard virtual machines. Tableau de bord de compte Automation hello, cliquez sur **nœuds DSC** -> **ajouter Azure VM**.

Sous **sélectionner des machines virtuelles tooonboard**, sélectionnez un ou plusieurs Azure virtual machines tooonboard.

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

Sous **configurer les données d’inscription**, entrez hello [les valeurs de gestionnaire de Configuration Local DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) requis pour votre cas d’usage et éventuellement un toohello de tooassign de configuration de nœud machine virtuelle.

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a>Modèles Microsoft Azure Resource Manager

Machines virtuelles peuvent être déployés et embarquées tooAzure Automation DSC via des modèles Azure Resource Manager. Consultez [configurer une machine virtuelle via l’extension DSC et Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) pour un exemple de modèle qui onboards un tooAzure existant de la machine virtuelle Automation DSC. toofind hello URL d’enregistrement clé et l’inscription effectuée en tant qu’entrée dans ce modèle, consultez hello [ **sécuriser l’inscription** ](#secure-registration) section ci-dessous.

### <a name="powershell"></a>PowerShell

Hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) applet de commande peut être des ordinateurs virtuels utilisés tooonboard hello portail Azure via PowerShell.

## <a name="amazon-web-services-aws-virtual-machines"></a>Machines virtuelles Amazon Web Services (AWS)

Vous pouvez facilement intégrer Amazon Web Services virtuels pour la gestion de la configuration par Azure Automation DSC à l’aide de hello AWS DSC Toolkit. Plus d’informations sur les outils d’analyse hello [ici](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a>Machines physiques/virtuelles Windows locales ou dans un cloud autre qu’Azure/AWS

Les ordinateurs Windows local et des ordinateurs Windows dans les clouds non-Azure (par exemple, Amazon Web Services) peuvent également être embarquées tooAzure Automation DSC, tant qu’ils ont un accès sortant toohello internet, via les quelques étapes simples :

1. Vérifiez que hello dernière version de [WMF 5](http://aka.ms/wmf5latest) est installé sur les ordinateurs hello souhaité tooonboard tooAzure Automation DSC.
2. Suivez les instructions de hello de section [ **DSC de génération de métaconfigurations** ](#generating-dsc-metaconfigurations) ci-dessous toogenerate un dossier contenant hello nécessaire métaconfigurations de DSC.
3. À distance s’appliquent hello DSC PowerShell métaconfiguration toohello ordinateurs tooonboard. **ordinateur Hello cette commande est exécutée à partir de doit avoir la version la plus récente de hello [WMF 5](http://aka.ms/wmf5latest) installé**:

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. Si vous ne pouvez pas appliquer hello DSC PowerShell métaconfigurations à distance, copiez le dossier de métaconfigurations de hello de l’étape 2 sur tooonboard de chaque ordinateur. Appelez ensuite **Set-DscLocalConfigurationManager** localement sur chaque ordinateur tooonboard.
5. À l’aide de hello portail Azure ou des applets de commande, vérifiez que hello machines tooonboard maintenant s’affichent en tant que nœuds DSC inscrit dans votre compte Azure Automation.

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a>Machines physiques/virtuelles Linux sur site, dans Azure, ou dans un cloud autre qu’Azure

Les ordinateurs locaux Linux, les ordinateurs Linux dans Azure, et les ordinateurs Linux dans des clouds non-Azure peuvent également être embarquées tooAzure Automation DSC, tant qu’ils ont un accès sortant toohello internet, via les quelques étapes simples :

1. Vérifiez que hello dernière version de [PowerShell DSC pour Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) est installé sur les ordinateurs hello souhaité tooonboard tooAzure Automation DSC.
2. Si hello [valeurs par défaut du Gestionnaire de Configuration Local DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) correspond à votre cas d’usage, et que vous souhaitez tooonboard machines telles qu’elles **les deux** extraient et tooAzure Automation DSC de rapports :

   + Sur chaque Linux ordinateur tooonboard tooAzure Automation DSC, utilisez tooonboard Register.py à l’aide de hello est par défaut du Gestionnaire de Configuration Local DSC PowerShell :

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + toofind hello URL d’enregistrement clé et l’inscription de votre compte Automation, consultez hello [ **sécuriser l’inscription** ](#secure-registration) section ci-dessous.

     Si hello Gestionnaire de Configuration Local DSC PowerShell par défaut **faire** **pas** correspond à votre cas d’usage ou si vous souhaitez tooonboard machines telles qu’elles uniquement de rapport tooAzure Automation DSC, mais ne tirez pas configuration ou des modules PowerShell à partir de celui-ci, suivez les étapes 3 à 6. Sinon, passez directement toostep 6.

3. Suivez les instructions de hello Bonjour [ **DSC de génération de métaconfigurations** ](#generating-dsc-metaconfigurations) section ci-dessous toogenerate un dossier contenant des métaconfigurations de DSC hello si nécessaire.
4. À distance s’appliquent hello DSC PowerShell métaconfiguration toohello ordinateurs tooonboard :

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

ordinateur Hello cette commande est exécutée à partir de doit avoir la version la plus récente de hello [WMF 5](http://aka.ms/wmf5latest) installé.

1. Si vous ne pouvez pas appliquer hello DSC PowerShell métaconfigurations à distance, pour chaque tooonboard ordinateur Linux, copiez machine toothat correspondante de hello métaconfiguration à partir du dossier à l’étape 5 sur l’ordinateur Linux de hello hello. Appelez ensuite `SetDscLocalConfigurationManager.py` localement sur chaque ordinateur Linux, vous souhaitez tooonboard tooAzure Automation DSC :

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. À l’aide de hello portail Azure ou des applets de commande, vérifiez que hello machines tooonboard maintenant s’affichent en tant que nœuds DSC inscrit dans votre compte Azure Automation.

## <a name="generating-dsc-metaconfigurations"></a>Génération de métaconfigurations DSC

toogenerically intégrer un ordinateur tooAzure Automation DSC, un [métaconfiguration DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) peut être générée qui, lorsque appliqué, indique à l’agent de hello DSC sur toopull d’ordinateur hello d’et/ou rapport tooAzure Automation DSC. Métaconfigurations DSC Azure Automation DSC peuvent être générées à l’aide d’une configuration DSC de PowerShell, ou applets de commande PowerShell d’automatisation Azure hello.

> [!NOTE]
> DSC métaconfigurations contient hello secrets nécessités tooonboard un tooan machine compte Automation pour la gestion. Assurez-vous que tooproperly protéger n’importe quel métaconfigurations DSC que vous créez, ou les supprimer après utilisation.

### <a name="using-a-dsc-configuration"></a>Utilisation d’une configuration DSC

1. Ouvrez hello PowerShell ISE en tant qu’administrateur sur un ordinateur dans votre environnement local. machine de Hello doit avoir la version la plus récente de hello [WMF 5](http://aka.ms/wmf5latest) installé.
2. Copiez hello localement le script suivant. Ce script contient une configuration DSC PowerShell pour la création de métaconfigurations et un tookick commande désactiver la création de métaconfiguration hello.

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. Renseignez la clé d’enregistrement hello et l’URL pour votre compte Automation, ainsi que les noms de hello de hello machines tooonboard. Tous les autres paramètres sont facultatifs. toofind hello URL d’enregistrement clé et l’inscription de votre compte Automation, consultez hello [ **sécuriser l’inscription** ](#secure-registration) section ci-dessous.
4. Si vous souhaitez hello machines tooreport DSC état informations tooAzure Automation DSC, mais il extrayez pas de configuration ou des modules PowerShell, définissez hello **ReportOnly** tootrue de paramètre.
5. Exécutez le script de hello. Vous devez maintenant avoir un dossier appelé **DscMetaConfigs** dans votre répertoire de travail contenant métaconfigurations de DSC PowerShell hello pour tooonboard de machines hello (en tant qu’administrateur) :

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a>À l’aide des applets de commande hello Azure Automation

Si les valeurs par défaut du Gestionnaire de Configuration Local DSC PowerShell hello correspond à votre cas d’usage, et que vous souhaitez tooonboard machines tels qu’ils extraient et rapport tooAzure Automation DSC, applets de commande hello Azure Automation fournissent une méthode simplifiée de la génération hello DSC métaconfigurations nécessitées :

1. Ouvrez la console PowerShell de hello ou PowerShell ISE en tant qu’administrateur sur un ordinateur dans votre environnement local.
2. Connectez-vous à l’aide du Gestionnaire de ressources tooAzure **AzureRmAccount-ajouter**
3. Télécharger hello DSC PowerShell métaconfigurations pour les ordinateurs hello tooonboard de hello Automation compte toowhich vous voulez que les nœuds de tooonboard :

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. Vous devez maintenant avoir un dossier appelé ***DscMetaConfigs***, contenant métaconfigurations de DSC PowerShell hello pour tooonboard de machines hello (en tant qu’administrateur) :
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a>Enregistrement sécurisé

Ordinateurs peuvent s’intégrer en toute sécurité tooan compte Azure Automation via le protocole d’inscription hello WMF 5 DSC, ce qui permet un nœud tooauthenticate tooa PowerShell DSC V2 extraire ou création d’un rapport serveur DSC (y compris Azure Automation DSC). nœud de Hello enregistre toohello sur le serveur à un **URL d’inscription**, l’authentification à l’aide un **clé d’inscription**. Pendant l’inscription, le nœud de hello DSC et DSC par extraction de données/Reporting server négocient un certificat unique pour cette toouse de nœud pour l’authentification toohello server postérieurs à le. Ce processus empêche les nœuds intégrés d’emprunter l’identité d’un autre nœud, par exemple si un nœud est compromis et agit à des fins malveillantes. Après l’inscription, clé d’inscription de hello n’est pas utilisée pour l’authentification à nouveau et est supprimée à partir du nœud de hello.

Vous pouvez obtenir des informations de hello requises pour le protocole d’inscription hello DSC de hello **gérer les clés** panneau dans le portail Azure en version préliminaire de hello. Pour ouvrir ce panneau en cliquant sur icône de clé hello sur hello **Essentials** Panneau de configuration pour hello compte Automation.

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* URL d’inscription est le champ URL de hello dans le panneau de gérer les clés hello.
* Clé d’inscription est hello clé d’accès primaire ou clé d’accès secondaire dans le panneau de gérer les clés hello. Vous pouvez utiliser l’une de ces deux clés.

Pour renforcer la sécurité des clés d’accès primaire et secondaire hello d’un compte Automation peuvent être régénérées à tout moment (sur hello **gérer les clés** panneau) des enregistrements du nœud futures tooprevent à l’aide des clés précédents.

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a>Résolution des problèmes liés à l’intégration de machines virtuelles Azure

Azure Automation DSC vous permet d’intégrer facilement des machines virtuelles Microsoft Azure à des fins de gestion de la configuration. Dans les coulisses hello, hello extension de Configuration d’état souhaité Azure VM est utilisé tooregister hello machine virtuelle dans Azure Automation DSC. Étant donné que hello extension de Configuration d’état souhaité Azure VM s’exécute de façon asynchrone, le suivi de sa progression et la résolution des problèmes de son exécution peuvent être importants.

> [!NOTE]
> N’importe quelle méthode de l’intégration une tooAzure de machine virtuelle de Windows Azure Automation DSC qui utilise l’extension de Configuration d’état souhaité Azure VM hello peut prendre les horaires de tooan pour tooshow de nœud hello des tel qu’enregistré dans Azure Automation. Il s’agit en raison de l’installation de toohello de Windows Management Framework 5.0 sur hello VM par extension hello DSC des machines virtuelles Azure, qui est requis tooonboard hello VM tooAzure Automation DSC.

tootroubleshoot ou la vue État hello Hello extension de Configuration d’état souhaité Azure VM, Bonjour Azure portal accédez toohello VM à intégrer, puis cliquez sur -> **tous les paramètres** -> **Extensions**   ->  **DSC**. Pour plus de détails, vous pouvez cliquer sur **Afficher l’état détaillé**.

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a>Expiration du certificat et nouvel enregistrement

Après avoir inscrit un ordinateur comme un nœud de DSC dans Azure Automation DSC, il existe de nombreuses raisons pour lesquelles vous devrez peut-être tooreregister ce nœud Bonjour ultérieure :

* Une fois inscrit, chaque nœud négocie automatiquement un certificat unique pour l'authentification qui expire après un an. Actuellement, hello protocole d’inscription DSC PowerShell ne peut pas renouveler automatiquement les certificats quand ils arrivent à expiration, vous avez besoin de nœuds de hello tooreregister après l’heure d’une année. Avant la réinscription, assurez-vous que chaque nœud exécute Windows Management Framework 5.0 RTM. Si l’expiration du certificat d’authentification d’un nœud et le nœud de hello n’est pas inscrit, nœud de hello sera toocommunicate impossible avec Azure Automation et est marqué « Ne répondant pas. » Réinscription effectué 90 jours ou inférieur à partir de l’heure d’expiration du certificat hello ou à tout moment après le délai d’expiration de certificat hello, génère un nouveau certificat généré et utilisé.
* toochange les [les valeurs de gestionnaire de Configuration Local DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) qui ont été définies lors de l’inscription initiale du nœud hello, telles que ConfigurationMode. Actuellement, ces valeurs de l’agent DSC peuvent être modifiées uniquement via une désinscription. une exception de Hello est hello Configuration de nœuds affectée toohello nœud : cela peut être modifié directement dans Azure Automation DSC.

L’enregistrement n’est possible dans la même façon que vous avez enregistré les nœud hello au départ, l’une des méthodes d’intégration de hello décrites dans ce document de hello. Vous n’avez pas besoin de toounregister un nœud à partir d’Azure Automation DSC avant la réinscription qu’il.

## <a name="related-articles"></a>Articles connexes

* [Vue d’ensemble d’Azure Automation DSC](automation-dsc-overview.md)
* [Applets de commande Azure Automation DSC](/powershell/module/azurerm.automation/#automation)
* [Tarification d’Azure Automation DSC](https://azure.microsoft.com/pricing/details/automation/)
