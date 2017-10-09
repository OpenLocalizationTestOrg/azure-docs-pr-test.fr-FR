---
title: aaaDeploy QuickBooks dans Azure RemoteApp | Documents Microsoft
description: "Découvrez comment tooshare QuickBooks avec Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="87deb-103">Comment déployer QuickBooks dans Azure RemoteApp ?</span><span class="sxs-lookup"><span data-stu-id="87deb-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="87deb-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="87deb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="87deb-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="87deb-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="87deb-106">Utilisez hello suivant informations tooshare QuickBooks en tant qu’application dans Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="87deb-106">Use hello following information tooshare QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="87deb-107">Vous pouvez partager QuickBooks 2015 Enterprise avec Azure RemoteApp dans une collection hybride ou de cloud.</span><span class="sxs-lookup"><span data-stu-id="87deb-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="87deb-108">fichier de l’entreprise Hello doit résider sur un ordinateur virtuel qui exécute le serveur de base de données QuickBooks distinct à partir de serveurs d’Azure RemoteApp hello.</span><span class="sxs-lookup"><span data-stu-id="87deb-108">hello company file must reside on a VM that is running QuickBooks database server that is separate from hello Azure RemoteApp servers.</span></span> <span data-ttu-id="87deb-109">Ne stockez jamais de fichier de l’entreprise sur votre image Azure RemoteApp hello - perte de données est attendue cas dans ce.</span><span class="sxs-lookup"><span data-stu-id="87deb-109">Never store hello company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="87deb-110">Seul QuickBooks Enterprise prend en charge un fichier QuickBooks hello hébergement sur un partage externe avec le serveur de base de données QuickBooks accessible via une mise en réseau Windows standard.</span><span class="sxs-lookup"><span data-stu-id="87deb-110">Only QuickBooks Enterprise supports hosting hello QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="87deb-111">Hello QuickBooks de base de données serveur qui héberge le fichier de l’entreprise hello doit résider sur un ordinateur de virtuel distinct au sein de hello même réseau virtuel en tant que hello collection Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="87deb-111">hello QuickBooks database server that is hosting hello company file must reside on a separate VM within hello same VNET as hello Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a><span data-ttu-id="87deb-112">Étapes toodeploy QuickBooks</span><span class="sxs-lookup"><span data-stu-id="87deb-112">Steps toodeploy QuickBooks</span></span>
1. <span data-ttu-id="87deb-113">Créer une machine virtuelle Azure et installer QuickBooks, serveur de base de données QuickBooks et placer le fichier hello entreprise sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="87deb-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place hello company file on a Azure VM.</span></span>  <span data-ttu-id="87deb-114">Assurez-vous que tooproperly configurer des règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="87deb-114">Make sure tooproperly configure firewall rules.</span></span>
2. <span data-ttu-id="87deb-115">Installer QuickBooks sur un [image personnalisée](remoteapp-imageoptions.md) et créer un [collection Azure RemoteApp](remoteapp-collections.md), cloud ou hybride dans hello exactement le même réseau virtuel où la hello machine virtuelle qui héberge hello serveur de base de données QuickBooks avec fichiers d’entreprise réside.</span><span class="sxs-lookup"><span data-stu-id="87deb-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within hello exact same VNET where hello VM hosting hello QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="87deb-116">[Publier](remoteapp-publish.md) QuickBooks application toousers</span><span class="sxs-lookup"><span data-stu-id="87deb-116">[Publish](remoteapp-publish.md) QuickBooks app toousers</span></span>
4. <span data-ttu-id="87deb-117">Lancer le client de QuickBooks d’Azure RemoteApp hébergé hello, accédez à l’aide du réseau du serveur de base de données du QuickBooks de hello hébergement toohello machine virtuelle standard de Windows et ouvrir le fichier de l’entreprise hello.</span><span class="sxs-lookup"><span data-stu-id="87deb-117">Launch hello Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking toohello VM hosting hello QuickBooks database server and open hello company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="87deb-118">Références de documentation</span><span class="sxs-lookup"><span data-stu-id="87deb-118">Documentation references</span></span>
* <span data-ttu-id="87deb-119">QuickBooks - [Configurations prises en charge](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="87deb-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="87deb-120">QuickBooks - [Options de déploiement](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="87deb-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="87deb-121">Vous pouvez également consulter ma présentation Ignite, [notions de base de Microsoft Azure RemoteApp gestion et d’Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -avançons too1:02:45 tooget toohello QuickBooks partie.</span><span class="sxs-lookup"><span data-stu-id="87deb-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward too1:02:45 tooget toohello QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="87deb-122">Architecture de déploiement</span><span class="sxs-lookup"><span data-stu-id="87deb-122">Deployment architecture</span></span>
![Déploiement de QuickBooks + Azure RemoteApp](./media/remoteapp-quickbooks/ra-quickbooks.png)

