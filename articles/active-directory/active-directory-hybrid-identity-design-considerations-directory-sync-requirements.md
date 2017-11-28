---
title: "aaaAzure considérations de conception hybride identité Active Directory - déterminer les besoins de synchronisation d’annuaire | Documents Microsoft"
description: "Identifier les exigences sont nécessaires pour la synchronisation de tous les utilisateurs de hello entre on = locaux et cloud d’entreprise de hello."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a><span data-ttu-id="626dd-103">Déterminer les exigences de synchronisation de répertoire</span><span class="sxs-lookup"><span data-stu-id="626dd-103">Determine directory synchronization requirements</span></span>
<span data-ttu-id="626dd-104">Synchronisation consiste à fournir aux utilisateurs une identité de cloud hello basée sur leur identité locale.</span><span class="sxs-lookup"><span data-stu-id="626dd-104">Synchronization is all about providing users an identity in hello cloud based on their on-premises identity.</span></span> <span data-ttu-id="626dd-105">Ou non qu’ils utiliseront le compte synchronisé pour l’authentification ou l’authentification fédérée, les utilisateurs de hello doivent toujours toohave une identité de cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="626dd-105">Whether or not they will use synchronized account for authentication or federated authentication, hello users will still need toohave an identity in hello cloud.</span></span>  <span data-ttu-id="626dd-106">Cette identité a besoin toobe conservées et mises à jour régulièrement.</span><span class="sxs-lookup"><span data-stu-id="626dd-106">This identity will need toobe maintained and updated periodically.</span></span>  <span data-ttu-id="626dd-107">mises à jour Hello peuvent prendre différentes formes, des modifications de toopassword de modifications de titre.</span><span class="sxs-lookup"><span data-stu-id="626dd-107">hello updates can take many forms, from title changes toopassword changes.</span></span>  

<span data-ttu-id="626dd-108">Commencez par évaluer les organisations hello identité utilisateur et la solution contraintes locales.</span><span class="sxs-lookup"><span data-stu-id="626dd-108">Start by evaluating hello organizations on-premises identity solution and user requirements.</span></span> <span data-ttu-id="626dd-109">Cette évaluation est important toodefine hello prescriptions comment les identités d’utilisateur seront créées et mis à jour dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="626dd-109">This evaluation is important toodefine hello technical requirements for how user identities will be created and maintained in hello cloud.</span></span>  <span data-ttu-id="626dd-110">Pour la plupart des organisations, Active Directory est local et ne sont hello des services locaux qui sont des utilisateurs par synchronisées de toutefois dans certains cas cela sera pas hello cas.</span><span class="sxs-lookup"><span data-stu-id="626dd-110">For a majority of organizations, Active Directory is on-premises and will be hello on-premises directory that users will by synchronized from, however in some cases this will not be hello case.</span></span>  

<span data-ttu-id="626dd-111">Vérifiez que hello tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="626dd-111">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="626dd-112">Combien avez-vous de forêts AD: une, plusieurs ou aucune ?</span><span class="sxs-lookup"><span data-stu-id="626dd-112">Do you have one AD forest, multiple, or none?</span></span>
  
  * <span data-ttu-id="626dd-113">Vers combien d'annuaires Azure AD allez-vous synchroniser ?</span><span class="sxs-lookup"><span data-stu-id="626dd-113">How many Azure AD directories will you be synchronizing to?</span></span>
    
    1. <span data-ttu-id="626dd-114">Utilisez-vous le filtrage ?</span><span class="sxs-lookup"><span data-stu-id="626dd-114">Are you using filtering?</span></span>
    2. <span data-ttu-id="626dd-115">Avez-vous prévu plusieurs serveurs Azure AD Connect ?</span><span class="sxs-lookup"><span data-stu-id="626dd-115">Do you have multiple Azure AD Connect servers planned?</span></span>
* <span data-ttu-id="626dd-116">Avez-vous actuellement un outil de synchronisation local ?</span><span class="sxs-lookup"><span data-stu-id="626dd-116">Do you currently have a synchronization tool on-premises?</span></span>
  
  * <span data-ttu-id="626dd-117">Si oui, vos utilisateurs bénéficient-ils d'un annuaire/d'une intégration virtuels d'identités ?</span><span class="sxs-lookup"><span data-stu-id="626dd-117">If yes, does your users if users have a virtual directory/integration of identities?</span></span>
* <span data-ttu-id="626dd-118">Vous disposez de n’importe quel autre répertoire local que vous souhaitez toosynchronize (par exemple, annuaire LDAP, base de données des ressources humaines, etc.) ?</span><span class="sxs-lookup"><span data-stu-id="626dd-118">Do you have any other directory on-premises that you want toosynchronize (e.g. LDAP Directory, HR database, etc)?</span></span>
  * <span data-ttu-id="626dd-119">Vous allez toobe effectuer n’importe quel GALSync ?</span><span class="sxs-lookup"><span data-stu-id="626dd-119">Are you going toobe doing any GALSync?</span></span>
  * <span data-ttu-id="626dd-120">Nouveautés d’état de hello actuel de l’UPN de votre organisation ?</span><span class="sxs-lookup"><span data-stu-id="626dd-120">What is hello current state of UPNs in your organization?</span></span> 
  * <span data-ttu-id="626dd-121">Avez-vous un annuaire différent pour l'authentification des utilisateurs ?</span><span class="sxs-lookup"><span data-stu-id="626dd-121">Do you have a different directory that users authenticate against?</span></span>
  * <span data-ttu-id="626dd-122">Votre entreprise utilise-t-elle Microsoft Exchange ?</span><span class="sxs-lookup"><span data-stu-id="626dd-122">Does your company use Microsoft Exchange?</span></span>
    * <span data-ttu-id="626dd-123">Le déploiement d'Exchange hybride est-il prévu ?</span><span class="sxs-lookup"><span data-stu-id="626dd-123">Do they plan of having a hybrid exchange deployment?</span></span>

<span data-ttu-id="626dd-124">Maintenant que vous avez une idée sur les conditions de synchronisation, vous devez toodetermine outil est un toomeet correct de hello ces exigences.</span><span class="sxs-lookup"><span data-stu-id="626dd-124">Now that you have an idea about your synchronization requirements, you need toodetermine which tool is hello correct one toomeet these requirements.</span></span>  <span data-ttu-id="626dd-125">Microsoft fournit plusieurs intégration d’annuaire tooaccomplish outils et la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="626dd-125">Microsoft provides several tools tooaccomplish directory integration and synchronization.</span></span>  <span data-ttu-id="626dd-126">Consultez hello [tableau de comparaison des outils identité hybride directory integration](active-directory-hybrid-identity-design-considerations-tools-comparison.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="626dd-126">See hello [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span></span> 

<span data-ttu-id="626dd-127">Maintenant que vous avez vos exigences de synchronisation et d’un outil hello pour ce faire, de votre société, vous avez besoin d’applications hello tooevaluate qui utilisent ces services d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="626dd-127">Now that you have your synchronization requirements and hello tool that will accomplish this for your company, you need tooevaluate hello applications that use these directory services.</span></span> <span data-ttu-id="626dd-128">Cette évaluation est importante toodefine hello spécifications techniques toointegrate ces cloud de toohello d’applications.</span><span class="sxs-lookup"><span data-stu-id="626dd-128">This evaluation is important toodefine hello technical requirements toointegrate these applications toohello cloud.</span></span> <span data-ttu-id="626dd-129">Vérifiez que hello tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="626dd-129">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="626dd-130">Ces applications seront déplacé toohello cloud et utiliser hello directory ?</span><span class="sxs-lookup"><span data-stu-id="626dd-130">Will these applications be moved toohello cloud and use hello directory?</span></span>
* <span data-ttu-id="626dd-131">Y a-t-il des attributs spéciaux qui doivent toobe synchronisé toohello cloud afin de ces applications peuvent les utiliser avec succès ?</span><span class="sxs-lookup"><span data-stu-id="626dd-131">Are there special attributes that need toobe synchronized toohello cloud so these applications can use them successfully?</span></span>
* <span data-ttu-id="626dd-132">Ces applications devez toobe réécrite parti tootake d’authentification de cloud ?</span><span class="sxs-lookup"><span data-stu-id="626dd-132">Will these applications need toobe re-written tootake advantage of cloud auth?</span></span>
* <span data-ttu-id="626dd-133">Ces applications continue toolive local tandis que les utilisateurs y accéder à l’aide d’identité de cloud hello ?</span><span class="sxs-lookup"><span data-stu-id="626dd-133">Will these applications continue toolive on-premises while users access them using hello cloud identity?</span></span>

<span data-ttu-id="626dd-134">Vous devez également toodetermine hello sécurité exigences et contraintes de synchronisation d’annuaires.</span><span class="sxs-lookup"><span data-stu-id="626dd-134">You also need toodetermine hello security requirements and constraints directory synchronization.</span></span> <span data-ttu-id="626dd-135">Cette évaluation est important tooget une liste d’exigences hello qui seront nécessaires dans l’ordre toocreate et conserver l’identité de l’utilisateur dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="626dd-135">This evaluation is important tooget a list of hello requirements that will be needed in order toocreate and maintain user’s identities in hello cloud.</span></span> <span data-ttu-id="626dd-136">Vérifiez que hello tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="626dd-136">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="626dd-137">Où serveur de synchronisation hello se trouver ?</span><span class="sxs-lookup"><span data-stu-id="626dd-137">Where will hello synchronization server be located?</span></span>
* <span data-ttu-id="626dd-138">Sera-t-il lié à un domaine ?</span><span class="sxs-lookup"><span data-stu-id="626dd-138">Will it be domain joined?</span></span>
* <span data-ttu-id="626dd-139">Serveur de hello se trouvera sur un réseau restreint derrière un pare-feu, par exemple un réseau de périmètre ?</span><span class="sxs-lookup"><span data-stu-id="626dd-139">Will hello server be located on a restricted network behind a firewall, such as a DMZ?</span></span>
  * <span data-ttu-id="626dd-140">Sera synchronisation toosupport des ports pare-feu tooopen en mesure de hello requis ?</span><span class="sxs-lookup"><span data-stu-id="626dd-140">Will you be able tooopen hello required firewall ports toosupport synchronization?</span></span>
* <span data-ttu-id="626dd-141">Disposez-vous d’un plan de récupération d’urgence pour le serveur de synchronisation hello ?</span><span class="sxs-lookup"><span data-stu-id="626dd-141">Do you have a disaster recovery plan for hello synchronization server?</span></span>
* <span data-ttu-id="626dd-142">Disposez-vous d’un compte disposant des autorisations correctes de hello pour toutes les forêts que vous souhaitez toosynch avec ?</span><span class="sxs-lookup"><span data-stu-id="626dd-142">Do you have an account with hello correct permissions for all forests you want toosynch with?</span></span>
  * <span data-ttu-id="626dd-143">Si votre entreprise ne sait pas réponses hello pour cette question, passez en revue la section hello « Autorisations pour la synchronisation de mot de passe » dans l’article de hello [installation hello Service de synchronisation Azure Active Directory](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) et déterminer si vous disposez déjà d’un compte disposant de ces autorisations ou si vous devez toocreate une.</span><span class="sxs-lookup"><span data-stu-id="626dd-143">If your company doesn’t know hello answer for this question, review hello section “Permissions for password synchronization” in hello article [Install hello Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need toocreate one.</span></span>
* <span data-ttu-id="626dd-144">Si vous avez synchronisation de multi-forêt est tooget en mesure de tooeach forêt de hello synchronisation server ?</span><span class="sxs-lookup"><span data-stu-id="626dd-144">If you have mutli-forest sync is hello sync server able tooget tooeach forest?</span></span>

> [!NOTE]
> <span data-ttu-id="626dd-145">Notez que tootake de chacune des réponses et comprendre hello sous-tend hello.</span><span class="sxs-lookup"><span data-stu-id="626dd-145">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="626dd-146">[Déterminer les besoins de réponse aux incidents](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) passe en revue les options hello disponibles.</span><span class="sxs-lookup"><span data-stu-id="626dd-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over hello options available.</span></span> <span data-ttu-id="626dd-147">En répondant à chacune de ces questions, vous sélectionnerez l’option correspondant le mieux à vos besoins métier.</span><span class="sxs-lookup"><span data-stu-id="626dd-147">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="626dd-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="626dd-148">Next steps</span></span>
[<span data-ttu-id="626dd-149">Déterminer les exigences d’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="626dd-149">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a><span data-ttu-id="626dd-150">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="626dd-150">See also</span></span>
[<span data-ttu-id="626dd-151">Présentation des considérations relatives à la conception</span><span class="sxs-lookup"><span data-stu-id="626dd-151">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)
