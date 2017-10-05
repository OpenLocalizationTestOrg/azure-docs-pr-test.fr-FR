---
title: "Réseaux connus dans le portail Azure Classic | Microsoft Docs"
description: "En configurant les réseaux connus, vous pouvez éviter que des adresses IP appartenant à votre organisation ne soient incluses dans les rapports Connexions depuis plusieurs zones géographiques et Connexions à partir d’adresses IP affichant une activité suspecte."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a><span data-ttu-id="5861b-103">Réseaux connus</span><span class="sxs-lookup"><span data-stu-id="5861b-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5861b-104">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="5861b-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="5861b-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="5861b-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="5861b-106">Vous pouvez utiliser les rapports d'accès et d'utilisation Azure Active Directory pour obtenir une visibilité complète sur l'intégrité et la sécurité du répertoire de votre société.</span><span class="sxs-lookup"><span data-stu-id="5861b-106">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="5861b-107">Grâce à ces informations, un administrateur de répertoire est capable de déterminer plus précisément les risques de sécurité potentiels et donc de les atténuer au maximum.</span><span class="sxs-lookup"><span data-stu-id="5861b-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="5861b-108">Il est possible que les rapports « *Connexions depuis plusieurs zones géographiques* » et « *Connexions à partir d’adresses IP affichant une activité suspecte* » signalent de manière incorrecte des adresses IP qui appartiennent en fait à votre organisation.</span><span class="sxs-lookup"><span data-stu-id="5861b-108">It is possible that the “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="5861b-109">Cela peut, par exemple, se produire dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="5861b-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="5861b-110">Un utilisateur de votre bureau de Boston qui s'est connecté à distance à votre centre de données à San Francisco déclenche le rapport « Connexions depuis plusieurs zones géographiques »</span><span class="sxs-lookup"><span data-stu-id="5861b-110">A user in your Boston office has signed in remotely to your data center in San Francisco triggers the “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="5861b-111">Un utilisateur de votre organisation qui tente de se connecter plusieurs fois avec un mot de passe incorrect déclenche le rapport « Connexions à partir d’adresses IP affichant une activité suspecte »</span><span class="sxs-lookup"><span data-stu-id="5861b-111">A user of your organization tries to sign-on several times with an incorrect password triggers the “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="5861b-112">Pour empêcher ces cas de générer des rapports de sécurité incorrects, vous devez ajouter des plages d'adresses IP connues à la liste d'adresses IP publiques de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="5861b-112">To prevent these cases from generating misleading security reports, you should add known IP address ranges to the list of your organization's public IP address.</span></span>    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a><span data-ttu-id="5861b-113">Pour ajouter les plages d'adresses IP publiques de votre organisation, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5861b-113">To add your organization’s public IP address ranges, perform the following steps:</span></span>

1. <span data-ttu-id="5861b-114">Connectez-vous au [portail de gestion Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5861b-114">Sign-on to the [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="5861b-115">Dans le volet gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5861b-115">In the left pane, click **Active Directory**.</span></span> 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="5861b-117">Dans l'onglet **Annuaire** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="5861b-117">In the **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="5861b-118">Dans le menu situé en haut, cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="5861b-118">In the menu on the top, click **Configure**.</span></span> 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="5861b-120">Sous l'onglet Configurer, accédez aux **plages d'adresses IP publiques de votre organisation**</span><span class="sxs-lookup"><span data-stu-id="5861b-120">On the Configure tab, go to **your organizations public IP address ranges**</span></span> 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="5861b-122">Cliquez sur **Ajouter des plages d'adresses IP connues**.</span><span class="sxs-lookup"><span data-stu-id="5861b-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="5861b-123">Ajouter les plages d'adresses dans la boîte de dialogue qui s'affiche, puis cliquez sur le bouton de vérification lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="5861b-123">Add your address ranges in the dialog box that appears, and then click the check button  when you are done.</span></span> 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="5861b-125">**Ressources supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="5861b-125">**Additional resources:**</span></span>

* [<span data-ttu-id="5861b-126">Affichage de vos rapports d’accès et d’utilisation</span><span class="sxs-lookup"><span data-stu-id="5861b-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="5861b-127">Connexions à partir d’adresses IP affichant une activité suspecte</span><span class="sxs-lookup"><span data-stu-id="5861b-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="5861b-128">Connexions depuis plusieurs zones géographiques</span><span class="sxs-lookup"><span data-stu-id="5861b-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

