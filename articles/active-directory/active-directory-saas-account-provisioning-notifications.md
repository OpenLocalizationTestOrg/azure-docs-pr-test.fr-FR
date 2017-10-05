---
title: "Notifications d’approvisionnement de comptes| Microsoft Docs"
description: "Découvrez comment vous assurer d’être informé des problèmes liés à l’approvisionnement des utilisateurs qui nécessitent votre attention en activant les notifications d’approvisionnement de comptes."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: b99037fc28eca1a3ebffefb9e99991e74f52c9a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="f6096-103">Notifications d’approvisionnement de comptes</span><span class="sxs-lookup"><span data-stu-id="f6096-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="f6096-104">Avec l’approvisionnement d’utilisateurs, vous pouvez automatiser le processus de gestion des utilisateurs dans les applications SaaS tierces.</span><span class="sxs-lookup"><span data-stu-id="f6096-104">With user provisioning, you can automate the process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="f6096-105">Bien qu’il soit automatisé, votre interaction avec ce processus est parfois nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f6096-105">While this is an automated process, your interaction with this process is from time to time required.</span></span> <br>
<span data-ttu-id="f6096-106">C’est par exemple le cas quand le mot de passe du compte que vous avez configuré pour échanger des données avec une application SaaS tierce a expiré.</span><span class="sxs-lookup"><span data-stu-id="f6096-106">This is, for example the case, when the password of the account you have configured to exchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="f6096-107">En activant les notifications d’approvisionnement de comptes, vous pouvez vous assurer d’être informé des problèmes liés à l’approvisionnement des utilisateurs qui nécessitent votre attention.</span><span class="sxs-lookup"><span data-stu-id="f6096-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related to user provisioning that require your attention.</span></span>

<span data-ttu-id="f6096-108">Vous activez ou désactivez les notifications d’approvisionnement de comptes dans le cadre de votre configuration d’approvisionnement d’utilisateurs pour une application SaaS tierce.</span><span class="sxs-lookup"><span data-stu-id="f6096-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![Approvisionnement d’utilisateurs][1] 

<span data-ttu-id="f6096-110">Pour activer les notifications d’approvisionnement de comptes, cochez la case associée dans la page de boîte de dialogue **Confirmation** , puis tapez l’alias de messagerie du destinataire.</span><span class="sxs-lookup"><span data-stu-id="f6096-110">To activate account provisioning notifications, select the related checkbox on the **Confirmation** dialog page, and then type the email alias of the recipient.</span></span>

![Notifications d’approvisionnement de comptes][2]

<span data-ttu-id="f6096-112">Vous pouvez entrer une liste de distribution comme destinataire ; toutefois, il convient de noter que le message électronique de notification contient des liens vers des rapports qui sont accessibles uniquement aux administrateurs Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6096-112">You can enter a distribution list as recipient; however, it is important to note that the notification email contains links to reports that are only accessible by the Azure AD administrators.</span></span>

<span data-ttu-id="f6096-113">Si vous avez activé les notifications d’approvisionnement de comptes, vous recevrez des messages électroniques à propos des problèmes critiques liés à l’approvisionnement des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f6096-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related to user provisioning.</span></span> <span data-ttu-id="f6096-114">Cependant, pour éviter une surcharge de courrier électronique, vous recevrez un seul message de notification par jour pour chaque application SaaS pour laquelle la notification par courrier électronique est activée.</span><span class="sxs-lookup"><span data-stu-id="f6096-114">However, to avoid an email overload, you will only receive one notification email per day for each SaaS application the notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="f6096-115">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="f6096-115">Related Articles</span></span>
* [<span data-ttu-id="f6096-116">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6096-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="f6096-117">Automatiser l’approvisionnement/le déprovisionnement des utilisateurs pour les applications SaaS</span><span class="sxs-lookup"><span data-stu-id="f6096-117">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="f6096-118">Personnalisation des mappages d’attributs pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="f6096-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="f6096-119">Écriture d’expressions pour les mappages d’attributs</span><span class="sxs-lookup"><span data-stu-id="f6096-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="f6096-120">Filtres d’étendue pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="f6096-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="f6096-121">Utilisation de SCIM pour activer la configuration automatique des utilisateurs et des groupes d’Azure Active Directory sur des applications</span><span class="sxs-lookup"><span data-stu-id="f6096-121">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="f6096-122">Liste des didacticiels sur l’intégration des applications SaaS</span><span class="sxs-lookup"><span data-stu-id="f6096-122">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
