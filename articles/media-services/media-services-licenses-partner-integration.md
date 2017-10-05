---
title: "Utilisation de partenaires pour fournir des licences Widevine à Azure Media Services | Microsoft Docs"
description: "Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) pour fournir un flux chiffré dynamiquement par AMS avec des DRM PlayReady et Widevine. La licence PlayReady provient du serveur de licences Media Services PlayReady et la licence Widevine est délivrée par le serveur de licences castLabs."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5bcad5a4-c0bb-4871-9cce-808a913c53e6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 6867e4f910970121df3858516c6bab3114c3c6f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="using-partners-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="a0215-104">Utilisation de partenaires pour fournir des licences Widevine à Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="a0215-104">Using partners to deliver Widevine licenses to Azure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="a0215-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a0215-105">Overview</span></span>
<span data-ttu-id="a0215-106">Microsoft Azure Media Services vous permet de diffuser du contenu MPEG-DASH protégé par Widevine DRM, qui est chiffré conformément à la spécification du chiffrement commun (CENC).</span><span class="sxs-lookup"><span data-stu-id="a0215-106">Microsoft Azure Media Services enables you to deliver MPEG-DASH protected with Widevine DRM, which is encrypted per the Common Encryption (CENC) specification.</span></span>

<span data-ttu-id="a0215-107">En commençant par le kit de développement logiciel (SDK) Media Services .NET version 3.5.2, Media Services vous permet de configurer le modèle de licence Widevine et d’obtenir des licences Widevine.</span><span class="sxs-lookup"><span data-stu-id="a0215-107">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="a0215-108">Vous pouvez également utiliser les partenaires AMS suivants pour vous aider à distribuer des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="a0215-108">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

## <a name="castlabs"></a><span data-ttu-id="a0215-109">castLabs</span><span class="sxs-lookup"><span data-stu-id="a0215-109">castLabs</span></span>
<span data-ttu-id="a0215-110">Vous pouvez utiliser [castLabs](http://castlabs.com/company/partners/azure/) pour fournir des licences Widevine.</span><span class="sxs-lookup"><span data-stu-id="a0215-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) to deliver Widevine licenses.</span></span> <span data-ttu-id="a0215-111">Pour plus d’informations, consultez [Utilisation de castLabs pour fournir des licences DRM à Azure Media Services](media-services-castlabs-integration.md)</span><span class="sxs-lookup"><span data-stu-id="a0215-111">For more information, see [Using castLabs to deliver DRM licenses to Azure Media Services](media-services-castlabs-integration.md)</span></span>

## <a name="axinom"></a><span data-ttu-id="a0215-112">Axinom</span><span class="sxs-lookup"><span data-stu-id="a0215-112">Axinom</span></span>
<span data-ttu-id="a0215-113">Vous pouvez utiliser [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) pour fournir des licences Widevine.</span><span class="sxs-lookup"><span data-stu-id="a0215-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) to deliver Widevine licenses.</span></span> <span data-ttu-id="a0215-114">Pour plus d’informations, consultez [Utilisation d’Axinom pour fournir des licences DRM à Azure Media Services](media-services-axinom-integration.md)</span><span class="sxs-lookup"><span data-stu-id="a0215-114">For more information, see [Using Axinom to deliver DRM licenses to Azure Media Services](media-services-axinom-integration.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a0215-115">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="a0215-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a0215-116">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="a0215-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a0215-117">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a0215-117">See also</span></span>
[<span data-ttu-id="a0215-118">Utilisation du chiffrement commun dynamique PlayReady et/ou Widevine</span><span class="sxs-lookup"><span data-stu-id="a0215-118">Using PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="a0215-119">Blog de Mingfei</span><span class="sxs-lookup"><span data-stu-id="a0215-119">Mingfei’s blog</span></span>](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

