---
title: "aaaProblem à l’aide d’accès des applications en libre-service | Documents Microsoft"
description: "Résoudre les problèmes connexes tooself service application l’accès"
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
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="2d758-103">Problème lié à l’accès aux applications en libre-service</span><span class="sxs-lookup"><span data-stu-id="2d758-103">Problem using self-service application access</span></span>

<span data-ttu-id="2d758-104">Accès à l’application automatique est un tooself aux utilisateurs de tooallow excellent moyen-découvrir les applications, vous pouvez également autoriser hello entreprise groupe tooapprove toothose applications.</span><span class="sxs-lookup"><span data-stu-id="2d758-104">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="2d758-105">Vous pouvez autoriser les informations d’identification de groupe toomanage hello hello entreprise affecté les utilisateurs de toothose de droite de l’authentification unique de mot de passe sur les Applications à partir de leurs panneaux d’accès.</span><span class="sxs-lookup"><span data-stu-id="2d758-105">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="2d758-106">Avant que vos utilisateurs découvrir automatiquement des applications à partir de leur volet d’accès, vous devez tooenable **accès à l’application automatique** tooany les applications que vous souhaitez tooallow utilisateurs tooself-découvrir et de demander l’accès à.</span><span class="sxs-lookup"><span data-stu-id="2d758-106">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="2d758-107">Général émet toocheck tout d’abord</span><span class="sxs-lookup"><span data-stu-id="2d758-107">General issues toocheck first</span></span>

-   <span data-ttu-id="2d758-108">Vérifiez que l’accès à l’application en libre-service est configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="2d758-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="2d758-109">Voir « Comment accéder à application en libre service tooconfigure ».</span><span class="sxs-lookup"><span data-stu-id="2d758-109">See “How tooconfigure self-service application access”.</span></span>

-   <span data-ttu-id="2d758-110">Vérifiez que hello utilisateur ou le groupe a été activé l’accès des applications en libre-service toorequest.</span><span class="sxs-lookup"><span data-stu-id="2d758-110">Make sure hello user or group has been enabled toorequest self-service application access.</span></span>

-   <span data-ttu-id="2d758-111">Vérifiez que hello utilisateur visite sur place de correct hello pour l’accès des applications en libre-service.</span><span class="sxs-lookup"><span data-stu-id="2d758-111">Make sure hello user is visiting hello correct place for self-service application access.</span></span> <span data-ttu-id="2d758-112">les utilisateurs peuvent naviguer tootheir [volet d’accès Application](https://myapps.microsoft.com/) et cliquez sur hello **+ ajouter** bouton toofind hello applications toowhich que vous avez activé les accès en libre-service.</span><span class="sxs-lookup"><span data-stu-id="2d758-112">users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled self-service access.</span></span>

-   <span data-ttu-id="2d758-113">Si l’accès à l’application automatique a été récemment configuré, réessayez toosign et l’extraction dans le volet d’accès de l’utilisateur hello après quelques minutes toosee si les modifications d’accès en libre-service hello apparaissent.</span><span class="sxs-lookup"><span data-stu-id="2d758-113">If self-service application access was just recently configured, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello self-service access changes have appeared.</span></span>

## <a name="how-tooconfigure-self-service-application-access"></a><span data-ttu-id="2d758-114">Comment accéder aux applications en libre-service tooconfigure</span><span class="sxs-lookup"><span data-stu-id="2d758-114">How tooconfigure self-service application access</span></span>

<span data-ttu-id="2d758-115">tooenable libre-service accès tooan une application, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2d758-115">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="2d758-116">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="2d758-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2d758-117">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="2d758-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2d758-118">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="2d758-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2d758-119">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2d758-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2d758-120">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="2d758-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2d758-121">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="2d758-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2d758-122">Sélectionnez l’application hello liste de hello toofrom tooenable accès en libre-service.</span><span class="sxs-lookup"><span data-stu-id="2d758-122">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="2d758-123">Une fois le charge de l’application hello, cliquez sur **libre-service** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2d758-123">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2d758-124">tooenable accès des applications en libre-service pour cette application, activez hello **autoriser l’application de toothis accès toorequest ?** basculer trop**Oui.**</span><span class="sxs-lookup"><span data-stu-id="2d758-124">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="2d758-125">Ensuite, tooselect hello groupe toowhich les utilisateurs qui demandent l’accès toothis application doit être ajoutée, cliquez sur le libellé de toohello suivant hello sélecteur **toowhich groupe doivent être assignées utilisateurs ajoutés ?** et sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="2d758-125">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="2d758-126">**Facultatif :** si vous souhaitez toorequire une approbation de l’entreprise avant que les utilisateurs sont autorisés à accéder, affectez à hello **exiger l’approbation avant d’accorder l’accès toothis application ?** basculer trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="2d758-126">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="2d758-127">**Facultatif : pour les applications à l’aide d’un mot de passe d’authentification unique sur uniquement,** si vous le souhaitez tooallow ces business approbateurs toospecify hello des mots de passe sont envoyés application toothis pour les utilisateurs approuvés, définissez hello **autoriser approbateurs tooset mots de passe de l’utilisateur pour cette application ?**  basculer trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="2d758-127">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="2d758-128">**Facultatif :** toospecify hello entreprise approbateurs sont autorisés à application de toothis tooapprove access, cliquez sur le libellé de toohello suivant hello sélecteur **qui est autorisé d’application de toothis accès tooapprove ?** tooselect des approbateurs d’entreprise too10.</span><span class="sxs-lookup"><span data-stu-id="2d758-128">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="2d758-129">Les groupes ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2d758-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="2d758-130">**Facultatif :** **pour les applications qui présentent les rôles**, si vous voulez que le rôle de tooa tooassign libre-service des utilisateurs approuvés, cliquez sur toohello suivant du sélecteur hello **toowhich rôle doivent être assigné aux utilisateurs dans ce application ?**  tooselect hello rôle toowhich ces utilisateurs doivent être affectés.</span><span class="sxs-lookup"><span data-stu-id="2d758-130">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="2d758-131">Cliquez sur hello **enregistrer** bouton haut hello hello panneau toofinish.</span><span class="sxs-lookup"><span data-stu-id="2d758-131">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="2d758-132">Après avoir terminé la configuration de l’application en libre service, les utilisateurs peuvent naviguer tootheir [volet d’accès Application](https://myapps.microsoft.com/) et cliquez sur hello **+ ajouter** bouton toofind hello applications toowhich que vous avez activé Accès en libre-service.</span><span class="sxs-lookup"><span data-stu-id="2d758-132">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="2d758-133">Les approbateurs d’entreprise reçoivent également une notification dans leur [volet d’accès aux applications](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="2d758-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="2d758-134">Vous pouvez activer un courrier électronique pour les informer lorsqu’un utilisateur a demandé l’application accès tooan nécessitant leur approbation.</span><span class="sxs-lookup"><span data-stu-id="2d758-134">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="2d758-135">Ces approbations prend en charge les workflows approbation unique uniquement, ce qui signifie que si vous spécifiez plusieurs approbateurs, tout seul approbateur peut approuver accès toohello application.</span><span class="sxs-lookup"><span data-stu-id="2d758-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="2d758-136">Si ces étapes de dépannage ne résolvent pas le problème de hello</span><span class="sxs-lookup"><span data-stu-id="2d758-136">If these troubleshooting steps do not resolve hello issue</span></span> 

<span data-ttu-id="2d758-137">Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :</span><span class="sxs-lookup"><span data-stu-id="2d758-137">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="2d758-138">ID d’erreur de corrélation</span><span class="sxs-lookup"><span data-stu-id="2d758-138">Correlation error ID</span></span>

-   <span data-ttu-id="2d758-139">UPN (adresse e-mail de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="2d758-139">UPN (user email address)</span></span>

-   <span data-ttu-id="2d758-140">ID de locataire</span><span class="sxs-lookup"><span data-stu-id="2d758-140">TenantID</span></span>

-   <span data-ttu-id="2d758-141">Type de navigateur</span><span class="sxs-lookup"><span data-stu-id="2d758-141">Browser type</span></span>

-   <span data-ttu-id="2d758-142">Fuseau horaire et heure/période à laquelle l’erreur se produit</span><span class="sxs-lookup"><span data-stu-id="2d758-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="2d758-143">Traces Fiddler</span><span class="sxs-lookup"><span data-stu-id="2d758-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d758-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d758-144">Next steps</span></span>
[<span data-ttu-id="2d758-145">Configuration d’Azure Active Directory pour la gestion de groupe en libre-service</span><span class="sxs-lookup"><span data-stu-id="2d758-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
