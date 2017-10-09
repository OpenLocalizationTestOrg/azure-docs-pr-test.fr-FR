---
title: "rôles de hello aaaConfigure pour Azure cloud service avec Visual Studio | Documents Microsoft"
description: "Découvrez comment tooset installer et configurer des rôles pour les services de cloud computing Azure à l’aide de Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="9e435-103">Configurer des rôles de service cloud Azure avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e435-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="9e435-104">Un service cloud Azure peut avoir un ou plusieurs rôles de travail ou rôles web.</span><span class="sxs-lookup"><span data-stu-id="9e435-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="9e435-105">Pour chaque rôle, vous devez toodefine comment configurer ce rôle et également configurez la façon dont ce rôle s’exécute.</span><span class="sxs-lookup"><span data-stu-id="9e435-105">For each role, you need toodefine how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="9e435-106">toolearn savoir plus sur les rôles dans les services de cloud computing, consultez la vidéo de hello [tooAzure de présentation des Services de cloud computing](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="9e435-106">toolearn more about roles in cloud services, see hello video [Introduction tooAzure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="9e435-107">informations de Hello pour votre service cloud sont stockées dans hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="9e435-107">hello information for your cloud service is stored in hello following files:</span></span>

- <span data-ttu-id="9e435-108">**ServiceDefinition.csdef** -fichier de définition de service hello définit les paramètres d’exécution de hello pour votre service cloud dont les rôles requis, points de terminaison et taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9e435-108">**ServiceDefinition.csdef** - hello service definition file defines hello runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="9e435-109">Aucune des données hello stockées dans `ServiceDefinition.csdef` peut être modifiée lorsque votre rôle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9e435-109">None of hello data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="9e435-110">**ServiceConfiguration.cscfg** - fichier de configuration de service hello configure le nombre d’instances d’un rôle est exécuté et les valeurs des paramètres de hello hello définis pour un rôle.</span><span class="sxs-lookup"><span data-stu-id="9e435-110">**ServiceConfiguration.cscfg** - hello service configuration file configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> <span data-ttu-id="9e435-111">Hello des données stockées dans `ServiceConfiguration.cscfg` peut être modifié pendant l’exécution de votre rôle.</span><span class="sxs-lookup"><span data-stu-id="9e435-111">hello data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="9e435-112">toostore différentes valeurs pour les paramètres de hello, qui contrôle comment un rôle s’exécute, vous pouvez définir plusieurs configurations de service.</span><span class="sxs-lookup"><span data-stu-id="9e435-112">toostore different values for hello settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="9e435-113">Vous pouvez utiliser une configuration de service différente pour chaque environnement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9e435-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="9e435-114">Par exemple, vous pouvez définir votre compte connexion chaîne toouse hello local de stockage Azure l’émulateur de stockage dans une configuration de service local et créer un autre service de configuration toouse le stockage Azure dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-114">For example, you can set your storage account connection string toouse hello local Azure storage emulator in a local service configuration and create another service configuration toouse Azure storage in hello cloud.</span></span>

<span data-ttu-id="9e435-115">Lorsque vous créez un service cloud Azure dans Visual Studio, deux configurations de service sont automatiquement créées et ajoutés tooyour projet Windows Azure :</span><span class="sxs-lookup"><span data-stu-id="9e435-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added tooyour Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="9e435-116">Configurer un service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="9e435-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="9e435-117">Vous pouvez configurer un service cloud Azure à partir de l’Explorateur de solutions dans Visual Studio, comme indiqué dans hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9e435-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in hello following steps:</span></span>

1. <span data-ttu-id="9e435-118">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e435-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="9e435-119">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello et, dans le menu contextuel de hello, sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="9e435-119">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
    ![Menu contextuel de projet dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="9e435-121">Dans la page de propriétés du projet hello, sélectionnez hello **développement** onglet.</span><span class="sxs-lookup"><span data-stu-id="9e435-121">In hello project's properties page, select hello **Development** tab.</span></span> 

    ![Page de propriétés du projet : onglet développement](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="9e435-123">Bonjour **Configuration du Service** liste, le nom hello select de configuration du service que vous souhaitez tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-123">In hello **Service Configuration** list, select hello name of hello service configuration that you want tooedit.</span></span> <span data-ttu-id="9e435-124">(Si vous souhaitez toomake modifie les configurations de service tooall hello pour ce rôle, sélectionnez **toutes les Configurations**.)</span><span class="sxs-lookup"><span data-stu-id="9e435-124">(If you want toomake changes tooall hello service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="9e435-125">Si vous choisissez une configuration de service spécifique, certaines propriétés sont désactivées parce qu’elles peuvent être définies uniquement pour toutes les configurations.</span><span class="sxs-lookup"><span data-stu-id="9e435-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="9e435-126">tooedit ces propriétés, vous devez sélectionner **toutes les Configurations**.</span><span class="sxs-lookup"><span data-stu-id="9e435-126">tooedit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Liste Configuration du service pour un service cloud Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a><span data-ttu-id="9e435-128">Modifier le nombre hello d’instances de rôle</span><span class="sxs-lookup"><span data-stu-id="9e435-128">Change hello number of role instances</span></span>
<span data-ttu-id="9e435-129">performances de hello tooimprove de votre service cloud, vous pouvez modifier le nombre hello d’instances d’un rôle qui sont en cours d’exécution, en fonction du nombre de hello d’utilisateurs ou de la charge de hello attendue pour un rôle particulier.</span><span class="sxs-lookup"><span data-stu-id="9e435-129">tooimprove hello performance of your cloud service, you can change hello number of instances of a role that are running, based on hello number of users or hello load expected for a particular role.</span></span> <span data-ttu-id="9e435-130">Une machine virtuelle distincte est créée pour chaque instance d’un rôle lorsque le service de cloud computing hello s’exécute dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9e435-130">A separate virtual machine is created for each instance of a role when hello cloud service runs in Azure.</span></span> <span data-ttu-id="9e435-131">Cela affecte la facturation de hello pour le déploiement de hello de ce service cloud.</span><span class="sxs-lookup"><span data-stu-id="9e435-131">This affects hello billing for hello deployment of this cloud service.</span></span> <span data-ttu-id="9e435-132">Pour plus d’informations sur la facturation, consultez [Comprendre votre facture Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="9e435-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="9e435-133">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e435-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="9e435-134">Dans **l’Explorateur de solutions**, développez le nœud de projet hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-134">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="9e435-135">Sous hello **rôles** nœud, de clic droit un rôle hello vous souhaitez tooupdate et, dans le menu contextuel de hello, sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="9e435-135">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="9e435-137">Sélectionnez hello **Configuration** onglet.</span><span class="sxs-lookup"><span data-stu-id="9e435-137">Select hello **Configuration** tab.</span></span>

    ![Onglet Configuration](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="9e435-139">Bonjour **Configuration du Service** liste, la configuration du service que vous souhaitez tooupdate sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-139">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>
   
    ![Liste Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="9e435-141">Bonjour **le nombre d’instances** texte, entrez le nombre de hello d’instances que vous souhaitez toostart pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="9e435-141">In hello **Instance count** text box, enter hello number of instances that you want toostart for this role.</span></span> <span data-ttu-id="9e435-142">Chaque instance s’exécute sur un ordinateur virtuel distinct lorsque vous publiez hello cloud service tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9e435-142">Each instance runs on a separate virtual machine when you publish hello cloud service tooAzure.</span></span>

    ![Nombre d’instances de hello mise à jour](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="9e435-144">À partir de hello Visual Studio, barre d’outils, sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9e435-144">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="9e435-145">Gérer des chaînes de connexion pour des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="9e435-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="9e435-146">Vous pouvez ajouter, supprimer ou modifier des chaînes de connexion pour vos configurations de service.</span><span class="sxs-lookup"><span data-stu-id="9e435-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="9e435-147">Par exemple, vous pouvez vouloir une chaîne de connexion locale pour une configuration de service local qui a pour valeur `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="9e435-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="9e435-148">Vous pouvez également vous tooconfigure une configuration de service cloud qui utilise un compte de stockage dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9e435-148">You might also want tooconfigure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="9e435-149">Lorsque vous entrez des informations clés de compte stockage Azure hello pour une chaîne de connexion de compte de stockage, ces informations sont stockées localement dans le fichier de configuration de service hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-149">When you enter hello Azure storage account key information for a storage account connection string, this information is stored locally in hello service configuration file.</span></span> <span data-ttu-id="9e435-150">Toutefois, ces informations ne sont pas stockées sous forme de texte chiffré pour le moment.</span><span class="sxs-lookup"><span data-stu-id="9e435-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="9e435-151">En utilisant une valeur différente pour chaque configuration de service, ne pas avoir toouse différentes chaînes de connexion dans votre service cloud ni modifier votre code lorsque vous publiez votre tooAzure de service cloud.</span><span class="sxs-lookup"><span data-stu-id="9e435-151">By using a different value for each service configuration, you do not have toouse different connection strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="9e435-152">Vous pouvez utiliser hello même nom pour la chaîne de connexion hello dans la valeur de votre code et hello est différent, selon la configuration du service hello que vous sélectionnez lorsque vous générez votre service cloud ou quand vous le publiez.</span><span class="sxs-lookup"><span data-stu-id="9e435-152">You can use hello same name for hello connection string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="9e435-153">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e435-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="9e435-154">Dans **l’Explorateur de solutions**, développez le nœud de projet hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-154">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="9e435-155">Sous hello **rôles** nœud, de clic droit un rôle hello vous souhaitez tooupdate et, dans le menu contextuel de hello, sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="9e435-155">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="9e435-157">Sélectionnez hello **paramètres** onglet.</span><span class="sxs-lookup"><span data-stu-id="9e435-157">Select hello **Settings** tab.</span></span>

    ![Onglet Paramètres](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="9e435-159">Bonjour **Configuration du Service** liste, la configuration du service que vous souhaitez tooupdate sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-159">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="9e435-161">tooadd une chaîne de connexion, sélectionnez **ajouter un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="9e435-161">tooadd a connection string, select **Add Setting**.</span></span>

    ![Ajouter une chaîne de connexion](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="9e435-163">Une fois que le nouveau paramètre de hello a été ajouté toohello liste, mettre à jour de ligne hello dans la liste de hello avec les informations nécessaires hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-163">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![New connection string](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="9e435-165">**Nom** -Entrez le nom hello que vous souhaitez toouse pour la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-165">**Name** - Enter hello name that you want toouse for hello connection string.</span></span>
    - <span data-ttu-id="9e435-166">**Type** : sélectionnez **chaîne de connexion** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-166">**Type** - Select **Connection String** from hello drop-down list.</span></span>
    - <span data-ttu-id="9e435-167">**Valeur** -vous pouvez soit entrer la chaîne de connexion hello directement dans hello **valeur** cellule ou toowork de points de suspension (...) sélectionnez hello Bonjour **créer une chaîne de connexion stockage** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9e435-167">**Value** - You can either enter hello connection string directly into hello **Value** cell, or select hello ellipsis (...) toowork in hello **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="9e435-168">Bonjour **créer une chaîne de connexion stockage** boîte de dialogue, sélectionnez une option pour **se connecter à l’aide de**.</span><span class="sxs-lookup"><span data-stu-id="9e435-168">In hello **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="9e435-169">Suivez ensuite les instructions hello pour option hello sélectionnée :</span><span class="sxs-lookup"><span data-stu-id="9e435-169">Then follow hello instructions for hello option you select:</span></span>

    - <span data-ttu-id="9e435-170">**Émulateur Microsoft Azure storage** -si vous sélectionnez cette option, les paramètres restants de hello sur la boîte de dialogue hello sont désactivées car ils s’appliquent uniquement tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9e435-170">**Microsoft Azure storage emulator** - If you select this option, hello remaining settings on hello dialog are disabled as they apply only tooAzure.</span></span> <span data-ttu-id="9e435-171">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e435-171">Select **OK**.</span></span>
    - <span data-ttu-id="9e435-172">**Votre abonnement** : Si vous sélectionnez cette option, utilisez hello déroulante liste, sélectionnez tooeither et un signe un compte Microsoft, ou ajoutez un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9e435-172">**Your subscription** - If you select this option, use hello dropdown list tooeither select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="9e435-173">Sélectionnez un abonnement et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="9e435-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="9e435-174">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e435-174">Select **OK**.</span></span>
    - <span data-ttu-id="9e435-175">**Entrées manuellement les informations d’identification** - Entrez le nom de compte de stockage hello et soit hello clé primaire ou secondaire.</span><span class="sxs-lookup"><span data-stu-id="9e435-175">**Manually entered credentials** - Enter hello storage account name, and either hello primary or second key.</span></span> <span data-ttu-id="9e435-176">Sélectionnez une option pour **Connexion** (le protocole HTTPS est recommandé pour la plupart des scénarios.) Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e435-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="9e435-177">toodelete une chaîne de connexion, sélectionnez la chaîne de connexion hello et sélectionnez **supprimer un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="9e435-177">toodelete a connection string, select hello connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="9e435-178">À partir de hello Visual Studio, barre d’outils, sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9e435-178">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="9e435-179">Accéder par programme à une chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="9e435-179">Programmatically access a connection string</span></span>

<span data-ttu-id="9e435-180">Hello étapes suivantes montrent comment tooprogrammatically accéder à une chaîne de connexion à l’aide de c#.</span><span class="sxs-lookup"><span data-stu-id="9e435-180">hello following steps show how tooprogrammatically access a connection string using C#.</span></span>

1. <span data-ttu-id="9e435-181">Ajoutez hello qui suit à l’aide du fichier de directives de tooa c# où vous allez paramètre hello de toouse :</span><span class="sxs-lookup"><span data-stu-id="9e435-181">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="9e435-182">Hello de code suivant illustre un exemple de procédure tooaccess une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="9e435-182">hello following code illustrates an example of how tooaccess a connection string.</span></span> <span data-ttu-id="9e435-183">Remplacez hello &lt;ConnectionStringName > espace réservé avec la valeur appropriée de hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-183">Replace hello &lt;ConnectionStringName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a><span data-ttu-id="9e435-184">Ajouter des paramètres personnalisés toouse dans votre service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="9e435-184">Add custom settings toouse in your Azure cloud service</span></span>
<span data-ttu-id="9e435-185">Paramètres personnalisés dans le fichier de configuration de service hello vous permettent d’ajouter un nom et une valeur pour une chaîne pour une configuration de service spécifique.</span><span class="sxs-lookup"><span data-stu-id="9e435-185">Custom settings in hello service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="9e435-186">Vous pouvez choisir toouse cette tooconfigure paramètre une fonctionnalité dans votre service cloud en lisant la valeur hello hello définition et l’utilisation de cette logique de hello toocontrol valeur dans votre code.</span><span class="sxs-lookup"><span data-stu-id="9e435-186">You might choose toouse this setting tooconfigure a feature in your cloud service by reading hello value of hello setting and using this value toocontrol hello logic in your code.</span></span> <span data-ttu-id="9e435-187">Vous pouvez modifier ces valeurs de configuration de service sans avoir à toorebuild votre package de services ou lorsque votre service cloud est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9e435-187">You can change these service configuration values without having toorebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="9e435-188">Votre code peut vérifier les notifications produites lorsqu’un paramètre est modifié.</span><span class="sxs-lookup"><span data-stu-id="9e435-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="9e435-189">Consultez [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e435-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="9e435-190">Vous pouvez ajouter, supprimer ou modifier des paramètres personnalisés pour vos configurations de service.</span><span class="sxs-lookup"><span data-stu-id="9e435-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="9e435-191">Vous pouvez vouloir différentes valeurs pour ces chaînes pour différentes configurations de service.</span><span class="sxs-lookup"><span data-stu-id="9e435-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="9e435-192">En utilisant une valeur différente pour chaque configuration de service, ne pas avoir toouse des chaînes différentes dans votre service cloud ni modifier votre code lorsque vous publiez votre tooAzure de service cloud.</span><span class="sxs-lookup"><span data-stu-id="9e435-192">By using a different value for each service configuration, you do not have toouse different strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="9e435-193">Vous pouvez utiliser hello même nom pour la chaîne hello dans votre code et hello est différent, selon la configuration du service hello que vous sélectionnez lorsque vous générez votre service cloud ou quand vous le publiez.</span><span class="sxs-lookup"><span data-stu-id="9e435-193">You can use hello same name for hello string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="9e435-194">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e435-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="9e435-195">Dans **l’Explorateur de solutions**, développez le nœud de projet hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-195">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="9e435-196">Sous hello **rôles** nœud, de clic droit un rôle hello vous souhaitez tooupdate et, dans le menu contextuel de hello, sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="9e435-196">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="9e435-198">Sélectionnez hello **paramètres** onglet.</span><span class="sxs-lookup"><span data-stu-id="9e435-198">Select hello **Settings** tab.</span></span>

    ![Onglet Paramètres](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="9e435-200">Bonjour **Configuration du Service** liste, la configuration du service que vous souhaitez tooupdate sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-200">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Liste Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="9e435-202">tooadd un paramètre personnalisé, sélectionnez **ajouter un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="9e435-202">tooadd a custom setting, select **Add Setting**.</span></span>

    ![Ajouter un paramètre personnalisé](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="9e435-204">Une fois que le nouveau paramètre de hello a été ajouté toohello liste, mettre à jour de ligne hello dans la liste de hello avec les informations nécessaires hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-204">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nouveau paramètre personnalisé](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="9e435-206">**Nom** -Entrez le nom hello du paramètre de hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-206">**Name** - Enter hello name of hello setting.</span></span>
    - <span data-ttu-id="9e435-207">**Type** : sélectionnez **chaîne** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-207">**Type** - Select **String** from hello drop-down list.</span></span>
    - <span data-ttu-id="9e435-208">**Valeur** -Entrez la valeur hello du paramètre de hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-208">**Value** - Enter hello value of hello setting.</span></span> <span data-ttu-id="9e435-209">Vous pouvez soit entrer la valeur de hello directement dans hello **valeur** cellule ou valeur hello Sélectionnez points de suspension (...) tooenter hello hello **modification de la chaîne** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9e435-209">You can either enter hello value directly into hello **Value** cell, or select hello ellipsis (...) tooenter hello value in hello **Edit String** dialog.</span></span>  

1. <span data-ttu-id="9e435-210">toodelete un paramètre personnalisé, sélectionnez le paramètre de hello, puis **supprimer un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="9e435-210">toodelete a custom setting, select hello setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="9e435-211">À partir de hello Visual Studio, barre d’outils, sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9e435-211">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="9e435-212">Accéder par programme à la valeur d’un paramètre personnalisé</span><span class="sxs-lookup"><span data-stu-id="9e435-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="9e435-213">Hello étapes suivantes montrent comment tooprogrammatically accéder à un paramètre personnalisé à l’aide de c#.</span><span class="sxs-lookup"><span data-stu-id="9e435-213">hello following steps show how tooprogrammatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="9e435-214">Ajoutez hello qui suit à l’aide du fichier de directives de tooa c# où vous allez paramètre hello de toouse :</span><span class="sxs-lookup"><span data-stu-id="9e435-214">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="9e435-215">Hello de code suivant illustre un exemple de procédure tooaccess un paramètre personnalisé.</span><span class="sxs-lookup"><span data-stu-id="9e435-215">hello following code illustrates an example of how tooaccess a custom setting.</span></span> <span data-ttu-id="9e435-216">Remplacez hello &lt;SettingName > espace réservé avec la valeur appropriée de hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-216">Replace hello &lt;SettingName> placeholder with hello appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="9e435-217">Gérer le stockage local pour chaque instance de rôle</span><span class="sxs-lookup"><span data-stu-id="9e435-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="9e435-218">Vous pouvez ajouter le stockage de système de fichiers local pour chaque instance d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="9e435-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="9e435-219">données de salutation stockées dans le stockage n’est pas accessible par d’autres instances de rôle hello pour le hello données sont stockées, ou par les autres rôles.</span><span class="sxs-lookup"><span data-stu-id="9e435-219">hello data stored in that storage is not accessible by other instances of hello role for which hello data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="9e435-220">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e435-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="9e435-221">Dans **l’Explorateur de solutions**, développez le nœud de projet hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-221">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="9e435-222">Sous hello **rôles** nœud, de clic droit un rôle hello vous souhaitez tooupdate et, dans le menu contextuel de hello, sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="9e435-222">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="9e435-224">Sélectionnez hello **stockage Local** onglet.</span><span class="sxs-lookup"><span data-stu-id="9e435-224">Select hello **Local Storage** tab.</span></span>

    ![Onglet Stockage local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="9e435-226">Bonjour **Configuration du Service** liste, vérifiez que **toutes les Configurations** est sélectionné comme paramètres de stockage local hello appliquent des configurations de service tooall.</span><span class="sxs-lookup"><span data-stu-id="9e435-226">In hello **Service Configuration** list, ensure that **All Configurations** is selected as hello local storage settings apply tooall service configurations.</span></span> <span data-ttu-id="9e435-227">Toute autre valeur entraîne de tous les champs d’entrée hello sur la page hello en cours de désactivation.</span><span class="sxs-lookup"><span data-stu-id="9e435-227">Any other value results in all hello input fields on hello page being disabled.</span></span> 

    ![Liste Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="9e435-229">tooadd une entrée de stockage local, sélectionnez **ajouter un stockage Local**.</span><span class="sxs-lookup"><span data-stu-id="9e435-229">tooadd a local storage entry, select **Add Local Storage**.</span></span>

    ![Ajouter le stockage local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="9e435-231">Une fois la nouvelle entrée de stockage local hello a été ajoutée toohello liste, mettre à jour de ligne hello dans la liste de hello avec les informations nécessaires hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-231">Once hello new local storage entry has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nouvelle entrée de stockage local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="9e435-233">**Nom** -Entrez le nom hello que vous souhaitez toouse de stockage local hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-233">**Name** - Enter hello name that you want toouse for hello new local storage.</span></span>
    - <span data-ttu-id="9e435-234">**Taille (Mo)** -Entrez la taille de hello en Mo dont vous avez besoin de stockage local hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-234">**Size (MB)** - Enter hello size in MB that you need for hello new local storage.</span></span>
    - <span data-ttu-id="9e435-235">**Nettoyage de recyclage des rôles** -sélectionner ces données de hello tooremove option dans le stockage local nouvelle hello lors de la machine virtuelle de hello pour le rôle de hello est recyclé.</span><span class="sxs-lookup"><span data-stu-id="9e435-235">**Clean on role recycle** - Select this option tooremove hello data in hello new local storage when hello virtual machine for hello role is recycled.</span></span>

1. <span data-ttu-id="9e435-236">toodelete une entrée de stockage local, sélectionnez l’entrée de hello et sélectionnez **supprimer le stockage Local**.</span><span class="sxs-lookup"><span data-stu-id="9e435-236">toodelete a local storage entry, select hello entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="9e435-237">À partir de hello Visual Studio, barre d’outils, sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9e435-237">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="9e435-238">Accès par programme au stockage local</span><span class="sxs-lookup"><span data-stu-id="9e435-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="9e435-239">Cette section illustre comment accéder à l’aide de c# en écrivant un fichier texte de test de stockage local tooprogrammatically `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="9e435-239">This section illustrates how tooprogrammatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-toolocal-storage"></a><span data-ttu-id="9e435-240">Écrire un stockage toolocal du fichier texte</span><span class="sxs-lookup"><span data-stu-id="9e435-240">Write a text file toolocal storage</span></span>

<span data-ttu-id="9e435-241">Hello suivant de code montre comment toowrite un texte toolocal stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="9e435-241">hello following code shows an example of how toowrite a text file toolocal storage.</span></span> <span data-ttu-id="9e435-242">Remplacez hello &lt;LocalStorageName > espace réservé avec la valeur appropriée de hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-242">Replace hello &lt;LocalStorageName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a><span data-ttu-id="9e435-243">Rechercher un fichier écrit toolocal stockage</span><span class="sxs-lookup"><span data-stu-id="9e435-243">Find a file written toolocal storage</span></span>

<span data-ttu-id="9e435-244">fichier de hello tooview créée par le code hello dans la section précédente de hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9e435-244">tooview hello file created by hello code in hello previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="9e435-245">Hello la zone de notification Windows, avec le bouton droit hello icône Windows Azure et, dans le menu contextuel de hello, sélectionnez **Show Compute Emulator UI**.</span><span class="sxs-lookup"><span data-stu-id="9e435-245">In hello Windows notification area, right-click hello Azure icon, and, from hello context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Afficher l’émulateur de calcul Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="9e435-247">Sélectionnez un rôle web de hello.</span><span class="sxs-lookup"><span data-stu-id="9e435-247">Select hello web role.</span></span>

    ![Émulateur de calcul Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="9e435-249">Sur hello **émulateur de calcul Azure Microsoft** menu, sélectionnez **outils** > **ouvrir magasin local**.</span><span class="sxs-lookup"><span data-stu-id="9e435-249">On hello **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Élément du menu Ouvrir magasin local](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="9e435-251">Lors de la fenêtre de l’Explorateur Windows hello s’ouvre, entrez « MyLocalStorageTest.txt'' dans hello **recherche** zone de texte, puis sélectionnez **entrée** recherche de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="9e435-251">When hello Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into hello **Search** text box, and select **Enter** toostart hello search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9e435-252">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e435-252">Next steps</span></span>
<span data-ttu-id="9e435-253">En savoir plus sur les projets Azure dans Visual Studio en lisant [Configuration d’un projet Azure](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="9e435-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="9e435-254">En savoir plus sur le schéma de service cloud hello en lisant [référence du schéma](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="9e435-254">Learn more about hello cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

