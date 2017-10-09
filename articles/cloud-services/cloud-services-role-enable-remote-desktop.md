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
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Activer une connexion Bureau à distance pour un rôle dans Azure Cloud Services

> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portail Azure Classic](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)

Vous pouvez activer une connexion Bureau à distance dans votre rôle pendant le développement en incluant les modules de bureau à distance hello dans votre définition de service, ou vous pouvez choisir tooenable Bureau à distance via hello Extension Bureau à distance. Hello approche par défaut est toouse hello Bureau à distance extension que vous pouvez activer le Bureau à distance même après que l’application hello est déployée sans tooredeploy votre application.

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a>Configurer le Bureau à distance à partir de hello portail Azure classic
Hello portail Azure classic utilise approche d’Extension Bureau à distance hello même après que l’application hello est déployée, vous pouvez activer Bureau à distance. Hello **configurer** page pour votre service cloud vous permet de tooenable Bureau à distance, modifier le compte d’administrateur local hello utilisé tooconnect toohello virtuels, les certificats hello utilisés dans l’authentification et définir hello date d’expiration.

1. Cliquez sur **Services de cloud computing**, cliquez sur nom hello du service de cloud hello, puis cliquez sur **configurer**.
2. Cliquez sur hello **distant** bouton bas hello.

    ![Services cloud à distance](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > toutes les instances de rôle sont redémarrées lorsque vous activez pour la première fois le Bureau à distance et cliquez sur OK (coche). tooprevent un redémarrage, le mot de passe hello hello certificat tooencrypt utilisé doit être installé sur le rôle de hello. tooprevent un redémarrage, [télécharger un certificat pour le service cloud hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , puis revenez toothis la boîte de dialogue.

3. Dans **rôles**, sélectionnez rôle hello souhaité tooupdate **tous les** pour tous les rôles.
4. Apportez hello modifications suivantes :

   * tooenable Bureau à distance, sélectionnez hello **activer le Bureau à distance** case à cocher. toodisable Bureau à distance, hello désactivez case à cocher.
   * Créer un compte toouse dans les connexions Bureau à distance toohello les instances de rôle.
   * Mettre à jour de mot de passe hello compte hello.
   * Sélectionnez un toouse certificat chargé pour l’authentification (à l’aide de téléchargement hello certificat **télécharger** sur hello **certificats** page) ou créer un nouveau certificat.
   * Modifier la date d’expiration de hello pour la configuration du Bureau à distance hello.

5. Lorsque les mises à jour de la configuration sont terminées, cliquez sur **OK** (coche).

## <a name="remote-into-role-instances"></a>À distance dans les instances de rôle
Une fois que Bureau à distance est activé sur les rôles de hello, vous pouvez à distance dans une instance de rôle via divers outils.

tooconnect tooa une instance de rôle à partir de hello portail Azure classic :

1. Cliquez sur **Instances** tooopen hello **Instances** page.
2. Sélectionnez une instance de rôle pour laquelle la fonctionnalité Bureau à distance est configurée.
3. Cliquez sur **connexion**et suivez le bureau de hello instructions tooopen hello.
4. Cliquez sur **ouvrir** , puis **Connect** toostart hello connexion Bureau à distance.

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a>Utilisez Visual Studio tooremote dans une instance de rôle
Dans l’Explorateur de serveurs Visual Studio :

1. Développez hello **Azure** > **Services de cloud computing** > **[nom du service cloud]** nœud.
2. Développez **Intermédiaire** ou **Production**.
3. Développez le rôle individuel de hello.
4. Cliquez sur une des instances de rôle hello, cliquez sur **se connecter à l’aide du Bureau à distance...** , puis entrez le nom d’utilisateur hello et le mot de passe.

![Bureau à distance de l’Explorateur de serveurs](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a>Utilisez le fichier RDP de PowerShell tooget hello
Vous pouvez utiliser hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) fichier RDP d’applet de commande tooretrieve hello. Vous pouvez ensuite utiliser fichier RDP de hello avec service de cloud de connexion Bureau à distance tooaccess hello.

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a>Télécharger le fichier RDP de hello via hello API REST Service Management par programmation
Vous pouvez utiliser hello [télécharger le fichier RDP](https://msdn.microsoft.com/library/jj157183.aspx) le fichier RDP hello reste opération toodownload.

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a>tooconfigure Bureau à distance dans le fichier de définition de service hello
Cette méthode vous permet de tooenable Bureau à distance pour une application hello lors du développement. Cette approche requiert des mots de passe chiffrés être stockées dans votre configuration du service fichier et toute configuration du Bureau à distance toohello mises à jour nécessitent un redéploiement de l’application hello. Si vous souhaitez tooavoid ces inconvénients, vous devez utiliser l’extension hello de bureau à distance en fonction d’approche décrite ci-dessus.  

Vous pouvez utiliser Visual Studio trop[activer une connexion Bureau à distance](../vs-azure-tools-remote-desktop-roles.md) à l’aide d’approche de fichiers de définition de service hello.  
les étapes de Hello ci-dessous décrivent hello modifications nécessaires toohello service modèle fichiers tooenable Bureau à distance. Visual Studio effectue automatiquement ces modifications lors de la publication.

### <a name="set-up-hello-connection-in-hello-service-model"></a>Configurer la connexion hello dans le modèle de service hello
Hello d’utilisation **importations** hello de tooimport élément **RemoteAccess** module et hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) fichier.

Hello fichier de définition de service doit être similaire toohello exemple avec hello suivant `<Imports>` élément ajouté.

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
Hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) fichier doit être similaire toohello l’exemple suivant, notez hello `<ConfigurationSettings>` et `<Certificates>` éléments. Hello certificat spécifié doit être [téléchargé le service de cloud computing toohello](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).

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


## <a name="additional-resources"></a>Ressources supplémentaires
[Comment tooConfigure Services de cloud computing](cloud-services-how-to-configure.md)
[Cloud FAQ - des services Bureau à distance](cloud-services-faq.md)
