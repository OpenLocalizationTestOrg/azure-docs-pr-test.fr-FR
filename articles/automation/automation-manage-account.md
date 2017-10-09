---
title: aaaManage compte Azure Automation | Documents Microsoft
description: "Cet article décrit comment toomanage hello configuration de votre compte Automation, telles que le renouvellement de certificat, la suppression et une configuration incorrecte."
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
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="f4857-103">Gestion d’un compte Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f4857-103">Manage Azure Automation account</span></span>
<span data-ttu-id="f4857-104">À un moment donné avant l’expiration de votre compte Automation, vous devez le certificat de hello toorenew.</span><span class="sxs-lookup"><span data-stu-id="f4857-104">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="f4857-105">Si vous pensez que ce compte d’identification hello a été compromise, vous pouvez supprimer et recréer.</span><span class="sxs-lookup"><span data-stu-id="f4857-105">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="f4857-106">Cette section explique comment tooperform ces opérations.</span><span class="sxs-lookup"><span data-stu-id="f4857-106">This section discusses how tooperform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="f4857-107">Renouvellement de certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="f4857-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="f4857-108">Hello un certificat auto-signé que vous avez créé pour hello exécuter en tant que compte expire un an à partir de la date de hello de création.</span><span class="sxs-lookup"><span data-stu-id="f4857-108">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="f4857-109">Vous pouvez le renouveler à tout moment avant qu’il n’expire.</span><span class="sxs-lookup"><span data-stu-id="f4857-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="f4857-110">Lors du renouvellement, il certificat valide de hello actuelle est retenue tooensure que les runbooks qui sont en attente jusqu'à ou activement en cours d’exécution, et qui s’authentifient avec hello compte d’identification, ne sont pas affectés négativement.</span><span class="sxs-lookup"><span data-stu-id="f4857-110">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="f4857-111">certificat de Hello reste valide jusqu'à ce que sa date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="f4857-111">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="f4857-112">Si vous avez configuré votre toouse de compte Automation s’exécuter en tant qu’un certificat émis par votre autorité de certification d’entreprise et que vous utilisez cette option, le certificat d’entreprise hello est remplacé par un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="f4857-112">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="f4857-113">toorenew hello certificat, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f4857-113">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="f4857-114">Bonjour portail Azure, ouvrez le compte Automation de hello.</span><span class="sxs-lookup"><span data-stu-id="f4857-114">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="f4857-115">Sur hello **compte Automation** panneau, Bonjour **compte propriétés** volet, sous **les paramètres de compte**, sélectionnez **exécuter en tant que comptes**.</span><span class="sxs-lookup"><span data-stu-id="f4857-115">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Panneau des propriétés du compte Automation](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="f4857-117">Sur hello **comptes d’identification** panneau des propriétés, sélectionnez soit hello d’identification de compte ou hello classique exécuter en tant que compte de certificat de hello toorenew pour.</span><span class="sxs-lookup"><span data-stu-id="f4857-117">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="f4857-118">Sur hello **propriétés** panneau pourquoi le compte sélectionné, cliquez sur **renouveler certificat**.</span><span class="sxs-lookup"><span data-stu-id="f4857-118">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Renouveler le certificat pour le compte d’identification](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="f4857-120">Pendant le renouvellement de certificat de hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="f4857-120">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="f4857-121">Supprimer un compte d’identification standard ou Classic</span><span class="sxs-lookup"><span data-stu-id="f4857-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="f4857-122">Cette section décrit comment toodelete et recréer un compte d’identification ou classique exécuter en tant que.</span><span class="sxs-lookup"><span data-stu-id="f4857-122">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="f4857-123">Lorsque vous effectuez cette action, hello compte Automation est conservée.</span><span class="sxs-lookup"><span data-stu-id="f4857-123">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="f4857-124">Après avoir supprimé un compte d’identification ou classique exécuter en tant que, vous pouvez le recréer dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f4857-124">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="f4857-125">Bonjour portail Azure, ouvrez le compte Automation de hello.</span><span class="sxs-lookup"><span data-stu-id="f4857-125">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="f4857-126">Sur hello **compte Automation** lame, hello compte volet Propriétés, sélectionnez **exécuter en tant que comptes**.</span><span class="sxs-lookup"><span data-stu-id="f4857-126">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="f4857-127">Sur hello **comptes d’identification** panneau des propriétés, sélectionnez soit hello d’identification de compte ou classique exécuter en tant que le compte que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="f4857-127">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="f4857-128">Ensuite, sous hello **propriétés** panneau pourquoi le compte sélectionné, cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="f4857-128">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Supprimer un compte d’identification](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="f4857-130">Lors de la suppression du compte de hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="f4857-130">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="f4857-131">Une fois que le compte de hello a été supprimé, vous pouvez recréer il sur hello **comptes d’identification** option de création du panneau des propriétés en sélectionnant hello **exécuter en tant que compte Azure**.</span><span class="sxs-lookup"><span data-stu-id="f4857-131">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Recréez le compte d’identification Automation hello](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="f4857-133">Configuration incorrecte</span><span class="sxs-lookup"><span data-stu-id="f4857-133">Misconfiguration</span></span>
<span data-ttu-id="f4857-134">Certains éléments de configuration nécessaires pour toofunction de compte Exécuter en tant qu’ou classique en hello peuvent correctement ont été supprimés ou créés correctement lors de l’installation initiale.</span><span class="sxs-lookup"><span data-stu-id="f4857-134">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="f4857-135">éléments de Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="f4857-135">hello items include:</span></span>

* <span data-ttu-id="f4857-136">Ressource de certificat</span><span class="sxs-lookup"><span data-stu-id="f4857-136">Certificate asset</span></span>
* <span data-ttu-id="f4857-137">Ressource de connexion</span><span class="sxs-lookup"><span data-stu-id="f4857-137">Connection asset</span></span>
* <span data-ttu-id="f4857-138">Compte d’identification a été supprimé de rôle de collaborateur hello</span><span class="sxs-lookup"><span data-stu-id="f4857-138">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="f4857-139">Principal du service ou application dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4857-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="f4857-140">Hello précédent et les autres instances d’une configuration incorrecte, hello compte Automation détecte hello modifie et affiche l’état *incomplet* sur hello **comptes d’identification** panneau des propriétés pour hello compte.</span><span class="sxs-lookup"><span data-stu-id="f4857-140">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![État Incomplet pour la configuration du compte d’identification](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="f4857-142">Lorsque vous sélectionnez le compte d’identification hello, hello compte **propriétés** volet affiche hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="f4857-142">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Message d’avertissement Incomplet pour la configuration du compte d’identification](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="f4857-144">.</span><span class="sxs-lookup"><span data-stu-id="f4857-144">.</span></span>

<span data-ttu-id="f4857-145">Vous pouvez rapidement résoudre ces problèmes de compte Exécuter en tant qu’à supprimer et recréer le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="f4857-145">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4857-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f4857-146">Next steps</span></span>
* <span data-ttu-id="f4857-147">Pour plus d’informations sur les principaux de Service, voir la rubrique trop[les objets de Principal du Service et Application](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="f4857-147">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="f4857-148">Pour plus d’informations sur le contrôle d’accès basée sur les rôles dans Azure Automation, consultez trop[contrôle d’accès basé sur un rôle dans Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="f4857-148">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="f4857-149">Pour plus d’informations sur les certificats et les services Azure, consultez trop[vue d’ensemble des certificats pour les Services de Cloud Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="f4857-149">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
