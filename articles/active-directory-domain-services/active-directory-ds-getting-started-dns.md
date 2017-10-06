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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="5ee27-103">Activer Azure Active Directory Domain Services (préversion)</span><span class="sxs-lookup"><span data-stu-id="5ee27-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="5ee27-104">Tâche 4 : mettre à jour les paramètres DNS pour hello réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="5ee27-104">Task 4: update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="5ee27-105">Bonjour précédant les tâches de configuration, vous avez correctement activé Azure Active Directory Domain Services pour votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="5ee27-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="5ee27-106">la tâche suivante Hello est tooensure que les ordinateurs d’un réseau virtuel de hello peuvent se connecter et utilisation de ces services.</span><span class="sxs-lookup"><span data-stu-id="5ee27-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="5ee27-107">Dans cet article, vous mettre à jour les paramètres du serveur DNS hello pour votre réseau virtuel toopoint toohello deux adresses IP où Azure des Services de domaine Active Directory est disponible sur le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5ee27-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

<span data-ttu-id="5ee27-108">paramètre de serveur DNS tooupdate hello pour le réseau virtuel de hello dans lequel vous avez activé Azure Active Directory Domain Services hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ee27-108">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="5ee27-109">Hello **vue d’ensemble** onglet répertorie un ensemble de **requis des étapes de configuration** toobe effectuée une fois votre domaine géré est entièrement configuré.</span><span class="sxs-lookup"><span data-stu-id="5ee27-109">hello **Overview** tab lists a set of **Required configuration steps** toobe performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="5ee27-110">première étape de configuration Hello est **paramètres du serveur DNS de mise à jour pour votre réseau virtuel**.</span><span class="sxs-lookup"><span data-stu-id="5ee27-110">hello first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Domain Services - Onglet Vue d’ensemble une fois la configuration terminée](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="5ee27-112">Lorsque votre domaine est entièrement configuré, deux adresses IP s’affichent dans cette vignette.</span><span class="sxs-lookup"><span data-stu-id="5ee27-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="5ee27-113">Chacune de ces adresses IP représente un contrôleur de domaine pour votre domaine managé.</span><span class="sxs-lookup"><span data-stu-id="5ee27-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="5ee27-114">toocopy hello première adresse IP tooclipboard d’adresses, cliquez sur tooit de hello copie bouton suivant.</span><span class="sxs-lookup"><span data-stu-id="5ee27-114">toocopy hello first IP address tooclipboard, click hello copy button next tooit.</span></span> <span data-ttu-id="5ee27-115">Puis cliquez sur hello **serveurs de configurer le serveur DNS** bouton.</span><span class="sxs-lookup"><span data-stu-id="5ee27-115">Then click hello **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="5ee27-116">Coller la première adresse IP de hello en hello **serveur DNS d’ajouter** textbox Bonjour **serveurs DNS** panneau.</span><span class="sxs-lookup"><span data-stu-id="5ee27-116">Paste hello first IP address into hello **Add DNS server** textbox in hello **DNS servers** blade.</span></span> <span data-ttu-id="5ee27-117">Faire défiler horizontalement toohello gauche toocopy hello deuxième adresse IP et le coller dans hello **serveur DNS d’ajouter** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5ee27-117">Scroll horizontally toohello left toocopy hello second IP address and paste it into hello **Add DNS server** textbox.</span></span>

    ![Domain Services - Mettre à jour le DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="5ee27-119">Cliquez sur **enregistrer** lorsque vous avez terminé les serveurs DNS tooupdate hello pour le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5ee27-119">Click **Save** when you are done tooupdate hello DNS servers for hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="5ee27-120">Machines virtuelles dans un réseau de hello obtenir uniquement les nouveaux paramètres DNS de hello après un redémarrage.</span><span class="sxs-lookup"><span data-stu-id="5ee27-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="5ee27-121">Si vous devez les paramètres de DNS tooget hello mis à jour immédiatement, déclencher le redémarrage d’un portail de hello, PowerShell ou hello CLI.</span><span class="sxs-lookup"><span data-stu-id="5ee27-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="5ee27-122">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="5ee27-122">Next step</span></span>
[<span data-ttu-id="5ee27-123">Tâche 5 : activer la synchronisation de mot de passe tooAzure les Services de domaine Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ee27-123">Task 5: enable password synchronization tooAzure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
