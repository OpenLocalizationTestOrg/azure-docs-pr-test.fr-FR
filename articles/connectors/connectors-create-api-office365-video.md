---
title: "Utiliser le connecteur Office 365 Video dans vos applications logiques | Microsoft Docs"
description: "Utiliser le connecteur Office 365 Video dans vos applications logiques Microsoft Azure App Service"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 738e5aa7-2523-4116-8b65-211b9063852d
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: f0e3613d4a3fd5478787c0365eb7a0bcde886c81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office365-video-connector"></a><span data-ttu-id="97a56-103">Prise en main du connecteur Office 365 Video</span><span class="sxs-lookup"><span data-stu-id="97a56-103">Get started with the Office365 Video connector</span></span>
<span data-ttu-id="97a56-104">Connexion à Office 365 Video pour obtenir des informations sur une vidéo Office 365, la liste des vidéos, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="97a56-104">Connect to Office 365 Video to get information about an Office 365 video, get a list of videos, and more.</span></span> <span data-ttu-id="97a56-105">Avec Office 365 Video, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="97a56-105">With Office 365 Video, you can:</span></span>

* <span data-ttu-id="97a56-106">Créer votre flux d’activité en fonction des données que vous obtenez d’Office 365 Video.</span><span class="sxs-lookup"><span data-stu-id="97a56-106">Build your business flow based on the data you get from Office 365 Video.</span></span> 
* <span data-ttu-id="97a56-107">Utiliser des actions pour vérifier l’état du portail vidéo, obtenir une liste de toutes les vidéos dans un canal, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="97a56-107">Use actions that check the video portal status, get a list of all video in a channel, and more.</span></span> <span data-ttu-id="97a56-108">Ces actions obtiennent une réponse, puis mettent la sortie à la disposition d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="97a56-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="97a56-109">Vous pouvez, par exemple, utiliser le connecteur Bing Search pour rechercher des vidéos Office 365, puis utiliser le connecteur Office 365 Video pour obtenir des informations sur ces vidéos.</span><span class="sxs-lookup"><span data-stu-id="97a56-109">For example, you can use the Bing Search connector to search for Office 365 videos, and then use the Office 365 video connector to get information about that video.</span></span> <span data-ttu-id="97a56-110">Si la vidéo répond à vos besoins, vous pouvez la publier sur Facebook.</span><span class="sxs-lookup"><span data-stu-id="97a56-110">If the video meets your requirements, you can post this video on Facebook.</span></span> 

<span data-ttu-id="97a56-111">Vous pouvez commencer par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="97a56-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office365-video-connector"></a><span data-ttu-id="97a56-112">Créer une connexion au connecteur Office 365 Video</span><span class="sxs-lookup"><span data-stu-id="97a56-112">Create a connection to Office365 Video connector</span></span>
<span data-ttu-id="97a56-113">Quand vous ajoutez ce connecteur à vos applications logiques, vous devez vous connecter à votre compte Office 365 Video et autoriser les applications logiques à se connecter à votre compte.</span><span class="sxs-lookup"><span data-stu-id="97a56-113">When you add this connector to your logic apps, you must sign-in to your Office 365 Video account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Video](../../includes/connectors-create-api-office365video.md)]
> 
> 

<span data-ttu-id="97a56-114">Après avoir créé la connexion, vous entrez les propriétés Office 365 Video, comme le nom du client ou l’ID du canal.</span><span class="sxs-lookup"><span data-stu-id="97a56-114">After you create the connection, you enter the Office 365 video properties, like the tenant name or channel ID.</span></span> 


## <a name="connector-specific-details"></a><span data-ttu-id="97a56-115">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="97a56-115">Connector-specific details</span></span>

<span data-ttu-id="97a56-116">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/office365videoconnector/).</span><span class="sxs-lookup"><span data-stu-id="97a56-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365videoconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="97a56-117">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="97a56-117">More connectors</span></span>
<span data-ttu-id="97a56-118">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="97a56-118">Go back to the [APIs list](apis-list.md).</span></span>