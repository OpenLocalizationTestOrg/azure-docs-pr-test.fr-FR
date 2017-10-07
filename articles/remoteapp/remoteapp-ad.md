---
title: aaaAzure AD + Active Directory requise pour Azure RemoteApp | Documents Microsoft
description: "Découvrez comment tooset des toowork d’Active Directory avec Azure RemoteApp."
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
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="7fa06-103">Configuration requise d’Azure AD et d’Active Directory pour Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="7fa06-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7fa06-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="7fa06-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7fa06-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7fa06-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7fa06-106">Pour votre collection de hybride Azure RemoteApp ou pour une collection de cloud que vous souhaitez toofederate à l’aide d’AD Connect, toodo, hello éléments suivants sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="7fa06-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want toofederate using AD Connect, you need toodo hello following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="7fa06-107">Connexion à Azure AD et Active Directory</span><span class="sxs-lookup"><span data-stu-id="7fa06-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="7fa06-108">Si vous souhaitez tooconnect votre locataire Azure AD et les environnements Active Directory local, utilisez Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7fa06-108">If you want tooconnect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="7fa06-109">Il vous faudra uniquement [4 clics](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello deux répertoires.</span><span class="sxs-lookup"><span data-stu-id="7fa06-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello two directories.</span></span>

<span data-ttu-id="7fa06-110">Remarque : la synchronisation d’annuaires est requise pour les collections hybride.</span><span class="sxs-lookup"><span data-stu-id="7fa06-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="7fa06-111">Vérifiez que votre @domain.com correspond</span><span class="sxs-lookup"><span data-stu-id="7fa06-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="7fa06-112">Avant de commencer, assurez-vous que hello UPN votre forêt locale correspondances le suffixe hello de votre domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7fa06-112">Before you get started, make sure that hello UPN for your on-premises forest matches hello suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="7fa06-113">Après avoir configuré hello domaine suffixe dans Azure AD, tous les utilisateurs qui se connectent à Azure RemoteApp seront connectez-vous en tant que « utilisateur @<hello suffix you set up>. »</span><span class="sxs-lookup"><span data-stu-id="7fa06-113">After you set up hello UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<hello suffix you set up>."</span></span> <span data-ttu-id="7fa06-114">Assurez-vous que les utilisateurs peuvent également se connecter avec hello même user@suffix dans le domaine local de hello.</span><span class="sxs-lookup"><span data-stu-id="7fa06-114">Make sure that users can also log in with hello same user@suffix into hello on-premises domain.</span></span> <span data-ttu-id="7fa06-115">Dans certains cas vous pouvez configurer un nom de domaine dans Azure AD lors de la spécification d’un suffixe de domaine différent pour hello utilisateur localement.</span><span class="sxs-lookup"><span data-stu-id="7fa06-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for hello user on-prem.</span></span> <span data-ttu-id="7fa06-116">Dans ce cas, vos utilisateurs ne sont pas être en mesure de tooconnect tooany appartenant au domaine ordinateurs ou des ressources via Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="7fa06-116">In this case, your users won't be able tooconnect tooany domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="7fa06-117">Par exemple, si vous configurez votre suffixe UPN dans AAD contoso.com, mais certains utilisateurs sur site et d’Active Directory sont toolog configuré avec @contoso.uk, ces utilisateurs ne seront pas connectez-vous toocorrectly en mesure de hello collection de ARA.</span><span class="sxs-lookup"><span data-stu-id="7fa06-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured toolog in with @contoso.uk, then those users will not be able toocorrectly log into hello ARA collection.</span></span> <span data-ttu-id="7fa06-118">Les utilisateurs de le QU'UPN dans AAD et Active Directory doit être même hello pour possible de toobe connexion hello »</span><span class="sxs-lookup"><span data-stu-id="7fa06-118">Users UPN in AAD and AD must be hello same for hello login toobe possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="7fa06-119">Création d’objets pour Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="7fa06-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="7fa06-120">Vous devez également hello toocreate objets d’Active Directory locaux suivants :</span><span class="sxs-lookup"><span data-stu-id="7fa06-120">You also need toocreate hello following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="7fa06-121">Un compte tooprovide accès toodomain ressources du service pour les programmes RemoteApp en joignant le domaine de postes de travail points de terminaison toohello local.</span><span class="sxs-lookup"><span data-stu-id="7fa06-121">A service account tooprovide access toodomain resources for RemoteApp programs by joining RDSH end points toohello on-premises domain.</span></span>
* <span data-ttu-id="7fa06-122">Une unité d’organisation (UO) toocontain RemoteApp ordinateur les objets.</span><span class="sxs-lookup"><span data-stu-id="7fa06-122">An Organizational Unit (OU) toocontain RemoteApp machine objects.</span></span> <span data-ttu-id="7fa06-123">Utilisation de l’unité d’organisation de hello est recommandé (mais n’est pas obligatoire) tooisolate hello comptes et les stratégies que vous utiliserez avec RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="7fa06-123">Use of hello OU is recommended (but not required) tooisolate hello accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="7fa06-124">Vous avez besoin de ces deux objets lorsque vous créez votre collection RemoteApp, soyez sûr toodo ces étapes tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="7fa06-124">You need both of these objects when you create your RemoteApp collection, so be sure toodo these steps first.</span></span>

