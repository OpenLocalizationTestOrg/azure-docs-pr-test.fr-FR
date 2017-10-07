---
title: "aaaDisable connexions utilisateur pour une application d’entreprise dans Active Directory de Azure | Documents Microsoft"
description: "Comment toodisable une application d’entreprise afin qu’aucun utilisateur ne peut se connecter tooit dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="05977-103">Désactiver les connexions utilisateur pour une application d’entreprise dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05977-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="05977-104">Il est facile toodisable une application d’entreprise afin qu’aucun utilisateur ne peut se connecter tooit dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05977-104">It's easy toodisable an enterprise application so that no users may sign in tooit in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="05977-105">Vous devez disposer des applications d’entreprise hello toomanage hello les autorisations appropriées, et vous devez être administrateur général pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="05977-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="05977-106">Comment désactiver les connexions des utilisateurs ?</span><span class="sxs-lookup"><span data-stu-id="05977-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="05977-107">Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="05977-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="05977-108">Sélectionnez **davantage de services**, entrez **Azure Active Directory** dans hello de zone de texte, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="05977-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="05977-109">Sur hello **Azure Active Directory** -  ***nom_répertoire*** blade (autrement dit, hello Azure AD panneau pour le répertoire hello vous gérez), sélectionnez **desapplicationsd’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="05977-109">On hello **Azure Active Directory** -  ***directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Ouverture des applications d’entreprise](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="05977-111">Sur hello **des applications d’entreprise** panneau, sélectionnez **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="05977-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="05977-112">Vous consultez une liste d’applications hello que vous pouvez gérer.</span><span class="sxs-lookup"><span data-stu-id="05977-112">You see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="05977-113">Sur hello **des applications d’entreprise - toutes les applications** panneau, sélectionnez une application.</span><span class="sxs-lookup"><span data-stu-id="05977-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="05977-114">Sur hello ***appname*** blade (autrement dit, hello blade avec nom hello d’application sélectionné hello dans le titre de hello), sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="05977-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![En sélectionnant hello toutes les commandes d’applications](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="05977-116">Sur hello ***appname*** - **propriétés** panneau, sélectionnez **non** pour **activée pour les utilisateurs de toosign ?**.</span><span class="sxs-lookup"><span data-stu-id="05977-116">On hello ***appname*** - **Properties** blade, select **No** for **Enabled for users toosign-in?**.</span></span>
8. <span data-ttu-id="05977-117">Sélectionnez hello **enregistrer** commande.</span><span class="sxs-lookup"><span data-stu-id="05977-117">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05977-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="05977-118">Next steps</span></span>
* [<span data-ttu-id="05977-119">Voir tous mes groupes</span><span class="sxs-lookup"><span data-stu-id="05977-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="05977-120">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="05977-120">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="05977-121">Supprimer l’affectation d’un utilisateur ou d’un groupe à une application d’entreprise dans la version préliminaire d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05977-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="05977-122">Modifier le nom hello ou un logo d’une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="05977-122">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
