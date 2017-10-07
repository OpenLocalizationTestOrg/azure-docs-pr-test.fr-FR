---
title: "Rapport d’utilisation d’aaaUnlicensed | Documents Microsoft"
description: "Bonjour rapport sans licence d’utilisation vous permet de de qu'identifier les utilisateurs sans licence qui sont à l’aide payer les fonctionnalités Azure AD."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="b196e-103">Rapport d’utilisation sans licence</span><span class="sxs-lookup"><span data-stu-id="b196e-103">Unlicensed usage report</span></span>
<span data-ttu-id="b196e-104">Bonjour rapport sans licence d’utilisation vous permet de de qu'identifier les utilisateurs sans licence qui sont à l’aide payer les fonctionnalités Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b196e-104">hello unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="b196e-105">Cela vous permet de toomake améliore l’utilisation des licences que vous avez achetées et tooidentify vous savez que vous ayez besoin de licences supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b196e-105">This allows you toomake better use of licenses that you have purchased and tooidentify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="b196e-106">rapport de Hello montre active l’utilisation de hello fonctionnalités payée hello 30 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="b196e-106">hello report shows active usage of hello paid features in hello last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="b196e-107">Structure du rapport</span><span class="sxs-lookup"><span data-stu-id="b196e-107">Report structure</span></span>
| <span data-ttu-id="b196e-108">Nom de la colonne</span><span class="sxs-lookup"><span data-stu-id="b196e-108">Column name</span></span> | <span data-ttu-id="b196e-109">Description</span><span class="sxs-lookup"><span data-stu-id="b196e-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b196e-110">Utilisateur sans licence</span><span class="sxs-lookup"><span data-stu-id="b196e-110">Unlicensed User</span></span> |<span data-ttu-id="b196e-111">Nom d’utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="b196e-111">Name of hello user</span></span> |
| <span data-ttu-id="b196e-112">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="b196e-112">Feature</span></span> |<span data-ttu-id="b196e-113">nom de la fonction Hello.</span><span class="sxs-lookup"><span data-stu-id="b196e-113">hello feature name.</span></span> <span data-ttu-id="b196e-114">Par exemple : accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="b196e-114">For example: conditional access</span></span> |
| <span data-ttu-id="b196e-115">Application utilisée</span><span class="sxs-lookup"><span data-stu-id="b196e-115">Application Accessed</span></span> |<span data-ttu-id="b196e-116">nom Hello d’application hello qui est accessible avec la fonctionnalité de hello.</span><span class="sxs-lookup"><span data-stu-id="b196e-116">hello name of hello application that is being accessed with hello feature.</span></span> <span data-ttu-id="b196e-117">Par exemple : Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="b196e-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="b196e-118">Si un compte d’utilisateur a été supprimé hello 'Sans licence utilisateur' colonne sera remplie avec un ID, comme 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="b196e-118">If a user account has been deleted hello ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="b196e-119">Fonctionnalité d’accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="b196e-119">Conditional access feature</span></span>
<span data-ttu-id="b196e-120">Les utilisateurs sans licence seront signalés lorsqu’ils accèdent à un service limité par une stratégie d’accès conditionnel s’ils ne disposent pas d’une licence Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="b196e-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="b196e-121">Cela s’applique tooMFA / stratégies de l’emplacement ainsi que les appareils des stratégies qui utilisent Intune.</span><span class="sxs-lookup"><span data-stu-id="b196e-121">This applies tooMFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="b196e-122">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b196e-122">See also</span></span>
* [<span data-ttu-id="b196e-123">Utilisation de l’accès conditionnel avec Office 365 et les autres applications connectées à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b196e-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="b196e-124">Prise en main de l’accès conditionnel tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="b196e-124">Getting started with conditional access tooAzure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

