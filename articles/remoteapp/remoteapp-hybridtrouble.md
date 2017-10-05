---
title: "Résoudre les problèmes de création de collections hybrides RemoteApp | Microsoft Docs"
description: "Apprenez comment dépanner les échecs de création de collections hybrides RemoteApp"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: a486dcb3f994cd78311ee86521a6792a4d57438e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="0d0ec-103">Résolution des problèmes de création de collections hybrides Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="0d0ec-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0d0ec-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0d0ec-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="0d0ec-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0d0ec-106">Une collection hybride est hébergée dans le cloud Azure et y stocke également les données, mais elle permet aussi aux utilisateurs d'accéder aux données et aux ressources stockées sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-106">A hybrid collection is hosted in and stores data in the Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="0d0ec-107">Les utilisateurs peuvent accéder aux applications en se connectant avec leurs informations d'identification d'entreprise, synchronisées ou fédérées avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="0d0ec-108">Vous pouvez déployer une collection hybride qui utilise un réseau virtuel Azure existant ou vous pouvez créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="0d0ec-109">Nous vous recommandons d’utiliser une plage CIDR suffisamment étendue lorsque vous créez ou utilisez un sous-réseau de réseau virtuel afin de pouvoir prendre en compte la croissance future d’Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="0d0ec-110">Vous n’avez pas encore créé votre collection ?</span><span class="sxs-lookup"><span data-stu-id="0d0ec-110">Haven't created your collection yet?</span></span> <span data-ttu-id="0d0ec-111">Pour plus d’informations, consultez la page [Création d’une collection hybride](remoteapp-create-hybrid-deployment.md) .</span><span class="sxs-lookup"><span data-stu-id="0d0ec-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for the steps.</span></span>

<span data-ttu-id="0d0ec-112">Si vous rencontrez des problèmes lors de la création de votre collection, ou si la collection ne fonctionne pas comme elle devrait, vérifiez les informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-112">If you are having trouble creating your collection, or if the collection isn't working the way you think it should, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="0d0ec-113">Votre image n'est pas valide</span><span class="sxs-lookup"><span data-stu-id="0d0ec-113">Your image is invalid</span></span>
<span data-ttu-id="0d0ec-114">Si vous voyez un message similaire à « GoldImageInvalid » lorsque vous attendez qu'Azure configure votre collection, cela signifie que votre image de modèle ne répond pas aux [exigences définies pour l'image](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="0d0ec-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="0d0ec-115">Donc, lisez ces [exigences](remoteapp-imagereqs.md), corrigez votre image et essayez de créer à nouveau votre collection.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="0d0ec-116">Votre réseau virtuel comporte-t-il des groupes de sécurité réseau ?</span><span class="sxs-lookup"><span data-stu-id="0d0ec-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="0d0ec-117">Si vous avez défini des groupes de sécurité réseau sur le sous-réseau que vous utilisez pour votre collection, assurez-vous que les [URL et les ports](remoteapp-ports.md) suivants sont accessibles à partir de votre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-117">If you have network security groups defined on the subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="0d0ec-118">Vous pouvez ajouter d’autres groupes de sécurité réseau pour les machines virtuelles que vous avez déployées dans le sous-réseau pour un contrôle plus strict.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-118">You can add additional network security groups to the VMs deployed by you in the subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="0d0ec-119">Utilisez-vous vos propres serveurs DNS ?</span><span class="sxs-lookup"><span data-stu-id="0d0ec-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="0d0ec-120">Et sont-ils accessibles à partir de votre sous-réseau de réseau virtuel ?</span><span class="sxs-lookup"><span data-stu-id="0d0ec-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="0d0ec-121">Vous devez vous assurer que les serveurs DNS de votre réseau sont toujours opérationnels et toujours capables de résoudre les machines virtuelles hébergées sur le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-121">You have to make sure the DNS servers in your VNET are always up and always able to resolve the virtual machines hosted in the VNET.</span></span> <span data-ttu-id="0d0ec-122">N'utilisez pas Google DNS pour cela.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="0d0ec-123">Pour les collections hybrides, vous utilisez vos propres serveurs DNS.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="0d0ec-124">Vous les spécifiez dans votre schéma de configuration réseau ou via le portail de gestion lorsque vous créez votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-124">You specify them in your network configuration schema or through the management portal when you create your virtual network.</span></span> <span data-ttu-id="0d0ec-125">Les serveurs DNS sont utilisés dans l’ordre dans lequel ils sont spécifiés par basculement, et non par tourniquet (round robin).</span><span class="sxs-lookup"><span data-stu-id="0d0ec-125">DNS servers are used in the order that they are specified in a failover manner (as opposed to round robin).</span></span>  
<span data-ttu-id="0d0ec-126">Reportez-vous à l’article [Résolution de noms pour les machines virtuelles et les instances de rôle](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) afin de vérifier que vos serveurs DNS sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-126">Please refer to [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) to make sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="0d0ec-127">Assurez-vous que les serveurs DNS de votre collection sont accessibles et disponibles à partir du sous-réseau de réseau virtuel spécifié pour cette collection.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-127">Make sure the DNS servers for your collection are accessible and available from the VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="0d0ec-128">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0d0ec-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Définition de votre serveur DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="0d0ec-130">Utilisez-vous un contrôleur de domaine Active Directory dans votre collection ?</span><span class="sxs-lookup"><span data-stu-id="0d0ec-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="0d0ec-131">Actuellement, un seul domaine Active Directory peut être associé à Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="0d0ec-132">La collection hybride prend en charge uniquement les comptes Azure Active Directory synchronisés à l’aide de l’outil DirSync à partir d’un déploiement de Windows Server Active Directory. Plus précisément, ils doivent être synchronisés avec l’option de synchronisation de mot de passe ou la fédération des services ADFS doit être configurée.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-132">The hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with the Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="0d0ec-133">Vous devez créer un domaine personnalisé qui correspond au suffixe de votre domaine local et configurer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-133">You need to create a custom domain that matches the UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="0d0ec-134">Consultez la page [Configuration d’Active Directory pour Azure RemoteApp](remoteapp-ad.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="0d0ec-135">Vérifiez que les détails du domaine fournis sont valides et que le contrôleur de domaine est accessible à partir de la machine virtuelle créée dans le sous-réseau utilisé pour Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-135">Make sure the domain details provided are valid and the domain controller is reachable from the VM created in the subnet used for Azure Remote App.</span></span> <span data-ttu-id="0d0ec-136">Assurez-vous également que les informations d’identification du compte de service fournies disposent des autorisations nécessaires pour ajouter des ordinateurs au domaine fourni et que le nom Active Directory fourni peut être résolu à partir du DNS fourni dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-136">Also make sure the service account credentials supplied have permissions to add computers to the provided domain and that the AD name provided can be resolved from the DNS provided in the VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="0d0ec-137">Quel nom de domaine avez-vous spécifié lorsque vous avez créé votre collection ?</span><span class="sxs-lookup"><span data-stu-id="0d0ec-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="0d0ec-138">Le nom de domaine que vous avez créé ou ajouté doit être un nom de domaine interne (et non pas votre nom de domaine Azure AD) et doit être au format DNS pouvant être résolu (contoso.local).</span><span class="sxs-lookup"><span data-stu-id="0d0ec-138">The domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="0d0ec-139">Par exemple, vous avez un nom interne Active Directory (contoso.local) et un UPN Active Directory (contoso.com) : vous devez utiliser le nom interne lorsque vous créez votre collection.</span><span class="sxs-lookup"><span data-stu-id="0d0ec-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have to use the internal name when you create your collection.</span></span>

