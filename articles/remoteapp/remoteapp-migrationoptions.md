---
title: "aaaOptions pour la migration en dehors d’Azure RemoteApp | Documents Microsoft"
description: "En savoir plus sur les options de hello pour la migration en dehors d’Azure RemoteApp."
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
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="673f0-103">Options de migration hors d’Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="673f0-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="673f0-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="673f0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="673f0-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="673f0-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="673f0-106">Si vous avez arrêté à l’aide d’Azure RemoteApp en raison de hello [annonce du retrait](https://go.microsoft.com/fwlink/?linkid=821148) ou parce que vous avez terminé votre version d’évaluation, vous devez toomigrate hors service d’applications Azure RemoteApp tooanother.</span><span class="sxs-lookup"><span data-stu-id="673f0-106">If you have stopped using Azure RemoteApp because of hello [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need toomigrate off of Azure RemoteApp tooanother app service.</span></span> <span data-ttu-id="673f0-107">Il existe deux approches différentes pour la migration : le déploiement autogéré (souvent appelé Infrastructure en tant que Service [IaaS]) ou une offre de plateforme entièrement gérée (souvent appelée Plateforme ou Logiciel en tant que service [PaaS/SaaS]).</span><span class="sxs-lookup"><span data-stu-id="673f0-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="673f0-108">L’IaaS en libre-service est un déploiement personnalisable que vous gérez, exploitez et possédez, directement déployé sur des machines virtuelles (VM) ou des systèmes physiques.</span><span class="sxs-lookup"><span data-stu-id="673f0-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="673f0-109">À hello autres terminer, une PaaS/SaaS entièrement géré offre est ressemble davantage à Azure RemoteApp - un partenaire fournit une couche de service sur une solution de communication à distance qui gère le fonctionnement et la maintenance, pendant que vous, en tant que client de hello, effectuer une gestion des applications et des images.</span><span class="sxs-lookup"><span data-stu-id="673f0-109">At hello other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as hello customer, do some image and app management.</span></span>

<span data-ttu-id="673f0-110">[Afficher hello Azure RemoteApp webinaires sur les options de migration](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), ou de lecture pour plus d’informations (y compris des exemples de différente options d’hébergement de hello).</span><span class="sxs-lookup"><span data-stu-id="673f0-110">[View hello Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of hello different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="673f0-111">Solutions autogérées (IaaS)</span><span class="sxs-lookup"><span data-stu-id="673f0-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="673f0-112">**RDS sur IaaS**</span><span class="sxs-lookup"><span data-stu-id="673f0-112">**RDS on IaaS**</span></span>
<span data-ttu-id="673f0-113">Vous pouvez déployer un déploiement de services Bureau à distance natif basé sur les sessions (dans Windows Server) à l’aide de RemoteApp sur des postes de travail locaux ou dans un environnement hébergé (comme sur les machines virtuelles Azure).</span><span class="sxs-lookup"><span data-stu-id="673f0-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="673f0-114">Les services Bureau à Distance sur les déploiements IaaS sont parfaits pour les clients déjà familiarisés avec cette solution et qui ont une expertise technique existante pour les déploiements de services Bureau à Distance.</span><span class="sxs-lookup"><span data-stu-id="673f0-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="673f0-115">Vous devez avec Software Assurance (SA) de licence en Volume pour les services Bureau à distance client accès licences toouse cette option de déploiement.</span><span class="sxs-lookup"><span data-stu-id="673f0-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses toouse this deployment option.</span></span>

<span data-ttu-id="673f0-116">Le déploiement des services Bureau à Distance sur des machines virtuelles Azure est plus facile que jamais lorsque vous utilisez le déploiement et des modèles d’application de correctifs (lisez la [présentation](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) puis [récupérez-les](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="673f0-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="673f0-117">Vous pouvez obtenir les mêmes fonctionnalités de mise à l’échelle élastiques avec les ressources de modèle de déploiement classique Azure (pas les ressources de modèle de ressource Azure) dans Azure RemoteApp hello à l’aide de hello [mise à l’échelle de script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), bien qu’il existe plus personnalisations et configurations.</span><span class="sxs-lookup"><span data-stu-id="673f0-117">You can get hello same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using hello [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="673f0-118">Lorsque vous déployez des services Bureau à distance sur des machines virtuelles Azure, est prise en charge via [Azure prend en charge](https://azure.microsoft.com/support/plans/), hello même professionnels du support technique vous pris en charge avec Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="673f0-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), hello same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="673f0-119">Vous pouvez obtenir des estimations de coût en fonction de votre utilisation existante en contactant [prise en charge Azure](https://azure.microsoft.com/support/plans/), ou vous pouvez effectuer des calculs vous-même à l’aide un bientôt toobe publié calculateur de coût.</span><span class="sxs-lookup"><span data-stu-id="673f0-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon toobe released Cost Calculator.</span></span>  <span data-ttu-id="673f0-120">En outre, avec des machines virtuelles de série N (actuellement en aperçu privé), vous pouvez ajouter vGPU - plus d’informations sur l’ajout de processeur et sur la façon de réponse trop[maîtriser les améliorations des services Bureau à distance dans Windows Server 2016](https://myignite.microsoft.com/videos/2794) dans notre session Ignite.</span><span class="sxs-lookup"><span data-stu-id="673f0-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how too[harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="673f0-121">Nous avons des guides de déploiement de l’étape par étape pour [Windows Server 2012 R2](http://aka.ms/rdsonazure) et [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist avec votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="673f0-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist with your deployment.</span></span> <span data-ttu-id="673f0-122">Extraire hello [blog du Bureau à distance](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) pour les informations les plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="673f0-122">Check out hello [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for hello latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="673f0-123">**Citrix sur IaaS**</span><span class="sxs-lookup"><span data-stu-id="673f0-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="673f0-124">Un déploiement Citrix natif de XenApp ou de XenDesktop basé sur les sessions peut être déployé localement ou dans un environnement hébergé (par exemple sur des machines virtuelles Azure).</span><span class="sxs-lookup"><span data-stu-id="673f0-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="673f0-125">Guide de déploiement étape par étape hello, consultez [7.6 XA de Citrix sur Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="673f0-125">Check out hello step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="673f0-126">En savoir plus sur [Citrix sur Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), avec notamment un calculateur de prix.</span><span class="sxs-lookup"><span data-stu-id="673f0-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="673f0-127">Vous pouvez également rechercher un [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss vos options avec.</span><span class="sxs-lookup"><span data-stu-id="673f0-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="673f0-128">Offres entièrement gérés (PaaS/SaaS)</span><span class="sxs-lookup"><span data-stu-id="673f0-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="673f0-129">Citrix XenApp Essentials (parution : avril 2017)</span><span class="sxs-lookup"><span data-stu-id="673f0-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="673f0-130">Disponible pour l’instant sur hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials est le nouveau service de virtualisation d’application hello, associant hello puissance et flexibilité de hello plateforme Cloud de Citrix avec simple hello et normative, et Pour utiliser la vision de Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="673f0-130">Available now on hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is hello new application virtualization service, combining hello power and flexibility of hello Citrix Cloud platform with hello simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="673f0-131">Les clients Azure RemoteApp existants peuvent [s’inscrire pour profiter d’une version d’évaluation gratuite](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="673f0-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="673f0-132">Remarque : seul le service utilisateur Citrix est gratuit. Calcul Azure et Stockage Azure sont payants.</span><span class="sxs-lookup"><span data-stu-id="673f0-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="673f0-133">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="673f0-133">Learn More:</span></span>
- [<span data-ttu-id="673f0-134">Migrer à partir d’Azure RemoteApp tooCitrix XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="673f0-134">Migrate from Azure RemoteApp tooCitrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="673f0-135">Citrix et Microsoft</span><span class="sxs-lookup"><span data-stu-id="673f0-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="673f0-136">[Présentation de Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k)</span><span class="sxs-lookup"><span data-stu-id="673f0-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="673f0-137">Services Citrix Cloud XenApp et XenDesktop</span><span class="sxs-lookup"><span data-stu-id="673f0-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="673f0-138">[Le Service Cloud XenApp Citrix et XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) est hello meilleure solution pour la remise de hello des applications et poste de travail, plus avancées de gestion et ses fonctionnalités de surveillance.</span><span class="sxs-lookup"><span data-stu-id="673f0-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is hello best solution for hello delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="673f0-139">Conexlink (nom de la plateforme : MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="673f0-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="673f0-140">[MyCloudIT](https://mycloudit.com) est une plate-forme d’automatisation pour toosimplify de sociétés informatiques, optimiser et mettre à l’échelle de la migration hello et remise des bureaux à distance, les applications à distance et l’infrastructure dans hello Microsoft Azure Cloud.</span><span class="sxs-lookup"><span data-stu-id="673f0-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies toosimplify, optimize, and scale hello migration and delivery of remote desktops, remote applications, and infrastructure in hello Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="673f0-141">plateforme de MyCloudIT Hello réduit le temps de déploiement en 95 %, Azure coût de 30 % et déplace de l’infrastructure informatique de leurs clients dans cloud hello retirés au bout de quelques séquences de touches.</span><span class="sxs-lookup"><span data-stu-id="673f0-141">hello MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into hello cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="673f0-142">Les partenaires peuvent désormais gérer les clients à partir d’un tableau de bord global, les utilisateurs finaux de service monde hello comme jamais auparavant et augmenter les revenus sans ajouter une charge supplémentaire ou formation Azure complète.</span><span class="sxs-lookup"><span data-stu-id="673f0-142">Partners can now manage customers from one global dashboard, service end users around hello world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="673f0-143">Emplacement principal : Dallas, Texas, États-Unis</span><span class="sxs-lookup"><span data-stu-id="673f0-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="673f0-144">Région de l’opération  : monde entier</span><span class="sxs-lookup"><span data-stu-id="673f0-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="673f0-145">Statut du partenaire : [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="673f0-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="673f0-146">Fournisseur de services Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="673f0-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="673f0-147">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="673f0-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="673f0-148">Solutions de migration Azure RemoteApp : Oui, [en savoir plus](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="673f0-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="673f0-149">Brian Garoutte, vice-président du développement commercial</span><span class="sxs-lookup"><span data-stu-id="673f0-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="673f0-150">Téléphone : 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="673f0-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="673f0-151">E-mail : [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="673f0-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="673f0-152">Frame</span><span class="sxs-lookup"><span data-stu-id="673f0-152">Frame</span></span>

<span data-ttu-id="673f0-153">Les organisations informatiques dans enterprise et gouvernement, fournisseurs de services gérés et principaux fournisseurs de logiciels choisissez toocreate de Frame et gérer leurs espaces de travail sécurisés, défini par logiciel dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="673f0-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame toocreate and manage their secure, software-defined workspaces in hello cloud.</span></span> <span data-ttu-id="673f0-154">À partir de toolarge petites organisations, Frame rend très facile toolet utilisateurs accéder aux applications Windows sur n’importe quel navigateur à partir de n’importe quel appareil.</span><span class="sxs-lookup"><span data-stu-id="673f0-154">From small toolarge organizations, Frame makes it incredibly easy toolet users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="673f0-155">Hello plateforme de Frame comprend tout ce dont un administrateur besoins toodeploy applications de cloud hello notamment hello infrastructure Azure et licences des services Bureau à distance (mettre votre propre compte Azure et licences est facultative).</span><span class="sxs-lookup"><span data-stu-id="673f0-155">hello Frame platform includes everything an admin needs toodeploy applications from hello cloud including hello Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="673f0-156">En savoir plus sur [Frame sur Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="673f0-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="673f0-157">Emplacement principal : San Mateo, CA, États-Unis</span><span class="sxs-lookup"><span data-stu-id="673f0-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="673f0-158">Région de l’opération  : monde entier</span><span class="sxs-lookup"><span data-stu-id="673f0-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="673f0-159">Partenaire Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="673f0-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="673f0-160">Téléphone : 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="673f0-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="673f0-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="673f0-161">Awingu</span></span>
<span data-ttu-id="673f0-162">Awingu fournit une solution simple d’espace de travail en ligne qui exécute des applications héritées, SaaS et des documents à partir d’un navigateur html5.</span><span class="sxs-lookup"><span data-stu-id="673f0-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="673f0-163">Ainsi, les applications sont disponibles en toute sécurité, sur tous les types d’appareils.</span><span class="sxs-lookup"><span data-stu-id="673f0-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="673f0-164">Pour les services SaaS, un large éventail d’options d’authentification unique (SSO) est disponible.</span><span class="sxs-lookup"><span data-stu-id="673f0-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="673f0-165">De plus, plusieurs systèmes de fichiers (cloud) peuvent être profondément intégrés dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="673f0-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="673f0-166">Espace de travail en ligne de Awingu enrichi donne suivant toofull mobilité, une sécurité optimale avec contrôles granulaires (par exemple, du téléchargement/chargement), l’utilisation complète de l’audit, l’authentification multifacteur (par exemple, Azure MFA), l’enregistrement de session et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="673f0-166">Next toofull mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="673f0-167">Solution originale, Awingu permet le partage de session d’application et de document pour une collaboration sûre et optimisée.</span><span class="sxs-lookup"><span data-stu-id="673f0-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="673f0-168">Awingu est une solution d’API ouverte, multi-AD et mutualisée.</span><span class="sxs-lookup"><span data-stu-id="673f0-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="673f0-169">Elle est utilisée par les petites et grandes entreprises, fournisseurs de services Cloud et les [ISV](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="673f0-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="673f0-170">Ces clients plaira particulièrement hello facile d’utilisation, facilité à installer et à faible coût total de possession.</span><span class="sxs-lookup"><span data-stu-id="673f0-170">These customers especially appreciate hello easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="673f0-171">Awingu tout-en-un est [disponibles dans Azure Marketplace de hello](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) avec 2 utilisateurs simultanés intégrés.</span><span class="sxs-lookup"><span data-stu-id="673f0-171">Awingu All-in-One is [available in hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="673f0-172">Des licences supplémentaires sont disponibles via un [large éventail de distributeurs et revendeurs](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="673f0-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="673f0-173">En savoir plus sur [Awingu sur comme autre tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="673f0-173">Learn more about [Awingu on as alternative tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="673f0-174">Emplacement principal : Belgique</span><span class="sxs-lookup"><span data-stu-id="673f0-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="673f0-175">Régions opérationnelles : EMEA, Amérique du Nord et Brésil</span><span class="sxs-lookup"><span data-stu-id="673f0-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="673f0-176">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="673f0-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="673f0-177">**Mondial** :</span><span class="sxs-lookup"><span data-stu-id="673f0-177">**Global**:</span></span>
> 
> <span data-ttu-id="673f0-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="673f0-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="673f0-179">E-mail : [arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="673f0-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="673f0-180">Téléphone : +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="673f0-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="673f0-181">**Siège en Belgique** :</span><span class="sxs-lookup"><span data-stu-id="673f0-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="673f0-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="673f0-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="673f0-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="673f0-183">9000 Gent</span></span>
> 
> <span data-ttu-id="673f0-184">E-mail : [info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="673f0-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="673f0-185">Téléphone : +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="673f0-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="673f0-186">**États-Unis** :</span><span class="sxs-lookup"><span data-stu-id="673f0-186">**USA**:</span></span>
> 
> <span data-ttu-id="673f0-187">7 floor, Ave 1177 Hello Amériques,</span><span class="sxs-lookup"><span data-stu-id="673f0-187">7th floor, 1177 Ave of hello Americas,</span></span>
> 
> <span data-ttu-id="673f0-188">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="673f0-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="673f0-189">E-mail : [info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="673f0-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="673f0-190">Fournisseur de services hébergés Microsoft</span><span class="sxs-lookup"><span data-stu-id="673f0-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="673f0-191">Partenaires d’hébergement offrent généralement entièrement géré hébergé bureau Windows et de hello de service d’application, qui peut inclure la gestion des ressources Azure, des systèmes d’exploitation, des applications et de support technique à l’aide du partenaire de hello du Gestionnaire de licences des contrats avec Microsoft et autres fournisseurs de logiciels, ainsi que d’en cours de contrat de licence de fournisseur de services de la licence d’accès abonné (SAL) revente tooallow.</span><span class="sxs-lookup"><span data-stu-id="673f0-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing hello Azure resources, operating systems, applications, and helpdesk using hello partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement tooallow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="673f0-192">Hello ci-après fournit des détails et informations de contact pour certaines des hébergeurs hello spécialisés pour aider les clients avec leur migration d’Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="673f0-192">hello following information provides details and contact information for some of hello hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="673f0-193">Extraire [liste actuelle de hello des fournisseurs de services hébergés](http://aka.ms/rdsonazurecertified) qui terminées hello RDS sur IaaS, chemin d’accès et d’évaluation de la formation.</span><span class="sxs-lookup"><span data-stu-id="673f0-193">Check out [hello current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed hello RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="673f0-194">Programme de fournisseur de services de Citrix</span><span class="sxs-lookup"><span data-stu-id="673f0-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="673f0-195">Hello Citrix Service fournisseur de programme facilite pour simplifier service fournisseurs toodeliver hello virtuel cloud computing tooSMBs, offre les services hello qu’ils souhaitent dans un modèle simple et de paiement à l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="673f0-195">hello Citrix Service Provider Program makes it easy for service providers toodeliver hello simplicity of virtual cloud computing tooSMBs, offering them hello services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="673f0-196">Les fournisseurs de services de Citrix développer leur activité Microsoft SPLA et développer leurs investissements de plateforme des services Bureau à distance avec n’importe quel appareil, accès en tout lieu, hello plus large prise en charge des applications une expérience enrichie, renforcer la sécurité et une extensibilité accrue.</span><span class="sxs-lookup"><span data-stu-id="673f0-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, hello broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="673f0-197">Ainsi, les fournisseurs de services de Citrix attirent plus d’abonnés, améliorent la satisfaction des clients et réduisent les coûts d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="673f0-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="673f0-198">[En savoir plus](http://www.citrix.com/products/service-providers.html) ou [trouver un partenaire](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="673f0-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="673f0-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="673f0-199">Acuutech</span></span>
<span data-ttu-id="673f0-200">[Acuutech](http://www.acuutech.com) spécialisée de fournir des solutions de bureau hébergées, fourniture de bureau et applications ISV expériences reposant sur la technologie tooa global client Microsoft base à partir d’Azure et de leurs propres centres de données.</span><span class="sxs-lookup"><span data-stu-id="673f0-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology tooa global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="673f0-201">Emplacements principaux : Londres, Royaume-Uni ; Singapour ; Houston, Texas</span><span class="sxs-lookup"><span data-stu-id="673f0-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="673f0-202">Région de l’opération  : monde entier</span><span class="sxs-lookup"><span data-stu-id="673f0-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="673f0-203">Statut du partenaire : Gold</span><span class="sxs-lookup"><span data-stu-id="673f0-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="673f0-204">Fournisseur de services Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="673f0-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="673f0-205">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="673f0-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="673f0-206">Solutions de migration Azure RemoteApp : Oui, [en savoir plus](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="673f0-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="673f0-207">**Royaume-Uni** :</span><span class="sxs-lookup"><span data-stu-id="673f0-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="673f0-208">5/6 York maison, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="673f0-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="673f0-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="673f0-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="673f0-210">Téléphone : +44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="673f0-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="673f0-211">**Singapour** :</span><span class="sxs-lookup"><span data-stu-id="673f0-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="673f0-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="673f0-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="673f0-213">Hello Globe, Singapour 069532</span><span class="sxs-lookup"><span data-stu-id="673f0-213">hello Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="673f0-214">Téléphone : +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="673f0-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="673f0-215">**Amérique du Nord** :</span><span class="sxs-lookup"><span data-stu-id="673f0-215">**North America**:</span></span>
>   
> <span data-ttu-id="673f0-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="673f0-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="673f0-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="673f0-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="673f0-218">Téléphone : +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="673f0-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="673f0-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="673f0-219">ASPEX</span></span>
<span data-ttu-id="673f0-220">[ASPEX](http://www.aspex.be/en) spécialisé dans les éditeurs de logiciels en cours de transition toohello Cloud et ISV' recherche toooptimize leurs configurations de cloud en cours.</span><span class="sxs-lookup"><span data-stu-id="673f0-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning toohello Cloud and ISV‘ looking toooptimize their current cloud setups.</span></span> <span data-ttu-id="673f0-221">ASPEX offre un large éventail de services gérés, d’opérations de développement et de conseil.</span><span class="sxs-lookup"><span data-stu-id="673f0-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="673f0-222">Emplacement principal : Anvers, Belgique</span><span class="sxs-lookup"><span data-stu-id="673f0-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="673f0-223">Région d’activité : Europe de l’Ouest</span><span class="sxs-lookup"><span data-stu-id="673f0-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="673f0-224">Statut du partenaire : [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="673f0-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="673f0-225">Fournisseur de services Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="673f0-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="673f0-226">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="673f0-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="673f0-227">Solutions de migration Azure RemoteApp : Oui, [en savoir plus](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="673f0-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="673f0-228">Téléphone  : +3232202198</span><span class="sxs-lookup"><span data-stu-id="673f0-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="673f0-229">Mail : [info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="673f0-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="673f0-230">Web : [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="673f0-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="673f0-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="673f0-231">Caase.com</span></span>
<span data-ttu-id="673f0-232">[Caase.com](http://www.caase.com/) aide les entreprises, administrations locales, des organismes non gouvernementaux et les établissements de soins de santé avec leur voyage vers un moyen plus intelligent de travail Bonjour Cloud Microsoft.</span><span class="sxs-lookup"><span data-stu-id="673f0-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in hello Microsoft Cloud.</span></span> <span data-ttu-id="673f0-233">être productif n’importe où et en toute sécurisé, avec n’importe quel appareil et pour un faible coût informatique.</span><span class="sxs-lookup"><span data-stu-id="673f0-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="673f0-234">Caase.com est un vrai spécialiste de Microsoft Office 365, Azure, Enterprise Mobility + Security et Windows.</span><span class="sxs-lookup"><span data-stu-id="673f0-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="673f0-235">Caase.com propose à ses clients du conseil, des services de migration, des programmes d’adoption, des formations, des services de gestion et de support dans l’optique de créer une plateforme optimisée et sécurisée favorisant la collaboration entre leurs employés, leurs partenaires et leurs fournisseurs.</span><span class="sxs-lookup"><span data-stu-id="673f0-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="673f0-236">Caase.com est maîtrisée hello de hello espace de travail Azure à distance (espace de travail mobile) et hello espace de travail numérique (Social Intranet).</span><span class="sxs-lookup"><span data-stu-id="673f0-236">Caase.com is hello mastermind of hello Azure Remote Workspace (mobile workplace) and hello Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="673f0-237">Les deux solutions – accomplies avec adoption – sont foundation hello qui garantit que les utilisateurs de hello de ces solutions ont expérience plus agréable, réussie et efficace de hello dans leur toohello itinéraire Cloud Microsoft.</span><span class="sxs-lookup"><span data-stu-id="673f0-237">Both solutions – accomplished with adoption – are hello foundation which ensures that hello users of these solutions have hello most pleasant, successful and effective experience in their route toohello Microsoft Cloud.</span></span>
<span data-ttu-id="673f0-238">Vous trouverez un texte de présentation de ces solutions, ainsi qu’une vidéo, à l’adresse suivante (en néerlandais) : http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="673f0-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="673f0-239">Région d’exploitation : siège aux Pays-Bas, portée mondiale</span><span class="sxs-lookup"><span data-stu-id="673f0-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="673f0-240">Statut du partenaire : [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="673f0-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="673f0-241">Fournisseur de services Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="673f0-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="673f0-242">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="673f0-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="673f0-243">Solutions de migration Azure RemoteApp : oui, [en savoir plus](http://caase.com/diensten/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="673f0-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="673f0-244">Pays-bas :</span><span class="sxs-lookup"><span data-stu-id="673f0-244">Netherlands:</span></span>
> 
> <span data-ttu-id="673f0-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="673f0-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="673f0-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="673f0-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="673f0-247">Téléphone : +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="673f0-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="673f0-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="673f0-248">Nerdio</span></span>
<span data-ttu-id="673f0-249">[Nerdio pour Azure](http://getnerdio.com/nfa/) est une plate-forme d’automatisation informatique qui remet ridiculement simple mise en service, la gestion et l’optimisation des environnements informatiques complets Bonjour cloud de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="673f0-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in hello Microsoft cloud.</span></span> <span data-ttu-id="673f0-250">Une paire d’heures suffit pour mettre en place des bureaux virtuels, des applications distantes et des serveurs.</span><span class="sxs-lookup"><span data-stu-id="673f0-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="673f0-251">Administrer l’environnement hello dans trois clics ou moins avec le portail d’administration Nerdio.</span><span class="sxs-lookup"><span data-stu-id="673f0-251">Administer hello environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="673f0-252">Utilisez intelligente montée en puissance automatique et enregistrez les 40 % de too60 dans les ressources IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="673f0-252">Use intelligent auto-scaling and save 40 too60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="673f0-253">Site principal : Chicago, IL. Région d’exploitation : monde. Statut partenaire : [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Fournisseur de services Microsoft Cloud : oui</span><span class="sxs-lookup"><span data-stu-id="673f0-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="673f0-254">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="673f0-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="673f0-255">Solutions de migration Azure RemoteApp : Oui</span><span class="sxs-lookup"><span data-stu-id="673f0-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="673f0-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="673f0-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="673f0-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="673f0-257">Suite 212</span></span>
> 
> <span data-ttu-id="673f0-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="673f0-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="673f0-259">États-Unis</span><span class="sxs-lookup"><span data-stu-id="673f0-259">USA</span></span>
> 
> <span data-ttu-id="673f0-260">(844) 4NERDIO poste 6</span><span class="sxs-lookup"><span data-stu-id="673f0-260">(844) 4NERDIO ext. 6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="673f0-261">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="673f0-261">**SaaSplaza**</span></span>
<span data-ttu-id="673f0-262">[SaaSplaza](http://www.saasplaza.com/) propose des services cloud privés et publics (Azure) pour toute la gamme Microsoft Dynamics (NAV, AX, GP, SL, CRM).</span><span class="sxs-lookup"><span data-stu-id="673f0-262">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="673f0-263">Emplacement principal : Pays-Bas</span><span class="sxs-lookup"><span data-stu-id="673f0-263">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="673f0-264">Région de l’opération : monde entier</span><span class="sxs-lookup"><span data-stu-id="673f0-264">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="673f0-265">Statut du partenaire : [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="673f0-265">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="673f0-266">Fournisseur de services Microsoft : Oui</span><span class="sxs-lookup"><span data-stu-id="673f0-266">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="673f0-267">Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux</span><span class="sxs-lookup"><span data-stu-id="673f0-267">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="673f0-268">**Europe / Moyen-Orient / Afrique** :</span><span class="sxs-lookup"><span data-stu-id="673f0-268">**EMEA**:</span></span>
> 
> <span data-ttu-id="673f0-269">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="673f0-269">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="673f0-270">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="673f0-270">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="673f0-271">Hello pays-bas</span><span class="sxs-lookup"><span data-stu-id="673f0-271">hello Netherlands</span></span>
> 
> <span data-ttu-id="673f0-272">Téléphone : +31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="673f0-272">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="673f0-273">**Amérique** :</span><span class="sxs-lookup"><span data-stu-id="673f0-273">**Americas**:</span></span>
> 
> <span data-ttu-id="673f0-274">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="673f0-274">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="673f0-275">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="673f0-275">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="673f0-276">San Diego</span><span class="sxs-lookup"><span data-stu-id="673f0-276">San Diego</span></span>
> 
> <span data-ttu-id="673f0-277">États-Unis</span><span class="sxs-lookup"><span data-stu-id="673f0-277">United States</span></span>
> 
> <span data-ttu-id="673f0-278">Téléphone : +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="673f0-278">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="673f0-279">**Asie-Pacifique** :</span><span class="sxs-lookup"><span data-stu-id="673f0-279">**APAC**:</span></span>
> 
> <span data-ttu-id="673f0-280">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="673f0-280">105 Cecil Street</span></span>
>    
> <span data-ttu-id="673f0-281">\#11-08, hello octogone</span><span class="sxs-lookup"><span data-stu-id="673f0-281">\#11-08, hello Octagon</span></span>
> 
> <span data-ttu-id="673f0-282">Singapour 069534</span><span class="sxs-lookup"><span data-stu-id="673f0-282">Singapore 069534</span></span>
> 
> <span data-ttu-id="673f0-283">Singapour</span><span class="sxs-lookup"><span data-stu-id="673f0-283">Singapore</span></span>
>   
> <span data-ttu-id="673f0-284">Téléphone - Singapour : +65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="673f0-284">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="673f0-285">Téléphone - Australie : +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="673f0-285">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="673f0-286">Téléphone - Nouvelle-Zélande : +64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="673f0-286">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="673f0-287">Besoin de plus d’aide ?</span><span class="sxs-lookup"><span data-stu-id="673f0-287">Need more help?</span></span>
<span data-ttu-id="673f0-288">Toujours besoin d’aide pour choisir ou des questions supplémentaires ?</span><span class="sxs-lookup"><span data-stu-id="673f0-288">Still need help choosing or have further questions?</span></span> <span data-ttu-id="673f0-289">Utilisez une des hello suivant les méthodes tooget aide.</span><span class="sxs-lookup"><span data-stu-id="673f0-289">Use one of hello following methods tooget help.</span></span> 

1. <span data-ttu-id="673f0-290">Envoyez-nous un e-mail à l’adresse [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="673f0-290">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="673f0-291">Contacter le [support Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="673f0-291">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="673f0-292">Commencez par créer un [ticket d’assistance Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="673f0-292">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="673f0-293">Appelez-nous.</span><span class="sxs-lookup"><span data-stu-id="673f0-293">Call us.</span></span> <span data-ttu-id="673f0-294">[Rechercher le numéro de téléphone d'un service commercial local](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="673f0-294">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

