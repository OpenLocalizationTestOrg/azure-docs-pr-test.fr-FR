---
title: aaaPublish une application dans Azure RemoteApp | Documents Microsoft
description: "Découvrez comment toopublish applications et ressources dans Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a><span data-ttu-id="31f57-103">Comment toopublish une application de RemoteApp</span><span class="sxs-lookup"><span data-stu-id="31f57-103">How toopublish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="31f57-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="31f57-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="31f57-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="31f57-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="31f57-106">Après avoir créé votre collection RemoteApp, vous devez toopublish hello applications ou les ressources que vous souhaitez toomake disponible pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="31f57-106">After you create your RemoteApp collection, you need toopublish hello apps or resources that you want toomake available for your users.</span></span> <span data-ttu-id="31f57-107">Hello images de modèle fournis avec votre abonnement n’ont quelques applications publiées par défaut - tooshare hello d’autres applications, vous devez toopublish les.</span><span class="sxs-lookup"><span data-stu-id="31f57-107">hello template images provided with your subscription only have a few apps published by default - tooshare hello other apps, you need toopublish them.</span></span>

> [!NOTE]
> <span data-ttu-id="31f57-108">Avez-vous besoin d’une application de tooupdate ?</span><span class="sxs-lookup"><span data-stu-id="31f57-108">Do you need tooupdate an app?</span></span> <span data-ttu-id="31f57-109">Vous devez trop[mise à jour hello image](remoteapp-update.md) première.</span><span class="sxs-lookup"><span data-stu-id="31f57-109">You'll need too[update hello image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="31f57-110">Sur hello **publication** dans le portail de hello, cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="31f57-110">On hello **Publishing** tab in hello portal, click **Publish**.</span></span> <span data-ttu-id="31f57-111">Vous pouvez ajouter une application à partir de votre image de modèle **Démarrer** menu ou fournissez hello chemin d’accès toowhere hello application est installée sur l’image de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="31f57-111">You can either add an app from your template image's **Start** menu or provide hello path toowhere hello app is installed on hello template image.</span></span> <span data-ttu-id="31f57-112">Si vous choisissez tooadd hello **Démarrer** menu, choisissez hello application toopublish à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="31f57-112">If you choose tooadd from hello **Start** menu, choose hello app toopublish from hello list.</span></span> <span data-ttu-id="31f57-113">Si vous choisissez application toohello de tooprovide hello chemin d’accès, entrez un nom pour l’application hello et application de toohello hello chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="31f57-113">If you choose tooprovide hello path toohello app, enter a name for hello app and hello path toohello app.</span></span> <span data-ttu-id="31f57-114">Utiliser des variables dans le chemin d’accès hello - par exemple, « % lecteur_système % » au lieu de « c:\".</span><span class="sxs-lookup"><span data-stu-id="31f57-114">Use variables in hello path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="31f57-115">Si vous souhaitez tooadd votre application à partir de hello **Démarrer** menu, vous devez toohave *ajouté ce toohello application **Démarrer** menu sur votre image de modèle.*</span><span class="sxs-lookup"><span data-stu-id="31f57-115">If you want tooadd your app from hello **Start** menu, you need toohave *added that app toohello **Start** menu on your template image.*</span></span> <span data-ttu-id="31f57-116">Dans le cas contraire, RemoteApp s’affiche uniquement les *est* sur hello **Démarrer** menu et vous ne sera pas.</span><span class="sxs-lookup"><span data-stu-id="31f57-116">Otherwise, RemoteApp will only see what *is* on hello **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="31f57-117">toomake que votre application est Bonjour **Démarrer** menu, placez un fichier de raccourci - **.lnk** : hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs dossier.</span><span class="sxs-lookup"><span data-stu-id="31f57-117">toomake sure your app is in hello **Start** menu, place a shortcut file - **.lnk** - inside hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="31f57-118">Si vous avez oublié tooadd hello application toohello **Démarrer** menu lorsque vous avez créé le modèle de hello, choisissez application toohello de tooadd hello chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="31f57-118">If you forgot tooadd hello app toohello **Start** menu when you created hello template, choose tooadd hello path toohello app.</span></span> <span data-ttu-id="31f57-119">(Ou recréez votre image de modèle, mais c'est un peu plus de travail.)</span><span class="sxs-lookup"><span data-stu-id="31f57-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

