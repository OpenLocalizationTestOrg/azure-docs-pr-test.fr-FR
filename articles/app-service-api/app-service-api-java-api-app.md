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
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a>Créer et déployer une application API Java dans Azure App Service
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Ce didacticiel montre comment toocreate une application Java et le déployer à l’aide de tooAzure App Service API Apps [Git]. instructions Hello dans ce didacticiel peuvent être suivies sur n’importe quel système d’exploitation qui est capable d’exécuter Java. tout code Hello dans ce didacticiel est intégré à l’aide de [Maven]. [JAX-r] est utilisé toocreate hello Service RESTful et est généré en fonction hello [Swagger] spécification de métadonnées à l’aide de hello [éditeur de Swagger].

## <a name="prerequisites"></a>Composants requis
1. [Kit 8 de développeur Java]\( (ou version ultérieure)
2. [Maven] doit être installé sur votre ordinateur de développement
3. [Git] doit être installé sur votre ordinateur de développement
4. Un payant ou [version d’évaluation gratuite] abonnement trop[Microsoft Azure]
5. Une application de test HTTP comme [Postman]

## <a name="scaffold-hello-api-using-swaggerio"></a>API de hello scaffold à l’aide de Swagger.IO
À l’aide de l’éditeur en ligne hello swagger.io, vous pouvez entrer le code JSON de Swagger ou YAML représentant la structure hello de votre API. Une fois que la surface d’exposition de hello API conçue, vous pouvez exporter pour une variété de plateformes et infrastructures. Dans la section suivante de hello, code de hello structuré sera tooinclude modifié des fonctionnalités fictive. 

Cette démonstration commence avec un corps JSON de Swagger que vous allez coller dans l’éditeur swagger.io hello, qui sera ensuite être utilisé toogenerate code en se servant de JAX-RS tooaccess un point de terminaison d’API REST. Ensuite, vous allez modifier des données fictives hello structuré code tooreturn, en simulant une API REST basées sur un mécanisme de persistance des données.  

1. Copiez hello suivant du Presse-papiers tooyour de code JSON de Swagger :
   
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
2. Accédez toohello [en ligne de l’éditeur Swagger]. Une fois, cliquez sur hello **fichier -> Coller JSON** élément de menu.
   
    ![Élément de menu Coller JSON][paste-json]
3. Collez hello JSON Contacts liste API Swagger vous avez copiée précédemment. 
   
    ![Collage du code JSON dans Swagger][pasted-swagger]
4. Afficher les pages de documentation hello et résumé des API de rendu dans l’éditeur de hello. 
   
    ![Affichage des documents Swagger générés][view-swagger-generated-docs]
5. Sélectionnez hello **générer de serveur -> JAX-RS** code menu option tooscaffold hello côté serveur, vous allez modifier une implémentation fictive tooadd ultérieure. 
   
    ![Générer l’élément de menu de code][generate-code-menu-item]
   
    Une fois que le code de hello est généré, vous recevrez un toodownload de fichier ZIP. Ce fichier contient le code hello structuré par le Générateur de code hello Swagger et toutes à générer des scripts. Décompressez le répertoire de tooa hello bibliothèque entière sur votre station de travail de développement. 

## <a name="edit-hello-code-tooadd-api-implementation"></a>Modifier hello Code tooadd implémentation de l’API
Dans cette section, vous allez remplacer la mise en œuvre de hello Swagger du code généré par du côté serveur avec votre code personnalisé. nouveau code de Hello retournera un client d’appelant d’entités toohello ArrayList de Contact. 

1. Ouvrez hello *Contact.java* fichier de modèle, qui se trouve dans hello *gen/src/java/swagger/e/s/modèle* dossier, à l’aide de [Visual Studio Code] ou votre éditeur de texte. 
   
    ![Ouvrir le fichier de modèle de contact][open-contact-model-file]
2. Ajouter hello suivant constructeur dans hello **Contact** classe. 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. Ouvrez hello *ContactsApiServiceImpl.java* fichier d’implémentation de service, qui se trouve dans hello *src/main/java/e/s/swagger/api/impl* dossier, à l’aide de [Visual Studio Code]ou votre éditeur de texte.
   
    ![Ouvrir le fichier de code du service de contact][open-contact-service-code-file]
4. Remplacer le code hello dans le fichier de hello avec cette nouvelle tooadd de code un code de service toohello implémentation fictive. 
   
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
5. Ouvrez une invite de commandes et modifiez le répertoire toohello racine de votre application.
6. Exécutez hello suivant Maven commande toobuild hello code et l’exécuter à l’aide de hello serveur d’applications Jetty localement. 
   
        mvn package jetty:run
7. Vous devez voir fenêtre de commande hello refléter que Jetty a démarré votre code sur le port 8080. 
   
    ![Ouvrir le fichier de code du service de contact][run-jetty-war]
8. Utilisez [Postman] méthode toomake une API de « obtenir tous les contacts » demande toohello à http://localhost : 8080/api/contacts.
   
    ![Hello d’appels API de Contacts][calling-contacts-api]
9. Utilisez [Postman] toomake une API de « obtenir le contact spécifique » demande toohello méthode situé à http://localhost : 8080/api/contacts/2.
   
    ![Hello d’appels API de Contacts][calling-specific-contact-api]
10. Pour finir, créez le fichier WAR de Java (ARchive Web) de hello en exécutant hello commande Maven dans votre console suivante. 
    
         mvn package war:war
11. Une fois le fichier WAR hello est généré, il sera placé dans hello **cible** dossier. Naviguez jusqu’au hello **cible** dossier et renommer le fichier WAR hello trop**ROOT.war**. (Assurez-vous de mise en majuscules de hello correspond à ce format).
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. Enfin, exécutez hello suivant les commandes à partir du dossier racine hello de votre application de toocreate un **déployer** toodeploy hello WAR de dossier toouse tooAzure de fichiers. 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a>Publier hello tooAzure de sortie du Service d’applications
Dans cette section, que vous allez apprendre comment toocreate une application API à l’aide de hello portail Azure, préparer cette application API pour l’hébergement d’applications Java et déployer hello nouvellement créé WAR fichier tooAzure toorun du Service d’applications pour votre nouvelle application API. 

1. Créer une application API Bonjour [portail Azure], en cliquant sur hello **Nouveau -> Web + Mobile -> application API** élément de menu, en entrant les détails de votre application et puis en cliquant sur **créer**.
   
    ![Créer une nouvelle API App][create-api-app]
2. Une fois que votre application API a été créée, ouvrez votre application **paramètres** panneau, puis cliquez sur hello **paramètres de l’Application** élément de menu. Sélectionnez hello Java les plus récents à partir des options disponibles de hello, puis sélectionnez hello Tomcat plus récente à partir de hello **conteneur Web** menu, puis sur **enregistrer**.
   
    ![Configurer Java Bonjour Panneau de l’application API][set-up-java]
3. Cliquez sur hello **informations d’identification de déploiement** menu Paramètres d’élément et fournir un nom d’utilisateur et un mot de passe vous souhaitez toouse pour la publication des fichiers tooyour application API. 
   
    ![Définir les informations d’identification de déploiement][deployment-credentials]
4. Cliquez sur hello **source du déploiement** élément de menu Paramètres. Une fois, cliquez sur hello **choisir les sources de** bouton, sélectionnez hello **référentiel Git Local** option, puis cliquez sur **OK**. Cette opération crée un référentiel Git fonctionnant sous Azure et associé à votre application API. Chaque fois que vous validez code toohello *master* branche du référentiel Git, votre code sera publié dans votre instance d’application API en cours d’exécution dynamique. 
   
    ![Configurer un nouveau référentiel Git local][select-git-repo]
5. Copiez le Presse-papiers de tooyour d’hello nouveau référentiel Git URL. Conservez-la, car dans un instant, vous devrez l’utiliser. 
   
    ![Configurer un nouveau référentiel Git pour votre application][copy-git-repo-url]
6. GIT push hello WAR fichier toohello référentiel en ligne. toodo, naviguez jusqu’au hello **déployer** dossier que vous avez créé précédemment afin que vous puissiez valider facilement code hello référentiel toohello en cours d’exécution dans votre application de Service. Une fois vous êtes dans la fenêtre de console hello et accédé au dossier hello où se trouve, dossier de WebApp hello émettre hello suivant Git commandes toolaunch hello processus et déclencher un déploiement. 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    Une fois que vous exécutez hello **push** demande, vous serez invité à indiquer pour mot de passe hello vous avez créé des informations d’identification de déploiement hello. Après avoir entré vos informations d’identification, vous devez voir votre affichage portail qui hello mise à jour a été déployée.
7. Si vous utilisez une fois encore Postman toohit hello nouvellement déployé API application s’exécutant dans Azure App Service, vous verrez que le comportement de hello est cohérent et que maintenant il retourne des données de contacts comme prévu, et à l’aide des modifications de code simple toohello Swagger.io structuré code Java. 
   
    ![Utilisation de l’API REST de contacts de Java en direct dans Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous ont été en mesure de toostart avec un fichier JSON de Swagger et du code Java modèle généré automatiquement obtenu à partir de l’éditeur Swagger.io hello. À partir de là, quelques modifications simples et le processus de déploiement Git vous ont permis d’obtenir une application API fonctionnelle rédigée en Java. étape suivante du didacticiel Hello montre comment trop[consommer des applications API à partir de clients de JavaScript, à l’aide de CORS][App Service API CORS]. Des didacticiels ultérieurs dans hello série indiquent comment tooimplement authentification et autorisation.

toobuild sur cet exemple, vous pouvez en savoir plus sur hello [stockage SDK pour Java] objets BLOB de toopersist hello JSON. Vous pouvez également utiliser hello [Document DB Java SDK] toosave votre tooAzure de données de Contact Document de base de données. 

<a name="see-also"></a>

## <a name="see-also"></a>Voir aussi
Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Azure pour les développeurs Java](/java/azure).

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
