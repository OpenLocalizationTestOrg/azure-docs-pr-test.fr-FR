---
title: "aaaTroubleshoot création de regroupements hybride de RemoteApp | Documents Microsoft"
description: "Découvrez comment tootroubleshoot les échecs de création de collection hybride de RemoteApp"
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
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="3cbd6-103">Résolution des problèmes de création de collections hybrides Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3cbd6-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3cbd6-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3cbd6-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3cbd6-106">Une collection hybride est hébergée dans et stocke des données dans hello cloud Azure, mais également permet aux utilisateurs accéder aux données et ressources stockées sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-106">A hybrid collection is hosted in and stores data in hello Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="3cbd6-107">Les utilisateurs peuvent accéder aux applications en se connectant avec leurs informations d'identification d'entreprise, synchronisées ou fédérées avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="3cbd6-108">Vous pouvez déployer une collection hybride qui utilise un réseau virtuel Azure existant ou vous pouvez créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="3cbd6-109">Nous vous recommandons d’utiliser une plage CIDR suffisamment étendue lorsque vous créez ou utilisez un sous-réseau de réseau virtuel afin de pouvoir prendre en compte la croissance future d’Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="3cbd6-110">Vous n’avez pas encore créé votre collection ?</span><span class="sxs-lookup"><span data-stu-id="3cbd6-110">Haven't created your collection yet?</span></span> <span data-ttu-id="3cbd6-111">Consultez [créer une collection hybride](remoteapp-create-hybrid-deployment.md) pour connaître les étapes hello.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for hello steps.</span></span>

<span data-ttu-id="3cbd6-112">Si vous rencontrez des problèmes de création de votre collection, ou si la collection de hello ne fonctionne pas moyen hello vous pensez qu’il doit, consultez hello informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-112">If you are having trouble creating your collection, or if hello collection isn't working hello way you think it should, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="3cbd6-113">Votre image n'est pas valide</span><span class="sxs-lookup"><span data-stu-id="3cbd6-113">Your image is invalid</span></span>
<span data-ttu-id="3cbd6-114">Si vous voyez un message comme « GoldImageInvalid » lorsque vous attendez Azure tooprovision votre collection, cela signifie que votre image de modèle ne répond pas aux hello [défini des exigences de l’image](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="3cbd6-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="3cbd6-115">Par conséquent, accédez à lire les [exigences](remoteapp-imagereqs.md), corrigez votre image et essayez toocreate à nouveau votre collection.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="3cbd6-116">Votre réseau virtuel comporte-t-il des groupes de sécurité réseau ?</span><span class="sxs-lookup"><span data-stu-id="3cbd6-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="3cbd6-117">Si vous avez définis sur le sous-réseau hello vous utilisez pour votre collection de groupes de sécurité réseau, assurez-vous que ces [URL et ports](remoteapp-ports.md) sont accessibles à partir de votre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-117">If you have network security groups defined on hello subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="3cbd6-118">Vous pouvez ajouter le réseau supplémentaires sécurité groupes toohello les ordinateurs virtuels déployés par vous dans un sous-réseau hello pour un contrôle plus strict.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-118">You can add additional network security groups toohello VMs deployed by you in hello subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="3cbd6-119">Utilisez-vous vos propres serveurs DNS ?</span><span class="sxs-lookup"><span data-stu-id="3cbd6-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="3cbd6-120">Et sont-ils accessibles à partir de votre sous-réseau de réseau virtuel ?</span><span class="sxs-lookup"><span data-stu-id="3cbd6-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="3cbd6-121">Vous avez toomake hello que les serveurs DNS dans votre réseau virtuel sont toujours des et toujours en mesure de tooresolve hello virtuels hébergés dans hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-121">You have toomake sure hello DNS servers in your VNET are always up and always able tooresolve hello virtual machines hosted in hello VNET.</span></span> <span data-ttu-id="3cbd6-122">N'utilisez pas Google DNS pour cela.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="3cbd6-123">Pour les collections hybrides, vous utilisez vos propres serveurs DNS.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="3cbd6-124">Vous spécifiez les dans votre schéma de configuration réseau ou via le portail de gestion hello lorsque vous créez votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-124">You specify them in your network configuration schema or through hello management portal when you create your virtual network.</span></span> <span data-ttu-id="3cbd6-125">Serveurs DNS sont utilisés dans l’ordre de hello qu’elles sont spécifiées sous forme de basculement (en opposition tooround (Round Robin)).</span><span class="sxs-lookup"><span data-stu-id="3cbd6-125">DNS servers are used in hello order that they are specified in a failover manner (as opposed tooround robin).</span></span>  
<span data-ttu-id="3cbd6-126">Reportez-vous trop[résolution de noms pour les machines virtuelles et Instances de rôle](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake que vos serveurs DNS sont correcly configuré.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-126">Please refer too[Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="3cbd6-127">Assurez-vous que les serveurs DNS hello pour votre collection sont accessibles et disponibles à partir du sous-réseau de réseau virtuel hello que vous avez spécifié pour cette collection.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-127">Make sure hello DNS servers for your collection are accessible and available from hello VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="3cbd6-128">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3cbd6-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Définition de votre serveur DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="3cbd6-130">Utilisez-vous un contrôleur de domaine Active Directory dans votre collection ?</span><span class="sxs-lookup"><span data-stu-id="3cbd6-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="3cbd6-131">Actuellement, un seul domaine Active Directory peut être associé à Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="3cbd6-132">collection de hybride Hello prend en charge uniquement les comptes Azure Active Directory qui ont été synchronisés à l’aide d’outil de synchronisation d’annuaire à partir d’un déploiement de Windows Server Active Directory ; plus précisément, soit synchronisé avec l’option de synchronisation de mot de passe de hello soit synchronisé avec fédération des Services de fédération Active Directory (AD FS) configurée.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-132">hello hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with hello Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="3cbd6-133">Vous devez toocreate un domaine personnalisé qui correspond au suffixe de domaine hello pour votre domaine local et configurez l’intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-133">You need toocreate a custom domain that matches hello UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="3cbd6-134">Consultez la page [Configuration d’Active Directory pour Azure RemoteApp](remoteapp-ad.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="3cbd6-135">Assurez-vous que les informations de domaine hello fournies sont valides et contrôleur de domaine hello est accessible à partir de hello que machine virtuelle créée dans le sous-réseau de hello utilisé pour l’application Azure à distance.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-135">Make sure hello domain details provided are valid and hello domain controller is reachable from hello VM created in hello subnet used for Azure Remote App.</span></span> <span data-ttu-id="3cbd6-136">Veillez également à ce compte de service hello informations d’identification fournies ont des autorisations tooadd ordinateurs toohello autant de domaine et qui hello nom AD fourni peut être résolu à partir de hello DNS fourni dans hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-136">Also make sure hello service account credentials supplied have permissions tooadd computers toohello provided domain and that hello AD name provided can be resolved from hello DNS provided in hello VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="3cbd6-137">Quel nom de domaine avez-vous spécifié lorsque vous avez créé votre collection ?</span><span class="sxs-lookup"><span data-stu-id="3cbd6-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="3cbd6-138">nom de domaine Hello vous avez créé ou ajouté doit être un nom de domaine interne (pas votre nom de domaine Azure AD) et doit être au format DNS pouvant être résolu (contoso.local).</span><span class="sxs-lookup"><span data-stu-id="3cbd6-138">hello domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="3cbd6-139">Par exemple, vous avez un nom interne de Active Directory (contoso.local) et un UPN de répertoire (contoso.com) - Active que nom interne de toouse hello lorsque vous créez votre collection.</span><span class="sxs-lookup"><span data-stu-id="3cbd6-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have toouse hello internal name when you create your collection.</span></span>

