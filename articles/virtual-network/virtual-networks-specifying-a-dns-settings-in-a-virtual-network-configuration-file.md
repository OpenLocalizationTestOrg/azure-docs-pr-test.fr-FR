---
title: "aaaSpecifying paramètres DNS dans un fichier de configuration de réseau virtuel | Documents Microsoft"
description: "Comment toochange des paramètres de serveur DNS dans un réseau virtuel à l’aide d’une configuration de réseau virtuel du fichier dans le modèle de déploiement classique de hello"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a>Définition des paramètres DNS dans un fichier de configuration de réseau virtuel
Un fichier de configuration de réseau a deux éléments que vous pouvez utiliser les paramètres du système DNS (Domain Name) toospecify : **DnsServers** et **DnsServerRef**. Vous pouvez ajouter une liste des serveurs DNS en spécifiant leurs adresses IP et référencer des noms toohello **DnsServers** élément. Vous pouvez ensuite utiliser un **DnsServerRef** toospecify élément les entrées de serveur DNS à partir de l’élément DnsServers de hello sont utilisées pour les différents sites de réseau au sein de votre réseau virtuel.

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement classique hello.

fichier de configuration de réseau Hello peut contenir hello suivant d’éléments. titre de Hello de chaque élément est lié tooa page qui fournit des informations supplémentaires sur l’élément de hello des paramètres de valeur.

> [!IMPORTANT]
> Pour plus d’informations sur la façon dont tooconfigure hello le fichier de configuration réseau, consultez [configuration d’un réseau virtuel à l’aide d’un fichier de Configuration réseau](virtual-networks-using-network-configuration-file.md). Pour plus d’informations sur chaque élément contenu dans le fichier de configuration de réseau hello, consultez [schéma de Configuration de réseau virtuel Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
> 
> 

[Élément Dns](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> Hello **nom** attribut Bonjour **DnsServer** élément est utilisé uniquement comme référence pour hello **DnsServerRef** élément. Il ne représente pas le nom d’hôte hello pour le serveur DNS de hello. Chaque **DnsServer** valeur d’attribut doit être unique sur tout abonnement de Microsoft Azure hello
> 
> 

[Élément de sites de réseau virtuel](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> Dans commande toospecify ce paramètre pour l’élément de Sites de réseau virtuel hello, il doit être défini précédemment dans l’élément DNS hello. Hello DnsServerRef *nom* Bonjour Sites de réseau virtuel doit faire référence tooa nom valeur spécifiée dans l’élément DNS hello pour DnsServer *nom*.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Comprendre hello [schéma de Configuration de réseau virtuel Azure](http://go.microsoft.com/fwlink/?LinkId=248093).
* Comprendre hello [schéma de Configuration du Service Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).
* [Configuration d’un réseau virtuel à l’aide d’un fichier de configuration réseau](virtual-networks-using-network-configuration-file.md)

