---
title: "aaaAzure journal d’intégration avec les journaux d’audit Azure Active Directory | Documents Microsoft"
description: "Découvrez comment tooinstall hello service d’intégration des journaux Azure et intégrer des journaux à partir des journaux d’audit Azure"
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
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="69eb9-103">Intégrer des journaux d’audit Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69eb9-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="69eb9-104">Les événements d’audit Azure Active Directory (Azure AD) vous aident à identifier les actions privilégiées survenues dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="69eb9-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="69eb9-105">Vous pouvez voir hello des types d’événements que vous pouvez suivre en examinant [événements de rapport d’audit Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="69eb9-105">You can see hello types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="69eb9-106">Avant de commencer les étapes hello dans cet article, vous devez passer en revue hello [prise en main](security-azure-log-integration-get-started.md) l’article et il les étapes hello.</span><span class="sxs-lookup"><span data-stu-id="69eb9-106">Before you attempt hello steps in this article, you must review hello [Get started](security-azure-log-integration-get-started.md) article and complete hello steps there.</span></span>

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a><span data-ttu-id="69eb9-107">Azure Active directory de toointegrate suit les journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="69eb9-107">Steps toointegrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="69eb9-108">Ouvrez l’invite de commandes hello et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="69eb9-108">Open hello command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="69eb9-109">Exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="69eb9-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="69eb9-110">Cette commande vous invite à entrer votre nom d’utilisateur Azure.</span><span class="sxs-lookup"><span data-stu-id="69eb9-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="69eb9-111">Hello commande crée ensuite un répertoire Azure Active Directory principal du service dans les clients hello Azure AD qui hébergent hello abonnements Azure dans le hello utilisateur connecté est un administrateur, un coadministrateur ou un propriétaire.</span><span class="sxs-lookup"><span data-stu-id="69eb9-111">hello command then creates an Azure Active Directory service principal in hello Azure AD tenants that host hello Azure subscriptions in which hello logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="69eb9-112">commande Hello échoue si l’utilisateur connecté hello est uniquement un utilisateur invité dans le locataire Azure AD de hello.</span><span class="sxs-lookup"><span data-stu-id="69eb9-112">hello command will fail if hello logged-in user is only a guest user in hello Azure AD tenant.</span></span> <span data-ttu-id="69eb9-113">TooAzure de l’authentification est effectuée via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69eb9-113">Authentication tooAzure is done through Azure AD.</span></span> <span data-ttu-id="69eb9-114">Création d’un principal de service pour l’intégration des journaux Azure crée hello identité Azure AD donné accès tooread à partir d’abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="69eb9-114">Creating a service principal for Azure Log Integration creates hello Azure AD identity that is given access tooread from Azure subscriptions.</span></span>

3. <span data-ttu-id="69eb9-115">Exécutez hello suivant commande tooprovide votre ID de client.</span><span class="sxs-lookup"><span data-stu-id="69eb9-115">Run hello following command tooprovide your tenant ID.</span></span> <span data-ttu-id="69eb9-116">Vous devez toobe des membres de la commande de hello client admin rôle toorun hello.</span><span class="sxs-lookup"><span data-stu-id="69eb9-116">You need toobe member of hello tenant admin role toorun hello command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="69eb9-117">Exemple :</span><span class="sxs-lookup"><span data-stu-id="69eb9-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="69eb9-118">Vérifiez que hello suivant tooconfirm de dossiers qui hello Azure Active Directory JSON les journaux d’audit est créé dans les :</span><span class="sxs-lookup"><span data-stu-id="69eb9-118">Check hello following folders tooconfirm that hello Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="69eb9-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="69eb9-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="69eb9-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="69eb9-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="69eb9-121">Hello vidéo suivante montre les étapes hello abordées dans cet article :</span><span class="sxs-lookup"><span data-stu-id="69eb9-121">hello following video demonstrates hello steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="69eb9-122">Pour obtenir des instructions spécifiques à ajouter des informations de hello dans les fichiers au format JSON hello dans vos informations de sécurité et le système de gestion (SIEM) des événements, contactez votre fournisseur SIEM.</span><span class="sxs-lookup"><span data-stu-id="69eb9-122">For specific instructions on bringing hello information in hello JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="69eb9-123">Aide de la Communauté est disponible via hello [Forum MSDN de Azure journal intégration](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="69eb9-123">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="69eb9-124">Ce forum permettant dans hello Azure journal intégration communautaire toosupport eux avec des questions, des réponses, des conseils et astuces.</span><span class="sxs-lookup"><span data-stu-id="69eb9-124">This forum enables people in hello Azure Log Integration community toosupport each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="69eb9-125">En outre, l’équipe d’intégration du journal Azure hello surveille ce forum et permet la mesure du possible.</span><span class="sxs-lookup"><span data-stu-id="69eb9-125">In addition, hello Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="69eb9-126">Vous pouvez également ouvrir une [demande de support](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="69eb9-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="69eb9-127">Sélectionnez **journal intégration** en tant que service hello pour lequel vous demandez la prise en charge.</span><span class="sxs-lookup"><span data-stu-id="69eb9-127">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69eb9-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="69eb9-128">Next steps</span></span>
<span data-ttu-id="69eb9-129">toolearn en savoir plus sur l’intégration des journaux Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="69eb9-129">toolearn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="69eb9-130">[Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) : cette page du Centre de téléchargement donne plus d’informations, la configuration système requise et les instructions d’installation pour l’intégration des journaux Azure.</span><span class="sxs-lookup"><span data-stu-id="69eb9-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="69eb9-131">[Introduction tooAzure intégration du journal](security-azure-log-integration-overview.md): cet article vous présente tooAzure intégration du journal, ses fonctionnalités clées et comment il fonctionne.</span><span class="sxs-lookup"><span data-stu-id="69eb9-131">[Introduction tooAzure Log Integration](security-azure-log-integration-overview.md): This article introduces you tooAzure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="69eb9-132">[Étapes de configuration du partenaire](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): ce billet de blog montre comment toowork d’intégration du journal Azure tooconfigure avec partenaire solutions Splunk, HP ArcSight et QRadar d’IBM.</span><span class="sxs-lookup"><span data-stu-id="69eb9-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how tooconfigure Azure Log Integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="69eb9-133">[Forum aux questions sur l’intégration des journaux Azure](security-azure-log-integration-faq.md) : cet article répond à des questions sur l’intégration des journaux Azure.</span><span class="sxs-lookup"><span data-stu-id="69eb9-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="69eb9-134">[Intégration des alertes du centre de sécurité avec l’intégration de Azure journal](../security-center/security-center-integrating-alerts-with-log-integration.md): cet article vous explique comment le centre de sécurité toosync des alertes, ainsi que des événements de sécurité d’ordinateur virtuel collectées par Diagnostics Windows Azure et les journaux d’audit Azure, avec votre analytique de journal ou Solution SIEM.</span><span class="sxs-lookup"><span data-stu-id="69eb9-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how toosync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="69eb9-135">[Nouvelles fonctionnalités pour les Diagnostics Azure et Azure des journaux d’audit](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): ce billet de blog vous présente les journaux d’audit tooAzure et autres fonctionnalités qui vous aident à obtenir les opérations hello de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="69eb9-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you tooAzure audit logs and other features that help you gain insights into hello operations of your Azure resources.</span></span>
