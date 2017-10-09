---
title: "appareils aaaManaging à l’aide de hello portail Azure - version préliminaire | Documents Microsoft"
description: "Découvrez comment toouse hello les appareils toomanage portail Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a><span data-ttu-id="7da6d-103">La gestion des appareils à l’aide de hello portail Azure, afficher un aperçu</span><span class="sxs-lookup"><span data-stu-id="7da6d-103">Managing devices using hello Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="7da6d-104">Cette fonctionnalité est actuellement disponible en préversion publique.</span><span class="sxs-lookup"><span data-stu-id="7da6d-104">This capability currently is in public preview.</span></span> <span data-ttu-id="7da6d-105">Préparez-vous à toorevert ou supprimer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="7da6d-105">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="7da6d-106">Hello fonctionnalité est disponible dans n’importe quel abonnement Azure Active Directory (Azure AD) au cours de la version préliminaire publique.</span><span class="sxs-lookup"><span data-stu-id="7da6d-106">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="7da6d-107">Toutefois, lorsque la fonctionnalité de hello devient disponible de manière générale, certains aspects de la fonctionnalité de hello peuvent nécessiter un abonnement premium à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7da6d-107">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="7da6d-108">La fonction de gestion des appareils intégrée à Azure Active Directory (Azure AD) vous permet de vous assurer que vos utilisateurs accèdent à vos ressources à partir d’appareils qui répondent à vos normes de conformité et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="7da6d-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="7da6d-109">Cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="7da6d-109">This topic:</span></span>

- <span data-ttu-id="7da6d-110">Part du principe que vous êtes familiarisé avec hello [gestion toodevice de présentation dans Azure Active Directory](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="7da6d-110">Assumes that you are familiar with hello [introduction toodevice management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="7da6d-111">Fournit des informations sur la gestion de vos appareils à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7da6d-111">Provides you with information about managing your devices using hello Azure portal</span></span>


<span data-ttu-id="7da6d-112">appareils toomanage Bonjour portail Azure, vous devez tooclick **périphériques** Bonjour **gérer** section Bonjour Bonjour **Azure Active Directory** panneau.</span><span class="sxs-lookup"><span data-stu-id="7da6d-112">toomanage devices in hello Azure portal, you need tooclick **Devices** in hello **Manage** section of hello hello **Azure Active Directory** blade.</span></span>

![Gérer un appareil Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="7da6d-114">Configurer les paramètres de l’appareil</span><span class="sxs-lookup"><span data-stu-id="7da6d-114">Configure device settings</span></span>

<span data-ttu-id="7da6d-115">toomanage vos appareils à l’aide de hello portail Azure, ils doivent toobe inscrit ou joint tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="7da6d-115">toomanage your devices using hello Azure portal, they need toobe either registered or joined tooAzure AD.</span></span> <span data-ttu-id="7da6d-116">En tant qu’administrateur, vous pouvez affiner le processus de hello d’enregistrement et la jonction d’appareils en configurant les paramètres de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="7da6d-116">As an administrator, you can fine-tune hello process of registering and joining devices by configuring hello device settings.</span></span>

![Gérer un appareil Intune](./media/device-management-azure-portal/22.png)


<span data-ttu-id="7da6d-118">panneau des paramètres de périphérique Hello vous permet de tooconfigure :</span><span class="sxs-lookup"><span data-stu-id="7da6d-118">hello device settings blade enables you tooconfigure:</span></span>

- <span data-ttu-id="7da6d-119">**Les utilisateurs peuvent joindre des appareils tooAzure AD** - ce paramètres vous permet de tooselect hello les utilisateurs peuvent joindre des appareils tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="7da6d-119">**Users may join devices tooAzure AD** - This settings enables you tooselect hello users who can join devices tooAzure AD.</span></span> <span data-ttu-id="7da6d-120">valeur par défaut Hello est **tous les**.</span><span class="sxs-lookup"><span data-stu-id="7da6d-120">hello default is **All**.</span></span>

- <span data-ttu-id="7da6d-121">**Les administrateurs locaux supplémentaires sur Azure AD les appareils joints à un** -vous pouvez sélectionner des utilisateurs hello disposant de droits d’administrateur local sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="7da6d-121">**Additional local administrators on Azure AD joined devices** - You can select hello users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="7da6d-122">Les utilisateurs ajoutés ici sont ajoutés toohello *administrateurs de l’appareil* rôle dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da6d-122">Users added here are added toohello *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="7da6d-123">Les administrateurs généraux Azure AD et les propriétaires d’appareils bénéficient de droits d’administrateur local par défaut.</span><span class="sxs-lookup"><span data-stu-id="7da6d-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="7da6d-124">Cette option est une fonctionnalité d’édition premium disponible au moyen de produits tels qu’Azure AD Premium ou hello Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="7da6d-124">This option is a premium edition capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="7da6d-125">**Les utilisateurs peuvent inscrire leurs appareils auprès d’Azure AD** -vous devez tooconfigure cette toobe de périphériques tooallow paramètre inscrit auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da6d-125">**Users may register their devices with Azure AD** - You need tooconfigure this setting tooallow devices toobe registered with Azure AD.</span></span> <span data-ttu-id="7da6d-126">Si vous sélectionnez **aucun**, les appareils ne sont pas autorisées tooregister lorsqu’ils ne sont pas Azure Active Directory joint ou hybrides Azure AD est joint.</span><span class="sxs-lookup"><span data-stu-id="7da6d-126">If you select **None**, devices are not allowed tooregister when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="7da6d-127">L’inscription auprès de Microsoft Intune ou de la Gestion des appareils mobiles (MDM) pour Office 365 nécessite l’enregistrement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="7da6d-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="7da6d-128">Si vous avez configuré l’un de ces services, l’option **TOUS** est sélectionnée et l’option **AUCUN** est désactivée.</span><span class="sxs-lookup"><span data-stu-id="7da6d-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="7da6d-129">**Exiger l’authentification multifacteur toojoin appareils** -vous pouvez choisir si les utilisateurs sont requis tooprovide une authentification de second facteur toojoin leur tooAzure appareil AD.</span><span class="sxs-lookup"><span data-stu-id="7da6d-129">**Require Multi-Factor Auth toojoin devices** - You can choose whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="7da6d-130">valeur par défaut Hello est **non**.</span><span class="sxs-lookup"><span data-stu-id="7da6d-130">hello default is **No**.</span></span> <span data-ttu-id="7da6d-131">Il est recommandé d’exiger une authentification multifacteur au moment de l’inscription d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="7da6d-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="7da6d-132">Avant d’activer l’authentification multifacteur pour ce service, vous devez vous assurer que l’authentification multifacteur est configurée pour les utilisateurs de hello qui inscrivent leurs appareils.</span><span class="sxs-lookup"><span data-stu-id="7da6d-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for hello users that register their devices.</span></span> <span data-ttu-id="7da6d-133">Pour plus d’informations sur les services d’authentification multifacteur Azure, consultez [Bien démarrer avec l’authentification multifacteur Azure](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7da6d-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="7da6d-134">**Nombre maximal d’appareils** -ce paramètre permet de tooselect hello de nombre maximal d’appareils qu’un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da6d-134">**Maximum number of devices** - This setting enables you tooselect hello maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="7da6d-135">Si un utilisateur atteint ce quota, ils sont en mesure de tooadd des périphériques supplémentaires jusqu'à ce qu’une ou plusieurs des périphériques existants de hello sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="7da6d-135">If a user reaches this quota, they are not be able tooadd additional devices until one or more of hello existing devices are removed.</span></span> <span data-ttu-id="7da6d-136">guillemet de périphérique Hello est comptabilisée pour tous les périphériques qui sont Azure AD joint ou Azure AD inscrit aujourd'hui.</span><span class="sxs-lookup"><span data-stu-id="7da6d-136">hello device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="7da6d-137">la valeur par défaut Hello est **20**.</span><span class="sxs-lookup"><span data-stu-id="7da6d-137">hello default value is **20**.</span></span>

- <span data-ttu-id="7da6d-138">**Les utilisateurs peuvent synchroniser les paramètres et données d’application pour les appareils** -par défaut, ce paramètre est défini trop**NONE**.</span><span class="sxs-lookup"><span data-stu-id="7da6d-138">**Users may sync settings and app data across devices** - By default, this setting is set too**NONE**.</span></span> <span data-ttu-id="7da6d-139">En sélectionnant des utilisateurs spécifiques ou des groupes ou tous permet de paramètres et toosync de données d’application de l’utilisateur hello sur leurs appareils Windows 10.</span><span class="sxs-lookup"><span data-stu-id="7da6d-139">Selecting specific users or groups or ALL allows hello user’s settings and app data toosync across their Windows 10 devices.</span></span> <span data-ttu-id="7da6d-140">Découvrez comment fonctionne la synchronisation dans Windows 10.</span><span class="sxs-lookup"><span data-stu-id="7da6d-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="7da6d-141">Cette option est une fonctionnalité premium disponible au moyen de produits tels qu’Azure AD Premium ou hello Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="7da6d-141">This option is a premium capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span>
 
    ![Gérer un appareil Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="7da6d-143">Localiser les appareils</span><span class="sxs-lookup"><span data-stu-id="7da6d-143">Locate devices</span></span>

<span data-ttu-id="7da6d-144">En tant qu’administrateur, Bonjour portail Azure, vous avez deux options toolocate inscrit et appareils joints à un :</span><span class="sxs-lookup"><span data-stu-id="7da6d-144">As an administrator, in hello Azure portal, you have two options toolocate registered and joined devices:</span></span>

- <span data-ttu-id="7da6d-145">**Tous les appareils** Bonjour **gérer** section Hello **périphériques** panneau</span><span class="sxs-lookup"><span data-stu-id="7da6d-145">**All devices** in hello **Manage** section of hello **Devices** blade</span></span>  

    ![Tous les appareils](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="7da6d-147">**Appareils** Bonjour **gérer** section d’un **utilisateur** panneau</span><span class="sxs-lookup"><span data-stu-id="7da6d-147">**Devices** in hello **Manage** section of a **User** blade</span></span>
 
    ![Tous les appareils](./media/device-management-azure-portal/43.png)



<span data-ttu-id="7da6d-149">Avec ces deux options, vous pouvez consulter tooa qui :</span><span class="sxs-lookup"><span data-stu-id="7da6d-149">With both options, you can get tooa view that:</span></span>


- <span data-ttu-id="7da6d-150">Vous permet de toosearch pour les appareils à l’aide du nom d’affichage hello en tant que filtre.</span><span class="sxs-lookup"><span data-stu-id="7da6d-150">Enables you toosearch for devices using hello display name as filter.</span></span>

- <span data-ttu-id="7da6d-151">Fournit une vue d’ensemble détaillée des appareils inscrits et joints</span><span class="sxs-lookup"><span data-stu-id="7da6d-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="7da6d-152">Vous permet de tâches courantes de gestion des périphériques tooperform</span><span class="sxs-lookup"><span data-stu-id="7da6d-152">Enables you tooperform common device management tasks</span></span>
   

![Tous les appareils](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="7da6d-154">Tâches de gestion des appareils</span><span class="sxs-lookup"><span data-stu-id="7da6d-154">Device management tasks</span></span>

<span data-ttu-id="7da6d-155">En tant qu’administrateur, vous pouvez gérer hello inscrit ou appareils joints à un.</span><span class="sxs-lookup"><span data-stu-id="7da6d-155">As an administrator, you can manage hello registered or joined devices.</span></span> <span data-ttu-id="7da6d-156">Cette section fournit des informations sur les tâches courantes de gestion des appareils.</span><span class="sxs-lookup"><span data-stu-id="7da6d-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="7da6d-157">**Gérer un appareil Intune** : si vous êtes un administrateur Intune, vous pouvez gérer les appareils marqués comme étant des appareils **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="7da6d-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="7da6d-158">Un administrateur peut voir d’autres appareils.</span><span class="sxs-lookup"><span data-stu-id="7da6d-158">An administrator can see additional device</span></span> 

![Gérer un appareil Intune](./media/device-management-azure-portal/31.png)


<span data-ttu-id="7da6d-160">**Activer/Désactiver un appareil Azure AD**</span><span class="sxs-lookup"><span data-stu-id="7da6d-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="7da6d-161">tooenable ou désactiver un périphérique, vous devez toobe un administrateur global dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da6d-161">tooenable or disable a device, you need toobe a global administrator in Azure  AD.</span></span> <span data-ttu-id="7da6d-162">Si vous désactivez un appareil, vous l’empêchez d’accéder à vos ressources Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da6d-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="7da6d-163">Appareil de hello toodisable, vous pouvez cliquer sur *...*</span><span class="sxs-lookup"><span data-stu-id="7da6d-163">toodisable hello device, you can either click *…*</span></span> <span data-ttu-id="7da6d-164">Cliquez sur périphérique hello pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7da6d-164">click hello device for additional details.</span></span>

 
![Gérer un appareil Intune](./media/device-management-azure-portal/33.png)

<span data-ttu-id="7da6d-166">Désactivation d’un périphérique change d’état de hello Bonjour **activé** colonne trop**non**.</span><span class="sxs-lookup"><span data-stu-id="7da6d-166">Disabling a device changes hello state in hello **ENABLED** column too**No**.</span></span>

![Désactiver un appareil](./media/device-management-azure-portal/32.png)


<span data-ttu-id="7da6d-168">**Supprimer un appareil Azure AD** -toodelete un appareil, vous devez toobe un administrateur global dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da6d-168">**Delete an Azure AD device** - toodelete a device, you need toobe a global administrator in Azure AD.</span></span>  
<span data-ttu-id="7da6d-169">La suppression d’un appareil :</span><span class="sxs-lookup"><span data-stu-id="7da6d-169">Deleting a device:</span></span>
 
- <span data-ttu-id="7da6d-170">Empêche celui-ci d’accéder à vos ressources Azure AD</span><span class="sxs-lookup"><span data-stu-id="7da6d-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="7da6d-171">Supprime tous les détails qui sont attachés toohello périphérique, par exemple, les clés BitLocker pour les appareils Windows</span><span class="sxs-lookup"><span data-stu-id="7da6d-171">Removes all details that are attached toohello device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="7da6d-172">Est une action irréversible et donc non recommandée, sauf si elle est absolument nécessaire</span><span class="sxs-lookup"><span data-stu-id="7da6d-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="7da6d-173">Si un appareil est géré par une autre autorité de gestion (par exemple, Microsoft Intune), assurez-vous que cet appareil hello a été réinitialisé / mis hors service avant de supprimer un périphérique de hello dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da6d-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that hello device has been wiped / retired before deleting hello device in Azure AD.</span></span>

<span data-ttu-id="7da6d-174">Vous pouvez cliquer sur « … »</span><span class="sxs-lookup"><span data-stu-id="7da6d-174">You can either select “…”</span></span> <span data-ttu-id="7da6d-175">toodelete hello périphérique ou cliquez sur périphérique hello pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="7da6d-175">toodelete hello device or click on hello device for additional details</span></span>
 
![Suppression d’un appareil](./media/device-management-azure-portal/34.png)


<span data-ttu-id="7da6d-177">**Afficher ou copier des ID de périphérique** -vous pouvez utiliser un périphérique ID tooverify hello périphérique ID plus d’informations sur les appareils hello ou à l’aide de PowerShell lors du dépannage.</span><span class="sxs-lookup"><span data-stu-id="7da6d-177">**View or copy device ID** - You can use a device ID tooverify hello device ID details on hello device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="7da6d-178">tooaccess hello copie, cliquez sur le périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="7da6d-178">tooaccess hello copy option, click hello device.</span></span>

![Afficher un ID d’appareil](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="7da6d-180">**Afficher ou copier les clés BitLocker** -si vous êtes un administrateur, vous pouvez afficher et hello de copie BitLocker clés toohelp utilisateurs toorecover leur lecteur chiffré.</span><span class="sxs-lookup"><span data-stu-id="7da6d-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy hello BitLocker keys toohelp users toorecover their encrypted drive.</span></span> <span data-ttu-id="7da6d-181">Ces clés sont uniquement disponibles pour les appareils Windows chiffrés dont les clés sont stockées dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7da6d-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="7da6d-182">Vous pouvez copier ces clés lorsque vous accédez aux détails d’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="7da6d-182">You can copy these keys when accessing details of hello device.</span></span>
 
![Afficher les clés BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="7da6d-184">Journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="7da6d-184">Audit logs</span></span>


<span data-ttu-id="7da6d-185">activités de périphérique Hello sont disponibles via les journaux d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="7da6d-185">hello device activities are available through hello activity logs.</span></span> <span data-ttu-id="7da6d-186">Cela inclut les activités déclenchées par le service d’inscription de périphérique hello ou par l’utilisateur de hello :</span><span class="sxs-lookup"><span data-stu-id="7da6d-186">This includes activities triggered by hello device registration service or by hello user:</span></span>

- <span data-ttu-id="7da6d-187">La création de périphérique et en ajoutant les utilisateurs/propriétaires d’appareil de hello</span><span class="sxs-lookup"><span data-stu-id="7da6d-187">Device creation and adding owners/users on hello device</span></span>

- <span data-ttu-id="7da6d-188">Modifie les paramètres toodevice</span><span class="sxs-lookup"><span data-stu-id="7da6d-188">Changes toodevice settings</span></span>

- <span data-ttu-id="7da6d-189">Opérations concernant les appareils, telles que la suppression ou la mise à jour d’un appareil</span><span class="sxs-lookup"><span data-stu-id="7da6d-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="7da6d-190">Votre toohello de point d’entrée l’audit des données est **journaux d’Audit** Bonjour **activité** section Hello **périphériques* panneau.</span><span class="sxs-lookup"><span data-stu-id="7da6d-190">Your entry point toohello auditing data is **Audit logs** in hello **Activity** section of hello **Devices* blade.</span></span>

![Journaux d’audit](./media/device-management-azure-portal/61.png)


<span data-ttu-id="7da6d-192">Un journal d’audit inclut un mode Liste par défaut, qui indique :</span><span class="sxs-lookup"><span data-stu-id="7da6d-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="7da6d-193">date de Hello et l’heure de l’occurrence de hello</span><span class="sxs-lookup"><span data-stu-id="7da6d-193">hello date and time of hello occurrence</span></span>

- <span data-ttu-id="7da6d-194">cibles de Hello</span><span class="sxs-lookup"><span data-stu-id="7da6d-194">hello targets</span></span>

- <span data-ttu-id="7da6d-195">Hello initiateur / acteur (qui) d’une activité</span><span class="sxs-lookup"><span data-stu-id="7da6d-195">hello initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="7da6d-196">activité Hello (quoi)</span><span class="sxs-lookup"><span data-stu-id="7da6d-196">hello activity (what)</span></span>

![Journaux d’audit](./media/device-management-azure-portal/63.png)

<span data-ttu-id="7da6d-198">Vous pouvez personnaliser l’affichage de liste hello en cliquant sur **colonnes** dans la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="7da6d-198">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>
 
![Journaux d’audit](./media/device-management-azure-portal/64.png)


<span data-ttu-id="7da6d-200">toonarrow bas hello signalés au niveau de tooa de données que fonctionne pour vous, vous pouvez filtrer les données d’audit hello hello suivant des champs à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="7da6d-200">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="7da6d-201">Catégorie</span><span class="sxs-lookup"><span data-stu-id="7da6d-201">Catergory</span></span>
- <span data-ttu-id="7da6d-202">Type de ressource d’activité</span><span class="sxs-lookup"><span data-stu-id="7da6d-202">Activity resource type</span></span>
- <span data-ttu-id="7da6d-203">Activité</span><span class="sxs-lookup"><span data-stu-id="7da6d-203">Activity</span></span>
- <span data-ttu-id="7da6d-204">Plage de dates</span><span class="sxs-lookup"><span data-stu-id="7da6d-204">Date range</span></span>
- <span data-ttu-id="7da6d-205">Cible</span><span class="sxs-lookup"><span data-stu-id="7da6d-205">Target</span></span>
- <span data-ttu-id="7da6d-206">Initié par (intervenant)</span><span class="sxs-lookup"><span data-stu-id="7da6d-206">Initiated By (Actor)</span></span>

<span data-ttu-id="7da6d-207">En outre toohello filtres, vous pouvez rechercher des entrées spécifiques.</span><span class="sxs-lookup"><span data-stu-id="7da6d-207">In addition toohello filters, you can search for specific entries.</span></span>

![Journaux d’audit](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="7da6d-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7da6d-209">Next steps</span></span>

* [<span data-ttu-id="7da6d-210">Gestion de toodevice introduction dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7da6d-210">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



