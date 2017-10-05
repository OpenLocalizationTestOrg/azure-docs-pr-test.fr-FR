---
title: "Ne stockez jamais de données sensibles sur des images personnalisées pour Azure RemoteApp | Microsoft Docs"
description: "En savoir plus sur les recommandations de stockage des données dans des images personnalisées dans Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75d5415d33324d957617426e75909a6c6c58b1f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="8ba8c-103">Ne stockez jamais de données sensibles sur des images personnalisées</span><span class="sxs-lookup"><span data-stu-id="8ba8c-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8ba8c-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8ba8c-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="8ba8c-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8ba8c-106">Lorsque vous hébergez votre propre application dans Azure RemoteApp, la première étape consiste à créer une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-106">When you host your own application in Azure RemoteApp, the first step is to create a custom image.</span></span> <span data-ttu-id="8ba8c-107">Nous utilisons cette image personnalisée pour créer des instances de machines virtuelles qui servent vos applications à vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-107">We use that custom image to create VM instances that serve your apps to your users.</span></span> <span data-ttu-id="8ba8c-108">L'image personnalisée doit contenir UNIQUEMENT des applications et jamais des données sensibles qui peuvent être perdues, notamment des bases de données SQL, des fichiers du personnel ou des fichiers de données spéciaux tels que les fichiers d'entreprise QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-108">The custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="8ba8c-109">Toutes les données sensibles doivent être externes à Azure RemoteApp, sur un serveur de fichiers, une autre machine virtuelle Azure ou SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-109">All sensitive data should reside external to Azure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="8ba8c-110">L'image doit simplement héberger l'application qui se connecte à la source de données et présente les données.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-110">The image should just host the application that connects to the data source and presents the data.</span></span> <span data-ttu-id="8ba8c-111">Consultez [Configuration requise pour les images Azure RemoteApp](remoteapp-imagereqs.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="8ba8c-112">Pour comprendre pourquoi vous ne devez pas stocker de données sensibles, vous devez comprendre le fonctionnement d'Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-112">To understand why you should not store sensitive data, you need to understand how Azure RemoteApp works.</span></span> <span data-ttu-id="8ba8c-113">Lorsqu'une collection est créée ou mise à jour, dans les coulisses, plusieurs clones ou des copies de l'image sont créés.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-113">When a collection is created or updated, behind the scenes multiple clones or copies of the image are created.</span></span> <span data-ttu-id="8ba8c-114">Toutes les instances de ces machines virtuelles sont des copies exactes de l'image personnalisée ; lorsque les utilisateurs lancent des applications, ils sont connectés à une de ces instances de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-114">All these VM instances are exact replicas of the custom image; when users launch applications they are connected to one of these VM instances.</span></span> <span data-ttu-id="8ba8c-115">Mais la même instance n'est pas garantie et importe peu car elles ne sont pas persistantes.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-115">But the same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="8ba8c-116">Les instances de machines virtuelles hébergeant les applications ne sont pas persistantes et peuvent être détruites ou supprimées, par exemple au cours de la mise à jour de la collection.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-116">The VM instances hosting the applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="8ba8c-117">Une fois que la collection est approvisionnée et que les utilisateurs commencent à se connecter aux machines virtuelles, les données utilisateur sont persistantes et protégées, car elles sont enregistrées sur un stockage distinct au sein d’un disque dur virtuel que nous appelons [disque de profil utilisateur (UPD)](remoteapp-upd.md) et qui correspond au profil utilisateur dans c:\users\<userprofile.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-117">Once the collection is provisioned and users start connecting to the VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is the user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="8ba8c-118">Lorsqu'une application démarre, l'UPD est monté et traité de la même façon qu’un profil utilisateur local par le système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-118">When an application starts, the UPD is mounted and treated just like a local user profile by the operating system.</span></span> <span data-ttu-id="8ba8c-119">En savoir plus sur la façon dont [Azure RemoteApp enregistre les données et paramètres utilisateur](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="8ba8c-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="8ba8c-120">Exemples de données qui ne doivent pas se trouver dans l'image :</span><span class="sxs-lookup"><span data-stu-id="8ba8c-120">Example data that should not reside in the image:</span></span>

* <span data-ttu-id="8ba8c-121">Données partagées accessibles aux utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8ba8c-121">Shared data for users to access</span></span>
* <span data-ttu-id="8ba8c-122">Base de données SQL ou QuickBooks</span><span class="sxs-lookup"><span data-stu-id="8ba8c-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="8ba8c-123">Toutes les données de D:\\</span><span class="sxs-lookup"><span data-stu-id="8ba8c-123">Any data in D:\\</span></span>

<span data-ttu-id="8ba8c-124">Exemples de données qui peuvent résider dans le profil par défaut à copier dans chaque UPD d’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="8ba8c-124">Example data that can reside in the default profile to be copied into every users’ UPD:</span></span>

* <span data-ttu-id="8ba8c-125">Fichiers de configuration par utilisateur</span><span class="sxs-lookup"><span data-stu-id="8ba8c-125">Configuration files per user</span></span>
* <span data-ttu-id="8ba8c-126">Scripts que les utilisateurs ont besoin de conserver dans leur UPD</span><span class="sxs-lookup"><span data-stu-id="8ba8c-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="8ba8c-127">Points clés :</span><span class="sxs-lookup"><span data-stu-id="8ba8c-127">Key points:</span></span>

* <span data-ttu-id="8ba8c-128">Ne stockez jamais de données sensibles qui peuvent être perdues sur l'image lors de la création d'une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-128">Never store sensitive data that can be lost on the image when creating a custom image.</span></span>
* <span data-ttu-id="8ba8c-129">Les données sensibles doivent toujours résider sur un serveur de fichiers distinct, sur une machine virtuelle Azure séparée, sur le cloud. Elles doivent toujours être externes aux instances de machines virtuelles qui hébergent vos applications au sein d’Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8ba8c-129">Sensitive data should always reside on a separate file server, separate Azure VM, on the cloud, and always external to the VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="8ba8c-130">Les données utilisateur sont enregistrées et conservées dans le disque de profil utilisateur (UPD)</span><span class="sxs-lookup"><span data-stu-id="8ba8c-130">User data is saved and persists in the user profile disk (UPD)</span></span>

