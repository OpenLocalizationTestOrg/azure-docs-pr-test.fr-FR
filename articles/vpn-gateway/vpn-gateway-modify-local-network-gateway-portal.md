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
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a>Modifier les paramètres de passerelle de réseau local à l’aide de hello portail Azure

Parfois hello votre passerelle de réseau local préfixe d’adresse ou GatewayIPAddress modifiés. Cet article vous montre comment toomodify vos paramètres de passerelle de réseau local. Vous pouvez également modifier ces paramètres à l’aide d’une méthode différente en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Interface de ligne de commande Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <a name="ipaddprefix"></a>Modifier les préfixes d’adresse IP

Lorsque vous modifiez des préfixes d’adresses IP, les étapes de hello que vous suivez dépendent de si votre passerelle de réseau local dispose d’une connexion.

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <a name="gwip"></a>Modifier l’adresse IP de passerelle hello

Si le périphérique VPN de hello que vous souhaitez tooconnect toohas modifié son adresse IP publique, vous devez tooreflect de passerelle du réseau local d’hello toomodify qui changent. Lorsque vous modifiez l’adresse IP hello, étapes hello que suivre dépendent de si votre passerelle de réseau local dispose d’une connexion.

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez vérifier votre connexion à la passerelle. Consultez [Vérifier la connexion à une passerelle](vpn-gateway-verify-connection-resource-manager.md).