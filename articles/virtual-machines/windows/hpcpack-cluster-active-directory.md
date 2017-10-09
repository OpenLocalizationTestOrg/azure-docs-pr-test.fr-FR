---
title: aaaHPC Pack cluster avec Azure Active Directory | Documents Microsoft
description: "Découvrez comment toointegrate une 2016 de Pack HPC cluster dans Azure avec Azure Active Directory"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="ee894-103">Gérer un cluster HPC Pack dans Azure avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee894-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="ee894-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) prend en charge l’intégration avec [Azure Active Directory](../../active-directory/index.md) (Azure AD) pour les administrateurs qui déploient un cluster HPC Pack dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ee894-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="ee894-105">Suivez les étapes de hello dans cet article pour hello suivant de tâches de niveau élevés :</span><span class="sxs-lookup"><span data-stu-id="ee894-105">Follow hello steps in this article for hello following high level tasks:</span></span> 
* <span data-ttu-id="ee894-106">Intégrer manuellement votre cluster HPC Pack avec votre locataire Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee894-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="ee894-107">Gérer et planifier des travaux dans votre cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="ee894-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="ee894-108">Intégration d’une solution de cluster HPC Pack à Azure AD suit les étapes standard toointegrate autres applications et services.</span><span class="sxs-lookup"><span data-stu-id="ee894-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps toointegrate other applications and services.</span></span> <span data-ttu-id="ee894-109">Cet article suppose que vous êtes familiarisé avec la gestion des utilisateurs de base dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee894-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="ee894-110">Pour plus d’informations et d’arrière-plan, consultez hello [documentation Azure Active Directory](../../active-directory/index.md) et hello suivant la section.</span><span class="sxs-lookup"><span data-stu-id="ee894-110">For more information and background, see hello [Azure Active Directory documentation](../../active-directory/index.md) and hello following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="ee894-111">Avantages de l’intégration</span><span class="sxs-lookup"><span data-stu-id="ee894-111">Benefits of integration</span></span>


<span data-ttu-id="ee894-112">Azure Active Directory (Azure AD) est une architecture mutualisé nuage annuaire et identité de service de gestion qui fournit l’accès de l’authentification unique (SSO) toocloud solutions.</span><span class="sxs-lookup"><span data-stu-id="ee894-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access toocloud solutions.</span></span>

<span data-ttu-id="ee894-113">Intégration d’un cluster HPC Pack avec Azure AD peut vous aider à atteindre hello suivant des objectifs :</span><span class="sxs-lookup"><span data-stu-id="ee894-113">Integration of an HPC Pack cluster with Azure AD can help you achieve hello following goals:</span></span>

* <span data-ttu-id="ee894-114">Supprimez contrôleur de domaine Active Directory hello traditionnel de cluster HPC Pack de hello.</span><span class="sxs-lookup"><span data-stu-id="ee894-114">Remove hello traditional Active Directory domain controller from hello HPC Pack cluster.</span></span> <span data-ttu-id="ee894-115">Cela peut permettre de réduire les coûts de hello de gestion de cluster de hello si cela n’est pas nécessaire pour votre entreprise et des processus de déploiement accélération hello.</span><span class="sxs-lookup"><span data-stu-id="ee894-115">This can help reduce hello costs of maintaining hello cluster if this is not necessary for your business, and speed-up hello deployment process.</span></span>
* <span data-ttu-id="ee894-116">Exploiter hello avantages mis par Azure AD suivants :</span><span class="sxs-lookup"><span data-stu-id="ee894-116">Leverage hello following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="ee894-117">Authentification unique</span><span class="sxs-lookup"><span data-stu-id="ee894-117">Single sign-on</span></span> 
    *   <span data-ttu-id="ee894-118">À l’aide d’une identité Active Directory locale pour un cluster HPC Pack hello dans Azure</span><span class="sxs-lookup"><span data-stu-id="ee894-118">Using a local AD identity for hello HPC Pack cluster in Azure</span></span> 

    ![Environnement Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="ee894-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ee894-120">Prerequisites</span></span>
* <span data-ttu-id="ee894-121">**Cluster HPC Pack 2016 déployé dans des machines virtuelles** : pour connaître les étapes, consultez [Déployer un cluster HPC Pack 2016 dans Azure](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ee894-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="ee894-122">Vous devez le nom DNS hello du nœud principal hello et les informations d’identification de hello d’un administrateur de cluster pour effectuer les étapes hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="ee894-122">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ee894-123">L’intégration d’Azure Active Directory n’est pas prise en charge dans les versions de HPC Pack antérieures au HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="ee894-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="ee894-124">**Ordinateur client** -vous avez besoin d’un Windows ou Windows Server client ordinateur trop exécuter des utilitaires clients HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ee894-124">**Client computer** - You need a Windows or Windows Server client computer too run HPC Pack client utilities.</span></span> <span data-ttu-id="ee894-125">Si vous souhaitez uniquement le portail web de toouse hello HPC Pack ou les travaux de toosubmit d’API REST, vous pouvez utiliser n’importe quel ordinateur client de votre choix.</span><span class="sxs-lookup"><span data-stu-id="ee894-125">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="ee894-126">**Utilitaires clients HPC Pack** -installer les utilitaires clients HPC Pack hello sur l’ordinateur client de hello, à l’aide du package d’installation gratuit hello disponible à partir de hello Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="ee894-126">**HPC Pack client utilities** - Install hello HPC Pack client utilities on hello client computer, using hello free installation package available from hello Microsoft Download Center.</span></span>


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="ee894-127">Étape 1 : Inscrire un serveur de cluster HPC hello avec votre client Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee894-127">Step 1: Register hello HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="ee894-128">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ee894-128">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ee894-129">Cliquez sur **Active Directory** dans hello du menu de gauche, puis cliquez sur répertoire hello dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="ee894-129">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="ee894-130">Vous devez disposer de ressources de tooaccess d’autorisation dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="ee894-130">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="ee894-131">Cliquez sur **Utilisateurs** et vérifiez que des comptes utilisateur ont déjà été créés ou configurés.</span><span class="sxs-lookup"><span data-stu-id="ee894-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="ee894-132">Cliquez sur **Applications** > **Ajouter**, puis cliquez sur **Ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="ee894-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="ee894-133">Entrez hello informations dans l’Assistant de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="ee894-133">Enter hello following information in hello wizard:</span></span>
    * <span data-ttu-id="ee894-134">**Nom** : HPCPackClusterServer.</span><span class="sxs-lookup"><span data-stu-id="ee894-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="ee894-135">**Type** : sélectionnez **Application web et/ou API web**.</span><span class="sxs-lookup"><span data-stu-id="ee894-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="ee894-136">**URL de l’authentification**hello - URL de base pour l’exemple hello, qui est par défaut`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="ee894-136">**Sign-on URL**- hello base URL for hello sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="ee894-137">**URI ID d’application** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="ee894-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="ee894-138">Remplacez `<Directory_name`> avec le nom complet de votre client Azure AD, par exemple, de hello `hpclocal.onmicrosoft.com`et remplacez `<application_name>` avec hello nom vous avez choisi précédemment.</span><span class="sxs-lookup"><span data-stu-id="ee894-138">Replace `<Directory_name`> with hello full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with hello name you chose previously.</span></span>

5. <span data-ttu-id="ee894-139">Une fois l’application hello est ajoutée, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="ee894-139">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="ee894-140">Configurer les propriétés suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="ee894-140">Configure hello following properties:</span></span>
    * <span data-ttu-id="ee894-141">Sélectionnez **Oui** pour **Application mutualisée**.</span><span class="sxs-lookup"><span data-stu-id="ee894-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="ee894-142">Sélectionnez **Oui** pour **utilisateur attribution obligatoire tooaccess application**.</span><span class="sxs-lookup"><span data-stu-id="ee894-142">Select **Yes** for **User assignment required tooaccess app**.</span></span>

6. <span data-ttu-id="ee894-143">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ee894-143">Click **Save**.</span></span> <span data-ttu-id="ee894-144">Une fois l’enregistrement terminé, cliquez sur **Gérer le manifeste**.</span><span class="sxs-lookup"><span data-stu-id="ee894-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="ee894-145">Cette action permet de télécharger le fichier JSON du manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="ee894-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="ee894-146">Manifeste de hello téléchargé modifier en recherchant hello `appRoles` définition et l’ajout de hello suivant le rôle d’application :</span><span class="sxs-lookup"><span data-stu-id="ee894-146">Edit hello downloaded manifest by locating hello `appRoles` setting and adding hello following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="ee894-147">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="ee894-147">Save hello file.</span></span> <span data-ttu-id="ee894-148">Puis, dans le portail hello, cliquez sur **gérer manifeste** > **télécharger le manifeste**.</span><span class="sxs-lookup"><span data-stu-id="ee894-148">Then in hello portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="ee894-149">Vous pouvez ensuite télécharger le manifeste de hello modifié.</span><span class="sxs-lookup"><span data-stu-id="ee894-149">You can then upload hello edited manifest.</span></span>
8. <span data-ttu-id="ee894-150">Cliquez sur **Utilisateurs**, sélectionnez un utilisateur, puis cliquez sur **Affecter**.</span><span class="sxs-lookup"><span data-stu-id="ee894-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="ee894-151">Attribuez l’un des utilisateurs toohello hello rôles disponibles (HpcUsers ou HpcAdminMirror).</span><span class="sxs-lookup"><span data-stu-id="ee894-151">Assign one of hello available roles (HpcUsers or HpcAdminMirror) toohello user.</span></span> <span data-ttu-id="ee894-152">Répétez cette étape avec des utilisateurs supplémentaires dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="ee894-152">Repeat this step with additional users in hello directory.</span></span> <span data-ttu-id="ee894-153">Pour plus d’informations générales sur les utilisateurs de cluster, consultez [Gestion des utilisateurs de clusters](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="ee894-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="ee894-154">les utilisateurs toomanage, nous recommandons d’utiliser le panneau d’aperçu hello Azure Active Directory Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee894-154">toomanage users, we recommend using hello Azure Active Directory preview blade in hello [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="ee894-155">Étape 2 : Inscrire un client de cluster HPC hello avec votre client Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee894-155">Step 2: Register hello HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="ee894-156">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ee894-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ee894-157">Cliquez sur **Active Directory** dans hello du menu de gauche, puis cliquez sur répertoire hello dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="ee894-157">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="ee894-158">Vous devez disposer de ressources de tooaccess d’autorisation dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="ee894-158">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="ee894-159">Cliquez sur **Applications** > **Ajouter**, puis cliquez sur **Ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="ee894-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="ee894-160">Entrez hello informations dans l’Assistant de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="ee894-160">Enter hello following information in hello wizard:</span></span>

    * <span data-ttu-id="ee894-161">**Nom** : HPCPackClusterClient.</span><span class="sxs-lookup"><span data-stu-id="ee894-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="ee894-162">**Type** : sélectionnez **Application cliente native**</span><span class="sxs-lookup"><span data-stu-id="ee894-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="ee894-163">**URI de redirection** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="ee894-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="ee894-164">Une fois l’application hello est ajoutée, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="ee894-164">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="ee894-165">Hello de copie **ID Client** valeur et l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="ee894-165">Copy hello **Client ID** value and save it.</span></span> <span data-ttu-id="ee894-166">Vous en aurez besoin plus tard lors de la configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="ee894-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="ee894-167">Dans **autorisations tooother applications**, cliquez sur **ajouter une Application**.</span><span class="sxs-lookup"><span data-stu-id="ee894-167">In **Permissions tooother applications**, click **Add Application**.</span></span> <span data-ttu-id="ee894-168">Rechercher et ajouter une application de HpcPackClusterServer hello (créée à l’étape 1).</span><span class="sxs-lookup"><span data-stu-id="ee894-168">Search and add hello  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="ee894-169">Bonjour **autorisations déléguées** liste déroulante, sélectionnez **accès HpcClusterServer**.</span><span class="sxs-lookup"><span data-stu-id="ee894-169">In hello **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="ee894-170">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ee894-170">Then click **Save**.</span></span>


## <a name="step-3-configure-hello-hpc-cluster"></a><span data-ttu-id="ee894-171">Étape 3 : Configurer le cluster HPC de hello</span><span class="sxs-lookup"><span data-stu-id="ee894-171">Step 3: Configure hello HPC cluster</span></span>

1. <span data-ttu-id="ee894-172">Se connecter toohello HPC Pack 2016 le nœud principal dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ee894-172">Connect toohello HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="ee894-173">Démarrez PowerShell HPC.</span><span class="sxs-lookup"><span data-stu-id="ee894-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="ee894-174">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ee894-174">Run hello following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="ee894-175">où</span><span class="sxs-lookup"><span data-stu-id="ee894-175">where</span></span>

    * <span data-ttu-id="ee894-176">`AADTenant`Spécifie le nom de client Azure AD hello, tel que`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="ee894-176">`AADTenant` specifies hello Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="ee894-177">`AADClientAppId`Spécifie l’ID de client hello pour l’application hello créée à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="ee894-177">`AADClientAppId` specifies hello client ID for hello app created in Step 2.</span></span>

4. <span data-ttu-id="ee894-178">Redémarrez le service de HpcSchedulerStateful hello.</span><span class="sxs-lookup"><span data-stu-id="ee894-178">Restart hello HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="ee894-179">Dans un cluster avec plusieurs nœuds principal, vous pouvez exécuter hello suivant de commandes PowerShell de hello du nœud principal tooswitch hello réplica principal pour le service de HpcSchedulerStateful hello :</span><span class="sxs-lookup"><span data-stu-id="ee894-179">In a cluster with multiple head nodes, you can run hello following PowerShell commands on hello head node tooswitch hello primary replica for hello HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a><span data-ttu-id="ee894-180">Étape 4 : Gérer et envoyer des travaux à partir du client de hello</span><span class="sxs-lookup"><span data-stu-id="ee894-180">Step 4: Manage and submit jobs from hello client</span></span>

<span data-ttu-id="ee894-181">tooinstall les utilitaires clients HPC Pack hello sur votre ordinateur, téléchargez les fichiers d’installation de HPC Pack 2016 (installation complète) à partir de hello Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="ee894-181">tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from hello Microsoft Download Center.</span></span> <span data-ttu-id="ee894-182">Lorsque vous commencez l’installation de hello, choisissez option d’installation de hello pour hello **utilitaires clients HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="ee894-182">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="ee894-183">ordinateur client de hello tooprepare, installez-en hello utilisé au cours de [le programme d’installation HPC cluster](hpcpack-2016-cluster.md) sur l’ordinateur client de hello.</span><span class="sxs-lookup"><span data-stu-id="ee894-183">tooprepare hello client computer, install hello certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on hello client computer.</span></span> <span data-ttu-id="ee894-184">Windows standards d’utilisation de certificats gestion procédures tooinstall hello certificat public toohello **certificats-utilisateur actuel** > **autorités de Certification racines de confiance** stocker.</span><span class="sxs-lookup"><span data-stu-id="ee894-184">Use standard Windows certificate management procedures tooinstall hello public certificate toohello **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="ee894-185">Vous pouvez maintenant exécuter des commandes de HPC Pack hello ou utilisez hello HPC Pack travail manager GUI toosubmit et gérer des travaux de cluster à l’aide du compte de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee894-185">You can now run hello HPC Pack commands or use hello HPC Pack Job manager GUI toosubmit and manage cluster jobs by using hello Azure AD account.</span></span> <span data-ttu-id="ee894-186">Pour les options d’envoi de travail, consultez [de cluster HPC d’envoyer des travaux tooan HPC Pack dans Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="ee894-186">For job submission options, see [Submit HPC jobs tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="ee894-187">Lorsque vous essayez de cluster HPC Pack toohello de tooconnect dans Azure pour hello première fois, une fenêtre contextuelle s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ee894-187">When you try tooconnect toohello HPC Pack cluster in Azure for hello first time, a popup windows appears.</span></span> <span data-ttu-id="ee894-188">Entrez votre toolog d’informations d’identification Azure AD dans.</span><span class="sxs-lookup"><span data-stu-id="ee894-188">Enter your Azure AD credentials toolog in.</span></span> <span data-ttu-id="ee894-189">jeton de Hello est ensuite mis en cache.</span><span class="sxs-lookup"><span data-stu-id="ee894-189">hello token is then cached.</span></span> <span data-ttu-id="ee894-190">Ultérieur cluster toohello de connexions dans Azure utilisation hello mis en cache le jeton, sauf si des modifications de l’authentification ou hello mis en cache est désactivé.</span><span class="sxs-lookup"><span data-stu-id="ee894-190">Later connections toohello cluster in Azure use hello cached token unless authentication changes or hello cached is cleared.</span></span>
>
  
<span data-ttu-id="ee894-191">Par exemple, après avoir effectué les étapes précédentes hello, vous pouvez interroger pour les travaux à partir d’un client local comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee894-191">For example, after completing hello previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="ee894-192">Applets de commande utiles pour l’envoi de travaux avec l’intégration Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee894-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-hello-local-token-cache"></a><span data-ttu-id="ee894-193">Gérer le cache de jetons local hello</span><span class="sxs-lookup"><span data-stu-id="ee894-193">Manage hello local token cache</span></span>

<span data-ttu-id="ee894-194">HPC Pack 2016 fournit deux nouvelles applets de commande PowerShell HPC toomanage hello local du cache de jetons.</span><span class="sxs-lookup"><span data-stu-id="ee894-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets toomanage hello local token cache.</span></span> <span data-ttu-id="ee894-195">Ces applets de commande sont utiles pour envoyer des travaux en mode non interactif.</span><span class="sxs-lookup"><span data-stu-id="ee894-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="ee894-196">Consultez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ee894-196">See hello following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a><span data-ttu-id="ee894-197">Définir les informations d’identification hello pour soumettre des tâches à l’aide du compte de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee894-197">Set hello credentials for submitting jobs using hello Azure AD account</span></span> 

<span data-ttu-id="ee894-198">Vous pouvez être amené travail hello toorun utilisateur de cluster HPC hello (pour un cluster HPC appartenant au domaine, exécuter en tant qu’un utilisateur de domaine, pour un cluster HPC non joints au domaine, exécuter en tant qu’un utilisateur local sur le nœud principal de hello).</span><span class="sxs-lookup"><span data-stu-id="ee894-198">Sometimes, you may want toorun hello job under hello HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on hello head node).</span></span>

1. <span data-ttu-id="ee894-199">Utilisez hello suit les informations d’identification de commandes tooset hello :</span><span class="sxs-lookup"><span data-stu-id="ee894-199">Use hello following commands tooset hello credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="ee894-200">Puis soumettez le travail de hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="ee894-200">Then submit hello job as follows.</span></span> <span data-ttu-id="ee894-201">tâche du Hello s’exécute sous $localUser sur les nœuds de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="ee894-201">hello job/task runs under $localUser on hello compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="ee894-202">Si `–Credential` n’est pas spécifié avec `Submit-HpcJob`, hello tâche s’exécute sous un utilisateur mappé local comme hello compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee894-202">If `–Credential` is not specified with `Submit-HpcJob`, hello job or task runs under a local mapped user as hello Azure AD account.</span></span> <span data-ttu-id="ee894-203">(cluster HPC de hello crée un utilisateur local avec hello comme hello tâche hello de Azure AD compte toorun du même nom.)</span><span class="sxs-lookup"><span data-stu-id="ee894-203">(hello HPC cluster creates a local user with hello same name as hello Azure AD account toorun hello task.)</span></span>
    
3. <span data-ttu-id="ee894-204">Définir les données étendues pour hello compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee894-204">Set extended data for hello Azure AD account.</span></span> <span data-ttu-id="ee894-205">Cela est utile lors de l’exécution d’un travail MPI sur des nœuds Linux à l’aide du compte de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee894-205">This is useful when running an MPI job on Linux nodes using hello Azure AD account.</span></span>

   * <span data-ttu-id="ee894-206">Définir les données étendues pour hello compte Azure AD elle-même</span><span class="sxs-lookup"><span data-stu-id="ee894-206">Set extended data for hello Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="ee894-207">Définir les données étendues et exécuter en tant qu’utilisateur du cluster HPC</span><span class="sxs-lookup"><span data-stu-id="ee894-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

