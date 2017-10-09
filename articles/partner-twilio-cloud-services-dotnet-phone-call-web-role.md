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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="126d5-104">Comment toomake un appel téléphonique à l’aide de Twilio dans un rôle web sur Azure</span><span class="sxs-lookup"><span data-stu-id="126d5-104">How toomake a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="126d5-105">Ce guide montre comment toouse Twilio toomake un appel à partir d’une page web hébergée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="126d5-105">This guide demonstrates how toouse Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="126d5-106">application résultante Hello invite hello utilisateur toomake un appel avec hello étant donné le nombre et le message, comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="126d5-106">hello resulting application prompts hello user toomake a call with hello given number and message, as shown in hello following screenshot.</span></span>

![Formulaire d'appel Azure utilisant Twilio et ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="126d5-108"><a name="twilio-prereqs"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="126d5-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="126d5-109">Vous devez suivant de hello toodo code hello de toouse dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="126d5-109">You will need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="126d5-110">Obtenir un compte Twilio et l’authentification jeton hello [Twilio Console][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="126d5-110">Acquire a Twilio account and authentication token from hello [Twilio Console][twilio_console].</span></span> <span data-ttu-id="126d5-111">tooget démarré avec Twilio, signe à [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="126d5-111">tooget started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="126d5-112">Pour vous faire une idée des tarifs, voir [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="126d5-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="126d5-113">Pour plus d’informations sur l’API fournie par Twilio de hello, consultez [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="126d5-113">For information about hello API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="126d5-114">Ajouter hello *bibliothèque .NET de Twilio* rôle web de tooyour.</span><span class="sxs-lookup"><span data-stu-id="126d5-114">Add hello *Twilio .NET libary* tooyour web role.</span></span> <span data-ttu-id="126d5-115">Consultez **projet de rôle web tooyour de bibliothèques de tooadd hello Twilio**, plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="126d5-115">See **tooadd hello Twilio libraries tooyour web role project**, later in this topic.</span></span>

<span data-ttu-id="126d5-116">Vous devriez également savoir comment créer un [rôle web de base sur Azure][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="126d5-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="126d5-117"><a name="howtocreateform"></a>Procédure : création d’un formulaire web pour établir un appel</span><span class="sxs-lookup"><span data-stu-id="126d5-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="126d5-118"><a id="use_nuget"></a>tooadd hello Twilio bibliothèques tooyour projet de rôle web :</span><span class="sxs-lookup"><span data-stu-id="126d5-118"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour web role project:</span></span>

1. <span data-ttu-id="126d5-119">Ouvrez votre solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="126d5-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="126d5-120">Cliquez avec le bouton droit sur **Références**.</span><span class="sxs-lookup"><span data-stu-id="126d5-120">Right-click **References**.</span></span>
3. <span data-ttu-id="126d5-121">Cliquez sur **Gérer les packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="126d5-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="126d5-122">Cliquez sur **En ligne**.</span><span class="sxs-lookup"><span data-stu-id="126d5-122">Click **Online**.</span></span>
5. <span data-ttu-id="126d5-123">Dans la zone en ligne de recherche hello, tapez *twilio*.</span><span class="sxs-lookup"><span data-stu-id="126d5-123">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="126d5-124">Cliquez sur **installer** sur le package de Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="126d5-124">Click **Install** on hello Twilio package.</span></span>

<span data-ttu-id="126d5-125">Hello suivant de code montre comment les données d’utilisateur de tooretrieve d’un appel du formulaire toocreate un site web.</span><span class="sxs-lookup"><span data-stu-id="126d5-125">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="126d5-126">Dans cet exemple, un rôle web ASP.NET appelé **TwilioCloud** est créé.</span><span class="sxs-lookup"><span data-stu-id="126d5-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

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

## <span data-ttu-id="126d5-127"><a id="howtocreatecode"></a>Comment : créer l’appel de hello hello code toomake</span><span class="sxs-lookup"><span data-stu-id="126d5-127"><a id="howtocreatecode"></a>How to: Create hello code toomake hello call</span></span>
<span data-ttu-id="126d5-128">Bonjour code suivant, qui est appelée lorsque l’utilisateur de hello termine le formulaire de hello, crée le message d’appel hello et génère l’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="126d5-128">hello following code, which is called when hello user completes hello form, creates hello call message and generates hello call.</span></span> <span data-ttu-id="126d5-129">Dans cet exemple, code de hello est exécuté dans le Gestionnaire d’événements onclick hello du bouton de hello sur le formulaire de hello.</span><span class="sxs-lookup"><span data-stu-id="126d5-129">In this example, hello code is run in hello onclick event handler of hello button on hello form.</span></span> <span data-ttu-id="126d5-130">(Utilisez votre compte Twilio et l’authentification de jeton au lieu des valeurs d’espace réservé hello affectés trop`accountSID` et `authToken` dans le code hello ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="126d5-130">(Use your Twilio account and authentication token instead of hello placeholder values assigned too`accountSID` and `authToken` in hello code below.)</span></span>

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

<span data-ttu-id="126d5-131">Hello est appelé, et point de terminaison Twilio hello, version de l’API et l’état d’appel hello sont affichés.</span><span class="sxs-lookup"><span data-stu-id="126d5-131">hello call is made, and hello Twilio endpoint, API version, and hello call status are displayed.</span></span> <span data-ttu-id="126d5-132">Hello suivant indique la capture d’écran production à partir d’un exemple d’exécution.</span><span class="sxs-lookup"><span data-stu-id="126d5-132">hello following screenshot shows output from a sample run.</span></span>

![Réponse Azure à un appel à l'aide de Twilio et ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="126d5-134">Pour plus d’informations sur TwiML, voir [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="126d5-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="126d5-135">Pour plus d’informations sur &lt;Say&gt; et d’autres verbes Twilio, voir [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="126d5-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="126d5-136"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="126d5-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="126d5-137">Ce code a été fourni tooshow vous fonctionnalités de base à l’aide de Twilio dans un rôle de web ASP.NET sur Azure.</span><span class="sxs-lookup"><span data-stu-id="126d5-137">This code was provided tooshow you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="126d5-138">Avant de déployer tooAzure en production, vous souhaiterez tooadd plus de gestion des erreurs ou d’autres fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="126d5-138">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="126d5-139">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="126d5-139">For example:</span></span>

* <span data-ttu-id="126d5-140">Au lieu d’utiliser un formulaire web, utilisez le stockage Blob Azure ou un numéro de téléphone de base de données SQL Azure instance toostore et a appeler le texte.</span><span class="sxs-lookup"><span data-stu-id="126d5-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance toostore phone numbers and call text.</span></span> <span data-ttu-id="126d5-141">Pour plus d’informations sur l’utilisation d’objets BLOB dans Azure, consultez [comment toouse hello service de stockage d’objets Blob Azure dans .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="126d5-141">For information about using Blobs in Azure, see [How toouse hello Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="126d5-142">Pour plus d’informations sur l’utilisation de base de données SQL, consultez [comment toouse SQL Azure de base de données dans les applications .NET][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="126d5-142">For information about using SQL Database, see [How toouse Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="126d5-143">Vous pouvez utiliser `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio l’ID de compte et l’authentification de jeton à partir des paramètres de configuration de votre déploiement, au lieu de coder en dur les valeurs hello dans votre formulaire.</span><span class="sxs-lookup"><span data-stu-id="126d5-143">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in your form.</span></span> <span data-ttu-id="126d5-144">Pour plus d’informations sur hello `RoleEnvironment` de classe, consultez [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="126d5-144">For information about hello `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="126d5-145">Lisez les consignes de sécurité hello Twilio à [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="126d5-145">Read hello Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="126d5-146">Pour en savoir plus sur Twilio, voir [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="126d5-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="126d5-147"><a name="seealso"></a>Voir aussi</span><span class="sxs-lookup"><span data-stu-id="126d5-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="126d5-148">Comment toouse Twilio pour les fonctionnalités de voix et de SMS à partir de Azure</span><span class="sxs-lookup"><span data-stu-id="126d5-148">How toouse Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

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
