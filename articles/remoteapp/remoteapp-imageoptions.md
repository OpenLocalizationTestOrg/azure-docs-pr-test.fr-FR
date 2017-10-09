---
title: aaaCreate une image Azure RemoteApp | Documents Microsoft
description: "En savoir plus sur les options de hello disponibles pour la création d’images pour Azure RemoteApp"
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
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="e4a3a-103">Création d’une image Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e4a3a-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e4a3a-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e4a3a-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e4a3a-106">Azure RemoteApp utilise des images toohold hello applications que vous partagez avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-106">Azure RemoteApp uses images toohold hello apps that you share with your users.</span></span> <span data-ttu-id="e4a3a-107">(Nous prendre votre image et l’utiliser machines virtuelles toocreate - ce que les utilisateurs de hello accèdent quand ils se connectent à Azure RemoteApp.) toocreate une collection Azure RemoteApp avec un choix d’applications, qu’il s’agisse de cloud ou hybride, vous commencez par créer une image avec les applications installées.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-107">(We take your image and use it toocreate VMs - that's what hello users access when they sign into Azure RemoteApp.) toocreate an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="e4a3a-108">Ensuite, créez un regroupement qui utilise cette image, affecter des utilisateurs toohello collection et publier des utilisateurs de toothose d’applications.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-108">Then, create a collection that uses that image, assign users toohello collection, and publish apps toothose users.</span></span>

<span data-ttu-id="e4a3a-109">Plusieurs choix s’offrent à vous pour créer ou utiliser des images.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-109">You have several options for creating or using images.</span></span> <span data-ttu-id="e4a3a-110">Hello base [exigence](remoteapp-imagereqs.md) pour une image est qu’il exécutent Windows Server 2012 R2 et hello hôte de Session de bureau à distance (RDSH) rôle est installé.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-110">hello basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have hello Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="e4a3a-111">La procédure commence à devenir intéressante au moment de choisir le mode de configuration.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="e4a3a-112">Vous avez hello options suivantes lorsqu’il s’agit de tooimages :</span><span class="sxs-lookup"><span data-stu-id="e4a3a-112">You have hello following options when it comes tooimages:</span></span>

* <span data-ttu-id="e4a3a-113">Vous pouvez importer et utiliser une [image basée sur une machine virtuelle Azure](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="e4a3a-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="e4a3a-114">Cette fonction est utile pour les applications cœur de métier nécessitant des paramètres personnalisés.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="e4a3a-115">Vous pouvez personnaliser toowork d’image hello pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-115">You can customize hello image toowork for hello app.</span></span>
* <span data-ttu-id="e4a3a-116">Vous pouvez [créer et charger une image personnalisée](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="e4a3a-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="e4a3a-117">Cette fonction est utile si vous disposez déjà d’une image que vous utilisez pour le déploiement local de vos services Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="e4a3a-118">Vous pouvez utiliser une des hello [images de modèle](remoteapp-images.md) inclus dans votre abonnement RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-118">You can use one of hello [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="e4a3a-119">Ces images sont créées et gérées par l’équipe de RemoteApp hello et contiennent certaines applications standards (par exemple hello Office suite) que vous pouvez créer des utilisateurs de tooyour disponibles.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-119">These images are created and maintained by hello RemoteApp team and contain some standard applications (like hello Office suite) that you can make available tooyour users.</span></span> <span data-ttu-id="e4a3a-120">Notez que cette image d’Office 365 Pro Plus hello uniquement peut être utilisée dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-120">Note that only hello Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="e4a3a-121">Quelle que soit l’où vous avez obtenu votre image ou comment vous la créez, vous souhaiterez toomake que vous comprenez hello [spécifications des applications](remoteapp-appreqs.md) tooensure votre application fonctionne correctement dans RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-121">Regardless of where you get your image or how you create it, you'll want toomake sure you understand hello [app requirements](remoteapp-appreqs.md) tooensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="e4a3a-122">Ensuite, la prochaine étape de hello est toocreate un [cloud](remoteapp-create-cloud-deployment.md) ou [hybride](remoteapp-create-hybrid-deployment.md) collection.</span><span class="sxs-lookup"><span data-stu-id="e4a3a-122">Then, hello next step is toocreate a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

