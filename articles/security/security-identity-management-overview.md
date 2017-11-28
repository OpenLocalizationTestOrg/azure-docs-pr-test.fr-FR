---
title: "Fonctionnalités de sécurité Azure liées à la gestion des identités | Microsoft Docs"
description: " Cet article fournit une vue d’ensemble des principales fonctionnalités de sécurité Azure liées à la gestion des identités. Les solutions de gestion des identités et accès de Microsoft aident les services informatiques à protéger l’accès aux applications et ressources dans le centre de données d’entreprise comme dans le cloud, en activant des niveaux supplémentaires de validation telles que l’authentification multifacteur et les stratégies d’accès conditionnel. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 5aa0a7ac-8f18-4ede-92a1-ae0dfe585e28
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: terrylan
ms.openlocfilehash: 8d00882caf5411240c5f0a3533c78c3dbe361ef2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-identity-management-security-overview"></a><span data-ttu-id="81505-104">Vue d’ensemble de la sécurité et de la gestion des identités Azure</span><span class="sxs-lookup"><span data-stu-id="81505-104">Azure identity management security overview</span></span>
<span data-ttu-id="81505-105">Les solutions de gestion des identités et accès de Microsoft aident les services informatiques à protéger l’accès aux applications et ressources dans le centre de données d’entreprise comme dans le cloud, en activant des niveaux supplémentaires de validation telles que l’authentification multifacteur et les stratégies d’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="81505-105">Microsoft identity and access management solutions help IT protect access to applications and resources across the corporate datacenter and into the cloud, enabling additional levels of validation such as multi-factor authentication and conditional access policies.</span></span> <span data-ttu-id="81505-106">En surveillant les activités suspectes via les fonctions avancées de reporting, d’audit et d’alertes de sécurité, vous êtes en mesure de limiter les problèmes de sécurité potentiels.</span><span class="sxs-lookup"><span data-stu-id="81505-106">Monitoring suspicious activity through advanced security reporting, auditing and alerting helps mitigate potential security issues.</span></span> <span data-ttu-id="81505-107">[Azure Active Directory Premium](../active-directory/active-directory-editions.md) fournit une authentification unique à des milliers d’applications cloud (SaaS) et assure un accès aux applications web que vous exécutez en local.</span><span class="sxs-lookup"><span data-stu-id="81505-107">[Azure Active Directory Premium](../active-directory/active-directory-editions.md) provides single sign-on to thousands of cloud (SaaS) apps and access to web apps you run on-premises.</span></span>

<span data-ttu-id="81505-108">Azure Active Directory (AD) présente de nombreux avantages en termes de sécurité :</span><span class="sxs-lookup"><span data-stu-id="81505-108">Security benefits of Azure Active Directory (AD) include the ability to:</span></span>

* <span data-ttu-id="81505-109">Création et gestion d’une identité unique pour chaque utilisateur de l’entreprise hybride, ce qui favorise la synchronisation des utilisateurs, des groupes et des appareils</span><span class="sxs-lookup"><span data-stu-id="81505-109">Create and manage a single identity for each user across your hybrid enterprise, keeping users, groups, and devices in sync</span></span>
* <span data-ttu-id="81505-110">Fourniture d’un accès par authentification unique à vos applications, y compris à des milliers d’applications SaaS pré-intégrées</span><span class="sxs-lookup"><span data-stu-id="81505-110">Provide single sign-on access to your applications including thousands of pre-integrated SaaS apps</span></span>
* <span data-ttu-id="81505-111">Activation de la sécurité d’accès aux applications en appliquant l’authentification multi-facteur basée sur des règles aussi bien pour les applications locales que pour les applications cloud</span><span class="sxs-lookup"><span data-stu-id="81505-111">Enable application access security by enforcing rules-based Multi-Factor Authentication for both on-premises and cloud applications</span></span>
* <span data-ttu-id="81505-112">Fourniture d’un accès à distance sécurisé aux applications web locales via le proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="81505-112">Provision secure remote access to on-premises web applications through Azure AD Application Proxy</span></span>

<span data-ttu-id="81505-113">Cet article vise à fournir une vue d’ensemble des principales fonctionnalités de sécurité Azure liées à la gestion des identités.</span><span class="sxs-lookup"><span data-stu-id="81505-113">The goal of this article is to provide an overview of the core Azure security features that help with identity management.</span></span> <span data-ttu-id="81505-114">Il contient également des liens vers des articles fournissant des informations complémentaires sur chaque fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="81505-114">We also provide links to articles that give details of each feature so you can learn more.</span></span>  

<span data-ttu-id="81505-115">Cet article se concentre sur les principales fonctionnalités de gestion d’identité Azure, à savoir :</span><span class="sxs-lookup"><span data-stu-id="81505-115">The article focuses on the following core Azure Identity management capabilities:</span></span>

* <span data-ttu-id="81505-116">Authentification unique</span><span class="sxs-lookup"><span data-stu-id="81505-116">Single sign-on</span></span>
* <span data-ttu-id="81505-117">Proxy inversé</span><span class="sxs-lookup"><span data-stu-id="81505-117">Reverse proxy</span></span>
* <span data-ttu-id="81505-118">Authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="81505-118">Multi-factor authentication</span></span>
* <span data-ttu-id="81505-119">Surveillance de la sécurité, alertes et rapports Machine Learning</span><span class="sxs-lookup"><span data-stu-id="81505-119">Security monitoring, alerts, and machine learning-based reports</span></span>
* <span data-ttu-id="81505-120">Gestion des identités et des accès des consommateurs</span><span class="sxs-lookup"><span data-stu-id="81505-120">Consumer identity and access management</span></span>
* <span data-ttu-id="81505-121">Inscription des appareils</span><span class="sxs-lookup"><span data-stu-id="81505-121">Device registration</span></span>
* <span data-ttu-id="81505-122">Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="81505-122">Privileged identity management</span></span>
* <span data-ttu-id="81505-123">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="81505-123">Identity protection</span></span>
* <span data-ttu-id="81505-124">Gestion des identités hybrides</span><span class="sxs-lookup"><span data-stu-id="81505-124">Hybrid identity management</span></span>

## <a name="single-sign-on"></a><span data-ttu-id="81505-125">Authentification unique</span><span class="sxs-lookup"><span data-stu-id="81505-125">Single sign-on</span></span>
<span data-ttu-id="81505-126">Avec l’authentification unique (SSO), vous pouvez accéder à toutes les applications et à toutes les ressources dont vous avez besoin pour travailler, en vous connectant une seule fois avec un seul compte utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81505-126">Single sign-on (SSO) means being able to access all the applications and resources that you need to do business, by signing in only once using a single user account.</span></span> <span data-ttu-id="81505-127">Une fois connecté, vous pouvez accéder à toutes les applications dont vous avez besoin sans devoir vous authentifier à nouveau (par exemple, taper un mot de passe).</span><span class="sxs-lookup"><span data-stu-id="81505-127">Once signed in, you can access all of the applications you need without being required to authenticate (for example, type a password) a second time.</span></span>

<span data-ttu-id="81505-128">De nombreuses entreprises s’appuient sur des applications SaaS comme Office 365, Box et Salesforce pour accroître la productivité des utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="81505-128">Many organizations rely upon software as a service (SaaS) applications such as Office 365, Box and Salesforce for end user productivity.</span></span> <span data-ttu-id="81505-129">Historiquement, le personnel informatique devait créer et mettre à jour chaque compte d’utilisateur dans chaque application SaaS et les utilisateurs devaient mémoriser un mot de passe pour chaque application SaaS.</span><span class="sxs-lookup"><span data-stu-id="81505-129">Historically, IT staff needed to individually create and update user accounts in each SaaS application, and users had to remember a password for each SaaS application.</span></span>

<span data-ttu-id="81505-130">Azure AD étend les environnements Active Directory local dans le cloud, ce qui permet aux utilisateurs d’utiliser leur compte professionnel principal, non seulement pour se connecter à leurs appareils liés au domaine et aux ressources de l’entreprise, mais aussi à toutes les applications SaaS et web nécessaires à leur travail.</span><span class="sxs-lookup"><span data-stu-id="81505-130">Azure AD extends on-premises Active Directory environments into the cloud, enabling users to use their primary organizational account to not only sign in to their domain-joined devices and company resources, but also all the web and SaaS applications needed for their job.</span></span>

<span data-ttu-id="81505-131">Non seulement les utilisateurs n’ont plus besoin de gérer plusieurs noms d’utilisateur et mots de passe, mais l’accès aux applications peut être automatiquement activé ou désactivé en fonction des groupes de l’organisation et de leur statut d’employé.</span><span class="sxs-lookup"><span data-stu-id="81505-131">Not only do users not have to manage multiple sets of usernames and passwords, application access can be automatically provisioned or de-provisioned based on organizational groups and their status as an employee.</span></span> <span data-ttu-id="81505-132">Azure AD ajoute des contrôles de sécurité et de gouvernance de l’accès qui vous permettent de gérer de manière centralisée l’accès des utilisateurs sur les différentes applications SaaS.</span><span class="sxs-lookup"><span data-stu-id="81505-132">Azure AD introduces security and access governance controls that enable you to centrally manage users' access across SaaS applications.</span></span>

<span data-ttu-id="81505-133">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="81505-133">Learn more:</span></span>

* [<span data-ttu-id="81505-134">Présentation de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="81505-134">Overview of Single Sign-On</span></span>](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)
* [<span data-ttu-id="81505-135">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="81505-135">What is application access and single sign-on with Azure Active Directory?</span></span>](../active-directory/active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="81505-136">Intégrer l’authentification unique Azure Active Directory aux applications SaaS</span><span class="sxs-lookup"><span data-stu-id="81505-136">Integrate Azure Active Directory single sign-on with SaaS apps</span></span>](../active-directory/active-directory-sso-integrate-saas-apps.md)

## <a name="reverse-proxy"></a><span data-ttu-id="81505-137">Proxy inversé</span><span class="sxs-lookup"><span data-stu-id="81505-137">Reverse proxy</span></span>
<span data-ttu-id="81505-138">Le proxy d’application Azure AD vous permet de publier des applications en local, telles que des sites [SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US), des [applications web Outlook](https://technet.microsoft.com/library/jj657718.aspx) et des applications [IIS](http://www.iis.net/) à l’intérieur de votre réseau privé et offre un accès sécurisé aux utilisateurs en dehors de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="81505-138">Azure AD Application Proxy lets you publish on-premises applications, such as [SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US) sites, [Outlook Web App](https://technet.microsoft.com/library/jj657718.aspx), and [IIS](http://www.iis.net/)-based apps inside your private network and provides secure access to users outside your network.</span></span> <span data-ttu-id="81505-139">Le proxy d’application assure l’accès à distance et l’authentification unique (SSO) pour de nombreux types d’applications web locales, avec les milliers d’applications SaaS prises en charge par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81505-139">Application Proxy provides remote access and single sign-on (SSO) for many types of on-premises web applications with the thousands of SaaS applications that Azure AD supports.</span></span> <span data-ttu-id="81505-140">Les employés peuvent se connecter à vos applications depuis leur domicile sur leurs propres appareils et s’authentifier par le biais de ce proxy cloud.</span><span class="sxs-lookup"><span data-stu-id="81505-140">Employees can log in to your apps from home on their own devices and authenticate through this cloud-based proxy.</span></span>

<span data-ttu-id="81505-141">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="81505-141">Learn more:</span></span>

* [<span data-ttu-id="81505-142">Activation du proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="81505-142">Enabling Azure AD Application Proxy</span></span>](../active-directory/active-directory-application-proxy-enable.md)
* [<span data-ttu-id="81505-143">Publier des applications avec le Proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="81505-143">Publish applications using Azure AD Application Proxy</span></span>](../active-directory/active-directory-application-proxy-publish.md)
* [<span data-ttu-id="81505-144">Authentification unique avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="81505-144">Single-sign-on with Application Proxy</span></span>](../active-directory/active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="81505-145">Utilisation de l’accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="81505-145">Working with conditional access</span></span>](../active-directory/active-directory-application-proxy-conditional-access.md)

## <a name="multi-factor-authentication"></a><span data-ttu-id="81505-146">Authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="81505-146">Multi-factor authentication</span></span>
<span data-ttu-id="81505-147">Azure Multi-Factor Authentication (MFA) est une méthode d’authentification qui nécessite l’utilisation de plusieurs méthodes de vérification et ajoute une deuxième couche critique de sécurité aux connexions et transactions des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="81505-147">Azure Multi-factor authentication (MFA) is a method of authentication that requires the use of more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="81505-148">MFA contribue à sécuriser l’accès aux données et aux applications tout en répondant à la demande des utilisateurs souhaitant un processus d’authentification simple.</span><span class="sxs-lookup"><span data-stu-id="81505-148">MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="81505-149">Elle fournit une authentification forte par le biais de diverses options de vérification : appel téléphonique, SMS, notification par application mobile ou code de vérification et jetons OAuth tiers.</span><span class="sxs-lookup"><span data-stu-id="81505-149">It delivers strong authentication via a range of verification options—phone call, text message, or mobile app notification or verification code and third party OAuth tokens.</span></span>

<span data-ttu-id="81505-150">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="81505-150">Learn more:</span></span>

* [<span data-ttu-id="81505-151">Authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="81505-151">Multi-factor authentication</span></span>](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [<span data-ttu-id="81505-152">Présentation d'Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="81505-152">What is Azure Multi-Factor Authentication?</span></span>](../multi-factor-authentication/multi-factor-authentication.md)
* [<span data-ttu-id="81505-153">Azure Multi-Factor Authentication : fonctionnement</span><span class="sxs-lookup"><span data-stu-id="81505-153">How Azure Multi-Factor Authentication works</span></span>](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a><span data-ttu-id="81505-154">Surveillance de la sécurité, alertes et rapports Machine Learning</span><span class="sxs-lookup"><span data-stu-id="81505-154">Security monitoring, alerts, and machine learning-based reports</span></span>
<span data-ttu-id="81505-155">Vous pouvez protéger votre entreprise grâce à la surveillance de la sécurité, aux alertes et aux rapports Machine Learning qui identifient les comportements d’accès incohérents.</span><span class="sxs-lookup"><span data-stu-id="81505-155">Security monitoring and alerts and machine learning-based reports that identify inconsistent access patterns can help you protect your business.</span></span> <span data-ttu-id="81505-156">Vous pouvez utiliser les rapports d'accès et d'utilisation Azure Active Directory pour obtenir une visibilité complète sur l'intégrité et la sécurité du répertoire de votre société.</span><span class="sxs-lookup"><span data-stu-id="81505-156">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="81505-157">Grâce à ces informations, un administrateur de répertoire est capable de déterminer plus précisément les risques de sécurité potentiels et donc de les atténuer au maximum.</span><span class="sxs-lookup"><span data-stu-id="81505-157">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="81505-158">Dans le portail Azure Classic, les rapports sont classés comme suit :</span><span class="sxs-lookup"><span data-stu-id="81505-158">In the Azure classic portal, reports are categorized in the following ways:</span></span>

* <span data-ttu-id="81505-159">Rapports d’anomalies : contiennent les événements de connexion qui peuvent nous sembler anormaux.</span><span class="sxs-lookup"><span data-stu-id="81505-159">Anomaly reports – contain sign in events that we found to be anomalous.</span></span> <span data-ttu-id="81505-160">Notre objectif est de vous faire part de ces activités et de vous permettre de déterminer si un événement est suspect.</span><span class="sxs-lookup"><span data-stu-id="81505-160">Our goal is to make you aware of such activity and enable you to be able to make a determination about whether an event is suspicious.</span></span>
* <span data-ttu-id="81505-161">Rapports d’application intégrée : fournissent des indications sur l’utilisation des applications du cloud au sein de votre société.</span><span class="sxs-lookup"><span data-stu-id="81505-161">Integrated Application reports – provide insights into how cloud applications are being used in your organization.</span></span> <span data-ttu-id="81505-162">Azure Active Directory permet d’intégrer des milliers d'applications du cloud.</span><span class="sxs-lookup"><span data-stu-id="81505-162">Azure Active Directory offers integration with thousands of cloud applications.</span></span>
* <span data-ttu-id="81505-163">Rapports d’erreurs : indiquent les erreurs qui peuvent survenir lors de la configuration de comptes sur des applications externes.</span><span class="sxs-lookup"><span data-stu-id="81505-163">Error reports – indicate errors that may occur when provisioning accounts to external applications.</span></span>
* <span data-ttu-id="81505-164">Rapports spécifiques à l’utilisateur : affichent les données d’activité relatives aux appareils/connexions d’un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="81505-164">User-specific reports – display device/sign in activity data for a specific user.</span></span>
* <span data-ttu-id="81505-165">Journaux d’activité : contiennent un enregistrement de tous les événements audités durant les dernières 24 heures, les derniers 7 jours ou les derniers 30 jours, des modifications d’activité de groupes, et des activités d’enregistrement et de réinitialisation de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="81505-165">Activity logs – contain a record of all audited events within the last 24 hours, last 7 days, or last 30 days, and group activity changes, and password reset and registration activity.</span></span>

<span data-ttu-id="81505-166">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="81505-166">Learn more:</span></span>

* [<span data-ttu-id="81505-167">Affichage de vos rapports d’accès et d’utilisation</span><span class="sxs-lookup"><span data-stu-id="81505-167">View your access and usage reports</span></span>](../active-directory/active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="81505-168">Prise en main de la création de rapports Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81505-168">Getting started with Azure Active Directory Reporting</span></span>](../active-directory/active-directory-reporting-getting-started.md)
* [<span data-ttu-id="81505-169">Guide Azure Active Directory Reporting Guide</span><span class="sxs-lookup"><span data-stu-id="81505-169">Azure Active Directory Reporting Guide</span></span>](../active-directory/active-directory-reporting-guide.md)

## <a name="consumer-identity-and-access-management"></a><span data-ttu-id="81505-170">Gestion des identités et des accès des consommateurs</span><span class="sxs-lookup"><span data-stu-id="81505-170">Consumer identity and access management</span></span>
<span data-ttu-id="81505-171">Pour les applications utilisées par les consommateurs, Azure Active Directory B2C offre un service de gestion de l’identité global et hautement disponible, qui s’adapte à des centaines de millions d’identités.</span><span class="sxs-lookup"><span data-stu-id="81505-171">Azure Active Directory B2C is a highly available, global, identity management service for consumer-facing applications that scales to hundreds of millions of identities.</span></span> <span data-ttu-id="81505-172">Le service peut être intégré sur l’ensemble des plateformes web et mobiles.</span><span class="sxs-lookup"><span data-stu-id="81505-172">It can be integrated across mobile and web platforms.</span></span> <span data-ttu-id="81505-173">Vos consommateurs peuvent se connecter à toutes vos applications via une expérience personnalisable en utilisant leurs comptes de réseaux sociaux existants ou en créant des comptes avec de nouvelles informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="81505-173">Your consumers can log on to all your applications through customizable experiences by using their existing social accounts or by creating new credentials.</span></span>

<span data-ttu-id="81505-174">Dans le passé, les développeurs d'applications qui souhaitaient inscrire et connecter les consommateurs à leurs applications écrivaient leur propre code.</span><span class="sxs-lookup"><span data-stu-id="81505-174">In the past, application developers who wanted to sign up and sign in consumers into their applications would have written their own code.</span></span> <span data-ttu-id="81505-175">Et ils auraient utilisé des systèmes ou des bases de données locaux pour stocker les noms d'utilisateur et les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="81505-175">And they would have used on-premises databases or systems to store usernames and passwords.</span></span> <span data-ttu-id="81505-176">Azure Active Directory B2C offre à votre organisation un meilleur moyen d’intégrer la gestion des identités des consommateurs dans vos applications à l’aide d’une plateforme sécurisée basée sur des normes et d’un ensemble complet de stratégies extensibles.</span><span class="sxs-lookup"><span data-stu-id="81505-176">Azure Active Directory B2C offers your organization a better way to integrate consumer identity management into applications with the help of a secure, standards-based platform and a large set of extensible policies.</span></span>

<span data-ttu-id="81505-177">Lorsque vous utilisez Azure Active Directory B2C, vos consommateurs peuvent s’inscrire auprès de vos applications à l’aide de leurs comptes sociaux existants (Facebook, Google, Amazon, LinkedIn) ou en créant des informations d’identification (adresse de messagerie et mot de passe, ou nom d’utilisateur et mot de passe).</span><span class="sxs-lookup"><span data-stu-id="81505-177">When you use Azure Active Directory B2C, your consumers can sign up for your applications by using their existing social accounts (Facebook, Google, Amazon, LinkedIn) or by creating new credentials (email address and password, or username and password).</span></span>

<span data-ttu-id="81505-178">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="81505-178">Learn more:</span></span>

* [<span data-ttu-id="81505-179">Qu’est-ce qu’Azure Active Directory B2C ?</span><span class="sxs-lookup"><span data-stu-id="81505-179">What is Azure Active Directory B2C?</span></span>](https://azure.microsoft.com/services/active-directory-b2c/)
* [<span data-ttu-id="81505-180">Azure Active Directory B2C en version préliminaire : Inscription et connexion de consommateurs à vos applications</span><span class="sxs-lookup"><span data-stu-id="81505-180">Azure Active Directory B2C preview: Sign up and sign in consumers in your applications</span></span>](../active-directory-b2c/active-directory-b2c-overview.md)
* [<span data-ttu-id="81505-181">Version préliminaire d’Azure Active Directory B2C : types d’applications</span><span class="sxs-lookup"><span data-stu-id="81505-181">Azure Active Directory B2C Preview: Types of Applications</span></span>](../active-directory-b2c/active-directory-b2c-apps.md)

## <a name="device-registration"></a><span data-ttu-id="81505-182">Enregistrement de l’appareil</span><span class="sxs-lookup"><span data-stu-id="81505-182">Device registration</span></span>
<span data-ttu-id="81505-183">Azure AD Device Registration est la base des scénarios d’ [accès conditionnel](../active-directory/active-directory-conditional-access-device-registration-overview.md) en fonction de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="81505-183">Azure AD Device Registration is the foundation for device-based [conditional access](../active-directory/active-directory-conditional-access-device-registration-overview.md) scenarios.</span></span> <span data-ttu-id="81505-184">Lors de l’inscription d’un appareil, Azure Active Directory Device Registration fournit une identité à l’appareil qui sera utilisée pour authentifier l’appareil lors de la connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="81505-184">When a device is registered, Azure Active Directory Device Registration provides the device with an identity that is used to authenticate the device when the user signs in.</span></span> <span data-ttu-id="81505-185">L’appareil authentifié et les attributs de l’appareil peuvent alors être utilisés pour appliquer des stratégies d’accès conditionnel pour les applications qui sont hébergées sur le cloud et localement.</span><span class="sxs-lookup"><span data-stu-id="81505-185">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span></span>

<span data-ttu-id="81505-186">Quand ils sont associés à une solution de gestion des appareils mobiles comme Intune, les attributs de l’appareil dans Azure Active Directory sont mis à jour avec des informations supplémentaires sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="81505-186">When combined with a mobile device management (MDM) solution such as Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span></span> <span data-ttu-id="81505-187">Cela vous permet de créer des règles d’accès conditionnel qui imposent que l’accès à partir des appareils réponde à vos normes de sécurité et de conformité.</span><span class="sxs-lookup"><span data-stu-id="81505-187">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span>

<span data-ttu-id="81505-188">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="81505-188">Learn more:</span></span>

* [<span data-ttu-id="81505-189">Prise en main du service Azure Active Directory Device Registration</span><span class="sxs-lookup"><span data-stu-id="81505-189">Get started with Azure Active Directory Device Registration</span></span>](../active-directory/active-directory-conditional-access-device-registration-overview.md)
* [<span data-ttu-id="81505-190">Inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine</span><span class="sxs-lookup"><span data-stu-id="81505-190">Automatic device registration with Azure Active Directory for Windows domain-joined devices</span></span>](../active-directory/active-directory-conditional-access-automatic-device-registration.md)
* [<span data-ttu-id="81505-191">Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine</span><span class="sxs-lookup"><span data-stu-id="81505-191">Set up automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>](../active-directory/active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="privileged-identity-management"></a><span data-ttu-id="81505-192">Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="81505-192">Privileged identity management</span></span>
<span data-ttu-id="81505-193">Le service Azure Active Directory (AD) Privileged Identity Management vous permet de gérer, de contrôler et de surveiller vos identités privilégiées et l’accès aux ressources dans Azure AD et dans d’autres services en ligne Microsoft tels qu’Office 365 ou Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="81505-193">Azure Active Directory (AD) Privileged Identity Management lets you manage, control, and monitor your privileged identities and access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="81505-194">Les utilisateurs doivent parfois effectuer des opérations privilégiées dans des ressources Azure ou Office 365, ou dans d'autres applications SaaS.</span><span class="sxs-lookup"><span data-stu-id="81505-194">Sometimes users need to carry out privileged operations in Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="81505-195">Cela signifie souvent que les entreprises doivent leur donner un accès privilégié permanent à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81505-195">This often means organizations have to give them permanent privileged access in Azure AD.</span></span> <span data-ttu-id="81505-196">C’est un risque de sécurité croissant pour les ressources hébergées dans le cloud, car les entreprises ne peuvent pas suffisamment surveiller ce que ces utilisateurs font avec leurs privilèges d'administrateur.</span><span class="sxs-lookup"><span data-stu-id="81505-196">This is a growing security risk for cloud-hosted resources because organizations can't sufficiently monitor what those users are doing with their admin privileges.</span></span> <span data-ttu-id="81505-197">En outre, si un compte d’utilisateur disposant d’un accès privilégié est compromis, cette seule faille peut affecter sa sécurité globale sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="81505-197">Additionally, if a user account with privileged access is compromised, that one breach could impact their overall cloud security.</span></span> <span data-ttu-id="81505-198">Azure AD Privileged Identity Management contribue à minimiser ce risque.</span><span class="sxs-lookup"><span data-stu-id="81505-198">Azure AD Privileged Identity Management helps to resolve this risk.</span></span>

<span data-ttu-id="81505-199">Grâce à Azure AD Privileged Identity Management, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="81505-199">Azure AD Privileged Identity Management lets you:</span></span>

* <span data-ttu-id="81505-200">Identifier les utilisateurs qui ont un rôle d’administrateur dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="81505-200">See which users are Azure AD admins</span></span>
* <span data-ttu-id="81505-201">Activer à la demande un accès administrateur « juste à temps » aux services Microsoft Online Services comme Office 365 et Intune</span><span class="sxs-lookup"><span data-stu-id="81505-201">Enable on-demand, "just in time" administrative access to Microsoft Online Services like Office 365 and Intune</span></span>
* <span data-ttu-id="81505-202">Obtenir des rapports sur l'historique des accès administrateur et sur les modifications apportées aux affectations de l'administrateur</span><span class="sxs-lookup"><span data-stu-id="81505-202">Get reports about administrator access history and changes in administrator assignments</span></span>
* <span data-ttu-id="81505-203">Recevoir des alertes sur l'accès à un rôle privilégié</span><span class="sxs-lookup"><span data-stu-id="81505-203">Get alerts about access to a privileged role</span></span>

<span data-ttu-id="81505-204">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="81505-204">Learn more:</span></span>

* [<span data-ttu-id="81505-205">Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="81505-205">Azure AD Privileged Identity Management</span></span>](../active-directory/active-directory-privileged-identity-management-configure.md)
* [<span data-ttu-id="81505-206">Rôles dans Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="81505-206">Roles in Azure AD Privileged Identity Management</span></span>](../active-directory/active-directory-privileged-identity-management-roles.md)
* [<span data-ttu-id="81505-207">Azure AD Privileged Identity Management : comment ajouter ou supprimer un rôle d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="81505-207">Azure AD Privileged Identity Management: How to add or remove a user role</span></span>](../active-directory/active-directory-privileged-identity-management-how-to-add-role-to-user.md)

## <a name="identity-protection"></a><span data-ttu-id="81505-208">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="81505-208">Identity protection</span></span>
<span data-ttu-id="81505-209">Azure AD Identity Protection est un service de sécurité offrant une vue consolidée des événements à risque et des vulnérabilités potentielles qui affectent les identités de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="81505-209">Azure AD Identity Protection is a security service that provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="81505-210">Identity Protection tire parti des fonctionnalités existantes de détection des anomalies d’Azure Active Directory (disponibles via les rapports d’activités anormales d’Azure AD) et introduit de nouveaux types d’événements à risque capables de détecter les anomalies en temps réel.</span><span class="sxs-lookup"><span data-stu-id="81505-210">Identity Protection leverages existing Azure Active Directory’s anomaly detection capabilities (available through Azure AD’s Anomalous Activity Reports), and introduces new risk event types that can detect anomalies in real-time.</span></span>

<span data-ttu-id="81505-211">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="81505-211">Learn more:</span></span>

* [<span data-ttu-id="81505-212">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="81505-212">Azure Active Directory Identity Protection</span></span>](../active-directory/active-directory-identityprotection.md)
* [<span data-ttu-id="81505-213">Channel 9 : Azure AD and Identity Show: Identity Protection Preview (Émission sur Azure AD et l’identité : présentation d’Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="81505-213">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="hybrid-identity-management"></a><span data-ttu-id="81505-214">Gestion des identités hybrides</span><span class="sxs-lookup"><span data-stu-id="81505-214">Hybrid identity management</span></span>
<span data-ttu-id="81505-215">L’approche d’identité de Microsoft s’étend aussi bien au cloud qu’à l’environnement local pour créer une identité d’utilisateur unique pour l’authentification et l’autorisation d’accès à toutes les ressources, indépendamment de l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="81505-215">Microsoft’s approach to identity spans on-premises and the cloud, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span>

<span data-ttu-id="81505-216">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="81505-216">Learn more:</span></span>

* [<span data-ttu-id="81505-217">Livre blanc sur les identités hybrides</span><span class="sxs-lookup"><span data-stu-id="81505-217">Hybrid identity white paper</span></span>](http://download.microsoft.com/download/D/B/A/DBA9E313-B833-48EE-998A-240AA799A8AB/Hybrid_Identity_White_Paper.pdf)
* [<span data-ttu-id="81505-218">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81505-218">Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/services/active-directory/)
* [<span data-ttu-id="81505-219">Blog de l’équipe Active Directory</span><span class="sxs-lookup"><span data-stu-id="81505-219">Active Directory Team Blog</span></span>](https://blogs.technet.microsoft.com/ad/)