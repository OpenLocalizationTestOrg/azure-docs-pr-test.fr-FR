---
title: "Assistant Sécurité d’Azure AD Privileged Identity Management"
description: "La première fois que vous utilisez l’extension Azure Active Directory Privileged Identity Management, un Assistant Sécurité s’affiche. Cet article décrit les étapes d’utilisation de l’Assistant."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 260d178f3d8158411b3ad266e3b0d15edbebc722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="a0f8d-104">Utilisation de l’Assistant Sécurité d’Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="a0f8d-104">Using the security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="a0f8d-105">Si vous êtes la première personne à exécuter Azure Privileged Identity Management (PIM) pour votre organisation, un Assistant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-105">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="a0f8d-106">Celui-ci vous aide à comprendre les risques liés à la sécurité des identités privilégiées et comment utiliser PIM pour les limiter.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-106">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span></span> <span data-ttu-id="a0f8d-107">Vous n’avez pas besoin d’apporter des modifications aux affectations de rôle existantes dans l’Assistant. Vous pouvez le faire ultérieurement si vous préférez.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-107">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="a0f8d-108">À quoi s’attendre</span><span class="sxs-lookup"><span data-stu-id="a0f8d-108">What to expect</span></span>
<span data-ttu-id="a0f8d-109">Avant le démarrage de votre organisation à l’aide de PIM, toutes les attributions de rôles sont permanentes : les utilisateurs ont toujours ces rôles, même s’ils n’ont pas actuellement besoin de leurs privilèges.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-109">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="a0f8d-110">La première étape de l’Assistant vous montre une liste des rôles à privilèges élevés et le nombre d’utilisateurs ayant actuellement ces rôles.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-110">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="a0f8d-111">Vous pouvez explorer en détail un rôle particulier pour en savoir plus sur les utilisateurs si certains vous sont inconnus.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-111">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="a0f8d-112">La deuxième étape de l’Assistant vous donne la possibilité de modifier les attributions du rôle d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-112">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="a0f8d-113">Il est important de disposer d’au moins un administrateur général et plusieurs administrateurs de rôle privilégié avec un compte professionnel ou scolaire (et non un compte Microsoft).</span><span class="sxs-lookup"><span data-stu-id="a0f8d-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="a0f8d-114">S’il n’existe qu’un seul administrateur de rôle privilégié, l’organisation ne pourra pas utiliser PIM si ce compte est supprimé.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-114">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span></span>
> <span data-ttu-id="a0f8d-115">En outre, conservez des affectations de rôle permanentes si un utilisateur possède un compte Microsoft (un compte pour se connecter aux services Microsoft tels que Skype et Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="a0f8d-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="a0f8d-116">Si vous envisagez d’exiger une authentification multifacteur (MFA) pour l’activation de ce rôle, cet utilisateur est exclu de ce rôle.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-116">If you plan to require MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="a0f8d-117">Une fois que vous avez apporté les modifications, l’Assistant ne s’affiche plus.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-117">After you have made changes, the wizard will no longer show up.</span></span> <span data-ttu-id="a0f8d-118">La prochaine fois que vous ou un autre administrateur de rôle privilégié utiliserez PIM, vous verrez le tableau de bord de PIM.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-118">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span></span>  

* <span data-ttu-id="a0f8d-119">Si vous souhaitez ajouter des utilisateurs dans des rôles ou en supprimer, ou encore modifier des affectations de l’état permanent à l’état éligible, consultez la rubrique [Comment ajouter ou supprimer un rôle d’utilisateur](active-directory-privileged-identity-management-how-to-add-role-to-user.md)pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-119">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="a0f8d-120">Si vous souhaitez autoriser plus d’utilisateurs à gérer PIM, consultez la rubrique expliquant [comment affecter un accès à PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="a0f8d-120">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0f8d-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0f8d-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

