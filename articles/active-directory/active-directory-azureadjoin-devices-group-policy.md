---
title: "expériences d’aaaConnect tooAzure de périphériques joints au domaine Active Directory pour Windows 10 | Documents Microsoft"
description: "Explique comment les administrateurs peuvent configurer réseau d’entreprise de stratégie de groupe tooenable périphériques toobe toohello de joints au domaine."
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
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a><span data-ttu-id="fd0dc-103">Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="fd0dc-103">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>
<span data-ttu-id="fd0dc-104">Jonction de domaine est organisations de manière standard hello connecté appareils pour le travail de hello cours des 15 dernières années et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-104">Domain join is hello traditional way organizations have connected devices for work for hello last 15 years and more.</span></span> <span data-ttu-id="fd0dc-105">Il a activé toosign d’utilisateurs dans les appareils tootheir à l’aide de leur travail de Windows Server Active Directory (Active Directory) ou comptes d’établissement scolaire et autorisées informatique toofully gérer ces appareils.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-105">It has enabled users toosign in tootheir devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT toofully manage these devices.</span></span> <span data-ttu-id="fd0dc-106">Les organisations reposent généralement sur l’acquisition d’images de méthodes tooprovision périphériques toousers et généralement utiliser System Center Configuration Manager (SCCM) ou la stratégie de groupe toomanage les.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-106">Organizations typically rely on imaging methods tooprovision devices toousers and generally use System Center Configuration Manager (SCCM) or Group Policy toomanage them.</span></span>


<span data-ttu-id="fd0dc-107">Jonction de domaine dans Windows 10 offre hello avantages suivants une fois que vous vous connectez les appareils tooAzure Active Directory (Azure AD) :</span><span class="sxs-lookup"><span data-stu-id="fd0dc-107">Domain join in Windows 10 provides you with hello following benefits after you connect devices tooAzure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="fd0dc-108">Seul sign-on (SSO) tooAzure AD ressources depuis n’importe où</span><span class="sxs-lookup"><span data-stu-id="fd0dc-108">Single sign-on (SSO) tooAzure AD resources from anywhere</span></span>
* <span data-ttu-id="fd0dc-109">Accès toohello enterprise du Windows Store à l’aide de travail ou d’établissement scolaire (aucun compte Microsoft requis)</span><span class="sxs-lookup"><span data-stu-id="fd0dc-109">Access toohello enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="fd0dc-110">itinérance des paramètres utilisateur compatible pour l’entreprise sur tous les appareils avec un compte professionnel ou scolaire (aucun compte Microsoft requis) ;</span><span class="sxs-lookup"><span data-stu-id="fd0dc-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="fd0dc-111">authentification forte et connexion pratique pour les comptes professionnels ou scolaires avec Windows Hello Entreprise et Windows Hello ;</span><span class="sxs-lookup"><span data-stu-id="fd0dc-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="fd0dc-112">Capacité toorestrict accéder uniquement toodevices qui sont conformes aux paramètres de stratégie de groupe d’unité d’organisation</span><span class="sxs-lookup"><span data-stu-id="fd0dc-112">Ability toorestrict access only toodevices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd0dc-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fd0dc-113">Prerequisites</span></span>
<span data-ttu-id="fd0dc-114">Jonction de domaine poursuit toobe utile.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-114">Domain join continues toobe useful.</span></span> <span data-ttu-id="fd0dc-115">Toutefois, tooget les avantages de hello Azure AD de l’authentification unique, l’itinérance des paramètres à l’aide de travail ou établissement scolaire et accéder au magasin de tooWindows avec un travail ou d’établissement scolaire, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="fd0dc-115">However, tooget hello Azure AD benefits of SSO, roaming of settings with work or school accounts, and access tooWindows Store with work or school accounts, you will need hello following:</span></span>

* <span data-ttu-id="fd0dc-116">Abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd0dc-116">Azure AD subscription</span></span>
* <span data-ttu-id="fd0dc-117">Azure AD Connect tooextend hello local active tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="fd0dc-117">Azure AD Connect tooextend hello on-premises directory tooAzure AD</span></span>
* <span data-ttu-id="fd0dc-118">Stratégie qui a défini tooconnect tooAzure de périphériques joints au domaine Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd0dc-118">Policy that's set tooconnect domain-joined devices tooAzure AD</span></span>
* <span data-ttu-id="fd0dc-119">Version de Windows 10 (version 10551 ou ultérieure) pour les appareils</span><span class="sxs-lookup"><span data-stu-id="fd0dc-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="fd0dc-120">tooenable Windows Hello entreprise et Windows Hello, vous aurez également besoin des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="fd0dc-120">tooenable Windows Hello for Business and Windows Hello, you will also need hello following:</span></span>

- <span data-ttu-id="fd0dc-121">**Infrastructure de clé publique (PKI)** pour l’émission de certificats utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="fd0dc-122">**Branche actuelle de System Center Configuration Manager** -vous devez tooinstall version 1606 ou supérieures.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-122">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span>  
<span data-ttu-id="fd0dc-123">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="fd0dc-123">For more information, see:</span></span> 
    - [<span data-ttu-id="fd0dc-124">Documentation de System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="fd0dc-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="fd0dc-125">Blog de l’équipe System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="fd0dc-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="fd0dc-126">Les paramètres Windows Hello Entreprise dans System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="fd0dc-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="fd0dc-127">En tant qu’une demande de déploiement toohello autre infrastructure à clé publique, vous pouvez effectuer les suivant hello :</span><span class="sxs-lookup"><span data-stu-id="fd0dc-127">As an alternative toohello PKI deployment requirement, you can do hello following:</span></span>

* <span data-ttu-id="fd0dc-128">Avoir quelques contrôleurs de domaine avec les services de domaine Active Directory Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="fd0dc-129">tooenable l’accès conditionnel, vous pouvez créer des paramètres de stratégie de groupe qui autorisent l’accès des périphériques appartenant à un toodomain avec des déploiements supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="fd0dc-129">tooenable conditional access, you can create Group Policy settings that allow access toodomain-joined devices with no additional deployments.</span></span> <span data-ttu-id="fd0dc-130">toomanage le contrôle d’accès basé sur la compatibilité du périphérique de hello, vous devrez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="fd0dc-130">toomanage access control based on compliance of hello device, you will need hello following:</span></span>

* <span data-ttu-id="fd0dc-131">System Center Configuration Manager Current Branch (version 1606 ou ultérieure) pour les scénarios Windows Hello Entreprise</span><span class="sxs-lookup"><span data-stu-id="fd0dc-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="fd0dc-132">Instructions de déploiement</span><span class="sxs-lookup"><span data-stu-id="fd0dc-132">Deployment instructions</span></span>

<span data-ttu-id="fd0dc-133">toodeploy, suivez les étapes de hello répertoriés dans [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="fd0dc-133">toodeploy, follow hello steps listed in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="fd0dc-134">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="fd0dc-134">Next step</span></span>
* [<span data-ttu-id="fd0dc-135">Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail</span><span class="sxs-lookup"><span data-stu-id="fd0dc-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="fd0dc-136">Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="fd0dc-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="fd0dc-137">En savoir plus sur les scénarios d’utilisation pour Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="fd0dc-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="fd0dc-138">Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="fd0dc-138">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="fd0dc-139">Configuration d’Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="fd0dc-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

