---
title: "utilisateur actuel d’aaaRegister hello pour les notifications push à l’aide des API Web | Documents Microsoft"
description: "Découvrez comment toorequest enregistrement des notifications push dans une application iOS avec Azure Notification Hubs lors de l’inscription est effectuée par l’API Web ASP.NET."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f859feb436093e703d7e1db38354dd356fff8efe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a>Inscrire l’utilisateur actuel de hello pour les notifications push à l’aide d’ASP.NET
> [!div class="op_single_selector"]
> * [iOS](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Cette rubrique vous montre comment toorequest push avec Azure Notification Hubs l’enregistrement des notifications lorsque l’inscription est effectuée par l’API Web ASP.NET. Cette rubrique étend le didacticiel de hello [avertir les utilisateurs avec des concentrateurs de Notification]. Vous devez avoir déjà terminé étapes hello requis dans ce service mobile de didacticiel toocreate hello authentifié. Pour plus d’informations sur hello notifier le scénario d’utilisateurs, consultez [avertir les utilisateurs avec des concentrateurs de Notification].

## <a name="update-your-app"></a>Mise à jour de votre application
1. Dans votre MainStoryboard_iPhone.storyboard, ajoutez hello suivant des composants à partir de la bibliothèque d’objets hello :
   
   * **Étiquette**: « Émission tooUser avec Notification Hubs »
   * **Étiquette**: « InstallationId »
   * **Étiquette**: « Utilisateur »
   * **Zone de texte**: « Utilisateur »
   * **Étiquette**: « Mot de passe »
   * **Zone de texte**: « Mot de passe »
   * **Bouton**: « Connexion »
     
     À ce stade, votre plan conceptuel ressemble à hello suivantes :
     
      ![][0]
2. Dans l’éditeur de l’assistant hello, créer prises pour tous les contrôles hello commuté et les appeler, rejoignez des champs de texte hello hello View Controller (délégué) et créer un **Action** pour hello **connexion** bouton.
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. Créez une classe nommée **DeviceInfo**, et hello de copie suivante de code dans la section d’interface hello du fichier de hello DeviceInfo.h :
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. Copiez hello suivant de code dans la section d’implémentation hello du fichier de DeviceInfo.m hello :
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store hello install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. Dans PushToUserAppDelegate.h, ajoutez hello suivant singleton de la propriété :
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. Bonjour **didFinishLaunchingWithOptions** méthode dans PushToUserAppDelegate.m, ajoutez hello suivant de code :
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    Hello première ligne initialise hello **DeviceInfo** singleton. Bonjour deuxième ligne démarre hello l’inscription pour les notifications push, qui est déjà présente est vous avez déjà effectué hello [prise en main des concentrateurs de Notification] didacticiel.
7. Dans PushToUserAppDelegate.m, implémentez la méthode hello **didRegisterForRemoteNotificationsWithDeviceToken** dans votre AppDelegate et ajoutez hello suivant de code :
   
        self.deviceInfo.deviceToken = deviceToken;
   
    Définit le jeton de périphérique hello pour demande de hello.
   
   > [!NOTE]
   > À ce stade, il ne doit pas y avoir d’autre code dans cette méthode. Si vous disposez déjà d’un appel toohello **registerNativeWithDeviceToken** méthode qui a été ajouté lorsque vous avez effectué hello [prise en main des concentrateurs de Notification](/manage/services/notification-hubs/get-started-notification-hubs-ios/) (didacticiel), vous devez commentez ou supprimez qui appel.
   > 
   > 
8. Dans le fichier de PushToUserAppDelegate.m hello, ajoutez hello suivant de méthode de gestionnaire :
   
   * application (void) :(UIApplication *) application didReceiveRemoteNotification :(NSDictionary *) userInfo {NSLog (@ « % @ », userInfo) ;   UIAlertView * alerte = [[alloc UIAlertView] initWithTitle:@"Notification » message : [userInfo objectForKey:@"inAppMessage »] délégué : nil cancelButtonTitle : @ otherButtonTitles:nil de « OK », nil] ;   [afficher alerte] ; }
   
   Cette méthode affiche une alerte dans l’interface utilisateur de hello lorsque votre application reçoit des notifications pendant son exécution.
9. Ouvrez hello PushToUserViewController.m fichier et clavier de retour hello Bonjour suivant la mise en œuvre :
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. Bonjour **viewDidLoad** méthode hello PushToUserViewController.m fichier, initialiser étiquette d’ID d’installation Bonjour comme suit :
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. Ajoutez hello propriétés dans l’interface dans PushToUserViewController.m suivantes :
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. Ensuite, ajoutez hello suivant la mise en œuvre :
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. De code suivant de hello de copie dans hello **connexion** créé par XCode de méthode de gestionnaire :
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    Cette méthode obtient un ID d’installation et le canal pour les notifications push et l’envoie, en même temps que le type d’appareil hello, toohello authentifié méthode API Web qui crée une inscription dans les concentrateurs de Notification. Cette API Web a été définie dans le cadre du didacticiel [avertir les utilisateurs avec des concentrateurs de Notification].

Maintenant que hello application cliente a été mis à jour, retourner toohello [avertir les utilisateurs avec des concentrateurs de Notification] et mettre à jour des notifications de toosend hello service mobile à l’aide de concentrateurs de Notification.

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[avertir les utilisateurs avec des concentrateurs de Notification]: /manage/services/notification-hubs/notify-users-aspnet

[prise en main des concentrateurs de Notification]: /manage/services/notification-hubs/get-started-notification-hubs-ios
