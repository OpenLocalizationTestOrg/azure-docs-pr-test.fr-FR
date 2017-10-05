---
title: "Connecter des appareils joints au domaine à Azure AD pour des expériences Windows 10 | Microsoft Docs"
description: "Explique comment les administrateurs peuvent configurer une stratégie de groupe pour permettre à des appareils d’être joints à un domaine du réseau d’entreprise."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a><span data-ttu-id="57131-103">Connecter des appareils joints au domaine à Azure AD pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="57131-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>
<span data-ttu-id="57131-104">La jonction de domaine est la méthode que les entreprises utilisent traditionnellement depuis une quinzaine d’années ou plus pour connecter leurs appareils professionnels.</span><span class="sxs-lookup"><span data-stu-id="57131-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span></span> <span data-ttu-id="57131-105">Elle permet aux utilisateurs de se connecter à leurs appareils avec leur compte professionnel ou scolaire Windows Server Active Directory et au service informatique de gérer intégralement ces appareils.</span><span class="sxs-lookup"><span data-stu-id="57131-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span></span> <span data-ttu-id="57131-106">En règle générale, les entreprises s'appuient sur des méthodes de création d'images pour mettre des appareils à la disposition des utilisateurs et utilisent System Center Configuration Manager (SCCM) ou une stratégie de groupe pour les gérer.</span><span class="sxs-lookup"><span data-stu-id="57131-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span></span>


<span data-ttu-id="57131-107">La jonction de domaine dans Windows 10 vous offre les avantages suivants après la connexion des appareils à Azure Active Directory (Azure AD) :</span><span class="sxs-lookup"><span data-stu-id="57131-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="57131-108">authentification unique (SSO) aux ressources Azure AD depuis n’importe où ;</span><span class="sxs-lookup"><span data-stu-id="57131-108">Single sign-on (SSO) to Azure AD resources from anywhere</span></span>
* <span data-ttu-id="57131-109">accès au Windows Store pour entreprises à l’aide de comptes professionnels ou scolaires (aucun compte Microsoft requis) ;</span><span class="sxs-lookup"><span data-stu-id="57131-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="57131-110">itinérance des paramètres utilisateur compatible pour l’entreprise sur tous les appareils avec un compte professionnel ou scolaire (aucun compte Microsoft requis) ;</span><span class="sxs-lookup"><span data-stu-id="57131-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="57131-111">authentification forte et connexion pratique pour les comptes professionnels ou scolaires avec Windows Hello Entreprise et Windows Hello ;</span><span class="sxs-lookup"><span data-stu-id="57131-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="57131-112">possibilité de restreindre l’accès aux appareils conformes aux paramètres de stratégie de groupe des appareils de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="57131-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57131-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="57131-113">Prerequisites</span></span>
<span data-ttu-id="57131-114">La jonction de domaine demeure utile.</span><span class="sxs-lookup"><span data-stu-id="57131-114">Domain join continues to be useful.</span></span> <span data-ttu-id="57131-115">Toutefois, pour bénéficier des avantages d’Azure AD pour l’authentification unique, de l’itinérance des paramètres avec un compte professionnel ou scolaire et de l’accès au Windows Store avec un compte professionnel ou scolaire, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="57131-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span></span>

* <span data-ttu-id="57131-116">Abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="57131-116">Azure AD subscription</span></span>
* <span data-ttu-id="57131-117">Azure AD Connect pour étendre l’annuaire local à Azure AD</span><span class="sxs-lookup"><span data-stu-id="57131-117">Azure AD Connect to extend the on-premises directory to Azure AD</span></span>
* <span data-ttu-id="57131-118">Stratégie définie pour connecter des appareils joints au domaine à Azure AD</span><span class="sxs-lookup"><span data-stu-id="57131-118">Policy that's set to connect domain-joined devices to Azure AD</span></span>
* <span data-ttu-id="57131-119">Version de Windows 10 (version 10551 ou ultérieure) pour les appareils</span><span class="sxs-lookup"><span data-stu-id="57131-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="57131-120">Pour activer Windows Hello Entreprise et Windows Hello, vous aurez également besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="57131-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span></span>

- <span data-ttu-id="57131-121">**Infrastructure de clé publique (PKI)** pour l’émission de certificats utilisateur.</span><span class="sxs-lookup"><span data-stu-id="57131-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="57131-122">**System Center Configuration Manager Current Branch** - Vous devez installer la version 1606 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="57131-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span>  
<span data-ttu-id="57131-123">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="57131-123">For more information, see:</span></span> 
    - [<span data-ttu-id="57131-124">Documentation de System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="57131-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="57131-125">Blog de l’équipe System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="57131-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="57131-126">Les paramètres Windows Hello Entreprise dans System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="57131-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="57131-127">En alternative à l'exigence de déploiement d'infrastructure à clé publique, vous pouvez procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="57131-127">As an alternative to the PKI deployment requirement, you can do the following:</span></span>

* <span data-ttu-id="57131-128">Avoir quelques contrôleurs de domaine avec les services de domaine Active Directory Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="57131-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="57131-129">Pour permettre un accès conditionnel, vous pouvez créer des paramètres de stratégie de groupe qui autorisent l’accès aux appareils joints au domaine sans déploiements supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="57131-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span></span> <span data-ttu-id="57131-130">Pour gérer le contrôle d’accès basé sur la conformité de l’appareil, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="57131-130">To manage access control based on compliance of the device, you will need the following:</span></span>

* <span data-ttu-id="57131-131">System Center Configuration Manager Current Branch (version 1606 ou ultérieure) pour les scénarios Windows Hello Entreprise</span><span class="sxs-lookup"><span data-stu-id="57131-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="57131-132">Instructions de déploiement</span><span class="sxs-lookup"><span data-stu-id="57131-132">Deployment instructions</span></span>

<span data-ttu-id="57131-133">Pour effectuer le déploiement, procédez comme indiqué dans [Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="57131-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="57131-134">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="57131-134">Next step</span></span>
* [<span data-ttu-id="57131-135">Windows 10 pour l’entreprise : plusieurs manières d’utiliser des appareils professionnels</span><span class="sxs-lookup"><span data-stu-id="57131-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="57131-136">Extension des fonctionnalités du cloud aux appareils Windows 10 via Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="57131-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="57131-137">En savoir plus sur les scénarios d’utilisation pour Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="57131-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="57131-138">Connecter des appareils joints au domaine à Azure AD pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="57131-138">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="57131-139">Configuration d’Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="57131-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

