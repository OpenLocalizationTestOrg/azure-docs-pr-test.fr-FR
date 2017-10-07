---
title: "aaaConfigure hello toujours sur le groupe de disponibilité sur une machine virtuelle de Azure à l’aide de PowerShell | Documents Microsoft"
description: "Ce didacticiel utilise des ressources qui ont été créées avec le modèle de déploiement classique hello. Vous utilisez PowerShell toocreate un groupe de disponibilité Always On dans Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a>Configurer hello Always On groupe de disponibilité sur une machine virtuelle de Azure avec PowerShell
> [!div class="op_single_selector"]
> * [Classic : interface utilisateur](../classic/portal-sql-alwayson-availability-groups.md)
> * [Classic : PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Avant de commencer, rappelez-vous que vous pouvez accomplir cette tâche dans le modèle Azure Resource Manager. Nous vous recommandons d’utiliser le modèle Azure Resource Manager pour les nouveaux déploiements. Consultez [Présentation des groupes de disponibilité SQL Server AlwaysOn sur des machines virtuelles Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT]
> Nous recommandons que la plupart des nouveaux déploiements utilisent le modèle de gestionnaire de ressources hello. Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello.

Machines virtuelles (VM) Azure peut aider le coût de base de données administrateurs toolower hello d’un système de SQL Server haute disponibilité. Ce didacticiel vous montre comment tooimplement une disponibilité de groupe à l’aide de SQL Server Always On de bout en bout à l’intérieur d’un environnement Azure. À la fin de hello du didacticiel de hello, votre solution SQL Server Always On dans Azure comprendra hello suivant d’éléments :

* un réseau virtuel contenant plusieurs sous-réseaux, notamment un sous-réseau frontal et un sous-réseau principal ;
* un contrôleur de domaine avec un domaine Active Directory ;
* Deux machines virtuelles SQL Server qui sont déployés toohello principal sous-réseau et domaine d’Active Directory toohello jointes.
* Un cluster de basculement de Windows de trois nœuds avec le modèle de quorum nœud majoritaire hello.
* un groupe de disponibilité avec deux réplicas avec validation synchrone d’une base de données de disponibilité.

Ce scénario est choisi pour sa simplicité, pas pour sa rentabilité ou pour d’autres avantages apportés par Azure. Par exemple, vous pouvez réduire nombre hello d’ordinateurs virtuels pour un toosave de groupe de disponibilité de deux réplicas sur les heures de calcul dans Azure à l’aide du contrôleur de domaine hello en tant que témoin de partage de fichiers hello quorum dans un cluster de basculement à deux nœuds. Cette méthode réduit le nombre d’ordinateurs virtuels hello par rapport à hello au-dessus de configuration.

Ce didacticiel est destiné à tooshow vous hello étapes sont requise tooset des hello décrit la solution ci-dessus, sans développer les détails hello de chaque étape. Par conséquent, au lieu de fournir des étapes de configuration de l’interface graphique utilisateur de hello, il utilise tootake de script PowerShell vous rapidement à chaque étape. Ce didacticiel suppose hello qui suit :

* Vous avez déjà un compte Azure avec un abonnement de machine virtuelle hello.
* Vous avez installé hello [applets de commande Azure PowerShell](/powershell/azure/overview).
* Vous disposez déjà d’une connaissance approfondie des groupes de disponibilité Always On pour les solutions locales. Pour plus d’informations, voir [Groupes de disponibilité AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a>Se connecter tooyour abonnement Azure et créer des réseaux virtuels de hello
1. Dans une fenêtre PowerShell sur votre ordinateur local, importez hello module Azure, téléchargez hello machine de tooyour de fichier de paramètres de publication et connecter votre tooyour de session PowerShell abonnement Azure en important les paramètres de publication hello téléchargé.

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    Hello **Get-AzurePublishSettingsFile** commande génère automatiquement un certificat de gestion Azure et le télécharge tooyour machine. Un navigateur s’ouvre automatiquement et que vous les informations d’identification du compte Microsoft hello tooenter demandées pour votre abonnement Azure. Hello téléchargé **.publishsettings** fichier contient toutes les informations de hello que vous avez besoin de toomanage votre abonnement Azure. Après avoir enregistré ce répertoire tooa local, importez-le à l’aide de hello **Import-AzurePublishSettingsFile** commande.

   > [!NOTE]
   > fichier .publishsettings de Hello contient vos informations d’identification (non encodées) qui sont utilisé tooadminister vos abonnements Azure et services. Hello meilleure pratique de sécurité pour ce fichier est toostore il temporairement en dehors de vos répertoires sources (par exemple, dans le dossier bibliothèques\documents hello), puis supprimez-le après l’importation du hello est terminée. Un utilisateur malveillant qui réussit à fichier .publishsettings de toohello access permettre modifier, créer et supprimer vos services Azure.

2. Définissez une série de variables que vous allez utiliser toocreate votre infrastructure de cloud computing.

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    Payer toohello attention suivant tooensure vos commandes réussira ultérieurement :

   * Variables **$storageAccountName** et **$dcServiceName** doit être unique parce qu’ils sont utilisés tooidentify votre compte de stockage cloud et le serveur en nuage, respectivement, sur hello Internet.
   * Hello des noms que vous spécifiez pour les variables **$affinityGroupName** et **$virtualNetworkName** sont configurés dans le document de configuration de réseau virtuel hello que vous utiliserez plus tard.
   * **$sqlImageName** Spécifie le nom hello mis à jour de l’image de machine virtuelle hello qui contient l’édition Enterprise de SQL Server 2012 Service Pack 1.
   * Par souci de simplicité, **Contoso ! 000** est hello même mot de passe qui est utilisé dans tout le didacticiel hello.

3. Créez un groupe d’affinités.

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. Créez un réseau virtuel en important un fichier de configuration.

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    fichier de configuration Hello contient hello suivant du document XML. En bref, il spécifie un réseau virtuel appelé **ContosoNET** dans le groupe d’affinité hello appelé **ContosoAG**. Il a l’espace d’adressage hello **10.10.0.0/16** et deux sous-réseaux, **10.10.1.0/24** et **10.10.2.0/24**, qui sont hello les sous-réseau frontal et le sous-réseau principal, respectivement. sous-réseau frontal de Hello est où vous pouvez placer des applications clientes telles que Microsoft SharePoint. sous-réseau principal de Hello est où vous allez placer les machines virtuelles hello SQL Server. Si vous modifiez hello **$affinityGroupName** et **$virtualNetworkName** variables précédemment, vous devez également modifier hello correspondant de noms ci-dessous.

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. Créez un compte de stockage a associé à un groupe d’affinité hello que vous créé et définissez en tant que compte de stockage actif hello dans votre abonnement.

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. Créer des serveur de contrôleur de domaine hello dans hello nouveau cloud service et la disponibilité de sauvegarde.

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    Ces commandes dirigées hello suivants choses :

   * **New-AzureVMConfig** crée une configuration de machine virtuelle.
   * **Ajouter-AzureProvisioningConfig** donne hello des paramètres de configuration d’un serveur Windows autonome.
   * **Ajouter-AzureDataDisk** ajoute le disque de données hello que vous allez utiliser pour le stockage de données Active Directory, avec hello tooNone de jeu d’option de mise en cache.
   * **New-AzureVM** crée un nouveau service cloud et hello du nouvel ordinateur virtuel Azure dans le nouveau service de cloud hello.

7. Patientez hello nouvelle machine virtuelle toobe est entièrement configuré et télécharger le répertoire de travail tooyour hello fichier Bureau à distance. Étant donné que hello nouvel ordinateur virtuel Azure a une tooprovision beaucoup de temps, hello `while` boucle continue toopoll hello nouvelle machine virtuelle jusqu'à ce qu’il est prêt à être utilisé.

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

serveur de contrôleur de domaine Hello est maintenant correctement configuré. Ensuite, vous devez configurer le domaine Active Directory de hello sur ce serveur de contrôleur de domaine. Laissez la fenêtre de PowerShell hello ouverte sur votre ordinateur local. Vous l’utiliserez à nouveau toocreate ultérieure hello deux machines virtuelles de serveur SQL.

## <a name="configure-hello-domain-controller"></a>Configurer le contrôleur de domaine hello
1. Se connecter toohello serveur de contrôleur de domaine en lançant le fichier Bureau à distance de hello. Utilisez le nom d’utilisateur AzureAdmin et le mot de passe d’administrateur de la machine hello **Contoso ! 000**, que vous avez spécifiés lors de la création hello nouvelle machine virtuelle.
2. Ouvrez une fenêtre PowerShell en mode administrateur.
3. Exécutez hello **DCPROMO. EXE** tooset de commande des hello **corp.contoso.com** domaine, avec les répertoires de données hello sur le lecteur M.

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    Après la commande hello, hello machine virtuelle redémarre automatiquement.

4. Connectez-vous de nouveau serveur de contrôleur de domaine toohello en lançant le fichier Bureau à distance de hello. Cette fois, connectez-vous en tant que **CORP\Administrator**.
5. Ouvrez une fenêtre PowerShell en mode administrateur et d’importation du module Active Directory PowerShell hello à l’aide de hello de commande suivante :

        Import-Module ActiveDirectory

6. Exécutez hello suivant du domaine de toohello commandes tooadd trois utilisateurs.

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    **CORP\Install** est tooconfigure utilisé tout ce dont les instances de service SQL Server toohello, cluster de basculement hello et groupe de disponibilité hello. **CORP\SQLSvc1** et **CORP\SQLSvc2** sont utilisés comme comptes de service SQL Server hello pour les machines virtuelles hello deux SQL Server.
7. Suivant de hello suivant, exécutez les commandes toogive **CORP\Install** hello autorisations toocreate ordinateur objets hello domaine.

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    Hello GUID spécifié ci-dessus est hello GUID pour le type d’objet ordinateur hello. Hello **CORP\Install** compte doit hello **lire toutes les propriétés** et **créer des objets ordinateur** hello de toocreate autorisations Active Directory des objets pour le basculement de hello cluster. Hello **lire toutes les propriétés** autorisation est accordée déjà tooCORP\Install par défaut, vous n’avez pas besoin toogrant il explicitement. Pour plus d’informations sur les autorisations qui sont nécessaires le cluster de basculement toocreate hello, consultez [Guide pas à pas du Cluster de basculement : configuration des comptes dans Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).

    Maintenant que vous avez terminé de configurer Active Directory et les objets utilisateur hello, vous allez créer deux machines virtuelles de serveur SQL et joignez-les toothis domaine.

## <a name="create-hello-sql-server-vms"></a>Créer des machines virtuelles hello SQL Server
1. Continuer toouse hello PowerShell fenêtre qui est ouverte sur votre ordinateur local. Définissez hello suivant des variables supplémentaires :

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    adresse IP de Hello **10.10.0.4** est généralement assignée toohello première machine virtuelle que vous créez dans hello **10.10.0.0/16** sous-réseau de votre réseau virtuel Azure. Vous devez vérifier qu’il s’agit des adresses de hello de votre serveur de contrôleur de domaine en exécutant **IPCONFIG**.
2. Exécution hello suivant hello toocreate de commandes dirigées tout d’abord nommé de machine virtuelle dans un cluster de basculement hello, **ContosoQuorum**:

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    Notez ce qui suit hello concernant la commande hello ci-dessus :

   * **Nouveau-AzureVMConfig** crée une configuration de machine virtuelle avec le nom de jeu hello haute disponibilité souhaité. Hello machines virtuelles suivantes seront créées avec hello même nom à haute disponibilité afin qu’ils sont joints toohello même groupe à haute disponibilité.
   * **Ajouter-AzureProvisioningConfig** jointures hello de domaine Active Directory de toohello machine virtuelle que vous avez créé.
   * **Set-AzureSubnet** emplacements hello machine virtuelle dans le sous-réseau principal de hello.
   * **New-AzureVM** crée un nouveau service cloud et hello du nouvel ordinateur virtuel Azure dans le nouveau service de cloud hello. Hello **DnsSettings** paramètre spécifie le serveur DNS hello pour les serveurs dans le nouveau service de cloud hello hello a adresseIP hello **10.10.0.4**. Il s’agit d’adresse IP de hello du serveur de contrôleur de domaine hello. Ce paramètre est nécessaire tooenable hello nouvelles machines virtuelles dans un domaine Active Directory de hello cloud service toojoin toohello avec succès. Sans ce paramètre, vous devez définir manuellement des paramètres IPv4 hello dans votre serveur de contrôleur de domaine de machine virtuelle toouse hello en tant que serveur DNS principal de hello après hello machine virtuelle est configurée, puis joindre le domaine Active Directory de hello VM toohello.
3. Exécution hello suivant dirigée commandes toocreate hello machines virtuelles SQL Server nommée **ContosoSQL1** et **ContosoSQL2**.

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    Notez ce qui suit hello concernant les commandes hello ci-dessus :

   * **Nouveau-AzureVMConfig** utilise hello le même nom de groupe de disponibilité en tant que serveur de contrôleur de domaine hello et utilise hello image de SQL Server 2012 Service Pack 1 Enterprise Edition dans la galerie de machine virtuelle hello. Il définit également hello d’exploitation système tooread-mise en cache disque uniquement (aucun cache d’écriture). Nous vous recommandons de migrer hello de base de données fichiers tooa disque de données distinct que vous attachez toohello machine virtuelle et configurez avec aucune lecture ou le cache d’écriture. Toutefois, hello il est recommandé ensuite tooremove cache d’écriture sur le disque du système d’exploitation hello, car vous ne pouvez pas supprimer le cache sur le disque du système d’exploitation hello de lecture.
   * **Ajouter-AzureProvisioningConfig** jointures hello de domaine Active Directory de toohello machine virtuelle que vous avez créé.
   * **Set-AzureSubnet** emplacements hello machine virtuelle dans le sous-réseau principal de hello.
   * **Ajouter-AzureEndpoint** ajoute des points de terminaison de l’accès afin que les applications clientes puissent accéder à ces instances de service SQL Server sur hello Internet. Des ports différents sont fournis tooContosoSQL1 et ContosoSQL2.
   * **New-AzureVM** crée hello nouvelle machine virtuelle de serveur SQL Bonjour même service de cloud computing comme ContosoQuorum. Vous devez placer les machines virtuelles de hello Bonjour même service cloud si vous souhaitez les toobe dans hello du même groupe à haute disponibilité.
4. Attendez que chaque toobe de machine virtuelle entièrement configuré et de toodownload de chaque ordinateur virtuel de son répertoire de travail tooyour fichier Bureau à distance. Hello `for` boucle hello parcourt les trois nouvelles machines virtuelles et exécute des commandes hello à l’intérieur des accolades hello pour chacun d’eux.

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    machines virtuelles Hello SQL Server sont maintenant configurés et en cours d’exécution, mais ils sont installés avec SQL Server avec les options par défaut.

## <a name="initialize-hello-failover-cluster-vms"></a>Initialiser les machines virtuelles du cluster de basculement hello
Dans cette section, vous devez toomodify hello trois serveurs que vous allez utiliser dans un cluster de basculement hello et l’installation de SQL Server hello. Plus précisément :

* Tous les serveurs : vous devez tooinstall hello **le Clustering de basculement** fonctionnalité.
* Tous les serveurs : vous devez tooadd **CORP\Install** en tant qu’ordinateur de hello **administrateur**.
* ContosoSQL1 et ContosoSQL2 uniquement : vous devez tooadd **CORP\Install** comme un **sysadmin** rôle dans la base de données par défaut hello.
* ContosoSQL1 et ContosoSQL2 uniquement : vous devez tooadd **NT AUTHORITY\System** comme un signe avec hello les autorisations suivantes :

  * Modifier un groupe de disponibilité
  * Connecter SQL
  * Afficher l’état du serveur
* ContosoSQL1 et ContosoSQL2 uniquement : hello **TCP** protocole est déjà activé sur hello machine virtuelle SQL Server. Toutefois, vous devez toujours le pare-feu tooopen hello pour l’accès à distance de SQL Server.

Vous êtes désormais prêt toostart. À partir de **ContosoQuorum**, suivez les étapes de hello ci-dessous :

1. Vous connecter trop**ContosoQuorum** en lançant les fichiers Bureau à distance de hello. Utilisez le nom d’utilisateur de l’administrateur hello **AzureAdmin** et le mot de passe **Contoso ! 000**, que vous avez spécifiés lors de la création de machines virtuelles de hello.
2. Vérifiez que les ordinateurs hello ont été correctement attachés trop**corp.contoso.com**.
3. Attendez que toofinish d’installation de SQL Server hello en cours d’exécution hello automatisée des tâches d’initialisation avant de continuer.
4. Ouvrez une fenêtre PowerShell en mode administrateur.
5. Installer la fonctionnalité de Clustering de basculement Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Ajoutez **CORP\Install** en tant qu’administrateur local.

        net localgroup administrators "CORP\Install" /Add
7. Déconnectez-vous de ContosoQuorum. Vous avez terminé avec ce serveur.

        logoff.exe

Ensuite, initialisez **ContosoSQL1** et **ContosoSQL2**. Suivez les étapes de hello ci-dessous, identiques pour les deux machines virtuelles SQL Server.

1. Connecter des machines virtuelles toohello deux SQL Server en lançant les fichiers Bureau à distance de hello. Utilisez le nom d’utilisateur de l’administrateur hello **AzureAdmin** et le mot de passe **Contoso ! 000**, que vous avez spécifiés lors de la création de machines virtuelles de hello.
2. Vérifiez que les ordinateurs hello ont été correctement attachés trop**corp.contoso.com**.
3. Attendez que toofinish d’installation de SQL Server hello en cours d’exécution hello automatisée des tâches d’initialisation avant de continuer.
4. Ouvrez une fenêtre PowerShell en mode administrateur.
5. Installer la fonctionnalité de Clustering de basculement Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Ajoutez **CORP\Install** en tant qu’administrateur local.

        net localgroup administrators "CORP\Install" /Add
7. Importer hello fournisseur PowerShell SQL Server.

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. Ajouter **CORP\Install** en tant que rôle de sysadmin hello pour l’instance de SQL Server par défaut hello.

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. Ajouter **NT AUTHORITY\System** comme un connectez-vous avec les autorisations hello trois décrites ci-dessus.

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. Ouvrez le pare-feu hello pour l’accès à distance de SQL Server.

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. Déconnectez-vous des deux machines virtuelles.

         logoff.exe

Enfin, vous êtes prêt tooconfigure le groupe de disponibilité hello. Vous allez utiliser tooperform de fournisseur PowerShell SQL Server hello concernent tous des hello **ContosoSQL1**.

## <a name="configure-hello-availability-group"></a>Configurer le groupe de disponibilité hello
1. Vous connecter trop**ContosoSQL1** en lançant les fichiers Bureau à distance de hello. Au lieu de vous connecter à l’aide du compte d’ordinateur hello, connectez-vous à l’aide de **CORP\Install**.
2. Ouvrez une fenêtre PowerShell en mode administrateur.
3. Définissez hello suivant variables :

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. Importer hello fournisseur PowerShell SQL Server.

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. Modifier le compte de service SQL Server hello pour ContosoSQL1 tooCORP\SQLSvc1.

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. Modifier le compte de service SQL Server hello pour ContosoSQL2 tooCORP\SQLSvc2.

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. Télécharger **CreateAzureFailoverCluster.ps1** de [création d’un Cluster de basculement pour les groupes de disponibilité AlwaysOn dans Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello répertoire de travail local. Vous utiliserez cette toohelp de script que vous créez un cluster de basculement fonctionnel. Pour plus d’informations sur l’interaction de Clustering de basculement Windows avec hello Azure réseau, voir [haute disponibilité et récupération d’urgence pour SQL Server dans Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).
8. Modifier le répertoire de travail tooyour et créer un cluster de basculement hello avec le script de hello téléchargé.

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. Activer les groupes de disponibilité Always On pour les instances de SQL Server par défaut hello sur **ContosoSQL1** et **ContosoSQL2**.

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. Créer un répertoire de sauvegarde et accorder des autorisations pour les comptes de service SQL Server hello. Vous allez utiliser cette base de données de répertoire tooprepare hello disponibilité sur réplica secondaire de hello.

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. Créer une base de données sur **ContosoSQL1** appelé **MyDB1**, effectuez une sauvegarde complète et une sauvegarde de journal et les restaurer sur **ContosoSQL2** avec hello **WITH NORECOVERY** option.

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. Créer des points de terminaison groupe de disponibilité hello sur hello machines virtuelles SQL Server et définissez des autorisations appropriées de hello sur les points de terminaison hello.

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. Créer des réplicas de disponibilité hello.

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. Enfin, créez le groupe de disponibilité hello et groupe de disponibilité toohello jointure hello réplica secondaire.

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a>Étapes suivantes
Vous avez correctement implémenté SQL Server Always On en créant un groupe de disponibilité dans Azure. tooconfigure un écouteur pour ce groupe de disponibilité, consultez [configurer un écouteur d’équilibrage de charge interne pour les groupes de disponibilité Always On dans Azure](../classic/ps-sql-int-listener.md).

Pour en savoir plus sur l’utilisation de SQL Server dans Azure, consultez [Présentation de SQL Server sur les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
