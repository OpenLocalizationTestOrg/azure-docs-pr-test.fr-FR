---
title: "environnement de test d’application aaaLOB | Documents Microsoft"
description: "En savoir plus l’environnement de cloud toocreate sur le web, application métier dans un hybride IT pro ou tests de développement."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>Configuration d’une application métier web dans un cloud hybride pour le test
Cette rubrique vous guide lors de la création d’un environnement cloud hybride simulé pour tester une application métier web hébergée dans Microsoft Azure. Voici la configuration obtenue de hello.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Cette configuration se compose des éléments suivants :

* Un réseau local simulé hébergé dans Azure (hello TestLab VNet).
* Un réseau virtuel intersite hébergé dans Azure (TestVNET).
* Une connexion VPN de réseau virtuel à réseau virtuel.
* Un serveur web métier, SQL server et contrôleur de domaine secondaire dans le réseau virtuel de TestVNET hello.

Cette configuration fournit une base et un point de départ commun à partir duquel vous pouvez :

* Développer et tester des applications métier hébergées sur IIS (Internet Information Services) avec un serveur principal de base de données SQL Server 2014 dans Azure.
* Tester cette charge de travail informatique hybride simulée basée sur le cloud.

Il existe trois principales phases toosetting, cet environnement de test de cloud hybride :

1. Configurer l’environnement de cloud hybride simulé hello.
2. Configurez l’ordinateur hello SQL server (SQL1).
3. Configurer hello LOB serveur (LOB1).

Cette charge de travail nécessite un abonnement Azure. Si vous avez un abonnement MSDN ou Visual Studio, consultez [Crédit Azure mensuel pour les abonnés Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

Pour obtenir un exemple d’une application LOB hébergée dans Azure de production, consultez hello **des applications métier** plan architecture à [diagrammes d’Architecture logicielle Microsoft et les projets](http://msdn.microsoft.com/dn630664).

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a>Phase 1 : Paramétrer l’environnement de cloud hybride simulé hello
Créer hello [environnement de test de cloud hybride simulé](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Étant donné que cet environnement de test ne nécessite pas la présence de hello du serveur hello APP1 sur le sous-réseau du réseau d’entreprise hello, vous pouvez l’arrêter pour l’instant.

Ceci est votre configuration actuelle.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a>Phase 2 : Configurer l’ordinateur hello SQL server (SQL1)
À partir de hello portail Azure, démarrer l’ordinateur de DC2 hello si nécessaire.

Ensuite, créez une machine virtuelle pour SQL1 avec ces commandes dans une invite de commandes Azure PowerShell sur votre ordinateur local. Toorunning préalable ces commandes, renseignez hello valeurs des variables et remove hello < et > caractères.

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Utilisez hello tooSQL1 de tooconnect portail Azure à l’aide du compte d’administrateur local hello de SQL1.

Ensuite, configurez le test de connectivité de base de tooallow règles pare-feu Windows et le trafic SQL Server. À partir d'une invite de commandes Windows PowerShell de niveau administrateur sur SQL1, exécutez ces commandes.

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

commande ping de Hello doit aboutir à quatre réponses de réussite de l’adresse IP 192.168.0.4.

Ensuite, ajoutez hello disque de données supplémentaire sur SQL1 en tant que nouveau volume avec la lettre de lecteur hello F:.

1. Dans le volet gauche hello du Gestionnaire de serveur, cliquez sur **File and Storage Services**, puis cliquez sur **disques**.
2. Dans le volet du sommaire hello, Bonjour **disques** , cliquez sur **disque 2** (avec hello **Partition** défini trop**inconnu**).
3. Cliquez sur **Tâches**, puis sur **Nouveau volume**.
4. Sur hello avant de commencer, page de hello Assistant Nouveau Volume, cliquez sur **suivant**.
5. Sur le serveur hello Select de hello et page de disque, cliquez sur **Disk 2**, puis cliquez sur **suivant**. À l’invite, cliquez sur **OK**.
6. Dans spécifier la taille de page de volume hello hello de hello, cliquez sur **suivant**.
7. Hello Assign tooa lecteur lettre ou un dossier de page, cliquez sur **suivant**.
8. Dans la page des paramètres système hello sélectionner un fichier, cliquez sur **suivant**.
9. Dans hello page Confirmer les sélections, cliquez sur **créer**.
10. Lorsque vous avez terminé, cliquez sur **Fermer**.

Exécutez ces commandes à l’invite de commande Windows PowerShell hello sur SQL1 :

    md f:\Data
    md f:\Log
    md f:\Backup

Joignez ensuite le domaine d’entreprise Windows Server Active Directory de toohello SQL1 avec les commandes suivantes à l’invite de Windows PowerShell hello sur SQL1.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Utiliser le compte hello CORP\User1 quand vous y êtes invité informations d’identification du compte de domaine toosupply pour hello **Add-Computer** commande.

Après le redémarrage, utilisez hello tooconnect portail Azure tooSQL1 *avec le compte administrateur local hello SQL1*.

Ensuite, configurez le lecteur F: hello SQL Server 2014 de toouse pour les nouvelles bases de données et des autorisations de compte d’utilisateur.

1. À partir de l’écran d’accueil hello, tapez **SQL Server Management**, puis cliquez sur **SQL Server 2014 Management Studio**.
2. Dans **connecter tooServer**, cliquez sur **connexion**.
3. Dans le volet d’arborescence hello l’Explorateur d’objets, cliquez sur **SQL1**, puis cliquez sur **propriétés**.
4. Bonjour **propriétés du serveur** fenêtre, cliquez sur **les paramètres de base de données**.
5. Recherchez hello **emplacements par défaut de base de données** et définir les valeurs suivantes : 
   * Pour **données**, le chemin d’accès de type hello **f:\Data**.
   * Pour **journal**, le chemin d’accès de type hello **f:\Log**.
   * Pour **sauvegarde**, le chemin d’accès de type hello **f:\Backup**.
   * Remarque : seules les nouvelles bases de données utilisent ces emplacements.
6. Cliquez sur hello **OK** fenêtre hello de tooclose.
7. Bonjour **l’Explorateur d’objets** volet de l’arborescence, ouvrez **sécurité**.
8. Cliquez avec le bouton droit sur **Connexions** et sélectionnez **Nouvelle connexion**.
9. Dans **Nom de connexion**, tapez **CORP\User1**.
10. Sur hello **rôles serveur** , cliquez sur **sysadmin**, puis cliquez sur **OK**.
11. Fermez Microsoft SQL Server Management Studio.

Ceci est votre configuration actuelle.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a>Phase 3 : Configurer le serveur LOB hello (LOB1)
Commencez par créer un ordinateur virtuel pour LOB1 avec les commandes suivantes à l’invite de commandes Azure PowerShell hello sur votre ordinateur local.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Ensuite, utilisez hello tooconnect portail Azure tooLOB1 avec informations d’identification hello du compte d’administrateur local hello de LOB1.

Ensuite, configurez un trafic de tooallow de règle de pare-feu Windows pour le test de connectivité de base. À partir d'une invite de commandes de Windows PowerShell de niveau administrateur sur LOB1, exécutez les commandes suivantes.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

commande ping de Hello doit aboutir à quatre réponses de réussite de l’adresse IP 192.168.0.4.

Ensuite, joindre LOB1 toohello CORP domaine Active Directory avec les commandes suivantes à l’invite de commandes Windows PowerShell hello.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Utiliser le compte hello CORP\User1 quand vous y êtes invité informations d’identification du compte de domaine toosupply pour hello **Add-Computer** commande.

Après le redémarrage, utilisez hello tooconnect portail Azure tooLOB1 avec le mot de passe et le compte de hello CORP\User1.

Ensuite, configurez LOB1 pour IIS et testez l'accès à partir de CLIENT1.

1. Dans le Gestionnaire de serveur, cliquez sur **Ajouter des rôles et des fonctionnalités**.
2. Sur hello **avant de commencer** , cliquez sur **suivant**.
3. Sur hello **sélectionner le type d’installation** , cliquez sur **suivant**.
4. Sur hello **serveur de destination sélectionnez** , cliquez sur **suivant**.
5. Sur hello **rôles serveur** , cliquez sur **serveur Web (IIS)** dans la liste des hello **rôles**.
6. Quand vous y êtes invité, cliquez sur **Ajouter des fonctionnalités**, puis sur **Suivant**.
7. Sur hello **sélectionner des fonctionnalités** , cliquez sur **suivant**.
8. Sur hello **serveur Web (IIS)** , cliquez sur **suivant**.
9. Sur hello **sélectionner les services de rôle** page, sélectionnez ou désactivez les cases à cocher hello pour les services hello nécessaires pour tester votre application métier, puis cliquez sur **suivant**.
10. Sur hello **confirmer les sélections d’installation** , cliquez sur **installer**.
11. Attendez que l’installation de hello de composants soit terminée, puis **fermer**.
12. À partir de hello portail Azure, connectez-vous toohello CLIENT1 ordinateur avec les informations d’identification du compte hello CORP\User1 et puis démarrez Internet Explorer.
13. Dans la barre d’adresses hello, tapez **http://lob1/** et appuyez sur ENTRÉE. Vous devez voir la page web de hello par défaut IIS 8.

Ceci est votre configuration actuelle.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Cet environnement est maintenant prêt pour vous toodeploy votre application basée sur le web sur les fonctionnalités LOB1 et de test à partir de CLIENT1 sur le sous-réseau du réseau d’entreprise hello.

## <a name="next-step"></a>Étape suivante
* Ajouter un nouvel ordinateur virtuel à l’aide de hello [portail Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

