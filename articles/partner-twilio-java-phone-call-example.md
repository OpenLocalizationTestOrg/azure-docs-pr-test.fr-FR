---
title: "Appel téléphonique à partir de Twilio (Java) | Microsoft Docs"
description: "Apprenez à passer un appel téléphonique à partir d'une page web à l'aide de Twilio dans une application Java sur Azure."
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
ms.openlocfilehash: 04ecb80a2a9e15b549b47138caf71c7e64bda500
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="e8081-103">Exécution d'un appel téléphonique à l'aide de Twilio dans une application Java sur Azure</span><span class="sxs-lookup"><span data-stu-id="e8081-103">How to Make a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="e8081-104">L'exemple qui suit montre comment utiliser Twilio pour passer un appel depuis une page Web hébergée sur Azure.</span><span class="sxs-lookup"><span data-stu-id="e8081-104">The following example shows you how you can use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="e8081-105">L'application finale demande à l'utilisateur les valeurs de l'appel téléphonique, comme illustré dans la capture d'écran qui suit.</span><span class="sxs-lookup"><span data-stu-id="e8081-105">The resulting application will prompt the user for phone call values, as shown in the following screen shot.</span></span>

![Formulaire d'appel Azure avec Twilio et Java][twilio_java]

<span data-ttu-id="e8081-107">Pour utiliser le code de cette rubrique, vous devrez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e8081-107">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="e8081-108">Obtenir un compte Twilio et un jeton d'authentification.</span><span class="sxs-lookup"><span data-stu-id="e8081-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="e8081-109">Pour démarrer avec Twilio, évaluez les tarifs dans la page [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="e8081-109">To get started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="e8081-110">Vous pouvez vous inscrire à [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="e8081-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="e8081-111">Pour plus d’informations sur l’API fournie par Twilio, consultez [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="e8081-111">For information about the API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="e8081-112">Obtenir le JAR Twilio.</span><span class="sxs-lookup"><span data-stu-id="e8081-112">Obtain the Twilio JAR.</span></span> <span data-ttu-id="e8081-113">Sur [https://github.com/twilio/twilio-java][twilio_java_github], vous pouvez télécharger les sources GitHub et créer votre propre JAR, ou télécharger un JAR préconstruit (avec ou sans dépendances).</span><span class="sxs-lookup"><span data-stu-id="e8081-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="e8081-114">Le code de cette rubrique a été écrit avec un JAR préconstruit TwilioJava-3.3.8-with-dependencies.</span><span class="sxs-lookup"><span data-stu-id="e8081-114">The code in this topic was written using the pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="e8081-115">Ajouter le JAR à votre chemin de build Java.</span><span class="sxs-lookup"><span data-stu-id="e8081-115">Add the JAR to your Java build path.</span></span>
4. <span data-ttu-id="e8081-116">Si vous utilisez Eclipse pour créer cette application Java, ajoutez le JAR Twilio à votre fichier WAR de déploiement d'application à l'aide de la fonction d'assembly de déploiement d'Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e8081-116">If you are using Eclipse to create this Java application, include the Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="e8081-117">Si vous n'utilisez pas Eclipse pour créer cette application Java, assurez-vous que le JAR Twilio est inclus dans le même rôle Azure que votre application Java et qu'il est ajouté au chemin de classe de votre application.</span><span class="sxs-lookup"><span data-stu-id="e8081-117">If you are not using Eclipse to create this Java application, ensure the Twilio JAR is included within the same Azure role as your Java application, and added to the class path of your application.</span></span>
5. <span data-ttu-id="e8081-118">Vérifiez que le keystore cacerts de votre JDK contient le certificat ESCA (Equifax Secure Certificate Authority) avec l'empreinte MD5 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (le numéro de série est 35:DE:F4:CF et que l'empreinte de SHA1 est D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="e8081-118">Ensure your cacerts keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="e8081-119">Il s’agit du certificat d’autorité de certification pour le service [https://api.twilio.com][twilio_api_service], qui est appelé lorsque vous utilisez les API Twilio.</span><span class="sxs-lookup"><span data-stu-id="e8081-119">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="e8081-120">Pour plus d’informations sur l’ajout de ce certificat d’autorité de certification au magasin de cacert de votre JDK, consultez [Ajout d’un certificat pour le magasin de certificats d’autorité de certification Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="e8081-120">For information about adding this CA certificate to your JDK's cacert store, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="e8081-121">En outre, vous êtes familiarisé avec les informations à [création un Hello World Application à l’aide de la boîte à outils Azure pour Eclipse][azure_java_eclipse_hello_world], ou à d’autres techniques pour l’hébergement d’applications Java dans Azure si vous n’utilisez pas d’Eclipse, est fortement recommandé.</span><span class="sxs-lookup"><span data-stu-id="e8081-121">Additionally, familiarity with the information at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="e8081-122">Création d'un formulaire web pour passer un appel</span><span class="sxs-lookup"><span data-stu-id="e8081-122">Create a web form for making a call</span></span>
<span data-ttu-id="e8081-123">Le code qui suit présente la conception d'un formulaire Web qui extrait les données des utilisateurs pour passer un appel.</span><span class="sxs-lookup"><span data-stu-id="e8081-123">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="e8081-124">Pour cet exemple, un projet Web dynamique **TwilioCloud** a été créé et le fichier JSP **callform.jsp** a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="e8081-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

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
           <td><input type="text" size=400 name="callText" value="Hello. This is the call text. Good bye." />
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

## <a name="create-the-code-to-make-the-call"></a><span data-ttu-id="e8081-125">Création du code pour passer l'appel</span><span class="sxs-lookup"><span data-stu-id="e8081-125">Create the code to make the call</span></span>
<span data-ttu-id="e8081-126">Le code qui suit, qui est appelé une fois que l'utilisateur remplit le formulaire affiché par callform.jsp, crée le message d'appel et lance l'appel.</span><span class="sxs-lookup"><span data-stu-id="e8081-126">The following code, which is called when the user completes the form displayed by callform.jsp, creates the call message and generates the call.</span></span> <span data-ttu-id="e8081-127">Dans cet exemple, le fichier JSP s'appelle **makecall.jsp** et il a été ajouté au projet **TwilioCloud**.</span><span class="sxs-lookup"><span data-stu-id="e8081-127">For purposes of this example, the JSP file is named **makecall.jsp** and was added to the **TwilioCloud** project.</span></span> <span data-ttu-id="e8081-128">(Utilisez votre compte Twilio et votre jeton d'authentification plutôt que les valeurs par défaut utilisées dans **accountSID** et **authToken** dans le code qui suit.)</span><span class="sxs-lookup"><span data-stu-id="e8081-128">(Use your Twilio account and authentication token instead of the placeholder values assigned to **accountSID** and **authToken** in the code below.)</span></span>

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
         // of the placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of the Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve the account, used later to retrieve the CallFactory.
         Account account = client.getAccount();

         // Display the client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display the API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve the values entered by the user.
         String callTo = request.getParameter("callTo");  
         // The Outgoing Caller ID, used for the From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in the user's text with '%20', 
         // to make the text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using the Twilio message and the user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display the message URL.
         out.println("<p>");
         out.println("The URL is " + Url);
         out.println("</p>");

         // Place the call From, To and URL values into a hash map. 
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

<span data-ttu-id="e8081-129">En plus de passer l'appel, makecall.jsp affiche le point de terminaison Twilio, la version de l'API et l'état de l'appel.</span><span class="sxs-lookup"><span data-stu-id="e8081-129">In addition to making the call, makecall.jsp displays the Twilio endpoint, API version, and the call status.</span></span> <span data-ttu-id="e8081-130">La capture d'écran suivante présente un exemple :</span><span class="sxs-lookup"><span data-stu-id="e8081-130">An example is the following screen shot:</span></span>

![Réponse d'appel Azure avec Twilio et Java][twilio_java_response]

## <a name="run-the-application"></a><span data-ttu-id="e8081-132">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="e8081-132">Run the application</span></span>
<span data-ttu-id="e8081-133">Voici les principales étapes à suivre pour exécuter votre application ; Détails de ces étapes, consultez [création un Hello World Application à l’aide de la boîte à outils Azure pour Eclipse][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="e8081-133">Following are the high-level steps to run your application; details for these steps can be found at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="e8081-134">Exportez votre WAR TwilioCloud dans le dossier Azure **approot** .</span><span class="sxs-lookup"><span data-stu-id="e8081-134">Export your TwilioCloud WAR to the Azure **approot** folder.</span></span> 
2. <span data-ttu-id="e8081-135">Modifiez **startup.cmd** pour décompresser votre WAR TwilioCloud.</span><span class="sxs-lookup"><span data-stu-id="e8081-135">Modify **startup.cmd** to unzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="e8081-136">Compilez votre application pour l'émulateur de calcul.</span><span class="sxs-lookup"><span data-stu-id="e8081-136">Compile your application for the compute emulator.</span></span>
4. <span data-ttu-id="e8081-137">Démarrez votre déploiement dans l'émulateur de calcul.</span><span class="sxs-lookup"><span data-stu-id="e8081-137">Start your deployment in the compute emulator.</span></span>
5. <span data-ttu-id="e8081-138">Ouvrez un navigateur et accédez à l'adresse **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="e8081-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="e8081-139">Entrez les valeurs dans le formulaire, cliquez sur **Make this call**, puis consultez les résultats dans makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="e8081-139">Enter values in the form, click **Make this call**, and then see the results in makecall.jsp.</span></span>

<span data-ttu-id="e8081-140">Dès que vous êtes prêt pour le déploiement sur Azure, effectuez une recompilation pour déploiement dans le cloud, déployez sur Azure et accédez à l'adresse http://*votre_nom_hébergé*.cloudapp.net/TwilioCloud/callform.jsp dans le navigateur (remplacez *votre_nom_hébergé* par votre valeur).</span><span class="sxs-lookup"><span data-stu-id="e8081-140">When you are ready to deploy to Azure, recompile for deployment to the cloud, deploy to Azure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in the browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8081-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e8081-141">Next steps</span></span>
<span data-ttu-id="e8081-142">Ce code vous est fourni afin de vous présenter les fonctions de base de l'utilisation de Twilio dans Java sur Azure.</span><span class="sxs-lookup"><span data-stu-id="e8081-142">This code was provided to show you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="e8081-143">Avant d'effectuer le déploiement de production sur Azure, vous pouvez ajouter d'autres fonctionnalités telles que la gestion des erreurs.</span><span class="sxs-lookup"><span data-stu-id="e8081-143">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="e8081-144">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e8081-144">For example:</span></span>

* <span data-ttu-id="e8081-145">Au lieu d'utiliser un formulaire web, vous pouvez utiliser des objets blob de stockage Azure ou SQL Database pour stocker les numéros de téléphone et le texte des appels.</span><span class="sxs-lookup"><span data-stu-id="e8081-145">Instead of using a web form, you could use Azure storage blobs or SQL Database to store phone numbers and call text.</span></span> <span data-ttu-id="e8081-146">Pour plus d’informations sur l’utilisation d’objets BLOB de stockage Azure dans Java, consultez [comment utiliser le Service de stockage d’objets Blob à partir de Java][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="e8081-146">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="e8081-147">Pour plus d’informations sur l’utilisation de base de données SQL en Java, consultez [à l’aide de la base de données SQL en Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="e8081-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="e8081-148">Vous pouvez utiliser **RoleEnvironment.getConfigurationSettings** pour récupérer l’ID du compte Twilio et le jeton d’authentification à partir des paramètres de configuration de votre déploiement, au lieu de coder les valeurs en dur dans makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="e8081-148">You could use **RoleEnvironment.getConfigurationSettings** to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in makecall.jsp.</span></span> <span data-ttu-id="e8081-149">Pour plus d’informations sur la **RoleEnvironment** de classe, consultez [à l’aide de la bibliothèque Runtime du Service Azure dans JSP] [ azure_runtime_jsp] et la documentation du package Azure Service Runtime [http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="e8081-149">For information about the **RoleEnvironment** class, see [Using the Azure Service Runtime Library in JSP][azure_runtime_jsp] and the Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="e8081-150">Le code makecall.jsp affecte une URL fournie par Twilio, [http://twimlets.com/message][twimlet_message_url], à la **Url** variable.</span><span class="sxs-lookup"><span data-stu-id="e8081-150">The makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], to the **Url** variable.</span></span> <span data-ttu-id="e8081-151">Cette URL fournit une réponse TwiML (Twilio Markup Language) qui précise à Twilio comment traiter l'appel.</span><span class="sxs-lookup"><span data-stu-id="e8081-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how to proceed with the call.</span></span> <span data-ttu-id="e8081-152">Par exemple, le code TwiML renvoyé peut contenir un verbe **&lt;Say&gt;** qui fait que le texte est lu au destinataire de l'appel.</span><span class="sxs-lookup"><span data-stu-id="e8081-152">For example, the TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken to the call recipient.</span></span> <span data-ttu-id="e8081-153">Au lieu d’utiliser l’URL fournie par Twilio, vous pouvez générer votre propre service pour répondre à demande de Twilio ; Pour plus d’informations, consultez [comment Twilio d’utilisation de la voix et les fonctionnalités de SMS dans Java][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="e8081-153">Instead of using the Twilio-provided URL, you could build your own service to respond to Twilio's request; for more information, see [How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="e8081-154">Vous trouverez plus d’informations sur TwiML à [http://www.twilio.com/docs/api/twiml][twiml]et plus d’informations sur  **&lt;prononcer&gt;**  et sont accessibles à tous les autres Twilio [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="e8081-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="e8081-155">Consultez les instructions de sécurité Twilio dans la page [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="e8081-155">Read the Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="e8081-156">Pour plus d’informations sur Twilio, consultez la page [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="e8081-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="e8081-157">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e8081-157">See Also</span></span>
* <span data-ttu-id="e8081-158">[L’utilisation de Twilio pour la voix et les fonctionnalités de SMS dans Java][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="e8081-158">[How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="e8081-159">[Ajout d’un certificat au magasin de certificats d’autorité de certification Java][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="e8081-159">[Adding a Certificate to the Java CA Certificate Store][add_ca_cert]</span></span>

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
