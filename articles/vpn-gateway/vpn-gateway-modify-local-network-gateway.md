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
# <a name="modify-local-network-gateway-settings-using-powershell"></a>Modification des paramètres de passerelle de réseau local à l’aide de PowerShell

Parfois hello votre passerelle de réseau local préfixe d’adresse ou GatewayIPAddress modifiés. Cet article vous montre comment toomodify vos paramètres de passerelle de réseau local. Vous pouvez également modifier ces paramètres à l’aide d’une méthode différente en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Interface de ligne de commande Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Avant de commencer

Installer la version la plus récente hello Hello applets de commande PowerShell de gestionnaire de ressources Azure. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) pour plus d’informations sur l’installation des applets de commande PowerShell hello.

## <a name="ipaddprefix"></a>Modifier les préfixes d’adresse IP

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="gwip"></a>Modifier l’adresse IP de passerelle hello

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez vérifier votre connexion à la passerelle. Consultez [Vérifier la connexion à une passerelle](vpn-gateway-verify-connection-resource-manager.md).