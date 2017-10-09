---
title: "Modifier des préfixes d’adresses IP passerelle hello réseau local et l’adresse IP de la passerelle VPN de hello | Azure | Portail | Documents Microsoft"
description: "Cet article vous guide tout au long de la modification des préfixes d’adresses IP de la passerelle de réseau local à l’aide de hello portail Azure."
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
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a><span data-ttu-id="1a4fd-103">Modifier les paramètres de passerelle de réseau local à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1a4fd-103">Modify local network gateway settings using hello Azure portal</span></span>

<span data-ttu-id="1a4fd-104">Parfois hello votre passerelle de réseau local préfixe d’adresse ou GatewayIPAddress modifiés.</span><span class="sxs-lookup"><span data-stu-id="1a4fd-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="1a4fd-105">Cet article vous montre comment toomodify vos paramètres de passerelle de réseau local.</span><span class="sxs-lookup"><span data-stu-id="1a4fd-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="1a4fd-106">Vous pouvez également modifier ces paramètres à l’aide d’une méthode différente en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="1a4fd-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a4fd-107">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1a4fd-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="1a4fd-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a4fd-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="1a4fd-109">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="1a4fd-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="1a4fd-110"><a name="ipaddprefix"></a>Modifier les préfixes d’adresse IP</span><span class="sxs-lookup"><span data-stu-id="1a4fd-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="1a4fd-111">Lorsque vous modifiez des préfixes d’adresses IP, les étapes de hello que vous suivez dépendent de si votre passerelle de réseau local dispose d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="1a4fd-111">When you modify IP address prefixes, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="1a4fd-112"><a name="gwip"></a>Modifier l’adresse IP de passerelle hello</span><span class="sxs-lookup"><span data-stu-id="1a4fd-112"><a name="gwip"></a>Modify hello gateway IP address</span></span>

<span data-ttu-id="1a4fd-113">Si le périphérique VPN de hello que vous souhaitez tooconnect toohas modifié son adresse IP publique, vous devez tooreflect de passerelle du réseau local d’hello toomodify qui changent.</span><span class="sxs-lookup"><span data-stu-id="1a4fd-113">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="1a4fd-114">Lorsque vous modifiez l’adresse IP hello, étapes hello que suivre dépendent de si votre passerelle de réseau local dispose d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="1a4fd-114">When you change hello public IP address, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1a4fd-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a4fd-115">Next steps</span></span>

<span data-ttu-id="1a4fd-116">Vous pouvez vérifier votre connexion à la passerelle.</span><span class="sxs-lookup"><span data-stu-id="1a4fd-116">You can verify your gateway connection.</span></span> <span data-ttu-id="1a4fd-117">Consultez [Vérifier la connexion à une passerelle](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1a4fd-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>