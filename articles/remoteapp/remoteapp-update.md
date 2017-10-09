---
title: aaaUpdate votre collection Azure RemoteApp | Documents Microsoft
description: "Découvrez comment tooupdate votre collection Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="d0dd8-103">Mise à jour d’une collection dans Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d0dd8-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d0dd8-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d0dd8-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d0dd8-106">Il arrivera un moment, inévitablement, lorsque vous devez tooupdate hello applications ou l’image dans votre collection Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-106">There will come a time, inevitably, when you need tooupdate hello apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="d0dd8-107">Si vous utilisez une des images hello inclus dans votre abonnement Azure RemoteApp, dans la collection un cloud ou hybride, mises à jour toutes les sont gérées par Azure RemoteApp lui-même, vous pouvez compter.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-107">If you are using one of hello images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="d0dd8-108">Toutefois, si vous utilisez une image personnalisée (que vous avez créé à partir de zéro ou que vous avez créé en modifiant un de nos images), vous êtes responsable de la gestion d’applications et image de hello.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining hello image and apps.</span></span> <span data-ttu-id="d0dd8-109">Si vous devez tooupdate votre image ou l’une des applications hello qu’il contient, vous devez toocreate une nouvelle version mise à jour d’image de hello, puis image existante du hello remplacer dans votre collection avec cette nouvelle image mis à jour.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-109">If you need tooupdate your image or any of hello apps inside it, you need toocreate a new, updated version of hello image, and then replace hello existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="d0dd8-110">Comment mettre à jour votre collection ?</span><span class="sxs-lookup"><span data-stu-id="d0dd8-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="d0dd8-111">C’est simple :</span><span class="sxs-lookup"><span data-stu-id="d0dd8-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="d0dd8-112">Image de hello de mise à jour que vous avez utilisé dans votre collection.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-112">Update hello image that you used in your collection.</span></span> <span data-ttu-id="d0dd8-113">Appliquez tous les correctifs et toutes les mises à jour nécessaires, puis enregistrez-la sous un nouveau nom.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="d0dd8-114">[Télécharger](remoteapp-uploadimage.md) ou [importer](remoteapp-image-on-azurevm.md) tooRemoteApp de cette image.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image tooRemoteApp.</span></span>
3. <span data-ttu-id="d0dd8-115">Maintenant, hello collection page, cliquez sur **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-115">Now, on hello collection page, click **Update**.</span></span>
4. <span data-ttu-id="d0dd8-116">Choisissez nouvelle image de hello hello **Image de modèle** liste.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-116">Choose hello new image from hello **Template Image** list.</span></span>
5. <span data-ttu-id="d0dd8-117">Voici une partie difficile de hello - vous devez toodecide comment toodeal avec tous les utilisateurs qui utilisent actuellement une application dans la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-117">Here's hello tricky part - you need toodecide how toodeal with any users that are currently using an app in hello collection.</span></span> <span data-ttu-id="d0dd8-118">Vous avez hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="d0dd8-118">You have hello following choices:</span></span>
   
   * <span data-ttu-id="d0dd8-119">**Donner aux utilisateurs 60 minutes après la mise à jour hello**.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-119">**Give users 60 minutes after hello update**.</span></span> <span data-ttu-id="d0dd8-120">Dès que la mise à jour de hello est terminée, Azure RemoteApp affichera un message tooany active les utilisateurs les invitant à toosave leur travail et le journal désactivé et reconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-120">As soon as hello update is finished, Azure RemoteApp will display a message tooany active users telling them toosave their work and log off and log back in.</span></span> <span data-ttu-id="d0dd8-121">Une fois les 60 minutes écoulées, tous les utilisateurs actifs qui ne se sont pas déconnectés seront automatiquement déconnectés.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="d0dd8-122">Les utilisateurs peuvent se reconnecter immédiatement.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="d0dd8-123">**Déconnecter immédiatement les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-123">**Sign users out immediately**.</span></span> <span data-ttu-id="d0dd8-124">Dès que la mise à jour de hello est terminée, déconnecter tous les utilisateurs automatiquement sans avertissement.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-124">As soon as hello update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="d0dd8-125">Si vous choisissez cette option, les utilisateurs risquent de perdre des données.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="d0dd8-126">Toutefois, ils peuvent se reconnecter toohello application immédiatement.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-126">However, they can reconnect toohello app immediately.</span></span>
6. <span data-ttu-id="d0dd8-127">Cliquez sur mise à jour de hello coche toostart hello.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-127">Click hello check mark toostart hello update.</span></span>

