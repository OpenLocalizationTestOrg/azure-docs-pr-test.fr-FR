---
title: "aaaTroubleshooting hybride Azure Active Directory joint des périphériques de bas niveau | Documents Microsoft"
description: "Dépannez des appareils hybrides de bas niveau joints à Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="3d870-103">Dépanner des appareils hybrides de bas niveau joints à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d870-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="3d870-104">Cette rubrique est applicable toohello uniquement suivant des appareils :</span><span class="sxs-lookup"><span data-stu-id="3d870-104">This topic is applicable only toohello following devices:</span></span> 

- <span data-ttu-id="3d870-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="3d870-105">Windows 7</span></span> 
- <span data-ttu-id="3d870-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="3d870-106">Windows 8.1</span></span> 
- <span data-ttu-id="3d870-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="3d870-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="3d870-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3d870-108">Windows Server 2012</span></span> 
- <span data-ttu-id="3d870-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3d870-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="3d870-110">Pour Windows 10 ou Windows Server 2016, consultez la page [Dépanner des appareils hybrides Windows 10 et Windows Server 2016 joints à Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-current.md).</span><span class="sxs-lookup"><span data-stu-id="3d870-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="3d870-111">Cette rubrique suppose que vous avez [configuré hybride Azure Active Directory des appareils joints à un](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="3d870-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="3d870-112">Accès conditionnel basé sur les appareils</span><span class="sxs-lookup"><span data-stu-id="3d870-112">Device-based conditional access</span></span>

- [<span data-ttu-id="3d870-113">Itinérance d’entreprise des paramètres</span><span class="sxs-lookup"><span data-stu-id="3d870-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="3d870-114">Windows Hello Entreprise</span><span class="sxs-lookup"><span data-stu-id="3d870-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="3d870-115">Cette rubrique fournit des conseils sur la façon dont des problèmes potentiels de tooresolve de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="3d870-115">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  

<span data-ttu-id="3d870-116">**Bon à savoir :**</span><span class="sxs-lookup"><span data-stu-id="3d870-116">**What you should know:**</span></span> 

- <span data-ttu-id="3d870-117">nombre maximal de Hello de périphériques par utilisateur est centré sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3d870-117">hello maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="3d870-118">Par exemple, si *jdoe* et *jharnett* tooa connexion périphérique, un enregistrement distinct (DeviceID) est créé pour chacun d’eux Bonjour **utilisateur** onglet info.</span><span class="sxs-lookup"><span data-stu-id="3d870-118">For example, if *jdoe* and *jharnett* sign-in tooa device, a separate registration (DeviceID) is created for each of them in hello **USER** info tab.</span></span>  

- <span data-ttu-id="3d870-119">l’inscription initiale de Hello / joindre des appareils est configuré tooperform une tentative d’ouverture de session ou verrouiller / déverrouiller.</span><span class="sxs-lookup"><span data-stu-id="3d870-119">hello initial registration / join of devices is configured tooperform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="3d870-120">Un délai de cinq minutes peut être déclenché par une tâche du Planificateur de tâches.</span><span class="sxs-lookup"><span data-stu-id="3d870-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="3d870-121">Une réinstallation du système d’exploitation de hello ou une manuelle annuler l’inscription et réinscrivez peuvent créer une nouvelle inscription sur Azure AD et résultats dans plusieurs entrées sous l’onglet d’informations utilisateur hello dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3d870-121">A reinstall of hello operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="3d870-122">Étape 1 : Récupération de l’état de l’inscription de hello</span><span class="sxs-lookup"><span data-stu-id="3d870-122">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="3d870-123">**état de l’inscription de hello tooverify :**</span><span class="sxs-lookup"><span data-stu-id="3d870-123">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="3d870-124">Invite de commandes ouverte hello en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="3d870-124">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="3d870-125">Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="3d870-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="3d870-126">Cette commande affiche une boîte de dialogue qui vous offre plus de détails sur l’état de jointure hello.</span><span class="sxs-lookup"><span data-stu-id="3d870-126">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a><span data-ttu-id="3d870-128">Étape 2 : Évaluer l’état de jointure hello hybrides Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d870-128">Step 2: Evaluate hello hybrid Azure AD join status</span></span> 

<span data-ttu-id="3d870-129">Si la jointure de hello hybrides Azure AD n’a pas réussi, boîte de dialogue hello vous offre plus d’informations sur le problème hello qui s’est produite.</span><span class="sxs-lookup"><span data-stu-id="3d870-129">If hello hybrid Azure AD join was not successful, hello dialog box provides you with details about hello issue that has occurred.</span></span>

<span data-ttu-id="3d870-130">**les problèmes les plus courants Hello sont :**</span><span class="sxs-lookup"><span data-stu-id="3d870-130">**hello most common issues are:**</span></span>

- <span data-ttu-id="3d870-131">Une mauvaise configuration d’AD FS ou d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d870-131">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="3d870-133">Vous n’êtes pas connecté en tant qu’utilisateur du domaine</span><span class="sxs-lookup"><span data-stu-id="3d870-133">You are not signed on as a domain user</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="3d870-135">Un quota a été atteint.</span><span class="sxs-lookup"><span data-stu-id="3d870-135">A quota has been reached</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="3d870-137">Hello service ne répond pas</span><span class="sxs-lookup"><span data-stu-id="3d870-137">hello service is not responding</span></span> 

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="3d870-139">Vous trouverez également des informations d’état hello dans le journal des événements hello sous **Applications et Services Log\Microsoft-jonction**.</span><span class="sxs-lookup"><span data-stu-id="3d870-139">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="3d870-140">**causes les plus courantes Hello pour une jointure de Azure AD hybride ayant échoué sont :**</span><span class="sxs-lookup"><span data-stu-id="3d870-140">**hello most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="3d870-141">Votre ordinateur n’est pas sur le réseau interne de hello organisation ou un réseau privé virtuel sans connexion tooan locaux contrôleur de domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d870-141">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="3d870-142">Vous êtes connecté sur l’ordinateur tooyour avec un compte d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="3d870-142">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="3d870-143">Problèmes de configuration du service :</span><span class="sxs-lookup"><span data-stu-id="3d870-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="3d870-144">Hello serveur de fédération a été configuré toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="3d870-144">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="3d870-145">Il n’existe aucun objet de Point de connexion qui pointe le nom de domaine vérifié tooyour dans Azure AD dans la forêt hello AD où appartient hello ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3d870-145">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="3d870-146">Un utilisateur a atteint la limite de hello des périphériques.</span><span class="sxs-lookup"><span data-stu-id="3d870-146">A user has reached hello limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3d870-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3d870-147">Next steps</span></span>

<span data-ttu-id="3d870-148">Pour toute question, consultez hello [Forum aux questions sur la gestion des appareils](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="3d870-148">For questions, see hello [device management FAQ](device-management-faq.md)</span></span>  
