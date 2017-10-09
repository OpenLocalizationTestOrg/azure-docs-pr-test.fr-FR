---
title: "aaaConfigure sécurisé LDAP (LDAPS) dans les Services de domaine Active Directory de Azure | Documents Microsoft"
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
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="8f3de-103">Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine managé Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="8f3de-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8f3de-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8f3de-104">Before you begin</span></span>
<span data-ttu-id="8f3de-105">Vérifiez que vous avez effectué [tâche 2 - tooa de certificat LDAP sécurisé exportation hello. Le fichier PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="8f3de-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="8f3de-106">Choisir toouse hello aperçu expérience du portail Azure ou hello toocomplete de portail classique Azure cette tâche.</span><span class="sxs-lookup"><span data-stu-id="8f3de-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="8f3de-107">**Portail Azure (aperçu)**: [Enable secure LDAP à l’aide de hello portail Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="8f3de-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="8f3de-108">**Portail Azure classic**: [Enable secure LDAP à l’aide du portail Azure classic de hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="8f3de-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a><span data-ttu-id="8f3de-109">Tâche 3 : activer LDAP sécurisé pour hello de domaine gérés à l’aide du portail Azure classic de hello</span><span class="sxs-lookup"><span data-stu-id="8f3de-109">Task 3 - enable secure LDAP for hello managed domain using hello classic Azure portal</span></span>
<span data-ttu-id="8f3de-110">tooenable LDAP sécurisé, effectuer hello configuration comme suit :</span><span class="sxs-lookup"><span data-stu-id="8f3de-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="8f3de-111">Accédez toohello  **[portail Azure classic](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="8f3de-111">Navigate toohello **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="8f3de-112">Sélectionnez hello **Active Directory** nœud dans le volet gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="8f3de-112">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="8f3de-113">Sélectionnez le répertoire de hello Azure AD (également désignée tooas « client »), pour lequel vous avez activé les Services de domaine Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f3de-113">Select hello Azure AD directory (also referred tooas 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Sélectionner un annuaire Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="8f3de-115">Cliquez sur hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="8f3de-115">Click hello **Configure** tab.</span></span>

    ![Configurer l’onglet de l’annuaire](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="8f3de-117">Faites défiler vers le bas la section toohello intitulée **services de domaine**.</span><span class="sxs-lookup"><span data-stu-id="8f3de-117">Scroll down toohello section titled **domain services**.</span></span> <span data-ttu-id="8f3de-118">Vous devez voir une option intitulée **LDAP sécurisé (LDAPS)** comme indiqué dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="8f3de-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in hello following screenshot:</span></span>

    ![Section de configuration des services de domaine](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="8f3de-120">Cliquez sur hello **configurer un certificat...**  toobring bouton haut hello **configurer le certificat pour LDAP sécurisé** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8f3de-120">Click hello **Configure certificate ...** button toobring up hello **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Configurer le certificat pour LDAP sécurisé](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="8f3de-122">Cliquez sur les éléments suivants icône de dossier hello **PFX fichier avec certificat** fichier PFX toospecify hello, qui contient le certificat hello vous souhaitez toouse pour toohello d’accès LDAP sécurisé géré de domaine.</span><span class="sxs-lookup"><span data-stu-id="8f3de-122">Click hello folder icon following **PFX FILE WITH CERTIFICATE** toospecify hello PFX file, which contains hello certificate you wish toouse for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="8f3de-123">Également entrer le mot de passe hello spécifié lors de l’exportation du fichier de certificat toohello PFX hello.</span><span class="sxs-lookup"><span data-stu-id="8f3de-123">Also enter hello password you specified when exporting hello certificate toohello PFX file.</span></span> <span data-ttu-id="8f3de-124">Ensuite, cliquez sur hello fait le bouton bas de hello.</span><span class="sxs-lookup"><span data-stu-id="8f3de-124">Then, click hello done button on hello bottom.</span></span>

    ![Spécifier le mot de passe et le fichier PFX pour LDAP sécurisé](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="8f3de-126">Hello **services de domaine** section Hello **configurer** onglet doit obtenir grisée et est Bonjour **en attente...**  état pendant quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="8f3de-126">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="8f3de-127">Pendant cette période, le certificat LDAPS hello est vérifié à l’exactitude et LDAP sécurisé est configuré pour votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="8f3de-127">During this period, hello LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![LDAP sécurisé - État En attente](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="8f3de-129">Il prend environ 10 minutes too15 tooenable LDAP sécurisé pour votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="8f3de-129">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="8f3de-130">Si hello fourni de certificat LDAP sécurisé ne correspond pas à hello requis critères, LDAP sécurisé n’est pas activée pour votre annuaire et vous voyez une erreur.</span><span class="sxs-lookup"><span data-stu-id="8f3de-130">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="8f3de-131">Par exemple, nom de domaine hello est incorrect, le certificat de hello a déjà expiré ou va bientôt expire.</span><span class="sxs-lookup"><span data-stu-id="8f3de-131">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="8f3de-132">Lorsque le LDAP sécurisé est activé pour votre domaine géré, hello **en attente...**  message disparaisse.</span><span class="sxs-lookup"><span data-stu-id="8f3de-132">When secure LDAP is successfully enabled for your managed domain, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="8f3de-133">Vous devez voir l’empreinte numérique hello de certificat hello affiché.</span><span class="sxs-lookup"><span data-stu-id="8f3de-133">You should see hello thumbprint of hello certificate displayed.</span></span>

    ![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a><span data-ttu-id="8f3de-135">Tâche 4 - activer l’accès LDAP sécurisé sur hello internet</span><span class="sxs-lookup"><span data-stu-id="8f3de-135">Task 4 - enable secure LDAP access over hello internet</span></span>
<span data-ttu-id="8f3de-136">**Tâches facultatives** : Si vous n’envisagez pas de domaine géré de tooaccess hello à l’aide du protocole LDAPS plus hello internet, ignorez cette étape de configuration.</span><span class="sxs-lookup"><span data-stu-id="8f3de-136">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="8f3de-137">Avant de commencer cette tâche, assurez-vous d’avoir effectué les étapes hello décrites dans [tâche 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="8f3de-137">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="8f3de-138">Vous devez voir une option trop**hello Activer SECURE LDAP accès via INTERNET** Bonjour **services de domaine** section Hello **configurer** page.</span><span class="sxs-lookup"><span data-stu-id="8f3de-138">You should see an option too**ENABLE SECURE LDAP ACCESS OVER hello INTERNET** in hello **domain services** section of hello **Configure** page.</span></span> <span data-ttu-id="8f3de-139">Cette option est définie trop**non** par défaut, car internet access toohello gérée domaine via LDAP sécurisé est désactivée par défaut.</span><span class="sxs-lookup"><span data-stu-id="8f3de-139">This option is set too**NO** by default since internet access toohello managed domain over secure LDAP is disabled by default.</span></span>

    ![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="8f3de-141">Activer/désactiver **hello Activer SECURE LDAP accès via INTERNET** trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="8f3de-141">Toggle **ENABLE SECURE LDAP ACCESS OVER hello INTERNET** too**YES**.</span></span> <span data-ttu-id="8f3de-142">Cliquez sur hello **enregistrer** bouton sur le panneau inférieur hello.</span><span class="sxs-lookup"><span data-stu-id="8f3de-142">Click hello **SAVE** button on hello bottom panel.</span></span>
    <span data-ttu-id="8f3de-143">![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="8f3de-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="8f3de-144">Hello **services de domaine** section Hello **configurer** onglet doit obtenir grisée et est Bonjour **en attente...**  état pendant quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="8f3de-144">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="8f3de-145">Après un certain temps, domaine géré tooyour accès internet via LDAP sécurisé est activé.</span><span class="sxs-lookup"><span data-stu-id="8f3de-145">After some time, internet access tooyour managed domain over secure LDAP is enabled.</span></span>

    ![LDAP sécurisé - État En attente](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="8f3de-147">Il prend environ 10 minutes tooenable accès à internet via LDAP sécurisé à votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="8f3de-147">It takes about 10 minutes tooenable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="8f3de-148">Lorsque vous tooyour d’accès LDAP sécurisé gérés domaine via hello internet est activée avec succès, hello **en attente...**  message disparaisse.</span><span class="sxs-lookup"><span data-stu-id="8f3de-148">When secure LDAP access tooyour managed domain over hello internet is successfully enabled, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="8f3de-149">Vous devez voir des adresses IP externes de hello adresse qui peut être utilisé tooaccess votre annuaire sur LDAPS dans le champ de hello **adresse IP externe pour LDAPS accès**.</span><span class="sxs-lookup"><span data-stu-id="8f3de-149">You should see hello external IP address that can be used tooaccess your directory over LDAPS in hello field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![LDAP sécurisé - Activé](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="8f3de-151">Tâche 5 - configurer DNS tooaccess hello domaine géré à partir de hello internet</span><span class="sxs-lookup"><span data-stu-id="8f3de-151">Task 5 - configure DNS tooaccess hello managed domain from hello internet</span></span>
<span data-ttu-id="8f3de-152">**Tâches facultatives** : Si vous n’envisagez pas de domaine géré de tooaccess hello à l’aide du protocole LDAPS plus hello internet, ignorez cette étape de configuration.</span><span class="sxs-lookup"><span data-stu-id="8f3de-152">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="8f3de-153">Avant de commencer cette tâche, assurez-vous d’avoir effectué les étapes hello décrites dans [tâche 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="8f3de-153">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="8f3de-154">Une fois que vous avez activé l’accès LDAP sécurisé sur internet de hello pour votre domaine géré, vous devez tooupdate DNS afin que les ordinateurs clients peuvent trouver ce domaine géré.</span><span class="sxs-lookup"><span data-stu-id="8f3de-154">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="8f3de-155">Extrémité hello de tâche 4, une adresse IP externe est affichée sur hello **configurer** onglet **adresse IP externe pour LDAPS accès**.</span><span class="sxs-lookup"><span data-stu-id="8f3de-155">At hello end of task 4, an external IP address is displayed on hello **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="8f3de-156">Configurez votre fournisseur DNS externe afin que ce nom DNS de hello Hello géré l’adresse IP externe de domaine (par exemple, ' ldaps.contoso100.com') toothis de points.</span><span class="sxs-lookup"><span data-stu-id="8f3de-156">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="8f3de-157">Dans notre exemple, nous devons hello toocreate suivant l’entrée DNS :</span><span class="sxs-lookup"><span data-stu-id="8f3de-157">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="8f3de-158">C’est tout : vous êtes maintenant toohello tooconnect prêt géré domaine à l’aide de LDAP sécurisé sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="8f3de-158">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="8f3de-159">Souvenez-vous que les ordinateurs clients doivent approuver l’émetteur de hello de hello LDAPS certificat toobe en mesure de tooconnect de correctement toohello gérés à l’aide du protocole LDAPS de domaine.</span><span class="sxs-lookup"><span data-stu-id="8f3de-159">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="8f3de-160">Si vous utilisez une autorité de certification d’entreprise ou d’une autorité de certification approuvée publiquement, il est inutile toodo quoi que ce soit dans la mesure où les ordinateurs clients approuver ces émetteurs de certificats.</span><span class="sxs-lookup"><span data-stu-id="8f3de-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="8f3de-161">Si vous utilisez un certificat auto-signé, vous devez tooinstall hello publique partie hello un certificat auto-signé dans le magasin de certificats approuvés hello sur l’ordinateur client de hello.</span><span class="sxs-lookup"><span data-stu-id="8f3de-161">If you are using a self-signed certificate, you need tooinstall hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="8f3de-162">Verrouillage LDAPS accéder au domaine géré de tooyour sur hello internet</span><span class="sxs-lookup"><span data-stu-id="8f3de-162">Lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="8f3de-163">**Tâches facultatives** : Si vous n’avez pas activé LDAPS domaine géré de toohello accès plus hello internet, ignorez cette étape de configuration.</span><span class="sxs-lookup"><span data-stu-id="8f3de-163">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="8f3de-164">Avant de commencer cette tâche, assurez-vous d’avoir effectué les étapes hello décrites dans [tâche 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="8f3de-164">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="8f3de-165">Exposition de votre domaine géré pour l’accès LDAPS sur hello internet représente une menace pour la sécurité.</span><span class="sxs-lookup"><span data-stu-id="8f3de-165">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="8f3de-166">Bonjour domaine géré est accessible à partir de hello internet au port hello utilisé pour LDAP sécurisé (autrement dit, le port 636).</span><span class="sxs-lookup"><span data-stu-id="8f3de-166">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="8f3de-167">Par conséquent, vous pouvez choisir toorestrict accès toohello géré domaine toospecific connu des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="8f3de-167">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="8f3de-168">Pour améliorer la sécurité, créez un groupe de sécurité réseau (NSG) et l’associer à sous-réseau hello où vous avez activé les Services de domaine Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f3de-168">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="8f3de-169">Hello tableau suivant illustre un exemple de groupe de sécurité réseau que vous pouvez configurer, toolock vers le bas un accès LDAP sécurisé sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="8f3de-169">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="8f3de-170">Hello NSG contient un ensemble de règles qui autorisent l’accès LDAPS entrant sur le port TCP 636 uniquement à partir d’un ensemble spécifique d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="8f3de-170">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="8f3de-171">Hello par défaut 'DenyAll' règle s’applique tooall reste du trafic entrant de hello internet.</span><span class="sxs-lookup"><span data-stu-id="8f3de-171">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="8f3de-172">Hello NSG règle tooallow LDAPS d’accès sur hello internet à partir d’adresses IP spécifiées a une priorité supérieure à la règle de DenyAll NSG de hello.</span><span class="sxs-lookup"><span data-stu-id="8f3de-172">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Exemple NSG toosecure LDAPS d’accès sur hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="8f3de-174">**Plus d’informations** - [Groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="8f3de-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="8f3de-175">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="8f3de-175">Related content</span></span>
* [<span data-ttu-id="8f3de-176">Services de domaine Azure AD : guide de prise en main</span><span class="sxs-lookup"><span data-stu-id="8f3de-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="8f3de-177">Administrer un domaine géré par les services de domaine Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f3de-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="8f3de-178">Gérer la stratégie de groupe sur un domaine géré par les services de domaine Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f3de-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="8f3de-179">Groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="8f3de-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="8f3de-180">Créer des groupes de sécurité réseau à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="8f3de-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
