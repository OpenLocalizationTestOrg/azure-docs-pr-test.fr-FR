---
title: "Configuration requise d’Azure AD et d’Active Directory pour Azure RemoteApp | Microsoft Docs"
description: "Découvrez comment configurer Active Directory pour l'utiliser avec Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="db978-103">Configuration requise d’Azure AD et d’Active Directory pour Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="db978-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="db978-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="db978-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="db978-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="db978-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="db978-106">Si vous souhaitez fédérer une collection hybride RemoteApp Azure ou une collection cloud à l’aide d’AD Connect, vous devez procéder ainsi.</span><span class="sxs-lookup"><span data-stu-id="db978-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want to federate using AD Connect, you need to do the following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="db978-107">Connexion à Azure AD et Active Directory</span><span class="sxs-lookup"><span data-stu-id="db978-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="db978-108">Si vous souhaitez connecter votre locataire Azure AD et vos environnements Active Directory locaux, utilisez AD Connect.</span><span class="sxs-lookup"><span data-stu-id="db978-108">If you want to connect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="db978-109">Il vous faudra simplement [cliquer 4 fois](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) pour connecter les deux annuaires.</span><span class="sxs-lookup"><span data-stu-id="db978-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) to connect the two directories.</span></span>

<span data-ttu-id="db978-110">Remarque : la synchronisation d’annuaires est requise pour les collections hybride.</span><span class="sxs-lookup"><span data-stu-id="db978-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="db978-111">Vérifiez que votre @domain.com correspond</span><span class="sxs-lookup"><span data-stu-id="db978-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="db978-112">Avant de commencer, assurez-vous que l’UPN de votre forêt locale correspond au suffixe de votre domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="db978-112">Before you get started, make sure that the UPN for your on-premises forest matches the suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="db978-113">Une fois que vous avez configuré le suffixe du domaine UPN dans Azure AD, tous les utilisateurs se connectant dans Azure RemoteApp sont connectés en tant que « utilisateur@<the suffix you set up> ».</span><span class="sxs-lookup"><span data-stu-id="db978-113">After you set up the UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<the suffix you set up>."</span></span> <span data-ttu-id="db978-114">Assurez-vous que les utilisateurs peuvent également ouvrir une session avec le même user@suffix dans le domaine local.</span><span class="sxs-lookup"><span data-stu-id="db978-114">Make sure that users can also log in with the same user@suffix into the on-premises domain.</span></span> <span data-ttu-id="db978-115">Dans certains cas vous pouvez configurer un nom de domaine dans Azure AD lors de la spécification d’un suffixe de domaine différent pour l’utilisateur local.</span><span class="sxs-lookup"><span data-stu-id="db978-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for the user on-prem.</span></span> <span data-ttu-id="db978-116">Dans ce cas, vos utilisateurs ne peuvent plus se connecter à des ordinateurs ou des ressources appartenant à un domaine via Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="db978-116">In this case, your users won't be able to connect to any domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="db978-117">Par exemple, si vous configurez votre suffixe de domaine UPN dans AAD en tant que contoso.com, mais que certains utilisateurs locaux/AD sont configurés pour se connecter avec @contoso.uk, ces utilisateurs ne pourront pas se connecter correctement à la collection ARA.</span><span class="sxs-lookup"><span data-stu-id="db978-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured to log in with @contoso.uk, then those users will not be able to correctly log into the ARA collection.</span></span> <span data-ttu-id="db978-118">L’UPN des utilisateurs doit être le même pour AAD et AD pour permettre la connexion.</span><span class="sxs-lookup"><span data-stu-id="db978-118">Users UPN in AAD and AD must be the same for the login to be possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="db978-119">Création d’objets pour Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="db978-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="db978-120">Vous devez également créer les objets Active Directory locaux suivants :</span><span class="sxs-lookup"><span data-stu-id="db978-120">You also need to create the following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="db978-121">Un compte de service afin de fournir l'accès aux ressources du domaine pour les programmes RemoteApp, en rattachant des points de terminaison RDSH au domaine local.</span><span class="sxs-lookup"><span data-stu-id="db978-121">A service account to provide access to domain resources for RemoteApp programs by joining RDSH end points to the on-premises domain.</span></span>
* <span data-ttu-id="db978-122">Une unité d'organisation pour contenir les objets ordinateur RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="db978-122">An Organizational Unit (OU) to contain RemoteApp machine objects.</span></span> <span data-ttu-id="db978-123">L'utilisation de l'unité d'organisation est recommandée (mais pas obligatoire) pour isoler les comptes et les stratégies que vous utiliserez avec RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="db978-123">Use of the OU is recommended (but not required) to isolate the accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="db978-124">Vous avez besoin de ces deux objets lorsque vous créez votre collection RemoteApp ; veuillez donc vous assurer d’avoir déjà effectué ces étapes.</span><span class="sxs-lookup"><span data-stu-id="db978-124">You need both of these objects when you create your RemoteApp collection, so be sure to do these steps first.</span></span>

