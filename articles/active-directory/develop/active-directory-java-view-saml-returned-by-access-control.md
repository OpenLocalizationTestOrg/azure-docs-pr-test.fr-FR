---
title: "aaaView SAML retourné par hello Access Control Service (Java)"
description: "Découvrez comment tooview SAML retourné par hello Service de contrôle d’accès dans des applications Java hébergé sur Azure."
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
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a><span data-ttu-id="071fd-103">Comment tooview SAML retourné par hello Azure Access Control Service</span><span class="sxs-lookup"><span data-stu-id="071fd-103">How tooview SAML returned by hello Azure Access Control Service</span></span>
<span data-ttu-id="071fd-104">Ce guide vous explique comment hello tooview sous-jacent Security Assertion Markup Language (SAML) retournées tooyour application par hello Azure Access Control Service (ACS).</span><span class="sxs-lookup"><span data-stu-id="071fd-104">This guide will show you how tooview hello underlying Security Assertion Markup Language (SAML) returned tooyour application by hello Azure Access Control Service (ACS).</span></span> <span data-ttu-id="071fd-105">guide de Hello s’appuie sur hello [comment tooAuthenticate utilisateurs Web auprès d’Azure Access Control Service à l’aide de Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) rubrique, en fournissant le code qui affiche des informations de SAML hello.</span><span class="sxs-lookup"><span data-stu-id="071fd-105">hello guide builds on hello [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays hello SAML information.</span></span> <span data-ttu-id="071fd-106">application Hello terminée ressemblera similaire toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="071fd-106">hello completed application will look similar toohello following.</span></span>

![Exemple de sortie SAML][saml_output]

<span data-ttu-id="071fd-108">Pour plus d’informations sur ACS, consultez hello [étapes](#next_steps) section.</span><span class="sxs-lookup"><span data-stu-id="071fd-108">For more information on ACS, see hello [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="071fd-109">Hello filtre d’Azure Access Control Services est une version préliminaire CTP.</span><span class="sxs-lookup"><span data-stu-id="071fd-109">hello Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="071fd-110">En tant que logiciel préliminaire, il n'est pas officiellement pris en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="071fd-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="071fd-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="071fd-111">Prerequisites</span></span>
<span data-ttu-id="071fd-112">tâches de hello toocomplete dans ce guide, complète hello exemple à l’adresse [comment tooAuthenticate utilisateurs Web auprès d’Azure Access Control Service à l’aide de Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) et l’utiliser comme point de départ pour ce didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="071fd-112">toocomplete hello tasks in this guide, complete hello sample at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as hello starting point for this tutorial.</span></span>

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a><span data-ttu-id="071fd-113">Ajouter hello JspWriter tooyour build chemin d’accès et le déploiement assembly de bibliothèque</span><span class="sxs-lookup"><span data-stu-id="071fd-113">Add hello JspWriter library tooyour build path and deployment assembly</span></span>
<span data-ttu-id="071fd-114">Ajout d’une bibliothèque hello contenant hello **javax.servlet.jsp.JspWriter** classe tooyour générer l’assembly de chemin d’accès et le déploiement.</span><span class="sxs-lookup"><span data-stu-id="071fd-114">Add hello library that contains hello **javax.servlet.jsp.JspWriter** class tooyour build path and deployment assembly.</span></span> <span data-ttu-id="071fd-115">Si vous utilisez Tomcat, bibliothèque de hello est **jsp-api.jar**, qui se trouve dans hello Apache **lib** dossier.</span><span class="sxs-lookup"><span data-stu-id="071fd-115">If you are using Tomcat, hello library is **jsp-api.jar**, which is located in hello Apache **lib** folder.</span></span>

1. <span data-ttu-id="071fd-116">Dans l’Explorateur de projets d’Eclipse, cliquez sur **MyACSHelloWorld**, cliquez sur **générer le chemin d’accès**, cliquez sur **configurer un chemin de Build**, cliquez sur hello **bibliothèques** onglet, puis cliquez sur **ajouter le fichiers JAR externe**.</span><span class="sxs-lookup"><span data-stu-id="071fd-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click hello **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="071fd-117">Bonjour **JAR de sélection** boîte de dialogue, accédez toohello JAR nécessaire, sélectionnez-le, puis cliquez sur **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="071fd-117">In hello **JAR Selection** dialog, navigate toohello necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="071fd-118">Avec hello **propriétés MyACSHelloWorld** boîte de dialogue encore ouverte, cliquez **Assembly de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="071fd-118">With hello **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="071fd-119">Bonjour **Assembly de déploiement Web** boîte de dialogue, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="071fd-119">In hello **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="071fd-120">Bonjour **nouvelle Directive d’Assembly** boîte de dialogue, cliquez sur **entrées du chemin d’accès de Build Java** puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="071fd-120">In hello **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="071fd-121">Sélectionnez la bibliothèque appropriée de hello et cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="071fd-121">Select hello appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="071fd-122">Cliquez sur **OK** tooclose hello **propriétés MyACSHelloWorld** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="071fd-122">Click **OK** tooclose hello **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-hello-jsp-file-toodisplay-saml"></a><span data-ttu-id="071fd-123">Modifier le fichier toodisplay SAML de hello JSP</span><span class="sxs-lookup"><span data-stu-id="071fd-123">Modify hello JSP file toodisplay SAML</span></span>
<span data-ttu-id="071fd-124">Modifier **index.jsp** hello toouse suivant de code.</span><span class="sxs-lookup"><span data-stu-id="071fd-124">Modify **index.jsp** toouse hello following code.</span></span>

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

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
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

            // Iterate hello child nodes of hello doc.
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

## <a name="run-hello-application"></a><span data-ttu-id="071fd-125">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="071fd-125">Run hello application</span></span>
1. <span data-ttu-id="071fd-126">Exécutez votre application dans l’émulateur de calcul hello ou déployer tooAzure, à l’aide des étapes hello sur [comment tooAuthenticate utilisateurs Web auprès d’Azure Access Control Service à l’aide de Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="071fd-126">Run your application in hello computer emulator or deploy tooAzure, using hello steps documented at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="071fd-127">Lancez un navigateur et ouvrez votre application Web.</span><span class="sxs-lookup"><span data-stu-id="071fd-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="071fd-128">Une fois la session tooyour application, vous verrez des informations SAML, y compris d’assertion de sécurité hello fournie par le fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="071fd-128">After you log on tooyour application, you'll see SAML information, including hello security assertion provided by hello identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="071fd-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="071fd-129">Next steps</span></span>
<span data-ttu-id="071fd-130">toofurther Explorer tooexperiment avec des scénarios plus sophistiqués et les fonctionnalités d’ACS, consultez [Access Control Service 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="071fd-130">toofurther explore ACS's functionality and tooexperiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
