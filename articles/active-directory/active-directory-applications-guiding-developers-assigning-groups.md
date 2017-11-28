---
title: aaaAssign regroupe les applications tooAzure AD | Des documents Microsoft
description: Comment tooimplement groupe affectation pour les applications Azure.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: 086619df09c13bf259afc3128d45ed804b99e519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-azure-active-directory-groups-tooan-application"></a><span data-ttu-id="18f43-103">Affecter des groupes Azure Active Directory tooan application</span><span class="sxs-lookup"><span data-stu-id="18f43-103">Assign Azure Active Directory groups tooan application</span></span>
<span data-ttu-id="18f43-104">Avant de pouvoir affecter des utilisateurs et applications tooan de groupes, vous devez imposer l’affectation d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="18f43-104">Before you can assign users and groups tooan application, you must require user assignment.</span></span> <span data-ttu-id="18f43-105">toolearn comment toorequire l’attribution utilisateur, consultez hello [nécessitant l’affectation d’utilisateurs](active-directory-applications-guiding-developers-requiring-user-assignment.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="18f43-105">toolearn how toorequire user assignment, see hello [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="18f43-106">Cet article suppose que vous avez déjà créé des groupes dans hello active directory que vous utilisez pour cette application.</span><span class="sxs-lookup"><span data-stu-id="18f43-106">This article assumes that you have already created groups in hello active directory you are using for this application.</span></span>

## <a name="assigning-groups-tooan-application"></a><span data-ttu-id="18f43-107">Affectation de groupes tooan Application</span><span class="sxs-lookup"><span data-stu-id="18f43-107">Assigning Groups tooan Application</span></span>
1. <span data-ttu-id="18f43-108">Ouvrez une session dans toohello portail Azure avec un compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="18f43-108">Log in toohello Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="18f43-109">Cliquez sur hello **tous les éléments** élément dans le menu principal hello.</span><span class="sxs-lookup"><span data-stu-id="18f43-109">Click on hello **All Items** item in hello main menu.</span></span>
3. <span data-ttu-id="18f43-110">Sélectionnez un répertoire hello que vous utilisez pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="18f43-110">Choose hello directory you are using for hello application.</span></span>
4. <span data-ttu-id="18f43-111">Cliquez sur hello **APPLICATIONS** onglet.</span><span class="sxs-lookup"><span data-stu-id="18f43-111">Click on hello **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="18f43-112">Sélectionnez l’application hello à partir de la liste de hello des applications associées à ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="18f43-112">Select hello application from hello list of applications associated with this directory.</span></span>
6. <span data-ttu-id="18f43-113">Cliquez sur hello **les utilisateurs et groupes** onglet.</span><span class="sxs-lookup"><span data-stu-id="18f43-113">Click hello **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="18f43-114">Liste de groupes dans active directory à l’aide de hello hello de filtres **groupes** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="18f43-114">Filter hello list of groups in your active directory by using hello **Groups** dropdown list.</span></span>
8. <span data-ttu-id="18f43-115">Sélectionnez le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="18f43-115">Select hello group.</span></span>
9. <span data-ttu-id="18f43-116">Cliquez sur **AFFECTER**.</span><span class="sxs-lookup"><span data-stu-id="18f43-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="18f43-117">Cliquez sur **Oui** lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="18f43-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18f43-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18f43-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
