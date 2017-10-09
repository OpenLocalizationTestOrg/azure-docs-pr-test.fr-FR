---
title: "informations aaaSizing pour un réseau virtuel dans Azure RemoteApp | Documents Microsoft"
description: "En savoir plus sur les conditions de l’adressage IP hello pour Azure RemoteApp en cours d’exécution avec un réseau virtuel"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="a3b53-103">Informations sur la taille des réseaux virtuels dans Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="a3b53-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a3b53-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="a3b53-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a3b53-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a3b53-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a3b53-106">Lorsque vous utilisez Azure RemoteApp avec un réseau virtuel (VNET), RemoteApp utilise des adresses IP au sein du sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="a3b53-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within hello subnet.</span></span> <span data-ttu-id="a3b53-107">En fonction de l’échelle de hello de votre service RemoteApp, vous devez tooensure que votre sous-réseau possède suffisamment d’adresses IP pour les ordinateurs virtuels de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a3b53-107">Based on hello scale of your RemoteApp service, you need tooensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="a3b53-108">Bien que ces indications sur la taille ne soient pas parfaites, compte tenu de la manière dont RemoteApp monte ou descend dynamiquement les machines virtuelles au sein d’une collection, celles-ci vous aideront à évaluer votre plage de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="a3b53-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="a3b53-109">Cela est particulièrement important car, une fois qu’un service RemoteApp est placé dans un réseau virtuel, vous ne peut pas augmenter la taille du sous-réseau hello sans supprimer RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a3b53-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase hello subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="a3b53-110">Pour chaque collection RemoteApp que vous souhaitez toorun atteint sa capacité maximale, vous devez disposer de 100 adresses IP disponibles.</span><span class="sxs-lookup"><span data-stu-id="a3b53-110">For each RemoteApp collection that you want toorun at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="a3b53-111">Par exemple, si vous avez une collection RemoteApp dans le plan Standard de hello et que vous souhaitez toohave hello maximum 500 utilisateurs, vous aurez 100 adresses IP dans la collection.</span><span class="sxs-lookup"><span data-stu-id="a3b53-111">For example, if you have one RemoteApp collection in hello Standard plan and you want toohave hello maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="a3b53-112">De même, vous devez 100 adresses IP pour une collection RemoteApp dans le plan de base hello a 800 utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a3b53-112">Similarly, you need 100 IP addresses for a RemoteApp collection in hello Basic plan that has 800 users.</span></span> <span data-ttu-id="a3b53-113">Si vous envisagez de toohave un nombre d’utilisateurs (inférieur à hello maximale), vous pouvez réduire des adresses IP hello nécessaires par collection.</span><span class="sxs-lookup"><span data-stu-id="a3b53-113">If you plan toohave fewer users (less than hello maximum), you can reduce hello IP addresses needed per collection.</span></span> <span data-ttu-id="a3b53-114">spécification de taille minimale de sous-réseau Hello est 30 adresses IP (/ 27).</span><span class="sxs-lookup"><span data-stu-id="a3b53-114">hello minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="a3b53-115">Passez en revue hello suivant toomake informations que votre réseau virtuel est configuré et fonctionne correctement :</span><span class="sxs-lookup"><span data-stu-id="a3b53-115">Check out hello following information toomake sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="a3b53-116">Migrer à partir d’un tooan de réseau virtuel personnel réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="a3b53-116">Migrate from a personal VNET tooan Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="a3b53-117">Valider toouse de réseau virtuel Azure hello avec Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="a3b53-117">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>](remoteapp-vnet.md)

