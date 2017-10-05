---
title: "Créer une image Azure RemoteApp | Microsoft Docs"
description: "En savoir plus sur les options disponibles pour la création d’images pour Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 4b8ba6f264f982e03930c5ad4ccdb2d80f2c8665
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="cc1dd-103">Création d’une image Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cc1dd-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cc1dd-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cc1dd-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="cc1dd-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cc1dd-106">Azure RemoteApp utilise des images pour conserver les applications que vous partagez avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-106">Azure RemoteApp uses images to hold the apps that you share with your users.</span></span> <span data-ttu-id="cc1dd-107">(Nous prenons votre image et nous l’utilisons pour créer des machines virtuelles auxquelles les utilisateurs accéderont lorsqu’ils se connecteront à Azure RemoteApp.) Pour créer une collection Azure RemoteApp avec un choix d’applications, de type cloud ou hybride, commencez par créer une image à partir des applications installées.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-107">(We take your image and use it to create VMs - that's what the users access when they sign into Azure RemoteApp.) To create an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="cc1dd-108">Créez ensuite une collection utilisant cette image, affectez des utilisateurs à la collection et publiez des applications pour ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-108">Then, create a collection that uses that image, assign users to the collection, and publish apps to those users.</span></span>

<span data-ttu-id="cc1dd-109">Plusieurs choix s’offrent à vous pour créer ou utiliser des images.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-109">You have several options for creating or using images.</span></span> <span data-ttu-id="cc1dd-110">L’exécution de Windows Server 2012 R2 et l’installation du rôle Hôte de session Bureau à distance (RDSH) constituent les [exigences](remoteapp-imagereqs.md) de base pour le fonctionnement d’une image.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-110">The basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have the Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="cc1dd-111">La procédure commence à devenir intéressante au moment de choisir le mode de configuration.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="cc1dd-112">Dans le cas des images, vous disposez des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc1dd-112">You have the following options when it comes to images:</span></span>

* <span data-ttu-id="cc1dd-113">Vous pouvez importer et utiliser une [image basée sur une machine virtuelle Azure](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="cc1dd-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="cc1dd-114">Cette fonction est utile pour les applications cœur de métier nécessitant des paramètres personnalisés.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="cc1dd-115">Vous pouvez personnaliser l’image à utiliser pour l’application.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-115">You can customize the image to work for the app.</span></span>
* <span data-ttu-id="cc1dd-116">Vous pouvez [créer et charger une image personnalisée](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="cc1dd-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="cc1dd-117">Cette fonction est utile si vous disposez déjà d’une image que vous utilisez pour le déploiement local de vos services Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="cc1dd-118">Vous pouvez utiliser l’une des [images de modèle](remoteapp-images.md) incluses dans votre abonnement RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-118">You can use one of the [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="cc1dd-119">Ces images sont créées et gérées par l’équipe RemoteApp et contiennent certaines applications standard (telles que la suite Office) que vous pouvez mettre à la disposition de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-119">These images are created and maintained by the RemoteApp team and contain some standard applications (like the Office suite) that you can make available to your users.</span></span> <span data-ttu-id="cc1dd-120">Notez que seule l’image d’Office 365 Pro Plus peut être utilisée dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-120">Note that only the Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="cc1dd-121">Quel que soit le mode de création ou la provenance de votre image, vérifiez que vous comprenez les [exigences de l’application](remoteapp-appreqs.md) afin de vous assurer que celle-ci fonctionne dans RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cc1dd-121">Regardless of where you get your image or how you create it, you'll want to make sure you understand the [app requirements](remoteapp-appreqs.md) to ensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="cc1dd-122">L’étape suivante consiste à créer une collection [cloud](remoteapp-create-cloud-deployment.md) ou [hybride](remoteapp-create-hybrid-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="cc1dd-122">Then, the next step is to create a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

