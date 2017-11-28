---
title: "Bien démarrer avec Azure AD v2 avec les applications iOS - Utilisation | Microsoft Docs"
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
ms.openlocfilehash: 2ac1117a31a101705539a1f75520ce8de43809a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="210ca-103">Utiliser la bibliothèque d’authentification Microsoft (MSAL) afin d’obtenir un jeton pour l’API Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="210ca-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="210ca-104">Ouvrez `ViewController.swift` et remplacez le code par :</span><span class="sxs-lookup"><span data-stu-id="210ca-104">Open `ViewController.swift` and replace the code with:</span></span>

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

     // This button will invoke the call to the Microsoft Graph API. It uses the
     // built in Swift libraries to create a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check to see if we have a current logged in user. If we don't, then we need to sign someone in.
            // We throw an interactionRequired so that we trigger the interactive signin.
            
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
            
            // interactionRequired means we need to ask the user to sign-in. This usually happens
            // when the user's Refresh Token is expired or if the user has changed their password
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
            
            // This is the catch all error.
            
            self.loggingText.text = "Unable to acquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable to create Application Context. Error: \(error)"
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
### <a name="more-information"></a><span data-ttu-id="210ca-105">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="210ca-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="210ca-106">Obtention d’un jeton d’utilisateur de manière interactive</span><span class="sxs-lookup"><span data-stu-id="210ca-106">Getting a user token interactively</span></span>
<span data-ttu-id="210ca-107">L’appel de la méthode `acquireToken` affiche une fenêtre de navigateur invitant l’utilisateur à se connecter.</span><span class="sxs-lookup"><span data-stu-id="210ca-107">Calling the `acquireToken` method results in a browser window prompting the user to sign in.</span></span> <span data-ttu-id="210ca-108">En général, les applications obligent un utilisateur à se connecter de manière interactive la première fois qu’elles doivent accéder à une ressource protégée ou lorsqu’une opération silencieuse d’acquisition de jeton échoue (par exemple, en cas d’expiration du mot de passe de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="210ca-108">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="210ca-109">Obtention d’un jeton d’utilisateur en mode silencieux</span><span class="sxs-lookup"><span data-stu-id="210ca-109">Getting a user token silently</span></span>
<span data-ttu-id="210ca-110">La méthode `acquireTokenSilent` gère les acquisitions et renouvellements de jetons sans aucune interaction de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="210ca-110">The `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="210ca-111">Quand `acquireToken` est exécuté pour la première fois, c’est en général la méthode `acquireTokenSilent` qui est utilisée pour obtenir les jetons permettant d’accéder aux ressources protégées pour les appels suivants, ainsi que pour les demandes ou renouvellements de jetons en mode silencieux.</span><span class="sxs-lookup"><span data-stu-id="210ca-111">After `acquireToken` is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>

<span data-ttu-id="210ca-112">`acquireTokenSilent` finira par échouer, par exemple si l’utilisateur s’est déconnecté ou a modifié son mot de passe sur un autre appareil.</span><span class="sxs-lookup"><span data-stu-id="210ca-112">Eventually, `acquireTokenSilent` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="210ca-113">Quand la bibliothèque MSAL détecte que le problème peut être résolu par une intervention interactive, elle déclenche une exception `MSALErrorCode.interactionRequired`.</span><span class="sxs-lookup"><span data-stu-id="210ca-113">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="210ca-114">Votre application peut gérer cette exception de deux manières :</span><span class="sxs-lookup"><span data-stu-id="210ca-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="210ca-115">En adressant immédiatement un appel à `acquireToken`, suite à quoi l’utilisateur est invité à se connecter.</span><span class="sxs-lookup"><span data-stu-id="210ca-115">Make a call against `acquireToken` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="210ca-116">Cette méthode est généralement employée dans les applications en ligne où aucun contenu hors connexion dans l’application n’est disponible pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="210ca-116">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="210ca-117">L’exemple d’application généré par cet Assistant Installation utilise ce modèle : vous pouvez le voir en action la première fois que vous exécutez l’application.</span><span class="sxs-lookup"><span data-stu-id="210ca-117">The sample application generated by this guided setup uses this pattern: you can see it in action the first time you execute the application.</span></span> <span data-ttu-id="210ca-118">Aucun utilisateur n’ayant jamais utilisé l’application, `applicationContext.users().first` contient une valeur null et une exception ` MSALErrorCode.interactionRequired ` est levée.</span><span class="sxs-lookup"><span data-stu-id="210ca-118">Because no user ever used the application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="210ca-119">Le code de l’exemple gère ensuite cette exception en appelant `acquireToken`, suite à quoi l’utilisateur est invité à se connecter.</span><span class="sxs-lookup"><span data-stu-id="210ca-119">The code in the sample then handles the exception by calling `acquireToken` resulting in prompting the user to sign in.</span></span>

2.  <span data-ttu-id="210ca-120">Les applications peuvent également signaler à l’utilisateur qu’une connexion interactive est requise afin qu’il puisse choisir le bon moment pour se connecter ou que l’application puisse réessayer d’exécuter `acquireTokenSilent` ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="210ca-120">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="210ca-121">Cette solution est généralement retenue lorsque l’utilisateur peut utiliser d’autres fonctionnalités de l’application sans être perturbé, notamment lorsque du contenu hors connexion est disponible dans l’application.</span><span class="sxs-lookup"><span data-stu-id="210ca-121">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="210ca-122">Dans ce cas, l’utilisateur peut décider quand il souhaite se connecter pour accéder à la ressource protégée ou pour actualiser les informations obsolètes. Ou bien, votre application peut décider de réexécuter `acquireTokenSilent` après une indisponibilité temporaire du réseau.</span><span class="sxs-lookup"><span data-stu-id="210ca-122">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="210ca-123">Appeler l’API Microsoft Graph à l’aide du jeton que vous venez d’obtenir</span><span class="sxs-lookup"><span data-stu-id="210ca-123">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="210ca-124">Ajoutez la nouvelle méthode ci-dessous à `ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="210ca-124">Add the new method below to `ViewController.swift`.</span></span> <span data-ttu-id="210ca-125">Cette méthode permet d’envoyer une demande `GET` à l’API Microsoft Graph à l’aide d’un *en-tête d’autorisation HTTP* :</span><span class="sxs-lookup"><span data-stu-id="210ca-125">This method is used to make a `GET` request against the Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify the Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set the Authorization header for the request. We use Bearer tokens, so we specify Bearer + the token we got from the result
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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="210ca-126">Envoi d’un appel REST à une API protégée</span><span class="sxs-lookup"><span data-stu-id="210ca-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="210ca-127">Dans cet exemple d’application, la méthode `getContentWithToken()` est utilisée pour envoyer une demande HTTP `GET` à une ressource protégée qui requiert un jeton, puis pour renvoyer le contenu à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="210ca-127">In this sample application, the `getContentWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="210ca-128">Cette méthode ajoute le jeton acquis dans l’*en-tête d’autorisation HTTP*.</span><span class="sxs-lookup"><span data-stu-id="210ca-128">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="210ca-129">Dans cet exemple, la ressource est le point de terminaison *me* de l’API Microsoft Graph, qui affiche les informations de profil de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="210ca-129">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="210ca-130">Configurer la déconnexion</span><span class="sxs-lookup"><span data-stu-id="210ca-130">Set up sign-out</span></span>

<span data-ttu-id="210ca-131">Ajoutez la méthode suivante à `ViewController.swift` pour déconnecter l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="210ca-131">Add the following method to `ViewController.swift` to sign out the user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from the cache for this application for the provided user
        // first parameter:   The user to remove from the cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="210ca-132">Plus d’informations sur la déconnexion</span><span class="sxs-lookup"><span data-stu-id="210ca-132">More info on sign-out</span></span>

<span data-ttu-id="210ca-133">La méthode `signoutButton` ci-dessus supprime l’utilisateur du cache utilisateur de la bibliothèque MSAL. Cette opération indique à la bibliothèque MSAL qu’elle doit oublier l’utilisateur actuel afin que la demande suivante d’acquisition de jeton n’aboutisse que si elle est effectuée de manière interactive.</span><span class="sxs-lookup"><span data-stu-id="210ca-133">The `signoutButton` method removes the user from the MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>

<span data-ttu-id="210ca-134">Bien que l’application de cet exemple ne prenne en charge qu’un seul utilisateur, la bibliothèque MSAL autorise les scénarios où plusieurs comptes peuvent être connectés en même temps. C’est notamment le cas dans une application de messagerie où un utilisateur a plusieurs comptes.</span><span class="sxs-lookup"><span data-stu-id="210ca-134">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-the-callback"></a><span data-ttu-id="210ca-135">Inscrire le rappel</span><span class="sxs-lookup"><span data-stu-id="210ca-135">Register the callback</span></span>

<span data-ttu-id="210ca-136">Une fois que l’utilisateur s’est authentifié, le navigateur le redirige vers l’application.</span><span class="sxs-lookup"><span data-stu-id="210ca-136">Once the user authenticates, the browser redirects the user back to the application.</span></span> <span data-ttu-id="210ca-137">Suivez les étapes ci-dessous pour inscrire ce rappel :</span><span class="sxs-lookup"><span data-stu-id="210ca-137">Follow the steps below to register this callback:</span></span>

1.  <span data-ttu-id="210ca-138">Ouvrez `AppDelegate.swift` et importez la bibliothèque MSAL :</span><span class="sxs-lookup"><span data-stu-id="210ca-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="210ca-139">Ajoutez la méthode suivante à votre classe <code>AppDelegate</code> pour gérer les rappels :</span><span class="sxs-lookup"><span data-stu-id="210ca-139">Add the following method to your <code>AppDelegate</code> class to handle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if the URL matches the redirect URI for a pending AppAuth
// authorization request and if so, will look for the code in the response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

