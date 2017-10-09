---
title: "aaaSpecifying paramètres DNS dans un fichier de configuration du service | Documents Microsoft"
description: "spécification de paramètres DNS personnalisés à l'aide du fichier de configuration de service d’un réseau virtuel"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>Définition des paramètres DNS dans un fichier de configuration de service
## <a name="dns-elements"></a>Éléments DNS
Un fichier de configuration de service peut contenir un élément DnsServers avec une liste d’adresses IPv4 pour les serveurs de système DNS (Domain Name) de hello hello service utilisera. Paramètres dans le fichier de configuration de service hello sont prioritaires sur les paramètres d’un fichier de configuration de réseau hello. Pour plus d’informations, consultez la rubrique [Schéma de configuration de service Azure (.cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx).

**Élément NetworkConfiguration**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> Hello **nom** attribut Bonjour **DnsServer** élément est utilisé uniquement comme un nom de référence. Il ne représente pas le nom d’hôte hello pour le serveur DNS de hello. Chaque **DnsServer** valeur d’attribut doit être unique sur tout abonnement de Microsoft Azure hello.
> 
> 

## <a name="see-also"></a>Voir aussi
[Schéma de configuration de service Azure (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Schéma de configuration du réseau virtuel Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Configuration d’un réseau virtuel à l’aide d’un fichier de configuration réseau](http://go.microsoft.com/fwlink/?LinkId=248094)

[Sur les paramètres de réseau virtuel dans hello portail de gestion](http://go.microsoft.com/fwlink/?LinkId=248092)

