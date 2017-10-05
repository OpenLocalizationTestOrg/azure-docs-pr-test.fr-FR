---
title: Publier une application dans Azure RemoteApp | Microsoft Docs
description: "Découvrez comment publier des applications et des ressources dans Azure RemoteApp."
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
ms.openlocfilehash: 4565fa498dbadd0601004c73bfee5171efe1fad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-publish-an-app-in-remoteapp"></a><span data-ttu-id="419b9-103">Publication d'une application dans RemoteApp</span><span class="sxs-lookup"><span data-stu-id="419b9-103">How to publish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="419b9-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="419b9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="419b9-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="419b9-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="419b9-106">Après avoir créé votre collection RemoteApp, vous devez publier les applications ou les ressources que vous souhaitez rendre disponibles pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="419b9-106">After you create your RemoteApp collection, you need to publish the apps or resources that you want to make available for your users.</span></span> <span data-ttu-id="419b9-107">Les images de modèle fournies avec votre abonnement ne contiennent que certaines applications publiées par défaut. Pour partager d’autres applications, vous devez les publier.</span><span class="sxs-lookup"><span data-stu-id="419b9-107">The template images provided with your subscription only have a few apps published by default - to share the other apps, you need to publish them.</span></span>

> [!NOTE]
> <span data-ttu-id="419b9-108">Vous devez mettre à jour une application ?</span><span class="sxs-lookup"><span data-stu-id="419b9-108">Do you need to update an app?</span></span> <span data-ttu-id="419b9-109">Il vous faut d’abord [mettre à jour l’image](remoteapp-update.md) .</span><span class="sxs-lookup"><span data-stu-id="419b9-109">You'll need to [update the image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="419b9-110">Sous l'onglet **Publication** du portail, cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="419b9-110">On the **Publishing** tab in the portal, click **Publish**.</span></span> <span data-ttu-id="419b9-111">Vous pouvez ajouter une application à partir du menu **Démarrer** de votre image de modèle ou indiquer le chemin d'accès de son répertoire d'installation dans l'image de modèle.</span><span class="sxs-lookup"><span data-stu-id="419b9-111">You can either add an app from your template image's **Start** menu or provide the path to where the app is installed on the template image.</span></span> <span data-ttu-id="419b9-112">Si vous choisissez d’ajouter une application à partir du menu **Démarrer** , sélectionnez l’application à publier dans la liste.</span><span class="sxs-lookup"><span data-stu-id="419b9-112">If you choose to add from the **Start** menu, choose the app to publish from the list.</span></span> <span data-ttu-id="419b9-113">Si vous choisissez d'indiquer le chemin d'accès à l'application, entrez un nom pour l'application et son chemin d'accès.</span><span class="sxs-lookup"><span data-stu-id="419b9-113">If you choose to provide the path to the app, enter a name for the app and the path to the app.</span></span> <span data-ttu-id="419b9-114">Utilisez des variables dans le chemin d'accès, par exemple, « %lecteur_système% » au lieu de "c: \".</span><span class="sxs-lookup"><span data-stu-id="419b9-114">Use variables in the path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="419b9-115">Si vous voulez ajouter votre application à partir du menu **Démarrer**, cette *application doit être ajoutée au menu **Démarrer** sur votre image de modèle.*</span><span class="sxs-lookup"><span data-stu-id="419b9-115">If you want to add your app from the **Start** menu, you need to have *added that app to the **Start** menu on your template image.*</span></span> <span data-ttu-id="419b9-116">Sinon, RemoteApp ne voit que ce qui *figure* dans le menu **Démarrer** et cela peut prêter à confusion.</span><span class="sxs-lookup"><span data-stu-id="419b9-116">Otherwise, RemoteApp will only see what *is* on the **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="419b9-117">Pour vous assurer que votre application figure dans le menu **Démarrer**, placez un fichier de raccourci **.lnk** dans le dossier %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs.</span><span class="sxs-lookup"><span data-stu-id="419b9-117">To make sure your app is in the **Start** menu, place a shortcut file - **.lnk** - inside the %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="419b9-118">Si vous avez oublié d'ajouter l'application au menu **Démarrer** au moment de la création du modèle, choisissez d'ajouter le chemin d'accès à l'application.</span><span class="sxs-lookup"><span data-stu-id="419b9-118">If you forgot to add the app to the **Start** menu when you created the template, choose to add the path to the app.</span></span> <span data-ttu-id="419b9-119">(Ou recréez votre image de modèle, mais c'est un peu plus de travail.)</span><span class="sxs-lookup"><span data-stu-id="419b9-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

