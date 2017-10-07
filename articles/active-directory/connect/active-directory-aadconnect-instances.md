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
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="ef9e7-103">Azure AD Connect : considérations spéciales relatives aux instances</span><span class="sxs-lookup"><span data-stu-id="ef9e7-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="ef9e7-104">Azure AD Connect est plus couramment utilisé avec hello world-wide instance de Azure AD et Office 365.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-104">Azure AD Connect is most commonly used with hello world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="ef9e7-105">Mais il existe également d’autres instances, qui ont des exigences différentes en matière d’URL et autres considérations spéciales.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="ef9e7-106">Microsoft Cloud Allemagne</span><span class="sxs-lookup"><span data-stu-id="ef9e7-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="ef9e7-107">Hello [Microsoft Cloud Allemagne](http://www.microsoft.de/cloud-deutschland) est un cloud souverain exploité par un tiers de confiance de données en allemand.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-107">hello [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="ef9e7-108">Tooopen URL de serveur proxy</span><span class="sxs-lookup"><span data-stu-id="ef9e7-108">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="ef9e7-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="ef9e7-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="ef9e7-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="ef9e7-110">\*.windows.net</span></span> |
| <span data-ttu-id="ef9e7-111">+ Listes de révocation de certificat</span><span class="sxs-lookup"><span data-stu-id="ef9e7-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="ef9e7-112">Lorsque vous vous connectez dans le locataire Azure AD de tooyour, vous devez utiliser un compte dans le domaine de onmicrosoft.de hello.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-112">When you sign in tooyour Azure AD tenant, you must use an account in hello onmicrosoft.de domain.</span></span>

<span data-ttu-id="ef9e7-113">Fonctionnalités qui ne sont pas présentes dans hello Microsoft Cloud Allemagne :</span><span class="sxs-lookup"><span data-stu-id="ef9e7-113">Features currently not present in hello Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="ef9e7-114">**Azure AD Connect Health** n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="ef9e7-115">Les **mises à jour automatiques** ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="ef9e7-116">L’**écriture différée de mot de passe** est disponible en préversion avec Azure AD Connect version 1.1.570.0 et ultérieures.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="ef9e7-117">Les autres services Azure AD Premium ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="ef9e7-118">Cloud Microsoft Azure Government</span><span class="sxs-lookup"><span data-stu-id="ef9e7-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="ef9e7-119">Hello [cloud de Microsoft Azure Government](https://azure.microsoft.com/features/gov/) est un cloud pour le gouvernement des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-119">hello [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="ef9e7-120">Ce cloud a été pris en charge par des versions antérieures de DirSync.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="ef9e7-121">À partir de la build 1.1.180 d’Azure AD Connect, hello nouvelle génération de cloud de hello est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-121">From build 1.1.180 of Azure AD Connect, hello next generation of hello cloud is supported.</span></span> <span data-ttu-id="ef9e7-122">Cette génération à l’aide de points de terminaison en fonction des États-Unis uniquement et avoir une autre liste de tooopen de l’URL de votre serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-122">This generation is using US-only based endpoints and have a different list of URLs tooopen in your proxy server.</span></span>

| <span data-ttu-id="ef9e7-123">Tooopen URL de serveur proxy</span><span class="sxs-lookup"><span data-stu-id="ef9e7-123">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="ef9e7-124">\**.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ef9e7-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="ef9e7-125">\*.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="ef9e7-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="ef9e7-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ef9e7-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="ef9e7-127">+ Listes de révocation de certificat</span><span class="sxs-lookup"><span data-stu-id="ef9e7-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="ef9e7-128">Azure AD Connect n’est pas en mesure de détecter les tooautomatically que votre client Azure AD se trouve dans le cloud de gouvernement hello.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-128">Azure AD Connect is not able tooautomatically detect that your Azure AD tenant is located in hello Government cloud.</span></span> <span data-ttu-id="ef9e7-129">Au lieu de cela, vous devez hello tootake suivant des actions lorsque vous installez Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-129">Instead you need tootake hello following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="ef9e7-130">Démarrer l’installation d’Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-130">Start hello Azure AD Connect installation.</span></span>
2. <span data-ttu-id="ef9e7-131">Lorsque vous voyez hello première page où vous êtes supposé tooaccept hello CLUF, ne continuez pas, mais laissez l’Assistant installation de hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-131">When you see hello first page where you are supposed tooaccept hello EULA, do not continue but leave hello installation wizard running.</span></span>
3. <span data-ttu-id="ef9e7-132">Démarrez regedit et modifier la clé de Registre hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello valeur `2`.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-132">Start regedit and change hello registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello value `2`.</span></span>
4. <span data-ttu-id="ef9e7-133">Assistant d’installation toohello Azure AD Connect revenir en arrière, accepter hello CLUF et continuer.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-133">Go back toohello Azure AD Connect installation wizard, accept hello EULA, and continue.</span></span> <span data-ttu-id="ef9e7-134">Pendant l’installation, assurez-vous que toouse hello **configuration personnalisée** chemin d’accès de l’installation (et non l’installation Express).</span><span class="sxs-lookup"><span data-stu-id="ef9e7-134">During installation, make sure toouse hello **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="ef9e7-135">Poursuivez les installation Bonjour comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-135">Then continue hello installation as usual.</span></span>

<span data-ttu-id="ef9e7-136">Fonctionnalités qui ne sont pas présentes dans le cloud de Microsoft Azure Government hello :</span><span class="sxs-lookup"><span data-stu-id="ef9e7-136">Features currently not present in hello Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="ef9e7-137">**Azure AD Connect Health** n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="ef9e7-138">Les **mises à jour automatiques** ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="ef9e7-139">L’**écriture différée de mot de passe** est disponible en préversion avec Azure AD Connect version 1.1.570.0 et ultérieures.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="ef9e7-140">Les autres services Azure AD Premium ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="ef9e7-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef9e7-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef9e7-141">Next steps</span></span>
<span data-ttu-id="ef9e7-142">En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="ef9e7-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
