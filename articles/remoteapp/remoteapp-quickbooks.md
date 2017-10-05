---
title: "Déploiement de QuickBooks dans Azure RemoteApp | Microsoft Docs"
description: "Découvrez comment partager QuickBooks avec Azure RemoteApp."
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
ms.openlocfilehash: bbfac45220f6ef36c9951daae0ced1974e8ddabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="2e56d-103">Comment déployer QuickBooks dans Azure RemoteApp ?</span><span class="sxs-lookup"><span data-stu-id="2e56d-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2e56d-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="2e56d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="2e56d-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="2e56d-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="2e56d-106">Utilisez les informations suivantes pour partager QuickBooks comme une application dans Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="2e56d-106">Use the following information to share QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="2e56d-107">Vous pouvez partager QuickBooks 2015 Enterprise avec Azure RemoteApp dans une collection hybride ou de cloud.</span><span class="sxs-lookup"><span data-stu-id="2e56d-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="2e56d-108">Le fichier d’entreprise doit résider sur une machine virtuelle qui exécute un serveur de base de données QuickBooks distinct des serveurs Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="2e56d-108">The company file must reside on a VM that is running QuickBooks database server that is separate from the Azure RemoteApp servers.</span></span> <span data-ttu-id="2e56d-109">Ne stockez jamais le fichier d'entreprise sur votre image Azure RemoteApp car vous risquez de perte des données.</span><span class="sxs-lookup"><span data-stu-id="2e56d-109">Never store the company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="2e56d-110">Seul QuickBooks Enterprise prend en charge l’hébergement du fichier QuickBooks sur un partage externe avec le serveur de base de données QuickBooks accessible via des réseaux Windows standard.</span><span class="sxs-lookup"><span data-stu-id="2e56d-110">Only QuickBooks Enterprise supports hosting the QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="2e56d-111">Le serveur de base de données QuickBooks qui héberge le fichier d’entreprise doit résider sur une machine virtuelle distincte située sur le même réseau virtuel que la collection Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="2e56d-111">The QuickBooks database server that is hosting the company file must reside on a separate VM within the same VNET as the Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-to-deploy-quickbooks"></a><span data-ttu-id="2e56d-112">Étapes pour déployer QuickBooks</span><span class="sxs-lookup"><span data-stu-id="2e56d-112">Steps to deploy QuickBooks</span></span>
1. <span data-ttu-id="2e56d-113">Créez une machine virtuelle Azure et installez QuickBooks, le serveur de base de données QuickBooks, puis placez le fichier d'entreprise sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="2e56d-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place the company file on a Azure VM.</span></span>  <span data-ttu-id="2e56d-114">Veillez à configurer correctement les règles du pare-feu.</span><span class="sxs-lookup"><span data-stu-id="2e56d-114">Make sure to properly configure firewall rules.</span></span>
2. <span data-ttu-id="2e56d-115">Installez QuickBooks sur une [image personnalisée](remoteapp-imageoptions.md) et créez une [collection Azure RemoteApp](remoteapp-collections.md) de cloud ou hybride au sein du même réseau virtuel où réside la machine virtuelle qui héberge le serveur de base de données QuickBooks contenant des fichiers d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="2e56d-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within the exact same VNET where the VM hosting the QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="2e56d-116">[Publication](remoteapp-publish.md) d’une application QuickBooks aux utilisateurs</span><span class="sxs-lookup"><span data-stu-id="2e56d-116">[Publish](remoteapp-publish.md) QuickBooks app to users</span></span>
4. <span data-ttu-id="2e56d-117">Lancez le client QuickBooks hébergé sur Azure RemoteApp, naviguez à l'aide d'une mise en réseau Windows standard vers la machine virtuelle qui héberge le serveur de base de données QuickBooks, puis ouvrez le fichier d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="2e56d-117">Launch the Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking to the VM hosting the QuickBooks database server and open the company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="2e56d-118">Références de documentation</span><span class="sxs-lookup"><span data-stu-id="2e56d-118">Documentation references</span></span>
* <span data-ttu-id="2e56d-119">QuickBooks - [Configurations prises en charge](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="2e56d-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="2e56d-120">QuickBooks - [Options de déploiement](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="2e56d-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="2e56d-121">Vous pouvez également consulter ma présentation Ignite, [Bases de la gestion et de l’administration de Microsoft Azure RemoteApp](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) en avançant rapidement jusqu’à 1:02:45 pour accéder à la partie QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="2e56d-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward to 1:02:45 to get to the QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="2e56d-122">Architecture de déploiement</span><span class="sxs-lookup"><span data-stu-id="2e56d-122">Deployment architecture</span></span>
![Déploiement de QuickBooks + Azure RemoteApp](./media/remoteapp-quickbooks/ra-quickbooks.png)

