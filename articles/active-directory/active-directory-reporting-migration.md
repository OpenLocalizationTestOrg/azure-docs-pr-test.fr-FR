---
title: "rapports d’activité d’aaaFind Bonjour portail Azure | Documents Microsoft"
description: "Découvrez comment les rapports toofind activité d’Azure Active Directory Bonjour portail Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a><span data-ttu-id="ef65b-103">Rechercher les rapports d’activité Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="ef65b-103">Find activity reports in hello Azure portal</span></span>

<span data-ttu-id="ef65b-104">Si vous déplacez de hello toohello de portail classique Azure portail Azure, vous obtenez un nouveau look journaux d’activité Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ef65b-104">If you are moving from hello Azure classic portal toohello Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="ef65b-105">Dans un récent [billet de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), nous expliquons comment vous pouvez voir des journaux d’activité dans le contexte hello de ressource hello vous travaillez dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ef65b-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in hello context of hello resource you are working on in hello Azure portal.</span></span> <span data-ttu-id="ef65b-106">Dans cet article, nous décrivons comment toofind les rapports que vous avez utilisé dans hello portail classique Azure Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ef65b-106">In this article, we describe how toofind reports that you used in hello Azure classic portal in hello Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="ef65b-107">Nouveautés</span><span class="sxs-lookup"><span data-stu-id="ef65b-107">What's new</span></span>

<span data-ttu-id="ef65b-108">Rapports Bonjour portail Azure classic sont divisées en catégories :</span><span class="sxs-lookup"><span data-stu-id="ef65b-108">Reports in hello Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="ef65b-109">Rapports de sécurité</span><span class="sxs-lookup"><span data-stu-id="ef65b-109">Security reports</span></span>
2.  <span data-ttu-id="ef65b-110">Rapports d’activité</span><span class="sxs-lookup"><span data-stu-id="ef65b-110">Activity reports</span></span>
3.  <span data-ttu-id="ef65b-111">Rapports d’application intégrée</span><span class="sxs-lookup"><span data-stu-id="ef65b-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="ef65b-112">Rapports d’activité et d’application intégrée</span><span class="sxs-lookup"><span data-stu-id="ef65b-112">Activity and integrated app reports</span></span>

<span data-ttu-id="ef65b-113">Pour un rapport basé sur le contexte Bonjour portail Azure, les rapports existants sont fusionnés dans une vue unique.</span><span class="sxs-lookup"><span data-stu-id="ef65b-113">For context-based reporting in hello Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="ef65b-114">Une seule API sous-jacente présente hello données toohello.</span><span class="sxs-lookup"><span data-stu-id="ef65b-114">A single, underlying API provides hello data toohello view.</span></span>

<span data-ttu-id="ef65b-115">toosee cette vue, sur hello **Azure Active Directory** panneau, sous **activité**, sélectionnez **journaux d’Audit**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-115">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="ef65b-116">![Journaux d’audit](./media/active-directory-reporting-migration/482.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="ef65b-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="ef65b-117">Hello suivant des rapports est consolidée dans cette vue :</span><span class="sxs-lookup"><span data-stu-id="ef65b-117">hello following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="ef65b-118">Rapport d’audit</span><span class="sxs-lookup"><span data-stu-id="ef65b-118">Audit report</span></span>
-   <span data-ttu-id="ef65b-119">Activité de réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="ef65b-119">Password reset activity</span></span>
-   <span data-ttu-id="ef65b-120">Activité de l’enregistrement de la réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="ef65b-120">Password reset registration activity</span></span>
-   <span data-ttu-id="ef65b-121">Activité de groupes en libre-service</span><span class="sxs-lookup"><span data-stu-id="ef65b-121">Self-service groups activity</span></span>
-   <span data-ttu-id="ef65b-122">Changements de nom de groupe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="ef65b-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="ef65b-123">Activité d’approvisionnement de compte</span><span class="sxs-lookup"><span data-stu-id="ef65b-123">Account provisioning activity</span></span>
-   <span data-ttu-id="ef65b-124">État de substitution de mot de passe</span><span class="sxs-lookup"><span data-stu-id="ef65b-124">Password rollover status</span></span>
-   <span data-ttu-id="ef65b-125">Erreurs de configuration de compte</span><span class="sxs-lookup"><span data-stu-id="ef65b-125">Account provisioning errors</span></span>


<span data-ttu-id="ef65b-126">Hello rapport d’utilisation de l’Application a été améliorée et est incluse dans hello **connexions** vue.</span><span class="sxs-lookup"><span data-stu-id="ef65b-126">hello Application Usage report has been enhanced and is included in hello **Sign-ins** view.</span></span> <span data-ttu-id="ef65b-127">toosee cette vue, sur hello **Azure Active Directory** panneau, sous **activité**, sélectionnez **connexions**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-127">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="ef65b-128">![Vue Connexions](./media/active-directory-reporting-migration/483.png "Vue Connexions")</span><span class="sxs-lookup"><span data-stu-id="ef65b-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="ef65b-129">Hello **connexions** vue inclut toutes les connexions utilisateur. Vous pouvez utiliser les informations d’utilisation de cette application informations tooget.</span><span class="sxs-lookup"><span data-stu-id="ef65b-129">hello **Sign-ins** view includes all user sign-ins. You can use this information tooget application usage information.</span></span> <span data-ttu-id="ef65b-130">Vous pouvez également afficher des informations sur l’utilisation de l’application Bonjour **des applications d’entreprise** vue d’ensemble, Bonjour **gérer** section.</span><span class="sxs-lookup"><span data-stu-id="ef65b-130">You also can view application usage information in hello **Enterprise applications** overview, in hello **MANAGE** section.</span></span>

<span data-ttu-id="ef65b-131">![Applications d’entreprise](./media/active-directory-reporting-migration/484.png "Applications d’entreprise")</span><span class="sxs-lookup"><span data-stu-id="ef65b-131">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="ef65b-132">Accéder à un rapport spécifique</span><span class="sxs-lookup"><span data-stu-id="ef65b-132">Access a specific report</span></span>

<span data-ttu-id="ef65b-133">Bien que hello portail Azure offre une vue unique, vous pouvez également rechercher à des rapports spécifiques.</span><span class="sxs-lookup"><span data-stu-id="ef65b-133">Although hello Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="ef65b-134">Journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="ef65b-134">Audit logs</span></span>

<span data-ttu-id="ef65b-135">Vos commentaires toocustomer de réponse, Bonjour portail Azure, vous pouvez utiliser avancées données hello tooaccess filtrage que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="ef65b-135">In response toocustomer feedback, in hello Azure portal, you can use advanced filtering tooaccess hello data you want.</span></span> <span data-ttu-id="ef65b-136">Un filtre, vous pouvez utiliser un *catégorie de l’activité*, qui répertorie hello différents types d’activité consigne dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef65b-136">One filter you can use is an *activity category*, which lists hello different types of activity logs in Azure AD.</span></span> <span data-ttu-id="ef65b-137">toowhat de résultats toonarrow vous recherchez, vous pouvez sélectionner une catégorie.</span><span class="sxs-lookup"><span data-stu-id="ef65b-137">toonarrow results toowhat you are looking for, you can select a category.</span></span>

<span data-ttu-id="ef65b-138">Par exemple, si vous êtes uniquement intéressé par les réinitialisations de mot de passe associé tooself-service activités, vous pouvez choisir hello **gestion de mot de passe libre-service** catégorie.</span><span class="sxs-lookup"><span data-stu-id="ef65b-138">For example, if you are interested only in activities related tooself-service password resets, you can choose hello **Self-service Password Management** category.</span></span> <span data-ttu-id="ef65b-139">catégories de Hello que vous consultez sont basées sur les ressources hello dans que vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="ef65b-139">hello categories you see are based on hello resource you are working in.</span></span>  

<span data-ttu-id="ef65b-140">![Options de catégorie sur la page de journaux d’Audit de filtre hello](./media/active-directory-reporting-migration/06.png "des options de catégorie sur la page de journaux d’Audit de filtre hello")</span><span class="sxs-lookup"><span data-stu-id="ef65b-140">![Category options on hello Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on hello Filter Audit Logs page")</span></span>

<span data-ttu-id="ef65b-141">Les catégories d’activités sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="ef65b-141">Activity categories include:</span></span>

- <span data-ttu-id="ef65b-142">Annuaire principal</span><span class="sxs-lookup"><span data-stu-id="ef65b-142">Core Directory</span></span>
- <span data-ttu-id="ef65b-143">Gestion des mots de passe en libre-service</span><span class="sxs-lookup"><span data-stu-id="ef65b-143">Self-service Password Management</span></span>
- <span data-ttu-id="ef65b-144">Gestion des groupes en libre-service</span><span class="sxs-lookup"><span data-stu-id="ef65b-144">Self-service Group Management</span></span>
- <span data-ttu-id="ef65b-145">Approvisionnement des comptes</span><span class="sxs-lookup"><span data-stu-id="ef65b-145">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="ef65b-146">Utilisation des applications</span><span class="sxs-lookup"><span data-stu-id="ef65b-146">Application usage</span></span>

<span data-ttu-id="ef65b-147">tooview des détails sur l’utilisation des applications pour toutes les applications ou d’une seule application, sous **activité**, sélectionnez **connexions**. résultats de hello toonarrow, vous pouvez filtrer sur le nom d’utilisateur ou le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="ef65b-147">tooview details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. toonarrow hello results, you can filter on user name or application name.</span></span>

<span data-ttu-id="ef65b-148">![Page Filtrer les événements de connexion](./media/active-directory-reporting-migration/07.png "Page Filtrer les événements de connexion")</span><span class="sxs-lookup"><span data-stu-id="ef65b-148">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="ef65b-149">Rapports de sécurité</span><span class="sxs-lookup"><span data-stu-id="ef65b-149">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="ef65b-150">Rapports d’activités anormales Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef65b-150">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="ef65b-151">Sécurité de l’activité anormale AD Azure des rapports à partir du portail Azure classic de hello ont été tooprovide consolidée vous avec une vue centralisée.</span><span class="sxs-lookup"><span data-stu-id="ef65b-151">Azure AD anomalous activity security reports from hello Azure classic portal have been consolidated tooprovide you with one, central view.</span></span> <span data-ttu-id="ef65b-152">Cette vue affiche tous les événements liés à la sécurité qu’Azure AD peut détecter et signaler dans des rapports.</span><span class="sxs-lookup"><span data-stu-id="ef65b-152">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="ef65b-153">Hello tableau suivant répertorie les rapports de sécurité de l’activité anormale hello Azure AD et les types d’événements risque correspondant Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ef65b-153">hello following table lists hello Azure AD anomalous activity security reports, and corresponding risk event types in hello Azure portal.</span></span>

| <span data-ttu-id="ef65b-154">Rapport d’activités anormales Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef65b-154">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="ef65b-155">Type d’événement à risque signalé par Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ef65b-155">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="ef65b-156">Utilisateurs avec des informations d’identification volées</span><span class="sxs-lookup"><span data-stu-id="ef65b-156">Users with leaked credentials</span></span> | <span data-ttu-id="ef65b-157">Informations d’identification divulguées</span><span class="sxs-lookup"><span data-stu-id="ef65b-157">Leaked credentials</span></span> |
| <span data-ttu-id="ef65b-158">Activité de connexion anormale</span><span class="sxs-lookup"><span data-stu-id="ef65b-158">Irregular sign-in activity</span></span> | <span data-ttu-id="ef65b-159">Voyage Impossible tooatypical emplacements</span><span class="sxs-lookup"><span data-stu-id="ef65b-159">Impossible travel tooatypical locations</span></span> |
| <span data-ttu-id="ef65b-160">Connexions à partir d’appareils potentiellement infectés</span><span class="sxs-lookup"><span data-stu-id="ef65b-160">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="ef65b-161">Connexions depuis des appareils infectés</span><span class="sxs-lookup"><span data-stu-id="ef65b-161">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="ef65b-162">Connexions à partir de sources inconnues</span><span class="sxs-lookup"><span data-stu-id="ef65b-162">Sign-ins from unknown sources</span></span> | <span data-ttu-id="ef65b-163">Connexions depuis des adresses IP anonymes</span><span class="sxs-lookup"><span data-stu-id="ef65b-163">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="ef65b-164">Connexions depuis des adresses IP avec des activités suspectes</span><span class="sxs-lookup"><span data-stu-id="ef65b-164">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="ef65b-165">Connexions depuis des adresses IP avec des activités suspectes</span><span class="sxs-lookup"><span data-stu-id="ef65b-165">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="ef65b-166">Connexions depuis des emplacements non connus</span><span class="sxs-lookup"><span data-stu-id="ef65b-166">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="ef65b-167">des rapports Hello suivant la sécurité de l’activité anormale Azure AD ne sont pas inclus en tant qu’événements risque Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="ef65b-167">hello following Azure AD anomalous activity security reports are not included as risk events in hello Azure portal:</span></span>

* <span data-ttu-id="ef65b-168">Connexions après plusieurs échecs</span><span class="sxs-lookup"><span data-stu-id="ef65b-168">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="ef65b-169">Connexions depuis plusieurs zones géographiques</span><span class="sxs-lookup"><span data-stu-id="ef65b-169">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="ef65b-170">Ces rapports sont toujours disponibles dans hello portail Azure classic, mais ils seront déconseillées à un moment donné dans hello futures.</span><span class="sxs-lookup"><span data-stu-id="ef65b-170">These reports are still available in hello Azure classic portal, but they will be deprecated at some time in hello future.</span></span>

<span data-ttu-id="ef65b-171">Pour plus d’informations, consultez [Événements à risque dans Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="ef65b-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="ef65b-172">Événements à risque détectés</span><span class="sxs-lookup"><span data-stu-id="ef65b-172">Detected risk events</span></span>

<span data-ttu-id="ef65b-173">Hello portail Azure, vous pouvez accéder à des rapports sur les événements à risque détectés sur hello **Azure Active Directory** panneau, sous **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-173">In hello Azure portal, you can access reports about detected risk events on hello **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="ef65b-174">Événements à risque détectés sont suivies dans hello suivant des rapports :</span><span class="sxs-lookup"><span data-stu-id="ef65b-174">Detected risk events are tracked in hello following reports:</span></span>   

- <span data-ttu-id="ef65b-175">les utilisateurs à risque ;</span><span class="sxs-lookup"><span data-stu-id="ef65b-175">Users at Risk</span></span>
- <span data-ttu-id="ef65b-176">les connexions risquées.</span><span class="sxs-lookup"><span data-stu-id="ef65b-176">Risky Sign-ins</span></span>

<span data-ttu-id="ef65b-177">![Rapports de sécurité](./media/active-directory-reporting-migration/04.png "Rapports de sécurité")</span><span class="sxs-lookup"><span data-stu-id="ef65b-177">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="ef65b-178">Pour plus d’informations sur les rapports de sécurité, consultez :</span><span class="sxs-lookup"><span data-stu-id="ef65b-178">For more information about security reports, see:</span></span>

- [<span data-ttu-id="ef65b-179">Utilisateurs sur les rapports de sécurité risque dans le portail d’Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="ef65b-179">Users at Risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="ef65b-180">Rapport de connexions présente des risques dans le portail d’Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="ef65b-180">Risky Sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a><span data-ttu-id="ef65b-181">Rapports d’activité Bonjour portail classique Azure et hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ef65b-181">Activity reports in hello Azure classic portal vs. hello Azure portal</span></span>

<span data-ttu-id="ef65b-182">tableau Hello dans cette section répertorie les rapports existants dans hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="ef65b-182">hello table in this section lists existing reports in hello Azure classic portal.</span></span> <span data-ttu-id="ef65b-183">Elle décrit également comment vous pouvez obtenir hello les mêmes informations dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ef65b-183">It also describes how you can get hello same information in hello Azure portal.</span></span>

<span data-ttu-id="ef65b-184">tooview tous l’audit des données, sur hello **Azure Active Directory** panneau, sous **activité**, accédez trop**journaux d’Audit**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-184">tooview all auditing data, on hello **Azure Active Directory** blade, under **ACTIVITY**, go too**Audit logs**.</span></span>

<span data-ttu-id="ef65b-185">![Journaux d’audit](./media/active-directory-reporting-migration/61.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="ef65b-185">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="ef65b-186">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="ef65b-186">Azure classic portal</span></span>                 | <span data-ttu-id="ef65b-187">toofind Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="ef65b-187">toofind in hello Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="ef65b-188">Journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="ef65b-188">Audit logs</span></span>                           | <span data-ttu-id="ef65b-189">Pour **Catégorie d’activité**, sélectionnez **Annuaire principal**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-189">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="ef65b-190">Activité de réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="ef65b-190">Password reset activity</span></span>              | <span data-ttu-id="ef65b-191">Pour **Catégorie d’activité**, sélectionnez **Gestion des mots de passe en libre-service**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-191">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="ef65b-192">Activité de l’enregistrement de la réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="ef65b-192">Password reset registration activity</span></span> | <span data-ttu-id="ef65b-193">Pour **Catégorie d’activité**, sélectionnez **Gestion des mots de passe en libre-service**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-193">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="ef65b-194">Activité de groupes en libre-service</span><span class="sxs-lookup"><span data-stu-id="ef65b-194">Self-service groups activity</span></span>         | <span data-ttu-id="ef65b-195">Pour **Catégorie d’activité**, sélectionnez **Gestion des groupes en libre-service**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-195">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="ef65b-196">Activité d’approvisionnement de compte</span><span class="sxs-lookup"><span data-stu-id="ef65b-196">Account provisioning activity</span></span>        | <span data-ttu-id="ef65b-197">Pour **Catégorie d’activité**, sélectionnez **Approvisionnement des utilisateurs de comptes**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-197">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="ef65b-198">État de substitution de mot de passe</span><span class="sxs-lookup"><span data-stu-id="ef65b-198">Password rollover status</span></span>             | <span data-ttu-id="ef65b-199">Pour **Catégorie d’activité**, sélectionnez **Substitution automatique de mot de passe d’application**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-199">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="ef65b-200">Erreurs de configuration de compte</span><span class="sxs-lookup"><span data-stu-id="ef65b-200">Account provisioning errors</span></span>          | <span data-ttu-id="ef65b-201">Pour **Catégorie d’activité**, sélectionnez **Approvisionnement des utilisateurs de comptes**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-201">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="ef65b-202">Changements de nom de groupe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="ef65b-202">Office365 Group Name Changes</span></span>         | <span data-ttu-id="ef65b-203">Pour **Catégorie d’activité**, sélectionnez **Gestion des mots de passe en libre-service**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-203">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="ef65b-204">Pour **Type de ressource activité**, sélectionnez **Groupe**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-204">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="ef65b-205">Pour **Source de l’activité**, sélectionnez **Groupes O365**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-205">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="ef65b-206">tooview hello **l’utilisation des applications** rapport hello **Azure Active Directory** panneau, sous **gérer**, sélectionnez **des Applications d’entreprise**, puis sélectionnez **connexions**.</span><span class="sxs-lookup"><span data-stu-id="ef65b-206">tooview hello **Application Usage** report, on hello **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="ef65b-207">![Rapport sur les connexions d’applications d’entreprise](./media/active-directory-reporting-migration/199.png "Rapport sur les connexions d’applications d’entreprise")</span><span class="sxs-lookup"><span data-stu-id="ef65b-207">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef65b-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef65b-208">Next steps</span></span>

<span data-ttu-id="ef65b-209">Pour une vue d’ensemble de la création de rapports, consultez hello [reporting d’Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ef65b-209">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
