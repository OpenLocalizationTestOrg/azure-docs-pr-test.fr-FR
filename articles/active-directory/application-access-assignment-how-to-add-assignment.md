---
title: application tooan aaaHow tooassign les utilisateurs et les groupes | Documents Microsoft
description: "Affecter des utilisateurs toogrant accès aux applications de toohello"
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a><span data-ttu-id="590ac-103">Comment tooassign les utilisateurs et les groupes d’application de tooan</span><span class="sxs-lookup"><span data-stu-id="590ac-103">How tooassign users and groups tooan application</span></span>

<span data-ttu-id="590ac-104">Avant que vos utilisateurs peuvent effectuer les hello ci-dessous pour une application spécifique, vous devez toofirst **affectez-les toohello application** toogrant les accès :</span><span class="sxs-lookup"><span data-stu-id="590ac-104">Before your users can do any of hello below for a specific application, you need toofirst **assign them toohello application** toogrant them access:</span></span>

-   <span data-ttu-id="590ac-105">Accéder à une application par **accédant directement les URL de l’application toohello** (également appelé initialisée par SP authentification).</span><span class="sxs-lookup"><span data-stu-id="590ac-105">Access an application by **navigating toohello application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="590ac-106">Accéder à une application à l’aide de hello **URL d’accès utilisateur** sur l’application **propriétés** page (également appelé initialisée par IDP authentification).</span><span class="sxs-lookup"><span data-stu-id="590ac-106">Access an application by using hello **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="590ac-107">Afficher une application sur leur [volet d’accès aux applications](https://myapps.microsoft.com/) ou leur application mobile.</span><span class="sxs-lookup"><span data-stu-id="590ac-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="590ac-108">Afficher une application qui apparaît sur leur [Lanceur d’applications Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="590ac-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-tooassign-applications-with-azure-active-directory"></a><span data-ttu-id="590ac-109">Applications tooassign de méthodes avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="590ac-109">Methods tooassign applications with Azure Active Directory</span></span> 

<span data-ttu-id="590ac-110">Il existe 3 méthodes d’affectation d’applications avec Azure Active Directory :</span><span class="sxs-lookup"><span data-stu-id="590ac-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="590ac-111">Affecter un utilisateur directement tooan application en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="590ac-111">Assign a user directly tooan application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="590ac-112">Assigner un groupe directement tooan application en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="590ac-112">Assign a group directly tooan application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="590ac-113">Activer les applications en libre-service accès tooallow utilisateurs toofind leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="590ac-113">Enable self-service application access tooallow users toofind their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="590ac-114">Affecter un utilisateur directement en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="590ac-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="590ac-115">tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="590ac-115">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="590ac-116">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="590ac-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="590ac-117">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="590ac-118">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="590ac-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="590ac-119">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="590ac-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="590ac-120">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="590ac-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="590ac-121">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="590ac-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="590ac-122">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-122">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="590ac-123">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-123">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="590ac-124">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="590ac-124">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="590ac-125">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="590ac-125">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="590ac-126">Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="590ac-126">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="590ac-127">Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="590ac-127">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="590ac-128">Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="590ac-128">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="590ac-129">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="590ac-129">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="590ac-130">Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="590ac-130">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="590ac-131">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="590ac-131">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="590ac-132">Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="590ac-132">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="590ac-133">Après une courte période de temps, les utilisateurs de hello que vous avez sélectionné en toolaunch en mesure de ces applications à l’aide de hello des méthodes décrites dans la section de description de solution hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-133">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="590ac-134">Assigner un groupe directement tooan application en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="590ac-134">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="590ac-135">tooassign un ou plusieurs groupes tooan application directement, hello suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="590ac-135">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="590ac-136">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="590ac-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="590ac-137">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="590ac-138">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="590ac-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="590ac-139">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="590ac-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="590ac-140">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="590ac-140">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="590ac-141">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="590ac-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="590ac-142">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-142">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="590ac-143">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-143">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="590ac-144">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="590ac-144">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="590ac-145">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="590ac-145">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="590ac-146">Type Bonjour **nom de groupe complète** groupe hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="590ac-146">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="590ac-147">Placez le curseur sur hello **groupe** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="590ac-147">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="590ac-148">Cliquez sur tooadd de photo ou le logo de profil de hello case à cocher toohello groupe suivant votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="590ac-148">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="590ac-149">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs groupes**, type dans un autre **nom de groupe complète** dans hello **recherche par nom ou adresse de messagerie** zone de recherche, Cliquez sur tooadd de case à cocher hello toohello de ce groupe **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="590ac-149">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="590ac-150">Lorsque vous avez fini de sélectionner les groupes, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="590ac-150">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="590ac-151">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un toohello de tooassign rôle groupes que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="590ac-151">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="590ac-152">Cliquez sur hello **affecter** bouton tooassign hello application toohello les groupes sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="590ac-152">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="590ac-153">Après une courte période de temps, les utilisateurs de hello au sein de groupes hello que vous avez sélectionné en toolaunch en mesure de ces applications à l’aide de hello des méthodes décrites dans la section de description de solution hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-153">After a short period of time, hello users within hello groups you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span> <span data-ttu-id="590ac-154">S’il s’agit de groupes dynamiques, un délai de traitement supplémentaire peut survenir avant que les utilisateurs ne voient ces affectations dans ces groupes affectés.</span><span class="sxs-lookup"><span data-stu-id="590ac-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="590ac-155">Activer les applications en libre-service accès tooallow utilisateurs toofind leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="590ac-155">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="590ac-156">Accès à l’application automatique est un tooself aux utilisateurs de tooallow excellent moyen-découvrir les applications, vous pouvez également autoriser hello entreprise groupe tooapprove toothose applications.</span><span class="sxs-lookup"><span data-stu-id="590ac-156">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="590ac-157">Vous pouvez autoriser les informations d’identification de groupe toomanage hello hello entreprise affecté les utilisateurs de toothose de droite de l’authentification unique de mot de passe sur les Applications à partir de leurs panneaux d’accès.</span><span class="sxs-lookup"><span data-stu-id="590ac-157">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="590ac-158">tooenable libre-service accès tooan une application, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="590ac-158">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="590ac-159">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="590ac-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="590ac-160">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="590ac-161">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="590ac-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="590ac-162">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="590ac-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="590ac-163">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="590ac-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="590ac-164">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="590ac-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="590ac-165">Sélectionnez l’application hello liste de hello toofrom tooenable accès en libre-service.</span><span class="sxs-lookup"><span data-stu-id="590ac-165">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="590ac-166">Une fois le charge de l’application hello, cliquez sur **libre-service** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-166">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="590ac-167">tooenable accès des applications en libre-service pour cette application, activez hello **autoriser l’application de toothis accès toorequest ?** basculer trop**Oui.**</span><span class="sxs-lookup"><span data-stu-id="590ac-167">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="590ac-168">Ensuite, tooselect hello groupe toowhich les utilisateurs qui demandent l’accès toothis application doit être ajoutée, cliquez sur le libellé de toohello suivant hello sélecteur **toowhich groupe doivent être assignées utilisateurs ajoutés ?** et sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="590ac-168">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="590ac-169">**Facultatif :** si vous souhaitez toorequire une approbation de l’entreprise avant que les utilisateurs sont autorisés à accéder, affectez à hello **exiger l’approbation avant d’accorder l’accès toothis application ?** basculer trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="590ac-169">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="590ac-170">**Facultatif : pour les applications à l’aide d’un mot de passe d’authentification unique sur uniquement,** si vous le souhaitez tooallow ces business approbateurs toospecify hello des mots de passe sont envoyés application toothis pour les utilisateurs approuvés, définissez hello **autoriser approbateurs tooset mots de passe de l’utilisateur pour cette application ?**  basculer trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="590ac-170">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="590ac-171">**Facultatif :** toospecify hello entreprise approbateurs sont autorisés à application de toothis tooapprove access, cliquez sur le libellé de toohello suivant hello sélecteur **qui est autorisé d’application de toothis accès tooapprove ?** tooselect des approbateurs d’entreprise too10.</span><span class="sxs-lookup"><span data-stu-id="590ac-171">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="590ac-172">Les groupes ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="590ac-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="590ac-173">**Facultatif :** **pour les applications qui présentent les rôles**, si vous voulez que le rôle de tooa tooassign libre-service des utilisateurs approuvés, cliquez sur toohello suivant du sélecteur hello **toowhich rôle doivent être assigné aux utilisateurs dans ce application ?**  tooselect hello rôle toowhich ces utilisateurs doivent être affectés.</span><span class="sxs-lookup"><span data-stu-id="590ac-173">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="590ac-174">Cliquez sur hello **enregistrer** bouton haut hello hello panneau toofinish.</span><span class="sxs-lookup"><span data-stu-id="590ac-174">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="590ac-175">Après avoir terminé la configuration de l’application en libre service, les utilisateurs peuvent naviguer tootheir [volet d’accès Application](https://myapps.microsoft.com/) et cliquez sur hello **+ ajouter** bouton toofind hello applications toowhich que vous avez activé Accès en libre-service.</span><span class="sxs-lookup"><span data-stu-id="590ac-175">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="590ac-176">Les approbateurs d’entreprise reçoivent également une notification dans leur [volet d’accès aux applications](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="590ac-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="590ac-177">Vous pouvez activer un courrier électronique pour les informer lorsqu’un utilisateur a demandé l’application accès tooan nécessitant leur approbation.</span><span class="sxs-lookup"><span data-stu-id="590ac-177">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="590ac-178">Ces approbations prend en charge les flux de travail approbation unique uniquement, ce qui signifie que si vous spécifiez plusieurs approbateurs, un approbateur unique peut application de toohello accès approbateur.</span><span class="sxs-lookup"><span data-stu-id="590ac-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="590ac-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="590ac-179">Next steps</span></span>
[<span data-ttu-id="590ac-180">Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="590ac-180">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
