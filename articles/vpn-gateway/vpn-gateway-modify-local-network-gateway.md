---
title: "Modifier des préfixes d’adresses IP passerelle hello réseau local et l’adresse IP de la passerelle VPN de hello | Azure | PowerShell | Documents Microsoft"
description: "Cet article vous guide tout au long du processus de modification des préfixes d’adresse IP de la passerelle de votre réseau local à l’aide de PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="26778-103">Modification des paramètres de passerelle de réseau local à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="26778-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="26778-104">Parfois hello votre passerelle de réseau local préfixe d’adresse ou GatewayIPAddress modifiés.</span><span class="sxs-lookup"><span data-stu-id="26778-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="26778-105">Cet article vous montre comment toomodify vos paramètres de passerelle de réseau local.</span><span class="sxs-lookup"><span data-stu-id="26778-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="26778-106">Vous pouvez également modifier ces paramètres à l’aide d’une méthode différente en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="26778-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="26778-107">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="26778-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="26778-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26778-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="26778-109">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="26778-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="26778-110"><a name="before"></a>Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="26778-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="26778-111">Installer la version la plus récente hello Hello applets de commande PowerShell de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="26778-111">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="26778-112">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) pour plus d’informations sur l’installation des applets de commande PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="26778-112">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing hello PowerShell cmdlets.</span></span>

## <span data-ttu-id="26778-113"><a name="ipaddprefix"></a>Modifier les préfixes d’adresse IP</span><span class="sxs-lookup"><span data-stu-id="26778-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="26778-114"><a name="gwip"></a>Modifier l’adresse IP de passerelle hello</span><span class="sxs-lookup"><span data-stu-id="26778-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="26778-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26778-115">Next steps</span></span>

<span data-ttu-id="26778-116">Vous pouvez vérifier votre connexion à la passerelle.</span><span class="sxs-lookup"><span data-stu-id="26778-116">You can verify your gateway connection.</span></span> <span data-ttu-id="26778-117">Consultez [Vérifier la connexion à une passerelle](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="26778-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>