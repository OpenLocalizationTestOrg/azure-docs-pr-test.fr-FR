---
title: "Attribuer des groupes à des applications Azure AD | Microsoft Docs"
description: "Implémentation de l’attribution de groupe pour les applications Azure."
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
ms.openlocfilehash: e0b0b87a454db96747f024e81882fe83d62fdbe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a><span data-ttu-id="71e76-103">Attribuer des groupes Azure Active Directory à une application</span><span class="sxs-lookup"><span data-stu-id="71e76-103">Assign Azure Active Directory groups to an application</span></span>
<span data-ttu-id="71e76-104">Avant d'affecter des utilisateurs et des groupes à une application, vous devez demander l'affectation de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="71e76-104">Before you can assign users and groups to an application, you must require user assignment.</span></span> <span data-ttu-id="71e76-105">Pour savoir comment demander l’affectation d’utilisateurs, consultez l’article [Demande de l’affectation de l’utilisateur](active-directory-applications-guiding-developers-requiring-user-assignment.md) .</span><span class="sxs-lookup"><span data-stu-id="71e76-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="71e76-106">Cet article suppose que vous avez déjà créé des groupes dans le répertoire actif que vous utilisez pour cette application.</span><span class="sxs-lookup"><span data-stu-id="71e76-106">This article assumes that you have already created groups in the active directory you are using for this application.</span></span>

## <a name="assigning-groups-to-an-application"></a><span data-ttu-id="71e76-107">Affectation de groupes à une application</span><span class="sxs-lookup"><span data-stu-id="71e76-107">Assigning Groups to an Application</span></span>
1. <span data-ttu-id="71e76-108">Connectez-vous au portail Azure avec un compte administrateur.</span><span class="sxs-lookup"><span data-stu-id="71e76-108">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="71e76-109">Dans le menu principal, cliquez sur **Tous les éléments** .</span><span class="sxs-lookup"><span data-stu-id="71e76-109">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="71e76-110">Choisissez le répertoire que vous utilisez pour l’application.</span><span class="sxs-lookup"><span data-stu-id="71e76-110">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="71e76-111">Cliquez sur l’onglet **APPLICATIONS** .</span><span class="sxs-lookup"><span data-stu-id="71e76-111">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="71e76-112">Sélectionnez l'application dans la liste des applications associées à ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="71e76-112">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="71e76-113">Cliquez sur l’onglet **UTILISATEURS ET GROUPES** .</span><span class="sxs-lookup"><span data-stu-id="71e76-113">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="71e76-114">Filtrez la liste des groupes dans le répertoire actif à l’aide de la liste déroulante **Groupes** .</span><span class="sxs-lookup"><span data-stu-id="71e76-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span></span>
8. <span data-ttu-id="71e76-115">Sélectionnez le groupe.</span><span class="sxs-lookup"><span data-stu-id="71e76-115">Select the group.</span></span>
9. <span data-ttu-id="71e76-116">Cliquez sur **AFFECTER**.</span><span class="sxs-lookup"><span data-stu-id="71e76-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="71e76-117">Cliquez sur **Oui** lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="71e76-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71e76-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71e76-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
