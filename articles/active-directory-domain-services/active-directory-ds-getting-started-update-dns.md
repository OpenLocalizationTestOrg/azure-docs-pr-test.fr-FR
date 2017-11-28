---
title: "Azure Active Directory Domain Services : Mettre à jour les paramètres DNS pour le réseau virtuel Azure de hello | Documents Microsoft"
description: Prise en main des services de domaine Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="78aa0-103">Mettre à jour les paramètres DNS pour hello réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="78aa0-103">Update DNS settings for hello Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="78aa0-104">Tâche 4 : Mettre à jour les paramètres DNS pour hello réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="78aa0-104">Task 4: Update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="78aa0-105">Bonjour précédant les tâches de configuration, vous avez correctement activé Azure Active Directory Domain Services pour votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="78aa0-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="78aa0-106">la tâche suivante Hello est tooensure que les ordinateurs d’un réseau virtuel de hello peuvent se connecter et utilisation de ces services.</span><span class="sxs-lookup"><span data-stu-id="78aa0-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="78aa0-107">Dans cet article, vous mettre à jour les paramètres du serveur DNS hello pour votre réseau virtuel toopoint toohello deux adresses IP où Azure des Services de domaine Active Directory est disponible sur le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="78aa0-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="78aa0-108">Une fois que vous avez activé Azure Active Directory Domain Services pour le répertoire de hello, notez les adresses IP hello pour Azure Active Directory Domain Services qui s’affichent sur hello **configurer** onglet de votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="78aa0-108">After you've enabled Azure Active Directory Domain Services for hello directory, note hello IP addresses for Azure Active Directory Domain Services that are displayed on hello **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="78aa0-109">paramètre de serveur DNS tooupdate hello pour le réseau virtuel de hello dans lequel vous avez activé Azure Active Directory Domain Services hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="78aa0-109">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="78aa0-110">Accédez toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="78aa0-110">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="78aa0-111">Dans le volet gauche de hello, sélectionnez **réseaux**.</span><span class="sxs-lookup"><span data-stu-id="78aa0-111">In hello left pane, select **Networks**.</span></span>  
    <span data-ttu-id="78aa0-112">Hello **réseaux** fenêtre s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="78aa0-112">hello **Networks** window opens.</span></span>

    ![Fenêtre Réseaux virtuels](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="78aa0-114">Sur hello **réseaux virtuels** onglet, le réseau virtuel de select hello dans lequel vous avez activé Azure des Services de domaine Active Directory tooview ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="78aa0-114">On hello **Virtual Networks** tab, select hello virtual network in which you enabled Azure Active Directory Domain Services tooview its properties.</span></span>
4. <span data-ttu-id="78aa0-115">Cliquez sur hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="78aa0-115">Click hello **Configure** tab.</span></span>

    ![Fenêtre Réseaux virtuels](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="78aa0-117">Bonjour **serveurs DNS** section, entrez les deux adresses IP hello qui étaient affichés dans hello **Services de domaine** section hello **configurer** onglet de votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="78aa0-117">In hello **DNS servers** section, enter both of hello IP addresses that were displayed in hello **Domain Services** section on hello **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="78aa0-118">Cliquez sur les paramètres du serveur DNS toosave hello pour ce réseau virtuel, dans le volet de tâches hello bas hello de fenêtre hello, **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="78aa0-118">toosave hello DNS server settings for this virtual network, in hello task pane at hello bottom of hello window, click **Save**.</span></span>

   ![Mettre à jour les paramètres du serveur DNS hello pour le réseau virtuel de hello](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="78aa0-120">Machines virtuelles dans un réseau de hello obtenir uniquement les nouveaux paramètres DNS de hello après un redémarrage.</span><span class="sxs-lookup"><span data-stu-id="78aa0-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="78aa0-121">Si vous devez les paramètres de DNS tooget hello mis à jour immédiatement, déclencher le redémarrage d’un portail de hello, PowerShell ou hello CLI.</span><span class="sxs-lookup"><span data-stu-id="78aa0-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="78aa0-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="78aa0-122">Next steps</span></span>
<span data-ttu-id="78aa0-123">Tâche 5 : [activer la synchronisation de mot de passe tooAzure les Services de domaine Active Directory](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="78aa0-123">Task 5: [Enable password synchronization tooAzure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
