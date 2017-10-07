---
title: "didacticiel de Bus REST aaaService à l’aide de relais de Azure | Documents Microsoft"
description: "Créez une simple application hôte Azure Service Bus Relay présentant une interface de type REST."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a>Didacticiel Azure WCF Relay REST

Ce didacticiel explique comment toobuild un relais Azure simple héberger application qui expose une interface basée sur REST. REST permet à un client web, comme un navigateur web, hello tooaccess les demandes API Service Bus via HTTP.

didacticiel de Hello utilise tooconstruct de modèle programmation hello REST de Windows Communication Foundation (WCF) un service REST sur le Bus de Service. Pour plus d’informations, consultez [modèle de programmation WCF REST](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) et [conception et implémentation de Services](/dotnet/framework/wcf/designing-and-implementing-services) Bonjour documentation WCF.

## <a name="step-1-create-a-namespace"></a>Étape 1 : Création d’un espace de noms

à l’aide de toobegin hello des fonctionnalités de relais dans Azure, vous devez d’abord créer un espace de noms de service. Un espace de noms fournit un conteneur d’étendue pour l’adressage des ressources Azure au sein de votre application. Suivez hello [ici les instructions](relay-create-namespace-portal.md) toocreate un espace de noms de relais.

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a>Étape 2 : Définir un toouse de contrat de service WCF de basée sur REST avec Azure relais

Lorsque vous créez un service WCF REST-style, vous devez définir le contrat de hello. contrat de Hello spécifie quelles opérations hello hôte prend en charge. Une opération de service peut être considérée comme une méthode de service web. Les contrats sont créés en définissant une interface C++, C# ou Visual Basic. Chaque méthode dans l’interface hello correspond l’opération de service spécifique tooa. Hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribut doit être appliqué tooeach interface et hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) l’attribut doit être appliqué tooeach opération. Si une méthode dans une interface qui possède hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) n’a pas de hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), cette méthode n’est pas exposée. code Hello utilisé pour ces tâches est indiqué dans l’exemple hello hello procédure.

Hello principale différence entre un contrat WCF et d’un contrat de type REST est Ajout de hello d’une propriété de toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx). Cette propriété permet de vous toomap une méthode dans la méthode d’interface tooa sur hello autre côté de l’interface de hello. Dans ce cas, nous allons utiliser [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink un tooHTTP de la méthode GET. Cela permet à Service Bus tooaccurately récupérer et d’interpréter les commandes envoyées toohello interface.

### <a name="toocreate-a-contract-with-an-interface"></a>toocreate un contrat avec une interface

1. Ouvrez Visual Studio en tant qu’administrateur : programme de hello avec le bouton droit dans hello **Démarrer** menu, puis sur **exécuter en tant qu’administrateur**.
2. Créez un projet d’application de console. Cliquez sur hello **fichier** menu et sélectionnez **nouveau**, puis sélectionnez **projet**. Bonjour **nouveau projet** boîte de dialogue, cliquez sur **Visual C#**, sélectionnez hello **Application Console** modèle et nommez-le **ImageListener**. Utiliser la valeur par défaut hello **emplacement**. Cliquez sur **OK** projet hello de toocreate.
3. Pour un projet C#, Visual Studio crée un fichier `Program.cs`. Cette classe contient vide `Main()` méthode, requis pour un toobuild de projet d’application console correctement.
4. Ajouter des références tooService Bus et **System.ServiceModel.dll** projet toohello en installant le package NuGet Service Bus de hello. Ce package ajoute automatiquement des références toohello Service Bus bibliothèques, ainsi que hello WCF **System.ServiceModel**. Dans l’Explorateur de solutions, cliquez sur hello **ImageListener** de projet, puis cliquez sur **gérer les Packages NuGet**. Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`. Cliquez sur **installer**et acceptez les conditions d’utilisation de hello.
5. Vous devez ajouter explicitement une référence trop**System.ServiceModel.Web.dll** toohello projet :
   
    a. Dans l’Explorateur de solutions, cliquez sur hello **références** dossier sous le dossier du projet hello, puis cliquez sur **ajouter une référence**.
   
    b. Bonjour **ajouter une référence** boîte de dialogue, cliquez sur hello **Framework** onglet sur le côté gauche de hello et Bonjour **recherche** , tapez **System.ServiceModel.Web** . Sélectionnez hello **System.ServiceModel.Web** case à cocher, puis cliquez sur **OK**.
6. Ajoutez hello suit `using` instructions haut hello du fichier Program.cs de hello.
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) est l’espace de noms hello qui active l’accès par programme des fonctions toobasic de WCF. Relais de WCF utilise de nombreux hello objets et les attributs des contrats de service WCF toodefine. Vous utiliserez cet espace de noms dans la plupart de vos applications de relais. De même, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) permettent de définir canal hello, qui est l’objet hello par le biais duquel vous communiquez avec le navigateur web du client relais d’Azure et hello. Enfin, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contient les types de hello qui vous permettent de toocreate les applications Web.
7. Renommer hello `ImageListener` espace de noms trop**Microsoft.ServiceBus.Samples**.
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. Directement après hello accolade de déclaration d’espace de noms hello, définir une nouvelle interface nommée **IImageContract** et appliquer hello **ServiceContractAttribute** interface de toohello d’attribut avec un valeur de `http://samples.microsoft.com/ServiceModel/Relay/`. valeur d’espace de noms Hello diffère de l’espace de noms hello que vous utilisez dans la portée de votre code hello. valeur d’espace de noms Hello est utilisée comme identificateur unique pour ce contrat et doit disposer d’informations de version. Pour plus d’informations, consultez la rubrique [Contrôle de version des services](http://go.microsoft.com/fwlink/?LinkID=180498). Une spécification explicite de l’espace de noms hello empêche l’espace de noms par défaut hello Ajout toohello le nom de contrat.
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. Au sein de hello `IImageContract` l’interface, déclarez une méthode pour hello d’opération unique hello `IImageContract` expose contrat Bonjour interface et appliquez hello `OperationContractAttribute` attribut méthode toohello que vous souhaitez tooexpose dans le cadre de hello public Service Bus contrat.
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. Bonjour **OperationContract** d’attribut, ajouter hello **WebGet** valeur.
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    Cette opération active hello tooroute de service de relais HTTP GET demande trop`GetImage`et hello tootranslate retournent des valeurs de `GetImage` dans une réponse HTTP GETRESPONSE. Plus loin dans le didacticiel de hello, vous allez utiliser un tooaccess de navigateur web de cette méthode et une image de hello toodisplay dans le navigateur de hello.
11. Directement après hello `IImageContract` définition, déclarez un canal qui hérite à la fois hello `IImageContract` et `IClientChannel` interfaces.
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    Un canal est l’objet WCF de hello via lequel client et le service de hello transmettent informations tooeach autres. Une version ultérieure, vous allez créer le canal de hello dans votre application hôte. Relais Azure utilise ensuite ce canal toopass hello requêtes GET HTTP hello navigateur tooyour **GetImage** implémentation. relais de Hello utilise également hello de hello canal tootake **GetImage** valeur de retour et la traduire en réponse HTTP GETRESPONSE du navigateur client hello.
12. À partir de hello **générer** menu, cliquez sur **générer la Solution** précision de hello tooconfirm de votre travail jusqu'à présent.

### <a name="example"></a>Exemple
Hello suivant de code montre une interface de base qui définit un contrat WCF relais.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a>Étape 3 : Implémenter un toouse de contrat de service WCF de basée sur REST Service Bus
Création d’un service de relais WCF de type REST nécessite que vous créez tout d’abord le contrat hello, qui est défini à l’aide d’une interface. étape suivante de Hello est interface de hello tooimplement. Cela implique la création d’une classe nommée **ImageService** qui implémente hello défini par l’utilisateur **IImageContract** interface. Une fois que vous implémentez le contrat de hello, vous configurez interface hello à l’aide d’un fichier App.config. fichier de configuration Hello contient les informations nécessaires pour l’application hello, telles que nom hello du service de hello, nom hello du contrat de hello et type hello du protocole est toocommunicate utilisé avec le service de relais hello. code de Hello utilisé pour ces tâches est fourni dans l’exemple hello hello procédure.

Comme les étapes précédentes hello, il existe très peu de différences entre l’implémentation d’un contrat de type REST et un contrat de relais de WCF.

### <a name="tooimplement-a-rest-style-service-bus-contract"></a>contrat de Service Bus tooimplement un style de REST
1. Créer une nouvelle classe nommée **ImageService** directement après la définition de hello Hello **IImageContract** interface. Hello **ImageService** classe implémente hello **IImageContract** interface.
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    Implémentations d’interface tooother similaires, vous pouvez implémenter la définition de hello dans un autre fichier. Toutefois, pour ce didacticiel, mise en œuvre hello s’affiche dans hello même fichier en tant que définition d’interface hello et `Main()` (méthode).
2. Appliquer hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribut toohello **IImageService** tooindicate de classe qui hello classe est une implémentation d’un contrat WCF.
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    Comme mentionné précédemment, cet espace de noms n'est pas un espace de noms standard. Au lieu de cela, il fait partie de la hello architecture WCF qui identifie le contrat de hello. Pour plus d’informations, consultez hello [les noms de contrat de données](https://msdn.microsoft.com/library/ms731045.aspx) rubrique Bonjour documentation WCF.
3. Ajoutez un projet de tooyour image .jpg.  
   
    Il s’agit d’une image par hello service Bonjour réception de navigateur. Cliquez avec le bouton droit sur votre projet, puis cliquez sur **Ajouter**. Cliquez ensuite sur **Élément existant**. Hello d’utilisation **ajouter un élément existant** tooan de toobrowse de boîte de dialogue appropriée .jpg, puis cliquez sur **ajouter**.
   
    Lorsque vous ajoutez un fichier de hello, assurez-vous que **tous les fichiers** est sélectionné dans toohello suivant de liste déroulante hello **nom de fichier :** champ. reste Hello de ce didacticiel part du principe que hello nom d’image de hello est « image.jpg ». Si vous avez un autre fichier, vous ont image de hello toorename, ou modifier votre toocompensate de code.
4. toomake que ce service en cours d’exécution de hello trouverez hello image fichier, en **l’Explorateur de solutions** avec le bouton droit de fichier d’image hello, puis cliquez sur **propriétés**. Bonjour **propriétés** volet, définissez **copier tooOutput active** trop**Copier si plus récent**.
5. Ajouter une référence toohello **System.Drawing.dll** toohello de l’assembly de projet et également ajouter suivant hello associés `using` instructions.  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. Bonjour **ImageService** classe, ajoutez hello suivants constructeur que les charges hello bitmap et prépare toosend toohello navigateur du client.
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. Directement après le code précédent de hello, ajoutez hello suivant **GetImage** méthode Bonjour **ImageService** message tooreturn HTTP de classe qui contient l’image de hello.
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    Cette implémentation utilise **MemoryStream** tooretrieve hello image et la préparer pour la diffusion en continu toohello navigateur. Démarre la position du flux hello à zéro, déclare le contenu du flux au format jpeg hello et transmet les informations de hello.
8. À partir de hello **générer** menu, cliquez sur **générer la Solution**.

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a>configuration de hello toodefine pour l’exécution du service web de hello sur Service Bus
1. Dans **l’Explorateur de solutions**, double-cliquez sur **App.config** tooopen dans l’éditeur de Visual Studio hello.
   
    Hello **App.config** fichier inclut le nom du service hello, point de terminaison (autrement dit, hello emplacement du relais de Azure expose pour que les clients et les hôtes toocommunicate entre eux) et liaison (type hello du protocole qui est utilisé toocommunicate). Hello principale différence ici est ce point de terminaison de service hello configuré fait référence tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) liaison.
2. Hello `<system.serviceModel>` XML est un élément WCF qui définit un ou plusieurs services. Ici, il est le point de terminaison et le nom du service utilisé toodefine hello. Bas hello hello `<system.serviceModel>` élément (mais toujours compris `<system.serviceModel>`), ajoutez un `<bindings>` élément ayant hello suivant le contenu. Définit les liaisons hello utilisées dans l’application hello. Vous pouvez définir plusieurs liaisons, mais pour ce didacticiel, vous n’en définissez qu'une seule.
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    code de précédent Hello définit un relais WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) la liaison avec **relayClientAuthenticationType** défini trop**aucun**. Ce paramètre indique qu'un point de terminaison utilisant cette liaison ne nécessite aucune information d'identification du client.
3. Après avoir hello `<bindings>` élément, ajouter un `<services>` élément. Les liaisons toohello similaires, vous pouvez définir plusieurs services dans un seul fichier de configuration. Toutefois, pour ce didacticiel, vous n’en définissez qu'un seul.
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    Cette étape configure un service qui utilise la valeur par défaut hello défini précédemment **webHttpRelayBinding**. Il utilise également la valeur par défaut hello **sbTokenProvider**, qui est défini dans l’étape suivante de hello.
4. Après avoir hello `<services>` élément, créer un `<behaviors>` élément avec hello suivant le contenu, en remplaçant « SAS_KEY » avec hello *Signature d’accès partagé* clé (SAS) vous avez préalablement obtenu à partir de hello [portail Azure ][Azure portal].
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. Toujours dans le fichier App.config, Bonjour `<appSettings>` élément, la valeur de chaîne de connexion entière de hello remplacer avec la chaîne de connexion hello obtenu à partir du portail de hello. 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. À partir de hello **générer** menu, cliquez sur **générer la Solution** toobuild hello ensemble de la solution.

### <a name="example"></a>Exemple
implémentation du service et de contrat hello pour un service basé sur REST qui est en cours d’exécution sur le Bus de Service à l’aide de hello affiche Hello suivant **WebHttpRelayBinding** liaison.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Hello suivant montre fichier App.config de hello associé hello service.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a>Étape 4 : Hôte hello basée sur REST de WCF service toouse Azure relais
Cette étape décrit comment toorun un site web de service à l’aide d’une application console avec WCF relais. Une liste complète de code hello écrite dans cette étape est fournie dans l’exemple hello hello procédure.

### <a name="toocreate-a-base-address-for-hello-service"></a>toocreate une adresse de base pour le service de hello
1. Bonjour `Main()` déclaration de fonction, de créer un espace de noms toostore variable hello de votre projet. Assurez-vous que tooreplace `yourNamespace` nom hello d’espace de noms de relais hello vous avez créé précédemment.
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    Service Bus utilise le nom hello de votre espace de noms de toocreate un URI unique.
2. Créer un `Uri` instance hello adresse de base du service de hello qui est basé sur l’espace de noms hello.
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a>toocreate et configurer l’hôte de service web hello
* Créer un hôte de service web hello, à l’aide d’adresse d’URI hello créé précédemment dans cette section.
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    hôte de service Hello est un objet hello WCF qui instancie l’application hôte de hello. Cet exemple transmet les type hello d’hôte souhaité toocreate (un **ImageService**), et également hello adresse auquel vous souhaitez que l’application hôte de hello tooexpose.

### <a name="toorun-hello-web-service-host"></a>hôte de service web toorun hello
1. Ouvrez hello service.
   
    ```csharp
    host.Open();
    ```
    service de Hello est en cours d’exécution.
2. Afficher un message indiquant que hello service s’exécute, et comment toostop hello service.
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Lorsque vous avez terminé, fermez l’hôte de service hello.
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a>Exemple
Hello, l’exemple suivant inclut le contrat de service hello et l’implémentation des étapes précédentes dans hello didacticiel et héberge hello le service dans une application console. Compilez hello après le code dans un fichier exécutable nommé ImageListener.exe.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a>Compiler le code hello
Après avoir généré la solution de hello, procédez comme hello suivant toorun hello application :

1. Appuyez sur **F5**, ou recherchez l’emplacement du fichier exécutable toohello (ImageListener\bin\Debug\ImageListener.exe), service de hello toorun. Conserver en cours d’exécution application hello, étape suivante de tooperform hello est nécessaire.
2. Copiez et collez l’adresse hello à partir de l’invite de commandes hello dans une image de hello toosee navigateur.
3. Lorsque vous avez terminé, appuyez sur **entrée** dans fenêtre d’invite de commandes hello tooclose hello application.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez créé une application qui utilise le service de relais Service Bus hello, consultez hello suivant toolearn articles plus sur Azure relais :

* [Azure Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [Vue d’ensemble d’Azure Relay](relay-what-is-it.md)
* [Comment toouse hello WCF de relais service avec .NET](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
