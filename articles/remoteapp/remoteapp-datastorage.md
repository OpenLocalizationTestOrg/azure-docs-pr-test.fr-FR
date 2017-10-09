---
title: "aaaNever magasin des données sensibles sur des images personnalisées pour Azure RemoteApp | Documents Microsoft"
description: "En savoir plus sur les recommandations de hello pour le stockage des données dans des images personnalisées dans Azure RemoteApp"
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
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="61255-103">Ne stockez jamais de données sensibles sur des images personnalisées</span><span class="sxs-lookup"><span data-stu-id="61255-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="61255-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="61255-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="61255-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="61255-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="61255-106">Lorsque vous hébergez votre application dans Azure RemoteApp, hello première étape consiste toocreate une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="61255-106">When you host your own application in Azure RemoteApp, hello first step is toocreate a custom image.</span></span> <span data-ttu-id="61255-107">Nous utilisons ce instances de machine virtuelle toocreate image personnalisée qui font Office de vos applications tooyour utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="61255-107">We use that custom image toocreate VM instances that serve your apps tooyour users.</span></span> <span data-ttu-id="61255-108">image personnalisée de Hello doit contenir uniquement les applications et les données sensibles ne peuvent être perdues, telles que les bases de données SQL, les fichiers du personnel ou des fichiers de données spéciaux tels que les fichiers d’entreprise QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="61255-108">hello custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="61255-109">Toutes les données sensibles doivent résider externe tooAzure RemoteApp sur un serveur de fichiers, une autre machine virtuelle Azure, ou dans SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="61255-109">All sensitive data should reside external tooAzure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="61255-110">image de Hello doit simplement hello application hôte se connecte la source de données toohello et présente les données de hello.</span><span class="sxs-lookup"><span data-stu-id="61255-110">hello image should just host hello application that connects toohello data source and presents hello data.</span></span> <span data-ttu-id="61255-111">Consultez [Configuration requise pour les images Azure RemoteApp](remoteapp-imagereqs.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="61255-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="61255-112">toounderstand pourquoi vous ne devez pas stocker les données sensibles, vous devez toounderstand fonctionnement d’Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="61255-112">toounderstand why you should not store sensitive data, you need toounderstand how Azure RemoteApp works.</span></span> <span data-ttu-id="61255-113">Lorsqu’une collection est créée ou mis à jour, coulisses hello plusieurs clones ou des copies de l’image de hello sont créés.</span><span class="sxs-lookup"><span data-stu-id="61255-113">When a collection is created or updated, behind hello scenes multiple clones or copies of hello image are created.</span></span> <span data-ttu-id="61255-114">Toutes les instances de ces ordinateurs virtuels sont des copies exactes de l’image personnalisée de hello ; Lorsque les utilisateurs lancent des applications qu’ils sont connecté tooone de ces instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="61255-114">All these VM instances are exact replicas of hello custom image; when users launch applications they are connected tooone of these VM instances.</span></span> <span data-ttu-id="61255-115">Mais hello même instance n’est pas garanti et importe peu, car ils ne sont pas permanentes.</span><span class="sxs-lookup"><span data-stu-id="61255-115">But hello same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="61255-116">Bonjour instances de machine virtuelle hello hébergement des applications sont non persistants et peuvent être détruits ou supprimés en fonction, par exemple, au cours de la mise à jour de la collection.</span><span class="sxs-lookup"><span data-stu-id="61255-116">hello VM instances hosting hello applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="61255-117">Une fois que la collection de hello est configurée et les utilisateurs commencent toohello connexion machines virtuelles, les données utilisateur sont persistantes et protégé, car elle est enregistrée sur le stockage distinct au sein d’un disque dur virtuel que nous appelons un [disque de profil utilisateur (UPD)](remoteapp-upd.md), qui est le profil d’utilisateur hello dans c:\users\<userprofile >.</span><span class="sxs-lookup"><span data-stu-id="61255-117">Once hello collection is provisioned and users start connecting toohello VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is hello user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="61255-118">Lorsqu’une application démarre, hello UPD est monté et traité comme un profil utilisateur local par le système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="61255-118">When an application starts, hello UPD is mounted and treated just like a local user profile by hello operating system.</span></span> <span data-ttu-id="61255-119">En savoir plus sur la façon dont [Azure RemoteApp enregistre les données et paramètres utilisateur](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="61255-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="61255-120">Exemple de données qui ne doit pas résider dans l’image de hello :</span><span class="sxs-lookup"><span data-stu-id="61255-120">Example data that should not reside in hello image:</span></span>

* <span data-ttu-id="61255-121">Données partagées pour les utilisateurs tooaccess</span><span class="sxs-lookup"><span data-stu-id="61255-121">Shared data for users tooaccess</span></span>
* <span data-ttu-id="61255-122">Base de données SQL ou QuickBooks</span><span class="sxs-lookup"><span data-stu-id="61255-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="61255-123">Toutes les données de D:\\</span><span class="sxs-lookup"><span data-stu-id="61255-123">Any data in D:\\</span></span>

<span data-ttu-id="61255-124">Exemple de données qui peut résider dans toobe de profil par défaut hello copié dans UPD chaque utilisateurs :</span><span class="sxs-lookup"><span data-stu-id="61255-124">Example data that can reside in hello default profile toobe copied into every users’ UPD:</span></span>

* <span data-ttu-id="61255-125">Fichiers de configuration par utilisateur</span><span class="sxs-lookup"><span data-stu-id="61255-125">Configuration files per user</span></span>
* <span data-ttu-id="61255-126">Scripts que les utilisateurs ont besoin de conserver dans leur UPD</span><span class="sxs-lookup"><span data-stu-id="61255-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="61255-127">Points clés :</span><span class="sxs-lookup"><span data-stu-id="61255-127">Key points:</span></span>

* <span data-ttu-id="61255-128">Ne stockez jamais des données sensibles qui peuvent être perdues sur l’image de hello lors de la création d’une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="61255-128">Never store sensitive data that can be lost on hello image when creating a custom image.</span></span>
* <span data-ttu-id="61255-129">Les données sensibles doivent toujours résider sur un serveur de fichiers distincts, en séparant Azure VM, sur le cloud de hello, toohello externe toujours les instances de machine virtuelle qui héberge vos applications dans Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="61255-129">Sensitive data should always reside on a separate file server, separate Azure VM, on hello cloud, and always external toohello VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="61255-130">Données utilisateur sont enregistrées et persiste dans le disque de profil utilisateur hello (UPD)</span><span class="sxs-lookup"><span data-stu-id="61255-130">User data is saved and persists in hello user profile disk (UPD)</span></span>

