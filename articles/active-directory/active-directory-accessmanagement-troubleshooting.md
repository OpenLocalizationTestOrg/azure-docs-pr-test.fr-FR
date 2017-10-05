---
title: "Résolution des problèmes liés à l’appartenance dynamique des groupes | Microsoft Docs"
description: "Conseils pour résoudre les problèmes d’appartenance dynamique à des groupes dans Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="7bb60-103">Résolution des problèmes liés à l’appartenance dynamique à des groupes</span><span class="sxs-lookup"><span data-stu-id="7bb60-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="7bb60-104">**J’ai configuré une règle sur un groupe, mais aucune appartenance n’est mise à jour dans le groupe**</span><span class="sxs-lookup"><span data-stu-id="7bb60-104">**I configured a rule on a group but no memberships get updated in the group**</span></span><br/><span data-ttu-id="7bb60-105">Sous l’onglet **Configuration**, vérifiez que le paramètre **Activer la gestion déléguée des groupes** a la valeur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="7bb60-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab.</span></span> <span data-ttu-id="7bb60-106">Ce paramètre s’affiche uniquement si vous êtes connecté en tant qu’utilisateur auquel est attribuée une licence Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="7bb60-106">You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="7bb60-107">Vérifiez les valeurs des attributs d’utilisateur sur la règle : des utilisateurs satisfont-ils à la règle ?</span><span class="sxs-lookup"><span data-stu-id="7bb60-107">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span></span>

<span data-ttu-id="7bb60-108">**J’ai configuré une règle, mais les membres existants sur celle-ci sont à présent supprimés**</span><span class="sxs-lookup"><span data-stu-id="7bb60-108">**I configured a rule, but now the existing members of the rule are removed**</span></span><br/><span data-ttu-id="7bb60-109">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="7bb60-109">This is expected behavior.</span></span> <span data-ttu-id="7bb60-110">Lors de l’activation ou de la modification d’une règle, les membres existants du groupe sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="7bb60-110">Existing members of the group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="7bb60-111">Les utilisateurs provenant de l’évaluation de la règle sont ajoutés en tant que membres du groupe.</span><span class="sxs-lookup"><span data-stu-id="7bb60-111">The users returned from evaluation of the rule are added as members to the group.</span></span>     

<span data-ttu-id="7bb60-112">**Je ne vois pas instantanément de changement d’appartenance quand j’ajoute ou quand je modifie une règle. Pourquoi ?**</span><span class="sxs-lookup"><span data-stu-id="7bb60-112">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="7bb60-113">L’évaluation de l’appartenance dédiée est effectuée régulièrement dans le cadre d’un processus asynchrone exécuté en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="7bb60-113">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="7bb60-114">La durée de l’opération est déterminée par le nombre d’utilisateurs dans votre annuaire et par la taille du groupe créé à la suite de la règle.</span><span class="sxs-lookup"><span data-stu-id="7bb60-114">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span></span> <span data-ttu-id="7bb60-115">Généralement, les annuaires contenant peu d’utilisateurs constatent les changements d’appartenance au groupe en moins de quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7bb60-115">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span></span> <span data-ttu-id="7bb60-116">Le renseignement des annuaires contenant de nombreux utilisateurs peut prendre plus de 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="7bb60-116">Directories with a large number of users can take 30 minutes or longer to populate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="7bb60-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7bb60-117">Next steps</span></span>
<span data-ttu-id="7bb60-118">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bb60-118">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="7bb60-119">Gestion de l’accès aux ressources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7bb60-119">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="7bb60-120">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7bb60-120">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="7bb60-121">Qu’est-ce qu’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7bb60-121">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="7bb60-122">Intégration des identités locales dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7bb60-122">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
