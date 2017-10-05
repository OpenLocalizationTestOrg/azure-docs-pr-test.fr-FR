---
title: "Créer et déployer une application API Java dans Azure App Service"
description: "Découvrez comment créer un package d’application API Java et le déployer sur Azure App Service."
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
ms.openlocfilehash: e38c540071cb49b0177e79178566d72ecb5f8886
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="f7134-103">Créer et déployer une application API Java dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f7134-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="f7134-104">Ce didacticiel explique comment créer une application Java et comment la déployer dans des applications API Azure App Service en utilisant [Git].</span><span class="sxs-lookup"><span data-stu-id="f7134-104">This tutorial shows how to create a Java application and deploy it to Azure App Service API Apps using [Git].</span></span> <span data-ttu-id="f7134-105">Les instructions de ce didacticiel s’appliquent à tous les systèmes d’exploitation pouvant exécuter Java.</span><span class="sxs-lookup"><span data-stu-id="f7134-105">The instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="f7134-106">Le code de ce didacticiel a été rédigé avec [Maven].</span><span class="sxs-lookup"><span data-stu-id="f7134-106">The code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="f7134-107">[Jax-RS] est utilisé pour créer le service RESTful et il est généré à partir des spécifications de métadonnées [Swagger] à l’aide de [l’éditeur Swagger].</span><span class="sxs-lookup"><span data-stu-id="f7134-107">[Jax-RS] is used to create the RESTful Service, and is generated based on the [Swagger] metadata specification using the [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7134-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f7134-108">Prerequisites</span></span>
1. <span data-ttu-id="f7134-109">[Kit 8 de développeur Java]\( (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="f7134-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="f7134-110">[Maven] doit être installé sur votre ordinateur de développement</span><span class="sxs-lookup"><span data-stu-id="f7134-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="f7134-111">[Git] doit être installé sur votre ordinateur de développement</span><span class="sxs-lookup"><span data-stu-id="f7134-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="f7134-112">Un abonnement payant ou une [version d’évaluation gratuite] dans [Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="f7134-112">A paid or [free trial] subscription to [Microsoft Azure]</span></span>
5. <span data-ttu-id="f7134-113">Une application de test HTTP comme [Postman]</span><span class="sxs-lookup"><span data-stu-id="f7134-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-the-api-using-swaggerio"></a><span data-ttu-id="f7134-114">Structure de l’API avec Swagger.IO</span><span class="sxs-lookup"><span data-stu-id="f7134-114">Scaffold the API using Swagger.IO</span></span>
<span data-ttu-id="f7134-115">Avec l’éditeur en ligne swagger.io, vous pouvez accéder au code JSON Swagger ou YAML qui représente la structure de votre API.</span><span class="sxs-lookup"><span data-stu-id="f7134-115">Using the swagger.io online editor, you can enter Swagger JSON or YAML code representing the structure of your API.</span></span> <span data-ttu-id="f7134-116">Une fois la surface d’exposition de l’API conçue, vous pouvez exporter le code pour différentes plateformes et infrastructures.</span><span class="sxs-lookup"><span data-stu-id="f7134-116">Once you have the API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="f7134-117">Dans la section qui suit, vous allez modifier la structure du code pour y inclure des fonctionnalités factices.</span><span class="sxs-lookup"><span data-stu-id="f7134-117">In the next section, the scaffolded code will be modified to include mock functionality.</span></span> 

<span data-ttu-id="f7134-118">Cette démonstration commence par le collage d’un corps JSON Swagger dans l’éditeur swagger.io, qui sera ensuite utilisé pour générer le code qui se sert de JAX-RS pour accéder à un point de terminaison API REST.</span><span class="sxs-lookup"><span data-stu-id="f7134-118">This demonstration will begin with a Swagger JSON body that you will paste into the swagger.io editor, which will then be used to generate code making use of JAX-RS to access a REST API endpoint.</span></span> <span data-ttu-id="f7134-119">Le code structuré sera ensuite modifié pour retourner des données fictives en simulant une API REST basée sur un mécanisme de conservation des données.</span><span class="sxs-lookup"><span data-stu-id="f7134-119">Then, you'll edit the scaffolded code to return mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="f7134-120">Copiez le code JSON Swagger ci-dessous dans le Presse-papiers :</span><span class="sxs-lookup"><span data-stu-id="f7134-120">Copy the following Swagger JSON code to your clipboard:</span></span>
   
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
2. <span data-ttu-id="f7134-121">Accédez à [l’éditeur Swagger en ligne].</span><span class="sxs-lookup"><span data-stu-id="f7134-121">Navigate to the [Online Swagger Editor].</span></span> <span data-ttu-id="f7134-122">Une fois arrivé à ce stade, cliquez sur l’élément de menu **Fichier -> Coller JSON**.</span><span class="sxs-lookup"><span data-stu-id="f7134-122">Once there, click the **File -> Paste JSON** menu item.</span></span>
   
    ![Élément de menu Coller JSON][paste-json]
3. <span data-ttu-id="f7134-124">Collez l’élément dans l’API JSON Swagger de liste de contacts que vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="f7134-124">Paste in the Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Collage du code JSON dans Swagger][pasted-swagger]
4. <span data-ttu-id="f7134-126">Affichez les pages de documentation et le résumé des API figurant dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="f7134-126">View the documentation pages and API summary rendered in the editor.</span></span> 
   
    ![Affichage des documents Swagger générés][view-swagger-generated-docs]
5. <span data-ttu-id="f7134-128">Sélectionnez l’option de menu **Générer serveur -> JAX-RS** pour structurer le code côté serveur que vous allez modifier par la suite pour y ajouter une implémentation factice.</span><span class="sxs-lookup"><span data-stu-id="f7134-128">Select the **Generate Server -> JAX-RS** menu option to scaffold the server-side code you'll edit later to add mock implementation.</span></span> 
   
    ![Générer l’élément de menu de code][generate-code-menu-item]
   
    <span data-ttu-id="f7134-130">Une fois le code généré, vous recevrez un fichier ZIP à télécharger.</span><span class="sxs-lookup"><span data-stu-id="f7134-130">Once the code is generated, you'll be provided a ZIP file to download.</span></span> <span data-ttu-id="f7134-131">Ce fichier contient le code généré automatiquement par le générateur de code Swagger et tous les scripts de compilation associés.</span><span class="sxs-lookup"><span data-stu-id="f7134-131">This file contains the code scaffolded by the Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="f7134-132">Décompressez la totalité de la bibliothèque dans un répertoire de votre station de travail de développement.</span><span class="sxs-lookup"><span data-stu-id="f7134-132">Unzip the entire library to a directory on your development workstation.</span></span> 

## <a name="edit-the-code-to-add-api-implementation"></a><span data-ttu-id="f7134-133">Modifiez le code pour ajouter l’implémentation de l’API</span><span class="sxs-lookup"><span data-stu-id="f7134-133">Edit the Code to add API Implementation</span></span>
<span data-ttu-id="f7134-134">Dans cette section, vous allez remplacer l’implémentation côté serveur du code généré par Swagger par votre code personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f7134-134">In this section, you'll replace the Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="f7134-135">Le nouveau code retournera une liste des tableaux (ArrayList) des entités de contacts au client appelant.</span><span class="sxs-lookup"><span data-stu-id="f7134-135">The new code will return an ArrayList of Contact entities to the calling client.</span></span> 

1. <span data-ttu-id="f7134-136">Ouvrez le fichier de modèle *Contact.java*, situé dans le dossier *src/gen/java/io/swagger/model*, avec [Visual Studio Code] ou dans votre éditeur de texte préféré.</span><span class="sxs-lookup"><span data-stu-id="f7134-136">Open the *Contact.java* model file, which is located in the *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Ouvrir le fichier de modèle de contact][open-contact-model-file]
2. <span data-ttu-id="f7134-138">Ajoutez le constructeur suivant à la classe **Contact**.</span><span class="sxs-lookup"><span data-stu-id="f7134-138">Add the following constructor within the **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="f7134-139">Ouvrez le fichier d’implémentation de service *ContactsApiServiceImpl.java*, situé dans le dossier *src/main/java/io/swagger/api/impl*, dans [Visual Studio Code] ou dans votre éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="f7134-139">Open the *ContactsApiServiceImpl.java* service implementation file, which is located in the *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Ouvrir le fichier de code du service de contact][open-contact-service-code-file]
4. <span data-ttu-id="f7134-141">Remplacez le code présent dans le fichier par ce nouveau code. Vous ajouterez ainsi une implémentation factice au code de service.</span><span class="sxs-lookup"><span data-stu-id="f7134-141">Overwrite the code in the file with this new code to add a mock implementation to the service code.</span></span> 
   
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
5. <span data-ttu-id="f7134-142">Ouvrez une invite de commandes et choisissez le dossier racine de votre application comme répertoire.</span><span class="sxs-lookup"><span data-stu-id="f7134-142">Open a command prompt and change directory to the root folder of your application.</span></span>
6. <span data-ttu-id="f7134-143">Exécutez la commande Maven suivante pour générer le code et exécutez-le localement à l’aide du serveur d’applications Jetty localement.</span><span class="sxs-lookup"><span data-stu-id="f7134-143">Execute the following Maven command to build the code and run it using the Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="f7134-144">La fenêtre de commande indique en principe que Jetty a démarré votre code sur le port 8080.</span><span class="sxs-lookup"><span data-stu-id="f7134-144">You should see the command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Ouvrir le fichier de code du service de contact][run-jetty-war]
8. <span data-ttu-id="f7134-146">Utilisez [Postman] pour exécuter une requête à la méthode API « get all contacts » sur http://localhost:8080/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="f7134-146">Use [Postman] to make a request to the "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Appeler l’API de contacts][calling-contacts-api]
9. <span data-ttu-id="f7134-148">Utilisez [Postman] pour exécuter une requête sur la méthode API « get specific contact » située sur http://localhost:8080/api/contacts/2.</span><span class="sxs-lookup"><span data-stu-id="f7134-148">Use [Postman] to make a request to the "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Appeler l’API de contacts][calling-specific-contact-api]
10. <span data-ttu-id="f7134-150">Enfin, générez le fichier WAR Java (ARchive Web) en exécutant la commande Maven suivante sur votre console.</span><span class="sxs-lookup"><span data-stu-id="f7134-150">Finally, build the Java WAR (Web ARchive) file by executing the following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="f7134-151">Une fois le fichier WAR généré, il est placé dans le dossier **cible** .</span><span class="sxs-lookup"><span data-stu-id="f7134-151">Once the WAR file is built, it will be placed into the **target** folder.</span></span> <span data-ttu-id="f7134-152">Accédez au dossier **cible**, et renommez le fichier WAR en lui affectant le nom **ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="f7134-152">Navigate into the **target** folder and rename the WAR file to **ROOT.war**.</span></span> <span data-ttu-id="f7134-153">(Veillez à respecter la casse).</span><span class="sxs-lookup"><span data-stu-id="f7134-153">(Make sure the capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="f7134-154">Enfin, exécutez les commandes suivantes à partir du dossier racine de votre application pour créer un dossier de **déploiement** à utiliser pour déployer le fichier WAR dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f7134-154">Finally, execute the following commands from the root folder of your application to create a **deploy** folder to use to deploy the WAR file to Azure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-the-output-to-azure-app-service"></a><span data-ttu-id="f7134-155">Publication du résultat dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f7134-155">Publish the output to Azure App Service</span></span>
<span data-ttu-id="f7134-156">Dans cette section, vous allez apprendre à créer une nouvelle application API App à l’aide du portail Azure, à préparer cette dernière pour l’hébergement d’applications Java et à déployer le fichier WAR récemment créé dans Azure App Service pour exécuter votre nouvelle application API.</span><span class="sxs-lookup"><span data-stu-id="f7134-156">In this section you'll learn how to create a new API App using the Azure Portal, prepare that API App for hosting Java applications, and deploy the newly-created WAR file to Azure App Service to run your new API App.</span></span> 

1. <span data-ttu-id="f7134-157">Créez une application API dans le [Portail Azure]. Pour cela, cliquez sur **Nouveau -> Web + Mobile -> Application API**, entrez les informations détaillées sur votre application, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f7134-157">Create a new API app in the [Azure portal], by clicking the **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Créer une nouvelle API App][create-api-app]
2. <span data-ttu-id="f7134-159">Une fois votre application API créée, ouvrez le panneau **Paramètres** de votre application , puis cliquez sur l’élément de menu **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="f7134-159">Once your API app has been created, open your app's **Settings** blade, and then click the **Application settings** menu item.</span></span> <span data-ttu-id="f7134-160">Sélectionnez les dernières versions de Java dans les options disponibles, sélectionnez la version la plus récente de Tomcat dans le menu **Conteneur web**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f7134-160">Select the latest Java versions from the available options, then select the latest Tomcat from the **Web container** menu, and then click **Save**.</span></span>
   
    ![Configurer Java dans le panneau application API][set-up-java]
3. <span data-ttu-id="f7134-162">Cliquez sur l’élément de menu de paramètre **Informations d’identification de déploiement** , puis fournissez le nom d’utilisateur et le mot de passe que vous souhaitez utiliser pour la publication de fichiers dans votre application API.</span><span class="sxs-lookup"><span data-stu-id="f7134-162">Click the **Deployment credentials** settings menu item, and provide a username and password you wish to use for publishing files to your API App.</span></span> 
   
    ![Définir les informations d’identification de déploiement][deployment-credentials]
4. <span data-ttu-id="f7134-164">Cliquez sur l’élément de menu de paramètre **Source de déploiement** .</span><span class="sxs-lookup"><span data-stu-id="f7134-164">Click the **Deployment source** settings menu item.</span></span> <span data-ttu-id="f7134-165">À ce stade, cliquez sur le bouton **Choisir la source**, sélectionnez l’option **Référentiel Git local**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7134-165">Once there, click the **Choose source** button, select the **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="f7134-166">Cette opération crée un référentiel Git fonctionnant sous Azure et associé à votre application API.</span><span class="sxs-lookup"><span data-stu-id="f7134-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="f7134-167">À chaque fois que vous validez le code dans la branche *master* du référentiel Git, votre code est publié dans l’instance d’application API en cours d’exécution en direct.</span><span class="sxs-lookup"><span data-stu-id="f7134-167">Each time you commit code to the *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Configurer un nouveau référentiel Git local][select-git-repo]
5. <span data-ttu-id="f7134-169">Copiez la nouvelle URL de référentiel Git dans votre presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="f7134-169">Copy the new Git repository's URL to your clipboard.</span></span> <span data-ttu-id="f7134-170">Conservez-la, car dans un instant, vous devrez l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="f7134-170">Save this as it will be important in a moment.</span></span> 
   
    ![Configurer un nouveau référentiel Git pour votre application][copy-git-repo-url]
6. <span data-ttu-id="f7134-172">GIT transfère le fichier WAR au référentiel en ligne.</span><span class="sxs-lookup"><span data-stu-id="f7134-172">Git push the WAR file to the online repository.</span></span> <span data-ttu-id="f7134-173">Pour ce faire, accédez au dossier **deploy** créé au préalable afin de pouvoir valider le code dans le référentiel en cours d’exécution de votre App Service.</span><span class="sxs-lookup"><span data-stu-id="f7134-173">To do this, navigate into the **deploy** folder you created earlier so that you can easily commit the code up to the repository running in your App Service.</span></span> <span data-ttu-id="f7134-174">Une fois que vous vous trouvez dans la fenêtre de console et que vous avez accédé au dossier contenant le dossier webapps, émettez les commandes Git qui suivent pour lancer le processus et déclencher un déploiement.</span><span class="sxs-lookup"><span data-stu-id="f7134-174">Once you're in the console window and navigated into the folder where the webapps folder is located, issue the following Git commands to launch the process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="f7134-175">Une fois que vous avez émis la requête **Push** , vous devez fournir le mot de passe que vous avez créé pour les informations d’identification précédemment.</span><span class="sxs-lookup"><span data-stu-id="f7134-175">Once you issue the **push** request, you'll be asked for the password you created for the deployment credential earlier.</span></span> <span data-ttu-id="f7134-176">Lorsque vous avez saisi vos informations d’identification, votre portail vous informe en principe que la mise à jour a été déployée.</span><span class="sxs-lookup"><span data-stu-id="f7134-176">After you enter your credentials, you should see your portal display that the update was deployed.</span></span>
7. <span data-ttu-id="f7134-177">Si vous utilisez une fois encore Postman pour atteindre l’application API qui vient d’être déployée dans Azure App Service, vous pourrez constater que le comportement est cohérent et que désormais, il retourne les coordonnées comme prévu et qu’il utilise des modifications simples du code Java de structure Swagger.io.</span><span class="sxs-lookup"><span data-stu-id="f7134-177">If you once again use Postman to hit the newly-deployed API App running in Azure App Service, you'll see that the behavior is consistent and that now it is returning contact data as expected, and using simple code changes to the Swagger.io scaffolded Java code.</span></span> 
   
    ![Utilisation de l’API REST de contacts de Java en direct dans Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="f7134-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f7134-179">Next steps</span></span>
<span data-ttu-id="f7134-180">Dans cet article, vous avez pu commencer avec un fichier Swagger JSON et un code avec structure Java obtenu à partir de l’éditeur Swagger.io.</span><span class="sxs-lookup"><span data-stu-id="f7134-180">In this article, you were able to start with a Swagger JSON file and some scaffolded Java code obtained from the Swagger.io editor.</span></span> <span data-ttu-id="f7134-181">À partir de là, quelques modifications simples et le processus de déploiement Git vous ont permis d’obtenir une application API fonctionnelle rédigée en Java.</span><span class="sxs-lookup"><span data-stu-id="f7134-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="f7134-182">Le didacticiel suivant montre comment [consommer des applications API à partir de clients JavaScript à l’aide de CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="f7134-182">The next tutorial shows how to [consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="f7134-183">Les didacticiels ultérieurs montrent comment implémenter l’authentification et l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="f7134-183">Later tutorials in the series show how to implement authentication and authorization.</span></span>

<span data-ttu-id="f7134-184">À partir de cet exemple, vous pouvez en apprendre davantage sur le [kit de développement logiciel de stockage pour Java] pour conserver les objets blob JSON.</span><span class="sxs-lookup"><span data-stu-id="f7134-184">To build on this sample, you can learn more about the [Storage SDK for Java] to persist the JSON blobs.</span></span> <span data-ttu-id="f7134-185">Vous pouvez également utiliser le [kit de développement logiciel Java Document DB] pour enregistrer vos données de contact pour la base de données de Document Azure.</span><span class="sxs-lookup"><span data-stu-id="f7134-185">Or, you could use the [Document DB Java SDK] to save your Contact data to Azure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="f7134-186">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f7134-186">See Also</span></span>
<span data-ttu-id="f7134-187">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Azure pour les développeurs Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="f7134-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[Portail Azure]: https://portal.azure.com/
[kit de développement logiciel Java Document DB]: ../documentdb/documentdb-java-application.md
[version d’évaluation gratuite]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Kit 8 de développeur Java]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Jax-RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[l’éditeur Swagger en ligne]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[kit de développement logiciel de stockage pour Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[l’éditeur Swagger]: http://editor.swagger.io/
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
