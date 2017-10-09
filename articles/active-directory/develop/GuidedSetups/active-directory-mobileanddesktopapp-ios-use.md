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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="2ed62-103">Utilisez hello bibliothèque d’authentification Microsoft (MSAL) tooget un jeton pour hello Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="2ed62-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="2ed62-104">Ouvrez `ViewController.swift` et remplacez le code hello avec :</span><span class="sxs-lookup"><span data-stu-id="2ed62-104">Open `ViewController.swift` and replace hello code with:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="2ed62-105">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="2ed62-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="2ed62-106">Obtention d’un jeton d’utilisateur de manière interactive</span><span class="sxs-lookup"><span data-stu-id="2ed62-106">Getting a user token interactively</span></span>
<span data-ttu-id="2ed62-107">Appel hello `acquireToken` résultats de la méthode dans une fenêtre de navigateur invitant hello toosign utilisateur dans.</span><span class="sxs-lookup"><span data-stu-id="2ed62-107">Calling hello `acquireToken` method results in a browser window prompting hello user toosign in.</span></span> <span data-ttu-id="2ed62-108">Applications nécessitent généralement un utilisateur toosign interactivement Bonjour première dont ils ont besoin tooaccess une ressource protégée, ou lorsqu’un tooacquire silencieux un jeton échoue (par exemple hello mot de passe expiré).</span><span class="sxs-lookup"><span data-stu-id="2ed62-108">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="2ed62-109">Obtention d’un jeton d’utilisateur en mode silencieux</span><span class="sxs-lookup"><span data-stu-id="2ed62-109">Getting a user token silently</span></span>
<span data-ttu-id="2ed62-110">Hello `acquireTokenSilent` méthode gère l’acquisition de jeton et renouvellement sans intervention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2ed62-110">hello `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="2ed62-111">Après avoir `acquireToken` est exécuté pour hello première fois, `acquireTokenSilent` est hello méthode couramment utilisée tooobtain jetons utilisés tooaccess protégée des ressources pour les appels suivants - en tant qu’appels toorequest ou renouveler des jetons sont effectuées en mode silencieux.</span><span class="sxs-lookup"><span data-stu-id="2ed62-111">After `acquireToken` is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>

<span data-ttu-id="2ed62-112">Finalement, `acquireTokenSilent` échoue, par exemple hello utilisateur s’est déconnecté, ou a modifié son mot de passe sur un autre périphérique.</span><span class="sxs-lookup"><span data-stu-id="2ed62-112">Eventually, `acquireTokenSilent` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="2ed62-113">Lorsque MSAL détecte que hello peut être résolu en demandant une action interactive, il déclenche une `MSALErrorCode.interactionRequired` exception.</span><span class="sxs-lookup"><span data-stu-id="2ed62-113">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="2ed62-114">Votre application peut gérer cette exception de deux manières :</span><span class="sxs-lookup"><span data-stu-id="2ed62-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="2ed62-115">Effectuer un appel sur `acquireToken` immédiatement, ce qui aboutit à l’invite hello toosign utilisateur dans.</span><span class="sxs-lookup"><span data-stu-id="2ed62-115">Make a call against `acquireToken` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="2ed62-116">Ce modèle est généralement utilisé dans les applications en ligne où il n’existe aucun contenu hors connexion dans l’application hello hello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2ed62-116">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="2ed62-117">exemple d’application Hello généré par cet Assistant d’installation utilise ce modèle : vous pouvez voir dans hello d’action première fois que vous exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2ed62-117">hello sample application generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello application.</span></span> <span data-ttu-id="2ed62-118">Car aucun utilisateur n’a jamais n’utilisé l’application hello, `applicationContext.users().first` contient une valeur null et un ` MSALErrorCode.interactionRequired ` exception sera levée.</span><span class="sxs-lookup"><span data-stu-id="2ed62-118">Because no user ever used hello application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="2ed62-119">Hello code dans l’exemple hello puis handles hello exception en appelant `acquireToken` résultant d’inviter toosign d’utilisateur hello dans.</span><span class="sxs-lookup"><span data-stu-id="2ed62-119">hello code in hello sample then handles hello exception by calling `acquireToken` resulting in prompting hello user toosign in.</span></span>

2.  <span data-ttu-id="2ed62-120">Les applications peuvent également faire d’un utilisateur de toohello d’indication visuelle qui une connexion à interactive étant requise, hello utilisateur sélectionne toosign du moment opportun hello dans ou application hello peut réessayer `acquireTokenSilent` ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="2ed62-120">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="2ed62-121">Cela est généralement utilisé lorsque l’utilisateur de hello peut utiliser d’autres fonctionnalités de l’application hello sans dérangement - par exemple, il est contenu hors connexion disponible dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2ed62-121">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="2ed62-122">Dans ce cas, hello utilisateur peut décider quand ils veulent toosign dans la ressource de hello protégé tooaccess, ou toorefresh hello des informations obsolètes, ou votre application peut décider tooretry `acquireTokenSilent` lorsque le réseau est restauré après n’est pas disponible temporairement.</span><span class="sxs-lookup"><span data-stu-id="2ed62-122">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="2ed62-123">Appeler l’API Microsoft Graph hello à l’aide du jeton hello que simplement obtenu</span><span class="sxs-lookup"><span data-stu-id="2ed62-123">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="2ed62-124">Ajouter nouvelle méthode hello ci-dessous trop`ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="2ed62-124">Add hello new method below too`ViewController.swift`.</span></span> <span data-ttu-id="2ed62-125">Cette méthode est utilisée toomake un `GET` demande à l’aide de l’API Microsoft Graph hello un *en-tête d’autorisation HTTP*:</span><span class="sxs-lookup"><span data-stu-id="2ed62-125">This method is used toomake a `GET` request against hello Microsoft Graph API using an *HTTP Authorization header*:</span></span>

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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="2ed62-126">Envoi d’un appel REST à une API protégée</span><span class="sxs-lookup"><span data-stu-id="2ed62-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="2ed62-127">Dans cet exemple d’application, hello `getContentWithToken()` méthode est utilisée toomake HTTP `GET` demande par rapport à une ressource protégée qui requiert un appelant de contenu toohello hello jeton, puis de retourner.</span><span class="sxs-lookup"><span data-stu-id="2ed62-127">In this sample application, hello `getContentWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="2ed62-128">Cette méthode ajoute un jeton de hello acquis Bonjour *en-tête d’autorisation HTTP*.</span><span class="sxs-lookup"><span data-stu-id="2ed62-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="2ed62-129">Pour cet exemple, les ressources hello sont hello Microsoft Graph API *me* endpoint – qui affiche des informations de profil de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="2ed62-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="2ed62-130">Configurer la déconnexion</span><span class="sxs-lookup"><span data-stu-id="2ed62-130">Set up sign-out</span></span>

<span data-ttu-id="2ed62-131">Ajouter hello suivant de méthode trop`ViewController.swift` toosign utilisateur de hello :</span><span class="sxs-lookup"><span data-stu-id="2ed62-131">Add hello following method too`ViewController.swift` toosign out hello user:</span></span>

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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="2ed62-132">Plus d’informations sur la déconnexion</span><span class="sxs-lookup"><span data-stu-id="2ed62-132">More info on sign-out</span></span>

<span data-ttu-id="2ed62-133">Hello `signoutButton` méthode supprime hello utilisateur hello cache d’utilisateur MSAL-cela efficacement indique à MSAL tooforget hello actuel utilisateur pour une demande ultérieure de tooacquire un jeton réussira uniquement si elle est rendue toobe interactive.</span><span class="sxs-lookup"><span data-stu-id="2ed62-133">hello `signoutButton` method removes hello user from hello MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>

<span data-ttu-id="2ed62-134">Bien que l’application hello dans cet exemple prend en charge un seul utilisateur, MSAL prend en charge les scénarios où plusieurs comptes peuvent être signés à hello simultanément et obtenir un exemple est une application de messagerie où un utilisateur possède plusieurs comptes.</span><span class="sxs-lookup"><span data-stu-id="2ed62-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-hello-callback"></a><span data-ttu-id="2ed62-135">Enregistrer le rappel de hello</span><span class="sxs-lookup"><span data-stu-id="2ed62-135">Register hello callback</span></span>

<span data-ttu-id="2ed62-136">Une fois que hello utilisateur s’authentifie, browser de hello redirige hello utilisateur toohello précédent de l’application.</span><span class="sxs-lookup"><span data-stu-id="2ed62-136">Once hello user authenticates, hello browser redirects hello user back toohello application.</span></span> <span data-ttu-id="2ed62-137">Suivez les étapes de hello ci-dessous tooregister ce rappel :</span><span class="sxs-lookup"><span data-stu-id="2ed62-137">Follow hello steps below tooregister this callback:</span></span>

1.  <span data-ttu-id="2ed62-138">Ouvrez `AppDelegate.swift` et importez la bibliothèque MSAL :</span><span class="sxs-lookup"><span data-stu-id="2ed62-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="2ed62-139">Ajouter hello suivant de méthode tooyour <code>AppDelegate</code> toohandle rappels de classe :</span><span class="sxs-lookup"><span data-stu-id="2ed62-139">Add hello following method tooyour <code>AppDelegate</code> class toohandle callbacks:</span></span>
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

