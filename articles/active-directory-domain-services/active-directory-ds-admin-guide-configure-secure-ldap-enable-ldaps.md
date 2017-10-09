---
title: "aaaConfigure sécurisé LDAP (LDAPS) dans les Services de domaine Active Directory de Azure | Documents Microsoft"
description: "Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine géré par les services de domaine Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="1b863-103">Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine managé Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="1b863-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1b863-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="1b863-104">Before you begin</span></span>
<span data-ttu-id="1b863-105">Vérifiez que vous avez effectué [tâche 2 - tooa de certificat LDAP sécurisé exportation hello. Le fichier PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="1b863-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="1b863-106">Choisir toouse hello aperçu expérience du portail Azure ou hello toocomplete de portail classique Azure cette tâche.</span><span class="sxs-lookup"><span data-stu-id="1b863-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="1b863-107">**Portail Azure (aperçu)**: [Enable secure LDAP à l’aide de hello portail Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="1b863-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="1b863-108">**Portail Azure classic**: [Enable secure LDAP à l’aide du portail Azure classic de hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="1b863-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a><span data-ttu-id="1b863-109">Tâche 3 : activer LDAP sécurisé pour hello de domaine gérés à l’aide de hello portail Azure (aperçu)</span><span class="sxs-lookup"><span data-stu-id="1b863-109">Task 3 - enable secure LDAP for hello managed domain using hello Azure portal (Preview)</span></span>
<span data-ttu-id="1b863-110">tooenable LDAP sécurisé, effectuer hello configuration comme suit :</span><span class="sxs-lookup"><span data-stu-id="1b863-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="1b863-111">Accédez toohello  **[portail Azure](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="1b863-111">Navigate toohello **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="1b863-112">Rechercher des services de domaine Bonjour **recherche les ressources** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="1b863-112">Search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="1b863-113">Sélectionnez **les Services de domaine Active Directory de Azure** à partir du résultat de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="1b863-113">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="1b863-114">Hello **les Services de domaine Active Directory de Azure** panneau répertorie votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="1b863-114">hello **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Rechercher le domaine managé en cours d’approvisionnement](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="1b863-116">Cliquez sur nom hello hello géré (par exemple, « contoso100.com ») de domaine toosee plus de détails sur le domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="1b863-116">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services - État d’approvisionnement](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="1b863-118">Cliquez sur **LDAP sécurisé** hello volet de navigation.</span><span class="sxs-lookup"><span data-stu-id="1b863-118">Click **Secure LDAP** on hello navigation pane.</span></span>

    ![Domain Services - Panneau LDAP sécurisé](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="1b863-120">Par défaut, accès tooyour managé domaine LDAP sécurisé est désactivé.</span><span class="sxs-lookup"><span data-stu-id="1b863-120">By default, secure LDAP access tooyour managed domain is disabled.</span></span> <span data-ttu-id="1b863-121">Activer/désactiver **LDAP sécurisé** trop**activer**.</span><span class="sxs-lookup"><span data-stu-id="1b863-121">Toggle **Secure LDAP** too**Enable**.</span></span>

    ![Activer LDAP sécurisé](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="1b863-123">Par défaut, tooyour d’accès LDAP sécurisé gérés domaine via hello qu'internet est désactivée.</span><span class="sxs-lookup"><span data-stu-id="1b863-123">By default, secure LDAP access tooyour managed domain over hello internet is disabled.</span></span> <span data-ttu-id="1b863-124">Activer/désactiver **autoriser l’accès LDAP sécurisé sur hello internet** trop**activer**, si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="1b863-124">Toggle **Allow secure LDAP access over hello internet** too**Enable**, if desired.</span></span> 

6. <span data-ttu-id="1b863-125">Cliquez sur suivant d’icône hello dossier **. Fichier PFX avec certificat LDAP sécurisé**.</span><span class="sxs-lookup"><span data-stu-id="1b863-125">Click hello folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="1b863-126">Spécifier le fichier PFX de hello chemin d’accès toohello avec certificat hello pour accès toohello managé domaine LDAP sécurisé.</span><span class="sxs-lookup"><span data-stu-id="1b863-126">Specify hello path toohello PFX file with hello certificate for secure LDAP access toohello managed domain.</span></span>

7. <span data-ttu-id="1b863-127">Spécifiez hello **toodecrypt de mot de passe. Le fichier PFX**.</span><span class="sxs-lookup"><span data-stu-id="1b863-127">Specify hello **Password toodecrypt .PFX file**.</span></span> <span data-ttu-id="1b863-128">Fournir hello même mot de passe utilisé lors de l’exportation du fichier de certificat toohello PFX hello.</span><span class="sxs-lookup"><span data-stu-id="1b863-128">Provide hello same password you used when exporting hello certificate toohello PFX file.</span></span>

8. <span data-ttu-id="1b863-129">Lorsque vous avez terminé, cliquez sur hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="1b863-129">When you are done, click hello **Save** button.</span></span>

9. <span data-ttu-id="1b863-130">Vous voyez une notification qui vous informe de que LDAP sécurisé est configuré pour le domaine géré de hello.</span><span class="sxs-lookup"><span data-stu-id="1b863-130">You see a notification that informs you secure LDAP is being configured for hello managed domain.</span></span> <span data-ttu-id="1b863-131">Jusqu'à ce que cette opération est terminée, vous ne pouvez pas modifier d’autres paramètres pour le domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="1b863-131">Until this operation is complete, you cannot modify other settings for hello domain.</span></span>

    ![Configuration de LDAP sécurisé pour le domaine géré de hello](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="1b863-133">Il prend environ 10 minutes too15 tooenable LDAP sécurisé pour votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="1b863-133">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="1b863-134">Si hello fourni de certificat LDAP sécurisé ne correspond pas à hello requis critères, LDAP sécurisé n’est pas activée pour votre annuaire et vous voyez une erreur.</span><span class="sxs-lookup"><span data-stu-id="1b863-134">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="1b863-135">Par exemple, nom de domaine hello est incorrect, le certificat de hello a déjà expiré ou va bientôt expire.</span><span class="sxs-lookup"><span data-stu-id="1b863-135">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span> <span data-ttu-id="1b863-136">Dans ce cas, réessayez avec un certificat valide.</span><span class="sxs-lookup"><span data-stu-id="1b863-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="1b863-137">Tâche 4 - configurer DNS tooaccess hello domaine géré à partir de hello internet</span><span class="sxs-lookup"><span data-stu-id="1b863-137">Task 4 - configure DNS tooaccess hello managed domain from hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="1b863-138">**Tâches facultatives** : Si vous n’envisagez pas de domaine géré de tooaccess hello à l’aide du protocole LDAPS plus hello internet, ignorez cette étape de configuration.</span><span class="sxs-lookup"><span data-stu-id="1b863-138">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="1b863-139">Avant de commencer cette tâche, assurez-vous d’avoir effectué les étapes hello décrites dans [tâche 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="1b863-139">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="1b863-140">Une fois que vous avez activé l’accès LDAP sécurisé sur internet de hello pour votre domaine géré, vous devez tooupdate DNS afin que les ordinateurs clients peuvent trouver ce domaine géré.</span><span class="sxs-lookup"><span data-stu-id="1b863-140">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="1b863-141">Extrémité hello de tâche 3, une adresse IP externe est affichée sur hello **propriétés** lame **adresse IP externe pour LDAPS accès**.</span><span class="sxs-lookup"><span data-stu-id="1b863-141">At hello end of task 3, an external IP address is displayed on hello **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="1b863-142">Configurez votre fournisseur DNS externe afin que ce nom DNS de hello Hello géré l’adresse IP externe de domaine (par exemple, ' ldaps.contoso100.com') toothis de points.</span><span class="sxs-lookup"><span data-stu-id="1b863-142">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="1b863-143">Dans notre exemple, nous devons hello toocreate suivant l’entrée DNS :</span><span class="sxs-lookup"><span data-stu-id="1b863-143">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="1b863-144">C’est tout : vous êtes maintenant toohello tooconnect prêt géré domaine à l’aide de LDAP sécurisé sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="1b863-144">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="1b863-145">Souvenez-vous que les ordinateurs clients doivent approuver l’émetteur de hello de hello LDAPS certificat toobe en mesure de tooconnect de correctement toohello gérés à l’aide du protocole LDAPS de domaine.</span><span class="sxs-lookup"><span data-stu-id="1b863-145">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="1b863-146">Si vous utilisez une autorité de certification approuvée publiquement, il est inutile toodo quoi que ce soit dans la mesure où les ordinateurs clients approuver ces émetteurs de certificats.</span><span class="sxs-lookup"><span data-stu-id="1b863-146">If you are using a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="1b863-147">Si vous utilisez un certificat auto-signé, installez hello publique partie hello un certificat auto-signé dans le magasin de certificats approuvés hello sur l’ordinateur client de hello.</span><span class="sxs-lookup"><span data-stu-id="1b863-147">If you are using a self-signed certificate, install hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="1b863-148">Tâche 5 : verrouillage LDAPS accéder tooyour géré domaine sur hello internet</span><span class="sxs-lookup"><span data-stu-id="1b863-148">Task 5 - lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="1b863-149">**Tâches facultatives** : Si vous n’avez pas activé LDAPS domaine géré de toohello accès plus hello internet, ignorez cette étape de configuration.</span><span class="sxs-lookup"><span data-stu-id="1b863-149">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="1b863-150">Avant de commencer cette tâche, assurez-vous d’avoir effectué les étapes hello décrites dans [tâche 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="1b863-150">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="1b863-151">Exposition de votre domaine géré pour l’accès LDAPS sur hello internet représente une menace pour la sécurité.</span><span class="sxs-lookup"><span data-stu-id="1b863-151">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="1b863-152">Bonjour domaine géré est accessible à partir de hello internet au port hello utilisé pour LDAP sécurisé (autrement dit, le port 636).</span><span class="sxs-lookup"><span data-stu-id="1b863-152">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="1b863-153">Par conséquent, vous pouvez choisir toorestrict accès toohello géré domaine toospecific connu des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="1b863-153">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="1b863-154">Pour améliorer la sécurité, créez un groupe de sécurité réseau (NSG) et l’associer à sous-réseau hello où vous avez activé les Services de domaine Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b863-154">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="1b863-155">Hello tableau suivant illustre un exemple de groupe de sécurité réseau que vous pouvez configurer, toolock vers le bas un accès LDAP sécurisé sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="1b863-155">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="1b863-156">Hello NSG contient un ensemble de règles qui autorisent l’accès LDAPS entrant sur le port TCP 636 uniquement à partir d’un ensemble spécifique d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="1b863-156">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="1b863-157">Hello par défaut 'DenyAll' règle s’applique tooall reste du trafic entrant de hello internet.</span><span class="sxs-lookup"><span data-stu-id="1b863-157">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="1b863-158">Hello NSG règle tooallow LDAPS d’accès sur hello internet à partir d’adresses IP spécifiées a une priorité supérieure à la règle de DenyAll NSG de hello.</span><span class="sxs-lookup"><span data-stu-id="1b863-158">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Exemple NSG toosecure LDAPS d’accès sur hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="1b863-160">**Plus d’informations** - [Groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="1b863-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="1b863-161">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="1b863-161">Related content</span></span>
* [<span data-ttu-id="1b863-162">Services de domaine Azure AD : guide de prise en main</span><span class="sxs-lookup"><span data-stu-id="1b863-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="1b863-163">Administrer un domaine géré par les services de domaine Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b863-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="1b863-164">Gérer la stratégie de groupe sur un domaine géré par les services de domaine Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b863-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="1b863-165">Groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="1b863-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="1b863-166">Créer des groupes de sécurité réseau à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1b863-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
