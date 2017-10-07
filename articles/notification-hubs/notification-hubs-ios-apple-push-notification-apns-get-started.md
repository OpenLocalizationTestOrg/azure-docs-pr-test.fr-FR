---
title: aaaSending tooiOS de notifications push avec Azure Notification Hubs | Documents Microsoft
description: "Dans ce didacticiel, vous découvrez comment toouse Azure Notification Hubs toosend push application iOS de tooan des notifications."
services: notification-hubs
documentationcenter: ios
keywords: notification push,notifications push,notifications push ios
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a>Envoi de tooiOS de notifications push avec Azure Notification Hubs
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).
> 
> 

Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push application iOS de tooan des notifications. Vous allez créer une application iOS vide qui reçoit des notifications push à l’aide de hello [les services de notifications Push Apple (APN)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html). 

Lorsque vous avez terminé, vous serez en mesure de toouse votre toobroadcast de concentrateur de notification push des appareils de hello notifications tooall votre application en cours d’exécution.

## <a name="before-you-begin"></a>Avant de commencer
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

le code Hello terminée pour ce didacticiel se trouve [sur GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted). 

## <a name="prerequisites"></a>Composants requis
Ce didacticiel requiert hello qui suit :

* [Services mobiles iOS SDK version 1.2.4]
* Version la plus récente de [Xcode]
* Un appareil compatible iOS 8 (ou version ultérieure)
* [programme pour développeurs Apple](https://developer.apple.com/programs/)
  
  > [!NOTE]
  > En raison de la configuration requise pour les notifications push, vous devez déployer et tester des notifications push sur un appareil physique iOS (iPhone ou iPad) au lieu de hello, iOS Simulator.
  > 
  > 

Vous devez terminer ce didacticiel avant de pouvoir suivre tous les autres didacticiels Notification Hubs pour les applications iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a>Configurer votre hub de notification pour les notifications Push iOS
Cette section présente la création d’un concentrateur de notification et de configuration de l’authentification avec APNS à l’aide de hello **.p12** : certificat push que vous avez créé. Si vous voulez toouse un concentrateur de notification que vous avez déjà créé, vous pouvez ignorer toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p>Cliquez sur hello <b>Notification Services</b> bouton Bonjour <b>paramètres</b> panneau, puis sélectionnez <b>Apple (APN)</b>. Cliquez sur <b>télécharger un certificat</b> et sélectionnez hello <b>.p12</b> que vous avez exporté précédemment. Assurez-vous que vous spécifiez également un mot de passe correct hello.</p>

<p>Assurez-vous que tooselect <b>Sandbox</b> mode car il s’agit pour le développement. Utilisez uniquement hello <b>Production</b> si vous souhaitez que toousers de notifications push toosend qui ont acheté votre application à partir du magasin de hello.</p>
</li>
</ol>
&emsp;&emsp;&emsp;&emsp;![Configurer APNS dans le portail Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)

&emsp;&emsp;&emsp;&emsp;![Configurer la certification APNS dans le portail Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

Votre concentrateur de notification est maintenant configuré toowork avec APNS, et vous avez tooregister de chaînes de connexion hello votre application et envoyez des notifications push.

## <a name="connect-your-ios-app-toonotification-hubs"></a>Se connecter à votre tooNotification d’application iOS concentrateurs
1. Dans Xcode, créez un projet iOS, puis sélectionnez hello **Application vue unique** modèle.
   
    ![Xcode - Application à vue unique][8]
    
2. Lors de la définition des options de hello pour votre nouveau projet, assurez-vous que toouse hello même **Product Name** et **identifiant d’organisation** que vous avez utilisé lorsque vous définissez précédemment des ID d’offre groupée hello sur hello Apple Developer portail.
   
    ![Xcode - options de projet][11]
    
3. Sous **cibles**, cliquez sur le nom de votre projet hello **paramètres de génération** onglet et développez **identité de signature de Code**, puis sous **déboguer**, définir votre identité de signature de code. Activer/désactiver **niveaux** de **base** trop**tous les**et définissez **profil de préparation** toohello configuration du profil que vous avez créé précédemment .
   
    Si vous ne voyez pas hello nouvelle configuration du profil que vous avez créé dans Xcode, essayez d’actualiser les profils hello pour votre identité de signature. Cliquez sur **Xcode** hello barre de menus, cliquez sur **préférences**, cliquez sur hello **compte** , cliquez sur hello **afficher les détails** , sur votre identité de signature, puis cliquez sur le bouton d’actualisation hello dans le coin inférieur droit de hello.
   
    ![Xcode - profil d’approvisionnement][9]
4. Télécharger hello [Services mobiles iOS SDK version 1.2.4] et décompressez les fichiers hello. Dans Xcode, avec le bouton droit de votre projet, puis cliquez sur hello **Ajout de fichiers à** hello de tooadd option **WindowsAzureMessaging.framework** projet Xcode de tooyour dossier. Sélectionnez **Copy items if needed**, puis cliquez sur **Add**.
   
   > [!NOTE]
   > concentrateurs de notification Hello SDK ne prend pas en charge bitcode sur Xcode 7.  Vous devez définir **Bitcode d’activer** trop**non** Bonjour **Options de Build** pour votre projet.
   > 
   > 
   
    ![Décompresser le SDK Azure][10]
5. Ajouter un en-tête fichier tooyour projet nommé `HubInfo.h`. Ce fichier conserve les constantes hello pour votre concentrateur de notification.  Ajouter hello suivant des définitions et de remplacer la réservation de littéral de chaîne hello avec votre *nom de hub* et hello *DefaultListenSharedAccessSignature* que vous avez notée précédemment.
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. Ouvrez votre `AppDelegate.h` fichier ajouter hello suit les directives d’importation :
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. Dans votre `AppDelegate.m file`, ajouter hello suivant code Bonjour `didFinishLaunchingWithOptions` méthode selon votre version d’iOS. Ce code enregistre le handle de votre appareil avec APNs :
   
    Pour iOS 8 :
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    Pour too8 de précédentes versions iOS :
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. Dans hello du même fichier, ajouter des méthodes suivantes de hello. Ce code connecte toohello hub de notification à l’aide des informations de connexion hello spécifié dans HubInfo.h. Il fournit ensuite une hub de notification de jeton toohello hello appareil afin que hello hub de notification peut envoyer des notifications :
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. Dans l’hello du même fichier, ajoutez hello suivant de méthode toodisplay un **UIAlert** si la notification de hello est reçue lors de l’application hello est active :

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. Générez et exécutez l’application hello sur votre tooverify appareil qu’il n’y a aucun échec.

## <a name="send-test-push-notifications"></a>Envoi de notifications Push de test
Vous pouvez tester la réception de notifications dans votre application en envoyant des notifications push dans hello [Azure Portal] via hello **dépannage** section dans le panneau de concentrateur hello (utilisez hello *d’envoiTest* option).

![Portail Azure - Test d’envoi][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a>(Facultatif) Envoyer des notifications push à partir de l’application hello
> [!IMPORTANT]
> Cet exemple montre comment envoyer des notifications à partir de l’application cliente de hello est fourni uniquement à des fins pédagogiques. Étant donné que vous devrez hello `DefaultFullSharedAccessSignature` toobe présent sur l’application cliente de hello, il expose les risques de toohello de concentrateur de notification qu’un utilisateur peut obtenir les notifications d’accès non autorisé de toosend tooyour clients.
> 
> 

Si vous souhaitez toosend notifications push au sein d’une application, cette section fournit un exemple de procédure toodo à l’aide de cette hello interface REST.

1. Dans Xcode, ouvrez `Main.storyboard` et ajoutez hello suivant des composants d’interface utilisateur à partir de hello objet bibliothèque tooallow hello utilisateur toosend des notifications push dans l’application hello :
   
   * Une étiquette sans texte d’étiquette. Il s’agit des erreurs tooreport utilisé lors de l’envoi des notifications. Hello **lignes** propriété doit être définie trop**0** afin qu’il se redimensionne automatiquement toohello la droite et les marges gauche et haut hello de vue de hello.
   * Un champ de texte avec **espace réservé** texte défini trop**entrer un Message de Notification**. Limiter le champ hello juste en dessous d’étiquette hello comme indiqué ci-dessous. Définissez hello View Controller que le délégué de sortie hello.
   * Un bouton intitulé **envoyer une Notification** contraint juste en dessous de champ de texte hello et dans le centre de horizontal hello.
     
     affichage de Hello doit se présenter comme suit :
     
     ![Concepteur Xcode][32]
2. [Ajoutez des prises de courant](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) de champ d’étiquette et le texte hello connectée à votre affichage et mettre à jour votre `interface` définition toosupport `UITextFieldDelegate` et `NSXMLParserDelegate`. Ajoutez les trois déclarations de propriété hello ci-dessous de prise en charge toohelp appelant hello API REST et analyse de la réponse de hello.
   
    Votre fichier ViewController.h doit se présenter comme suit :
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. Ouvrez `HubInfo.h` et ajoutez hello suivant des constantes qui seront utilisés pour l’envoi de hub de notifications tooyour. Remplacez le littéral de chaîne espace réservé hello avec votre véritable *DefaultFullSharedAccessSignature* chaîne de connexion.
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. Ajoutez hello suivant `#import` instructions tooyour `ViewController.h` fichier.
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. Dans `ViewController.m` ajouter hello après l’implémentation d’interface toohello code. Ce code analysera la chaîne de connexion *DefaultFullSharedAccessSignature* . Comme mentionné dans hello [référence d’API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), ces informations analysées seront toogenerate utilisé un jeton SAP pour hello **autorisation** en-tête de demande.
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. Dans `ViewController.m`, mise à jour hello `viewDidLoad` chaîne de connexion méthode tooparse hello lors de la charge de la vue de hello. Également ajouter des méthodes d’utilitaire hello, illustrés ci-dessous, l’implémentation d’interface toohello.  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. Dans `ViewController.m`, ajouter hello suivant code toohello interface implémentation toogenerate hello SaS jeton d’autorisation qui sera fournie dans hello **autorisation** en-tête, comme indiqué dans hello [API REST Référence](http://msdn.microsoft.com/library/azure/dn495627.aspx).
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. CTRL + glisser à partir de hello **envoyer une Notification** bouton trop`ViewController.m` tooadd une action nommée **SendNotificationMessage** pour hello **Touch bas** événement. Mettre à jour méthode hello suivant code toosend hello notification à l’aide des API REST de hello.
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. Dans `ViewController.m`, ajoutez hello suivant toosupport de méthode délégué fermeture clavier hello pour le champ de texte hello. CTRL + glisser à partir de hello texte champ toohello View Controller icône hello de concepteur tooset interface hello afficher contrôleur que le délégué de sortie hello.
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. Dans `ViewController.m`, ajouter suivant de hello déléguer réponse hello analyse de méthodes toosupport à l’aide de `NSXMLParser`.
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. Générez le projet de hello et vérifiez qu’il n’y a aucune erreur.

> [!NOTE]
> Si vous rencontrez une erreur de build dans Xcode7 sur la prise en charge bitcode, vous devez modifier hello **paramètres de génération** > **Bitcode activer (ENABLE_BITCODE)** trop**non** dans Xcode. Hello SDK de concentrateurs de Notification ne prend pas en charge bitcode. 
> 
> 

Vous pouvez trouver toutes les charges utiles de notifications possibles hello Bonjour Apple [Local et le Guide de programmation de Notification Push].

## <a name="checking-if-your-app-can-receive-push-notifications"></a>Vérifier si votre application peut recevoir des notifications Push
des notifications push tootest sur iOS, vous devez déployer le périphérique d’e/s physiques tooa hello application. Impossible d’envoyer des notifications de push Apple à l’aide de hello, iOS Simulator.

1. Exécutez l’application hello et vérifiez que l’inscription réussit, puis appuyez sur **OK**.
   
    ![Test d’inscription de notifications Push pour applications iOS][33]
2. Vous pouvez envoyer une notification push de test à partir de hello [Azure Portal], comme décrit ci-dessus. Si vous avez ajouté le code pour l’envoi de notifications push dans l’application hello, touchez tooenter de champ de texte hello à l’intérieur d’un message de notification. Appuyez sur hello **envoyer** bouton sur le clavier de hello ou hello **envoyer une Notification** bouton dans le message de notification hello vue toosend hello.
   
    ![Test d’envoi de notifications Push pour applications iOS][34]
3. Hello notifications sont envoyées tooall périphériques inscrit tooreceive notifications hello hello Hub de Notification particulier.
   
    ![Test de réception de notifications Push pour applications iOS][35]

## <a name="next-steps"></a>Étapes suivantes
Dans cet exemple simple, vous diffusées tooall de notifications push à vos appareils iOS inscrits. Nous vous suggérons de franchir une étape supplémentaire dans votre apprentissage que vous passez toohello [Azure Notification Hubs d’avertir les utilisateurs pour iOS avec le serveur principal .NET] didacticiel qui vous guidera dans la création d’un push de toosend principal des notifications à l’aide de balises. 

Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, vous pouvez également déplacer sur toohello [toosend utiliser Notification Hubs actualités] didacticiel. 

Pour obtenir des informations générales sur Notification Hubs, consultez [Recommandations relatives à Notification Hubs].

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[Services mobiles iOS SDK version 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Recommandations relatives à Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs d’avertir les utilisateurs pour iOS avec le serveur principal .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[toosend utiliser Notification Hubs actualités]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[Local et le Guide de programmation de Notification Push]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure Portal]: https://portal.azure.com
