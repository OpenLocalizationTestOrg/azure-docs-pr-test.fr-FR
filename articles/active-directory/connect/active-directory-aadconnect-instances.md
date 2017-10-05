---
title: 'Azure AD Connect : Instances de service Sync | Microsoft Docs'
description: "Cette page décrit des considérations spéciales relatives aux instances d’Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e8321c3d16253226a5931cacbce6fa5d50b697bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="672f9-103">Azure AD Connect : considérations spéciales relatives aux instances</span><span class="sxs-lookup"><span data-stu-id="672f9-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="672f9-104">Azure AD Connect est couramment utilisé avec l’instance mondiale d’Azure AD et Office 365.</span><span class="sxs-lookup"><span data-stu-id="672f9-104">Azure AD Connect is most commonly used with the world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="672f9-105">Mais il existe également d’autres instances, qui ont des exigences différentes en matière d’URL et autres considérations spéciales.</span><span class="sxs-lookup"><span data-stu-id="672f9-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="672f9-106">Microsoft Cloud Allemagne</span><span class="sxs-lookup"><span data-stu-id="672f9-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="672f9-107">[Microsoft Cloud Allemagne](http://www.microsoft.de/cloud-deutschland) est un cloud souverain géré par un client allemand approuvé dans le domaine des données.</span><span class="sxs-lookup"><span data-stu-id="672f9-107">The [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="672f9-108">URL à ouvrir dans le serveur proxy</span><span class="sxs-lookup"><span data-stu-id="672f9-108">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="672f9-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="672f9-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="672f9-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="672f9-110">\*.windows.net</span></span> |
| <span data-ttu-id="672f9-111">+ Listes de révocation de certificat</span><span class="sxs-lookup"><span data-stu-id="672f9-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="672f9-112">Quand vous vous connectez à votre locataire Azure AD, vous devez utiliser un compte du domaine onmicrosoft.de.</span><span class="sxs-lookup"><span data-stu-id="672f9-112">When you sign in to your Azure AD tenant, you must use an account in the onmicrosoft.de domain.</span></span>

<span data-ttu-id="672f9-113">Fonctionnalités actuellement absentes de Microsoft Cloud Allemagne :</span><span class="sxs-lookup"><span data-stu-id="672f9-113">Features currently not present in the Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="672f9-114">**Azure AD Connect Health** n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="672f9-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="672f9-115">Les **mises à jour automatiques** ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="672f9-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="672f9-116">L’**écriture différée de mot de passe** est disponible en préversion avec Azure AD Connect version 1.1.570.0 et ultérieures.</span><span class="sxs-lookup"><span data-stu-id="672f9-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="672f9-117">Les autres services Azure AD Premium ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="672f9-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="672f9-118">Cloud Microsoft Azure Government</span><span class="sxs-lookup"><span data-stu-id="672f9-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="672f9-119">Le [cloud Microsoft Azure Government](https://azure.microsoft.com/features/gov/) est un cloud du gouvernement des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="672f9-119">The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="672f9-120">Ce cloud a été pris en charge par des versions antérieures de DirSync.</span><span class="sxs-lookup"><span data-stu-id="672f9-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="672f9-121">À partir de la build 1.1.180 d’Azure AD Connect, la nouvelle génération du cloud est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="672f9-121">From build 1.1.180 of Azure AD Connect, the next generation of the cloud is supported.</span></span> <span data-ttu-id="672f9-122">Cette génération utilise des points de terminaison États-Unis uniquement et a sa propre liste d’URL à ouvrir dans votre serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="672f9-122">This generation is using US-only based endpoints and have a different list of URLs to open in your proxy server.</span></span>

| <span data-ttu-id="672f9-123">URL à ouvrir dans le serveur proxy</span><span class="sxs-lookup"><span data-stu-id="672f9-123">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="672f9-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="672f9-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="672f9-125">\*.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="672f9-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="672f9-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="672f9-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="672f9-127">+ Listes de révocation de certificat</span><span class="sxs-lookup"><span data-stu-id="672f9-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="672f9-128">Azure AD Connect ne peut pas détecter automatiquement que votre locataire Azure AD se trouve dans le cloud Government.</span><span class="sxs-lookup"><span data-stu-id="672f9-128">Azure AD Connect is not able to automatically detect that your Azure AD tenant is located in the Government cloud.</span></span> <span data-ttu-id="672f9-129">Au lieu de cela, vous devez effectuer les actions suivantes lorsque vous installez Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="672f9-129">Instead you need to take the following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="672f9-130">Lancez l’installation d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="672f9-130">Start the Azure AD Connect installation.</span></span>
2. <span data-ttu-id="672f9-131">Quand vous voyez apparaître la première page où vous êtes censé accepter le CLUF, ne poursuivez pas, mais laissez l’Assistant Installation en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="672f9-131">When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.</span></span>
3. <span data-ttu-id="672f9-132">Lancez regedit et modifiez la clé de registre de la valeur `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` à la valeur `2`.</span><span class="sxs-lookup"><span data-stu-id="672f9-132">Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `2`.</span></span>
4. <span data-ttu-id="672f9-133">Revenez à l’Assistant Installation d’Azure AD Connect, acceptez le CLUF et continuez.</span><span class="sxs-lookup"><span data-stu-id="672f9-133">Go back to the Azure AD Connect installation wizard, accept the EULA, and continue.</span></span> <span data-ttu-id="672f9-134">Pendant l’installation, veillez à utiliser le chemin d’accès d’installation de la **configuration personnalisée** (et non l’installation rapide).</span><span class="sxs-lookup"><span data-stu-id="672f9-134">During installation, make sure to use the **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="672f9-135">Puis continuez l’installation normalement.</span><span class="sxs-lookup"><span data-stu-id="672f9-135">Then continue the installation as usual.</span></span>

<span data-ttu-id="672f9-136">Fonctionnalités actuellement absentes du cloud Microsoft Azure Government :</span><span class="sxs-lookup"><span data-stu-id="672f9-136">Features currently not present in the Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="672f9-137">**Azure AD Connect Health** n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="672f9-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="672f9-138">Les **mises à jour automatiques** ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="672f9-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="672f9-139">L’**écriture différée de mot de passe** est disponible en préversion avec Azure AD Connect version 1.1.570.0 et ultérieures.</span><span class="sxs-lookup"><span data-stu-id="672f9-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="672f9-140">Les autres services Azure AD Premium ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="672f9-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="672f9-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="672f9-141">Next steps</span></span>
<span data-ttu-id="672f9-142">En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="672f9-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
