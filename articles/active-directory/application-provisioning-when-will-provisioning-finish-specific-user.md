---
title: "Déterminer à quel moment un utilisateur spécifique pourra accéder à une application | Microsoft Docs"
description: "Comment déterminer à quel moment un utilisateur très important pourra accéder à une application que vous avez configurée pour l’approvisionnement des utilisateurs avec Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: fcefb31904cfb77022db0358e9feee6a0479db81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-to-access-an-application"></a><span data-ttu-id="24c9c-103">Déterminer à quel moment un utilisateur spécifique pourra accéder à une application</span><span class="sxs-lookup"><span data-stu-id="24c9c-103">Find out when a specific user will be able to access an application</span></span>
<span data-ttu-id="24c9c-104">Lorsque vous utilisez l’approvisionnement automatique des utilisateurs avec une application, Azure AD approvisionne et met à jour automatiquement les comptes d’utilisateur dans une application selon différents éléments comme [l’affectation d’utilisateurs et de groupes](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) et selon un intervalle régulier planifié (généralement toutes les 10 minutes).</span><span class="sxs-lookup"><span data-stu-id="24c9c-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="24c9c-105">Combien de temps cela prend-il ?</span><span class="sxs-lookup"><span data-stu-id="24c9c-105">How long does it take?</span></span>

<span data-ttu-id="24c9c-106">Le temps nécessaire à l’approvisionnement d’un utilisateur donné sera différent selon qu’une synchronisation initiale « complète » a déjà eu lieu ou non.</span><span class="sxs-lookup"><span data-stu-id="24c9c-106">The time it takes for a given user to be provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="24c9c-107">La première synchronisation entre Azure AD et une application peut prendre de 20 minutes à plusieurs heures, en fonction de la taille de l’annuaire Azure AD et du nombre d’utilisateurs dans l’étendue de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="24c9c-107">The first sync between Azure AD and an app can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="24c9c-108">Les synchronisations qui suivent la synchronisation initiale sont plus rapides (10 minutes, par exemple) car le service d’approvisionnement stocke les filigranes qui représentent l’état des deux systèmes après la synchronisation initiale, ce qui améliore les performances des synchronisations suivantes.</span><span class="sxs-lookup"><span data-stu-id="24c9c-108">Subsequent syncs after the initial sync be faster (e.g. within 10 minutes), as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-check-the-status-of-a-user"></a><span data-ttu-id="24c9c-109">Vérification de l’état d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="24c9c-109">How to check the status of a user</span></span>

<span data-ttu-id="24c9c-110">Pour consulter l’état de l’approvisionnement d’un utilisateur spécifique, consultez les journaux d’audit dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24c9c-110">To see the provisioning status for a selected user, consult the Audit logs in Azure AD.</span></span>

<span data-ttu-id="24c9c-111">Les journaux d’audit d’approvisionnement sont accessibles dans le Portail Azure, sous l’onglet **Azure Active Directory &gt; Applications d’entreprise &gt; \[Nom de l’application\] &gt; Journaux d’audit**.</span><span class="sxs-lookup"><span data-stu-id="24c9c-111">The provisioning audit logs can be accessed in the Azure portal, in the **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab.</span></span> <span data-ttu-id="24c9c-112">Filtrez les journaux sur la catégorie **Approvisionnement des comptes** pour afficher uniquement les événements d’approvisionnement de cette application.</span><span class="sxs-lookup"><span data-stu-id="24c9c-112">Filter the logs on the **Account Provisioning** category to only see the provisioning events for that app.</span></span> <span data-ttu-id="24c9c-113">Vous pouvez rechercher des utilisateurs en fonction de l’ID de correspondance qui a été configuré pour eux dans les mappages d’attributs.</span><span class="sxs-lookup"><span data-stu-id="24c9c-113">You can search for users based on the “matching ID” that was configured for them in the attribute mappings.</span></span> 

<span data-ttu-id="24c9c-114">Par exemple, si vous avez configuré le nom d’utilisateur principal ou l’adresse e-mail en tant qu’attribut correspondant côté Azure AD, et si l’utilisateur qui n’est pas approvisionné a la valeur « audrey@contoso.com », recherchez les journaux d’audit correspondant à « audrey@contoso.com » et passez en revue les entrées renvoyées.</span><span class="sxs-lookup"><span data-stu-id="24c9c-114">For example, if you configured the “user principal name” or “email address” as the matching attribute on the Azure AD side, and the user not being provisioning has a value of “audrey@contoso.com”, then search the audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="24c9c-115">Les journaux d’audit d’approvisionnement enregistrent toutes les opérations effectuées par le service d’approvisionnement, y compris :</span><span class="sxs-lookup"><span data-stu-id="24c9c-115">The provisioning audit logs record all the operations performed by the provisioning service, including:</span></span>

* <span data-ttu-id="24c9c-116">Interrogation d’Azure AD concernant les utilisateurs assignés qui se trouvent dans l’étendue de l’approvisionnement</span><span class="sxs-lookup"><span data-stu-id="24c9c-116">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="24c9c-117">Interrogation de l’application cible concernant l’existence de ces utilisateurs</span><span class="sxs-lookup"><span data-stu-id="24c9c-117">Querying the target app for the existence of those users</span></span>
* <span data-ttu-id="24c9c-118">Comparaison des objets utilisateur du système</span><span class="sxs-lookup"><span data-stu-id="24c9c-118">Comparing the user objects between the system</span></span>
* <span data-ttu-id="24c9c-119">Ajout, mise à jour ou désactivation du compte d’utilisateur dans le système cible en fonction de la comparaison</span><span class="sxs-lookup"><span data-stu-id="24c9c-119">Adding, updating, or disabling the user account in the target system based on the comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="24c9c-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24c9c-120">Next steps</span></span>
<span data-ttu-id="24c9c-121">[Automatisation de l’approvisionnement et de l’annulation de l’approvisionnement des utilisateurs pour les applications SaaS avec Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)</span><span class="sxs-lookup"><span data-stu-id="24c9c-121">[Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
