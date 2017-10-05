---
title: "Gestion des appareils avec le portail Azure - Préversion | Microsoft Docs"
description: "Découvrez comment utiliser le portail Azure pour gérer les appareils."
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
ms.openlocfilehash: 4b46e1627a229b0649d9ccd2550cd28fda9849f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-devices-using-the-azure-portal---preview"></a><span data-ttu-id="8f67d-103">Gestion des appareils avec le portail Azure - Préversion</span><span class="sxs-lookup"><span data-stu-id="8f67d-103">Managing devices using the Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="8f67d-104">Cette fonctionnalité est actuellement disponible en préversion publique.</span><span class="sxs-lookup"><span data-stu-id="8f67d-104">This capability currently is in public preview.</span></span> <span data-ttu-id="8f67d-105">Soyez prêt à rétablir ou à supprimer les modifications.</span><span class="sxs-lookup"><span data-stu-id="8f67d-105">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="8f67d-106">La fonctionnalité est disponible dans tout abonnement Azure Active Directory (Azure AD) durant la période de préversion publique.</span><span class="sxs-lookup"><span data-stu-id="8f67d-106">The feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="8f67d-107">Toutefois, lorsque la fonctionnalité sera généralement disponible, il se peut que certains de ses aspects nécessitent un abonnement Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="8f67d-107">However, when the feature becomes generally available, some aspects of the feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="8f67d-108">La fonction de gestion des appareils intégrée à Azure Active Directory (Azure AD) vous permet de vous assurer que vos utilisateurs accèdent à vos ressources à partir d’appareils qui répondent à vos normes de conformité et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="8f67d-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="8f67d-109">Cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="8f67d-109">This topic:</span></span>

- <span data-ttu-id="8f67d-110">Suppose que vous avez lu la [Présentation de la gestion des appareils dans Azure Active Directory](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8f67d-110">Assumes that you are familiar with the [introduction to device management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="8f67d-111">Fournit des informations sur la gestion des appareils avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="8f67d-111">Provides you with information about managing your devices using the Azure portal</span></span>


<span data-ttu-id="8f67d-112">Pour gérer les appareils dans le portail Azure, cliquez sur **Appareils** dans la section **Gérer** du panneau **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8f67d-112">To manage devices in the Azure portal, you need to click **Devices** in the **Manage** section of the the **Azure Active Directory** blade.</span></span>

![Gérer un appareil Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="8f67d-114">Configurer les paramètres de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8f67d-114">Configure device settings</span></span>

<span data-ttu-id="8f67d-115">Pour gérer vos appareils avec le portail Azure, vous devez les inscrire ou les joindre à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-115">To manage your devices using the Azure portal, they need to be either registered or joined to Azure AD.</span></span> <span data-ttu-id="8f67d-116">En tant qu’administrateur, vous pouvez affiner le processus d’inscription et de jonction des appareils en configurant les paramètres de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8f67d-116">As an administrator, you can fine-tune the process of registering and joining devices by configuring the device settings.</span></span>

![Gérer un appareil Intune](./media/device-management-azure-portal/22.png)


<span data-ttu-id="8f67d-118">Le panneau Paramètres de l’appareil vous permet de configurer les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="8f67d-118">The device settings blade enables you to configure:</span></span>

- <span data-ttu-id="8f67d-119">**Les utilisateurs peuvent joindre des appareils à Azure AD** : ce paramètre vous permet de sélectionner les utilisateurs qui peuvent joindre des appareils à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-119">**Users may join devices to Azure AD** - This settings enables you to select the users who can join devices to Azure AD.</span></span> <span data-ttu-id="8f67d-120">La valeur par défaut est **Tous**.</span><span class="sxs-lookup"><span data-stu-id="8f67d-120">The default is **All**.</span></span>

- <span data-ttu-id="8f67d-121">**Administrateurs locaux supplémentaires sur les appareils joints à Azure AD** : vous pouvez sélectionner les utilisateurs qui peuvent disposer de droits d’administrateur local sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="8f67d-121">**Additional local administrators on Azure AD joined devices** - You can select the users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="8f67d-122">Les utilisateurs ajoutés ici sont ajoutés au rôle *Administrateurs d’appareils* dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-122">Users added here are added to the *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="8f67d-123">Les administrateurs généraux Azure AD et les propriétaires d’appareils bénéficient de droits d’administrateur local par défaut.</span><span class="sxs-lookup"><span data-stu-id="8f67d-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="8f67d-124">Cette option est une fonctionnalité de l’édition Premium disponible dans les produits comme Azure AD Premium ou EMS (Enterprise Mobility Suite).</span><span class="sxs-lookup"><span data-stu-id="8f67d-124">This option is a premium edition capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="8f67d-125">**Les utilisateurs peuvent inscrire leurs appareils sur Azure AD** : vous devez configurer ce paramètre pour permettre l’inscription des appareils dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-125">**Users may register their devices with Azure AD** - You need to configure this setting to allow devices to be registered with Azure AD.</span></span> <span data-ttu-id="8f67d-126">Si vous sélectionnez **Aucun**, les appareils ne peuvent pas être inscrits s’ils ne sont pas joints à Azure AD ou s’il ne s’agit pas d’appareils hybrides joints à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-126">If you select **None**, devices are not allowed to register when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="8f67d-127">L’inscription auprès de Microsoft Intune ou de la Gestion des appareils mobiles (MDM) pour Office 365 nécessite l’enregistrement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8f67d-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="8f67d-128">Si vous avez configuré l’un de ces services, l’option **TOUS** est sélectionnée et l’option **AUCUN** est désactivée.</span><span class="sxs-lookup"><span data-stu-id="8f67d-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="8f67d-129">**Exiger Multi-factor Auth pour joindre des appareils** : vous pouvez demander aux utilisateurs de fournir un second facteur d’authentification pour joindre leurs appareils à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-129">**Require Multi-Factor Auth to join devices** - You can choose whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="8f67d-130">La valeur par défaut est **Non**.</span><span class="sxs-lookup"><span data-stu-id="8f67d-130">The default is **No**.</span></span> <span data-ttu-id="8f67d-131">Il est recommandé d’exiger une authentification multifacteur au moment de l’inscription d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="8f67d-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="8f67d-132">Avant d’activer l’authentification multifacteur pour ce service, vous devez vérifier que l’authentification multifacteur est configurée pour les utilisateurs qui inscrivent leurs appareils.</span><span class="sxs-lookup"><span data-stu-id="8f67d-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for the users that register their devices.</span></span> <span data-ttu-id="8f67d-133">Pour plus d’informations sur les services d’authentification multifacteur Azure, consultez [Bien démarrer avec l’authentification multifacteur Azure](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8f67d-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="8f67d-134">**Nombre maximal d’appareils par utilisateur** : ce paramètre permet de sélectionner le nombre maximal d’appareils qu’un utilisateur peut avoir dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-134">**Maximum number of devices** - This setting enables you to select the maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="8f67d-135">Si un utilisateur atteint ce quota, il ne pourra pas ajouter d’autres appareils tant qu’un ou plusieurs appareils existants n’auront pas été supprimés.</span><span class="sxs-lookup"><span data-stu-id="8f67d-135">If a user reaches this quota, they are not be able to add additional devices until one or more of the existing devices are removed.</span></span> <span data-ttu-id="8f67d-136">Le quota d’appareils comptabilise tous les appareils qui sont actuellement joints à Azure AD ou inscrits à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-136">The device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="8f67d-137">La valeur par défaut est de **20** appareils.</span><span class="sxs-lookup"><span data-stu-id="8f67d-137">The default value is **20**.</span></span>

- <span data-ttu-id="8f67d-138">**Les utilisateurs peuvent synchroniser les paramètres et les données d’application sur différents appareils** : par défaut, ce paramètre est défini sur **AUCUN**.</span><span class="sxs-lookup"><span data-stu-id="8f67d-138">**Users may sync settings and app data across devices** - By default, this setting is set to **NONE**.</span></span> <span data-ttu-id="8f67d-139">La sélection de certains utilisateurs ou groupes, ou de TOUS, permet aux paramètres et aux données d’application de l’utilisateur d’être synchronisés sur ses appareils Windows 10.</span><span class="sxs-lookup"><span data-stu-id="8f67d-139">Selecting specific users or groups or ALL allows the user’s settings and app data to sync across their Windows 10 devices.</span></span> <span data-ttu-id="8f67d-140">Découvrez comment fonctionne la synchronisation dans Windows 10.</span><span class="sxs-lookup"><span data-stu-id="8f67d-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="8f67d-141">Cette option est une fonctionnalité de l’édition Premium disponible dans les produits comme Azure AD Premium ou EMS (Enterprise Mobility Suite).</span><span class="sxs-lookup"><span data-stu-id="8f67d-141">This option is a premium capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span>
 
    ![Gérer un appareil Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="8f67d-143">Localiser les appareils</span><span class="sxs-lookup"><span data-stu-id="8f67d-143">Locate devices</span></span>

<span data-ttu-id="8f67d-144">En tant qu’administrateur, dans le portail Azure, deux options permettent de localiser les appareils inscrits et joints :</span><span class="sxs-lookup"><span data-stu-id="8f67d-144">As an administrator, in the Azure portal, you have two options to locate registered and joined devices:</span></span>

- <span data-ttu-id="8f67d-145">**Tous les appareils** dans la section **Gérer** du panneau **Appareils**</span><span class="sxs-lookup"><span data-stu-id="8f67d-145">**All devices** in the **Manage** section of the **Devices** blade</span></span>  

    ![Tous les appareils](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="8f67d-147">**Appareils** dans la section **Gérer** du panneau **Utilisateur**</span><span class="sxs-lookup"><span data-stu-id="8f67d-147">**Devices** in the **Manage** section of a **User** blade</span></span>
 
    ![Tous les appareils](./media/device-management-azure-portal/43.png)



<span data-ttu-id="8f67d-149">Ces deux options permettent d’accéder à une vue qui :</span><span class="sxs-lookup"><span data-stu-id="8f67d-149">With both options, you can get to a view that:</span></span>


- <span data-ttu-id="8f67d-150">Permet de rechercher des appareils en utilisant leur nom d’affichage comme filtre</span><span class="sxs-lookup"><span data-stu-id="8f67d-150">Enables you to search for devices using the display name as filter.</span></span>

- <span data-ttu-id="8f67d-151">Fournit une vue d’ensemble détaillée des appareils inscrits et joints</span><span class="sxs-lookup"><span data-stu-id="8f67d-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="8f67d-152">Permet d’effectuer les tâches courantes de gestion des appareils</span><span class="sxs-lookup"><span data-stu-id="8f67d-152">Enables you to perform common device management tasks</span></span>
   

![Tous les appareils](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="8f67d-154">Tâches de gestion des appareils</span><span class="sxs-lookup"><span data-stu-id="8f67d-154">Device management tasks</span></span>

<span data-ttu-id="8f67d-155">En tant qu’administrateur, vous pouvez gérer les appareils inscrits ou joints.</span><span class="sxs-lookup"><span data-stu-id="8f67d-155">As an administrator, you can manage the registered or joined devices.</span></span> <span data-ttu-id="8f67d-156">Cette section fournit des informations sur les tâches courantes de gestion des appareils.</span><span class="sxs-lookup"><span data-stu-id="8f67d-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="8f67d-157">**Gérer un appareil Intune** : si vous êtes un administrateur Intune, vous pouvez gérer les appareils marqués comme étant des appareils **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="8f67d-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="8f67d-158">Un administrateur peut voir d’autres appareils.</span><span class="sxs-lookup"><span data-stu-id="8f67d-158">An administrator can see additional device</span></span> 

![Gérer un appareil Intune](./media/device-management-azure-portal/31.png)


<span data-ttu-id="8f67d-160">**Activer/Désactiver un appareil Azure AD**</span><span class="sxs-lookup"><span data-stu-id="8f67d-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="8f67d-161">Pour activer ou désactiver un appareil, vous devez être administrateur général dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-161">To enable or disable a device, you need to be a global administrator in Azure  AD.</span></span> <span data-ttu-id="8f67d-162">Si vous désactivez un appareil, vous l’empêchez d’accéder à vos ressources Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="8f67d-163">Pour désactiver l’appareil, vous pouvez cliquer sur *...*</span><span class="sxs-lookup"><span data-stu-id="8f67d-163">To disable the device, you can either click *…*</span></span> <span data-ttu-id="8f67d-164">ou cliquer sur l’appareil pour afficher des informations le concernant.</span><span class="sxs-lookup"><span data-stu-id="8f67d-164">click the device for additional details.</span></span>

 
![Gérer un appareil Intune](./media/device-management-azure-portal/33.png)

<span data-ttu-id="8f67d-166">Quand vous désactivez un appareil, la colonne **Activé** affiche la valeur **Non**.</span><span class="sxs-lookup"><span data-stu-id="8f67d-166">Disabling a device changes the state in the **ENABLED** column to **No**.</span></span>

![Désactiver un appareil](./media/device-management-azure-portal/32.png)


<span data-ttu-id="8f67d-168">**Supprimer un appareil Azure AD** : pour activer ou désactiver un appareil, vous devez être administrateur général dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-168">**Delete an Azure AD device** - To delete a device, you need to be a global administrator in Azure AD.</span></span>  
<span data-ttu-id="8f67d-169">La suppression d’un appareil :</span><span class="sxs-lookup"><span data-stu-id="8f67d-169">Deleting a device:</span></span>
 
- <span data-ttu-id="8f67d-170">Empêche celui-ci d’accéder à vos ressources Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f67d-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="8f67d-171">Supprime toutes les informations associées à l’appareil, par exemple, les clés BitLocker des appareils Windows</span><span class="sxs-lookup"><span data-stu-id="8f67d-171">Removes all details that are attached to the device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="8f67d-172">Est une action irréversible et donc non recommandée, sauf si elle est absolument nécessaire</span><span class="sxs-lookup"><span data-stu-id="8f67d-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="8f67d-173">Si un appareil est géré par une autre autorité de gestion (par exemple, Microsoft Intune), vérifiez que l’appareil a été réinitialisé ou mis hors service avant de le supprimer d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that the device has been wiped / retired before deleting the device in Azure AD.</span></span>

<span data-ttu-id="8f67d-174">Vous pouvez cliquer sur « … »</span><span class="sxs-lookup"><span data-stu-id="8f67d-174">You can either select “…”</span></span> <span data-ttu-id="8f67d-175">pour supprimer l’appareil ou cliquer sur l’appareil pour afficher les informations le concernant.</span><span class="sxs-lookup"><span data-stu-id="8f67d-175">to delete the device or click on the device for additional details</span></span>
 
![Suppression d’un appareil](./media/device-management-azure-portal/34.png)


<span data-ttu-id="8f67d-177">**Afficher ou copier l’ID de l’appareil** : vous pouvez utiliser un ID d’appareil pour vérifier les informations d’ID de l’appareil ou utiliser PowerShell lors du dépannage.</span><span class="sxs-lookup"><span data-stu-id="8f67d-177">**View or copy device ID** - You can use a device ID to verify the device ID details on the device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="8f67d-178">Pour accéder à l’option de copie, cliquez sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8f67d-178">To access the copy option, click the device.</span></span>

![Afficher un ID d’appareil](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="8f67d-180">**Afficher ou copier des clés BitLocker** : si vous êtes administrateur, vous pouvez afficher et copier les clés BitLocker pour permettre aux utilisateurs de récupérer leur lecteur chiffré.</span><span class="sxs-lookup"><span data-stu-id="8f67d-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy the BitLocker keys to help users to recover their encrypted drive.</span></span> <span data-ttu-id="8f67d-181">Ces clés sont uniquement disponibles pour les appareils Windows chiffrés dont les clés sont stockées dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f67d-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="8f67d-182">Vous pouvez copier ces clés lorsque vous accédez aux informations de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8f67d-182">You can copy these keys when accessing details of the device.</span></span>
 
![Afficher les clés BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="8f67d-184">Journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="8f67d-184">Audit logs</span></span>


<span data-ttu-id="8f67d-185">Les activités de l’appareil sont disponibles dans les journaux d’activité.</span><span class="sxs-lookup"><span data-stu-id="8f67d-185">The device activities are available through the activity logs.</span></span> <span data-ttu-id="8f67d-186">Elles comprennent les activités déclenchées par le service d’inscription des appareils ou par l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="8f67d-186">This includes activities triggered by the device registration service or by the user:</span></span>

- <span data-ttu-id="8f67d-187">Création d’un appareil et ajout de propriétaires/d’utilisateurs sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="8f67d-187">Device creation and adding owners/users on the device</span></span>

- <span data-ttu-id="8f67d-188">Modification des paramètres de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8f67d-188">Changes to device settings</span></span>

- <span data-ttu-id="8f67d-189">Opérations concernant les appareils, telles que la suppression ou la mise à jour d’un appareil</span><span class="sxs-lookup"><span data-stu-id="8f67d-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="8f67d-190">Les **Journaux d’audit** dans la section **Activité** du panneau **Appareils* constituent le point d’entrée des données d’audit.</span><span class="sxs-lookup"><span data-stu-id="8f67d-190">Your entry point to the auditing data is **Audit logs** in the **Activity** section of the **Devices* blade.</span></span>

![Journaux d’audit](./media/device-management-azure-portal/61.png)


<span data-ttu-id="8f67d-192">Un journal d’audit inclut un mode Liste par défaut, qui indique :</span><span class="sxs-lookup"><span data-stu-id="8f67d-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="8f67d-193">la date et l’heure de l’occurrence</span><span class="sxs-lookup"><span data-stu-id="8f67d-193">the date and time of the occurrence</span></span>

- <span data-ttu-id="8f67d-194">les cibles</span><span class="sxs-lookup"><span data-stu-id="8f67d-194">the targets</span></span>

- <span data-ttu-id="8f67d-195">l’initiateur/intervenant d’une activité (qui)</span><span class="sxs-lookup"><span data-stu-id="8f67d-195">the initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="8f67d-196">l’activité (quoi)</span><span class="sxs-lookup"><span data-stu-id="8f67d-196">the activity (what)</span></span>

![Journaux d’audit](./media/device-management-azure-portal/63.png)

<span data-ttu-id="8f67d-198">Vous pouvez personnaliser le mode Liste en cliquant sur **Colonnes** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="8f67d-198">You can customize the list view by clicking **Columns** in the toolbar.</span></span>
 
![Journaux d’audit](./media/device-management-azure-portal/64.png)


<span data-ttu-id="8f67d-200">Pour limiter les données transmises à un niveau qui vous convient, vous pouvez filtrer les données d’audit à l’aide des champs suivants :</span><span class="sxs-lookup"><span data-stu-id="8f67d-200">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="8f67d-201">Catégorie</span><span class="sxs-lookup"><span data-stu-id="8f67d-201">Catergory</span></span>
- <span data-ttu-id="8f67d-202">Type de ressource d’activité</span><span class="sxs-lookup"><span data-stu-id="8f67d-202">Activity resource type</span></span>
- <span data-ttu-id="8f67d-203">Activité</span><span class="sxs-lookup"><span data-stu-id="8f67d-203">Activity</span></span>
- <span data-ttu-id="8f67d-204">Plage de dates</span><span class="sxs-lookup"><span data-stu-id="8f67d-204">Date range</span></span>
- <span data-ttu-id="8f67d-205">Cible</span><span class="sxs-lookup"><span data-stu-id="8f67d-205">Target</span></span>
- <span data-ttu-id="8f67d-206">Initié par (intervenant)</span><span class="sxs-lookup"><span data-stu-id="8f67d-206">Initiated By (Actor)</span></span>

<span data-ttu-id="8f67d-207">Vous pouvez filtrer les entrées, mais également rechercher des entrées spécifiques.</span><span class="sxs-lookup"><span data-stu-id="8f67d-207">In addition to the filters, you can search for specific entries.</span></span>

![Journaux d’audit](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="8f67d-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8f67d-209">Next steps</span></span>

* [<span data-ttu-id="8f67d-210">Présentation de la gestion des appareils dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f67d-210">Introduction to device management in Azure Active Directory</span></span>](device-management-introduction.md)



