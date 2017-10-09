---
title: "aaaHow toomake un appel téléphonique à partir de Twilio (.NET) | Documents Microsoft"
description: "Découvrez comment toomake un appel téléphonique et envoyer un SMS de message avec le service de l’API de Twilio hello sur Azure. Exemples de code écrits en .NET."
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 857d89961c563a51fef944f4a72828036af79b43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a>Comment toomake un appel téléphonique à l’aide de Twilio dans un rôle web sur Azure
Ce guide montre comment toouse Twilio toomake un appel à partir d’une page web hébergée dans Azure. application résultante Hello invite hello utilisateur toomake un appel avec hello étant donné le nombre et le message, comme indiqué dans hello suivant capture d’écran.

![Formulaire d'appel Azure utilisant Twilio et ASP.NET][twilio_dotnet_basic_form]

## <a name="twilio-prereqs"></a>Configuration requise
Vous devez suivant de hello toodo code hello de toouse dans cette rubrique :

1. Obtenir un compte Twilio et l’authentification jeton hello [Twilio Console][twilio_console]. tooget démarré avec Twilio, signe à [https://www.twilio.com/try-twilio][try_twilio]. Pour vous faire une idée des tarifs, voir [http://www.twilio.com/pricing][twilio_pricing]. Pour plus d’informations sur l’API fournie par Twilio de hello, consultez [http://www.twilio.com/voice/api][twilio_api].
2. Ajouter hello *bibliothèque .NET de Twilio* rôle web de tooyour. Consultez **projet de rôle web tooyour de bibliothèques de tooadd hello Twilio**, plus loin dans cette rubrique.

Vous devriez également savoir comment créer un [rôle web de base sur Azure][azure_webroles_get_started].

## <a name="howtocreateform"></a>Procédure : création d’un formulaire web pour établir un appel
<a id="use_nuget"></a>tooadd hello Twilio bibliothèques tooyour projet de rôle web :

1. Ouvrez votre solution dans Visual Studio.
2. Cliquez avec le bouton droit sur **Références**.
3. Cliquez sur **Gérer les packages NuGet...**
4. Cliquez sur **En ligne**.
5. Dans la zone en ligne de recherche hello, tapez *twilio*.
6. Cliquez sur **installer** sur le package de Twilio hello.

Hello suivant de code montre comment les données d’utilisateur de tooretrieve d’un appel du formulaire toocreate un site web. Dans cet exemple, un rôle web ASP.NET appelé **TwilioCloud** est créé.

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <a id="howtocreatecode"></a>Comment : créer l’appel de hello hello code toomake
Bonjour code suivant, qui est appelée lorsque l’utilisateur de hello termine le formulaire de hello, crée le message d’appel hello et génère l’appel de hello. Dans cet exemple, code de hello est exécuté dans le Gestionnaire d’événements onclick hello du bouton de hello sur le formulaire de hello. (Utilisez votre compte Twilio et l’authentification de jeton au lieu des valeurs d’espace réservé hello affectés trop`accountSID` et `authToken` dans le code hello ci-dessous.)

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // hello placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of hello Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve hello account, used later tooretrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve hello values entered by hello user.
                var too= PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using hello Twilio message and hello user-entered
                // text. You must replace spaces in hello user's text with '%20'
                // toomake hello text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display hello endpoint, API version, and hello URL for hello message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"hello URL is {url}");

                // Place hello call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

Hello est appelé, et point de terminaison Twilio hello, version de l’API et l’état d’appel hello sont affichés. Hello suivant indique la capture d’écran production à partir d’un exemple d’exécution.

![Réponse Azure à un appel à l'aide de Twilio et ASP.NET][twilio_dotnet_basic_form_output]

Pour plus d’informations sur TwiML, voir [http://www.twilio.com/docs/api/twiml][twiml]. Pour plus d’informations sur &lt;Say&gt; et d’autres verbes Twilio, voir [http://www.twilio.com/docs/api/twiml/say][twilio_say].

## <a id="nextsteps"></a>Étapes suivantes
Ce code a été fourni tooshow vous fonctionnalités de base à l’aide de Twilio dans un rôle de web ASP.NET sur Azure. Avant de déployer tooAzure en production, vous souhaiterez tooadd plus de gestion des erreurs ou d’autres fonctionnalités. Par exemple :

* Au lieu d’utiliser un formulaire web, utilisez le stockage Blob Azure ou un numéro de téléphone de base de données SQL Azure instance toostore et a appeler le texte. Pour plus d’informations sur l’utilisation d’objets BLOB dans Azure, consultez [comment toouse hello service de stockage d’objets Blob Azure dans .NET][howto_blob_storage_dotnet]. Pour plus d’informations sur l’utilisation de base de données SQL, consultez [comment toouse SQL Azure de base de données dans les applications .NET][howto_sql_azure_dotnet].
* Vous pouvez utiliser `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio l’ID de compte et l’authentification de jeton à partir des paramètres de configuration de votre déploiement, au lieu de coder en dur les valeurs hello dans votre formulaire. Pour plus d’informations sur hello `RoleEnvironment` de classe, consultez [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].
* Lisez les consignes de sécurité hello Twilio à [https://www.twilio.com/docs/security][twilio_docs_security].
* Pour en savoir plus sur Twilio, voir [https://www.twilio.com/docs][twilio_docs].

## <a name="seealso"></a>Voir aussi
* [Comment toouse Twilio pour les fonctionnalités de voix et de SMS à partir de Azure](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
