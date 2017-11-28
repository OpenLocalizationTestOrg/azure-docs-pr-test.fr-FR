---
title: "Affichage des données SAML renvoyées par ACS (Java)"
description: "Découvrez comment afficher SAML renvoyé par le service de contrôle d'accès dans les applications Java hébergées sur Azure."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: 1552e624a4703138ab82f7133ceaec3dbd04e1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-view-saml-returned-by-the-azure-access-control-service"></a><span data-ttu-id="1914a-103">Affichage des données SAML (Security Assertion Markup Language) renvoyées par Azure Access Control Service</span><span class="sxs-lookup"><span data-stu-id="1914a-103">How to view SAML returned by the Azure Access Control Service</span></span>
<span data-ttu-id="1914a-104">Ce guide explique comment afficher les données SAML (Security Assertion Markup Language) sous-jacentes renvoyées à votre application par Azure Access Control Service (ACS).</span><span class="sxs-lookup"><span data-stu-id="1914a-104">This guide will show you how to view the underlying Security Assertion Markup Language (SAML) returned to your application by the Azure Access Control Service (ACS).</span></span> <span data-ttu-id="1914a-105">Ce guide s’appuie sur la rubrique [Authentification des utilisateurs web auprès d’Azure Access Control Service à l’aide d’Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) en fournissant le code nécessaire à l’affichage des données SAML.</span><span class="sxs-lookup"><span data-stu-id="1914a-105">The guide builds on the [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays the SAML information.</span></span> <span data-ttu-id="1914a-106">L'application terminée sera semblable à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="1914a-106">The completed application will look similar to the following.</span></span>

![Exemple de sortie SAML][saml_output]

<span data-ttu-id="1914a-108">Pour plus d'informations sur ACS, consultez la section [Étapes suivantes](#next_steps) .</span><span class="sxs-lookup"><span data-stu-id="1914a-108">For more information on ACS, see the [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="1914a-109">Le filtre ACS Azure est une version préliminaire de la technologie destinée à la communauté.</span><span class="sxs-lookup"><span data-stu-id="1914a-109">The Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="1914a-110">En tant que logiciel préliminaire, il n'est pas officiellement pris en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1914a-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1914a-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1914a-111">Prerequisites</span></span>
<span data-ttu-id="1914a-112">Pour réaliser les tâches présentées dans ce guide, suivez l'exemple de la rubrique [Authentification des utilisateurs Web auprès d'Azure Access Control Service à l'aide d'Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) et utilisez-le comme point de départ de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1914a-112">To complete the tasks in this guide, complete the sample at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as the starting point for this tutorial.</span></span>

## <a name="add-the-jspwriter-library-to-your-build-path-and-deployment-assembly"></a><span data-ttu-id="1914a-113">Ajout de la bibliothèque JspWriter au chemin d'accès de la build et à l'assembly de déploiement</span><span class="sxs-lookup"><span data-stu-id="1914a-113">Add the JspWriter library to your build path and deployment assembly</span></span>
<span data-ttu-id="1914a-114">Ajoutez la bibliothèque contenant la classe **javax.servlet.jsp.JspWriter** au chemin d'accès de la build et à l'assembly de déploiement.</span><span class="sxs-lookup"><span data-stu-id="1914a-114">Add the library that contains the **javax.servlet.jsp.JspWriter** class to your build path and deployment assembly.</span></span> <span data-ttu-id="1914a-115">Si vous utilisez Tomcat, utilisez la bibliothèque **jsp-api.jar** située dans le dossier **lib** d'Apache.</span><span class="sxs-lookup"><span data-stu-id="1914a-115">If you are using Tomcat, the library is **jsp-api.jar**, which is located in the Apache **lib** folder.</span></span>

1. <span data-ttu-id="1914a-116">Dans l'Explorateur de projets Eclipse, cliquez avec le bouton droit sur **MyACSHelloWorld**, puis cliquez sur **Build Path**, sur **Configure Build Path**, sur l'onglet **Libraries** et sur **Add External JARs**.</span><span class="sxs-lookup"><span data-stu-id="1914a-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click the **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="1914a-117">Dans la boîte de dialogue **JAR Selection**, accédez au fichier JAR requis, sélectionnez-le, puis cliquez sur **Open**.</span><span class="sxs-lookup"><span data-stu-id="1914a-117">In the **JAR Selection** dialog, navigate to the necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="1914a-118">Dans la boîte de dialogue **Properties for MyACSHelloWorld**, cliquez sur **Deployment Assembly**.</span><span class="sxs-lookup"><span data-stu-id="1914a-118">With the **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="1914a-119">Dans la boîte de dialogue **Web Deployment Assembly**, cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="1914a-119">In the **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="1914a-120">Dans la boîte de dialogue **New Assembly Directive**, cliquez sur **Java Build Path Entries** puis sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="1914a-120">In the **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="1914a-121">Sélectionnez la bibliothèque qui convient, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="1914a-121">Select the appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="1914a-122">Cliquez sur **OK** pour fermer la boîte de dialogue **Properties for MyACSHelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="1914a-122">Click **OK** to close the **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-the-jsp-file-to-display-saml"></a><span data-ttu-id="1914a-123">Modification du fichier JSP pour afficher les données SAML</span><span class="sxs-lookup"><span data-stu-id="1914a-123">Modify the JSP file to display SAML</span></span>
<span data-ttu-id="1914a-124">Modifiez le fichier **index.jsp** de manière à utiliser le code suivant.</span><span class="sxs-lookup"><span data-stu-id="1914a-124">Modify **index.jsp** to use the following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print the text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out the child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate the names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish the sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process the child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate the child nodes of the doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-the-application"></a><span data-ttu-id="1914a-125">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="1914a-125">Run the application</span></span>
1. <span data-ttu-id="1914a-126">Exécutez votre application dans l'émulateur de l'ordinateur ou déployez-la dans Azure en suivant la procédure décrite à la rubrique [Authentification des utilisateurs Web auprès d'Azure Access Control Service à l'aide d'Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="1914a-126">Run your application in the computer emulator or deploy to Azure, using the steps documented at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="1914a-127">Lancez un navigateur et ouvrez votre application Web.</span><span class="sxs-lookup"><span data-stu-id="1914a-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="1914a-128">Une fois connecté à votre application, vous verrez les données SAML ainsi que l'assertion de sécurité fournie par le fournisseur d'identité.</span><span class="sxs-lookup"><span data-stu-id="1914a-128">After you log on to your application, you'll see SAML information, including the security assertion provided by the identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1914a-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1914a-129">Next steps</span></span>
<span data-ttu-id="1914a-130">Pour en savoir plus sur les fonctionnalités ACS et découvrir des scénarios plus complexes, consultez la page [Access Control Service 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="1914a-130">To further explore ACS's functionality and to experiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify the JSP file to display SAML]: #modify_jsp
[Add the JspWriter library to your build path and deployment assembly]: #add_library
[Run the application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How to Authenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
