---
title: "Options de migration hors d’Azure RemoteApp | Microsoft Docs"
description: "Découvrez les options de migration hors d’Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9ab63124e2521ee1922d15c1e388c54d50eb8301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="93ba3-103">Options de migration hors d’Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="93ba3-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="93ba3-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="93ba3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="93ba3-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="93ba3-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="93ba3-106">Si vous avez cessé d’utiliser RemoteApp du fait de [l’annonce de la suppression](https://go.microsoft.com/fwlink/?linkid=821148) ou parce que vous avez terminé votre évaluation, vous devez migrer d’Azure RemoteApp vers un autre service d’application.</span><span class="sxs-lookup"><span data-stu-id="93ba3-106">If you have stopped using Azure RemoteApp because of the [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need to migrate off of Azure RemoteApp to another app service.</span></span> <span data-ttu-id="93ba3-107">Il existe deux approches différentes pour la migration : le déploiement autogéré (souvent appelé Infrastructure en tant que Service [IaaS]) ou une offre de plateforme entièrement gérée (souvent appelée Plateforme ou Logiciel en tant que service [PaaS/SaaS]).</span><span class="sxs-lookup"><span data-stu-id="93ba3-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="93ba3-108">L’IaaS en libre-service est un déploiement personnalisable que vous gérez, exploitez et possédez, directement déployé sur des machines virtuelles (VM) ou des systèmes physiques.</span><span class="sxs-lookup"><span data-stu-id="93ba3-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="93ba3-109">En face, une offre de PaaS/SaaS entièrement géré ressemble davantage à Azure RemoteApp : un partenaire fournit une couche de service sur une solution d’accès distant qui gère les opérations et la maintenance, pendant que vous, en tant que client, effectuez la gestion des images et applications.</span><span class="sxs-lookup"><span data-stu-id="93ba3-109">At the other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as the customer, do some image and app management.</span></span>

<span data-ttu-id="93ba3-110">[Consultez les webinaires Azure RemoteApp sur les options de migration](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), ou lisez la suite pour plus d’informations (y compris des exemples des différentes options d’hébergement).</span><span class="sxs-lookup"><span data-stu-id="93ba3-110">[View the Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of the different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="93ba3-111">Solutions autogérées (IaaS)</span><span class="sxs-lookup"><span data-stu-id="93ba3-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="93ba3-112">**RDS sur IaaS**</span><span class="sxs-lookup"><span data-stu-id="93ba3-112">**RDS on IaaS**</span></span>
<span data-ttu-id="93ba3-113">Vous pouvez déployer un déploiement de services Bureau à distance natif basé sur les sessions (dans Windows Server) à l’aide de RemoteApp sur des postes de travail locaux ou dans un environnement hébergé (comme sur les machines virtuelles Azure).</span><span class="sxs-lookup"><span data-stu-id="93ba3-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="93ba3-114">Les services Bureau à Distance sur les déploiements IaaS sont parfaits pour les clients déjà familiarisés avec cette solution et qui ont une expertise technique existante pour les déploiements de services Bureau à Distance.</span><span class="sxs-lookup"><span data-stu-id="93ba3-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="93ba3-115">Vous avez besoin de licences en volume avec Software Assurance (SA) pour les licences d’accès client aux services Bureau à distance pour utiliser cette option de déploiement.</span><span class="sxs-lookup"><span data-stu-id="93ba3-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses to use this deployment option.</span></span>

<span data-ttu-id="93ba3-116">Le déploiement des services Bureau à Distance sur des machines virtuelles Azure est plus facile que jamais lorsque vous utilisez le déploiement et des modèles d’application de correctifs (lisez la [présentation](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) puis [récupérez-les](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="93ba3-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="93ba3-117">Vous pouvez obtenir les mêmes fonctionnalités de mise à l’échelle flexibles avec des ressources de modèle de déploiement Azure Classic (et non des ressources de modèle de ressource Azure) dans Azure RemoteApp à l’aide du [script de mise à l’échelle automatique](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), bien qu’il existe davantage de personnalisations et de configurations.</span><span class="sxs-lookup"><span data-stu-id="93ba3-117">You can get the same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using the [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="93ba3-118">Lorsque vous déployez des services Bureau à Distance sur des machines virtuelles Azure, le support technique est fourni via le [Support Azure](https://azure.microsoft.com/support/plans/), les mêmes professionnels d’assistance technique qui vous ont assisté avec Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="93ba3-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), the same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="93ba3-119">Vous pouvez obtenir des estimations de coût en fonction de votre utilisation existante en contactant le [Support Azure](https://azure.microsoft.com/support/plans/), ou vous pouvez effectuer les calculs vous-même à l’aide de notre calculateur de coûts à venir.</span><span class="sxs-lookup"><span data-stu-id="93ba3-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon to be released Cost Calculator.</span></span>  <span data-ttu-id="93ba3-120">En outre, avec les machines virtuelles de série N (actuellement en version préliminaire privée), vous pouvez ajouter des vGPU - Pour plus d’informations sur l’ajout de vGPU et sur la [prise en main des améliorations des services de Bureau à distance dans Windows Server 2016](https://myignite.microsoft.com/videos/2794), consultez notre session Ignite.</span><span class="sxs-lookup"><span data-stu-id="93ba3-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how to [harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="93ba3-121">Nous proposons des guides de déploiement étape par étape pour [Windows Server 2012 R2](http://aka.ms/rdsonazure) et [Windows Server 2016](http://aka.ms/rdsonazure2016) afin de faciliter votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="93ba3-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) to assist with your deployment.</span></span> <span data-ttu-id="93ba3-122">Consultez le [blog du Bureau à distance](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) pour les dernières informations.</span><span class="sxs-lookup"><span data-stu-id="93ba3-122">Check out the [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for the latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="93ba3-123">**Citrix sur IaaS**</span><span class="sxs-lookup"><span data-stu-id="93ba3-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="93ba3-124">Un déploiement Citrix natif de XenApp ou de XenDesktop basé sur les sessions peut être déployé localement ou dans un environnement hébergé (par exemple sur des machines virtuelles Azure).</span><span class="sxs-lookup"><span data-stu-id="93ba3-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="93ba3-125">Consultez le guide de déploiement étape par étape, [Citrix XA 7.6 sur Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="93ba3-125">Check out the step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="93ba3-126">En savoir plus sur [Citrix sur Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), avec notamment un calculateur de prix.</span><span class="sxs-lookup"><span data-stu-id="93ba3-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="93ba3-127">Vous pouvez également rechercher un [contact Citrix](http://citrix.com/English/contact/index.asp) pour discuter de vos options.</span><span class="sxs-lookup"><span data-stu-id="93ba3-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) to discuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="93ba3-128">Offres entièrement gérés (PaaS/SaaS)</span><span class="sxs-lookup"><span data-stu-id="93ba3-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="93ba3-129">Citrix XenApp Essentials (parution : avril 2017)</span><span class="sxs-lookup"><span data-stu-id="93ba3-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="93ba3-130">Désormais disponible sur la [Place de marché Azure](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials est un nouveau service de virtualisation d’application. Il associe la puissance et la flexibilité de la plateforme Citrix Cloud à la vision simple, normative et facile à utiliser de Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="93ba3-130">Available now on the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is the new application virtualization service, combining the power and flexibility of the Citrix Cloud platform with the simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="93ba3-131">Les clients Azure RemoteApp existants peuvent [s’inscrire pour profiter d’une version d’évaluation gratuite](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="93ba3-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="93ba3-132">Remarque : seul le service utilisateur Citrix est gratuit. Calcul Azure et Stockage Azure sont payants.</span><span class="sxs-lookup"><span data-stu-id="93ba3-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="93ba3-133">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="93ba3-133">Learn More:</span></span>
- [<span data-ttu-id="93ba3-134">Migrer d’Azure RemoteApp vers Citrix XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="93ba3-134">Migrate from Azure RemoteApp to Citrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="93ba3-135">Citrix et Microsoft</span><span class="sxs-lookup"><span data-stu-id="93ba3-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="93ba3-136">[Présentation de Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k)</span><span class="sxs-lookup"><span data-stu-id="93ba3-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="93ba3-137">Services Citrix Cloud XenApp et XenDesktop</span><span class="sxs-lookup"><span data-stu-id="93ba3-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="93ba3-138">Le [service Citrix Cloud XenApp et XenDesktop](https://www.citrix.com/products/citrix-cloud/services.html) est la solution optimale pour la prestation d’applications et de postes de travail, ainsi que pour les capacités avancées de gestion et de supervision.</span><span class="sxs-lookup"><span data-stu-id="93ba3-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is the best solution for the delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="93ba3-139">Conexlink (nom de la plateforme : MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="93ba3-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="93ba3-140">[MyCloudIT](https://mycloudit.com) est une plateforme d’automatisation pour les entreprises informatiques qui souhaitent simplifier, optimiser et mettre à l’échelle la migration et la livraison de bureaux à distance, d’applications à distance et d’infrastructures dans le cloud Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="93ba3-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies to simplify, optimize, and scale the migration and delivery of remote desktops, remote applications, and infrastructure in the Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="93ba3-141">La plateforme MyCloudIT réduit le temps nécessaire au déploiement de 95 %, les coûts liés à Azure de 30 %, et déplace l’infrastructure informatique entière des clients dans le cloud en quelques clics.</span><span class="sxs-lookup"><span data-stu-id="93ba3-141">The MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into the cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="93ba3-142">Les partenaires peuvent désormais gérer les clients à partir d’un tableau de bord global, les utilisateurs finaux de service à travers le monde entier comme jamais auparavant et augmenter leur chiffre d’affaires sans ajouter de surcharge supplémentaire ou nécessiter de formation approfondie à Azure.</span><span class="sxs-lookup"><span data-stu-id="93ba3-142">Partners can now manage customers from one global dashboard, service end users around the world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="93ba3-143">Emplacement principal : Dallas, Texas, États-Unis</span><span class="sxs-lookup"><span data-stu-id="93ba3-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="93ba3-144">Région de l’opération  : monde entier</span><span class="sxs-lookup"><span data-stu-id="93ba3-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="93ba3-145">Statut du partenaire : [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="93ba3-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="93ba3-146">Fournisseur de services Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="93ba3-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="93ba3-147">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="93ba3-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="93ba3-148">Solutions de migration Azure RemoteApp : Oui, [en savoir plus](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="93ba3-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="93ba3-149">Brian Garoutte, vice-président du développement commercial</span><span class="sxs-lookup"><span data-stu-id="93ba3-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="93ba3-150">Téléphone : 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="93ba3-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="93ba3-151">E-mail : [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="93ba3-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="93ba3-152">Frame</span><span class="sxs-lookup"><span data-stu-id="93ba3-152">Frame</span></span>

<span data-ttu-id="93ba3-153">Les organisations informatiques des entreprises et du gouvernement, les fournisseurs de services gérés et les principaux éditeurs de logiciels choisissent Frame pour créer et gérer leurs espaces de travail sécurisés et à définition logicielle dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="93ba3-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame to create and manage their secure, software-defined workspaces in the cloud.</span></span> <span data-ttu-id="93ba3-154">Des petites aux grandes entreprises, Frame facilite considérablement l’accès aux applications Windows pour les utilisateurs, sur n’importe quel navigateur et n’importe quel appareil.</span><span class="sxs-lookup"><span data-stu-id="93ba3-154">From small to large organizations, Frame makes it incredibly easy to let users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="93ba3-155">La plateforme Frame comprend tout ce dont un administrateur a besoin pour déployer des applications à partir du cloud, notamment l’infrastructure Azure et les licences des services Bureau à distance (il est facultatif d’apporter son propre compte Azure et ses propres licences).</span><span class="sxs-lookup"><span data-stu-id="93ba3-155">The Frame platform includes everything an admin needs to deploy applications from the cloud including the Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="93ba3-156">En savoir plus sur [Frame sur Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="93ba3-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="93ba3-157">Emplacement principal : San Mateo, CA, États-Unis</span><span class="sxs-lookup"><span data-stu-id="93ba3-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="93ba3-158">Région de l’opération  : monde entier</span><span class="sxs-lookup"><span data-stu-id="93ba3-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="93ba3-159">Partenaire Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="93ba3-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="93ba3-160">Téléphone : 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="93ba3-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="93ba3-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="93ba3-161">Awingu</span></span>
<span data-ttu-id="93ba3-162">Awingu fournit une solution simple d’espace de travail en ligne qui exécute des applications héritées, SaaS et des documents à partir d’un navigateur html5.</span><span class="sxs-lookup"><span data-stu-id="93ba3-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="93ba3-163">Ainsi, les applications sont disponibles en toute sécurité, sur tous les types d’appareils.</span><span class="sxs-lookup"><span data-stu-id="93ba3-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="93ba3-164">Pour les services SaaS, un large éventail d’options d’authentification unique (SSO) est disponible.</span><span class="sxs-lookup"><span data-stu-id="93ba3-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="93ba3-165">De plus, plusieurs systèmes de fichiers (cloud) peuvent être profondément intégrés dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="93ba3-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="93ba3-166">En plus d’une mobilité totale, l’espace de travail en ligne riche d’Awingu offre un niveau de sécurité optimal avec des contrôles granulaires (par exemple, téléchargement / chargement), audit d’utilisation complet, Multi-Factor Authentication (par exemple, Azure MFA), enregistrement de session et bien plus.</span><span class="sxs-lookup"><span data-stu-id="93ba3-166">Next to full mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="93ba3-167">Solution originale, Awingu permet le partage de session d’application et de document pour une collaboration sûre et optimisée.</span><span class="sxs-lookup"><span data-stu-id="93ba3-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="93ba3-168">Awingu est une solution d’API ouverte, multi-AD et mutualisée.</span><span class="sxs-lookup"><span data-stu-id="93ba3-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="93ba3-169">Elle est utilisée par les petites et grandes entreprises, fournisseurs de services Cloud et les [ISV](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="93ba3-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="93ba3-170">Ces clients apprécieront particulièrement sa simplicité d’utilisation et d’installation et les faibles coûts de possession.</span><span class="sxs-lookup"><span data-stu-id="93ba3-170">These customers especially appreciate the easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="93ba3-171">Awingu All-in-One est [disponible dans Place de marché Azure](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) avec 2 utilisateurs simultanés intégrés.</span><span class="sxs-lookup"><span data-stu-id="93ba3-171">Awingu All-in-One is [available in the Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="93ba3-172">Des licences supplémentaires sont disponibles via un [large éventail de distributeurs et revendeurs](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="93ba3-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="93ba3-173">En savoir plus sur [Awingu comme alternative à Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="93ba3-173">Learn more about [Awingu on as alternative to Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="93ba3-174">Emplacement principal : Belgique</span><span class="sxs-lookup"><span data-stu-id="93ba3-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="93ba3-175">Régions opérationnelles : EMEA, Amérique du Nord et Brésil</span><span class="sxs-lookup"><span data-stu-id="93ba3-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="93ba3-176">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="93ba3-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="93ba3-177">**Mondial** :</span><span class="sxs-lookup"><span data-stu-id="93ba3-177">**Global**:</span></span>
> 
> <span data-ttu-id="93ba3-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="93ba3-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="93ba3-179">E-mail : [arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="93ba3-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="93ba3-180">Téléphone : +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="93ba3-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="93ba3-181">**Siège en Belgique** :</span><span class="sxs-lookup"><span data-stu-id="93ba3-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="93ba3-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="93ba3-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="93ba3-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="93ba3-183">9000 Gent</span></span>
> 
> <span data-ttu-id="93ba3-184">E-mail : [info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="93ba3-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="93ba3-185">Téléphone : +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="93ba3-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="93ba3-186">**États-Unis** :</span><span class="sxs-lookup"><span data-stu-id="93ba3-186">**USA**:</span></span>
> 
> <span data-ttu-id="93ba3-187">7th floor, 1177 Ave of the Americas,</span><span class="sxs-lookup"><span data-stu-id="93ba3-187">7th floor, 1177 Ave of the Americas,</span></span>
> 
> <span data-ttu-id="93ba3-188">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="93ba3-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="93ba3-189">E-mail : [info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="93ba3-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="93ba3-190">Fournisseur de services hébergés Microsoft</span><span class="sxs-lookup"><span data-stu-id="93ba3-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="93ba3-191">Les partenaires d’hébergement offrent généralement un service hébergé entièrement géré de service d’application et bureau Windows, ce qui peut inclure la gestion des ressources Azure, des systèmes d’exploitation, des applications et du support technique en fonction des contrats de licence du partenaire avec Microsoft et d’autres fournisseurs de logiciels, ainsi qu’un contrat de licence de fournisseur de services pour permettre la revente de la licence d’accès SAL.</span><span class="sxs-lookup"><span data-stu-id="93ba3-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing the Azure resources, operating systems, applications, and helpdesk using the partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement to allow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="93ba3-192">Les informations suivantes fournissent des détails et des informations de contact pour certains des hébergeurs spécialisés dans l’assistance aux clients pour leur migration Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="93ba3-192">The following information provides details and contact information for some of the hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="93ba3-193">Découvrez [la liste actuelle des fournisseurs de services hébergés](http://aka.ms/rdsonazurecertified) qui ont effectué le parcours d’apprentissage et l’évaluation de RDS sur IaaS.</span><span class="sxs-lookup"><span data-stu-id="93ba3-193">Check out [the current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed the RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="93ba3-194">Programme de fournisseur de services de Citrix</span><span class="sxs-lookup"><span data-stu-id="93ba3-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="93ba3-195">Le programme de fournisseur de services de Citrix permet aux fournisseurs de services d’offrir la simplicité du cloud computing virtuel aux petites et moyennes entreprises, en leur offrant les services souhaités dans un modèle simple et proposant un paiement à l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="93ba3-195">The Citrix Service Provider Program makes it easy for service providers to deliver the simplicity of virtual cloud computing to SMBs, offering them the services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="93ba3-196">Les fournisseurs de services Citrix développent leurs entreprises Microsoft SPLA et prolongent leurs investissements sur la plateforme de services de Bureau à distance sur tout appareil, avec un accès en tout lieu, la meilleure prise en charge d’applications disponible, une expérience riche, une meilleure sécurité et une évolutivité accrue.</span><span class="sxs-lookup"><span data-stu-id="93ba3-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, the broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="93ba3-197">Ainsi, les fournisseurs de services de Citrix attirent plus d’abonnés, améliorent la satisfaction des clients et réduisent les coûts d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="93ba3-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="93ba3-198">[En savoir plus](http://www.citrix.com/products/service-providers.html) ou [trouver un partenaire](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="93ba3-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="93ba3-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="93ba3-199">Acuutech</span></span>
<span data-ttu-id="93ba3-200">[Acuutech](http://www.acuutech.com) se spécialise dans la fourniture de solutions de bureaux hébergés, en livrant des expériences complètes d’application de bureau et d’éditeurs de logiciels construites sur la technologie Microsoft pour une base de clients globale, à partir d’Azure et leurs propres centres de données.</span><span class="sxs-lookup"><span data-stu-id="93ba3-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology to a global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="93ba3-201">Emplacements principaux : Londres, Royaume-Uni ; Singapour ; Houston, Texas</span><span class="sxs-lookup"><span data-stu-id="93ba3-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="93ba3-202">Région de l’opération  : monde entier</span><span class="sxs-lookup"><span data-stu-id="93ba3-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="93ba3-203">Statut du partenaire : Gold</span><span class="sxs-lookup"><span data-stu-id="93ba3-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="93ba3-204">Fournisseur de services Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="93ba3-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="93ba3-205">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="93ba3-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="93ba3-206">Solutions de migration Azure RemoteApp : Oui, [en savoir plus](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="93ba3-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="93ba3-207">**Royaume-Uni** :</span><span class="sxs-lookup"><span data-stu-id="93ba3-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="93ba3-208">5/6 York maison, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="93ba3-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="93ba3-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="93ba3-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="93ba3-210">Téléphone : +44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="93ba3-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="93ba3-211">**Singapour** :</span><span class="sxs-lookup"><span data-stu-id="93ba3-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="93ba3-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="93ba3-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="93ba3-213">The Globe, Singapore 069532</span><span class="sxs-lookup"><span data-stu-id="93ba3-213">The Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="93ba3-214">Téléphone : +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="93ba3-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="93ba3-215">**Amérique du Nord** :</span><span class="sxs-lookup"><span data-stu-id="93ba3-215">**North America**:</span></span>
>   
> <span data-ttu-id="93ba3-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="93ba3-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="93ba3-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="93ba3-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="93ba3-218">Téléphone : +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="93ba3-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="93ba3-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="93ba3-219">ASPEX</span></span>
<span data-ttu-id="93ba3-220">[ASPEX](http://www.aspex.be/en) se spécialise dans les éditeurs de logiciels en transition vers le cloud et ceux cherchant à optimiser leurs configurations cloud actuelles.</span><span class="sxs-lookup"><span data-stu-id="93ba3-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning to the Cloud and ISV‘ looking to optimize their current cloud setups.</span></span> <span data-ttu-id="93ba3-221">ASPEX offre un large éventail de services gérés, d’opérations de développement et de conseil.</span><span class="sxs-lookup"><span data-stu-id="93ba3-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="93ba3-222">Emplacement principal : Anvers, Belgique</span><span class="sxs-lookup"><span data-stu-id="93ba3-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="93ba3-223">Région d’activité : Europe de l’Ouest</span><span class="sxs-lookup"><span data-stu-id="93ba3-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="93ba3-224">Statut du partenaire : [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="93ba3-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="93ba3-225">Fournisseur de services Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="93ba3-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="93ba3-226">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="93ba3-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="93ba3-227">Solutions de migration Azure RemoteApp : Oui, [en savoir plus](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="93ba3-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="93ba3-228">Téléphone  : +3232202198</span><span class="sxs-lookup"><span data-stu-id="93ba3-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="93ba3-229">Mail : [info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="93ba3-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="93ba3-230">Web : [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="93ba3-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="93ba3-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="93ba3-231">Caase.com</span></span>
<span data-ttu-id="93ba3-232">[Caase.com](http://www.caase.com/) accompagne les entreprises, les administrations locales, les organismes non gouvernementaux et les établissements de santé dans leur quête d’une utilisation plus avertie de Microsoft Cloud, à savoir,</span><span class="sxs-lookup"><span data-stu-id="93ba3-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in the Microsoft Cloud.</span></span> <span data-ttu-id="93ba3-233">être productif n’importe où et en toute sécurisé, avec n’importe quel appareil et pour un faible coût informatique.</span><span class="sxs-lookup"><span data-stu-id="93ba3-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="93ba3-234">Caase.com est un vrai spécialiste de Microsoft Office 365, Azure, Enterprise Mobility + Security et Windows.</span><span class="sxs-lookup"><span data-stu-id="93ba3-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="93ba3-235">Caase.com propose à ses clients du conseil, des services de migration, des programmes d’adoption, des formations, des services de gestion et de support dans l’optique de créer une plateforme optimisée et sécurisée favorisant la collaboration entre leurs employés, leurs partenaires et leurs fournisseurs.</span><span class="sxs-lookup"><span data-stu-id="93ba3-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="93ba3-236">Caase.com est l’architecte d’Azure Remote Worskpace (espace de travail mobile) et de Digital Workplace (intranet social).</span><span class="sxs-lookup"><span data-stu-id="93ba3-236">Caase.com is the mastermind of the Azure Remote Workspace (mobile workplace) and the Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="93ba3-237">Ces deux solutions, qui s’accompagnent d’un programme d’adoption, assurent à leurs utilisateurs une transition vers Microsoft Cloud des plus agréables, concluantes et efficaces.</span><span class="sxs-lookup"><span data-stu-id="93ba3-237">Both solutions – accomplished with adoption – are the foundation which ensures that the users of these solutions have the most pleasant, successful and effective experience in their route to the Microsoft Cloud.</span></span>
<span data-ttu-id="93ba3-238">Vous trouverez un texte de présentation de ces solutions, ainsi qu’une vidéo, à l’adresse suivante (en néerlandais) : http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="93ba3-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="93ba3-239">Région d’exploitation : siège aux Pays-Bas, portée mondiale</span><span class="sxs-lookup"><span data-stu-id="93ba3-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="93ba3-240">Statut du partenaire : [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="93ba3-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="93ba3-241">Fournisseur de services Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="93ba3-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="93ba3-242">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="93ba3-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="93ba3-243">Solutions de migration Azure RemoteApp : oui, [en savoir plus](http://caase.com/diensten/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="93ba3-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="93ba3-244">Pays-bas :</span><span class="sxs-lookup"><span data-stu-id="93ba3-244">Netherlands:</span></span>
> 
> <span data-ttu-id="93ba3-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="93ba3-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="93ba3-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="93ba3-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="93ba3-247">Téléphone : +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="93ba3-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="93ba3-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="93ba3-248">Nerdio</span></span>
<span data-ttu-id="93ba3-249">[Nerdio for Azure](http://getnerdio.com/nfa/) est une plateforme d’automatisation informatique qui facilite considérablement l’approvisionnement, la gestion et l’optimisation des environnements informatiques complets dans Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="93ba3-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in the Microsoft cloud.</span></span> <span data-ttu-id="93ba3-250">Une paire d’heures suffit pour mettre en place des bureaux virtuels, des applications distantes et des serveurs.</span><span class="sxs-lookup"><span data-stu-id="93ba3-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="93ba3-251">Grâce au portail d’administration Nerdio, vous administrez l’environnement en quelques clics.</span><span class="sxs-lookup"><span data-stu-id="93ba3-251">Administer the environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="93ba3-252">La mise à l’échelle automatique et intelligente permet quant à elle d’économiser entre 40 et 60 % de ressources Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="93ba3-252">Use intelligent auto-scaling and save 40 to 60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="93ba3-253">Site principal : Chicago, IL. Région d’exploitation : monde. Statut partenaire : [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Fournisseur de services Microsoft Cloud : oui</span><span class="sxs-lookup"><span data-stu-id="93ba3-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="93ba3-254">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="93ba3-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="93ba3-255">Solutions de migration Azure RemoteApp : Oui</span><span class="sxs-lookup"><span data-stu-id="93ba3-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="93ba3-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="93ba3-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="93ba3-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="93ba3-257">Suite 212</span></span>
> 
> <span data-ttu-id="93ba3-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="93ba3-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="93ba3-259">États-Unis</span><span class="sxs-lookup"><span data-stu-id="93ba3-259">USA</span></span>
> 
> <span data-ttu-id="93ba3-260">(844) 4NERDIO poste</span><span class="sxs-lookup"><span data-stu-id="93ba3-260">(844) 4NERDIO ext.</span></span> <span data-ttu-id="93ba3-261">6</span><span class="sxs-lookup"><span data-stu-id="93ba3-261">6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="93ba3-262">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="93ba3-262">**SaaSplaza**</span></span>
<span data-ttu-id="93ba3-263">[SaaSplaza](http://www.saasplaza.com/) propose des services cloud privés et publics (Azure) pour toute la gamme Microsoft Dynamics (NAV, AX, GP, SL, CRM).</span><span class="sxs-lookup"><span data-stu-id="93ba3-263">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="93ba3-264">Emplacement principal : Pays-Bas</span><span class="sxs-lookup"><span data-stu-id="93ba3-264">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="93ba3-265">Région de l’opération : monde entier</span><span class="sxs-lookup"><span data-stu-id="93ba3-265">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="93ba3-266">Statut du partenaire : [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="93ba3-266">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="93ba3-267">Fournisseur de services Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="93ba3-267">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="93ba3-268">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="93ba3-268">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="93ba3-269">**Europe / Moyen-Orient / Afrique** :</span><span class="sxs-lookup"><span data-stu-id="93ba3-269">**EMEA**:</span></span>
> 
> <span data-ttu-id="93ba3-270">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="93ba3-270">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="93ba3-271">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="93ba3-271">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="93ba3-272">Pays-Bas</span><span class="sxs-lookup"><span data-stu-id="93ba3-272">The Netherlands</span></span>
> 
> <span data-ttu-id="93ba3-273">Téléphone : +31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="93ba3-273">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="93ba3-274">**Amérique** :</span><span class="sxs-lookup"><span data-stu-id="93ba3-274">**Americas**:</span></span>
> 
> <span data-ttu-id="93ba3-275">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="93ba3-275">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="93ba3-276">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="93ba3-276">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="93ba3-277">San Diego</span><span class="sxs-lookup"><span data-stu-id="93ba3-277">San Diego</span></span>
> 
> <span data-ttu-id="93ba3-278">États-Unis</span><span class="sxs-lookup"><span data-stu-id="93ba3-278">United States</span></span>
> 
> <span data-ttu-id="93ba3-279">Téléphone : +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="93ba3-279">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="93ba3-280">**Asie-Pacifique** :</span><span class="sxs-lookup"><span data-stu-id="93ba3-280">**APAC**:</span></span>
> 
> <span data-ttu-id="93ba3-281">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="93ba3-281">105 Cecil Street</span></span>
>    
> <span data-ttu-id="93ba3-282">\#11-08, The Octagon</span><span class="sxs-lookup"><span data-stu-id="93ba3-282">\#11-08, The Octagon</span></span>
> 
> <span data-ttu-id="93ba3-283">Singapour 069534</span><span class="sxs-lookup"><span data-stu-id="93ba3-283">Singapore 069534</span></span>
> 
> <span data-ttu-id="93ba3-284">Singapour</span><span class="sxs-lookup"><span data-stu-id="93ba3-284">Singapore</span></span>
>   
> <span data-ttu-id="93ba3-285">Téléphone - Singapour : +65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="93ba3-285">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="93ba3-286">Téléphone - Australie : +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="93ba3-286">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="93ba3-287">Téléphone - Nouvelle-Zélande : +64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="93ba3-287">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="93ba3-288">Besoin de plus d’aide ?</span><span class="sxs-lookup"><span data-stu-id="93ba3-288">Need more help?</span></span>
<span data-ttu-id="93ba3-289">Toujours besoin d’aide pour choisir ou des questions supplémentaires ?</span><span class="sxs-lookup"><span data-stu-id="93ba3-289">Still need help choosing or have further questions?</span></span> <span data-ttu-id="93ba3-290">Utilisez l’une des méthodes suivantes pour obtenir de l’aide.</span><span class="sxs-lookup"><span data-stu-id="93ba3-290">Use one of the following methods to get help.</span></span> 

1. <span data-ttu-id="93ba3-291">Envoyez-nous un e-mail à l’adresse [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="93ba3-291">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="93ba3-292">Contacter le [support Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="93ba3-292">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="93ba3-293">Commencez par créer un [ticket d’assistance Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="93ba3-293">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="93ba3-294">Appelez-nous.</span><span class="sxs-lookup"><span data-stu-id="93ba3-294">Call us.</span></span> <span data-ttu-id="93ba3-295">[Rechercher le numéro de téléphone d'un service commercial local](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="93ba3-295">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

