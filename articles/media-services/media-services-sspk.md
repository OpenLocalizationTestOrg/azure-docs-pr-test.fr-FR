---
title: "aaaLicensing Microsoft® Kit Smooth Streaming Client Porting Kit"
description: "Découvrez comment toolicensing hello Microsoft® Kit Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="f1925-103">Licence du kit de portage du client de diffusion en continu lisse Microsoft®</span><span class="sxs-lookup"><span data-stu-id="f1925-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="f1925-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f1925-104">Overview</span></span>
<span data-ttu-id="f1925-105">Microsoft Kit Smooth Streaming Client Porting Kit (**SSPK** en abrégé) est une implémentation de client de diffusion en continu lisse qui est optimisé toohelp incorporé les fabricants de périphériques, câble et les opérateurs mobiles, les fournisseurs de service de contenu, combiné les fabricants, éditeurs de logiciels indépendants (ISV), solution fournisseurs toocreate produits et services et de diffusion en continu de contenu de diffusion adaptative au format de diffusion en continu lisse.</span><span class="sxs-lookup"><span data-stu-id="f1925-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized toohelp embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers toocreate products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="f1925-106">SSPK est une implémentation d’indépendants appareil et la plateforme du client de diffusion en continu qui peut être déplacée par la plateforme et l’appareil de tooany Licencié hello.</span><span class="sxs-lookup"><span data-stu-id="f1925-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by hello licensee tooany device and platform.</span></span> 

<span data-ttu-id="f1925-107">Inclus ci-dessous est une architecture de haut niveau et zone de IIS Kit Smooth Streaming Porting Kit hello en œuvre Smooth Streaming Client fourni par Microsoft et inclut tous les hello core une logique pour la lecture du contenu de diffusion en continu lisse.</span><span class="sxs-lookup"><span data-stu-id="f1925-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is hello Smooth Streaming Client implementation provided by Microsoft and includes all hello core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="f1925-108">Il est ensuite transféré par des partenaires pour un périphérique ou une plate-forme, grâce à l’implémentation des interfaces appropriées.</span><span class="sxs-lookup"><span data-stu-id="f1925-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="f1925-110">Description</span><span class="sxs-lookup"><span data-stu-id="f1925-110">Description</span></span>
<span data-ttu-id="f1925-111">SSPK est concédé sous licence selon des conditions représentant une excellente valeur pour l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="f1925-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="f1925-112">Licence SSPK fournit l’industrie hello avec :</span><span class="sxs-lookup"><span data-stu-id="f1925-112">SSPK license provides hello industry with:</span></span>

* <span data-ttu-id="f1925-113">Source de kit de portage Smooth Streaming en C++</span><span class="sxs-lookup"><span data-stu-id="f1925-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="f1925-114">implémente la fonctionnalité Client Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="f1925-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="f1925-115">ajoute une analyse de format, heuristique, une logique de mise en mémoire tampon, etc.</span><span class="sxs-lookup"><span data-stu-id="f1925-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="f1925-116">API d’application joueur</span><span class="sxs-lookup"><span data-stu-id="f1925-116">Player application APIs</span></span> 
  * <span data-ttu-id="f1925-117">interfaces de programmation pour une interaction avec une application de lecteur multimédia</span><span class="sxs-lookup"><span data-stu-id="f1925-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="f1925-118">Interface de couche d’abstraction de plateforme (PAL)</span><span class="sxs-lookup"><span data-stu-id="f1925-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="f1925-119">interfaces de programmation pour l’interaction avec le système d’exploitation hello (threads, sockets)</span><span class="sxs-lookup"><span data-stu-id="f1925-119">programming interfaces for interaction with hello operating system (threads, sockets)</span></span>
* <span data-ttu-id="f1925-120">Interface de couche d’abstraction matérielle</span><span class="sxs-lookup"><span data-stu-id="f1925-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="f1925-121">interfaces de programmation pour l‘interaction avec les décodeurs A/V matériels (décodage, rendu)</span><span class="sxs-lookup"><span data-stu-id="f1925-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="f1925-122">Interface de gestion de droits numériques (Digital Rights Management - DRM)</span><span class="sxs-lookup"><span data-stu-id="f1925-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="f1925-123">interfaces de programmation pour la gestion des DRM via hello couche d’Abstraction de gestion des droits numériques (DAL)</span><span class="sxs-lookup"><span data-stu-id="f1925-123">programming interfaces for handling DRM through hello DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="f1925-124">Le kit de portage PlayReady Microsoft est fourni séparément, mais s’intègre via cette interface.</span><span class="sxs-lookup"><span data-stu-id="f1925-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="f1925-125">Pour plus d‘informations sur les licences pour appareil Microsoft PlayReady cliquez [ici](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="f1925-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="f1925-126">Échantillons de l’implémentation</span><span class="sxs-lookup"><span data-stu-id="f1925-126">Implementation samples</span></span> 
  * <span data-ttu-id="f1925-127">exemple d‘implémentation PAL pour Linux</span><span class="sxs-lookup"><span data-stu-id="f1925-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="f1925-128">exemple d‘implémentation HAL pour GStreamer</span><span class="sxs-lookup"><span data-stu-id="f1925-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="f1925-129">Options de licence</span><span class="sxs-lookup"><span data-stu-id="f1925-129">Licensing Options</span></span>
<span data-ttu-id="f1925-130">Microsoft Kit Smooth Streaming Client Porting Kit est effectuée toolicensees disponible sous deux contrats de licence distinctes : une pour le développement Client de diffusion en continu lisse intérimaire des produits et une autre pour la distribution de Smooth Streaming Client Final produits tooend par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f1925-130">Microsoft Smooth Streaming Client Porting Kit is made available toolicensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products tooend users.</span></span>

* <span data-ttu-id="f1925-131">Pour chipset fabricants, intégrateurs système ou logiciels indépendant (ISV) qui ont besoin d’un portage de code source kit toodevelop intérimaire produits, une Microsoft Kit Smooth Streaming Client Porting Kit **licence temporaire** doit être exécutée.</span><span class="sxs-lookup"><span data-stu-id="f1925-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit toodevelop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="f1925-132">Pour les fabricants de périphériques ou les éditeurs de logiciels indépendants qui ont besoin des droits de distribution pour les utilisateurs tooend Smooth Streaming Client Final produits, hello Microsoft Kit Smooth Streaming Client Porting Kit **licence du produit Final** doit être exécutée.</span><span class="sxs-lookup"><span data-stu-id="f1925-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products tooend users, hello Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="f1925-133">Licence de produit intermédiaire pour le kit Microsoft Smooth Streaming Client Porting</span><span class="sxs-lookup"><span data-stu-id="f1925-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="f1925-134">Sous cette licence, Microsoft propose un kit Smooth Streaming Client Porting Kit hello toodevelop de droits de propriété intellectuelle et distribuer les licenciés d’appareil Client de diffusion en continu lisse intérimaire des produits tooother Kit Smooth Streaming Client Porting Kit qui distribuer Smooth Streaming Client Final produits.</span><span class="sxs-lookup"><span data-stu-id="f1925-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and hello necessary intellectual property rights toodevelop and distribute Smooth Streaming Client Interim Products tooother Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="f1925-135">Structure des frais</span><span class="sxs-lookup"><span data-stu-id="f1925-135">Fee structure</span></span>
<span data-ttu-id="f1925-136">Frais de licence de 50 000 dollars US fournit un accès toohello Kit Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="f1925-136">A U.S. $50,000 one-time license fee provides access toohello Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="f1925-137">Licence de produit final pour le kit de portage Smooth Streaming client</span><span class="sxs-lookup"><span data-stu-id="f1925-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="f1925-138">Sous cette licence, Microsoft propose nécessaires tooreceive de droits de propriété intellectuelle Client de diffusion en continu lisse intérimaire des produits d’autres licenciés du Kit Smooth Streaming Client Porting Kit et le toodistribute marquée Smooth finale de Client One-Boot de diffusion en continu Utilisateurs tooend de produits.</span><span class="sxs-lookup"><span data-stu-id="f1925-138">Under this license, Microsoft offers all necessary intellectual property rights tooreceive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and toodistribute company-branded Smooth Streaming Client Final Products tooend users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="f1925-139">Structure des frais</span><span class="sxs-lookup"><span data-stu-id="f1925-139">Fee structure</span></span>
<span data-ttu-id="f1925-140">Hello Smooth Streaming Client finale du produit est proposée sous un modèle de droits d’auteur en tant que sous :</span><span class="sxs-lookup"><span data-stu-id="f1925-140">hello Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="f1925-141">0,10 $ par implémentation de périphérique expédiés</span><span class="sxs-lookup"><span data-stu-id="f1925-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="f1925-142">droits d’auteur Hello est limitée à 50 000 dollars chaque année</span><span class="sxs-lookup"><span data-stu-id="f1925-142">hello royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="f1925-143">Pas de redevance pour les 10 000 premières implémentations de périphérique chaque année</span><span class="sxs-lookup"><span data-stu-id="f1925-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="f1925-144">Procédure d’achat de licence et accès à SSPK</span><span class="sxs-lookup"><span data-stu-id="f1925-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="f1925-145">Veuillez envoyer un e-mail [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) pour toute requête relative aux licences des requêtes.</span><span class="sxs-lookup"><span data-stu-id="f1925-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="f1925-146">Hello [portal de Distribution de SSPK](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) est accessible tooregistered détenteurs d’une licence temporaire.</span><span class="sxs-lookup"><span data-stu-id="f1925-146">hello [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible tooregistered Interim licensees.</span></span>

<span data-ttu-id="f1925-147">Licenciés intérimaire et SSPK Final peuvent soumettre des questions techniques trop[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f1925-147">Interim and Final SSPK licensees can submit technical questions too[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="f1925-148">Les titulaires de licence d’accord de produit intermédiaire de client de diffusion lisse Microsoft</span><span class="sxs-lookup"><span data-stu-id="f1925-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="f1925-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="f1925-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="f1925-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="f1925-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="f1925-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="f1925-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="f1925-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="f1925-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="f1925-153">Alticast Corporation</span></span>
* <span data-ttu-id="f1925-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="f1925-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="f1925-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="f1925-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-157">Cavium, Inc.</span></span>
* <span data-ttu-id="f1925-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="f1925-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="f1925-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-159">Enseo, Inc.</span></span>
* <span data-ttu-id="f1925-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="f1925-160">Fluendo S.A.</span></span>
* <span data-ttu-id="f1925-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="f1925-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="f1925-162">Infomir GMBH</span></span>
* <span data-ttu-id="f1925-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="f1925-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="f1925-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="f1925-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="f1925-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="f1925-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-166">MediaTek Inc.</span></span>
* <span data-ttu-id="f1925-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="f1925-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="f1925-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="f1925-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="f1925-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="f1925-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="f1925-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="f1925-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="f1925-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="f1925-172">SoftAtHome</span></span>
* <span data-ttu-id="f1925-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="f1925-173">Sony Corporation</span></span>
* <span data-ttu-id="f1925-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="f1925-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="f1925-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="f1925-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="f1925-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="f1925-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="f1925-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="f1925-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="f1925-180">Titulaires de licence d’accord de produit final de client de diffusion lisse Microsoft</span><span class="sxs-lookup"><span data-stu-id="f1925-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="f1925-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="f1925-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="f1925-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="f1925-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="f1925-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="f1925-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="f1925-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="f1925-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="f1925-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="f1925-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="f1925-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="f1925-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="f1925-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="f1925-189">VE TİC.</span></span> <span data-ttu-id="f1925-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="f1925-190">A.Ş</span></span>
* <span data-ttu-id="f1925-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="f1925-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="f1925-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="f1925-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="f1925-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="f1925-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="f1925-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="f1925-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="f1925-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-196">Enseo, Inc.</span></span>
* <span data-ttu-id="f1925-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="f1925-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="f1925-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="f1925-198">Fluendo S.A.</span></span>
* <span data-ttu-id="f1925-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="f1925-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="f1925-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="f1925-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="f1925-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="f1925-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="f1925-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="f1925-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="f1925-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="f1925-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="f1925-205">Infomir GMBH</span></span>
* <span data-ttu-id="f1925-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="f1925-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="f1925-207">KDDI Corporation</span></span>
* <span data-ttu-id="f1925-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="f1925-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="f1925-209">Orange SA</span></span>
* <span data-ttu-id="f1925-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="f1925-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="f1925-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="f1925-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="f1925-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="f1925-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="f1925-213">Shenzhen Jiuzhou Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="f1925-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="f1925-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="f1925-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="f1925-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="f1925-216">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="f1925-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="f1925-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="f1925-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="f1925-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="f1925-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="f1925-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="f1925-219">SoftAtHome</span></span>
* <span data-ttu-id="f1925-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="f1925-220">Sony Corporation</span></span>
* <span data-ttu-id="f1925-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="f1925-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="f1925-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="f1925-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="f1925-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="f1925-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="f1925-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="f1925-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="f1925-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="f1925-226">Universal Media Corporation /Slovaquie/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="f1925-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="f1925-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="f1925-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="f1925-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="f1925-228">Wistron Corporation</span></span>
* <span data-ttu-id="f1925-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="f1925-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="f1925-230">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="f1925-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f1925-231">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="f1925-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

