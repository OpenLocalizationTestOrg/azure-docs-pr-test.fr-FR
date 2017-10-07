---
title: "aaaCannot supprimer un réseau virtuel dans Azure | Documents Microsoft"
description: "Découvrez comment tootroubleshoot hello problème dans lequel vous ne pouvez pas supprimer un réseau virtuel dans Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a>Résolution des problèmes : Échec de la toodelete un réseau virtuel dans Azure

Vous pouvez recevoir des erreurs lorsque vous essayez de toodelete un réseau virtuel dans Microsoft Azure. Cet article fournit la résolution des problèmes étapes toohelp vous résolvez ce problème. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>Instructions pour la résolution des problèmes 

1. [Vérifiez si une passerelle de réseau virtuel s’exécute dans le réseau virtuel de hello](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).
2. [Vérifiez si une passerelle d’application s’exécute dans le réseau virtuel de hello](#check-whether-an-application-gateway-is-running-in-the-virtual-network).
3. [Vérifier si le Service de domaine Azure Active Directory est activée dans le réseau virtuel de hello](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).
4. [Vérifiez si le réseau virtuel de hello est connecté tooother ressources](#check-whether-the-virtual-network-is-connected-to-other-resource).
5. [Vérifiez si un ordinateur virtuel est en cours d’exécution dans le réseau virtuel de hello](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).
6. [Vérifiez si le réseau virtuel de hello est bloquée dans la migration](#check-whether-the-virtual-network-is-stuck-in-migration).

## <a name="troubleshooting-steps"></a>Étapes de dépannage

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a>Vérifiez si une passerelle de réseau virtuel s’exécute dans le réseau virtuel de hello

réseau virtuel de hello tooremove, vous devez d’abord supprimer passerelle de réseau virtuel hello.

Pour les réseaux virtuels classiques, accédez à toohello **vue d’ensemble** page de réseau virtuel classique de hello Bonjour portail Azure. Bonjour **connexions VPN** section, si hello est en cours d’exécution dans le réseau virtuel de hello, vous verrez hello IP adresse de passerelle de hello. 

![Vérifier si la passerelle est en cours d’exécution](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

Pour les réseaux virtuels, accédez à toohello **vue d’ensemble** page de réseau virtuel de hello. Vérifiez **périphériques connectés** pour la passerelle de réseau virtuel hello.

![Hello du périphérique connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

Vous pouvez supprimer la passerelle de hello, avant de supprimer les **connexion** objets dans la passerelle de hello. 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a>Vérifiez si une passerelle d’application s’exécute dans le réseau virtuel de hello

Accédez toohello **vue d’ensemble** page de réseau virtuel de hello. Vérifiez hello **périphériques connectés** pour la passerelle d’application hello.

![Hello du périphérique connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

S’il existe une passerelle d’application, vous devez le supprimer avant de pouvoir supprimer les réseaux virtuels hello.

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a>Vérifier si le Service de domaine Azure Active Directory est activée dans le réseau virtuel de hello

Si hello des services de domaine Active Directory est activée et connectée toohello des réseaux virtuels, vous ne pouvez pas supprimer ce réseau virtuel. 

![Hello du périphérique connecté](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

toodisable hello service, procédez comme suit :

1. Accédez toohello [portail Azure classic](https://manage.windowsazure.com).
2. Dans le volet gauche de hello, sélectionnez **Active Directory**.
3. Sélectionnez répertoire Azure Active Directory (Azure AD) hello qui a des services de domaine Active Directory activée.
4. Sélectionnez hello **configurer** onglet.
5. Sous **services de domaine**, modifiez hello **activer les services de domaine pour ce répertoire** option trop**non**.  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a>Vérifiez si le réseau virtuel de hello est connecté tooother ressource

Recherchez les liaisons de circuit, les connexions et les homologations de réseaux virtuels. Une de ces peut entraîner un toofail de suppression du réseau virtuel. 

Hello ordre de suppression recommandée est la suivante :

1. Connexions de passerelle
2. Passerelles
3. Adresses IP
4. Homologations de réseaux virtuels
5. App Service Environment (ASE)

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a>Vérifiez si un ordinateur virtuel est en cours d’exécution dans le réseau virtuel de hello

Assurez-vous qu’aucun ordinateur virtuel n’est dans un réseau virtuel de hello.

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a>Vérifiez si le réseau virtuel de hello est bloquée dans la migration

Si le réseau virtuel de hello est bloquée dans un état de migration, il ne peut pas être supprimé. Exécutez hello après la migration de commande tooabort hello et ensuite supprimer le réseau virtuel de hello.

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a>Étapes suivantes

- [Réseau virtuel Azure](virtual-networks-overview.md)
- [FAQ sur les réseaux virtuels Azure](virtual-networks-faq.md)