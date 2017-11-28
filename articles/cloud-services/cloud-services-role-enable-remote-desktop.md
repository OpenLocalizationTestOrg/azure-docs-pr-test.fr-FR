---
title: "Activation du Bureau à distance dans Service cloud Azure | Microsoft Docs"
description: "Configuration de l’application de service cloud Azure pour autoriser les connexions Bureau à distance"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 413e72e9a39fcde84f56bfc61a6bc72dbadf1c97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="cb918-103">Activer une connexion Bureau à distance pour un rôle dans Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="cb918-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb918-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="cb918-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="cb918-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="cb918-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="cb918-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb918-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="cb918-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb918-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="cb918-108">Vous pouvez activer une connexion Bureau à distance dans votre rôle pendant le développement en incluant les modules Bureau à distance dans votre définition de service. Vous pouvez aussi activer le Bureau à distance via l’extension Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="cb918-108">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="cb918-109">Cette deuxième approche est recommandée, car elle vous permet d’activer le Bureau à distance sans avoir à redéployer votre application.</span><span class="sxs-lookup"><span data-stu-id="cb918-109">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-classic-portal"></a><span data-ttu-id="cb918-110">Configurer le Bureau à distance à partir du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="cb918-110">Configure Remote Desktop from the Azure classic portal</span></span>
<span data-ttu-id="cb918-111">Le portail Azure Classic utilise l’approche basée sur l’extension Bureau à distance, ce qui vous permet d’activer le Bureau à distance même après déployé l’application.</span><span class="sxs-lookup"><span data-stu-id="cb918-111">The Azure classic portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="cb918-112">La page **Configurer** de votre service cloud vous permet d’activer le Bureau à distance, de changer le compte Administrateur local utilisé pour la connexion aux machines virtuelles ou le certificat employé dans l’authentification, et de définir la date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="cb918-112">The **Configure** page for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="cb918-113">Cliquez sur **Cloud Services**, cliquez sur le nom du service cloud, puis cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="cb918-113">Click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="cb918-114">Cliquez sur le bouton **Distant** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="cb918-114">Click the **Remote** button at the bottom.</span></span>

    ![Services cloud à distance](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="cb918-116">toutes les instances de rôle sont redémarrées lorsque vous activez pour la première fois le Bureau à distance et cliquez sur OK (coche).</span><span class="sxs-lookup"><span data-stu-id="cb918-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="cb918-117">Pour éviter un redémarrage, le certificat utilisé pour chiffrer le mot de passe doit être installé sur le rôle.</span><span class="sxs-lookup"><span data-stu-id="cb918-117">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="cb918-118">Pour éviter un redémarrage, [téléchargez un certificat pour le service cloud](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , puis revenez à cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cb918-118">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>

3. <span data-ttu-id="cb918-119">Dans **Roles**, sélectionnez le rôle que vous voulez mettre à jour ou sélectionnez **Tous** pour tous les rôles.</span><span class="sxs-lookup"><span data-stu-id="cb918-119">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>
4. <span data-ttu-id="cb918-120">Effectuez les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="cb918-120">Make any of the following changes:</span></span>

   * <span data-ttu-id="cb918-121">Pour activer le Bureau à distance, activez la case à cocher **Enable Remote Desktop** .</span><span class="sxs-lookup"><span data-stu-id="cb918-121">To enable Remote Desktop, select the **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="cb918-122">Pour désactiver le Bureau à distance, désactivez la case à cocher.</span><span class="sxs-lookup"><span data-stu-id="cb918-122">To disable Remote Desktop, clear the check box.</span></span>
   * <span data-ttu-id="cb918-123">Créez un compte pour utiliser les connexions Bureau à distance aux instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="cb918-123">Create an account to use in Remote Desktop connections to the role instances.</span></span>
   * <span data-ttu-id="cb918-124">Mettez à jour le mot de passe du compte existant.</span><span class="sxs-lookup"><span data-stu-id="cb918-124">Update the password for the existing account.</span></span>
   * <span data-ttu-id="cb918-125">Sélectionnez le certificat téléchargé à utiliser pour l’authentification (téléchargez le certificat en utilisant la commande **Télécharger** sur la page **Certificats**) ou créez un certificat.</span><span class="sxs-lookup"><span data-stu-id="cb918-125">Select an uploaded certificate to use for authentication (upload the certificate using **Upload** on the **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="cb918-126">Changez la date d'expiration de la configuration du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="cb918-126">Change the expiration date for the Remote Desktop configuration.</span></span>

5. <span data-ttu-id="cb918-127">Lorsque les mises à jour de la configuration sont terminées, cliquez sur **OK** (coche).</span><span class="sxs-lookup"><span data-stu-id="cb918-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="cb918-128">À distance dans les instances de rôle</span><span class="sxs-lookup"><span data-stu-id="cb918-128">Remote into role instances</span></span>
<span data-ttu-id="cb918-129">Une fois le Bureau à distance activé sur les rôles, vous pouvez vous connecter à distance à une instance de rôle via divers outils.</span><span class="sxs-lookup"><span data-stu-id="cb918-129">Once Remote Desktop is enabled on the roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="cb918-130">Pour vous connecter à une instance de rôle à partir du portail Azure Classic :</span><span class="sxs-lookup"><span data-stu-id="cb918-130">To connect to a role instance from the Azure classic portal:</span></span>

1. <span data-ttu-id="cb918-131">Cliquez sur **Instances** pour ouvrir la page **Instances**.</span><span class="sxs-lookup"><span data-stu-id="cb918-131">Click **Instances** to open the **Instances** page.</span></span>
2. <span data-ttu-id="cb918-132">Sélectionnez une instance de rôle pour laquelle la fonctionnalité Bureau à distance est configurée.</span><span class="sxs-lookup"><span data-stu-id="cb918-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="cb918-133">Cliquez sur **Connecter**et suivez les instructions pour ouvrir le Bureau.</span><span class="sxs-lookup"><span data-stu-id="cb918-133">Click **Connect**, and follow the instructions to open the desktop.</span></span>
4. <span data-ttu-id="cb918-134">Cliquez sur **Ouvrir**, puis sur **Connecter** pour démarrer la connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="cb918-134">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

### <a name="use-visual-studio-to-remote-into-a-role-instance"></a><span data-ttu-id="cb918-135">Utiliser Visual Studio pour se connecter à distance à une instance de rôle</span><span class="sxs-lookup"><span data-stu-id="cb918-135">Use Visual Studio to remote into a role instance</span></span>
<span data-ttu-id="cb918-136">Dans l’Explorateur de serveurs Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="cb918-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="cb918-137">Développez le nœud **Azure** > **Cloud Services** > **[nom du service cloud]**.</span><span class="sxs-lookup"><span data-stu-id="cb918-137">Expand the **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="cb918-138">Développez **Intermédiaire** ou **Production**.</span><span class="sxs-lookup"><span data-stu-id="cb918-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="cb918-139">Développez le rôle individuel.</span><span class="sxs-lookup"><span data-stu-id="cb918-139">Expand the individual role.</span></span>
4. <span data-ttu-id="cb918-140">Cliquez avec le bouton droit sur l’une des instances de rôle, cliquez sur **Connexion à l’aide de Bureau à distance**, puis entrez le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="cb918-140">Right-click one of the role instances, click **Connect using Remote Desktop...**, and then enter the user name and password.</span></span>

![Bureau à distance de l’Explorateur de serveurs](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-to-get-the-rdp-file"></a><span data-ttu-id="cb918-142">Utiliser PowerShell pour récupérer le fichier RDP</span><span class="sxs-lookup"><span data-stu-id="cb918-142">Use PowerShell to get the RDP file</span></span>
<span data-ttu-id="cb918-143">Vous pouvez utiliser l’applet de commande [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) pour récupérer le fichier RDP.</span><span class="sxs-lookup"><span data-stu-id="cb918-143">You can use the [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet to retrieve the RDP file.</span></span> <span data-ttu-id="cb918-144">Vous pouvez ensuite utiliser le fichier RDP avec Connexion Bureau à distance pour accéder au service cloud.</span><span class="sxs-lookup"><span data-stu-id="cb918-144">You can then use the RDP file with Remote Desktop Connection to access the cloud service.</span></span>

### <a name="programmatically-download-the-rdp-file-through-the-service-management-rest-api"></a><span data-ttu-id="cb918-145">Télécharger par programme le fichier RDP via l’API REST de gestion des services</span><span class="sxs-lookup"><span data-stu-id="cb918-145">Programmatically download the RDP file through the Service Management REST API</span></span>
<span data-ttu-id="cb918-146">Vous pouvez utiliser l’opération REST [Télécharger le fichier RDP](https://msdn.microsoft.com/library/jj157183.aspx) pour télécharger le fichier RDP.</span><span class="sxs-lookup"><span data-stu-id="cb918-146">You can use the [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation to download the RDP file.</span></span>

## <a name="to-configure-remote-desktop-in-the-service-definition-file"></a><span data-ttu-id="cb918-147">Pour configurer le Bureau à distance dans le fichier de définition de service</span><span class="sxs-lookup"><span data-stu-id="cb918-147">To configure Remote Desktop in the service definition file</span></span>
<span data-ttu-id="cb918-148">Cette méthode vous permet d’activer le Bureau à distance pour l’application pendant le développement.</span><span class="sxs-lookup"><span data-stu-id="cb918-148">This method allows you to enable Remote Desktop for the application during development.</span></span> <span data-ttu-id="cb918-149">Cette approche exige que les mots de passe chiffrés soient stockés dans le fichier de configuration de service. Par ailleurs, toute mise à jour apportée à la configuration du Bureau à distance nécessite un redéploiement de l’application.</span><span class="sxs-lookup"><span data-stu-id="cb918-149">This approach requires encrypted passwords be stored in your service configuration file and any updates to the remote desktop configuration would require a redeployment of the application.</span></span> <span data-ttu-id="cb918-150">Pour éviter ces inconvénients, suivez l’approche basée sur l’extension Bureau à distance décrite précédemment.</span><span class="sxs-lookup"><span data-stu-id="cb918-150">If you want to avoid these downsides you should use the remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="cb918-151">Vous pouvez utiliser Visual Studio pour [activer une connexion Bureau à distance](../vs-azure-tools-remote-desktop-roles.md) à l’aide de l’approche basée sur le fichier de définition de service.</span><span class="sxs-lookup"><span data-stu-id="cb918-151">You can use Visual Studio to [enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using the service definition file approach.</span></span>  
<span data-ttu-id="cb918-152">La procédure ci-dessous décrit les modifications qui doivent être apportées aux fichiers de modèle de service pour activer le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="cb918-152">The steps below describe the changes needed to the service model files to enable remote desktop.</span></span> <span data-ttu-id="cb918-153">Visual Studio effectue automatiquement ces modifications lors de la publication.</span><span class="sxs-lookup"><span data-stu-id="cb918-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-the-connection-in-the-service-model"></a><span data-ttu-id="cb918-154">Configurer la connexion dans le modèle de service</span><span class="sxs-lookup"><span data-stu-id="cb918-154">Set up the connection in the service model</span></span>
<span data-ttu-id="cb918-155">Utilisez l’élément **Importations** pour importer les modules **RemoteAccess** et **RemoteForwarder** dans le fichier [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef).</span><span class="sxs-lookup"><span data-stu-id="cb918-155">Use the **Imports** element to import the **RemoteAccess** module and the **RemoteForwarder** module to the [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="cb918-156">Ce fichier de définition de service doit être similaire à l’exemple suivant avec l’élément `<Imports>` ajouté.</span><span class="sxs-lookup"><span data-stu-id="cb918-156">The service definition file should be similar to the following example with the `<Imports>` element added.</span></span>

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
<span data-ttu-id="cb918-157">Le fichier [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) doit être semblable à l’exemple suivant. Notez les éléments `<ConfigurationSettings>` et `<Certificates>`.</span><span class="sxs-lookup"><span data-stu-id="cb918-157">The [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar to the following example, note the `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="cb918-158">Le certificat spécifié doit être [téléchargé dans le service cloud](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="cb918-158">The Certificate specified must be [uploaded to the cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a><span data-ttu-id="cb918-159">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cb918-159">Additional Resources</span></span>
<span data-ttu-id="cb918-160">[Configuration des services cloud](cloud-services-how-to-configure.md)
[FAQ relative aux services cloud : Bureau à distance](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="cb918-160">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
