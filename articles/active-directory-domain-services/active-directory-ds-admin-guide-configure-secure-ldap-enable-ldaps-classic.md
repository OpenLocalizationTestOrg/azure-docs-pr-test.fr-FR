---
title: "Configurer le protocole LDAPS (LDAP sécurisé) dans les services de domaine Azure AD | Microsoft Docs"
description: "Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine géré par les services de domaine Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 3aafe209aad7383cd0610d147b5fdba673023c93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="85b9c-103">Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine managé Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="85b9c-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="85b9c-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="85b9c-104">Before you begin</span></span>
<span data-ttu-id="85b9c-105">Vérifiez que vous avez accompli la [Tâche 2 : Exporter le certificat du protocole LDAP sécurisé vers un fichier .PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="85b9c-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="85b9c-106">Choisissez entre utiliser le portail Azure en préversion ou le portail Azure Classic pour effectuer cette tâche.</span><span class="sxs-lookup"><span data-stu-id="85b9c-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="85b9c-107">**Portail Azure (préversion)** : [Activer LDAP sécurisé à l’aide du portail Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="85b9c-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="85b9c-108">**Portail Azure Classic** : [Activer LDAP sécurisé à l’aide du portail Azure Classic](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="85b9c-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal"></a><span data-ttu-id="85b9c-109">Tâche 3 : Activer LDAP sécurisé pour le domaine managé à l’aide du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="85b9c-109">Task 3 - enable secure LDAP for the managed domain using the classic Azure portal</span></span>
<span data-ttu-id="85b9c-110">Exécutez les étapes de configuration suivantes pour activer le protocole LDAP sécurisé :</span><span class="sxs-lookup"><span data-stu-id="85b9c-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="85b9c-111">Accédez au **[portail Azure Classic](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="85b9c-111">Navigate to the **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="85b9c-112">Sélectionnez le nœud **Active Directory** dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="85b9c-112">Select the **Active Directory** node on the left pane.</span></span>
3. <span data-ttu-id="85b9c-113">Sélectionnez le répertoire Azure AD (également appelé « client ») pour lequel vous avez activé les services de domaine Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="85b9c-113">Select the Azure AD directory (also referred to as 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Sélectionner un annuaire Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="85b9c-115">Cliquez sur l'onglet **Configurer** .</span><span class="sxs-lookup"><span data-stu-id="85b9c-115">Click the **Configure** tab.</span></span>

    ![Configurer l’onglet de l’annuaire](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="85b9c-117">Faites défiler la page jusqu’à la section relative aux **services de domaine**.</span><span class="sxs-lookup"><span data-stu-id="85b9c-117">Scroll down to the section titled **domain services**.</span></span> <span data-ttu-id="85b9c-118">L’option **LDAP sécurisé (LDAPS)** doit s’afficher comme illustré dans la capture d’écran ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="85b9c-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in the following screenshot:</span></span>

    ![Section de configuration des services de domaine](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="85b9c-120">Cliquez sur le bouton **Configurer le certificat...** pour ouvrir la boîte de dialogue **Configurer le certificat pour LDAP sécurisé**.</span><span class="sxs-lookup"><span data-stu-id="85b9c-120">Click the **Configure certificate ...** button to bring up the **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Configurer le certificat pour LDAP sécurisé](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="85b9c-122">Cliquez sur l’icône du dossier située après **Fichier PFX avec certificat** pour spécifier le fichier PFX contenant le certificat que vous souhaitez utiliser pour l’accès LDAP sécurisé au domaine managé.</span><span class="sxs-lookup"><span data-stu-id="85b9c-122">Click the folder icon following **PFX FILE WITH CERTIFICATE** to specify the PFX file, which contains the certificate you wish to use for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="85b9c-123">Indiquez également le mot de passe spécifié lors de l’exportation du certificat vers le fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="85b9c-123">Also enter the password you specified when exporting the certificate to the PFX file.</span></span> <span data-ttu-id="85b9c-124">Puis, cliquez sur le bouton Terminé, au bas de la page.</span><span class="sxs-lookup"><span data-stu-id="85b9c-124">Then, click the done button on the bottom.</span></span>

    ![Spécifier le mot de passe et le fichier PFX pour LDAP sécurisé](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="85b9c-126">La section **Services de domaine** de l’onglet **Configurer** doit être grisée ; elle reste à l’état **En attente...** pendant quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="85b9c-126">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="85b9c-127">Pendant cette période, l’exactitude du certificat LDAP sécurisé est vérifiée et le protocole LDAP sécurisé est configuré pour votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="85b9c-127">During this period, the LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![LDAP sécurisé - État En attente](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="85b9c-129">L’activation du protocole LDAP sécurisé pour votre domaine géré dure 10 à 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="85b9c-129">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="85b9c-130">Si le certificat LDAP sécurisé fourni ne correspond pas aux critères requis, le protocole LDAP sécurisé n’est pas activé pour votre annuaire et une erreur s’affiche.</span><span class="sxs-lookup"><span data-stu-id="85b9c-130">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="85b9c-131">Par exemple, le nom de domaine est incorrect, le certificat a expiré ou arrivera bientôt à expiration.</span><span class="sxs-lookup"><span data-stu-id="85b9c-131">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="85b9c-132">Lorsque le protocole LDAP sécurisé est activé pour votre domaine géré, le message **En attente...** doit disparaître.</span><span class="sxs-lookup"><span data-stu-id="85b9c-132">When secure LDAP is successfully enabled for your managed domain, the **Pending...** message should disappear.</span></span> <span data-ttu-id="85b9c-133">Le Thumbprint du certificat doit être affiché.</span><span class="sxs-lookup"><span data-stu-id="85b9c-133">You should see the thumbprint of the certificate displayed.</span></span>

    ![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-the-internet"></a><span data-ttu-id="85b9c-135">Tâche 4 : Activer l’accès LDAP sécurisé via Internet</span><span class="sxs-lookup"><span data-stu-id="85b9c-135">Task 4 - enable secure LDAP access over the internet</span></span>
<span data-ttu-id="85b9c-136">**Tâche facultative** : ignorez cette étape de configuration si vous n’envisagez pas d’accéder au domaine géré via le protocole LDAP sécurisé sur Internet.</span><span class="sxs-lookup"><span data-stu-id="85b9c-136">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="85b9c-137">Avant de commencer cette tâche, vérifiez que vous avez effectué les étapes décrites dans la [Tâche 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="85b9c-137">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="85b9c-138">Vous devez voir apparaître une option **ACTIVER L’ACCÈS LDAP SÉCURISÉ SUR INTERNET** dans la section **Services de domaine** de la page **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="85b9c-138">You should see an option to **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** in the **domain services** section of the **Configure** page.</span></span> <span data-ttu-id="85b9c-139">Cette option est définie sur **NON** par défaut, car l’accès Internet au domaine géré via LDAP sécurisé est désactivé par défaut.</span><span class="sxs-lookup"><span data-stu-id="85b9c-139">This option is set to **NO** by default since internet access to the managed domain over secure LDAP is disabled by default.</span></span>

    ![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="85b9c-141">Affectez à l’option **ACTIVER L’ACCÈS LDAP SÉCURISÉ SUR INTERNET** la valeur **OUI**.</span><span class="sxs-lookup"><span data-stu-id="85b9c-141">Toggle **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** to **YES**.</span></span> <span data-ttu-id="85b9c-142">Cliquez sur le bouton **ENREGISTRER** situé sur le panneau inférieur.</span><span class="sxs-lookup"><span data-stu-id="85b9c-142">Click the **SAVE** button on the bottom panel.</span></span>
    <span data-ttu-id="85b9c-143">![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="85b9c-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="85b9c-144">La section **Services de domaine** de l’onglet **Configurer** doit être grisée ; elle reste à l’état **En attente...** pendant quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="85b9c-144">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="85b9c-145">Après un laps de temps, l’accès Internet à votre domaine géré via LDAP sécurisé est activé.</span><span class="sxs-lookup"><span data-stu-id="85b9c-145">After some time, internet access to your managed domain over secure LDAP is enabled.</span></span>

    ![LDAP sécurisé - État En attente](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="85b9c-147">L’activation de l’accès Internet via le protocole LDAP sécurisé pour votre domaine géré dure 10 minutes environ.</span><span class="sxs-lookup"><span data-stu-id="85b9c-147">It takes about 10 minutes to enable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="85b9c-148">Lorsque l’accès LDAP sécurisé à votre domaine géré via Internet est activé, le message **En attente...** doit disparaître.</span><span class="sxs-lookup"><span data-stu-id="85b9c-148">When secure LDAP access to your managed domain over the internet is successfully enabled, the **Pending...** message should disappear.</span></span> <span data-ttu-id="85b9c-149">Vous devez voir l’adresse IP externe qui peut être utilisée pour accéder à votre répertoire par l’intermédiaire du protocole LDAP sécurisé dans le champ **ADRESSE IP EXTERNE POUR L’ACCÈS LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="85b9c-149">You should see the external IP address that can be used to access your directory over LDAPS in the field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="85b9c-151">Tâche 5 : Configurer DNS pour accéder au domaine managé à partir d’Internet</span><span class="sxs-lookup"><span data-stu-id="85b9c-151">Task 5 - configure DNS to access the managed domain from the internet</span></span>
<span data-ttu-id="85b9c-152">**Tâche facultative** : ignorez cette étape de configuration si vous n’envisagez pas d’accéder au domaine géré via le protocole LDAP sécurisé sur Internet.</span><span class="sxs-lookup"><span data-stu-id="85b9c-152">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="85b9c-153">Avant de commencer cette tâche, vérifiez que vous avez effectué les étapes décrites dans la [Tâche 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="85b9c-153">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="85b9c-154">Une fois l’accès LDAP sécurisé via Internet activé pour le domaine géré, vous devez mettre à jour DNS, afin que les ordinateurs clients puissent détecter ce domaine.</span><span class="sxs-lookup"><span data-stu-id="85b9c-154">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="85b9c-155">À la fin de la tâche 4, une adresse IP externe est affichée sur l’onglet **Configurer** de la page **ADRESSE IP EXTERNE POUR L’ACCÈS LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="85b9c-155">At the end of task 4, an external IP address is displayed on the **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="85b9c-156">Configurez votre fournisseur DNS externe afin que le nom DNS du domaine géré (par exemple, 'ldaps.contoso100.com') pointe vers cette adresse IP externe.</span><span class="sxs-lookup"><span data-stu-id="85b9c-156">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="85b9c-157">Dans notre exemple, nous devons créer l’entrée DNS suivante :</span><span class="sxs-lookup"><span data-stu-id="85b9c-157">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="85b9c-158">Et voilà, vous êtes maintenant prêt à vous connecter au domaine géré à l’aide du protocole LDAP sécurisé sur Internet.</span><span class="sxs-lookup"><span data-stu-id="85b9c-158">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="85b9c-159">N’oubliez pas que les ordinateurs clients doivent approuver l’émetteur du certificat LDAP sécurisé afin d’être en mesure de se connecter au domaine géré à l’aide du protocole LDAP sécurisé.</span><span class="sxs-lookup"><span data-stu-id="85b9c-159">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="85b9c-160">Si vous utilisez une autorité de certification d’entreprise ou une autorité de certification approuvée publiquement, vous n’avez rien à faire, car les ordinateurs clients approuvent ces émetteurs de certificats.</span><span class="sxs-lookup"><span data-stu-id="85b9c-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="85b9c-161">Si vous utilisez un certificat auto-signé, vous devez installer la partie publique du certificat auto-signé dans le magasin de certificats de confiance sur l’ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="85b9c-161">If you are using a self-signed certificate, you need to install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="85b9c-162">Verrouiller l’accès LDAPS à votre domaine managé via internet</span><span class="sxs-lookup"><span data-stu-id="85b9c-162">Lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="85b9c-163">**Tâche facultative** : si vous n’avez pas activé l’accès LDAPS au domaine managé via internet, ignorez cette étape de configuration.</span><span class="sxs-lookup"><span data-stu-id="85b9c-163">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="85b9c-164">Avant de commencer cette tâche, vérifiez que vous avez effectué les étapes décrites dans la [Tâche 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="85b9c-164">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="85b9c-165">L’exposition de votre domaine managé pour l’accès LDAPS via Internet constitue une menace pour la sécurité.</span><span class="sxs-lookup"><span data-stu-id="85b9c-165">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="85b9c-166">Le domaine managé est accessible à partir d’Internet sur le port utilisé pour le LDAP sécurisé (port 636).</span><span class="sxs-lookup"><span data-stu-id="85b9c-166">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="85b9c-167">Par conséquent, vous pouvez choisir de restreindre l’accès au domaine managé à des adresses IP connues spécifiques.</span><span class="sxs-lookup"><span data-stu-id="85b9c-167">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="85b9c-168">Pour améliorer la sécurité, créez un groupe de sécurité réseau (NSG) et associez-le au réseau virtuel dans lequel est activé Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="85b9c-168">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="85b9c-169">Le tableau suivant illustre un exemple de groupe de sécurité réseau que vous pouvez configurer pour verrouiller l’accès LDAP sécurisé via Internet.</span><span class="sxs-lookup"><span data-stu-id="85b9c-169">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="85b9c-170">Le groupe de sécurité réseau contient un ensemble de règles qui autorisent l’accès LDAPS entrant sur le port TCP 636 uniquement à partir d’un ensemble spécifique d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="85b9c-170">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="85b9c-171">La règle « DenyAll » par défaut s’applique à tout autre trafic entrant en provenance d’internet.</span><span class="sxs-lookup"><span data-stu-id="85b9c-171">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="85b9c-172">La règle de groupe de sécurité réseau pour autoriser l’accès LDAPS via Internet à partir d’adresses IP spécifiées prend le pas sur la règle DenyAll NSG.</span><span class="sxs-lookup"><span data-stu-id="85b9c-172">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![Exemple de groupe de sécurité réseau pour l’accès LDAP sécurisé via internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="85b9c-174">**Plus d’informations** - [Groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="85b9c-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="85b9c-175">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="85b9c-175">Related content</span></span>
* [<span data-ttu-id="85b9c-176">Services de domaine Azure AD : guide de prise en main</span><span class="sxs-lookup"><span data-stu-id="85b9c-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="85b9c-177">Administrer un domaine géré par les services de domaine Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85b9c-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="85b9c-178">Gérer la stratégie de groupe sur un domaine géré par les services de domaine Azure AD</span><span class="sxs-lookup"><span data-stu-id="85b9c-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="85b9c-179">Groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="85b9c-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="85b9c-180">Créer des groupes de sécurité réseau à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="85b9c-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
