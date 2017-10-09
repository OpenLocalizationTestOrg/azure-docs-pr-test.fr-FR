---
title: "aaaEnable Bureau à distance dans un Service Cloud Azure | Documents Microsoft"
description: "Tooconfigure votre azure cloud service connexions Bureau à distance tooallow d’application"
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
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="4a621-103">Activer une connexion Bureau à distance pour un rôle dans Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="4a621-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a621-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4a621-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="4a621-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="4a621-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="4a621-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a621-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="4a621-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4a621-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="4a621-108">Vous pouvez activer une connexion Bureau à distance dans votre rôle pendant le développement en incluant les modules de bureau à distance hello dans votre définition de service, ou vous pouvez choisir tooenable Bureau à distance via hello Extension Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="4a621-108">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="4a621-109">Hello approche par défaut est toouse hello Bureau à distance extension que vous pouvez activer le Bureau à distance même après que l’application hello est déployée sans tooredeploy votre application.</span><span class="sxs-lookup"><span data-stu-id="4a621-109">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a><span data-ttu-id="4a621-110">Configurer le Bureau à distance à partir de hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="4a621-110">Configure Remote Desktop from hello Azure classic portal</span></span>
<span data-ttu-id="4a621-111">Hello portail Azure classic utilise approche d’Extension Bureau à distance hello même après que l’application hello est déployée, vous pouvez activer Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="4a621-111">hello Azure classic portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="4a621-112">Hello **configurer** page pour votre service cloud vous permet de tooenable Bureau à distance, modifier le compte d’administrateur local hello utilisé tooconnect toohello virtuels, les certificats hello utilisés dans l’authentification et définir hello date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="4a621-112">hello **Configure** page for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="4a621-113">Cliquez sur **Services de cloud computing**, cliquez sur nom hello du service de cloud hello, puis cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="4a621-113">Click **Cloud Services**, click hello name of hello cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="4a621-114">Cliquez sur hello **distant** bouton bas hello.</span><span class="sxs-lookup"><span data-stu-id="4a621-114">Click hello **Remote** button at hello bottom.</span></span>

    ![Services cloud à distance](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="4a621-116">toutes les instances de rôle sont redémarrées lorsque vous activez pour la première fois le Bureau à distance et cliquez sur OK (coche).</span><span class="sxs-lookup"><span data-stu-id="4a621-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="4a621-117">tooprevent un redémarrage, le mot de passe hello hello certificat tooencrypt utilisé doit être installé sur le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="4a621-117">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="4a621-118">tooprevent un redémarrage, [télécharger un certificat pour le service cloud hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , puis revenez toothis la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4a621-118">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>

3. <span data-ttu-id="4a621-119">Dans **rôles**, sélectionnez rôle hello souhaité tooupdate **tous les** pour tous les rôles.</span><span class="sxs-lookup"><span data-stu-id="4a621-119">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>
4. <span data-ttu-id="4a621-120">Apportez hello modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="4a621-120">Make any of hello following changes:</span></span>

   * <span data-ttu-id="4a621-121">tooenable Bureau à distance, sélectionnez hello **activer le Bureau à distance** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="4a621-121">tooenable Remote Desktop, select hello **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="4a621-122">toodisable Bureau à distance, hello désactivez case à cocher.</span><span class="sxs-lookup"><span data-stu-id="4a621-122">toodisable Remote Desktop, clear hello check box.</span></span>
   * <span data-ttu-id="4a621-123">Créer un compte toouse dans les connexions Bureau à distance toohello les instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="4a621-123">Create an account toouse in Remote Desktop connections toohello role instances.</span></span>
   * <span data-ttu-id="4a621-124">Mettre à jour de mot de passe hello compte hello.</span><span class="sxs-lookup"><span data-stu-id="4a621-124">Update hello password for hello existing account.</span></span>
   * <span data-ttu-id="4a621-125">Sélectionnez un toouse certificat chargé pour l’authentification (à l’aide de téléchargement hello certificat **télécharger** sur hello **certificats** page) ou créer un nouveau certificat.</span><span class="sxs-lookup"><span data-stu-id="4a621-125">Select an uploaded certificate toouse for authentication (upload hello certificate using **Upload** on hello **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="4a621-126">Modifier la date d’expiration de hello pour la configuration du Bureau à distance hello.</span><span class="sxs-lookup"><span data-stu-id="4a621-126">Change hello expiration date for hello Remote Desktop configuration.</span></span>

5. <span data-ttu-id="4a621-127">Lorsque les mises à jour de la configuration sont terminées, cliquez sur **OK** (coche).</span><span class="sxs-lookup"><span data-stu-id="4a621-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="4a621-128">À distance dans les instances de rôle</span><span class="sxs-lookup"><span data-stu-id="4a621-128">Remote into role instances</span></span>
<span data-ttu-id="4a621-129">Une fois que Bureau à distance est activé sur les rôles de hello, vous pouvez à distance dans une instance de rôle via divers outils.</span><span class="sxs-lookup"><span data-stu-id="4a621-129">Once Remote Desktop is enabled on hello roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="4a621-130">tooconnect tooa une instance de rôle à partir de hello portail Azure classic :</span><span class="sxs-lookup"><span data-stu-id="4a621-130">tooconnect tooa role instance from hello Azure classic portal:</span></span>

1. <span data-ttu-id="4a621-131">Cliquez sur **Instances** tooopen hello **Instances** page.</span><span class="sxs-lookup"><span data-stu-id="4a621-131">Click **Instances** tooopen hello **Instances** page.</span></span>
2. <span data-ttu-id="4a621-132">Sélectionnez une instance de rôle pour laquelle la fonctionnalité Bureau à distance est configurée.</span><span class="sxs-lookup"><span data-stu-id="4a621-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="4a621-133">Cliquez sur **connexion**et suivez le bureau de hello instructions tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="4a621-133">Click **Connect**, and follow hello instructions tooopen hello desktop.</span></span>
4. <span data-ttu-id="4a621-134">Cliquez sur **ouvrir** , puis **Connect** toostart hello connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="4a621-134">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a><span data-ttu-id="4a621-135">Utilisez Visual Studio tooremote dans une instance de rôle</span><span class="sxs-lookup"><span data-stu-id="4a621-135">Use Visual Studio tooremote into a role instance</span></span>
<span data-ttu-id="4a621-136">Dans l’Explorateur de serveurs Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="4a621-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="4a621-137">Développez hello **Azure** > **Services de cloud computing** > **[nom du service cloud]** nœud.</span><span class="sxs-lookup"><span data-stu-id="4a621-137">Expand hello **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="4a621-138">Développez **Intermédiaire** ou **Production**.</span><span class="sxs-lookup"><span data-stu-id="4a621-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="4a621-139">Développez le rôle individuel de hello.</span><span class="sxs-lookup"><span data-stu-id="4a621-139">Expand hello individual role.</span></span>
4. <span data-ttu-id="4a621-140">Cliquez sur une des instances de rôle hello, cliquez sur **se connecter à l’aide du Bureau à distance...** , puis entrez le nom d’utilisateur hello et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4a621-140">Right-click one of hello role instances, click **Connect using Remote Desktop...**, and then enter hello user name and password.</span></span>

![Bureau à distance de l’Explorateur de serveurs](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a><span data-ttu-id="4a621-142">Utilisez le fichier RDP de PowerShell tooget hello</span><span class="sxs-lookup"><span data-stu-id="4a621-142">Use PowerShell tooget hello RDP file</span></span>
<span data-ttu-id="4a621-143">Vous pouvez utiliser hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) fichier RDP d’applet de commande tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="4a621-143">You can use hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP file.</span></span> <span data-ttu-id="4a621-144">Vous pouvez ensuite utiliser fichier RDP de hello avec service de cloud de connexion Bureau à distance tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="4a621-144">You can then use hello RDP file with Remote Desktop Connection tooaccess hello cloud service.</span></span>

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a><span data-ttu-id="4a621-145">Télécharger le fichier RDP de hello via hello API REST Service Management par programmation</span><span class="sxs-lookup"><span data-stu-id="4a621-145">Programmatically download hello RDP file through hello Service Management REST API</span></span>
<span data-ttu-id="4a621-146">Vous pouvez utiliser hello [télécharger le fichier RDP](https://msdn.microsoft.com/library/jj157183.aspx) le fichier RDP hello reste opération toodownload.</span><span class="sxs-lookup"><span data-stu-id="4a621-146">You can use hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation toodownload hello RDP file.</span></span>

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a><span data-ttu-id="4a621-147">tooconfigure Bureau à distance dans le fichier de définition de service hello</span><span class="sxs-lookup"><span data-stu-id="4a621-147">tooconfigure Remote Desktop in hello service definition file</span></span>
<span data-ttu-id="4a621-148">Cette méthode vous permet de tooenable Bureau à distance pour une application hello lors du développement.</span><span class="sxs-lookup"><span data-stu-id="4a621-148">This method allows you tooenable Remote Desktop for hello application during development.</span></span> <span data-ttu-id="4a621-149">Cette approche requiert des mots de passe chiffrés être stockées dans votre configuration du service fichier et toute configuration du Bureau à distance toohello mises à jour nécessitent un redéploiement de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4a621-149">This approach requires encrypted passwords be stored in your service configuration file and any updates toohello remote desktop configuration would require a redeployment of hello application.</span></span> <span data-ttu-id="4a621-150">Si vous souhaitez tooavoid ces inconvénients, vous devez utiliser l’extension hello de bureau à distance en fonction d’approche décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4a621-150">If you want tooavoid these downsides you should use hello remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="4a621-151">Vous pouvez utiliser Visual Studio trop[activer une connexion Bureau à distance](../vs-azure-tools-remote-desktop-roles.md) à l’aide d’approche de fichiers de définition de service hello.</span><span class="sxs-lookup"><span data-stu-id="4a621-151">You can use Visual Studio too[enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using hello service definition file approach.</span></span>  
<span data-ttu-id="4a621-152">les étapes de Hello ci-dessous décrivent hello modifications nécessaires toohello service modèle fichiers tooenable Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="4a621-152">hello steps below describe hello changes needed toohello service model files tooenable remote desktop.</span></span> <span data-ttu-id="4a621-153">Visual Studio effectue automatiquement ces modifications lors de la publication.</span><span class="sxs-lookup"><span data-stu-id="4a621-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-hello-connection-in-hello-service-model"></a><span data-ttu-id="4a621-154">Configurer la connexion hello dans le modèle de service hello</span><span class="sxs-lookup"><span data-stu-id="4a621-154">Set up hello connection in hello service model</span></span>
<span data-ttu-id="4a621-155">Hello d’utilisation **importations** hello de tooimport élément **RemoteAccess** module et hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) fichier.</span><span class="sxs-lookup"><span data-stu-id="4a621-155">Use hello **Imports** element tooimport hello **RemoteAccess** module and hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="4a621-156">Hello fichier de définition de service doit être similaire toohello exemple avec hello suivant `<Imports>` élément ajouté.</span><span class="sxs-lookup"><span data-stu-id="4a621-156">hello service definition file should be similar toohello following example with hello `<Imports>` element added.</span></span>

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
<span data-ttu-id="4a621-157">Hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) fichier doit être similaire toohello l’exemple suivant, notez hello `<ConfigurationSettings>` et `<Certificates>` éléments.</span><span class="sxs-lookup"><span data-stu-id="4a621-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar toohello following example, note hello `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="4a621-158">Hello certificat spécifié doit être [téléchargé le service de cloud computing toohello](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="4a621-158">hello Certificate specified must be [uploaded toohello cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

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


## <a name="additional-resources"></a><span data-ttu-id="4a621-159">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4a621-159">Additional Resources</span></span>
<span data-ttu-id="4a621-160">[Comment tooConfigure Services de cloud computing](cloud-services-how-to-configure.md)
[Cloud FAQ - des services Bureau à distance](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="4a621-160">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
