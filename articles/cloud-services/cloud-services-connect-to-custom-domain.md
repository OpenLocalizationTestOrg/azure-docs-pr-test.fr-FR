---
title: "Connexion d’un service cloud à un contrôleur de domaine personnalisé | Microsoft Docs"
description: "Découvrez comment connecter vos rôles web/de travail à un domaine Active Directory personnalisé à l’aide de Powershell et de l’extension de domaine Active Directory"
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
ms.openlocfilehash: 17f6918371678ac849198bff4e3b3eea8678c660
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-azure-cloud-services-roles-to-a-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="cf8d2-103">Connexion des rôles de services cloud Azure à un contrôleur de domaine Active Directory personnalisé hébergé dans Azure</span><span class="sxs-lookup"><span data-stu-id="cf8d2-103">Connecting Azure Cloud Services Roles to a custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="cf8d2-104">Nous allons tout d’abord définir un réseau virtuel (VNet) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="cf8d2-105">Nous allons ensuite ajouter un contrôleur de domaine Active Directory (hébergé sur une machine virtuelle Azure) sur le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) to the VNet.</span></span> <span data-ttu-id="cf8d2-106">Ensuite, nous ajouterons des rôles de service cloud existants sur le réseau virtuel créé au préalable, puis les connecterons au contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-106">Next, we will add existing cloud service roles to the pre-created VNet, then connect them to the Domain Controller.</span></span>

<span data-ttu-id="cf8d2-107">Avant de commencer, quelques aspects à prendre en compte :</span><span class="sxs-lookup"><span data-stu-id="cf8d2-107">Before we get started, couple of things to keep in mind:</span></span>

1. <span data-ttu-id="cf8d2-108">Ce didacticiel utilise Powershell. Par conséquent, vérifiez qu’Azure Powershell est installé et prêt à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready to go.</span></span> <span data-ttu-id="cf8d2-109">Pour obtenir de l’aide sur la configuration d’Azure Powershell, consultez l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cf8d2-109">To get help with setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="cf8d2-110">Vos instances de contrôleur de domaine AD et de rôle web/de travail doivent se trouver dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-110">Your AD Domain Controller and Web/Worker Role instances need to be in the VNet.</span></span>

<span data-ttu-id="cf8d2-111">Suivez ce guide pas à pas et, si vous rencontrez des problèmes, laissez-nous un commentaire à la fin de l’article.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at the end of the article.</span></span> <span data-ttu-id="cf8d2-112">Nous reviendrons vers vous (oui, nous lisons les commentaires).</span><span class="sxs-lookup"><span data-stu-id="cf8d2-112">Someone will get back to you (yes, we do read comments).</span></span>

<span data-ttu-id="cf8d2-113">Le réseau qui est référencé par le service cloud doit être un **réseau virtuel classique**.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-113">The network that is referenced by the cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="cf8d2-114">Création d'un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="cf8d2-114">Create a Virtual Network</span></span>
<span data-ttu-id="cf8d2-115">Vous pouvez créer un réseau virtuel dans Azure via le portail Azure ou Powershell.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-115">You can create a Virtual Network in Azure using the Azure portal or PowerShell.</span></span> <span data-ttu-id="cf8d2-116">Pour ce didacticiel, nous utiliserons Powershell.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="cf8d2-117">Pour créer un réseau virtuel à l’aide du portail Azure, consultez l’article [Création d’un réseau virtuel](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="cf8d2-117">To create a Virtual Network using the Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="cf8d2-118">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cf8d2-118">Create a Virtual Machine</span></span>
<span data-ttu-id="cf8d2-119">Une fois que vous avez terminé la configuration du réseau virtuel, vous devrez créer un contrôleur de domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-119">Once you have completed setting up the Virtual Network, you will need to create an AD Domain Controller.</span></span> <span data-ttu-id="cf8d2-120">Pour ce didacticiel, nous configurerons un contrôleur de domaine Active Directory sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="cf8d2-121">Pour ce faire, créez une machine virtuelle via Powershell à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cf8d2-121">To do this, create a virtual machine through PowerShell using the following commands:</span></span>

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

# Create a VM and add it to the Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-to-a-domain-controller"></a><span data-ttu-id="cf8d2-122">Promotion de votre machine virtuelle vers un contrôleur de domaine</span><span class="sxs-lookup"><span data-stu-id="cf8d2-122">Promote your Virtual Machine to a Domain Controller</span></span>
<span data-ttu-id="cf8d2-123">Pour configurer la machine virtuelle comme un contrôleur de domaine Active Directory, vous devez ouvrir une session sur la machine virtuelle et la configurer.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-123">To configure the Virtual Machine as an AD Domain Controller, you will need to log in to the VM and configure it.</span></span>

<span data-ttu-id="cf8d2-124">Pour vous connecter à la machine virtuelle, vous pouvez obtenir le fichier RDP via Powershell. Utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cf8d2-124">To log in to the VM, you can get the RDP file through PowerShell, use the following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="cf8d2-125">Une fois connecté à la machine virtuelle, configurez votre machine virtuelle comme un contrôleur de domaine Active Directory en suivant le guide pas à pas de la rubrique [Configuration de votre contrôleur de domaine Active Directory de client](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf8d2-125">Once you are signed in to the VM, set up your Virtual Machine as an AD Domain Controller by following the step-by-step guide on [How to set up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-to-the-virtual-network"></a><span data-ttu-id="cf8d2-126">Ajout de votre service cloud au réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="cf8d2-126">Add your Cloud Service to the Virtual Network</span></span>
<span data-ttu-id="cf8d2-127">Ensuite, vous devez ajouter le déploiement de votre service cloud sur le nouveau réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-127">Next, you need to add your cloud service deployment to the new VNet.</span></span> <span data-ttu-id="cf8d2-128">Pour ce faire, modifiez votre cscfg de service cloud en ajoutant les sections pertinentes à votre cscfg à l'aide de Visual Studio ou de l'éditeur de votre choix.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-128">To do this, modify your cloud service cscfg by adding the relevant sections to your cscfg using Visual Studio or the editor of your choice.</span></span>

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

<span data-ttu-id="cf8d2-129">Générez ensuite votre projet de services cloud et déployez-le dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-129">Next build your cloud services project and deploy it to Azure.</span></span> <span data-ttu-id="cf8d2-130">Pour obtenir de l'aide pour le déploiement de votre package de services cloud dans Azure, consultez l'article [Création et déploiement d'un service cloud](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="cf8d2-130">To get help with deploying your cloud services package to Azure, see [How to Create and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-to-the-domain"></a><span data-ttu-id="cf8d2-131">Connexion de vos rôles web/de travail au domaine</span><span class="sxs-lookup"><span data-stu-id="cf8d2-131">Connect your web/worker roles to the domain</span></span>
<span data-ttu-id="cf8d2-132">Une fois votre projet de service cloud déployé sur Azure, connectez vos instances de rôle pour le domaine Active Directory personnalisé à l'aide de l'extension de domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-132">Once your cloud service project is deployed on Azure, connect your role instances to the custom AD domain using the AD Domain Extension.</span></span> <span data-ttu-id="cf8d2-133">Pour ajouter l’extension de domaine Active Directory à votre déploiement de services cloud existant et rejoindre le domaine personnalisé, exécutez les commandes suivantes dans Powershell :</span><span class="sxs-lookup"><span data-stu-id="cf8d2-133">To add the AD Domain Extension to your existing cloud services deployment and join the custom domain, execute the following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension to the cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="cf8d2-134">Et c’est terminé !</span><span class="sxs-lookup"><span data-stu-id="cf8d2-134">And that's it.</span></span>

<span data-ttu-id="cf8d2-135">Vos services cloud doivent être joints à votre contrôleur de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-135">Your cloud services should be joined to your custom domain controller.</span></span> <span data-ttu-id="cf8d2-136">Si vous souhaitez en savoir plus sur les différentes options disponibles pour la configuration de l’extension de domaine Active Directory, utilisez l’aide PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-136">If you would like to learn more about the different options available for how to configure AD Domain Extension, use the PowerShell help.</span></span> <span data-ttu-id="cf8d2-137">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="cf8d2-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
