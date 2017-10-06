---
title: "Azure Active Directory Domain Services : guide d’administration | Microsoft Docs"
description: "Joindre un domaine géré tooa machine virtuelle Windows Azure PowerShell et le modèle de déploiement classique hello."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a>Joindre un domaine géré tooa machine virtuelle Windows Server à l’aide de PowerShell
> [!div class="op_single_selector"]
> * [Portail Azure Classic - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Les Services de domaine Active Directory Azure ne prend pas en charge modèle du Gestionnaire de ressources hello.
>
>

Ces étapes montrent le fonctionnement des commandes toocustomize un ensemble d’Azure PowerShell qui créer et préconfigurer une machine virtuelle Azure Windows à l’aide d’une approche de bloc de construction. Ces étapes vous permettent de créer une machine virtuelle Azure Windows et de joindre le domaine géré de tooan des Services de domaine Active Directory de Azure.

Ces étapes utilisent une méthode de cases à remplir pour créer des jeux de commandes Azure PowerShell. Cette approche peut être utile si vous tooPowerShell nouveau ou vous souhaitez tooknow le toospecify de valeurs pour la configuration réussie. Les utilisateurs expérimentés PowerShell peuvent prendre les commandes hello et remplacer leurs propres valeurs pour les variables de hello (lignes hello commençant par « $»).

Si vous n’avez pas déjà fait, suivez les instructions de hello de [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell sur votre ordinateur local. Puis ouvrez une invite de commandes Windows PowerShell.

## <a name="step-1-add-your-account"></a>Étape 1 : Ajouter votre compte
1. À l’invite de commandes PowerShell hello, tapez **Add-AzureAccount** et cliquez sur **entrée**.
2. Tapez hello adresse de messagerie associée à votre abonnement Azure et cliquez sur **continuer**.
3. Tapez hello de mot de passe pour votre compte.
4. Cliquez sur **Se connecter**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>Étape 2 : Configurer votre abonnement et votre compte de stockage
Définissez votre abonnement Azure et le compte de stockage en exécutant ces commandes à l’invite de commandes Windows PowerShell hello. Tous les éléments entre guillemets hello, notamment hello < et >, remplacez les noms corrects hello.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Vous pouvez obtenir les nom d’abonnement approprié hello de hello propriété SubscriptionName de sortie hello Hello **Get-AzureSubscription** commande. Vous pouvez obtenir nom de compte de stockage correct hello de hello propriété Label du résultat hello de hello **Get-AzureStorageAccount** commande une fois que vous exécutez hello **Select-AzureSubscription** commande.

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a>Étape 3 : Procédure pas à pas : configurer l’ordinateur virtuel de hello et joindre le domaine géré de toohello
Voici toocreate Azure PowerShell correspondante du jeu de commande hello cet ordinateur virtuel, des lignes vides entre chaque bloc pour une meilleure lisibilité.

Indiquez les informations toobe de machine virtuelle Windows hello configuré.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

Pour les valeurs de InstanceSize hello pour D, DS ou machines virtuelles de série G, consultez [Machine virtuelle et les tailles de Service Cloud pour Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

Fournissent des informations sur le domaine géré de hello.

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

Spécifiez le nom hello du service de cloud hello.

    $svcname="Contoso100-test"

Spécifiez nom hello Hello de toowhich de réseau virtuel hello que machine virtuelle doit être joint. Vérifiez que ce domaine d’AAD-DS gérés hello est disponible dans ce réseau virtuel.

    $vnetname="MyPreviewVnet"

Sélectionnez hello VM image toobe utilisé tooprovision hello machine virtuelle.

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

Configurer hello VM - nom de machine virtuelle de jeu, instance toobe taille et de l’image utilisée.

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Obtenir des informations d’identification d’administrateur local pour hello machine virtuelle. Choisissez un mot de passe administrateur fort.

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

Obtenir des informations d’identification pour un compte d’utilisateur qui appartiennent à toojoin VM toohello managé domaine du groupe des administrateurs de contrôleur de domaine too'AAD de. Ne spécifiez nom de domaine hello - pour l’instance, dans notre exemple, nous spécifions « bob » comme nom d’utilisateur hello.

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

Configurer hello VM - spécifier la condition de jointure de domaine et les informations d’identification requises.

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

Définissez un sous-réseau pour hello machine virtuelle.

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

Facultatif : Point toohello adresse du domaine de hello. Si vous définissez des serveurs DNS pour le réseau virtuel de hello adresses IP de hello Hello de toobe domaine géré hello des Services de domaine Active Directory de Azure, cette étape n’est pas requise.

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

Maintenant, hello de disposition appartenant au domaine machine virtuelle Windows.

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a>Script tooprovision une machine virtuelle Windows et le joindre automatiquement domaine géré de Services de domaine AAD tooan
Cette commande PowerShell crée une machine virtuelle pour un serveur métier qui :

* Utilise l’image de Windows Server 2012 R2 Datacenter hello.
* est une machine virtuelle très petite
* A le nom hello Contoso100 et de test.
* Est automatiquement jointe toohello contoso100 managé un domaine.
* Est ajouté toohello même réseau virtuel que hello géré de domaine.

Voici hello exemple complet script toocreate hello Windows virtual machine et le joindre automatiquement domaine géré de toohello des Services de domaine Active Directory de Azure.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a>Contenu connexe
* [Services de domaine Azure AD : guide de prise en main](active-directory-ds-getting-started.md)
* [Administrer un domaine géré par les services de domaine Azure Active Directory](active-directory-ds-admin-guide-administer-domain.md)
