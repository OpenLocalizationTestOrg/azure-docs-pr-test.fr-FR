---
title: aaaTroubleshooting des membres dynamiques pour les groupes | Documents Microsoft
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
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="08351-103">Résolution des problèmes liés à l’appartenance dynamique à des groupes</span><span class="sxs-lookup"><span data-stu-id="08351-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="08351-104">**J’ai configuré une règle sur un groupe, mais aucune appartenance mis à jour dans le groupe de hello**</span><span class="sxs-lookup"><span data-stu-id="08351-104">**I configured a rule on a group but no memberships get updated in hello group**</span></span><br/><span data-ttu-id="08351-105">Vérifiez que hello **activer gestion déléguée des groupes** est défini trop**Oui** Bonjour **configurer** onglet. Vous verrez ce paramètre uniquement si vous êtes connecté en tant qu’un toowhom utilisateur une licence Azure Active Directory Premium est attribuée.</span><span class="sxs-lookup"><span data-stu-id="08351-105">Verify that hello **Enable delegated group management** setting is set too**Yes** in hello **Configure** tab. You will see this setting only if you are signed in as a user toowhom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="08351-106">Vérifiez les valeurs hello pour les attributs d’utilisateur sur une règle hello : existe-t-il des utilisateurs qui répondent aux règles de hello ?</span><span class="sxs-lookup"><span data-stu-id="08351-106">Verify hello values for user attributes on hello rule: are there users that satisfy hello rule?</span></span>

<span data-ttu-id="08351-107">**J’ai configuré une règle, mais maintenant les membres existants de hello de règle de hello sont supprimés**</span><span class="sxs-lookup"><span data-stu-id="08351-107">**I configured a rule, but now hello existing members of hello rule are removed**</span></span><br/><span data-ttu-id="08351-108">Ce comportement est normal.</span><span class="sxs-lookup"><span data-stu-id="08351-108">This is expected behavior.</span></span> <span data-ttu-id="08351-109">Les membres existants du groupe de hello sont supprimés lorsqu’une règle est activée ou modifiée.</span><span class="sxs-lookup"><span data-stu-id="08351-109">Existing members of hello group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="08351-110">les utilisateurs de Hello retournés à partir de l’évaluation de la règle de hello sont ajoutés en tant que groupe de membres toohello.</span><span class="sxs-lookup"><span data-stu-id="08351-110">hello users returned from evaluation of hello rule are added as members toohello group.</span></span>     

<span data-ttu-id="08351-111">**Je ne vois pas instantanément de changement d’appartenance quand j’ajoute ou quand je modifie une règle. Pourquoi ?**</span><span class="sxs-lookup"><span data-stu-id="08351-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="08351-112">L’évaluation de l’appartenance dédiée est effectuée régulièrement dans le cadre d’un processus asynchrone exécuté en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="08351-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="08351-113">La durée pendant laquelle hello a est déterminé par un nombre d’utilisateurs dans votre répertoire et hello la taille de groupe hello créé suite à la règle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="08351-113">How long hello process takes is determined by hello number of users in your directory and hello size of hello group created as a result of hello rule.</span></span> <span data-ttu-id="08351-114">En règle générale, les répertoires avec un nombre réduit d’utilisateurs verrez changements d’appartenance au groupe hello en moins de quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="08351-114">Typically, directories with small numbers of users will see hello group membership changes in less than a few minutes.</span></span> <span data-ttu-id="08351-115">Répertoires avec un grand nombre d’utilisateurs peuvent prendre 30 minutes ou plu toopopulate.</span><span class="sxs-lookup"><span data-stu-id="08351-115">Directories with a large number of users can take 30 minutes or longer toopopulate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="08351-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="08351-116">Next steps</span></span>
<span data-ttu-id="08351-117">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="08351-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="08351-118">La gestion des accès tooresources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08351-118">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="08351-119">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08351-119">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="08351-120">Qu’est-ce qu’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="08351-120">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="08351-121">Intégration des identités locales dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08351-121">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
