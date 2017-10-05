---
title: "Gestion d’un compte Azure Automation | Microsoft Docs"
description: "Cet article décrit comment gérer la configuration de votre compte Automation, telle que le renouvellement du certificat, la suppression et une configuration incorrecte."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 41efdbcacede74bac038342688362ff480cadc7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="9a2c2-103">Gestion d’un compte Azure Automation</span><span class="sxs-lookup"><span data-stu-id="9a2c2-103">Manage Azure Automation account</span></span>
<span data-ttu-id="9a2c2-104">Avant que votre compte Automation n’expire, vous devez renouveler le certificat.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-104">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="9a2c2-105">Si vous pensez que le compte d’identification a été compromis, vous pouvez le supprimer et le recréer.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-105">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="9a2c2-106">Cette section décrit comment effectuer ces opérations.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-106">This section discusses how to perform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="9a2c2-107">Renouvellement de certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="9a2c2-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="9a2c2-108">Le certificat auto-signé que vous avez créé pour le compte d’identification expire 1 an après la date de création.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-108">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="9a2c2-109">Vous pouvez le renouveler à tout moment avant qu’il n’expire.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="9a2c2-110">Lorsque vous le renouvelez, le certificat valide en cours est conservé afin de garantir que les Runbooks en file d’attente ou en cours d’exécution, qui s’authentifient avec le compte d’identification, ne sont pas affectés.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-110">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="9a2c2-111">Le certificat reste valide jusqu’à sa date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-111">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="9a2c2-112">Si vous avez configuré votre compte d’identification Automation pour utiliser un certificat émis par votre autorité de certification d’entreprise et que vous utilisez cette option, ce certificat sera remplacé par un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-112">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="9a2c2-113">Pour renouveler le certificat, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9a2c2-113">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="9a2c2-114">Dans le portail Azure, ouvrez le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-114">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="9a2c2-115">Dans le panneau **Compte Automation**, dans le volet **Propriétés du compte**, sous **Paramètres du compte**, sélectionnez **Comptes d’identification**.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-115">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Panneau des propriétés du compte Automation](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="9a2c2-117">Dans le panneau des propriétés des **Comptes d’identification**, sélectionnez le compte d’identification standard ou le compte d’identification Classic pour lequel vous souhaitez renouveler le certificat.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-117">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="9a2c2-118">Sur le panneau **Propriétés** du compte sélectionné, cliquez sur **Renouveler le certificat**.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-118">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Renouveler le certificat pour le compte d’identification](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="9a2c2-120">Pour suivre la progression du renouvellement du certificat, accédez à l’onglet **Notifications** du menu.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-120">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="9a2c2-121">Supprimer un compte d’identification standard ou Classic</span><span class="sxs-lookup"><span data-stu-id="9a2c2-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="9a2c2-122">Cette section décrit comment supprimer et recréer votre compte d’identification standard ou Classic.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-122">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="9a2c2-123">Lorsque vous effectuez cette opération, le compte Automation est conservé.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-123">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="9a2c2-124">Après avoir supprimé le compte d’identification standard ou le compte d’identification Classic, vous pouvez le recréer dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-124">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="9a2c2-125">Dans le portail Azure, ouvrez le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-125">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="9a2c2-126">Dans le panneau **Compte Automation**, dans le volet des propriétés du compte, sélectionnez **Comptes d’identification**.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-126">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="9a2c2-127">Dans le panneau des propriétés des **Comptes d’identification**, sélectionnez le compte d’identification standard ou le compte d’identification Classic que vous voulez supprimer.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-127">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="9a2c2-128">Ensuite, dans le panneau **Propriétés** du compte sélectionné, cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-128">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Supprimer un compte d’identification](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="9a2c2-130">Pour suivre la progression de la suppression du compte, accédez à l’onglet **Notifications** du menu.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-130">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="9a2c2-131">Une fois le compte supprimé, vous pouvez le recréer sur le panneau des propriétés **Comptes d’identification** en sélectionnant l’option de création **Compte d’identification Azure**.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-131">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Recréer le compte d’identification Automation](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="9a2c2-133">Configuration incorrecte</span><span class="sxs-lookup"><span data-stu-id="9a2c2-133">Misconfiguration</span></span>
<span data-ttu-id="9a2c2-134">Certains éléments de configuration nécessaires pour que le compte d’identification standard ou le compte d’identification Classic fonctionne correctement ont peut-être été supprimés ou n’ont pas été créés correctement lors de l’installation initiale.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-134">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="9a2c2-135">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9a2c2-135">The items include:</span></span>

* <span data-ttu-id="9a2c2-136">Ressource de certificat</span><span class="sxs-lookup"><span data-stu-id="9a2c2-136">Certificate asset</span></span>
* <span data-ttu-id="9a2c2-137">Ressource de connexion</span><span class="sxs-lookup"><span data-stu-id="9a2c2-137">Connection asset</span></span>
* <span data-ttu-id="9a2c2-138">Compte d’identification supprimé du rôle Contributeur</span><span class="sxs-lookup"><span data-stu-id="9a2c2-138">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="9a2c2-139">Principal du service ou application dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a2c2-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="9a2c2-140">Dans les cas précédents et dans d’autres instances de configuration incorrecte, le compte Automation détecte les modifications et affiche l’état *Incomplet* dans le panneau des propriétés **Comptes d’identification** du compte.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-140">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![État Incomplet pour la configuration du compte d’identification](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="9a2c2-142">Lorsque vous sélectionnez le compte d’identification, le volet **Propriétés** du compte affiche le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="9a2c2-142">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Message d’avertissement Incomplet pour la configuration du compte d’identification](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="9a2c2-144">.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-144">.</span></span>

<span data-ttu-id="9a2c2-145">Vous pouvez rapidement résoudre ces problèmes liés au compte d’identification en supprimant et en recréant le compte.</span><span class="sxs-lookup"><span data-stu-id="9a2c2-145">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a2c2-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9a2c2-146">Next steps</span></span>
* <span data-ttu-id="9a2c2-147">Pour plus d’informations sur les principaux de service, consultez l’article [Objets Principal du service et Application](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="9a2c2-147">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="9a2c2-148">Pour plus d’informations sur le contrôle d’accès en fonction du rôle dans Azure Automation, reportez-vous à l’article [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="9a2c2-148">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="9a2c2-149">Pour plus d’informations sur les certificats et les services Azure, consultez la page [Vue d’ensemble des certificats pour Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="9a2c2-149">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>