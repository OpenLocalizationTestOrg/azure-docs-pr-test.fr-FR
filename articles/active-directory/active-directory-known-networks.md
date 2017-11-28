---
title: "Réseaux aaaKnown Bonjour portail classique Azure | Documents Microsoft"
description: "En configurant les réseaux connus, vous évite d’avoir des adresses IP appartenant à votre organisation incluse dans hello connexions depuis plusieurs zones géographiques et des connexions à partir d’adresses IP avec les rapports d’activité suspecte."
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
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a><span data-ttu-id="8f385-103">Réseaux connus</span><span class="sxs-lookup"><span data-stu-id="8f385-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f385-104">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="8f385-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="8f385-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8f385-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="8f385-106">Vous pouvez utiliser l’accès Azure Active Directory et l’utilisation des rapports toogain visibilité intégrité de hello et la sécurité de répertoire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="8f385-106">You can use Azure Active Directory's access and usage reports toogain visibility into hello integrity and security of your organization’s directory.</span></span> <span data-ttu-id="8f385-107">Avec cette information, un administrateur d’annuaire peut déterminer plus précisément où peut se trouver des risques de sécurité afin qu’ils peuvent planifier en conséquence toomitigate ces risques.</span><span class="sxs-lookup"><span data-stu-id="8f385-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan toomitigate those risks.</span></span>

<span data-ttu-id="8f385-108">Il est possible que hello »*connexions depuis plusieurs zones géographiques*« et »*connexions à partir d’adresses IP avec une activité suspecte*« rapports signaler de manière incorrecte les adresses IP qui sont en réalité détenus par votre organisation.</span><span class="sxs-lookup"><span data-stu-id="8f385-108">It is possible that hello “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="8f385-109">Cela peut, par exemple, se produire dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="8f385-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="8f385-110">Un utilisateur de votre bureau de Boston s’est connecté à distance tooyour centre de données dans les déclencheurs de San Francisco hello les rapports « Connexions depuis plusieurs zones géographiques »</span><span class="sxs-lookup"><span data-stu-id="8f385-110">A user in your Boston office has signed in remotely tooyour data center in San Francisco triggers hello “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="8f385-111">Un utilisateur de votre organisation tente toosign sur plusieurs fois avec un hello de déclencheurs de mot de passe incorrect les rapports « Connexions à partir d’adresses IP avec une activité suspecte »</span><span class="sxs-lookup"><span data-stu-id="8f385-111">A user of your organization tries toosign-on several times with an incorrect password triggers hello “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="8f385-112">tooprevent ces cas de sécurité trompeuse générant des rapports, vous devez ajouter les connus adresse toohello liste des plages IP de l’adresse IP publique de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="8f385-112">tooprevent these cases from generating misleading security reports, you should add known IP address ranges toohello list of your organization's public IP address.</span></span>    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a><span data-ttu-id="8f385-113">plages d’adresse IP publique de votre organisation tooadd, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8f385-113">tooadd your organization’s public IP address ranges, perform hello following steps:</span></span>

1. <span data-ttu-id="8f385-114">Authentification toohello [portail de gestion Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8f385-114">Sign-on toohello [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="8f385-115">Dans le volet gauche de hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8f385-115">In hello left pane, click **Active Directory**.</span></span> 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="8f385-117">Bonjour **répertoire** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="8f385-117">In hello **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="8f385-118">Dans le menu hello haut de hello, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="8f385-118">In hello menu on hello top, click **Configure**.</span></span> 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="8f385-120">Sur l’onglet configurer de hello, accédez trop**vos plages d’adresses IP publiques organisations**</span><span class="sxs-lookup"><span data-stu-id="8f385-120">On hello Configure tab, go too**your organizations public IP address ranges**</span></span> 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="8f385-122">Cliquez sur **Ajouter des plages d'adresses IP connues**.</span><span class="sxs-lookup"><span data-stu-id="8f385-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="8f385-123">Ajoutez vos plages d’adresses dans la boîte de dialogue hello qui s’affiche, puis cliquez sur la coche hello lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="8f385-123">Add your address ranges in hello dialog box that appears, and then click hello check button  when you are done.</span></span> 

    ![Réseaux connus](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="8f385-125">**Ressources supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="8f385-125">**Additional resources:**</span></span>

* [<span data-ttu-id="8f385-126">Affichage de vos rapports d’accès et d’utilisation</span><span class="sxs-lookup"><span data-stu-id="8f385-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="8f385-127">Connexions à partir d’adresses IP affichant une activité suspecte</span><span class="sxs-lookup"><span data-stu-id="8f385-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="8f385-128">Connexions depuis plusieurs zones géographiques</span><span class="sxs-lookup"><span data-stu-id="8f385-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

