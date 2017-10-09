---
title: "Assistant de sécurité aaaThe Azure AD Privileged Identity Management"
description: "Hello première fois que vous utilisez extension d’Azure Active Directory Privileged Identity Management hello, s’affiche avec un Assistant de sécurité. Cet article décrit les étapes de hello pour utiliser l’Assistant de hello."
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
ms.openlocfilehash: 0b3019134d3c7cfac33b3acfcf430b4d4f67b119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="65700-104">À l’aide de l’Assistant sécurité hello dans Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="65700-104">Using hello security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="65700-105">Si vous êtes hello première personne toorun Azure Privileged Identity Management (PIM) pour votre organisation, un Assistant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="65700-105">If you're hello first person toorun Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="65700-106">Assistant de Hello vous permet de comprendre les risques de sécurité hello d’identités privilégiées et comment toouse PIM tooreduce ces risques.</span><span class="sxs-lookup"><span data-stu-id="65700-106">hello wizard helps you understand hello security risks of privileged identities and how toouse PIM tooreduce those risks.</span></span> <span data-ttu-id="65700-107">Vous n’avez pas besoin toomake les attributions de rôle tooexisting modifications dans l’Assistant de hello, si vous préférez toodo plus tard.</span><span class="sxs-lookup"><span data-stu-id="65700-107">You don't need toomake any changes tooexisting role assignments in hello wizard, if you prefer toodo it later.</span></span>

## <a name="what-tooexpect"></a><span data-ttu-id="65700-108">Quel tooexpect</span><span class="sxs-lookup"><span data-stu-id="65700-108">What tooexpect</span></span>
<span data-ttu-id="65700-109">Avant le démarrage de votre organisation à l’aide de PIM, toutes les attributions de rôle sont permanentes : hello utilisateurs sont toujours à ces rôles même si elles ne doivent pas actuellement de leurs privilèges.</span><span class="sxs-lookup"><span data-stu-id="65700-109">Before your organization starts using PIM, all role assignments are permanent: hello users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="65700-110">Hello première étape de hello Assistant vous présente une liste des rôles de privilèges élevés et le nombre d’utilisateurs actuellement dans ces rôles.</span><span class="sxs-lookup"><span data-stu-id="65700-110">hello first step of hello wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="65700-111">Vous pouvez Explorer toolearn de rôle particulier tooa savoir plus sur les utilisateurs si une ou plusieurs d'entre eux sont inconnues.</span><span class="sxs-lookup"><span data-stu-id="65700-111">You can drill in tooa particular role toolearn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="65700-112">Hello deuxième étape de hello Assistant vous donne les attributions de rôles d’administrateur toochange opportunité.</span><span class="sxs-lookup"><span data-stu-id="65700-112">hello second step of hello wizard gives you an opportunity toochange administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="65700-113">Il est important de disposer d’au moins un administrateur général et plusieurs administrateurs de rôle privilégié avec un compte professionnel ou scolaire (et non un compte Microsoft).</span><span class="sxs-lookup"><span data-stu-id="65700-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="65700-114">S’il n'existe qu’un seul administrateur du rôle privilégié, organisation de hello ne seront pas en mesure de toomanage PIM si ce compte est supprimé.</span><span class="sxs-lookup"><span data-stu-id="65700-114">If there is only one privileged role administrator, hello organization will not be able toomanage PIM if that account is deleted.</span></span>
> <span data-ttu-id="65700-115">En outre, conserver les attributions de rôles permanente si un utilisateur possède un compte Microsoft (compte qu’ils utilisent toosign dans tooMicrosoft des services tels que Skype et Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="65700-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use toosign in tooMicrosoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="65700-116">Si vous envisagez de toorequire l’authentification Multifacteur pour l’activation de ce rôle, cet utilisateur sera verrouillé.</span><span class="sxs-lookup"><span data-stu-id="65700-116">If you plan toorequire MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="65700-117">Une fois que vous avez apporté des modifications, Assistant de hello n’affiche plus.</span><span class="sxs-lookup"><span data-stu-id="65700-117">After you have made changes, hello wizard will no longer show up.</span></span> <span data-ttu-id="65700-118">Hello prochaine fois que vous ou un autre administrateur de rôle privilégié utilisez PIM, vous verrez hello PIM tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="65700-118">hello next time you or another privileged role administrator use PIM, you will see hello PIM dashboard.</span></span>  

* <span data-ttu-id="65700-119">Si vous souhaitez tooadd ou supprimer des utilisateurs des rôles ou modifier les affectations de tooeligible permanente, en savoir plus sur [comment tooadd ou supprimer le rôle d’un utilisateur](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="65700-119">If you would like tooadd or remove users from roles or change assignments from permanent tooeligible, read more at [how tooadd or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="65700-120">Si vous souhaitez que toogive davantage d’utilisateurs accès toomanage PIM, en savoir plus sur [comment toogive aux toomanage dans PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="65700-120">If you would like toogive more users access toomanage PIM, read more at [how toogive access toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65700-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="65700-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

