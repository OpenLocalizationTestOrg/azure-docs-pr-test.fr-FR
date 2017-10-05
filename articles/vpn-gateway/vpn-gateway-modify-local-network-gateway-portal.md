---
title: "Modifier les préfixes d’adresse IP d’une passerelle de réseau local et l’adresse IP d’une passerelle VPN | Azure | Portail | Microsoft Docs"
description: "Cet article vous guide tout au long du processus de modification des préfixes d’adresse IP de la passerelle de votre réseau local à l’aide du portail Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: bdd6f90fe97408bd45a72adf58bfdc190207de46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-portal"></a><span data-ttu-id="ec49f-103">Modifier les paramètres de la passerelle du réseau local à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="ec49f-103">Modify local network gateway settings using the Azure portal</span></span>

<span data-ttu-id="ec49f-104">Parfois, les paramètres de la passerelle de réseau local AddressPrefix ou GatewayIPAddress changent.</span><span class="sxs-lookup"><span data-stu-id="ec49f-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="ec49f-105">Cet article vous montre comment modifier les paramètres de passerelle de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="ec49f-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="ec49f-106">Vous pouvez également modifier ces paramètres à l’aide d’une méthode différente en sélectionnant une autre option dans la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="ec49f-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec49f-107">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ec49f-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="ec49f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec49f-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="ec49f-109">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ec49f-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="ec49f-110"><a name="ipaddprefix"></a>Modifier les préfixes d’adresse IP</span><span class="sxs-lookup"><span data-stu-id="ec49f-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="ec49f-111">Lorsque vous modifiez des préfixes d’adresse IP, la procédure à suivre varie selon que votre passerelle de réseau local dispose d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="ec49f-111">When you modify IP address prefixes, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="ec49f-112"><a name="gwip"></a>Modifier l’adresse IP de la passerelle</span><span class="sxs-lookup"><span data-stu-id="ec49f-112"><a name="gwip"></a>Modify the gateway IP address</span></span>

<span data-ttu-id="ec49f-113">Si le périphérique VPN auquel vous souhaitez vous connecter a changé son adresse IP publique, vous devez modifier la passerelle de réseau local pour refléter cette modification.</span><span class="sxs-lookup"><span data-stu-id="ec49f-113">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="ec49f-114">Lorsque vous modifiez l’adresse IP publique, la procédure à suivre varie selon que votre passerelle de réseau local dispose d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="ec49f-114">When you change the public IP address, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ec49f-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec49f-115">Next steps</span></span>

<span data-ttu-id="ec49f-116">Vous pouvez vérifier votre connexion à la passerelle.</span><span class="sxs-lookup"><span data-stu-id="ec49f-116">You can verify your gateway connection.</span></span> <span data-ttu-id="ec49f-117">Consultez [Vérifier la connexion à une passerelle](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ec49f-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>