---
title: aaaAzure AD v2 iOS route - utilisez | Documents Microsoft
description: "Cet article explique comment les applications iOS (Swift) peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 22e67850e2e0b14b6d68815d8f23e18ce2e878ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Utilisez hello bibliothèque d’authentification Microsoft (MSAL) tooget un jeton pour hello Microsoft Graph API

Ouvrez `ViewController.swift` et remplacez le code hello avec :

```swift
import UIKit
import MSAL

class ViewController: UIViewController, UITextFieldDelegate, URLSessionDelegate {
    
    let kClientID = "Your_Application_Id_Here"
    let kAuthority = "https://login.microsoftonline.com/common/v2.0"

    let kGraphURI = "https://graph.microsoft.com/v1.0/me/"
    let kScopes: [String] = ["https://graph.microsoft.com/user.read"]
    
    var accessToken = String()
    var applicationContext = MSALPublicClientApplication.init()

    @IBOutlet weak var loggingText: UITextView!
    @IBOutlet weak var signoutButton: UIButton!

     // This button will invoke hello call toohello Microsoft Graph API. It uses the
     // built in Swift libraries toocreate a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check toosee if we have a current logged in user. If we don't, then we need toosign someone in.
            // We throw an interactionRequired so that we trigger hello interactive signin.
            
            if  try self.applicationContext.users().isEmpty {
                throw NSError.init(domain: "MSALErrorDomain", code: MSALErrorCode.interactionRequired.rawValue, userInfo: nil)
            } else {
            
            // Acquire a token for an existing user silently
            
            try self.applicationContext.acquireTokenSilent(forScopes: self.kScopes, user: applicationContext.users().first) { (result, error) in
    
                    if error == nil {
                        self.accessToken = (result?.accessToken)!
                        self.loggingText.text = "Refreshing token silently)"
                        self.loggingText.text = "Refreshed Access token is \(self.accessToken)"
                        
                        self.signoutButton.isEnabled = true;
                        self.getContentWithToken()
    
                    } else {
                        self.loggingText.text = "Could not acquire token silently: \(error ?? "No error information" as! Error)"
    
                    }
                }
            }
        }  catch let error as NSError {
            
            // interactionRequired means we need tooask hello user toosign-in. This usually happens
            // when hello user's Refresh Token is expired or if hello user has changed their password
            // among other possible reasons.
            
            if error.code == MSALErrorCode.interactionRequired.rawValue {
                
                self.applicationContext.acquireToken(forScopes: self.kScopes) { (result, error) in
                        if error == nil {
                            self.accessToken = (result?.accessToken)!
                            self.loggingText.text = "Access token is \(self.accessToken)"
                            self.signoutButton.isEnabled = true;
                            self.getContentWithToken()
                            
                        } else  {
                            self.loggingText.text = "Could not acquire token: \(error ?? "No error information" as! Error)"
                        }
                }
                
            }
            
        } catch {
            
            // This is hello catch all error.
            
            self.loggingText.text = "Unable tooacquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable toocreate Application Context. Error: \(error)"
        }
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        
        if self.accessToken.isEmpty {
            signoutButton.isEnabled = false; 
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Informations complémentaires
#### <a name="getting-a-user-token-interactively"></a>Obtention d’un jeton d’utilisateur de manière interactive
Appel hello `acquireToken` résultats de la méthode dans une fenêtre de navigateur invitant hello toosign utilisateur dans. Applications nécessitent généralement un utilisateur toosign interactivement Bonjour première dont ils ont besoin tooaccess une ressource protégée, ou lorsqu’un tooacquire silencieux un jeton échoue (par exemple hello mot de passe expiré).

#### <a name="getting-a-user-token-silently"></a>Obtention d’un jeton d’utilisateur en mode silencieux
Hello `acquireTokenSilent` méthode gère l’acquisition de jeton et renouvellement sans intervention de l’utilisateur. Après avoir `acquireToken` est exécuté pour hello première fois, `acquireTokenSilent` est hello méthode couramment utilisée tooobtain jetons utilisés tooaccess protégée des ressources pour les appels suivants - en tant qu’appels toorequest ou renouveler des jetons sont effectuées en mode silencieux.

Finalement, `acquireTokenSilent` échoue, par exemple hello utilisateur s’est déconnecté, ou a modifié son mot de passe sur un autre périphérique. Lorsque MSAL détecte que hello peut être résolu en demandant une action interactive, il déclenche une `MSALErrorCode.interactionRequired` exception. Votre application peut gérer cette exception de deux manières :

1.  Effectuer un appel sur `acquireToken` immédiatement, ce qui aboutit à l’invite hello toosign utilisateur dans. Ce modèle est généralement utilisé dans les applications en ligne où il n’existe aucun contenu hors connexion dans l’application hello hello utilisateur. exemple d’application Hello généré par cet Assistant d’installation utilise ce modèle : vous pouvez voir dans hello d’action première fois que vous exécutez l’application hello. Car aucun utilisateur n’a jamais n’utilisé l’application hello, `applicationContext.users().first` contient une valeur null et un ` MSALErrorCode.interactionRequired ` exception sera levée. Hello code dans l’exemple hello puis handles hello exception en appelant `acquireToken` résultant d’inviter toosign d’utilisateur hello dans.

2.  Les applications peuvent également faire d’un utilisateur de toohello d’indication visuelle qui une connexion à interactive étant requise, hello utilisateur sélectionne toosign du moment opportun hello dans ou application hello peut réessayer `acquireTokenSilent` ultérieurement. Cela est généralement utilisé lorsque l’utilisateur de hello peut utiliser d’autres fonctionnalités de l’application hello sans dérangement - par exemple, il est contenu hors connexion disponible dans l’application hello. Dans ce cas, hello utilisateur peut décider quand ils veulent toosign dans la ressource de hello protégé tooaccess, ou toorefresh hello des informations obsolètes, ou votre application peut décider tooretry `acquireTokenSilent` lorsque le réseau est restauré après n’est pas disponible temporairement.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Appeler l’API Microsoft Graph hello à l’aide du jeton hello que simplement obtenu

Ajouter nouvelle méthode hello ci-dessous trop`ViewController.swift`. Cette méthode est utilisée toomake un `GET` demande à l’aide de l’API Microsoft Graph hello un *en-tête d’autorisation HTTP*:

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify hello Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set hello Authorization header for hello request. We use Bearer tokens, so we specify Bearer + hello token we got from hello result
    request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")
    let urlSession = URLSession(configuration: sessionConfig, delegate: self, delegateQueue: OperationQueue.main)
    
    urlSession.dataTask(with: request) { data, response, error in
        let result = try? JSONSerialization.jsonObject(with: data!, options: [])
                    if result != nil {
                
                self.loggingText.text = result.debugDescription
            }
        }.resume()
}
```

<!--start-collapse-->
### <a name="making-a-rest-call-against-a-protected-api"></a>Envoi d’un appel REST à une API protégée

Dans cet exemple d’application, hello `getContentWithToken()` méthode est utilisée toomake HTTP `GET` demande par rapport à une ressource protégée qui requiert un appelant de contenu toohello hello jeton, puis de retourner. Cette méthode ajoute un jeton de hello acquis Bonjour *en-tête d’autorisation HTTP*. Pour cet exemple, les ressources hello sont hello Microsoft Graph API *me* endpoint – qui affiche des informations de profil de l’utilisateur hello.
<!--end-collapse-->

## <a name="set-up-sign-out"></a>Configurer la déconnexion

Ajouter hello suivant de méthode trop`ViewController.swift` toosign utilisateur de hello :

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from hello cache for this application for hello provided user
        // first parameter:   hello user tooremove from hello cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a>Plus d’informations sur la déconnexion

Hello `signoutButton` méthode supprime hello utilisateur hello cache d’utilisateur MSAL-cela efficacement indique à MSAL tooforget hello actuel utilisateur pour une demande ultérieure de tooacquire un jeton réussira uniquement si elle est rendue toobe interactive.

Bien que l’application hello dans cet exemple prend en charge un seul utilisateur, MSAL prend en charge les scénarios où plusieurs comptes peuvent être signés à hello simultanément et obtenir un exemple est une application de messagerie où un utilisateur possède plusieurs comptes.
<!--end-collapse-->

## <a name="register-hello-callback"></a>Enregistrer le rappel de hello

Une fois que hello utilisateur s’authentifie, browser de hello redirige hello utilisateur toohello précédent de l’application. Suivez les étapes de hello ci-dessous tooregister ce rappel :

1.  Ouvrez `AppDelegate.swift` et importez la bibliothèque MSAL :

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Ajouter hello suivant de méthode tooyour <code>AppDelegate</code> toohandle rappels de classe :
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if hello URL matches hello redirect URI for a pending AppAuth
// authorization request and if so, will look for hello code in hello response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

