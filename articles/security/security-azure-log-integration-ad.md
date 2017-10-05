---
title: "Intégration des journaux Azure aux journaux d’audit Azure Active Directory | Microsoft Docs"
description: "Découvrez comment installer le service d’intégration des journaux Azure et intégrer les journaux à partir des journaux d’audit Azure."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 8a1295cc86057ed72940e774d0bd423d61142e31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="f1e04-103">Intégrer des journaux d’audit Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1e04-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="f1e04-104">Les événements d’audit Azure Active Directory (Azure AD) vous aident à identifier les actions privilégiées survenues dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1e04-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="f1e04-105">Vous pouvez voir les types d’événements que vous pouvez suivre en examinant [les événements du rapport d’audit Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="f1e04-105">You can see the types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f1e04-106">Avant d’effectuer les étapes décrites dans cet article, vous devez lire l’article [Bien démarrer](security-azure-log-integration-get-started.md) et effectuez les étapes qui y sont citées.</span><span class="sxs-lookup"><span data-stu-id="f1e04-106">Before you attempt the steps in this article, you must review the [Get started](security-azure-log-integration-get-started.md) article and complete the steps there.</span></span>

## <a name="steps-to-integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="f1e04-107">Procédure d’intégration des journaux d’audit Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1e04-107">Steps to integrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="f1e04-108">Ouvrez l’invite de commandes et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f1e04-108">Open the command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="f1e04-109">Exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="f1e04-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="f1e04-110">Cette commande vous invite à entrer votre nom d’utilisateur Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e04-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="f1e04-111">La commande crée ensuite un principal du service Azure Active Directory dans les locataires Azure AD qui hébergent les abonnements Azure dans lesquels l’utilisateur connecté est un administrateur, un coadministrateur ou un propriétaire.</span><span class="sxs-lookup"><span data-stu-id="f1e04-111">The command then creates an Azure Active Directory service principal in the Azure AD tenants that host the Azure subscriptions in which the logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="f1e04-112">La commande échoue si l’utilisateur connecté est seulement un utilisateur invité dans le locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1e04-112">The command will fail if the logged-in user is only a guest user in the Azure AD tenant.</span></span> <span data-ttu-id="f1e04-113">L’authentification à Azure s’effectue avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1e04-113">Authentication to Azure is done through Azure AD.</span></span> <span data-ttu-id="f1e04-114">La création d’un principal du service pour l’intégration de journaux Azure crée l’identité Azure AD qui aura un accès en lecture aux abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e04-114">Creating a service principal for Azure Log Integration creates the Azure AD identity that is given access to read from Azure subscriptions.</span></span>

3. <span data-ttu-id="f1e04-115">Exécutez la commande suivante pour fournir votre ID de locataire.</span><span class="sxs-lookup"><span data-stu-id="f1e04-115">Run the following command to provide your tenant ID.</span></span> <span data-ttu-id="f1e04-116">Vous devez être membre du rôle administrateur de locataire pour exécuter la commande.</span><span class="sxs-lookup"><span data-stu-id="f1e04-116">You need to be member of the tenant admin role to run the command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="f1e04-117">Exemple :</span><span class="sxs-lookup"><span data-stu-id="f1e04-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="f1e04-118">Vérifiez les dossiers suivants pour confirmer que les fichiers JSON de journaux d’audit Azure Active Directory y sont créés :</span><span class="sxs-lookup"><span data-stu-id="f1e04-118">Check the following folders to confirm that the Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="f1e04-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="f1e04-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="f1e04-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="f1e04-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="f1e04-121">La vidéo suivante montre les étapes décrites dans cet article :</span><span class="sxs-lookup"><span data-stu-id="f1e04-121">The following video demonstrates the steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="f1e04-122">Pour obtenir des instructions précises sur l’ajout des informations de vos fichiers JSON dans votre système de gestion des événements et des informations de sécurité (SIEM), contactez votre fournisseur SIEM.</span><span class="sxs-lookup"><span data-stu-id="f1e04-122">For specific instructions on bringing the information in the JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="f1e04-123">L’aide de la Communauté est disponible via le [forum MSDN d’intégration des journaux Azure](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="f1e04-123">Community assistance is available through the [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="f1e04-124">Ce forum permet aux membres de la communauté de l’intégration des journaux Azure de s’entraider, grâce à des questions, des réponses, des conseils et des astuces.</span><span class="sxs-lookup"><span data-stu-id="f1e04-124">This forum enables people in the Azure Log Integration community to support each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="f1e04-125">En outre, l’équipe d’intégration des journaux Azure supervise ce forum et apporte son aide quand cela est possible.</span><span class="sxs-lookup"><span data-stu-id="f1e04-125">In addition, the Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="f1e04-126">Vous pouvez également ouvrir une [demande de support](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="f1e04-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="f1e04-127">Pour ce faire, sélectionnez **Intégration du journal** comme service pour lequel vous demandez de l’aide.</span><span class="sxs-lookup"><span data-stu-id="f1e04-127">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1e04-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1e04-128">Next steps</span></span>
<span data-ttu-id="f1e04-129">Pour en savoir plus sur l’intégration des journaux Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="f1e04-129">To learn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="f1e04-130">[Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) : cette page du Centre de téléchargement donne plus d’informations, la configuration système requise et les instructions d’installation pour l’intégration des journaux Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e04-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="f1e04-131">[Introduction à l’intégration de journaux Azure](security-azure-log-integration-overview.md) : cet article présente l’intégration des journaux Azure, ses principales fonctionnalités et son fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="f1e04-131">[Introduction to Azure Log Integration](security-azure-log-integration-overview.md): This article introduces you to Azure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="f1e04-132">[Étapes de configuration de partenaires](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) : ce billet de blog vous montre comment configurer l’intégration des journaux Azure pour travailler avec des solutions de partenaires Splunk, HP ArcSight et IBM QRadar.</span><span class="sxs-lookup"><span data-stu-id="f1e04-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how to configure Azure Log Integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="f1e04-133">[Forum aux questions sur l’intégration des journaux Azure](security-azure-log-integration-faq.md) : cet article répond à des questions sur l’intégration des journaux Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e04-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="f1e04-134">[Intégration des alertes du Security Center avec les journaux Azure](../security-center/security-center-integrating-alerts-with-log-integration.md) : cet article montre comment synchroniser les alertes du Security Center, ainsi que les événements de sécurité des machines virtuelles collectés par Azure Diagnostics et les journaux d’audit Azure dans leur solution SIEM ou Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f1e04-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how to sync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="f1e04-135">[Nouvelles fonctionnalités des diagnostics Azure et des journaux d’Audit Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) : ce billet de blog présente les journaux d’Audit Azure et autres fonctionnalités pour vous permettre de mieux connaître les opérations de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e04-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you to Azure audit logs and other features that help you gain insights into the operations of your Azure resources.</span></span>
