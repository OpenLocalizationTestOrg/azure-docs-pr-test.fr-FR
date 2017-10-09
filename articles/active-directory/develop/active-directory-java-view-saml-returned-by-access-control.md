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
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a>Comment tooview SAML retourné par hello Azure Access Control Service
Ce guide vous explique comment hello tooview sous-jacent Security Assertion Markup Language (SAML) retournées tooyour application par hello Azure Access Control Service (ACS). guide de Hello s’appuie sur hello [comment tooAuthenticate utilisateurs Web auprès d’Azure Access Control Service à l’aide de Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) rubrique, en fournissant le code qui affiche des informations de SAML hello. application Hello terminée ressemblera similaire toohello suivant.

![Exemple de sortie SAML][saml_output]

Pour plus d’informations sur ACS, consultez hello [étapes](#next_steps) section.

> [!NOTE]
> Hello filtre d’Azure Access Control Services est une version préliminaire CTP. En tant que logiciel préliminaire, il n'est pas officiellement pris en charge par Microsoft.
> 
> 

## <a name="prerequisites"></a>Composants requis
tâches de hello toocomplete dans ce guide, complète hello exemple à l’adresse [comment tooAuthenticate utilisateurs Web auprès d’Azure Access Control Service à l’aide de Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) et l’utiliser comme point de départ pour ce didacticiel de hello.

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a>Ajouter hello JspWriter tooyour build chemin d’accès et le déploiement assembly de bibliothèque
Ajout d’une bibliothèque hello contenant hello **javax.servlet.jsp.JspWriter** classe tooyour générer l’assembly de chemin d’accès et le déploiement. Si vous utilisez Tomcat, bibliothèque de hello est **jsp-api.jar**, qui se trouve dans hello Apache **lib** dossier.

1. Dans l’Explorateur de projets d’Eclipse, cliquez sur **MyACSHelloWorld**, cliquez sur **générer le chemin d’accès**, cliquez sur **configurer un chemin de Build**, cliquez sur hello **bibliothèques** onglet, puis cliquez sur **ajouter le fichiers JAR externe**.
2. Bonjour **JAR de sélection** boîte de dialogue, accédez toohello JAR nécessaire, sélectionnez-le, puis cliquez sur **ouvrir**.
3. Avec hello **propriétés MyACSHelloWorld** boîte de dialogue encore ouverte, cliquez **Assembly de déploiement**.
4. Bonjour **Assembly de déploiement Web** boîte de dialogue, cliquez sur **ajouter**.
5. Bonjour **nouvelle Directive d’Assembly** boîte de dialogue, cliquez sur **entrées du chemin d’accès de Build Java** puis cliquez sur **suivant**.
6. Sélectionnez la bibliothèque appropriée de hello et cliquez sur **Terminer**.
7. Cliquez sur **OK** tooclose hello **propriétés MyACSHelloWorld** boîte de dialogue.

## <a name="modify-hello-jsp-file-toodisplay-saml"></a>Modifier le fichier toodisplay SAML de hello JSP
Modifier **index.jsp** hello toouse suivant de code.

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

## <a name="run-hello-application"></a>Exécutez l’application hello
1. Exécutez votre application dans l’émulateur de calcul hello ou déployer tooAzure, à l’aide des étapes hello sur [comment tooAuthenticate utilisateurs Web auprès d’Azure Access Control Service à l’aide de Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).
2. Lancez un navigateur et ouvrez votre application Web. Une fois la session tooyour application, vous verrez des informations SAML, y compris d’assertion de sécurité hello fournie par le fournisseur d’identité hello.

## <a name="next-steps"></a>Étapes suivantes
toofurther Explorer tooexperiment avec des scénarios plus sophistiqués et les fonctionnalités d’ACS, consultez [Access Control Service 2.0][Access Control Service 2.0].

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
