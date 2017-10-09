---
title: "Vérifiez que le trafic d’aaaverify le transfert IP de l’Observateur réseau Azure - PowerShell | Documents Microsoft"
description: "Cet article décrit comment toocheck si tooor le trafic à partir d’un ordinateur virtuel est autorisé ou refusé à l’aide de PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="89201-103">Vérifiez si le trafic est autorisé ou refusé tooor à partir d’une machine virtuelle avec les flux IP Vérifiez un composant de l’Observateur de réseau Azure</span><span class="sxs-lookup"><span data-stu-id="89201-103">Check if traffic is allowed or denied tooor from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="89201-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="89201-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="89201-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="89201-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="89201-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="89201-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="89201-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="89201-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="89201-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="89201-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="89201-109">Vérifiez que les flux IP est une fonctionnalité de l’Observateur réseau qui vous permet de tooverify si le trafic est autorisé à tooor à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="89201-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="89201-110">Ce scénario est utile tooget un état actuel de si un ordinateur virtuel peut communiquer avec les ressources externes tooan ou principal.</span><span class="sxs-lookup"><span data-stu-id="89201-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="89201-111">Les flux IP vérifier peut être utilisé tooverify si vos règles de groupe de sécurité réseau (NSG) sont correctement configurés et résoudre les problèmes de flux qui sont bloqués par les règles du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="89201-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="89201-112">Une autre raison de l’utilisation de IP flux Vérifiez à bloquer le trafic de tooensure est bloqué correctement par hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="89201-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="89201-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="89201-113">Before you begin</span></span>

<span data-ttu-id="89201-114">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau ou une instance existante de l’Observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="89201-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="89201-115">scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.</span><span class="sxs-lookup"><span data-stu-id="89201-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="89201-116">Scénario</span><span class="sxs-lookup"><span data-stu-id="89201-116">Scenario</span></span>

<span data-ttu-id="89201-117">Ce scénario d’IP utilise vérifier tooverify si un ordinateur virtuel peuvent communiquer avec les tooa connus adresse IP de Bing.</span><span class="sxs-lookup"><span data-stu-id="89201-117">This scenario uses IP flow verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="89201-118">Si le trafic de hello est refusé, elle retourne la règle de sécurité hello refuse ce trafic.</span><span class="sxs-lookup"><span data-stu-id="89201-118">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="89201-119">toolearn plus d’informations sur le flux d’IP vérifier, visitez [les flux IP vérifier la vue d’ensemble](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="89201-119">toolearn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="89201-120">Récupérer Network Watcher</span><span class="sxs-lookup"><span data-stu-id="89201-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="89201-121">première étape de Hello est instance de l’Observateur réseau tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="89201-121">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="89201-122">Hello `$networkWatcher` variable est passée toohello IP flux vérifier l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="89201-122">hello `$networkWatcher` variable is passed toohello IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="89201-123">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="89201-123">Get a VM</span></span>

<span data-ttu-id="89201-124">Les flux IP vérifier tooor le trafic de tests à partir d’une adresse IP sur un tooor de l’ordinateur virtuel à partir d’une destination à distance.</span><span class="sxs-lookup"><span data-stu-id="89201-124">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="89201-125">Un Id d’un ordinateur virtuel est requis pour l’applet de commande hello.</span><span class="sxs-lookup"><span data-stu-id="89201-125">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="89201-126">Si vous connaissez déjà les ID hello de hello machine virtuelle toouse, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="89201-126">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a><span data-ttu-id="89201-127">Obtenir hello cartes réseau</span><span class="sxs-lookup"><span data-stu-id="89201-127">Get hello NICS</span></span>

<span data-ttu-id="89201-128">adresse IP de Hello d’une carte réseau sur l’ordinateur virtuel de hello est nécessaire, dans cet exemple, nous récupérons hello cartes d’interface réseau sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="89201-128">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="89201-129">Si vous connaissez déjà hello IP d’adresses que vous souhaitez tootest sur l’ordinateur virtuel de hello, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="89201-129">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="89201-130">Exécuter la vérification des flux IP</span><span class="sxs-lookup"><span data-stu-id="89201-130">Run IP flow verify</span></span>

<span data-ttu-id="89201-131">Maintenant que nous avons des informations hello nécessaire toorun hello applet de commande, nous exécutons hello `Test-AzureRmNetworkWatcherIPFlow` trafic de hello tootest applet de commande.</span><span class="sxs-lookup"><span data-stu-id="89201-131">Now that we have hello information needed toorun hello cmdlet, we run hello `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="89201-132">Dans cet exemple, nous utilisons la première adresse IP de hello sur la carte réseau de première hello.</span><span class="sxs-lookup"><span data-stu-id="89201-132">In this example, we are using hello first IP address on hello first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="89201-133">Les flux IP vérifier requiert que les ressources d’ordinateur virtuel hello est allouée toorun.</span><span class="sxs-lookup"><span data-stu-id="89201-133">IP flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="89201-134">Analyser les résultats</span><span class="sxs-lookup"><span data-stu-id="89201-134">Review Results</span></span>

<span data-ttu-id="89201-135">Après l’exécution `Test-AzureRmNetworkWatcherIPFlow` hello résultats sont retournés, exemple hello est résultats hello retournés à partir de hello précédant l’étape.</span><span class="sxs-lookup"><span data-stu-id="89201-135">After running `Test-AzureRmNetworkWatcherIPFlow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="89201-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89201-136">Next steps</span></span>

<span data-ttu-id="89201-137">Si le trafic est bloqué et ne doit pas être, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui sont définis.</span><span class="sxs-lookup"><span data-stu-id="89201-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













