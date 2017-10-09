---
title: des adresses IP publiques (classiques) aaaAzure niveau Instance | Documents Microsoft
description: "Comprendre les adresses IP (ILPIP) publique au niveau instance et comment toomanage les à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="e7f04-103">Vue d’ensemble des adresses IP publiques de niveau d’instance (classique)</span><span class="sxs-lookup"><span data-stu-id="e7f04-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="e7f04-104">Une instance IP publique au niveau (ILPIP) est une adresse IP publique que vous pouvez attribuer directement instance de rôle de machine virtuelle ou les Services de cloud computing tooa, plutôt que service cloud toohello résidant dans votre machine virtuelle ou instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="e7f04-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly tooa VM or Cloud Services role instance, rather than toohello cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="e7f04-105">Un ILPIP n’a pas lieu hello hello adresse IP virtuelle (VIP) qui est affectée à tooyour le service cloud.</span><span class="sxs-lookup"><span data-stu-id="e7f04-105">An ILPIP doesn’t take hello place of hello virtual IP (VIP) that is assigned tooyour cloud service.</span></span> <span data-ttu-id="e7f04-106">Au lieu de cela, il est une adresse IP supplémentaire que vous pouvez utiliser tooconnect directement tooyour machine virtuelle ou instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="e7f04-106">Rather, it’s an additional IP address that you can use tooconnect directly tooyour VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7f04-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7f04-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="e7f04-108">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="e7f04-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="e7f04-109">Microsoft vous recommande de créer des machines virtuelles via Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e7f04-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="e7f04-110">Assurez-vous que vous comprenez le fonctionnement des [adresses IP](virtual-network-ip-addresses-overview-classic.md) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e7f04-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![Différences entre les adresses IP publiques de niveau d’instance (ILPIP) et les adresses IP virtuelles (VIP)](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="e7f04-112">Comme indiqué dans la Figure 1, le service cloud hello est accessible à l’aide d’une adresse IP virtuelle, lors de hello des ordinateurs virtuels individuels sont normalement accessibles à l’aide d’adresses IP virtuelles :&lt;numéro de port&gt;.</span><span class="sxs-lookup"><span data-stu-id="e7f04-112">As shown in Figure 1, hello cloud service is accessed using a VIP, while hello individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="e7f04-113">En assignant un tooa ILPIP un ordinateur virtuel spécifique, qui peuvent être des ordinateurs virtuels accessibles directement à l’aide de cette adresse IP.</span><span class="sxs-lookup"><span data-stu-id="e7f04-113">By assigning an ILPIP tooa specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="e7f04-114">Lorsque vous créez un service cloud dans Azure, les enregistrements A DNS correspondants sont créés automatiquement service de toohello tooallow accès via un nom de domaine complet (FQDN), au lieu d’utiliser l’adresse IP virtuelle réel de hello.</span><span class="sxs-lookup"><span data-stu-id="e7f04-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically tooallow access toohello service through a fully qualified domain name (FQDN), instead of using hello actual VIP.</span></span> <span data-ttu-id="e7f04-115">Hello même processus se produit pour un ILPIP, ce qui permet l’accès toohello machine virtuelle ou instance de rôle par le nom de domaine complet au lieu de hello ILPIP.</span><span class="sxs-lookup"><span data-stu-id="e7f04-115">hello same process happens for an ILPIP, allowing access toohello VM or role instance by FQDN instead of hello ILPIP.</span></span> <span data-ttu-id="e7f04-116">Par exemple, si vous créez un service cloud nommé *contosoadservice*, et que vous configurez un rôle web nommé *contosoweb* avec deux instances, hello registres Azure suivant A des enregistrements pour les instances de hello :</span><span class="sxs-lookup"><span data-stu-id="e7f04-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers hello following A records for hello instances:</span></span>

* <span data-ttu-id="e7f04-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="e7f04-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="e7f04-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="e7f04-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="e7f04-119">Vous ne pouvez affecter qu’une seule adresse ILPIP par machine virtuelle ou instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="e7f04-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="e7f04-120">Vous pouvez utiliser des ILPIPs too5 par abonnement.</span><span class="sxs-lookup"><span data-stu-id="e7f04-120">You can use up too5 ILPIPs per subscription.</span></span> <span data-ttu-id="e7f04-121">Les adresses ILPIP ne sont pas prises en charge pour les machines virtuelles à plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="e7f04-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="e7f04-122">Pourquoi demander une adresse ILPIP ?</span><span class="sxs-lookup"><span data-stu-id="e7f04-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="e7f04-123">Si vous souhaitez toobe tooyour de tooconnect en mesure de machine virtuelle ou instance de rôle via une adresse IP affectée directement tooit, au lieu d’utiliser le cloud de hello service VIP :&lt;numéro de port&gt;, demander une ILPIP pour votre machine virtuelle ou instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="e7f04-123">If you want toobe able tooconnect tooyour VM or role instance by an IP address assigned directly tooit, rather than using hello cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="e7f04-124">**FTP actif** -en affectant une tooa ILPIP machine virtuelle, il peut recevoir le trafic sur n’importe quel port.</span><span class="sxs-lookup"><span data-stu-id="e7f04-124">**Active FTP** - By assigning an ILPIP tooa VM, it can receive traffic on any port.</span></span> <span data-ttu-id="e7f04-125">Points de terminaison ne sont pas requises pour hello le trafic tooreceive de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e7f04-125">Endpoints are not required for hello VM tooreceive traffic.</span></span>  <span data-ttu-id="e7f04-126">Pour plus d’informations sur le protocole de hello FTP, consultez (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [vue d’ensemble du protocole FTP].</span><span class="sxs-lookup"><span data-stu-id="e7f04-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on hello FTP protocol.</span></span>
* <span data-ttu-id="e7f04-127">**IP sortante** - le trafic sortant en provenance de hello machine virtuelle est mappé toohello ILPIP en tant que source de hello et hello ILPIP identifie de façon unique les entités tooexternal hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e7f04-127">**Outbound IP** - Outbound traffic originating from hello VM is mapped toohello ILPIP as hello source and hello ILPIP uniquely identifies hello VM tooexternal entities.</span></span>

> [!NOTE]
> <span data-ttu-id="e7f04-128">Bonjour précédentes, une adresse ILPIP a été référencé tooas une adresse IP (PIP) publique.</span><span class="sxs-lookup"><span data-stu-id="e7f04-128">In hello past, an ILPIP address was referred tooas a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="e7f04-129">Gérer une adresse ILPIP pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e7f04-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="e7f04-130">Bonjour tâches suivantes permettre de toocreate, affecter et supprimer ILPIPs à partir d’ordinateurs virtuels :</span><span class="sxs-lookup"><span data-stu-id="e7f04-130">hello following tasks enable you toocreate, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="e7f04-131">Comment toorequest un ILPIP lors de la création d’ordinateurs virtuels à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7f04-131">How toorequest an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="e7f04-132">Hello PowerShell script suivant crée un service cloud nommé *FTPService*, récupère une image à partir d’Azure, crée un ordinateur virtuel nommé *FTPInstance* à l’aide de l’image hello récupérée, définit hello VM toouse un ILPIP, et ajoute le nouveau service hello VM toohello :</span><span class="sxs-lookup"><span data-stu-id="e7f04-132">hello following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using hello retrieved image, sets hello VM toouse an ILPIP, and adds hello VM toohello new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="e7f04-133">Comment tooretrieve les informations de ILPIP pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e7f04-133">How tooretrieve ILPIP information for a VM</span></span>
<span data-ttu-id="e7f04-134">tooview hello ILPIP concernant hello machine virtuelle créée avec le script précédent de hello, exécutez hello suivant de commande PowerShell et observer les valeurs hello pour *PublicIPAddress* et *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="e7f04-134">tooview hello ILPIP information for hello VM created with hello previous script, run hello following PowerShell command and observe hello values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="e7f04-135">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="e7f04-135">Expected output:</span></span>
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a><span data-ttu-id="e7f04-136">Comment tooremove un ILPIP à partir d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e7f04-136">How tooremove an ILPIP from a VM</span></span>
<span data-ttu-id="e7f04-137">tooremove hello ILPIP ajouté toohello machine virtuelle dans le script précédent hello, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="e7f04-137">tooremove hello ILPIP added toohello VM in hello previous script, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a><span data-ttu-id="e7f04-138">Comment tooadd un tooan ILPIP machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="e7f04-138">How tooadd an ILPIP tooan existing VM</span></span>
<span data-ttu-id="e7f04-139">tooadd un toohello ILPIP machine virtuelle créée à l’aide du script hello précédente, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e7f04-139">tooadd an ILPIP toohello VM created using hello script previous, run hello following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="e7f04-140">Gérer une adresse ILPIP pour une instance de rôle de services cloud</span><span class="sxs-lookup"><span data-stu-id="e7f04-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="e7f04-141">tooadd une instance de rôle Services de cloud computing de tooa ILPIP, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="e7f04-141">tooadd an ILPIP tooa Cloud Services role instance, complete hello following steps:</span></span>

1. <span data-ttu-id="e7f04-142">Téléchargez le fichier .cscfg de hello pour service de cloud hello en effectuant hello étapes Bonjour [comment les Services de cloud computing tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) l’article.</span><span class="sxs-lookup"><span data-stu-id="e7f04-142">Download hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="e7f04-143">Fichier .cscfg hello en ajoutant hello `InstanceAddress` élément.</span><span class="sxs-lookup"><span data-stu-id="e7f04-143">Update hello .cscfg file by adding hello `InstanceAddress` element.</span></span> <span data-ttu-id="e7f04-144">Hello exemple suivant ajoute une ILPIP nommé *MyPublicIP* tooa instance de rôle nommé *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="e7f04-144">hello following sample adds an ILPIP named *MyPublicIP* tooa role instance named *WebRole1*:</span></span> 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. <span data-ttu-id="e7f04-145">Télécharger le fichier .cscfg de hello pour service de cloud hello en effectuant hello étapes Bonjour [comment les Services de cloud computing tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) l’article.</span><span class="sxs-lookup"><span data-stu-id="e7f04-145">Upload hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7f04-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e7f04-146">Next steps</span></span>
* <span data-ttu-id="e7f04-147">Comprendre comment [l’adressage IP](virtual-network-ip-addresses-overview-classic.md) fonctionne dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="e7f04-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="e7f04-148">En savoir plus sur les [adresses IP réservées](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="e7f04-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
