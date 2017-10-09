---
title: "aaaConnect un tooa de Service Cloud contrôleur de domaine personnalisé | Documents Microsoft"
description: "Découvrez comment tooconnect votre personnalisé de tooa de rôles web/de travail domaine Active Directory à l’aide de PowerShell et l’Extension de domaine Active Directory"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="37781-103">Connexion personnalisée tooa de rôles des Services Azure Cloud hébergé par le contrôleur de domaine Active Directory dans Azure</span><span class="sxs-lookup"><span data-stu-id="37781-103">Connecting Azure Cloud Services Roles tooa custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="37781-104">Nous allons tout d’abord définir un réseau virtuel (VNet) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="37781-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="37781-105">Nous allons ensuite ajouter un contrôleur de domaine Active Directory (hébergé sur une Machine virtuelle de Azure) de toohello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="37781-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) toohello VNet.</span></span> <span data-ttu-id="37781-106">Ensuite, nous Ajouter existant toohello de rôles de service cloud créé au préalable réseau virtuel, puis connectez-les toohello contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="37781-106">Next, we will add existing cloud service roles toohello pre-created VNet, then connect them toohello Domain Controller.</span></span>

<span data-ttu-id="37781-107">Avant de commencer, deux de tookeep choses à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="37781-107">Before we get started, couple of things tookeep in mind:</span></span>

1. <span data-ttu-id="37781-108">Ce didacticiel utilise PowerShell, par conséquent, assurez-vous que vous disposez d’Azure PowerShell est installé et prêt toogo.</span><span class="sxs-lookup"><span data-stu-id="37781-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready toogo.</span></span> <span data-ttu-id="37781-109">tooget de l’aide sur la configuration d’Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="37781-109">tooget help with setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="37781-110">Les instances de votre contrôleur de domaine Active Directory et les rôles Web/de travail doivent toobe Bonjour réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="37781-110">Your AD Domain Controller and Web/Worker Role instances need toobe in hello VNet.</span></span>

<span data-ttu-id="37781-111">Suivez ce guide pas à pas et si vous rencontrez des problèmes, nous laisser un commentaire à la fin de hello de l’article de hello.</span><span class="sxs-lookup"><span data-stu-id="37781-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at hello end of hello article.</span></span> <span data-ttu-id="37781-112">Une personne retrouvez tooyou (Oui, nous lisons commentaires).</span><span class="sxs-lookup"><span data-stu-id="37781-112">Someone will get back tooyou (yes, we do read comments).</span></span>

<span data-ttu-id="37781-113">réseau Hello qui est référencé par le service de cloud computing hello doit être un **réseau virtuel classique**.</span><span class="sxs-lookup"><span data-stu-id="37781-113">hello network that is referenced by hello cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="37781-114">Création d'un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="37781-114">Create a Virtual Network</span></span>
<span data-ttu-id="37781-115">Vous pouvez créer un réseau virtuel dans Azure à l’aide de hello portail Azure ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37781-115">You can create a Virtual Network in Azure using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="37781-116">Pour ce didacticiel, nous utiliserons Powershell.</span><span class="sxs-lookup"><span data-stu-id="37781-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="37781-117">un réseau virtuel à l’aide de toocreate hello Azure portail, consultez [créer un réseau virtuel](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="37781-117">toocreate a Virtual Network using hello Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="37781-118">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="37781-118">Create a Virtual Machine</span></span>
<span data-ttu-id="37781-119">Une fois que vous avez terminé la configuration de réseau virtuel de hello, vous devez toocreate un contrôleur de domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37781-119">Once you have completed setting up hello Virtual Network, you will need toocreate an AD Domain Controller.</span></span> <span data-ttu-id="37781-120">Pour ce didacticiel, nous configurerons un contrôleur de domaine Active Directory sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="37781-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="37781-121">toodo, créez une machine virtuelle via PowerShell à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="37781-121">toodo this, create a virtual machine through PowerShell using hello following commands:</span></span>

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a><span data-ttu-id="37781-122">Promouvoir votre tooa d’ordinateur virtuel contrôleur de domaine</span><span class="sxs-lookup"><span data-stu-id="37781-122">Promote your Virtual Machine tooa Domain Controller</span></span>
<span data-ttu-id="37781-123">tooconfigure hello Machine virtuelle tant que contrôleur de domaine Active Directory, vous devez toolog dans toohello machine virtuelle et configurez-le.</span><span class="sxs-lookup"><span data-stu-id="37781-123">tooconfigure hello Virtual Machine as an AD Domain Controller, you will need toolog in toohello VM and configure it.</span></span>

<span data-ttu-id="37781-124">toolog dans toohello machine virtuelle, vous pouvez obtenir le fichier RDP de hello via PowerShell, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="37781-124">toolog in toohello VM, you can get hello RDP file through PowerShell, use hello following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="37781-125">Une fois que vous êtes connecté toohello VM, configuré votre Machine virtuelle comme un contrôleur de domaine Active Directory en suivant guide pas à pas de hello dans [comment tooset votre contrôleur de domaine Active Directory du client](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="37781-125">Once you are signed in toohello VM, set up your Virtual Machine as an AD Domain Controller by following hello step-by-step guide on [How tooset up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-toohello-virtual-network"></a><span data-ttu-id="37781-126">Ajoutez votre réseau virtuel de toohello Service Cloud</span><span class="sxs-lookup"><span data-stu-id="37781-126">Add your Cloud Service toohello Virtual Network</span></span>
<span data-ttu-id="37781-127">Ensuite, vous devez tooadd votre toohello de déploiement de service cloud nouveau réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="37781-127">Next, you need tooadd your cloud service deployment toohello new VNet.</span></span> <span data-ttu-id="37781-128">toodo, modifier votre service cloud cscfg en ajoutant hello sections pertinentes tooyour cscfg à l’aide de Visual Studio ou de bienvenue de l’éditeur de votre choix.</span><span class="sxs-lookup"><span data-stu-id="37781-128">toodo this, modify your cloud service cscfg by adding hello relevant sections tooyour cscfg using Visual Studio or hello editor of your choice.</span></span>

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

<span data-ttu-id="37781-129">Ensuite, générez votre projet de services cloud et déployez-le tooAzure.</span><span class="sxs-lookup"><span data-stu-id="37781-129">Next build your cloud services project and deploy it tooAzure.</span></span> <span data-ttu-id="37781-130">aide tooget avec le déploiement de votre tooAzure de package de services cloud, consultez [comment tooCreate et déployer un Service Cloud](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="37781-130">tooget help with deploying your cloud services package tooAzure, see [How tooCreate and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-toohello-domain"></a><span data-ttu-id="37781-131">Se connecter à votre domaine toohello de rôles web/de travail</span><span class="sxs-lookup"><span data-stu-id="37781-131">Connect your web/worker roles toohello domain</span></span>
<span data-ttu-id="37781-132">Une fois votre projet de service cloud est déployé sur Azure, connectez-vous à votre domaine toohello AD personnalisé d’instances de rôle hello Extension de domaine Active Directory à l’aide de.</span><span class="sxs-lookup"><span data-stu-id="37781-132">Once your cloud service project is deployed on Azure, connect your role instances toohello custom AD domain using hello AD Domain Extension.</span></span> <span data-ttu-id="37781-133">tooadd hello déploiement des services cloud existant Extension de domaine Active Directory tooyour et joindre le domaine personnalisé hello, exécutez hello suivant les commandes dans PowerShell :</span><span class="sxs-lookup"><span data-stu-id="37781-133">tooadd hello AD Domain Extension tooyour existing cloud services deployment and join hello custom domain, execute hello following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="37781-134">Et c’est terminé !</span><span class="sxs-lookup"><span data-stu-id="37781-134">And that's it.</span></span>

<span data-ttu-id="37781-135">Vos services de cloud doivent être le contrôleur de domaine personnalisé tooyour jointes.</span><span class="sxs-lookup"><span data-stu-id="37781-135">Your cloud services should be joined tooyour custom domain controller.</span></span> <span data-ttu-id="37781-136">Si vous souhaitez que toolearn plus hello différentes options disponibles pour la tooconfigure Extension de domaine Active Directory, utilisez hello PowerShell aide.</span><span class="sxs-lookup"><span data-stu-id="37781-136">If you would like toolearn more about hello different options available for how tooconfigure AD Domain Extension, use hello PowerShell help.</span></span> <span data-ttu-id="37781-137">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="37781-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
