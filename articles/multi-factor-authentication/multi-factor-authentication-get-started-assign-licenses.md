---
title: "icenses aaaAssign pour l’authentification Multifacteur Azure | Documents Microsoft"
description: "Découvrez comment tooassign utilisateur licences pour Microsoft Azure multi-Factor Authentication."
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
ms.openlocfilehash: ca324eb4d6622fdad8bd3d74b7e1595919e36535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-toousers"></a><span data-ttu-id="74b83-103">Affectation d’un toousers de licences Azure MFA, Azure AD Premium ou Enterprise Mobility</span><span class="sxs-lookup"><span data-stu-id="74b83-103">Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license toousers</span></span>
<span data-ttu-id="74b83-104">Si vous avez acheté des licences Enterprise Mobility Suite, Azure AD Premium ou Azure MFA, il est inutile toocreate un fournisseur d’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="74b83-104">If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need toocreate a Multi-Factor Auth provider.</span></span> <span data-ttu-id="74b83-105">Une fois que vous affectez des licences hello tooyour utilisateurs, vous pouvez commencer à les activer pour l’authentification Multifacteur.</span><span class="sxs-lookup"><span data-stu-id="74b83-105">Once you assign hello licenses tooyour users, you can begin enabling them for MFA.</span></span>

## <a name="tooassign-a-license"></a><span data-ttu-id="74b83-106">tooassign une licence</span><span class="sxs-lookup"><span data-stu-id="74b83-106">tooassign a license</span></span>
1. <span data-ttu-id="74b83-107">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="74b83-107">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="74b83-108">Sur hello gauche, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74b83-108">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="74b83-109">Sur la page Active Directory de hello, double-cliquez sur le répertoire hello qui a des utilisateurs hello tooenable.</span><span class="sxs-lookup"><span data-stu-id="74b83-109">On hello Active Directory page, double-click hello directory that has hello users you wish tooenable.</span></span>
4. <span data-ttu-id="74b83-110">En hello haut hello active, sélectionnez **licences**.</span><span class="sxs-lookup"><span data-stu-id="74b83-110">At hello top of hello directory page, select **Licenses**.</span></span>
   <span data-ttu-id="74b83-111">![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span><span class="sxs-lookup"><span data-stu-id="74b83-111">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span></span>
5. <span data-ttu-id="74b83-112">Sur la page des licences hello, sélectionnez **Azure multi-Factor Authentication**, **Active Directory Premium**, ou **Enterprise Mobility Suite**.</span><span class="sxs-lookup"><span data-stu-id="74b83-112">On hello Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.</span></span>  <span data-ttu-id="74b83-113">Si vous ne disposez que d’une licence, celle-ci doit normalement être sélectionnée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="74b83-113">If you only have one, then it should be selected automatically.</span></span>
6. <span data-ttu-id="74b83-114">Au bas de hello de page de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="74b83-114">At hello bottom of hello page, click **Assign**.</span></span>
   <span data-ttu-id="74b83-115">![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span><span class="sxs-lookup"><span data-stu-id="74b83-115">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span></span>
7. <span data-ttu-id="74b83-116">Dans la zone hello qui s’affiche, cliquez sur Suivant toohello utilisateurs ou groupes de licences tooassign à.</span><span class="sxs-lookup"><span data-stu-id="74b83-116">In hello box that comes up, click next toohello users or groups you want tooassign licenses to.</span></span>  <span data-ttu-id="74b83-117">Une coche verte doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="74b83-117">You should see a green check mark appear.</span></span>
8. <span data-ttu-id="74b83-118">Cliquez sur hello coche icône toosave hello change.</span><span class="sxs-lookup"><span data-stu-id="74b83-118">Click hello check mark icon toosave hello changes.</span></span>
   <span data-ttu-id="74b83-119">![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span><span class="sxs-lookup"><span data-stu-id="74b83-119">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span></span>
9. <span data-ttu-id="74b83-120">Vous devriez voir un message indiquant le nombre de licences qui ont été attribuées et le nombre d’échecs, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="74b83-120">You should see a message saying how many licenses were assigned and how many may have failed.</span></span>  <span data-ttu-id="74b83-121">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="74b83-121">Click **Ok**.</span></span>
   <span data-ttu-id="74b83-122">![Attribuer des licences](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span><span class="sxs-lookup"><span data-stu-id="74b83-122">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="74b83-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="74b83-123">Next steps</span></span>

- <span data-ttu-id="74b83-124">Pour plus d’informations, consultez [Qu’est-ce que la licence Microsoft Azure Active Directory ?](../active-directory/active-directory-licensing-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="74b83-124">For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)</span></span>
