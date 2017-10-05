---
title: Attribution de licences pour Azure MFA| Microsoft Docs
description: "Découvrez comment attribuer des licences pour Microsoft Azure Multi-Factor Authentication"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ROBOTS: NOINDEX
ms.openlocfilehash: 45522bf526c4aeab1d6ccc8891a55a0436ff9320
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-to-users"></a><span data-ttu-id="3df05-103">Attribution d’une licence Azure MFA, Azure AD Premium ou Enterprise Mobility aux utilisateurs</span><span class="sxs-lookup"><span data-stu-id="3df05-103">Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license to users</span></span>
<span data-ttu-id="3df05-104">Si vous avez acheté des licences Azure MFA, Azure AD Premium ou Enterprise Mobility Suite, il est inutile de créer un fournisseur Multi-Factor Auth.</span><span class="sxs-lookup"><span data-stu-id="3df05-104">If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need to create a Multi-Factor Auth provider.</span></span> <span data-ttu-id="3df05-105">Une fois que vous avez attribué des licences à vos utilisateurs, vous pouvez commencer à les activer pour l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="3df05-105">Once you assign the licenses to your users, you can begin enabling them for MFA.</span></span>

## <a name="to-assign-a-license"></a><span data-ttu-id="3df05-106">Pour attribuer une licence</span><span class="sxs-lookup"><span data-stu-id="3df05-106">To assign a license</span></span>
1. <span data-ttu-id="3df05-107">Connectez-vous en tant qu’administrateur au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3df05-107">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="3df05-108">Sélectionnez **Active Directory**à gauche.</span><span class="sxs-lookup"><span data-stu-id="3df05-108">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="3df05-109">Sur la page Active Directory, double-cliquez sur le répertoire qui contient les utilisateurs que vous souhaitez activer.</span><span class="sxs-lookup"><span data-stu-id="3df05-109">On the Active Directory page, double-click the directory that has the users you wish to enable.</span></span>
4. <span data-ttu-id="3df05-110">En haut de la page du répertoire, sélectionnez **Licences**.</span><span class="sxs-lookup"><span data-stu-id="3df05-110">At the top of the directory page, select **Licenses**.</span></span>
   <span data-ttu-id="3df05-111">![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span><span class="sxs-lookup"><span data-stu-id="3df05-111">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span></span>
5. <span data-ttu-id="3df05-112">Sur la page Licences, sélectionnez **Azure Multi-Factor Authentication**, **Active Directory Premium** ou **Enterprise Mobility Suite**.</span><span class="sxs-lookup"><span data-stu-id="3df05-112">On the Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.</span></span>  <span data-ttu-id="3df05-113">Si vous ne disposez que d’une licence, celle-ci doit normalement être sélectionnée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="3df05-113">If you only have one, then it should be selected automatically.</span></span>
6. <span data-ttu-id="3df05-114">En bas de cette page, cliquez sur **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="3df05-114">At the bottom of the page, click **Assign**.</span></span>
   <span data-ttu-id="3df05-115">![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span><span class="sxs-lookup"><span data-stu-id="3df05-115">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span></span>
7. <span data-ttu-id="3df05-116">Dans la zone qui s’affiche, cliquez en regard des utilisateurs ou groupes auxquels vous souhaitez attribuer des licences.</span><span class="sxs-lookup"><span data-stu-id="3df05-116">In the box that comes up, click next to the users or groups you want to assign licenses to.</span></span>  <span data-ttu-id="3df05-117">Une coche verte doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="3df05-117">You should see a green check mark appear.</span></span>
8. <span data-ttu-id="3df05-118">Cliquez sur la coche pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="3df05-118">Click the check mark icon to save the changes.</span></span>
   <span data-ttu-id="3df05-119">![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span><span class="sxs-lookup"><span data-stu-id="3df05-119">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span></span>
9. <span data-ttu-id="3df05-120">Vous devriez voir un message indiquant le nombre de licences qui ont été attribuées et le nombre d’échecs, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="3df05-120">You should see a message saying how many licenses were assigned and how many may have failed.</span></span>  <span data-ttu-id="3df05-121">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3df05-121">Click **Ok**.</span></span>
   <span data-ttu-id="3df05-122">![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span><span class="sxs-lookup"><span data-stu-id="3df05-122">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3df05-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3df05-123">Next steps</span></span>

- <span data-ttu-id="3df05-124">Pour plus d’informations, consultez [Qu’est-ce que la licence Microsoft Azure Active Directory ?](../active-directory/active-directory-licensing-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="3df05-124">For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)</span></span>
