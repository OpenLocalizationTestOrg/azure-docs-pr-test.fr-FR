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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a>Comment tooMake un Twilio à l’aide d’un appel téléphonique dans une Application Java sur Azure
Hello suivant montre comment vous pouvez utiliser Twilio toomake un appel à partir d’une page web hébergée dans Azure. application qui en résulte Hello invite utilisateur hello pour les valeurs de l’appel téléphonique, comme indiqué dans hello suivant capture d’écran.

![Formulaire d'appel Azure avec Twilio et Java][twilio_java]

Éléments dont vous aurez besoin toodo hello code hello de toouse dans cette rubrique :

1. Obtenir un compte Twilio et un jeton d'authentification. tooget main Twilio, évaluer la tarification au [http://www.twilio.com/pricing][twilio_pricing]. Vous pouvez vous inscrire à [https://www.twilio.com/try-twilio][try_twilio]. Pour plus d’informations sur l’API fournie par Twilio de hello, consultez [http://www.twilio.com/api][twilio_api].
2. Obtenir hello Twilio JAR. À [https://github.com/twilio/twilio-java][twilio_java_github], vous pouvez télécharger hello GitHub sources et créer vos propres JAR ou télécharger le fichier JAR prédéfini (avec ou sans dépendances).
   code Hello dans cette rubrique a été écrite à l’aide de hello prégénérées TwilioJava 3.3.8 avec dépendances JAR.
3. Ajoutez tooyour JAR de hello chemin d’accès de build Java.
4. Si vous utilisez Eclipse toocreate cette application Java, inclure hello Twilio JAR dans votre fichier de déploiement de l’application (WAR) à l’aide de la fonction d’assemblage déploiement d’Eclipse. Si vous n’utilisez pas Eclipse toocreate cette application Java, assurez-vous de hello Twilio JAR est incluse dans hello même rôle Azure comme chemin de classe Java toohello application et ajout de votre application.
5. Vérifiez votre magasin de clés cacerts contient le certificat d’autorité de certification Equifax Secure hello avec 67:CB:9 d’empreinte digitale MD5 D : C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello série est 35:DE:F4:CF et une empreinte digitale hello SHA1 D2:32:09:AD:23:D 3:14:23:21:74:E4:0 D : 7F:9 D : 62:13:97:86:63:3A). Il s’agit hello autorité de certification pour hello [https://api.twilio.com] [ twilio_api_service] service, qui est appelée lors de l’utilisation de Twilio APIs. Pour plus d’informations sur l’ajout de magasin de certificats d’autorité de certification de cette JDK de tooyour cacert, consultez [Ajout d’un toohello certificat magasin de certificats d’autorité de certification Java][add_ca_cert].

En outre, vous êtes familiarisé avec les informations de hello au [création d’un Bonjour Hello World l’Application à l’aide de boîte à outils Azure pour Eclipse][azure_java_eclipse_hello_world], ou à d’autres techniques pour l’hébergement d’applications Java dans Azure if vous n’utilisez pas d’Eclipse, est fortement recommandé.

## <a name="create-a-web-form-for-making-a-call"></a>Création d'un formulaire web pour passer un appel
Hello suivant de code montre comment les données d’utilisateur de tooretrieve d’un appel du formulaire toocreate un site web. Pour cet exemple, un projet Web dynamique **TwilioCloud** a été créé et le fichier JSP **callform.jsp** a été ajouté.

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

## <a name="create-hello-code-toomake-hello-call"></a>Créer l’appel de hello hello code toomake
Bonjour code suivant, qui est appelée lorsque l’utilisateur de hello termine écran hello affiché par callform.jsp, crée le message d’appel hello et génère l’appel de hello. Pour les besoins de cet exemple, un fichier JSP hello est nommé **makecall.jsp** et a été ajoutée toohello **TwilioCloud** projet. (Utilisez votre compte Twilio et l’authentification de jeton au lieu des valeurs d’espace réservé hello affectés trop**accountSID** et **jeton d’authentification** dans le code hello ci-dessous.)

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

En outre toomaking hello appel, makecall.jsp affiche le point de terminaison Twilio hello, version de l’API et l’état d’appel hello. Par exemple, hello suivant capture d’écran :

![Réponse d'appel Azure avec Twilio et Java][twilio_java_response]

## <a name="run-hello-application"></a>Exécutez l’application hello
Suivantes sont hello toorun des étapes de votre application ; Détails de ces étapes, consultez [création d’un Bonjour Hello World l’Application à l’aide de boîte à outils Azure pour Eclipse][azure_java_eclipse_hello_world].

1. Exporter votre toohello TwilioCloud WAR Azure **approot** dossier. 
2. Modifier **startup.cmd** toounzip votre WAR TwilioCloud.
3. Compilez votre application pour l’émulateur de calcul hello.
4. Démarrer le déploiement dans l’émulateur de calcul hello.
5. Ouvrez un navigateur et accédez à l'adresse **http://localhost:8080/TwilioCloud/callform.jsp**.
6. Entrez les valeurs sous forme de hello, cliquez sur **effectuer cet appel**, puis consultez les résultats hello dans makecall.jsp.

Lorsque vous êtes prêt toodeploy tooAzure, recompilez pour le cloud de déploiement toohello, déployer tooAzure, et exécuter http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp dans le navigateur de hello (valeur de remplacement votre pour *your_hosted_name*).

## <a name="next-steps"></a>Étapes suivantes
Ce code a été fourni tooshow vous fonctionnalités de base à l’aide de Twilio dans Java sur Azure. Avant de déployer tooAzure en production, vous souhaiterez tooadd plus de gestion des erreurs ou d’autres fonctionnalités. Par exemple :

* Au lieu d’utiliser un formulaire web, vous pourriez utiliser des objets BLOB de stockage Azure ou les numéros de téléphone toostore de base de données SQL et appeler le texte. Pour plus d’informations sur l’utilisation d’objets BLOB de stockage Azure dans Java, consultez [comment tooUse hello Service de stockage d’objets Blob à partir de Java][howto_blob_storage_java]. Pour plus d’informations sur l’utilisation de base de données SQL en Java, consultez [à l’aide de la base de données SQL en Java][howto_sql_azure_java].
* Vous pouvez utiliser **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio l’ID de compte et l’authentification de jeton à partir des paramètres de configuration de votre déploiement, au lieu de coder en dur les valeurs hello dans makecall.jsp. Pour plus d’informations sur hello **RoleEnvironment** de classe, consultez [Using hello bibliothèque Runtime du Service Azure dans JSP] [ azure_runtime_jsp] et la documentation de package de Runtime du Service Azure hello à [http://dl.windowsazure.com/javadoc][azure_javadoc].
* code de makecall.jsp Hello affecte une URL fournie par Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable. Cette URL permet une réponse de Twilio Markup Language (TwiML) qui informe Twilio comment tooproceed avec hello appeler. Par exemple, hello TwiML retourné peut contenir un  **&lt;prononcer&gt;**  verbe qui résulte dans le texte est prononcée toohello destinataire de l’appel. Au lieu d’utiliser l’URL fournie par Twilio de hello, vous pouvez générer demande de votre propre tooTwilio toorespond service ; Pour plus d’informations, consultez [comment tooUse Twilio pour la voix et les fonctionnalités de SMS dans Java][howto_twilio_voice_sms_java]. Vous trouverez plus d’informations sur TwiML à [http://www.twilio.com/docs/api/twiml][twiml]et plus d’informations sur  **&lt;prononcer&gt;**  et sont accessibles à tous les autres Twilio [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Lisez les consignes de sécurité hello Twilio à [https://www.twilio.com/docs/security][twilio_docs_security].

Pour plus d’informations sur Twilio, consultez la page [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Voir aussi
* [Comment tooUse Twilio pour la voix et les fonctionnalités de SMS dans Java][howto_twilio_voice_sms_java]
* [Ajout d’un certificat de toohello magasin de certificats d’autorité de certification Java][add_ca_cert]

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
