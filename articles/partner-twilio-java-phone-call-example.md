---
title: "aaaHow tooMake un appel téléphonique à partir de Twilio (Java) | Documents Microsoft"
description: "Découvrez comment appeler des toomake un téléphone à partir d’une page web à l’aide de Twilio dans une application Java sur Azure."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="d6cd1-103">Comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application Java sur Azure</span><span class="sxs-lookup"><span data-stu-id="d6cd1-103">How tooMake a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="d6cd1-104">Hello suivant montre comment vous pouvez utiliser Twilio toomake un appel à partir d’une page web hébergée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-104">hello following example shows you how you can use Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="d6cd1-105">application qui en résulte Hello invite utilisateur hello pour les valeurs de l’appel téléphonique, comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-105">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Formulaire d'appel Azure avec Twilio et Java][twilio_java]

<span data-ttu-id="d6cd1-107">Éléments dont vous aurez besoin toodo hello code hello de toouse dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="d6cd1-107">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="d6cd1-108">Obtenir un compte Twilio et un jeton d'authentification.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="d6cd1-109">tooget main Twilio, évaluer la tarification au [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-109">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="d6cd1-110">Vous pouvez vous inscrire à [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="d6cd1-111">Pour plus d’informations sur l’API fournie par Twilio de hello, consultez [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-111">For information about hello API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="d6cd1-112">Obtenir hello Twilio JAR.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-112">Obtain hello Twilio JAR.</span></span> <span data-ttu-id="d6cd1-113">À [https://github.com/twilio/twilio-java][twilio_java_github], vous pouvez télécharger hello GitHub sources et créer vos propres JAR ou télécharger le fichier JAR prédéfini (avec ou sans dépendances).</span><span class="sxs-lookup"><span data-stu-id="d6cd1-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="d6cd1-114">code Hello dans cette rubrique a été écrite à l’aide de hello prégénérées TwilioJava 3.3.8 avec dépendances JAR.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-114">hello code in this topic was written using hello pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="d6cd1-115">Ajoutez tooyour JAR de hello chemin d’accès de build Java.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-115">Add hello JAR tooyour Java build path.</span></span>
4. <span data-ttu-id="d6cd1-116">Si vous utilisez Eclipse toocreate cette application Java, inclure hello Twilio JAR dans votre fichier de déploiement de l’application (WAR) à l’aide de la fonction d’assemblage déploiement d’Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-116">If you are using Eclipse toocreate this Java application, include hello Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="d6cd1-117">Si vous n’utilisez pas Eclipse toocreate cette application Java, assurez-vous de hello Twilio JAR est incluse dans hello même rôle Azure comme chemin de classe Java toohello application et ajout de votre application.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-117">If you are not using Eclipse toocreate this Java application, ensure hello Twilio JAR is included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>
5. <span data-ttu-id="d6cd1-118">Vérifiez votre magasin de clés cacerts contient le certificat d’autorité de certification Equifax Secure hello avec 67:CB:9 d’empreinte digitale MD5 D : C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello série est 35:DE:F4:CF et une empreinte digitale hello SHA1 D2:32:09:AD:23:D 3:14:23:21:74:E4:0 D : 7F:9 D : 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="d6cd1-118">Ensure your cacerts keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="d6cd1-119">Il s’agit hello autorité de certification pour hello [https://api.twilio.com] [ twilio_api_service] service, qui est appelée lors de l’utilisation de Twilio APIs.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-119">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="d6cd1-120">Pour plus d’informations sur l’ajout de magasin de certificats d’autorité de certification de cette JDK de tooyour cacert, consultez [Ajout d’un toohello certificat magasin de certificats d’autorité de certification Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-120">For information about adding this CA certificate tooyour JDK's cacert store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="d6cd1-121">En outre, vous êtes familiarisé avec les informations de hello au [création d’un Bonjour Hello World l’Application à l’aide de boîte à outils Azure pour Eclipse][azure_java_eclipse_hello_world], ou à d’autres techniques pour l’hébergement d’applications Java dans Azure if vous n’utilisez pas d’Eclipse, est fortement recommandé.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-121">Additionally, familiarity with hello information at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="d6cd1-122">Création d'un formulaire web pour passer un appel</span><span class="sxs-lookup"><span data-stu-id="d6cd1-122">Create a web form for making a call</span></span>
<span data-ttu-id="d6cd1-123">Hello suivant de code montre comment les données d’utilisateur de tooretrieve d’un appel du formulaire toocreate un site web.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-123">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="d6cd1-124">Pour cet exemple, un projet Web dynamique **TwilioCloud** a été créé et le fichier JSP **callform.jsp** a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="d6cd1-125">Créer l’appel de hello hello code toomake</span><span class="sxs-lookup"><span data-stu-id="d6cd1-125">Create hello code toomake hello call</span></span>
<span data-ttu-id="d6cd1-126">Bonjour code suivant, qui est appelée lorsque l’utilisateur de hello termine écran hello affiché par callform.jsp, crée le message d’appel hello et génère l’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-126">hello following code, which is called when hello user completes hello form displayed by callform.jsp, creates hello call message and generates hello call.</span></span> <span data-ttu-id="d6cd1-127">Pour les besoins de cet exemple, un fichier JSP hello est nommé **makecall.jsp** et a été ajoutée toohello **TwilioCloud** projet.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-127">For purposes of this example, hello JSP file is named **makecall.jsp** and was added toohello **TwilioCloud** project.</span></span> <span data-ttu-id="d6cd1-128">(Utilisez votre compte Twilio et l’authentification de jeton au lieu des valeurs d’espace réservé hello affectés trop**accountSID** et **jeton d’authentification** dans le code hello ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="d6cd1-128">(Use your Twilio account and authentication token instead of hello placeholder values assigned too**accountSID** and **authToken** in hello code below.)</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

<span data-ttu-id="d6cd1-129">En outre toomaking hello appel, makecall.jsp affiche le point de terminaison Twilio hello, version de l’API et l’état d’appel hello.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-129">In addition toomaking hello call, makecall.jsp displays hello Twilio endpoint, API version, and hello call status.</span></span> <span data-ttu-id="d6cd1-130">Par exemple, hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="d6cd1-130">An example is hello following screen shot:</span></span>

![Réponse d'appel Azure avec Twilio et Java][twilio_java_response]

## <a name="run-hello-application"></a><span data-ttu-id="d6cd1-132">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="d6cd1-132">Run hello application</span></span>
<span data-ttu-id="d6cd1-133">Suivantes sont hello toorun des étapes de votre application ; Détails de ces étapes, consultez [création d’un Bonjour Hello World l’Application à l’aide de boîte à outils Azure pour Eclipse][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-133">Following are hello high-level steps toorun your application; details for these steps can be found at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="d6cd1-134">Exporter votre toohello TwilioCloud WAR Azure **approot** dossier.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-134">Export your TwilioCloud WAR toohello Azure **approot** folder.</span></span> 
2. <span data-ttu-id="d6cd1-135">Modifier **startup.cmd** toounzip votre WAR TwilioCloud.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-135">Modify **startup.cmd** toounzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="d6cd1-136">Compilez votre application pour l’émulateur de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-136">Compile your application for hello compute emulator.</span></span>
4. <span data-ttu-id="d6cd1-137">Démarrer le déploiement dans l’émulateur de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-137">Start your deployment in hello compute emulator.</span></span>
5. <span data-ttu-id="d6cd1-138">Ouvrez un navigateur et accédez à l'adresse **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="d6cd1-139">Entrez les valeurs sous forme de hello, cliquez sur **effectuer cet appel**, puis consultez les résultats hello dans makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-139">Enter values in hello form, click **Make this call**, and then see hello results in makecall.jsp.</span></span>

<span data-ttu-id="d6cd1-140">Lorsque vous êtes prêt toodeploy tooAzure, recompilez pour le cloud de déploiement toohello, déployer tooAzure, et exécuter http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp dans le navigateur de hello (valeur de remplacement votre pour *your_hosted_name*).</span><span class="sxs-lookup"><span data-stu-id="d6cd1-140">When you are ready toodeploy tooAzure, recompile for deployment toohello cloud, deploy tooAzure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in hello browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6cd1-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6cd1-141">Next steps</span></span>
<span data-ttu-id="d6cd1-142">Ce code a été fourni tooshow vous fonctionnalités de base à l’aide de Twilio dans Java sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-142">This code was provided tooshow you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="d6cd1-143">Avant de déployer tooAzure en production, vous souhaiterez tooadd plus de gestion des erreurs ou d’autres fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-143">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="d6cd1-144">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6cd1-144">For example:</span></span>

* <span data-ttu-id="d6cd1-145">Au lieu d’utiliser un formulaire web, vous pourriez utiliser des objets BLOB de stockage Azure ou les numéros de téléphone toostore de base de données SQL et appeler le texte.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-145">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="d6cd1-146">Pour plus d’informations sur l’utilisation d’objets BLOB de stockage Azure dans Java, consultez [comment tooUse hello Service de stockage d’objets Blob à partir de Java][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-146">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="d6cd1-147">Pour plus d’informations sur l’utilisation de base de données SQL en Java, consultez [à l’aide de la base de données SQL en Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="d6cd1-148">Vous pouvez utiliser **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio l’ID de compte et l’authentification de jeton à partir des paramètres de configuration de votre déploiement, au lieu de coder en dur les valeurs hello dans makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-148">You could use **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in makecall.jsp.</span></span> <span data-ttu-id="d6cd1-149">Pour plus d’informations sur hello **RoleEnvironment** de classe, consultez [Using hello bibliothèque Runtime du Service Azure dans JSP] [ azure_runtime_jsp] et la documentation de package de Runtime du Service Azure hello à [http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-149">For information about hello **RoleEnvironment** class, see [Using hello Azure Service Runtime Library in JSP][azure_runtime_jsp] and hello Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="d6cd1-150">code de makecall.jsp Hello affecte une URL fournie par Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-150">hello makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable.</span></span> <span data-ttu-id="d6cd1-151">Cette URL permet une réponse de Twilio Markup Language (TwiML) qui informe Twilio comment tooproceed avec hello appeler.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="d6cd1-152">Par exemple, hello TwiML retourné peut contenir un  **&lt;prononcer&gt;**  verbe qui résulte dans le texte est prononcée toohello destinataire de l’appel.</span><span class="sxs-lookup"><span data-stu-id="d6cd1-152">For example, hello TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="d6cd1-153">Au lieu d’utiliser l’URL fournie par Twilio de hello, vous pouvez générer demande de votre propre tooTwilio toorespond service ; Pour plus d’informations, consultez [comment tooUse Twilio pour la voix et les fonctionnalités de SMS dans Java][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-153">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="d6cd1-154">Vous trouverez plus d’informations sur TwiML à [http://www.twilio.com/docs/api/twiml][twiml]et plus d’informations sur  **&lt;prononcer&gt;**  et sont accessibles à tous les autres Twilio [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="d6cd1-155">Lisez les consignes de sécurité hello Twilio à [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-155">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="d6cd1-156">Pour plus d’informations sur Twilio, consultez la page [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="d6cd1-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="d6cd1-157">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d6cd1-157">See Also</span></span>
* <span data-ttu-id="d6cd1-158">[Comment tooUse Twilio pour la voix et les fonctionnalités de SMS dans Java][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="d6cd1-158">[How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="d6cd1-159">[Ajout d’un certificat de toohello magasin de certificats d’autorité de certification Java][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="d6cd1-159">[Adding a Certificate toohello Java CA Certificate Store][add_ca_cert]</span></span>

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
