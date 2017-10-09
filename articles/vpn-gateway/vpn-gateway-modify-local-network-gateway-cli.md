---
title: "Modifier des préfixes d’adresses IP passerelle hello réseau local et l’adresse IP de la passerelle VPN de hello | Azure | CLI | Documents Microsoft"
description: "Cet article vous guide tout au long de la modification des préfixes d’adresses IP de la passerelle de réseau local à l’aide de hello CLI d’Azure."
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
ms.openlocfilehash: 4b8bbf3e9d3d42ac2d12f87360fa0a4134c57a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a><span data-ttu-id="74b0d-103">Modifier les paramètres de passerelle de réseau local à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="74b0d-103">Modify local network gateway settings using hello Azure CLI</span></span>

<span data-ttu-id="74b0d-104">Modifient parfois paramètres hello pour votre préfixe de l’adresse de passerelle de réseau local ou l’adresse IP de passerelle.</span><span class="sxs-lookup"><span data-stu-id="74b0d-104">Sometimes hello settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="74b0d-105">Cet article vous montre comment toomodify vos paramètres de passerelle de réseau local.</span><span class="sxs-lookup"><span data-stu-id="74b0d-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="74b0d-106">Vous pouvez également modifier ces paramètres à l’aide d’une méthode différente en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="74b0d-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="74b0d-107">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="74b0d-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="74b0d-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="74b0d-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="74b0d-109">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="74b0d-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="74b0d-110"><a name="before"></a>Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="74b0d-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="74b0d-111">Installer la version la plus récente hello des commandes CLI de hello (version 2.0 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="74b0d-111">Install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="74b0d-112">Pour plus d’informations sur l’installation des commandes CLI de hello, consultez [installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="74b0d-112">For information about installing hello CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="74b0d-113"><a name="ipaddprefix"></a>Modifier les préfixes d’adresse IP</span><span class="sxs-lookup"><span data-stu-id="74b0d-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="74b0d-114"><a name="gwip"></a>Modifier l’adresse IP de passerelle hello</span><span class="sxs-lookup"><span data-stu-id="74b0d-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="74b0d-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="74b0d-115">Next steps</span></span>

<span data-ttu-id="74b0d-116">Vous pouvez vérifier votre connexion à la passerelle.</span><span class="sxs-lookup"><span data-stu-id="74b0d-116">You can verify your gateway connection.</span></span> <span data-ttu-id="74b0d-117">Consultez [Vérifier la connexion à une passerelle](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="74b0d-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

