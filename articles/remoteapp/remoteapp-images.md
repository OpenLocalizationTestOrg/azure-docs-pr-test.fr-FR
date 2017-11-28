---
title: "aaaWhat est dans les images de modèle hello Azure RemoteApp ? | Microsoft Docs"
description: "En savoir plus sur les images de modèle hello inclus avec Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a><span data-ttu-id="d972d-104">Nouveautés dans les images de modèle hello Azure RemoteApp ?</span><span class="sxs-lookup"><span data-stu-id="d972d-104">What is in hello Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d972d-105">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="d972d-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d972d-106">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d972d-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d972d-107">Votre abonnement Azure RemoteApp comprend trois images de modèle :</span><span class="sxs-lookup"><span data-stu-id="d972d-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="d972d-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d972d-108">Windows Server 2012</span></span>
* <span data-ttu-id="d972d-109">Microsoft Office 365 ProPlus (abonnement Office 365 requis)</span><span class="sxs-lookup"><span data-stu-id="d972d-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="d972d-110">Microsoft Office Professionnel Plus 2013 (version d'évaluation uniquement)</span><span class="sxs-lookup"><span data-stu-id="d972d-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d972d-111">Votre abonnement Azure RemoteApp vous permet de qu'accéder logiciel toohello dans les images de hello, avec l’exception hello d’Office 365 ProPlus, ce qui nécessite un abonnement distinct, et Office 2013, qui ne peut pas être utilisé en production.</span><span class="sxs-lookup"><span data-stu-id="d972d-111">Your Azure RemoteApp subscription grants you access toohello software in hello images, with hello exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="d972d-112">Cela signifie que vous pouvez partager les programmes hello ou applications sur les images de modèle hello avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d972d-112">This means that you can share hello programs or apps on hello template images with your users.</span></span> <span data-ttu-id="d972d-113">Par exemple, si vous créez un regroupement qui utilise l’image de Windows Server 2012 R2 hello, vous pouvez publier System Center Endpoint Protection pour tooaccess utilisateurs via RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d972d-113">For example, if you create a collection that uses hello Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users tooaccess through RemoteApp.</span></span>
> 
> <span data-ttu-id="d972d-114">Extraire hello [RemoteApp licences détails](remoteapp-licensing.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d972d-114">Check out hello [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="d972d-115">Et [à l’aide d’Office avec Azure RemoteApp](remoteapp-o365.md) pourquoi les informations de licence Office.</span><span class="sxs-lookup"><span data-stu-id="d972d-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for hello Office licensing info.</span></span>
> 
> 

<span data-ttu-id="d972d-116">Continuez votre lecture pour en savoir plus sur ce que contient chaque image.</span><span class="sxs-lookup"><span data-stu-id="d972d-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--hello-vanilla-image"></a><span data-ttu-id="d972d-117">Windows Server 2012 R2 (« hello vanille image »)</span><span class="sxs-lookup"><span data-stu-id="d972d-117">Windows Server 2012 R2  ("hello vanilla image")</span></span>
<span data-ttu-id="d972d-118">Cette image est basée sur le système d’exploitation Microsoft Windows Server 2012 R2 Datacenter et a hello suivantes des rôles et fonctionnalités installés toomeet les exigences de hello pour les images de modèle Azure RemoteApp :</span><span class="sxs-lookup"><span data-stu-id="d972d-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has hello following roles and features installed toomeet hello requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="d972d-119">.NET Framework 4.5, 3.5.1, 3.5</span><span class="sxs-lookup"><span data-stu-id="d972d-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="d972d-120">Expérience utilisateur</span><span class="sxs-lookup"><span data-stu-id="d972d-120">Desktop Experience</span></span>
* <span data-ttu-id="d972d-121">Services de prise en charge de l'écriture manuscrite</span><span class="sxs-lookup"><span data-stu-id="d972d-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="d972d-122">Media Foundation</span><span class="sxs-lookup"><span data-stu-id="d972d-122">Media Foundation</span></span>
* <span data-ttu-id="d972d-123">Hôte de session Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="d972d-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="d972d-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="d972d-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="d972d-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="d972d-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="d972d-126">Prise en charge WoW64</span><span class="sxs-lookup"><span data-stu-id="d972d-126">WoW64 Support</span></span>

<span data-ttu-id="d972d-127">Cette image a également hello suivant des applications installées :</span><span class="sxs-lookup"><span data-stu-id="d972d-127">This image also has hello following applications installed:</span></span>

* <span data-ttu-id="d972d-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="d972d-128">Adobe Flash Player</span></span>
* <span data-ttu-id="d972d-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="d972d-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="d972d-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="d972d-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="d972d-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="d972d-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="d972d-132">Microsoft Office 365 ProPlus (abonnement requis)</span><span class="sxs-lookup"><span data-stu-id="d972d-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="d972d-133">Office 365 est hello plus de l’application demandé, nous avons créé une image « personnalisée » pour vous toowork avec.</span><span class="sxs-lookup"><span data-stu-id="d972d-133">Office 365 is hello most requested application, so we created a "custom" image for you toowork with.</span></span>

<span data-ttu-id="d972d-134">Cette image est une extension de l’image de vanille hello et a hello les composants suivants de Microsoft Office 365 ProPlus installé en outre les composants toohello décrits dans l’image de Windows Server 2012 R2 hello :</span><span class="sxs-lookup"><span data-stu-id="d972d-134">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 365 ProPlus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="d972d-135">Access</span><span class="sxs-lookup"><span data-stu-id="d972d-135">Access</span></span>
* <span data-ttu-id="d972d-136">Excel</span><span class="sxs-lookup"><span data-stu-id="d972d-136">Excel</span></span>
* <span data-ttu-id="d972d-137">Lync</span><span class="sxs-lookup"><span data-stu-id="d972d-137">Lync</span></span>
* <span data-ttu-id="d972d-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="d972d-138">OneNote</span></span>
* <span data-ttu-id="d972d-139">OneDrive entreprise (Notez que l’agent de synchronisation hello n’est pas prise en charge pour une utilisation avec Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="d972d-139">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="d972d-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="d972d-140">Outlook</span></span>
* <span data-ttu-id="d972d-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d972d-141">PowerPoint</span></span>
* <span data-ttu-id="d972d-142">Word</span><span class="sxs-lookup"><span data-stu-id="d972d-142">Word</span></span>
* <span data-ttu-id="d972d-143">Outils de vérification linguistique Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="d972d-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="d972d-144">image de Hello inclut également Pro de Visio et de Project Professionnel.</span><span class="sxs-lookup"><span data-stu-id="d972d-144">hello image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="d972d-145">Et hello suivant des applications, ainsi :</span><span class="sxs-lookup"><span data-stu-id="d972d-145">And hello following applications, as well:</span></span>

* <span data-ttu-id="d972d-146">SQL Native Client</span><span class="sxs-lookup"><span data-stu-id="d972d-146">SQL Native client</span></span>
* <span data-ttu-id="d972d-147">Pilote ODBC</span><span class="sxs-lookup"><span data-stu-id="d972d-147">ODBC Driver</span></span>
* <span data-ttu-id="d972d-148">Client d'exploration de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="d972d-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="d972d-149">Client MasterDataServices</span><span class="sxs-lookup"><span data-stu-id="d972d-149">MasterDataServices client</span></span>
* <span data-ttu-id="d972d-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="d972d-150">Microsoft Publisher</span></span>
* <span data-ttu-id="d972d-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="d972d-151">PowerQuery</span></span>
* <span data-ttu-id="d972d-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="d972d-152">PowerMap</span></span>

<span data-ttu-id="d972d-153">Toutes les fonctionnalités des applications Office 365 ProPlus sont disponibles uniquement pour les utilisateurs qui disposent d'une offre Office 365 ProPlus.</span><span class="sxs-lookup"><span data-stu-id="d972d-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="d972d-154">Pour plus d’informations sur l’abonnement de hello Office 365 plans consultez [des plans de services Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span><span class="sxs-lookup"><span data-stu-id="d972d-154">For more details on hello Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="d972d-155">Des questions supplémentaires ?</span><span class="sxs-lookup"><span data-stu-id="d972d-155">Still have questions?</span></span> <span data-ttu-id="d972d-156">Extraire hello [Office 365 + RemoteApp](remoteapp-o365.md) plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d972d-156">Check out hello [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="d972d-157">Consultez également nouvel article de hello, [comment toouse votre abonnement Office 365 avec Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="d972d-157">Also check out hello new article, [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="d972d-158">Notez que vous devez toolicense Office 365 ProPlus, Visio Professionnel et Project Pro séparément, ils ont chacun leur propre licence.</span><span class="sxs-lookup"><span data-stu-id="d972d-158">Note that you need toolicense Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="d972d-159">Microsoft Office Professionnel Plus 2013 (version d'évaluation uniquement)</span><span class="sxs-lookup"><span data-stu-id="d972d-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="d972d-160">Pendant la période d’évaluation gratuite de hello, vous pouvez tester le service hello avec l’image de hello Office 2013.</span><span class="sxs-lookup"><span data-stu-id="d972d-160">During hello free trial period, you can test hello service with hello Office 2013 image.</span></span>

<span data-ttu-id="d972d-161">Cette image est une extension de l’image de vanille hello et a hello les composants suivants de Microsoft Office 2013 Professionnel Plus installé par ailleurs toohello composants décrits dans l’image de Windows Server 2012 R2 hello :</span><span class="sxs-lookup"><span data-stu-id="d972d-161">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 2013 Professional Plus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="d972d-162">Access</span><span class="sxs-lookup"><span data-stu-id="d972d-162">Access</span></span>
* <span data-ttu-id="d972d-163">Excel</span><span class="sxs-lookup"><span data-stu-id="d972d-163">Excel</span></span>
* <span data-ttu-id="d972d-164">Lync</span><span class="sxs-lookup"><span data-stu-id="d972d-164">Lync</span></span>
* <span data-ttu-id="d972d-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="d972d-165">OneNote</span></span>
* <span data-ttu-id="d972d-166">OneDrive entreprise (Notez que l’agent de synchronisation hello n’est pas prise en charge pour une utilisation avec Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="d972d-166">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="d972d-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="d972d-167">Outlook</span></span>
* <span data-ttu-id="d972d-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d972d-168">PowerPoint</span></span>
* <span data-ttu-id="d972d-169">projet</span><span class="sxs-lookup"><span data-stu-id="d972d-169">Project</span></span>
* <span data-ttu-id="d972d-170">Visio</span><span class="sxs-lookup"><span data-stu-id="d972d-170">Visio</span></span>
* <span data-ttu-id="d972d-171">Word</span><span class="sxs-lookup"><span data-stu-id="d972d-171">Word</span></span>
* <span data-ttu-id="d972d-172">Outils de vérification linguistique Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="d972d-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d972d-173">**Informations légales :** cette image n’inclut pas de licence Microsoft Office et *ne peut pas être utilisée en production*.</span><span class="sxs-lookup"><span data-stu-id="d972d-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="d972d-174">image d’Office 2013 Professionnel Plus Hello est destinée uniquement à des fins d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="d972d-174">hello Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="d972d-175">Si vous souhaitez que les applications Office toouse dans Azure RemoteApp pour la production, vous avez besoin d’image de Office 365 ProPlus toouse hello.</span><span class="sxs-lookup"><span data-stu-id="d972d-175">If you want toouse Office apps in Azure RemoteApp for production, you need toouse hello Office 365 ProPlus image.</span></span> <span data-ttu-id="d972d-176">Pour plus d'informations sur la licence Office, consultez [Utilisation d'Office 365 avec Azure RemoteApp](remoteapp-o365.md)</span><span class="sxs-lookup"><span data-stu-id="d972d-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

