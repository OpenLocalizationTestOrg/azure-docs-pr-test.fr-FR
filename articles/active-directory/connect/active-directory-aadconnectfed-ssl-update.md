---
title: "Azure AD Connect : Certificat SSL hello mise à jour pour une batterie de serveurs de Services de fédération Active Directory (AD FS) | Documents Microsoft"
description: "Ce document détails hello étapes tooupdate hello certificat SSL d’une batterie de serveurs AD FS à l’aide d’Azure AD Connect."
services: active-directory
keywords: "azure ad connect, mise à jour de ssl adfs, mise à jour d’un certificat adfs, modifier un certificat adfs, nouveau certificat adfs, certificat adfs, mettre à jour un certificat ssl adf, mettre à jour un certificat adf ssl, configurer un certificat ssl adf, adfs, ssl, certificat, adfs certificat de communication de service, mettre à jour la fédération, configurer la fédération, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="31ba6-104">Mettre à jour le certificat SSL de hello pour une batterie de serveurs de Services de fédération Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="31ba6-104">Update hello SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="31ba6-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="31ba6-105">Overview</span></span>
<span data-ttu-id="31ba6-106">Cet article décrit comment vous pouvez utiliser le certificat SSL de Azure AD Connect tooupdate hello pour une batterie de serveurs de Services de fédération Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="31ba6-106">This article describes how you can use Azure AD Connect tooupdate hello SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="31ba6-107">Vous pouvez utiliser le certificat SSL de hello Azure AD Connect outil tooeasily mise à jour hello pour la batterie de serveurs hello AD FS même si hello utilisateur méthode de connexion sélectionné n’est pas AD FS.</span><span class="sxs-lookup"><span data-stu-id="31ba6-107">You can use hello Azure AD Connect tool tooeasily update hello SSL certificate for hello AD FS farm even if hello user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="31ba6-108">Vous pouvez effectuer hello ensemble de l’opération de mise à jour le certificat SSL pour la batterie de serveurs hello AD FS sur l’ensemble de fédération et de serveurs Web Application Proxy (WAP) en trois étapes simples :</span><span class="sxs-lookup"><span data-stu-id="31ba6-108">You can perform hello whole operation of updating SSL certificate for hello AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Trois étapes](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="31ba6-110">toolearn en savoir plus sur les certificats utilisés par AD FS, consultez [présentation des certificats utilisés par AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="31ba6-110">toolearn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31ba6-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="31ba6-111">Prerequisites</span></span>

* <span data-ttu-id="31ba6-112">**Batterie de serveurs AD FS** : Assurez-vous que votre batterie AD FS est basée sur Windows Server 2012 R2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="31ba6-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="31ba6-113">**Azure AD Connect**: Vérifiez que hello version d’Azure AD Connect est 1.1.443.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="31ba6-113">**Azure AD Connect**: Ensure that hello version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="31ba6-114">Vous allez utiliser la tâche hello **mise à jour AD certificat SSL FS**.</span><span class="sxs-lookup"><span data-stu-id="31ba6-114">You'll use hello task **Update AD FS SSL certificate**.</span></span>

![Mettre à jour la tâche SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="31ba6-116">Étape 1 : Fournir les informations sur la batterie de serveurs AD FS</span><span class="sxs-lookup"><span data-stu-id="31ba6-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="31ba6-117">Azure AD Connect automatiquement par les tentatives tooobtain d’informations sur la batterie de serveurs hello AD FS :</span><span class="sxs-lookup"><span data-stu-id="31ba6-117">Azure AD Connect attempts tooobtain information about hello AD FS farm automatically by:</span></span>
1. <span data-ttu-id="31ba6-118">Interrogation des informations de batterie de serveurs hello d’AD FS (Windows Server 2016 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="31ba6-118">Querying hello farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="31ba6-119">Référence à des informations de hello exécutions précédentes, qui sont stockés en local avec Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="31ba6-119">Referencing hello information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="31ba6-120">Vous pouvez modifier la liste hello des serveurs qui sont affichés en ajoutant ou supprimant hello serveurs tooreflect hello configuration actuelle de la batterie de serveurs hello AD FS.</span><span class="sxs-lookup"><span data-stu-id="31ba6-120">You can modify hello list of servers that are displayed by adding or removing hello servers tooreflect hello current configuration of hello AD FS farm.</span></span> <span data-ttu-id="31ba6-121">Dès que les informations de serveur hello sont fournies, Azure AD Connect affiche la connectivité de hello et l’état actuel du certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="31ba6-121">As soon as hello server information is provided, Azure AD Connect displays hello connectivity and current SSL certificate status.</span></span>

![Informations du serveur AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="31ba6-123">Si la liste de hello contient un serveur qui ne fait plus partie de la batterie de serveurs hello AD FS, cliquez sur **supprimer** serveur hello toodelete liste hello des serveurs dans votre batterie AD FS.</span><span class="sxs-lookup"><span data-stu-id="31ba6-123">If hello list contains a server that's no longer part of hello AD FS farm, click **Remove** toodelete hello server from hello list of servers in your AD FS farm.</span></span>

![Serveur hors connexion dans la liste](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="31ba6-125">Suppression d’un serveur à partir de la liste de hello de serveurs pour un AD FS de batterie de serveurs dans Azure AD Connect est une opération locale et les mises à jour hello concernant hello batterie AD FS qui tient à jour Azure AD Connect localement.</span><span class="sxs-lookup"><span data-stu-id="31ba6-125">Removing a server from hello list of servers for an AD FS farm in Azure AD Connect is a local operation and updates hello information for hello AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="31ba6-126">Azure AD Connect ne modifie pas configuration hello sur AD FS tooreflect hello modification.</span><span class="sxs-lookup"><span data-stu-id="31ba6-126">Azure AD Connect doesn't modify hello configuration on AD FS tooreflect hello change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="31ba6-127">Étape 2 : Fournir un nouveau certificat SSL</span><span class="sxs-lookup"><span data-stu-id="31ba6-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="31ba6-128">Une fois que vous avez confirmé hello plus d’informations sur les serveurs de batterie de serveurs AD FS, Azure AD Connect demande un nouveau certificat SSL de hello.</span><span class="sxs-lookup"><span data-stu-id="31ba6-128">After you've confirmed hello information about AD FS farm servers, Azure AD Connect asks for hello new SSL certificate.</span></span> <span data-ttu-id="31ba6-129">Fournir une installation de hello toocontinue protégé par mot de passe PFX certificat.</span><span class="sxs-lookup"><span data-stu-id="31ba6-129">Provide a password-protected PFX certificate toocontinue hello installation.</span></span>

![Certificat SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="31ba6-131">Une fois que vous fournissez le certificat de hello, Azure AD Connect passe par une série de conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="31ba6-131">After you provide hello certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="31ba6-132">Vérifiez que hello certificat tooensure qui hello certificat est correct pour la batterie de serveurs hello AD FS :</span><span class="sxs-lookup"><span data-stu-id="31ba6-132">Verify hello certificate tooensure that hello certificate is correct for hello AD FS farm:</span></span>

-   <span data-ttu-id="31ba6-133">Bonjour nom d’objet/remplacement du nom de sujet de certificat de hello est même hello en tant que nom de service de fédération hello, ou il s’agit d’un certificat générique.</span><span class="sxs-lookup"><span data-stu-id="31ba6-133">hello subject name/alternate subject name for hello certificate is either hello same as hello federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="31ba6-134">certificat de Hello est valide pendant plus de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="31ba6-134">hello certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="31ba6-135">chaîne d’approbation de certificat Hello est valide.</span><span class="sxs-lookup"><span data-stu-id="31ba6-135">hello certificate trust chain is valid.</span></span>
-   <span data-ttu-id="31ba6-136">certificat de Hello est protégé par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="31ba6-136">hello certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-hello-update"></a><span data-ttu-id="31ba6-137">Étape 3 : Sélectionner des serveurs de mise à jour hello</span><span class="sxs-lookup"><span data-stu-id="31ba6-137">Step 3: Select servers for hello update</span></span>

<span data-ttu-id="31ba6-138">Dans l’étape suivante de hello, sélectionnez les serveurs de hello nécessitant un certificat SSL de toohave hello mis à jour.</span><span class="sxs-lookup"><span data-stu-id="31ba6-138">In hello next step, select hello servers that need toohave hello SSL certificate updated.</span></span> <span data-ttu-id="31ba6-139">Serveurs qui sont hors connexion ne peut pas être sélectionnés pour la mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="31ba6-139">Servers that are offline can't be selected for hello update.</span></span>

![Sélectionnez des serveurs tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="31ba6-141">Après avoir terminé la configuration de hello, Azure AD Connect affiche de message de type hello qui indique l’état de hello de mise à jour hello et fournit une option tooverify hello AD FS connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="31ba6-141">After you complete hello configuration, Azure AD Connect displays hello message that indicates hello status of hello update and provides an option tooverify hello AD FS sign-in.</span></span>

![Configuration terminée](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="31ba6-143">FAQ</span><span class="sxs-lookup"><span data-stu-id="31ba6-143">FAQs</span></span>

* <span data-ttu-id="31ba6-144">**Quelle doit être hello nom du sujet du certificat de hello hello nouveau certificat SSL AD FS ?**</span><span class="sxs-lookup"><span data-stu-id="31ba6-144">**What should be hello subject name of hello certificate for hello new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="31ba6-145">Azure AD Connect vérifie si hello/remplacement du nom du sujet nom du sujet hello certificat contient le nom de service de fédération hello.</span><span class="sxs-lookup"><span data-stu-id="31ba6-145">Azure AD Connect checks if hello subject name/alternate subject name of hello certificate contains hello federation service name.</span></span> <span data-ttu-id="31ba6-146">Par exemple, si le nom de votre service de fédération est fs.contoso.com, nom de l’objet de nom/autre sujet hello doit être fs.contoso.com.  Les certificats à caractères génériques sont également acceptés.</span><span class="sxs-lookup"><span data-stu-id="31ba6-146">For example, if your federation service name is fs.contoso.com, hello subject name/alternate subject name must be fs.contoso.com.  Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="31ba6-147">**Pourquoi suis-je invité pour les informations d’identification à nouveau sur la page du serveur WAP hello ?**</span><span class="sxs-lookup"><span data-stu-id="31ba6-147">**Why am I asked for credentials again on hello WAP server page?**</span></span>

    <span data-ttu-id="31ba6-148">Si les informations d’identification de hello que vous fournissez pour la connexion des serveurs de FS tooAD n’ont également les serveurs de proxy hello privilège toomanage hello, Azure AD Connect vous demande des informations d’identification qui ont des privilèges d’administrateur sur les serveurs de proxy hello.</span><span class="sxs-lookup"><span data-stu-id="31ba6-148">If hello credentials you provide for connecting tooAD FS servers don't also have hello privilege toomanage hello WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on hello WAP servers.</span></span>

* <span data-ttu-id="31ba6-149">**serveur de Hello est affiché en mode hors connexion. Que dois-je faire ?**</span><span class="sxs-lookup"><span data-stu-id="31ba6-149">**hello server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="31ba6-150">Azure AD Connect ne peut pas effectuer une opération si hello serveur est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="31ba6-150">Azure AD Connect can't perform any operation if hello server is offline.</span></span> <span data-ttu-id="31ba6-151">Si le serveur de hello fait partie de hello batterie AD FS, puis vérifiez le serveur de toohello connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="31ba6-151">If hello server is part of hello AD FS farm, then check hello connectivity toohello server.</span></span> <span data-ttu-id="31ba6-152">Une fois que vous avez résolu le problème de hello, appuyez sur hello actualisation icône tooupdate hello de l’état dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="31ba6-152">After you've resolved hello issue, press hello refresh icon tooupdate hello status in hello wizard.</span></span> <span data-ttu-id="31ba6-153">Si le serveur de hello faisait partie de hello batterie précédemment mais maintenant n’existe plus, cliquez sur **supprimer** toodelete tient à jour de liste de hello des serveurs Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="31ba6-153">If hello server was part of hello farm earlier but now no longer exists, click **Remove** toodelete it from hello list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="31ba6-154">Suppression de serveur hello dans liste hello dans Azure AD Connect ne modifie pas hello configuration AD FS lui-même.</span><span class="sxs-lookup"><span data-stu-id="31ba6-154">Removing hello server from hello list in Azure AD Connect doesn't alter hello AD FS configuration itself.</span></span> <span data-ttu-id="31ba6-155">Si vous utilisez AD FS dans Windows Server 2016 ou version ultérieure, reste du serveur hello dans les paramètres de configuration hello et s’affichera à nouveau hello prochaine hello tâche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="31ba6-155">If you're using AD FS in Windows Server 2016 or later, hello server remains in hello configuration settings and will be shown again hello next time hello task is run.</span></span>

* <span data-ttu-id="31ba6-156">**Puis-je mettre à jour un sous-ensemble de mes serveurs de la batterie de serveurs avec le nouveau certificat SSL de hello ?**</span><span class="sxs-lookup"><span data-stu-id="31ba6-156">**Can I update a subset of my farm servers with hello new SSL certificate?**</span></span>

    <span data-ttu-id="31ba6-157">Oui.</span><span class="sxs-lookup"><span data-stu-id="31ba6-157">Yes.</span></span> <span data-ttu-id="31ba6-158">Vous pouvez toujours exécuter la tâche hello **certificat SSL de mise à jour** à nouveau les hello tooupdate serveurs restant.</span><span class="sxs-lookup"><span data-stu-id="31ba6-158">You can always run hello task **Update SSL Certificate** again tooupdate hello remaining servers.</span></span> <span data-ttu-id="31ba6-159">Sur hello **sélectionnez des serveurs SSL de certificats mise à jour** page, vous pouvez trier hello liste des serveurs sur **date d’expiration de SSL** tooeasily accès hello serveurs qui ne sont pas encore mis à jour.</span><span class="sxs-lookup"><span data-stu-id="31ba6-159">On hello **Select servers for SSL certificate update** page, you can sort hello list of servers on **SSL Expiry date** tooeasily access hello servers that aren't updated yet.</span></span>

* <span data-ttu-id="31ba6-160">**J’ai supprimé serveur hello Bonjour précédente exécution, mais il est toujours affiché comme en mode hors connexion et est répertorié sur la page de serveurs ADFS hello AD. Pourquoi est-il toujours les serveur hors connexion hello même après la suppression d’il ?**</span><span class="sxs-lookup"><span data-stu-id="31ba6-160">**I removed hello server in hello previous run, but it's still being shown as offline and listed on hello AD FS Servers page. Why is hello offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="31ba6-161">Suppression de serveur hello dans liste hello dans Azure AD Connect ne supprime Bonjour configuration AD FS.</span><span class="sxs-lookup"><span data-stu-id="31ba6-161">Removing hello server from hello list in Azure AD Connect doesn't remove it in hello AD FS configuration.</span></span> <span data-ttu-id="31ba6-162">Azure AD Connect fait référence à AD FS (Windows Server 2016 ou version ultérieure) pour toutes les informations concernant la batterie de serveurs hello.</span><span class="sxs-lookup"><span data-stu-id="31ba6-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about hello farm.</span></span> <span data-ttu-id="31ba6-163">Si le serveur de hello est toujours présente dans hello configuration AD FS, il sera répertorié dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="31ba6-163">If hello server is still present in hello AD FS configuration, it will be listed back in hello list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="31ba6-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31ba6-164">Next steps</span></span>

- [<span data-ttu-id="31ba6-165">Fédération avec Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="31ba6-165">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="31ba6-166">Gestion des services AD FS (Active Directory Federation Services) et personnalisation avec Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="31ba6-166">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
