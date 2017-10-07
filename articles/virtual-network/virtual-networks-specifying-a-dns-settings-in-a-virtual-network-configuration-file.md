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
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="860f7-103">Définition des paramètres DNS dans un fichier de configuration de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="860f7-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="860f7-104">Un fichier de configuration de réseau a deux éléments que vous pouvez utiliser les paramètres du système DNS (Domain Name) toospecify : **DnsServers** et **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="860f7-104">A network configuration file has two elements that you can use toospecify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="860f7-105">Vous pouvez ajouter une liste des serveurs DNS en spécifiant leurs adresses IP et référencer des noms toohello **DnsServers** élément.</span><span class="sxs-lookup"><span data-stu-id="860f7-105">You can add a list of DNS servers by specifying their IP addresses and reference names toohello **DnsServers** element.</span></span> <span data-ttu-id="860f7-106">Vous pouvez ensuite utiliser un **DnsServerRef** toospecify élément les entrées de serveur DNS à partir de l’élément DnsServers de hello sont utilisées pour les différents sites de réseau au sein de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="860f7-106">You can then use a **DnsServerRef** element toospecify which DNS server entries from hello DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="860f7-107">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="860f7-107">This article covers hello classic deployment model.</span></span>

<span data-ttu-id="860f7-108">fichier de configuration de réseau Hello peut contenir hello suivant d’éléments.</span><span class="sxs-lookup"><span data-stu-id="860f7-108">hello network configuration file may contain hello following elements.</span></span> <span data-ttu-id="860f7-109">titre de Hello de chaque élément est lié tooa page qui fournit des informations supplémentaires sur l’élément de hello des paramètres de valeur.</span><span class="sxs-lookup"><span data-stu-id="860f7-109">hello title of each element is linked tooa page that provides additional information about hello element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="860f7-110">Pour plus d’informations sur la façon dont tooconfigure hello le fichier de configuration réseau, consultez [configuration d’un réseau virtuel à l’aide d’un fichier de Configuration réseau](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="860f7-110">For information about how tooconfigure hello network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="860f7-111">Pour plus d’informations sur chaque élément contenu dans le fichier de configuration de réseau hello, consultez [schéma de Configuration de réseau virtuel Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="860f7-111">For information about each element contained in hello network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="860f7-112">Élément Dns</span><span class="sxs-lookup"><span data-stu-id="860f7-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="860f7-113">Hello **nom** attribut Bonjour **DnsServer** élément est utilisé uniquement comme référence pour hello **DnsServerRef** élément.</span><span class="sxs-lookup"><span data-stu-id="860f7-113">hello **name** attribute in hello **DnsServer** element is used only as a reference for hello **DnsServerRef** element.</span></span> <span data-ttu-id="860f7-114">Il ne représente pas le nom d’hôte hello pour le serveur DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="860f7-114">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="860f7-115">Chaque **DnsServer** valeur d’attribut doit être unique sur tout abonnement de Microsoft Azure hello</span><span class="sxs-lookup"><span data-stu-id="860f7-115">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="860f7-116">Élément de sites de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="860f7-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="860f7-117">Dans commande toospecify ce paramètre pour l’élément de Sites de réseau virtuel hello, il doit être défini précédemment dans l’élément DNS hello.</span><span class="sxs-lookup"><span data-stu-id="860f7-117">In order toospecify this setting for hello Virtual Network Sites element, it must be previously defined in hello DNS element.</span></span> <span data-ttu-id="860f7-118">Hello DnsServerRef *nom* Bonjour Sites de réseau virtuel doit faire référence tooa nom valeur spécifiée dans l’élément DNS hello pour DnsServer *nom*.</span><span class="sxs-lookup"><span data-stu-id="860f7-118">hello DnsServerRef *name* in hello Virtual Network Sites element must refer tooa name value specified in hello DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="860f7-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="860f7-119">Next steps</span></span>
* <span data-ttu-id="860f7-120">Comprendre hello [schéma de Configuration de réseau virtuel Azure](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="860f7-120">Understand hello [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="860f7-121">Comprendre hello [schéma de Configuration du Service Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="860f7-121">Understand hello [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="860f7-122">[Configuration d’un réseau virtuel à l’aide d’un fichier de configuration réseau](virtual-networks-using-network-configuration-file.md)</span><span class="sxs-lookup"><span data-stu-id="860f7-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

