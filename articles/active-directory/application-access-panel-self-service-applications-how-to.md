---
title: "accès à l’application automatique aaaHow toouse | Documents Microsoft"
description: "Activer les applications en libre-service accès tooallow utilisateurs toofind leurs propres applications."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a><span data-ttu-id="054c1-103">Comment accéder aux applications en libre-service toouse</span><span class="sxs-lookup"><span data-stu-id="054c1-103">How toouse self-service application access</span></span>

<span data-ttu-id="054c1-104">Avant que vos utilisateurs découvrir automatiquement des applications à partir de leur volet d’accès, vous devez tooenable **accès à l’application automatique** tooany les applications que vous souhaitez tooallow utilisateurs tooself-découvrir et de demander l’accès à.</span><span class="sxs-lookup"><span data-stu-id="054c1-104">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

<span data-ttu-id="054c1-105">Cette fonctionnalité est un excellent moyen de vous toosave temps et l’argent en tant qu’un groupe informatique et il est vivement recommandée dans le cadre d’un déploiement d’applications modernes avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="054c1-105">This feature is a great way for you toosave time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="054c1-106">À l’aide de cette fonctionnalité, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="054c1-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="054c1-107">Permettre aux utilisateurs de découvrir automatiquement les applications à partir de hello [volet d’accès Application](https://myapps.microsoft.com/) sans déranger hello informatique de groupe.</span><span class="sxs-lookup"><span data-stu-id="054c1-107">Let users self-discover applications from hello [Application Access Panel](https://myapps.microsoft.com/) without bothering hello IT group.</span></span>

-   <span data-ttu-id="054c1-108">Ajoutez ces groupe préconfiguré tooa des utilisateurs afin de pouvoir voir qui a demandé l’accès, de supprimer l’accès et gérer des rôles hello toothem.</span><span class="sxs-lookup"><span data-stu-id="054c1-108">Add those users tooa pre-configured group so you can see who has requested access, remove access, and manage hello roles assigned toothem.</span></span>

-   <span data-ttu-id="054c1-109">Si vous le souhaitez autorisant un approbateur d’entreprise tooapprove les demandes d’accès application hello groupe informatique n’a pas besoin.</span><span class="sxs-lookup"><span data-stu-id="054c1-109">Optionally allow a business approver tooapprove application access requests so hello IT group doesn’t have to.</span></span>

-   <span data-ttu-id="054c1-110">Configurez éventuellement des personnes too10 peuvent autoriser l’accès toothis application.</span><span class="sxs-lookup"><span data-stu-id="054c1-110">Optionally configure up too10 individuals who may approve access toothis application.</span></span>

-   <span data-ttu-id="054c1-111">Si vous le souhaitez autoriser un approbateur d’entreprise des mots de passe tooset hello ces utilisateurs peuvent utiliser toosign dans l’application toohello, directement à partir de l’approbateur d’entreprise hello [volet d’accès Application](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="054c1-111">Optionally allow a business approver tooset hello passwords those users can use toosign in toohello application, right from hello business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="054c1-112">Éventuellement automatiquement attribuer le rôle d’application tooan libre-service des utilisateurs attribués directement.</span><span class="sxs-lookup"><span data-stu-id="054c1-112">Optionally automatically assign self-service assigned users tooan application role directly.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="054c1-113">Activer les applications en libre-service accès tooallow utilisateurs toofind leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="054c1-113">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="054c1-114">Accès à l’application automatique est un tooself aux utilisateurs de tooallow excellent moyen-découvrir les applications, vous pouvez également autoriser hello entreprise groupe tooapprove toothose applications.</span><span class="sxs-lookup"><span data-stu-id="054c1-114">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="054c1-115">Vous pouvez autoriser les informations d’identification de groupe toomanage hello hello entreprise affecté les utilisateurs de toothose de droite de l’authentification unique de mot de passe sur les Applications à partir de leurs panneaux d’accès.</span><span class="sxs-lookup"><span data-stu-id="054c1-115">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="054c1-116">tooenable libre-service accès tooan une application, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="054c1-116">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="054c1-117">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="054c1-117">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="054c1-118">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="054c1-118">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="054c1-119">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="054c1-119">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="054c1-120">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="054c1-120">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="054c1-121">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="054c1-121">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="054c1-122">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="054c1-122">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="054c1-123">Sélectionnez l’application hello liste de hello toofrom tooenable accès en libre-service.</span><span class="sxs-lookup"><span data-stu-id="054c1-123">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="054c1-124">Une fois le charge de l’application hello, cliquez sur **libre-service** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="054c1-124">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="054c1-125">tooenable accès des applications en libre-service pour cette application, activez hello **autoriser l’application de toothis accès toorequest ?** basculer trop**Oui.**</span><span class="sxs-lookup"><span data-stu-id="054c1-125">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="054c1-126">Ensuite, tooselect hello groupe toowhich les utilisateurs qui demandent l’accès toothis application doit être ajoutée, cliquez sur le libellé de toohello suivant hello sélecteur **toowhich groupe doivent être assignées utilisateurs ajoutés ?** et sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="054c1-126">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="054c1-127">**Facultatif :** si vous souhaitez toorequire une approbation de l’entreprise avant que les utilisateurs sont autorisés à accéder, affectez à hello **exiger l’approbation avant d’accorder l’accès toothis application ?** basculer trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="054c1-127">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="054c1-128">**Facultatif : pour les applications à l’aide d’un mot de passe d’authentification unique sur uniquement,** si vous le souhaitez tooallow ces business approbateurs toospecify hello des mots de passe sont envoyés application toothis pour les utilisateurs approuvés, définissez hello **autoriser approbateurs tooset mots de passe de l’utilisateur pour cette application ?**  basculer trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="054c1-128">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="054c1-129">**Facultatif :** toospecify hello entreprise approbateurs sont autorisés à application de toothis tooapprove access, cliquez sur le libellé de toohello suivant hello sélecteur **qui est autorisé d’application de toothis accès tooapprove ?** tooselect des approbateurs d’entreprise too10.</span><span class="sxs-lookup"><span data-stu-id="054c1-129">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

   * <span data-ttu-id="054c1-130">Les groupes ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="054c1-130">Groups are not supported.</span></span>

13. <span data-ttu-id="054c1-131">**Facultatif :** **pour les applications qui présentent les rôles**, si vous voulez que le rôle de tooa tooassign libre-service des utilisateurs approuvés, cliquez sur toohello suivant du sélecteur hello **toowhich rôle doivent être assigné aux utilisateurs dans ce application ?**  tooselect hello rôle toowhich ces utilisateurs doivent être affectés.</span><span class="sxs-lookup"><span data-stu-id="054c1-131">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="054c1-132">Cliquez sur hello **enregistrer** bouton haut hello hello panneau toofinish.</span><span class="sxs-lookup"><span data-stu-id="054c1-132">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="054c1-133">Après avoir terminé la configuration de l’application en libre service, les utilisateurs peuvent naviguer tootheir [volet d’accès Application](https://myapps.microsoft.com/) et cliquez sur hello **+ ajouter** bouton toofind hello applications toowhich que vous avez activé Accès en libre-service.</span><span class="sxs-lookup"><span data-stu-id="054c1-133">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="054c1-134">Les approbateurs d’entreprise reçoivent également une notification dans leur [volet d’accès aux applications](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="054c1-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="054c1-135">Vous pouvez activer un courrier électronique pour les informer lorsqu’un utilisateur a demandé l’application accès tooan nécessitant leur approbation.</span><span class="sxs-lookup"><span data-stu-id="054c1-135">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="054c1-136">Ces approbations prend en charge les workflows approbation unique uniquement, ce qui signifie que si vous spécifiez plusieurs approbateurs, tout seul approbateur peut approuver accès toohello application.</span><span class="sxs-lookup"><span data-stu-id="054c1-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="054c1-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="054c1-137">Next steps</span></span>
[<span data-ttu-id="054c1-138">Configuration d’Azure Active Directory pour la gestion de groupe en libre-service</span><span class="sxs-lookup"><span data-stu-id="054c1-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
