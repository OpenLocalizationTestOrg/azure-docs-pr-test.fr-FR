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
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="7d77e-103">Définition des paramètres DNS dans un fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7d77e-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="7d77e-104">Éléments DNS</span><span class="sxs-lookup"><span data-stu-id="7d77e-104">DNS elements</span></span>
<span data-ttu-id="7d77e-105">Un fichier de configuration de service peut contenir un élément DnsServers avec une liste d’adresses IPv4 pour les serveurs de système DNS (Domain Name) de hello hello service utilisera.</span><span class="sxs-lookup"><span data-stu-id="7d77e-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for hello Domain Name System (DNS) servers that hello service will use.</span></span> <span data-ttu-id="7d77e-106">Paramètres dans le fichier de configuration de service hello sont prioritaires sur les paramètres d’un fichier de configuration de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="7d77e-106">Settings in hello service configuration file take precedence over settings in hello network configuration file.</span></span> <span data-ttu-id="7d77e-107">Pour plus d’informations, consultez la rubrique [Schéma de configuration de service Azure (.cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d77e-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="7d77e-108">**Élément NetworkConfiguration**</span><span class="sxs-lookup"><span data-stu-id="7d77e-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="7d77e-109">Hello **nom** attribut Bonjour **DnsServer** élément est utilisé uniquement comme un nom de référence.</span><span class="sxs-lookup"><span data-stu-id="7d77e-109">hello **name** attribute in hello **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="7d77e-110">Il ne représente pas le nom d’hôte hello pour le serveur DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="7d77e-110">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="7d77e-111">Chaque **DnsServer** valeur d’attribut doit être unique sur tout abonnement de Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7d77e-111">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="7d77e-112">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7d77e-112">See Also</span></span>
[<span data-ttu-id="7d77e-113">Schéma de configuration de service Azure (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="7d77e-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="7d77e-114">Schéma de configuration du réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="7d77e-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="7d77e-115">Configuration d’un réseau virtuel à l’aide d’un fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="7d77e-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="7d77e-116">Sur les paramètres de réseau virtuel dans hello portail de gestion</span><span class="sxs-lookup"><span data-stu-id="7d77e-116">About Virtual Network settings in hello Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

