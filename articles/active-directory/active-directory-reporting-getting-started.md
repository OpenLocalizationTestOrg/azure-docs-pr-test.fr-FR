---
title: "Création de rapports Azure Active Directory : Prise en main | Microsoft Docs"
description: "Listes hello différents rapports disponibles dans le rapport d’Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a><span data-ttu-id="c75e9-103">Prise en main de la création de rapports Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c75e9-103">Getting started with Azure Active Directory Reporting</span></span>
## <a name="what-it-is"></a><span data-ttu-id="c75e9-104">Présentation</span><span class="sxs-lookup"><span data-stu-id="c75e9-104">What it is</span></span>
<span data-ttu-id="c75e9-105">Azure Active Directory (Azure AD) comprend des rapports sur la sécurité, les activités et l’audit concernant votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c75e9-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span></span> <span data-ttu-id="c75e9-106">Voici une liste des rapports hello inclus :</span><span class="sxs-lookup"><span data-stu-id="c75e9-106">Here's a list of hello reports included:</span></span>

### <a name="security-reports"></a><span data-ttu-id="c75e9-107">Rapports de sécurité</span><span class="sxs-lookup"><span data-stu-id="c75e9-107">Security reports</span></span>
* <span data-ttu-id="c75e9-108">Connexions à partir de sources inconnues</span><span class="sxs-lookup"><span data-stu-id="c75e9-108">Sign-ins from unknown sources</span></span>
* <span data-ttu-id="c75e9-109">Connexions après plusieurs échecs</span><span class="sxs-lookup"><span data-stu-id="c75e9-109">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="c75e9-110">Connexions depuis plusieurs zones géographiques</span><span class="sxs-lookup"><span data-stu-id="c75e9-110">Sign-ins from multiple geographies</span></span>
* <span data-ttu-id="c75e9-111">Connexions depuis des adresses IP avec des activités suspectes</span><span class="sxs-lookup"><span data-stu-id="c75e9-111">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="c75e9-112">Activité de connexion anormale</span><span class="sxs-lookup"><span data-stu-id="c75e9-112">Irregular sign-in activity</span></span>
* <span data-ttu-id="c75e9-113">Connexions à partir d’appareils potentiellement infectés</span><span class="sxs-lookup"><span data-stu-id="c75e9-113">Sign-ins from possibly infected devices</span></span>
* <span data-ttu-id="c75e9-114">Utilisateurs ayant une activité de connexion anormale</span><span class="sxs-lookup"><span data-stu-id="c75e9-114">Users with anomalous sign-in activity</span></span>

### <a name="activity-reports"></a><span data-ttu-id="c75e9-115">Rapports d’activité</span><span class="sxs-lookup"><span data-stu-id="c75e9-115">Activity reports</span></span>
* <span data-ttu-id="c75e9-116">Utilisation des applications : résumé</span><span class="sxs-lookup"><span data-stu-id="c75e9-116">Application usage: summary</span></span>
* <span data-ttu-id="c75e9-117">Utilisation des applications : présentation détaillée</span><span class="sxs-lookup"><span data-stu-id="c75e9-117">Application usage: detailed</span></span>
* <span data-ttu-id="c75e9-118">Tableau de bord de l’application</span><span class="sxs-lookup"><span data-stu-id="c75e9-118">Application dashboard</span></span>
* <span data-ttu-id="c75e9-119">Erreurs de configuration de compte</span><span class="sxs-lookup"><span data-stu-id="c75e9-119">Account provisioning errors</span></span>
* <span data-ttu-id="c75e9-120">Appareils des utilisateur individuels</span><span class="sxs-lookup"><span data-stu-id="c75e9-120">Individual user devices</span></span>
* <span data-ttu-id="c75e9-121">Activité des utilisateurs individuels</span><span class="sxs-lookup"><span data-stu-id="c75e9-121">Individual user Activity</span></span>
* <span data-ttu-id="c75e9-122">Rapport d'activité de groupes</span><span class="sxs-lookup"><span data-stu-id="c75e9-122">Groups activity report</span></span>
* <span data-ttu-id="c75e9-123">Rapport d’activité de l’enregistrement de la réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="c75e9-123">Password Reset Registration Activity Report</span></span>
* <span data-ttu-id="c75e9-124">Activité de réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="c75e9-124">Password reset activity</span></span>

### <a name="audit-reports"></a><span data-ttu-id="c75e9-125">Rapport d’audit</span><span class="sxs-lookup"><span data-stu-id="c75e9-125">Audit reports</span></span>
* <span data-ttu-id="c75e9-126">Rapport d’audit d’annuaire</span><span class="sxs-lookup"><span data-stu-id="c75e9-126">Directory audit report</span></span>

> [!TIP]
> <span data-ttu-id="c75e9-127">Pour plus d’informations sur la création de rapports Azure AD, consultez la page [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="c75e9-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="how-it-works"></a><span data-ttu-id="c75e9-128">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="c75e9-128">How it works</span></span>
### <a name="reporting-pipeline"></a><span data-ttu-id="c75e9-129">Pipeline de création de rapports</span><span class="sxs-lookup"><span data-stu-id="c75e9-129">Reporting pipeline</span></span>
<span data-ttu-id="c75e9-130">pipeline de création de rapports Hello se compose de trois étapes principales.</span><span class="sxs-lookup"><span data-stu-id="c75e9-130">hello reporting pipeline consists of three main steps.</span></span> <span data-ttu-id="c75e9-131">Chaque fois qu’un utilisateur se connecte, ou une authentification est effectuée, suivant de hello se produit :</span><span class="sxs-lookup"><span data-stu-id="c75e9-131">Every time a user signs in, or an authentication is made, hello following happens:</span></span>

* <span data-ttu-id="c75e9-132">Tout d’abord, hello utilisateur authentifié (avec ou sans succès) et hello est stocké dans les bases de données de service hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c75e9-132">First, hello user is authenticated (successfully or unsuccessfully), and hello result is stored in hello Azure Active Directory service databases.</span></span>
* <span data-ttu-id="c75e9-133">À intervalles réguliers, toutes les connexions récentes sont traitées.</span><span class="sxs-lookup"><span data-stu-id="c75e9-133">At regular intervals, all recent sign ins are processed.</span></span> <span data-ttu-id="c75e9-134">À ce stade, nos algorithmes de sécurité et de surveillance des activités anormales recherchent toute activité suspecte dans les connexions récentes.</span><span class="sxs-lookup"><span data-stu-id="c75e9-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span></span>
* <span data-ttu-id="c75e9-135">Après traitement, les rapports de hello sont écrites, mis en cache et pris en charge dans hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="c75e9-135">After processing, hello reports are written, cached, and served in hello Azure classic portal.</span></span>

### <a name="report-generation-times"></a><span data-ttu-id="c75e9-136">Durée de génération des rapports</span><span class="sxs-lookup"><span data-stu-id="c75e9-136">Report generation times</span></span>
<span data-ttu-id="c75e9-137">En raison du volume important de toohello d’authentifications et signe que connexions traitées par hello plateforme d’Azure AD, hello plus récent connexions traitées sont, en moyenne, datant d’une heure.</span><span class="sxs-lookup"><span data-stu-id="c75e9-137">Due toohello large volume of authentications and sign ins processed by hello Azure AD platform, hello most recent sign-ins processed are, on average, one hour old.</span></span> <span data-ttu-id="c75e9-138">Dans de rares cas, il peut falloir too8 heures tooprocess hello plus récente de connexions.</span><span class="sxs-lookup"><span data-stu-id="c75e9-138">In rare cases, it may take up too8 hours tooprocess hello most recent sign-ins.</span></span>

<span data-ttu-id="c75e9-139">Vous trouverez connectez-vous hello plus récente traitée en examinant le texte d’aide hello haut hello de chaque rapport.</span><span class="sxs-lookup"><span data-stu-id="c75e9-139">You can find hello most recent processed sign-in by examining hello help text at hello top of each report.</span></span>

![Texte d’aide en haut de hello de chaque rapport](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> <span data-ttu-id="c75e9-141">Pour plus d’informations sur la création de rapports Azure AD, consultez la page [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="c75e9-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="getting-started"></a><span data-ttu-id="c75e9-142">Prise en main</span><span class="sxs-lookup"><span data-stu-id="c75e9-142">Getting started</span></span>
### <a name="sign-into-hello-azure-classic-portal"></a><span data-ttu-id="c75e9-143">Se connecter à hello de portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="c75e9-143">Sign into hello Azure classic portal</span></span>
<span data-ttu-id="c75e9-144">Tout d’abord, vous devez toosign dans hello [portail Azure classic](https://manage.windowsazure.com) en tant qu’un administrateur global ou de conformité.</span><span class="sxs-lookup"><span data-stu-id="c75e9-144">First, you'll need toosign into hello [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span></span> <span data-ttu-id="c75e9-145">Vous doit également être un administrateur de service d’abonnement Azure ou un coadministrateur ou être à l’aide de hello « accès tooAzure AD » abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c75e9-145">You must also be an Azure subscription service administrator or co-administrator, or be using hello "Access tooAzure AD" Azure subscription.</span></span>

### <a name="navigate-tooreports"></a><span data-ttu-id="c75e9-146">Accédez tooReports</span><span class="sxs-lookup"><span data-stu-id="c75e9-146">Navigate tooReports</span></span>
<span data-ttu-id="c75e9-147">tooview rapports, accédez à onglet Rapports de toohello haut hello de votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c75e9-147">tooview Reports, navigate toohello Reports tab at hello top of your directory.</span></span>

<span data-ttu-id="c75e9-148">S’il s’agit d’affichage des rapports de hello pour la première fois, vous devez boîte de dialogue tooagree tooa avant de pouvoir afficher les rapports hello.</span><span class="sxs-lookup"><span data-stu-id="c75e9-148">If this is your first time viewing hello reports, you'll need tooagree tooa dialog box before you can view hello reports.</span></span> <span data-ttu-id="c75e9-149">Il s’agit de tooensure qu’il est acceptable pour les administrateurs de votre organisation de tooview ces données, qui peuvent être considérées comme des informations personnelles dans certains pays.</span><span class="sxs-lookup"><span data-stu-id="c75e9-149">This is tooensure that it's acceptable for admins in your organization tooview this data, which may be considered private information in some countries.</span></span>

![Boîte de dialogue](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a><span data-ttu-id="c75e9-151">Explorer chaque rapport</span><span class="sxs-lookup"><span data-stu-id="c75e9-151">Explore each report</span></span>
<span data-ttu-id="c75e9-152">Naviguer dans chaque rapport toosee hello de données collectées et hello-connexions traitées.</span><span class="sxs-lookup"><span data-stu-id="c75e9-152">Navigate into each report toosee hello data being collected and hello sign-ins processed.</span></span> <span data-ttu-id="c75e9-153">Vous trouverez une [liste de tous les rapports hello ici](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c75e9-153">You can find a [list of all hello reports here](active-directory-reporting-guide.md).</span></span>

![Tous les rapports](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a><span data-ttu-id="c75e9-155">Télécharger des rapports de hello en tant que volume partagé de cluster</span><span class="sxs-lookup"><span data-stu-id="c75e9-155">Download hello reports as CSV</span></span>
<span data-ttu-id="c75e9-156">Chaque rapport peut être téléchargé dans un fichier CSV (valeurs séparées par des virgules).</span><span class="sxs-lookup"><span data-stu-id="c75e9-156">Each report can be downloaded as a CSV (comma-separated value) file.</span></span> <span data-ttu-id="c75e9-157">Vous pouvez utiliser ces fichiers dans Excel, Power BI ou analyse tiers programmes toofurther analyser vos données.</span><span class="sxs-lookup"><span data-stu-id="c75e9-157">You can use these files in Excel, PowerBI or third-party analysis programs toofurther analyze your data.</span></span>

<span data-ttu-id="c75e9-158">toodownload un rapport en tant que volume partagé de cluster, accédez toohello rapport et cliquez sur « Télécharger » en bas de hello.</span><span class="sxs-lookup"><span data-stu-id="c75e9-158">toodownload any report as a CSV, navigate toohello report and click "Download" at hello bottom.</span></span>

![Bouton de téléchargement](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> <span data-ttu-id="c75e9-160">Pour plus d’informations sur la création de rapports Azure AD, consultez la page [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="c75e9-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c75e9-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c75e9-161">Next steps</span></span>
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a><span data-ttu-id="c75e9-162">Personnalisation des alertes d’activité anormale dans les connexions</span><span class="sxs-lookup"><span data-stu-id="c75e9-162">Customize alerts for anomalous sign in activity</span></span>
<span data-ttu-id="c75e9-163">Accédez à onglet de « Configurer » toohello de votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="c75e9-163">Navigate toohello "Configure" tab of your directory.</span></span>

<span data-ttu-id="c75e9-164">Faire défiler vers la section de « Notifications » toohello.</span><span class="sxs-lookup"><span data-stu-id="c75e9-164">Scroll toohello "Notifications" section.</span></span>

<span data-ttu-id="c75e9-165">Activer ou désactiver la section de « Notifications par courrier électronique de connexions anormales » hello.</span><span class="sxs-lookup"><span data-stu-id="c75e9-165">Enable or disable hello "Email Notifications of Anomalous sign-ins" section.</span></span>

![Hello section Notifications](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a><span data-ttu-id="c75e9-167">Hello intégrer des API de création de rapports AD Azure</span><span class="sxs-lookup"><span data-stu-id="c75e9-167">Integrate with hello Azure AD Reporting API</span></span>
<span data-ttu-id="c75e9-168">Consultez [prise en main de hello API Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c75e9-168">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

### <a name="engage-multi-factor-authentication-on-users"></a><span data-ttu-id="c75e9-169">Application de l’authentification multifacteur aux utilisateurs</span><span class="sxs-lookup"><span data-stu-id="c75e9-169">Engage Multi-Factor Authentication on users</span></span>
<span data-ttu-id="c75e9-170">Sélectionnez un utilisateur dans un rapport.</span><span class="sxs-lookup"><span data-stu-id="c75e9-170">Select a user in a report.</span></span>

<span data-ttu-id="c75e9-171">Cliquez sur hello « Activer l’authentification Multifacteur » en bas de hello d’écran hello.</span><span class="sxs-lookup"><span data-stu-id="c75e9-171">Click hello "Enable MFA" button at hello bottom of hello screen.</span></span>

![bouton de l’authentification multifacteur Hello bas hello écran hello](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> <span data-ttu-id="c75e9-173">Pour plus d’informations sur la création de rapports Azure AD, consultez la page [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="c75e9-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="learn-more"></a><span data-ttu-id="c75e9-174">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="c75e9-174">Learn more</span></span>
### <a name="audit-events"></a><span data-ttu-id="c75e9-175">Événements d'audit</span><span class="sxs-lookup"><span data-stu-id="c75e9-175">Audit events</span></span>
<span data-ttu-id="c75e9-176">Obtenir des informations sur les événements sont auditées dans répertoire hello dans [Azure Active Directory Reporting événements d’Audit](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="c75e9-176">Learn about what events are audited in hello directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span></span>

### <a name="api-integration"></a><span data-ttu-id="c75e9-177">Intégration de l’API</span><span class="sxs-lookup"><span data-stu-id="c75e9-177">API Integration</span></span>
<span data-ttu-id="c75e9-178">Consultez [prise en main de hello API Reporting](active-directory-reporting-api-getting-started.md) et hello [documentation de référence API](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span><span class="sxs-lookup"><span data-stu-id="c75e9-178">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md) and hello [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span></span>

### <a name="get-in-touch"></a><span data-ttu-id="c75e9-179">Prendre contact</span><span class="sxs-lookup"><span data-stu-id="c75e9-179">Get in touch</span></span>
<span data-ttu-id="c75e9-180">Envoyez un message à [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) pour faire part de vos commentaires, obtenir de l’aide ou poser une question.</span><span class="sxs-lookup"><span data-stu-id="c75e9-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span></span>

> [!TIP]
> <span data-ttu-id="c75e9-181">Pour plus d’informations sur la création de rapports Azure AD, consultez la page [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="c75e9-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

