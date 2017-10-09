---
title: "listes de contrôle d’accès de point de terminaison Azure d’aaaManage | PowerShell | Classique | Documents Microsoft"
description: "Découvrez comment toomanage ACL avec PowerShell"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a>Gérer les listes de contrôle d’accès de point de terminaison à l’aide de PowerShell dans le modèle de déploiement classique de hello
Vous pouvez créer et gérer des listes de contrôle d’accès réseau (ACL) pour les points de terminaison à l’aide d’Azure PowerShell ou dans le portail de gestion de hello. Dans cette rubrique, vous trouverez des procédures pour les tâches courantes des listes de contrôle d’accès que vous pouvez effectuer à l’aide de PowerShell. Pour la liste d’Azure PowerShell hello applets de commande consultez [applets de commande Azure Management](http://go.microsoft.com/fwlink/?LinkId=317721). Pour plus d’informations sur les listes de contrôle d’accès, consultez [Qu’est-ce qu’une liste de contrôle d’accès (ACL) réseau ?](virtual-networks-acl.md). Si vous souhaitez toomanage vos ACL à l’aide du portail de gestion de hello, consultez [comment tooSet des points de terminaison tooa Machine virtuelle](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="manage-network-acls-by-using-azure-powershell"></a>Gérer les listes de contrôle d’accès réseau à l’aide d’Azure PowerShell
Vous pouvez utiliser toocreate d’applets de commande Azure PowerShell, supprimer et configurer (set) listes de contrôle d’accès réseau (ACL). Nous avons inclus quelques exemples de certaines façons hello que vous pouvez configurer une liste ACL à l’aide de PowerShell.

tooretrieve une liste complète des applets de commande PowerShell de l’ACL de hello, vous pouvez utiliser de hello suivantes :

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a>Créer une liste de contrôle d’accès réseau avec des règles qui autorisent l’accès à un sous-réseau distant
exemple Hello ci-dessous illustre un toocreate de façon une ACL contient des règles. Cette liste ACL est ensuite appliquée tooa point de terminaison de machine virtuelle. listes de contrôle Hello dans l’exemple hello ci-dessous permettront l’accès à un sous-réseau distant. toocreate une ACL réseau avec les règles d’autorisation pour un sous-réseau distant, ouvrez Azure PowerShell ISE. Copiez et collez le script hello ci-dessous, configurez le script de hello avec vos propres valeurs et puis exécutez le script de hello.

1. Créer un nouvel objet de liste ACL réseau hello.
   
        $acl1 = New-AzureAclConfig
2. Définissez une règle qui autorise l’accès depuis un sous-réseau distant. Dans l’exemple hello ci-dessous, vous définissez la règle *100* (qui est prioritaire sur la règle 200 et versions ultérieures) sous-réseau distant de hello tooallow *10.0.0.0/8* accéder au point de terminaison de machine virtuelle toohello. Remplacez les valeurs hello par vos propres exigences de configuration. nom de Hello « SharePoint ACL config » doit être remplacé par nom convivial de hello que vous souhaitez toocall cette règle.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. Pour les règles supplémentaires, répétez l’applet de commande hello, en remplaçant les valeurs hello avec vos propres exigences de configuration. Être vraiment toochange hello règle numéro tooreflect hello commande dans lequel vous souhaitez hello règles toobe est appliqué. nombre le moins élevé Hello est prioritaire sur nombre plus élevé de hello.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. Ensuite, vous pouvez créer un nouveau point de terminaison (Add) ou définir hello ACL pour un point de terminaison existant (Set). Dans cet exemple, nous allons ajouter qu'un nouveau point de terminaison de machine virtuelle appelé « web » et la mise à jour de terminaison de machine virtuelle hello avec hello paramètres ACL.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. Ensuite, combinez les applets de commande hello et exécuter le script de hello. Pour cet exemple, hello combiné des applets de commande ressemble à ceci :
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a>Supprimer une règle de liste de contrôle d’accès réseau qui autorise l’accès depuis un sous-réseau distant
exemple Hello ci-dessous illustre une façon de tooremove une règle de liste ACL réseau.  règles de tooremove une règle ACL réseau avec une autorisation pour un sous-réseau distant, ouvrez Azure PowerShell ISE. Copiez et collez le script hello ci-dessous, configurez le script de hello avec vos propres valeurs et puis exécutez le script de hello.

1. Première étape est tooget hello ACL réseau objet point de terminaison de machine virtuelle hello. Vous devez ensuite supprimer règle hello. Dans ce cas, nous la supprimons par son ID de règle. Cela supprime uniquement les ID de règle hello 0 à partir de la liste ACL de hello. Elle ne supprime pas l’objet de liste ACL hello à partir du point de terminaison de machine virtuelle hello.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. Ensuite, vous devez appliquer le point de terminaison de machine virtuelle hello ACL réseau objet toohello et mettre à jour de la machine virtuelle de hello.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a>Supprimer une liste de contrôle d’accès réseau d’un point de terminaison de machine virtuelle
Dans certains scénarios, vous pourriez tooremove un objet ACL réseau à partir d’un point de terminaison de machine virtuelle. toodo qui, ouvrez Azure PowerShell ISE. Copiez et collez le script hello ci-dessous, configurez le script de hello avec vos propres valeurs et puis exécutez le script de hello.

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a>Étapes suivantes
[Qu’est-ce qu’une liste de contrôle d’accès (ACL) réseau ?](virtual-networks-acl.md)

