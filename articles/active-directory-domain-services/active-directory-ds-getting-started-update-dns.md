---
title: "Azure Active Directory Domain Services : mettre à jour les paramètres DNS pour le réseau virtuel Azure | Microsoft Docs"
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
ms.openlocfilehash: 8bee2a25f196d645b27f30f21305b1550e44e07a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="1c93b-103">Mettre à jour les paramètres DNS pour le réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="1c93b-103">Update DNS settings for the Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="1c93b-104">Tâche 4 : mettre à jour les paramètres DNS pour le réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="1c93b-104">Task 4: Update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="1c93b-105">Dans les tâches de configuration précédentes, vous avez activé Azure Active Directory Domain Services pour votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="1c93b-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="1c93b-106">La tâche suivante consiste à s’assurer que les ordinateurs du réseau virtuel peuvent se connecter et utiliser ces services.</span><span class="sxs-lookup"><span data-stu-id="1c93b-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="1c93b-107">Dans cet article, vous mettez à jour les paramètres de serveur DNS de votre réseau virtuel afin qu’il pointe vers les deux adresses IP pour lesquelles Azure Active Directory Domain Services est disponible sur le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1c93b-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="1c93b-108">Après avoir activé Azure Active Directory Domain Services pour le répertoire, notez les adresses IP d’Azure Active Directory Domain Services affichées dans l’onglet **Configurer** de votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="1c93b-108">After you've enabled Azure Active Directory Domain Services for the directory, note the IP addresses for Azure Active Directory Domain Services that are displayed on the **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="1c93b-109">Afin de mettre à jour le paramètre de serveur DNS pour le réseau virtuel sur lequel vous avez activé Azure Active Directory Domain Services, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c93b-109">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="1c93b-110">Connectez-vous au [Portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1c93b-110">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="1c93b-111">Dans le volet gauche, sélectionnez **Réseaux**.</span><span class="sxs-lookup"><span data-stu-id="1c93b-111">In the left pane, select **Networks**.</span></span>  
    <span data-ttu-id="1c93b-112">La fenêtre **Réseaux** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="1c93b-112">The **Networks** window opens.</span></span>

    ![Fenêtre Réseaux virtuels](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="1c93b-114">Dans l’onglet **Réseaux virtuels**, sélectionnez le réseau virtuel sur lequel vous avez activé Azure Active Directory Domain Services afin d’en afficher les propriétés.</span><span class="sxs-lookup"><span data-stu-id="1c93b-114">On the **Virtual Networks** tab, select the virtual network in which you enabled Azure Active Directory Domain Services to view its properties.</span></span>
4. <span data-ttu-id="1c93b-115">Cliquez sur l'onglet **Configurer** .</span><span class="sxs-lookup"><span data-stu-id="1c93b-115">Click the **Configure** tab.</span></span>

    ![Fenêtre Réseaux virtuels](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="1c93b-117">Dans la section **Serveurs DNS**, entrez les deux adresses IP qui étaient affichées dans la section **Services de domaine** de l’onglet **Configurer** de votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="1c93b-117">In the **DNS servers** section, enter both of the IP addresses that were displayed in the **Domain Services** section on the **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="1c93b-118">Pour enregistrer les paramètres de serveur DNS pour ce réseau virtuel, cliquez sur **Enregistrer** dans le volet des tâches au bas de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="1c93b-118">To save the DNS server settings for this virtual network, in the task pane at the bottom of the window, click **Save**.</span></span>

   ![Mettre à jour les paramètres de serveur DNS pour le réseau virtuel](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="1c93b-120">Les machines virtuelles du réseau n’obtiendront les nouveaux paramètres DNS qu’après un redémarrage.</span><span class="sxs-lookup"><span data-stu-id="1c93b-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="1c93b-121">Si vous avez besoin qu’elles obtiennent les paramètres DNS mis à jour immédiatement, déclenchez un redémarrage via le portail, PowerShell ou l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="1c93b-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="1c93b-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1c93b-122">Next steps</span></span>
<span data-ttu-id="1c93b-123">Tâche 5 : [activer la synchronisation du mot de passe pour Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="1c93b-123">Task 5: [Enable password synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
