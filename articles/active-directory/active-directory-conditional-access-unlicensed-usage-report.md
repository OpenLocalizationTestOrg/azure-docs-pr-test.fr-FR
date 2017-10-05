---
title: "Rapport d’utilisation sans licence | Microsoft Docs"
description: "Le rapport d’utilisation sans licence vous aide à identifier les utilisateurs qui utilisent les fonctionnalités Azure AD payantes sans licence."
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
ms.openlocfilehash: c0b4f455f067e825362bdecc02ea62d7984f0d31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="63e83-103">Rapport d’utilisation sans licence</span><span class="sxs-lookup"><span data-stu-id="63e83-103">Unlicensed usage report</span></span>
<span data-ttu-id="63e83-104">Le rapport d’utilisation sans licence vous aide à identifier les utilisateurs qui utilisent les fonctionnalités Azure AD payantes sans licence.</span><span class="sxs-lookup"><span data-stu-id="63e83-104">The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="63e83-105">Cela vous permet de tirer un meilleur profit des licences que vous avez achetées et vous aide à déterminer le bon moment pour faire l’acquisition de licences supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="63e83-105">This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="63e83-106">Le rapport présente l’utilisation active des fonctionnalités payantes au cours des 30 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="63e83-106">The report shows active usage of the paid features in the last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="63e83-107">Structure du rapport</span><span class="sxs-lookup"><span data-stu-id="63e83-107">Report structure</span></span>
| <span data-ttu-id="63e83-108">Nom de la colonne</span><span class="sxs-lookup"><span data-stu-id="63e83-108">Column name</span></span> | <span data-ttu-id="63e83-109">Description</span><span class="sxs-lookup"><span data-stu-id="63e83-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="63e83-110">Utilisateur sans licence</span><span class="sxs-lookup"><span data-stu-id="63e83-110">Unlicensed User</span></span> |<span data-ttu-id="63e83-111">Nom de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="63e83-111">Name of the user</span></span> |
| <span data-ttu-id="63e83-112">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="63e83-112">Feature</span></span> |<span data-ttu-id="63e83-113">Nom de la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="63e83-113">The feature name.</span></span> <span data-ttu-id="63e83-114">Par exemple : accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="63e83-114">For example: conditional access</span></span> |
| <span data-ttu-id="63e83-115">Application utilisée</span><span class="sxs-lookup"><span data-stu-id="63e83-115">Application Accessed</span></span> |<span data-ttu-id="63e83-116">Le nom de l’application à laquelle l’utilisateur a accédé via la fonctionnalité utilisée.</span><span class="sxs-lookup"><span data-stu-id="63e83-116">The name of the application that is being accessed with the feature.</span></span> <span data-ttu-id="63e83-117">Par exemple : Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="63e83-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="63e83-118">Si un compte d’utilisateur a été supprimé, un ID du type 1003000090D8B285 sera renseigné dans la colonne « Utilisateur sans licence »</span><span class="sxs-lookup"><span data-stu-id="63e83-118">If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="63e83-119">Fonctionnalité d’accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="63e83-119">Conditional access feature</span></span>
<span data-ttu-id="63e83-120">Les utilisateurs sans licence seront signalés lorsqu’ils accèdent à un service limité par une stratégie d’accès conditionnel s’ils ne disposent pas d’une licence Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="63e83-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="63e83-121">Cela s’applique aux stratégies MFA / d’emplacement, ainsi qu’aux stratégies de périphériques utilisant Intune.</span><span class="sxs-lookup"><span data-stu-id="63e83-121">This applies to MFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="63e83-122">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="63e83-122">See also</span></span>
* [<span data-ttu-id="63e83-123">Utilisation de l’accès conditionnel avec Office 365 et les autres applications connectées à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63e83-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="63e83-124">Prise en main de l’accès conditionnel à Azure AD</span><span class="sxs-lookup"><span data-stu-id="63e83-124">Getting started with conditional access to Azure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

