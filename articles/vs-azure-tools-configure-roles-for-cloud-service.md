---
title: "Configurer les rôles pour un service cloud Azure avec Visual Studio | Microsoft Docs"
description: "Découvrez comment installer et configurer des rôles pour les services cloud Azure à l’aide de Visual Studio."
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
ms.openlocfilehash: 17da71ac0c5ab9330b9244c0354e4d161d98229e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="f97f5-103">Configurer des rôles de service cloud Azure avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f97f5-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="f97f5-104">Un service cloud Azure peut avoir un ou plusieurs rôles de travail ou rôles web.</span><span class="sxs-lookup"><span data-stu-id="f97f5-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="f97f5-105">Pour chaque rôle, vous devez définir le mode de configuration de ce rôle et configurer son mode d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f97f5-105">For each role, you need to define how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="f97f5-106">Pour en savoir plus sur les rôles dans les services cloud, regardez la vidéo [Introduction aux services cloud Azure](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="f97f5-106">To learn more about roles in cloud services, see the video [Introduction to Azure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="f97f5-107">Les informations pour votre service cloud sont stockées dans les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="f97f5-107">The information for your cloud service is stored in the following files:</span></span>

- <span data-ttu-id="f97f5-108">**ServiceDefinition.csdef** : le fichier de définition de service définit les paramètres d’exécution de votre service cloud, y compris les rôles requis, les points de terminaison et la taille de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f97f5-108">**ServiceDefinition.csdef** - The service definition file defines the runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="f97f5-109">Aucune des données stockées dans `ServiceDefinition.csdef` ne peut être modifiée lorsque votre rôle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f97f5-109">None of the data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="f97f5-110">**ServiceConfiguration.cscfg** : le fichier de configuration de service configure le nombre d’instances d’un rôle exécutées et les valeurs des paramètres définis pour un rôle.</span><span class="sxs-lookup"><span data-stu-id="f97f5-110">**ServiceConfiguration.cscfg** - The service configuration file configures how many instances of a role are run and the values of the settings defined for a role.</span></span> <span data-ttu-id="f97f5-111">Les données stockées dans `ServiceConfiguration.cscfg` peuvent être modifiées lorsque votre rôle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f97f5-111">The data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="f97f5-112">Pour stocker différentes valeurs pour les paramètres qui contrôlent l’exécution d’un rôle, vous pouvez définir plusieurs configurations de service.</span><span class="sxs-lookup"><span data-stu-id="f97f5-112">To store different values for the settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="f97f5-113">Vous pouvez utiliser une configuration de service différente pour chaque environnement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="f97f5-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="f97f5-114">Par exemple, vous pouvez définir votre chaîne de connexion de compte de stockage pour utiliser l’émulateur de stockage Azure local dans une configuration de service local et créer une autre configuration de service pour utiliser le stockage Azure dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="f97f5-114">For example, you can set your storage account connection string to use the local Azure storage emulator in a local service configuration and create another service configuration to use Azure storage in the cloud.</span></span>

<span data-ttu-id="f97f5-115">Lorsque vous créez un service cloud Azure dans Visual Studio, deux configurations de service sont automatiquement créées et ajoutées à votre projet Azure :</span><span class="sxs-lookup"><span data-stu-id="f97f5-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added to your Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="f97f5-116">Configurer un service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="f97f5-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="f97f5-117">Vous pouvez configurer un service cloud Azure à partir de l’Explorateur de solutions dans Visual Studio, comme indiqué dans les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f97f5-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in the following steps:</span></span>

1. <span data-ttu-id="f97f5-118">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f97f5-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="f97f5-119">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet, puis, dans le menu contextuel, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-119">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>
   
    ![Menu contextuel de projet dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="f97f5-121">Dans la page de propriétés du projet, sélectionnez l’onglet **Développement**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-121">In the project's properties page, select the **Development** tab.</span></span> 

    ![Page de propriétés du projet : onglet développement](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="f97f5-123">Dans la liste **Configuration du service**, sélectionnez le nom de la configuration de service que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="f97f5-123">In the **Service Configuration** list, select the name of the service configuration that you want to edit.</span></span> <span data-ttu-id="f97f5-124">(Si vous souhaitez modifier toutes les configurations de service pour ce rôle, sélectionnez **Toutes les configurations**.)</span><span class="sxs-lookup"><span data-stu-id="f97f5-124">(If you want to make changes to all the service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="f97f5-125">Si vous choisissez une configuration de service spécifique, certaines propriétés sont désactivées parce qu’elles peuvent être définies uniquement pour toutes les configurations.</span><span class="sxs-lookup"><span data-stu-id="f97f5-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="f97f5-126">Pour modifier ces propriétés, vous devez sélectionner **Toutes les configurations**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-126">To edit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Liste Configuration du service pour un service cloud Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-the-number-of-role-instances"></a><span data-ttu-id="f97f5-128">Modifier le nombre d’instances d’un rôle</span><span class="sxs-lookup"><span data-stu-id="f97f5-128">Change the number of role instances</span></span>
<span data-ttu-id="f97f5-129">Pour améliorer la performance de votre service cloud, vous pouvez modifier le nombre d’instances d’un rôle qui s’exécutent, en fonction du nombre d’utilisateurs ou de la charge attendue pour un rôle particulier.</span><span class="sxs-lookup"><span data-stu-id="f97f5-129">To improve the performance of your cloud service, you can change the number of instances of a role that are running, based on the number of users or the load expected for a particular role.</span></span> <span data-ttu-id="f97f5-130">Une machine virtuelle distincte est créée pour chaque instance d’un rôle quand le service cloud s’exécute dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f97f5-130">A separate virtual machine is created for each instance of a role when the cloud service runs in Azure.</span></span> <span data-ttu-id="f97f5-131">Cela affecte la facturation correspondant au déploiement de ce service cloud.</span><span class="sxs-lookup"><span data-stu-id="f97f5-131">This affects the billing for the deployment of this cloud service.</span></span> <span data-ttu-id="f97f5-132">Pour plus d’informations sur la facturation, consultez [Comprendre votre facture Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="f97f5-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="f97f5-133">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f97f5-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="f97f5-134">Dans **l’Explorateur de solutions**, développez le nœud du projet.</span><span class="sxs-lookup"><span data-stu-id="f97f5-134">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="f97f5-135">Sous le nœud **Rôles**, cliquez avec le bouton droit sur le rôle que vous souhaitez mettre à jour, puis, dans le menu contextuel, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-135">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="f97f5-137">Sélectionnez l’onglet **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-137">Select the **Configuration** tab.</span></span>

    ![Onglet Configuration](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="f97f5-139">Dans la liste **Configuration du service**, sélectionnez la configuration de service que vous voulez mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="f97f5-139">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>
   
    ![Liste Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="f97f5-141">Dans la zone de texte **Nombre d’instances** , entrez le nombre d’instances que vous voulez démarrer pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="f97f5-141">In the **Instance count** text box, enter the number of instances that you want to start for this role.</span></span> <span data-ttu-id="f97f5-142">Chaque instance s’exécute sur une machine virtuelle distincte quand vous publiez le service cloud sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f97f5-142">Each instance runs on a separate virtual machine when you publish the cloud service to Azure.</span></span>

    ![Mise à jour du nombre d’instances](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="f97f5-144">Dans la barre d’outils de Visual Studio, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-144">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="f97f5-145">Gérer des chaînes de connexion pour des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="f97f5-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="f97f5-146">Vous pouvez ajouter, supprimer ou modifier des chaînes de connexion pour vos configurations de service.</span><span class="sxs-lookup"><span data-stu-id="f97f5-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="f97f5-147">Par exemple, vous pouvez vouloir une chaîne de connexion locale pour une configuration de service local qui a pour valeur `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="f97f5-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="f97f5-148">Vous pouvez aussi vouloir définir une configuration de service cloud qui utilise un compte de stockage dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f97f5-148">You might also want to configure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="f97f5-149">Lorsque vous entrez les informations de clé du compte de stockage Azure pour une chaîne de connexion de compte de stockage, ces informations sont stockées localement dans le fichier de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="f97f5-149">When you enter the Azure storage account key information for a storage account connection string, this information is stored locally in the service configuration file.</span></span> <span data-ttu-id="f97f5-150">Toutefois, ces informations ne sont pas stockées sous forme de texte chiffré pour le moment.</span><span class="sxs-lookup"><span data-stu-id="f97f5-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="f97f5-151">Si vous utilisez une valeur différente pour chaque configuration de service, il n’est pas nécessaire d’utiliser des chaînes de connexion différentes dans votre service cloud ni de modifier votre code quand vous publiez votre service cloud sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f97f5-151">By using a different value for each service configuration, you do not have to use different connection strings in your cloud service or modify your code when you publish your cloud service to Azure.</span></span> <span data-ttu-id="f97f5-152">Vous pouvez utiliser le même nom pour la chaîne de connexion dans votre code, et la valeur sera différente, en fonction de la configuration de service que vous sélectionnez quand vous générez votre service cloud ou quand vous le publiez.</span><span class="sxs-lookup"><span data-stu-id="f97f5-152">You can use the same name for the connection string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="f97f5-153">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f97f5-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="f97f5-154">Dans **l’Explorateur de solutions**, développez le nœud du projet.</span><span class="sxs-lookup"><span data-stu-id="f97f5-154">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="f97f5-155">Sous le nœud **Rôles**, cliquez avec le bouton droit sur le rôle que vous souhaitez mettre à jour, puis, dans le menu contextuel, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-155">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="f97f5-157">Sélectionnez l’onglet **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-157">Select the **Settings** tab.</span></span>

    ![Onglet Paramètres](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="f97f5-159">Dans la liste **Configuration du service**, sélectionnez la configuration de service que vous voulez mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="f97f5-159">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>

    ![Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="f97f5-161">Pour ajouter une chaîne de connexion, sélectionnez **Ajouter un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-161">To add a connection string, select **Add Setting**.</span></span>

    ![Ajouter une chaîne de connexion](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="f97f5-163">Une fois le nouveau paramètre ajouté à la liste, mettez à jour la ligne dans la liste avec les informations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="f97f5-163">Once the new setting has been added to the list, update the row in the list with the necessary information.</span></span>

    ![New connection string](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="f97f5-165">**Nom** : entrez le nom que vous voulez utiliser pour la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="f97f5-165">**Name** - Enter the name that you want to use for the connection string.</span></span>
    - <span data-ttu-id="f97f5-166">**Type** : sélectionnez **Chaîne de connexion** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="f97f5-166">**Type** - Select **Connection String** from the drop-down list.</span></span>
    - <span data-ttu-id="f97f5-167">**Valeur** : vous pouvez entrer la chaîne de connexion directement dans la cellule **Valeur** ou sélectionner les points de suspension (...) pour utiliser la boîte de dialogue **Créer une chaîne de connexion de stockage**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-167">**Value** - You can either enter the connection string directly into the **Value** cell, or select the ellipsis (...) to work in the **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="f97f5-168">Dans la boîte de dialogue **Créer une chaîne de connexion de stockage**, sélectionnez une option pour **Se connecter avec**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-168">In the **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="f97f5-169">Suivez les instructions correspondant à l’option sélectionnée :</span><span class="sxs-lookup"><span data-stu-id="f97f5-169">Then follow the instructions for the option you select:</span></span>

    - <span data-ttu-id="f97f5-170">**Émulateur de stockage Microsoft Azure** : si vous sélectionnez cette option, les autres paramètres de la boîte de dialogue sont désactivés, car ils s’appliquent uniquement à Azure.</span><span class="sxs-lookup"><span data-stu-id="f97f5-170">**Microsoft Azure storage emulator** - If you select this option, the remaining settings on the dialog are disabled as they apply only to Azure.</span></span> <span data-ttu-id="f97f5-171">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-171">Select **OK**.</span></span>
    - <span data-ttu-id="f97f5-172">**Votre abonnement** : si vous sélectionnez cette option, utilisez la liste déroulante pour sélectionner un compte Microsoft et s’y connecter ou pour ajouter un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f97f5-172">**Your subscription** - If you select this option, use the dropdown list to either select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="f97f5-173">Sélectionnez un abonnement et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="f97f5-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="f97f5-174">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-174">Select **OK**.</span></span>
    - <span data-ttu-id="f97f5-175">**Informations d’identification entrées manuellement** : entrez le nom du compte de stockage, ainsi que la clé primaire ou secondaire.</span><span class="sxs-lookup"><span data-stu-id="f97f5-175">**Manually entered credentials** - Enter the storage account name, and either the primary or second key.</span></span> <span data-ttu-id="f97f5-176">Sélectionnez une option pour **Connexion** (le protocole HTTPS est recommandé pour la plupart des scénarios.) Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="f97f5-177">Pour supprimer une chaîne de connexion, sélectionnez-la, puis sélectionnez **Supprimer un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-177">To delete a connection string, select the connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="f97f5-178">Dans la barre d’outils de Visual Studio, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-178">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="f97f5-179">Accéder par programme à une chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="f97f5-179">Programmatically access a connection string</span></span>

<span data-ttu-id="f97f5-180">Les étapes suivantes montrent comment accéder par programme à une chaîne de connexion en C#.</span><span class="sxs-lookup"><span data-stu-id="f97f5-180">The following steps show how to programmatically access a connection string using C#.</span></span>

1. <span data-ttu-id="f97f5-181">En utilisant les directives, ajoutez le contenu suivant dans un fichier en C# dans lequel vous allez utiliser le paramètre :</span><span class="sxs-lookup"><span data-stu-id="f97f5-181">Add the following using directives to a C# file where you are going to use the setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="f97f5-182">Le code suivant illustre un exemple d’accès à une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="f97f5-182">The following code illustrates an example of how to access a connection string.</span></span> <span data-ttu-id="f97f5-183">Remplacez l’espace réservé &lt;ConnectionStringName> par la valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="f97f5-183">Replace the &lt;ConnectionStringName> placeholder with the appropriate value.</span></span> 

    ```csharp
    // Setup the connection to Azure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-to-use-in-your-azure-cloud-service"></a><span data-ttu-id="f97f5-184">Ajouter des paramètres personnalisés à utiliser dans votre service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="f97f5-184">Add custom settings to use in your Azure cloud service</span></span>
<span data-ttu-id="f97f5-185">Les paramètres personnalisés dans le fichier de configuration de service vous permettent d’ajouter un nom et une valeur pour une chaîne pour une configuration de service spécifique.</span><span class="sxs-lookup"><span data-stu-id="f97f5-185">Custom settings in the service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="f97f5-186">Vous pouvez choisir d’utiliser ce paramètre pour configurer une fonctionnalité dans votre service cloud en lisant la valeur du paramètre et en utilisant cette valeur pour contrôler la logique de votre code.</span><span class="sxs-lookup"><span data-stu-id="f97f5-186">You might choose to use this setting to configure a feature in your cloud service by reading the value of the setting and using this value to control the logic in your code.</span></span> <span data-ttu-id="f97f5-187">Vous pouvez modifier ces valeurs de configuration de service sans devoir régénérer votre package de services ou lorsque votre service cloud est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f97f5-187">You can change these service configuration values without having to rebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="f97f5-188">Votre code peut vérifier les notifications produites lorsqu’un paramètre est modifié.</span><span class="sxs-lookup"><span data-stu-id="f97f5-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="f97f5-189">Consultez [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="f97f5-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="f97f5-190">Vous pouvez ajouter, supprimer ou modifier des paramètres personnalisés pour vos configurations de service.</span><span class="sxs-lookup"><span data-stu-id="f97f5-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="f97f5-191">Vous pouvez vouloir différentes valeurs pour ces chaînes pour différentes configurations de service.</span><span class="sxs-lookup"><span data-stu-id="f97f5-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="f97f5-192">Si vous utilisez une valeur différente pour chaque configuration de service, il n’est pas nécessaire d’utiliser des chaînes différentes dans votre service cloud ni de modifier votre code quand vous publiez votre service cloud sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f97f5-192">By using a different value for each service configuration, you do not have to use different strings in your cloud service or modify your code when you publish your cloud service to Azure.</span></span> <span data-ttu-id="f97f5-193">Vous pouvez utiliser le même nom pour la chaîne dans votre code et la valeur sera différente, en fonction de la configuration de service que vous sélectionnez quand vous générez votre service cloud ou quand vous le publiez.</span><span class="sxs-lookup"><span data-stu-id="f97f5-193">You can use the same name for the string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="f97f5-194">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f97f5-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="f97f5-195">Dans **l’Explorateur de solutions**, développez le nœud du projet.</span><span class="sxs-lookup"><span data-stu-id="f97f5-195">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="f97f5-196">Sous le nœud **Rôles**, cliquez avec le bouton droit sur le rôle que vous souhaitez mettre à jour, puis, dans le menu contextuel, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-196">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="f97f5-198">Sélectionnez l’onglet **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-198">Select the **Settings** tab.</span></span>

    ![Onglet Paramètres](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="f97f5-200">Dans la liste **Configuration du service**, sélectionnez la configuration de service que vous voulez mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="f97f5-200">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>

    ![Liste Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="f97f5-202">Pour ajouter un paramètre personnalisé, sélectionnez **Ajouter un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-202">To add a custom setting, select **Add Setting**.</span></span>

    ![Ajouter un paramètre personnalisé](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="f97f5-204">Une fois le nouveau paramètre ajouté à la liste, mettez à jour la ligne dans la liste avec les informations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="f97f5-204">Once the new setting has been added to the list, update the row in the list with the necessary information.</span></span>

    ![Nouveau paramètre personnalisé](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="f97f5-206">**Nom** : entrez le nom du paramètre.</span><span class="sxs-lookup"><span data-stu-id="f97f5-206">**Name** - Enter the name of the setting.</span></span>
    - <span data-ttu-id="f97f5-207">**Type** : sélectionnez **Chaîne** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="f97f5-207">**Type** - Select **String** from the drop-down list.</span></span>
    - <span data-ttu-id="f97f5-208">**Valeur** : entrez la valeur du paramètre.</span><span class="sxs-lookup"><span data-stu-id="f97f5-208">**Value** - Enter the value of the setting.</span></span> <span data-ttu-id="f97f5-209">Vous pouvez entrer directement la valeur dans la cellule **Valeur** ou sélectionner les points de suspension (...) pour entrer la valeur dans la boîte de dialogue **Modifier la chaîne**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-209">You can either enter the value directly into the **Value** cell, or select the ellipsis (...) to enter the value in the **Edit String** dialog.</span></span>  

1. <span data-ttu-id="f97f5-210">Pour supprimer un paramètre personnalisé, sélectionnez-le, puis sélectionnez **Supprimer un paramètre**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-210">To delete a custom setting, select the setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="f97f5-211">Dans la barre d’outils de Visual Studio, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-211">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="f97f5-212">Accéder par programme à la valeur d’un paramètre personnalisé</span><span class="sxs-lookup"><span data-stu-id="f97f5-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="f97f5-213">Les étapes suivantes montrent comment accéder par programme à un paramètre personnalisé en C#.</span><span class="sxs-lookup"><span data-stu-id="f97f5-213">The following steps show how to programmatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="f97f5-214">En utilisant les directives, ajoutez le contenu suivant dans un fichier en C# dans lequel vous allez utiliser le paramètre :</span><span class="sxs-lookup"><span data-stu-id="f97f5-214">Add the following using directives to a C# file where you are going to use the setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="f97f5-215">Le code suivant illustre un exemple d’accès à un paramètre personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f97f5-215">The following code illustrates an example of how to access a custom setting.</span></span> <span data-ttu-id="f97f5-216">Remplacez l’espace réservé &lt;SettingName> par la valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="f97f5-216">Replace the &lt;SettingName> placeholder with the appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="f97f5-217">Gérer le stockage local pour chaque instance de rôle</span><span class="sxs-lookup"><span data-stu-id="f97f5-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="f97f5-218">Vous pouvez ajouter le stockage de système de fichiers local pour chaque instance d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="f97f5-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="f97f5-219">Les données stockées dans cet espace de stockage ne sont pas accessibles aux autres instances du rôle pour lequel les données sont stockées ni aux autres rôles.</span><span class="sxs-lookup"><span data-stu-id="f97f5-219">The data stored in that storage is not accessible by other instances of the role for which the data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="f97f5-220">Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f97f5-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="f97f5-221">Dans **l’Explorateur de solutions**, développez le nœud du projet.</span><span class="sxs-lookup"><span data-stu-id="f97f5-221">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="f97f5-222">Sous le nœud **Rôles**, cliquez avec le bouton droit sur le rôle que vous souhaitez mettre à jour, puis, dans le menu contextuel, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-222">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="f97f5-224">Sélectionnez l’onglet **Stockage local**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-224">Select the **Local Storage** tab.</span></span>

    ![Onglet Stockage local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="f97f5-226">Dans la liste **Configuration du service**, vérifiez que l’option **Toutes les configurations** est sélectionnée, car les paramètres de stockage local s’appliquent à toutes les configurations de service.</span><span class="sxs-lookup"><span data-stu-id="f97f5-226">In the **Service Configuration** list, ensure that **All Configurations** is selected as the local storage settings apply to all service configurations.</span></span> <span data-ttu-id="f97f5-227">Toute autre valeur entraîne la désactivation de tous les champs d’entrée de la page.</span><span class="sxs-lookup"><span data-stu-id="f97f5-227">Any other value results in all the input fields on the page being disabled.</span></span> 

    ![Liste Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="f97f5-229">Pour ajouter une entrée de stockage local, sélectionnez **Ajouter le stockage local**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-229">To add a local storage entry, select **Add Local Storage**.</span></span>

    ![Ajouter le stockage local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="f97f5-231">Une fois la nouvelle entrée de stockage local ajoutée à la liste, mettez à jour la ligne dans la liste avec les informations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="f97f5-231">Once the new local storage entry has been added to the list, update the row in the list with the necessary information.</span></span>

    ![Nouvelle entrée de stockage local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="f97f5-233">**Nom** : entrez le nom que vous voulez utiliser pour le nouveau stockage local.</span><span class="sxs-lookup"><span data-stu-id="f97f5-233">**Name** - Enter the name that you want to use for the new local storage.</span></span>
    - <span data-ttu-id="f97f5-234">**Taille (Mo)** : entrez la taille (en Mo) dont vous avez besoin pour le nouveau stockage local.</span><span class="sxs-lookup"><span data-stu-id="f97f5-234">**Size (MB)** - Enter the size in MB that you need for the new local storage.</span></span>
    - <span data-ttu-id="f97f5-235">**Nettoyer après le recyclage des rôles** : sélectionnez cette option pour supprimer les données dans le nouveau stockage local quand la machine virtuelle pour le rôle est recyclée.</span><span class="sxs-lookup"><span data-stu-id="f97f5-235">**Clean on role recycle** - Select this option to remove the data in the new local storage when the virtual machine for the role is recycled.</span></span>

1. <span data-ttu-id="f97f5-236">Pour supprimer une entrée de stockage local, sélectionnez l’entrée, puis **Remove Local Storage (Supprimer le stockage local)**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-236">To delete a local storage entry, select the entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="f97f5-237">Dans la barre d’outils de Visual Studio, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-237">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="f97f5-238">Accès par programme au stockage local</span><span class="sxs-lookup"><span data-stu-id="f97f5-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="f97f5-239">Cette section montre comment accéder par programme au stockage local en C# en écrivant un fichier texte de test `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="f97f5-239">This section illustrates how to programmatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-to-local-storage"></a><span data-ttu-id="f97f5-240">Écrire un fichier texte dans le stockage local</span><span class="sxs-lookup"><span data-stu-id="f97f5-240">Write a text file to local storage</span></span>

<span data-ttu-id="f97f5-241">Le code suivant présente un exemple d’écriture de fichier texte dans le stockage local.</span><span class="sxs-lookup"><span data-stu-id="f97f5-241">The following code shows an example of how to write a text file to local storage.</span></span> <span data-ttu-id="f97f5-242">Remplacez l’espace réservé &lt;LocalStorageName> par la valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="f97f5-242">Replace the &lt;LocalStorageName> placeholder with the appropriate value.</span></span> 

    ```csharp
    // Retrieve an object that points to the local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define the file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-to-local-storage"></a><span data-ttu-id="f97f5-243">Rechercher un fichier écrit dans le stockage local</span><span class="sxs-lookup"><span data-stu-id="f97f5-243">Find a file written to local storage</span></span>

<span data-ttu-id="f97f5-244">Pour afficher le fichier créé par le code dans la section précédente, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f97f5-244">To view the file created by the code in the previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="f97f5-245">Dans la zone de notification Windows, cliquez avec le bouton droit sur l’icône Azure, puis, dans le menu contextuel, sélectionnez **Afficher l’interface utilisateur de l’émulateur de calcul**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-245">In the Windows notification area, right-click the Azure icon, and, from the context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Afficher l’émulateur de calcul Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="f97f5-247">Sélectionnez le rôle web.</span><span class="sxs-lookup"><span data-stu-id="f97f5-247">Select the web role.</span></span>

    ![Émulateur de calcul Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="f97f5-249">Dans le menu **Émulateur de calcul Microsoft Azure**, sélectionnez **Outils** > **Ouvrir magasin local**.</span><span class="sxs-lookup"><span data-stu-id="f97f5-249">On the **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Élément du menu Ouvrir magasin local](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="f97f5-251">Lorsque la fenêtre de l’Explorateur Windows s’ouvre, entrez « MyLocalStorageTest.txt » dans la zone de texte **Rechercher**, puis sélectionnez **Entrée** pour démarrer la recherche.</span><span class="sxs-lookup"><span data-stu-id="f97f5-251">When the Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into the **Search** text box, and select **Enter** to start the search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f97f5-252">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f97f5-252">Next steps</span></span>
<span data-ttu-id="f97f5-253">En savoir plus sur les projets Azure dans Visual Studio en lisant [Configuration d’un projet Azure](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="f97f5-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="f97f5-254">En savoir plus sur le schéma de service cloud en lisant [Référence de schéma](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="f97f5-254">Learn more about the cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

