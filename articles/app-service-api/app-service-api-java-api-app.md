---
title: "aaaBuild et déployer une application API Java dans Azure App Service"
description: "Découvrez comment toocreate une application API Java empaqueter et déployer tooAzure du Service d’applications."
services: app-service\api
documentationcenter: java
author: rmcmurray
manager: erikre
editor: tdykstra
ms.assetid: 8d21ba5f-fc57-4269-bc8f-2fcab936ec22
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 04/25/2017
ms.author: rachelap;robmcm
ms.openlocfilehash: a4056fec870b1c4bed8ee14bb0e748b3ee89b9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="c15a0-103">Créer et déployer une application API Java dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c15a0-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="c15a0-104">Ce didacticiel montre comment toocreate une application Java et le déployer à l’aide de tooAzure App Service API Apps [Git].</span><span class="sxs-lookup"><span data-stu-id="c15a0-104">This tutorial shows how toocreate a Java application and deploy it tooAzure App Service API Apps using [Git].</span></span> <span data-ttu-id="c15a0-105">instructions Hello dans ce didacticiel peuvent être suivies sur n’importe quel système d’exploitation qui est capable d’exécuter Java.</span><span class="sxs-lookup"><span data-stu-id="c15a0-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="c15a0-106">tout code Hello dans ce didacticiel est intégré à l’aide de [Maven].</span><span class="sxs-lookup"><span data-stu-id="c15a0-106">hello code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="c15a0-107">[JAX-r] est utilisé toocreate hello Service RESTful et est généré en fonction hello [Swagger] spécification de métadonnées à l’aide de hello [éditeur de Swagger].</span><span class="sxs-lookup"><span data-stu-id="c15a0-107">[Jax-RS] is used toocreate hello RESTful Service, and is generated based on hello [Swagger] metadata specification using hello [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c15a0-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c15a0-108">Prerequisites</span></span>
1. <span data-ttu-id="c15a0-109">[Kit 8 de développeur Java]\( (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="c15a0-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="c15a0-110">[Maven] doit être installé sur votre ordinateur de développement</span><span class="sxs-lookup"><span data-stu-id="c15a0-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="c15a0-111">[Git] doit être installé sur votre ordinateur de développement</span><span class="sxs-lookup"><span data-stu-id="c15a0-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="c15a0-112">Un payant ou [version d’évaluation gratuite] abonnement trop[Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="c15a0-112">A paid or [free trial] subscription too[Microsoft Azure]</span></span>
5. <span data-ttu-id="c15a0-113">Une application de test HTTP comme [Postman]</span><span class="sxs-lookup"><span data-stu-id="c15a0-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-hello-api-using-swaggerio"></a><span data-ttu-id="c15a0-114">API de hello scaffold à l’aide de Swagger.IO</span><span class="sxs-lookup"><span data-stu-id="c15a0-114">Scaffold hello API using Swagger.IO</span></span>
<span data-ttu-id="c15a0-115">À l’aide de l’éditeur en ligne hello swagger.io, vous pouvez entrer le code JSON de Swagger ou YAML représentant la structure hello de votre API.</span><span class="sxs-lookup"><span data-stu-id="c15a0-115">Using hello swagger.io online editor, you can enter Swagger JSON or YAML code representing hello structure of your API.</span></span> <span data-ttu-id="c15a0-116">Une fois que la surface d’exposition de hello API conçue, vous pouvez exporter pour une variété de plateformes et infrastructures.</span><span class="sxs-lookup"><span data-stu-id="c15a0-116">Once you have hello API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="c15a0-117">Dans la section suivante de hello, code de hello structuré sera tooinclude modifié des fonctionnalités fictive.</span><span class="sxs-lookup"><span data-stu-id="c15a0-117">In hello next section, hello scaffolded code will be modified tooinclude mock functionality.</span></span> 

<span data-ttu-id="c15a0-118">Cette démonstration commence avec un corps JSON de Swagger que vous allez coller dans l’éditeur swagger.io hello, qui sera ensuite être utilisé toogenerate code en se servant de JAX-RS tooaccess un point de terminaison d’API REST.</span><span class="sxs-lookup"><span data-stu-id="c15a0-118">This demonstration will begin with a Swagger JSON body that you will paste into hello swagger.io editor, which will then be used toogenerate code making use of JAX-RS tooaccess a REST API endpoint.</span></span> <span data-ttu-id="c15a0-119">Ensuite, vous allez modifier des données fictives hello structuré code tooreturn, en simulant une API REST basées sur un mécanisme de persistance des données.</span><span class="sxs-lookup"><span data-stu-id="c15a0-119">Then, you'll edit hello scaffolded code tooreturn mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="c15a0-120">Copiez hello suivant du Presse-papiers tooyour de code JSON de Swagger :</span><span class="sxs-lookup"><span data-stu-id="c15a0-120">Copy hello following Swagger JSON code tooyour clipboard:</span></span>
   
        {
            "swagger": "2.0",
            "info": {
                "version": "v1",
                "title": "Contact List",
                "description": "A Contact list API based on Swagger and built using Java"
            },
            "host": "localhost",
            "schemes": [
                "http",
                "https"
            ],
            "basePath": "/api",
            "paths": {
                "/contacts": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_get",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                },
                "/contacts/{id}": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_getById",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "parameters": [
                            {
                                "name": "id",
                                "in": "path",
                                "required": true,
                                "type": "integer",
                                "format": "int32"
                            }
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                }
            },
            "definitions": {
                "Contact": {
                    "type": "object",
                    "properties": {
                        "Id": {
                            "format": "int32",
                            "type": "integer"
                        },
                        "Name": {
                            "type": "string"
                        },
                        "EmailAddress": {
                            "type": "string"
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="c15a0-121">Accédez toohello [en ligne de l’éditeur Swagger].</span><span class="sxs-lookup"><span data-stu-id="c15a0-121">Navigate toohello [Online Swagger Editor].</span></span> <span data-ttu-id="c15a0-122">Une fois, cliquez sur hello **fichier -> Coller JSON** élément de menu.</span><span class="sxs-lookup"><span data-stu-id="c15a0-122">Once there, click hello **File -> Paste JSON** menu item.</span></span>
   
    ![Élément de menu Coller JSON][paste-json]
3. <span data-ttu-id="c15a0-124">Collez hello JSON Contacts liste API Swagger vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="c15a0-124">Paste in hello Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Collage du code JSON dans Swagger][pasted-swagger]
4. <span data-ttu-id="c15a0-126">Afficher les pages de documentation hello et résumé des API de rendu dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="c15a0-126">View hello documentation pages and API summary rendered in hello editor.</span></span> 
   
    ![Affichage des documents Swagger générés][view-swagger-generated-docs]
5. <span data-ttu-id="c15a0-128">Sélectionnez hello **générer de serveur -> JAX-RS** code menu option tooscaffold hello côté serveur, vous allez modifier une implémentation fictive tooadd ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c15a0-128">Select hello **Generate Server -> JAX-RS** menu option tooscaffold hello server-side code you'll edit later tooadd mock implementation.</span></span> 
   
    ![Générer l’élément de menu de code][generate-code-menu-item]
   
    <span data-ttu-id="c15a0-130">Une fois que le code de hello est généré, vous recevrez un toodownload de fichier ZIP.</span><span class="sxs-lookup"><span data-stu-id="c15a0-130">Once hello code is generated, you'll be provided a ZIP file toodownload.</span></span> <span data-ttu-id="c15a0-131">Ce fichier contient le code hello structuré par le Générateur de code hello Swagger et toutes à générer des scripts.</span><span class="sxs-lookup"><span data-stu-id="c15a0-131">This file contains hello code scaffolded by hello Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="c15a0-132">Décompressez le répertoire de tooa hello bibliothèque entière sur votre station de travail de développement.</span><span class="sxs-lookup"><span data-stu-id="c15a0-132">Unzip hello entire library tooa directory on your development workstation.</span></span> 

## <a name="edit-hello-code-tooadd-api-implementation"></a><span data-ttu-id="c15a0-133">Modifier hello Code tooadd implémentation de l’API</span><span class="sxs-lookup"><span data-stu-id="c15a0-133">Edit hello Code tooadd API Implementation</span></span>
<span data-ttu-id="c15a0-134">Dans cette section, vous allez remplacer la mise en œuvre de hello Swagger du code généré par du côté serveur avec votre code personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c15a0-134">In this section, you'll replace hello Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="c15a0-135">nouveau code de Hello retournera un client d’appelant d’entités toohello ArrayList de Contact.</span><span class="sxs-lookup"><span data-stu-id="c15a0-135">hello new code will return an ArrayList of Contact entities toohello calling client.</span></span> 

1. <span data-ttu-id="c15a0-136">Ouvrez hello *Contact.java* fichier de modèle, qui se trouve dans hello *gen/src/java/swagger/e/s/modèle* dossier, à l’aide de [Visual Studio Code] ou votre éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="c15a0-136">Open hello *Contact.java* model file, which is located in hello *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Ouvrir le fichier de modèle de contact][open-contact-model-file]
2. <span data-ttu-id="c15a0-138">Ajouter hello suivant constructeur dans hello **Contact** classe.</span><span class="sxs-lookup"><span data-stu-id="c15a0-138">Add hello following constructor within hello **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="c15a0-139">Ouvrez hello *ContactsApiServiceImpl.java* fichier d’implémentation de service, qui se trouve dans hello *src/main/java/e/s/swagger/api/impl* dossier, à l’aide de [Visual Studio Code]ou votre éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="c15a0-139">Open hello *ContactsApiServiceImpl.java* service implementation file, which is located in hello *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Ouvrir le fichier de code du service de contact][open-contact-service-code-file]
4. <span data-ttu-id="c15a0-141">Remplacer le code hello dans le fichier de hello avec cette nouvelle tooadd de code un code de service toohello implémentation fictive.</span><span class="sxs-lookup"><span data-stu-id="c15a0-141">Overwrite hello code in hello file with this new code tooadd a mock implementation toohello service code.</span></span> 
   
        package io.swagger.api.impl;
   
        import io.swagger.api.*;
        
        import io.swagger.model.Contact;
        import java.util.*;
        import io.swagger.api.NotFoundException;
               
        import javax.ws.rs.core.Response;
        import javax.ws.rs.core.SecurityContext;
   
        @javax.annotation.Generated(value = "class io.swagger.codegen.languages.JaxRSServerCodegen", date = "2015-11-24T21:54:11.648Z")
        public class ContactsApiServiceImpl extends ContactsApiService {
   
            private ArrayList<Contact> loadContacts()
            {
                ArrayList<Contact> list = new ArrayList<Contact>();
                list.add(new Contact(1, "Barney Poland", "barney@contoso.com"));
                list.add(new Contact(2, "Lacy Barrera", "lacy@contoso.com"));
                list.add(new Contact(3, "Lora Riggs", "lora@contoso.com"));
                return list;
            }
   
            @Override
            public Response contactsGet(SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                return Response.ok().entity(list).build();
                }
   
            @Override
            public Response contactsGetById(Integer id, SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                Contact ret = null;
   
                for(int i=0; i<list.size(); i++)
                {
                    if(list.get(i).getId() == id)
                        {
                            ret = list.get(i);
                        }
                }
                return Response.ok().entity(ret).build();
            }
        }
5. <span data-ttu-id="c15a0-142">Ouvrez une invite de commandes et modifiez le répertoire toohello racine de votre application.</span><span class="sxs-lookup"><span data-stu-id="c15a0-142">Open a command prompt and change directory toohello root folder of your application.</span></span>
6. <span data-ttu-id="c15a0-143">Exécutez hello suivant Maven commande toobuild hello code et l’exécuter à l’aide de hello serveur d’applications Jetty localement.</span><span class="sxs-lookup"><span data-stu-id="c15a0-143">Execute hello following Maven command toobuild hello code and run it using hello Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="c15a0-144">Vous devez voir fenêtre de commande hello refléter que Jetty a démarré votre code sur le port 8080.</span><span class="sxs-lookup"><span data-stu-id="c15a0-144">You should see hello command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Ouvrir le fichier de code du service de contact][run-jetty-war]
8. <span data-ttu-id="c15a0-146">Utilisez [Postman] méthode toomake une API de « obtenir tous les contacts » demande toohello à http://localhost : 8080/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="c15a0-146">Use [Postman] toomake a request toohello "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Hello d’appels API de Contacts][calling-contacts-api]
9. <span data-ttu-id="c15a0-148">Utilisez [Postman] toomake une API de « obtenir le contact spécifique » demande toohello méthode situé à http://localhost : 8080/api/contacts/2.</span><span class="sxs-lookup"><span data-stu-id="c15a0-148">Use [Postman] toomake a request toohello "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Hello d’appels API de Contacts][calling-specific-contact-api]
10. <span data-ttu-id="c15a0-150">Pour finir, créez le fichier WAR de Java (ARchive Web) de hello en exécutant hello commande Maven dans votre console suivante.</span><span class="sxs-lookup"><span data-stu-id="c15a0-150">Finally, build hello Java WAR (Web ARchive) file by executing hello following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="c15a0-151">Une fois le fichier WAR hello est généré, il sera placé dans hello **cible** dossier.</span><span class="sxs-lookup"><span data-stu-id="c15a0-151">Once hello WAR file is built, it will be placed into hello **target** folder.</span></span> <span data-ttu-id="c15a0-152">Naviguez jusqu’au hello **cible** dossier et renommer le fichier WAR hello trop**ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="c15a0-152">Navigate into hello **target** folder and rename hello WAR file too**ROOT.war**.</span></span> <span data-ttu-id="c15a0-153">(Assurez-vous de mise en majuscules de hello correspond à ce format).</span><span class="sxs-lookup"><span data-stu-id="c15a0-153">(Make sure hello capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="c15a0-154">Enfin, exécutez hello suivant les commandes à partir du dossier racine hello de votre application de toocreate un **déployer** toodeploy hello WAR de dossier toouse tooAzure de fichiers.</span><span class="sxs-lookup"><span data-stu-id="c15a0-154">Finally, execute hello following commands from hello root folder of your application toocreate a **deploy** folder toouse toodeploy hello WAR file tooAzure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a><span data-ttu-id="c15a0-155">Publier hello tooAzure de sortie du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="c15a0-155">Publish hello output tooAzure App Service</span></span>
<span data-ttu-id="c15a0-156">Dans cette section, que vous allez apprendre comment toocreate une application API à l’aide de hello portail Azure, préparer cette application API pour l’hébergement d’applications Java et déployer hello nouvellement créé WAR fichier tooAzure toorun du Service d’applications pour votre nouvelle application API.</span><span class="sxs-lookup"><span data-stu-id="c15a0-156">In this section you'll learn how toocreate a new API App using hello Azure Portal, prepare that API App for hosting Java applications, and deploy hello newly-created WAR file tooAzure App Service toorun your new API App.</span></span> 

1. <span data-ttu-id="c15a0-157">Créer une application API Bonjour [portail Azure], en cliquant sur hello **Nouveau -> Web + Mobile -> application API** élément de menu, en entrant les détails de votre application et puis en cliquant sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="c15a0-157">Create a new API app in hello [Azure portal], by clicking hello **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Créer une nouvelle API App][create-api-app]
2. <span data-ttu-id="c15a0-159">Une fois que votre application API a été créée, ouvrez votre application **paramètres** panneau, puis cliquez sur hello **paramètres de l’Application** élément de menu.</span><span class="sxs-lookup"><span data-stu-id="c15a0-159">Once your API app has been created, open your app's **Settings** blade, and then click hello **Application settings** menu item.</span></span> <span data-ttu-id="c15a0-160">Sélectionnez hello Java les plus récents à partir des options disponibles de hello, puis sélectionnez hello Tomcat plus récente à partir de hello **conteneur Web** menu, puis sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c15a0-160">Select hello latest Java versions from hello available options, then select hello latest Tomcat from hello **Web container** menu, and then click **Save**.</span></span>
   
    ![Configurer Java Bonjour Panneau de l’application API][set-up-java]
3. <span data-ttu-id="c15a0-162">Cliquez sur hello **informations d’identification de déploiement** menu Paramètres d’élément et fournir un nom d’utilisateur et un mot de passe vous souhaitez toouse pour la publication des fichiers tooyour application API.</span><span class="sxs-lookup"><span data-stu-id="c15a0-162">Click hello **Deployment credentials** settings menu item, and provide a username and password you wish toouse for publishing files tooyour API App.</span></span> 
   
    ![Définir les informations d’identification de déploiement][deployment-credentials]
4. <span data-ttu-id="c15a0-164">Cliquez sur hello **source du déploiement** élément de menu Paramètres.</span><span class="sxs-lookup"><span data-stu-id="c15a0-164">Click hello **Deployment source** settings menu item.</span></span> <span data-ttu-id="c15a0-165">Une fois, cliquez sur hello **choisir les sources de** bouton, sélectionnez hello **référentiel Git Local** option, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c15a0-165">Once there, click hello **Choose source** button, select hello **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="c15a0-166">Cette opération crée un référentiel Git fonctionnant sous Azure et associé à votre application API.</span><span class="sxs-lookup"><span data-stu-id="c15a0-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="c15a0-167">Chaque fois que vous validez code toohello *master* branche du référentiel Git, votre code sera publié dans votre instance d’application API en cours d’exécution dynamique.</span><span class="sxs-lookup"><span data-stu-id="c15a0-167">Each time you commit code toohello *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Configurer un nouveau référentiel Git local][select-git-repo]
5. <span data-ttu-id="c15a0-169">Copiez le Presse-papiers de tooyour d’hello nouveau référentiel Git URL.</span><span class="sxs-lookup"><span data-stu-id="c15a0-169">Copy hello new Git repository's URL tooyour clipboard.</span></span> <span data-ttu-id="c15a0-170">Conservez-la, car dans un instant, vous devrez l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="c15a0-170">Save this as it will be important in a moment.</span></span> 
   
    ![Configurer un nouveau référentiel Git pour votre application][copy-git-repo-url]
6. <span data-ttu-id="c15a0-172">GIT push hello WAR fichier toohello référentiel en ligne.</span><span class="sxs-lookup"><span data-stu-id="c15a0-172">Git push hello WAR file toohello online repository.</span></span> <span data-ttu-id="c15a0-173">toodo, naviguez jusqu’au hello **déployer** dossier que vous avez créé précédemment afin que vous puissiez valider facilement code hello référentiel toohello en cours d’exécution dans votre application de Service.</span><span class="sxs-lookup"><span data-stu-id="c15a0-173">toodo this, navigate into hello **deploy** folder you created earlier so that you can easily commit hello code up toohello repository running in your App Service.</span></span> <span data-ttu-id="c15a0-174">Une fois vous êtes dans la fenêtre de console hello et accédé au dossier hello où se trouve, dossier de WebApp hello émettre hello suivant Git commandes toolaunch hello processus et déclencher un déploiement.</span><span class="sxs-lookup"><span data-stu-id="c15a0-174">Once you're in hello console window and navigated into hello folder where hello webapps folder is located, issue hello following Git commands toolaunch hello process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="c15a0-175">Une fois que vous exécutez hello **push** demande, vous serez invité à indiquer pour mot de passe hello vous avez créé des informations d’identification de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="c15a0-175">Once you issue hello **push** request, you'll be asked for hello password you created for hello deployment credential earlier.</span></span> <span data-ttu-id="c15a0-176">Après avoir entré vos informations d’identification, vous devez voir votre affichage portail qui hello mise à jour a été déployée.</span><span class="sxs-lookup"><span data-stu-id="c15a0-176">After you enter your credentials, you should see your portal display that hello update was deployed.</span></span>
7. <span data-ttu-id="c15a0-177">Si vous utilisez une fois encore Postman toohit hello nouvellement déployé API application s’exécutant dans Azure App Service, vous verrez que le comportement de hello est cohérent et que maintenant il retourne des données de contacts comme prévu, et à l’aide des modifications de code simple toohello Swagger.io structuré code Java.</span><span class="sxs-lookup"><span data-stu-id="c15a0-177">If you once again use Postman toohit hello newly-deployed API App running in Azure App Service, you'll see that hello behavior is consistent and that now it is returning contact data as expected, and using simple code changes toohello Swagger.io scaffolded Java code.</span></span> 
   
    ![Utilisation de l’API REST de contacts de Java en direct dans Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="c15a0-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c15a0-179">Next steps</span></span>
<span data-ttu-id="c15a0-180">Dans cet article, vous ont été en mesure de toostart avec un fichier JSON de Swagger et du code Java modèle généré automatiquement obtenu à partir de l’éditeur Swagger.io hello.</span><span class="sxs-lookup"><span data-stu-id="c15a0-180">In this article, you were able toostart with a Swagger JSON file and some scaffolded Java code obtained from hello Swagger.io editor.</span></span> <span data-ttu-id="c15a0-181">À partir de là, quelques modifications simples et le processus de déploiement Git vous ont permis d’obtenir une application API fonctionnelle rédigée en Java.</span><span class="sxs-lookup"><span data-stu-id="c15a0-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="c15a0-182">étape suivante du didacticiel Hello montre comment trop[consommer des applications API à partir de clients de JavaScript, à l’aide de CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="c15a0-182">hello next tutorial shows how too[consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="c15a0-183">Des didacticiels ultérieurs dans hello série indiquent comment tooimplement authentification et autorisation.</span><span class="sxs-lookup"><span data-stu-id="c15a0-183">Later tutorials in hello series show how tooimplement authentication and authorization.</span></span>

<span data-ttu-id="c15a0-184">toobuild sur cet exemple, vous pouvez en savoir plus sur hello [stockage SDK pour Java] objets BLOB de toopersist hello JSON.</span><span class="sxs-lookup"><span data-stu-id="c15a0-184">toobuild on this sample, you can learn more about hello [Storage SDK for Java] toopersist hello JSON blobs.</span></span> <span data-ttu-id="c15a0-185">Vous pouvez également utiliser hello [Document DB Java SDK] toosave votre tooAzure de données de Contact Document de base de données.</span><span class="sxs-lookup"><span data-stu-id="c15a0-185">Or, you could use hello [Document DB Java SDK] toosave your Contact data tooAzure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="c15a0-186">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c15a0-186">See Also</span></span>
<span data-ttu-id="c15a0-187">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Azure pour les développeurs Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="c15a0-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[portail Azure]: https://portal.azure.com/
[Document DB Java SDK]: ../documentdb/documentdb-java-application.md
[version d’évaluation gratuite]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Kit 8 de développeur Java]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[JAX-r]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[en ligne de l’éditeur Swagger]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[stockage SDK pour Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[éditeur de Swagger]: http://editor.swagger.io/
[Visual Studio Code]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: ./media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: ./media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: ./media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: ./media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: ./media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: ./media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: ./media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: ./media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: ./media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: ./media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: ./media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: ./media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: ./media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: ./media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: ./media/app-service-api-java-api-app/postman-calling-azure-contacts.png
